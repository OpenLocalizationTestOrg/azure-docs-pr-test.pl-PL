---
title: aaaSchedules automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Harmonogramy automatyzacji są automatycznie używane tooschedule elementy runbook toostart usługi Automatyzacja Azure. Opisuje sposób toocreate i zarządzanie harmonogramem w, dzięki czemu może automatycznie uruchomić element runbook o określonej godzinie lub zgodnie z harmonogramem cyklicznym."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1c2da639-ad20-4848-920b-88e471b2e1d9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2016
ms.author: magoedte
ms.openlocfilehash: 888a5d15fd3442a2b8ab18dd8b0eb4ab9ad0c0d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Planowanie elementu Runbook w usłudze Azure Automation
tooschedule elementu runbook w automatyzacji Azure toostart o określonej godzinie, można połączyć tooone lub więcej harmonogramów. Harmonogram może być skonfigurowany tooeither uruchom raz lub pojawiał co godzinę lub harmonogramu dziennego dla elementów runbook w hello klasycznego portalu Azure i elementów runbook w portalu Azure hello, można również zaplanować je co tydzień, miesięczne, określone dni tygodnia hello lub dni hello miesiąc lub określony dzień miesiąca hello.  Element runbook może być połączone toomultiple harmonogramy, a harmonogram może mieć wielu tooit elementy runbook połączone.

> [!NOTE]
> Harmonogramy aktualnie nie obsługuje konfiguracji DSC automatyzacji Azure.
> 
> 

## <a name="windows-powershell-cmdlets"></a>Polecenia cmdlet programu Windows PowerShell
polecenia cmdlet Hello w hello w poniższej tabeli są używane toocreate i zarządzaj nimi harmonogramów z programu Windows PowerShell w automatyzacji Azure. One dostarczane jako część hello [modułu Azure PowerShell](/powershell/azure/overview).

| Polecenia cmdlet | Opis |
|:--- |:--- |
| **Polecenia cmdlet Menedżera zasobów systemu Azure** | |
| [Get-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/get-azurermautomationschedule) |Pobiera harmonogram. |
| [Nowe AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) |Tworzy nowy harmonogram. |
| [Usuń AzureRmAutomationSchedule](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |Usuwa harmonogram. |
| [Zestaw AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) |Ustawia właściwości hello istniejącego harmonogramu. |
| [Get-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |Pobiera zaplanowanego elementach runbook. |
| [Rejestr AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |Kojarzy elementu runbook z harmonogramem. |
| [Wyrejestruj AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |Dissociates elementu runbook z harmonogramem. |
| **Polecenia cmdlet do zarządzania usługi Azure** | |
| [Get-AzureAutomationSchedule](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |Pobiera harmonogram. |
| [Nowe AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |Tworzy nowy harmonogram. |
| [Usuń AzureAutomationSchedule](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |Usuwa harmonogram. |
| [Zestaw AzureAutomationSchedule](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |Ustawia właściwości hello istniejącego harmonogramu. |
| [Get-AzureAutomationScheduledRunbook](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Pobiera zaplanowanego elementach runbook. |
| [Rejestr AzureAutomationScheduledRunbook](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Kojarzy elementu runbook z harmonogramem. |
| [Wyrejestruj AzureAutomationScheduledRunbook](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Dissociates elementu runbook z harmonogramem. |

## <a name="creating-a-schedule"></a>Tworzenie harmonogramu
W portalu klasycznym hello lub programu Windows PowerShell, można utworzyć nowy harmonogram dla elementów runbook w hello portalu Azure. Istnieje również opcja hello utworzenia nowego harmonogramu połączenia przy użyciu hello Azure classic harmonogram tooa lub portalu Azure.

> [!NOTE]
> Automatyzacja Azure użyje modułów najnowszego hello na Twoim koncie automatyzacji po uruchomieniu nowego zaplanowanego zadania.  tooavoid wpływu na Twoje elementy runbook i hello procesów one zautomatyzować, należy najpierw przetestować wszystkie elementy runbook, które zostały połączone harmonogramy przy użyciu konta automatyzacji przeznaczonego do testowania.  Spowoduje to zweryfikować zaplanowane elementy runbook kontynuować toowork poprawnie i może nie dalsze rozwiązywanie problemów i zastosowanie wszystkie dokonane zmiany wymagane przed Migrowanie tooproduction wersji elementu runbook hello zaktualizowane.  
>  Konta automatyzacji nie automatycznie zapewni wszystkich nowych wersji modułów, chyba że zaktualizowano je ręcznie, wybierając hello [modułów Azure aktualizacji](automation-update-azure-modules.md) opcję hello **modułów** bloku. 
>  

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate nowego harmonogramu w hello portalu Azure
1. W portalu Azure, z Twojego konta automatyzacji hello kliknij hello **zasoby** hello tooopen kafelka **zasoby** bloku.
2. Kliknij przycisk hello **harmonogramy** hello tooopen kafelka **harmonogramy** bloku.
3. Kliknij przycisk **Dodaj harmonogram** u góry bloku hello hello.
4. Na powitania **nowy harmonogram** bloku, a typ **nazwa** i opcjonalnie **opis** hello nowego harmonogramu.
5. Wybierz harmonogram hello będą uruchamiane raz, czy reoccurring zgodnie z harmonogramem, wybierając **raz** lub **cyklu**.  W przypadku wybrania **raz** określ **godzina rozpoczęcia** , a następnie kliknij przycisk **Utwórz**.  W przypadku wybrania **cyklu**, określ **godzina rozpoczęcia** i częstotliwość hello częstotliwość hello runbook toorepeat - przez **godzina**, **dzień**, **tygodnia**, lub **miesiąca**.  W przypadku wybrania **tygodnia** lub **miesiąca** z listy rozwijanej hello hello **opcji cyklu** będzie widoczny w bloku hello i na wybór, powitalne **cyklu Opcja** zobaczy bloku i można wybrać hello dzień tygodnia, w przypadku wybrania **tygodnia**.  W przypadku wybrania **miesiąca**, można wybrać **dni tygodnia** lub określone dni miesiąca hello na hello kalendarza, a na koniec jest ma toorun na hello ostatni dzień miesiąca hello, lub nie, a następnie kliknij przycisk **OK** .   

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate nowego harmonogramu w hello klasycznego portalu Azure
1. W hello klasycznego portalu Azure wybierz automatyzacji, a następnie wybierz nazwę hello konta automatyzacji.
2. Wybierz hello **zasoby** kartę.
3. U dołu hello hello, kliknij przycisk **Dodaj ustawienie**.
4. Kliknij przycisk **Dodaj harmonogram**.
5. Wpisz **nazwa** i opcjonalnie **opis** dla nowych schedule.your hello zostanie uruchomiony harmonogram **jeden raz**, **co godzinę**, **Codzienne**, **co tydzień**, lub **miesięczne**.
6. Określ **czas rozpoczęcia** i inne opcje, w zależności od typu wybranego harmonogramu hello.

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate nowy harmonogram za pomocą programu Windows PowerShell
Można użyć hello [AzureAutomationSchedule nowy](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) toocreate polecenia cmdlet nowy harmonogram automatyzacji Azure classic elementów runbook, lub [AzureRmAutomationSchedule nowy](/powershell/module/azurerm.automation/new-azurermautomationschedule) polecenia cmdlet dla elementów runbook w hello Azure Portal. Należy określić godzinę rozpoczęcia hello hello harmonogram i częstotliwość hello, który ma być uruchamiany.

Hello następujące przykładowe polecenia Pokaż jak toocreate harmonogram hello 15 i 30 każdego miesiąca, za pomocą polecenia cmdlet usługi Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

następujące przykładowe polecenia Hello Pokaż toocreate nowy harmonogram który działania każdego dnia godzinie 3:30 20 stycznia 2015 począwszy od polecenia cmdlet usługi Azure Service Management.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-tooa-runbook"></a>Łączenie elementu runbook tooa harmonogramu
Element runbook może być połączone toomultiple harmonogramy, a harmonogram może mieć wielu tooit elementy runbook połączone. Jeśli element runbook ma parametry, można podać wartości dla nich. Należy podać wartości parametrów obowiązkowych i może podać wartości parametrów opcjonalnych.  Te wartości będą używane na każdym razem, gdy element runbook hello jest uruchomiony przez ten harmonogram.  Możesz dołączyć hello tego samego harmonogram tooanother i określ wartości różnych parametrów.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink element tooa harmonogram o hello portalu Azure
1. W portalu Azure, z Twojego konta automatyzacji hello kliknij hello **Runbook** hello tooopen kafelka **elementów Runbook** bloku.
2. Kliknij nazwę hello hello tooschedule elementu runbook.
3. Jeśli hello elementu runbook nie jest aktualnie połączony tooa harmonogram, będzie można hello danej opcji toocreate nowy harmonogram lub łącze tooan istniejącego harmonogramu.  
4. Jeśli hello runbook ma parametry, można wybrać opcję hello **zmodyfikuj parametry uruchomieniowe (domyślne: Azure)** i hello **parametry** bloku są prezentowane w którym można wprowadzić informacje hello odpowiednio.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink element tooa harmonogram o hello klasycznego portalu Azure
1. Hello klasycznego portalu Azure, wybierz **automatyzacji** a następnie kliknij nazwę hello konta automatyzacji.
2. Wybierz hello **elementów Runbook** kartę.
3. Kliknij nazwę hello hello tooschedule elementu runbook.
4. Kliknij przycisk hello **harmonogram** kartę.
5. Jeśli hello elementu runbook nie jest aktualnie połączony tooa harmonogram, a następnie użytkownik będzie mógł skorzystać z opcji hello zbyt**Link tooa nowy harmonogram** lub **tooan harmonogram istniejące łącze**.  Jeśli element runbook hello jest aktualnie połączony tooa harmonogram, kliknij przycisk **łącze** na hello dołu hello tooaccess okna te opcje.
6. Jeśli hello runbook ma parametry, pojawi się monit podanie ich wartości.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink runbook tooa harmonogramu przy użyciu programu Windows PowerShell
Można użyć hello [AzureAutomationScheduledRunbook rejestru](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink runbook klasycznego tooa harmonogramu lub [AzureRmAutomationScheduledRunbook rejestru](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) polecenia cmdlet dla elementów runbook w portalu Azure hello.  Można określić wartości parametrów hello runbook z parametrem parametry hello. Zobacz [uruchamianie elementu Runbook automatyzacji Azure](automation-starting-a-runbook.md) Aby uzyskać więcej informacji na temat określania wartości parametrów.

Hello następujące przykładowe polecenia Pokaż jak toolink runbook tooa harmonogramu przy użyciu polecenia cmdlet usługi Azure Resource Manager z parametrami.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
Hello następujące przykładowe polecenia Pokaż jak toolink harmonogramu przy użyciu polecenia cmdlet usługi Azure Service Management z parametrami.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a>Wyłączanie harmonogramu
Po wyłączeniu harmonogramu nie będzie działać tooit wszystkie elementy runbook połączone z tym harmonogramem. Można ręcznie wyłączyć harmonogram lub ustaw czas wygaśnięcia harmonogramów z częstotliwością po ich utworzeniu. Po osiągnięciu czas wygaśnięcia hello hello harmonogram zostanie wyłączony.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable harmonogram z hello portalu Azure
1. W portalu Azure, z Twojego konta automatyzacji hello kliknij hello **zasoby** hello tooopen kafelka **zasoby** bloku.
2. Kliknij przycisk hello **harmonogramy** hello tooopen kafelka **harmonogramy** bloku.
3. Kliknij nazwę hello harmonogram tooopen hello szczegóły blok.
4. Zmień **włączone** za**nr**.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable harmonogram z hello klasycznego portalu Azure
Można wyłączyć harmonogram w hello klasycznego portalu Azure na stronie Szczegóły harmonogramu hello hello harmonogramu.

1. W hello klasycznego portalu Azure wybierz automatyzacji, a następnie kliknij nazwę hello konta automatyzacji.
2. Wybierz kartę Zasoby hello.
3. Kliknij nazwę hello tooopen harmonogramu jego stronę szczegółów.
4. Zmień **włączone** za**nr**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable harmonogramu przy użyciu programu Windows PowerShell
Można użyć hello [AzureAutomationSchedule zestaw](http://msdn.microsoft.com/library/azure/dn690270.aspx) polecenia cmdlet toochange hello właściwości istniejącego harmonogramu klasycznego elementu runbook lub [AzureRmAutomationSchedule zestaw](/powershell/module/azurerm.automation/set-azurermautomationschedule) polecenia cmdlet dla elementów runbook w hello Azure Portal. Witaj toodisable zaplanować, określ **false** dla hello **IsEnabled** parametru.

Hello następujące przykładowe polecenia Pokaż jak toodisable harmonogram dla elementu runbook za pomocą polecenia cmdlet usługi Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

Hello następujące przykładowe polecenia pokazują, jak za pomocą harmonogramu toodisable hello polecenia cmdlet usługi Azure Service Management.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a>Następne kroki
* tooget pracę z elementów runbook automatyzacji Azure, zobacz [uruchamianie elementu Runbook automatyzacji Azure](automation-starting-a-runbook.md) 

