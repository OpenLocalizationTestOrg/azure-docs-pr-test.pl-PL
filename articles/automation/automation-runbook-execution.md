---
title: Wykonanie elementu Runbook automatyzacji Azure | Dokumentacja firmy Microsoft
description: "W tym artykule opisano szczegółowe informacje o przetwarzaniu elementu runbook automatyzacji Azure."
services: automation
documentationcenter: 
author: georgewallace
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/15/2017
ms.author: magoedte;bwren
ms.openlocfilehash: a443071aee3e0f845de4387322d2866157a9fe87
ms.sourcegitcommit: 357afe80eae48e14dffdd51224c863c898303449
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/15/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Wykonanie elementu Runbook automatyzacji Azure
Po uruchomieniu elementu runbook w automatyzacji Azure tworzone jest zadanie. Zadanie jest pojedynczym wystąpieniem wykonania elementu runbook. Pracownik usługi Automatyzacja Azure jest przypisany do każdego zadania. Pracownicy są współużytkowane przez wiele kont platformy Azure, są odizolowane od siebie zadań z różnych kont automatyzacji. Możesz nie mieć kontroli za pośrednictwem których procesu roboczego obsługującym żądanie dla zadania. Pojedynczy element runbook może mieć wiele zadań została uruchomiona w tym samym czasie.  Może być ponownie używane środowiska wykonania zadań z tego samego konta automatyzacji. Podczas wyświetlania listy elementów runbook w portalu Azure, wyświetla stan wszystkich zadań, które zostały uruchomione dla każdego elementu runbook. Aby śledzić stan każdego z nich, można wyświetlić listę zadań dla każdego elementu runbook. Opis stany różne zadania [stany zadania](#job-statuses).

Na poniższym diagramie przedstawiono cykl życia zadania elementu runbook dla [graficznych elementów runbook](automation-runbook-types.md#graphical-runbooks) i [elementach runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).

![Stany zadania — przepływ pracy programu PowerShell](./media/automation-runbook-execution/job-statuses.png)

Na poniższym diagramie przedstawiono cykl życia zadania elementu runbook dla [elementy runbook programu PowerShell](automation-runbook-types.md#powershell-runbooks).

![Stany zadania — skrypt programu PowerShell](./media/automation-runbook-execution/job-statuses-script.png)

Twoje zadania mają dostęp do zasobów na platformie Azure przez utworzenie połączenia z subskrypcją platformy Azure. Tylko mają dostęp do zasobów w centrum danych, jeśli te zasoby są dostępne z chmury publicznej.

## <a name="job-statuses"></a>Stany zadania
W poniższej tabeli opisano różne stany, które są możliwe w dla zadania.

| Stan | Opis |
|:--- |:--- |
| Ukończony |Zadanie zostało ukończone pomyślnie. |
| Niepowodzenie |Dla [graficzny i przepływ pracy programu PowerShell elementów runbook](automation-runbook-types.md), element runbook kompilacja nie powiodła się.  Aby uzyskać [elementów runbook skrypt programu PowerShell](automation-runbook-types.md), nie można uruchomić elementu runbook lub zadania wystąpił wyjątek. |
| Nie powiodło się, oczekiwania dla zasobów |Zadanie nie powiodło się, ponieważ osiągnął [odpowiedni udział](#fair-share) ograniczyć trzy razy i z tego samego punktu kontrolnego lub od początku elementu runbook każdej godzina rozpoczęcia. |
| W kolejce |Zadanie oczekuje dla zasobów procesu roboczego automatyzacji dostępny, aby można było go uruchomić. |
| Uruchamianie |Zadanie zostało przypisane do procesu roboczego, a system jest w trakcie jego uruchomienie. |
| Wznawianie |System jest w trakcie wznawiania zadania po został wstrzymany. |
| Uruchomione |Zadanie zostało uruchomione. |
| Uruchomiona, oczekiwania dla zasobów |Zadanie zostało zwolnione, ponieważ osiągnął [odpowiedni udział](#fair-share) limit. Jest wznawiana wkrótce z ostatniego punktu kontrolnego. |
| Zatrzymane |Zadanie zostało zatrzymane przez użytkownika przed jej ukończeniem. |
| Zatrzymywanie |System jest w trakcie zatrzymywania zadania. |
| Wstrzymano |Zadanie zostało zawieszone przez użytkownika przez system lub za pomocą polecenia w elemencie runbook. Zawieszone zadanie można uruchomić ponownie i wznowić z ostatniego punktu kontrolnego lub od początku elementu runbook, jeśli nie ma on punkty kontrolne. Element runbook zostanie zawieszony przez system tylko, po wystąpieniu wyjątku. Domyślnie jest równa ErrorActionPreference **Kontynuuj**, co oznacza, że zadanie będzie uruchomione w przypadku wystąpienia błędu. Jeśli ustawiono tę zmienną preferencji **zatrzymać**, a następnie wstrzymuje zadanie w przypadku wystąpienia błędu.  Dotyczy [graficzny i przepływ pracy programu PowerShell elementów runbook](automation-runbook-types.md) tylko. |
| Wstrzymywanie |System próbuje zawiesić zadanie na żądanie użytkownika. Element runbook musi dotrzeć do swojego następnego punktu kontrolnego, zanim może zostać zawieszone. Jeśli przekazany już ostatni punkt kontrolny, a następnie jego zakończenie przed może zostać zawieszone.  Dotyczy [graficzny i przepływ pracy programu PowerShell elementów runbook](automation-runbook-types.md) tylko. |

## <a name="viewing-job-status-from-the-azure-portal"></a>Wyświetlanie stanu zadań z portalu Azure
Możesz wyświetlić podsumowanie stanu wszystkich zadań elementu runbook lub przejście do szczegółów określonego zadania elementu runbook w portalu Azure lub konfigurowania integracji z obszaru roboczego analizy dzienników programu Microsoft Operations Management Suite (OMS) do przekazywania strumienia zadania stanu i zadania elementu runbook.  Aby uzyskać więcej informacji na temat integracji z analizy dzienników OMS, zobacz [przekazuj strumienie zadania i stan zadania z automatyzacji analizy dzienników (OMS)](automation-manage-send-joblogs-log-analytics.md).  

### <a name="automation-runbook-jobs-summary"></a>Podsumowanie zadań elementu runbook automatyzacji
Po prawej stronie wybrane konto automatyzacji wyświetlane podsumowanie wszystkich zadań elementu runbook do wybranego konta automatyzacji w ramach **statystyki zadania** kafelka.<br><br> ![Kafelek statystyki zadania](./media/automation-runbook-execution/automation-account-job-status-summary.png).<br> Ten Kafelek Wyświetla graficzną reprezentację stanu zadania dla wszystkich zadań wykonywanych i liczba.  

Kliknięcie kafelka przedstawia **zadania** bloku, który zawiera listę podsumowania wszystkie zadania wykonywane, stan, wykonywania zadania oraz czas rozpoczęcia i zakończenia.<br><br> ![Bloku zadania konta automatyzacji](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  Lista zadań można filtrować, wybierając **filtrowania zadań** i filtru określonego elementu runbook, stan zadania, lub z listy rozwijanej, zakres daty i godziny do przeszukania.<br><br> ![Stan zadania filtru](./media/automation-runbook-execution/automation-account-jobs-filter.png)

Alternatywnie można wyświetlić szczegóły podsumowania zadania dla określonego elementu runbook przez wybranie tego elementu runbook z **Runbook** bloku w konta automatyzacji, a następnie wybierz **zadania** kafelka.  Stwarza **zadania** bloku i z tego miejsca można kliknąć rekord zadania, aby wyświetlić jego szczegóły i danych wyjściowych.<br><br> ![Bloku zadania konta automatyzacji](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>Podsumowanie zadania
Można wyświetlić listę wszystkich zadań, które zostały utworzone dla określonego elementu runbook i ich najnowszy stan. Można filtrować tej listy według stanu zadania i zakresu dat dla ostatniej zmiany zadania. Aby wyświetlić jego szczegółowe informacje i dane wyjściowe, kliknij nazwę zadania. Widok szczegółowy zadania zawiera wartości parametrów elementu runbook udostępnione danemu zadaniu.

Poniższe kroki służy do wyświetlania zadań elementu runbook.

1. W portalu Azure wybierz **automatyzacji** , a następnie wybierz nazwę konta automatyzacji.
2. Koncentrator, zaznacz **elementów Runbook** , a następnie na **elementów Runbook** bloku wybierz element z listy.
3. W bloku dla wybranego elementu runbook, kliknij **zadania** kafelka.
4. Kliknij jedno z zadań na liście, a następnie w bloku szczegóły zadania elementu runbook można wyświetlić jego szczegóły i danych wyjściowych.

## <a name="retrieving-job-status-using-windows-powershell"></a>Trwa pobieranie stanu zadania za pomocą środowiska Windows PowerShell
Można użyć [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) do pobrania zadań utworzonych dla elementu runbook i szczegółów dotyczących określonego zadania. Po uruchomieniu elementu runbook przy użyciu programu Windows PowerShell [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx), a następnie zwraca zadania wynikowe. Użyj [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)danych wyjściowych danych wyjściowych, aby uzyskać zadanie.

Następujące przykładowe polecenia Pobierz ostatnie zadanie przykładowego elementu runbook i wyświetla jego stan, wartości parametrów elementu runbook oraz dane wyjściowe z zadania.

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>Odpowiedni udział
Aby udostępnianie zasobów między wszystkich elementów runbook w chmurze, usługi Automatyzacja Azure tymczasowo spowoduje zwolnienie wszystkie zadania po działaniu na trzy godziny.  W tym czasie zadania dla [opartych na środowisku PowerShell elementów runbook](automation-runbook-types.md#powershell-runbooks) zostały zatrzymane i nie zostanie uruchomiona ponownie.  Pokazuje stan zadania **zatrzymane**.  Ten typ elementu runbook zawsze zostanie ponownie od samego początku, ponieważ nie obsługują punkty kontrolne.  

[Na podstawie przepływu pracy programu PowerShell elementów runbook](automation-runbook-types.md#powershell-workflow-runbooks) zostanie wznowione z ostatnią [punktu kontrolnego](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints).  Po uruchomieniu trzy godziny, zadanie elementu runbook zostanie zawieszony przez usługę i jego stan pokazuje **uruchomiony, oczekiwanie na zasoby**.  Po udostępnieniu piaskownicy, element runbook zostanie automatycznie ponownie, usługa Automatyzacja i przywraca z ostatniego punktu kontrolnego.  Jest to normalne zachowanie przepływu pracy programu PowerShell dla zawiesić/restart.  Jeśli element runbook ponownie przekracza trzy godziny środowiska uruchomieniowego, proces jest powtarzany, maksymalnie trzy razy.  Po uruchomieniu trzecich, jeśli element runbook jeszcze nie zostało ukończone w ciągu trzech godzin, a następnie zadania elementu runbook nie powiodło się i pokazuje stan zadania **nie powiodło się oczekiwanie na zasoby**.  W takim przypadku zostanie wyświetlony następujący wyjątek z awarią.

*Zadanie nie może kontynuować z powodu wielokrotnie został wykluczony z tego samego punktu kontrolnego. Upewnij się, że element Runbook nie wykona operacji długich bez utrwalanie stanu.*

To jest ochrona usługi z elementów runbook uruchomionych w nieskończoność nie kończą działania, ponieważ nie są oni wprowadzać go do następnego punktu kontrolnego bez zwalnianie ponownie.

Jeśli element runbook ma punktów kontrolnych lub zadanie nie osiągnęła pierwszy punkt kontrolny przed zwalnianie, następnie jest uruchamiany ponownie od samego początku.  

Podczas tworzenia elementu runbook, należy upewnić się, że czas do uruchomienia żadnych działań między dwoma punktami kontrolnymi nie przekracza trzy godziny. Należy dodać punkty kontrolne do elementu runbook, aby upewnić się, że nie osiągnięciu tego limitu trzy godziny lub podzielić long długotrwałych operacji. Na przykład element runbook może wykonywać indeksowanie na duże bazy danych SQL. Jeśli operacja jednego nie zostanie ukończone przed upływem limitu odpowiedni udział, zadania są zwolnione i ponownego uruchomienia od początku. W takim przypadku należy podzielić operacji indeksowanie w wielu kroków, takich jak indeksowanie jedna tabela w czasie i następnie Wstaw punkt kontrolny po zakończeniu każdej operacji, dzięki czemu można wznowić zadanie, po ostatniej operacji, aby zakończyć.

## <a name="next-steps"></a>Następne kroki
* Aby dowiedzieć się więcej na temat różnych metod, które mogą służyć do uruchamiania elementu runbook automatyzacji Azure, zobacz [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md)

