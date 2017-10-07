---
title: "aaaCollecting analizy dzienników danych do elementu runbook automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Samouczek krok po kroku, który przedstawiono tworzenie elementu runbook w automatyzacji Azure toocollect danych do repozytorium OMS hello do analizy przez analizy dzienników."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a>Zbieranie danych w analizy dzienników z elementu runbook usługi Automatyzacja Azure
Można zbierać znaczną ilość danych analizy dzienników z różnych źródeł w tym [źródeł danych](../log-analytics/log-analytics-data-sources.md) na agentach, a także [dane zbierane z platformy Azure](../log-analytics/log-analytics-azure-storage.md).  Chociaż wymagających toocollect danych, która nie jest dostępny za pośrednictwem tych źródeł standardowe są scenariusze.  W takich przypadkach można użyć hello [interfejsu API modułów zbierających dane HTTP](../log-analytics/log-analytics-data-collector-api.md) toowrite danych tooLog Analytics za pomocą dowolnego klienta interfejsu API REST.  Typowe tooperform metody tej kolekcji danych używa elementu runbook automatyzacji Azure.   

Ten samouczek przeprowadzi Cię przez proces hello tworzenie i Planowanie elementu runbook w automatyzacji Azure toowrite danych tooLog Analytics.


## <a name="prerequisites"></a>Wymagania wstępne
Ten scenariusz wymaga hello następujące zasoby skonfigurowane w ramach subskrypcji platformy Azure.  Jednocześnie może być bezpłatne konto.

- [Obszar roboczy analizy dziennika](../log-analytics/log-analytics-get-started.md).
- [Konto usługi Automatyzacja Azure](../automation/automation-offering-get-started.md).

## <a name="overview-of-scenario"></a>Omówienie scenariusza
W tym samouczku przedstawiono tworzenie elementu runbook, który służy do zbierania informacji o automatyzacji zadań.  Elementy Runbook automatyzacji Azure są implementowane przy użyciu programu PowerShell, więc będzie rozpoczyna się od pisania i testowania skrypt w edytorze usługi Automatyzacja Azure hello.  Po zweryfikowaniu zbierasz hello wymagane informacje, będzie zapisu tego tooLog danych Analytics i sprawdź hello niestandardowego typu danych.  Na koniec zostanie utworzony element runbook hello toostart harmonogramu w regularnych odstępach czasu.

> [!NOTE]
> Można skonfigurować usługi Automatyzacja Azure toosend zadania informacji tooLog Analytics bez tego elementu runbook.  Ten scenariusz jest głównie używane toosupport hello samouczek i zaleca się wysłanie hello danych tooa testu z obszaru roboczego.  


## <a name="1-install-data-collector-api-module"></a>1. Zainstaluj moduł interfejsu API modułów zbierających dane
Każdy [żądania z interfejsu API modułów zbierających dane HTTP hello](../log-analytics/log-analytics-data-collector-api.md#create-a-request) musi być prawidłowo sformatowany i Dołącz nagłówek autoryzacji.  Można to zrobić w elemencie runbook, ale może zmniejszyć ilość hello kod wymagany przy użyciu modułu, który ułatwia ten proces.  Jest jeden moduł, którego można używać [modułu OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI) w hello galerii programu PowerShell.

toouse [modułu](../automation/automation-integration-modules.md) w elemencie runbook, musi być zainstalowany na Twoim koncie automatyzacji.  Funkcje w hello module hello dowolnym elemencie runbook w hello można używać tego samego konta.  Można zainstalować nowy moduł, wybierając **zasoby** > **modułów** > **dodać moduł** na Twoim koncie automatyzacji.  

Hello galerii programu PowerShell jednak daje toodeploy opcja szybkiego modułu bezpośrednio konta automatyzacji tooyour dzięki tej opcji można użyć w tym samouczku.  

![Moduł OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. Przejdź za[galerii programu PowerShell](https://www.powershellgallery.com/).
2. Wyszukaj **OMSIngestionAPI**.
3. Polecenie hello **tooAzure automatyzacji wdrażania** przycisku.
4. Wybierz konto automatyzacji, a następnie kliknij przycisk **OK** tooinstall hello modułu.


## <a name="2-create-automation-variables"></a>2. Utwórz zmienne automatyzacji
[Zmienne automatyzacji](..\automation\automation-variables.md) przechowywania wartości, które mogą być używane przez wszystkie elementy runbook na Twoim koncie automatyzacji.  Tworzenia elementów runbook więcej elastyczne, umożliwiając toochange te wartości bez konieczności edytowania hello rzeczywistego elementu runbook. Każde żądanie z hello interfejsu API modułów zbierających dane HTTP wymaga hello identyfikator i klucz obszaru roboczego OMS hello i zmiennej zasoby są idealne toostore te informacje.  

![Zmienne](media/operations-management-suite-runbook-datacollect/variables.png)

1. W hello portalu Azure Przejdź tooyour konta automatyzacji.
2. Wybierz **zmienne** w obszarze **zasobów udostępnionych**.
2. Kliknij przycisk **dodać zmienną** i Utwórz dwie zmienne hello w hello w poniższej tabeli.

| Właściwość | Wartość Identyfikatora obszaru roboczego | Wartość klucza obszaru roboczego |
|:--|:--|:--|
| Nazwa | WorkspaceId | WorkspaceKey |
| Typ | Ciąg | Ciąg |
| Wartość | Wklej hello identyfikator obszaru roboczego z obszaru roboczego analizy dzienników. | Wklej się przy użyciu hello podstawowej lub dodatkowej klucz obszaru roboczego analizy dzienników. |
| Zaszyfrowane | Nie | Tak |



## <a name="3-create-runbook"></a>3. Tworzenie elementu runbook

W portalu hello, w którym można edytować i przetestuj element runbook usługi Automatyzacja Azure występuje edytora.  Masz hello opcja toouse hello skryptu Edytor toowork z [PowerShell bezpośrednio](../automation/automation-edit-textual-runbook.md) lub [utworzyć graficzny element runbook](../automation/automation-graphical-authoring-intro.md).  W tym samouczku będzie działać z skrypt programu PowerShell. 

![Edytowanie elementu Runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. Przejdź tooyour konta automatyzacji.  
2. Kliknij przycisk **Runbook** > **Dodaj element runbook** > **Utwórz nowy element runbook**.
3. Nazwa elementu runbook hello, wpisz **zbieranie automatyzacji zadania**.  Typ elementu runbook hello wybierz **PowerShell**.
4. Kliknij przycisk **Utwórz** toocreate hello elementu runbook, a następnie rozpocznij hello edytora.
5. Skopiuj i Wklej powitania po kodu na powitania elementu runbook.  Można znaleźć toohello komentarzy w skrypcie hello opis hello kodu.
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a>4. Testowego elementu runbook
Automatyzacja Azure zawiera środowisko zbyt[przetestuj element runbook](../automation/automation-testing-runbook.md) przed opublikowaniem.  Można sprawdzić hello danych zbieranych przez element runbook hello i sprawdź, czy zapisuje tooLog Analytics zgodnie z oczekiwaniami przed jej opublikowaniem tooproduction. 
 
![Testowego elementu runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. Kliknij przycisk **zapisać** toosave hello runbook.
1. Kliknij przycisk **okienku testu** tooopen hello runbook w środowisku testowym hello.
3. Ponieważ element runbook ma parametry, możesz tooenter zostanie wyświetlony monit o wartości dla nich.  Wprowadź nazwę grupy zasobów hello hello i automatyzacji hello konta użytkownika będzie toocollect informacje o zadaniu z.
4. Kliknij przycisk **Start** toohello uruchomić hello elementu runbook.
3. Hello runbook rozpocznie się ze stanem **w kolejce** przed przechodzi ona zbyt**systemem**.  
3. Hello runbook powinien być wyświetlany pełne dane wyjściowe z zadania hello zbierane w formacie json.  Jeśli nie są wyświetlane żadne zadania, następnie mogły wystąpić żadne zadania utworzone na koncie automatyzacji hello w hello ostatniej godziny.  Spróbuj uruchomić przy użyciu konta automatyzacji hello dowolnym elemencie runbook, a następnie wykonaj ponownie hello testu.
4. Upewnij się, że hello dane wyjściowe nie wyświetla się, że wszelkie błędy hello post tooLog polecenia Analytics.  Powinien mieć następujące toohello podobne wiadomości.

    ![Dane wyjściowe POST](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a>5. Weryfikuj rekordy w analizy dzienników
Po hello elementu runbook została ukończona w teście i upewnieniu się, dane wyjściowe hello został pomyślnie odebrany, może sprawdzić, czy rekordy hello zostały utworzone przy użyciu [wyszukiwania dziennika w analizy dzienników](../log-analytics/log-analytics-log-searches.md).

![Wpisu w Dzienniku](media/operations-management-suite-runbook-datacollect/log-output.png)

1. W hello portalu Azure wybierz obszar roboczy analizy dzienników.
2. Polecenie **dziennika wyszukiwania**.
3. Witaj wpisz następujące polecenie `Type=AutomationJob_CL` i kliknij przycisk Wyszukaj hello. Należy pamiętać, że typ rekordu hello zawiera _CL, który nie jest określone w skrypcie hello.  Ten sufiks jest tooindicate typu dziennika toohello automatycznie dołączany jest typem Dziennik niestandardowy.
4. Powinny pojawić się jeden lub więcej rekordów zwrócił wskazujący, że ten element runbook hello działa zgodnie z oczekiwaniami.


## <a name="6-publish-hello-runbook"></a>6. Publikowanie elementu runbook hello
Po upewnieniu się, że hello element runbook działa poprawnie, należy toopublish go, dlatego może być uruchomiony w środowisku produkcyjnym.  Można kontynuować tooedit i testowanie elementu runbook hello bez modyfikowania hello opublikowanej wersji.  

![Publikowanie elementu runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. Zwraca tooyour konta automatyzacji.
2. Polecenie **Runbook** i wybierz **zbieranie automatyzacji zadania**.
3. Kliknij przycisk **Edytuj** , a następnie **publikowania**.
4. Kliknij przycisk **tak** gdy zadawane tooverify mają toooverwrite hello wcześniej publikowane wersji.

## <a name="7-set-logging-options"></a>7. Ustaw opcje rejestrowania 
Dla testu, zostały stanie tooview [pełne dane wyjściowe](../automation/automation-runbook-output-and-messages.md#message-streams) ponieważ wartość zmiennej hello $VerbosePreference w skrypcie hello.  W środowisku produkcyjnym należy właściwości tooset hello rejestrowania dla elementu runbook hello Chcąc tooview pełne dane wyjściowe.  Dla elementu runbook hello jest używany w tym samouczku spowoduje to wyświetlenie danych json hello wysyłane tooLog Analytics.

![Rejestrowanie i śledzenie](media/operations-management-suite-runbook-datacollect/logging.png)

1. W elemencie runbook hello właściwości wybierz **rejestrowania i śledzenia** w obszarze **ustawienia elementu Runbook**.
2. Zmień ustawienia hello **rejestrowania rekordów pełnych** za**na**.
3. Kliknij pozycję **Zapisz**.

## <a name="8-schedule-runbook"></a>8. Planowanie elementu runbook
Witaj najczęściej sposób toostart elementu runbook, który służy do zbierania danych monitorowania jest tooschedule on toorun automatycznie.  Można to zrobić, tworząc [Harmonogram automatyzacji Azure](../automation/automation-schedules.md) i dołączania ich tooyour elementu runbook.

![Planowanie elementu runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. Witaj właściwości dla elementu runbook, zaznacz **harmonogramy** w obszarze **zasobów**.
2. Kliknij przycisk **Dodaj harmonogram** > **powiązania elementu runbook tooyour harmonogram** > **Utwórz nowy harmonogram**.
5. Typ w hello następujące wartości hello harmonogram, a następnie kliknij przycisk **Utwórz**.

| Właściwość | Wartość |
|:--|:--|
| Nazwa | Co godzinę AutomationJobs |
| Rozpoczyna się | Wybierz wszystkie czas bieżący czas hello ostatnich co najmniej 5 minut. |
| Cykl | Cykliczne |
| Powtarzanie co | 1 godzina |
| Wygaśnięcie zestawu | Nie |

Po utworzeniu harmonogramu hello należy wartości parametrów hello tooset, które będą używane w każdym uruchomieniu tego harmonogramu hello elementu runbook.

6. Kliknij przycisk **Skonfiguruj parametry i parametry uruchomieniowe**.
7. Podaj wartości dla Twojego **ResourceGroupName** i **AutomationAccountName**.
8. Kliknij przycisk **OK**. 

## <a name="9-verify-runbook-starts-on-schedule"></a>9. Sprawdź element runbook uruchamia zgodnie z harmonogramem
Zawsze, gdy element runbook jest uruchamiany, [tworzone jest zadanie](../automation/automation-runbook-execution.md) i wszelkie dane wyjściowe rejestrowane.  W rzeczywistości są hello jest zbieranie tych samych zadań, które hello elementu runbook.  Możesz sprawdzić, czy ten element runbook hello uruchamiany zgodnie z oczekiwaniami, sprawdzając hello zadania dla elementu runbook powitania po upływie hello czas rozpoczęcia harmonogramu hello.

![Zadania](media/operations-management-suite-runbook-datacollect/jobs.png)

1. Witaj właściwości dla elementu runbook, zaznacz **zadania** w obszarze **zasobów**.
2. Powinny pojawić się, że dostęp do listy zadań dla każdego elementu runbook hello czas uruchomienia.
3. Kliknij jeden z tooview zadania hello jego szczegóły.
4. Polecenie **wszystkie dzienniki** tooview hello dzienników i danych wyjściowych z hello elementu runbook.
5. Przewiń toohello toofind dolnej wprowadzania podobne toohello obraz poniżej.<br>![Pełne](media/operations-management-suite-runbook-datacollect/verbose.png)
6. Kliknij ten wpis tooview hello szczegółowe dane json, którego wysłano tooLog Analytics.



## <a name="next-steps"></a>Następne kroki
- Użyj [Widok projektanta](../log-analytics/log-analytics-view-designer.md) toocreate wyświetlania widoku hello danych, aby zostały pobrane toohello analizy dzienników repozytorium.
- Pakiet w elemencie runbook [rozwiązania do zarządzania](operations-management-suite-solutions-creating.md) toodistribute toocustomers.
- Dowiedz się więcej o [analizy dzienników](https://docs.microsoft.com/azure/log-analytics/).
- Dowiedz się więcej o [usługi Automatyzacja Azure](https://docs.microsoft.com/azure/automation/).
- Dowiedz się więcej o hello [interfejsu API modułów zbierających dane HTTP](../log-analytics/log-analytics-data-collector-api.md).
