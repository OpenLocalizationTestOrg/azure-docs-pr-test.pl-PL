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
# <a name="run-background-tasks-with-webjobs"></a><span data-ttu-id="016dc-103">Uruchamianie zadań w tle za pomocą zadań WebJob</span><span class="sxs-lookup"><span data-stu-id="016dc-103">Run Background tasks with WebJobs</span></span>
## <a name="overview"></a><span data-ttu-id="016dc-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="016dc-104">Overview</span></span>
<span data-ttu-id="016dc-105">Mogą uruchamiać programów lub skryptów, które znajdują się w zadań Webjob w Twojej [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci web na trzy sposoby: na żądanie, w sposób ciągły, lub zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="016dc-105">You can run programs or scripts in WebJobs in your [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web app in three ways: on demand, continuously, or on a schedule.</span></span> <span data-ttu-id="016dc-106">Nie ma żadnych dodatkowych kosztów, aby użyć zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="016dc-106">There is no additional cost to use WebJobs.</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="016dc-107">W tym artykule pokazano, jak wdrażanie przy użyciu zadań Webjob [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="016dc-107">This article shows how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="016dc-108">Aby uzyskać informacje o sposobie wdrażania przy użyciu programu Visual Studio lub proces ciągłego dostarczania, zobacz [sposobu wdrażania zadań Webjob Azure do aplikacji sieci Web](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="016dc-108">For information about how to deploy by using Visual Studio or a continuous delivery process, see [How to Deploy Azure WebJobs to Web Apps](websites-dotnet-deploy-webjobs.md).</span></span>

<span data-ttu-id="016dc-109">Zestaw SDK zadań Webjob Azure upraszcza wiele zadań Webjob zadania programowania.</span><span class="sxs-lookup"><span data-stu-id="016dc-109">The Azure WebJobs SDK simplifies many WebJobs programming tasks.</span></span> <span data-ttu-id="016dc-110">Aby uzyskać więcej informacji, zobacz [co to jest zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="016dc-110">For more information, see [What is the WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

 <span data-ttu-id="016dc-111">Środowisko Azure Functions zapewnia uruchamianie programów i skryptów z niekorzystającą środowiska lub aplikacji usługi app Service w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="016dc-111">Azure Functions provides another way to run programs and scripts from either a serverless environment or from an App Service app.</span></span> <span data-ttu-id="016dc-112">Aby uzyskać więcej informacji, zobacz [Azure Functions — omówienie](../azure-functions/functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="016dc-112">For more information, see [Azure Functions overview](../azure-functions/functions-overview.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="016dc-113"><a name="acceptablefiles"></a>Typy plików akceptowalne dla skryptów lub programów</span><span class="sxs-lookup"><span data-stu-id="016dc-113"><a name="acceptablefiles"></a>Acceptable file types for scripts or programs</span></span>
<span data-ttu-id="016dc-114">Akceptowane są następujące typy plików:</span><span class="sxs-lookup"><span data-stu-id="016dc-114">The following file types are accepted:</span></span>

* <span data-ttu-id="016dc-115">cmd, bat, .exe (przy użyciu cmd systemu windows)</span><span class="sxs-lookup"><span data-stu-id="016dc-115">.cmd, .bat, .exe (using windows cmd)</span></span>
* <span data-ttu-id="016dc-116">ps1 (przy użyciu programu powershell)</span><span class="sxs-lookup"><span data-stu-id="016dc-116">.ps1 (using powershell)</span></span>
* <span data-ttu-id="016dc-117">SH (przy użyciu bash)</span><span class="sxs-lookup"><span data-stu-id="016dc-117">.sh (using bash)</span></span>
* <span data-ttu-id="016dc-118">PHP (za pomocą języka php)</span><span class="sxs-lookup"><span data-stu-id="016dc-118">.php (using php)</span></span>
* <span data-ttu-id="016dc-119">.PY (przy użyciu języka python)</span><span class="sxs-lookup"><span data-stu-id="016dc-119">.py (using python)</span></span>
* <span data-ttu-id="016dc-120">js (przy użyciu węzła)</span><span class="sxs-lookup"><span data-stu-id="016dc-120">.js (using node)</span></span>
* <span data-ttu-id="016dc-121">JAR (przy użyciu języka java)</span><span class="sxs-lookup"><span data-stu-id="016dc-121">.jar (using java)</span></span>

## <span data-ttu-id="016dc-122"><a name="CreateOnDemand"></a>Tworzenie na żądanie zadania WebJob w portalu</span><span class="sxs-lookup"><span data-stu-id="016dc-122"><a name="CreateOnDemand"></a>Create an on demand WebJob in the portal</span></span>
1. <span data-ttu-id="016dc-123">W **aplikacji sieci Web** bloku [Azure Portal](https://portal.azure.com), kliknij przycisk **wszystkie ustawienia > zadań Webjob** pokazanie **Webjob** bloku.</span><span class="sxs-lookup"><span data-stu-id="016dc-123">In the **Web App** blade of the [Azure Portal](https://portal.azure.com), click **All settings > WebJobs** to show the **WebJobs** blade.</span></span>
   
    ![Blok zadania WebJob](./media/web-sites-create-web-jobs/wjblade.png)
2. <span data-ttu-id="016dc-125">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="016dc-125">Click **Add**.</span></span> <span data-ttu-id="016dc-126">**Dodać zadania WebJob** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="016dc-126">The **Add WebJob** dialog appears.</span></span>
   
    ![Dodawanie bloku zadania WebJob](./media/web-sites-create-web-jobs/addwjblade.png)
3. <span data-ttu-id="016dc-128">W obszarze **nazwa**, podaj nazwę dla zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="016dc-128">Under **Name**, provide a name for the WebJob.</span></span> <span data-ttu-id="016dc-129">Nazwa musi rozpoczynać się literą lub cyfrą i nie może zawierać żadnych znaków specjalnych innych niż "-" i "_".</span><span class="sxs-lookup"><span data-stu-id="016dc-129">The name must start with a letter or a number and cannot contain any special characters other than "-" and "_".</span></span>
4. <span data-ttu-id="016dc-130">W **sposobu wykonywania** wybierz **uruchomić na żądanie**.</span><span class="sxs-lookup"><span data-stu-id="016dc-130">In the **How to Run** box, choose **Run on Demand**.</span></span>
5. <span data-ttu-id="016dc-131">W **przekazywanie pliku** polu, kliknij ikonę folderu i przejdź do pliku zip, który zawiera skrypt.</span><span class="sxs-lookup"><span data-stu-id="016dc-131">In the **File Upload** box, click the folder icon and browse to the zip file that contains your script.</span></span> <span data-ttu-id="016dc-132">Plik zip powinien zawierać pliku wykonywalnego (.exe .cmd bat SH, PHP PY i js) oraz wszelkie pliki pomocnicze potrzebne do uruchomienia tego programu lub skryptu.</span><span class="sxs-lookup"><span data-stu-id="016dc-132">The zip file should contain your executable (.exe .cmd .bat .sh .php .py .js) as well as any supporting files needed to run the program or script.</span></span>
6. <span data-ttu-id="016dc-133">Sprawdź **Utwórz** przekazywać skrypt do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="016dc-133">Check **Create** to upload the script to your web app.</span></span> 
   
    <span data-ttu-id="016dc-134">Nazwa określona dla zadania WebJob zostanie wyświetlony na liście w **Webjob** bloku.</span><span class="sxs-lookup"><span data-stu-id="016dc-134">The name you specified for the WebJob appears in the list on the **WebJobs** blade.</span></span>
7. <span data-ttu-id="016dc-135">Aby uruchomić zadania WebJob, kliknij prawym przyciskiem myszy jego nazwę na liście, a następnie kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="016dc-135">To run the WebJob, right-click its name in the list and click **Run**.</span></span>
   
    ![Uruchom zadanie WebJob](./media/web-sites-create-web-jobs/runondemand.png)

## <span data-ttu-id="016dc-137"><a name="CreateContinuous"></a>Tworzenie stale uruchomione zadania WebJob</span><span class="sxs-lookup"><span data-stu-id="016dc-137"><a name="CreateContinuous"></a>Create a continuously running WebJob</span></span>
1. <span data-ttu-id="016dc-138">Aby utworzyć stale wykonywania zadania WebJob, wykonaj te same czynności dla tworzenie zadanie WebJob, które jest uruchamiane jeden raz, ale w **sposobu wykonywania** wybierz **ciągłe**.</span><span class="sxs-lookup"><span data-stu-id="016dc-138">To create a continuously executing WebJob, follow the same steps for creating a WebJob that runs once, but in the **How to Run** box, choose **Continuous**.</span></span>
2. <span data-ttu-id="016dc-139">Aby uruchomić lub zatrzymać ciągłe zadanie WebJob, kliknij prawym przyciskiem myszy zadanie WebJob na liście, a następnie kliknij przycisk **Start** lub **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="016dc-139">To start or stop a continuous WebJob, right-click the WebJob in the list and click **Start** or **Stop**.</span></span>

> [!NOTE]
> <span data-ttu-id="016dc-140">Jeśli aplikacja sieci web jest uruchamiana na więcej niż jedno wystąpienie, stale uruchomione zadanie WebJob będzie działać we wszystkich swoich wystąpień.</span><span class="sxs-lookup"><span data-stu-id="016dc-140">If your web app runs on more than one instance, a continuously running WebJob will run on all of your instances.</span></span> <span data-ttu-id="016dc-141">Uruchom na żądanie i zaplanowanych zadań Webjob w pojedynczym wystąpieniu wybrane do równoważenia obciążenia przy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="016dc-141">On-demand and scheduled WebJobs run on a single instance selected for load balancing by Microsoft Azure.</span></span>
> 
> <span data-ttu-id="016dc-142">Dla ciągłe zadania Webjob do uruchomienia, niezawodne i we wszystkich wystąpieniach, Włącz zawsze włączone * ustawienia konfiguracji dla aplikacji sieci web w przeciwnym razie można zatrzymać działanie w przypadku witryny hosta SCM był bezczynny zbyt długo.</span><span class="sxs-lookup"><span data-stu-id="016dc-142">For Continuous WebJobs to run reliably and on all instances, enable the Always On* configuration setting for the web app otherwise they can stop running when the SCM host site has been idle for too long.</span></span>
> 
> 

## <span data-ttu-id="016dc-143"><a name="CreateScheduledCRON"></a>Utwórz zaplanowane zadanie WebJob przy użyciu wyrażenia usługi CRON</span><span class="sxs-lookup"><span data-stu-id="016dc-143"><a name="CreateScheduledCRON"></a>Create a scheduled WebJob using a CRON expression</span></span>
<span data-ttu-id="016dc-144">Ta metoda jest dostępna do aplikacji sieci Web działających w trybie podstawowa, standardowa lub Premium i wymaga **zawsze na** ustawienie zostało włączone w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="016dc-144">This technique is available to Web Apps running in Basic, Standard or Premium mode, and requires the **Always On** setting to be enabled on the app.</span></span>

<span data-ttu-id="016dc-145">Aby włączyć na żądanie zadania WebJob do zaplanowane zadania WebJob, wystarczy dołączyć `settings.job` pliku w katalogu głównym pliku zip zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="016dc-145">To turn an On Demand WebJob into a scheduled WebJob, simply include a `settings.job` file at the root of your WebJob zip file.</span></span> <span data-ttu-id="016dc-146">Ten plik JSON powinien zawierać `schedule` właściwość o [CRON wyrażenia](https://en.wikipedia.org/wiki/Cron), na przykład poniżej.</span><span class="sxs-lookup"><span data-stu-id="016dc-146">This JSON file should include a `schedule` property with a [CRON expression](https://en.wikipedia.org/wiki/Cron), per example below.</span></span>

<span data-ttu-id="016dc-147">Wyrażenie CRON składa się z pola 6: `{second} {minute} {hour} {day} {month} {day of the week}`.</span><span class="sxs-lookup"><span data-stu-id="016dc-147">The CRON expression is composed of 6 fields: `{second} {minute} {hour} {day} {month} {day of the week}`.</span></span>

<span data-ttu-id="016dc-148">Na przykład, aby wyzwolić WebJob co 15 minut z `settings.job` musi:</span><span class="sxs-lookup"><span data-stu-id="016dc-148">For example, to trigger your WebJob every 15 minutes, your `settings.job` would have:</span></span>

```json
{
    "schedule": "0 */15 * * * *"
}
``` 

<span data-ttu-id="016dc-149">Inne przykłady CRON harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="016dc-149">Other CRON schedule examples:</span></span>

* <span data-ttu-id="016dc-150">Co godzinę (tj. gdy liczba minut wynosi 0):`0 0 * * * *`</span><span class="sxs-lookup"><span data-stu-id="016dc-150">Every hour (i.e. whenever the count of minutes is 0): `0 0 * * * *`</span></span> 
* <span data-ttu-id="016dc-151">Co godzinę z 9 AM do 17: 00:`0 0 9-17 * * *`</span><span class="sxs-lookup"><span data-stu-id="016dc-151">Every hour from 9 AM to 5 PM: `0 0 9-17 * * *`</span></span> 
* <span data-ttu-id="016dc-152">W 9:30 AM codziennie:`0 30 9 * * *`</span><span class="sxs-lookup"><span data-stu-id="016dc-152">At 9:30 AM every day: `0 30 9 * * *`</span></span>
* <span data-ttu-id="016dc-153">W 9:30 AM każdej tydzień:`0 30 9 * * 1-5`</span><span class="sxs-lookup"><span data-stu-id="016dc-153">At 9:30 AM every week day: `0 30 9 * * 1-5`</span></span>

<span data-ttu-id="016dc-154">**Uwaga**: wdrażając zadanie WebJob z programu Visual Studio, upewnij się oznaczyć Twojej `settings.job` właściwości pliku jako Kopiuj, jeśli nowszy ".</span><span class="sxs-lookup"><span data-stu-id="016dc-154">**Note**: when deploying a WebJob from Visual Studio, make sure to mark your `settings.job` file properties as 'Copy if newer'.</span></span>

## <span data-ttu-id="016dc-155"><a name="CreateScheduled"></a>Utwórz zaplanowane zadanie WebJob przy użyciu harmonogramu Azure</span><span class="sxs-lookup"><span data-stu-id="016dc-155"><a name="CreateScheduled"></a>Create a scheduled WebJob using the Azure Scheduler</span></span>
<span data-ttu-id="016dc-156">Następujące techniki alternatywne korzysta z Harmonogram systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="016dc-156">The following alternate technique makes use of the Azure Scheduler.</span></span> <span data-ttu-id="016dc-157">W takim przypadku WebJob nie ma żadnych bezpośrednich wiedzy harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="016dc-157">In this case, your WebJob does not have any direct knowledge of the schedule.</span></span> <span data-ttu-id="016dc-158">Zamiast tego harmonogramu Azure pobiera skonfigurowane do wyzwolenia WebJob zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="016dc-158">Instead, the Azure Scheduler gets configured to trigger your WebJob on a schedule.</span></span> 

<span data-ttu-id="016dc-159">Azure Portal nie ma jeszcze możliwość tworzenia zaplanowanych zadań WebJob, ale dopiero po dodaniu tej funkcji możesz zrobić to za pomocą [klasyczny portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="016dc-159">The Azure Portal doesn't yet have the ability to create a scheduled WebJob, but until that feature is added you can do it by using the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="016dc-160">W [klasyczny portal](http://manage.windowsazure.com) przejdź do zadania WebJob i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="016dc-160">In the [classic portal](http://manage.windowsazure.com) go to the WebJob page and click **Add**.</span></span>
2. <span data-ttu-id="016dc-161">W **sposobu wykonywania** wybierz **uruchamiane zgodnie z harmonogramem**.</span><span class="sxs-lookup"><span data-stu-id="016dc-161">In the **How to Run** box, choose **Run on a schedule**.</span></span>
   
    ![Nowe zadanie zaplanowane][NewScheduledJob]
3. <span data-ttu-id="016dc-163">Wybierz **Region harmonogramu** dla zadania, a następnie kliknij strzałkę w prawym dolnym rogu okna dialogowego, aby przejść do następnego ekranu.</span><span class="sxs-lookup"><span data-stu-id="016dc-163">Choose the **Scheduler Region** for your job, and then click the arrow on the bottom right of the dialog to proceed to the next screen.</span></span>
4. <span data-ttu-id="016dc-164">W **Utwórz zadanie** okno dialogowe, wybierz typ **cyklu** ma: **jednorazowe zadania** lub **zadania cykliczny**.</span><span class="sxs-lookup"><span data-stu-id="016dc-164">In the **Create Job** dialog, choose the type of **Recurrence** you want: **One-time job** or **Recurring job**.</span></span>
   
    ![Harmonogram cyklu][SchdRecurrence]
5. <span data-ttu-id="016dc-166">Wybierz również **uruchamianie** czasu: **teraz** lub **w określonym czasie**.</span><span class="sxs-lookup"><span data-stu-id="016dc-166">Also choose a **Starting** time: **Now** or **At a specific time**.</span></span>
   
    ![Czas rozpoczęcia harmonogramu][SchdStart]
6. <span data-ttu-id="016dc-168">Jeśli chcesz uruchomić w określonym czasie, wybierz początkowy wartości czasu w obszarze **uruchamiania na**.</span><span class="sxs-lookup"><span data-stu-id="016dc-168">If you want to start at a specific time, choose your starting time values under **Starting On**.</span></span>
   
    ![Rozpoczęcia harmonogramu w określonym czasie][SchdStartOn]
7. <span data-ttu-id="016dc-170">W przypadku wybrania cyklicznych zadań masz **Powtórz co** opcję, aby określić częstotliwość występowania i **kończąc na** opcję, aby określić godzinę zakończenia.</span><span class="sxs-lookup"><span data-stu-id="016dc-170">If you chose a recurring job, you have the **Recur Every** option to specify the frequency of occurrence and the **Ending On** option to specify an ending time.</span></span>
   
    ![Harmonogram cyklu][SchdRecurEvery]
8. <span data-ttu-id="016dc-172">Jeśli wybierzesz **tygodni**, można wybrać **na konkretny harmonogram** i określ dni tygodnia, w których zadanie do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="016dc-172">If you choose **Weeks**, you can select the **On a Particular Schedule** box and specify the days of the week that you want the job to run.</span></span>
   
    ![Harmonogram dni tygodnia][SchdWeeksOnParticular]
9. <span data-ttu-id="016dc-174">Jeśli wybierzesz **miesięcy** i wybierz **na konkretny harmonogram** pole, można ustawić zadanie do działania w szczególności numerowane **dni** w miesiącu.</span><span class="sxs-lookup"><span data-stu-id="016dc-174">If you choose **Months** and select the **On a Particular Schedule** box, you can set the job to run on particular numbered **Days** in the month.</span></span> 
   
    ![Harmonogram określonych dat w miesiącu][SchdMonthsOnPartDays]
10. <span data-ttu-id="016dc-176">Jeśli wybierzesz **dni tygodnia**, który dzień lub dni tygodnia, można wybrać w miesiącu zadanie do uruchomienia na.</span><span class="sxs-lookup"><span data-stu-id="016dc-176">If you choose **Week Days**, you can select which day or days of the week in the month you want the job to run on.</span></span>
    
     ![Zaplanuj określonym tygodniu dni miesiąca][SchdMonthsOnPartWeekDays]
11. <span data-ttu-id="016dc-178">Ponadto umożliwia także **wystąpień** opcję, aby wybrać którym tygodniu miesiąca (pierwszej, drugiej, trzeci itp.) podczas wykonywania zadania do uruchomienia na dni tygodnia, można określić.</span><span class="sxs-lookup"><span data-stu-id="016dc-178">Finally, you can also use the **Occurrences** option to choose which week in the month (first, second, third etc.) you want the job to run on the week days you specified.</span></span>
    
    ![Zaplanuj dni tygodnia określonego w szczególności tygodnie miesiąca][SchdMonthsOnPartWeekDaysOccurences]
12. <span data-ttu-id="016dc-180">Po utworzeniu co najmniej jedno zadanie na karcie zadań Webjob z ich stan, typ harmonogramu i inne informacje pojawi się ich nazw.</span><span class="sxs-lookup"><span data-stu-id="016dc-180">After you have created one or more jobs, their names will appear on the WebJobs tab with their status, schedule type, and other information.</span></span> <span data-ttu-id="016dc-181">Informacje historyczne dotyczące 30 ostatnich zadań Webjob jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="016dc-181">Historical information for the last 30  WebJobs is maintained.</span></span>
    
    ![Lista zadań][WebJobsListWithSeveralJobs]

### <span data-ttu-id="016dc-183"><a name="Scheduler"></a>Zaplanowane zadania i harmonogram systemu Azure</span><span class="sxs-lookup"><span data-stu-id="016dc-183"><a name="Scheduler"></a>Scheduled jobs and Azure Scheduler</span></span>
<span data-ttu-id="016dc-184">Zaplanowane zadania można dodatkowo skonfigurować na stronach Harmonogram systemu Azure [klasyczny portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="016dc-184">Scheduled jobs can be further configured in the Azure Scheduler pages of the [classic portal](http://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="016dc-185">Na stronie zadań Webjob kliknij zadanie **harmonogram** łącze, aby przejść do strony portalu Azure harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="016dc-185">On the WebJobs page, click the job's **schedule** link to navigate to the Azure Scheduler portal page.</span></span> 
   
   ![Łącze do harmonogramu systemu Azure][LinkToScheduler]
2. <span data-ttu-id="016dc-187">Na stronie harmonogram kliknij zadanie.</span><span class="sxs-lookup"><span data-stu-id="016dc-187">On the Scheduler page, click the job.</span></span>
   
    ![Zadania na stronie portalu harmonogramu][SchedulerPortal]
3. <span data-ttu-id="016dc-189">**Akcji zadania** strona zostanie otwarta, w którym można dodatkowo skonfigurować zadanie.</span><span class="sxs-lookup"><span data-stu-id="016dc-189">The **Job Action** page opens, where you can further configure the job.</span></span> 
   
    ![Akcja zadania PageInScheduler][JobActionPageInScheduler]

## <span data-ttu-id="016dc-191"><a name="ViewJobHistory"></a>Wyświetlanie historii zadań</span><span class="sxs-lookup"><span data-stu-id="016dc-191"><a name="ViewJobHistory"></a>View the job history</span></span>
1. <span data-ttu-id="016dc-192">Aby wyświetlić historię wykonywania zadania, w tym zadania utworzone przy użyciu zestawu SDK zadań Webjob, kliknij odpowiednie łącze w sekcji **dzienniki** kolumny bloku zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="016dc-192">To view the execution history of a job, including jobs created with the WebJobs SDK, click  its corresponding link under the **Logs** column of the WebJobs blade.</span></span> <span data-ttu-id="016dc-193">(Aby skopiować adres URL strony pliku dziennika do Schowka w razie potrzeby można użyć ikony Schowka).</span><span class="sxs-lookup"><span data-stu-id="016dc-193">(You can use the clipboard icon to copy the URL of the log file page to the clipboard if you wish.)</span></span>
   
    ![Łącze dzienników](./media/web-sites-create-web-jobs/wjbladelogslink.png)
2. <span data-ttu-id="016dc-195">Kliknięcie łącza spowoduje otwarcie strony szczegółów dla zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="016dc-195">Clicking the link opens the details page for the WebJob.</span></span> <span data-ttu-id="016dc-196">Ta strona zawiera nazwę polecenia Uruchom został uruchomiony, czas i jego powodzenia lub niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="016dc-196">This page shows you the name of the command run, the last times it ran, and its success or failure.</span></span> <span data-ttu-id="016dc-197">W obszarze **ostatnie zadanie uruchamia**, kliknij, aby zobaczyć więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="016dc-197">Under **Recent job runs**, click a time to see further details.</span></span>
   
    ![WebJobDetails][WebJobDetails]
3. <span data-ttu-id="016dc-199">**Szczegóły uruchomienia zadania WebJob** zostanie wyświetlona strona.</span><span class="sxs-lookup"><span data-stu-id="016dc-199">The **WebJob Run Details** page appears.</span></span> <span data-ttu-id="016dc-200">Kliknij przycisk **dane wyjściowe Przełącz** tekst zawartość dziennika.</span><span class="sxs-lookup"><span data-stu-id="016dc-200">Click **Toggle Output** to see the text of the log contents.</span></span> <span data-ttu-id="016dc-201">Dziennik wyjścia jest w formacie tekstowym.</span><span class="sxs-lookup"><span data-stu-id="016dc-201">The output log is in text format.</span></span> 
   
    ![Szczegóły uruchomienia zadania sieci Web][WebJobRunDetails]
4. <span data-ttu-id="016dc-203">Aby wyświetlić tekstu wyjściowego w osobnym oknie przeglądarki, kliknij **Pobierz** łącza.</span><span class="sxs-lookup"><span data-stu-id="016dc-203">To see the output text in a separate browser window, click the **download** link.</span></span> <span data-ttu-id="016dc-204">Aby pobrać samego tekstu, kliknij łącze prawym przyciskiem myszy i użyj opcji przeglądarki, aby zapisać zawartość pliku.</span><span class="sxs-lookup"><span data-stu-id="016dc-204">To download the text itself, right-click the link and use your browser options to save the file contents.</span></span>
   
    ![Pobieranie danych wyjściowych dziennika][DownloadLogOutput]
5. <span data-ttu-id="016dc-206">**Webjob** łącze umieszczone u góry strony oferują wygodny sposób na uzyskanie dostępu do listy zadań Webjob na pulpicie nawigacyjnym historii.</span><span class="sxs-lookup"><span data-stu-id="016dc-206">The **WebJobs** link at the top of the page provides a convenient way to get to a list of WebJobs on the history dashboard.</span></span>
   
    ![Link do listy zadań Webjob][WebJobsLinkToDashboardList]
   
    ![Lista zadań Webjob na pulpicie nawigacyjnym historii][WebJobsListInJobsDashboard]
   
    <span data-ttu-id="016dc-209">Klikając jedno z poniższych linków, przejście do strony szczegółów zadania WebJob dla wybranego zadania.</span><span class="sxs-lookup"><span data-stu-id="016dc-209">Clicking one of these links takes you to the WebJob Details page for the job you selected.</span></span>

## <span data-ttu-id="016dc-210"><a name="WHPNotes"></a>Uwagi</span><span class="sxs-lookup"><span data-stu-id="016dc-210"><a name="WHPNotes"></a>Notes</span></span>
* <span data-ttu-id="016dc-211">Aplikacje sieci Web w trybie wolnych może upłynął limit czasu po 20 minut, jeśli istnieją żadne żądania do witryny scm (wdrażania) i aplikacji sieci web portalu nie otwierać na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="016dc-211">Web apps in Free mode can time out after 20 minutes if there are no requests to the scm (deployment) site and the web app's portal is not open in Azure.</span></span> <span data-ttu-id="016dc-212">Żądania do rzeczywistej lokacji nie spowoduje zresetowanie to.</span><span class="sxs-lookup"><span data-stu-id="016dc-212">Requests to the actual site will not reset this.</span></span>
* <span data-ttu-id="016dc-213">Kod ciągłe zadania trzeba napisać. do uruchamiania w pętli nieskończonej.</span><span class="sxs-lookup"><span data-stu-id="016dc-213">Code for a continuous job needs to be written to run in an endless loop.</span></span>
* <span data-ttu-id="016dc-214">Zadania ciągłego uruchamiaj stale tylko wtedy, gdy aplikacja sieci web jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="016dc-214">Continuous jobs run continuously only when the web app is up.</span></span>
* <span data-ttu-id="016dc-215">Podstawowe i oferty standardowe tryby zawsze na funkcji, gdy włączone, uniemożliwia przechodzących do stanu bezczynności aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="016dc-215">Basic and Standard modes offer the Always On feature which, when enabled, prevents web apps from becoming idle.</span></span>
* <span data-ttu-id="016dc-216">Można jedynie debugować pracujące zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="016dc-216">You can only debug continuously running WebJobs.</span></span> <span data-ttu-id="016dc-217">Debugowanie zadań Webjob według harmonogramu lub na żądanie nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="016dc-217">Debugging scheduled or on-demand WebJobs is not supported.</span></span>

## <span data-ttu-id="016dc-218"><a name="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="016dc-218"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="016dc-219">Aby uzyskać więcej informacji, zobacz [zasobów zalecane zadań Webjob Azure][WebJobsRecommendedResources].</span><span class="sxs-lookup"><span data-stu-id="016dc-219">For more information, see [Azure WebJobs Recommended Resources][WebJobsRecommendedResources].</span></span>

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

