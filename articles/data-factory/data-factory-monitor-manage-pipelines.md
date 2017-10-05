---
title: "Monitorowanie i zarządzanie nimi potoki przy użyciu portalu Azure i programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać portalu Azure i programu Azure PowerShell do monitorowania i zarządzania fabryki danych Azure i potoki, które zostały utworzone."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 61bb5379cd94dd00814e14420947e7783999ff0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-azure-portal-and-powershell"></a><span data-ttu-id="459d2-103">Monitorowanie i zarządzanie nimi potoki fabryki danych Azure przy użyciu portalu Azure i programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="459d2-103">Monitor and manage Azure Data Factory pipelines by using the Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="459d2-104">Przy użyciu portalu Azure/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="459d2-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="459d2-105">Przy użyciu monitorowania i zarządzania aplikacjami</span><span class="sxs-lookup"><span data-stu-id="459d2-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="459d2-106">Aplikacja monitorowania i zarządzania zapewnia lepszą obsługę do monitorowania i zarządzania potoki Twoje dane i rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="459d2-106">The monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="459d2-107">Aby uzyskać informacje dotyczące korzystania z aplikacji, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji monitorowanie i zarządzanie](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="459d2-107">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="459d2-108">W tym artykule opisano sposób monitorowania, zarządzania i debugowania z potoków przy użyciu portalu Azure i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="459d2-108">This article describes how to monitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="459d2-109">Artykuł zawiera także informacje o jak tworzyć alerty i bądź na bieżąco o awarii.</span><span class="sxs-lookup"><span data-stu-id="459d2-109">The article also provides information on how to create alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="459d2-110">Potoki i stanów działania</span><span class="sxs-lookup"><span data-stu-id="459d2-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="459d2-111">Za pomocą portalu Azure, możesz:</span><span class="sxs-lookup"><span data-stu-id="459d2-111">By using the Azure portal, you can:</span></span>

* <span data-ttu-id="459d2-112">Wyświetl fabrykę danych jako diagram.</span><span class="sxs-lookup"><span data-stu-id="459d2-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="459d2-113">Przeglądanie działań w potoku.</span><span class="sxs-lookup"><span data-stu-id="459d2-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="459d2-114">Umożliwia wyświetlanie zestawów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="459d2-114">View input and output datasets.</span></span>

<span data-ttu-id="459d2-115">W tej sekcji opisano również sposób przejścia wycinek zestawu danych z jednego stanu do innego stanu.</span><span class="sxs-lookup"><span data-stu-id="459d2-115">This section also describes how a dataset slice transitions from one state to another state.</span></span>   

### <a name="navigate-to-your-data-factory"></a><span data-ttu-id="459d2-116">Przejdź z fabryką danych</span><span class="sxs-lookup"><span data-stu-id="459d2-116">Navigate to your data factory</span></span>
1. <span data-ttu-id="459d2-117">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="459d2-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="459d2-118">Kliknij przycisk **fabryki danych** w menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="459d2-118">Click **Data factories** on the menu on the left.</span></span> <span data-ttu-id="459d2-119">Jeśli nie widzisz, kliknij przycisk **więcej usług >**, a następnie kliknij przycisk **fabryki danych** w obszarze **analizy i analiza** kategorii.</span><span class="sxs-lookup"><span data-stu-id="459d2-119">If you don't see it, click **More services >**, and then click **Data factories** under the **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Przeglądaj wszystkie > fabryki danych](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="459d2-121">Na **fabryki danych** bloku, wybierz fabryki danych, która Cię interesują.</span><span class="sxs-lookup"><span data-stu-id="459d2-121">On the **Data factories** blade, select the data factory that you're interested in.</span></span>

    ![Wybierz usługi fabryka danych](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="459d2-123">Powinna zostać wyświetlona strona główna dla fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="459d2-123">You should see the home page for the data factory.</span></span>

   ![Blok fabryki danych](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="459d2-125">Widok diagramu w fabryce danych</span><span class="sxs-lookup"><span data-stu-id="459d2-125">Diagram view of your data factory</span></span>
<span data-ttu-id="459d2-126">**Diagram** widoku fabryki danych zapewnia jeden szkła monitorować i zarządzać fabryki danych i jego zasoby.</span><span class="sxs-lookup"><span data-stu-id="459d2-126">The **Diagram** view of a data factory provides a single pane of glass to monitor and manage the data factory and its assets.</span></span> <span data-ttu-id="459d2-127">Aby wyświetlić **Diagram** wyświetlić w fabryce danych, kliknij przycisk **Diagram** na stronie głównej dla fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="459d2-127">To see the **Diagram** view of your data factory, click **Diagram** on the home page for the data factory.</span></span>

![Widok diagramu](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="459d2-129">Można powiększać, pomniejszyć, Powiększ do dopasowania, powiększenie do 100%, Zablokuj układ diagramu i automatycznie rozmieszczaj potoki i zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="459d2-129">You can zoom in, zoom out, zoom to fit, zoom to 100%, lock the layout of the diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="459d2-130">Możesz również sprawdzić informacje elementy powiązane dane (to znaczy Pokaż elementy nadrzędne i podrzędne wybranego elementu).</span><span class="sxs-lookup"><span data-stu-id="459d2-130">You can also see the data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="459d2-131">Działania w potoku</span><span class="sxs-lookup"><span data-stu-id="459d2-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="459d2-132">Kliknij prawym przyciskiem myszy potok, a następnie kliknij przycisk **Otwórz potoku** aby zobaczyć wszystkie działania w potoku, wraz z zestawów danych wejściowych i wyjściowych dla działania.</span><span class="sxs-lookup"><span data-stu-id="459d2-132">Right-click the pipeline, and then click **Open pipeline** to see all activities in the pipeline, along with input and output datasets for the activities.</span></span> <span data-ttu-id="459d2-133">Ta funkcja jest przydatne, gdy potoku sieci zawiera więcej niż jedno działanie i chcesz poznać operacyjne elementy powiązane z jednym potoku.</span><span class="sxs-lookup"><span data-stu-id="459d2-133">This feature is useful when your pipeline includes more than one activity and you want to understand the operational lineage of a single pipeline.</span></span>

    ![Menu Otwórz potok](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="459d2-135">Działanie kopiowania w potoku z danych wejściowych i wyjściowych widać w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="459d2-135">In the following example, you see a copy activity in the pipeline with an input and an output.</span></span> 

    ![Działania w potoku](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="459d2-137">Przejdź na powrót do strony głównej fabryki danych, klikając **fabryki danych** łącza w łączach w lewym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="459d2-137">You can navigate back to the home page of the data factory by clicking the **Data factory** link in the breadcrumb at the top-left corner.</span></span>

    ![Przejdź z powrotem do fabryki danych](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-the-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="459d2-139">Wyświetl stan każdego działania w potoku</span><span class="sxs-lookup"><span data-stu-id="459d2-139">View the state of each activity inside a pipeline</span></span>
<span data-ttu-id="459d2-140">Można wyświetlić bieżący stan działania, wyświetlając stan zestawów danych, które są tworzone podczas działania.</span><span class="sxs-lookup"><span data-stu-id="459d2-140">You can view the current state of an activity by viewing the status of any of the datasets that are produced by the activity.</span></span>

<span data-ttu-id="459d2-141">Klikając dwukrotnie **OutputBlobTable** w **Diagram**, zobaczysz wycinków, które są tworzone przez uruchamia innej aktywności w potoku.</span><span class="sxs-lookup"><span data-stu-id="459d2-141">By double-clicking the **OutputBlobTable** in the **Diagram**, you can see all the slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="459d2-142">Można zobaczyć, czy działanie kopiowania został uruchomiony pomyślnie w ciągu ostatnich ośmiu godzin, a wyprodukowanych wycinki **gotowe** stanu.</span><span class="sxs-lookup"><span data-stu-id="459d2-142">You can see that the copy activity ran successfully for the last eight hours and produced the slices in the **Ready** state.</span></span>  

![Stan potoku](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="459d2-144">Wycinków zestaw danych w fabryce danych może mieć jeden z następujących stanów:</span><span class="sxs-lookup"><span data-stu-id="459d2-144">The dataset slices in the data factory can have one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="459d2-145">Stan</span><span class="sxs-lookup"><span data-stu-id="459d2-145">State</span></span></th><th align="left"><span data-ttu-id="459d2-146">Substrat</span><span class="sxs-lookup"><span data-stu-id="459d2-146">Substate</span></span></th><th align="left"><span data-ttu-id="459d2-147">Opis</span><span class="sxs-lookup"><span data-stu-id="459d2-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="459d2-148">Oczekiwanie</span><span class="sxs-lookup"><span data-stu-id="459d2-148">Waiting</span></span></td><td><span data-ttu-id="459d2-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="459d2-149">ScheduleTime</span></span></td><td><span data-ttu-id="459d2-150">Czas nie pochodzą dla uruchomienia wycinka.</span><span class="sxs-lookup"><span data-stu-id="459d2-150">The time hasn't come for the slice to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="459d2-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="459d2-151">DatasetDependencies</span></span></td><td><span data-ttu-id="459d2-152">Zależności strumienia wychodzącego nie są gotowe.</span><span class="sxs-lookup"><span data-stu-id="459d2-152">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="459d2-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="459d2-153">ComputeResources</span></span></td><td><span data-ttu-id="459d2-154">Zasoby obliczeniowe są niedostępne.</span><span class="sxs-lookup"><span data-stu-id="459d2-154">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="459d2-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="459d2-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="459d2-156">Wszystkie wystąpienia działania są zajęte uruchamianiem innych wycinków.</span><span class="sxs-lookup"><span data-stu-id="459d2-156">All the activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="459d2-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="459d2-157">ActivityResume</span></span></td><td><span data-ttu-id="459d2-158">Działanie jest wstrzymane i nie może uruchamiać wycinków, dopóki nie zostanie wznowione działania.</span><span class="sxs-lookup"><span data-stu-id="459d2-158">The activity is paused and can't run the slices until the activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="459d2-159">Spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="459d2-159">Retry</span></span></td><td><span data-ttu-id="459d2-160">Ponawiane wykonania działania.</span><span class="sxs-lookup"><span data-stu-id="459d2-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="459d2-161">Walidacja</span><span class="sxs-lookup"><span data-stu-id="459d2-161">Validation</span></span></td><td><span data-ttu-id="459d2-162">Weryfikacja jeszcze się nie rozpoczął.</span><span class="sxs-lookup"><span data-stu-id="459d2-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="459d2-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="459d2-163">ValidationRetry</span></span></td><td><span data-ttu-id="459d2-164">Sprawdzanie poprawności oczekuje na ponowienie próby.</span><span class="sxs-lookup"><span data-stu-id="459d2-164">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="459d2-165">W toku</span><span class="sxs-lookup"><span data-stu-id="459d2-165">InProgress</span></span></td><td><span data-ttu-id="459d2-166">Sprawdzanie poprawności</span><span class="sxs-lookup"><span data-stu-id="459d2-166">Validating</span></span></td><td><span data-ttu-id="459d2-167">Trwa sprawdzanie poprawności.</span><span class="sxs-lookup"><span data-stu-id="459d2-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="459d2-168">Wycinek jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="459d2-168">The slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="459d2-169">Nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="459d2-169">Failed</span></span></td><td><span data-ttu-id="459d2-170">Upłynął limit czasu</span><span class="sxs-lookup"><span data-stu-id="459d2-170">TimedOut</span></span></td><td><span data-ttu-id="459d2-171">Wykonywanie działania trwało dłużej niż jest dozwolonych przez działanie.</span><span class="sxs-lookup"><span data-stu-id="459d2-171">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="459d2-172">Anulowane</span><span class="sxs-lookup"><span data-stu-id="459d2-172">Canceled</span></span></td><td><span data-ttu-id="459d2-173">Wycinek zostało anulowane przez akcję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="459d2-173">The slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="459d2-174">Walidacja</span><span class="sxs-lookup"><span data-stu-id="459d2-174">Validation</span></span></td><td><span data-ttu-id="459d2-175">Weryfikacja nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="459d2-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="459d2-176">Nie można wygenerować i/lub sprawdzić poprawności wycinka.</span><span class="sxs-lookup"><span data-stu-id="459d2-176">The slice failed to be generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="459d2-177">Gotowe</span><span class="sxs-lookup"><span data-stu-id="459d2-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="459d2-178">Wycinek jest gotowy do użycia.</span><span class="sxs-lookup"><span data-stu-id="459d2-178">The slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="459d2-179">Pominięto</span><span class="sxs-lookup"><span data-stu-id="459d2-179">Skipped</span></span></td><td><span data-ttu-id="459d2-180">Brak</span><span class="sxs-lookup"><span data-stu-id="459d2-180">None</span></span></td><td><span data-ttu-id="459d2-181">Wycinek nie jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="459d2-181">The slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="459d2-182">Brak</span><span class="sxs-lookup"><span data-stu-id="459d2-182">None</span></span></td><td>-</td><td><span data-ttu-id="459d2-183">Wycinek miał poprzednio inny stan, ale został zresetowany.</span><span class="sxs-lookup"><span data-stu-id="459d2-183">A slice used to exist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="459d2-184">Szczegółowe informacje o wycinek można wyświetlić, klikając polecenie wpisu wycinka w **ostatnio zaktualizowano wycinków** bloku.</span><span class="sxs-lookup"><span data-stu-id="459d2-184">You can view the details about a slice by clicking a slice entry on the **Recently Updated Slices** blade.</span></span>

![Szczegóły wycinka](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="459d2-186">Jeśli wykonano wycinka wiele razy, zobacz wielu wierszy **odbywa się działanie** listy.</span><span class="sxs-lookup"><span data-stu-id="459d2-186">If the slice has been executed multiple times, you see multiple rows in the **Activity runs** list.</span></span> <span data-ttu-id="459d2-187">Można wyświetlić szczegółowe informacje o działaniu uruchomić, klikając przycisk Uruchom wpisu w **odbywa się działanie** listy.</span><span class="sxs-lookup"><span data-stu-id="459d2-187">You can view details about an activity run by clicking the run entry in the **Activity runs** list.</span></span> <span data-ttu-id="459d2-188">Lista zawiera wszystkie pliki dziennika, oraz komunikat o błędzie, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="459d2-188">The list shows all the log files, along with an error message if there is one.</span></span> <span data-ttu-id="459d2-189">Ta funkcja jest przydatna do wyświetlania dzienników i debugowania bez konieczności opuszczania fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="459d2-189">This feature is useful to view and debug logs without having to leave your data factory.</span></span>

![Szczegóły uruchamiania działania](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="459d2-191">Jeśli go nie ma **gotowe** stanu, widać wycinków strumienia wychodzącego, które nie są gotowe i blokuje bieżący fragment wykonywanie w **wycinków strumienia wychodzącego, które nie są gotowe** listy.</span><span class="sxs-lookup"><span data-stu-id="459d2-191">If the slice isn't in the **Ready** state, you can see the upstream slices that aren't ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="459d2-192">Ta funkcja jest przydatna, gdy Twoje wycinka **oczekiwania** stanu i chcesz poznać nadrzędnego zależności wycinka oczekuje na.</span><span class="sxs-lookup"><span data-stu-id="459d2-192">This feature is useful when your slice is in **Waiting** state and you want to understand the upstream dependencies that the slice is waiting on.</span></span>

![Niegotowe wycinki strumienia wychodzącego](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="459d2-194">Diagram stanu zestawu danych</span><span class="sxs-lookup"><span data-stu-id="459d2-194">Dataset state diagram</span></span>
<span data-ttu-id="459d2-195">Po wdrożeniu fabryki danych i potoki ma nieprawidłowy okres aktywności, zestaw danych wycinków przejście z jednego stanu do innego.</span><span class="sxs-lookup"><span data-stu-id="459d2-195">After you deploy a data factory and the pipelines have a valid active period, the dataset slices transition from one state to another.</span></span> <span data-ttu-id="459d2-196">Obecnie stanu wycinka następujące na poniższym diagramie stanu:</span><span class="sxs-lookup"><span data-stu-id="459d2-196">Currently, the slice status follows the following state diagram:</span></span>

![Diagram stanu](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="459d2-198">Przepływ zestawu danych stanu przejścia w fabryce danych jest następująca: oczekiwania -> w toku/w toku (sprawdzania) -> gotowe/nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="459d2-198">The dataset state transition flow in data factory is the following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="459d2-199">Wycinek jest uruchamiany w **oczekiwania** stanu oczekiwania na warunki wstępne, które muszą być spełnione, przed rozpoczęciem wykonywania.</span><span class="sxs-lookup"><span data-stu-id="459d2-199">The slice starts in a **Waiting** state, waiting for preconditions to be met before it executes.</span></span> <span data-ttu-id="459d2-200">Następnie działanie rozpoczyna wykonywanie i wycinka przechodzi w stan **w toku** stanu.</span><span class="sxs-lookup"><span data-stu-id="459d2-200">Then, the activity starts executing, and the slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="459d2-201">Wykonanie działania może powodzenie lub niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="459d2-201">The activity execution might succeed or fail.</span></span> <span data-ttu-id="459d2-202">Wycinek jest oznaczony jako **gotowe** lub ****, na podstawie wyniku wykonania.</span><span class="sxs-lookup"><span data-stu-id="459d2-202">The slice is marked as **Ready** or **Failed**, based on the result of the execution.</span></span>

<span data-ttu-id="459d2-203">Można zresetować wycinka tak, aby wrócić do poprzedniej strony z **gotowe** lub **** stan **oczekiwania** stanu.</span><span class="sxs-lookup"><span data-stu-id="459d2-203">You can reset the slice to go back from the **Ready** or **Failed** state to the **Waiting** state.</span></span> <span data-ttu-id="459d2-204">Można również zaznaczyć stanu wycinka do **Pomiń**, które uniemożliwiają działanie z wykonywania i nie przetwarzania wycinka.</span><span class="sxs-lookup"><span data-stu-id="459d2-204">You can also mark the slice state to **Skip**, which prevents the activity from executing and not processing the slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="459d2-205">Wstrzymywanie i wznawianie potoki</span><span class="sxs-lookup"><span data-stu-id="459d2-205">Pause and resume pipelines</span></span>
<span data-ttu-id="459d2-206">Twoje potoki można zarządzać za pomocą programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="459d2-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="459d2-207">Na przykład można wstrzymywać i wznawiać potoki przez uruchomienie polecenia cmdlet programu Azure PowerShell przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="459d2-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="459d2-208">Widok diagramu nie obsługuje wstrzymywanie i wznawianie potoków.</span><span class="sxs-lookup"><span data-stu-id="459d2-208">The diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="459d2-209">Jeśli chcesz użyć interfejsu użytkownika, za pomocą aplikacji monitorowania i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="459d2-209">If you want to use an user interface, use the monitoring and managing application.</span></span> <span data-ttu-id="459d2-210">Aby uzyskać informacje dotyczące korzystania z aplikacji, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji monitorowanie i zarządzanie](data-factory-monitor-manage-app.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="459d2-210">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="459d2-211">Można Wstrzymaj/zawiesić potoki przy użyciu **Suspend-AzureRmDataFactoryPipeline** polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="459d2-211">You can pause/suspend pipelines by using the **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="459d2-212">To polecenie cmdlet jest przydatne, gdy nie chcesz uruchomić z potoków, dopóki problem nie zostanie rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="459d2-212">This cmdlet is useful when you don’t want to run your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="459d2-213">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="459d2-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="459d2-214">Po usunięciu problemu z potoku, można wznowić zawieszonego procesu za pomocą następującego polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="459d2-214">After the issue has been fixed with the pipeline, you can resume the suspended pipeline by running the following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="459d2-215">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="459d2-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="459d2-216">Debugowanie potoki</span><span class="sxs-lookup"><span data-stu-id="459d2-216">Debug pipelines</span></span>
<span data-ttu-id="459d2-217">Fabryka danych Azure zapewnia zaawansowane możliwości debugowania i rozwiązywania problemów z potoków, za pomocą portalu Azure i programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="459d2-217">Azure Data Factory provides rich capabilities for you to debug and troubleshoot pipelines by using the Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="459d2-218">[! Uwaga} jest znacznie łatwiejsze Rozwiązywanie problemów z błędami, za pomocą aplikacji do zarządzania i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="459d2-218">[!NOTE} It is much easier to troubleshot errors using the Monitoring & Management App.</span></span> <span data-ttu-id="459d2-219">Aby uzyskać informacje dotyczące korzystania z aplikacji, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji monitorowanie i zarządzanie](data-factory-monitor-manage-app.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="459d2-219">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="459d2-220">Znaleziono błędów w potoku</span><span class="sxs-lookup"><span data-stu-id="459d2-220">Find errors in a pipeline</span></span>
<span data-ttu-id="459d2-221">W przypadku niepowodzenia uruchomienia działania w potoku zestawu danych, który jest generowany przez potok jest w stanie błędu z powodu błędu.</span><span class="sxs-lookup"><span data-stu-id="459d2-221">If the activity run fails in a pipeline, the dataset that is produced by the pipeline is in an error state because of the failure.</span></span> <span data-ttu-id="459d2-222">Można debugować i rozwiązywanie problemów z fabryki danych Azure przy użyciu następujących metod.</span><span class="sxs-lookup"><span data-stu-id="459d2-222">You can debug and troubleshoot errors in Azure Data Factory by using the following methods.</span></span>

#### <a name="use-the-azure-portal-to-debug-an-error"></a><span data-ttu-id="459d2-223">Debugowanie błędów przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="459d2-223">Use the Azure portal to debug an error</span></span>
1. <span data-ttu-id="459d2-224">Na **tabeli** bloku, kliknij przycisk wycinek problem, który ma **stan** ustawioną ****.</span><span class="sxs-lookup"><span data-stu-id="459d2-224">On the **Table** blade, click the problem slice that has the **Status** set to **Failed**.</span></span>

   ![Blok tabeli z wycinka problem](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="459d2-226">Na **wycinka danych** bloku, kliknij przycisk uruchamiania działania, która nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="459d2-226">On the **Data slice** blade, click the activity run that failed.</span></span>

   ![Wycinek danych z powodu błędu](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="459d2-228">Na **szczegóły uruchomienia działania** bloku, możesz pobrać pliki, które są powiązane z przetwarzaniem HDInsight.</span><span class="sxs-lookup"><span data-stu-id="459d2-228">On the **Activity run details** blade, you can download the files that are associated with the HDInsight processing.</span></span> <span data-ttu-id="459d2-229">Kliknij przycisk **Pobierz** dla stanu/stderr można pobrać pliku dziennika błędów, który zawiera szczegóły dotyczące błędu.</span><span class="sxs-lookup"><span data-stu-id="459d2-229">Click **Download** for Status/stderr to download the error log file that contains details about the error.</span></span>

   ![Działanie Uruchom szczegóły blok z powodu błędu](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-to-debug-an-error"></a><span data-ttu-id="459d2-231">Debugowanie wystąpił błąd przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="459d2-231">Use PowerShell to debug an error</span></span>
1. <span data-ttu-id="459d2-232">Uruchom program **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="459d2-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="459d2-233">Uruchom **Get AzureRmDataFactorySlice** polecenie, aby wyświetlić wycinków i ich Stany.</span><span class="sxs-lookup"><span data-stu-id="459d2-233">Run the **Get-AzureRmDataFactorySlice** command to see the slices and their statuses.</span></span> <span data-ttu-id="459d2-234">Powinny pojawić się wycinek ze statusem ****.</span><span class="sxs-lookup"><span data-stu-id="459d2-234">You should see a slice with the status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="459d2-235">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="459d2-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="459d2-236">Zastąp **StartDateTime** czas rozpoczęcia z potoku.</span><span class="sxs-lookup"><span data-stu-id="459d2-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="459d2-237">Teraz uruchom **Get AzureRmDataFactoryRun** Uruchom polecenie cmdlet, aby uzyskać szczegółowe informacje o działaniach dla wycinka.</span><span class="sxs-lookup"><span data-stu-id="459d2-237">Now, run the **Get-AzureRmDataFactoryRun** cmdlet to get details about the activity run for the slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="459d2-238">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="459d2-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="459d2-239">Wartość StartDateTime jest czas rozpoczęcia wycinka błąd/problem zanotowaną w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="459d2-239">The value of StartDateTime is the start time for the error/problem slice that you noted from the previous step.</span></span> <span data-ttu-id="459d2-240">Daty i godziny należy ująć w podwójny cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="459d2-240">The date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="459d2-241">Powinny pojawić się dane wyjściowe zawierające szczegółowe informacje o błędzie, który jest podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="459d2-241">You should see output with details about the error that is similar to the following:</span></span>

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. <span data-ttu-id="459d2-242">Można uruchomić **AzureRmDataFactoryLog Zapisz** polecenia cmdlet z identyfikatorem Zobacz z danych wyjściowych i pobierania plików dziennika za pomocą **- DownloadLogsoption** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="459d2-242">You can run the **Save-AzureRmDataFactoryLog** cmdlet with the Id value that you see from the output, and download the log files by using the **-DownloadLogsoption** for the cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="459d2-243">Uruchom ponownie błędów w potoku</span><span class="sxs-lookup"><span data-stu-id="459d2-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="459d2-244">Możliwe jest łatwiejsze Rozwiązywanie problemów i ponownie uruchom wycinków nie powiodło się przy użyciu monitorowania & aplikacji do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="459d2-244">It's easier to troubleshoot errors and rerun failed slices by using the Monitoring & Management App.</span></span> <span data-ttu-id="459d2-245">Aby uzyskać informacje dotyczące korzystania z aplikacji, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji monitorowanie i zarządzanie](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="459d2-245">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-the-azure-portal"></a><span data-ttu-id="459d2-246">Korzystanie z witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="459d2-246">Use the Azure portal</span></span>
<span data-ttu-id="459d2-247">Po Rozwiązywanie problemów i debugowanie błędów w potoku, przechodząc do wycinek błąd i klikając, można uruchomić błędów **Uruchom** przycisk paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="459d2-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating to the error slice and clicking the **Run** button on the command bar.</span></span>

![Uruchom ponownie wycinek nie powiodło się](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="459d2-249">W przypadku wycinka Weryfikacja nie powiodła się z powodu błędu zasad (na przykład, jeśli dane są niedostępne), można naprawić błędu i ponownie zweryfikować, klikając **weryfikacji** przycisk paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="459d2-249">In case the slice has failed validation because of a policy failure (for example, if data isn't available), you can fix the failure and validate again by clicking the **Validate** button on the command bar.</span></span>

![Usuń błędy i sprawdzania poprawności](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="459d2-251">Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="459d2-251">Use Azure PowerShell</span></span>
<span data-ttu-id="459d2-252">Uruchom ponownie błędów za pomocą **AzureRmDataFactorySliceStatus zestaw** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="459d2-252">You can rerun failures by using the **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="459d2-253">Zobacz [AzureRmDataFactorySliceStatus zestaw](https://msdn.microsoft.com/library/mt603522.aspx) temat o składni i inne szczegóły dotyczące polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="459d2-253">See the [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about the cmdlet.</span></span>

<span data-ttu-id="459d2-254">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="459d2-254">**Example:**</span></span>

<span data-ttu-id="459d2-255">Poniższy przykład ustawia stan wszystkich wycinki dla tabeli "DAWikiAggregatedData" Oczekiwanie w fabryce danych Azure "WikiADF".</span><span class="sxs-lookup"><span data-stu-id="459d2-255">The following example sets the status of all slices for the table 'DAWikiAggregatedData' to 'Waiting' in the Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="459d2-256">Typ "aktualizacji" ma ustawioną wartość "Parametru UpstreamInPipeline", co oznacza, że stanów każdy wycinek dla tabeli i wszystkie tabele zależne (nadrzędnego) są ustawione na "Oczekiwanie".</span><span class="sxs-lookup"><span data-stu-id="459d2-256">The 'UpdateType' is set to 'UpstreamInPipeline', which means that statuses of each slice for the table and all the dependent (upstream) tables are set to 'Waiting'.</span></span> <span data-ttu-id="459d2-257">Możliwe wartości tego parametru jest "Indywidualny".</span><span class="sxs-lookup"><span data-stu-id="459d2-257">The other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="459d2-258">Tworzenie alertów</span><span class="sxs-lookup"><span data-stu-id="459d2-258">Create alerts</span></span>
<span data-ttu-id="459d2-259">Azure dzienniki zdarzeń użytkownika podczas zasobów platformy Azure (na przykład fabryka danych) jest utworzone, zaktualizować lub usunąć.</span><span class="sxs-lookup"><span data-stu-id="459d2-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="459d2-260">Alerty można tworzyć na te zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="459d2-260">You can create alerts on these events.</span></span> <span data-ttu-id="459d2-261">Fabryka danych służy do przechwytywania różnych metryk i tworzyć alerty na metryki.</span><span class="sxs-lookup"><span data-stu-id="459d2-261">You can use Data Factory to capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="459d2-262">Firma Microsoft zaleca używanie zdarzeń monitorowania w czasie rzeczywistym i metryki w celach historycznych.</span><span class="sxs-lookup"><span data-stu-id="459d2-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="459d2-263">Alerty dotyczące zdarzeń</span><span class="sxs-lookup"><span data-stu-id="459d2-263">Alerts on events</span></span>
<span data-ttu-id="459d2-264">Zdarzenia Azure udostępniają przydatne wgląd w działania wykonywane w zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="459d2-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="459d2-265">Podczas korzystania z fabryki danych Azure, zdarzenia są generowane, gdy:</span><span class="sxs-lookup"><span data-stu-id="459d2-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="459d2-266">Fabryka danych jest utworzone, zaktualizować lub usunąć.</span><span class="sxs-lookup"><span data-stu-id="459d2-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="459d2-267">Przetwarzanie danych (jako "działa") został uruchomiony lub zakończona.</span><span class="sxs-lookup"><span data-stu-id="459d2-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="459d2-268">Klaster usługi HDInsight na żądanie jest utworzone lub usunięte.</span><span class="sxs-lookup"><span data-stu-id="459d2-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="459d2-269">Można tworzyć alerty dotyczące tych zdarzeń użytkownika i skonfigurować je do wysyłania powiadomień e-mail do administratora i coadministrators subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="459d2-269">You can create alerts on these user events and configure them to send email notifications to the administrator and coadministrators of the subscription.</span></span> <span data-ttu-id="459d2-270">Ponadto można określić adresy e-mail dodatkowych użytkowników, którzy chcą otrzymywać powiadomienia pocztą e-mail, gdy są spełnione warunki.</span><span class="sxs-lookup"><span data-stu-id="459d2-270">In addition, you can specify additional email addresses of users who need to receive email notifications when the conditions are met.</span></span> <span data-ttu-id="459d2-271">Ta funkcja jest przydatne, gdy chcesz bądź na bieżąco na błędy i nie chcesz na stałe monitorowanie fabrykę danych.</span><span class="sxs-lookup"><span data-stu-id="459d2-271">This feature is useful when you want to get notified on failures and don’t want to continuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="459d2-272">Obecnie portalu nie wyświetla alerty dotyczące zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="459d2-272">Currently, the portal doesn't show alerts on events.</span></span> <span data-ttu-id="459d2-273">Użyj [zarządzania i monitorowania aplikacji](data-factory-monitor-manage-app.md) Aby wyświetlić wszystkie alerty.</span><span class="sxs-lookup"><span data-stu-id="459d2-273">Use the [Monitoring and Management app](data-factory-monitor-manage-app.md) to see all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="459d2-274">Określ definicję alertu</span><span class="sxs-lookup"><span data-stu-id="459d2-274">Specify an alert definition</span></span>
<span data-ttu-id="459d2-275">Aby określić definicję alertu, należy utworzyć pliku JSON, który opisuje czynności, które chcesz otrzymywać alerty o.</span><span class="sxs-lookup"><span data-stu-id="459d2-275">To specify an alert definition, you create a JSON file that describes the operations that you want to be alerted on.</span></span> <span data-ttu-id="459d2-276">W poniższym przykładzie alert wysyła wiadomość e-mail z powiadomieniem dla operacji RunFinished.</span><span class="sxs-lookup"><span data-stu-id="459d2-276">In the following example, the alert sends an email notification for the RunFinished operation.</span></span> <span data-ttu-id="459d2-277">Na konkretnym wiadomość e-mail z powiadomieniem jest wysyłany, gdy działa w fabryce danych zostało ukończone i uruchomienie nie powiodło się (stan = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="459d2-277">To be specific, an email notification is sent when a run in the data factory has completed and the run has failed (Status = FailedExecution).</span></span>

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of the data slices for the Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

<span data-ttu-id="459d2-278">Możesz usunąć **podstanu** z definicji JSON, jeśli nie chcesz otrzymywać alerty na określony błąd.</span><span class="sxs-lookup"><span data-stu-id="459d2-278">You can remove **subStatus** from the JSON definition if you don’t want to be alerted on a specific failure.</span></span>

<span data-ttu-id="459d2-279">Ten przykład konfiguruje alert dla wszystkich fabryki danych w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="459d2-279">This example sets up the alert for all data factories in your subscription.</span></span> <span data-ttu-id="459d2-280">Jeśli chcesz alert dla fabryki danych, można określić fabryki danych **resourceUri** w **źródła danych**:</span><span class="sxs-lookup"><span data-stu-id="459d2-280">If you want the alert to be set up for a particular data factory, you can specify data factory **resourceUri** in the **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="459d2-281">Poniższa tabela zawiera listę dostępnych operacji i stanów (i podstany).</span><span class="sxs-lookup"><span data-stu-id="459d2-281">The following table provides the list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="459d2-282">Nazwa operacji</span><span class="sxs-lookup"><span data-stu-id="459d2-282">Operation name</span></span> | <span data-ttu-id="459d2-283">Stan</span><span class="sxs-lookup"><span data-stu-id="459d2-283">Status</span></span> | <span data-ttu-id="459d2-284">Podstan</span><span class="sxs-lookup"><span data-stu-id="459d2-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="459d2-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="459d2-285">RunStarted</span></span> |<span data-ttu-id="459d2-286">Rozpoczęto</span><span class="sxs-lookup"><span data-stu-id="459d2-286">Started</span></span> |<span data-ttu-id="459d2-287">Uruchamianie</span><span class="sxs-lookup"><span data-stu-id="459d2-287">Starting</span></span> |
| <span data-ttu-id="459d2-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="459d2-288">RunFinished</span></span> |<span data-ttu-id="459d2-289">Nie powiodło się / powiodło się.</span><span class="sxs-lookup"><span data-stu-id="459d2-289">Failed / Succeeded</span></span> |<span data-ttu-id="459d2-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="459d2-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="459d2-291">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="459d2-291">Succeeded</span></span><br/><br/><span data-ttu-id="459d2-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="459d2-292">FailedExecution</span></span><br/><br/><span data-ttu-id="459d2-293">Upłynął limit czasu</span><span class="sxs-lookup"><span data-stu-id="459d2-293">TimedOut</span></span><br/><br/><span data-ttu-id="459d2-294">< anulowane</span><span class="sxs-lookup"><span data-stu-id="459d2-294"><Canceled</span></span><br/><br/><span data-ttu-id="459d2-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="459d2-295">FailedValidation</span></span><br/><br/><span data-ttu-id="459d2-296">porzucone</span><span class="sxs-lookup"><span data-stu-id="459d2-296">Abandoned</span></span> |
| <span data-ttu-id="459d2-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="459d2-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="459d2-298">Rozpoczęto</span><span class="sxs-lookup"><span data-stu-id="459d2-298">Started</span></span> | |
| <span data-ttu-id="459d2-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="459d2-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="459d2-300">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="459d2-300">Succeeded</span></span> | |
| <span data-ttu-id="459d2-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="459d2-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="459d2-302">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="459d2-302">Succeeded</span></span> | |

<span data-ttu-id="459d2-303">Zobacz [Tworzenie reguły alertu](https://msdn.microsoft.com/library/azure/dn510366.aspx) szczegółowe informacje o elementach JSON, które są używane w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="459d2-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about the JSON elements that are used in the example.</span></span>

#### <a name="deploy-the-alert"></a><span data-ttu-id="459d2-304">Wdrażanie alertu</span><span class="sxs-lookup"><span data-stu-id="459d2-304">Deploy the alert</span></span>
<span data-ttu-id="459d2-305">Aby wdrożyć alert, należy użyć polecenia cmdlet programu Azure PowerShell **AzureRmResourceGroupDeployment nowy**, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="459d2-305">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="459d2-306">Po wdrożenia grupy zasobów zakończyło się pomyślnie, wyświetlona następujące komunikaty:</span><span class="sxs-lookup"><span data-stu-id="459d2-306">After the resource group deployment has finished successfully, you see the following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - The StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts to remove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> <span data-ttu-id="459d2-307">Można użyć [Tworzenie reguły alertu](https://msdn.microsoft.com/library/azure/dn510366.aspx) interfejsu API REST do utworzenia reguły alertu.</span><span class="sxs-lookup"><span data-stu-id="459d2-307">You can use the [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API to create an alert rule.</span></span> <span data-ttu-id="459d2-308">Ładunek JSON jest podobny do formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="459d2-308">The JSON payload is similar to the JSON example.</span></span>  


#### <a name="retrieve-the-list-of-azure-resource-group-deployments"></a><span data-ttu-id="459d2-309">Pobieranie listy wdrożeń grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="459d2-309">Retrieve the list of Azure resource group deployments</span></span>
<span data-ttu-id="459d2-310">Aby pobrać listę wdrożeń grupy wdrożonych zasobów platformy Azure, użyj polecenia cmdlet **Get-AzureRmResourceGroupDeployment**, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="459d2-310">To retrieve the list of deployed Azure resource group deployments, use the cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="459d2-311">Obsługa zdarzeń użytkownika</span><span class="sxs-lookup"><span data-stu-id="459d2-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="459d2-312">Można wyświetlić wszystkie zdarzenia, które są generowane po kliknięciu przycisku **metryki i operacje** kafelka.</span><span class="sxs-lookup"><span data-stu-id="459d2-312">You can see all the events that are generated after clicking the **Metrics and operations** tile.</span></span>

    ![Kafelek metryki i operacje](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="459d2-314">Kliknij przycisk **zdarzenia** Kafelek, aby zobaczyć zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="459d2-314">Click the **Events** tile to see the events.</span></span>

    ![Kafelek zdarzenia](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="459d2-316">Na **zdarzenia** bloku można zobaczyć szczegółowe informacje dotyczące zdarzeń, zdarzeń filtrowane i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="459d2-316">On the **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Blok zdarzenia](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="459d2-318">Kliknij przycisk **operacji** na liście operacji, która powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="459d2-318">Click an **Operation** in the operations list that causes an error.</span></span>

    ![Wybierz operację](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="459d2-320">Kliknij przycisk **błąd** zdarzeń, aby wyświetlić szczegóły dotyczące błędu.</span><span class="sxs-lookup"><span data-stu-id="459d2-320">Click an **Error** event to see details about the error.</span></span>

    ![Błąd zdarzenia](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="459d2-322">Zobacz [poleceń cmdlet Azure wglądu](https://msdn.microsoft.com/library/mt282452.aspx) dla poleceń cmdlet programu PowerShell, który umożliwia dodawanie, pobrać lub usunąć alerty.</span><span class="sxs-lookup"><span data-stu-id="459d2-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use to add, get, or remove alerts.</span></span> <span data-ttu-id="459d2-323">Oto kilka przykładów użycia **Get-AlertRule** polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="459d2-323">Here are a few examples of using the **Get-AlertRule** cmdlet:</span></span>

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of the data slices for the Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

<span data-ttu-id="459d2-324">Uruchom następujące polecenia get-help, aby wyświetlić szczegółowe informacje i przykłady dotyczące polecenia cmdlet Get-AlertRule.</span><span class="sxs-lookup"><span data-stu-id="459d2-324">Run the following get-help commands to see details and examples for the Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="459d2-325">Jeśli zdarzenia Generowanie alertów są widoczne w bloku portalu, ale nie otrzymywać powiadomienia pocztą e-mail, sprawdź, czy adres e-mail, który jest określony jest ustawiony do odbierania wiadomości e-mail od nadawców zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="459d2-325">If you see the alert generation events on the portal blade but you don't receive email notifications, check whether the email address that is specified is set to receive emails from external senders.</span></span> <span data-ttu-id="459d2-326">Wiadomości e-mail alertów może zostały zablokowane przez ustawienia poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="459d2-326">The alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="459d2-327">Alerty dotyczące metryk</span><span class="sxs-lookup"><span data-stu-id="459d2-327">Alerts on metrics</span></span>
<span data-ttu-id="459d2-328">W fabryce danych można przechwytywać różnych metryk i tworzyć alerty na metryki.</span><span class="sxs-lookup"><span data-stu-id="459d2-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="459d2-329">Można monitorować i tworzyć alerty na następujące metryki wycinków w fabryce danych:</span><span class="sxs-lookup"><span data-stu-id="459d2-329">You can monitor and create alerts on the following metrics for the slices in your data factory:</span></span>

* <span data-ttu-id="459d2-330">**Uruchamia nie powiodło się**</span><span class="sxs-lookup"><span data-stu-id="459d2-330">**Failed Runs**</span></span>
* <span data-ttu-id="459d2-331">**Uruchamia się pomyślnie**</span><span class="sxs-lookup"><span data-stu-id="459d2-331">**Successful Runs**</span></span>

<span data-ttu-id="459d2-332">Te metryki są przydatne i ułatwiają zapoznaj się z omówieniem ogólnej nie powiodło się i pomyślne przebiegów w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="459d2-332">These metrics are useful and help you to get an overview of overall failed and successful runs in the data factory.</span></span> <span data-ttu-id="459d2-333">Metryki są emitowane w każdym użyciu uruchomienia wycinka.</span><span class="sxs-lookup"><span data-stu-id="459d2-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="459d2-334">Na początku godzinę, te metryki są agregowane i przypisany do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="459d2-334">At the beginning of the hour, these metrics are aggregated and pushed to your storage account.</span></span> <span data-ttu-id="459d2-335">Aby włączyć metryki, należy skonfigurować konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="459d2-335">To enable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="459d2-336">Włączyć metryki</span><span class="sxs-lookup"><span data-stu-id="459d2-336">Enable metrics</span></span>
<span data-ttu-id="459d2-337">Aby włączyć metryki, kliknij poniższy z **fabryki danych** bloku:</span><span class="sxs-lookup"><span data-stu-id="459d2-337">To enable metrics, click the following from the **Data Factory** blade:</span></span>

<span data-ttu-id="459d2-338">**Monitorowanie** > **Metryka** > **ustawień diagnostycznych** > **diagnostyki**</span><span class="sxs-lookup"><span data-stu-id="459d2-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Łącze diagnostyki](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="459d2-340">Na **diagnostyki** bloku, kliknij przycisk **na**, wybierz konto magazynu i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="459d2-340">On the **Diagnostics** blade, click **On**, select the storage account, and click **Save**.</span></span>

![Diagnostyka bloku](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="459d2-342">Może potrwać do godziny na podstawie metryk, które mają być wyświetlane na **monitorowanie** bloku ponieważ agregacji metryki się stanie, co godzinę.</span><span class="sxs-lookup"><span data-stu-id="459d2-342">It might take up to one hour for the metrics to be visible on the **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="459d2-343">Konfigurowanie alertu na metryk</span><span class="sxs-lookup"><span data-stu-id="459d2-343">Set up an alert on metrics</span></span>
<span data-ttu-id="459d2-344">Kliknij przycisk **fabryki danych metryki** Kafelek:</span><span class="sxs-lookup"><span data-stu-id="459d2-344">Click the **Data Factory metrics** tile:</span></span>

![Kafelek metryki fabryki danych](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="459d2-346">Na **Metryka** bloku, kliknij przycisk **+ Dodaj alert** na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="459d2-346">On the **Metric** blade, click **+ Add alert** on the toolbar.</span></span>
<span data-ttu-id="459d2-347">![Blok metryki fabryki danych > Dodaj alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="459d2-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="459d2-348">Na **dodać regułę alertu** strony, wykonaj następujące czynności, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="459d2-348">On the **Add an alert rule** page, do the following steps, and click **OK**.</span></span>

* <span data-ttu-id="459d2-349">Wprowadź nazwę alertu (przykład: "nie powiodło się alert").</span><span class="sxs-lookup"><span data-stu-id="459d2-349">Enter a name for the alert (example: "failed alert").</span></span>
* <span data-ttu-id="459d2-350">Wprowadź opis alertu (przykład: "Wyślij wiadomość e-mail, gdy wystąpi błąd").</span><span class="sxs-lookup"><span data-stu-id="459d2-350">Enter a description for the alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="459d2-351">Wybierz metrykę (vs "Działa nie powiodło się". "Pomyślne uruchomień").</span><span class="sxs-lookup"><span data-stu-id="459d2-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="459d2-352">Określ warunek i wartość progową.</span><span class="sxs-lookup"><span data-stu-id="459d2-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="459d2-353">Określ czas.</span><span class="sxs-lookup"><span data-stu-id="459d2-353">Specify the period of time.</span></span>
* <span data-ttu-id="459d2-354">Określ, czy do właściciele, współautorzy i czytelnicy powinna być wysyłana wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="459d2-354">Specify whether an email should be sent to owners, contributors, and readers.</span></span>

![Blok metryki fabryki danych > Dodaj regułę alertów](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="459d2-356">Po dodaniu reguły alertu pomyślnie, bloku zostanie zamknięte i zostanie wyświetlony nowy alert na **Metryka** bloku.</span><span class="sxs-lookup"><span data-stu-id="459d2-356">After the alert rule is added successfully, the blade closes and you see the new alert on the **Metric** blade.</span></span>

![Blok metryki fabryki danych > Nowy alert dodane](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="459d2-358">Liczba alertów w powinno również zostać wyświetlone **reguły alertów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="459d2-358">You should also see the number of alerts in the **Alert rules** tile.</span></span> <span data-ttu-id="459d2-359">Kliknij przycisk **reguły alertów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="459d2-359">Click the **Alert rules** tile.</span></span>

![Blok metryki fabryki danych — reguły alertów](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="459d2-361">Na **alerty reguły** bloku, zobacz wszystkie istniejące alerty.</span><span class="sxs-lookup"><span data-stu-id="459d2-361">On the **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="459d2-362">Aby dodać alert, kliknij przycisk **Dodaj alert** na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="459d2-362">To add an alert, click **Add alert** on the toolbar.</span></span>

![Blok reguły alertów](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="459d2-364">Powiadomienia o alertach</span><span class="sxs-lookup"><span data-stu-id="459d2-364">Alert notifications</span></span>
<span data-ttu-id="459d2-365">Reguły alertów spełnia warunek, powinien otrzymywać wiadomość e-mail z informacją, że alert jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="459d2-365">After the alert rule matches the condition, you should get an email that says the alert is activated.</span></span> <span data-ttu-id="459d2-366">Problem został rozwiązany i stan alertu nie jest już zgodny, możesz otrzymywać wiadomości e-mail z informacją, że alert został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="459d2-366">After the issue is resolved and the alert condition doesn’t match anymore, you get an email that says the alert is resolved.</span></span>

<span data-ttu-id="459d2-367">To zachowanie różni się od zdarzenia wysyłania powiadomienia na każdy błąd, który regułę alertu kwalifikuje się do.</span><span class="sxs-lookup"><span data-stu-id="459d2-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="459d2-368">Wdrażanie alerty za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="459d2-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="459d2-369">Alerty dotyczące metryk można wdrożyć w taki sam sposób jak w przypadku zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="459d2-369">You can deploy alerts for metrics the same way that you do for events.</span></span>

<span data-ttu-id="459d2-370">**Definicja alertu**</span><span class="sxs-lookup"><span data-stu-id="459d2-370">**Alert definition**</span></span>

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

<span data-ttu-id="459d2-371">Zastąp *subscriptionId*, *resourceGroupName*, i *dataFactoryName* w przykładzie z odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="459d2-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in the sample with appropriate values.</span></span>

<span data-ttu-id="459d2-372">*metricName* obecnie obsługuje dwie wartości:</span><span class="sxs-lookup"><span data-stu-id="459d2-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="459d2-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="459d2-373">FailedRuns</span></span>
* <span data-ttu-id="459d2-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="459d2-374">SuccessfulRuns</span></span>

<span data-ttu-id="459d2-375">**Wdrażanie alertu**</span><span class="sxs-lookup"><span data-stu-id="459d2-375">**Deploy the alert**</span></span>

<span data-ttu-id="459d2-376">Aby wdrożyć alert, należy użyć polecenia cmdlet programu Azure PowerShell **AzureRmResourceGroupDeployment nowy**, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="459d2-376">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="459d2-377">Powinny pojawić się następujące komunikat po pomyślnym wdrożeniu:</span><span class="sxs-lookup"><span data-stu-id="459d2-377">You should see following message after a successful deployment:</span></span>

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

<span data-ttu-id="459d2-378">Można również użyć **AlertRule Dodaj** polecenia cmdlet, aby wdrożyć zasady alertu.</span><span class="sxs-lookup"><span data-stu-id="459d2-378">You can also use the **Add-AlertRule** cmdlet to deploy an alert rule.</span></span> <span data-ttu-id="459d2-379">Zobacz [AlertRule Dodaj](https://msdn.microsoft.com/library/mt282468.aspx) tematu, aby uzyskać szczegółowe informacje i przykłady.</span><span class="sxs-lookup"><span data-stu-id="459d2-379">See the [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-to-a-different-resource-group-or-subscription"></a><span data-ttu-id="459d2-380">Przenieś fabryki danych do innej grupy zasobów lub subskrypcji</span><span class="sxs-lookup"><span data-stu-id="459d2-380">Move a data factory to a different resource group or subscription</span></span>
<span data-ttu-id="459d2-381">Fabryka danych można przenieść do innej grupie zasobów lub różnych subskrypcji przy użyciu **Przenieś** polecenia paska przycisk na stronie głównej w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="459d2-381">You can move a data factory to a different resource group or a different subscription by using the **Move** command bar button on the home page of your data factory.</span></span>

![Przenieś fabryki danych](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="459d2-383">Można również przenosić powiązanych zasobów (takich jak alerty, które są skojarzone z fabryki danych), wraz z fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="459d2-383">You can also move any related resources (such as alerts that are associated with the data factory), along with the data factory.</span></span>

![Przenoszenie zasobów, okno dialogowe](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
