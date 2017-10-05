---
title: "Kwerenda dotycząca wiadomości B2B usługi Operations Management Suite — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie zapytań do śledzenia AS2, X 12 i EDIFACT wiadomości w Operations Management Suite"
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
ms.openlocfilehash: 2748d3d3daf7c13dca05f663a4a088598e1b3605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-the-microsoft-operations-management-suite-oms"></a><span data-ttu-id="96b49-103">Zapytanie o AS2, X 12 i EDIFACT wiadomości pakiet zarządzania Operations (OMS) firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="96b49-103">Query for AS2, X12, and EDIFACT messages in the Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="96b49-104">Aby znaleźć AS2, X12 lub EDIFACT wiadomości, że podczas śledzenia z [Azure Log Analytics](../log-analytics/log-analytics-overview.md) w [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), można utworzyć kwerendy, które akcje na podstawie określonych kryteriów filtrowania.</span><span class="sxs-lookup"><span data-stu-id="96b49-104">To find the AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="96b49-105">Na przykład można znaleźć na podstawie różnych kontroli określonych wymiany wiadomości.</span><span class="sxs-lookup"><span data-stu-id="96b49-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="96b49-106">Wymagania</span><span class="sxs-lookup"><span data-stu-id="96b49-106">Requirements</span></span>

* <span data-ttu-id="96b49-107">Aplikację logiki, który został skonfigurowany z rejestrowania diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="96b49-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="96b49-108">Dowiedz się [sposób tworzenia aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) i [jak skonfigurować rejestrowanie dla danej aplikacji logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="96b49-108">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="96b49-109">Konta integracji, które skonfigurowano przy użyciu rejestrowania i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="96b49-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="96b49-110">Dowiedz się [sposobu tworzenia konta integracji](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) i [jak skonfigurować monitorowanie i rejestrowanie dla tego konta](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="96b49-110">Learn [how to create an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how to set up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="96b49-111">Jeśli nie jest jeszcze, [publikowania danych diagnostycznych do analizy dzienników](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) i [Konfigurowanie śledzenia w OMS wiadomości](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="96b49-111">If you haven't already, [publish diagnostic data to Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="96b49-112">Po zostały spełnione wymagania poprzedniej, powinien mieć obszar roboczy [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="96b49-112">After you've met the previous requirements, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="96b49-113">Należy używać tego samego obszaru roboczego OMS śledzenia komunikacji B2B w OMS.</span><span class="sxs-lookup"><span data-stu-id="96b49-113">You should use the same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="96b49-114">Dowiedz się, jeśli nie masz obszar roboczy OMS [jak Utwórz obszar roboczy OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="96b49-114">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-the-operations-management-suite-portal"></a><span data-ttu-id="96b49-115">Tworzenie kwerend komunikatów z filtrami w portalu usługi Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="96b49-115">Create message queries with filters in the Operations Management Suite portal</span></span>

<span data-ttu-id="96b49-116">Ten przykład przedstawia, jak można znaleźć na podstawie ich liczby kontroli wymiany wiadomości.</span><span class="sxs-lookup"><span data-stu-id="96b49-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="96b49-117">Jeśli znasz nazwę obszar roboczy OMS, przejdź do strony głównej obszaru roboczego (`https://{your-workspace-name}.portal.mms.microsoft.com`) i uruchomić w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="96b49-117">If you know your OMS workspace name, go to your workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="96b49-118">W przeciwnym razie Rozpocznij w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="96b49-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="96b49-119">W [portalu Azure](https://portal.azure.com), wybierz **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="96b49-119">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="96b49-120">Wyszukaj "analizy dzienników", a następnie wybierz pozycję **analizy dzienników** w sposób pokazany poniżej:</span><span class="sxs-lookup"><span data-stu-id="96b49-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Znajdź analizy dzienników](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="96b49-122">W obszarze **analizy dzienników**, Znajdź i wybierz obszar roboczy OMS.</span><span class="sxs-lookup"><span data-stu-id="96b49-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Wybierz obszar roboczy OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="96b49-124">W obszarze **zarządzania**, wybierz **portalu OMS**.</span><span class="sxs-lookup"><span data-stu-id="96b49-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Wybierz portalu OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="96b49-126">Na stronie głównej OMS wybierz **wyszukiwania dziennika**.</span><span class="sxs-lookup"><span data-stu-id="96b49-126">On your OMS home page, choose **Log Search**.</span></span>

   ![Na stronie głównej OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="96b49-128">— lub —</span><span class="sxs-lookup"><span data-stu-id="96b49-128">-or-</span></span>

   ![W menu OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="96b49-130">W polu wyszukiwania wprowadź pola, które chcesz odnaleźć, a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="96b49-130">In the search box, enter a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="96b49-131">Po rozpoczęciu wprowadzania, OMS pokazuje, pasujących i operacje, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="96b49-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="96b49-132">Dowiedz się więcej o [jak wyszukiwania danych analizy dzienników](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="96b49-132">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="96b49-133">W tym przykładzie wyszukuje zdarzeń o **typu = AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="96b49-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Wpisz ciąg zapytania](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="96b49-135">Na pasku po lewej stronie Wybierz przedział czasu, który chcesz wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="96b49-135">In the left bar, choose the timeframe that you want to view.</span></span> <span data-ttu-id="96b49-136">Aby dodać filtr do zapytania, wybierz **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="96b49-136">To add a filter to your query, choose **+Add**.</span></span>

   ![Dodaj filtr do zapytania](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="96b49-138">W obszarze **Dodaj filtry**, wprowadź nazwę filtru, aby umożliwić znalezienie filtr ma.</span><span class="sxs-lookup"><span data-stu-id="96b49-138">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="96b49-139">Wybierz filtr, a następnie wybierz pozycję **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="96b49-139">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="96b49-140">Aby znaleźć numer formantu wymiany, w tym przykładzie wyszukuje dla słowa "wymiany" i wybiera **event_record_messageProperties_interchangeControlNumber_s** jako filtr.</span><span class="sxs-lookup"><span data-stu-id="96b49-140">To find the interchange control number, this example searches for the word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as the filter.</span></span>

   ![Wybierz filtr](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="96b49-142">Na pasku po lewej stronie wybierz wartości filtru, który chcesz użyć, a następnie wybierz pozycję **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="96b49-142">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   <span data-ttu-id="96b49-143">W tym przykładzie wybiera numer kontroli wymiany wiadomości, którą chcemy udostępnić.</span><span class="sxs-lookup"><span data-stu-id="96b49-143">This example selects the interchange control number for the messages we want.</span></span>

   ![Wybierz wartości filtru](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="96b49-145">Teraz wróć do zapytania, które tworzysz.</span><span class="sxs-lookup"><span data-stu-id="96b49-145">Now return to the query that you're building.</span></span> <span data-ttu-id="96b49-146">Kwerenda została zaktualizowana wybrany filtr zdarzeń i wartość.</span><span class="sxs-lookup"><span data-stu-id="96b49-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="96b49-147">Poprzednie wyniki teraz są zbyt filtrowane.</span><span class="sxs-lookup"><span data-stu-id="96b49-147">Your previous results are now filtered too.</span></span>

    ![Wróć do filtrowane wyniki zapytania](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="96b49-149">Zapisz zapytanie do użytku w przyszłości</span><span class="sxs-lookup"><span data-stu-id="96b49-149">Save your query for future use</span></span>

1. <span data-ttu-id="96b49-150">Z kwerendy na **wyszukiwania dziennika** wybierz pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="96b49-150">From your query on the **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="96b49-151">Nadaj nazwę kwerendy, wybierz kategorię i wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="96b49-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Nadaj zapytania, nazwę i kategorii](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="96b49-153">Aby wyświetlić kwerendy, wybierz **ulubione**.</span><span class="sxs-lookup"><span data-stu-id="96b49-153">To view your query, choose **Favorites**.</span></span>

   ![Wybierz pozycję "Ulubione"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="96b49-155">W obszarze **zapisane wyszukiwania**, wybierz zapytanie, dzięki czemu można wyświetlić wyniki.</span><span class="sxs-lookup"><span data-stu-id="96b49-155">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="96b49-156">Aby zaktualizować zapytania, aby umożliwić znalezienie różne wyniki, Edytuj zapytanie.</span><span class="sxs-lookup"><span data-stu-id="96b49-156">To update the query so you can find different results, edit the query.</span></span>

   ![Wybierz zapytanie](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-the-operations-management-suite-portal"></a><span data-ttu-id="96b49-158">Znajdź i uruchom zapisane kwerendy w portalu usługi Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="96b49-158">Find and run saved queries in the Operations Management Suite portal</span></span>

1. <span data-ttu-id="96b49-159">Otwórz stronę główną obszar roboczy OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) i wybierz polecenie **wyszukiwania dziennika**.</span><span class="sxs-lookup"><span data-stu-id="96b49-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![Na stronie głównej OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="96b49-161">— lub —</span><span class="sxs-lookup"><span data-stu-id="96b49-161">-or-</span></span>

   ![W menu OMS wybierz "Dziennik wyszukiwania"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="96b49-163">Na **wyszukiwania dziennika** strony głównej, wybierz **ulubione**.</span><span class="sxs-lookup"><span data-stu-id="96b49-163">On the **Log Search** home page, choose **Favorites**.</span></span>

   ![Wybierz pozycję "Ulubione"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="96b49-165">W obszarze **zapisane wyszukiwania**, wybierz zapytanie, dzięki czemu można wyświetlić wyniki.</span><span class="sxs-lookup"><span data-stu-id="96b49-165">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="96b49-166">Aby zaktualizować zapytania, aby umożliwić znalezienie różne wyniki, Edytuj zapytanie.</span><span class="sxs-lookup"><span data-stu-id="96b49-166">To update the query so you can find different results, edit the query.</span></span>

   ![Wybierz zapytanie](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="96b49-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96b49-168">Next steps</span></span>

* [<span data-ttu-id="96b49-169">Schematy śledzenia AS2</span><span class="sxs-lookup"><span data-stu-id="96b49-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="96b49-170">Schematy śledzenia X12</span><span class="sxs-lookup"><span data-stu-id="96b49-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="96b49-171">Śledzenie niestandardowych schematów</span><span class="sxs-lookup"><span data-stu-id="96b49-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)