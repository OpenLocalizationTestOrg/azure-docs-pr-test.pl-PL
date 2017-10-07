---
title: "aaaLive strumienia metryk niestandardowych metryk i diagnostyki w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Monitorowanie aplikacji sieci web w czasie rzeczywistym z metryki niestandardowe i diagnozowanie problemów z błędów, ślady i wydarzeń na żywo źródło danych."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="8e676-103">Strumień na żywo metryki: Monitor & Diagnozuj z opóźnieniem 1 sekundę</span><span class="sxs-lookup"><span data-stu-id="8e676-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="8e676-104">Sonda hello interwałów pulsu aplikacji sieci web na żywo, w środowisku produkcyjnym za pomocą strumień na żywo metryki z [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e676-104">Probe hello beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="8e676-105">Wybierz i filtrować toowatch liczniki metryki i wydajności w czasie rzeczywistym, bez żadnej usługi tooyour zakłóceń.</span><span class="sxs-lookup"><span data-stu-id="8e676-105">Select and filter metrics and performance counters toowatch in real time, without any disturbance tooyour service.</span></span> <span data-ttu-id="8e676-106">Sprawdź dane śledzenia stosu z żądań próbki nie powiodło się i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="8e676-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="8e676-107">Razem z [profilera](app-insights-profiler.md), [debugera migawki](app-insights-snapshot-debugger.md), i [testowania wydajności](app-insights-monitor-web-app-availability.md#performance-tests), strumień na żywo metryki udostępnia zaawansowane i nieinwazyjna narzędzie diagnostyczne dla sieci web na żywo lokacja.</span><span class="sxs-lookup"><span data-stu-id="8e676-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="8e676-108">Strumień na żywo metryki można:</span><span class="sxs-lookup"><span data-stu-id="8e676-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="8e676-109">Sprawdź poprawność poprawkę podczas jego zwolnienia obserwując liczniki wydajności i niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="8e676-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="8e676-110">Obejrzyj hello wpływu testu obciążenia i diagnozowanie problemów na żywo.</span><span class="sxs-lookup"><span data-stu-id="8e676-110">Watch hello effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="8e676-111">Skupić się na sesje poszczególnego testu lub odfiltrować znanych problemów, wybierając i metryki hello ma toowatch filtrowania.</span><span class="sxs-lookup"><span data-stu-id="8e676-111">Focus on particular test sessions or filter out known issues, by selecting and filtering hello metrics you want toowatch.</span></span>
* <span data-ttu-id="8e676-112">Pobierz dane śledzenia wyjątków, po ich wprowadzeniu.</span><span class="sxs-lookup"><span data-stu-id="8e676-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="8e676-113">Doświadczenia z filtrami toofind hello najistotniejsza kluczowych wskaźników wydajności.</span><span class="sxs-lookup"><span data-stu-id="8e676-113">Experiment with filters toofind hello most relevant KPIs.</span></span>
* <span data-ttu-id="8e676-114">Monitorowanie oknami wydajności licznika na żywo.</span><span class="sxs-lookup"><span data-stu-id="8e676-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="8e676-115">Łatwo zidentyfikować serwera, na którym występują problemy i filtrować wszystkie hello na żywo/KPI źródła toojust tego serwera.</span><span class="sxs-lookup"><span data-stu-id="8e676-115">Easily identify a server that is having issues, and filter all hello KPI/live feed toojust that server.</span></span>

<span data-ttu-id="8e676-116">[![Metryki strumienia wideo na żywo](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="8e676-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="8e676-117">Strumień na żywo metryki jest obecnie dostępna w aplikacji ASP.NET uruchomionych lokalnie lub w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="8e676-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in hello Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="8e676-118">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="8e676-118">Get started</span></span>

1. <span data-ttu-id="8e676-119">Jeśli nie jest jeszcze [zainstalowane usługi Application Insights](app-insights-asp-net.md) w aplikacji sieci web ASP.NET lub [aplikacji dla systemu Windows server](app-insights-windows-services.md), zrób to teraz.</span><span class="sxs-lookup"><span data-stu-id="8e676-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="8e676-120">**Aktualizacja toohello najnowszej wersji** hello pakietu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8e676-120">**Update toohello latest version** of hello Application Insights package.</span></span> <span data-ttu-id="8e676-121">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt i wybierz polecenie **pakiety zarządzania pakietami Nuget**.</span><span class="sxs-lookup"><span data-stu-id="8e676-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="8e676-122">Otwórz hello **aktualizacje** karcie wyboru **Uwzględnij wersję wstępną**i wybrać wszystkie pakiety Microsoft.ApplicationInsights.* hello.</span><span class="sxs-lookup"><span data-stu-id="8e676-122">Open hello **Updates** tab, check **Include prerelease**, and select all hello Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="8e676-123">Ponownie wdróż aplikację.</span><span class="sxs-lookup"><span data-stu-id="8e676-123">Redeploy your app.</span></span>

3. <span data-ttu-id="8e676-124">W hello [portalu Azure](https://portal.azure.com), otwórz hello zasobu usługi Application Insights dla aplikacji, a następnie strumień na żywo.</span><span class="sxs-lookup"><span data-stu-id="8e676-124">In hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="8e676-125">[Witaj bezpieczny kanał kontrolny](#secure-the-control-channel) Jeśli poufnych danych, takich jak nazwy klienta można użyć w filtry.</span><span class="sxs-lookup"><span data-stu-id="8e676-125">[Secure hello control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![W bloku omówienie powitania kliknij strumień na żywo](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="8e676-127">Brak danych?</span><span class="sxs-lookup"><span data-stu-id="8e676-127">No data?</span></span> <span data-ttu-id="8e676-128">Sprawdź zapory serwera</span><span class="sxs-lookup"><span data-stu-id="8e676-128">Check your server firewall</span></span>

<span data-ttu-id="8e676-129">Sprawdź hello [wychodzące portów dla strumień na żywo metryki](app-insights-ip-addresses.md#outgoing-ports) są otwarte w zaporze hello serwerów.</span><span class="sxs-lookup"><span data-stu-id="8e676-129">Check hello [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in hello firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="8e676-130">Jaka jest różnica strumień na żywo metryki z Eksploratora metryk i analiza?</span><span class="sxs-lookup"><span data-stu-id="8e676-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="8e676-131">Transmisja strumieniowa na żywo</span><span class="sxs-lookup"><span data-stu-id="8e676-131">Live Stream</span></span> | <span data-ttu-id="8e676-132">Eksploratora metryk i analiza</span><span class="sxs-lookup"><span data-stu-id="8e676-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="8e676-133">Opóźnienie</span><span class="sxs-lookup"><span data-stu-id="8e676-133">Latency</span></span>|<span data-ttu-id="8e676-134">Dane wyświetlane w ciągu sekundy</span><span class="sxs-lookup"><span data-stu-id="8e676-134">Data displayed within one second</span></span>|<span data-ttu-id="8e676-135">Zagregowane w ciągu minut</span><span class="sxs-lookup"><span data-stu-id="8e676-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="8e676-136">Brak okresu przechowywania</span><span class="sxs-lookup"><span data-stu-id="8e676-136">No retention</span></span>|<span data-ttu-id="8e676-137">Danych będzie nadal występować, gdy znajduje się na powitania wykresu, a następnie zostaje odrzucone</span><span class="sxs-lookup"><span data-stu-id="8e676-137">Data persists while it's on hello chart, and is then discarded</span></span>|[<span data-ttu-id="8e676-138">Dane przechowywane przez 90 dni</span><span class="sxs-lookup"><span data-stu-id="8e676-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="8e676-139">Na żądanie</span><span class="sxs-lookup"><span data-stu-id="8e676-139">On demand</span></span>|<span data-ttu-id="8e676-140">Dane przesyłane strumieniowo podczas otwierania metryki na żywo</span><span class="sxs-lookup"><span data-stu-id="8e676-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="8e676-141">Dane są przesyłane przy każdym hello zestawu SDK jest zainstalowany i włączony</span><span class="sxs-lookup"><span data-stu-id="8e676-141">Data is sent whenever hello SDK is installed and enabled</span></span>|
|<span data-ttu-id="8e676-142">Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="8e676-142">Free</span></span>|<span data-ttu-id="8e676-143">Bezpłatne strumień na żywo danych nie istnieje</span><span class="sxs-lookup"><span data-stu-id="8e676-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="8e676-144">Zbyt podmiotu[ceny](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="8e676-144">Subject too[pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="8e676-145">Próbkowanie</span><span class="sxs-lookup"><span data-stu-id="8e676-145">Sampling</span></span>|<span data-ttu-id="8e676-146">Wszystkie wybrane metryki i liczniki są przesyłane.</span><span class="sxs-lookup"><span data-stu-id="8e676-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="8e676-147">Błędy i ślady stosu są próbkowane.</span><span class="sxs-lookup"><span data-stu-id="8e676-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="8e676-148">TelemetryProcessors nie są stosowane.</span><span class="sxs-lookup"><span data-stu-id="8e676-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="8e676-149">Zdarzenia mogą być [próbkowany](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="8e676-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="8e676-150">Kanał kontrolny</span><span class="sxs-lookup"><span data-stu-id="8e676-150">Control channel</span></span>|<span data-ttu-id="8e676-151">Sygnały formant filtru są wysyłane toohello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="8e676-151">Filter control signals are sent toohello SDK.</span></span> <span data-ttu-id="8e676-152">Firma Microsoft zaleca [bezpiecznego kanału](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="8e676-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="8e676-153">Komunikacja jest jednokierunkowe toohello portalu</span><span class="sxs-lookup"><span data-stu-id="8e676-153">Communication is one-way, toohello portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="8e676-154">Wybierz i filtrowanie Twoje metryki</span><span class="sxs-lookup"><span data-stu-id="8e676-154">Select and filter your metrics</span></span>

<span data-ttu-id="8e676-155">(Dostępne w klasycznej aplikacji ASP.NET przy użyciu hello najnowszej wersji zestawu SDK.)</span><span class="sxs-lookup"><span data-stu-id="8e676-155">(Available on classic ASP.NET apps with hello latest SDK.)</span></span>

<span data-ttu-id="8e676-156">Stosowanie filtrów dowolnego na dowolnym telemetrii usługi Application Insights z portalu hello można monitorować niestandardowych wskaźnik KPI na żywo.</span><span class="sxs-lookup"><span data-stu-id="8e676-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from hello portal.</span></span> <span data-ttu-id="8e676-157">Kliknij formant filtru hello pokazujący, gdy użytkownik myszą żadnego z wykresami hello.</span><span class="sxs-lookup"><span data-stu-id="8e676-157">Click hello filter control that shows when you mouse-over any of hello charts.</span></span> <span data-ttu-id="8e676-158">powitania po wykresu jest kreślenia niestandardowych liczbę żądań wskaźnika KPI z filtrami na adres URL i czas trwania atrybutów.</span><span class="sxs-lookup"><span data-stu-id="8e676-158">hello following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="8e676-159">Sprawdź poprawność filtry z hello podglądu strumienia sekcja, która zawiera źródło danych na żywo dane telemetryczne, które spełniają kryteria hello, określone w dowolnym momencie w czasie.</span><span class="sxs-lookup"><span data-stu-id="8e676-159">Validate your filters with hello Stream Preview section that shows a live feed of telemetry that matches hello criteria you have specified at any point in time.</span></span> 

![Żądanie niestandardowego wskaźnika KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="8e676-161">Można monitorować wartość inna niż liczba.</span><span class="sxs-lookup"><span data-stu-id="8e676-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="8e676-162">Opcje Hello są zależne od typu hello strumienia, który może być dowolnym telemetrii usługi Application Insights: żądań, zależności, wyjątki, śledzenie, zdarzenia lub metryki.</span><span class="sxs-lookup"><span data-stu-id="8e676-162">hello options depend on hello type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="8e676-163">Może być własną [niestandardowych miar](app-insights-api-custom-events-metrics.md#properties):</span><span class="sxs-lookup"><span data-stu-id="8e676-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Wartość opcji](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="8e676-165">Ponadto tooApplication wgląd w dane telemetryczne, można również monitorować wszystkie licznika wydajności systemu Windows zaznaczając który hello strumienia opcje i podanie nazwy hello hello licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="8e676-165">In addition tooApplication Insights telemetry, you can also monitor any Windows performance counter by selecting that from hello stream options, and providing hello name of hello performance counter.</span></span>

<span data-ttu-id="8e676-166">Metryki na żywo są agregowane w dwóch miejscach: lokalnie na każdym serwerze, a następnie na wszystkich serwerach.</span><span class="sxs-lookup"><span data-stu-id="8e676-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="8e676-167">Możesz zmienić domyślną hello w zaznaczając inne opcje w hello odpowiednich rozwijane.</span><span class="sxs-lookup"><span data-stu-id="8e676-167">You can change hello default at either by selecting other options in hello respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="8e676-168">Przykładowe dane telemetryczne: Niestandardowych zdarzeń diagnostycznych na żywo</span><span class="sxs-lookup"><span data-stu-id="8e676-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="8e676-169">Domyślnie program hello na żywo źródło zdarzeń przedstawiono przykłady żądań zakończonych niepowodzeniem wywołania zależności, wyjątki, zdarzeń i śledzenia.</span><span class="sxs-lookup"><span data-stu-id="8e676-169">By default, hello live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="8e676-170">Kliknij przycisk kryteria ikony filtru hello hello stosowane toosee w dowolnym momencie w czasie.</span><span class="sxs-lookup"><span data-stu-id="8e676-170">Click hello filter icon toosee hello applied criteria at any point in time.</span></span> 

![Źródła danych na żywo domyślne](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="8e676-172">Jako o metryki, można określić żadnych tooany dowolnego kryterium typów hello telemetrii usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8e676-172">As with metrics, you can specify any arbitrary criteria tooany of hello Application Insights telemetry types.</span></span> <span data-ttu-id="8e676-173">W tym przykładzie mamy wybierania określone żądanie błędów, ślady i zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="8e676-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="8e676-174">Możemy również wybierania wszystkie zależności błędy i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="8e676-174">We are also selecting all exceptions and dependency failures.</span></span>

![Niestandardowego źródła danych na żywo](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="8e676-176">Uwaga: Obecnie kryteriów na podstawie komunikatu wyjątku używać komunikat o wyjątku peryferyjnych hello.</span><span class="sxs-lookup"><span data-stu-id="8e676-176">Note: Currently, for Exception message-based criteria, use hello outermost exception message.</span></span> <span data-ttu-id="8e676-177">W hello poprzedzających przykład toofilter limit hello niegroźne wyjątek z komunikatem o wyjątku wewnętrznego (hello następujące "<--" ogranicznika) "hello klient został rozłączony."</span><span class="sxs-lookup"><span data-stu-id="8e676-177">In hello preceding example, toofilter out hello benign exception with inner exception message (follows hello "<--" delimiter) "hello client disconnected."</span></span> <span data-ttu-id="8e676-178">Użyj wiadomości nie zawiera kryteriów "Błąd podczas odczytu treści żądania".</span><span class="sxs-lookup"><span data-stu-id="8e676-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="8e676-179">Wyświetl szczegóły hello elementu hello na żywo źródła danych, klikając go.</span><span class="sxs-lookup"><span data-stu-id="8e676-179">See hello details of an item in hello live feed by clicking it.</span></span> <span data-ttu-id="8e676-180">W przypadku wstrzymania hello źródła danych, klikając pozycję **wstrzymać** lub po prostu przewijania w dół lub klikając element.</span><span class="sxs-lookup"><span data-stu-id="8e676-180">You can pause hello feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="8e676-181">Źródła danych na żywo zostanie wznowiona po Przewiń wstecz toohello top lub klikając hello licznika elementów zebranych podczas została wstrzymana.</span><span class="sxs-lookup"><span data-stu-id="8e676-181">Live feed will resume after you scroll back toohello top, or by clicking hello counter of items collected while it was paused.</span></span>

![Próbkowany awarii na żywo](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="8e676-183">Filtruj według wystąpienia serwera</span><span class="sxs-lookup"><span data-stu-id="8e676-183">Filter by server instance</span></span>

<span data-ttu-id="8e676-184">Jeśli chcesz toomonitor wystąpienia roli konkretnego serwera, można filtrować według serwera.</span><span class="sxs-lookup"><span data-stu-id="8e676-184">If you want toomonitor a particular server role instance, you can filter by server.</span></span>

![Próbkowany awarii na żywo](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="8e676-186">Wymagania dotyczące zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="8e676-186">SDK Requirements</span></span>
<span data-ttu-id="8e676-187">Niestandardowe strumień na żywo metryki jest dostępna z wersji 2.4.0-beta2 lub nowszej programu [zestaw SDK usługi Application Insights dla sieci web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="8e676-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="8e676-188">Należy pamiętać, opcja "Uwzględnij wydanie wstępne" tooselect z Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="8e676-188">Remember tooselect "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-hello-control-channel"></a><span data-ttu-id="8e676-189">Bezpieczny kanał kontrolny hello</span><span class="sxs-lookup"><span data-stu-id="8e676-189">Secure hello control channel</span></span>
<span data-ttu-id="8e676-190">Hello niestandardowe filtry kryteria są wysyłane toohello wstecz na żywo metryki składników w hello zestaw SDK usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8e676-190">hello custom filters criteria you specify are sent back toohello Live Metrics component in hello Application Insights SDK.</span></span> <span data-ttu-id="8e676-191">filtry Hello potencjalnie mogą zawierać poufne informacje, takie jak customerIDs.</span><span class="sxs-lookup"><span data-stu-id="8e676-191">hello filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="8e676-192">Możesz wprowadzić kanału hello zabezpieczyć za pomocą klucza tajnego interfejsu API dodatkowo toohello klucza instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="8e676-192">You can make hello channel secure with a secret API key in addition toohello instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="8e676-193">Utwórz klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="8e676-193">Create an API Key</span></span>

![Utwórz klucz interfejsu api](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a><span data-ttu-id="8e676-195">Dodaj tooConfiguration klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="8e676-195">Add API key tooConfiguration</span></span>
<span data-ttu-id="8e676-196">W pliku applicationinsights.config hello Dodaj hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="8e676-196">In hello applicationinsights.config file, add hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="8e676-197">Lub w kodzie, ustaw ją na powitania QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="8e676-197">Or in code, set it on hello QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="8e676-198">Jednak jeśli rozpoznaje i zaufania hello wszystkich połączonych serwerów, możesz spróbować filtry niestandardowe hello bez kanału hello uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="8e676-198">However, if you recognize and trust all hello connected servers, you can try hello custom filters without hello authenticated channel.</span></span> <span data-ttu-id="8e676-199">Ta opcja jest dostępna przez sześć miesięcy.</span><span class="sxs-lookup"><span data-stu-id="8e676-199">This option is available for six months.</span></span> <span data-ttu-id="8e676-200">To zastąpienie jest wymagana raz na nowej sesji, lub gdy nowy serwer przejściu do trybu online.</span><span class="sxs-lookup"><span data-stu-id="8e676-200">This override is required once every new session, or when a new server comes online.</span></span>

![Opcje uwierzytelniania metryki na żywo](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="8e676-202">Zdecydowanie zaleca się skonfigurowanie kanału hello uwierzytelniony przed wprowadzeniem potencjalnie wrażliwe informacje, takie jak CustomerID w hello kryteria filtrowania.</span><span class="sxs-lookup"><span data-stu-id="8e676-202">We strongly recommend that you set up hello authenticated channel before entering potentially sensitive information like CustomerID in hello filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="8e676-203">Generowanie wydajności testu obciążenia</span><span class="sxs-lookup"><span data-stu-id="8e676-203">Generating a performance test load</span></span>

<span data-ttu-id="8e676-204">Jeśli chcesz toowatch hello wpływu obciążenia zwiększyć, użyj hello testu wydajności bloku.</span><span class="sxs-lookup"><span data-stu-id="8e676-204">If you want toowatch hello effect of a load increase, use hello Performance Test blade.</span></span> <span data-ttu-id="8e676-205">Symuluje ona żądań z liczba równoczesnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8e676-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="8e676-206">Można uruchomić albo "testy ręczne" (ping testy) pojedynczego adresu URL, lub można je uruchomić [testu wydajności sieci web wieloetapowych](app-insights-monitor-web-app-availability.md#multi-step-web-tests) przekazywania (w hello sam sposób jak dostępności testu).</span><span class="sxs-lookup"><span data-stu-id="8e676-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in hello same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="8e676-207">Po utworzeniu testu wydajności hello Otwórz hello testu i hello bloku strumień na żywo w oddzielnych okien.</span><span class="sxs-lookup"><span data-stu-id="8e676-207">After you create hello performance test, open hello test and hello Live Stream blade in separate windows.</span></span> <span data-ttu-id="8e676-208">Zostanie wyświetlony, gdy hello w kolejce uruchamia test wydajności i obejrzyj strumień na żywo na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="8e676-208">You can see when hello queued performance test starts, and watch live stream at hello same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="8e676-209">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="8e676-209">Troubleshooting</span></span>

<span data-ttu-id="8e676-210">Brak danych?</span><span class="sxs-lookup"><span data-stu-id="8e676-210">No data?</span></span> <span data-ttu-id="8e676-211">Jeśli aplikacja znajduje się w sieci chronionej: strumień na żywo metryki korzysta z innych adresów IP, niż inne telemetrii usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8e676-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="8e676-212">Upewnij się, że [adresów IP](app-insights-ip-addresses.md) w zaporze są otwarte.</span><span class="sxs-lookup"><span data-stu-id="8e676-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="8e676-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8e676-213">Next steps</span></span>
* [<span data-ttu-id="8e676-214">Monitorowanie użycia za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="8e676-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="8e676-215">W wyszukiwaniu diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="8e676-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="8e676-216">Profiler</span><span class="sxs-lookup"><span data-stu-id="8e676-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="8e676-217">Debuger migawki</span><span class="sxs-lookup"><span data-stu-id="8e676-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
