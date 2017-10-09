---
title: "aaaForward tooOMS danych raportowania usługi Konfiguracja DSC automatyzacji Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób toosend żądanego stanu (DSC) Konfiguracja raportowania tooMicrosoft Operations Management Suite Log Analytics toodeliver dodatkowe wglądu w dane i zarządzania."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a>Przekazuj Konfiguracja DSC automatyzacji Azure raportowania tooOMS danych analizy dzienników

Automatyzacja może wysyłać węzła DSC stan tooyour danych analizy dzienników programu Microsoft Operations Management Suite (OMS) obszar roboczy.  
Stan zgodności jest widoczny w portalu Azure hello lub przy użyciu programu PowerShell, dla węzłów i dla poszczególnych zasobów DSC w konfiguracji węzła. Analiza dzienników można:

* Pobierz informacje o zgodności dla węzłów zarządzanych i pojedynczych zasobów
* Wyzwalanie poczty e-mail lub alertu na podstawie stanu zgodności
* Zapis zaawansowanych zapytań na węzłach zarządzanych
* Korelowanie stanu zgodności dla konta automatyzacji
* Wizualizuj historii zgodności węzła wraz z upływem czasu

## <a name="prerequisites"></a>Wymagania wstępne

toostart wysyłania z usługi Konfiguracja DSC automatyzacji raporty tooLog Analytics, należy:

* Witaj listopada 2016 lub nowszej wersji usługi [programu Azure PowerShell](/powershell/azure/overview) (v2.3.0).
* Konto usługi Azure Automation. Aby uzyskać więcej informacji, zobacz [wprowadzenie do korzystania z usługi Automatyzacja Azure](automation-offering-get-started.md)
* Obszar roboczy analizy dzienników z **Automatyzacja i kontrola** oferty usługi. Aby uzyskać więcej informacji, zobacz [wprowadzenie do analizy dzienników](../log-analytics/log-analytics-get-started.md).
* Co najmniej jeden węzeł Konfiguracja DSC automatyzacji Azure. Aby uzyskać więcej informacji, zobacz [dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md) 

## <a name="set-up-integration-with-log-analytics"></a>Konfigurowanie integracji z analizy dzienników

toobegin importowanie danych z usługi Konfiguracja DSC automatyzacji Azure do analizy dzienników, pełną hello następujące kroki:

1. Zaloguj się za tooyour konto platformy Azure w programie PowerShell. Zobacz [Zaloguj się przy użyciu programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0)
1. Pobierz hello _ResourceId_ Twojego konta automatyzacji, uruchamiając następujące polecenia programu PowerShell hello: (Jeśli masz więcej niż jedno konto automatyzacji, wybierz hello _ResourceID_ dla konta hello tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. Pobierz hello _ResourceId_ obszaru roboczego analizy dzienników, uruchamiając następujące polecenia programu PowerShell hello: (Jeśli masz więcej niż jednego obszaru roboczego wybierz hello _ResourceID_ dla obszaru roboczego hello ma tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. Witaj uruchom następujące polecenia programu PowerShell, zastępując `<AutomationResourceId>` i `<WorkspaceResourceId>` z hello _ResourceId_ wartości z każdej z poprzednich kroków hello:

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

Importowanie danych z usługi Konfiguracja DSC automatyzacji Azure do analizy dzienników toostop, uruchomić hello następującego polecenia programu PowerShell.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a>Wyświetl dzienniki hello DSC

Po skonfigurowaniu integracji z analizy dzienników dla danych usługi Konfiguracja DSC automatyzacji **wyszukiwania dziennika** na powitania pojawi się przycisk **węzłów DSC** bloku Twoje konto usługi Automatyzacja. Kliknij przycisk hello **wyszukiwania dziennika** przycisk tooview hello dzienniki danych węzła DSC.

![Przycisk wyszukiwania dziennika](media/automation-dsc-diagnostics/log-search-button.png)

Witaj **wyszukiwania dziennika** zostanie otwarty blok i widzisz **DscNodeStatusData** operacji dla każdego węzła DSC i **DscResourceStatusData** operacja dla każdej [DSC zasób](https://msdn.microsoft.com/powershell/dsc/resources) wywołana w węźle zastosowane toothat konfiguracji węzła hello.

Witaj **DscResourceStatusData** operacja zawiera informacje o błędzie dla wszystkich zasobów DSC, których nie powiodła się.

Kliknij przycisk każdej operacji w hello listy toosee hello danych dla tej operacji.

Można również wyświetlić dzienniki hello wyszukując [w module analiz dziennika. Zobacz [wyszukiwanie danych przy użyciu dziennika wyszukiwania](../log-analytics/log-analytics-log-searches.md).
Typ hello następujące zapytanie toofind Twojego DSC dzienników:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`

Można również ograniczyć hello zapytania według nazwy operacji hello. Na przykład: "typ = AzureDiagnostics ResourceProvider ="MICROSOFT. Kategoria AUTOMATYZACJI"="DscNodeStatus"OperationName ="DscNodeStatusData"

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a>Wyślij wiadomość e-mail w przypadku niepowodzenia sprawdzania zgodności DSC

Jeden z naszych żądań najwyższym odbiorcy jest toosend możliwości hello adresu e-mail lub tekstu w przypadku wystąpienia problemów z konfiguracją usługi Konfiguracja DSC.   

Reguła alertu, Rozpocznij od utworzenia dziennika wyszukiwanie rekordów raportu DSC hello, które powinny wywoływać hello alert toocreate.  Kliknij przycisk hello **Alert** przycisk toocreate i skonfigurować hello reguły alertów.

1. Na stronie Przegląd analizy dziennika powitania kliknij **wyszukiwania dziennika**.
1. Utwórz kwerendę wyszukiwania dziennika dla alertu, wpisując powitania po wyszukiwania do pola zapytania hello:`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`

  Jeśli zdefiniowano dzienników z ponad jednego automatyzacji konto lub subskrypcja tooyour obszaru roboczego można grupować alerty subskrypcji i konto automatyzacji.  
  Nazwa konta automatyzacji mogą pochodzić z pola zasobów hello hello wyszukiwania DscNodeStatusData.  
1. tooopen hello **Dodaj regułę alertu** kliknij **alertu** u góry hello hello strony. Aby uzyskać więcej informacji na powitania opcje tooconfigure hello alert, zobacz [alertów w analizy dzienników](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-failed-dsc-resources-across-all-nodes"></a>Znajdź zasoby DSC nie powiodło się we wszystkich węzłach

Jedną z zalet przy użyciu analizy dzienników jest, że można wyszukiwać sprawdzenie nie powiodło się w węzłach.
toofind wszystkich wystąpień usługi Konfiguracja DSC zasobów, których nie powiodła się.

1. Na stronie Przegląd analizy dziennika powitania kliknij **wyszukiwania dziennika**.
1. Utwórz kwerendę wyszukiwania dziennika dla alertu, wpisując powitania po wyszukiwania do pola zapytania hello:`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`

### <a name="view-historical-dsc-node-status"></a>Wyświetl historyczne stan węzła DSC

Na koniec można toovisualize historii stanu węzła DSC wraz z upływem czasu.  
Wraz z upływem czasu, można użyć toosearch tej kwerendy stanu hello statusu węzła DSC.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

Spowoduje to wyświetlenie wykres stanu węzła hello wraz z upływem czasu.

## <a name="log-analytics-records"></a>Rekordy usługi Log Analytics

Diagnostyka usługi Automatyzacja Azure tworzy dwie kategorie rekordów w analizy dzienników.

### <a name="dscnodestatusdata"></a>DscNodeStatusData

| Właściwość | Opis |
| --- | --- |
| TimeGenerated |Data i godzina, gdy uruchomiono hello sprawdzania zgodności. |
| OperationName |DscNodeStatusData |
| Typ ResultType |Określa, czy węzeł hello jest zgodne. |
| NodeName_s |Nazwa Hello hello węzła zarządzanego. |
| NodeComplianceStatus_s |Określa, czy węzeł hello jest zgodne. |
| DscReportStatus |Określa, czy sprawdzanie zgodności hello zostało wykonane pomyślnie. |
| ConfigurationMode | Sposób konfiguracji hello jest węzłem toohello zastosowane. Możliwe wartości to __"ApplyOnly"__,__"ApplyandMonitior"__, i __"ApplyandAutoCorrect"__. <ul><li>__ApplyOnly__: DSC stosuje hello konfiguracji i nie działają dalsze, chyba że nową konfigurację spoczywa węzeł docelowy toohello lub gdy nowej konfiguracji są pobierane z serwera. Po początkowej stosowania nowej konfiguracji DSC nie sprawdza odejście od stanu wcześniej skonfigurowany. DSC tooapply hello konfiguracji prób, dopóki nie zostanie pomyślnie przed __ApplyOnly__ obowiązuje. </li><li> __ApplyAndMonitor__: jest to wartość domyślna hello. Witaj LCM stosuje wszelkie nowe konfiguracje. Po początkowej stosowania nowej konfiguracji Jeśli węzeł docelowy hello drifts ze stanu hello potrzeby DSC raporty niezgodności hello w dziennikach. DSC tooapply hello konfiguracji prób, dopóki nie zostanie pomyślnie przed __ApplyAndMonitor__ obowiązuje.</li><li>__ApplyAndAutoCorrect__: DSC stosuje wszelkie nowe konfiguracje. Po początkowej stosowania nowej konfiguracji Jeśli węzeł docelowy hello drifts ze stanu hello potrzeby DSC raporty niezgodności hello w dziennikach i ponowne zastosowanie hello bieżącej konfiguracji.</li></ul> |
| HostName_s | Nazwa Hello hello węzła zarządzanego. |
| Adres IP | adres IPv4 Hello hello zarządzane węzła. |
| Kategoria | DscNodeStatus |
| Zasób | Nazwa Hello hello konto usługi Automatyzacja Azure. |
| Tenant_g | Identyfikator GUID, który identyfikuje hello dzierżawy hello wywołującego. |
| NodeId_g |Identyfikator GUID, który identyfikuje hello węzła zarządzanego. |
| DscReportId_g |Identyfikator GUID, który identyfikuje hello raportu. |
| LastSeenTime_t |Data i godzina, kiedy ostatnio były wyświetlane hello raportu. |
| ReportStartTime_t |Data i godzina uruchomienia hello raportu. |
| ReportEndTime_t |Data i godzina zakończenia hello raportu. |
| NumberOfResources_d |w węźle toohello zastosowano konfigurację hello o nazwie Hello liczba zasobów usługi Konfiguracja DSC. |
| SourceSystem | Jak analizy dzienników zbierane dane hello. Zawsze *Azure* diagnostyki Azure. |
| Identyfikator zasobu |Określa konto usługi Automatyzacja Azure hello. |
| ResultDescription | Witaj opis dla tej operacji. |
| SubscriptionId | Witaj subskrypcji platformy Azure identyfikatora (GUID) dla hello konta automatyzacji. |
| ResourceGroup | Nazwa grupy zasobów hello hello konta automatyzacji. |
| ResourceProvider | FIRMY MICROSOFT. AUTOMATYZACJA |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |Identyfikator GUID jest hello identyfikator korelacji hello raportu zgodności. |

### <a name="dscresourcestatusdata"></a>DscResourceStatusData

| Właściwość | Opis |
| --- | --- |
| TimeGenerated |Data i godzina, gdy uruchomiono hello sprawdzania zgodności. |
| OperationName |DscResourceStatusData|
| Typ ResultType |Określa, czy zasób hello jest zgodne. |
| NodeName_s |Nazwa Hello hello węzła zarządzanego. |
| Kategoria | DscNodeStatus |
| Zasób | Nazwa Hello hello konto usługi Automatyzacja Azure. |
| Tenant_g | Identyfikator GUID, który identyfikuje hello dzierżawy hello wywołującego. |
| NodeId_g |Identyfikator GUID, który identyfikuje hello węzła zarządzanego. |
| DscReportId_g |Identyfikator GUID, który identyfikuje hello raportu. |
| DscResourceId_s |Witaj nazwa wystąpienia zasobu hello DSC. |
| DscResourceName_s |Nazwa Hello hello DSC zasobu. |
| DscResourceStatus_s |Określa, czy hello zasobów DSC jest zgodne. |
| DscModuleName_s |Nazwa Hello hello moduł programu PowerShell, który zawiera hello DSC zasobów. |
| DscModuleVersion_s |Wersja Hello hello moduł programu PowerShell, który zawiera hello DSC zasobów. |
| DscConfigurationName_s |Nazwa Hello konfiguracji hello stosowane toohello węzła. |
| ErrorCode_s | Kod błędu Hello Jeśli hello zasobów nie powiodła się. |
| ErrorMessage_s |Witaj komunikat o błędzie Jeśli hello zasobów nie powiodła się. |
| DscResourceDuration_d |Witaj czas w sekundach, którzy uruchomili hello DSC zasobów. |
| SourceSystem | Jak analizy dzienników zbierane dane hello. Zawsze *Azure* diagnostyki Azure. |
| Identyfikator zasobu |Określa konto usługi Automatyzacja Azure hello. |
| ResultDescription | Witaj opis dla tej operacji. |
| SubscriptionId | Witaj subskrypcji platformy Azure identyfikatora (GUID) dla hello konta automatyzacji. |
| ResourceGroup | Nazwa grupy zasobów hello hello konta automatyzacji. |
| ResourceProvider | FIRMY MICROSOFT. AUTOMATYZACJA |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |Identyfikator GUID jest hello identyfikator korelacji hello raportu zgodności. |

## <a name="summary"></a>Podsumowanie

Wysyłając tooLog danych z usługi Konfiguracja DSC automatyzacji Analytics można uzyskać lepszy wgląd w stan hello węzły DSC automatyzacji przez:

* Konfigurowanie alertów toonotify należy po problemu
* Przy użyciu niestandardowych widoków i toovisualize zapytań wyszukiwania z wyników elementu runbook, stan zadania elementu runbook i inne powiązane kluczowych wskaźników i metryki.  

Analiza dzienników zapewnia większą widoczność operacyjne tooyour usługi Konfiguracja DSC automatyzacji dane i może ułatwić szybciej adres zdarzenia.  

## <a name="next-steps"></a>Następne kroki

* Zobacz więcej informacji na temat sposobu tooconstruct różne zapytania i przejrzyj hello usługi Konfiguracja DSC automatyzacji dzienniki z analizy dzienników toolearn [Zaloguj wyszukiwania analizy dzienników](../log-analytics/log-analytics-log-searches.md)
* toolearn więcej informacji na temat przy użyciu usługi Konfiguracja DSC automatyzacji Azure, zobacz [wprowadzenie do korzystania z usługi Konfiguracja DSC automatyzacji Azure](automation-dsc-getting-started.md)
* toolearn więcej informacji na temat analizy dzienników OMS i źródeł zbierania danych, zobacz [Azure zbierania danych magazynu w omówieniu analizy dzienników](../log-analytics/log-analytics-azure-storage.md)

