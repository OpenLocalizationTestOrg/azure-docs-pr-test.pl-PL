---
title: "aaaMonitor i zarządzanie nimi w potokach danych - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello monitorowanie i zarządzanie toomonitor aplikacji i zarządzanie fabryki danych Azure i potoki."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a><span data-ttu-id="0a8c3-103">Monitorowanie i zarządzanie nimi potoki fabryki danych Azure przy użyciu aplikacji hello monitorowanie i zarządzanie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-103">Monitor and manage Azure Data Factory pipelines by using hello Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a8c3-104">Przy użyciu portalu Azure/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a8c3-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="0a8c3-105">Przy użyciu monitorowania i zarządzania aplikacjami</span><span class="sxs-lookup"><span data-stu-id="0a8c3-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="0a8c3-106">W tym artykule opisano, jak toouse hello toomonitor aplikacji zarządzania i monitorowania, zarządzania i debugowania potoki z fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-106">This article describes how toouse hello Monitoring and Management app toomonitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="0a8c3-107">Zawiera także informacje o jak toocreate alerty tooget powiadomienie dotyczące niepowodzeń.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-107">It also provides information on how toocreate alerts tooget notified on failures.</span></span> <span data-ttu-id="0a8c3-108">Użytkownik może rozpocząć korzystanie z aplikacji hello przez oglądaniu powitania po wideo:</span><span class="sxs-lookup"><span data-stu-id="0a8c3-108">You can get started with using hello application by watching hello following video:</span></span>

> [!NOTE]
> <span data-ttu-id="0a8c3-109">Witaj interfejsu użytkownika pokazano hello wideo może nie pasować informacje wyświetlane w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-109">hello user interface shown in hello video may not exactly match what you see in hello portal.</span></span> <span data-ttu-id="0a8c3-110">Jest nieco starszy, przy zachowaniu pojęcia hello tego samego.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-110">It's slightly older, but concepts remain hello same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a><span data-ttu-id="0a8c3-111">Uruchamianie aplikacji hello monitorowanie i zarządzanie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-111">Launch hello Monitoring and Management app</span></span>
<span data-ttu-id="0a8c3-112">hello toolaunch monitora i aplikacji do zarządzania, kliknij przycisk hello **Monitor & Zarządzaj** Kafelek na powitania **fabryki danych** bloku fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-112">toolaunch hello Monitor and Management app, click hello **Monitor & Manage** tile on hello **Data Factory** blade for your data factory.</span></span>

![Monitorowanie kafelka na stronie głównej hello fabryki danych](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="0a8c3-114">Powinna zostać wyświetlona aplikacja monitorowanie i zarządzanie hello otworzyć w osobnym oknie.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-114">You should see hello Monitoring and Management app open in a separate window.</span></span>  

![Aplikacja do monitorowania i zarządzania](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="0a8c3-116">Jeśli widzisz tej przeglądarki sieci web hello jest zablokowany na "Autoryzowanie...", wyczyść hello **zablokować pliki cookie innych firm, a dane lokacji** pole wyboru--lub Zachowaj ono zaznaczone, utworzyć wyjątek **login.microsoftonline.com** , a następnie spróbuj ponownie tooopen hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-116">If you see that hello web browser is stuck at "Authorizing...", clear hello **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>


<span data-ttu-id="0a8c3-117">Na liście działanie Windows hello w środkowym okienku hello zobaczysz okno działania przy każdym uruchomieniu działania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-117">In hello Activity Windows list in hello middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="0a8c3-118">Na przykład jeśli hello toorun działania zaplanowane co godzinę przez pięć godzin, zobacz pięć okien działania skojarzonych z wycinków danych pięć.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-118">For example, if you have hello activity scheduled toorun hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="0a8c3-119">Jeśli nie widzisz działania windows hello liście u dołu hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="0a8c3-119">If you don't see activity windows in hello list at hello bottom, do hello following:</span></span>
 
- <span data-ttu-id="0a8c3-120">Aktualizacja hello **godzina rozpoczęcia** i **czas zakończenia** filtrów w hello top toomatch hello start i end razy potoku sieci, a następnie kliknij hello **Zastosuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-120">Update hello **start time** and **end time** filters at hello top toomatch hello start and end times of your pipeline, and then click hello **Apply** button.</span></span>  
- <span data-ttu-id="0a8c3-121">Lista działań Windows Hello nie zostanie automatycznie odświeżony.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-121">hello Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="0a8c3-122">Kliknij przycisk hello **Odśwież** przycisk na powitania narzędzi hello **okien działania** listy.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-122">Click hello **Refresh** button on hello toolbar in hello **Activity Windows** list.</span></span>  

<span data-ttu-id="0a8c3-123">Jeśli nie masz tootest aplikacji fabryki danych te kroki, hello samouczek: [kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych przy użyciu fabryki danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0a8c3-123">If you don't have a Data Factory application tootest these steps with, do hello tutorial: [copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-hello-monitoring-and-management-app"></a><span data-ttu-id="0a8c3-124">Zrozumienie aplikacji hello monitorowanie i zarządzanie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-124">Understand hello Monitoring and Management app</span></span>
<span data-ttu-id="0a8c3-125">Dostępne są trzy karty po lewej stronie powitania: **Eksploratora zasobów**, **widoków monitorowania**, i **alerty**.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-125">There are three tabs on hello left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="0a8c3-126">Witaj pierwszej karcie (**Eksploratora zasobów**) jest domyślnie zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-126">hello first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="0a8c3-127">Eksplorator zasobów</span><span class="sxs-lookup"><span data-stu-id="0a8c3-127">Resource Explorer</span></span>
<span data-ttu-id="0a8c3-128">Znajdują się hello w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="0a8c3-128">You see hello following:</span></span>

* <span data-ttu-id="0a8c3-129">Witaj Eksploratora zasobów **widok drzewa** w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-129">hello Resource Explorer **tree view** in hello left pane.</span></span>
* <span data-ttu-id="0a8c3-130">Witaj **widoku diagramu** u góry hello w środkowym okienku hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-130">hello **Diagram View** at hello top in hello middle pane.</span></span>
* <span data-ttu-id="0a8c3-131">Witaj **okien działania** listy u dołu hello w środkowym okienku hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-131">hello **Activity Windows** list at hello bottom in hello middle pane.</span></span>
* <span data-ttu-id="0a8c3-132">Witaj **właściwości**, **działania okna Eksploratora**, i **skryptu** karty w okienku po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-132">hello **Properties**, **Activity Window Explorer**, and **Script** tabs in hello right pane.</span></span>

<span data-ttu-id="0a8c3-133">W Eksploratorze zasobów zobacz temat wszystkie zasoby (potoki, zestawy danych połączonych usług) w fabryce danych hello w widoku drzewa.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in hello data factory in a tree view.</span></span> <span data-ttu-id="0a8c3-134">Po wybraniu obiektu, w Eksploratorze zasobów:</span><span class="sxs-lookup"><span data-stu-id="0a8c3-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="0a8c3-135">Witaj skojarzone jednostki zostanie wyróżniona w widoku diagramu hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-135">hello associated Data Factory entity is highlighted in hello Diagram View.</span></span>
* <span data-ttu-id="0a8c3-136">[Skojarzone działanie windows](data-factory-scheduling-and-execution.md) zostały wyróżnione na liście działanie Windows hello u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in hello Activity Windows list at hello bottom.</span></span>  
* <span data-ttu-id="0a8c3-137">właściwości Hello hello wybranego obiektu są wyświetlane w oknie właściwości hello w okienku po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-137">hello properties of hello selected object are shown in hello Properties window in hello right pane.</span></span>
* <span data-ttu-id="0a8c3-138">Hello definicji JSON wybranego obiektu hello jest wyświetlany, jeśli ma to zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-138">hello JSON definition of hello selected object is shown, if applicable.</span></span> <span data-ttu-id="0a8c3-139">Na przykład: połączonej usługi, zestawu danych lub potoku.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Eksplorator zasobów](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="0a8c3-141">Zobacz hello [planowania i wykonywania](data-factory-scheduling-and-execution.md) artykułu, aby uzyskać szczegółowe informacje o pojęciach dotyczących działania systemu windows.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-141">See hello [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="0a8c3-142">Widok diagramu</span><span class="sxs-lookup"><span data-stu-id="0a8c3-142">Diagram View</span></span>
<span data-ttu-id="0a8c3-143">Hello widoku diagramu fabryki danych zapewnia jeden z toomonitor szkła i zarządzanie fabryki danych i jego zasoby.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-143">hello Diagram View of a data factory provides a single pane of glass toomonitor and manage a data factory and its assets.</span></span> <span data-ttu-id="0a8c3-144">Po wybraniu podmiot fabryki danych (dataset/potoku) w widoku diagramu hello:</span><span class="sxs-lookup"><span data-stu-id="0a8c3-144">When you select a Data Factory entity (dataset/pipeline) in hello Diagram View:</span></span>

* <span data-ttu-id="0a8c3-145">w widoku drzewa hello wybrano jednostki fabryki danych Hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-145">hello data factory entity is selected in hello tree view.</span></span>
* <span data-ttu-id="0a8c3-146">Witaj skojarzone działanie, które systemu windows są wyróżnione na liście działanie Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-146">hello associated activity windows are highlighted in hello Activity Windows list.</span></span>
* <span data-ttu-id="0a8c3-147">właściwości Hello hello wybranego obiektu są wyświetlane w oknie właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-147">hello properties of hello selected object are shown in hello Properties window.</span></span>

<span data-ttu-id="0a8c3-148">Po włączeniu potoku hello (nie jest w stanie wstrzymania) jest wyświetlany zielony linią:</span><span class="sxs-lookup"><span data-stu-id="0a8c3-148">When hello pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Potok uruchomiona](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="0a8c3-150">Można wstrzymać, wznowić lub zakończenie potoku, wybierając ją w widoku diagramu hello i za pomocą przycisków hello na pasku poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-150">You can pause, resume, or terminate a pipeline by selecting it in hello diagram view and using hello buttons on hello command bar.</span></span>

![Wstrzymanie/wznowienie na pasku poleceń hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="0a8c3-152">Istnieją trzy przyciski paska poleceń dla potoku hello w hello widoku diagramu.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-152">There are three command bar buttons for hello pipeline in hello Diagram View.</span></span> <span data-ttu-id="0a8c3-153">Możesz użyć hello drugiego przycisku toopause hello potoku.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-153">You can use hello second button toopause hello pipeline.</span></span> <span data-ttu-id="0a8c3-154">Wstrzymywanie nie zakończyć hello aktualnie uruchomione działania i umożliwia ich kontynuować toocompletion.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-154">Pausing doesn't terminate hello currently running activities and lets them proceed toocompletion.</span></span> <span data-ttu-id="0a8c3-155">przycisk trzeci Hello potoku hello wstrzymuje i kończy istniejące wykonywanych działań.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-155">hello third button pauses hello pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="0a8c3-156">pierwszy przycisk Hello wznawia hello potoku.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-156">hello first button resumes hello pipeline.</span></span> <span data-ttu-id="0a8c3-157">Wstrzymanie planowaną zmienia kolor hello hello potoku.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-157">When your pipeline is paused, hello color of hello pipeline changes.</span></span> <span data-ttu-id="0a8c3-158">Na przykład wstrzymanie potoku wygląda powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="0a8c3-158">For example, a paused pipeline looks like in hello following image:</span></span> 

![Wstrzymane potoku](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="0a8c3-160">Można wybrać wiele potoki dwóch lub więcej używając hello klawisz Ctrl.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-160">You can multi-select two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="0a8c3-161">Potoki wielu hello polecenia paska przycisków toopause/wznawiania można użyć w czasie.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-161">You can use hello command bar buttons toopause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="0a8c3-162">Użytkownik może również kliknąć prawym przyciskiem myszy potoku i wybrania opcji toosuspend, Wznów lub zakończenie potoku.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-162">You can also right-click a pipeline and select options toosuspend, resume, or terminate a pipeline.</span></span> 

![Menu kontekstowe dla potoku](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="0a8c3-164">Kliknij przycisk hello **Otwórz potoku** opcję toosee wszystkie działania hello w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-164">Click hello **Open pipeline** option toosee all hello activities in hello pipeline.</span></span> 

![Menu Otwórz potok](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="0a8c3-166">W widoku potoku hello otwarty można zobaczyć wszystkie działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-166">In hello opened pipeline view, you see all activities in hello pipeline.</span></span> <span data-ttu-id="0a8c3-167">W tym przykładzie jest tylko jedno działanie: działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Otwarty potoku](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="0a8c3-169">toogo kopii toohello poprzedni widok, kliknij przycisk Nazwa fabryki danych hello hello nawigacją menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-169">toogo back toohello previous view, click hello data factory name in hello breadcrumb menu at hello top.</span></span>

<span data-ttu-id="0a8c3-170">W widoku potoku hello po wybraniu wyjściowy zestaw danych lub gdy mysz przesuwa się nad hello wyjściowy zestaw danych, zobaczysz okno podręczne działania Windows hello dla tego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-170">In hello pipeline view, when you select an output dataset or when you move your mouse over hello output dataset, you see hello Activity Windows pop-up window for that dataset.</span></span>

![Okno podręczne działania systemu Windows](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="0a8c3-172">Można kliknąć szczegóły toosee okna działania dla niego hello **właściwości** okna w okienku po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-172">You can click an activity window toosee details for it in hello **Properties** window in hello right pane.</span></span>

![Działanie właściwości okna](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="0a8c3-174">W okienku po prawej stronie powitania, Przełącz toohello **działania okna Eksploratora** karcie toosee więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-174">In hello right pane, switch toohello **Activity Window Explorer** tab toosee more details.</span></span>

![Działanie okno Eksploratora](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="0a8c3-176">Zobacz też **rozpoznać zmienne** dla każdego próba uruchomienia działania w hello **prób** sekcji.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-176">You also see **resolved variables** for each run attempt for an activity in hello **Attempts** section.</span></span>

![Zmienne rozwiązany](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="0a8c3-178">Przełącz toohello **skryptu** karcie toosee hello JSON skryptu definicji hello wybranego obiektu.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-178">Switch toohello **Script** tab toosee hello JSON script definition for hello selected object.</span></span>   

![Karta skryptu](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="0a8c3-180">Można wyświetlić okien działania w trzech miejscach:</span><span class="sxs-lookup"><span data-stu-id="0a8c3-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="0a8c3-181">Witaj okien działania wyskakujących w hello widoku diagramu (w środkowym okienku).</span><span class="sxs-lookup"><span data-stu-id="0a8c3-181">hello Activity Windows pop-up in hello Diagram View (middle pane).</span></span>
* <span data-ttu-id="0a8c3-182">Działanie okno Eksploratora Hello w okienku po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-182">hello Activity Window Explorer in hello right pane.</span></span>
* <span data-ttu-id="0a8c3-183">Lista działania systemu Windows Hello w hello dolnym okienku.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-183">hello Activity Windows list in hello bottom pane.</span></span>

<span data-ttu-id="0a8c3-184">W oknie podręcznym działania Windows hello i działania okna Eksploratora toohello można przewijać w poprzednim tygodniu i hello hello następnym tygodniu za pomocą strzałki w lewo i w prawo.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-184">In hello Activity Windows pop-up and Activity Window Explorer, you can scroll toohello previous week and hello next week by using hello left and right arrows.</span></span>

![Strzałki prawej/lewej strony okna Eksploratora działania](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="0a8c3-186">U dołu hello hello widoku diagramu, zobacz tych przycisków: powiększanie, zmniejszanie, tooFit powiększenia powiększenie 100%, Zablokuj układ.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-186">At hello bottom of hello Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom tooFit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="0a8c3-187">Witaj **układu blokady** przycisk zapobiega przypadkowemu przenoszeniu tabel i potoków hello widoku diagramu.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-187">hello **Lock layout** button prevents you from accidentally moving tables and pipelines in hello Diagram View.</span></span> <span data-ttu-id="0a8c3-188">Jest on domyślnie.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-188">It's on by default.</span></span> <span data-ttu-id="0a8c3-189">Można ją wyłączyć i przenosić jednostek hello diagramu.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-189">You can turn it off and move entities around in hello diagram.</span></span> <span data-ttu-id="0a8c3-190">Wyłączenie opcji, można użyć hello ostatniego przycisk tooautomatically pozycji tabele i potoki.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-190">When you turn it off, you can use hello last button tooautomatically position tables and pipelines.</span></span> <span data-ttu-id="0a8c3-191">Można również powiększanie lub pomniejszanie za pomocą kółka myszy hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-191">You can also zoom in or out by using hello mouse wheel.</span></span>

![Diagram przedstawiający polecenia powiększenia widoku](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="0a8c3-193">Lista działania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="0a8c3-193">Activity Windows list</span></span>
<span data-ttu-id="0a8c3-194">Lista okien działania Hello u dołu hello w środkowym okienku hello Wyświetla wszystkie działania windows hello zestawu danych, wybranym hello Eksploratora zasobów lub hello widoku diagramu.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-194">hello Activity Windows list at hello bottom of hello middle pane displays all activity windows for hello dataset that you selected in hello Resource Explorer or hello Diagram View.</span></span> <span data-ttu-id="0a8c3-195">Domyślnie lista hello jest w kolejności malejącej, co oznacza, że widoczny hello najnowsze okno działania u góry hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-195">By default, hello list is in descending order, which means that you see hello latest activity window at hello top.</span></span>

![Lista działania systemu Windows](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="0a8c3-197">Ta lista nie odświeżane automatycznie, więc go odświeżyć. Użyj przycisku Odśwież hello na powitania toomanually narzędzi.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-197">This list doesn't refresh automatically, so use hello refresh button on hello toolbar toomanually refresh it.</span></span>  

<span data-ttu-id="0a8c3-198">Działanie systemu windows może działać w jednym z hello następujące stany:</span><span class="sxs-lookup"><span data-stu-id="0a8c3-198">Activity windows can be in one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="0a8c3-199">Stan</span><span class="sxs-lookup"><span data-stu-id="0a8c3-199">Status</span></span></th><th align="left"><span data-ttu-id="0a8c3-200">Podstan</span><span class="sxs-lookup"><span data-stu-id="0a8c3-200">Substatus</span></span></th><th align="left"><span data-ttu-id="0a8c3-201">Opis</span><span class="sxs-lookup"><span data-stu-id="0a8c3-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="0a8c3-202">Oczekiwanie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-202">Waiting</span></span></td><td><span data-ttu-id="0a8c3-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="0a8c3-203">ScheduleTime</span></span></td><td><span data-ttu-id="0a8c3-204">czas Hello nie pochodzą dla hello działania okna toorun.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-204">hello time hasn't come for hello activity window toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0a8c3-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="0a8c3-205">DatasetDependencies</span></span></td><td><span data-ttu-id="0a8c3-206">zależności strumienia wychodzącego Hello nie są gotowe.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-206">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0a8c3-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="0a8c3-207">ComputeResources</span></span></td><td><span data-ttu-id="0a8c3-208">zasoby obliczeniowe Hello nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-208">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0a8c3-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="0a8c3-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="0a8c3-210">Wszystkie wystąpienia działania hello są zajęte uruchamianiem innych okien działania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-210">All hello activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0a8c3-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="0a8c3-211">ActivityResume</span></span></td><td><span data-ttu-id="0a8c3-212">działanie Hello jest wstrzymane i nie można uruchomić okien działania hello, dopóki nie zostanie wznowione.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-212">hello activity is paused and can't run hello activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0a8c3-213">Spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-213">Retry</span></span></td><td><span data-ttu-id="0a8c3-214">ponawiane Hello wykonania działania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-214">hello activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0a8c3-215">Walidacja</span><span class="sxs-lookup"><span data-stu-id="0a8c3-215">Validation</span></span></td><td><span data-ttu-id="0a8c3-216">Weryfikacja jeszcze się nie rozpoczął.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0a8c3-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="0a8c3-217">ValidationRetry</span></span></td><td><span data-ttu-id="0a8c3-218">Sprawdzanie poprawności jest ponowione toobe oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-218">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="0a8c3-219">W toku</span><span class="sxs-lookup"><span data-stu-id="0a8c3-219">InProgress</span></span></td><td><span data-ttu-id="0a8c3-220">Sprawdzanie poprawności</span><span class="sxs-lookup"><span data-stu-id="0a8c3-220">Validating</span></span></td><td><span data-ttu-id="0a8c3-221">Trwa sprawdzanie poprawności.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="0a8c3-222">Okno działania Hello jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-222">hello activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="0a8c3-223">Nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="0a8c3-223">Failed</span></span></td><td><span data-ttu-id="0a8c3-224">Upłynął limit czasu</span><span class="sxs-lookup"><span data-stu-id="0a8c3-224">TimedOut</span></span></td><td><span data-ttu-id="0a8c3-225">Witaj działania wykonywanie trwało dłużej niż jest dozwolonych przez działanie hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-225">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0a8c3-226">Anulowane</span><span class="sxs-lookup"><span data-stu-id="0a8c3-226">Canceled</span></span></td><td><span data-ttu-id="0a8c3-227">Okno działania Hello zostało anulowane przez akcję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-227">hello activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0a8c3-228">Walidacja</span><span class="sxs-lookup"><span data-stu-id="0a8c3-228">Validation</span></span></td><td><span data-ttu-id="0a8c3-229">Weryfikacja nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="0a8c3-230">Okno działania Hello nie toobe wygenerowany lub sprawdzić jego poprawności.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-230">hello activity window failed toobe generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="0a8c3-231">Gotowe</span><span class="sxs-lookup"><span data-stu-id="0a8c3-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="0a8c3-232">Okno działania Hello jest gotowy do użycia.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-232">hello activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0a8c3-233">Pominięto</span><span class="sxs-lookup"><span data-stu-id="0a8c3-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="0a8c3-234">Okno działania Hello nie został przetworzony.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-234">hello activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0a8c3-235">Brak</span><span class="sxs-lookup"><span data-stu-id="0a8c3-235">None</span></span></td><td>-</td><td><span data-ttu-id="0a8c3-236">Okno działania używane tooexist inny stan, ale został zresetowany.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-236">An activity window used tooexist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="0a8c3-237">Po kliknięciu okno działania na liście hello Zobacz szczegółowe informacje o nim w hello **Eksploratora Windows działania** lub hello **właściwości** okno na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-237">When you click an activity window in hello list, you see details about it in hello **Activity Windows Explorer** or hello **Properties** window on hello right.</span></span>

![Działanie okno Eksploratora](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="0a8c3-239">Odśwież działania systemu windows</span><span class="sxs-lookup"><span data-stu-id="0a8c3-239">Refresh activity windows</span></span>
<span data-ttu-id="0a8c3-240">Szczegóły Hello nie są automatycznie odświeżane, należy więc hello odświeżania (przycisk hello drugi) na pasku toomanually odświeżania hello działania systemu windows lista poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-240">hello details aren't automatically refreshed, so use hello refresh button (hello second button) on hello command bar toomanually refresh hello activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="0a8c3-241">Okno właściwości</span><span class="sxs-lookup"><span data-stu-id="0a8c3-241">Properties window</span></span>
<span data-ttu-id="0a8c3-242">Okno właściwości Hello znajduje się w okienku prawej hello hello zarządzania i monitorowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-242">hello Properties window is in hello right-most pane of hello Monitoring and Management app.</span></span>

![Okno właściwości](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="0a8c3-244">Wyświetla właściwości elementu hello, wybranym hello Eksploratora zasobów (widok drzewa), widok diagramu lub listę okien działania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-244">It displays properties for hello item that you selected in hello Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="0a8c3-245">Działanie okno Eksploratora</span><span class="sxs-lookup"><span data-stu-id="0a8c3-245">Activity Window Explorer</span></span>
<span data-ttu-id="0a8c3-246">Witaj **działania okna Eksploratora** okno jest w okienku prawej hello hello zarządzania i monitorowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-246">hello **Activity Window Explorer** window is in hello right-most pane of hello Monitoring and Management app.</span></span> <span data-ttu-id="0a8c3-247">Wyświetla szczegółowe informacje o okno działania hello wybranego w oknie podręcznym działania Windows hello lub listy działania Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-247">It displays details about hello activity window that you selected in hello Activity Windows pop-up window or hello Activity Windows list.</span></span>

![Działanie okno Eksploratora](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="0a8c3-249">Okno działania tooanother można przełączać, klikając go w widoku kalendarza hello u góry hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-249">You can switch tooanother activity window by clicking it in hello calendar view at hello top.</span></span> <span data-ttu-id="0a8c3-250">Można również użyć przycisk strzałki w lewo/Strzałka w prawo hello okien działania top toosee hello z hello poprzedniego tygodnia lub hello następnym tygodniu.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-250">You can also use hello left arrow/right arrow buttons at hello top toosee activity windows from hello previous week or hello next week.</span></span>

<span data-ttu-id="0a8c3-251">Można użyć przycisków paska narzędzi hello hello dolnym okienku toorerun hello działania okno lub odświeżyć szczegóły hello w okienku hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-251">You can use hello toolbar buttons in hello bottom pane toorerun hello activity window or refresh hello details in hello pane.</span></span>

### <a name="script"></a><span data-ttu-id="0a8c3-252">Skrypt</span><span class="sxs-lookup"><span data-stu-id="0a8c3-252">Script</span></span>
<span data-ttu-id="0a8c3-253">Można użyć hello **skryptu** kartę tooview hello definicji JSON hello wybrane jednostek fabryki danych (połączonej usługi, zestawu danych lub potoku).</span><span class="sxs-lookup"><span data-stu-id="0a8c3-253">You can use hello **Script** tab tooview hello JSON definition of hello selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Karta skryptu](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="0a8c3-255">Używanie widoków systemu</span><span class="sxs-lookup"><span data-stu-id="0a8c3-255">Use system views</span></span>
<span data-ttu-id="0a8c3-256">Witaj zarządzania i monitorowania aplikacji zawiera widoki wbudowanych systemu (**ostatnie okien działania**, **nie powiodło się okien działania**, **okien działania w toku**) który Zezwalaj tooview windows ostatnie/nie powiodło się/w trakcie działania z fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-256">hello Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you tooview recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="0a8c3-257">Przełącz toohello **widoków monitorowania** karcie po lewej stronie powitania, klikając go.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-257">Switch toohello **Monitoring Views** tab on hello left by clicking it.</span></span>

![Karta widoków monitorowania](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="0a8c3-259">Obecnie istnieją trzy widoki systemowe, które są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="0a8c3-260">Wybierz opcję toosee ostatnie działanie systemu windows, okien działania nie powiodło się lub okien działania w toku na liście działanie Windows hello (u dołu hello hello w środkowym okienku).</span><span class="sxs-lookup"><span data-stu-id="0a8c3-260">Select an option toosee recent activity windows, failed activity windows, or in-progress activity windows in hello Activity Windows list (at hello bottom of hello middle pane).</span></span>

<span data-ttu-id="0a8c3-261">Po wybraniu hello **ostatnie okien działania** opcji, zobacz wszystkie ostatnie okien działania w porządku malejącym hello **ostatniej próby czasu**.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-261">When you select hello **Recent activity windows** option, you see all recent activity windows in descending order of hello **last attempt time**.</span></span>

<span data-ttu-id="0a8c3-262">Można użyć hello **nie powiodło się okien działania** wyświetlanie okien działania toosee nie powiodło się na liście hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-262">You can use hello **Failed activity windows** view toosee all failed activity windows in hello list.</span></span> <span data-ttu-id="0a8c3-263">Wybierz przedział nieudana czynność w hello szczegółów toosee listy informacji na ten temat w hello **właściwości** okna lub hello **działania okna Eksploratora**.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-263">Select a failed activity window in hello list toosee details about it in hello **Properties** window or hello **Activity Window Explorer**.</span></span> <span data-ttu-id="0a8c3-264">Możesz również pobrać wszystkie dzienniki dla okna działanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="0a8c3-265">Sortuj i Filtruj działania systemu windows</span><span class="sxs-lookup"><span data-stu-id="0a8c3-265">Sort and filter activity windows</span></span>
<span data-ttu-id="0a8c3-266">Zmiana hello **godzina rozpoczęcia** i **czas zakończenia** ustawienia w poleceniu hello paska toofilter działania w systemie windows.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-266">Change hello **start time** and **end time** settings in hello command bar toofilter activity windows.</span></span> <span data-ttu-id="0a8c3-267">Po zmianie hello godzinę rozpoczęcia i zakończenia, kliknij hello przycisku Dalej toohello zakończenia czasu toorefresh hello okien działania listę.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-267">After you change hello start time and end time, click hello button next toohello end time toorefresh hello Activity Windows list.</span></span>

![Czas rozpoczęcia i zakończenia](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="0a8c3-269">Obecnie wszystkie godziny są w formacie UTC w aplikacji hello zarządzania i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-269">Currently, all times are in UTC format in hello Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="0a8c3-270">W hello **listę okien działania**, kliknij nazwę hello kolumny (na przykład: stanu).</span><span class="sxs-lookup"><span data-stu-id="0a8c3-270">In hello **Activity Windows list**, click hello name of a column (for example: Status).</span></span>

![Działanie systemu Windows lista kolumn menu](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="0a8c3-272">Można wykonać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="0a8c3-272">You can do hello following:</span></span>

* <span data-ttu-id="0a8c3-273">Sortowanie w kolejności rosnącej.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-273">Sort in ascending order.</span></span>
* <span data-ttu-id="0a8c3-274">Sortowanie w kolejności malejącej.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-274">Sort in descending order.</span></span>
* <span data-ttu-id="0a8c3-275">Filtruj według jednego lub więcej wartości (gotowe, oczekiwania itd.).</span><span class="sxs-lookup"><span data-stu-id="0a8c3-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="0a8c3-276">Po określeniu filtru w kolumnie jest wyświetlany przycisk filtru hello włączone dla tej kolumny, co oznacza, że hello wartości w kolumnie hello są filtrowane wartości.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-276">When you specify a filter on a column, you see hello filter button enabled for that column, which indicates that hello values in hello column are filtered values.</span></span>

![Filtrować według kolumny z listy działania Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="0a8c3-278">Można użyć tych samych wyskakującego okienka filtrów tooclear hello.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-278">You can use hello same pop-up window tooclear filters.</span></span> <span data-ttu-id="0a8c3-279">tooclear wszystkie filtry dla listy działania Windows hello, kliknij przycisk Wyczyść filtr hello na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-279">tooclear all filters for hello Activity Windows list, click hello clear filter button on hello command bar.</span></span>

![Wyczyść wszystkie filtry dla listy działania Windows hello](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="0a8c3-281">Akcje usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="0a8c3-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="0a8c3-282">Uruchom ponownie wybrane działanie systemu windows</span><span class="sxs-lookup"><span data-stu-id="0a8c3-282">Rerun selected activity windows</span></span>
<span data-ttu-id="0a8c3-283">Wybierz przedział działania, kliknij hello strzałka na powitania pierwszy przycisk paska poleceń w dół i wybierz **Uruchom ponownie** / **ponownie z powyżej w potoku**.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-283">Select an activity window, click hello down arrow for hello first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="0a8c3-284">Po wybraniu hello **ponownie z powyżej w potoku** opcji zwracające on również wszystkich okien działania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-284">When you select hello **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="0a8c3-285">![Ponownie uruchom okno działania](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="0a8c3-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="0a8c3-286">Można również wybrać wiele okien działania liście hello i uruchom je ponownie na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-286">You can also select multiple activity windows in hello list and rerun them at hello same time.</span></span> <span data-ttu-id="0a8c3-287">Może być toofilter okien działania na podstawie stanu hello (na przykład: ****)--i uruchom ponownie po usunięciu hello problem, który powoduje hello działania windows toofail okien działania hello nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-287">You might want toofilter activity windows based on hello status (for example: **Failed**)--and then rerun hello failed activity windows after correcting hello issue that causes hello activity windows toofail.</span></span> <span data-ttu-id="0a8c3-288">Zobacz hello następujących sekcji, aby uzyskać więcej informacji dotyczących filtrowania działania windows hello na liście.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-288">See hello following section for details about filtering activity windows in hello list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="0a8c3-289">Wstrzymanie/wznowienie wielu potoki</span><span class="sxs-lookup"><span data-stu-id="0a8c3-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="0a8c3-290">Można multiselect potoki dwóch lub więcej używając hello klawisz Ctrl.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-290">You can multiselect two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="0a8c3-291">Korzystając z przycisków paska poleceń hello (które są wyróżnione na powitania czerwony prostokąt powitania po obrazu) toopause/wznowienia ich.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-291">You can use hello command bar buttons (which are highlighted in hello red rectangle in hello following image) toopause/resume them.</span></span>

![Wstrzymanie/wznowienie na pasku poleceń hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="0a8c3-293">Tworzenie alertów</span><span class="sxs-lookup"><span data-stu-id="0a8c3-293">Create alerts</span></span>
<span data-ttu-id="0a8c3-294">Witaj **alerty** strony pozwala na tworzenie alertów i wyświetlanie/edytowanie/usuwanie istniejące alerty.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-294">hello **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="0a8c3-295">Użytkownik może również Włącz/Wyłącz alert.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="0a8c3-296">toosee hello strony alertów, kliknij przycisk hello **alerty** kartę.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-296">toosee hello Alerts page, click hello **Alerts** tab.</span></span>

![Karta alerty](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a><span data-ttu-id="0a8c3-298">toocreate alertu</span><span class="sxs-lookup"><span data-stu-id="0a8c3-298">toocreate an alert</span></span>
1. <span data-ttu-id="0a8c3-299">Kliknij przycisk **dodać Alert** tooadd alertu.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-299">Click **Add Alert** tooadd an alert.</span></span> <span data-ttu-id="0a8c3-300">Zobacz hello **szczegóły** strony.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-300">You see hello **Details** page.</span></span>

    ![Utwórz alerty — strona szczegółów](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="0a8c3-302">Określ hello **nazwa** i **opis** hello alert, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-302">Specify hello **Name** and **Description** for hello alert, and click **Next**.</span></span> <span data-ttu-id="0a8c3-303">Powinny pojawić się hello **filtry** strony.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-303">You should see hello **Filters** page.</span></span>

    ![Utwórz alerty — filtry strony](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="0a8c3-305">Wybierz hello **zdarzeń**, **stan**, i **podstanu** (opcjonalnie), które mają toocreate usługi fabryka danych alertów dla i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-305">Select hello **event**, **status**, and **substatus** (optional) that you want toocreate a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="0a8c3-306">Powinny pojawić się hello **adresatów** strony.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-306">You should see hello **Recipients** page.</span></span>

    ![Utwórz alerty — strona adresatów](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="0a8c3-308">Wybierz hello **poczty E-mail Administratorzy subskrypcji** opcji lub wprowadź **e-mail administratora dodatkowe**i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-308">Select hello **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="0a8c3-309">Powinien zostać wyświetlony alert hello hello na liście.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-309">You should see hello alert in hello list.</span></span>

    ![Lista alertów](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="0a8c3-311">Na liście alertów hello użyj przycisków hello, które są skojarzone z hello alertu tooedit/delete/Włącz/Wyłącz alert.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-311">In hello Alerts list, use hello buttons that are associated with hello alert tooedit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="0a8c3-312">Podstan zdarzeń/stanu</span><span class="sxs-lookup"><span data-stu-id="0a8c3-312">Event/status/substatus</span></span>
<span data-ttu-id="0a8c3-313">Witaj Poniższa tabela zawiera listę hello dostępnych zdarzeń oraz Stany (i podstany).</span><span class="sxs-lookup"><span data-stu-id="0a8c3-313">hello following table provides hello list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="0a8c3-314">Nazwa zdarzenia</span><span class="sxs-lookup"><span data-stu-id="0a8c3-314">Event name</span></span> | <span data-ttu-id="0a8c3-315">Stan</span><span class="sxs-lookup"><span data-stu-id="0a8c3-315">Status</span></span> | <span data-ttu-id="0a8c3-316">Podstan</span><span class="sxs-lookup"><span data-stu-id="0a8c3-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0a8c3-317">Działanie Uruchom wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-317">Activity Run Started</span></span> |<span data-ttu-id="0a8c3-318">Rozpoczęto</span><span class="sxs-lookup"><span data-stu-id="0a8c3-318">Started</span></span> |<span data-ttu-id="0a8c3-319">Uruchamianie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-319">Starting</span></span> |
| <span data-ttu-id="0a8c3-320">Działanie Uruchom Zakończono</span><span class="sxs-lookup"><span data-stu-id="0a8c3-320">Activity Run Finished</span></span> |<span data-ttu-id="0a8c3-321">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-321">Succeeded</span></span> |<span data-ttu-id="0a8c3-322">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-322">Succeeded</span></span> |
| <span data-ttu-id="0a8c3-323">Działanie Uruchom Zakończono</span><span class="sxs-lookup"><span data-stu-id="0a8c3-323">Activity Run Finished</span></span> |<span data-ttu-id="0a8c3-324">Nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="0a8c3-324">Failed</span></span> |<span data-ttu-id="0a8c3-325">Alokacja zasobów nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="0a8c3-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="0a8c3-326">Wykonanie nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="0a8c3-326">Failed Execution</span></span><br/><br/><span data-ttu-id="0a8c3-327">Upłynął limit czasu</span><span class="sxs-lookup"><span data-stu-id="0a8c3-327">Timed Out</span></span><br/><br/><span data-ttu-id="0a8c3-328">Sprawdzanie poprawności nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="0a8c3-328">Failed Validation</span></span><br/><br/><span data-ttu-id="0a8c3-329">porzucone</span><span class="sxs-lookup"><span data-stu-id="0a8c3-329">Abandoned</span></span> |
| <span data-ttu-id="0a8c3-330">Rozpoczęto tworzenie klastra HDI na żądanie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="0a8c3-331">Rozpoczęto</span><span class="sxs-lookup"><span data-stu-id="0a8c3-331">Started</span></span> |-|
| <span data-ttu-id="0a8c3-332">Pomyślnie utworzono klaster HDI na żądanie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="0a8c3-333">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-333">Succeeded</span></span> |-|
| <span data-ttu-id="0a8c3-334">Usunąć klaster HDI na żądanie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="0a8c3-335">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="0a8c3-335">Succeeded</span></span> |-|

### <a name="tooedit-delete-or-disable-an-alert"></a><span data-ttu-id="0a8c3-336">tooedit, usunąć lub wyłączyć alertu</span><span class="sxs-lookup"><span data-stu-id="0a8c3-336">tooedit, delete, or disable an alert</span></span>

<span data-ttu-id="0a8c3-337">Użyj powitania po tooedit przycisków (wyróżnionych kolorem czerwonym), usuń lub Wyłącz alert.</span><span class="sxs-lookup"><span data-stu-id="0a8c3-337">Use hello following buttons (highlighted in red) tooedit, delete, or disable an alert.</span></span>

![Przyciski alertów](./media/data-factory-monitor-manage-app/AlertButtons.png)
