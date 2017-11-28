---
title: "aaaUsing wyszukiwania w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Wyszukaj i Filtruj nieprzetworzone dane telemetryczne wysyłane przez aplikację sieci web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="ac134-103">Za pomocą wyszukiwania w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="ac134-103">Using Search in Application Insights</span></span>
<span data-ttu-id="ac134-104">Wyszukiwanie jest funkcją [usługi Application Insights](app-insights-overview.md) Użyj toofind i eksplorować dane telemetryczne poszczególnych elementów, takich jak wyświetleń strony, wyjątki lub żądania sieci web.</span><span class="sxs-lookup"><span data-stu-id="ac134-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use toofind and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="ac134-105">I ślady dziennika i zdarzenia, które mają być kodowane można wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="ac134-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="ac134-106">(W przypadku bardziej złożonych kwerend za pośrednictwem danych użyj [Analytics](app-insights-analytics-tour.md).)</span><span class="sxs-lookup"><span data-stu-id="ac134-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="ac134-107">Gdzie możesz zobaczyć wyszukiwania?</span><span class="sxs-lookup"><span data-stu-id="ac134-107">Where do you see Search?</span></span>
### <a name="in-hello-azure-portal"></a><span data-ttu-id="ac134-108">W portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="ac134-108">In hello Azure portal</span></span>
<span data-ttu-id="ac134-109">Diagnostycznych wyszukiwania można otworzyć jawnie za pomocą bloku omówienie Insights aplikacji hello aplikacji:</span><span class="sxs-lookup"><span data-stu-id="ac134-109">You can open diagnostic search explicitly from hello Application Insights Overview blade of your application:</span></span>

![Otwórz wyszukiwanie diagnostycznych](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="ac134-111">Otwiera również po kliknięciu przez niektóre wykresów i elementów siatki.</span><span class="sxs-lookup"><span data-stu-id="ac134-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="ac134-112">W takim przypadku jego filtrów jest wstępnie ustawiony toofocus hello typu wybranego elementu.</span><span class="sxs-lookup"><span data-stu-id="ac134-112">In this case, its filters are pre-set toofocus on hello type of item you selected.</span></span> 

<span data-ttu-id="ac134-113">Na przykład w bloku omówienie hello, brak wykres słupkowy żądań sklasyfikowane przez czas odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ac134-113">For example, on hello Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="ac134-114">Kliknij go, toosee zakresu wydajności listy poszczególnych żądań w tym zakres czasu odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="ac134-114">Click through a performance range toosee a list of individual requests in that response time range:</span></span>

![Kliknij przycisk za pomocą żądania wydajności](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="ac134-116">główną Hello diagnostycznych wyszukiwania jest lista elementów telemetrii - żądań serwera strony widoki, niestandardowych zdarzeń, które mają być zakodowane i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="ac134-116">hello main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="ac134-117">Na powitania u góry listy hello jest podsumowanie wykres przedstawiający liczby zdarzeń w czasie.</span><span class="sxs-lookup"><span data-stu-id="ac134-117">At hello top of hello list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="ac134-118">Kliknij przycisk Odśwież tooget nowych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ac134-118">Click Refresh tooget new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="ac134-119">W programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac134-119">In Visual Studio</span></span>

<span data-ttu-id="ac134-120">W programie Visual Studio jest również okno wyszukiwania usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ac134-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="ac134-121">Jest to najbardziej przydatny w przypadku wyświetlania dane telemetryczne zdarzenia generowane przez aplikacji hello, debugowanej.</span><span class="sxs-lookup"><span data-stu-id="ac134-121">It's most useful for displaying telemetry events generated by hello application that you're debugging.</span></span> <span data-ttu-id="ac134-122">Ale może także wyświetlać hello zdarzenia zebrane z opublikowanych aplikacji w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ac134-122">But it can also show hello events collected from your published app at hello Azure portal.</span></span>

<span data-ttu-id="ac134-123">Otwórz okno wyszukiwania hello w programie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ac134-123">Open hello Search window in Visual Studio:</span></span>

![Visual Studio Otwórz wyszukiwanie usługi Application Insights](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="ac134-125">Okno wyszukiwania Hello ma funkcje podobne toohello sieci web portalu:</span><span class="sxs-lookup"><span data-stu-id="ac134-125">hello Search window has features similar toohello web portal:</span></span>

![Okno wyszukiwania w usłudze Visual Studio Application Insights](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="ac134-127">Hello operacji Śledź karta jest dostępna, po otwarciu żądania lub widok strony.</span><span class="sxs-lookup"><span data-stu-id="ac134-127">hello Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="ac134-128">"Operacji" jest skojarzony z jednym widokiem żądania lub strony tooa sekwencję zdarzeń o.</span><span class="sxs-lookup"><span data-stu-id="ac134-128">An 'operation' is a sequence of events that is associated with tooa single request or page view.</span></span> <span data-ttu-id="ac134-129">Na przykład wywołania zależności, wyjątki dzienników śledzenia i niestandardowych zdarzeń może być częścią jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="ac134-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="ac134-130">Pokazuje kartę śledzenie operacji Hello hello graficznie czas i czas trwania tych zdarzeń w widoku żądania lub strona toohello relacji.</span><span class="sxs-lookup"><span data-stu-id="ac134-130">hello Track Operation tab shows graphically hello timing and duration of these events in relation toohello request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="ac134-131">Przejrzyj poszczególne elementy</span><span class="sxs-lookup"><span data-stu-id="ac134-131">Inspect individual items</span></span>
<span data-ttu-id="ac134-132">Wybierz pola klucza toosee elementu telemetrii i elementy powiązane.</span><span class="sxs-lookup"><span data-stu-id="ac134-132">Select any telemetry item toosee key fields and related items.</span></span> <span data-ttu-id="ac134-133">Jeśli chcesz toosee hello pełny zestaw pól, kliknij przycisk "...".</span><span class="sxs-lookup"><span data-stu-id="ac134-133">If you want toosee hello full set of fields, click "...".</span></span> 

![Kliknij nowy element roboczy, Edytuj pola hello, a następnie kliknij przycisk OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="ac134-135">Typy zdarzeń filtru</span><span class="sxs-lookup"><span data-stu-id="ac134-135">Filter event types</span></span>
<span data-ttu-id="ac134-136">Otwórz hello bloku filtr i wybierz typy zdarzeń hello mają toosee.</span><span class="sxs-lookup"><span data-stu-id="ac134-136">Open hello Filter blade and choose hello event types you want toosee.</span></span> <span data-ttu-id="ac134-137">(Później, jeśli toorestore hello filtry, z którymi został otwarty hello bloku, kliknij Resetuj).</span><span class="sxs-lookup"><span data-stu-id="ac134-137">(If, later, you want toorestore hello filters with which you opened hello blade, click Reset.)</span></span>

![Wybierz filtr, a następnie wybierz typy telemetrii](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="ac134-139">typy zdarzeń Hello są:</span><span class="sxs-lookup"><span data-stu-id="ac134-139">hello event types are:</span></span>

* <span data-ttu-id="ac134-140">**Śledzenia** - [dzienniki diagnostyczne](app-insights-asp-net-trace-logs.md) tym TrackTrace, log4Net, NLog i System.Diagnostic.Trace wywołania.</span><span class="sxs-lookup"><span data-stu-id="ac134-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="ac134-141">**Żądanie** -żądania HTTP odebrane przez aplikacji serwera, w tym stron, skryptów, obrazów, plików w stylu i danych.</span><span class="sxs-lookup"><span data-stu-id="ac134-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="ac134-142">Te zdarzenia są używane toocreate hello żądań i odpowiedzi Omówienie wykresów.</span><span class="sxs-lookup"><span data-stu-id="ac134-142">These events are used toocreate hello request and response overview charts.</span></span>
* <span data-ttu-id="ac134-143">**Widok strony** - [danych Telemetrycznych wysłanych przez klienta sieci web hello](app-insights-javascript.md), używane toocreate strony Wyświetlanie raportów.</span><span class="sxs-lookup"><span data-stu-id="ac134-143">**Page View** - [Telemetry sent by hello web client](app-insights-javascript.md), used toocreate page view reports.</span></span> 
* <span data-ttu-id="ac134-144">**Zdarzenie niestandardowe** — Jeśli w kolejności dodaje zbyt tooTrackEvent() wywołania[monitorowanie użycia](app-insights-api-custom-events-metrics.md), można je znaleźć tutaj.</span><span class="sxs-lookup"><span data-stu-id="ac134-144">**Custom Event** - If you inserted calls tooTrackEvent() in order too[monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="ac134-145">**Wyjątek** — nieprzechwyconych [wyjątków w serwerze hello](app-insights-asp-net-exceptions.md)oraz te, które możesz zalogować się przy użyciu funkcji TrackException().</span><span class="sxs-lookup"><span data-stu-id="ac134-145">**Exception** - Uncaught [exceptions in hello server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="ac134-146">**Zależności** - [wywołania z aplikacji serwera](app-insights-asp-net-dependencies.md) tooother usług takich jak interfejsów API REST lub baz danych i wywołania AJAX z Twojej [kodu klienta](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="ac134-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) tooother services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="ac134-147">**Dostępność** -wyniki [testów dostępności](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="ac134-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="ac134-148">Filtrowanie według wartości właściwości</span><span class="sxs-lookup"><span data-stu-id="ac134-148">Filter on property values</span></span>
<span data-ttu-id="ac134-149">Można filtrować zdarzenia na powitania wartości ich właściwości.</span><span class="sxs-lookup"><span data-stu-id="ac134-149">You can filter events on hello values of their properties.</span></span> <span data-ttu-id="ac134-150">Dostępne właściwości Hello zależą od wybranych typów zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="ac134-150">hello available properties depend on hello event types you selected.</span></span> 

<span data-ttu-id="ac134-151">Na przykład wybierz limit żądań z kodem określoną odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="ac134-151">For example, pick out requests with a specific response code.</span></span> 

![Rozwiń węzeł właściwości i wybierz wartość](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="ac134-153">Wybieranie wartości właściwości określonego ma hello efektu takie same jak wszystkie wartości.</span><span class="sxs-lookup"><span data-stu-id="ac134-153">Choosing no values of a particular property has hello same effect as choosing all values.</span></span> <span data-ttu-id="ac134-154">Przełączenie filtrowanie dla tej właściwości jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="ac134-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="ac134-155">Zawęzić kryteria wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="ac134-155">Narrow your search</span></span>
<span data-ttu-id="ac134-156">Powiadomienie, że hello tej liczby toohello rogu wartości filtru hello pokazują, jak wiele wystąpień są w bieżącym zestawie filtrowane hello.</span><span class="sxs-lookup"><span data-stu-id="ac134-156">Notice that hello counts toohello right of hello filter values show how many occurrences there are in hello current filtered set.</span></span> 

<span data-ttu-id="ac134-157">W tym przykładzie jest wyraźne żądanie "Rpt/pracowników" hello powoduje większość błędów hello "500":</span><span class="sxs-lookup"><span data-stu-id="ac134-157">In this example, it's clear that hello 'Rpt/Employees' request results in most of hello '500' errors:</span></span>

![Rozwiń węzeł właściwości i wybierz wartość](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a><span data-ttu-id="ac134-159">Znajdź zdarzenia z hello tę samą właściwość</span><span class="sxs-lookup"><span data-stu-id="ac134-159">Find events with hello same property</span></span>
<span data-ttu-id="ac134-160">Znajdź wszystkie hello elementy hello takie same wartości właściwości:</span><span class="sxs-lookup"><span data-stu-id="ac134-160">Find all hello items with hello same property value:</span></span>

![Kliknij prawym przyciskiem myszy właściwości](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a><span data-ttu-id="ac134-162">Wyszukiwanie danych hello</span><span class="sxs-lookup"><span data-stu-id="ac134-162">Search hello data</span></span>

> [!NOTE]
> <span data-ttu-id="ac134-163">toowrite bardziej złożonych zapytań, otwórz [ **Analytics** ](app-insights-analytics-tour.md) od góry hello hello wyszukiwania bloku.</span><span class="sxs-lookup"><span data-stu-id="ac134-163">toowrite more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from hello top of hello Search blade.</span></span>
> 

<span data-ttu-id="ac134-164">Możesz wyszukać warunków w dowolnym hello wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="ac134-164">You can search for terms in any of hello property values.</span></span> <span data-ttu-id="ac134-165">Jest to szczególnie przydatne, jeśli w języku [zdarzeń niestandardowych](app-insights-api-custom-events-metrics.md) z wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="ac134-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="ac134-166">Może być tooset zakres czasu, są szybsze jako wyszukiwania w zakresie krótszy.</span><span class="sxs-lookup"><span data-stu-id="ac134-166">You might want tooset a time range, as searches over a shorter range are faster.</span></span> 

![Otwórz wyszukiwanie diagnostycznych](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="ac134-168">Wyszukiwanie słów pełną, nie podciągów.</span><span class="sxs-lookup"><span data-stu-id="ac134-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="ac134-169">Używaj znaków specjalnych tooenclose znaki cudzysłowu.</span><span class="sxs-lookup"><span data-stu-id="ac134-169">Use quotation marks tooenclose special characters.</span></span>

| <span data-ttu-id="ac134-170">Ciąg</span><span class="sxs-lookup"><span data-stu-id="ac134-170">string</span></span> | <span data-ttu-id="ac134-171">jest *nie* został znaleziony przez klasę</span><span class="sxs-lookup"><span data-stu-id="ac134-171">is *not* found by</span></span> | <span data-ttu-id="ac134-172">te znaleźć</span><span class="sxs-lookup"><span data-stu-id="ac134-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ac134-173">HomeController.About</span><span class="sxs-lookup"><span data-stu-id="ac134-173">HomeController.About</span></span> |<span data-ttu-id="ac134-174">Strona główna</span><span class="sxs-lookup"><span data-stu-id="ac134-174">home</span></span><br/><span data-ttu-id="ac134-175">Kontrolera</span><span class="sxs-lookup"><span data-stu-id="ac134-175">controller</span></span><br/><span data-ttu-id="ac134-176">limit</span><span class="sxs-lookup"><span data-stu-id="ac134-176">out</span></span> | <span data-ttu-id="ac134-177">homecontroller</span><span class="sxs-lookup"><span data-stu-id="ac134-177">homecontroller</span></span><br/><span data-ttu-id="ac134-178">— informacje</span><span class="sxs-lookup"><span data-stu-id="ac134-178">about</span></span><br/><span data-ttu-id="ac134-179">"homecontroller.about"</span><span class="sxs-lookup"><span data-stu-id="ac134-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="ac134-180">Stany Zjednoczone</span><span class="sxs-lookup"><span data-stu-id="ac134-180">United States</span></span>|<span data-ttu-id="ac134-181">Sygnalizowanie UNI</span><span class="sxs-lookup"><span data-stu-id="ac134-181">Uni</span></span><br/><span data-ttu-id="ac134-182">obcięta</span><span class="sxs-lookup"><span data-stu-id="ac134-182">ted</span></span>|<span data-ttu-id="ac134-183">Zjednoczone</span><span class="sxs-lookup"><span data-stu-id="ac134-183">united</span></span><br/><span data-ttu-id="ac134-184">Stany</span><span class="sxs-lookup"><span data-stu-id="ac134-184">states</span></span><br/><span data-ttu-id="ac134-185">Stany Zjednoczone i</span><span class="sxs-lookup"><span data-stu-id="ac134-185">united AND states</span></span><br/><span data-ttu-id="ac134-186">"Stanów Zjednoczonych"</span><span class="sxs-lookup"><span data-stu-id="ac134-186">"united states"</span></span>

<span data-ttu-id="ac134-187">Poniżej przedstawiono hello wyrażeniach wyszukiwania, których można użyć:</span><span class="sxs-lookup"><span data-stu-id="ac134-187">Here are hello search expressions you can use:</span></span>

| <span data-ttu-id="ac134-188">Przykładowe zapytanie</span><span class="sxs-lookup"><span data-stu-id="ac134-188">Sample query</span></span> | <span data-ttu-id="ac134-189">Efekt</span><span class="sxs-lookup"><span data-stu-id="ac134-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="ac134-190">Znajdź wszystkie zdarzenia w zakresie czasu hello, których pola zawierają hello word "apple"</span><span class="sxs-lookup"><span data-stu-id="ac134-190">Find all events in hello time range whose fields include hello word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="ac134-191">Znajdź zdarzenia, które zawierają oba słowa.</span><span class="sxs-lookup"><span data-stu-id="ac134-191">Find events that contain both words.</span></span> <span data-ttu-id="ac134-192">Użyj kapitału "i", nie "i".</span><span class="sxs-lookup"><span data-stu-id="ac134-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="ac134-193">Znajdź zdarzenia, które zawierają program Microsoft word.</span><span class="sxs-lookup"><span data-stu-id="ac134-193">Find events that contain either word.</span></span> <span data-ttu-id="ac134-194">Użyj "Lub", nie "lub".</span><span class="sxs-lookup"><span data-stu-id="ac134-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="ac134-195">Krótka forma.</span><span class="sxs-lookup"><span data-stu-id="ac134-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="ac134-196">Znajdź zdarzenia zawierające o jedno słowo, ale nie hello innych.</span><span class="sxs-lookup"><span data-stu-id="ac134-196">Find events that contain one word but not hello other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="ac134-197">Próbkowanie</span><span class="sxs-lookup"><span data-stu-id="ac134-197">Sampling</span></span>
<span data-ttu-id="ac134-198">Jeśli aplikacja generuje wiele telemetrii (i używasz hello 2.0.0-beta3 wersji zestawu SDK platformy ASP.NET lub nowszym), moduł adaptacyjną próbkowania hello automatycznie zmniejsza hello wolumin, który jest wysyłany portalu toohello wysyłając reprezentatywny część zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ac134-198">If your app generates a lot of telemetry (and you are using hello ASP.NET SDK version 2.0.0-beta3 or later), hello adaptive sampling module automatically reduces hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="ac134-199">Jednak zdarzenia będące pokrewne toohello w jednym żądaniu są zaznaczany lub odznaczany jako grupa, dzięki czemu można przechodzić między powiązanych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="ac134-199">However, events that are related toohello same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="ac134-200">[Więcej informacji na temat próbkowania](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="ac134-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="ac134-201">Utwórz element roboczy</span><span class="sxs-lookup"><span data-stu-id="ac134-201">Create work item</span></span>
<span data-ttu-id="ac134-202">Szczegóły hello z dowolnego elementu danych telemetrycznych można utworzyć usterki w witrynie GitHub lub Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="ac134-202">You can create a bug in GitHub or Visual Studio Team Services with hello details from any telemetry item.</span></span> 

![Kliknij nowy element roboczy, Edytuj pola hello, a następnie kliknij przycisk OK.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="ac134-204">Witaj po raz pierwszy to zrobisz, zostanie wyświetlona prośba tooconfigure tooyour łącze usługi Team Services konta i projektu.</span><span class="sxs-lookup"><span data-stu-id="ac134-204">hello first time you do this, you are asked tooconfigure a link tooyour Team Services account and project.</span></span>

![Wypełnienie hello adres URL serwera usługi Team Services i hello nazwę projektu, a następnie kliknij przycisk Autoryzuj](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="ac134-206">(Można również skonfigurować łącze hello w bloku elementów roboczych hello.)</span><span class="sxs-lookup"><span data-stu-id="ac134-206">(You can also configure hello link on hello Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="ac134-207">Zapisz wyszukiwanie</span><span class="sxs-lookup"><span data-stu-id="ac134-207">Save your search</span></span>
<span data-ttu-id="ac134-208">Po ustawieniu wszystkich filtrów hello, który ma hello wyszukiwania można zapisać jako ulubione.</span><span class="sxs-lookup"><span data-stu-id="ac134-208">When you've set all hello filters you want, you can save hello search as a favorite.</span></span> <span data-ttu-id="ac134-209">Jeśli pracujesz w organizacji konta, możesz wybrać czy tooshare go przy użyciu innych członków zespołu.</span><span class="sxs-lookup"><span data-stu-id="ac134-209">If you work in an organizational account, you can choose whether tooshare it with other team members.</span></span>

![Kliknij przycisk Ulubione, hello Nazwa zestawu, a następnie kliknij przycisk Zapisz](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="ac134-211">Wyszukaj hello toosee ponownie, **bloku omówienie Przejdź toohello** , a następnie otwórz Ulubione:</span><span class="sxs-lookup"><span data-stu-id="ac134-211">toosee hello search again, **go toohello overview blade** and open Favorites:</span></span>

![Ulubione kafelka](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="ac134-213">Zapisanie z zakresem względne czasu, ponownie otworzyć bloku hello ma hello najnowsze dane.</span><span class="sxs-lookup"><span data-stu-id="ac134-213">If you saved with Relative time range, hello re-opened blade has hello latest data.</span></span> <span data-ttu-id="ac134-214">Zapisanie z zakresem czasu bezwzględnego, zobacz hello tych samych danych zawsze.</span><span class="sxs-lookup"><span data-stu-id="ac134-214">If you saved with Absolute time range, you see hello same data every time.</span></span> <span data-ttu-id="ac134-215">(Jeśli 'Relative' nie jest dostępna podczas ma toosave element ulubiony, kliknij zakres czasu w nagłówku hello i ustaw zakres czasu nie niestandardowego zakresu.)</span><span class="sxs-lookup"><span data-stu-id="ac134-215">(If 'Relative' isn't available when you want toosave a favorite, click Time Range in hello header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-tooapplication-insights"></a><span data-ttu-id="ac134-216">Wysłać dane telemetryczne więcej szczegółowych informacji tooApplication</span><span class="sxs-lookup"><span data-stu-id="ac134-216">Send more telemetry tooApplication Insights</span></span>
<span data-ttu-id="ac134-217">W dodatku toohello poza pola danych telemetrycznych wysłanych przez zestaw SDK usługi Application Insights można:</span><span class="sxs-lookup"><span data-stu-id="ac134-217">In addition toohello out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="ac134-218">Śledzenie dziennika z Twojego struktury rejestrowania ulubionych w [.NET](app-insights-asp-net-trace-logs.md) lub [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ac134-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="ac134-219">Oznacza to, można przeszukiwać ślady dziennika i skorelowania je z wyświetleń strony, wyjątków i inne zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="ac134-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="ac134-220">[Pisanie kodu](app-insights-api-custom-events-metrics.md) toosend zdarzeń niestandardowych, wyświetleń strony i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="ac134-220">[Write code](app-insights-api-custom-events-metrics.md) toosend custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="ac134-221">[Dowiedz się, jak dzienniki toosend oraz telemetria niestandardowa tooApplication Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ac134-221">[Learn how toosend logs and custom telemetry tooApplication Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="ac134-222"><a name="questions"></a>FUNKCJA PYTANIA I ODPOWIEDZI</span><span class="sxs-lookup"><span data-stu-id="ac134-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="ac134-223"><a name="limits"></a>Jak dużo danych jest zachowywana?</span><span class="sxs-lookup"><span data-stu-id="ac134-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="ac134-224">Zobacz hello [podsumowanie limity](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="ac134-224">See hello [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="ac134-225">Jak wyświetlić dane POST w Moje żądania serwera</span><span class="sxs-lookup"><span data-stu-id="ac134-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="ac134-226">Firma Microsoft hello danych POST nie rejestruj automatycznie, ale może użyć [TrackTrace lub dziennika wywołań](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ac134-226">We don't log hello POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="ac134-227">Umieszczanie danych POST hello w parametrze wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="ac134-227">Put hello POST data in hello message parameter.</span></span> <span data-ttu-id="ac134-228">Nie można filtrować wiadomości powitania w hello sam sposób można filtrować według właściwości, ale limit rozmiaru hello jest dłużej.</span><span class="sxs-lookup"><span data-stu-id="ac134-228">You can't filter on hello message in hello same way you can filter on properties, but hello size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="ac134-229">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="ac134-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="ac134-230"><a name="add"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac134-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="ac134-231">Zapis złożonych zapytań w module analiz</span><span class="sxs-lookup"><span data-stu-id="ac134-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="ac134-232">Wysyłanie dzienników oraz telemetria niestandardowa tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="ac134-232">Send logs and custom telemetry tooApplication Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="ac134-233">Konfigurowanie dostępności i testy czasu odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="ac134-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="ac134-234">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="ac134-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
