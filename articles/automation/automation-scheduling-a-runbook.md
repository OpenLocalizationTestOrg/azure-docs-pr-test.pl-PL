---
title: Element runbook automatyzacji Azure aaaScheduling | Dokumentacja firmy Microsoft
description: "Opisuje sposób toocreate Harmonogram automatyzacji Azure, aby automatycznie można uruchomić elementu runbook o określonej godzinie lub zgodnie z harmonogramem cyklicznym."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: c215b7ff6aa200466f3be566facba3c0cffcc924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Planowanie elementu Runbook w usłudze Azure Automation
tooschedule elementu runbook w automatyzacji Azure toostart o określonej godzinie, można połączyć tooone lub więcej harmonogramów. Harmonogram może być skonfigurowany tooeither uruchom raz lub na reoccurring godzinową lub dzienną harmonogramu dla elementów runbook w hello klasycznego portalu Azure i elementów runbook w portalu Azure hello, można również zaplanować je co tydzień, miesięczne, określone dni tygodnia hello lub dni miesiąc Hello, lub określony dzień miesiąca hello.  Element runbook może być połączone toomultiple harmonogramy, a harmonogram może mieć wielu tooit elementy runbook połączone.

## <a name="creating-a-schedule"></a>Tworzenie harmonogramu
W portalu klasycznym hello lub programu Windows PowerShell, można utworzyć nowy harmonogram dla elementów runbook w hello portalu Azure. Istnieje również opcja hello utworzenia nowego harmonogramu połączenia przy użyciu hello Azure classic harmonogram tooa lub portalu Azure.

> [!NOTE]
> Po skojarzeniu harmonogram z elementu runbook, automatyzacji przechowuje hello bieżącej wersji modułów hello na koncie i łączy je toothat harmonogramu.  Oznacza to, że jeśli znajdował się na koncie modułu w wersji 1.0, gdy utworzono harmonogram, a następnie zaktualizuj hello modułu tooversion 2.0, harmonogram hello będą nadal toouse 1.0.  W kolejności toouse hello modułu zaktualizowanych wersji należy utworzyć nowy harmonogram. 
> 
> 

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate nowego harmonogramu w hello klasycznego portalu Azure
1. W hello klasycznego portalu Azure wybierz automatyzacji, a następnie wybierz nazwę hello konta automatyzacji.
2. Wybierz hello **zasoby** kartę.
3. U dołu hello hello, kliknij przycisk **Dodaj ustawienie**.
4. Kliknij przycisk **Dodaj harmonogram**.
5. Wpisz **nazwa** i opcjonalnie **opis** dla nowych schedule.your hello zostanie uruchomiony harmonogram **jeden raz**, **co godzinę**, **Codzienne**, **co tydzień**, lub **miesięczne**.
6. Określ **czas rozpoczęcia** i inne opcje, w zależności od typu wybranego harmonogramu hello.

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate nowego harmonogramu w hello portalu Azure
1. W portalu Azure, z Twojego konta automatyzacji hello kliknij hello **zasoby** hello tooopen kafelka **zasoby** bloku.
2. Kliknij przycisk hello **harmonogramy** hello tooopen kafelka **harmonogramy** bloku.
3. Kliknij przycisk **Dodaj harmonogram** u góry bloku hello hello.
4. Na powitania **nowy harmonogram** bloku, a typ **nazwa** i opcjonalnie **opis** hello nowego harmonogramu.
5. Wybierz harmonogram hello będą uruchamiane raz, czy reoccurring zgodnie z harmonogramem, wybierając **raz** lub **cyklu**.  W przypadku wybrania **raz** określ **godzina rozpoczęcia** , a następnie kliknij przycisk **Utwórz**.  W przypadku wybrania **cyklu**, określ **godzina rozpoczęcia** i częstotliwość hello częstotliwość hello runbook toorepeat - przez **godzina**, **dzień**, **tygodnia**, lub **miesiąca**.  W przypadku wybrania **tygodnia** lub **miesiąca** z listy rozwijanej hello hello **opcji cyklu** będzie widoczny w bloku hello i na wybór, powitalne **cyklu Opcja** zobaczy bloku i można wybrać hello dzień tygodnia, w przypadku wybrania **tygodnia**.  W przypadku wybrania **miesiąca**, aby wybrać **dni tygodnia** lub określone dni miesiąca hello na hello kalendarza, a na koniec jest ma toorun go na hello ostatni dzień miesiąca hello, lub nie, a następnie kliknij przycisk **OK** .   

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate nowy harmonogram za pomocą programu Windows PowerShell
Można użyć hello [AzureAutomationSchedule nowy](http://msdn.microsoft.com/library/azure/dn690271.aspx) toocreate polecenia cmdlet nowy harmonogram automatyzacji Azure classic elementów runbook, lub [AzureRmAutomationSchedule nowy](https://msdn.microsoft.com/library/mt603577.aspx) polecenia cmdlet dla elementów runbook w hello Azure Portal. Należy określić godzinę rozpoczęcia hello hello harmonogram i częstotliwość hello, który ma być uruchamiany.

następujące przykładowe polecenia Hello Pokaż toocreate nowy harmonogram który działania każdego dnia godzinie 3:30 20 stycznia 2015 począwszy od polecenia cmdlet usługi Azure Service Management.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

Witaj następujące przykładowe polecenia pokazuje sposób toocreate harmonogram hello 15 i 30 każdego miesiąca, za pomocą polecenia cmdlet usługi Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-tooa-runbook"></a>Łączenie elementu runbook tooa harmonogramu
Element runbook może być połączone toomultiple harmonogramy, a harmonogram może mieć wielu tooit elementy runbook połączone. Jeśli element runbook ma parametry, można podać wartości dla nich. Należy podać wartości parametrów obowiązkowych i może podać wartości parametrów opcjonalnych.  Te wartości będą używane na każdym razem, gdy element runbook hello jest uruchomiony przez ten harmonogram.  Możesz dołączyć hello tego samego harmonogram tooanother i określ wartości różnych parametrów.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink element tooa harmonogram o hello klasycznego portalu Azure
1. Hello klasycznego portalu Azure, wybierz **automatyzacji** , a następnie kliknij nazwę hello konta automatyzacji.
2. Wybierz hello **elementów Runbook** kartę.
3. Kliknij nazwę hello hello tooschedule elementu runbook.
4. Kliknij przycisk hello **harmonogram** kartę.
5. Jeśli hello elementu runbook nie jest aktualnie połączony tooa harmonogram, a następnie użytkownik będzie mógł skorzystać z opcji hello zbyt**Link tooa nowy harmonogram** lub **tooan harmonogram istniejące łącze**.  Jeśli element runbook hello jest aktualnie połączony tooa harmonogram, kliknij przycisk **łącze** na hello dołu hello tooaccess okna te opcje.
6. Jeśli hello runbook ma parametry, pojawi się monit podanie ich wartości.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink element tooa harmonogram o hello portalu Azure
1. W portalu Azure, z Twojego konta automatyzacji hello kliknij hello **Runbook** hello tooopen kafelka **elementów Runbook** bloku.
2. Kliknij nazwę hello hello tooschedule elementu runbook.
3. Jeśli hello elementu runbook nie jest aktualnie połączony tooa harmonogram, będzie można hello danej opcji toocreate nowy harmonogram lub łącze tooan istniejącego harmonogramu.  
4. Jeśli hello runbook ma parametry, można wybrać opcję hello **zmodyfikuj parametry uruchomieniowe (domyślne: Azure)** i hello **parametry** bloku są prezentowane w którym można wprowadzić informacje hello odpowiednio.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink runbook tooa harmonogramu przy użyciu programu Windows PowerShell
Można użyć hello [AzureAutomationScheduledRunbook rejestru](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink runbook klasycznego tooa harmonogramu lub [AzureRmAutomationScheduledRunbook rejestru](https://msdn.microsoft.com/library/mt603575.aspx) polecenia cmdlet dla elementów runbook w portalu Azure hello.  Można określić wartości parametrów hello runbook z parametrem parametry hello. Zobacz [uruchamianie elementu Runbook automatyzacji Azure](automation-starting-a-runbook.md) Aby uzyskać więcej informacji na temat określania wartości parametrów.

Hello następujące przykładowe polecenia Pokaż jak toolink harmonogramu przy użyciu polecenia cmdlet usługi Azure Service Management z parametrami.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

Hello następujące przykładowe polecenia Pokaż jak toolink runbook tooa harmonogramu przy użyciu polecenia cmdlet usługi Azure Resource Manager z parametrami.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a>Wyłączanie harmonogramu
Po wyłączeniu harmonogramu nie będzie działać tooit wszystkie elementy runbook połączone z tym harmonogramem. Można ręcznie wyłączyć harmonogram lub ustaw czas wygaśnięcia harmonogramów z częstotliwością po ich utworzeniu. Po osiągnięciu czas wygaśnięcia hello hello harmonogram zostanie wyłączony.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable harmonogram z hello klasycznego portalu Azure
Można wyłączyć harmonogram w hello klasycznego portalu Azure na stronie Szczegóły harmonogramu hello hello harmonogramu.

1. W hello klasycznego portalu Azure wybierz automatyzacji, a następnie kliknij przycisk w hello nazwa konta automatyzacji.
2. Wybierz kartę Zasoby hello.
3. Kliknij nazwę hello tooopen harmonogramu jego stronę szczegółów.
4. Zmień **włączone** za**nr**.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable harmonogram z hello portalu Azure
1. W portalu Azure, z Twojego konta automatyzacji hello kliknij hello **zasoby** hello tooopen kafelka **zasoby** bloku.
2. Kliknij przycisk hello **harmonogramy** hello tooopen kafelka **harmonogramy** bloku.
3. Kliknij nazwę hello harmonogram tooopen hello szczegóły blok.
4. Zmień **włączone** za**nr**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable harmonogramu przy użyciu programu Windows PowerShell
Można użyć hello [AzureAutomationSchedule zestaw](http://msdn.microsoft.com/library/azure/dn690270.aspx) polecenia cmdlet toochange hello właściwości istniejącego harmonogramu klasycznego elementu runbook lub [AzureRmAutomationSchedule zestaw](https://msdn.microsoft.com/library/mt603566.aspx) polecenia cmdlet dla elementów runbook w hello Azure Portal. Witaj toodisable zaplanować, określ **false** dla hello **IsEnabled** parametru.

Hello następujące przykładowe polecenia pokazują, jak za pomocą harmonogramu toodisable hello polecenia cmdlet usługi Azure Service Management.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

Hello następujące przykładowe polecenia Pokaż jak toodisable harmonogram dla elementu runbook za pomocą polecenia cmdlet usługi Azure Resource Manager.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a>Następne kroki
* Zobacz toolearn więcej informacji na temat pracy z harmonogramami, [zasobów harmonogramu usługi Automatyzacja Azure](http://msdn.microsoft.com/library/azure/dn940016.aspx)
* tooget pracę z elementów runbook automatyzacji Azure, zobacz [uruchamianie elementu Runbook automatyzacji Azure](automation-starting-a-runbook.md) 

