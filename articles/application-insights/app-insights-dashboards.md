---
title: "Pulpity nawigacyjne i nawigacja w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Utwórz widoki kwerend i wykresy APM klucza."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9987f04e7e71df5fe10c8bc209a390cb940ec4f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="navigation-and-dashboards-in-the-application-insights-portal"></a><span data-ttu-id="0bd57-103">Nawigacji i pulpitów nawigacyjnych w portalu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="0bd57-103">Navigation and Dashboards in the Application Insights portal</span></span>
<span data-ttu-id="0bd57-104">Po utworzeniu [skonfiguruj usługę Application Insights w projekcie](app-insights-overview.md), dane telemetryczne dotyczące wydajności i użycia aplikacji będą wyświetlane w projektu zasobu usługi Application Insights w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0bd57-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="0bd57-105">Znajdź telemetrii</span><span class="sxs-lookup"><span data-stu-id="0bd57-105">Find your telemetry</span></span>
<span data-ttu-id="0bd57-106">Zaloguj się do [portalu Azure](https://portal.azure.com) i przejdź do zasobu usługi Application Insights, który został utworzony dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0bd57-106">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the Application Insights resource that you created for your app.</span></span>

![Kliknij przycisk Przeglądaj, wybierz usługę Application Insights, a następnie aplikacji.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="0bd57-108">Omówienie bloku (strona) aplikacji przedstawiono podsumowanie kluczowych metryk diagnostyki aplikacji i jest bramy do innych funkcji w portalu.</span><span class="sxs-lookup"><span data-stu-id="0bd57-108">The overview blade (page) for your app shows a summary of the key diagnostic metrics of your app, and is a gateway to the other features of the portal.</span></span>

![Głównych tras, aby wyświetlić telemetrii](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="0bd57-110">Można dostosować żadnego z wykresami i siatki i przypiąć je na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="0bd57-110">You can customize any of the charts and grids and pin them to a dashboard.</span></span> <span data-ttu-id="0bd57-111">W ten sposób można zebrać razem klucza dane telemetryczne z różnych aplikacji na pulpicie nawigacyjnym centralnej.</span><span class="sxs-lookup"><span data-stu-id="0bd57-111">That way, you can bring together the key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="0bd57-112">Pulpity nawigacyjne</span><span class="sxs-lookup"><span data-stu-id="0bd57-112">Dashboards</span></span>
<span data-ttu-id="0bd57-113">Najpierw Zobacz po zalogowaniu się do [portalu Microsoft Azure](https://portal.azure.com) jest pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="0bd57-113">The first thing you see after you sign in to the [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="0bd57-114">W tym miejscu można zebrać razem wykresy, które są najważniejsze dla Ciebie we wszystkich zasobów platformy Azure, w tym dane telemetryczne z [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0bd57-114">Here you can bring together the charts that are most important to you across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Dostosowany pulpit nawigacyjny.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="0bd57-116">**Przejdź do określonych zasobów** takich jak aplikacji w usłudze Application Insights: Użyj pasku po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="0bd57-116">**Navigate to specific resources** such as your app in Application Insights: Use the left bar.</span></span>
2. <span data-ttu-id="0bd57-117">**Wróć do bieżącego pulpitu nawigacyjnego**, lub przełącz się do innych widoków ostatnie: Użyj menu rozwijane u góry po lewej.</span><span class="sxs-lookup"><span data-stu-id="0bd57-117">**Return to the current dashboard**, or switch to other recent views: Use the drop-down menu at top left.</span></span>
3. <span data-ttu-id="0bd57-118">**Przełącz pulpity nawigacyjne**: Użyj menu rozwijanego tytuł pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="0bd57-118">**Switch dashboards**: Use the drop-down menu on the dashboard title</span></span>
4. <span data-ttu-id="0bd57-119">**Tworzenie, edytowanie i udostępnianie pulpitów nawigacyjnych** na pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="0bd57-119">**Create, edit, and share dashboards** in the dashboard toolbar.</span></span>
5. <span data-ttu-id="0bd57-120">**Edytuj pulpitu nawigacyjnego**: Umieść kursor nad kafelka, a następnie użyć jego górnym pasku do przenoszenia, dostosować lub usuń go.</span><span class="sxs-lookup"><span data-stu-id="0bd57-120">**Edit the dashboard**: Hover over a tile and then use its top bar to move, customize, or remove it.</span></span>

## <a name="add-to-a-dashboard"></a><span data-ttu-id="0bd57-121">Dodaj do pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="0bd57-121">Add to a dashboard</span></span>
<span data-ttu-id="0bd57-122">Podczas wyszukiwania w bloku lub zbiór wykresy, która ma zastosowanie szczególnie, można przypiąć kopii do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="0bd57-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it to the dashboard.</span></span> <span data-ttu-id="0bd57-123">Zobaczysz go następnym razem, gdy istnieje powrocie.</span><span class="sxs-lookup"><span data-stu-id="0bd57-123">You'll see it next time you return there.</span></span>

![Aby przypiąć wykres, umieść kursor nad jego, a następnie kliknij przycisk "..." w nagłówku.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="0bd57-125">Numer PIN wykres do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="0bd57-125">Pin chart to dashboard.</span></span> <span data-ttu-id="0bd57-126">Kopię wykres zostanie wyświetlony na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="0bd57-126">A copy of the chart appears on the dashboard.</span></span>
2. <span data-ttu-id="0bd57-127">Przypnij cały blok do pulpitu nawigacyjnego — pojawia się na pulpicie nawigacyjnym jako kafelków, które można kliknąć, za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="0bd57-127">Pin the whole blade to the dashboard - it appears on the dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="0bd57-128">Kliknij lewym górnym rogu, aby powrócić do bieżącego pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="0bd57-128">Click the top left corner to return to the current dashboard.</span></span> <span data-ttu-id="0bd57-129">Następnie można użyć listy rozwijanej, aby powrócić do bieżącego widoku.</span><span class="sxs-lookup"><span data-stu-id="0bd57-129">Then you can use the drop-down menu to return to the current view.</span></span>

<span data-ttu-id="0bd57-130">Zwróć uwagę, że wykresów są podzielone na kafelkach: kafelka może zawierać więcej niż jeden wykres.</span><span class="sxs-lookup"><span data-stu-id="0bd57-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="0bd57-131">Można przypiąć całego kafelka pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="0bd57-131">You pin the whole tile to the dashboard.</span></span>

<span data-ttu-id="0bd57-132">Wykres są automatycznie odświeżane z częstotliwością, która zależy od zakresu czasu wykresu:</span><span class="sxs-lookup"><span data-stu-id="0bd57-132">The chart is automatically refreshed with a frequency that depends on the chart's time range:</span></span>

* <span data-ttu-id="0bd57-133">Maksymalnie 1 godzina przedziałów czasu: Odśwież co 5 minut</span><span class="sxs-lookup"><span data-stu-id="0bd57-133">Time range up to 1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="0bd57-134">Zakres czasu 1-24 godzin: Odśwież co 15 minut</span><span class="sxs-lookup"><span data-stu-id="0bd57-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="0bd57-135">Zakres powyżej 24 godzin czasu: (zakres czasu) / 60.</span><span class="sxs-lookup"><span data-stu-id="0bd57-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="0bd57-136">Przypnij dowolnej kwerendy w module analiz</span><span class="sxs-lookup"><span data-stu-id="0bd57-136">Pin any query in Analytics</span></span>
<span data-ttu-id="0bd57-137">Możesz również [przypiąć Analytics](app-insights-analytics-using.md#pin-to-dashboard) wykresy do [udostępnionego](#share-dashboards-with-your-team) pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="0bd57-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts to a [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="0bd57-138">Dzięki temu można Dodaj wykresy każde zapytanie dowolnego obok standardowe metryki.</span><span class="sxs-lookup"><span data-stu-id="0bd57-138">This allows you to add charts of any arbitrary query alongside the standard metrics.</span></span> 

<span data-ttu-id="0bd57-139">Wyniki są automatycznie obliczane ponownie co godzinę.</span><span class="sxs-lookup"><span data-stu-id="0bd57-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="0bd57-140">Kliknij ikonę odświeżania na wykresie, aby ponownie obliczyć natychmiast.</span><span class="sxs-lookup"><span data-stu-id="0bd57-140">Click the Refresh icon on the chart to recalculate immediately.</span></span> <span data-ttu-id="0bd57-141">(Odśwież w przeglądarce nie oblicza ponownie.)</span><span class="sxs-lookup"><span data-stu-id="0bd57-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-the-dashboard"></a><span data-ttu-id="0bd57-142">Dostosuj kafelka na pulpicie nawigacyjnym</span><span class="sxs-lookup"><span data-stu-id="0bd57-142">Adjust a tile on the dashboard</span></span>
<span data-ttu-id="0bd57-143">Po kafelka na pulpicie nawigacyjnym można dostosować.</span><span class="sxs-lookup"><span data-stu-id="0bd57-143">Once a tile is on the dashboard, you can adjust it.</span></span>

![Umieść kursor nad wykresu, aby go edytować.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="0bd57-145">Dodaj wykres do fragmentu.</span><span class="sxs-lookup"><span data-stu-id="0bd57-145">Add a chart to the tile.</span></span>
2. <span data-ttu-id="0bd57-146">Ustaw metryki, Grupuj według wymiaru i styl (tabeli, wykres) wykresu.</span><span class="sxs-lookup"><span data-stu-id="0bd57-146">Set the metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="0bd57-147">Przeciągnij w diagramie, aby powiększyć; Kliknij przycisk Cofnij, aby zresetować timespan; Ustawianie właściwości filtru dla wykresów na kafelku.</span><span class="sxs-lookup"><span data-stu-id="0bd57-147">Drag across the diagram to zoom in; click the undo button to reset the timespan; set filter properties for the charts on the tile.</span></span>
4. <span data-ttu-id="0bd57-148">Ustaw tytułem kafelka.</span><span class="sxs-lookup"><span data-stu-id="0bd57-148">Set tile title.</span></span>

<span data-ttu-id="0bd57-149">Kafelki przypięte z Eksploratora metryk bloków ma więcej opcji edycji niż Kafelki przypięte z bloku omówienie.</span><span class="sxs-lookup"><span data-stu-id="0bd57-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="0bd57-150">Kafelek oryginalnego przypięte nie ma wpływu zmiany.</span><span class="sxs-lookup"><span data-stu-id="0bd57-150">The original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="0bd57-151">Przełączanie między pulpity nawigacyjne</span><span class="sxs-lookup"><span data-stu-id="0bd57-151">Switch between dashboards</span></span>
<span data-ttu-id="0bd57-152">Można zapisać więcej niż jednym pulpicie nawigacyjnym i przełączać się między nimi.</span><span class="sxs-lookup"><span data-stu-id="0bd57-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="0bd57-153">Po przypięciu wykres lub bloku, są one dodawane do bieżącego pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="0bd57-153">When you pin a chart or blade, they're added to the current dashboard.</span></span>

![Aby przełączyć między pulpitami nawigacyjnymi, kliknij pozycję pulpit nawigacyjny i wybierz zapisany pulpitu nawigacyjnego.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="0bd57-157">Na przykład może być jednym pulpicie nawigacyjnym do wyświetlania pełnego ekranu w pokoju zespołu i drugi dla rozwoju ogólne.</span><span class="sxs-lookup"><span data-stu-id="0bd57-157">For example, you might have one dashboard for displaying full screen in the team room, and another for general development.</span></span>

<span data-ttu-id="0bd57-158">Na pulpicie nawigacyjnym zostanie wyświetlony blok jako Kafelek: kliknij go, aby przejść do bloku.</span><span class="sxs-lookup"><span data-stu-id="0bd57-158">On the dashboard, a blade appears as a tile: click it to go to the blade.</span></span> <span data-ttu-id="0bd57-159">Wykres replikuje wykresu w jej oryginalnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="0bd57-159">A chart replicates the chart in its original location.</span></span>

![Kliknij Kafelek, aby otworzyć blok, który reprezentuje](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="0bd57-161">Udostępnianie pulpitów nawigacyjnych</span><span class="sxs-lookup"><span data-stu-id="0bd57-161">Share dashboards</span></span>
<span data-ttu-id="0bd57-162">Po utworzeniu pulpitu nawigacyjnego, można go udostępniać innym użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="0bd57-162">When you've created a dashboard, you can share it with other users.</span></span>

![W nagłówku pulpitu nawigacyjnego kliknij przycisk Udostępnij](./media/app-insights-dashboards/41.png)

<span data-ttu-id="0bd57-164">Dowiedz się więcej o [ról i kontroli dostępu](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="0bd57-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="0bd57-165">Aplikacja nawigacji</span><span class="sxs-lookup"><span data-stu-id="0bd57-165">App navigation</span></span>
<span data-ttu-id="0bd57-166">Omówienie bloku jest bramy, aby uzyskać więcej informacji o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0bd57-166">The overview blade is the gateway to more information about your app.</span></span>

* <span data-ttu-id="0bd57-167">**Kafelek lub wykres** — kliknij Kafelek lub wykresu, aby zobaczyć więcej szczegółów na temat jego wartość.</span><span class="sxs-lookup"><span data-stu-id="0bd57-167">**Any chart or tile** - Click any tile or chart to see more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="0bd57-168">Przyciski bloku — omówienie</span><span class="sxs-lookup"><span data-stu-id="0bd57-168">Overview blade buttons</span></span>
![Omówienie bloku górnym pasku nawigacyjnym](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="0bd57-170">[**Eksploratora metryk** ](app-insights-metrics-explorer.md) — tworzenie własnych wykresów wydajności i użycia.</span><span class="sxs-lookup"><span data-stu-id="0bd57-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="0bd57-171">[**Wyszukiwanie** ](app-insights-diagnostic-search.md) — Zbadaj określone wystąpienia zdarzenia, takie jak żądań, wyjątków, lub dziennika śledzenia.</span><span class="sxs-lookup"><span data-stu-id="0bd57-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="0bd57-172">[**Analiza** ](app-insights-analytics.md) -wydajnych zapytań za pośrednictwem telemetrii.</span><span class="sxs-lookup"><span data-stu-id="0bd57-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="0bd57-173">**Zakres czasu** — Dostosuj zakres wyświetlanych przez wszystkich schematów w bloku.</span><span class="sxs-lookup"><span data-stu-id="0bd57-173">**Time range** - Adjust the range displayed by all the charts on the blade.</span></span>
* <span data-ttu-id="0bd57-174">**Usuń** — Usuwanie zasobu usługi Application Insights dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0bd57-174">**Delete** - Delete the Application Insights resource for this app.</span></span> <span data-ttu-id="0bd57-175">Należy również albo usunąć pakietów usługi Application Insights w kodzie aplikacji, lub edytować [klucza Instrumentacji](app-insights-create-new-resource.md#copy-the-instrumentation-key) w aplikacji, aby przekierować dane telemetryczne do innego zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0bd57-175">You should also either remove the Application Insights packages from your app code, or edit the [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app to direct telemetry to a different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="0bd57-176">Karta Essentials</span><span class="sxs-lookup"><span data-stu-id="0bd57-176">Essentials tab</span></span>
* <span data-ttu-id="0bd57-177">[Klucz Instrumentacji](app-insights-create-new-resource.md#copy-the-instrumentation-key) -identyfikuje tego zasobu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0bd57-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="0bd57-178">Cennik - dostęp do funkcji caps dostępne i ustaw woluminu.</span><span class="sxs-lookup"><span data-stu-id="0bd57-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="0bd57-179">Pasek nawigacyjny aplikacji</span><span class="sxs-lookup"><span data-stu-id="0bd57-179">App navigation bar</span></span>
![Lewy pasek nawigacyjny](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="0bd57-181">**Omówienie** -powrócić do bloku Omówienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0bd57-181">**Overview** - Return to the app overview blade.</span></span>
* <span data-ttu-id="0bd57-182">**Dziennik aktywności** — alerty i zdarzenia administracyjne platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd57-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="0bd57-183">[**Kontrola dostępu** ](app-insights-resources-roles-access-control.md) — zapewnianie dostępu do członków zespołu i inne.</span><span class="sxs-lookup"><span data-stu-id="0bd57-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access to team members and others.</span></span>
* <span data-ttu-id="0bd57-184">[**Tagi** ](../azure-resource-manager/resource-group-using-tags.md) -używaj tagów do grupy aplikacji z innymi osobami.</span><span class="sxs-lookup"><span data-stu-id="0bd57-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags to group your app with others.</span></span>

<span data-ttu-id="0bd57-185">ZBADAJ</span><span class="sxs-lookup"><span data-stu-id="0bd57-185">INVESTIGATE</span></span>

* <span data-ttu-id="0bd57-186">[**Mapowanie aplikacji** ](app-insights-app-map.md) -aktywna mapa przedstawiająca składniki aplikacji, pochodzących z informacji o zależnościach.</span><span class="sxs-lookup"><span data-stu-id="0bd57-186">[**Application map**](app-insights-app-map.md) - Active map showing the components of your application, derived from the dependency information.</span></span>
* <span data-ttu-id="0bd57-187">[**Inteligentne wykrywania** ](app-insights-proactive-diagnostics.md) — Przejrzyj ostatnie alerty dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="0bd57-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="0bd57-188">[**Strumień na żywo** ](app-insights-live-stream.md) — A ustalony zbiór metryki niemal natychmiastowe przydatne podczas wdrażania nowej kompilacji lub debugowania.</span><span class="sxs-lookup"><span data-stu-id="0bd57-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="0bd57-189">[**Dostępność / testów sieci Web** ](app-insights-monitor-web-app-availability.md) -wysyłać żądania regularne do aplikacji sieci web z wokół world.*</span><span class="sxs-lookup"><span data-stu-id="0bd57-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests to your web app from around the world.*</span></span>
* <span data-ttu-id="0bd57-190">[**Błędów, wydajności** ](app-insights-web-monitor-performance.md) -wyjątki, awariami i czas odpowiedzi dla żądań kierowanych do aplikacji i żądania od aplikacji [zależności](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="0bd57-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests to your app and for requests from your app to [dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="0bd57-191">[**Wydajność** ](app-insights-web-monitor-performance.md) — czas odpowiedzi, czas odpowiedzi zależności.</span><span class="sxs-lookup"><span data-stu-id="0bd57-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="0bd57-192">[Serwery](app-insights-web-monitor-performance.md) -liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="0bd57-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="0bd57-193">Jeśli dostępne możesz [Zainstaluj Monitor stanu](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="0bd57-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="0bd57-194">**Przeglądarka** — strona widoku i wydajności AJAX.</span><span class="sxs-lookup"><span data-stu-id="0bd57-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="0bd57-195">Jeśli dostępne możesz [Instrumentacja stron sieci web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="0bd57-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="0bd57-196">**Użycie** — strona widoku, użytkownika i sesji liczby.</span><span class="sxs-lookup"><span data-stu-id="0bd57-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="0bd57-197">Jeśli dostępne możesz [Instrumentacja stron sieci web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="0bd57-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="0bd57-198">KONFIGUROWANIE</span><span class="sxs-lookup"><span data-stu-id="0bd57-198">CONFIGURE</span></span>

* <span data-ttu-id="0bd57-199">**Wprowadzenie** — samouczek wbudowanego.</span><span class="sxs-lookup"><span data-stu-id="0bd57-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="0bd57-200">**Właściwości** -klucza instrumentacji, subskrypcji i identyfikator zasobu.</span><span class="sxs-lookup"><span data-stu-id="0bd57-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="0bd57-201">[Alerty](app-insights-alerts.md) -metryki konfiguracji alertu.</span><span class="sxs-lookup"><span data-stu-id="0bd57-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="0bd57-202">[Eksport ciągły](app-insights-export-telemetry.md) — Konfigurowanie eksportowania danych telemetrycznych do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd57-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry to Azure storage.</span></span>
* <span data-ttu-id="0bd57-203">[Testowanie wydajności](app-insights-monitor-web-app-availability.md#performance-tests) -konfigurowania syntetycznego obciążenia w witrynie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0bd57-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="0bd57-204">[Limit przydziału i cenach](app-insights-pricing.md) i [próbkowania wprowadzanie](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="0bd57-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="0bd57-205">**Dostępu do interfejsu API** — tworzenie [wersji adnotacje](app-insights-annotations.md) i interfejsu API dostępu do danych.</span><span class="sxs-lookup"><span data-stu-id="0bd57-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for the Data Access API.</span></span>
* <span data-ttu-id="0bd57-206">[**Elementy robocze** ](app-insights-diagnostic-search.md#create-work-item) -nawiązać połączenia z pracy, w systemie śledzenia, dzięki czemu można tworzyć błędy podczas sprawdzania telemetrii.</span><span class="sxs-lookup"><span data-stu-id="0bd57-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect to a work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="0bd57-207">USTAWIENIA</span><span class="sxs-lookup"><span data-stu-id="0bd57-207">SETTINGS</span></span>

* <span data-ttu-id="0bd57-208">[**Blokuje** ](../azure-resource-manager/resource-group-lock-resources.md) — blokowanie zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0bd57-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="0bd57-209">[**Skrypt automatyzacji** ](app-insights-powershell.md) — Eksportowanie definicji zasobów platformy Azure, aby jako szablon służy do tworzenia nowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="0bd57-209">[**Automation script**](app-insights-powershell.md) - export a definition of the Azure resource so that you can use it as a template to create new resources.</span></span>


## <a name="video"></a><span data-ttu-id="0bd57-210">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="0bd57-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="0bd57-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0bd57-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="0bd57-212">Eksploratora metryk</span><span class="sxs-lookup"><span data-stu-id="0bd57-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="0bd57-213">Filtr i segmentu metryki</span><span class="sxs-lookup"><span data-stu-id="0bd57-213">Filter and segment metrics</span></span> |![Przykładowe wyszukiwania](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="0bd57-215">Wyszukiwanie diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="0bd57-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="0bd57-216">Znajdowanie i Sprawdź zdarzenia, zdarzenia powiązane i tworzenie usterki</span><span class="sxs-lookup"><span data-stu-id="0bd57-216">Find and inspect events, related events, and create bugs</span></span> |![Przykładowe wyszukiwania](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="0bd57-218">Analiza</span><span class="sxs-lookup"><span data-stu-id="0bd57-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="0bd57-219">Język zapytania zaawansowane</span><span class="sxs-lookup"><span data-stu-id="0bd57-219">Powerful query language</span></span> |![Przykładowe wyszukiwania](./media/app-insights-dashboards/63.png) |
