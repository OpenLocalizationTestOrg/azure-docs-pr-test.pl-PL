---
title: "Strumień metryk niestandardowych metryk i diagnostyki w usłudze Azure Application Insights na żywo | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 1eb2e0c467d4fb4cb263047caf58d36231578d9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="84055-103">Strumień na żywo metryki: Monitor & Diagnozuj z opóźnieniem 1 sekundę</span><span class="sxs-lookup"><span data-stu-id="84055-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="84055-104">Sonda Puls wznowiony aplikacji sieci web na żywo, w środowisku produkcyjnym za pomocą strumień na żywo metryki z [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84055-104">Probe the beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="84055-105">Wybierz i filtrować liczniki wydajności i metryk, które należy obserwować w czasie rzeczywistym, bez jakichkolwiek zakłóceń w usłudze.</span><span class="sxs-lookup"><span data-stu-id="84055-105">Select and filter metrics and performance counters to watch in real time, without any disturbance to your service.</span></span> <span data-ttu-id="84055-106">Sprawdź dane śledzenia stosu z żądań próbki nie powiodło się i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="84055-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="84055-107">Razem z [profilera](app-insights-profiler.md), [debugera migawki](app-insights-snapshot-debugger.md), i [testowania wydajności](app-insights-monitor-web-app-availability.md#performance-tests), strumień na żywo metryki udostępnia zaawansowane i nieinwazyjna narzędzie diagnostyczne dla sieci web na żywo lokacja.</span><span class="sxs-lookup"><span data-stu-id="84055-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="84055-108">Strumień na żywo metryki można:</span><span class="sxs-lookup"><span data-stu-id="84055-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="84055-109">Sprawdź poprawność poprawkę podczas jego zwolnienia obserwując liczniki wydajności i niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="84055-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="84055-110">Obejrzyj wpływu testu obciążenia i diagnozowanie problemów na żywo.</span><span class="sxs-lookup"><span data-stu-id="84055-110">Watch the effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="84055-111">Skupić się na sesje poszczególnego testu lub odfiltrować znanych problemów, wybierając i filtrowanie metryk, które chcesz obejrzeć.</span><span class="sxs-lookup"><span data-stu-id="84055-111">Focus on particular test sessions or filter out known issues, by selecting and filtering the metrics you want to watch.</span></span>
* <span data-ttu-id="84055-112">Pobierz dane śledzenia wyjątków, po ich wprowadzeniu.</span><span class="sxs-lookup"><span data-stu-id="84055-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="84055-113">Poeksperymentuj z filtrów, aby znaleźć najbardziej odpowiednie kluczowych wskaźników wydajności.</span><span class="sxs-lookup"><span data-stu-id="84055-113">Experiment with filters to find the most relevant KPIs.</span></span>
* <span data-ttu-id="84055-114">Monitorowanie oknami wydajności licznika na żywo.</span><span class="sxs-lookup"><span data-stu-id="84055-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="84055-115">Łatwo zidentyfikować serwera, na którym występują problemy i filtr, który wszystkich kluczowych wskaźników wydajności/live źródła danych tylko z tym serwerem.</span><span class="sxs-lookup"><span data-stu-id="84055-115">Easily identify a server that is having issues, and filter all the KPI/live feed to just that server.</span></span>

<span data-ttu-id="84055-116">[![Metryki strumienia wideo na żywo](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="84055-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="84055-117">Strumień na żywo metryki jest obecnie dostępna w aplikacji ASP.NET uruchomionych lokalnie lub w chmurze.</span><span class="sxs-lookup"><span data-stu-id="84055-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in the Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="84055-118">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="84055-118">Get started</span></span>

1. <span data-ttu-id="84055-119">Jeśli nie jest jeszcze [zainstalowane usługi Application Insights](app-insights-asp-net.md) w aplikacji sieci web ASP.NET lub [aplikacji dla systemu Windows server](app-insights-windows-services.md), zrób to teraz.</span><span class="sxs-lookup"><span data-stu-id="84055-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="84055-120">**Aktualizacja do najnowszej wersji** pakietu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="84055-120">**Update to the latest version** of the Application Insights package.</span></span> <span data-ttu-id="84055-121">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt i wybierz polecenie **pakiety zarządzania pakietami Nuget**.</span><span class="sxs-lookup"><span data-stu-id="84055-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="84055-122">Otwórz **aktualizacje** karcie wyboru **Uwzględnij wersję wstępną**i wybrać wszystkie pakiety Microsoft.ApplicationInsights.*.</span><span class="sxs-lookup"><span data-stu-id="84055-122">Open the **Updates** tab, check **Include prerelease**, and select all the Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="84055-123">Ponownie wdróż aplikację.</span><span class="sxs-lookup"><span data-stu-id="84055-123">Redeploy your app.</span></span>

3. <span data-ttu-id="84055-124">W [portalu Azure](https://portal.azure.com), otwórz zasobu usługi Application Insights dla aplikacji, a następnie strumień na żywo.</span><span class="sxs-lookup"><span data-stu-id="84055-124">In the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="84055-125">[Bezpieczny kanał kontrolny](#secure-the-control-channel) Jeśli poufnych danych, takich jak nazwy klienta można użyć w filtry.</span><span class="sxs-lookup"><span data-stu-id="84055-125">[Secure the control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![W bloku Przegląd kliknij strumień na żywo](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="84055-127">Brak danych?</span><span class="sxs-lookup"><span data-stu-id="84055-127">No data?</span></span> <span data-ttu-id="84055-128">Sprawdź zapory serwera</span><span class="sxs-lookup"><span data-stu-id="84055-128">Check your server firewall</span></span>

<span data-ttu-id="84055-129">Sprawdź [wychodzące portów dla strumień na żywo metryki](app-insights-ip-addresses.md#outgoing-ports) są otwarte w zaporze serwerów.</span><span class="sxs-lookup"><span data-stu-id="84055-129">Check the [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in the firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="84055-130">Jaka jest różnica strumień na żywo metryki z Eksploratora metryk i analiza?</span><span class="sxs-lookup"><span data-stu-id="84055-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="84055-131">Strumień na żywo</span><span class="sxs-lookup"><span data-stu-id="84055-131">Live Stream</span></span> | <span data-ttu-id="84055-132">Eksploratora metryk i analiza</span><span class="sxs-lookup"><span data-stu-id="84055-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="84055-133">Opóźnienie</span><span class="sxs-lookup"><span data-stu-id="84055-133">Latency</span></span>|<span data-ttu-id="84055-134">Dane wyświetlane w ciągu sekundy</span><span class="sxs-lookup"><span data-stu-id="84055-134">Data displayed within one second</span></span>|<span data-ttu-id="84055-135">Zagregowane w ciągu minut</span><span class="sxs-lookup"><span data-stu-id="84055-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="84055-136">Brak okresu przechowywania</span><span class="sxs-lookup"><span data-stu-id="84055-136">No retention</span></span>|<span data-ttu-id="84055-137">Danych będzie nadal występować, gdy jest na wykresie, a następnie zostaje odrzucone</span><span class="sxs-lookup"><span data-stu-id="84055-137">Data persists while it's on the chart, and is then discarded</span></span>|[<span data-ttu-id="84055-138">Dane przechowywane przez 90 dni</span><span class="sxs-lookup"><span data-stu-id="84055-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="84055-139">Na żądanie</span><span class="sxs-lookup"><span data-stu-id="84055-139">On demand</span></span>|<span data-ttu-id="84055-140">Dane przesyłane strumieniowo podczas otwierania metryki na żywo</span><span class="sxs-lookup"><span data-stu-id="84055-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="84055-141">Dane są przesyłane, gdy zestaw SDK jest zainstalowany i włączony</span><span class="sxs-lookup"><span data-stu-id="84055-141">Data is sent whenever the SDK is installed and enabled</span></span>|
|<span data-ttu-id="84055-142">Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="84055-142">Free</span></span>|<span data-ttu-id="84055-143">Bezpłatne strumień na żywo danych nie istnieje</span><span class="sxs-lookup"><span data-stu-id="84055-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="84055-144">Warunkiem [ceny](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="84055-144">Subject to [pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="84055-145">Próbkowanie</span><span class="sxs-lookup"><span data-stu-id="84055-145">Sampling</span></span>|<span data-ttu-id="84055-146">Wszystkie wybrane metryki i liczniki są przesyłane.</span><span class="sxs-lookup"><span data-stu-id="84055-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="84055-147">Błędy i ślady stosu są próbkowane.</span><span class="sxs-lookup"><span data-stu-id="84055-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="84055-148">TelemetryProcessors nie są stosowane.</span><span class="sxs-lookup"><span data-stu-id="84055-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="84055-149">Zdarzenia mogą być [próbkowany](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="84055-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="84055-150">Kanał kontrolny</span><span class="sxs-lookup"><span data-stu-id="84055-150">Control channel</span></span>|<span data-ttu-id="84055-151">Sygnały formant filtru są wysyłane do zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="84055-151">Filter control signals are sent to the SDK.</span></span> <span data-ttu-id="84055-152">Firma Microsoft zaleca [bezpiecznego kanału](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="84055-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="84055-153">Komunikacja jest jednokierunkowa do portalu</span><span class="sxs-lookup"><span data-stu-id="84055-153">Communication is one-way, to the portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="84055-154">Wybierz i filtrowanie Twoje metryki</span><span class="sxs-lookup"><span data-stu-id="84055-154">Select and filter your metrics</span></span>

<span data-ttu-id="84055-155">(Dostępne w klasycznej aplikacji ASP.NET przy użyciu najnowszej wersji zestawu SDK).</span><span class="sxs-lookup"><span data-stu-id="84055-155">(Available on classic ASP.NET apps with the latest SDK.)</span></span>

<span data-ttu-id="84055-156">Niestandardowe wskaźnik KPI na żywo można monitorować, stosując filtry dowolnego na dowolnym telemetrii usługi Application Insights z portalu.</span><span class="sxs-lookup"><span data-stu-id="84055-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from the portal.</span></span> <span data-ttu-id="84055-157">Kliknij formant filtru, który pokazuje, kiedy użytkownik myszą żadnego z wykresami.</span><span class="sxs-lookup"><span data-stu-id="84055-157">Click the filter control that shows when you mouse-over any of the charts.</span></span> <span data-ttu-id="84055-158">Poniższy schemat jest kreślenia niestandardowych liczbę żądań wskaźnika KPI z filtrami na adres URL i czas trwania atrybutów.</span><span class="sxs-lookup"><span data-stu-id="84055-158">The following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="84055-159">Sprawdź poprawność filtry z sekcji podglądu strumienia, który zawiera źródło danych na żywo dane telemetryczne, który spełnia kryteria określone w dowolnym momencie w czasie.</span><span class="sxs-lookup"><span data-stu-id="84055-159">Validate your filters with the Stream Preview section that shows a live feed of telemetry that matches the criteria you have specified at any point in time.</span></span> 

![Żądanie niestandardowego wskaźnika KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="84055-161">Można monitorować wartość inna niż liczba.</span><span class="sxs-lookup"><span data-stu-id="84055-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="84055-162">Opcje zależą od typu stream, który może być dowolnym telemetrii usługi Application Insights: żądań, zależności, wyjątki, śledzenie, zdarzenia lub metryki.</span><span class="sxs-lookup"><span data-stu-id="84055-162">The options depend on the type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="84055-163">Może być własną [niestandardowych miar](app-insights-api-custom-events-metrics.md#properties):</span><span class="sxs-lookup"><span data-stu-id="84055-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Wartość opcji](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="84055-165">Oprócz telemetrii usługi Application Insights można również monitorować żadnych licznika wydajności systemu Windows, zaznaczając który opcje strumienia i podanie nazwy licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="84055-165">In addition to Application Insights telemetry, you can also monitor any Windows performance counter by selecting that from the stream options, and providing the name of the performance counter.</span></span>

<span data-ttu-id="84055-166">Metryki na żywo są agregowane w dwóch miejscach: lokalnie na każdym serwerze, a następnie na wszystkich serwerach.</span><span class="sxs-lookup"><span data-stu-id="84055-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="84055-167">Możesz zmienić domyślną w zaznaczając inne opcje w odpowiednich listach rozwijanych.</span><span class="sxs-lookup"><span data-stu-id="84055-167">You can change the default at either by selecting other options in the respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="84055-168">Przykładowe dane telemetryczne: Niestandardowych zdarzeń diagnostycznych na żywo</span><span class="sxs-lookup"><span data-stu-id="84055-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="84055-169">Domyślnie na żywo źródła zdarzeń zawiera przykłady żądań zakończonych niepowodzeniem wywołania zależności, wyjątki, zdarzeń i śledzenia.</span><span class="sxs-lookup"><span data-stu-id="84055-169">By default, the live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="84055-170">Kliknij ikonę filtru, aby wyświetlić kryteria zastosowane w dowolnym momencie w czasie.</span><span class="sxs-lookup"><span data-stu-id="84055-170">Click the filter icon to see the applied criteria at any point in time.</span></span> 

![Źródła danych na żywo domyślne](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="84055-172">Jako o metryki, można określić żadnych kryteriów dowolne typy telemetrii usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="84055-172">As with metrics, you can specify any arbitrary criteria to any of the Application Insights telemetry types.</span></span> <span data-ttu-id="84055-173">W tym przykładzie mamy wybierania określone żądanie błędów, ślady i zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="84055-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="84055-174">Możemy również wybierania wszystkie zależności błędy i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="84055-174">We are also selecting all exceptions and dependency failures.</span></span>

![Niestandardowego źródła danych na żywo](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="84055-176">Uwaga: Obecnie kryteriów na podstawie komunikatu wyjątku używać komunikat o wyjątku najbardziej zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="84055-176">Note: Currently, for Exception message-based criteria, use the outermost exception message.</span></span> <span data-ttu-id="84055-177">W powyższym przykładzie filtrowanie niegroźne wyjątek z komunikatem o wyjątku wewnętrznego (następuje "<--" ogranicznika) "klient rozłączył się."</span><span class="sxs-lookup"><span data-stu-id="84055-177">In the preceding example, to filter out the benign exception with inner exception message (follows the "<--" delimiter) "The client disconnected."</span></span> <span data-ttu-id="84055-178">Użyj wiadomości nie zawiera kryteriów "Błąd podczas odczytu treści żądania".</span><span class="sxs-lookup"><span data-stu-id="84055-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="84055-179">Zobacz szczegóły elementów w źródle danych na żywo, klikając go.</span><span class="sxs-lookup"><span data-stu-id="84055-179">See the details of an item in the live feed by clicking it.</span></span> <span data-ttu-id="84055-180">Źródła danych można wstrzymać albo klikając **wstrzymać** lub po prostu przewijania w dół lub klikając element.</span><span class="sxs-lookup"><span data-stu-id="84055-180">You can pause the feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="84055-181">Źródła danych na żywo zostanie wznowiona po przewiń do góry lub przez kliknięcie przycisku licznik elementów zebranych podczas została wstrzymana.</span><span class="sxs-lookup"><span data-stu-id="84055-181">Live feed will resume after you scroll back to the top, or by clicking the counter of items collected while it was paused.</span></span>

![Próbkowany awarii na żywo](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="84055-183">Filtruj według wystąpienia serwera</span><span class="sxs-lookup"><span data-stu-id="84055-183">Filter by server instance</span></span>

<span data-ttu-id="84055-184">Jeśli chcesz monitorować wystąpienia roli konkretnego serwera, można filtrować według serwera.</span><span class="sxs-lookup"><span data-stu-id="84055-184">If you want to monitor a particular server role instance, you can filter by server.</span></span>

![Próbkowany awarii na żywo](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="84055-186">Wymagania dotyczące zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="84055-186">SDK Requirements</span></span>
<span data-ttu-id="84055-187">Niestandardowe strumień na żywo metryki jest dostępna z wersji 2.4.0-beta2 lub nowszej programu [zestaw SDK usługi Application Insights dla sieci web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="84055-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="84055-188">Pamiętaj wybrać opcję "Uwzględnij wydanie wstępne" z Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="84055-188">Remember to select "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-the-control-channel"></a><span data-ttu-id="84055-189">Bezpieczny kanał kontrolny</span><span class="sxs-lookup"><span data-stu-id="84055-189">Secure the control channel</span></span>
<span data-ttu-id="84055-190">Filtry niestandardowe podane kryteria są odsyłane do składnika metryki na żywo w zestaw SDK usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="84055-190">The custom filters criteria you specify are sent back to the Live Metrics component in the Application Insights SDK.</span></span> <span data-ttu-id="84055-191">Filtry potencjalnie mogą zawierać poufne informacje, takie jak customerIDs.</span><span class="sxs-lookup"><span data-stu-id="84055-191">The filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="84055-192">Kanał można zabezpieczyć przy użyciu tajnego klucza interfejsu API, oprócz klucza instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="84055-192">You can make the channel secure with a secret API key in addition to the instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="84055-193">Utwórz klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="84055-193">Create an API Key</span></span>

![Utwórz klucz interfejsu api](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-to-configuration"></a><span data-ttu-id="84055-195">Dodaj klucz interfejsu API do konfiguracji</span><span class="sxs-lookup"><span data-stu-id="84055-195">Add API key to Configuration</span></span>
<span data-ttu-id="84055-196">W pliku applicationinsights.config dodać AuthenticationApiKey QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="84055-196">In the applicationinsights.config file, add the AuthenticationApiKey to the QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="84055-197">Lub w kodzie, ustaw go w QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="84055-197">Or in code, set it on the QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="84055-198">Jednak jeśli rozpoznaje i zaufania połączonych serwerów, możesz spróbować filtry niestandardowe bez uwierzytelnionego kanału.</span><span class="sxs-lookup"><span data-stu-id="84055-198">However, if you recognize and trust all the connected servers, you can try the custom filters without the authenticated channel.</span></span> <span data-ttu-id="84055-199">Ta opcja jest dostępna przez sześć miesięcy.</span><span class="sxs-lookup"><span data-stu-id="84055-199">This option is available for six months.</span></span> <span data-ttu-id="84055-200">To zastąpienie jest wymagana raz na nowej sesji, lub gdy nowy serwer przejściu do trybu online.</span><span class="sxs-lookup"><span data-stu-id="84055-200">This override is required once every new session, or when a new server comes online.</span></span>

![Opcje uwierzytelniania metryki na żywo](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="84055-202">Zdecydowanie zaleca się skonfigurowanie kanału uwierzytelnionego przed wprowadzeniem potencjalnie wrażliwe informacje, takie jak CustomerID w kryteriach filtrowania.</span><span class="sxs-lookup"><span data-stu-id="84055-202">We strongly recommend that you set up the authenticated channel before entering potentially sensitive information like CustomerID in the filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="84055-203">Generowanie wydajności testu obciążenia</span><span class="sxs-lookup"><span data-stu-id="84055-203">Generating a performance test load</span></span>

<span data-ttu-id="84055-204">Jeśli chcesz obserwować wpływ wzrostu obciążenia, użyj bloku testu wydajności.</span><span class="sxs-lookup"><span data-stu-id="84055-204">If you want to watch the effect of a load increase, use the Performance Test blade.</span></span> <span data-ttu-id="84055-205">Symuluje ona żądań z liczba równoczesnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="84055-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="84055-206">Można uruchomić albo "testy ręczne" (ping testy) pojedynczego adresu URL, lub można je uruchomić [testu wydajności sieci web wieloetapowych](app-insights-monitor-web-app-availability.md#multi-step-web-tests) przekazywanego (w taki sam sposób jak test dostępności).</span><span class="sxs-lookup"><span data-stu-id="84055-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in the same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="84055-207">Po utworzeniu testu wydajności, otwórz testu i bloku strumień na żywo w oddzielnych okien.</span><span class="sxs-lookup"><span data-stu-id="84055-207">After you create the performance test, open the test and the Live Stream blade in separate windows.</span></span> <span data-ttu-id="84055-208">W tym samym czasie widoczne podczas uruchamiania testu wydajności umieszczonych w kolejce i obejrzyj strumień na żywo.</span><span class="sxs-lookup"><span data-stu-id="84055-208">You can see when the queued performance test starts, and watch live stream at the same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="84055-209">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="84055-209">Troubleshooting</span></span>

<span data-ttu-id="84055-210">Brak danych?</span><span class="sxs-lookup"><span data-stu-id="84055-210">No data?</span></span> <span data-ttu-id="84055-211">Jeśli aplikacja znajduje się w sieci chronionej: strumień na żywo metryki korzysta z innych adresów IP, niż inne telemetrii usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="84055-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="84055-212">Upewnij się, że [adresów IP](app-insights-ip-addresses.md) w zaporze są otwarte.</span><span class="sxs-lookup"><span data-stu-id="84055-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="84055-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84055-213">Next steps</span></span>
* [<span data-ttu-id="84055-214">Monitorowanie użycia za pomocą usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="84055-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="84055-215">W wyszukiwaniu diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="84055-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="84055-216">Profiler</span><span class="sxs-lookup"><span data-stu-id="84055-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="84055-217">Debuger migawki</span><span class="sxs-lookup"><span data-stu-id="84055-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
