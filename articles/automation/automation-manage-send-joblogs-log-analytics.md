---
title: "aaaForward tooOMS dane zadanie usługi Automatyzacja Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób toosend stanu i runbook zadanie strumieni tooMicrosoft Operations Management Suite Log Analytics toodeliver dodatkowe szczegółowe dane i zarządzania."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a>Przekazuj strumienie zadania i stan zadania z automatyzacji tooLog Analytics (OMS)
Automatyzacja może wysyłać runbook zadania stanu i zadania strumienie tooyour programu Microsoft Operations Management Suite (OMS) obszar roboczy analizy dzienników.  Rejestruje zadania i strumieni zadania są widoczne w portalu Azure hello lub przy użyciu programu PowerShell, dla poszczególnych zadań, a to pozwala tooperform dochodzenia proste. Teraz przy użyciu analizy dzienników można:

* Uzyskiwanie wglądu w zadaniach automatyzacji
* Wyzwalacz poczty e-mail lub alertu oparte na stan zadania elementu runbook (na przykład nie powiodło się lub wstrzymane)
* Zapis zaawansowanych zapytań na strumienie zadania
* Korelowanie zadań na konta automatyzacji
* Wizualizuj historię zadania wraz z upływem czasu     

## <a name="prerequisites-and-deployment-considerations"></a>Wymagania wstępne i zagadnienia dotyczące wdrażania
toostart Wysyłanie Twojej automatyzacji w dziennikach tooLog Analytics, należy:

1. Witaj listopada 2016 lub nowszej wersji usługi [programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).
2. Obszar roboczy analizy dzienników. Aby uzyskać więcej informacji, zobacz [wprowadzenie do analizy dzienników](../log-analytics/log-analytics-get-started.md). 
3. Witaj ResourceId dla Twojego konta usługi Automatyzacja Azure

Witaj toofind ResourceId dla konta usługi Automatyzacja Azure i obszaru roboczego analizy dzienników, uruchom hello następującego środowiska PowerShell:

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

Jeśli masz wiele kont automatyzacji lub obszary robocze, w danych wyjściowych hello hello poprzedzających poleceń, Znajdź hello *nazwa* należy tooconfigure i skopiuj wartość hello *ResourceId*.

Jeśli potrzebujesz toofind hello *nazwa* Twojego konta automatyzacji w hello portalu Azure wybierz konto automatyzacji z hello **konto automatyzacji** bloku, a następnie wybierz **wszystkie ustawienia**.  Z hello **wszystkie ustawienia** bloku, w obszarze **ustawienia konta** wybierz **właściwości**.  W hello **właściwości** bloku, pamiętaj, te wartości.<br> ![Właściwości konta automatyzacji](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).

## <a name="set-up-integration-with-log-analytics"></a>Konfigurowanie integracji z analizy dzienników
1. Na komputerze, należy uruchomić **programu Windows PowerShell** z hello **Start** ekranu.  
2. Skopiuj i Wklej hello następującego środowiska PowerShell i edytować wartość hello hello `$workspaceId` i `$automationAccountId`.  Dla hello `-Environment` są prawidłowe wartości parametru, *AzureCloud* lub *AzureUSGovernment* w zależności od pracujesz w środowisku chmury hello.     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

Po uruchomieniu tego skryptu, zostanie wyświetlony w ciągu 10 minut nowe JobLogs lub JobStreams zapisywana rekordów w analizy dzienników.

toosee hello dzienniki, uruchom następujące zapytanie operacji wyszukiwania dziennika analizy dzienników hello:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="verify-configuration"></a>Weryfikowanie konfiguracji
tooconfirm, który wysyła Twoje konto usługi Automatyzacja w dziennikach tooyour obszaru roboczego analizy dzienników, sprawdź, czy diagnostyki są poprawnie ustawione na koncie automatyzacji hello przy użyciu hello następującego środowiska PowerShell:

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

W danych wyjściowych hello upewnij się, że:
+ W obszarze *dzienniki*, hello wartość *włączone* jest *wartość True*
+ Witaj wartość *WorkspaceId* ustawiono toohello ResourceId obszaru roboczego analizy dzienników


## <a name="log-analytics-records"></a>Rekordy usługi Log Analytics
Diagnostyka usługi Automatyzacja Azure tworzy dwa typy rekordów w analizy dzienników i są oznaczone jako **typu = AzureDiagnostics**.

### <a name="job-logs"></a>Rejestruje zadania
| Właściwość | Opis |
| --- | --- |
| TimeGenerated |Data i godzina, kiedy wykonać zadanie elementu runbook hello. |
| RunbookName_s |Nazwa Hello hello elementu runbook. |
| Caller_s |Kto zainicjował operację hello.  Możliwe wartości to adres e-mail lub system w przypadku zaplanowanych zadań. |
| Tenant_g | Identyfikator GUID, który identyfikuje hello dzierżawy hello wywołującego. |
| JobId_g |Identyfikator GUID jest hello identyfikator hello zadania elementu runbook. |
| Typ ResultType |Stan Hello hello zadanie elementu runbook.  Możliwe wartości:<br>— Uruchomione<br>— Zatrzymane<br>— Wstrzymane<br>— Nie powiodło się<br>-Ukończone |
| Kategoria | Klasyfikacja hello typu danych.  Do automatyzacji wartość hello jest JobLogs. |
| OperationName | Określa typ hello operacje wykonywane na platformie Azure.  Do automatyzacji wartość hello jest zadanie. |
| Zasób | Nazwa hello konta automatyzacji |
| SourceSystem | Jak analizy dzienników zbierane dane hello. Zawsze *Azure* diagnostyki Azure. |
| ResultDescription |Opisuje stan wyniku zadania elementu runbook hello.  Możliwe wartości:<br>— Zadanie jest uruchomione<br>— Zadanie nie powiodło się<br>— Zadanie zostało ukończone |
| CorrelationId |Identyfikator GUID jest hello identyfikator korelacji hello zadania elementu runbook. |
| Identyfikator zasobu |Określa identyfikator zasobu konto usługi Automatyzacja Azure hello hello elementu runbook. |
| SubscriptionId | Witaj subskrypcji platformy Azure identyfikatora (GUID) dla hello konta automatyzacji. |
| ResourceGroup | Nazwa grupy zasobów hello hello konta automatyzacji. |
| ResourceProvider | FIRMY MICROSOFT. AUTOMATYZACJA |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>Strumienie zadania
| Właściwość | Opis |
| --- | --- |
| TimeGenerated |Data i godzina, kiedy wykonać zadanie elementu runbook hello. |
| RunbookName_s |Nazwa Hello hello elementu runbook. |
| Caller_s |Kto zainicjował operację hello.  Możliwe wartości to adres e-mail lub system w przypadku zaplanowanych zadań. |
| StreamType_s |Typ Hello strumienia zadania. Możliwe wartości:<br>— Postęp<br>— Dane wyjściowe<br>— Ostrzeżenie<br>— Błąd<br>— Debugowanie<br>— Pełne |
| Tenant_g | Identyfikator GUID, który identyfikuje hello dzierżawy hello wywołującego. |
| JobId_g |Identyfikator GUID jest hello identyfikator hello zadania elementu runbook. |
| Typ ResultType |Stan Hello hello zadanie elementu runbook.  Możliwe wartości:<br>— W toku |
| Kategoria | Klasyfikacja hello typu danych.  Do automatyzacji wartość hello jest JobStreams. |
| OperationName | Określa typ hello operacje wykonywane na platformie Azure.  Do automatyzacji wartość hello jest zadanie. |
| Zasób | Nazwa hello konta automatyzacji |
| SourceSystem | Jak analizy dzienników zbierane dane hello. Zawsze *Azure* diagnostyki Azure. |
| ResultDescription |Obejmuje strumienia wyjściowego hello z hello elementu runbook. |
| CorrelationId |Identyfikator GUID jest hello identyfikator korelacji hello zadania elementu runbook. |
| Identyfikator zasobu |Określa identyfikator zasobu konto usługi Automatyzacja Azure hello hello elementu runbook. |
| SubscriptionId | Witaj subskrypcji platformy Azure identyfikatora (GUID) dla hello konta automatyzacji. |
| ResourceGroup | Nazwa grupy zasobów hello hello konta automatyzacji. |
| ResourceProvider | FIRMY MICROSOFT. AUTOMATYZACJA |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>Wyświetlanie automatyzacji loguje analizy dzienników
Teraz, gdy rozpoczęto wysyłanie tooLog dzienniki programu automatyzacji zadanie analizy, zobacz, co można zrobić za pomocą tych dzienników wewnątrz analizy dzienników.

toosee hello dzienniki, uruchom następujące zapytanie hello:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>Wyślij wiadomość e-mail, gdy zadanie elementu runbook nie powiodło się lub wstrzymuje
Jeden z naszych najwyższym odbiorcy zapyta dotyczy toosend możliwości hello adresu e-mail lub tekstu w przypadku wystąpienia problemów z zadanie elementu runbook.   

reguły toocreate alert, rozpoczyna się od utworzenia wyszukiwania dziennika elementu runbook hello rekordów zadań, które powinny wywoływać hello alert.  Kliknij przycisk hello **Alert** przycisk toocreate i skonfigurować hello reguły alertów.

1. Na stronie Przegląd analizy dziennika powitania kliknij **wyszukiwania dziennika**.
2. Utwórz kwerendę wyszukiwania dziennika dla alertu, wpisując powitania po wyszukiwania do pola zapytania hello: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` można także grupować według hello RunbookName przy użyciu:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`   

   Jeśli zdefiniowano dzienników z ponad jednego automatyzacji konto lub subskrypcja tooyour obszaru roboczego można grupować alerty subskrypcji i konto automatyzacji.  Nazwa konta automatyzacji mogą pochodzić z pola zasobów hello hello wyszukiwania JobLogs.  
3. tooopen hello **Dodaj regułę alertu** kliknij **alertu** u góry hello hello strony. Szczegółowe informacje o hello opcje tooconfigure hello alertu, zobacz [alertów w analizy dzienników](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-all-jobs-that-have-completed-with-errors"></a>Znajdź wszystkie zadania, które zostały ukończone z błędami
Ponadto tooalerting na awarie, można znaleźć po błąd niepowodujący zadanie elementu runbook. W takich przypadkach PowerShell tworzy strumień błędów, ale błędy niepowodujący hello nie spowodować toosuspend Twojego zadania lub się nie powieść.    

1. W obszarze roboczym analizy dzienników, kliknij przycisk **wyszukiwania dziennika**.
2. W polu zapytania hello wpisz `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` , a następnie kliknij przycisk **wyszukiwania**.

### <a name="view-job-streams-for-a-job"></a>Wyświetl zadania strumieni zadania
Podczas debugowania zadania, można również toolook do hello strumieni zadania.  Witaj następujące zapytanie Wyświetla wszystkich strumieni hello pojedynczego zadania z identyfikatorem GUID 2ebd22ea-e05e-4eb9 - 9d 76-d73cbd4356e0:   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a>Widok stanu zadania historycznych
Na koniec można toovisualize historię zadania wraz z upływem czasu.  Wraz z upływem czasu, można użyć tego toosearch zapytania hello stanu zadań.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> ![Wykres stanu zadania historycznych OMS](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>Podsumowanie
Wysyłając Twojej automatyzacji zadań stanu i strumień danych tooLog Analytics można uzyskać lepszy wgląd w stan hello automatyzacji zadań przez:
+ Konfigurowanie alertów toonotify należy po problemu
+ Przy użyciu niestandardowych widoków i toovisualize zapytań wyszukiwania z wyników elementu runbook, stan zadania elementu runbook i inne powiązane kluczowych wskaźników i metryki.  

Analiza dzienników zapewnia lepszą widoczność operacyjne tooyour automatyzacji zadań i może ułatwić adres zdarzenia szybciej.  

## <a name="next-steps"></a>Następne kroki
* Zobacz toolearn więcej informacji na temat sposobu tooconstruct różne zapytania i przejrzyj hello automatyzacji zadania dzienniki z analizy dzienników [Zaloguj wyszukiwania analizy dzienników](../log-analytics/log-analytics-log-searches.md)
* toounderstand toocreate i pobrać dane wyjściowe i komunikaty o błędach z elementami runbook, zobacz temat [elementu Runbook dane wyjściowe i komunikaty](automation-runbook-output-and-messages.md)
* więcej informacji o wykonanie elementu runbook, w jaki sposób toomonitor zadań i inne szczegółowe informacje techniczne, zobacz toolearn [śledzić zadania elementu runbook](automation-runbook-execution.md)
* toolearn więcej informacji na temat analizy dzienników OMS i źródeł zbierania danych, zobacz [Azure zbierania danych magazynu w omówieniu analizy dzienników](../log-analytics/log-analytics-azure-storage.md)
