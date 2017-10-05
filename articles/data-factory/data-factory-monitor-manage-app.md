---
title: "Monitorowanie i zarządzanie nimi w potokach danych - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak monitorować i zarządzać nimi fabryki danych Azure i potoki przy użyciu aplikacji zarządzania i monitorowania."
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
ms.openlocfilehash: d5a2d1f3d85b8a2212326cfcfd0ba5d80356b769
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-monitoring-and-management-app"></a><span data-ttu-id="6f0f0-103">Monitorowanie i zarządzanie nimi potoki fabryki danych Azure przy użyciu aplikacji monitorowanie i zarządzanie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f0f0-104">Przy użyciu portalu Azure/Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f0f0-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="6f0f0-105">Przy użyciu monitorowania i zarządzania aplikacjami</span><span class="sxs-lookup"><span data-stu-id="6f0f0-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="6f0f0-106">W tym artykule opisano sposób użycia aplikacji zarządzania i monitorowania do monitorowania, zarządzania i debugowania potoki z fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-106">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="6f0f0-107">Zawiera również informacje dotyczące sposobu tworzenia alerty, Otrzymuj powiadomienia dotyczące niepowodzeń.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-107">It also provides information on how to create alerts to get notified on failures.</span></span> <span data-ttu-id="6f0f0-108">Możesz rozpocząć pracę z przy użyciu aplikacji od obejrzenia poniższego klipu wideo:</span><span class="sxs-lookup"><span data-stu-id="6f0f0-108">You can get started with using the application by watching the following video:</span></span>

> [!NOTE]
> <span data-ttu-id="6f0f0-109">Interfejs użytkownika pokazano wideo może nie pasować zobaczyć w portalu.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-109">The user interface shown in the video may not exactly match what you see in the portal.</span></span> <span data-ttu-id="6f0f0-110">Jest nieco starszy, ale pojęcia pozostają takie same.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-110">It's slightly older, but concepts remain the same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-the-monitoring-and-management-app"></a><span data-ttu-id="6f0f0-111">Uruchom aplikacji do zarządzania i monitorowania</span><span class="sxs-lookup"><span data-stu-id="6f0f0-111">Launch the Monitoring and Management app</span></span>
<span data-ttu-id="6f0f0-112">Aby uruchomić Monitor i zarządzania aplikacji, kliknij przycisk **Monitor & Zarządzaj** Kafelek na **fabryki danych** bloku fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-112">To launch the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span></span>

![Monitorowanie kafelka na stronie głównej fabryki danych](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="6f0f0-114">Monitorowanie i zarządzanie aplikacji, Otwórz w osobnym oknie powinny być widoczne.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-114">You should see the Monitoring and Management app open in a separate window.</span></span>  

![Aplikacja do monitorowania i zarządzania](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="6f0f0-116">Jeśli zobaczysz, że przeglądarki sieci web jest zablokowany na "Autoryzowanie...", wyczyść **zablokować pliki cookie innych firm, a dane lokacji** pole wyboru--lub Zachowaj ono zaznaczone, utworzyć wyjątek **login.microsoftonline.com**, i Spróbuj ponownie otworzyć aplikację.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-116">If you see that the web browser is stuck at "Authorizing...", clear the **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try to open the app again.</span></span>


<span data-ttu-id="6f0f0-117">Na liście okien działania w środkowym okienku zobaczysz okno działania przy każdym uruchomieniu działania.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-117">In the Activity Windows list in the middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="6f0f0-118">Na przykład jeśli masz działania zaplanowane co godzinę przez pięć godzin, zobacz pięć okien działania związane z pięciu wycinków danych.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-118">For example, if you have the activity scheduled to run hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="6f0f0-119">Jeśli nie widzisz okien działania na liście u dołu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6f0f0-119">If you don't see activity windows in the list at the bottom, do the following:</span></span>
 
- <span data-ttu-id="6f0f0-120">Aktualizacja **godzina rozpoczęcia** i **czas zakończenia** filtrów w górnej odpowiada godziny rozpoczęcia i zakończenia potoku sieci, a następnie kliknij przycisk **Zastosuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-120">Update the **start time** and **end time** filters at the top to match the start and end times of your pipeline, and then click the **Apply** button.</span></span>  
- <span data-ttu-id="6f0f0-121">Lista okien działania nie zostanie automatycznie odświeżony.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-121">The Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="6f0f0-122">Kliknij przycisk **Odśwież** przycisk na pasku narzędzi w **okien działania** listy.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-122">Click the **Refresh** button on the toolbar in the **Activity Windows** list.</span></span>  

<span data-ttu-id="6f0f0-123">Jeśli nie masz aplikacji fabryki danych, aby przetestować te kroki samouczka wykonaj: [skopiowanie danych z magazynu obiektów Blob do bazy danych SQL przy użyciu fabryki danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6f0f0-123">If you don't have a Data Factory application to test these steps with, do the tutorial: [copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-the-monitoring-and-management-app"></a><span data-ttu-id="6f0f0-124">Informacje o monitorowaniu i aplikacji do zarządzania</span><span class="sxs-lookup"><span data-stu-id="6f0f0-124">Understand the Monitoring and Management app</span></span>
<span data-ttu-id="6f0f0-125">Dostępne są trzy karty po lewej stronie: **Eksploratora zasobów**, **widoków monitorowania**, i **alerty**.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-125">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="6f0f0-126">Pierwszej karcie (**Eksploratora zasobów**) jest domyślnie zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-126">The first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="6f0f0-127">Eksplorator zasobów</span><span class="sxs-lookup"><span data-stu-id="6f0f0-127">Resource Explorer</span></span>
<span data-ttu-id="6f0f0-128">Zostanie wyświetlony poniżej:</span><span class="sxs-lookup"><span data-stu-id="6f0f0-128">You see the following:</span></span>

* <span data-ttu-id="6f0f0-129">Eksplorator zasobów **widok drzewa** w okienku po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-129">The Resource Explorer **tree view** in the left pane.</span></span>
* <span data-ttu-id="6f0f0-130">**Widoku diagramu** u góry w środkowym okienku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-130">The **Diagram View** at the top in the middle pane.</span></span>
* <span data-ttu-id="6f0f0-131">**Okien działania** listy u dołu w środkowym okienku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-131">The **Activity Windows** list at the bottom in the middle pane.</span></span>
* <span data-ttu-id="6f0f0-132">**Właściwości**, **działania okna Eksploratora**, i **skryptu** karty w okienku po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-132">The **Properties**, **Activity Window Explorer**, and **Script** tabs in the right pane.</span></span>

<span data-ttu-id="6f0f0-133">W Eksploratorze zasobów zobacz temat wszystkie zasoby (potoki, zestawy danych połączonych usług) w fabryce danych w widoku drzewa.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span></span> <span data-ttu-id="6f0f0-134">Po wybraniu obiektu, w Eksploratorze zasobów:</span><span class="sxs-lookup"><span data-stu-id="6f0f0-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="6f0f0-135">Skojarzonej jednostki fabryki danych zostanie wyróżniona w widoku diagramu.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-135">The associated Data Factory entity is highlighted in the Diagram View.</span></span>
* <span data-ttu-id="6f0f0-136">[Skojarzone działanie windows](data-factory-scheduling-and-execution.md) zostały wyróżnione na liście okien działania u dołu.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span></span>  
* <span data-ttu-id="6f0f0-137">Właściwości wybranego obiektu są wyświetlane w oknie właściwości w okienku po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-137">The properties of the selected object are shown in the Properties window in the right pane.</span></span>
* <span data-ttu-id="6f0f0-138">Definicja JSON wybranego obiektu jest wyświetlany, jeśli ma to zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-138">The JSON definition of the selected object is shown, if applicable.</span></span> <span data-ttu-id="6f0f0-139">Na przykład: połączonej usługi, zestawu danych lub potoku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Eksplorator zasobów](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="6f0f0-141">Zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md) artykułu, aby uzyskać szczegółowe informacje o pojęciach dotyczących działania systemu windows.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-141">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="6f0f0-142">Widok diagramu</span><span class="sxs-lookup"><span data-stu-id="6f0f0-142">Diagram View</span></span>
<span data-ttu-id="6f0f0-143">Widok diagramu fabryki danych zapewnia jeden szkła monitorować i zarządzać fabryki danych i jego zasoby.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-143">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span></span> <span data-ttu-id="6f0f0-144">Po wybraniu jednostki fabryki danych (dataset/potoku) w widoku diagramu:</span><span class="sxs-lookup"><span data-stu-id="6f0f0-144">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span></span>

* <span data-ttu-id="6f0f0-145">Obiekt fabryki danych wybrano w widoku drzewa.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-145">The data factory entity is selected in the tree view.</span></span>
* <span data-ttu-id="6f0f0-146">Skojarzone działanie systemu windows są wyróżnione na liście działania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-146">The associated activity windows are highlighted in the Activity Windows list.</span></span>
* <span data-ttu-id="6f0f0-147">Właściwości wybranego obiektu są wyświetlane w oknie właściwości.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-147">The properties of the selected object are shown in the Properties window.</span></span>

<span data-ttu-id="6f0f0-148">Po włączeniu potoku (nie jest w stanie wstrzymania) jest wyświetlany zielony linią:</span><span class="sxs-lookup"><span data-stu-id="6f0f0-148">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Potok uruchomiona](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="6f0f0-150">Można wstrzymać, wznowić lub zakończenie potoku, wybierając ją w widoku diagramu i za pomocą przycisków na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-150">You can pause, resume, or terminate a pipeline by selecting it in the diagram view and using the buttons on the command bar.</span></span>

![Wstrzymanie/wznowienie na pasku poleceń](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="6f0f0-152">Istnieją trzy przyciski paska poleceń dla potoku, w widoku diagramu.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-152">There are three command bar buttons for the pipeline in the Diagram View.</span></span> <span data-ttu-id="6f0f0-153">Drugi przycisk służy do wstrzymywania potoku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-153">You can use the second button to pause the pipeline.</span></span> <span data-ttu-id="6f0f0-154">Wstrzymywanie nie przerwanie działania aktualnie uruchomione i pozwala przejść do zakończenia.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-154">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span></span> <span data-ttu-id="6f0f0-155">Trzeci przycisk potoku wstrzymuje i kończy istniejące wykonywanych działań.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-155">The third button pauses the pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="6f0f0-156">Pierwszy przycisk wznawia potoku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-156">The first button resumes the pipeline.</span></span> <span data-ttu-id="6f0f0-157">Wstrzymanie planowaną zmienia kolor potoku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-157">When your pipeline is paused, the color of the pipeline changes.</span></span> <span data-ttu-id="6f0f0-158">Na przykład wstrzymanie potoku wygląda jak na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="6f0f0-158">For example, a paused pipeline looks like in the following image:</span></span> 

![Wstrzymane potoku](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="6f0f0-160">Możesz wybrać wiele potoki dwóch lub więcej za pomocą klawisza Ctrl.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-160">You can multi-select two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="6f0f0-161">Przyciski paska poleceń służy do wstrzymanie/wznowienie potoki wielu naraz.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-161">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="6f0f0-162">Można również kliknij prawym przyciskiem myszy potoku i wybierz opcję, aby wstrzymać, wznowić lub przerywania potoku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-162">You can also right-click a pipeline and select options to suspend, resume, or terminate a pipeline.</span></span> 

![Menu kontekstowe dla potoku](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="6f0f0-164">Kliknij przycisk **Otwórz potoku** opcji, aby zobaczyć wszystkie działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-164">Click the **Open pipeline** option to see all the activities in the pipeline.</span></span> 

![Menu Otwórz potok](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="6f0f0-166">W widoku otwartą potoku wyświetlane są wszystkie działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-166">In the opened pipeline view, you see all activities in the pipeline.</span></span> <span data-ttu-id="6f0f0-167">W tym przykładzie jest tylko jedno działanie: działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Otwarty potoku](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="6f0f0-169">Aby powrócić do poprzedniego widoku, kliknij przycisk Nazwa fabryki danych w menu stron nadrzędnych u góry.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-169">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span></span>

<span data-ttu-id="6f0f0-170">W widoku potoku po wybraniu wyjściowy zestaw danych lub gdy mysz przesuwa się nad wyjściowy zestaw danych, zobaczysz okno podręczne działania systemu Windows dla tego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-170">In the pipeline view, when you select an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span></span>

![Okno podręczne działania systemu Windows](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="6f0f0-172">Możesz kliknąć okno działania, aby wyświetlić szczegóły dla niego w **właściwości** okna w okienku po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-172">You can click an activity window to see details for it in the **Properties** window in the right pane.</span></span>

![Działanie właściwości okna](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="6f0f0-174">W okienku po prawej stronie, przełącz się do **działania okna Eksploratora** kartę, aby zobaczyć więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-174">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span></span>

![Działanie okno Eksploratora](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="6f0f0-176">Zobacz też **rozpoznać zmienne** dla każdego próba uruchomienia działania w **prób** sekcji.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-176">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span></span>

![Zmienne rozwiązany](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="6f0f0-178">Przełącz się do **skryptu** kartę, aby wyświetlić definicji skryptu JSON dla wybranego obiektu.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-178">Switch to the **Script** tab to see the JSON script definition for the selected object.</span></span>   

![Karta skryptu](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="6f0f0-180">Można wyświetlić okien działania w trzech miejscach:</span><span class="sxs-lookup"><span data-stu-id="6f0f0-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="6f0f0-181">Okienko wyskakujące okien działania w widoku diagramu (w środkowym okienku).</span><span class="sxs-lookup"><span data-stu-id="6f0f0-181">The Activity Windows pop-up in the Diagram View (middle pane).</span></span>
* <span data-ttu-id="6f0f0-182">Eksplorator okna działania w okienku po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-182">The Activity Window Explorer in the right pane.</span></span>
* <span data-ttu-id="6f0f0-183">Lista okien działania w dolnym okienku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-183">The Activity Windows list in the bottom pane.</span></span>

<span data-ttu-id="6f0f0-184">W oknie podręcznym okien działania i działania okna Eksploratora można przewijać w poprzednim tygodniu i następnym tygodniu za pomocą strzałki w lewo i w prawo.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-184">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span></span>

![Strzałki prawej/lewej strony okna Eksploratora działania](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="6f0f0-186">W dolnej części widoku diagramu, zobacz tych przycisków: powiększenia powiększanie, zmniejszanie, aby dopasować, powiększenie 100%, Zablokuj układ.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-186">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="6f0f0-187">**Układu blokady** przycisk zapobiega przypadkowemu przenoszeniu tabel i potoków w widoku diagramu.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-187">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span></span> <span data-ttu-id="6f0f0-188">Jest on domyślnie.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-188">It's on by default.</span></span> <span data-ttu-id="6f0f0-189">Można ją wyłączyć i przenosić jednostek na diagramie.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-189">You can turn it off and move entities around in the diagram.</span></span> <span data-ttu-id="6f0f0-190">Wyłączenie opcji, można użyć przycisku ostatniej ma automatycznie tabele i potoki.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-190">When you turn it off, you can use the last button to automatically position tables and pipelines.</span></span> <span data-ttu-id="6f0f0-191">Za pomocą kółka myszy, można powiększyć lub pomniejszyć.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-191">You can also zoom in or out by using the mouse wheel.</span></span>

![Diagram przedstawiający polecenia powiększenia widoku](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="6f0f0-193">Lista działania systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6f0f0-193">Activity Windows list</span></span>
<span data-ttu-id="6f0f0-194">Na liście okien działania w dolnej części środkowym okienku zostaną wyświetlone wszystkie okna działania dla zestawu danych, który wybrano w widoku diagramu lub Eksploratora zasobów.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-194">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span></span> <span data-ttu-id="6f0f0-195">Domyślnie lista jest w kolejności malejącej, co oznacza, że wyświetlane najnowsze okna działanie u góry.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-195">By default, the list is in descending order, which means that you see the latest activity window at the top.</span></span>

![Lista działania systemu Windows](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="6f0f0-197">Ta lista nie automatycznego odświeżania, należy więc przycisk Odśwież na pasku narzędzi go ręcznie odświeżyć.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-197">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span></span>  

<span data-ttu-id="6f0f0-198">Działanie systemu windows może być w jednym z następujących stanów:</span><span class="sxs-lookup"><span data-stu-id="6f0f0-198">Activity windows can be in one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="6f0f0-199">Stan</span><span class="sxs-lookup"><span data-stu-id="6f0f0-199">Status</span></span></th><th align="left"><span data-ttu-id="6f0f0-200">Podstan</span><span class="sxs-lookup"><span data-stu-id="6f0f0-200">Substatus</span></span></th><th align="left"><span data-ttu-id="6f0f0-201">Opis</span><span class="sxs-lookup"><span data-stu-id="6f0f0-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="6f0f0-202">Oczekiwanie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-202">Waiting</span></span></td><td><span data-ttu-id="6f0f0-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="6f0f0-203">ScheduleTime</span></span></td><td><span data-ttu-id="6f0f0-204">Czas nie pochodzą okna działania do uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-204">The time hasn't come for the activity window to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6f0f0-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="6f0f0-205">DatasetDependencies</span></span></td><td><span data-ttu-id="6f0f0-206">Zależności strumienia wychodzącego nie są gotowe.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-206">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6f0f0-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="6f0f0-207">ComputeResources</span></span></td><td><span data-ttu-id="6f0f0-208">Zasoby obliczeniowe są niedostępne.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-208">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6f0f0-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="6f0f0-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="6f0f0-210">Wszystkie wystąpienia działania są zajęte uruchamianiem innych okien działania.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-210">All the activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6f0f0-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="6f0f0-211">ActivityResume</span></span></td><td><span data-ttu-id="6f0f0-212">Działanie jest wstrzymane i nie można uruchomić okien działania, dopóki nie zostanie wznowione.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-212">The activity is paused and can't run the activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6f0f0-213">Spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-213">Retry</span></span></td><td><span data-ttu-id="6f0f0-214">Ponawiane wykonania działania.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-214">The activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6f0f0-215">Walidacja</span><span class="sxs-lookup"><span data-stu-id="6f0f0-215">Validation</span></span></td><td><span data-ttu-id="6f0f0-216">Weryfikacja jeszcze się nie rozpoczął.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6f0f0-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="6f0f0-217">ValidationRetry</span></span></td><td><span data-ttu-id="6f0f0-218">Sprawdzanie poprawności oczekuje na ponowienie próby.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-218">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="6f0f0-219">W toku</span><span class="sxs-lookup"><span data-stu-id="6f0f0-219">InProgress</span></span></td><td><span data-ttu-id="6f0f0-220">Sprawdzanie poprawności</span><span class="sxs-lookup"><span data-stu-id="6f0f0-220">Validating</span></span></td><td><span data-ttu-id="6f0f0-221">Trwa sprawdzanie poprawności.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="6f0f0-222">Okno działania jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-222">The activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="6f0f0-223">Nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="6f0f0-223">Failed</span></span></td><td><span data-ttu-id="6f0f0-224">Upłynął limit czasu</span><span class="sxs-lookup"><span data-stu-id="6f0f0-224">TimedOut</span></span></td><td><span data-ttu-id="6f0f0-225">Wykonywanie działania trwało dłużej niż jest dozwolonych przez działanie.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-225">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6f0f0-226">Anulowane</span><span class="sxs-lookup"><span data-stu-id="6f0f0-226">Canceled</span></span></td><td><span data-ttu-id="6f0f0-227">Okno działanie zostało anulowane przez akcję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-227">The activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6f0f0-228">Walidacja</span><span class="sxs-lookup"><span data-stu-id="6f0f0-228">Validation</span></span></td><td><span data-ttu-id="6f0f0-229">Weryfikacja nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="6f0f0-230">Okno działania nie powiodło się można wygenerować lub sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-230">The activity window failed to be generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="6f0f0-231">Gotowe</span><span class="sxs-lookup"><span data-stu-id="6f0f0-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="6f0f0-232">Okno działania jest gotowy do użycia.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-232">The activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6f0f0-233">Pominięto</span><span class="sxs-lookup"><span data-stu-id="6f0f0-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="6f0f0-234">Okno działania nie został przetworzony.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-234">The activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6f0f0-235">Brak</span><span class="sxs-lookup"><span data-stu-id="6f0f0-235">None</span></span></td><td>-</td><td><span data-ttu-id="6f0f0-236">Okno działania miał poprzednio inny stan, ale został zresetowany.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-236">An activity window used to exist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="6f0f0-237">Po kliknięciu okno działania na liście, zobacz szczegóły w **Eksploratora Windows działania** lub **właściwości** okna po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-237">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span></span>

![Działanie okno Eksploratora](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="6f0f0-239">Odśwież działania systemu windows</span><span class="sxs-lookup"><span data-stu-id="6f0f0-239">Refresh activity windows</span></span>
<span data-ttu-id="6f0f0-240">Szczegóły nie są automatycznie odświeżane, należy więc przycisk Odśwież (drugi przycisk) na pasku poleceń, aby ręcznie odświeżyć listę działania systemu windows.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-240">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="6f0f0-241">Okno właściwości</span><span class="sxs-lookup"><span data-stu-id="6f0f0-241">Properties window</span></span>
<span data-ttu-id="6f0f0-242">Okno właściwości znajduje się w okienku prawej zarządzania i monitorowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-242">The Properties window is in the right-most pane of the Monitoring and Management app.</span></span>

![Okno właściwości](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="6f0f0-244">Wyświetla właściwości dla elementu wybranego w Eksploratorze zasobów (widok drzewa), widok diagramu lub listę okien działania.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-244">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="6f0f0-245">Działanie okno Eksploratora</span><span class="sxs-lookup"><span data-stu-id="6f0f0-245">Activity Window Explorer</span></span>
<span data-ttu-id="6f0f0-246">**Działania okna Eksploratora** okna znajduje się w okienku prawej zarządzania i monitorowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-246">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span></span> <span data-ttu-id="6f0f0-247">Wyświetla szczegółowe informacje o oknie działania wybranego w oknie podręcznym okien działania lub listę okien działania.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-247">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span></span>

![Działanie okno Eksploratora](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="6f0f0-249">Można przełączyć do innego okna działania, klikając go w widoku kalendarza u góry.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-249">You can switch to another activity window by clicking it in the calendar view at the top.</span></span> <span data-ttu-id="6f0f0-250">Umożliwia także przycisk strzałki w lewo/Strzałka w prawo na górze wyświetlić okien działania z poprzedniego tygodnia lub następnym tygodniu.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-250">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span></span>

<span data-ttu-id="6f0f0-251">Przyciski paska narzędzi w okienku u dołu umożliwia ponownie uruchom okno działania lub Odśwież dane w okienku.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-251">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span></span>

### <a name="script"></a><span data-ttu-id="6f0f0-252">Skrypt</span><span class="sxs-lookup"><span data-stu-id="6f0f0-252">Script</span></span>
<span data-ttu-id="6f0f0-253">Można użyć **skryptu** kartę, aby wyświetlić definicji JSON wybranej jednostki fabryki danych (połączonej usługi, zestawu danych lub potoku).</span><span class="sxs-lookup"><span data-stu-id="6f0f0-253">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Karta skryptu](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="6f0f0-255">Używanie widoków systemu</span><span class="sxs-lookup"><span data-stu-id="6f0f0-255">Use system views</span></span>
<span data-ttu-id="6f0f0-256">Monitorowanie i zarządzanie aplikacja zawiera widoki wbudowanych systemu (**ostatnie okien działania**, **nie powiodło się okien działania**, **okien działania w toku**) zezwalające na Możesz wyświetlić fabrykę danych w oknie ostatnie/nie powiodło się/w trakcie działania.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-256">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="6f0f0-257">Przełącz się do **widoków monitorowania** karcie po lewej stronie, klikając go.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-257">Switch to the **Monitoring Views** tab on the left by clicking it.</span></span>

![Karta widoków monitorowania](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="6f0f0-259">Obecnie istnieją trzy widoki systemowe, które są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="6f0f0-260">Wybierz opcję, aby wyświetlić ostatnie działanie systemu windows, windows działanie nie powiodło się lub okien działania w toku na liście działania systemu Windows (w dolnej części środkowym okienku).</span><span class="sxs-lookup"><span data-stu-id="6f0f0-260">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span></span>

<span data-ttu-id="6f0f0-261">Po wybraniu **ostatnie okien działania** opcji, zobacz wszystkie ostatnie okien działania malejąco **ostatniej próby czasu**.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-261">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span></span>

<span data-ttu-id="6f0f0-262">Można użyć **nie powiodło się okien działania** widok, aby wyświetlić wszystkich okien działania nie powiodło się na liście.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-262">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span></span> <span data-ttu-id="6f0f0-263">Wybierz przedział działanie nie powiodło się na liście, aby zobaczyć szczegółowe informacje o nim w **właściwości** okna lub **działania okna Eksploratora**.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-263">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span></span> <span data-ttu-id="6f0f0-264">Możesz również pobrać wszystkie dzienniki dla okna działanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="6f0f0-265">Sortuj i Filtruj działania systemu windows</span><span class="sxs-lookup"><span data-stu-id="6f0f0-265">Sort and filter activity windows</span></span>
<span data-ttu-id="6f0f0-266">Zmień **godzina rozpoczęcia** i **czas zakończenia** ustawienia paska poleceń do systemu windows działanie filtru.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-266">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span></span> <span data-ttu-id="6f0f0-267">Po zmianie godziny rozpoczęcia i godzina zakończenia, kliknij przycisk Dalej, aby odświeżyć listę okien działania czas zakończenia.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-267">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span></span>

![Czas rozpoczęcia i zakończenia](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="6f0f0-269">Obecnie wszystkie godziny są w formacie UTC w aplikacji zarządzania i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-269">Currently, all times are in UTC format in the Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="6f0f0-270">W **listę okien działania**, kliknij nazwę kolumny (na przykład: stanu).</span><span class="sxs-lookup"><span data-stu-id="6f0f0-270">In the **Activity Windows list**, click the name of a column (for example: Status).</span></span>

![Działanie systemu Windows lista kolumn menu](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="6f0f0-272">Można wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6f0f0-272">You can do the following:</span></span>

* <span data-ttu-id="6f0f0-273">Sortowanie w kolejności rosnącej.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-273">Sort in ascending order.</span></span>
* <span data-ttu-id="6f0f0-274">Sortowanie w kolejności malejącej.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-274">Sort in descending order.</span></span>
* <span data-ttu-id="6f0f0-275">Filtruj według jednego lub więcej wartości (gotowe, oczekiwania itd.).</span><span class="sxs-lookup"><span data-stu-id="6f0f0-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="6f0f0-276">Po określeniu filtru w kolumnie jest wyświetlany przycisk filtru włączone dla tej kolumny, co oznacza, że wartości w kolumnie są filtrowane wartości.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-276">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span></span>

![Filtrować według kolumny listy działania systemu Windows](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="6f0f0-278">Aby wyczyścić filtry służy tym samym oknie podręcznym.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-278">You can use the same pop-up window to clear filters.</span></span> <span data-ttu-id="6f0f0-279">Aby wyczyścić wszystkie filtry listę okien działania, kliknij przycisk Wyczyść filtr na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-279">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span></span>

![Wyczyść wszystkie filtry listę okien działania](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="6f0f0-281">Akcje usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="6f0f0-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="6f0f0-282">Uruchom ponownie wybrane działanie systemu windows</span><span class="sxs-lookup"><span data-stu-id="6f0f0-282">Rerun selected activity windows</span></span>
<span data-ttu-id="6f0f0-283">Wybierz przedział działania, kliknij strzałkę w dół dla przycisku pierwszej pasek poleceń, a następnie wybierz **Uruchom ponownie** / **ponownie z powyżej w potoku**.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-283">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="6f0f0-284">Po wybraniu **ponownie z powyżej w potoku** opcji zwracające on również wszystkich okien działania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-284">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="6f0f0-285">![Ponownie uruchom okno działania](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="6f0f0-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="6f0f0-286">Można również wybrać wiele okien działania na liście i uruchom je ponownie w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-286">You can also select multiple activity windows in the list and rerun them at the same time.</span></span> <span data-ttu-id="6f0f0-287">Można filtrować na podstawie stanu działania z systemem windows (na przykład: ****) — a następnie ponownie uruchom okien działania nie powiodło się po usunięciu problemu, który powoduje, że okien działania się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-287">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span></span> <span data-ttu-id="6f0f0-288">Zobacz sekcję poniżej, aby uzyskać więcej informacji dotyczących filtrowania okien działania na liście.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-288">See the following section for details about filtering activity windows in the list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="6f0f0-289">Wstrzymanie/wznowienie wielu potoki</span><span class="sxs-lookup"><span data-stu-id="6f0f0-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="6f0f0-290">Możesz multiselect potoki dwóch lub więcej za pomocą klawisza Ctrl.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-290">You can multiselect two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="6f0f0-291">Przyciski paska poleceń (które są wyróżnione kolorem czerwonym prostokątem na poniższej ilustracji) służy do wstrzymanie/wznowienie je.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-291">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span></span>

![Wstrzymanie/wznowienie na pasku poleceń](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="6f0f0-293">Tworzenie alertów</span><span class="sxs-lookup"><span data-stu-id="6f0f0-293">Create alerts</span></span>
<span data-ttu-id="6f0f0-294">**Alerty** strony pozwala na tworzenie alertów i wyświetlanie/edytowanie/usuwanie istniejące alerty.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-294">The **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="6f0f0-295">Użytkownik może również Włącz/Wyłącz alert.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="6f0f0-296">Aby wyświetlić stronę alertów, kliknij przycisk **alerty** kartę.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-296">To see the Alerts page, click the **Alerts** tab.</span></span>

![Karta alerty](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="to-create-an-alert"></a><span data-ttu-id="6f0f0-298">Aby utworzyć alert</span><span class="sxs-lookup"><span data-stu-id="6f0f0-298">To create an alert</span></span>
1. <span data-ttu-id="6f0f0-299">Kliknij przycisk **dodać Alert** można dodać alert.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-299">Click **Add Alert** to add an alert.</span></span> <span data-ttu-id="6f0f0-300">Zostanie wyświetlony **szczegóły** strony.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-300">You see the **Details** page.</span></span>

    ![Utwórz alerty — strona szczegółów](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="6f0f0-302">Określ **nazwa** i **opis** alert, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-302">Specify the **Name** and **Description** for the alert, and click **Next**.</span></span> <span data-ttu-id="6f0f0-303">Powinny pojawić się **filtry** strony.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-303">You should see the **Filters** page.</span></span>

    ![Utwórz alerty — filtry strony](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="6f0f0-305">Wybierz **zdarzeń**, **stan**, i **podstanu** (opcjonalnie) mają Utwórz alert usługi fabryka danych dla, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-305">Select the **event**, **status**, and **substatus** (optional) that you want to create a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="6f0f0-306">Powinny pojawić się **adresatów** strony.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-306">You should see the **Recipients** page.</span></span>

    ![Utwórz alerty — strona adresatów](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="6f0f0-308">Wybierz **poczty E-mail Administratorzy subskrypcji** opcji lub wprowadź **e-mail administratora dodatkowe**i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-308">Select the **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="6f0f0-309">Powinien zostać wyświetlony alert na liście.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-309">You should see the alert in the list.</span></span>

    ![Lista alertów](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="6f0f0-311">Na liście alertów użyj przycisków, które są skojarzone z alertem do edycji/delete/Włącz/Wyłącz alert.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-311">In the Alerts list, use the buttons that are associated with the alert to edit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="6f0f0-312">Podstan zdarzeń/stanu</span><span class="sxs-lookup"><span data-stu-id="6f0f0-312">Event/status/substatus</span></span>
<span data-ttu-id="6f0f0-313">Poniższa tabela zawiera listę dostępnych zdarzeń oraz Stany (i podstany).</span><span class="sxs-lookup"><span data-stu-id="6f0f0-313">The following table provides the list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="6f0f0-314">Nazwa zdarzenia</span><span class="sxs-lookup"><span data-stu-id="6f0f0-314">Event name</span></span> | <span data-ttu-id="6f0f0-315">Stan</span><span class="sxs-lookup"><span data-stu-id="6f0f0-315">Status</span></span> | <span data-ttu-id="6f0f0-316">Podstan</span><span class="sxs-lookup"><span data-stu-id="6f0f0-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6f0f0-317">Działanie Uruchom wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-317">Activity Run Started</span></span> |<span data-ttu-id="6f0f0-318">Rozpoczęto</span><span class="sxs-lookup"><span data-stu-id="6f0f0-318">Started</span></span> |<span data-ttu-id="6f0f0-319">Uruchamianie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-319">Starting</span></span> |
| <span data-ttu-id="6f0f0-320">Działanie Uruchom Zakończono</span><span class="sxs-lookup"><span data-stu-id="6f0f0-320">Activity Run Finished</span></span> |<span data-ttu-id="6f0f0-321">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-321">Succeeded</span></span> |<span data-ttu-id="6f0f0-322">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-322">Succeeded</span></span> |
| <span data-ttu-id="6f0f0-323">Działanie Uruchom Zakończono</span><span class="sxs-lookup"><span data-stu-id="6f0f0-323">Activity Run Finished</span></span> |<span data-ttu-id="6f0f0-324">Nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="6f0f0-324">Failed</span></span> |<span data-ttu-id="6f0f0-325">Alokacja zasobów nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="6f0f0-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="6f0f0-326">Wykonanie nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="6f0f0-326">Failed Execution</span></span><br/><br/><span data-ttu-id="6f0f0-327">Upłynął limit czasu</span><span class="sxs-lookup"><span data-stu-id="6f0f0-327">Timed Out</span></span><br/><br/><span data-ttu-id="6f0f0-328">Sprawdzanie poprawności nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="6f0f0-328">Failed Validation</span></span><br/><br/><span data-ttu-id="6f0f0-329">porzucone</span><span class="sxs-lookup"><span data-stu-id="6f0f0-329">Abandoned</span></span> |
| <span data-ttu-id="6f0f0-330">Rozpoczęto tworzenie klastra HDI na żądanie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="6f0f0-331">Rozpoczęto</span><span class="sxs-lookup"><span data-stu-id="6f0f0-331">Started</span></span> |-|
| <span data-ttu-id="6f0f0-332">Pomyślnie utworzono klaster HDI na żądanie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="6f0f0-333">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-333">Succeeded</span></span> |-|
| <span data-ttu-id="6f0f0-334">Usunąć klaster HDI na żądanie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="6f0f0-335">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="6f0f0-335">Succeeded</span></span> |-|

### <a name="to-edit-delete-or-disable-an-alert"></a><span data-ttu-id="6f0f0-336">Aby edytować, usunąć lub wyłączyć alertu</span><span class="sxs-lookup"><span data-stu-id="6f0f0-336">To edit, delete, or disable an alert</span></span>

<span data-ttu-id="6f0f0-337">Użyj przycisków następujące (wyróżnionych kolorem czerwonym), aby edytować, usuwać lub Wyłącz alert.</span><span class="sxs-lookup"><span data-stu-id="6f0f0-337">Use the following buttons (highlighted in red) to edit, delete, or disable an alert.</span></span>

![Przyciski alertów](./media/data-factory-monitor-manage-app/AlertButtons.png)
