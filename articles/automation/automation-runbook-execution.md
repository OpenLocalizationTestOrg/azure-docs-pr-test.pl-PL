---
title: wykonanie aaaRunbook automatyzacji Azure | Dokumentacja firmy Microsoft
description: "W tym artykule opisano szczegóły hello przetwarzaniu elementu runbook automatyzacji Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: bwren
ms.openlocfilehash: bdb535675443353d44640bc7773de3f9dac5e42c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Wykonanie elementu Runbook automatyzacji Azure
Po uruchomieniu elementu runbook w automatyzacji Azure tworzone jest zadanie. Zadanie jest pojedynczym wystąpieniem wykonania elementu runbook. Automatyzacja Azure, proces roboczy jest przypisany toorun każdego zadania. Pracownicy są współużytkowane przez wiele kont platformy Azure, są odizolowane od siebie zadań z różnych kont automatyzacji. Nie masz kontrolę nad którym żądania hello usługi procesu roboczego dla zadania.  Pojedynczy element runbook może mieć wiele zadań została uruchomiona w tym samym czasie. Po wyświetleniu hello listę elementów runbook w portalu Azure hello wymieniono hello stan wszystkich zadań, które zostały uruchomione dla każdego elementu runbook. Witaj listy zadań dla każdego elementu runbook można wyświetlić w kolejności tootrack hello stan każdego z nich. Opis hello stany różne zadania, zobacz [stany zadania](#job-statuses).

Witaj Poniższy diagram przedstawia hello cyklem życia zadania elementu runbook dla [graficznych elementów runbook](automation-runbook-types.md#graphical-runbooks) i [elementach runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).

![Stany zadania — przepływ pracy programu PowerShell](./media/automation-runbook-execution/job-statuses.png)

Witaj Poniższy diagram przedstawia hello cyklem życia zadania elementu runbook dla [elementy runbook programu PowerShell](automation-runbook-types.md#powershell-runbooks).

![Stany zadania — skrypt programu PowerShell](./media/automation-runbook-execution/job-statuses-script.png)

Twoje zadania mają tooyour dostęp do usługi Azure zasobów poprzez tooyour połączenia subskrypcji platformy Azure. Tylko mają tooresources dostępu w centrum danych, jeśli te zasoby są dostępne z chmury publicznej hello.

## <a name="job-statuses"></a>Stany zadania
Witaj poniższej tabeli opisano hello różne stany, które są możliwe w dla zadania.

| Stan | Opis |
|:--- |:--- |
| ukończone |Witaj zadanie zostało ukończone pomyślnie. |
| Nie powiodło się |Dla [graficzny i przepływ pracy programu PowerShell elementów runbook](automation-runbook-types.md), hello runbook toocompile nie powiodło się.  Dla [elementów runbook skrypt programu PowerShell](automation-runbook-types.md), hello elementu runbook nie powiodło się toostart lub hello zadania wystąpił wyjątek. |
| Nie powiodło się, oczekiwania dla zasobów |Witaj zadanie nie powiodło się, ponieważ osiągnął hello [odpowiedni udział](#fairshare) ograniczyć trzy razy, a następnie uruchomiona z hello tego samego punktu kontrolnego lub od hello elementu hello runbook każda godzina rozpoczęcia. |
| W kolejce |Hello zadanie oczekuje na zasoby na toocome procesu roboczego automatyzacji dostępny tak, aby można było go uruchomić. |
| Uruchamianie |Hello zadanie zostało przypisane tooa pracownika, oraz systemu hello jest proces hello jego uruchomienie. |
| Wznawianie pracy |Hello system jest proces hello wznawianie zadania powitania po został wstrzymany. |
| Działanie |Witaj zadanie jest uruchomione. |
| Uruchomiona, oczekiwania dla zasobów |Witaj zadania został zwolniony, ponieważ osiągnął hello [odpowiedni udział](#fairshare) limit. Jest wznawiana wkrótce z ostatniego punktu kontrolnego. |
| Zatrzymane |Witaj zadanie zostało zatrzymane przez użytkownika hello, przed jego ukończeniem. |
| Zatrzymywanie |Hello system jest hello proces zatrzymywania zadania hello. |
| Zawieszone |zadanie Hello zostało zawieszone przez użytkownika hello przez hello system lub za pomocą polecenia w elemencie runbook hello. Zawieszone zadanie można uruchomić ponownie i wznowić z ostatniego punktu kontrolnego lub od początku hello hello elementu runbook, jeśli nie ma on punkty kontrolne. Hello runbook tylko zostanie zawieszony przez system powitania po wystąpieniu wyjątku. Domyślnie ErrorActionPreference ustawiono zbyt**Kontynuuj**, co oznacza zadania hello kontynuowanie działania w przypadku wystąpienia błędu. Jeśli ta zmienna preferencji jest ustawiona zbyt**zatrzymać**, następnie zadania hello zawiesza się w przypadku wystąpienia błędu.  Stosuje zbyt[graficzny i przepływ pracy programu PowerShell elementów runbook](automation-runbook-types.md) tylko. |
| Zawieszanie |Hello system próbuje toosuspend hello zadanie na żądanie hello hello użytkownika. Witaj runbook musi dotrzeć do swojego następnego punktu kontrolnego, zanim może zostać zawieszone. Jeśli przekazany już ostatni punkt kontrolny, a następnie jego zakończenie przed może zostać zawieszone.  Stosuje zbyt[graficzny i przepływ pracy programu PowerShell elementów runbook](automation-runbook-types.md) tylko. |

## <a name="viewing-job-status-from-hello-azure-portal"></a>Wyświetlanie stanu zadań z hello portalu Azure
Możesz wyświetlić podsumowanie stanu wszystkich zadań elementu runbook lub przejście do szczegółów określonego zadania elementu runbook w portalu Azure hello lub konfigurowania integracji programu stan zadania elementu runbook tooforward obszaru roboczego analizy dzienników programu Microsoft Operations Management Suite (OMS) i strumienie zadania.  Aby uzyskać więcej informacji na temat integracji z analizy dzienników OMS, zobacz [przekazuj strumienie zadania i stan zadania z automatyzacji tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).  

### <a name="automation-runbook-jobs-summary"></a>Podsumowanie zadań elementu runbook automatyzacji
Na powitania prawo do wybranego konta automatyzacji, wyświetlane podsumowanie wszystkich hello zadania elementów runbook do wybranego konta automatyzacji w ramach **statystyki zadania** kafelka.<br><br> ![Kafelek statystyki zadania](./media/automation-runbook-execution/automation-account-job-status-summary.png).<br> Ten Kafelek Wyświetla graficzną reprezentację hello stan zadania dla wszystkich zadań wykonywanych i liczba.  

Kliknięcie kafelka hello przedstawia hello **zadania** bloku, który zawiera listę podsumowania wszystkie zadania wykonywane, stan, wykonywania zadania oraz czas rozpoczęcia i zakończenia.<br><br> ![Bloku zadania konta automatyzacji](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  Można filtrować hello listę prac, wybierając **filtrowania zadań** i filtrować według określonego elementu runbook, stan zadania, lub z listy rozwijanej hello hello toosearch zakres daty/godziny w ciągu.<br><br> ![Stan zadania filtru](./media/automation-runbook-execution/automation-account-jobs-filter.png)

Alternatywnie można wyświetlić szczegóły podsumowania zadania dla określonego elementu runbook przez wybranie tego elementu runbook z hello **elementów Runbook** bloku w konta automatyzacji, a następnie wybierz opcję hello **zadania** kafelka.  Stwarza hello **zadania** bloku i z tego miejsca możesz kliknąć tooview rekordów zlecenia hello jego szczegóły i danych wyjściowych.<br><br> ![Bloku zadania konta automatyzacji](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>Podsumowanie zadania
Można wyświetlić listę wszystkich zadań hello, które zostały utworzone dla określonego elementu runbook i ich najnowszy stan. Tej listy można filtrować według stanu zadania i hello zakres dat dla hello Ostatnia zmiana toohello zadania. tooview jego szczegółowe informacje i dane wyjściowe, kliknij nazwę hello zadania. Witaj widok szczegółowy zadania hello zawiera hello wartości parametrów elementu runbook hello, które zostały podane toothat zadania.

Możesz użyć hello następujące kroki tooview hello zadań elementu runbook.

1. Hello portalu Azure, wybierz **automatyzacji** , a następnie wybierz nazwę hello konta automatyzacji.
2. Z Centrum hello wybierz **elementów Runbook** , a następnie na powitania **elementów Runbook** bloku wybierz element z listy hello.
3. W bloku hello hello wybrany element runbook, kliknij hello **zadania** kafelka.
4. Kliknij jeden z zadań hello hello listy i w bloku szczegóły zadania elementu runbook hello można wyświetlić jego szczegóły i danych wyjściowych.

## <a name="retrieving-job-status-using-windows-powershell"></a>Trwa pobieranie stanu zadania za pomocą środowiska Windows PowerShell
Można użyć hello [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) tooretrieve hello zadania utworzone dla elementu runbook i hello szczegółów dotyczących określonego zadania. Po uruchomieniu elementu runbook przy użyciu programu Windows PowerShell [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx), a następnie zwraca zadania wynikowe hello. Użyj [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)tooget danych wyjściowych danych wyjściowych zadania.

Witaj następujące przykładowe polecenia Pobierz hello ostatnie zadanie przykładowego elementu runbook i wyświetla jego stan, wartości hello podany dla parametrów elementu runbook hello i dane wyjściowe z zadania hello hello.

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>Odpowiedni udział
W kolejności tooshare zasobów między wszystkich elementów runbook w chmurze hello usługi Automatyzacja Azure tymczasowo spowoduje zwolnienie wszystkie zadania po działaniu na trzy godziny.  W tym czasie zadania dla [opartych na środowisku PowerShell elementów runbook](automation-runbook-types.md#powershell-runbooks) zostały zatrzymane i nie zostanie uruchomiona ponownie.  Witaj pokazuje stan zadania **zatrzymane**.  Ten typ elementu runbook zawsze zostanie ponownie od początku hello, ponieważ nie obsługują punkty kontrolne.  

[Na podstawie przepływu pracy programu PowerShell elementów runbook](automation-runbook-types.md#powershell-workflow-runbooks) zostanie wznowione z ostatnią [punktu kontrolnego](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints).  Po uruchomieniu trzech godzin, hello zadanie elementu runbook zostanie zawieszony przez usługę hello i jego stan pokazuje **uruchomiony, oczekiwanie na zasoby**.  Po udostępnieniu piaskownicy hello runbook zostanie automatycznie ponownie, usługa Automatyzacja hello i przywraca z ostatniego punktu kontrolnego hello.  Jest to normalne zachowanie przepływu pracy programu PowerShell dla zawiesić/restart.  Jeśli hello runbook ponownie przekracza trzy godziny środowiska uruchomieniowego, hello proces jest powtarzany, zapasowej toothree razy.  Po hello trzecim ponownym uruchomieniu, jeśli hello runbook jeszcze nie zostało ukończone w ciągu trzech godzin, a następnie hello zadanie elementu runbook nie powiodło się i pokazuje stan zadania hello **nie powiodło się oczekiwanie na zasoby**.  W takim przypadku zostanie wyświetlony następujący wyjątek z błędem hello hello.

*zadanie Hello nie może kontynuować wykonywania, ponieważ wielokrotnie został wykluczony z hello tego samego punktu kontrolnego. Upewnij się, że element Runbook nie wykona operacji długich bez utrwalanie stanu.*

Jest usługa hello tooprotect uruchamiania elementów runbook bez ukończenia, ponieważ nie są one toomake mogli go toohello następnego punktu kontrolnego bez zwalnianie ponownie.

Jeśli zadania hello nie osiągnęła hello pierwszy punkt kontrolny przed zwalnianie hello runbook ma punktów kontrolnych, następnie ponownego uruchomienia od początku hello.  

Podczas tworzenia elementu runbook, należy upewnić się, że toorun czasu hello żadnych działań między dwoma punktami kontrolnymi nie przekracza trzy godziny. Może być konieczne tooadd punktów kontrolnych tooyour runbook tooensure że nie osiągnięciu tego limitu trzy godziny lub podzielić long długotrwałych operacji. Na przykład element runbook może wykonywać indeksowanie na duże bazy danych SQL. Jeśli operacja jednego nie zostanie zakończone w odpowiedniej hello limit udziału, a następnie zadania hello są zwolnione i ponownego uruchomienia od początku hello. W takim przypadku należy podzielić hello Indeksowanie operacji w wielu kroków, takich jak indeksowanie jedna tabela w czasie, a następnie Włóż punkt kontrolny po zakończeniu każdej operacji, dzięki czemu hello zadania można wznowić po hello ostatniej operacji toocomplete.

## <a name="next-steps"></a>Następne kroki
* toolearn więcej informacji na temat różnych metod hello, które mogą być używane toostart elementu runbook automatyzacji Azure, zobacz [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md)

