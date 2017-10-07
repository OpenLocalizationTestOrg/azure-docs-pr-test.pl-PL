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
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="1849d-103">Uruchamianie zadań w tle za pomocą zadań WebJob</span><span class="sxs-lookup"><span data-stu-id="1849d-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="1849d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1849d-104">Overview</span></span>
<span data-ttu-id="1849d-105">Mogą uruchamiać programów lub skryptów, które znajdują się w zadań Webjob w Twojej [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci web na trzy sposoby: na żądanie, w sposób ciągły, lub zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="1849d-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="1849d-106">Nie ma żadnych dodatkowych kosztów toouse zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="1849d-106">There is no additional cost toouse WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="1849d-107">W tym artykule opisano, jak hello toodeploy zadań Webjob przy użyciu [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1849d-107">This article shows how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="1849d-108">Aby uzyskać informacje na temat toodeploy za pomocą programu Visual Studio lub proces ciągłego dostarczania, zobacz [jak tooDeploy zadań Webjob Azure tooWeb aplikacji](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="1849d-108">For information about how toodeploy by using Visual Studio or a continuous delivery process, see [How tooDeploy Azure WebJobs tooWeb Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="1849d-109">Witaj zestaw SDK zadań Webjob Azure upraszcza wiele zadań programowania zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="1849d-109">hello Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="1849d-110">Aby uzyskać więcej informacji, zobacz [co to jest zestaw SDK zadań Webjob hello](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="1849d-110">For more information, see [What is hello WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="1849d-111">Środowisko Azure Functions zapewnia inny sposób toorun programy i skrypty z niekorzystającą środowiska lub aplikację usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1849d-111">Azure Functions provides another way toorun programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="1849d-112">Aby uzyskać więcej informacji, zobacz [Azure Functions — omówienie](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1849d-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="1849d-113"><a name="acceptablefiles"></a>Typy plików akceptowalne dla skryptów lub programów</span><span class="sxs-lookup"><span data-stu-id="1849d-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="1849d-114">akceptowane są Hello następujące typy plików:</span><span class="sxs-lookup"><span data-stu-id="1849d-114">hello following file types are accepted:</span></span>

* <span data-ttu-id="1849d-115">cmd, bat, .exe (przy użyciu cmd systemu windows)</span><span class="sxs-lookup"><span data-stu-id="1849d-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="1849d-116">ps1 (przy użyciu programu powershell)</span><span class="sxs-lookup"><span data-stu-id="1849d-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="1849d-117">SH (przy użyciu bash)</span><span class="sxs-lookup"><span data-stu-id="1849d-117">.sh (using bash)</span></span>
* <span data-ttu-id="1849d-118">PHP (za pomocą języka php)</span><span class="sxs-lookup"><span data-stu-id="1849d-118">.php (using php)</span></span>
* <span data-ttu-id="1849d-119">.PY (przy użyciu języka python)</span><span class="sxs-lookup"><span data-stu-id="1849d-119">.py (using python)</span></span>
* <span data-ttu-id="1849d-120">js (przy użyciu węzła)</span><span class="sxs-lookup"><span data-stu-id="1849d-120">.js (using node)</span></span>
* <span data-ttu-id="1849d-121">JAR (przy użyciu języka java)</span><span class="sxs-lookup"><span data-stu-id="1849d-121">.jar (using java)</span></span>

## <span data-ttu-id="1849d-122"><a name="CreateOnDemand"></a>Tworzenie na żądanie zadania WebJob w portalu hello</span><span class="sxs-lookup"><span data-stu-id="1849d-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in hello portal</span></span>
1. <span data-ttu-id="1849d-123">W hello **aplikacji sieci Web** bloku hello [Azure Portal](https://portal.azure.com), kliknij przycisk **wszystkie ustawienia > zadań Webjob** tooshow hello **Webjob** bloku.</span><span class="sxs-lookup"><span data-stu-id="1849d-123">In hello **Web App** blade of hello [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** tooshow hello **WebJobs** blade.</span></span>
   
    ![Blok zadania WebJob](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="1849d-125">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="1849d-125">Click **Add**.</span></span> <span data-ttu-id="1849d-126">Witaj **dodać zadania WebJob** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="1849d-126">hello **Add WebJob** dialog appears.</span></span>
   
    ![Dodawanie bloku zadania WebJob](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="1849d-128">W obszarze **nazwa**, podaj nazwę hello zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="1849d-128">Under **Name**, provide a name for hello WebJob.</span></span> <span data-ttu-id="1849d-129">Witaj nazwa musi zaczynać się literą lub cyfrą i nie może zawierać żadnych znaków specjalnych innych niż "-" i "_".</span><span class="sxs-lookup"><span data-stu-id="1849d-129">hello name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="1849d-130">W hello **jak tooRun** wybierz **uruchomić na żądanie**.</span><span class="sxs-lookup"><span data-stu-id="1849d-130">In hello **How tooRun** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="1849d-131">W hello **przekazywanie pliku** polu, kliknij ikonę folderu hello i Przeglądaj toohello pliku zip, który zawiera skrypt.</span><span class="sxs-lookup"><span data-stu-id="1849d-131">In hello **File Upload** box, click hello folder icon and browse toohello zip file that contains your script.</span></span> <span data-ttu-id="1849d-132">plik zip Hello powinien zawierać pliku wykonywalnego (.exe .cmd bat SH, PHP PY i js) oraz wszelkie pliki pomocnicze potrzebne toorun hello programu lub skryptu.</span><span class="sxs-lookup"><span data-stu-id="1849d-132">hello zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed toorun hello program or script.</span></span>
6. <span data-ttu-id="1849d-133">Sprawdź **Utwórz** aplikacji sieci web tooyour tooupload hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="1849d-133">Check **Create** tooupload hello script tooyour web app.</span></span> 
   
    <span data-ttu-id="1849d-134">Hello nazwa określona dla zadania WebJob hello pojawia się na liście hello na powitania **Webjob** bloku.</span><span class="sxs-lookup"><span data-stu-id="1849d-134">hello name you specified for hello WebJob appears in hello list on hello **WebJobs** blade.</span></span>
7. <span data-ttu-id="1849d-135">Witaj toorun zadania WebJob, kliknij prawym przyciskiem myszy jej nazwę na powitania listy i kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="1849d-135">toorun hello WebJob, right-click its name in hello list and click **Run**.</span></span>
   
    ![Uruchom zadanie WebJob](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="1849d-137"><a name="CreateContinuous"></a>Tworzenie stale uruchomione zadania WebJob</span><span class="sxs-lookup"><span data-stu-id="1849d-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="1849d-138">toocreate stale wykonywania zadania WebJob, wykonaj hello same kroki dla tworzenie zadanie WebJob, które jest uruchamiane jeden raz, ale w hello **jak tooRun** wybierz **ciągłe**.</span><span class="sxs-lookup"><span data-stu-id="1849d-138">toocreate a continuously executing WebJob, follow hello same steps for creating a WebJob that runs once, but in hello **How tooRun** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="1849d-139">toostart lub zatrzymania ciągłe zadanie WebJob, kliknij prawym przyciskiem myszy hello zadania WebJob hello listy i kliknij przycisk **Start** lub **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="1849d-139">toostart or stop a continuous WebJob, right-click hello WebJob in hello list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="1849d-140">Jeśli aplikacja sieci web jest uruchamiana na więcej niż jedno wystąpienie, stale uruchomione zadanie WebJob będzie działać we wszystkich swoich wystąpień.</span><span class="sxs-lookup"><span data-stu-id="1849d-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="1849d-141">Uruchom na żądanie i zaplanowanych zadań Webjob w pojedynczym wystąpieniu wybrane do równoważenia obciążenia przy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1849d-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="1849d-142">W przypadku ciągłe zadania Webjob toorun niezawodne i we wszystkich wystąpieniach włączyć hello zawsze na * ustawienia konfiguracji dla hello aplikacji sieci web w przeciwnym razie można zatrzymać działanie w przypadku witryny hosta SCM hello jest bezczynny zbyt długo.</span><span class="sxs-lookup"><span data-stu-id="1849d-142">For Continuous WebJobs toorun reliably and on all instances, enable hello Always On* configuration setting for hello web app otherwise they can stop running when hello SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="1849d-143"><a name="CreateScheduledCRON"></a>Utwórz zaplanowane zadanie WebJob przy użyciu wyrażenia usługi CRON</span><span class="sxs-lookup"><span data-stu-id="1849d-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="1849d-144">Ta metoda jest dostępna tooWeb aplikacji działających w trybie podstawowa, standardowa lub Premium i wymaga hello **zawsze na** ustawienie toobe włączona w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1849d-144">This technique is available tooWeb Apps running in Basic, Standard or Premium mode, and requires hello **Always On** setting toobe enabled on hello app.</span></span>

<span data-ttu-id="1849d-145">tooturn na żądanie zadania WebJob do zaplanowane zadania WebJob, wystarczy dołączyć `settings.job` pliku hello głównym pliku zip zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="1849d-145">tooturn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at hello root of your WebJob zip file.</span></span> <span data-ttu-id="1849d-146">Ten plik JSON powinien zawierać `schedule` właściwość o [CRON wyrażenia](https://en.wikipedia.org/wiki/Cron), na przykład poniżej.</span><span class="sxs-lookup"><span data-stu-id="1849d-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="1849d-147">Hello wyrażenie CRON składa się z pola 6: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span><span class="sxs-lookup"><span data-stu-id="1849d-147">hello CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of hello week}`.</span></span>

<span data-ttu-id="1849d-148">Na przykład tootrigger WebJob co 15 minut z `settings.job` musi:</span><span class="sxs-lookup"><span data-stu-id="1849d-148">For example, tootrigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="1849d-149">Inne przykłady CRON harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="1849d-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="1849d-150">Co godzinę (tj. gdy hello liczba minut wynosi 0):`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="1849d-150">Every hour (i.e. whenever hello count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="1849d-151">Co godzinę z 9 AM too5 PM:`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="1849d-151">Every hour from 9 AM too5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="1849d-152">W 9:30 AM codziennie:`0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="1849d-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="1849d-153">W 9:30 AM każdej tydzień:`0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="1849d-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="1849d-154">**Uwaga**: wdrażając zadanie WebJob z programu Visual Studio, upewnij się, że toomark Twojego `settings.job` właściwości pliku jako Kopiuj, jeśli nowszy ".</span><span class="sxs-lookup"><span data-stu-id="1849d-154">**Note**: when deploying a WebJob from Visual Studio, make sure toomark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="1849d-155"><a name="CreateScheduled"></a>Utwórz zaplanowane zadanie WebJob przy użyciu hello Harmonogram systemu Azure</span><span class="sxs-lookup"><span data-stu-id="1849d-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using hello Azure Scheduler</span></span>
<span data-ttu-id="1849d-156">Witaj, następujące techniki alternatywne sprawia, że użycie hello Harmonogram systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="1849d-156">hello following alternate technique makes use of hello Azure Scheduler.</span></span> <span data-ttu-id="1849d-157">W takim przypadku WebJob nie ma bezpośredniego znać hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="1849d-157">In this case, your WebJob does not have any direct knowledge of hello schedule.</span></span> <span data-ttu-id="1849d-158">Zamiast tego hello Azure harmonogramu pobiera skonfigurowanego tootrigger WebJob zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="1849d-158">Instead, hello Azure Scheduler gets configured tootrigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="1849d-159">Azure Portal Hello nie ma jeszcze toocreate możliwości hello zaplanowane zadania WebJob, ale dopiero po dodaniu tej funkcji możesz zrobić to za pomocą hello [klasyczny portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1849d-159">hello Azure Portal doesn't yet have hello ability toocreate a scheduled WebJob, but until that feature is added you can do it by using hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="1849d-160">W hello [klasyczny portal](http://manage.windowsazure.com) przejdź do strony zadania WebJob toohello i kliknij polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="1849d-160">In hello [classic portal](http://manage.windowsazure.com) go toohello WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="1849d-161">W hello **jak tooRun** wybierz **uruchamiane zgodnie z harmonogramem**.</span><span class="sxs-lookup"><span data-stu-id="1849d-161">In hello **How tooRun** box, choose **Run on a schedule**.</span></span>
   
    ![Nowe zadanie zaplanowane][NewScheduledJob]
3. <span data-ttu-id="1849d-163">Wybierz hello **Region harmonogramu** dla zadania, a następnie kliknij strzałkę hello na powitania prawym dolnym rogu hello okna dialogowego tooproceed toohello następnego ekranu.</span><span class="sxs-lookup"><span data-stu-id="1849d-163">Choose hello **Scheduler Region** for your job, and then click hello arrow on hello bottom right of hello dialog tooproceed toohello next screen.</span></span>
4. <span data-ttu-id="1849d-164">W hello **Utwórz zadanie** okno dialogowe, wybierz typ hello **cyklu** ma: **jednorazowe zadania** lub **zadania cykliczny**.</span><span class="sxs-lookup"><span data-stu-id="1849d-164">In hello **Create Job** dialog, choose hello type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Harmonogram cyklu][SchdRecurrence]
5. <span data-ttu-id="1849d-166">Wybierz również **uruchamianie** czasu: **teraz** lub **w określonym czasie**.</span><span class="sxs-lookup"><span data-stu-id="1849d-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Czas rozpoczęcia harmonogramu][SchdStart]
6. <span data-ttu-id="1849d-168">Jeśli chcesz toostart w określonym czasie, wybierz początkowy wartości czasu w obszarze **uruchamiania na**.</span><span class="sxs-lookup"><span data-stu-id="1849d-168">If you want toostart at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Rozpoczęcia harmonogramu w określonym czasie][SchdStartOn]
7. <span data-ttu-id="1849d-170">W przypadku wybrania cyklicznych zadań masz hello **Powtórz co** opcję toospecify hello częstotliwości występowania i hello **kończąc na** toospecify opcji Godzina zakończenia.</span><span class="sxs-lookup"><span data-stu-id="1849d-170">If you chose a recurring job, you have hello **Recur Every** option toospecify hello frequency of occurrence and hello **Ending On** option toospecify an ending time.</span></span>
   
    ![Harmonogram cyklu][SchdRecurEvery]
8. <span data-ttu-id="1849d-172">Jeśli wybierzesz **tygodni**, możesz wybrać hello **na konkretny harmonogram** i określ hello dni tygodnia hello, który ma hello toorun zadania.</span><span class="sxs-lookup"><span data-stu-id="1849d-172">If you choose **Weeks**, you can select hello **On a Particular Schedule** box and specify hello days of hello week that you want hello job toorun.</span></span>
   
    ![Harmonogram dni tygodnia hello][SchdWeeksOnParticular]
9. <span data-ttu-id="1849d-174">Jeśli wybierzesz **miesięcy** i wybierz hello **na konkretny harmonogram** pole, można ustawić toorun zadania hello w szczególności numerowane **dni** w miesiącu hello.</span><span class="sxs-lookup"><span data-stu-id="1849d-174">If you choose **Months** and select hello **On a Particular Schedule** box, you can set hello job toorun on particular numbered **Days** in hello month.</span></span> 
   
    ![Zaplanuj określonej daty w hello miesiąca][SchdMonthsOnPartDays]
10. <span data-ttu-id="1849d-176">Jeśli wybierzesz **dni tygodnia**, który dzień lub dni tygodnia hello można wybrać w miesiącu hello ma hello toorun zadania na.</span><span class="sxs-lookup"><span data-stu-id="1849d-176">If you choose **Week Days**, you can select which day or days of hello week in hello month you want hello job toorun on.</span></span>
    
     ![Zaplanuj określonym tygodniu dni miesiąca][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="1849d-178">Na koniec można również użyć hello **wystąpień** toochoose opcji którym tygodniu miesiąca hello (pierwszej, drugiej, trzeci itp.) mają toorun zadania hello na powitania dni tygodnia, można określić.</span><span class="sxs-lookup"><span data-stu-id="1849d-178">Finally, you can also use hello **Occurrences** option toochoose which week in hello month (first, second, third etc.) you want hello job toorun on hello week days you specified.</span></span>
    
    ![Zaplanuj dni tygodnia określonego w szczególności tygodnie miesiąca][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="1849d-180">Po utworzeniu co najmniej jedno zadanie, ich nazwy będą wyświetlane na karcie zadania Webjob hello z ich stanem zaplanować typ i inne informacje.</span><span class="sxs-lookup"><span data-stu-id="1849d-180">After you have created one or more jobs, their names will appear on hello WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="1849d-181">Informacje historyczne na powitania ostatnie 30 zadań Webjob jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="1849d-181">Historical information for hello last 30  WebJobs is maintained.</span></span>
    
    ![Lista zadań][WebJobsListWithSeveralJobs]

### <span data-ttu-id="1849d-183"><a name="Scheduler"></a>Zaplanowane zadania i harmonogram systemu Azure</span><span class="sxs-lookup"><span data-stu-id="1849d-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="1849d-184">Zaplanowane zadania można dodatkowo skonfigurować w stronach Harmonogram systemu Azure hello hello [klasyczny portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="1849d-184">Scheduled jobs can be further configured in hello Azure Scheduler pages of hello [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="1849d-185">Na stronie zadań Webjob powitania kliknij zadanie hello **harmonogram** strony portalu łącze toonavigate toohello Harmonogram systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="1849d-185">On hello WebJobs page, click hello job's **schedule** link toonavigate toohello Azure Scheduler portal page.</span></span> 
   
   ![Łącze tooAzure harmonogramu][LinkToScheduler]
2. <span data-ttu-id="1849d-187">Na stronie harmonogram powitania kliknij hello zadania.</span><span class="sxs-lookup"><span data-stu-id="1849d-187">On hello Scheduler page, click hello job.</span></span>
   
    ![Zadania na stronie portalu hello harmonogramu][SchedulerPortal]
3. <span data-ttu-id="1849d-189">Witaj **akcji zadania** otwierania, gdzie można dodatkowo skonfigurować zadania hello strony.</span><span class="sxs-lookup"><span data-stu-id="1849d-189">hello **Job Action** page opens, where you can further configure hello job.</span></span> 
   
    ![Akcja zadania PageInScheduler][JobActionPageInScheduler]

## <span data-ttu-id="1849d-191"><a name="ViewJobHistory"></a>Wyświetlanie historii zadań hello</span><span class="sxs-lookup"><span data-stu-id="1849d-191"><a name="ViewJobHistory"></a>View hello job history</span></span>
1. <span data-ttu-id="1849d-192">historii wykonywania hello tooview zadania, w tym zadania utworzone za pomocą hello zestaw SDK zadań Webjob, kliknij odpowiednie łącze w hello **dzienniki** kolumny hello bloku zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="1849d-192">tooview hello execution history of a job, including jobs created with hello WebJobs SDK, click  its corresponding link under hello **Logs** column of hello WebJobs blade.</span></span> <span data-ttu-id="1849d-193">(Możesz użyć hello Schowka toocopy hello adres URL ikony hello dziennika pliku strony toohello Schowka w razie potrzeby.)</span><span class="sxs-lookup"><span data-stu-id="1849d-193">(You can use hello clipboard icon toocopy hello URL of hello log file page toohello clipboard if you wish.)</span></span>
   
    ![Łącze dzienników](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="1849d-195">Kliknięcie łącza hello otwiera stronę szczegółów hello hello zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="1849d-195">Clicking hello link opens hello details page for hello WebJob.</span></span> <span data-ttu-id="1849d-196">Ten przedstawia strony hello nazwa Uruchom polecenie hello, hello został uruchomiony, czas i jego powodzenia lub niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="1849d-196">This page shows you hello name of hello command run, hello last times it ran, and its success or failure.</span></span> <span data-ttu-id="1849d-197">W obszarze **ostatnie zadanie uruchamia**, kliknij przycisk toosee czasu dalsze szczegóły.</span><span class="sxs-lookup"><span data-stu-id="1849d-197">Under **Recent job runs**, click a time toosee further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="1849d-199">Witaj **szczegóły uruchomienia zadania WebJob** zostanie wyświetlona strona.</span><span class="sxs-lookup"><span data-stu-id="1849d-199">hello **WebJob Run Details** page appears.</span></span> <span data-ttu-id="1849d-200">Kliknij przycisk **dane wyjściowe Przełącz** toosee tekst hello hello zawartość dziennika.</span><span class="sxs-lookup"><span data-stu-id="1849d-200">Click **Toggle Output** toosee hello text of hello log contents.</span></span> <span data-ttu-id="1849d-201">Dziennik wyjścia Hello jest w formacie tekstowym.</span><span class="sxs-lookup"><span data-stu-id="1849d-201">hello output log is in text format.</span></span> 
   
    ![Szczegóły uruchomienia zadania sieci Web][WebJobRunDetails]
4. <span data-ttu-id="1849d-203">tekstu wyjściowego hello toosee w osobnym oknie przeglądarki, kliknij przycisk hello **Pobierz** łącza.</span><span class="sxs-lookup"><span data-stu-id="1849d-203">toosee hello output text in a separate browser window, click hello **download** link.</span></span> <span data-ttu-id="1849d-204">toodownload hello tekst, kliknij prawym przyciskiem myszy łącze hello i używać zawartości z przeglądarki opcje toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="1849d-204">toodownload hello text itself, right-click hello link and use your browser options toosave hello file contents.</span></span>
   
    ![Pobieranie danych wyjściowych dziennika][DownloadLogOutput]
5. <span data-ttu-id="1849d-206">Witaj **Webjob** łącze u góry strony hello hello zawiera wygodny sposób tooget tooa listę zadań Webjob na pulpicie nawigacyjnym historii hello.</span><span class="sxs-lookup"><span data-stu-id="1849d-206">hello **WebJobs** link at hello top of hello page provides a convenient way tooget tooa list of WebJobs on hello history dashboard.</span></span>
   
    ![Łącze tooWebJobs listy][WebJobsLinkToDashboardList]
   
    ![Lista zadań Webjob na pulpicie nawigacyjnym historii][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="1849d-209">Klikając jedno z poniższych linków, przyjmuje się Strona szczegółów zadania WebJob toohello hello zadania, które można wybrać.</span><span class="sxs-lookup"><span data-stu-id="1849d-209">Clicking one of these links takes you toohello WebJob Details page for hello job you selected.</span></span>

## <span data-ttu-id="1849d-210"><a name="WHPNotes"></a>Uwagi</span><span class="sxs-lookup"><span data-stu-id="1849d-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="1849d-211">Aplikacje sieci Web w trybie wolnych może upłynął limit czasu po upływie 20 minut, jeśli nie ma żadnych żądań toohello scm (wdrożenie) witryny i aplikacji sieci web hello portal nie jest otwarty na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1849d-211">Web apps in Free mode can time out after 20 minutes if there are no requests toohello scm (deployment) site and hello web app's portal is not open in Azure.</span></span> <span data-ttu-id="1849d-212">Żądania toohello lokacji nie spowoduje zresetowanie to.</span><span class="sxs-lookup"><span data-stu-id="1849d-212">Requests toohello actual site will not reset this.</span></span>
* <span data-ttu-id="1849d-213">Kod dla zadania ciągłego musi toobe napisany toorun w pętli nieskończonej.</span><span class="sxs-lookup"><span data-stu-id="1849d-213">Code for a continuous job needs toobe written toorun in an endless loop.</span></span>
* <span data-ttu-id="1849d-214">Zadania ciągłego uruchamiaj stale tylko wtedy, gdy aplikacja sieci web hello jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="1849d-214">Continuous jobs run continuously only when hello web app is up.</span></span>
* <span data-ttu-id="1849d-215">Podstawowa i standardowa tryby oferta hello zawsze na funkcji, które po włączeniu uniemożliwia przechodzących do stanu bezczynności aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1849d-215">Basic and Standard modes offer hello Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="1849d-216">Można jedynie debugować pracujące zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="1849d-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="1849d-217">Debugowanie zadań Webjob według harmonogramu lub na żądanie nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="1849d-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="1849d-218"><a name="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1849d-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="1849d-219">Aby uzyskać więcej informacji, zobacz [zasobów zalecane zadań Webjob Azure][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="1849d-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

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

