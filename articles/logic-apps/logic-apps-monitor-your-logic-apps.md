---
title: "Sprawdź stan, skonfiguruj rejestrowanie i uzyskiwanie alertów - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Stan Monitora wydajności dla usługi logic apps rejestrowanie danych diagnostycznych i Konfigurowanie alertów"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 4795f5728d4ce6ff21b97bc3fefd6a53e0c6a11b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="601a7-103">Monitorowanie stanu, konfigurowanie rejestrowania diagnostyki i Włącz alerty dla usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="601a7-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="601a7-104">Po [tworzenie i uruchamianie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md), można sprawdzić historię uruchomień, Historia wyzwalacza, stanu i wydajności.</span><span class="sxs-lookup"><span data-stu-id="601a7-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="601a7-105">Monitorowanie zdarzeń w czasie rzeczywistym i debugowanie bardziej rozbudowane, skonfiguruj [rejestrowania diagnostyki](#azure-diagnostics) aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="601a7-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="601a7-106">W ten sposób można [Znajdowanie i wyświetlać zdarzenia](#find-events), takie jak zdarzenia wyzwalacza, uruchom zdarzeń i zdarzenia akcji.</span><span class="sxs-lookup"><span data-stu-id="601a7-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="601a7-107">Możesz także użyć tej funkcji [danych diagnostycznych z innymi usługami](#extend-diagnostic-data), takie jak usługi Azure Storage i Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="601a7-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="601a7-108">Aby otrzymywać powiadomień o awarii lub innych możliwych problemów, skonfiguruj [alerty](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="601a7-108">To get notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="601a7-109">Na przykład można utworzyć alertu wykrywa "więcej niż pięć uruchamia się niepowodzeniem w ciągu godziny."</span><span class="sxs-lookup"><span data-stu-id="601a7-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="601a7-110">Można również skonfigurować monitorowanie, śledzenie i rejestrowanie programowo przy użyciu [ustawienia zdarzeń diagnostyki Azure i właściwości](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="601a7-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="601a7-111">Uruchamia widok i historii wyzwalacza dla aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="601a7-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="601a7-112">Aby znaleźć aplikację logiki w [portalu Azure](https://portal.azure.com), w menu głównym Azure wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="601a7-112">To find your logic app in the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **More services**.</span></span> <span data-ttu-id="601a7-113">W polu wyszukiwania Znajdź "aplikacje logiki", a następnie wybierz pozycję **Logic apps**.</span><span class="sxs-lookup"><span data-stu-id="601a7-113">In the search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Znajdź aplikację logiki](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="601a7-115">Azure portal zawiera wszystkie aplikacje logiki, które są skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="601a7-115">The Azure portal shows all the logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="601a7-116">Wybierz aplikację logiki, a następnie wybierz **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="601a7-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="601a7-117">Portalu Azure zawiera historię uruchomień i historii wyzwalacza dla aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="601a7-117">The Azure portal shows the runs history and trigger history for your logic app.</span></span> <span data-ttu-id="601a7-118">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="601a7-118">For example:</span></span>

   ![Historia i wyzwalacza historii uruchomieniu aplikacji logiki](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="601a7-120">**Uruchamia historii** zawiera wszystkie elementy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="601a7-120">**Runs history** shows all the runs for your logic app.</span></span> 
   * <span data-ttu-id="601a7-121">**Wyzwalanie historii** pokazuje wszystkie działania wyzwalacza aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="601a7-121">**Trigger History** shows all the trigger activity for your logic app.</span></span>

   <span data-ttu-id="601a7-122">Opis stanu, zobacz [rozwiązywania problemów z aplikacją logiki](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="601a7-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="601a7-123">Jeśli nie możesz znaleźć dane, które należy oczekiwać na pasku narzędzi wybierz **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="601a7-123">If you don't find the data that you expect, on the toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="601a7-124">Aby wyświetlić kroki z określonego działania, w obszarze **uruchamia historii**, wybierz opcję uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="601a7-124">To view the steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="601a7-125">Widok monitora zawiera każdego kroku w uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="601a7-125">The monitor view shows each step in that run.</span></span> <span data-ttu-id="601a7-126">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="601a7-126">For example:</span></span>

   ![Akcje dla określonego przebiegu](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="601a7-128">Aby uzyskać więcej informacji o przebiegu, wybierz **Uruchom szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="601a7-128">To get more details about the run, choose **Run Details**.</span></span> <span data-ttu-id="601a7-129">Te informacje zawiera podsumowanie kroków, stan, dane wejściowe i wyniki dla przebiegu.</span><span class="sxs-lookup"><span data-stu-id="601a7-129">This information summarizes the steps, status, inputs, and outputs for the run.</span></span> 

   ![Wybierz polecenie "Uruchom szczegóły"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="601a7-131">Na przykład można uzyskać przy uruchomieniu **identyfikator korelacji**, który może być konieczne, gdy używasz [interfejsu API REST dla usługi Logic Apps](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="601a7-131">For example, you can get the run's **Correlation ID**, which you might need when you use the [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="601a7-132">Aby uzyskać szczegółowe informacje o określonym kroku, należy wybrać tego kroku.</span><span class="sxs-lookup"><span data-stu-id="601a7-132">To get details about a specific step, choose that step.</span></span> <span data-ttu-id="601a7-133">Teraz możesz przejrzeć szczegóły, takie jak wejść, wyjść i wszelkie błędy, które wystąpiły w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="601a7-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="601a7-134">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="601a7-134">For example:</span></span>

   ![Szczegółowe informacje krok](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="601a7-136">Wszystkie szczegóły środowiska uruchomieniowego i zdarzenia są szyfrowane w ramach usługi Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="601a7-136">All runtime details and events are encrypted within the Logic Apps service.</span></span> <span data-ttu-id="601a7-137">Są one odszyfrowane tylko wtedy, gdy użytkownik zażąda do wyświetlania tych danych.</span><span class="sxs-lookup"><span data-stu-id="601a7-137">They are decrypted only when a user requests to view that data.</span></span> <span data-ttu-id="601a7-138">Można też kontrolować dostęp do tych zdarzeń o [based kontroli dostępu (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="601a7-138">You can also control access to these events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="601a7-139">Aby uzyskać szczegółowe informacje o zdarzeniu określonego wyzwalacza, przejdź wstecz do **omówienie** okienka.</span><span class="sxs-lookup"><span data-stu-id="601a7-139">To get details about a specific trigger event, go back to the **Overview** pane.</span></span> <span data-ttu-id="601a7-140">W obszarze **wyzwolenia historii**, wybierz zdarzenia wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="601a7-140">Under **Trigger history**, select the trigger event.</span></span> <span data-ttu-id="601a7-141">Teraz można przejrzeć szczegóły, takie jak wejściach i wyjściach, na przykład:</span><span class="sxs-lookup"><span data-stu-id="601a7-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Szczegóły danych wyjściowych zdarzenia wyzwalacza](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="601a7-143">Włącz diagnostykę, rejestrowanie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="601a7-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="601a7-144">Bardziej rozbudowane debugowanie z szczegóły środowiska uruchomieniowego i zdarzenia, można skonfigurować z funkcji rejestrowania diagnostyki [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="601a7-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="601a7-145">Analiza dzienników jest usługą [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) który monitoruje chmurze i lokalnych środowiskach, które pomagają zachować ich dostępności i wydajności.</span><span class="sxs-lookup"><span data-stu-id="601a7-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments to help you maintain their availability and performance.</span></span> 

<span data-ttu-id="601a7-146">Przed rozpoczęciem, musisz mieć obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="601a7-146">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="601a7-147">Dowiedz się [jak Utwórz obszar roboczy OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="601a7-147">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="601a7-148">W [portalu Azure](https://portal.azure.com), Znajdź i wybierz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="601a7-148">In the [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="601a7-149">W menu bloku aplikacji logiki w obszarze **monitorowanie**, wybierz **diagnostyki** > **ustawień diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="601a7-149">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Przejdź do monitorowania, diagnostyki, ustawień diagnostycznych](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="601a7-151">W obszarze **ustawień diagnostycznych**, wybierz **na**.</span><span class="sxs-lookup"><span data-stu-id="601a7-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Włączanie dzienników diagnostycznych](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="601a7-153">Teraz wybierz OMS kategorii obszaru roboczego i zdarzenia logowania, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="601a7-153">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="601a7-154">Wybierz **wysyłać do analizy dzienników**.</span><span class="sxs-lookup"><span data-stu-id="601a7-154">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="601a7-155">W obszarze **analizy dzienników**, wybierz **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="601a7-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="601a7-156">W obszarze **obszarów roboczych OMS**, wybierz obszar roboczy OMS na potrzeby rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="601a7-156">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="601a7-157">W obszarze **dziennika**, wybierz pozycję **WorkflowRuntime** kategorii.</span><span class="sxs-lookup"><span data-stu-id="601a7-157">Under **Log**, select the **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="601a7-158">Interwał metryki.</span><span class="sxs-lookup"><span data-stu-id="601a7-158">Choose the metric interval.</span></span>
   6. <span data-ttu-id="601a7-159">Gdy wszystko będzie gotowe, wybierz pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="601a7-159">When you're done, choose **Save**.</span></span>

   ![Wybierz obszar roboczy OMS i dane dotyczące rejestrowania](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="601a7-161">Teraz można znaleźć zdarzeń i inne dane dla zdarzenia wyzwalacza, uruchom zdarzenia i akcji.</span><span class="sxs-lookup"><span data-stu-id="601a7-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="601a7-162">Znajdź zdarzenia i dane aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="601a7-162">Find events and data for your logic app</span></span>

<span data-ttu-id="601a7-163">Aby znaleźć i wyświetlić zdarzenia w aplikacji logiki, takie jak wyzwolenia zdarzenia, uruchom zdarzenia i akcji, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="601a7-163">To find and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="601a7-164">W [portalu Azure](https://portal.azure.com), wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="601a7-164">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="601a7-165">Wyszukaj "analizy dzienników", a następnie wybierz **analizy dzienników** w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="601a7-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Wybierz pozycję "Analizy dzienników"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="601a7-167">W obszarze **analizy dzienników**, Znajdź i wybierz obszar roboczy OMS.</span><span class="sxs-lookup"><span data-stu-id="601a7-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Wybierz obszar roboczy OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="601a7-169">W obszarze **zarządzania**, wybierz **portalu OMS**.</span><span class="sxs-lookup"><span data-stu-id="601a7-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![Wybierz pozycję "Portalu OMS"](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="601a7-171">Na stronie głównej OMS wybierz **wyszukiwania dziennika**.</span><span class="sxs-lookup"><span data-stu-id="601a7-171">On your OMS home page, choose **Log Search**.</span></span>

   ![Na stronie głównej OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="601a7-173">— lub —</span><span class="sxs-lookup"><span data-stu-id="601a7-173">-or-</span></span>

   ![W menu OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="601a7-175">W polu wyszukiwania określ pola, które chcesz odnaleźć, a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="601a7-175">In the search box, specify a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="601a7-176">Po rozpoczęciu wprowadzania, OMS pokazuje, pasujących i operacje, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="601a7-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="601a7-177">Na przykład, aby znaleźć zdarzenia pierwszych 10, które wystąpiły, wprowadź i wybierz tego zapytania wyszukiwania: **kategorii = WorkflowRuntime | 10 pierwszych**</span><span class="sxs-lookup"><span data-stu-id="601a7-177">For example, to find the top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Wprowadź ciąg wyszukiwania](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="601a7-179">Dowiedz się więcej o [jak wyszukiwania danych analizy dzienników](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="601a7-179">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="601a7-180">Na stronie wyników na pasku po lewej stronie Wybierz przedział czasu, który chcesz wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="601a7-180">On the results page, in the left bar, choose the timeframe that you want to view.</span></span>
<span data-ttu-id="601a7-181">Aby zawęzić kwerendę, dodając filtr, wybierz **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="601a7-181">To refine your query by adding a filter, choose **+Add**.</span></span>

   ![Wybierz przedział czasu dla wyników zapytania](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="601a7-183">W obszarze **Dodaj filtry**, wprowadź nazwę filtru, aby umożliwić znalezienie filtr ma.</span><span class="sxs-lookup"><span data-stu-id="601a7-183">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="601a7-184">Wybierz filtr, a następnie wybierz pozycję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="601a7-184">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="601a7-185">W tym przykładzie użyto słowa "status" do znalezienia zdarzeń nie powiodło się w obszarze **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="601a7-185">This example uses the word "status" to find failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="601a7-186">Tutaj filtr dla **status_s** jest już wybrana.</span><span class="sxs-lookup"><span data-stu-id="601a7-186">Here the filter for **status_s** is already selected.</span></span>

   ![Wybierz filtr](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="601a7-188">Na pasku po lewej stronie wybierz wartości filtru, który chcesz użyć, a następnie wybierz pozycję **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="601a7-188">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   ![Wybierz wartości filtru, wybierz polecenie "Zastosuj"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="601a7-190">Teraz wróć do zapytania, które tworzysz.</span><span class="sxs-lookup"><span data-stu-id="601a7-190">Now return to the query that you're building.</span></span> <span data-ttu-id="601a7-191">Zapytanie jest aktualizowana z wybranego filtru i wartość.</span><span class="sxs-lookup"><span data-stu-id="601a7-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="601a7-192">Poprzednie wyniki teraz są zbyt filtrowane.</span><span class="sxs-lookup"><span data-stu-id="601a7-192">Your previous results are now filtered too.</span></span>

   ![Wróć do filtrowane wyniki zapytania](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="601a7-194">Aby zapisać kwerendę do użycia w przyszłości, należy wybrać **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="601a7-194">To save your query for future use, choose **Save**.</span></span> <span data-ttu-id="601a7-195">Dowiedz się [jak zapisać zapytanie](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="601a7-195">Learn [how to save your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="601a7-196">Rozszerzanie, jak i gdzie używać danych diagnostycznych z innymi usługami</span><span class="sxs-lookup"><span data-stu-id="601a7-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="601a7-197">Wraz z Azure Log Analytics można rozszerzyć, jak używasz aplikacji logiki danych diagnostycznych z innymi usługami Azure, na przykład:</span><span class="sxs-lookup"><span data-stu-id="601a7-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="601a7-198">Archiwum, które dzienniki diagnostyczne platformy Azure w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="601a7-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="601a7-199">Strumieniowe przesyłanie dzienników diagnostycznych platformy Azure do usługi Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="601a7-199">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="601a7-200">Następnie monitorowanie za pomocą telemetrii i analiza z innych usług, takich jak get w czasie rzeczywistym [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) i [usługi Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="601a7-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="601a7-201">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="601a7-201">For example:</span></span>

* [<span data-ttu-id="601a7-202">Strumień danych z usługi Event Hubs Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="601a7-202">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="601a7-203">Analizować dane przesyłane strumieniowo z usługi Stream Analytics i utworzyć pulpit nawigacyjny analiz w czasie rzeczywistym w usłudze Power BI</span><span class="sxs-lookup"><span data-stu-id="601a7-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="601a7-204">Oparte na opcje, które chcesz skonfigurować, upewnij się, że możesz pierwszy [utworzyć konto magazynu Azure](../storage/common/storage-create-storage-account.md) lub [tworzenia Centrum zdarzeń Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="601a7-204">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="601a7-205">Następnie wybierz opcje dla których chcesz wysyłać dane diagnostyczne:</span><span class="sxs-lookup"><span data-stu-id="601a7-205">Then select the options for where you want to send diagnostic data:</span></span>

![Wysyłanie danych do magazynu Azure konta lub zdarzenia koncentratora.](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="601a7-207">Okresy przechowywania mają zastosowanie tylko wtedy, gdy chcesz użyć konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="601a7-207">Retention periods apply only when you choose to use a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="601a7-208">Ustawianie alertów dla aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="601a7-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="601a7-209">Aby monitorować Przekroczono próg dla aplikacji logiki lub określonych metryk, skonfiguruj [alertów w usłudze Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="601a7-209">To monitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="601a7-210">Dowiedz się więcej o [metryki na platformie Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="601a7-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="601a7-211">Aby skonfigurować alerty bez [Azure Log Analytics](../log-analytics/log-analytics-overview.md), wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="601a7-211">To set up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="601a7-212">Bardziej zaawansowane kryteria alertów i akcji [Konfigurowanie analizy dzienników](#azure-diagnostics) zbyt.</span><span class="sxs-lookup"><span data-stu-id="601a7-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="601a7-213">W menu bloku aplikacji logiki w obszarze **monitorowanie**, wybierz **diagnostyki** > **reguły alertów** > **Dodaj alert** w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="601a7-213">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Dodawanie alertu dla aplikacji logiki](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="601a7-215">Na **dodać regułę alertu** bloku tworzenia alertu, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="601a7-215">On the **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="601a7-216">W obszarze **zasobów**, wybierz aplikację logiki, jeśli nie już wybrana.</span><span class="sxs-lookup"><span data-stu-id="601a7-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="601a7-217">Nadaj nazwę i opis alertu.</span><span class="sxs-lookup"><span data-stu-id="601a7-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="601a7-218">Wybierz **Metryka** lub zdarzenie, które mają być śledzone.</span><span class="sxs-lookup"><span data-stu-id="601a7-218">Select a **Metric** or event that you want to track.</span></span>
   4. <span data-ttu-id="601a7-219">Wybierz **warunku**, określ **próg** dla metryki i wybierz **okres** monitorowania ta metryka.</span><span class="sxs-lookup"><span data-stu-id="601a7-219">Select a **Condition**, specify a **Threshold** for the metric, and select the **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="601a7-220">Wybierz, czy do wysyłania wiadomości e-mail dla alertu.</span><span class="sxs-lookup"><span data-stu-id="601a7-220">Select whether to send mail for the alert.</span></span> 
   6. <span data-ttu-id="601a7-221">Określ inne adresy e-mail do wysyłania alertu.</span><span class="sxs-lookup"><span data-stu-id="601a7-221">Specify any other email addresses for sending the alert.</span></span> 
   <span data-ttu-id="601a7-222">Można również określić adres URL elementu webhook gdzie chcesz wysyłać alert.</span><span class="sxs-lookup"><span data-stu-id="601a7-222">You can also specify a webhook URL where you want to send the alert.</span></span>

   <span data-ttu-id="601a7-223">Na przykład ta reguła wysyła alert, gdy jest pięć lub więcej uruchamia się niepowodzeniem w ciągu godziny:</span><span class="sxs-lookup"><span data-stu-id="601a7-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Utwórz metryki regułę alertu](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="601a7-225">Aby uruchomić aplikację logiki z poziomu alertu, można dołączyć [wyzwalacza żądania](../connectors/connectors-native-reqres.md) w przepływie pracy, który umożliwia wykonywanie zadań takich jak te przykłady:</span><span class="sxs-lookup"><span data-stu-id="601a7-225">To run a logic app from an alert, you can include the [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="601a7-226">POST do Slack</span><span class="sxs-lookup"><span data-stu-id="601a7-226">Post to Slack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="601a7-227">Wyślij tekstu</span><span class="sxs-lookup"><span data-stu-id="601a7-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="601a7-228">Dodaj komunikat do kolejki</span><span class="sxs-lookup"><span data-stu-id="601a7-228">Add a message to a queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="601a7-229">Ustawienia zdarzeń diagnostyki Azure i szczegóły</span><span class="sxs-lookup"><span data-stu-id="601a7-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="601a7-230">Każde zdarzenie diagnostyczne zawiera szczegółowe informacje o aplikacji logiki oraz czy zdarzenie, na przykład stan i godzina rozpoczęcia, godziny zakończenia, itp.</span><span class="sxs-lookup"><span data-stu-id="601a7-230">Each diagnostic event has details about your logic app and that event, for example, the status, start time, end time, and so on.</span></span> <span data-ttu-id="601a7-231">Aby programowo skonfigurować monitorowanie i śledzenie i rejestrowanie, jednostki organizacyjnej można użyć tych informacji z [interfejsu API REST dla usługi Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) i [interfejsu API REST Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="601a7-231">To programmatically set up monitoring, tracking, and logging, ou can use these details with the [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and the [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="601a7-232">Na przykład `ActionCompleted` zdarzenie ma `clientTrackingId` i `trackedProperties` właściwości, które służą do monitorowania i śledzenia:</span><span class="sxs-lookup"><span data-stu-id="601a7-232">For example, the `ActionCompleted` event has the `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* <span data-ttu-id="601a7-233">`clientTrackingId`: Jeśli nie zostanie podana Azure automatycznie generuje ten identyfikator i są powiązane zdarzenia na uruchamianie aplikacji logiki, w tym wszystkie zagnieżdżone przepływy pracy wywoływanych z aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="601a7-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from the logic app.</span></span> <span data-ttu-id="601a7-234">Można ręcznie określić ten identyfikator z wyzwalaczy przekazując `x-ms-client-tracking-id` nagłówek o niestandardowych wartość identyfikator w żądaniu wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="601a7-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in the trigger request.</span></span> <span data-ttu-id="601a7-235">Można użyć wyzwalacza żądania, wyzwalacz protokołu HTTP lub wyzwalacza elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="601a7-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="601a7-236">`trackedProperties`: Aby śledzić wejściowych i wyjściowych danych diagnostycznych, można dodać właściwości śledzonych do akcji w definicji JSON aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="601a7-236">`trackedProperties`: To track inputs or outputs in diagnostics data, you can add tracked properties to actions in your logic app's JSON definition.</span></span> <span data-ttu-id="601a7-237">Właściwości śledzonych można śledzić tylko jednej akcji wejściach i wyjściach, ale może użyć `correlation` właściwości zdarzenia do skorelowania w akcji do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="601a7-237">Tracked properties can track only a single action's inputs and outputs, but you can use the `correlation` properties of events to correlate across actions in a run.</span></span>

  <span data-ttu-id="601a7-238">Aby śledzić co najmniej jednej właściwości, należy dodać `trackedProperties` sekcji i właściwości, aby definicji działania.</span><span class="sxs-lookup"><span data-stu-id="601a7-238">To track one or more properties, add the `trackedProperties` section and the properties you want to the action definition.</span></span> <span data-ttu-id="601a7-239">Na przykład załóżmy, że chcesz śledzić dane, takie jak "Identyfikator zamówienia" w obrębie telemetrii:</span><span class="sxs-lookup"><span data-stu-id="601a7-239">For example, suppose you want to track data like an "order ID" in your telemetry:</span></span>

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="601a7-240">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="601a7-240">Next steps</span></span>

* [<span data-ttu-id="601a7-241">Tworzenie szablonów dla wdrożenia aplikacji logiki i zarządzania zleceniami</span><span class="sxs-lookup"><span data-stu-id="601a7-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="601a7-242">Scenariusze B2B z pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="601a7-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="601a7-243">Monitorowanie komunikatów B2B</span><span class="sxs-lookup"><span data-stu-id="601a7-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)