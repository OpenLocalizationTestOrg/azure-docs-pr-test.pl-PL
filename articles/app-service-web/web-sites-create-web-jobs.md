---
title: "zadania w tle aaaRun z zadań Webjob"
description: "Dowiedz się, jak jest toorun zadania w tle na platformie Azure aplikacje sieci web."
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
ms.openlocfilehash: 96a3d977a806e7192207f0f4da79dfd248694336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-background-tasks-with-webjobs"></a>Uruchamianie zadań w tle za pomocą zadań WebJob
## <a name="overview"></a>Omówienie
Mogą uruchamiać programów lub skryptów, które znajdują się w zadań Webjob w Twojej [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci web na trzy sposoby: na żądanie, w sposób ciągły, lub zgodnie z harmonogramem. Nie ma żadnych dodatkowych kosztów toouse zadań Webjob.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

W tym artykule opisano, jak hello toodeploy zadań Webjob przy użyciu [Azure Portal](https://portal.azure.com). Aby uzyskać informacje na temat toodeploy za pomocą programu Visual Studio lub proces ciągłego dostarczania, zobacz [jak tooDeploy zadań Webjob Azure tooWeb aplikacji](websites-dotnet-deploy-webjobs.md).

Witaj zestaw SDK zadań Webjob Azure upraszcza wiele zadań programowania zadań Webjob. Aby uzyskać więcej informacji, zobacz [co to jest zestaw SDK zadań Webjob hello](websites-dotnet-webjobs-sdk.md).

 Środowisko Azure Functions zapewnia inny sposób toorun programy i skrypty z niekorzystającą środowiska lub aplikację usługi aplikacji. Aby uzyskać więcej informacji, zobacz [Azure Functions — omówienie](../azure-functions/functions-overview.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="acceptablefiles"></a>Typy plików akceptowalne dla skryptów lub programów
akceptowane są Hello następujące typy plików:

* cmd, bat, .exe (przy użyciu cmd systemu windows)
* ps1 (przy użyciu programu powershell)
* SH (przy użyciu bash)
* PHP (za pomocą języka php)
* .PY (przy użyciu języka python)
* js (przy użyciu węzła)
* JAR (przy użyciu języka java)

## <a name="CreateOnDemand"></a>Tworzenie na żądanie zadania WebJob w portalu hello
1. W hello **aplikacji sieci Web** bloku hello [Azure Portal](https://portal.azure.com), kliknij przycisk **wszystkie ustawienia > zadań Webjob** tooshow hello **Webjob** bloku.
   
    ![Blok zadania WebJob](./media/web-sites-create-web-jobs/wjblade.png)
2. Kliknij pozycję **Dodaj**. Witaj **dodać zadania WebJob** zostanie wyświetlone okno dialogowe.
   
    ![Dodawanie bloku zadania WebJob](./media/web-sites-create-web-jobs/addwjblade.png)
3. W obszarze **nazwa**, podaj nazwę hello zadania WebJob. Witaj nazwa musi zaczynać się literą lub cyfrą i nie może zawierać żadnych znaków specjalnych innych niż "-" i "_".
4. W hello **jak tooRun** wybierz **uruchomić na żądanie**.
5. W hello **przekazywanie pliku** polu, kliknij ikonę folderu hello i Przeglądaj toohello pliku zip, który zawiera skrypt. plik zip Hello powinien zawierać pliku wykonywalnego (.exe .cmd bat SH, PHP PY i js) oraz wszelkie pliki pomocnicze potrzebne toorun hello programu lub skryptu.
6. Sprawdź **Utwórz** aplikacji sieci web tooyour tooupload hello skryptu. 
   
    Hello nazwa określona dla zadania WebJob hello pojawia się na liście hello na powitania **Webjob** bloku.
7. Witaj toorun zadania WebJob, kliknij prawym przyciskiem myszy jej nazwę na powitania listy i kliknij przycisk **Uruchom**.
   
    ![Uruchom zadanie WebJob](./media/web-sites-create-web-jobs/runondemand.png)

## <a name="CreateContinuous"></a>Tworzenie stale uruchomione zadania WebJob
1. toocreate stale wykonywania zadania WebJob, wykonaj hello same kroki dla tworzenie zadanie WebJob, które jest uruchamiane jeden raz, ale w hello **jak tooRun** wybierz **ciągłe**.
2. toostart lub zatrzymania ciągłe zadanie WebJob, kliknij prawym przyciskiem myszy hello zadania WebJob hello listy i kliknij przycisk **Start** lub **zatrzymać**.

> [!NOTE]
> Jeśli aplikacja sieci web jest uruchamiana na więcej niż jedno wystąpienie, stale uruchomione zadanie WebJob będzie działać we wszystkich swoich wystąpień. Uruchom na żądanie i zaplanowanych zadań Webjob w pojedynczym wystąpieniu wybrane do równoważenia obciążenia przy Microsoft Azure.
> 
> W przypadku ciągłe zadania Webjob toorun niezawodne i we wszystkich wystąpieniach włączyć hello zawsze na * ustawienia konfiguracji dla hello aplikacji sieci web w przeciwnym razie można zatrzymać działanie w przypadku witryny hosta SCM hello jest bezczynny zbyt długo.
> 
> 

## <a name="CreateScheduledCRON"></a>Utwórz zaplanowane zadanie WebJob przy użyciu wyrażenia usługi CRON
Ta metoda jest dostępna tooWeb aplikacji działających w trybie podstawowa, standardowa lub Premium i wymaga hello **zawsze na** ustawienie toobe włączona w aplikacji hello.

tooturn na żądanie zadania WebJob do zaplanowane zadania WebJob, wystarczy dołączyć `settings.job` pliku hello głównym pliku zip zadania WebJob. Ten plik JSON powinien zawierać `schedule` właściwość o [CRON wyrażenia](https://en.wikipedia.org/wiki/Cron), na przykład poniżej.

Hello wyrażenie CRON składa się z pola 6: `{second} {minute} {hour} {day} {month} {day of hello week}`.

Na przykład tootrigger WebJob co 15 minut z `settings.job` musi:

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

Inne przykłady CRON harmonogramu:

* Co godzinę (tj. gdy hello liczba minut wynosi 0):`0 0 * * * *` 
* Co godzinę z 9 AM too5 PM:`0 0 9-17 * * *` 
* W 9:30 AM codziennie:`0 30 9 * * *`
* W 9:30 AM każdej tydzień:`0 30 9 * * 1-5`

**Uwaga**: wdrażając zadanie WebJob z programu Visual Studio, upewnij się, że toomark Twojego `settings.job` właściwości pliku jako Kopiuj, jeśli nowszy ".

## <a name="CreateScheduled"></a>Utwórz zaplanowane zadanie WebJob przy użyciu hello Harmonogram systemu Azure
Witaj, następujące techniki alternatywne sprawia, że użycie hello Harmonogram systemu Azure. W takim przypadku WebJob nie ma bezpośredniego znać hello harmonogramu. Zamiast tego hello Azure harmonogramu pobiera skonfigurowanego tootrigger WebJob zgodnie z harmonogramem. 

Azure Portal Hello nie ma jeszcze toocreate możliwości hello zaplanowane zadania WebJob, ale dopiero po dodaniu tej funkcji możesz zrobić to za pomocą hello [klasyczny portal](http://manage.windowsazure.com).

1. W hello [klasyczny portal](http://manage.windowsazure.com) przejdź do strony zadania WebJob toohello i kliknij polecenie **Dodaj**.
2. W hello **jak tooRun** wybierz **uruchamiane zgodnie z harmonogramem**.
   
    ![Nowe zadanie zaplanowane][NewScheduledJob]
3. Wybierz hello **Region harmonogramu** dla zadania, a następnie kliknij strzałkę hello na powitania prawym dolnym rogu hello okna dialogowego tooproceed toohello następnego ekranu.
4. W hello **Utwórz zadanie** okno dialogowe, wybierz typ hello **cyklu** ma: **jednorazowe zadania** lub **zadania cykliczny**.
   
    ![Harmonogram cyklu][SchdRecurrence]
5. Wybierz również **uruchamianie** czasu: **teraz** lub **w określonym czasie**.
   
    ![Czas rozpoczęcia harmonogramu][SchdStart]
6. Jeśli chcesz toostart w określonym czasie, wybierz początkowy wartości czasu w obszarze **uruchamiania na**.
   
    ![Rozpoczęcia harmonogramu w określonym czasie][SchdStartOn]
7. W przypadku wybrania cyklicznych zadań masz hello **Powtórz co** opcję toospecify hello częstotliwości występowania i hello **kończąc na** toospecify opcji Godzina zakończenia.
   
    ![Harmonogram cyklu][SchdRecurEvery]
8. Jeśli wybierzesz **tygodni**, możesz wybrać hello **na konkretny harmonogram** i określ hello dni tygodnia hello, który ma hello toorun zadania.
   
    ![Harmonogram dni tygodnia hello][SchdWeeksOnParticular]
9. Jeśli wybierzesz **miesięcy** i wybierz hello **na konkretny harmonogram** pole, można ustawić toorun zadania hello w szczególności numerowane **dni** w miesiącu hello. 
   
    ![Zaplanuj określonej daty w hello miesiąca][SchdMonthsOnPartDays]
10. Jeśli wybierzesz **dni tygodnia**, który dzień lub dni tygodnia hello można wybrać w miesiącu hello ma hello toorun zadania na.
    
     ![Zaplanuj określonym tygodniu dni miesiąca][SchdMonthsOnPartWeekDays]
11. Na koniec można również użyć hello **wystąpień** toochoose opcji którym tygodniu miesiąca hello (pierwszej, drugiej, trzeci itp.) mają toorun zadania hello na powitania dni tygodnia, można określić.
    
    ![Zaplanuj dni tygodnia określonego w szczególności tygodnie miesiąca][SchdMonthsOnPartWeekDaysOccurences]
12. Po utworzeniu co najmniej jedno zadanie, ich nazwy będą wyświetlane na karcie zadania Webjob hello z ich stanem zaplanować typ i inne informacje. Informacje historyczne na powitania ostatnie 30 zadań Webjob jest obsługiwana.
    
    ![Lista zadań][WebJobsListWithSeveralJobs]

### <a name="Scheduler"></a>Zaplanowane zadania i harmonogram systemu Azure
Zaplanowane zadania można dodatkowo skonfigurować w stronach Harmonogram systemu Azure hello hello [klasyczny portal](http://manage.windowsazure.com).

1. Na stronie zadań Webjob powitania kliknij zadanie hello **harmonogram** strony portalu łącze toonavigate toohello Harmonogram systemu Azure. 
   
   ![Łącze tooAzure harmonogramu][LinkToScheduler]
2. Na stronie harmonogram powitania kliknij hello zadania.
   
    ![Zadania na stronie portalu hello harmonogramu][SchedulerPortal]
3. Witaj **akcji zadania** otwierania, gdzie można dodatkowo skonfigurować zadania hello strony. 
   
    ![Akcja zadania PageInScheduler][JobActionPageInScheduler]

## <a name="ViewJobHistory"></a>Wyświetlanie historii zadań hello
1. historii wykonywania hello tooview zadania, w tym zadania utworzone za pomocą hello zestaw SDK zadań Webjob, kliknij odpowiednie łącze w hello **dzienniki** kolumny hello bloku zadań Webjob. (Możesz użyć hello Schowka toocopy hello adres URL ikony hello dziennika pliku strony toohello Schowka w razie potrzeby.)
   
    ![Łącze dzienników](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. Kliknięcie łącza hello otwiera stronę szczegółów hello hello zadania WebJob. Ten przedstawia strony hello nazwa Uruchom polecenie hello, hello został uruchomiony, czas i jego powodzenia lub niepowodzenia. W obszarze **ostatnie zadanie uruchamia**, kliknij przycisk toosee czasu dalsze szczegóły.
   
    ![WebJobDetails][WebJobDetails]
3. Witaj **szczegóły uruchomienia zadania WebJob** zostanie wyświetlona strona. Kliknij przycisk **dane wyjściowe Przełącz** toosee tekst hello hello zawartość dziennika. Dziennik wyjścia Hello jest w formacie tekstowym. 
   
    ![Szczegóły uruchomienia zadania sieci Web][WebJobRunDetails]
4. tekstu wyjściowego hello toosee w osobnym oknie przeglądarki, kliknij przycisk hello **Pobierz** łącza. toodownload hello tekst, kliknij prawym przyciskiem myszy łącze hello i używać zawartości z przeglądarki opcje toosave hello pliku.
   
    ![Pobieranie danych wyjściowych dziennika][DownloadLogOutput]
5. Witaj **Webjob** łącze u góry strony hello hello zawiera wygodny sposób tooget tooa listę zadań Webjob na pulpicie nawigacyjnym historii hello.
   
    ![Łącze tooWebJobs listy][WebJobsLinkToDashboardList]
   
    ![Lista zadań Webjob na pulpicie nawigacyjnym historii][WebJobsListInJobsDashboard]
   
    Klikając jedno z poniższych linków, przyjmuje się Strona szczegółów zadania WebJob toohello hello zadania, które można wybrać.

## <a name="WHPNotes"></a>Uwagi
* Aplikacje sieci Web w trybie wolnych może upłynął limit czasu po upływie 20 minut, jeśli nie ma żadnych żądań toohello scm (wdrożenie) witryny i aplikacji sieci web hello portal nie jest otwarty na platformie Azure. Żądania toohello lokacji nie spowoduje zresetowanie to.
* Kod dla zadania ciągłego musi toobe napisany toorun w pętli nieskończonej.
* Zadania ciągłego uruchamiaj stale tylko wtedy, gdy aplikacja sieci web hello jest uruchomiony.
* Podstawowa i standardowa tryby oferta hello zawsze na funkcji, które po włączeniu uniemożliwia przechodzących do stanu bezczynności aplikacji sieci web.
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

