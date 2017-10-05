---
title: "Uruchamianie zadań w tle za pomocą zadań WebJob"
description: "Dowiedz się, jak wykonywać zadania w tle w aplikacjach sieci web platformy Azure."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: af01771e-54eb-4aea-af5f-f883ff39572b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2016
ms.author: glenga
ms.openlocfilehash: 3f8ae748e3d9c6b4e342536926a52b4e8f37ee51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-background-tasks-with-webjobs"></a>Uruchamianie zadań w tle za pomocą zadań WebJob
## <a name="overview"></a>Omówienie
Mogą uruchamiać programów lub skryptów, które znajdują się w zadań Webjob w Twojej [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci web na trzy sposoby: na żądanie, w sposób ciągły, lub zgodnie z harmonogramem. Nie ma żadnych dodatkowych kosztów, aby użyć zadań Webjob.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

W tym artykule pokazano, jak wdrażanie przy użyciu zadań Webjob [Azure Portal](https://portal.azure.com). Aby uzyskać informacje o sposobie wdrażania przy użyciu programu Visual Studio lub proces ciągłego dostarczania, zobacz [sposobu wdrażania zadań Webjob Azure do aplikacji sieci Web](websites-dotnet-deploy-webjobs.md).

Zestaw SDK zadań Webjob Azure upraszcza wiele zadań Webjob zadania programowania. Aby uzyskać więcej informacji, zobacz [co to jest zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md).

 Środowisko Azure Functions zapewnia uruchamianie programów i skryptów z niekorzystającą środowiska lub aplikacji usługi app Service w inny sposób. Aby uzyskać więcej informacji, zobacz [Azure Functions — omówienie](../azure-functions/functions-overview.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>Typy plików akceptowalne dla skryptów lub programów
Akceptowane są następujące typy plików:

* cmd, bat, .exe (przy użyciu cmd systemu windows)
* ps1 (przy użyciu programu powershell)
* SH (przy użyciu bash)
* PHP (za pomocą języka php)
* .PY (przy użyciu języka python)
* js (przy użyciu węzła)
* JAR (przy użyciu języka java)

## <a name="CreateOnDemand"></a>Tworzenie na żądanie zadania WebJob w portalu
1. W **aplikacji sieci Web** bloku [Azure Portal](https://portal.azure.com), kliknij przycisk **wszystkie ustawienia > zadań Webjob** pokazanie **Webjob** bloku.
   
    ![Blok zadania WebJob](./media/web-sites-create-web-jobs/wjblade.png)
2. Kliknij pozycję **Dodaj**. **Dodać zadania WebJob** zostanie wyświetlone okno dialogowe.
   
    ![Dodawanie bloku zadania WebJob](./media/web-sites-create-web-jobs/addwjblade.png)
3. W obszarze **nazwa**, podaj nazwę dla zadania WebJob. Nazwa musi rozpoczynać się literą lub cyfrą i nie może zawierać żadnych znaków specjalnych innych niż "-" i "_".
4. W **sposobu wykonywania** wybierz **uruchomić na żądanie**.
5. W **przekazywanie pliku** polu, kliknij ikonę folderu i przejdź do pliku zip, który zawiera skrypt. Plik zip powinien zawierać pliku wykonywalnego (.exe .cmd bat SH, PHP PY i js) oraz wszelkie pliki pomocnicze potrzebne do uruchomienia tego programu lub skryptu.
6. Sprawdź **Utwórz** przekazywać skrypt do aplikacji sieci web. 
   
    Nazwa określona dla zadania WebJob zostanie wyświetlony na liście w **Webjob** bloku.
7. Aby uruchomić zadania WebJob, kliknij prawym przyciskiem myszy jego nazwę na liście, a następnie kliknij przycisk **Uruchom**.
   
    ![Uruchom zadanie WebJob](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>Tworzenie stale uruchomione zadania WebJob
1. Aby utworzyć stale wykonywania zadania WebJob, wykonaj te same czynności dla tworzenie zadanie WebJob, które jest uruchamiane jeden raz, ale w **sposobu wykonywania** wybierz **ciągłe**.
2. Aby uruchomić lub zatrzymać ciągłe zadanie WebJob, kliknij prawym przyciskiem myszy zadanie WebJob na liście, a następnie kliknij przycisk **Start** lub **zatrzymać**.

> [!NOTE]
> Jeśli aplikacja sieci web jest uruchamiana na więcej niż jedno wystąpienie, stale uruchomione zadanie WebJob będzie działać we wszystkich swoich wystąpień. Uruchom na żądanie i zaplanowanych zadań Webjob w pojedynczym wystąpieniu wybrane do równoważenia obciążenia przy Microsoft Azure.
> 
> Dla ciągłe zadania Webjob do uruchomienia, niezawodne i we wszystkich wystąpieniach, Włącz zawsze włączone * ustawienia konfiguracji dla aplikacji sieci web w przeciwnym razie można zatrzymać działanie w przypadku witryny hosta SCM był bezczynny zbyt długo.
> 
> 

## <a name="CreateScheduledCRON"></a>Utwórz zaplanowane zadanie WebJob przy użyciu wyrażenia usługi CRON
Ta metoda jest dostępna do aplikacji sieci Web działających w trybie podstawowa, standardowa lub Premium i wymaga **zawsze na** ustawienie zostało włączone w aplikacji.

Aby włączyć na żądanie zadania WebJob do zaplanowane zadania WebJob, wystarczy dołączyć `settings.job` pliku w katalogu głównym pliku zip zadania WebJob. Ten plik JSON powinien zawierać `schedule` właściwość o [CRON wyrażenia](https://en.wikipedia.org/wiki/Cron), na przykład poniżej.

Wyrażenie CRON składa się z pola 6: `{second} {minute} {hour} {day} {month} {day of the week}`.

Na przykład, aby wyzwolić WebJob co 15 minut z `settings.job` musi:

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

Inne przykłady CRON harmonogramu:

* Co godzinę (tj. gdy liczba minut wynosi 0):`0 0 * * * *` 
* Co godzinę z 9 AM do 17: 00:`0 0 9-17 * * *` 
* W 9:30 AM codziennie:`0 30 9 * * *`
* W 9:30 AM każdej tydzień:`0 30 9 * * 1-5`

**Uwaga**: wdrażając zadanie WebJob z programu Visual Studio, upewnij się oznaczyć Twojej `settings.job` właściwości pliku jako Kopiuj, jeśli nowszy ".

## <a name="CreateScheduled"></a>Utwórz zaplanowane zadanie WebJob przy użyciu harmonogramu Azure
Następujące techniki alternatywne korzysta z Harmonogram systemu Azure. W takim przypadku WebJob nie ma żadnych bezpośrednich wiedzy harmonogramu. Zamiast tego harmonogramu Azure pobiera skonfigurowane do wyzwolenia WebJob zgodnie z harmonogramem. 

Azure Portal nie ma jeszcze możliwość tworzenia zaplanowanych zadań WebJob, ale dopiero po dodaniu tej funkcji możesz zrobić to za pomocą [klasyczny portal](http://manage.windowsazure.com).

1. W [klasyczny portal](http://manage.windowsazure.com) przejdź do zadania WebJob i kliknij przycisk **Dodaj**.
2. W **sposobu wykonywania** wybierz **uruchamiane zgodnie z harmonogramem**.
   
    ![Nowe zadanie zaplanowane][NewScheduledJob]
3. Wybierz **Region harmonogramu** dla zadania, a następnie kliknij strzałkę w prawym dolnym rogu okna dialogowego, aby przejść do następnego ekranu.
4. W **Utwórz zadanie** okno dialogowe, wybierz typ **cyklu** ma: **jednorazowe zadania** lub **zadania cykliczny**.
   
    ![Harmonogram cyklu][SchdRecurrence]
5. Wybierz również **uruchamianie** czasu: **teraz** lub **w określonym czasie**.
   
    ![Czas rozpoczęcia harmonogramu][SchdStart]
6. Jeśli chcesz uruchomić w określonym czasie, wybierz początkowy wartości czasu w obszarze **uruchamiania na**.
   
    ![Rozpoczęcia harmonogramu w określonym czasie][SchdStartOn]
7. W przypadku wybrania cyklicznych zadań masz **Powtórz co** opcję, aby określić częstotliwość występowania i **kończąc na** opcję, aby określić godzinę zakończenia.
   
    ![Harmonogram cyklu][SchdRecurEvery]
8. Jeśli wybierzesz **tygodni**, można wybrać **na konkretny harmonogram** i określ dni tygodnia, w których zadanie do uruchomienia.
   
    ![Harmonogram dni tygodnia][SchdWeeksOnParticular]
9. Jeśli wybierzesz **miesięcy** i wybierz **na konkretny harmonogram** pole, można ustawić zadanie do działania w szczególności numerowane **dni** w miesiącu. 
   
    ![Harmonogram określonych dat w miesiącu][SchdMonthsOnPartDays]
10. Jeśli wybierzesz **dni tygodnia**, który dzień lub dni tygodnia, można wybrać w miesiącu zadanie do uruchomienia na.
    
     ![Zaplanuj określonym tygodniu dni miesiąca][SchdMonthsOnPartWeekDays]
11. Ponadto umożliwia także **wystąpień** opcję, aby wybrać którym tygodniu miesiąca (pierwszej, drugiej, trzeci itp.) podczas wykonywania zadania do uruchomienia na dni tygodnia, można określić.
    
    ![Zaplanuj dni tygodnia określonego w szczególności tygodnie miesiąca][SchdMonthsOnPartWeekDaysOccurences]
12. Po utworzeniu co najmniej jedno zadanie na karcie zadań Webjob z ich stan, typ harmonogramu i inne informacje pojawi się ich nazw. Informacje historyczne dotyczące 30 ostatnich zadań Webjob jest obsługiwana.
    
    ![Lista zadań][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>Zaplanowane zadania i harmonogram systemu Azure
Zaplanowane zadania można dodatkowo skonfigurować na stronach Harmonogram systemu Azure [klasyczny portal](http://manage.windowsazure.com).

1. Na stronie zadań Webjob kliknij zadanie **harmonogram** łącze, aby przejść do strony portalu Azure harmonogramu. 
   
   ![Łącze do harmonogramu systemu Azure][LinkToScheduler]
2. Na stronie harmonogram kliknij zadanie.
   
    ![Zadania na stronie portalu harmonogramu][SchedulerPortal]
3. **Akcji zadania** strona zostanie otwarta, w którym można dodatkowo skonfigurować zadanie. 
   
    ![Akcja zadania PageInScheduler][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>Wyświetlanie historii zadań
1. Aby wyświetlić historię wykonywania zadania, w tym zadania utworzone przy użyciu zestawu SDK zadań Webjob, kliknij odpowiednie łącze w sekcji **dzienniki** kolumny bloku zadań Webjob. (Aby skopiować adres URL strony pliku dziennika do Schowka w razie potrzeby można użyć ikony Schowka).
   
    ![Łącze dzienników](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. Kliknięcie łącza spowoduje otwarcie strony szczegółów dla zadania WebJob. Ta strona zawiera nazwę polecenia Uruchom został uruchomiony, czas i jego powodzenia lub niepowodzenia. W obszarze **ostatnie zadanie uruchamia**, kliknij, aby zobaczyć więcej informacji.
   
    ![WebJobDetails][WebJobDetails]
3. **Szczegóły uruchomienia zadania WebJob** zostanie wyświetlona strona. Kliknij przycisk **dane wyjściowe Przełącz** tekst zawartość dziennika. Dziennik wyjścia jest w formacie tekstowym. 
   
    ![Szczegóły uruchomienia zadania sieci Web][WebJobRunDetails]
4. Aby wyświetlić tekstu wyjściowego w osobnym oknie przeglądarki, kliknij **Pobierz** łącza. Aby pobrać samego tekstu, kliknij łącze prawym przyciskiem myszy i użyj opcji przeglądarki, aby zapisać zawartość pliku.
   
    ![Pobieranie danych wyjściowych dziennika][DownloadLogOutput]
5. **Webjob** łącze umieszczone u góry strony oferują wygodny sposób na uzyskanie dostępu do listy zadań Webjob na pulpicie nawigacyjnym historii.
   
    ![Link do listy zadań Webjob][WebJobsLinkToDashboardList]
   
    ![Lista zadań Webjob na pulpicie nawigacyjnym historii][WebJobsListInJobsDashboard]
   
    Klikając jedno z poniższych linków, przejście do strony szczegółów zadania WebJob dla wybranego zadania.

## <a name="WHPNotes"></a>Uwagi
* Aplikacje sieci Web w trybie wolnych może upłynął limit czasu po 20 minut, jeśli istnieją żadne żądania do witryny scm (wdrażania) i aplikacji sieci web portalu nie otwierać na platformie Azure. Żądania do rzeczywistej lokacji nie spowoduje zresetowanie to.
* Kod ciągłe zadania trzeba napisać. do uruchamiania w pętli nieskończonej.
* Zadania ciągłego uruchamiaj stale tylko wtedy, gdy aplikacja sieci web jest uruchomiony.
* Podstawowe i oferty standardowe tryby zawsze na funkcji, gdy włączone, uniemożliwia przechodzących do stanu bezczynności aplikacji sieci web.
* Można jedynie debugować pracujące zadań Webjob. Debugowanie zadań Webjob według harmonogramu lub na żądanie nie jest obsługiwane.

## <a name="NextSteps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz [zasobów zalecane zadań Webjob Azure][WebJobsRecommendedResources].

[PSonWebJobs]:http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx
[WebJobsRecommendedResources]:http://go.microsoft.com/fwlink/?LinkId=390226

[OnDemandWebJob]: ./media/web-sites-create-web-jobs/01aOnDemandWebJob.png
[WebJobsList]: ./media/web-sites-create-web-jobs/02aWebJobsList.png
[NewContinuousJob]: ./media/web-sites-create-web-jobs/03aNewContinuousJob.png
[NewScheduledJob]: ./media/web-sites-create-web-jobs/04aNewScheduledJob.png
[SchdRecurrence]: ./media/web-sites-create-web-jobs/05SchdRecurrence.png
[SchdStart]: ./media/web-sites-create-web-jobs/06SchdStart.png
[SchdStartOn]: ./media/web-sites-create-web-jobs/07SchdStartOn.png
[SchdRecurEvery]: ./media/web-sites-create-web-jobs/08SchdRecurEvery.png
[SchdWeeksOnParticular]: ./media/web-sites-create-web-jobs/09SchdWeeksOnParticular.png
[SchdMonthsOnPartDays]: ./media/web-sites-create-web-jobs/10SchdMonthsOnPartDays.png
[SchdMonthsOnPartWeekDays]: ./media/web-sites-create-web-jobs/11SchdMonthsOnPartWeekDays.png
[SchdMonthsOnPartWeekDaysOccurences]: ./media/web-sites-create-web-jobs/12SchdMonthsOnPartWeekDaysOccurences.png
[RunOnce]: ./media/web-sites-create-web-jobs/13RunOnce.png
[WebJobsListWithSeveralJobs]: ./media/web-sites-create-web-jobs/13WebJobsListWithSeveralJobs.png
[WebJobLogs]: ./media/web-sites-create-web-jobs/14WebJobLogs.png
[WebJobDetails]: ./media/web-sites-create-web-jobs/15WebJobDetails.png
[WebJobRunDetails]: ./media/web-sites-create-web-jobs/16WebJobRunDetails.png
[DownloadLogOutput]: ./media/web-sites-create-web-jobs/17DownloadLogOutput.png
[WebJobsLinkToDashboardList]: ./media/web-sites-create-web-jobs/18WebJobsLinkToDashboardList.png
[WebJobsListInJobsDashboard]: ./media/web-sites-create-web-jobs/19WebJobsListInJobsDashboard.png
[LinkToScheduler]: ./media/web-sites-create-web-jobs/31LinkToScheduler.png
[SchedulerPortal]: ./media/web-sites-create-web-jobs/32SchedulerPortal.png
[JobActionPageInScheduler]: ./media/web-sites-create-web-jobs/33JobActionPageInScheduler.png

