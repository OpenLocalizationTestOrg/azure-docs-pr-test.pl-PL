---
title: "aaaMonitor oraz zarządzanie nimi potoki hello portalu Azure i programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello portalu Azure i toomonitor programu Azure PowerShell i zarządzanie hello fabryki danych Azure i potoki, które zostały utworzone."
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
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a><span data-ttu-id="213c7-103">Monitorowanie i zarządzanie nimi potoki fabryki danych Azure przy użyciu programu PowerShell i hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="213c7-103">Monitor and manage Azure Data Factory pipelines by using hello Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="213c7-104">Przy użyciu portalu Azure/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="213c7-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="213c7-105">Przy użyciu monitorowania i zarządzania aplikacjami</span><span class="sxs-lookup"><span data-stu-id="213c7-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="213c7-106">Aplikacja Hello monitorowanie i zarządzanie zapewnia lepszą obsługę do monitorowania i zarządzania potoki Twoje dane i rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="213c7-106">hello monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="213c7-107">Aby uzyskać informacje dotyczące korzystania z aplikacji hello, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji hello monitorowanie i zarządzanie](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="213c7-107">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="213c7-108">W tym artykule opisano sposób toomonitor, zarządzania i debugowania z potoków przy użyciu portalu Azure i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="213c7-108">This article describes how toomonitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="213c7-109">Witaj artykuł zawiera również informacje dotyczące sposobu toocreate alertów i pobrać powiadamiany o niepowodzeniach.</span><span class="sxs-lookup"><span data-stu-id="213c7-109">hello article also provides information on how toocreate alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="213c7-110">Potoki i stanów działania</span><span class="sxs-lookup"><span data-stu-id="213c7-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="213c7-111">Za pomocą hello portalu Azure, możesz:</span><span class="sxs-lookup"><span data-stu-id="213c7-111">By using hello Azure portal, you can:</span></span>

* <span data-ttu-id="213c7-112">Wyświetl fabrykę danych jako diagram.</span><span class="sxs-lookup"><span data-stu-id="213c7-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="213c7-113">Przeglądanie działań w potoku.</span><span class="sxs-lookup"><span data-stu-id="213c7-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="213c7-114">Umożliwia wyświetlanie zestawów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="213c7-114">View input and output datasets.</span></span>

<span data-ttu-id="213c7-115">W tej sekcji opisano również sposób przejścia wycinek zestawu danych z jednego stanu tooanother.</span><span class="sxs-lookup"><span data-stu-id="213c7-115">This section also describes how a dataset slice transitions from one state tooanother state.</span></span>   

### <a name="navigate-tooyour-data-factory"></a><span data-ttu-id="213c7-116">Przejdź tooyour fabryki danych</span><span class="sxs-lookup"><span data-stu-id="213c7-116">Navigate tooyour data factory</span></span>
1. <span data-ttu-id="213c7-117">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="213c7-117">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="213c7-118">Kliknij przycisk **fabryki danych** menu hello powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="213c7-118">Click **Data factories** on hello menu on hello left.</span></span> <span data-ttu-id="213c7-119">Jeśli nie widzisz, kliknij przycisk **więcej usług >**, a następnie kliknij przycisk **fabryki danych** w obszarze hello **analizy i analiza** kategorii.</span><span class="sxs-lookup"><span data-stu-id="213c7-119">If you don't see it, click **More services >**, and then click **Data factories** under hello **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Przeglądaj wszystkie > fabryki danych](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="213c7-121">Na powitania **fabryki danych** bloku, wybierz hello fabryki danych, która Cię.</span><span class="sxs-lookup"><span data-stu-id="213c7-121">On hello **Data factories** blade, select hello data factory that you're interested in.</span></span>

    ![Wybierz usługi fabryka danych](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="213c7-123">Powinna zostać wyświetlona strona główna hello hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="213c7-123">You should see hello home page for hello data factory.</span></span>

   ![Blok fabryki danych](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="213c7-125">Widok diagramu w fabryce danych</span><span class="sxs-lookup"><span data-stu-id="213c7-125">Diagram view of your data factory</span></span>
<span data-ttu-id="213c7-126">Witaj **Diagram** widok fabryki danych zapewnia jeden z toomonitor szkła i zarządzanie hello fabryki danych i jego zasoby.</span><span class="sxs-lookup"><span data-stu-id="213c7-126">hello **Diagram** view of a data factory provides a single pane of glass toomonitor and manage hello data factory and its assets.</span></span> <span data-ttu-id="213c7-127">Witaj toosee **Diagram** wyświetlić w fabryce danych, kliknij przycisk **Diagram** na stronie głównej hello hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="213c7-127">toosee hello **Diagram** view of your data factory, click **Diagram** on hello home page for hello data factory.</span></span>

![Widok diagramu](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="213c7-129">Można powiększać, pomniejszyć toofit powiększenia, powiększenia too100%, blokady hello układu diagramu hello i automatycznie rozmieszczaj potoki i zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="213c7-129">You can zoom in, zoom out, zoom toofit, zoom too100%, lock hello layout of hello diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="213c7-130">Możesz również sprawdzić hello danych elementy powiązane informacje (to znaczy Pokaż elementy nadrzędne i podrzędne wybranego elementu).</span><span class="sxs-lookup"><span data-stu-id="213c7-130">You can also see hello data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="213c7-131">Działania w potoku</span><span class="sxs-lookup"><span data-stu-id="213c7-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="213c7-132">Kliknij prawym przyciskiem myszy hello potok, a następnie kliknij przycisk **Otwórz potoku** toosee wszystkie działania w hello w potoku, wraz z zestawów danych wejściowych i wyjściowych dla działania hello.</span><span class="sxs-lookup"><span data-stu-id="213c7-132">Right-click hello pipeline, and then click **Open pipeline** toosee all activities in hello pipeline, along with input and output datasets for hello activities.</span></span> <span data-ttu-id="213c7-133">Ta funkcja jest przydatna w przypadku potoku sieci zawiera więcej niż jedno działanie toounderstand hello operacyjne elementy powiązane z pojedynczy potok.</span><span class="sxs-lookup"><span data-stu-id="213c7-133">This feature is useful when your pipeline includes more than one activity and you want toounderstand hello operational lineage of a single pipeline.</span></span>

    ![Menu Otwórz potok](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="213c7-135">Poniższy przykład hello jest widoczny działanie kopiowania w potoku hello z danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="213c7-135">In hello following example, you see a copy activity in hello pipeline with an input and an output.</span></span> 

    ![Działania w potoku](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="213c7-137">Strona główna toohello wstecz hello fabryki danych można przejść, klikając hello **fabryki danych** łącze w nadrzędnych hello na powitania lewego górnego rogu.</span><span class="sxs-lookup"><span data-stu-id="213c7-137">You can navigate back toohello home page of hello data factory by clicking hello **Data factory** link in hello breadcrumb at hello top-left corner.</span></span>

    ![Przejdź wstecz toodata fabryki](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="213c7-139">Widok stanu hello każdego działania w potoku</span><span class="sxs-lookup"><span data-stu-id="213c7-139">View hello state of each activity inside a pipeline</span></span>
<span data-ttu-id="213c7-140">Można wyświetlić hello bieżący stan działania, wyświetlając stan hello dowolnego hello zestawów danych, które są generowane przez działanie hello.</span><span class="sxs-lookup"><span data-stu-id="213c7-140">You can view hello current state of an activity by viewing hello status of any of hello datasets that are produced by hello activity.</span></span>

<span data-ttu-id="213c7-141">Klikając dwukrotnie hello **OutputBlobTable** w hello **Diagram**, można wyświetlić wszystkie fragmenty hello, które są tworzone przez uruchamia innej aktywności w potoku.</span><span class="sxs-lookup"><span data-stu-id="213c7-141">By double-clicking hello **OutputBlobTable** in hello **Diagram**, you can see all hello slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="213c7-142">Widoczne czy działanie kopiowania hello został uruchomiony pomyślnie na powitania ostatnich ośmiu godzinach i wyprodukowanych hello wycinki hello **gotowe** stanu.</span><span class="sxs-lookup"><span data-stu-id="213c7-142">You can see that hello copy activity ran successfully for hello last eight hours and produced hello slices in hello **Ready** state.</span></span>  

![Stan potoku hello](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="213c7-144">Witaj wycinków zestaw danych w fabryce danych hello może mieć jeden z hello następujące stany:</span><span class="sxs-lookup"><span data-stu-id="213c7-144">hello dataset slices in hello data factory can have one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="213c7-145">Stan</span><span class="sxs-lookup"><span data-stu-id="213c7-145">State</span></span></th><th align="left"><span data-ttu-id="213c7-146">Substrat</span><span class="sxs-lookup"><span data-stu-id="213c7-146">Substate</span></span></th><th align="left"><span data-ttu-id="213c7-147">Opis</span><span class="sxs-lookup"><span data-stu-id="213c7-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="213c7-148">Oczekiwanie</span><span class="sxs-lookup"><span data-stu-id="213c7-148">Waiting</span></span></td><td><span data-ttu-id="213c7-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="213c7-149">ScheduleTime</span></span></td><td><span data-ttu-id="213c7-150">czas Hello nie pochodzą dla hello toorun wycinka.</span><span class="sxs-lookup"><span data-stu-id="213c7-150">hello time hasn't come for hello slice toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="213c7-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="213c7-151">DatasetDependencies</span></span></td><td><span data-ttu-id="213c7-152">zależności strumienia wychodzącego Hello nie są gotowe.</span><span class="sxs-lookup"><span data-stu-id="213c7-152">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="213c7-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="213c7-153">ComputeResources</span></span></td><td><span data-ttu-id="213c7-154">zasoby obliczeniowe Hello nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="213c7-154">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="213c7-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="213c7-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="213c7-156">Wszystkie wystąpienia działania hello są zajęte uruchamianiem innych wycinków.</span><span class="sxs-lookup"><span data-stu-id="213c7-156">All hello activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="213c7-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="213c7-157">ActivityResume</span></span></td><td><span data-ttu-id="213c7-158">działanie Hello jest wstrzymane i nie można uruchomić hello wycinków, dopóki nie zostanie wznowione hello działania.</span><span class="sxs-lookup"><span data-stu-id="213c7-158">hello activity is paused and can't run hello slices until hello activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="213c7-159">Spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="213c7-159">Retry</span></span></td><td><span data-ttu-id="213c7-160">Ponawiane wykonania działania.</span><span class="sxs-lookup"><span data-stu-id="213c7-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="213c7-161">Walidacja</span><span class="sxs-lookup"><span data-stu-id="213c7-161">Validation</span></span></td><td><span data-ttu-id="213c7-162">Weryfikacja jeszcze się nie rozpoczął.</span><span class="sxs-lookup"><span data-stu-id="213c7-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="213c7-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="213c7-163">ValidationRetry</span></span></td><td><span data-ttu-id="213c7-164">Sprawdzanie poprawności jest ponowione toobe oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="213c7-164">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="213c7-165">W toku</span><span class="sxs-lookup"><span data-stu-id="213c7-165">InProgress</span></span></td><td><span data-ttu-id="213c7-166">Sprawdzanie poprawności</span><span class="sxs-lookup"><span data-stu-id="213c7-166">Validating</span></span></td><td><span data-ttu-id="213c7-167">Trwa sprawdzanie poprawności.</span><span class="sxs-lookup"><span data-stu-id="213c7-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="213c7-168">Witaj wycinek jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="213c7-168">hello slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="213c7-169">Nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="213c7-169">Failed</span></span></td><td><span data-ttu-id="213c7-170">Upłynął limit czasu</span><span class="sxs-lookup"><span data-stu-id="213c7-170">TimedOut</span></span></td><td><span data-ttu-id="213c7-171">Witaj działania wykonywanie trwało dłużej niż jest dozwolonych przez działanie hello.</span><span class="sxs-lookup"><span data-stu-id="213c7-171">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="213c7-172">Anulowane</span><span class="sxs-lookup"><span data-stu-id="213c7-172">Canceled</span></span></td><td><span data-ttu-id="213c7-173">wycinek Hello zostało anulowane przez akcję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="213c7-173">hello slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="213c7-174">Walidacja</span><span class="sxs-lookup"><span data-stu-id="213c7-174">Validation</span></span></td><td><span data-ttu-id="213c7-175">Weryfikacja nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="213c7-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="213c7-176">wycinek Hello nie toobe wygenerowany i/lub sprawdzić poprawności.</span><span class="sxs-lookup"><span data-stu-id="213c7-176">hello slice failed toobe generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="213c7-177">Gotowe</span><span class="sxs-lookup"><span data-stu-id="213c7-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="213c7-178">Witaj wycinek jest gotowy do użycia.</span><span class="sxs-lookup"><span data-stu-id="213c7-178">hello slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="213c7-179">Pominięto</span><span class="sxs-lookup"><span data-stu-id="213c7-179">Skipped</span></span></td><td><span data-ttu-id="213c7-180">Brak</span><span class="sxs-lookup"><span data-stu-id="213c7-180">None</span></span></td><td><span data-ttu-id="213c7-181">wycinek Hello nie jest przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="213c7-181">hello slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="213c7-182">Brak</span><span class="sxs-lookup"><span data-stu-id="213c7-182">None</span></span></td><td>-</td><td><span data-ttu-id="213c7-183">Wycinek używane tooexist inny stan, ale został zresetowany.</span><span class="sxs-lookup"><span data-stu-id="213c7-183">A slice used tooexist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="213c7-184">Szczegóły hello wycinek można wyświetlić, klikając wpisem wycinka na powitania **ostatnio zaktualizowano wycinków** bloku.</span><span class="sxs-lookup"><span data-stu-id="213c7-184">You can view hello details about a slice by clicking a slice entry on hello **Recently Updated Slices** blade.</span></span>

![Szczegóły wycinka](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="213c7-186">Jeśli wykonano wycinek hello wiele razy, zobacz wielu wierszy hello **odbywa się działanie** listy.</span><span class="sxs-lookup"><span data-stu-id="213c7-186">If hello slice has been executed multiple times, you see multiple rows in hello **Activity runs** list.</span></span> <span data-ttu-id="213c7-187">Można wyświetlić szczegółowe informacje o działaniu uruchomić, klikając polecenie wpisu hello Uruchom hello **odbywa się działanie** listy.</span><span class="sxs-lookup"><span data-stu-id="213c7-187">You can view details about an activity run by clicking hello run entry in hello **Activity runs** list.</span></span> <span data-ttu-id="213c7-188">Witaj lista zawiera wszystkie pliki dziennika hello, oraz komunikat o błędzie, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="213c7-188">hello list shows all hello log files, along with an error message if there is one.</span></span> <span data-ttu-id="213c7-189">Ta funkcja jest przydatna dzienniki tooview i debugowania, bez konieczności tooleave z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="213c7-189">This feature is useful tooview and debug logs without having tooleave your data factory.</span></span>

![Szczegóły uruchamiania działania](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="213c7-191">Jeśli nie ma wycinek hello hello **gotowe** stanu, można zobaczyć hello niegotowe wycinki strumienia wychodzącego nie są gotowe i blokuje hello bieżący fragment wykonywanie w hello **wycinków strumienia wychodzącego, które nie są gotowe** listy.</span><span class="sxs-lookup"><span data-stu-id="213c7-191">If hello slice isn't in hello **Ready** state, you can see hello upstream slices that aren't ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="213c7-192">Ta funkcja jest przydatna, gdy Twoje wycinka **oczekiwania** stanu, a ma toounderstand hello nadrzędnego zależności, które hello wycinek oczekuje na.</span><span class="sxs-lookup"><span data-stu-id="213c7-192">This feature is useful when your slice is in **Waiting** state and you want toounderstand hello upstream dependencies that hello slice is waiting on.</span></span>

![Niegotowe wycinki strumienia wychodzącego](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="213c7-194">Diagram stanu zestawu danych</span><span class="sxs-lookup"><span data-stu-id="213c7-194">Dataset state diagram</span></span>
<span data-ttu-id="213c7-195">Po wdrożeniu fabryki danych i potoki hello ma nieprawidłowy okres aktywności, zestaw danych hello wycinków przejście od jednego stanu tooanother.</span><span class="sxs-lookup"><span data-stu-id="213c7-195">After you deploy a data factory and hello pipelines have a valid active period, hello dataset slices transition from one state tooanother.</span></span> <span data-ttu-id="213c7-196">Obecnie stanu wycinka hello następujące powitania po diagram stanu:</span><span class="sxs-lookup"><span data-stu-id="213c7-196">Currently, hello slice status follows hello following state diagram:</span></span>

![Diagram stanu](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="213c7-198">Hello przepływ przejścia stanu zestawu danych w fabryce danych jest następujące hello: oczekiwania -> w toku/w toku (sprawdzania) -> gotowe/nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="213c7-198">hello dataset state transition flow in data factory is hello following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="213c7-199">wycinek Hello jest uruchamiany w **oczekiwania** stanu oczekiwania na toobe warunki wstępne zostały spełnione przed rozpoczęciem wykonywania.</span><span class="sxs-lookup"><span data-stu-id="213c7-199">hello slice starts in a **Waiting** state, waiting for preconditions toobe met before it executes.</span></span> <span data-ttu-id="213c7-200">Następnie rozpoczęciem wykonywania działania hello i wycinek hello przechodzi w stan **w toku** stanu.</span><span class="sxs-lookup"><span data-stu-id="213c7-200">Then, hello activity starts executing, and hello slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="213c7-201">wykonanie działania Hello może powodzenie lub niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="213c7-201">hello activity execution might succeed or fail.</span></span> <span data-ttu-id="213c7-202">wycinek Hello jest oznaczony jako **gotowe** lub **nie powiodło się**, na podstawie wyniku hello hello wykonywania.</span><span class="sxs-lookup"><span data-stu-id="213c7-202">hello slice is marked as **Ready** or **Failed**, based on hello result of hello execution.</span></span>

<span data-ttu-id="213c7-203">Można zresetować toogo wycinka powitania od hello **gotowe** lub **** toohello stanu **oczekiwania** stanu.</span><span class="sxs-lookup"><span data-stu-id="213c7-203">You can reset hello slice toogo back from hello **Ready** or **Failed** state toohello **Waiting** state.</span></span> <span data-ttu-id="213c7-204">Można również oznaczyć stanu wycinka hello zbyt**Pomiń**, co uniemożliwia działania hello wykonywania i nie przetwarza hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="213c7-204">You can also mark hello slice state too**Skip**, which prevents hello activity from executing and not processing hello slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="213c7-205">Wstrzymywanie i wznawianie potoki</span><span class="sxs-lookup"><span data-stu-id="213c7-205">Pause and resume pipelines</span></span>
<span data-ttu-id="213c7-206">Twoje potoki można zarządzać za pomocą programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="213c7-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="213c7-207">Na przykład można wstrzymywać i wznawiać potoki przez uruchomienie polecenia cmdlet programu Azure PowerShell przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="213c7-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="213c7-208">Widok diagramu Hello nie obsługuje wstrzymywanie i wznawianie potoków.</span><span class="sxs-lookup"><span data-stu-id="213c7-208">hello diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="213c7-209">Toouse interfejsu użytkownika, należy użyć hello monitorowanie i zarządzanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="213c7-209">If you want toouse an user interface, use hello monitoring and managing application.</span></span> <span data-ttu-id="213c7-210">Aby uzyskać informacje dotyczące korzystania z aplikacji hello, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji hello monitorowanie i zarządzanie](data-factory-monitor-manage-app.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="213c7-210">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="213c7-211">Można Wstrzymaj/zawiesić potoki przy użyciu hello **Suspend-AzureRmDataFactoryPipeline** polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="213c7-211">You can pause/suspend pipelines by using hello **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="213c7-212">To polecenie cmdlet jest przydatne, gdy nie chcesz toorun Twojego potoki dopóki problem nie zostanie rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="213c7-212">This cmdlet is useful when you don’t want toorun your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="213c7-213">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="213c7-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="213c7-214">Po hello problem został rozwiązany z potoku hello, można wznowić zawieszone hello potoku, uruchamiając następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="213c7-214">After hello issue has been fixed with hello pipeline, you can resume hello suspended pipeline by running hello following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="213c7-215">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="213c7-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="213c7-216">Debugowanie potoki</span><span class="sxs-lookup"><span data-stu-id="213c7-216">Debug pipelines</span></span>
<span data-ttu-id="213c7-217">Fabryka danych Azure udostępnia bogate możliwości dla Ciebie toodebug i rozwiązywania problemów z potoków, za pomocą hello portalu Azure i programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="213c7-217">Azure Data Factory provides rich capabilities for you toodebug and troubleshoot pipelines by using hello Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="213c7-218">[! [Uwaga} jest znacznie łatwiejsze tootroubleshot, który błędów za pomocą Witaj, monitorowania i aplikacji do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="213c7-218">[!NOTE} It is much easier tootroubleshot errors using hello Monitoring & Management App.</span></span> <span data-ttu-id="213c7-219">Aby uzyskać informacje dotyczące korzystania z aplikacji hello, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji hello monitorowanie i zarządzanie](data-factory-monitor-manage-app.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="213c7-219">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="213c7-220">Znaleziono błędów w potoku</span><span class="sxs-lookup"><span data-stu-id="213c7-220">Find errors in a pipeline</span></span>
<span data-ttu-id="213c7-221">W przypadku niepowodzenia uruchomienia działania hello w potoku zestawu danych hello, który jest generowany przez potok hello jest w stanie błędu z powodu błędu hello.</span><span class="sxs-lookup"><span data-stu-id="213c7-221">If hello activity run fails in a pipeline, hello dataset that is produced by hello pipeline is in an error state because of hello failure.</span></span> <span data-ttu-id="213c7-222">Można debugować i rozwiązywanie problemów z fabryki danych Azure przy użyciu następujących metod hello.</span><span class="sxs-lookup"><span data-stu-id="213c7-222">You can debug and troubleshoot errors in Azure Data Factory by using hello following methods.</span></span>

#### <a name="use-hello-azure-portal-toodebug-an-error"></a><span data-ttu-id="213c7-223">Użyj hello toodebug portalu Azure wystąpił błąd</span><span class="sxs-lookup"><span data-stu-id="213c7-223">Use hello Azure portal toodebug an error</span></span>
1. <span data-ttu-id="213c7-224">Na powitania **tabeli** bloku, kliknij hello problem wycinek, który ma hello **stan** ustawić także****.</span><span class="sxs-lookup"><span data-stu-id="213c7-224">On hello **Table** blade, click hello problem slice that has hello **Status** set too**Failed**.</span></span>

   ![Blok tabeli z wycinka problem](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="213c7-226">Na powitania **wycinka danych** bloku, kliknij działanie hello uruchamiania, która nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="213c7-226">On hello **Data slice** blade, click hello activity run that failed.</span></span>

   ![Wycinek danych z powodu błędu](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="213c7-228">Na powitania **szczegóły uruchomienia działania** bloku, możesz pobrać hello pliki, które są skojarzone z hello HDInsight przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="213c7-228">On hello **Activity run details** blade, you can download hello files that are associated with hello HDInsight processing.</span></span> <span data-ttu-id="213c7-229">Kliknij przycisk **Pobierz** dla stanu/stderr toodownload hello pliku dziennika błędów, który zawiera szczegółowe informacje o błędzie hello.</span><span class="sxs-lookup"><span data-stu-id="213c7-229">Click **Download** for Status/stderr toodownload hello error log file that contains details about hello error.</span></span>

   ![Działanie Uruchom szczegóły blok z powodu błędu](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a><span data-ttu-id="213c7-231">Użyj programu PowerShell toodebug błąd</span><span class="sxs-lookup"><span data-stu-id="213c7-231">Use PowerShell toodebug an error</span></span>
1. <span data-ttu-id="213c7-232">Uruchom program **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="213c7-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="213c7-233">Uruchom hello **Get-AzureRmDataFactorySlice** polecenia wycinków hello toosee i ich Stany.</span><span class="sxs-lookup"><span data-stu-id="213c7-233">Run hello **Get-AzureRmDataFactorySlice** command toosee hello slices and their statuses.</span></span> <span data-ttu-id="213c7-234">Powinny pojawić się wycinek ze stanem hello ****.</span><span class="sxs-lookup"><span data-stu-id="213c7-234">You should see a slice with hello status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="213c7-235">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="213c7-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="213c7-236">Zastąp **StartDateTime** czas rozpoczęcia z potoku.</span><span class="sxs-lookup"><span data-stu-id="213c7-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="213c7-237">Teraz uruchom hello **Get AzureRmDataFactoryRun** Uruchom polecenia cmdlet tooget szczegóły dotyczące działania hello hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="213c7-237">Now, run hello **Get-AzureRmDataFactoryRun** cmdlet tooget details about hello activity run for hello slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="213c7-238">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="213c7-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="213c7-239">wartość Hello StartDateTime jest czas rozpoczęcia hello hello błąd/problem wycinek, który zauważyć hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="213c7-239">hello value of StartDateTime is hello start time for hello error/problem slice that you noted from hello previous step.</span></span> <span data-ttu-id="213c7-240">Witaj daty i godziny należy ująć w podwójny cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="213c7-240">hello date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="213c7-241">Powinny pojawić się dane wyjściowe ze szczegółami hello błędu, który jest podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="213c7-241">You should see output with details about hello error that is similar toohello following:</span></span>

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
5. <span data-ttu-id="213c7-242">Możesz uruchomić hello **AzureRmDataFactoryLog Zapisz** polecenia cmdlet z hello wartość identyfikatora Zobacz z danych wyjściowych hello i pobierania plików dziennika hello za pomocą hello **- DownloadLogsoption** hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="213c7-242">You can run hello **Save-AzureRmDataFactoryLog** cmdlet with hello Id value that you see from hello output, and download hello log files by using hello **-DownloadLogsoption** for hello cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="213c7-243">Uruchom ponownie błędów w potoku</span><span class="sxs-lookup"><span data-stu-id="213c7-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="213c7-244">Jest łatwiejsze tootroubleshoot błędów i uruchom ponownie zakończone niepowodzeniem wycinków przy użyciu hello monitorowanie & aplikacji do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="213c7-244">It's easier tootroubleshoot errors and rerun failed slices by using hello Monitoring & Management App.</span></span> <span data-ttu-id="213c7-245">Aby uzyskać informacje dotyczące korzystania z aplikacji hello, zobacz [monitorować i zarządzać nimi potoki fabryki danych przy użyciu aplikacji hello monitorowanie i zarządzanie](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="213c7-245">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-hello-azure-portal"></a><span data-ttu-id="213c7-246">Użyj hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="213c7-246">Use hello Azure portal</span></span>
<span data-ttu-id="213c7-247">Po Rozwiązywanie problemów i debugowanie błędów w potoku, należy ponownie uruchomić błędów przechodząc toohello błąd wycinka i klikając hello **Uruchom** przycisk na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="213c7-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating toohello error slice and clicking hello **Run** button on hello command bar.</span></span>

![Uruchom ponownie wycinek nie powiodło się](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="213c7-249">W przypadku wycinek hello Weryfikacja nie powiodła się z powodu błędu zasad (na przykład, jeśli dane są niedostępne), można naprawić błąd hello i ponownie zweryfikować, klikając hello **weryfikacji** przycisk na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="213c7-249">In case hello slice has failed validation because of a policy failure (for example, if data isn't available), you can fix hello failure and validate again by clicking hello **Validate** button on hello command bar.</span></span>

![Usuń błędy i sprawdzania poprawności](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="213c7-251">Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="213c7-251">Use Azure PowerShell</span></span>
<span data-ttu-id="213c7-252">Uruchom ponownie błędów przy użyciu hello **AzureRmDataFactorySliceStatus zestaw** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="213c7-252">You can rerun failures by using hello **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="213c7-253">Zobacz hello [AzureRmDataFactorySliceStatus zestaw](https://msdn.microsoft.com/library/mt603522.aspx) temat o składni i inne szczegółowe informacje o hello polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="213c7-253">See hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about hello cmdlet.</span></span>

<span data-ttu-id="213c7-254">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="213c7-254">**Example:**</span></span>

<span data-ttu-id="213c7-255">Witaj poniższy przykład przedstawia stan wszystkich fragmentów hello tabeli "DAWikiAggregatedData" too'Waiting hello "w fabryce danych Azure hello"WikiADF".</span><span class="sxs-lookup"><span data-stu-id="213c7-255">hello following example sets hello status of all slices for hello table 'DAWikiAggregatedData' too'Waiting' in hello Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="213c7-256">Witaj "Typ aktualizacji" ustawiono too'UpstreamInPipeline ", co oznacza, że stanów każdy wycinek dla tabeli hello i wszystkie hello zależne tabele (nadrzędnego) są ustawione too'Waiting".</span><span class="sxs-lookup"><span data-stu-id="213c7-256">hello 'UpdateType' is set too'UpstreamInPipeline', which means that statuses of each slice for hello table and all hello dependent (upstream) tables are set too'Waiting'.</span></span> <span data-ttu-id="213c7-257">Witaj inne możliwe wartości tego parametru to "Indywidualny".</span><span class="sxs-lookup"><span data-stu-id="213c7-257">hello other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="213c7-258">Tworzenie alertów</span><span class="sxs-lookup"><span data-stu-id="213c7-258">Create alerts</span></span>
<span data-ttu-id="213c7-259">Azure dzienniki zdarzeń użytkownika podczas zasobów platformy Azure (na przykład fabryka danych) jest utworzone, zaktualizować lub usunąć.</span><span class="sxs-lookup"><span data-stu-id="213c7-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="213c7-260">Alerty można tworzyć na te zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="213c7-260">You can create alerts on these events.</span></span> <span data-ttu-id="213c7-261">Można użyć różnych metryk toocapture fabryki danych i tworzenie alertów na metryki.</span><span class="sxs-lookup"><span data-stu-id="213c7-261">You can use Data Factory toocapture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="213c7-262">Firma Microsoft zaleca używanie zdarzeń monitorowania w czasie rzeczywistym i metryki w celach historycznych.</span><span class="sxs-lookup"><span data-stu-id="213c7-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="213c7-263">Alerty dotyczące zdarzeń</span><span class="sxs-lookup"><span data-stu-id="213c7-263">Alerts on events</span></span>
<span data-ttu-id="213c7-264">Zdarzenia Azure udostępniają przydatne wgląd w działania wykonywane w zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="213c7-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="213c7-265">Podczas korzystania z fabryki danych Azure, zdarzenia są generowane, gdy:</span><span class="sxs-lookup"><span data-stu-id="213c7-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="213c7-266">Fabryka danych jest utworzone, zaktualizować lub usunąć.</span><span class="sxs-lookup"><span data-stu-id="213c7-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="213c7-267">Przetwarzanie danych (jako "działa") został uruchomiony lub zakończona.</span><span class="sxs-lookup"><span data-stu-id="213c7-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="213c7-268">Klaster usługi HDInsight na żądanie jest utworzone lub usunięte.</span><span class="sxs-lookup"><span data-stu-id="213c7-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="213c7-269">Możesz tworzyć alerty dotyczące tych zdarzeń użytkownika i je skonfigurować, administrator toohello powiadomienia e-mail toosend i coadministrators hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="213c7-269">You can create alerts on these user events and configure them toosend email notifications toohello administrator and coadministrators of hello subscription.</span></span> <span data-ttu-id="213c7-270">Ponadto można określić adresy e-mail dodatkowych użytkowników, którzy potrzebują tooreceive powiadomienia e-mail, gdy są spełnione warunki hello.</span><span class="sxs-lookup"><span data-stu-id="213c7-270">In addition, you can specify additional email addresses of users who need tooreceive email notifications when hello conditions are met.</span></span> <span data-ttu-id="213c7-271">Ta funkcja jest przydatne, gdy mają tooget powiadomienie dotyczące niepowodzeń i nie mają toocontinuously monitor fabrykę danych.</span><span class="sxs-lookup"><span data-stu-id="213c7-271">This feature is useful when you want tooget notified on failures and don’t want toocontinuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="213c7-272">Obecnie hello portal nie wyświetla alerty dotyczące zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="213c7-272">Currently, hello portal doesn't show alerts on events.</span></span> <span data-ttu-id="213c7-273">Użyj hello [zarządzania i monitorowania aplikacji](data-factory-monitor-manage-app.md) toosee wszystkie alerty.</span><span class="sxs-lookup"><span data-stu-id="213c7-273">Use hello [Monitoring and Management app](data-factory-monitor-manage-app.md) toosee all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="213c7-274">Określ definicję alertu</span><span class="sxs-lookup"><span data-stu-id="213c7-274">Specify an alert definition</span></span>
<span data-ttu-id="213c7-275">toospecify definicji alertu, tworzenie pliku JSON, który opisuje hello operacje, które chcesz toobe alerty o.</span><span class="sxs-lookup"><span data-stu-id="213c7-275">toospecify an alert definition, you create a JSON file that describes hello operations that you want toobe alerted on.</span></span> <span data-ttu-id="213c7-276">W hello poniższy przykład hello alert wysyła wiadomość e-mail z powiadomieniem do hello RunFinished operacji.</span><span class="sxs-lookup"><span data-stu-id="213c7-276">In hello following example, hello alert sends an email notification for hello RunFinished operation.</span></span> <span data-ttu-id="213c7-277">toobe określonych, powiadomienie e-mail są wysyłane podczas wykonywania w fabryce danych hello zostało ukończone i hello uruchomienie nie powiodło się (stan = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="213c7-277">toobe specific, an email notification is sent when a run in hello data factory has completed and hello run has failed (Status = FailedExecution).</span></span>

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
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
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

<span data-ttu-id="213c7-278">Możesz usunąć **podstanu** z hello definicji JSON, jeśli nie chcesz toobe alerty na określony błąd.</span><span class="sxs-lookup"><span data-stu-id="213c7-278">You can remove **subStatus** from hello JSON definition if you don’t want toobe alerted on a specific failure.</span></span>

<span data-ttu-id="213c7-279">Ten przykład konfiguruje hello alert dla wszystkich fabryki danych w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="213c7-279">This example sets up hello alert for all data factories in your subscription.</span></span> <span data-ttu-id="213c7-280">Jeśli chcesz hello toobe alertów dla fabryki danych, można określić fabryki danych **resourceUri** w hello **źródła danych**:</span><span class="sxs-lookup"><span data-stu-id="213c7-280">If you want hello alert toobe set up for a particular data factory, you can specify data factory **resourceUri** in hello **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="213c7-281">Witaj Poniższa tabela zawiera listę hello dostępne operacje, Stany (i podstany).</span><span class="sxs-lookup"><span data-stu-id="213c7-281">hello following table provides hello list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="213c7-282">Nazwa operacji</span><span class="sxs-lookup"><span data-stu-id="213c7-282">Operation name</span></span> | <span data-ttu-id="213c7-283">Stan</span><span class="sxs-lookup"><span data-stu-id="213c7-283">Status</span></span> | <span data-ttu-id="213c7-284">Podstan</span><span class="sxs-lookup"><span data-stu-id="213c7-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="213c7-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="213c7-285">RunStarted</span></span> |<span data-ttu-id="213c7-286">Rozpoczęto</span><span class="sxs-lookup"><span data-stu-id="213c7-286">Started</span></span> |<span data-ttu-id="213c7-287">Uruchamianie</span><span class="sxs-lookup"><span data-stu-id="213c7-287">Starting</span></span> |
| <span data-ttu-id="213c7-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="213c7-288">RunFinished</span></span> |<span data-ttu-id="213c7-289">Nie powiodło się / powiodło się.</span><span class="sxs-lookup"><span data-stu-id="213c7-289">Failed / Succeeded</span></span> |<span data-ttu-id="213c7-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="213c7-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="213c7-291">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="213c7-291">Succeeded</span></span><br/><br/><span data-ttu-id="213c7-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="213c7-292">FailedExecution</span></span><br/><br/><span data-ttu-id="213c7-293">Upłynął limit czasu</span><span class="sxs-lookup"><span data-stu-id="213c7-293">TimedOut</span></span><br/><br/><span data-ttu-id="213c7-294">< anulowane</span><span class="sxs-lookup"><span data-stu-id="213c7-294"><Canceled</span></span><br/><br/><span data-ttu-id="213c7-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="213c7-295">FailedValidation</span></span><br/><br/><span data-ttu-id="213c7-296">porzucone</span><span class="sxs-lookup"><span data-stu-id="213c7-296">Abandoned</span></span> |
| <span data-ttu-id="213c7-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="213c7-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="213c7-298">Rozpoczęto</span><span class="sxs-lookup"><span data-stu-id="213c7-298">Started</span></span> | |
| <span data-ttu-id="213c7-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="213c7-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="213c7-300">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="213c7-300">Succeeded</span></span> | |
| <span data-ttu-id="213c7-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="213c7-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="213c7-302">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="213c7-302">Succeeded</span></span> | |

<span data-ttu-id="213c7-303">Zobacz [Tworzenie reguły alertu](https://msdn.microsoft.com/library/azure/dn510366.aspx) szczegółowe informacje o hello elementy JSON, które są używane w przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="213c7-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about hello JSON elements that are used in hello example.</span></span>

#### <a name="deploy-hello-alert"></a><span data-ttu-id="213c7-304">Wdrażanie hello alertu</span><span class="sxs-lookup"><span data-stu-id="213c7-304">Deploy hello alert</span></span>
<span data-ttu-id="213c7-305">alert hello toodeploy, polecenia cmdlet programu Azure PowerShell służącego do hello **AzureRmResourceGroupDeployment nowy**, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="213c7-305">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="213c7-306">Po wdrożenie grupy zasobów hello zakończyło się pomyślnie, zostanie wyświetlony hello następujące komunikaty:</span><span class="sxs-lookup"><span data-stu-id="213c7-306">After hello resource group deployment has finished successfully, you see hello following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
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
> <span data-ttu-id="213c7-307">Można użyć hello [Tworzenie reguły alertu](https://msdn.microsoft.com/library/azure/dn510366.aspx) toocreate interfejsu API REST regułę alertu.</span><span class="sxs-lookup"><span data-stu-id="213c7-307">You can use hello [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate an alert rule.</span></span> <span data-ttu-id="213c7-308">ładunek JSON Hello jest podobny przykład JSON toohello.</span><span class="sxs-lookup"><span data-stu-id="213c7-308">hello JSON payload is similar toohello JSON example.</span></span>  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a><span data-ttu-id="213c7-309">Pobieranie listy hello wdrożeń grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="213c7-309">Retrieve hello list of Azure resource group deployments</span></span>
<span data-ttu-id="213c7-310">Lista hello tooretrieve wdrożone wdrożenia grupy zasobów platformy Azure, użyj polecenia cmdlet hello **Get-AzureRmResourceGroupDeployment**, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="213c7-310">tooretrieve hello list of deployed Azure resource group deployments, use hello cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

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

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="213c7-311">Obsługa zdarzeń użytkownika</span><span class="sxs-lookup"><span data-stu-id="213c7-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="213c7-312">Można wyświetlić wszystkie zdarzenia hello, które są generowane po kliknięciu przycisku hello **metryki i operacje** kafelka.</span><span class="sxs-lookup"><span data-stu-id="213c7-312">You can see all hello events that are generated after clicking hello **Metrics and operations** tile.</span></span>

    ![Kafelek metryki i operacje](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="213c7-314">Kliknij przycisk hello **zdarzenia** kafelka toosee hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="213c7-314">Click hello **Events** tile toosee hello events.</span></span>

    ![Kafelek zdarzenia](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="213c7-316">Na powitania **zdarzenia** bloku można zobaczyć szczegółowe informacje dotyczące zdarzeń, zdarzeń filtrowane i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="213c7-316">On hello **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Blok zdarzenia](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="213c7-318">Kliknij przycisk **operacji** hello operacje listy, które powoduje błąd.</span><span class="sxs-lookup"><span data-stu-id="213c7-318">Click an **Operation** in hello operations list that causes an error.</span></span>

    ![Wybierz operację](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="213c7-320">Kliknij przycisk **błąd** zdarzenia toosee szczegóły błędu hello.</span><span class="sxs-lookup"><span data-stu-id="213c7-320">Click an **Error** event toosee details about hello error.</span></span>

    ![Błąd zdarzenia](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="213c7-322">Zobacz [poleceń cmdlet Azure wglądu](https://msdn.microsoft.com/library/mt282452.aspx) dla poleceń cmdlet programu PowerShell służącego tooadd, pobrać lub usunąć alerty.</span><span class="sxs-lookup"><span data-stu-id="213c7-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use tooadd, get, or remove alerts.</span></span> <span data-ttu-id="213c7-323">Oto kilka przykładów użycia hello **Get-AlertRule** polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="213c7-323">Here are a few examples of using hello **Get-AlertRule** cmdlet:</span></span>

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
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
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

<span data-ttu-id="213c7-324">Uruchom następujące szczegóły toosee polecenia get-help i przykłady dotyczące polecenia cmdlet Get-AlertRule hello hello.</span><span class="sxs-lookup"><span data-stu-id="213c7-324">Run hello following get-help commands toosee details and examples for hello Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="213c7-325">Jeśli zostanie wyświetlony na powitania Generowanie alertów zdarzeń hello bloku portalu, ale nie otrzymywać powiadomienia pocztą e-mail, sprawdź, czy określonego adresu e-mail hello ustawiono tooreceive wiadomości e-mail od nadawców zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="213c7-325">If you see hello alert generation events on hello portal blade but you don't receive email notifications, check whether hello email address that is specified is set tooreceive emails from external senders.</span></span> <span data-ttu-id="213c7-326">wiadomości e-mail alertów Hello może zostały zablokowane przez ustawienia poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="213c7-326">hello alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="213c7-327">Alerty dotyczące metryk</span><span class="sxs-lookup"><span data-stu-id="213c7-327">Alerts on metrics</span></span>
<span data-ttu-id="213c7-328">W fabryce danych można przechwytywać różnych metryk i tworzyć alerty na metryki.</span><span class="sxs-lookup"><span data-stu-id="213c7-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="213c7-329">Można monitorować i tworzyć alerty na powitania po metryki wycinki hello w fabryce danych:</span><span class="sxs-lookup"><span data-stu-id="213c7-329">You can monitor and create alerts on hello following metrics for hello slices in your data factory:</span></span>

* <span data-ttu-id="213c7-330">**Uruchamia nie powiodło się**</span><span class="sxs-lookup"><span data-stu-id="213c7-330">**Failed Runs**</span></span>
* <span data-ttu-id="213c7-331">**Uruchamia się pomyślnie**</span><span class="sxs-lookup"><span data-stu-id="213c7-331">**Successful Runs**</span></span>

<span data-ttu-id="213c7-332">Te metryki są przydatne i ułatwiają tooget omówienie ogólnej nie powiodło się i pomyślnego uruchomienia w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="213c7-332">These metrics are useful and help you tooget an overview of overall failed and successful runs in hello data factory.</span></span> <span data-ttu-id="213c7-333">Metryki są emitowane w każdym użyciu uruchomienia wycinka.</span><span class="sxs-lookup"><span data-stu-id="213c7-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="213c7-334">Na początku hello hello godzinę, te metryki są agregowane i wypychana tooyour konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="213c7-334">At hello beginning of hello hour, these metrics are aggregated and pushed tooyour storage account.</span></span> <span data-ttu-id="213c7-335">metryki tooenable, skonfiguruj konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="213c7-335">tooenable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="213c7-336">Włączyć metryki</span><span class="sxs-lookup"><span data-stu-id="213c7-336">Enable metrics</span></span>
<span data-ttu-id="213c7-337">tooenable metryki, kliknij poniżej hello z hello **fabryki danych** bloku:</span><span class="sxs-lookup"><span data-stu-id="213c7-337">tooenable metrics, click hello following from hello **Data Factory** blade:</span></span>

<span data-ttu-id="213c7-338">**Monitorowanie** > **Metryka** > **ustawień diagnostycznych** > **diagnostyki**</span><span class="sxs-lookup"><span data-stu-id="213c7-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Łącze diagnostyki](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="213c7-340">Na powitania **diagnostyki** bloku, kliknij przycisk **na**, wybierz konto magazynu hello i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="213c7-340">On hello **Diagnostics** blade, click **On**, select hello storage account, and click **Save**.</span></span>

![Diagnostyka bloku](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="213c7-342">Może potrwać godzinę tooone toobe metryki hello widoczne na powitania **monitorowanie** bloku ponieważ agregacji metryki się stanie, co godzinę.</span><span class="sxs-lookup"><span data-stu-id="213c7-342">It might take up tooone hour for hello metrics toobe visible on hello **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="213c7-343">Konfigurowanie alertu na metryk</span><span class="sxs-lookup"><span data-stu-id="213c7-343">Set up an alert on metrics</span></span>
<span data-ttu-id="213c7-344">Kliknij przycisk hello **fabryki danych metryki** Kafelek:</span><span class="sxs-lookup"><span data-stu-id="213c7-344">Click hello **Data Factory metrics** tile:</span></span>

![Kafelek metryki fabryki danych](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="213c7-346">Na powitania **Metryka** bloku, kliknij przycisk **+ Dodaj alert** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="213c7-346">On hello **Metric** blade, click **+ Add alert** on hello toolbar.</span></span>
<span data-ttu-id="213c7-347">![Blok metryki fabryki danych > Dodaj alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="213c7-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="213c7-348">Na powitania **dodać regułę alertu** hello następujące kroki, a kliknij pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="213c7-348">On hello **Add an alert rule** page, do hello following steps, and click **OK**.</span></span>

* <span data-ttu-id="213c7-349">Wprowadź nazwę dla alertu hello (przykład: "nie powiodło się alert").</span><span class="sxs-lookup"><span data-stu-id="213c7-349">Enter a name for hello alert (example: "failed alert").</span></span>
* <span data-ttu-id="213c7-350">Wprowadź opis alertu hello (przykład: "Wyślij wiadomość e-mail, gdy wystąpi błąd").</span><span class="sxs-lookup"><span data-stu-id="213c7-350">Enter a description for hello alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="213c7-351">Wybierz metrykę (vs "Działa nie powiodło się". "Pomyślne uruchomień").</span><span class="sxs-lookup"><span data-stu-id="213c7-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="213c7-352">Określ warunek i wartość progową.</span><span class="sxs-lookup"><span data-stu-id="213c7-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="213c7-353">Określ hello okres czasu.</span><span class="sxs-lookup"><span data-stu-id="213c7-353">Specify hello period of time.</span></span>
* <span data-ttu-id="213c7-354">Określ, czy mają być wysyłane wiadomości e-mail, tooowners, współautorzy i czytelnicy.</span><span class="sxs-lookup"><span data-stu-id="213c7-354">Specify whether an email should be sent tooowners, contributors, and readers.</span></span>

![Blok metryki fabryki danych > Dodaj regułę alertów](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="213c7-356">Po dodaniu reguły alertu hello pomyślnie, zamyka hello bloku i zostanie wyświetlony nowy alert hello na powitania **Metryka** bloku.</span><span class="sxs-lookup"><span data-stu-id="213c7-356">After hello alert rule is added successfully, hello blade closes and you see hello new alert on hello **Metric** blade.</span></span>

![Blok metryki fabryki danych > Nowy alert dodane](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="213c7-358">Powinno również zostać wyświetlone powitalne liczbę alertów w hello **reguły alertów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="213c7-358">You should also see hello number of alerts in hello **Alert rules** tile.</span></span> <span data-ttu-id="213c7-359">Kliknij przycisk hello **reguły alertów** kafelka.</span><span class="sxs-lookup"><span data-stu-id="213c7-359">Click hello **Alert rules** tile.</span></span>

![Blok metryki fabryki danych — reguły alertów](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="213c7-361">Na powitania **alerty reguły** bloku, zobacz wszystkie istniejące alerty.</span><span class="sxs-lookup"><span data-stu-id="213c7-361">On hello **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="213c7-362">tooadd alert, kliknij przycisk **Dodaj alert** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="213c7-362">tooadd an alert, click **Add alert** on hello toolbar.</span></span>

![Blok reguły alertów](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="213c7-364">Powiadomienia o alertach</span><span class="sxs-lookup"><span data-stu-id="213c7-364">Alert notifications</span></span>
<span data-ttu-id="213c7-365">Po hello reguły alertu spełnia warunek hello, należy pobrać wiadomość e-mail z informacją, że hello alert jest aktywny.</span><span class="sxs-lookup"><span data-stu-id="213c7-365">After hello alert rule matches hello condition, you should get an email that says hello alert is activated.</span></span> <span data-ttu-id="213c7-366">Po hello problem zostanie rozwiązany i hello warunku alertu nie jest już zgodny, otrzymasz wiadomość e-mail z informacją, że hello alert został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="213c7-366">After hello issue is resolved and hello alert condition doesn’t match anymore, you get an email that says hello alert is resolved.</span></span>

<span data-ttu-id="213c7-367">To zachowanie różni się od zdarzenia wysyłania powiadomienia na każdy błąd, który regułę alertu kwalifikuje się do.</span><span class="sxs-lookup"><span data-stu-id="213c7-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="213c7-368">Wdrażanie alerty za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="213c7-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="213c7-369">Alerty można wdrożyć dla metryki hello sam sposób jak w przypadku zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="213c7-369">You can deploy alerts for metrics hello same way that you do for events.</span></span>

<span data-ttu-id="213c7-370">**Definicja alertu**</span><span class="sxs-lookup"><span data-stu-id="213c7-370">**Alert definition**</span></span>

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

<span data-ttu-id="213c7-371">Zastąp *subscriptionId*, *resourceGroupName*, i *dataFactoryName* w przykładowym hello z odpowiednie wartości.</span><span class="sxs-lookup"><span data-stu-id="213c7-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in hello sample with appropriate values.</span></span>

<span data-ttu-id="213c7-372">*metricName* obecnie obsługuje dwie wartości:</span><span class="sxs-lookup"><span data-stu-id="213c7-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="213c7-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="213c7-373">FailedRuns</span></span>
* <span data-ttu-id="213c7-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="213c7-374">SuccessfulRuns</span></span>

<span data-ttu-id="213c7-375">**Wdrażanie hello alertu**</span><span class="sxs-lookup"><span data-stu-id="213c7-375">**Deploy hello alert**</span></span>

<span data-ttu-id="213c7-376">alert hello toodeploy, polecenia cmdlet programu Azure PowerShell służącego do hello **AzureRmResourceGroupDeployment nowy**, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="213c7-376">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="213c7-377">Powinny pojawić się następujące komunikat po pomyślnym wdrożeniu:</span><span class="sxs-lookup"><span data-stu-id="213c7-377">You should see following message after a successful deployment:</span></span>

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

<span data-ttu-id="213c7-378">Można również użyć hello **AlertRule Dodaj** toodeploy polecenia cmdlet reguły alertu.</span><span class="sxs-lookup"><span data-stu-id="213c7-378">You can also use hello **Add-AlertRule** cmdlet toodeploy an alert rule.</span></span> <span data-ttu-id="213c7-379">Zobacz hello [AlertRule Dodaj](https://msdn.microsoft.com/library/mt282468.aspx) tematu, aby uzyskać szczegółowe informacje i przykłady.</span><span class="sxs-lookup"><span data-stu-id="213c7-379">See hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a><span data-ttu-id="213c7-380">Przenoszenie danych fabryki tooa innej grupie zasobów lub subskrypcji</span><span class="sxs-lookup"><span data-stu-id="213c7-380">Move a data factory tooa different resource group or subscription</span></span>
<span data-ttu-id="213c7-381">Data factory tooa innej grupie zasobów lub różnych subskrypcji można przenieść za pomocą hello **Przenieś** polecenia paska przycisk na stronie głównej hello w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="213c7-381">You can move a data factory tooa different resource group or a different subscription by using hello **Move** command bar button on hello home page of your data factory.</span></span>

![Przenieś fabryki danych](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="213c7-383">Można również przenosić powiązanych zasobów (takich jak alerty, które są skojarzone z fabryką danych hello), wraz z hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="213c7-383">You can also move any related resources (such as alerts that are associated with hello data factory), along with hello data factory.</span></span>

![Przenoszenie zasobów, okno dialogowe](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
