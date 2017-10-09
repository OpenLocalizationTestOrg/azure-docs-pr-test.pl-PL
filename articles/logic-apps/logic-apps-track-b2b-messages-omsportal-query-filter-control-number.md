---
title: "aaaQuery wiadomości B2B w Operations Management Suite — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie zapytań tootrack AS2, X 12 i EDIFACT wiadomości w hello Operations Management Suite"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a><span data-ttu-id="17aab-103">Zapytanie o AS2, X 12 i EDIFACT wiadomości powitania programu Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="17aab-103">Query for AS2, X12, and EDIFACT messages in hello Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="17aab-104">toofind hello AS2, X 12 i EDIFACT komunikaty śledzenia z [Azure Log Analytics](../log-analytics/log-analytics-overview.md) w hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), można utworzyć kwerendy, które są oparte na określonych akcji filtrowania kryteria.</span><span class="sxs-lookup"><span data-stu-id="17aab-104">toofind hello AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="17aab-105">Na przykład można znaleźć na podstawie różnych kontroli określonych wymiany wiadomości.</span><span class="sxs-lookup"><span data-stu-id="17aab-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="17aab-106">Wymagania</span><span class="sxs-lookup"><span data-stu-id="17aab-106">Requirements</span></span>

* <span data-ttu-id="17aab-107">Aplikację logiki, który został skonfigurowany z rejestrowania diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="17aab-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="17aab-108">Dowiedz się [jak toocreate aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) i [jak tooset rejestrowanie dla danej aplikacji logiki danych](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="17aab-108">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="17aab-109">Konta integracji, które skonfigurowano przy użyciu rejestrowania i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="17aab-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="17aab-110">Dowiedz się [jak toocreate konta integracji](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) i [jak tooset monitorowania i rejestrowania dla tego konta](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="17aab-110">Learn [how toocreate an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how tooset up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="17aab-111">Jeśli nie jest jeszcze, [publikowania danych diagnostycznych tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) i [Konfigurowanie śledzenia w OMS wiadomości](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="17aab-111">If you haven't already, [publish diagnostic data tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="17aab-112">Po zostały spełnione wymagania poprzedniej hello, powinien mieć obszar roboczy w hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="17aab-112">After you've met hello previous requirements, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="17aab-113">Należy używać tego samego pakietu OMS obszaru roboczego do śledzenia komunikacji B2B w OMS hello.</span><span class="sxs-lookup"><span data-stu-id="17aab-113">You should use hello same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="17aab-114">Dowiedz się, jeśli nie masz obszar roboczy OMS [jak toocreate obszarem roboczym pakietu OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="17aab-114">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a><span data-ttu-id="17aab-115">Tworzenie kwerend komunikatów z filtrami w portalu usługi Operations Management Suite hello</span><span class="sxs-lookup"><span data-stu-id="17aab-115">Create message queries with filters in hello Operations Management Suite portal</span></span>

<span data-ttu-id="17aab-116">Ten przykład przedstawia, jak można znaleźć na podstawie ich liczby kontroli wymiany wiadomości.</span><span class="sxs-lookup"><span data-stu-id="17aab-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="17aab-117">Jeśli znasz nazwę obszar roboczy OMS Przejdź strona główna obszaru roboczego tooyour (`https://{your-workspace-name}.portal.mms.microsoft.com`) i uruchomić w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="17aab-117">If you know your OMS workspace name, go tooyour workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="17aab-118">W przeciwnym razie Rozpocznij w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="17aab-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="17aab-119">W hello [portalu Azure](https://portal.azure.com), wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="17aab-119">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="17aab-120">Wyszukaj "analizy dzienników", a następnie wybierz pozycję **analizy dzienników** w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="17aab-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Znajdź analizy dzienników](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="17aab-122">W obszarze **analizy dzienników**, Znajdź i wybierz obszar roboczy OMS.</span><span class="sxs-lookup"><span data-stu-id="17aab-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Wybierz obszar roboczy OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="17aab-124">W obszarze **zarządzania**, wybierz **portalu OMS**.</span><span class="sxs-lookup"><span data-stu-id="17aab-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Wybierz portalu OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="17aab-126">Na stronie głównej OMS wybierz **wyszukiwania dziennika**.</span><span class="sxs-lookup"><span data-stu-id="17aab-126">On your OMS home page, choose **Log Search**.</span></span>

   ![Na stronie głównej OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="17aab-128">— lub —</span><span class="sxs-lookup"><span data-stu-id="17aab-128">-or-</span></span>

   ![W menu OMS hello wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="17aab-130">W polu wyszukiwania hello, wprowadź pola, które mają toofind i naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="17aab-130">In hello search box, enter a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="17aab-131">Po rozpoczęciu wprowadzania, OMS pokazuje, pasujących i operacje, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="17aab-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="17aab-132">Dowiedz się więcej o [jak toofind danych analizy dzienników](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="17aab-132">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="17aab-133">W tym przykładzie wyszukuje zdarzeń o **typu = AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="17aab-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Wpisz ciąg zapytania](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="17aab-135">Na pasku po lewej stronie powitania, wybierz przedział czasu hello, które mają tooview.</span><span class="sxs-lookup"><span data-stu-id="17aab-135">In hello left bar, choose hello timeframe that you want tooview.</span></span> <span data-ttu-id="17aab-136">tooadd kwerendy tooyour filtru, wybierz **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="17aab-136">tooadd a filter tooyour query, choose **+Add**.</span></span>

   ![Dodaj filtr tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="17aab-138">W obszarze **Dodaj filtry**, wprowadź nazwę filtru hello, aby umożliwić znalezienie hello filtr ma.</span><span class="sxs-lookup"><span data-stu-id="17aab-138">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="17aab-139">Wybierz filtr hello, a następnie wybierz pozycję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="17aab-139">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="17aab-140">toofind numer formantu wymiany hello, w tym przykładzie wyszukuje hello word "wymiany" i wybiera **event_record_messageProperties_interchangeControlNumber_s** jako hello filtru.</span><span class="sxs-lookup"><span data-stu-id="17aab-140">toofind hello interchange control number, this example searches for hello word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as hello filter.</span></span>

   ![Wybierz filtr](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="17aab-142">Na pasku po lewej stronie powitania, wybierz wartość filtru hello mają toouse i wybierz polecenie **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="17aab-142">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   <span data-ttu-id="17aab-143">W tym przykładzie wybiera numer kontroli hello wymiany wiadomości powitania, którą chcemy udostępnić.</span><span class="sxs-lookup"><span data-stu-id="17aab-143">This example selects hello interchange control number for hello messages we want.</span></span>

   ![Wybierz wartości filtru](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="17aab-145">Teraz wróć toohello zapytania, które tworzysz.</span><span class="sxs-lookup"><span data-stu-id="17aab-145">Now return toohello query that you're building.</span></span> <span data-ttu-id="17aab-146">Kwerenda została zaktualizowana wybrany filtr zdarzeń i wartość.</span><span class="sxs-lookup"><span data-stu-id="17aab-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="17aab-147">Poprzednie wyniki teraz są zbyt filtrowane.</span><span class="sxs-lookup"><span data-stu-id="17aab-147">Your previous results are now filtered too.</span></span>

    ![Zwraca tooyour filtrowane wyniki zapytania](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="17aab-149">Zapisz zapytanie do użytku w przyszłości</span><span class="sxs-lookup"><span data-stu-id="17aab-149">Save your query for future use</span></span>

1. <span data-ttu-id="17aab-150">Z kwerendy na powitania **wyszukiwania dziennika** wybierz pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="17aab-150">From your query on hello **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="17aab-151">Nadaj nazwę kwerendy, wybierz kategorię i wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="17aab-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Nadaj zapytania, nazwę i kategorii](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="17aab-153">tooview kwerendy, wybierz **ulubione**.</span><span class="sxs-lookup"><span data-stu-id="17aab-153">tooview your query, choose **Favorites**.</span></span>

   ![Wybierz pozycję "Ulubione"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="17aab-155">W obszarze **zapisane wyszukiwania**, wybierz zapytanie, dzięki czemu można wyświetlić wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="17aab-155">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="17aab-156">tooupdate hello zapytania, aby umożliwić znalezienie różne wyniki, Edytuj hello zapytanie.</span><span class="sxs-lookup"><span data-stu-id="17aab-156">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Wybierz zapytanie](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a><span data-ttu-id="17aab-158">Znajdź i uruchom zapisane kwerendy w portalu usługi Operations Management Suite hello</span><span class="sxs-lookup"><span data-stu-id="17aab-158">Find and run saved queries in hello Operations Management Suite portal</span></span>

1. <span data-ttu-id="17aab-159">Otwórz stronę główną obszar roboczy OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) i wybierz polecenie **wyszukiwania dziennika**.</span><span class="sxs-lookup"><span data-stu-id="17aab-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![Na stronie głównej OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="17aab-161">— lub —</span><span class="sxs-lookup"><span data-stu-id="17aab-161">-or-</span></span>

   ![W menu OMS hello wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="17aab-163">Na powitania **wyszukiwania dziennika** strony głównej, wybierz **ulubione**.</span><span class="sxs-lookup"><span data-stu-id="17aab-163">On hello **Log Search** home page, choose **Favorites**.</span></span>

   ![Wybierz pozycję "Ulubione"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="17aab-165">W obszarze **zapisane wyszukiwania**, wybierz zapytanie, dzięki czemu można wyświetlić wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="17aab-165">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="17aab-166">tooupdate hello zapytania, aby umożliwić znalezienie różne wyniki, Edytuj hello zapytanie.</span><span class="sxs-lookup"><span data-stu-id="17aab-166">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Wybierz zapytanie](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="17aab-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="17aab-168">Next steps</span></span>

* [<span data-ttu-id="17aab-169">Schematy śledzenia AS2</span><span class="sxs-lookup"><span data-stu-id="17aab-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="17aab-170">Schematy śledzenia X12</span><span class="sxs-lookup"><span data-stu-id="17aab-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="17aab-171">Śledzenie niestandardowych schematów</span><span class="sxs-lookup"><span data-stu-id="17aab-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)