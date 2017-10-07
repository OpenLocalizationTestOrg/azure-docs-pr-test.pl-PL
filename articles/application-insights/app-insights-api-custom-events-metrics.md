---
title: "aaaApplication Insights interfejsu API dla niestandardowych zdarzeń i metryk | Dokumentacja firmy Microsoft"
description: "Wstaw kilku wierszy kodu w sposób użycia tootrack urządzenia lub aplikacji komputerowej, strony sieci Web lub usługi i diagnozowanie problemów."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="9b7eb-103">Aplikacji interfejsu API Insights dla niestandardowych zdarzeń i metryk</span><span class="sxs-lookup"><span data-stu-id="9b7eb-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="9b7eb-104">Wstaw kilku wierszy kodu w Twojej aplikacji toofind się, co robią użytkownicy z nim lub toohelp diagnozowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-104">Insert a few lines of code in your application toofind out what users are doing with it, or toohelp diagnose issues.</span></span> <span data-ttu-id="9b7eb-105">Może wysłać dane telemetryczne z aplikacji urządzenia i pulpitu, klientów w sieci web i serwerów sieci web.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="9b7eb-106">Użyj hello [Azure Application Insights](app-insights-overview.md) podstawowe interfejsu API telemetrii toosend niestandardowe zdarzenia i metryki i własnych wersji standard telemetrii.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-106">Use hello [Azure Application Insights](app-insights-overview.md) core telemetry API toosend custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="9b7eb-107">Ten interfejs API jest hello tego samego interfejsu API standardzie hello używanego przez moduły zbierające dane usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-107">This API is hello same API that hello standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="9b7eb-108">Podsumowanie interfejsu API</span><span class="sxs-lookup"><span data-stu-id="9b7eb-108">API summary</span></span>
<span data-ttu-id="9b7eb-109">Witaj interfejsu API jest jednolita na wszystkich platformach, oprócz kilku małe różnice.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-109">hello API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="9b7eb-110">Metoda</span><span class="sxs-lookup"><span data-stu-id="9b7eb-110">Method</span></span> | <span data-ttu-id="9b7eb-111">Używany do</span><span class="sxs-lookup"><span data-stu-id="9b7eb-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="9b7eb-112">Stron, ekrany, bloków lub formularzy.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="9b7eb-113">Akcje użytkownika oraz inne zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-113">User actions and other events.</span></span> <span data-ttu-id="9b7eb-114">Wydajność zachowanie lub toomonitor używane tootrack użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-114">Used tootrack user behavior or toomonitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="9b7eb-115">Wskaźników wydajności, takich jak długości kolejki nie powiązane zdarzenia toospecific.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-115">Performance measurements such as queue lengths not related toospecific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="9b7eb-116">Wyjątki rejestrowania diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="9b7eb-117">Gdzie występują w relacji tooother zdarzeń i przejrzyj śladów stosu śledzenia.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-117">Trace where they occur in relation tooother events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="9b7eb-118">Rejestrowanie hello częstotliwość i czas trwania żądania serwera do analizy wydajności.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-118">Logging hello frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="9b7eb-119">Komunikaty dziennika diagnostycznego.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-119">Diagnostic log messages.</span></span> <span data-ttu-id="9b7eb-120">Istnieje również możliwość przechwytywania dzienniki innych firm.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="9b7eb-121">Czas trwania hello rejestrowania i częstotliwość wywołań tooexternal składników, które zależy od aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-121">Logging hello duration and frequency of calls tooexternal components that your app depends on.</span></span> |

<span data-ttu-id="9b7eb-122">Możesz [dołączanie właściwości i metryki](#properties) toomost tych wywołań telemetrii.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-122">You can [attach properties and metrics](#properties) toomost of these telemetry calls.</span></span>

## <span data-ttu-id="9b7eb-123"><a name="prep"></a>Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="9b7eb-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="9b7eb-124">Jeśli to odwołanie nie ma jeszcze na zestaw SDK usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="9b7eb-125">Dodaj projekt tooyour zestaw SDK usługi Application Insights hello:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-125">Add hello Application Insights SDK tooyour project:</span></span>

  * [<span data-ttu-id="9b7eb-126">Projektu programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9b7eb-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="9b7eb-127">Projekt języka Java</span><span class="sxs-lookup"><span data-stu-id="9b7eb-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="9b7eb-128">Język JavaScript w każdej strony sieci Web</span><span class="sxs-lookup"><span data-stu-id="9b7eb-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="9b7eb-129">W kodzie serwera sieci web lub urządzenia obejmują:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="9b7eb-130">*C#:*`using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="9b7eb-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="9b7eb-131">*Visual Basic:*`Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="9b7eb-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="9b7eb-132">*Java:*`import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="9b7eb-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="9b7eb-133">Utworzenie wystąpienia TelemetryClient</span><span class="sxs-lookup"><span data-stu-id="9b7eb-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="9b7eb-134">Skonstruować wystąpienia `TelemetryClient` (z wyjątkiem w języku JavaScript, na stronach sieci Web):</span><span class="sxs-lookup"><span data-stu-id="9b7eb-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="9b7eb-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="9b7eb-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="9b7eb-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="9b7eb-138">TelemetryClient jest wątkowo.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="9b7eb-139">Zalecane jest użycie wystąpienia TelemetryClient dla każdego modułu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="9b7eb-140">Na przykład może mieć jedno wystąpienie TelemetryClient w Twojej przychodzących żądań HTTP sieci web usługi tooreport i drugą w zdarzeń klasy logiki biznesowej tooreport oprogramowania pośredniczącego.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-140">For instance, you may have one TelemetryClient instance in your web service tooreport incoming HTTP requests, and another in a middleware class tooreport business logic events.</span></span> <span data-ttu-id="9b7eb-141">Można ustawić właściwości, takie jak `TelemetryClient.Context.User.Id` tootrack użytkowników i sesji, lub `TelemetryClient.Context.Device.Id` tooidentify hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-141">You can set properties such as `TelemetryClient.Context.User.Id` tootrack users and sessions, or `TelemetryClient.Context.Device.Id` tooidentify hello machine.</span></span> <span data-ttu-id="9b7eb-142">Te informacje są dołączone tooall zdarzenia, które hello wysyła wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-142">This information is attached tooall events that hello instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="9b7eb-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="9b7eb-143">TrackEvent</span></span>
<span data-ttu-id="9b7eb-144">W usłudze Application Insights *zdarzenie niestandardowe* jest punkt danych, które można wyświetlić w [Eksploratora metryk](app-insights-metrics-explorer.md) jako zagregowanej liczby, a następnie w [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md) jako poszczególnych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="9b7eb-145">(Nie jest powiązane tooMVC lub inne framework "zdarzenia.")</span><span class="sxs-lookup"><span data-stu-id="9b7eb-145">(It isn't related tooMVC or other framework "events.")</span></span>

<span data-ttu-id="9b7eb-146">Wstaw `TrackEvent` Twojego toocount kod odwołuje się różne zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-146">Insert `TrackEvent` calls in your code toocount various events.</span></span> <span data-ttu-id="9b7eb-147">Jak często użytkownicy wybrać określonej funkcji, jak często one celach określonego lub może być częstotliwość tworzenia poszczególnych typów błędów.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="9b7eb-148">Na przykład w aplikacji gry, należy wysłać zdarzenie w przypadku użytkownik wins gry hello:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-148">For example, in a game app, send an event whenever a user wins hello game:</span></span>

<span data-ttu-id="9b7eb-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="9b7eb-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="9b7eb-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="9b7eb-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a><span data-ttu-id="9b7eb-153">Wyświetlanie zdarzeń w portalu Microsoft Azure hello</span><span class="sxs-lookup"><span data-stu-id="9b7eb-153">View your events in hello Microsoft Azure portal</span></span>
<span data-ttu-id="9b7eb-154">toosee liczbę zdarzeń, otwórz [Eksploratora metryk](app-insights-metrics-explorer.md) bloku, Dodaj nowy wykres i wybierz **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-154">toosee a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Liczba zdarzeń niestandardowych w temacie](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="9b7eb-156">toocompare hello liczby różnych zdarzeń, Ustaw typ wykresu hello zbyt**siatki**i grupę o nazwie zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-156">toocompare hello counts of different events, set hello chart type too**Grid**, and group by event name:</span></span>

![Ustaw typ wykresu hello i grupowania](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="9b7eb-158">Na siatce powitania kliknij zdarzenie nazwa toosee poszczególnych wystąpień tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-158">On hello grid, click through an event name toosee individual occurrences of that event.</span></span> <span data-ttu-id="9b7eb-159">toosee bardziej szczegółowe - kliknij każde zdarzenie w hello listy.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-159">toosee more detail - click any occurrence in hello list.</span></span>

![Drążenie wskroś hello zdarzenia](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="9b7eb-161">toofocus na określonych zdarzeń w wyszukiwania lub Eksploratora metryk zestaw hello bloku filtru toohello zdarzeń nazw, które interesują Cię:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-161">toofocus on specific events in either Search or Metrics Explorer, set hello blade's filter toohello event names that you're interested in:</span></span>

![Otwórz filtrów, rozwiń nazwę zdarzenia, a następnie wybierz co najmniej jedną wartość](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="9b7eb-163">Niestandardowe zdarzenia w module analiz</span><span class="sxs-lookup"><span data-stu-id="9b7eb-163">Custom events in Analytics</span></span>

<span data-ttu-id="9b7eb-164">dane telemetryczne Hello jest dostępna w hello `customEvents` tabeli w [Application Insights Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-164">hello telemetry is available in hello `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="9b7eb-165">Każdy wiersz reprezentuje wywołanie za`trackEvent(..)` w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-165">Each row represents a call too`trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="9b7eb-166">Jeśli [próbkowania](app-insights-sampling.md) jest używany w operacji, właściwości wartość elementu itemCount hello wskazuje wartość większą niż 1.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-166">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="9b7eb-167">Na przykład wartość elementu itemCount == 10 oznacza, że z tootrackEvent() 10 wywołania procesu pobierania próbek hello jedynie przesyłane, jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-167">For example itemCount==10 means that of 10 calls tootrackEvent(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="9b7eb-168">tooget poprawne liczba zdarzeń niestandardowych, należy użyć w związku z tym kod wykorzystania, takich jak `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-168">tooget a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="9b7eb-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="9b7eb-169">TrackMetric</span></span>

<span data-ttu-id="9b7eb-170">Usługa Application Insights można wykresu metryk, które nie są dołączone tooparticular zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-170">Application Insights can chart metrics that are not attached tooparticular events.</span></span> <span data-ttu-id="9b7eb-171">Na przykład można monitorować długość kolejki w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="9b7eb-172">O metryki hello pojedynczych pomiarów mogą być przydatne, mniej niż hello zmian i trendów i wykresy tak statystyczne są przydatne.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-172">With metrics, hello individual measurements are of less interest than hello variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="9b7eb-173">Kolejność metryki toosend tooApplication Insights, można użyć hello `TrackMetric(..)` interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-173">In order toosend metrics tooApplication Insights, you can use hello `TrackMetric(..)` API.</span></span> <span data-ttu-id="9b7eb-174">Istnieją dwa sposoby toosend metryki:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-174">There are two ways toosend a metric:</span></span> 

* <span data-ttu-id="9b7eb-175">Pojedyncza wartość.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-175">Single value.</span></span> <span data-ttu-id="9b7eb-176">Za każdym razem, gdy miary są wykonywane w aplikacji, możesz wysłać hello odpowiadającej jej wartości tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-176">Every time you perform a measurement in your application, you send hello corresponding value tooApplication Insights.</span></span> <span data-ttu-id="9b7eb-177">Załóżmy na przykład, że masz metrykę opisujące hello liczba elementów w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-177">For example, assume that you have a metric describing hello number of items in a container.</span></span> <span data-ttu-id="9b7eb-178">W określonym czasie umieść trzy elementy do kontenera hello, a następnie usuń dwa elementy.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-178">During a particular time period, you first put three items into hello container and then you remove two items.</span></span> <span data-ttu-id="9b7eb-179">W związku z tym spowodowałoby wywołanie `TrackMetric` dwa razy: najpierw przekazywanie wartości hello `3` , a następnie hello wartość `-2`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-179">Accordingly, you would call `TrackMetric` twice: first passing hello value `3` and then hello value `-2`.</span></span> <span data-ttu-id="9b7eb-180">Usługa Application Insights przechowuje obie wartości w Twoim imieniu.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="9b7eb-181">Agregacji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-181">Aggregation.</span></span> <span data-ttu-id="9b7eb-182">Podczas pracy z metryki, co pojedynczego pomiaru jest rzadko.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="9b7eb-183">Zamiast tego ważne jest podsumowanie co się stało w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="9b7eb-184">Taki skrót jest nazywany _agregacji_.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="9b7eb-185">W hello powyżej przykładzie, jest hello agregacji sum metryki dla tego okresu `1` i hello liczba wartości metryki hello jest `2`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-185">In hello above example, hello aggregate metric sum for that time period is `1` and hello count of hello metric values is `2`.</span></span> <span data-ttu-id="9b7eb-186">Korzystając z metody agregacji hello, można tylko wywołać `TrackMetric` raz w czasie okresu i wysyłania hello wartości zagregowanych.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-186">When using hello aggregation approach, you only invoke `TrackMetric` once per time period and send hello aggregate values.</span></span> <span data-ttu-id="9b7eb-187">Jest to hello zalecane podejście, ponieważ mogą znacznie zmniejszyć koszt hello i wydajności nakładów pracy, wysyłając mniej danych punktów tooApplication Insights podczas nadal zbierania wszystkich odpowiednich informacji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-187">This is hello recommended approach since it can significantly reduce hello cost and performance overhead by sending fewer data points tooApplication Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="9b7eb-188">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="9b7eb-189">Pojedynczych wartości</span><span class="sxs-lookup"><span data-stu-id="9b7eb-189">Single values</span></span>

<span data-ttu-id="9b7eb-190">toosend pojedynczą wartość metryki:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-190">toosend a single metric value:</span></span>

<span data-ttu-id="9b7eb-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="9b7eb-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="9b7eb-193">Agregowanie metryk</span><span class="sxs-lookup"><span data-stu-id="9b7eb-193">Aggregating metrics</span></span>

<span data-ttu-id="9b7eb-194">Przed wysłaniem do nich z aplikację, tooreduce przepustowości, kosztów i tooimprove wydajności zalecane jest tooaggregate metryki.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-194">It is recommended tooaggregate metrics before sending them from your app, tooreduce bandwidth, cost and tooimprove performance.</span></span>
<span data-ttu-id="9b7eb-195">Oto przykład agregację kodu:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="9b7eb-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-196">*C#*</span></span>

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="9b7eb-197">Metryki niestandardowe w Eksploratorze metryk</span><span class="sxs-lookup"><span data-stu-id="9b7eb-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="9b7eb-198">wyniki hello toosee, otwórz Eksploratora metryk i Dodaj nowy wykres.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-198">toosee hello results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="9b7eb-199">Edytuj hello wykresu tooshow Twojego metryki.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-199">Edit hello chart tooshow your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="9b7eb-200">Twoje niestandardowa Metryka może potrwać kilka minut tooappear hello liście dostępne metryki.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-200">Your custom metric might take several minutes tooappear in hello list of available metrics.</span></span>
>

![Dodawanie nowego wykresu lub wybierz wykres, a w obszarze niestandardowe, wybierz Twoje metryki](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="9b7eb-202">Metryki niestandardowe w module analiz</span><span class="sxs-lookup"><span data-stu-id="9b7eb-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="9b7eb-203">dane telemetryczne Hello jest dostępna w hello `customMetrics` tabeli w [Application Insights Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-203">hello telemetry is available in hello `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="9b7eb-204">Każdy wiersz reprezentuje wywołanie za`trackMetric(..)` w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-204">Each row represents a call too`trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="9b7eb-205">`valueSum`-Jest suma hello hello pomiarów.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-205">`valueSum` - This is hello sum of hello measurements.</span></span> <span data-ttu-id="9b7eb-206">tooget wartości średniej hello, dzielenie przez `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-206">tooget hello mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="9b7eb-207">`valueCount`-hello liczba pomiarów, które zostały zagregowane w to `trackMetric(..)` wywołania.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-207">`valueCount` - hello number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="9b7eb-208">Liczba wyświetleń strony</span><span class="sxs-lookup"><span data-stu-id="9b7eb-208">Page views</span></span>
<span data-ttu-id="9b7eb-209">W aplikacji lub strony sieci Web urządzenia po załadowaniu każdej ekranu lub strony, domyślnie jest wysyłane dane telemetryczne wyświetleń strony.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="9b7eb-210">Ale można zmienić tego tootrack wyświetleń strony w czasie dodatkowych lub innych.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-210">But you can change that tootrack page views at additional or different times.</span></span> <span data-ttu-id="9b7eb-211">Na przykład w aplikacji, która zawiera tabulatory lub bloków, można tootrack strony zawsze, gdy użytkownik hello otwiera nowy blok.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-211">For example, in an app that displays tabs or blades, you might want tootrack a page whenever hello user opens a new blade.</span></span>

![Obiektyw użycia w bloku — omówienie](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="9b7eb-213">Dane użytkownika i sesji są wysyłane jako właściwości wraz z wyświetleń strony, dlatego hello użytkownika i sesji wykresy pochodzić aktywności, po dane telemetryczne wyświetleń strony.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-213">User and session data is sent as properties along with page views, so hello user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="9b7eb-214">Widoki niestandardowe strony</span><span class="sxs-lookup"><span data-stu-id="9b7eb-214">Custom page views</span></span>
<span data-ttu-id="9b7eb-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="9b7eb-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="9b7eb-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="9b7eb-218">Jeśli masz kilka kart w różnych stron HTML, można określić hello adresu URL za:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-218">If you have several tabs within different HTML pages, you can specify hello URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="9b7eb-219">Liczba wyświetleń strony chronometrażu</span><span class="sxs-lookup"><span data-stu-id="9b7eb-219">Timing page views</span></span>
<span data-ttu-id="9b7eb-220">Domyślnie razy hello raportowane klientowi jako **czas ładowania strony widoku** są mierzone od, gdy przeglądarka hello wysyła żądanie hello, dopóki zdarzeń ładowania strony przeglądarki hello jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-220">By default, hello times reported as **Page view load time** are measured from when hello browser sends hello request, until hello browser's page load event is called.</span></span>

<span data-ttu-id="9b7eb-221">Zamiast tego możesz:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-221">Instead, you can either:</span></span>

* <span data-ttu-id="9b7eb-222">Ustaw jawne czasu trwania w hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) wywołania: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-222">Set an explicit duration in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="9b7eb-223">Użyj wywołań chronometrażu widoku strony hello `startTrackPage` i `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-223">Use hello page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="9b7eb-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-224">*JavaScript*</span></span>

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="9b7eb-225">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="9b7eb-225">...</span></span>

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="9b7eb-226">Witaj nazwy używanej jako pierwszy parametr hello kojarzy hello start i Zatrzymaj wywołania.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-226">hello name that you use as hello first parameter associates hello start and stop calls.</span></span> <span data-ttu-id="9b7eb-227">Domyślnie nazwa toohello bieżącej strony.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-227">It defaults toohello current page name.</span></span>

<span data-ttu-id="9b7eb-228">Hello wynikowy ładowania strony okresów wyświetlana w Eksploratorze metryk pochodzą od interwału powitania między hello uruchamianie i zatrzymywanie wywołania.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-228">hello resulting page load durations displayed in Metrics Explorer are derived from hello interval between hello start and stop calls.</span></span> <span data-ttu-id="9b7eb-229">Jest zapasowej tooyou jakie interwał czasu rzeczywistego.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-229">It's up tooyou what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="9b7eb-230">Dane telemetryczne strony w module analiz</span><span class="sxs-lookup"><span data-stu-id="9b7eb-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="9b7eb-231">W [Analytics](app-insights-analytics.md) dwóch tabel wyświetlane dane z operacji przeglądarki:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="9b7eb-232">Witaj `pageViews` tabela zawiera dane o hello adresu URL i tytuł strony</span><span class="sxs-lookup"><span data-stu-id="9b7eb-232">hello `pageViews` table contains data about hello URL and page title</span></span>
* <span data-ttu-id="9b7eb-233">Witaj `browserTimings` tabeli zawiera dane dotyczące wydajności klienta, takich jak tooprocess czas poświęcony na powitania hello przychodzących danych.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-233">hello `browserTimings` table contains data about client performance, such as hello time taken tooprocess hello incoming data</span></span>

<span data-ttu-id="9b7eb-234">toofind jak długo przeglądarki hello przyjmuje tooprocess różne strony:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-234">toofind how long hello browser takes tooprocess different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="9b7eb-235">popularities hello toodiscover różnych przeglądarek:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-235">toodiscover hello popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="9b7eb-236">Dołącz tooassociate strony widoki tooAJAX wywołania zależności:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-236">tooassociate page views tooAJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="9b7eb-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="9b7eb-237">TrackRequest</span></span>
<span data-ttu-id="9b7eb-238">Serwer Hello SDK używa TrackRequest toolog HTTP żądania.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-238">hello server SDK uses TrackRequest toolog HTTP requests.</span></span>

<span data-ttu-id="9b7eb-239">Możesz można także wywołać ją samodzielnie Chcąc toosimulate żądania w kontekście gdzie nie ma uruchomiony moduł usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-239">You can also call it yourself if you want toosimulate requests in a context where you don't have hello web service module running.</span></span>

<span data-ttu-id="9b7eb-240">Jednak zalecane jest dane telemetryczne żądania toosend sposób gdzie żądania hello działa jako hello <a href="#operation-context">kontekstu operacji</a>.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-240">However, hello recommended way toosend request telemetry is where hello request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="9b7eb-241">Operacja kontekstu</span><span class="sxs-lookup"><span data-stu-id="9b7eb-241">Operation context</span></span>
<span data-ttu-id="9b7eb-242">Elementy danych telemetrycznych można skojarzyć razem dołączając toothem identyfikatora typowych operacji</span><span class="sxs-lookup"><span data-stu-id="9b7eb-242">You can associate telemetry items together by attaching toothem a common operation ID.</span></span> <span data-ttu-id="9b7eb-243">Standardowy moduł żądania śledzenia Hello robi to wyjątków i inne zdarzenia, które są wysyłane podczas przetwarzania żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-243">hello standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="9b7eb-244">W [wyszukiwania](app-insights-diagnostic-search.md) i [Analytics](app-insights-analytics.md), można użyć hello identyfikator tooeasily Znajdź wszystkie zdarzenia związane z hello żądania.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use hello ID tooeasily find any events associated with hello request.</span></span>

<span data-ttu-id="9b7eb-245">Identyfikator hello tooset Najprostszym sposobem Hello jest tooset kontekstu operacji za pomocą tego wzorca:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-245">hello easiest way tooset hello ID is tooset an operation context by using this pattern:</span></span>

<span data-ttu-id="9b7eb-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="9b7eb-247">Wraz z ustawienie kontekstu operacji `StartOperation` tworzy element telemetrii hello typu, który określisz.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-247">Along with setting an operation context, `StartOperation` creates a telemetry item of hello type that you specify.</span></span> <span data-ttu-id="9b7eb-248">Element wysyła dane telemetryczne hello podczas usuwania operacji hello lub jawnie wywołać `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-248">It sends hello telemetry item when you dispose hello operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="9b7eb-249">Jeśli używasz `RequestTelemetry` jako typ danych telemetrycznych hello, jego długość ustawiono interwał toohello upłynął czasu rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-249">If you use `RequestTelemetry` as hello telemetry type, its duration is set toohello timed interval between start and stop.</span></span>

<span data-ttu-id="9b7eb-250">Nie można zagnieżdżać kontekstów operacji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="9b7eb-251">Jeśli istnieje już kontekstu operacji, a następnie jego identyfikator jest skojarzony z wszystkie elementy zawarte hello, w tym utworzone za pomocą elementu hello `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-251">If there is already an operation context, then its ID is associated with all hello contained items, including hello item created with `StartOperation`.</span></span>

<span data-ttu-id="9b7eb-252">W polu Wyszukaj hello operacji kontekst jest używane toocreate hello **elementy pokrewne** listy:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-252">In Search, hello operation context is used toocreate hello **Related Items** list:</span></span>

![Elementy pokrewne](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="9b7eb-254">Zobacz [aplikacji — szczegółowe informacje — niestandardowy operacji tracking.md] uzyskać więcej informacji o niestandardowych operacji śledzenia.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="9b7eb-255">Żądań w module analiz</span><span class="sxs-lookup"><span data-stu-id="9b7eb-255">Requests in Analytics</span></span> 

<span data-ttu-id="9b7eb-256">W [Application Insights Analytics](app-insights-analytics.md), żądań Pokaż w górę w hello `requests` tabeli.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in hello `requests` table.</span></span>

<span data-ttu-id="9b7eb-257">Jeśli [próbkowania](app-insights-sampling.md) jest w operacji właściwości wartość elementu itemCount hello wyświetli wartość większą niż 1.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-257">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="9b7eb-258">Na przykład wartość elementu itemCount == 10 oznacza, że z tootrackRequest() 10 wywołania procesu pobierania próbek hello jedynie przesyłane, jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-258">For example itemCount==10 means that of 10 calls tootrackRequest(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="9b7eb-259">tooget poprawną liczbę żądań i Średni czas trwania segmentowanych przez żądanie nazwy, takie jak użyć kodu:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-259">tooget a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="9b7eb-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="9b7eb-260">TrackException</span></span>
<span data-ttu-id="9b7eb-261">Wyślij wyjątki tooApplication Insights:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-261">Send exceptions tooApplication Insights:</span></span>

* <span data-ttu-id="9b7eb-262">zbyt[policzyć](app-insights-metrics-explorer.md), jako informacje o częstotliwości hello problemu.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-262">too[count them](app-insights-metrics-explorer.md), as an indication of hello frequency of a problem.</span></span>
* <span data-ttu-id="9b7eb-263">zbyt[Sprawdź indywidualne wystąpienia](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-263">too[examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="9b7eb-264">Witaj raporty zawierają hello śladów stosu.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-264">hello reports include hello stack traces.</span></span>

<span data-ttu-id="9b7eb-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="9b7eb-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="9b7eb-267">zestawy SDK Hello catch wiele wyjątków automatycznie, więc nie zawsze są toocall TrackException jawnie.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-267">hello SDKs catch many exceptions automatically, so you don't always have toocall TrackException explicitly.</span></span>

* <span data-ttu-id="9b7eb-268">ASP.NET: [napisać kod wyjątki toocatch](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-268">ASP.NET: [Write code toocatch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="9b7eb-269">J2EE: [wyjątki są przechwytywane automatycznie](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="9b7eb-270">JavaScript: Wyjątki są przechwytywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="9b7eb-271">Automatyczne zbieranie toodisable, dodać fragment kodu toohello wiersza wstawiany strony sieci Web:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-271">If you want toodisable automatic collection, add a line toohello code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="9b7eb-272">Wyjątki w module analiz</span><span class="sxs-lookup"><span data-stu-id="9b7eb-272">Exceptions in Analytics</span></span>

<span data-ttu-id="9b7eb-273">W [Application Insights Analytics](app-insights-analytics.md), wyjątki widoczne w hello `exceptions` tabeli.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in hello `exceptions` table.</span></span>

<span data-ttu-id="9b7eb-274">Jeśli [próbkowania](app-insights-sampling.md) jest używany w operacji, hello `itemCount` właściwość wskazuje wartość większą niż 1.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-274">If [sampling](app-insights-sampling.md) is in operation, hello `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="9b7eb-275">Na przykład wartość elementu itemCount == 10 oznacza, że z tootrackException() 10 wywołania procesu pobierania próbek hello jedynie przesyłane, jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-275">For example itemCount==10 means that of 10 calls tootrackException(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="9b7eb-276">tooget poprawne liczba wyjątków segmentowanych przez typ wyjątku, takie jak użyć kodu:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-276">tooget a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="9b7eb-277">Większość hello ważne informacje stosu już jest wyodrębniany do oddzielnych zmiennych, ale można ściągnąć powitania od siebie `details` struktury tooget więcej.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-277">Most of hello important stack information is already extracted into separate variables, but you can pull apart hello `details` structure tooget more.</span></span> <span data-ttu-id="9b7eb-278">Ponieważ ta struktura jest dynamiczny, należy rzutować hello wynik toohello typu oczekiwane.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-278">Since this structure is dynamic, you should cast hello result toohello type you expect.</span></span> <span data-ttu-id="9b7eb-279">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="9b7eb-280">Wyjątki tooassociate z ich powiązanego żądania użyć sprzężenia:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-280">tooassociate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="9b7eb-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="9b7eb-281">TrackTrace</span></span>
<span data-ttu-id="9b7eb-282">Użyj TrackTrace toohelp diagnozować problemy, wysyłając tooApplication "nawigacją dziennik" szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-282">Use TrackTrace toohelp diagnose problems by sending a "breadcrumb trail" tooApplication Insights.</span></span> <span data-ttu-id="9b7eb-283">Umożliwia wysyłanie fragmentów danych diagnostycznych i sprawdzać ich w [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="9b7eb-284">[Zaloguj się kart](app-insights-asp-net-trace-logs.md) za pomocą tego portalu toohello interfejsu API toosend dzienniki innych firm.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API toosend third-party logs toohello portal.</span></span>

<span data-ttu-id="9b7eb-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="9b7eb-286">Można wyszukiwać w treści wiadomości, ale (w przeciwieństwie do wartości właściwości) nie można filtrować na nim.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="9b7eb-287">limit rozmiaru Hello na `message` jest znacznie wyższa niż limit hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-287">hello size limit on `message` is much higher than hello limit on properties.</span></span>
<span data-ttu-id="9b7eb-288">Zaletą TrackTrace jest umieszczenie stosunkowo długo dane wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-288">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="9b7eb-289">Na przykład można zakodować danych POST.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="9b7eb-290">Ponadto możesz dodać komunikat tooyour poziomu ważności.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-290">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="9b7eb-291">I, podobnie jak inne dane telemetryczne, możesz dodać toohelp wartości właściwości, które można filtrować lub wyszukiwania dla różnych zestawów danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-291">And, like other telemetry, you can add property values toohelp you filter or search for different sets of traces.</span></span> <span data-ttu-id="9b7eb-292">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="9b7eb-293">W [wyszukiwania](app-insights-diagnostic-search.md), następnie można łatwo filtrować wszystkie wiadomości powitania poziomu ważności określonego związane tooa określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all hello messages of a particular severity level that relate tooa particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="9b7eb-294">Dane śledzenia w analityka</span><span class="sxs-lookup"><span data-stu-id="9b7eb-294">Traces in Analytics</span></span>

<span data-ttu-id="9b7eb-295">W [Application Insights Analytics](app-insights-analytics.md), odwołuje Pokaż tooTrackTrace hello `traces` tabeli.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-295">In [Application Insights Analytics](app-insights-analytics.md), calls tooTrackTrace show up in hello `traces` table.</span></span>

<span data-ttu-id="9b7eb-296">Jeśli [próbkowania](app-insights-sampling.md) jest używany w operacji, właściwości wartość elementu itemCount hello wskazuje wartość większą niż 1.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-296">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="9b7eb-297">Na przykład wartość elementu itemCount == 10 oznacza, że 10 wymaga zbyt`trackTrace()`, proces pobierania próbek hello przesyłane tylko jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-297">For example itemCount==10 means that of 10 calls too`trackTrace()`, hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="9b7eb-298">tooget poprawną liczbę wywołań śledzenia, należy używać w związku z tym kod takich jak `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-298">tooget a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="9b7eb-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="9b7eb-299">TrackDependency</span></span>
<span data-ttu-id="9b7eb-300">Użyj hello TrackDependency wywołać czas reakcji hello tootrack i odsetka pomyślnych wywołań zewnętrznego fragmentu tooan kodu.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-300">Use hello TrackDependency call tootrack hello response times and success rates of calls tooan external piece of code.</span></span> <span data-ttu-id="9b7eb-301">Witaj wyniki są wyświetlane na wykresach zależności hello w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-301">hello results appear in hello dependency charts in hello portal.</span></span>

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

<span data-ttu-id="9b7eb-302">Pamiętaj serwera hello zawierają zestawy SDK [modułu zależności](app-insights-asp-net-dependencies.md) która wykrywa i śledzi pewne wywołania zależności automatycznie — na przykład toodatabases i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-302">Remember that hello server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, toodatabases and REST APIs.</span></span> <span data-ttu-id="9b7eb-303">Masz tooinstall agenta w module hello toomake serwer działa.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-303">You have tooinstall an agent on your server toomake hello module work.</span></span> <span data-ttu-id="9b7eb-304">Używasz to wywołanie nie przechwytuje wywołań tootrack hello automatycznego śledzenia, lub jeśli nie chcesz tooinstall hello agenta.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-304">You use this call if you want tootrack calls that hello automated tracking doesn't catch, or if you don't want tooinstall hello agent.</span></span>

<span data-ttu-id="9b7eb-305">Edytuj tooturn poza hello standardowy moduł śledzenia zależności, [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) i Usuń odwołanie hello zbyt`DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-305">tooturn off hello standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete hello reference too`DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="9b7eb-306">Zależności w module analiz</span><span class="sxs-lookup"><span data-stu-id="9b7eb-306">Dependencies in Analytics</span></span>

<span data-ttu-id="9b7eb-307">W [Application Insights Analytics](app-insights-analytics.md), wywołania trackDependency widoczne w hello `dependencies` tabeli.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in hello `dependencies` table.</span></span>

<span data-ttu-id="9b7eb-308">Jeśli [próbkowania](app-insights-sampling.md) jest używany w operacji, właściwości wartość elementu itemCount hello wskazuje wartość większą niż 1.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-308">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="9b7eb-309">Na przykład wartość elementu itemCount == 10 oznacza, że z tootrackDependency() 10 wywołania procesu pobierania próbek hello jedynie przesyłane, jeden z nich.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-309">For example itemCount==10 means that of 10 calls tootrackDependency(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="9b7eb-310">tooget poprawną liczbę zależności segmentowanych przez składnik docelowy, takich jak użyć kodu:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-310">tooget a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="9b7eb-311">zależności tooassociate z ich żądań powiązane, należy użyć sprzężenia:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-311">tooassociate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="9b7eb-312">Opróżnienie danych</span><span class="sxs-lookup"><span data-stu-id="9b7eb-312">Flushing data</span></span>
<span data-ttu-id="9b7eb-313">Zwykle hello SDK wysyła dane w czasie wybrany toominimize hello wpływ na powitania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-313">Normally, hello SDK sends data at times chosen toominimize hello impact on hello user.</span></span> <span data-ttu-id="9b7eb-314">Jednak w niektórych przypadkach można buforu hello tooflush — na przykład, jeśli używasz hello zestawu SDK w aplikacji, która kończy pracę.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-314">However, in some cases, you might want tooflush hello buffer--for example, if you are using hello SDK in an application that shuts down.</span></span>

<span data-ttu-id="9b7eb-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="9b7eb-316">Należy pamiętać, że funkcja hello asynchronicznego dla hello [kanału dane telemetryczne serwera](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-316">Note that hello function is asynchronous for hello [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="9b7eb-317">Użytkownicy uwierzytelnieni</span><span class="sxs-lookup"><span data-stu-id="9b7eb-317">Authenticated users</span></span>
<span data-ttu-id="9b7eb-318">W aplikacji sieci web użytkownicy są (domyślnie) identyfikowani na podstawie plików cookie.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="9b7eb-319">Użytkownik może być traktowane więcej niż raz, jeśli uzyskują oni dostęp do aplikacji z innego komputera lub przeglądarki lub one usunąć pliki cookie.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="9b7eb-320">Jeśli aplikacja tooyour logowania użytkownika, można uzyskać dokładniejsze liczba przez ustawienie Identyfikatora użytkownika hello uwierzytelniony w kodzie przeglądarki hello:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-320">If users sign in tooyour app, you can get a more accurate count by setting hello authenticated user ID in hello browser code:</span></span>

<span data-ttu-id="9b7eb-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-321">*JavaScript*</span></span>

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="9b7eb-322">W sieci web platformy ASP.NET MVC aplikacji, na przykład:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="9b7eb-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="9b7eb-324">Nie jest konieczne toouse hello użytkownika rzeczywistej nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-324">It isn't necessary toouse hello user's actual sign-in name.</span></span> <span data-ttu-id="9b7eb-325">Ma tylko toobe identyfikator unikatowy toothat użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-325">It only has toobe an ID that is unique toothat user.</span></span> <span data-ttu-id="9b7eb-326">Nie może zawierać spacji ani żadnego ze znaków hello `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-326">It must not include spaces or any of hello characters `,;=|`.</span></span>

<span data-ttu-id="9b7eb-327">Identyfikator użytkownika Hello jest również ustawiona w pliku cookie sesji i wysyłane toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-327">hello user ID is also set in a session cookie and sent toohello server.</span></span> <span data-ttu-id="9b7eb-328">Po zainstalowaniu serwera hello SDK hello uwierzytelnić użytkownika, którego identyfikator jest wysyłany jako część właściwości kontekstu powitania klienta i serwera telemetrii.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-328">If hello server SDK is installed, hello authenticated user ID is sent as part of hello context properties of both client and server telemetry.</span></span> <span data-ttu-id="9b7eb-329">Następnie można filtrować i wyszukaj w nim.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-329">You can then filter and search on it.</span></span>

<span data-ttu-id="9b7eb-330">Aplikacji do konta grupy, użytkownicy, można również przesłać identyfikator konta hello (z hello sam znak ograniczenia).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-330">If your app groups users into accounts, you can also pass an identifier for hello account (with hello same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="9b7eb-331">W [Eksploratora metryk](app-insights-metrics-explorer.md), można utworzyć wykres obliczającej **uwierzytelnieni użytkownicy,**, i **kont użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="9b7eb-332">Możesz również [wyszukiwania](app-insights-diagnostic-search.md) dla punktów danych klienta z nazwami użytkowników i kont.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="9b7eb-333"><a name="properties"></a>Filtrowanie, wyszukiwanie i podzielenie danych za pomocą właściwości</span><span class="sxs-lookup"><span data-stu-id="9b7eb-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="9b7eb-334">Możesz dołączyć właściwości i pomiarów tooyour zdarzenia (i również toometrics wyświetleń strony, wyjątków i innych danych telemetrycznych).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-334">You can attach properties and measurements tooyour events (and also toometrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="9b7eb-335">*Właściwości* są wartości ciągu, której można toofilter telemetrii w raportach użycia hello.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-335">*Properties* are string values that you can use toofilter your telemetry in hello usage reports.</span></span> <span data-ttu-id="9b7eb-336">Na przykład jeśli aplikacja udostępnia kilka gier, możesz dołączyć nazwę hello hello gier tooeach zdarzenia tak aby były widoczne, które gry są bardziej popularne.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-336">For example, if your app provides several games, you can attach hello name of hello game tooeach event so that you can see which games are more popular.</span></span>

<span data-ttu-id="9b7eb-337">Ma limitu 8192 na powitania długość ciągu.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-337">There's a limit of 8192 on hello string length.</span></span> <span data-ttu-id="9b7eb-338">(Toosend duże zestawy danych, należy użyć parametru wiadomość hello [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="9b7eb-338">(If you want toosend large chunks of data, use hello message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="9b7eb-339">*Metryki* są wartości liczbowe, które mogą być prezentowane w postaci graficznej.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="9b7eb-340">Na przykład można toosee przypadku stopniowego zwiększenia hello wyniki, które osiągnięcia Twojej graczy.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-340">For example, you might want toosee if there's a gradual increase in hello scores that your gamers achieve.</span></span> <span data-ttu-id="9b7eb-341">Wykresy Hello można segmentowanych przez powitalne oddzielnych właściwości, które są wysyłane z zdarzeń hello, dzięki czemu można uzyskać lub skumulowany wykresy dotyczące różnych gier.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-341">hello graphs can be segmented by hello properties that are sent with hello event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="9b7eb-342">Wartości metryki toobe prawidłowo wyświetlany powinny one być większy lub równy too0.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-342">For metric values toobe correctly displayed, they should be greater than or equal too0.</span></span>

<span data-ttu-id="9b7eb-343">Brak niektórych [limity liczby hello właściwości, wartości właściwości i metryki](#limits) pomocne.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-343">There are some [limits on hello number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="9b7eb-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-344">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="9b7eb-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="9b7eb-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="9b7eb-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="9b7eb-348">Zajmie się toolog dane osobowe lub informacje we właściwościach.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-348">Take care not toolog personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="9b7eb-349">*Jeśli używasz metryki*, otwórz Eksploratora metryk i wybierz metrykę hello z hello **niestandardowy** grupy:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-349">*If you used metrics*, open Metrics Explorer and select hello metric from hello **Custom** group:</span></span>

![Otwórz Eksploratora metryk, wybierz hello wykresu i wybierz metrykę hello](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="9b7eb-351">Jeśli nie zostanie wyświetlone Twoje metryki lub hello **niestandardowy** pozycji nie ma, zamknij hello wybór bloku i spróbuj ponownie później.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-351">If your metric doesn't appear, or if hello **Custom** heading isn't there, close hello selection blade and try again later.</span></span> <span data-ttu-id="9b7eb-352">Metryki czasami może zająć godzinę toobe agregowana przez potok hello.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-352">Metrics can sometimes take an hour toobe aggregated through hello pipeline.</span></span>

<span data-ttu-id="9b7eb-353">*Jeśli używasz właściwości i metryki*, podzielić Metryka hello przez właściwość hello:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-353">*If you used properties and metrics*, segment hello metric by hello property:</span></span>

![Ustaw grupowanie, a następnie wybierz właściwość hello Grupuj według](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="9b7eb-355">*W wyszukiwaniu diagnostycznych*, można wyświetlić właściwości hello i metryki poszczególnych wystąpień tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-355">*In Diagnostic Search*, you can view hello properties and metrics of individual occurrences of an event.</span></span>

![Wybierz wystąpienie, a następnie wybierz pozycję "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="9b7eb-357">Użyj hello **wyszukiwania** pola toosee wystąpienia zdarzenia, które mają określoną wartość właściwości.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-357">Use hello **Search** field toosee event occurrences that have a particular property value.</span></span>

![Wpisz termin do wyszukiwania](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="9b7eb-359">[Dowiedz się więcej o wyrażeniach wyszukiwania](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-tooset-properties-and-metrics"></a><span data-ttu-id="9b7eb-360">Alternatywna metoda tooset właściwości i metryki</span><span class="sxs-lookup"><span data-stu-id="9b7eb-360">Alternative way tooset properties and metrics</span></span>
<span data-ttu-id="9b7eb-361">Jeśli jest to bardziej wygodne, można zebrać parametry hello zdarzenia w oddzielnych obiektów:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-361">If it's more convenient, you can collect hello parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="9b7eb-362">Nie należy używać ponownie hello tego samego wystąpienia elementu telemetrii (`event` w tym przykładzie) toocall Track*() wiele razy.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-362">Don't reuse hello same telemetry item instance (`event` in this example) toocall Track*() multiple times.</span></span> <span data-ttu-id="9b7eb-363">Może to spowodować toobe danych telemetrycznych wysłanych z nieprawidłowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-363">This may cause telemetry toobe sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="9b7eb-364">Niestandardowe pomiarów i właściwości w module analiz</span><span class="sxs-lookup"><span data-stu-id="9b7eb-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="9b7eb-365">W [Analytics](app-insights-analytics.md), właściwości i metryki niestandardowe Pokaż w hello `customMeasurements` i `customDimensions` atrybuty każdego rekordu telemetrii.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in hello `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="9b7eb-366">Na przykład po dodaniu właściwość o nazwie "gier" tooyour dane telemetryczne żądania to zapytanie liczby wystąpień różne wartości "gry" hello i Pokaż średnią hello hello metryki niestandardowe "wynik":</span><span class="sxs-lookup"><span data-stu-id="9b7eb-366">For example, if you have added a property named "game" tooyour request telemetry, this query counts hello occurrences of different values of "game", and show hello average of hello custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="9b7eb-367">Zwróć uwagę, że:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-367">Notice that:</span></span>

* <span data-ttu-id="9b7eb-368">Podczas wyodrębniania wartości z hello customDimensions lub customMeasurements JSON, ma typ dynamiczne i dlatego należy rzutować go `tostring` lub `todouble`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-368">When you extract a value from hello customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="9b7eb-369">Konto tootake możliwości hello [próbkowania](app-insights-sampling.md), należy użyć `sum(itemCount)`, a nie `count()`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-369">tootake account of hello possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="9b7eb-370"><a name="timed"></a>Zdarzenia czasowe</span><span class="sxs-lookup"><span data-stu-id="9b7eb-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="9b7eb-371">Czasami ma toochart, jak długo trwa tooperform akcji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-371">Sometimes you want toochart how long it takes tooperform an action.</span></span> <span data-ttu-id="9b7eb-372">Na przykład może być tooknow jak długo użytkowników zająć tooconsider wyborów w grę.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-372">For example, you might want tooknow how long users take tooconsider choices in a game.</span></span> <span data-ttu-id="9b7eb-373">Można użyć parametru pomiaru hello tego.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-373">You can use hello measurement parameter for this.</span></span>

<span data-ttu-id="9b7eb-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="9b7eb-375"><a name="defaults"></a>Właściwości domyślne telemetria niestandardowa</span><span class="sxs-lookup"><span data-stu-id="9b7eb-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="9b7eb-376">Jeśli chcesz tooset domyślne wartości właściwości dla niektórych hello zdarzeń niestandardowych, które należy zapisać można ustawić je w wystąpieniu TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-376">If you want tooset default property values for some of hello custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="9b7eb-377">Są one dołączone tooevery telemetrii elementu, który został wysłany przez klienta.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-377">They are attached tooevery telemetry item that's sent from that client.</span></span>

<span data-ttu-id="9b7eb-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="9b7eb-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="9b7eb-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="9b7eb-381">Wywołania poszczególnych danych telemetrycznych można zastąpić wartości domyślne hello w słownikach ich właściwości.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-381">Individual telemetry calls can override hello default values in their property dictionaries.</span></span>

<span data-ttu-id="9b7eb-382">*Dla języka JavaScript sieci web klientów*, [Użyj inicjatory telemetrii JavaScript](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="9b7eb-383">*dane telemetryczne tooall właściwości tooadd*, włącznie z danymi hello z modułów kolekcji standardowych [zaimplementować `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-383">*tooadd properties tooall telemetry*, including hello data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="9b7eb-384">Próbkowanie, filtrowania i przetwarzanie telemetrii</span><span class="sxs-lookup"><span data-stu-id="9b7eb-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="9b7eb-385">Można napisać kod tooprocess telemetrii przed wysłaniem z hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-385">You can write code tooprocess your telemetry before it's sent from hello SDK.</span></span> <span data-ttu-id="9b7eb-386">Przetwarzanie Hello zawiera dane są przesyłane z modułów standardowe telemetrii hello, takich jak kolekcji żądania HTTP i zależności kolekcji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-386">hello processing includes data that's sent from hello standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="9b7eb-387">[Dodaj właściwości](app-insights-api-filtering-sampling.md#add-properties) tootelemetry zaimplementowanie `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) tootelemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="9b7eb-388">Na przykład można dodać numery wersji lub wartości, które mają być obliczane od innych właściwości.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="9b7eb-389">[Filtrowanie](app-insights-api-filtering-sampling.md#filtering) można zmodyfikować lub odrzucić telemetrii przed wysłaniem z hello SDK zaimplementowanie `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from hello SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="9b7eb-390">Możesz kontrolować, co jest wysyłana lub odrzucone, ale masz tooaccount dla hello wpływu na Twoje metryki.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-390">You control what is sent or discarded, but you have tooaccount for hello effect on your metrics.</span></span> <span data-ttu-id="9b7eb-391">W zależności od tego, jak można odrzucić elementów może spowodować utratę toonavigate możliwości hello między elementy powiązane.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-391">Depending on how you discard items, you might lose hello ability toonavigate between related items.</span></span>

<span data-ttu-id="9b7eb-392">[Próbkowanie](app-insights-api-filtering-sampling.md) jest woluminem spakowanych rozwiązania tooreduce hello danych, które są wysyłane z portalem toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution tooreduce hello volume of data that's sent from your app toohello portal.</span></span> <span data-ttu-id="9b7eb-393">Robi to bez wpływu na powitania wyświetlane metryki.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-393">It does so without affecting hello displayed metrics.</span></span> <span data-ttu-id="9b7eb-394">I kopiuje je bez wpływu na możliwość problemów toodiagnose przechodzenie między powiązane elementy, takie jak wyjątki, żądania i wyświetleń strony.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-394">And it does so without affecting your ability toodiagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="9b7eb-395">[Dowiedz się więcej](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="9b7eb-396">Wyłączanie telemetrii</span><span class="sxs-lookup"><span data-stu-id="9b7eb-396">Disabling telemetry</span></span>
<span data-ttu-id="9b7eb-397">zbyt*dynamicznie zatrzymywania i uruchamiania* hello zbierania i przekazywania danych telemetrii:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-397">too*dynamically stop and start* hello collection and transmission of telemetry:</span></span>

<span data-ttu-id="9b7eb-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="9b7eb-399">zbyt*wyłączyć wybranego standardowe moduły zbierające*— na przykład liczniki wydajności żądań HTTP i zależności — Usuń lub komentarz hello odpowiednich wierszy w [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Można to zrobisz, na przykład, jeśli chcesz toosend danych TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-399">too*disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <span data-ttu-id="9b7eb-400"><a name="debug"></a>Tryb dewelopera</span><span class="sxs-lookup"><span data-stu-id="9b7eb-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="9b7eb-401">Podczas debugowania, jest przydatne toohave telemetrii przyspieszone przez potok hello tak, aby od razu Zobacz wyniki.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-401">During debugging, it's useful toohave your telemetry expedited through hello pipeline so that you can see results immediately.</span></span> <span data-ttu-id="9b7eb-402">Możesz również get przejrzeć dodatkowe komunikaty ułatwiające śledzenia problemów z hello telemetrii.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-402">You also get additional messages that help you trace any problems with hello telemetry.</span></span> <span data-ttu-id="9b7eb-403">Wyłącz go w środowisku produkcyjnym, ponieważ może to spowolnić aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="9b7eb-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="9b7eb-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="9b7eb-406"><a name="ikey"></a>Ustawienie hello klucza instrumentacji dla wybranego telemetria niestandardowa</span><span class="sxs-lookup"><span data-stu-id="9b7eb-406"><a name="ikey"></a> Setting hello instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="9b7eb-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="9b7eb-408"><a name="dynamic-ikey"></a>Klucz Instrumentacji dynamiczne</span><span class="sxs-lookup"><span data-stu-id="9b7eb-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="9b7eb-409">łączenie się dane telemetryczne z programowanie, testów i środowisk produkcyjnych tooavoid można [utworzyć oddzielne zasobów usługi Application Insights](app-insights-create-new-resource.md) i zmiany ich kluczy, w zależności od środowiska hello.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-409">tooavoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on hello environment.</span></span>

<span data-ttu-id="9b7eb-410">Zamiast pobierania klucza Instrumentacji hello hello pliku konfiguracji, możesz ustawić w kodzie.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-410">Instead of getting hello instrumentation key from hello configuration file, you can set it in your code.</span></span> <span data-ttu-id="9b7eb-411">Ustaw klucz hello w metodzie inicjowania, takich jak pliku global.aspx.cs w usługi ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-411">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="9b7eb-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="9b7eb-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="9b7eb-414">Na stronach sieci Web, może być tooset go z serwera sieci web hello stanu zamiast kodowania go dosłownie w hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-414">In webpages, you might want tooset it from hello web server's state, rather than coding it literally into hello script.</span></span> <span data-ttu-id="9b7eb-415">Na przykład na stronie sieci Web wygenerowane w aplikacji ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="9b7eb-416">*Język JavaScript w Razor*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="9b7eb-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="9b7eb-417">TelemetryContext</span></span>
<span data-ttu-id="9b7eb-418">TelemetryClient ma właściwość kontekstu, która zawiera wartości, które są wysyłane oraz wszystkie dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="9b7eb-419">Zwykle są ustawione przez moduły standardowe telemetrii hello, ale można również ustawić je samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-419">They are normally set by hello standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="9b7eb-420">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9b7eb-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="9b7eb-421">Jeśli ustawisz dowolne z tych wartości samodzielnie, rozważ usunięcie hello odpowiedni wiersz z [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), dzięki czemu hello standardowe wartości i wartości, na których nie pobrać pomylić.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-421">If you set any of these values yourself, consider removing hello relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and hello standard values don't get confused.</span></span>

* <span data-ttu-id="9b7eb-422">**Składnik**: hello aplikacji i jej wersję.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-422">**Component**: hello app and its version.</span></span>
* <span data-ttu-id="9b7eb-423">**Urządzenie**: dane dotyczące urządzenia hello, gdzie aplikacja hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-423">**Device**: Data about hello device where hello app is running.</span></span> <span data-ttu-id="9b7eb-424">(W aplikacjach sieci web jest powitania serwera lub klienta urządzenia, które telemetrii hello są wysyłane z).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-424">(In web apps, this is hello server or client device that hello telemetry is sent from.)</span></span>
* <span data-ttu-id="9b7eb-425">**InstrumentationKey**: hello zasobu usługi Application Insights, w którym są wyświetlane dane telemetryczne hello Azure.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-425">**InstrumentationKey**: hello Application Insights resource in Azure where hello telemetry appear.</span></span> <span data-ttu-id="9b7eb-426">On zwykle jest pobierany z ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="9b7eb-427">**Lokalizacja**: hello lokalizację geograficzną urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-427">**Location**: hello geographic location of hello device.</span></span>
* <span data-ttu-id="9b7eb-428">**Operacja**: W aplikacji sieci web, hello bieżącego żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-428">**Operation**: In web apps, hello current HTTP request.</span></span> <span data-ttu-id="9b7eb-429">W innych typów aplikacji można ustawić tego zdarzenia toogroup ze sobą.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-429">In other app types, you can set this toogroup events together.</span></span>
  * <span data-ttu-id="9b7eb-430">**Identyfikator**: wartość wygenerowaną odpowiadająca różnych zdarzeń, dzięki czemu inspekcji żadnych zdarzeń diagnostycznych wyszukiwania można znaleźć powiązanych elementów.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="9b7eb-431">**Nazwa**: identyfikator zwykle hello adres URL żądania hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-431">**Name**: An identifier, usually hello URL of hello HTTP request.</span></span>
  * <span data-ttu-id="9b7eb-432">**SyntheticSource**: Jeśli nie wartość null lub jest pusty, ciąg, który wskazuje źródła hello hello żądania został zidentyfikowany jako test robota lub sieci web.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-432">**SyntheticSource**: If not null or empty, a string that indicates that hello source of hello request has been identified as a robot or web test.</span></span> <span data-ttu-id="9b7eb-433">Domyślnie jest ona wykluczana z obliczeń w Eksploratorze metryk.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="9b7eb-434">**Właściwości**: właściwości, które są wysyłane z wszystkich danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="9b7eb-435">Może zostać zastąpiona w poszczególnych Śledź * wywołania.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="9b7eb-436">**Sesja**: hello sesja.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-436">**Session**: hello user's session.</span></span> <span data-ttu-id="9b7eb-437">Identyfikator Hello jest ustawiony tooa wygenerowany wartość, która jest zmieniany, gdy użytkownik hello nie była aktywna przez pewien czas.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-437">hello ID is set tooa generated value, which is changed when hello user has not been active for a while.</span></span>
* <span data-ttu-id="9b7eb-438">**Użytkownik**: informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="9b7eb-439">Limity</span><span class="sxs-lookup"><span data-stu-id="9b7eb-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="9b7eb-440">Naciśnięcie limit szybkości danych hello, użyj tooavoid [próbkowania](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-440">tooavoid hitting hello data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="9b7eb-441">toodetermine, jak długo dane są przechowywane, zobacz [przechowywanie danych i ochrona prywatności](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-441">toodetermine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="9b7eb-442">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="9b7eb-442">Reference docs</span></span>
* [<span data-ttu-id="9b7eb-443">Platformy ASP.NET — dokumentacja</span><span class="sxs-lookup"><span data-stu-id="9b7eb-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="9b7eb-444">Dokumentacja programu Java</span><span class="sxs-lookup"><span data-stu-id="9b7eb-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="9b7eb-445">JavaScript — odwołanie</span><span class="sxs-lookup"><span data-stu-id="9b7eb-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="9b7eb-446">Zestaw SDK systemu Android</span><span class="sxs-lookup"><span data-stu-id="9b7eb-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="9b7eb-447">Zestaw SDK systemu iOS</span><span class="sxs-lookup"><span data-stu-id="9b7eb-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="9b7eb-448">Kod zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="9b7eb-448">SDK code</span></span>
* [<span data-ttu-id="9b7eb-449">Platformy ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="9b7eb-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="9b7eb-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="9b7eb-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="9b7eb-451">Pakiety systemu Windows Server</span><span class="sxs-lookup"><span data-stu-id="9b7eb-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="9b7eb-452">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="9b7eb-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="9b7eb-453">Zestaw SDK dla języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="9b7eb-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="9b7eb-454">Wszystkie platformy</span><span class="sxs-lookup"><span data-stu-id="9b7eb-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="9b7eb-455">Pytania</span><span class="sxs-lookup"><span data-stu-id="9b7eb-455">Questions</span></span>
* <span data-ttu-id="9b7eb-456">*Jakie wyjątki może zgłosić Track_() wywołania*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="9b7eb-457">Brak.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-457">None.</span></span> <span data-ttu-id="9b7eb-458">Nie ma potrzeby toowrap ich w klauzulach try-catch.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-458">You don't need toowrap them in try-catch clauses.</span></span> <span data-ttu-id="9b7eb-459">Jeśli hello SDK napotyka problemy, będzie rejestrować wiadomości w danych wyjściowych konsoli debugowania hello i — jeśli hello wiadomości uzyskać za pomocą — diagnostycznych wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9b7eb-459">If hello SDK encounters problems, it will log messages in hello debug console output and--if hello messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="9b7eb-460">*Czy istnieje danych tooget interfejsu API REST z portalu hello?*</span><span class="sxs-lookup"><span data-stu-id="9b7eb-460">*Is there a REST API tooget data from hello portal?*</span></span>

    <span data-ttu-id="9b7eb-461">Tak, hello [dostępu do danych interfejsu API](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-461">Yes, hello [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="9b7eb-462">Inne sposoby tooextract dane obejmują [wyeksportować z Analytics tooPower BI](app-insights-export-power-bi.md) i [Eksport ciągły](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="9b7eb-462">Other ways tooextract data include [export from Analytics tooPower BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="9b7eb-463"><a name="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b7eb-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="9b7eb-464">Wyszukiwanie zdarzeń i dzienniki</span><span class="sxs-lookup"><span data-stu-id="9b7eb-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="9b7eb-465">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="9b7eb-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


