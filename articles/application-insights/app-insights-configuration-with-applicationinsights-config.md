---
title: "Odwołanie aaaApplicationInsights.config - Azure | Dokumentacja firmy Microsoft"
description: "Włącz lub wyłącz modułów zbierania danych i Dodaj liczniki wydajności i innych parametrów."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="1e33d-103">Konfigurowanie hello zestaw SDK usługi Application Insights z ApplicationInsights.config lub XML</span><span class="sxs-lookup"><span data-stu-id="1e33d-103">Configuring hello Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="1e33d-104">Witaj zestaw SDK usługi Application Insights .NET składa się z liczby pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e33d-104">hello Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="1e33d-105">[Pakiet podstawowy](http://www.nuget.org/packages/Microsoft.ApplicationInsights) zapewnia hello interfejsu API do wysyłania danych telemetrycznych na powitania usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1e33d-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides hello API for sending telemetry to hello Application Insights.</span></span> <span data-ttu-id="1e33d-106">[Dodatkowe pakiety](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) Podaj dane telemetryczne *modułów* i *inicjatory* automatycznie śledzenia dane telemetryczne z aplikacji i jej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="1e33d-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="1e33d-107">Dostosowując hello pliku konfiguracji, można włączyć lub wyłączyć inicjatory i moduły danych telemetrycznych i ustaw parametry dla niektórych z nich.</span><span class="sxs-lookup"><span data-stu-id="1e33d-107">By adjusting hello configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="1e33d-108">plik konfiguracji Hello nosi nazwę `ApplicationInsights.config` lub `ApplicationInsights.xml`, w zależności od typu hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e33d-108">hello configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on hello type of your application.</span></span> <span data-ttu-id="1e33d-109">Jest automatycznie dodawany tooyour projektu, gdy użytkownik [zainstalować większość wersji zestawu SDK hello][start].</span><span class="sxs-lookup"><span data-stu-id="1e33d-109">It is automatically added tooyour project when you [install most versions of hello SDK][start].</span></span> <span data-ttu-id="1e33d-110">Jest także dodawane tooa aplikacji sieci web przez [Monitor stanu na serwerze IIS][redfield], lub po wybraniu hello Appplication Insights [rozszerzenia dla witryny sieci Web platformy Azure lub wirtualna](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1e33d-110">It is also added tooa web app by [Status Monitor on an IIS server][redfield], or when you select hello Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="1e33d-111">Nie ma pliku równoważne toocontrol hello [SDK na stronie sieci web][client].</span><span class="sxs-lookup"><span data-stu-id="1e33d-111">There isn't an equivalent file toocontrol hello [SDK in a web page][client].</span></span>

<span data-ttu-id="1e33d-112">W tym dokumencie opisano hello sekcje, które zostanie wyświetlony w konfiguracji hello plików, jak ich kontrolowania składników hello hello zestawu SDK, i które pakiety NuGet obciążenia tych składników.</span><span class="sxs-lookup"><span data-stu-id="1e33d-112">This document describes hello sections you see in hello configuration file, how they control hello components of hello SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="1e33d-113">Moduły danych telemetrycznych (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="1e33d-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="1e33d-114">Każdy moduł telemetrii służy do zbierania danych dla określonego typu i używa hello core API toosend hello danych.</span><span class="sxs-lookup"><span data-stu-id="1e33d-114">Each telemetry module collects a specific type of data and uses hello core API toosend hello data.</span></span> <span data-ttu-id="1e33d-115">Moduły Hello są instalowane przez różne pakiety NuGet, które również dodać pliku .config toohello wiersze wymagane hello.</span><span class="sxs-lookup"><span data-stu-id="1e33d-115">hello modules are installed by different NuGet packages, which also add hello required lines toohello .config file.</span></span>

<span data-ttu-id="1e33d-116">Brak węzła w pliku konfiguracyjnym powitania dla każdego modułu.</span><span class="sxs-lookup"><span data-stu-id="1e33d-116">There's a node in hello configuration file for each module.</span></span> <span data-ttu-id="1e33d-117">toodisable modułu, Usuń węzeł hello lub komentarz go.</span><span class="sxs-lookup"><span data-stu-id="1e33d-117">toodisable a module, delete hello node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="1e33d-118">Śledzenia zależności</span><span class="sxs-lookup"><span data-stu-id="1e33d-118">Dependency Tracking</span></span>
<span data-ttu-id="1e33d-119">[Śledzenia zależności](app-insights-asp-net-dependencies.md) zbiera dane telemetryczne dotyczące wywołania aplikacji sprawia, że toodatabases i usług zewnętrznych i baz danych.</span><span class="sxs-lookup"><span data-stu-id="1e33d-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes toodatabases and external services and databases.</span></span> <span data-ttu-id="1e33d-120">tooallow toowork tego modułu na serwerze usług IIS, należy za[Zainstaluj Monitor stanu][redfield].</span><span class="sxs-lookup"><span data-stu-id="1e33d-120">tooallow this module toowork in an IIS server, you need too[install Status Monitor][redfield].</span></span> <span data-ttu-id="1e33d-121">toouse go w aplikacji sieci web platformy Azure lub maszyn wirtualnych, [wybierz rozszerzenia usługi Application Insights hello](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1e33d-121">toouse it in Azure web apps or VMs, [select hello Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="1e33d-122">Można również napisać własny śledzenia kodu za pomocą hello zależności [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="1e33d-122">You can also write your own dependency tracking code using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="1e33d-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e33d-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="1e33d-124">Moduł zbierający wydajności</span><span class="sxs-lookup"><span data-stu-id="1e33d-124">Performance collector</span></span>
<span data-ttu-id="1e33d-125">[Zbiera dane liczników wydajności systemu](app-insights-performance-counters.md) na przykład procesora CPU, pamięci i sieci obciążenia z instalacji usług IIS.</span><span class="sxs-lookup"><span data-stu-id="1e33d-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="1e33d-126">Można określić, które toocollect liczników, łącznie z liczników wydajności, które zostały skonfigurowane samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="1e33d-126">You can specify which counters toocollect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="1e33d-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e33d-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="1e33d-128">Diagnostyka Telemetrię usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="1e33d-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="1e33d-129">Witaj `DiagnosticsTelemetryModule` raporty błędów w hello usługi Application Insights Instrumentacji kodu.</span><span class="sxs-lookup"><span data-stu-id="1e33d-129">hello `DiagnosticsTelemetryModule` reports errors in hello Application Insights instrumentation code itself.</span></span> <span data-ttu-id="1e33d-130">Na przykład jeśli kod hello nie ma dostępu do liczników wydajności lub `ITelemetryInitializer` zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="1e33d-130">For example, if hello code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="1e33d-131">Dane telemetryczne śledzenia śledzone przez ten moduł jest wyświetlana w hello [diagnostycznych wyszukiwania][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="1e33d-131">Trace telemetry tracked by this module appears in hello [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="1e33d-132">Wysyła toodc.services.vsallin.net danych diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="1e33d-132">Sends diagnostic data toodc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="1e33d-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e33d-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="1e33d-134">Zainstalowanie tylko ten pakiet plik ApplicationInsights.config hello nie jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="1e33d-134">If you only install this package, hello ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="1e33d-135">Tryb dewelopera</span><span class="sxs-lookup"><span data-stu-id="1e33d-135">Developer Mode</span></span>
<span data-ttu-id="1e33d-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`Wymusza hello usługi Application Insights `TelemetryChannel` toosend natychmiast danych telemetrii jeden element w czasie, gdy debuger jest dołączony toohello procesu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e33d-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces hello Application Insights `TelemetryChannel` toosend data immediately, one telemetry item at a time, when a debugger is attached toohello application process.</span></span> <span data-ttu-id="1e33d-137">Zmniejsza to hello ilość czasu między hello moment, gdy aplikacja śledzi telemetrii i wyświetlanym na powitania portalu Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1e33d-137">This reduces hello amount of time between hello moment when your application tracks telemetry and when it appears on hello Application Insights portal.</span></span> <span data-ttu-id="1e33d-138">Powoduje znaczne obciążenie procesora CPU i sieci przepustowości.</span><span class="sxs-lookup"><span data-stu-id="1e33d-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="1e33d-139">[Application Insights w systemie Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="1e33d-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="1e33d-140">Śledzenie żądań sieci Web</span><span class="sxs-lookup"><span data-stu-id="1e33d-140">Web Request Tracking</span></span>
<span data-ttu-id="1e33d-141">Raporty hello [kod odpowiedzi czasu i wynik](app-insights-asp-net.md) żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="1e33d-141">Reports hello [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="1e33d-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="1e33d-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="1e33d-143">Śledzenie wyjątków</span><span class="sxs-lookup"><span data-stu-id="1e33d-143">Exception tracking</span></span>
<span data-ttu-id="1e33d-144">`ExceptionTrackingTelemetryModule`śledzi nieobsługiwanych wyjątków w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="1e33d-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="1e33d-145">Zobacz [błędy i wyjątki][exceptions].</span><span class="sxs-lookup"><span data-stu-id="1e33d-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="1e33d-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="1e33d-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="1e33d-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule`-śledzi [być niezauważalna wyjątki zadań](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e33d-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="1e33d-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule`-śledzi nieobsługiwanych wyjątków dla procesu roboczego ról, usług systemu windows i aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="1e33d-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="1e33d-149">[Application Insights w systemie Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e33d-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="1e33d-150">Źródła zdarzeń śledzenia</span><span class="sxs-lookup"><span data-stu-id="1e33d-150">EventSource Tracking</span></span>
<span data-ttu-id="1e33d-151">`EventSourceTelemetryModule`Umożliwia tooconfigure EventSource toobe zdarzenia wysyłane tooApplication Insights jako dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="1e33d-151">`EventSourceTelemetryModule` allows you tooconfigure EventSource events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="1e33d-152">Informacje dotyczące śledzenia zdarzeń źródła zdarzeń, zobacz [za pomocą zdarzeń EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="1e33d-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="1e33d-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="1e33d-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="1e33d-154">Śledzenie zdarzeń ETW.</span><span class="sxs-lookup"><span data-stu-id="1e33d-154">ETW Event Tracking</span></span>
<span data-ttu-id="1e33d-155">`EtwCollectorTelemetryModule`Umożliwia tooconfigure zdarzenia z toobe dostawców ETW wysyłane tooApplication Insights jako dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="1e33d-155">`EtwCollectorTelemetryModule` allows you tooconfigure events from ETW providers toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="1e33d-156">Aby uzyskać informacji na temat śledzenia zdarzeń funkcji ETW, zobacz [przy użyciu zdarzenia ETW](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="1e33d-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="1e33d-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="1e33d-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="1e33d-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="1e33d-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="1e33d-159">Pakiet Microsoft.ApplicationInsights Hello zawiera hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) z hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="1e33d-159">hello Microsoft.ApplicationInsights package provides hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) of hello SDK.</span></span> <span data-ttu-id="1e33d-160">Hello inne moduły danych telemetrycznych użyć tej funkcji i można również [go używać toodefine własne dane telemetryczne](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="1e33d-160">hello other telemetry modules use this, and you can also [use it toodefine your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="1e33d-161">Nie wpisu w ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="1e33d-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="1e33d-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e33d-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="1e33d-163">Po zainstalowaniu właśnie ta NuGet, nie pliku .config jest generowany.</span><span class="sxs-lookup"><span data-stu-id="1e33d-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="1e33d-164">Kanał telemetrii</span><span class="sxs-lookup"><span data-stu-id="1e33d-164">Telemetry Channel</span></span>
<span data-ttu-id="1e33d-165">kanał danych telemetrycznych Hello zarządza buforowania i transmisji toohello telemetrii usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1e33d-165">hello telemetry channel manages buffering and transmission of telemetry toohello Application Insights service.</span></span>

* <span data-ttu-id="1e33d-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`jest hello kanału domyślnego dla usług.</span><span class="sxs-lookup"><span data-stu-id="1e33d-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is hello default channel for services.</span></span> <span data-ttu-id="1e33d-167">Buforuje dane w pamięci.</span><span class="sxs-lookup"><span data-stu-id="1e33d-167">It buffers data in memory.</span></span>
* <span data-ttu-id="1e33d-168">`Microsoft.ApplicationInsights.PersistenceChannel`jest to alternatywa dla aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="1e33d-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="1e33d-169">Każdy magazyn toopersistent unflushed danych może pomóc zaoszczędzić podczas aplikacji zostanie zamknięte w dół i wysyła go po uruchomieniu aplikacji hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="1e33d-169">It can save any unflushed data toopersistent storage when your app closes down, and will send it when hello app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="1e33d-170">Inicjatory telemetrii (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="1e33d-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="1e33d-171">Inicjatory telemetrii ustawiania właściwości kontekstu, które są wysyłane wraz ze wszystkich elementów telemetrii.</span><span class="sxs-lookup"><span data-stu-id="1e33d-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="1e33d-172">Możesz [napisać własny inicjatory](app-insights-api-filtering-sampling.md#add-properties) tooset właściwości kontekstu.</span><span class="sxs-lookup"><span data-stu-id="1e33d-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) tooset context properties.</span></span>

<span data-ttu-id="1e33d-173">Inicjatory standardowe Hello jest ustawiony przez pakietów hello sieci Web lub Windows Server NuGet:</span><span class="sxs-lookup"><span data-stu-id="1e33d-173">hello standard initializers are all set either by hello Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="1e33d-174">`AccountIdTelemetryInitializer`Ustawia właściwość AccountId hello.</span><span class="sxs-lookup"><span data-stu-id="1e33d-174">`AccountIdTelemetryInitializer` sets hello AccountId property.</span></span>
* <span data-ttu-id="1e33d-175">`AuthenticatedUserIdTelemetryInitializer`Ustawia właściwość AuthenticatedUserId hello zgodnie z ustaleniami przez hello JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="1e33d-175">`AuthenticatedUserIdTelemetryInitializer` sets hello AuthenticatedUserId property as set by hello JavaScript SDK.</span></span>
* <span data-ttu-id="1e33d-176">`AzureRoleEnvironmentTelemetryInitializer`aktualizacje hello `RoleName` i `RoleInstance` właściwości hello `Device` kontekst dla wszystkich elementów telemetrii informacjami wyodrębnionymi z hello środowiska uruchomieniowego platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1e33d-176">`AzureRoleEnvironmentTelemetryInitializer` updates hello `RoleName` and `RoleInstance` properties of hello `Device` context for all telemetry items with information extracted from hello Azure runtime environment.</span></span>
* <span data-ttu-id="1e33d-177">`BuildInfoConfigComponentVersionTelemetryInitializer`aktualizacje hello `Version` właściwości hello `Component` kontekst dla wszystkich elementów danych telemetrycznych z wartością hello wyodrębniony z hello `BuildInfo.config` za pomocą MS Build.</span><span class="sxs-lookup"><span data-stu-id="1e33d-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates hello `Version` property of hello `Component` context for all telemetry items with hello value extracted from hello `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="1e33d-178">`ClientIpHeaderTelemetryInitializer`aktualizacje `Ip` właściwości hello `Location` kontekstu wszystkich elementów telemetrii oparte na powitania `X-Forwarded-For` nagłówka HTTP hello żądania.</span><span class="sxs-lookup"><span data-stu-id="1e33d-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of hello `Location` context of all telemetry items based on hello `X-Forwarded-For` HTTP header of hello request.</span></span>
* <span data-ttu-id="1e33d-179">`DeviceTelemetryInitializer`następujące właściwości hello hello aktualizacje `Device` kontekst dla wszystkich elementów telemetrii.</span><span class="sxs-lookup"><span data-stu-id="1e33d-179">`DeviceTelemetryInitializer` updates hello following properties of hello `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="1e33d-180">`Type`ustawiono zbyt "Komputer"</span><span class="sxs-lookup"><span data-stu-id="1e33d-180">`Type` is set too"PC"</span></span>
  * <span data-ttu-id="1e33d-181">`Id`ustawiono toohello nazwa domeny komputera hello którym hello aplikacji sieci web jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="1e33d-181">`Id` is set toohello domain name of hello computer where hello web application is running.</span></span>
  * <span data-ttu-id="1e33d-182">`OemName`ustawiono wartość toohello wyodrębniony z hello `Win32_ComputerSystem.Manufacturer` pola przy użyciu usługi WMI.</span><span class="sxs-lookup"><span data-stu-id="1e33d-182">`OemName` is set toohello value extracted from hello `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="1e33d-183">`Model`ustawiono wartość toohello wyodrębniony z hello `Win32_ComputerSystem.Model` pola przy użyciu usługi WMI.</span><span class="sxs-lookup"><span data-stu-id="1e33d-183">`Model` is set toohello value extracted from hello `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="1e33d-184">`NetworkType`ustawiono wartość toohello wyodrębniony z hello `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="1e33d-184">`NetworkType` is set toohello value extracted from hello `NetworkInterface`.</span></span>
  * <span data-ttu-id="1e33d-185">`Language`ustawiono nazwę toohello hello `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="1e33d-185">`Language` is set toohello name of hello `CurrentCulture`.</span></span>
* <span data-ttu-id="1e33d-186">`DomainNameRoleInstanceTelemetryInitializer`aktualizacje hello `RoleInstance` właściwości hello `Device` kontekst dla wszystkich elementów danych telemetrycznych z nazwą domeny hello hello komputera, którym jest uruchomiona aplikacja sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="1e33d-186">`DomainNameRoleInstanceTelemetryInitializer` updates hello `RoleInstance` property of hello `Device` context for all telemetry items with hello domain name of hello computer where hello web application is running.</span></span>
* <span data-ttu-id="1e33d-187">`OperationNameTelemetryInitializer`aktualizacje hello `Name` właściwości hello `RequestTelemetry` i hello `Name` właściwości hello `Operation` kontekstu wszystkich elementów telemetrii w oparciu metody hello HTTP, jak również nazwy hello wywołanej tooprocess ASP.NET MVC kontroler i Akcja żądanie.</span><span class="sxs-lookup"><span data-stu-id="1e33d-187">`OperationNameTelemetryInitializer` updates hello `Name` property of hello `RequestTelemetry` and hello `Name` property of hello `Operation` context of all telemetry items based on hello HTTP method, as well as names of ASP.NET MVC controller and action invoked tooprocess hello request.</span></span>
* <span data-ttu-id="1e33d-188">`OperationIdTelemetryInitializer`lub `OperationCorrelationTelemetryInitializer` hello aktualizacje `Operation.Id` właściwości kontekstu wszystkich elementów telemetrii śledzone podczas obsługi żądania z hello są generowane automatycznie `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="1e33d-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates hello `Operation.Id` context property of all telemetry items tracked while handling a request with hello automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="1e33d-189">`SessionTelemetryInitializer`aktualizacje hello `Id` właściwości hello `Session` kontekst dla wszystkich elementów danych telemetrycznych z wartością wyodrębniony z hello `ai_session` pliku cookie generowane przez hello kod Instrumentacji ApplicationInsights JavaScript uruchomiony w przeglądarce użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="1e33d-189">`SessionTelemetryInitializer` updates hello `Id` property of hello `Session` context for all telemetry items with value extracted from hello `ai_session` cookie generated by hello ApplicationInsights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="1e33d-190">`SyntheticTelemetryInitializer`lub `SyntheticUserAgentTelemetryInitializer` hello aktualizacje `User`, `Session` i `Operation` kontekstów właściwości wszystkich elementów telemetrii śledzone podczas przetwarzania żądania z syntetycznego źródła, takich jak dostępności testu lub bot aparatu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1e33d-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates hello `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="1e33d-191">Domyślnie [Eksploratora metryk](app-insights-metrics-explorer.md) syntetycznych telemetrii nie są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="1e33d-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="1e33d-192">Witaj `<Filters>` ustawić identyfikowanie właściwości hello żądań.</span><span class="sxs-lookup"><span data-stu-id="1e33d-192">hello `<Filters>` set identifying properties of hello requests.</span></span>
* <span data-ttu-id="1e33d-193">`UserAgentTelemetryInitializer`aktualizacje hello `UserAgent` właściwości hello `User` kontekstu wszystkich elementów telemetrii oparte na powitania `User-Agent` nagłówka HTTP hello żądania.</span><span class="sxs-lookup"><span data-stu-id="1e33d-193">`UserAgentTelemetryInitializer` updates hello `UserAgent` property of hello `User` context of all telemetry items based on hello `User-Agent` HTTP header of hello request.</span></span>
* <span data-ttu-id="1e33d-194">`UserTelemetryInitializer`aktualizacje hello `Id` i `AcquisitionDate` właściwości `User` kontekst dla wszystkich elementów danych telemetrycznych z wartościami wyodrębniony z hello `ai_user` wygenerowane przez kod Instrumentacji JavaScript Insights aplikacji hello działający w hello pliku cookie przeglądarki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1e33d-194">`UserTelemetryInitializer` updates hello `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from hello `ai_user` cookie generated by hello Application Insights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="1e33d-195">`WebTestTelemetryInitializer`Ustawia hello identyfikatora użytkownika, identyfikator sesji i właściwości syntetycznego źródła dla tego dostarczanych w żądaniach HTTP [testów dostępności](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="1e33d-195">`WebTestTelemetryInitializer` sets hello user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="1e33d-196">Witaj `<Filters>` ustawić identyfikowanie właściwości hello żądań.</span><span class="sxs-lookup"><span data-stu-id="1e33d-196">hello `<Filters>` set identifying properties of hello requests.</span></span>

<span data-ttu-id="1e33d-197">Dla aplikacji .NET działających w sieci szkieletowej usług, mogą obejmować hello `Microsoft.ApplicationInsights.ServiceFabric` pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e33d-197">For .NET applications running in Service Fabric, you can include hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="1e33d-198">Ten pakiet zawiera `FabricTelemetryInitializer`, która dodaje elementy tootelemetry właściwości sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="1e33d-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties tootelemetry items.</span></span> <span data-ttu-id="1e33d-199">Aby uzyskać więcej informacji, zobacz hello [GitHub strony](https://go.microsoft.com/fwlink/?linkid=848457) o właściwości hello dodane przez ten pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e33d-199">For more information, see hello [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about hello properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="1e33d-200">Dane telemetryczne procesorów (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="1e33d-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="1e33d-201">Procesory telemetrii można filtrować i zmodyfikować każdy element telemetrii tuż przed wysłaniem hello SDK toohello portalu.</span><span class="sxs-lookup"><span data-stu-id="1e33d-201">Telemetry processors can filter and modify each telemetry item just before it is sent from hello SDK toohello portal.</span></span>

<span data-ttu-id="1e33d-202">Możesz [zapisu procesorów telemetrii](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="1e33d-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="1e33d-203">Procesor telemetrii próbkowania adaptacyjną (od 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="1e33d-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="1e33d-204">Ta opcja jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="1e33d-204">This is enabled by default.</span></span> <span data-ttu-id="1e33d-205">Jeśli aplikacja wyśle dużej ilości danych telemetrii, spowoduje usunięcie tego procesora, część z nich.</span><span class="sxs-lookup"><span data-stu-id="1e33d-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="1e33d-206">Hello parametru zapewnia hello docelowego, który algorytm hello próbuje tooachieve.</span><span class="sxs-lookup"><span data-stu-id="1e33d-206">hello parameter provides hello target that hello algorithm tries tooachieve.</span></span> <span data-ttu-id="1e33d-207">Każde wystąpienie hello SDK działa niezależnie, więc jeśli serwer działa w klastrze kilka maszyn, hello rzeczywista ilość danych telemetrycznych będzie mnożona odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="1e33d-207">Each instance of hello SDK works independently, so if your server is a cluster of several machines, hello actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="1e33d-208">[Dowiedz się więcej o próbkowania](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="1e33d-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="1e33d-209">Procesor telemetrii stałej częstotliwość próbkowania (od 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="1e33d-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="1e33d-210">Istnieje również standard [próbkowanie procesora telemetrii](app-insights-api-filtering-sampling.md) (od 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="1e33d-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="1e33d-211">Parametrów kanału (Java)</span><span class="sxs-lookup"><span data-stu-id="1e33d-211">Channel parameters (Java)</span></span>
<span data-ttu-id="1e33d-212">Te parametry wpływa na sposób hello zestawu Java SDK powinien przechowywania i opróżniania danych telemetrycznych hello zbierane.</span><span class="sxs-lookup"><span data-stu-id="1e33d-212">These parameters affect how hello Java SDK should store and flush hello telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="1e33d-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="1e33d-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="1e33d-214">Witaj liczba elementów dane telemetryczne, które mogą być przechowywane w magazynie w pamięci hello SDK.</span><span class="sxs-lookup"><span data-stu-id="1e33d-214">hello number of telemetry items that can be stored in hello SDK's in-memory storage.</span></span> <span data-ttu-id="1e33d-215">Po osiągnięciu tej liczby hello telemetrii bufor jest opróżniany — oznacza to, elementy telemetrii hello wysyłane są toohello serwera usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1e33d-215">When this number is reached, hello telemetry buffer is flushed - that is, hello telemetry items are sent toohello Application Insights server.</span></span>

* <span data-ttu-id="1e33d-216">Min: 1</span><span class="sxs-lookup"><span data-stu-id="1e33d-216">Min: 1</span></span>
* <span data-ttu-id="1e33d-217">Maksymalna liczba: 1000</span><span class="sxs-lookup"><span data-stu-id="1e33d-217">Max: 1000</span></span>
* <span data-ttu-id="1e33d-218">Domyślne: 500</span><span class="sxs-lookup"><span data-stu-id="1e33d-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="1e33d-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="1e33d-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="1e33d-220">Określa, jak często hello danych przechowywanych w magazynie w pamięci hello powinny być wyczyszczone (wysłane tooApplication szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="1e33d-220">Determines how often hello data that is stored in hello in-memory storage should be flushed (sent tooApplication Insights).</span></span>

* <span data-ttu-id="1e33d-221">Min: 1</span><span class="sxs-lookup"><span data-stu-id="1e33d-221">Min: 1</span></span>
* <span data-ttu-id="1e33d-222">Maksymalna liczba: 300</span><span class="sxs-lookup"><span data-stu-id="1e33d-222">Max: 300</span></span>
* <span data-ttu-id="1e33d-223">Domyślne: 5</span><span class="sxs-lookup"><span data-stu-id="1e33d-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="1e33d-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="1e33d-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="1e33d-225">Określa maksymalny rozmiar hello w Megabajtach, który jest przydzielony toohello magazynu trwałego na dysku lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="1e33d-225">Determines hello maximum size in MB that is allotted toohello persistent storage on hello local disk.</span></span> <span data-ttu-id="1e33d-226">Magazyn ten jest używany dla trwałych elementów telemetrii, których nie powiodła się punkt końcowy usługi Application Insights toohello toobe przesyłane.</span><span class="sxs-lookup"><span data-stu-id="1e33d-226">This storage is used for persisting telemetry items that failed toobe transmitted toohello Application Insights endpoint.</span></span> <span data-ttu-id="1e33d-227">Po spełnieniu rozmiar magazynu hello nowych elementów telemetrii zostaną odrzucone.</span><span class="sxs-lookup"><span data-stu-id="1e33d-227">When hello storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="1e33d-228">Min: 1</span><span class="sxs-lookup"><span data-stu-id="1e33d-228">Min: 1</span></span>
* <span data-ttu-id="1e33d-229">Maksymalna: 100</span><span class="sxs-lookup"><span data-stu-id="1e33d-229">Max: 100</span></span>
* <span data-ttu-id="1e33d-230">Domyślny: 10</span><span class="sxs-lookup"><span data-stu-id="1e33d-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="1e33d-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="1e33d-231">InstrumentationKey</span></span>
<span data-ttu-id="1e33d-232">Określa hello zasobu usługi Application Insights, w którym dane są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="1e33d-232">This determines hello Application Insights resource in which your data appears.</span></span> <span data-ttu-id="1e33d-233">Zwykle tworzenia oddzielnych zasobu, za pomocą osobnych klucza dla poszczególnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e33d-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="1e33d-234">Jeśli chcesz tooset hello klucz dynamicznie — na przykład jeśli chcesz toosend wyników z Twoich zasobów toodifferent aplikacji — można pominąć hello klucz z pliku konfiguracji hello i ustaw go w kodzie.</span><span class="sxs-lookup"><span data-stu-id="1e33d-234">If you want tooset hello key dynamically - for example if you want toosend results from your application toodifferent resources - you can omit hello key from hello configuration file, and set it in code instead.</span></span>

<span data-ttu-id="1e33d-235">tooset hello klucza dla wszystkich wystąpień TelemetryClient moduły standardowe telemetrii ustawić klucza hello TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="1e33d-235">tooset hello key for all instances of TelemetryClient, including standard telemetry modules, set hello key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="1e33d-236">Wykonaj następujące czynności w metodzie inicjowania, takich jak pliku global.aspx.cs w usługi ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="1e33d-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="1e33d-237">Wystarczy toosend określony zbiór zdarzenia tooa innego zasobu, można ustawić klucza hello dla określonych TelemetryClient:</span><span class="sxs-lookup"><span data-stu-id="1e33d-237">If you just want toosend a specific set of events tooa different resource, you can set hello key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="1e33d-238">nowy klucz tooget [utworzyć nowy zasób w portalu usługi Application Insights hello][new].</span><span class="sxs-lookup"><span data-stu-id="1e33d-238">tooget a new key, [create a new resource in hello Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e33d-239">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e33d-239">Next steps</span></span>
<span data-ttu-id="1e33d-240">[Dowiedz się więcej o hello interfejsu API][api].</span><span class="sxs-lookup"><span data-stu-id="1e33d-240">[Learn more about hello API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
