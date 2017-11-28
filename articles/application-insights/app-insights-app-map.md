---
title: "Mapa w usłudze Azure Application Insights aaaApplication | Dokumentacja firmy Microsoft"
description: "Wizualną prezentację hello zależności między składnikami aplikacji etykietą kluczowych wskaźników wydajności i alerty."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="a9354-103">Mapowanie aplikacji w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="a9354-103">Application Map in Application Insights</span></span>
<span data-ttu-id="a9354-104">W [Azure Application Insights](app-insights-overview.md), mapa aplikacji jest układu wizualnego relacji zależności hello składników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a9354-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of hello dependency relationships of your application components.</span></span> <span data-ttu-id="a9354-105">Każdy składnik pokazuje wskaźników KPI takich jak toohelp obciążenia, błędów, wydajności i alerty, odnajdywanie dowolny składnik przyczyną problemu z wydajnością lub błędu.</span><span class="sxs-lookup"><span data-stu-id="a9354-105">Each component shows KPIs such as load, performance, failures, and alerts, toohelp you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="a9354-106">Kliknij go, z dowolnym toomore składnika szczegółowe diagnostycznych, takich jak zdarzenia usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a9354-106">You can click through from any component toomore detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="a9354-107">Jeśli aplikacja korzysta z usług Azure, możesz również kliknąć za pośrednictwem diagnostics tooAzure, takie jak zalecenia doradcy bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="a9354-107">If your app uses Azure services, you can also click through tooAzure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="a9354-108">Podobnie jak inne wykresy można przypiąć toohello mapy aplikacji pulpitu nawigacyjnego platformy Azure, gdzie jest pełną funkcjonalność.</span><span class="sxs-lookup"><span data-stu-id="a9354-108">Like other charts, you can pin an application map toohello Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-hello-application-map"></a><span data-ttu-id="a9354-109">Mapowanie aplikacji hello otwarte</span><span class="sxs-lookup"><span data-stu-id="a9354-109">Open hello application map</span></span>
<span data-ttu-id="a9354-110">Mapa hello Otwórz za pomocą bloku omówienie hello aplikacji:</span><span class="sxs-lookup"><span data-stu-id="a9354-110">Open hello map from hello overview blade for your application:</span></span>

![Otwórz aplikację mapy](./media/app-insights-app-map/01.png)

![Mapa aplikacji](./media/app-insights-app-map/02.png)

<span data-ttu-id="a9354-113">Mapa Hello pokazuje:</span><span class="sxs-lookup"><span data-stu-id="a9354-113">hello map shows:</span></span>

* <span data-ttu-id="a9354-114">Testy dostępności</span><span class="sxs-lookup"><span data-stu-id="a9354-114">Availability tests</span></span>
* <span data-ttu-id="a9354-115">Składnik po stronie klienta (monitorowane w ramach hello JavaScript SDK)</span><span class="sxs-lookup"><span data-stu-id="a9354-115">Client-side component (monitored with hello JavaScript SDK)</span></span>
* <span data-ttu-id="a9354-116">Składnik po stronie serwera</span><span class="sxs-lookup"><span data-stu-id="a9354-116">Server-side component</span></span>
* <span data-ttu-id="a9354-117">Zależności hello składniki klienta i serwera</span><span class="sxs-lookup"><span data-stu-id="a9354-117">Dependencies of hello client and server components</span></span>

<span data-ttu-id="a9354-118">Można zwijać i rozwijać grupy łącze zależności:</span><span class="sxs-lookup"><span data-stu-id="a9354-118">You can expand and collapse dependency link groups:</span></span>

![Zwiń](./media/app-insights-app-map/03.png)

<span data-ttu-id="a9354-120">Jeśli masz wiele zależności jednego typu (SQL, HTTP itp.) są zgrupowane.</span><span class="sxs-lookup"><span data-stu-id="a9354-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![zależności grupowanych](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="a9354-122">Dodatkowych problemów</span><span class="sxs-lookup"><span data-stu-id="a9354-122">Spot problems</span></span>
<span data-ttu-id="a9354-123">Każdy węzeł ma odpowiednie wskaźniki, jak hello ładowania, wydajności i niepowodzenie szybkości dla tego składnika.</span><span class="sxs-lookup"><span data-stu-id="a9354-123">Each node has relevant performance indicators, such as hello load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="a9354-124">Ikonami ostrzeżenia zaznacz możliwych problemów.</span><span class="sxs-lookup"><span data-stu-id="a9354-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="a9354-125">Pomarańczowe ostrzeżenie oznacza, że błędy występują w żądaniach, wyświetleń strony lub wywołania zależności.</span><span class="sxs-lookup"><span data-stu-id="a9354-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="a9354-126">Czerwony oznacza współczynnik awaryjności powyżej 5%.</span><span class="sxs-lookup"><span data-stu-id="a9354-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="a9354-127">Jeśli chcesz tooadjust tych progów, Otwórz opcje.</span><span class="sxs-lookup"><span data-stu-id="a9354-127">If you want tooadjust these thresholds, open Options.</span></span>

![ikony błędu](./media/app-insights-app-map/04.png)

<span data-ttu-id="a9354-129">Aktywne alerty również Pokaż zapasową:</span><span class="sxs-lookup"><span data-stu-id="a9354-129">Active alerts also show up:</span></span> 

![aktywne alerty](./media/app-insights-app-map/05.png)

<span data-ttu-id="a9354-131">Jeśli używasz usług SQL Azure jest ikonę, która pokazuje, kiedy są zalecenia, w jaki sposób można poprawić wydajność.</span><span class="sxs-lookup"><span data-stu-id="a9354-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![zalecenie Azure](./media/app-insights-app-map/06.png)

<span data-ttu-id="a9354-133">Kliknij żadnych tooget ikona więcej szczegółów:</span><span class="sxs-lookup"><span data-stu-id="a9354-133">Click any icon tooget more details:</span></span>

![zalecenie Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="a9354-135">Kliknij diagnostyczne za pośrednictwem</span><span class="sxs-lookup"><span data-stu-id="a9354-135">Diagnostic click through</span></span>
<span data-ttu-id="a9354-136">Każdego z węzłów hello na mapie hello oferuje docelowe kliknij za pomocą diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="a9354-136">Each of hello nodes on hello map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="a9354-137">Opcje Hello będą się różnić w zależności od typu hello hello węzła.</span><span class="sxs-lookup"><span data-stu-id="a9354-137">hello options vary depending on hello type of hello node.</span></span>

![Opcje serwera](./media/app-insights-app-map/09.png)

<span data-ttu-id="a9354-139">Dla składników, które są hostowane na platformie Azure opcje hello obejmują toothem łączy bezpośrednich.</span><span class="sxs-lookup"><span data-stu-id="a9354-139">For components that are hosted in Azure, hello options include direct links toothem.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="a9354-140">Filtry i zakres czasu</span><span class="sxs-lookup"><span data-stu-id="a9354-140">Filters and time range</span></span>
<span data-ttu-id="a9354-141">Domyślnie mapy hello znajduje się podsumowanie wszystkich danych hello dostępna dla wybranego zakresu czasu hello.</span><span class="sxs-lookup"><span data-stu-id="a9354-141">By default, hello map summarizes all hello data available for hello chosen time range.</span></span> <span data-ttu-id="a9354-142">Ale filtru nazwy tylko w określonych operacji tooinclude lub zależności.</span><span class="sxs-lookup"><span data-stu-id="a9354-142">But you can filter it tooinclude only specific operation names or dependencies.</span></span>

* <span data-ttu-id="a9354-143">Nazwa operacji: dotyczy zarówno wyświetleń strony i typy żądania po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="a9354-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="a9354-144">Po wybraniu tej opcji hello Mapa pokazuje hello wskaźnika KPI w węźle serwera/klienta hello tylko w operacjach hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="a9354-144">With this option, hello map shows hello KPI on hello server/client-side node for hello selected operations only.</span></span> <span data-ttu-id="a9354-145">Pokazuje zależności hello wywoływana w kontekście hello tych określonych działań.</span><span class="sxs-lookup"><span data-stu-id="a9354-145">It shows hello dependencies called in hello context of those specific operations.</span></span>
* <span data-ttu-id="a9354-146">Nazwa podstawowa zależności: dotyczy to również hello AJAX przeglądarki zależności i zależności po stronie serwera.</span><span class="sxs-lookup"><span data-stu-id="a9354-146">Dependency base name: This includes hello AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="a9354-147">Jeśli raport dane telemetryczne zależności niestandardowych z hello TrackDependency API pojawią się również w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="a9354-147">If you report custom dependency telemetry with hello TrackDependency API, they also appear here.</span></span> <span data-ttu-id="a9354-148">Możesz wybrać tooshow zależności hello na mapie hello.</span><span class="sxs-lookup"><span data-stu-id="a9354-148">You can select hello dependencies tooshow on hello map.</span></span> <span data-ttu-id="a9354-149">Obecnie to pole wyboru nie filtruje hello żądania po stronie serwera lub hello wyświetleń strony po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="a9354-149">Currently this selection does not filter hello server-side requests, or hello client-side page views.</span></span>

![Ustaw filtry](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="a9354-151">Zapisz filtry</span><span class="sxs-lookup"><span data-stu-id="a9354-151">Save filters</span></span>
<span data-ttu-id="a9354-152">w przypadku zastosowania filtrów hello toosave, hello numeru pin filtrowane widoku na [pulpitu nawigacyjnego](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="a9354-152">toosave hello filters you have applied, pin hello filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Toodashboard numeru PIN](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="a9354-154">Okienko błędu</span><span class="sxs-lookup"><span data-stu-id="a9354-154">Error pane</span></span>
<span data-ttu-id="a9354-155">Po kliknięciu węzła w mapie hello okienko błędu jest wyświetlany na prawej stronie powitania podsumowania błędów dla tego węzła.</span><span class="sxs-lookup"><span data-stu-id="a9354-155">When you click a node in hello map, an error pane is displayed on hello right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="a9354-156">Awarie są najpierw pogrupowane według Identyfikatora operacji i pogrupowane według identyfikatora problemu.</span><span class="sxs-lookup"><span data-stu-id="a9354-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Okienko błędu](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="a9354-158">Kliknięcie awarii przyjmuje toohello ostatniego wystąpienia tego błędu.</span><span class="sxs-lookup"><span data-stu-id="a9354-158">Clicking on a failure takes you toohello most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="a9354-159">Kondycja zasobów</span><span class="sxs-lookup"><span data-stu-id="a9354-159">Resource health</span></span>
<span data-ttu-id="a9354-160">W przypadku niektórych typów zasobów kondycja zasobu jest wyświetlany u góry okienka błąd hello hello.</span><span class="sxs-lookup"><span data-stu-id="a9354-160">For some resource types, resource health is displayed at hello top of hello error pane.</span></span> <span data-ttu-id="a9354-161">Na przykład kliknięcie węzła SQL spowoduje wyświetlenie hello kondycji bazy danych i alerty, które mają być uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="a9354-161">For example, clicking a SQL node will show hello database health and any alerts that have fired.</span></span>

![Kondycja zasobów](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="a9354-163">Możesz kliknąć hello zasobu Nazwa tooview standardowe omówienie metryki dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a9354-163">You can click hello resource name tooview standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="a9354-164">System end-to-end aplikacji mapy</span><span class="sxs-lookup"><span data-stu-id="a9354-164">End-to-end system app maps</span></span>

<span data-ttu-id="a9354-165">*Wymaga zestawu SDK w wersji 2.3 lub nowszej*</span><span class="sxs-lookup"><span data-stu-id="a9354-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="a9354-166">Jeśli aplikacja ma kilka części — na przykład usługi zaplecza dodatkowo możesz toohello aplikacji sieci web — mogą być prezentowane z ich wszystkich na mapie jednej zintegrowanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a9354-166">If your application has several components - for example, a back-end service in addition toohello web app - then you can show them all on one integrated app map.</span></span>

![Ustaw filtry](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="a9354-168">Mapa aplikacji Hello znajduje węzły serwera, wykonując wszystkie wywołania zależności HTTP między serwerami z hello zainstalowany zestaw SDK usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a9354-168">hello app map finds server nodes by following any HTTP dependency calls made between servers with hello Application Insights SDK installed.</span></span> <span data-ttu-id="a9354-169">Każdy zasób usługi Application Insights zakłada, że toocontain jeden serwer.</span><span class="sxs-lookup"><span data-stu-id="a9354-169">Each Application Insights resource is assumed toocontain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="a9354-170">Mapa aplikacji usługi roli (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="a9354-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="a9354-171">Funkcja mapy usługi roli aplikacji Hello w wersji zapoznawczej pozwala mapy aplikacji hello toouse z wieloma serwerami wysyłania danych toohello tego samego zasobu usługi Application Insights / klucz instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="a9354-171">hello preview multi-role app map feature allows you toouse hello app map with multiple servers sending data toohello same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="a9354-172">Serwery w mapie hello są podzielone przez właściwość cloud_RoleName hello elementów telemetrii.</span><span class="sxs-lookup"><span data-stu-id="a9354-172">Servers in hello map are segmented by hello cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="a9354-173">Ustaw *Mapa aplikacji usługi roli* za*na* z hello tooenable bloku podglądy tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a9354-173">Set *Multi-role Application Map* too*On* from hello Previews blade tooenable this configuration.</span></span>

<span data-ttu-id="a9354-174">Ta metoda może być wskazane w aplikacji micro-services lub w innych sytuacjach, w którym mają być toocorrelate zdarzenia na wielu serwerach w ramach pojedynczego zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a9354-174">This approach may be desired in a micro-services application, or in other scenarios where you want toocorrelate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="a9354-175">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="a9354-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="a9354-176">Opinia</span><span class="sxs-lookup"><span data-stu-id="a9354-176">Feedback</span></span>
<span data-ttu-id="a9354-177">Prześlij opinię za pośrednictwem portalu opinie hello.</span><span class="sxs-lookup"><span data-stu-id="a9354-177">Please provide feedback through hello portal feedback option.</span></span>

![Obraz MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="a9354-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a9354-179">Next steps</span></span>

* [<span data-ttu-id="a9354-180">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a9354-180">Azure portal</span></span>](https://portal.azure.com)
