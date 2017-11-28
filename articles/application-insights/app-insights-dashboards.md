---
title: aaaDashboards i nawigacja w hello Azure Application Insights | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a><span data-ttu-id="b5948-103">Nawigacji i pulpitów nawigacyjnych w portalu usługi Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="b5948-103">Navigation and Dashboards in hello Application Insights portal</span></span>
<span data-ttu-id="b5948-104">Po utworzeniu [skonfiguruj usługę Application Insights w projekcie](app-insights-overview.md), dane telemetryczne dotyczące wydajności i użycia aplikacji będą wyświetlane w projektu zasobu usługi Application Insights w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b5948-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="b5948-105">Znajdź telemetrii</span><span class="sxs-lookup"><span data-stu-id="b5948-105">Find your telemetry</span></span>
<span data-ttu-id="b5948-106">Zaloguj się toohello [portalu Azure](https://portal.azure.com) i przejdź do zasobu usługi Application Insights toohello, który został utworzony dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5948-106">Sign in toohello [Azure portal](https://portal.azure.com) and navigate toohello Application Insights resource that you created for your app.</span></span>

![Kliknij przycisk Przeglądaj, wybierz usługę Application Insights, a następnie aplikacji.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="b5948-108">Hello omówienie bloku (strona) dla aplikacji przedstawiono podsumowanie kluczowych metryk diagnostycznych hello aplikacji i jest toohello bramy innych funkcji hello portalu.</span><span class="sxs-lookup"><span data-stu-id="b5948-108">hello overview blade (page) for your app shows a summary of hello key diagnostic metrics of your app, and is a gateway toohello other features of hello portal.</span></span>

![Główne marszruty tooview telemetrii](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="b5948-110">Można dostosować żadnego z wykresami hello i siatki i przypiąć je tooa pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b5948-110">You can customize any of hello charts and grids and pin them tooa dashboard.</span></span> <span data-ttu-id="b5948-111">W ten sposób można zebrać razem hello klucza dane telemetryczne z różnych aplikacji na pulpicie nawigacyjnym centralnej.</span><span class="sxs-lookup"><span data-stu-id="b5948-111">That way, you can bring together hello key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="b5948-112">Pulpity nawigacyjne</span><span class="sxs-lookup"><span data-stu-id="b5948-112">Dashboards</span></span>
<span data-ttu-id="b5948-113">Witaj po pierwsze zostanie wyświetlony po zalogowaniu w toohello [portalu Microsoft Azure](https://portal.azure.com) jest pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="b5948-113">hello first thing you see after you sign in toohello [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="b5948-114">W tym miejscu można zebrać razem hello wykresy, które będą tooyou najważniejszych dla wszystkich zasobów platformy Azure, w tym dane telemetryczne z [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5948-114">Here you can bring together hello charts that are most important tooyou across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Dostosowany pulpit nawigacyjny.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="b5948-116">**Przejdź zasobów toospecific** takich jak aplikacji w usłudze Application Insights: Użyj hello lewy pasek.</span><span class="sxs-lookup"><span data-stu-id="b5948-116">**Navigate toospecific resources** such as your app in Application Insights: Use hello left bar.</span></span>
2. <span data-ttu-id="b5948-117">**Zwracany toohello bieżącego pulpitu nawigacyjnego**, lub przełączania widoków ostatnie tooother: Użyj menu rozwijanego hello u góry po lewej.</span><span class="sxs-lookup"><span data-stu-id="b5948-117">**Return toohello current dashboard**, or switch tooother recent views: Use hello drop-down menu at top left.</span></span>
3. <span data-ttu-id="b5948-118">**Przełącz pulpity nawigacyjne**: Użyj menu rozwijanego hello na powitania Tytuł pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="b5948-118">**Switch dashboards**: Use hello drop-down menu on hello dashboard title</span></span>
4. <span data-ttu-id="b5948-119">**Tworzenie, edytowanie i udostępnianie pulpitów nawigacyjnych** hello pulpitu nawigacyjnego w pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="b5948-119">**Create, edit, and share dashboards** in hello dashboard toolbar.</span></span>
5. <span data-ttu-id="b5948-120">**Edytuj pulpitu nawigacyjnego hello**: Umieść kursor nad kafelka, a następnie użyć jego górnej paska toomove, dostosowywanie, lub usuń go.</span><span class="sxs-lookup"><span data-stu-id="b5948-120">**Edit hello dashboard**: Hover over a tile and then use its top bar toomove, customize, or remove it.</span></span>

## <a name="add-tooa-dashboard"></a><span data-ttu-id="b5948-121">Dodaj tooa pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="b5948-121">Add tooa dashboard</span></span>
<span data-ttu-id="b5948-122">Podczas wyszukiwania w bloku lub zbiór wykresy, która ma zastosowanie szczególnie, można przypiąć kopii toohello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b5948-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it toohello dashboard.</span></span> <span data-ttu-id="b5948-123">Zobaczysz go następnym razem, gdy istnieje powrocie.</span><span class="sxs-lookup"><span data-stu-id="b5948-123">You'll see it next time you return there.</span></span>

![toopin wykresu, umieść kursor nad jego, a następnie kliknij przycisk "..." w nagłówku hello.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="b5948-125">Przypnij toodashboard wykresu.</span><span class="sxs-lookup"><span data-stu-id="b5948-125">Pin chart toodashboard.</span></span> <span data-ttu-id="b5948-126">Kopię hello wykres zostanie wyświetlony na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="b5948-126">A copy of hello chart appears on hello dashboard.</span></span>
2. <span data-ttu-id="b5948-127">Numer PIN hello cały blok toohello pulpitu nawigacyjnego — jest widoczny na pulpicie nawigacyjnym hello jako kafelków, które można kliknąć, za pomocą.</span><span class="sxs-lookup"><span data-stu-id="b5948-127">Pin hello whole blade toohello dashboard - it appears on hello dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="b5948-128">Kliknij przycisk hello lewym górnym rogu tooreturn toohello bieżącego pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b5948-128">Click hello top left corner tooreturn toohello current dashboard.</span></span> <span data-ttu-id="b5948-129">Następnie można użyć hello menu rozwijanego tooreturn toohello bieżący widok.</span><span class="sxs-lookup"><span data-stu-id="b5948-129">Then you can use hello drop-down menu tooreturn toohello current view.</span></span>

<span data-ttu-id="b5948-130">Zwróć uwagę, że wykresów są podzielone na kafelkach: kafelka może zawierać więcej niż jeden wykres.</span><span class="sxs-lookup"><span data-stu-id="b5948-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="b5948-131">Pulpit nawigacyjny toohello całego kafelka hello można przypiąć.</span><span class="sxs-lookup"><span data-stu-id="b5948-131">You pin hello whole tile toohello dashboard.</span></span>

<span data-ttu-id="b5948-132">Wykres Hello są automatycznie odświeżane z częstotliwością, która zależy od zakresu czasu wykresu hello:</span><span class="sxs-lookup"><span data-stu-id="b5948-132">hello chart is automatically refreshed with a frequency that depends on hello chart's time range:</span></span>

* <span data-ttu-id="b5948-133">Zakres zapasowej godzinę too1 czasu: Odśwież co 5 minut</span><span class="sxs-lookup"><span data-stu-id="b5948-133">Time range up too1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="b5948-134">Zakres czasu 1-24 godzin: Odśwież co 15 minut</span><span class="sxs-lookup"><span data-stu-id="b5948-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="b5948-135">Zakres powyżej 24 godzin czasu: (zakres czasu) / 60.</span><span class="sxs-lookup"><span data-stu-id="b5948-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="b5948-136">Przypnij dowolnej kwerendy w module analiz</span><span class="sxs-lookup"><span data-stu-id="b5948-136">Pin any query in Analytics</span></span>
<span data-ttu-id="b5948-137">Możesz również [przypiąć Analytics](app-insights-analytics-using.md#pin-to-dashboard) tooa wykresów [udostępnionego](#share-dashboards-with-your-team) pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b5948-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts tooa [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="b5948-138">Dzięki temu wykresy tooadd wszelkie zapytania dowolnego obok hello standardowe metryki.</span><span class="sxs-lookup"><span data-stu-id="b5948-138">This allows you tooadd charts of any arbitrary query alongside hello standard metrics.</span></span> 

<span data-ttu-id="b5948-139">Wyniki są automatycznie obliczane ponownie co godzinę.</span><span class="sxs-lookup"><span data-stu-id="b5948-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="b5948-140">Kliknij ikonę odświeżania hello na powitania wykresu toorecalculate natychmiast.</span><span class="sxs-lookup"><span data-stu-id="b5948-140">Click hello Refresh icon on hello chart toorecalculate immediately.</span></span> <span data-ttu-id="b5948-141">(Odśwież w przeglądarce nie oblicza ponownie.)</span><span class="sxs-lookup"><span data-stu-id="b5948-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-hello-dashboard"></a><span data-ttu-id="b5948-142">Dostosuj kafelka na pulpicie nawigacyjnym hello</span><span class="sxs-lookup"><span data-stu-id="b5948-142">Adjust a tile on hello dashboard</span></span>
<span data-ttu-id="b5948-143">Po kafelka na pulpicie nawigacyjnym hello można dostosować.</span><span class="sxs-lookup"><span data-stu-id="b5948-143">Once a tile is on hello dashboard, you can adjust it.</span></span>

![Umieść kursor nad wykresu w kolejności tooedit go.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="b5948-145">Dodaj kafelka toohello wykresu.</span><span class="sxs-lookup"><span data-stu-id="b5948-145">Add a chart toohello tile.</span></span>
2. <span data-ttu-id="b5948-146">Metryka hello zestaw Grupuj według wymiaru i styl (tabeli, wykres) wykresu.</span><span class="sxs-lookup"><span data-stu-id="b5948-146">Set hello metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="b5948-147">Przeciąganie hello diagram toozoom Kliknij przycisk hello cofania przycisk tooreset hello timespan; Ustaw właściwości filtru w przypadku wykresów hello na kafelku hello.</span><span class="sxs-lookup"><span data-stu-id="b5948-147">Drag across hello diagram toozoom in; click hello undo button tooreset hello timespan; set filter properties for hello charts on hello tile.</span></span>
4. <span data-ttu-id="b5948-148">Ustaw tytułem kafelka.</span><span class="sxs-lookup"><span data-stu-id="b5948-148">Set tile title.</span></span>

<span data-ttu-id="b5948-149">Kafelki przypięte z Eksploratora metryk bloków ma więcej opcji edycji niż Kafelki przypięte z bloku omówienie.</span><span class="sxs-lookup"><span data-stu-id="b5948-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="b5948-150">Hello Kafelek oryginalnego przypięte nie ma wpływu zmiany.</span><span class="sxs-lookup"><span data-stu-id="b5948-150">hello original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="b5948-151">Przełączanie między pulpity nawigacyjne</span><span class="sxs-lookup"><span data-stu-id="b5948-151">Switch between dashboards</span></span>
<span data-ttu-id="b5948-152">Można zapisać więcej niż jednym pulpicie nawigacyjnym i przełączać się między nimi.</span><span class="sxs-lookup"><span data-stu-id="b5948-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="b5948-153">Po przypięciu wykres lub bloku, są one dodawane toohello bieżącego pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b5948-153">When you pin a chart or blade, they're added toohello current dashboard.</span></span>

![tooswitch między pulpitami nawigacyjnymi, kliknij pozycję pulpit nawigacyjny i wybierz zapisany pulpitu nawigacyjnego.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="b5948-157">Na przykład może być jednym pulpicie nawigacyjnym do wyświetlania pełnego ekranu w pokoju zespołu hello i drugi dla rozwoju ogólne.</span><span class="sxs-lookup"><span data-stu-id="b5948-157">For example, you might have one dashboard for displaying full screen in hello team room, and another for general development.</span></span>

<span data-ttu-id="b5948-158">Na pulpicie nawigacyjnym hello, blok jest wyświetlana jako Kafelek: kliknij go toogo toohello bloku.</span><span class="sxs-lookup"><span data-stu-id="b5948-158">On hello dashboard, a blade appears as a tile: click it toogo toohello blade.</span></span> <span data-ttu-id="b5948-159">Wykres replikuje hello wykresu w jej oryginalnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="b5948-159">A chart replicates hello chart in its original location.</span></span>

![Kliknij przycisk bloku hello tooopen kafelka, który reprezentuje](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="b5948-161">Udostępnianie pulpitów nawigacyjnych</span><span class="sxs-lookup"><span data-stu-id="b5948-161">Share dashboards</span></span>
<span data-ttu-id="b5948-162">Po utworzeniu pulpitu nawigacyjnego, można go udostępniać innym użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="b5948-162">When you've created a dashboard, you can share it with other users.</span></span>

![W nagłówku pulpitu nawigacyjnego hello kliknij przycisk Udostępnij](./media/app-insights-dashboards/41.png)

<span data-ttu-id="b5948-164">Dowiedz się więcej o [ról i kontroli dostępu](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="b5948-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="b5948-165">Aplikacja nawigacji</span><span class="sxs-lookup"><span data-stu-id="b5948-165">App navigation</span></span>
<span data-ttu-id="b5948-166">Blok omówienie Hello jest hello bramy toomore informacje o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5948-166">hello overview blade is hello gateway toomore information about your app.</span></span>

* <span data-ttu-id="b5948-167">**Kafelek lub wykres** — kliknij Kafelek lub wykresu toosee szczegółowe informacje o jego wartość.</span><span class="sxs-lookup"><span data-stu-id="b5948-167">**Any chart or tile** - Click any tile or chart toosee more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="b5948-168">Przyciski bloku — omówienie</span><span class="sxs-lookup"><span data-stu-id="b5948-168">Overview blade buttons</span></span>
![Omówienie bloku górnym pasku nawigacyjnym](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="b5948-170">[**Eksploratora metryk** ](app-insights-metrics-explorer.md) — tworzenie własnych wykresów wydajności i użycia.</span><span class="sxs-lookup"><span data-stu-id="b5948-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="b5948-171">[**Wyszukiwanie** ](app-insights-diagnostic-search.md) — Zbadaj określone wystąpienia zdarzenia, takie jak żądań, wyjątków, lub dziennika śledzenia.</span><span class="sxs-lookup"><span data-stu-id="b5948-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="b5948-172">[**Analiza** ](app-insights-analytics.md) -wydajnych zapytań za pośrednictwem telemetrii.</span><span class="sxs-lookup"><span data-stu-id="b5948-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="b5948-173">**Zakres czasu** — Dostosuj zakres hello wyświetlane przez wszystkich schematów hello na powitania bloku.</span><span class="sxs-lookup"><span data-stu-id="b5948-173">**Time range** - Adjust hello range displayed by all hello charts on hello blade.</span></span>
* <span data-ttu-id="b5948-174">**Usuń** -Usuń hello zasobu usługi Application Insights dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5948-174">**Delete** - Delete hello Application Insights resource for this app.</span></span> <span data-ttu-id="b5948-175">Należy również albo usunąć hello pakietów usługi Application Insights w kodzie aplikacji, lub edytować hello [klucza Instrumentacji](app-insights-create-new-resource.md#copy-the-instrumentation-key) w zasobu usługi Application Insights różnych tooa Twojej aplikacji toodirect telemetrii.</span><span class="sxs-lookup"><span data-stu-id="b5948-175">You should also either remove hello Application Insights packages from your app code, or edit hello [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app toodirect telemetry tooa different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="b5948-176">Karta Essentials</span><span class="sxs-lookup"><span data-stu-id="b5948-176">Essentials tab</span></span>
* <span data-ttu-id="b5948-177">[Klucz Instrumentacji](app-insights-create-new-resource.md#copy-the-instrumentation-key) -identyfikuje tego zasobu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5948-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="b5948-178">Cennik - dostęp do funkcji caps dostępne i ustaw woluminu.</span><span class="sxs-lookup"><span data-stu-id="b5948-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="b5948-179">Pasek nawigacyjny aplikacji</span><span class="sxs-lookup"><span data-stu-id="b5948-179">App navigation bar</span></span>
![Lewy pasek nawigacyjny](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="b5948-181">**Omówienie** -bloku Omówienie aplikacji toohello zwracany.</span><span class="sxs-lookup"><span data-stu-id="b5948-181">**Overview** - Return toohello app overview blade.</span></span>
* <span data-ttu-id="b5948-182">**Dziennik aktywności** — alerty i zdarzenia administracyjne platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b5948-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="b5948-183">[**Kontrola dostępu** ](app-insights-resources-roles-access-control.md) — Podaj członków tooteam dostępu i innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b5948-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access tooteam members and others.</span></span>
* <span data-ttu-id="b5948-184">[**Tagi** ](../azure-resource-manager/resource-group-using-tags.md) -Użyj tagów toogroup aplikacji z innymi osobami.</span><span class="sxs-lookup"><span data-stu-id="b5948-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags toogroup your app with others.</span></span>

<span data-ttu-id="b5948-185">ZBADAJ</span><span class="sxs-lookup"><span data-stu-id="b5948-185">INVESTIGATE</span></span>

* <span data-ttu-id="b5948-186">[**Mapowanie aplikacji** ](app-insights-app-map.md) -aktywna mapa przedstawiająca hello składniki aplikacji, pochodną hello informacji o zależnościach.</span><span class="sxs-lookup"><span data-stu-id="b5948-186">[**Application map**](app-insights-app-map.md) - Active map showing hello components of your application, derived from hello dependency information.</span></span>
* <span data-ttu-id="b5948-187">[**Inteligentne wykrywania** ](app-insights-proactive-diagnostics.md) — Przejrzyj ostatnie alerty dotyczące wydajności.</span><span class="sxs-lookup"><span data-stu-id="b5948-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="b5948-188">[**Strumień na żywo** ](app-insights-live-stream.md) — A ustalony zbiór metryki niemal natychmiastowe przydatne podczas wdrażania nowej kompilacji lub debugowania.</span><span class="sxs-lookup"><span data-stu-id="b5948-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="b5948-189">[**Dostępność / testów sieci Web** ](app-insights-monitor-web-app-availability.md) -wysyłania żądań regularne tooyour aplikacji sieci web z wokół hello world.*</span><span class="sxs-lookup"><span data-stu-id="b5948-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests tooyour web app from around hello world.*</span></span>
* <span data-ttu-id="b5948-190">[**Błędów, wydajności** ](app-insights-web-monitor-performance.md) -wyjątki, awariami i odpowiedzi czasu dla aplikacji tooyour żądań i żądań z aplikacji w zbyt[zależności](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="b5948-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests tooyour app and for requests from your app too[dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="b5948-191">[**Wydajność** ](app-insights-web-monitor-performance.md) — czas odpowiedzi, czas odpowiedzi zależności.</span><span class="sxs-lookup"><span data-stu-id="b5948-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="b5948-192">[Serwery](app-insights-web-monitor-performance.md) -liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="b5948-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="b5948-193">Jeśli dostępne możesz [Zainstaluj Monitor stanu](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="b5948-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="b5948-194">**Przeglądarka** — strona widoku i wydajności AJAX.</span><span class="sxs-lookup"><span data-stu-id="b5948-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="b5948-195">Jeśli dostępne możesz [Instrumentacja stron sieci web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="b5948-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="b5948-196">**Użycie** — strona widoku, użytkownika i sesji liczby.</span><span class="sxs-lookup"><span data-stu-id="b5948-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="b5948-197">Jeśli dostępne możesz [Instrumentacja stron sieci web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="b5948-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="b5948-198">KONFIGUROWANIE</span><span class="sxs-lookup"><span data-stu-id="b5948-198">CONFIGURE</span></span>

* <span data-ttu-id="b5948-199">**Wprowadzenie** — samouczek wbudowanego.</span><span class="sxs-lookup"><span data-stu-id="b5948-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="b5948-200">**Właściwości** -klucza instrumentacji, subskrypcji i identyfikator zasobu.</span><span class="sxs-lookup"><span data-stu-id="b5948-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="b5948-201">[Alerty](app-insights-alerts.md) -metryki konfiguracji alertu.</span><span class="sxs-lookup"><span data-stu-id="b5948-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="b5948-202">[Eksport ciągły](app-insights-export-telemetry.md) — Konfigurowanie eksportowania telemetrii tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="b5948-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry tooAzure storage.</span></span>
* <span data-ttu-id="b5948-203">[Testowanie wydajności](app-insights-monitor-web-app-availability.md#performance-tests) -konfigurowania syntetycznego obciążenia w witrynie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b5948-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="b5948-204">[Limit przydziału i cenach](app-insights-pricing.md) i [próbkowania wprowadzanie](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="b5948-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="b5948-205">**Dostępu do interfejsu API** — tworzenie [wersji adnotacje](app-insights-annotations.md) i hello interfejsu API usługi Data Access.</span><span class="sxs-lookup"><span data-stu-id="b5948-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for hello Data Access API.</span></span>
* <span data-ttu-id="b5948-206">[**Elementy robocze** ](app-insights-diagnostic-search.md#create-work-item) -Połącz pracy tooa systemie śledzenia, dzięki czemu można tworzyć błędy podczas sprawdzania telemetrii.</span><span class="sxs-lookup"><span data-stu-id="b5948-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect tooa work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="b5948-207">USTAWIENIA</span><span class="sxs-lookup"><span data-stu-id="b5948-207">SETTINGS</span></span>

* <span data-ttu-id="b5948-208">[**Blokuje** ](../azure-resource-manager/resource-group-lock-resources.md) — blokowanie zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b5948-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="b5948-209">[**Skrypt automatyzacji** ](app-insights-powershell.md) — Eksportowanie definicji hello zasobów platformy Azure, dzięki czemu można użyć jej jako szablonu toocreate nowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="b5948-209">[**Automation script**](app-insights-powershell.md) - export a definition of hello Azure resource so that you can use it as a template toocreate new resources.</span></span>


## <a name="video"></a><span data-ttu-id="b5948-210">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="b5948-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="b5948-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b5948-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="b5948-212">Eksploratora metryk</span><span class="sxs-lookup"><span data-stu-id="b5948-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="b5948-213">Filtr i segmentu metryki</span><span class="sxs-lookup"><span data-stu-id="b5948-213">Filter and segment metrics</span></span> |![Przykładowe wyszukiwania](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="b5948-215">Wyszukiwanie diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="b5948-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="b5948-216">Znajdowanie i Sprawdź zdarzenia, zdarzenia powiązane i tworzenie usterki</span><span class="sxs-lookup"><span data-stu-id="b5948-216">Find and inspect events, related events, and create bugs</span></span> |![Przykładowe wyszukiwania](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="b5948-218">Analiza</span><span class="sxs-lookup"><span data-stu-id="b5948-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="b5948-219">Język zapytania zaawansowane</span><span class="sxs-lookup"><span data-stu-id="b5948-219">Powerful query language</span></span> |![Przykładowe wyszukiwania](./media/app-insights-dashboards/63.png) |
