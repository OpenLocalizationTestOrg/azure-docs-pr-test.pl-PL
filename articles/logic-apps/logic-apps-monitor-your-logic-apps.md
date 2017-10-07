---
title: "Stan aaaCheck Konfigurowanie rejestrowania i uzyskiwanie alertów - Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="d30d9-103">Monitorowanie stanu, konfigurowanie rejestrowania diagnostyki i Włącz alerty dla usługi Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="d30d9-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="d30d9-104">Po [tworzenie i uruchamianie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md), można sprawdzić historię uruchomień, Historia wyzwalacza, stanu i wydajności.</span><span class="sxs-lookup"><span data-stu-id="d30d9-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="d30d9-105">Monitorowanie zdarzeń w czasie rzeczywistym i debugowanie bardziej rozbudowane, skonfiguruj [rejestrowania diagnostyki](#azure-diagnostics) aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="d30d9-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="d30d9-106">W ten sposób można [Znajdowanie i wyświetlać zdarzenia](#find-events), takie jak zdarzenia wyzwalacza, uruchom zdarzeń i zdarzenia akcji.</span><span class="sxs-lookup"><span data-stu-id="d30d9-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="d30d9-107">Możesz także użyć tej funkcji [danych diagnostycznych z innymi usługami](#extend-diagnostic-data), takie jak usługi Azure Storage i Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d30d9-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="d30d9-108">Konfigurowanie tooget powiadomienia o awarii lub innych możliwych problemów [alerty](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="d30d9-108">tooget notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="d30d9-109">Na przykład można utworzyć alertu wykrywa "więcej niż pięć uruchamia się niepowodzeniem w ciągu godziny."</span><span class="sxs-lookup"><span data-stu-id="d30d9-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="d30d9-110">Można również skonfigurować monitorowanie, śledzenie i rejestrowanie programowo przy użyciu [ustawienia zdarzeń diagnostyki Azure i właściwości](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="d30d9-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="d30d9-111">Uruchamia widok i historii wyzwalacza dla aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="d30d9-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="d30d9-112">toofind aplikację logiki w hello [portalu Azure](https://portal.azure.com)na temat hello Azure menu głównego, wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-112">toofind your logic app in hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **More services**.</span></span> <span data-ttu-id="d30d9-113">Pole wyszukiwania Witaj, "aplikacje logiki" Znajdź i wybierz polecenie **Logic apps**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-113">In hello search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Znajdź aplikację logiki](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="d30d9-115">Hello portalu Azure zawiera wszystkie aplikacje logiki hello, które są skojarzone z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d30d9-115">hello Azure portal shows all hello logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="d30d9-116">Wybierz aplikację logiki, a następnie wybierz **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="d30d9-117">Hello portalu Azure zawiera historię uruchomień hello i historii wyzwalacza dla aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="d30d9-117">hello Azure portal shows hello runs history and trigger history for your logic app.</span></span> <span data-ttu-id="d30d9-118">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d30d9-118">For example:</span></span>

   ![Historia i wyzwalacza historii uruchomieniu aplikacji logiki](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="d30d9-120">**Uruchamia historii** zawiera wszystkie elementy hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="d30d9-120">**Runs history** shows all hello runs for your logic app.</span></span> 
   * <span data-ttu-id="d30d9-121">**Wyzwalanie historii** pokazuje wszystkie działania wyzwalacza hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="d30d9-121">**Trigger History** shows all hello trigger activity for your logic app.</span></span>

   <span data-ttu-id="d30d9-122">Opis stanu, zobacz [rozwiązywania problemów z aplikacją logiki](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="d30d9-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="d30d9-123">Jeśli nie możesz znaleźć hello dane, które należy oczekiwać na powitania narzędzi wybierz **Odśwież**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-123">If you don't find hello data that you expect, on hello toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="d30d9-124">Witaj tooview kroków z określonego działania, w obszarze **uruchamia historii**, wybierz opcję uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="d30d9-124">tooview hello steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="d30d9-125">Widok monitora Hello zawiera każdego kroku w uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="d30d9-125">hello monitor view shows each step in that run.</span></span> <span data-ttu-id="d30d9-126">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d30d9-126">For example:</span></span>

   ![Akcje dla określonego przebiegu](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="d30d9-128">tooget więcej szczegółów na temat hello uruchomić, wybierz **Uruchom szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-128">tooget more details about hello run, choose **Run Details**.</span></span> <span data-ttu-id="d30d9-129">Te informacje zawiera podsumowanie kroków hello, stan, dane wejściowe, a dane wyjściowe dla hello Uruchom.</span><span class="sxs-lookup"><span data-stu-id="d30d9-129">This information summarizes hello steps, status, inputs, and outputs for hello run.</span></span> 

   ![Wybierz polecenie "Uruchom szczegóły"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="d30d9-131">Na przykład można uzyskać hello na uruchamianie **identyfikator korelacji**, który może być konieczne użycie hello [interfejsu API REST dla usługi Logic Apps](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="d30d9-131">For example, you can get hello run's **Correlation ID**, which you might need when you use hello [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="d30d9-132">tooget szczegółowe informacje o określonym kroku, można wybrać tego kroku.</span><span class="sxs-lookup"><span data-stu-id="d30d9-132">tooget details about a specific step, choose that step.</span></span> <span data-ttu-id="d30d9-133">Teraz możesz przejrzeć szczegóły, takie jak wejść, wyjść i wszelkie błędy, które wystąpiły w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="d30d9-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="d30d9-134">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d30d9-134">For example:</span></span>

   ![Szczegółowe informacje krok](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="d30d9-136">Wszystkie szczegóły środowiska uruchomieniowego i zdarzenia są szyfrowane w hello usługi Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="d30d9-136">All runtime details and events are encrypted within hello Logic Apps service.</span></span> <span data-ttu-id="d30d9-137">Są one odszyfrowane tylko wtedy, gdy użytkownik zażąda tooview tych danych.</span><span class="sxs-lookup"><span data-stu-id="d30d9-137">They are decrypted only when a user requests tooview that data.</span></span> <span data-ttu-id="d30d9-138">Można też kontrolować dostęp toothese zdarzeń o [based kontroli dostępu (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="d30d9-138">You can also control access toothese events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="d30d9-139">tooget szczegóły dotyczące zdarzenia określonego wyzwalacza, przejdź wstecz toohello **omówienie** okienka.</span><span class="sxs-lookup"><span data-stu-id="d30d9-139">tooget details about a specific trigger event, go back toohello **Overview** pane.</span></span> <span data-ttu-id="d30d9-140">W obszarze **wyzwolenia historii**, wybierz pozycję hello wyzwalacz zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d30d9-140">Under **Trigger history**, select hello trigger event.</span></span> <span data-ttu-id="d30d9-141">Teraz można przejrzeć szczegóły, takie jak wejściach i wyjściach, na przykład:</span><span class="sxs-lookup"><span data-stu-id="d30d9-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Szczegóły danych wyjściowych zdarzenia wyzwalacza](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="d30d9-143">Włącz diagnostykę, rejestrowanie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="d30d9-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="d30d9-144">Bardziej rozbudowane debugowanie z szczegóły środowiska uruchomieniowego i zdarzenia, można skonfigurować z funkcji rejestrowania diagnostyki [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d30d9-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="d30d9-145">Analiza dzienników jest usługą [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) który monitoruje chmurze i lokalnych środowiskach toohelp Obsługa ich dostępności i wydajności.</span><span class="sxs-lookup"><span data-stu-id="d30d9-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments toohelp you maintain their availability and performance.</span></span> 

<span data-ttu-id="d30d9-146">Przed rozpoczęciem należy toohave obszarem roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="d30d9-146">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="d30d9-147">Dowiedz się [jak toocreate obszarem roboczym pakietu OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d30d9-147">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="d30d9-148">W hello [portalu Azure](https://portal.azure.com), Znajdź i wybierz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="d30d9-148">In hello [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="d30d9-149">Menu hello logiki aplikacji bloku w obszarze **monitorowanie**, wybierz **diagnostyki** > **ustawień diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-149">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Przejdź do ustawień diagnostycznych tooMonitoring, diagnostyki](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="d30d9-151">W obszarze **ustawień diagnostycznych**, wybierz **na**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Włączanie dzienników diagnostycznych](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="d30d9-153">Teraz wybierz hello OMS obszaru roboczego i zdarzeń kategorii w celu rejestrowania, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="d30d9-153">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="d30d9-154">Wybierz **wysyłania tooLog Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-154">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="d30d9-155">W obszarze **analizy dzienników**, wybierz **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="d30d9-156">W obszarze **obszarów roboczych OMS**, wybierz toouse obszar roboczy OMS hello logowania.</span><span class="sxs-lookup"><span data-stu-id="d30d9-156">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="d30d9-157">W obszarze **dziennika**, wybierz pozycję hello **WorkflowRuntime** kategorii.</span><span class="sxs-lookup"><span data-stu-id="d30d9-157">Under **Log**, select hello **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="d30d9-158">Interwał hello metryki.</span><span class="sxs-lookup"><span data-stu-id="d30d9-158">Choose hello metric interval.</span></span>
   6. <span data-ttu-id="d30d9-159">Gdy wszystko będzie gotowe, wybierz pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-159">When you're done, choose **Save**.</span></span>

   ![Wybierz obszar roboczy OMS i dane dotyczące rejestrowania](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="d30d9-161">Teraz można znaleźć zdarzeń i inne dane dla zdarzenia wyzwalacza, uruchom zdarzenia i akcji.</span><span class="sxs-lookup"><span data-stu-id="d30d9-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="d30d9-162">Znajdź zdarzenia i dane aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="d30d9-162">Find events and data for your logic app</span></span>

<span data-ttu-id="d30d9-163">zdarzenia toofind i widok w aplikację logiki, takich jak zdarzenia wyzwalacza, uruchom zdarzenia i akcji, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="d30d9-163">toofind and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="d30d9-164">W hello [portalu Azure](https://portal.azure.com), wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-164">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="d30d9-165">Wyszukaj "analizy dzienników", a następnie wybierz **analizy dzienników** w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="d30d9-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Wybierz pozycję "Analizy dzienników"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="d30d9-167">W obszarze **analizy dzienników**, Znajdź i wybierz obszar roboczy OMS.</span><span class="sxs-lookup"><span data-stu-id="d30d9-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Wybierz obszar roboczy OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="d30d9-169">W obszarze **zarządzania**, wybierz **portalu OMS**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![Wybierz pozycję "Portalu OMS"](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="d30d9-171">Na stronie głównej OMS wybierz **wyszukiwania dziennika**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-171">On your OMS home page, choose **Log Search**.</span></span>

   ![Na stronie głównej OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="d30d9-173">— lub —</span><span class="sxs-lookup"><span data-stu-id="d30d9-173">-or-</span></span>

   ![W menu OMS hello wybierz "Dziennik wyszukiwania"](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="d30d9-175">W polu wyszukiwania hello, określ pola, które mają toofind i naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-175">In hello search box, specify a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="d30d9-176">Po rozpoczęciu wprowadzania, OMS pokazuje, pasujących i operacje, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="d30d9-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="d30d9-177">Na przykład toofind hello 10 pierwszych zdarzenia, które wystąpiły, wprowadź i wybierz tego zapytania wyszukiwania: **kategorii = WorkflowRuntime | 10 pierwszych**</span><span class="sxs-lookup"><span data-stu-id="d30d9-177">For example, toofind hello top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Wprowadź ciąg wyszukiwania](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="d30d9-179">Dowiedz się więcej o [jak toofind danych analizy dzienników](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="d30d9-179">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="d30d9-180">Na stronie wyników hello hello pasku po lewej stronie, wybierz przedział czasu hello, które mają tooview.</span><span class="sxs-lookup"><span data-stu-id="d30d9-180">On hello results page, in hello left bar, choose hello timeframe that you want tooview.</span></span>
<span data-ttu-id="d30d9-181">Wybierz zapytanie, dodając filtr, toorefine **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-181">toorefine your query by adding a filter, choose **+Add**.</span></span>

   ![Wybierz przedział czasu dla wyników zapytania](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="d30d9-183">W obszarze **Dodaj filtry**, wprowadź nazwę filtru hello, aby umożliwić znalezienie hello filtr ma.</span><span class="sxs-lookup"><span data-stu-id="d30d9-183">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="d30d9-184">Wybierz filtr hello, a następnie wybierz pozycję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-184">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="d30d9-185">W tym przykładzie używa hello word toofind "status" nie powiodło się zdarzenia w obszarze **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-185">This example uses hello word "status" toofind failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="d30d9-186">W tym miejscu hello filtr dla **status_s** jest już wybrana.</span><span class="sxs-lookup"><span data-stu-id="d30d9-186">Here hello filter for **status_s** is already selected.</span></span>

   ![Wybierz filtr](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="d30d9-188">Na pasku po lewej stronie powitania, wybierz wartość filtru hello mają toouse i wybierz polecenie **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-188">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   ![Wybierz wartości filtru, wybierz polecenie "Zastosuj"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="d30d9-190">Teraz wróć toohello zapytania, które tworzysz.</span><span class="sxs-lookup"><span data-stu-id="d30d9-190">Now return toohello query that you're building.</span></span> <span data-ttu-id="d30d9-191">Zapytanie jest aktualizowana z wybranego filtru i wartość.</span><span class="sxs-lookup"><span data-stu-id="d30d9-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="d30d9-192">Poprzednie wyniki teraz są zbyt filtrowane.</span><span class="sxs-lookup"><span data-stu-id="d30d9-192">Your previous results are now filtered too.</span></span>

   ![Zwraca tooyour filtrowane wyniki zapytania](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="d30d9-194">Wybierz zapytanie do użytku w przyszłości, toosave **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="d30d9-194">toosave your query for future use, choose **Save**.</span></span> <span data-ttu-id="d30d9-195">Dowiedz się [jak toosave kwerendy](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="d30d9-195">Learn [how toosave your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="d30d9-196">Rozszerzanie, jak i gdzie używać danych diagnostycznych z innymi usługami</span><span class="sxs-lookup"><span data-stu-id="d30d9-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="d30d9-197">Wraz z Azure Log Analytics można rozszerzyć, jak używasz aplikacji logiki danych diagnostycznych z innymi usługami Azure, na przykład:</span><span class="sxs-lookup"><span data-stu-id="d30d9-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="d30d9-198">Archiwum, które dzienniki diagnostyczne platformy Azure w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="d30d9-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="d30d9-199">Strumień tooAzure dzienników diagnostyki Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d30d9-199">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="d30d9-200">Następnie monitorowanie za pomocą telemetrii i analiza z innych usług, takich jak get w czasie rzeczywistym [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) i [usługi Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="d30d9-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="d30d9-201">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d30d9-201">For example:</span></span>

* [<span data-ttu-id="d30d9-202">Strumień danych z usługi Event Hubs tooStream analityka</span><span class="sxs-lookup"><span data-stu-id="d30d9-202">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="d30d9-203">Analizować dane przesyłane strumieniowo z usługi Stream Analytics i utworzyć pulpit nawigacyjny analiz w czasie rzeczywistym w usłudze Power BI</span><span class="sxs-lookup"><span data-stu-id="d30d9-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="d30d9-204">Oparte na powitania opcje, które chcesz skonfigurować, upewnij się, że możesz pierwszy [utworzyć konto magazynu Azure](../storage/common/storage-create-storage-account.md) lub [tworzenia Centrum zdarzeń Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="d30d9-204">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="d30d9-205">Następnie wybierz opcje hello miejscu toosend danych diagnostycznych:</span><span class="sxs-lookup"><span data-stu-id="d30d9-205">Then select hello options for where you want toosend diagnostic data:</span></span>

![Wysyłanie danych tooAzure magazynu konta lub zdarzenia Centrum](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="d30d9-207">Okresy przechowywania mają zastosowanie tylko wtedy, gdy wybierzesz toouse konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d30d9-207">Retention periods apply only when you choose toouse a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="d30d9-208">Ustawianie alertów dla aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="d30d9-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="d30d9-209">Przekroczono próg dla aplikacji logiki, lub określonych metryk toomonitor Konfigurowanie [alertów w usłudze Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="d30d9-209">toomonitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="d30d9-210">Dowiedz się więcej o [metryki na platformie Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d30d9-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="d30d9-211">tooset alerty bez [Azure Log Analytics](../log-analytics/log-analytics-overview.md), wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="d30d9-211">tooset up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="d30d9-212">Bardziej zaawansowane kryteria alertów i akcji [Konfigurowanie analizy dzienników](#azure-diagnostics) zbyt.</span><span class="sxs-lookup"><span data-stu-id="d30d9-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="d30d9-213">Menu hello logiki aplikacji bloku w obszarze **monitorowanie**, wybierz **diagnostyki** > **reguły alertów** > **Dodaj alert**w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="d30d9-213">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Dodawanie alertu dla aplikacji logiki](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="d30d9-215">Na powitania **dodać regułę alertu** bloku tworzenia alertu, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="d30d9-215">On hello **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="d30d9-216">W obszarze **zasobów**, wybierz aplikację logiki, jeśli nie już wybrana.</span><span class="sxs-lookup"><span data-stu-id="d30d9-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="d30d9-217">Nadaj nazwę i opis alertu.</span><span class="sxs-lookup"><span data-stu-id="d30d9-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="d30d9-218">Wybierz **Metryka** lub zdarzenie, które mają tootrack.</span><span class="sxs-lookup"><span data-stu-id="d30d9-218">Select a **Metric** or event that you want tootrack.</span></span>
   4. <span data-ttu-id="d30d9-219">Wybierz **warunku**, określ **próg** hello metryki i wybierz hello **okres** monitorowania ta metryka.</span><span class="sxs-lookup"><span data-stu-id="d30d9-219">Select a **Condition**, specify a **Threshold** for hello metric, and select hello **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="d30d9-220">Wybierz, czy toosend poczty hello alertu.</span><span class="sxs-lookup"><span data-stu-id="d30d9-220">Select whether toosend mail for hello alert.</span></span> 
   6. <span data-ttu-id="d30d9-221">Określ inne adresy e-mail do wysyłania alertu hello.</span><span class="sxs-lookup"><span data-stu-id="d30d9-221">Specify any other email addresses for sending hello alert.</span></span> 
   <span data-ttu-id="d30d9-222">Można również określić adres URL elementu webhook miejscu toosend hello alertu.</span><span class="sxs-lookup"><span data-stu-id="d30d9-222">You can also specify a webhook URL where you want toosend hello alert.</span></span>

   <span data-ttu-id="d30d9-223">Na przykład ta reguła wysyła alert, gdy jest pięć lub więcej uruchamia się niepowodzeniem w ciągu godziny:</span><span class="sxs-lookup"><span data-stu-id="d30d9-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Utwórz metryki regułę alertu](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="d30d9-225">toorun aplikacji logiki z poziomu alertu można uwzględnić hello [wyzwalacza żądania](../connectors/connectors-native-reqres.md) w przepływie pracy, który umożliwia wykonywanie zadań takich jak te przykłady:</span><span class="sxs-lookup"><span data-stu-id="d30d9-225">toorun a logic app from an alert, you can include hello [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="d30d9-226">Post tooSlack</span><span class="sxs-lookup"><span data-stu-id="d30d9-226">Post tooSlack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="d30d9-227">Wyślij tekstu</span><span class="sxs-lookup"><span data-stu-id="d30d9-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="d30d9-228">Dodaj tooa kolejki komunikatów</span><span class="sxs-lookup"><span data-stu-id="d30d9-228">Add a message tooa queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="d30d9-229">Ustawienia zdarzeń diagnostyki Azure i szczegóły</span><span class="sxs-lookup"><span data-stu-id="d30d9-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="d30d9-230">Każde zdarzenie diagnostyczne ma szczegółowe informacje o aplikacji logiki oraz czy zdarzenie, na przykład hello stan i godzina rozpoczęcia, godziny zakończenia, itp.</span><span class="sxs-lookup"><span data-stu-id="d30d9-230">Each diagnostic event has details about your logic app and that event, for example, hello status, start time, end time, and so on.</span></span> <span data-ttu-id="d30d9-231">Konfigurowanie monitorowania, śledzenie i rejestrowanie tooprogrammatically, jednostki organizacyjnej za pomocą te szczegóły hello [interfejsu API REST dla usługi Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) i hello [interfejsu API REST Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="d30d9-231">tooprogrammatically set up monitoring, tracking, and logging, ou can use these details with hello [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and hello [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="d30d9-232">Na przykład Witaj `ActionCompleted` zdarzenie ma hello `clientTrackingId` i `trackedProperties` właściwości, które służą do monitorowania i śledzenia:</span><span class="sxs-lookup"><span data-stu-id="d30d9-232">For example, hello `ActionCompleted` event has hello `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

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

* <span data-ttu-id="d30d9-233">`clientTrackingId`: Jeśli nie pod warunkiem Azure automatycznie generuje ten identyfikator i są powiązane zdarzenia na uruchamianie aplikacji logiki, w tym wszystkie zagnieżdżone przepływy pracy wywoływanych z hello logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d30d9-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from hello logic app.</span></span> <span data-ttu-id="d30d9-234">Można ręcznie określić ten identyfikator z wyzwalaczy przekazując `x-ms-client-tracking-id` nagłówek o niestandardowych wartość identyfikator w żądaniu wyzwalacza hello.</span><span class="sxs-lookup"><span data-stu-id="d30d9-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in hello trigger request.</span></span> <span data-ttu-id="d30d9-235">Można użyć wyzwalacza żądania, wyzwalacz protokołu HTTP lub wyzwalacza elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="d30d9-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="d30d9-236">`trackedProperties`: tootrack wejściowych i wyjściowych danych diagnostycznych, możesz dodać tooactions śledzonych właściwości w definicji JSON aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="d30d9-236">`trackedProperties`: tootrack inputs or outputs in diagnostics data, you can add tracked properties tooactions in your logic app's JSON definition.</span></span> <span data-ttu-id="d30d9-237">Właściwości śledzonych można śledzić tylko jednej akcji wejściach i wyjściach, ale może użyć hello `correlation` właściwości zdarzenia toocorrelate przez akcje do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="d30d9-237">Tracked properties can track only a single action's inputs and outputs, but you can use hello `correlation` properties of events toocorrelate across actions in a run.</span></span>

  <span data-ttu-id="d30d9-238">tootrack hello Dodaj co najmniej jednej właściwości `trackedProperties` sekcji i hello właściwości, które toohello definicji działania.</span><span class="sxs-lookup"><span data-stu-id="d30d9-238">tootrack one or more properties, add hello `trackedProperties` section and hello properties you want toohello action definition.</span></span> <span data-ttu-id="d30d9-239">Na przykład załóżmy, że chcesz tootrack dane, takie jak "Identyfikator zamówienia" w obrębie telemetrii:</span><span class="sxs-lookup"><span data-stu-id="d30d9-239">For example, suppose you want tootrack data like an "order ID" in your telemetry:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d30d9-240">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d30d9-240">Next steps</span></span>

* [<span data-ttu-id="d30d9-241">Tworzenie szablonów dla wdrożenia aplikacji logiki i zarządzania zleceniami</span><span class="sxs-lookup"><span data-stu-id="d30d9-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="d30d9-242">Scenariusze B2B z pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="d30d9-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="d30d9-243">Monitorowanie komunikatów B2B</span><span class="sxs-lookup"><span data-stu-id="d30d9-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)