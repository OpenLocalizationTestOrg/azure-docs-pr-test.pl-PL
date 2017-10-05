---
title: "Odwołanie ApplicationInsights.config - Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 7737f47d4181b5e920434f3a5372991efb58f63e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-the-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="e0d98-103">Konfigurowanie zestawu SDK usługi Application Insights za pomocą pliku ApplicationInsights.config lub xml</span><span class="sxs-lookup"><span data-stu-id="e0d98-103">Configuring the Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="e0d98-104">Zestaw SDK usługi Application Insights .NET składa się z liczby pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="e0d98-104">The Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="e0d98-105">[Pakiet podstawowy](http://www.nuget.org/packages/Microsoft.ApplicationInsights) udostępnia interfejs API wysyłania danych telemetrycznych do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e0d98-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides the API for sending telemetry to the Application Insights.</span></span> <span data-ttu-id="e0d98-106">[Dodatkowe pakiety](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) Podaj dane telemetryczne *modułów* i *inicjatory* automatycznie śledzenia dane telemetryczne z aplikacji i jej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="e0d98-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="e0d98-107">Dostosowując plik konfiguracji, można włączyć lub wyłączyć inicjatory i moduły danych telemetrycznych i ustaw parametry dla niektórych z nich.</span><span class="sxs-lookup"><span data-stu-id="e0d98-107">By adjusting the configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="e0d98-108">Plik konfiguracji ma nazwę `ApplicationInsights.config` lub `ApplicationInsights.xml`, w zależności od typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0d98-108">The configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on the type of your application.</span></span> <span data-ttu-id="e0d98-109">Jest automatycznie dodawany do projektu po możesz [zainstalować większość wersji zestawu SDK][start].</span><span class="sxs-lookup"><span data-stu-id="e0d98-109">It is automatically added to your project when you [install most versions of the SDK][start].</span></span> <span data-ttu-id="e0d98-110">Jest także dodawane do aplikacji sieci web przez [Monitor stanu na serwerze IIS][redfield], lub po wybraniu Appplication Insights [rozszerzenia dla witryny sieci Web platformy Azure lub wirtualna](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="e0d98-110">It is also added to a web app by [Status Monitor on an IIS server][redfield], or when you select the Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="e0d98-111">Nie ma równoważny plik do kontroli [SDK na stronie sieci web][client].</span><span class="sxs-lookup"><span data-stu-id="e0d98-111">There isn't an equivalent file to control the [SDK in a web page][client].</span></span>

<span data-ttu-id="e0d98-112">W tym dokumencie opisano sekcje, które widać w konfiguracji plików i sposobu ich kontrolowania składniki zestawu SDK, i które pakiety NuGet obciążenia tych składników.</span><span class="sxs-lookup"><span data-stu-id="e0d98-112">This document describes the sections you see in the configuration file, how they control the components of the SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="e0d98-113">Moduły danych telemetrycznych (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="e0d98-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="e0d98-114">Każdy moduł telemetrii zbiera określonego typu danych i wysyła dane przy użyciu core interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e0d98-114">Each telemetry module collects a specific type of data and uses the core API to send the data.</span></span> <span data-ttu-id="e0d98-115">Moduły są instalowane przez różne pakiety NuGet, które również dodać wymagane wiersze do pliku .config.</span><span class="sxs-lookup"><span data-stu-id="e0d98-115">The modules are installed by different NuGet packages, which also add the required lines to the .config file.</span></span>

<span data-ttu-id="e0d98-116">Brak węzła w pliku konfiguracji dla każdego modułu.</span><span class="sxs-lookup"><span data-stu-id="e0d98-116">There's a node in the configuration file for each module.</span></span> <span data-ttu-id="e0d98-117">Aby wyłączyć moduł, Usuń węzeł lub komentarz go.</span><span class="sxs-lookup"><span data-stu-id="e0d98-117">To disable a module, delete the node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="e0d98-118">Śledzenia zależności</span><span class="sxs-lookup"><span data-stu-id="e0d98-118">Dependency Tracking</span></span>
<span data-ttu-id="e0d98-119">[Śledzenia zależności](app-insights-asp-net-dependencies.md) zbiera dane telemetryczne dotyczące wywołania aplikacji sprawia, że do baz danych i baz danych i usług zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="e0d98-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes to databases and external services and databases.</span></span> <span data-ttu-id="e0d98-120">Aby umożliwić tego modułu do pracy w serwerze IIS, musisz [Zainstaluj Monitor stanu][redfield].</span><span class="sxs-lookup"><span data-stu-id="e0d98-120">To allow this module to work in an IIS server, you need to [install Status Monitor][redfield].</span></span> <span data-ttu-id="e0d98-121">Aby użyć go w aplikacji sieci web platformy Azure lub maszyn wirtualnych, [wybierz rozszerzenia usługi Application Insights](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="e0d98-121">To use it in Azure web apps or VMs, [select the Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="e0d98-122">Można również napisać własny zależności śledzenia kodu za pomocą [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="e0d98-122">You can also write your own dependency tracking code using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="e0d98-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e0d98-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="e0d98-124">Moduł zbierający wydajności</span><span class="sxs-lookup"><span data-stu-id="e0d98-124">Performance collector</span></span>
<span data-ttu-id="e0d98-125">[Zbiera dane liczników wydajności systemu](app-insights-performance-counters.md) na przykład procesora CPU, pamięci i sieci obciążenia z instalacji usług IIS.</span><span class="sxs-lookup"><span data-stu-id="e0d98-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="e0d98-126">Można określić które liczniki do zbierania, łącznie z liczników wydajności, które zostały skonfigurowane samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="e0d98-126">You can specify which counters to collect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="e0d98-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e0d98-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="e0d98-128">Diagnostyka Telemetrię usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0d98-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="e0d98-129">`DiagnosticsTelemetryModule` Raporty błędów w kodzie Instrumentacji usługi Application Insights samej siebie.</span><span class="sxs-lookup"><span data-stu-id="e0d98-129">The `DiagnosticsTelemetryModule` reports errors in the Application Insights instrumentation code itself.</span></span> <span data-ttu-id="e0d98-130">Na przykład jeśli kod nie może uzyskać dostępu do liczników wydajności lub `ITelemetryInitializer` zgłasza wyjątek.</span><span class="sxs-lookup"><span data-stu-id="e0d98-130">For example, if the code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="e0d98-131">Dane telemetryczne śledzenia śledzone przez ten moduł jest wyświetlana w [diagnostycznych wyszukiwania][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="e0d98-131">Trace telemetry tracked by this module appears in the [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="e0d98-132">Wysyła dane diagnostyczne do dc.services.vsallin.net.</span><span class="sxs-lookup"><span data-stu-id="e0d98-132">Sends diagnostic data to dc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="e0d98-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e0d98-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="e0d98-134">Po zainstalowaniu tylko ten pakiet, plik ApplicationInsights.config nie jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="e0d98-134">If you only install this package, the ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="e0d98-135">Tryb dewelopera</span><span class="sxs-lookup"><span data-stu-id="e0d98-135">Developer Mode</span></span>
<span data-ttu-id="e0d98-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`Wymusza usługi Application Insights `TelemetryChannel` Aby wysłać dane od razu, telemetrii jeden element w czasie, gdy debuger jest dołączony do procesu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0d98-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces the Application Insights `TelemetryChannel` to send data immediately, one telemetry item at a time, when a debugger is attached to the application process.</span></span> <span data-ttu-id="e0d98-137">Zmniejsza to ilość czasu od chwili, gdy aplikacja śledzi telemetrii i wyświetlanym na portalu Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e0d98-137">This reduces the amount of time between the moment when your application tracks telemetry and when it appears on the Application Insights portal.</span></span> <span data-ttu-id="e0d98-138">Powoduje znaczne obciążenie procesora CPU i sieci przepustowości.</span><span class="sxs-lookup"><span data-stu-id="e0d98-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="e0d98-139">[Application Insights w systemie Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="e0d98-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="e0d98-140">Śledzenie żądań sieci Web</span><span class="sxs-lookup"><span data-stu-id="e0d98-140">Web Request Tracking</span></span>
<span data-ttu-id="e0d98-141">Raporty [kod odpowiedzi czasu i wynik](app-insights-asp-net.md) żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="e0d98-141">Reports the [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="e0d98-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="e0d98-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="e0d98-143">Śledzenie wyjątków</span><span class="sxs-lookup"><span data-stu-id="e0d98-143">Exception tracking</span></span>
<span data-ttu-id="e0d98-144">`ExceptionTrackingTelemetryModule`śledzi nieobsługiwanych wyjątków w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e0d98-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="e0d98-145">Zobacz [błędy i wyjątki][exceptions].</span><span class="sxs-lookup"><span data-stu-id="e0d98-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="e0d98-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="e0d98-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="e0d98-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule`-śledzi [być niezauważalna wyjątki zadań](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0d98-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="e0d98-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule`-śledzi nieobsługiwanych wyjątków dla procesu roboczego ról, usług systemu windows i aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="e0d98-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="e0d98-149">[Application Insights w systemie Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e0d98-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="e0d98-150">Źródła zdarzeń śledzenia</span><span class="sxs-lookup"><span data-stu-id="e0d98-150">EventSource Tracking</span></span>
<span data-ttu-id="e0d98-151">`EventSourceTelemetryModule`Umożliwia skonfigurowanie EventSource zdarzenia mają być wysyłane do usługi Application Insights jako dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="e0d98-151">`EventSourceTelemetryModule` allows you to configure EventSource events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="e0d98-152">Informacje dotyczące śledzenia zdarzeń źródła zdarzeń, zobacz [za pomocą zdarzeń EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="e0d98-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="e0d98-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="e0d98-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="e0d98-154">Śledzenie zdarzeń ETW.</span><span class="sxs-lookup"><span data-stu-id="e0d98-154">ETW Event Tracking</span></span>
<span data-ttu-id="e0d98-155">`EtwCollectorTelemetryModule`Umożliwia skonfigurowanie zdarzeń od dostawcy ETW do wysłania do usługi Application Insights jako dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="e0d98-155">`EtwCollectorTelemetryModule` allows you to configure events from ETW providers to be sent to Application Insights as traces.</span></span> <span data-ttu-id="e0d98-156">Aby uzyskać informacji na temat śledzenia zdarzeń funkcji ETW, zobacz [przy użyciu zdarzenia ETW](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="e0d98-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="e0d98-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="e0d98-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="e0d98-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="e0d98-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="e0d98-159">Udostępnia pakiet Microsoft.ApplicationInsights [core API](https://msdn.microsoft.com/library/mt420197.aspx) zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="e0d98-159">The Microsoft.ApplicationInsights package provides the [core API](https://msdn.microsoft.com/library/mt420197.aspx) of the SDK.</span></span> <span data-ttu-id="e0d98-160">Użyj innych modułów telemetrii i można również [użyj go do zdefiniowania własnych telemetrii](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e0d98-160">The other telemetry modules use this, and you can also [use it to define your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="e0d98-161">Nie wpisu w ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="e0d98-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="e0d98-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e0d98-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="e0d98-163">Po zainstalowaniu właśnie ta NuGet, nie pliku .config jest generowany.</span><span class="sxs-lookup"><span data-stu-id="e0d98-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="e0d98-164">Kanał telemetrii</span><span class="sxs-lookup"><span data-stu-id="e0d98-164">Telemetry Channel</span></span>
<span data-ttu-id="e0d98-165">Kanał danych telemetrycznych zarządza buforowania i przekazywania telemetrii usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e0d98-165">The telemetry channel manages buffering and transmission of telemetry to the Application Insights service.</span></span>

* <span data-ttu-id="e0d98-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`jest domyślnym kanale dla usług.</span><span class="sxs-lookup"><span data-stu-id="e0d98-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is the default channel for services.</span></span> <span data-ttu-id="e0d98-167">Buforuje dane w pamięci.</span><span class="sxs-lookup"><span data-stu-id="e0d98-167">It buffers data in memory.</span></span>
* <span data-ttu-id="e0d98-168">`Microsoft.ApplicationInsights.PersistenceChannel`jest to alternatywa dla aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="e0d98-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="e0d98-169">Gdy aplikacji zostanie zamknięte w dół i wysyła go po uruchomieniu aplikacji ponownie może pomóc zaoszczędzić unflushed danych do magazynu trwałego.</span><span class="sxs-lookup"><span data-stu-id="e0d98-169">It can save any unflushed data to persistent storage when your app closes down, and will send it when the app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="e0d98-170">Inicjatory telemetrii (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="e0d98-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="e0d98-171">Inicjatory telemetrii ustawiania właściwości kontekstu, które są wysyłane wraz ze wszystkich elementów telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e0d98-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="e0d98-172">Możesz [napisać własny inicjatory](app-insights-api-filtering-sampling.md#add-properties) można ustawić właściwości kontekstu.</span><span class="sxs-lookup"><span data-stu-id="e0d98-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) to set context properties.</span></span>

<span data-ttu-id="e0d98-173">Inicjatory standardowe jest ustawiony przez pakiety sieci Web lub Windows Server NuGet:</span><span class="sxs-lookup"><span data-stu-id="e0d98-173">The standard initializers are all set either by the Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="e0d98-174">`AccountIdTelemetryInitializer`Ustawia właściwość AccountId.</span><span class="sxs-lookup"><span data-stu-id="e0d98-174">`AccountIdTelemetryInitializer` sets the AccountId property.</span></span>
* <span data-ttu-id="e0d98-175">`AuthenticatedUserIdTelemetryInitializer`Ustawia właściwość AuthenticatedUserId zgodnie z ustawieniami JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="e0d98-175">`AuthenticatedUserIdTelemetryInitializer` sets the AuthenticatedUserId property as set by the JavaScript SDK.</span></span>
* <span data-ttu-id="e0d98-176">`AzureRoleEnvironmentTelemetryInitializer`aktualizacje `RoleName` i `RoleInstance` właściwości `Device` kontekst dla wszystkich elementów telemetrii informacjami wyodrębnionymi z środowiska uruchomieniowego platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e0d98-176">`AzureRoleEnvironmentTelemetryInitializer` updates the `RoleName` and `RoleInstance` properties of the `Device` context for all telemetry items with information extracted from the Azure runtime environment.</span></span>
* <span data-ttu-id="e0d98-177">`BuildInfoConfigComponentVersionTelemetryInitializer`aktualizacje `Version` właściwość `Component` kontekst dla wszystkich elementów danych telemetrycznych z wartością wyodrębniony z `BuildInfo.config` za pomocą MS Build.</span><span class="sxs-lookup"><span data-stu-id="e0d98-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates the `Version` property of the `Component` context for all telemetry items with the value extracted from the `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="e0d98-178">`ClientIpHeaderTelemetryInitializer`aktualizacje `Ip` właściwość `Location` na podstawie kontekstu wszystkich elementów telemetrii `X-Forwarded-For` nagłówka HTTP żądania.</span><span class="sxs-lookup"><span data-stu-id="e0d98-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of the `Location` context of all telemetry items based on the `X-Forwarded-For` HTTP header of the request.</span></span>
* <span data-ttu-id="e0d98-179">`DeviceTelemetryInitializer`aktualizacje następujących właściwości `Device` kontekst dla wszystkich elementów telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e0d98-179">`DeviceTelemetryInitializer` updates the following properties of the `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="e0d98-180">`Type`ma ustawioną wartość "Komputer"</span><span class="sxs-lookup"><span data-stu-id="e0d98-180">`Type` is set to "PC"</span></span>
  * <span data-ttu-id="e0d98-181">`Id`ustawiono nazwę domeny komputera, na którym działa aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="e0d98-181">`Id` is set to the domain name of the computer where the web application is running.</span></span>
  * <span data-ttu-id="e0d98-182">`OemName`ma ustawioną wartość wyodrębniony z `Win32_ComputerSystem.Manufacturer` pola przy użyciu usługi WMI.</span><span class="sxs-lookup"><span data-stu-id="e0d98-182">`OemName` is set to the value extracted from the `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="e0d98-183">`Model`ma ustawioną wartość wyodrębniony z `Win32_ComputerSystem.Model` pola przy użyciu usługi WMI.</span><span class="sxs-lookup"><span data-stu-id="e0d98-183">`Model` is set to the value extracted from the `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="e0d98-184">`NetworkType`ma ustawioną wartość wyodrębniony z `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="e0d98-184">`NetworkType` is set to the value extracted from the `NetworkInterface`.</span></span>
  * <span data-ttu-id="e0d98-185">`Language`ustawiono nazwę `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="e0d98-185">`Language` is set to the name of the `CurrentCulture`.</span></span>
* <span data-ttu-id="e0d98-186">`DomainNameRoleInstanceTelemetryInitializer`aktualizacje `RoleInstance` właściwość `Device` kontekst dla wszystkich elementów danych telemetrycznych z nazwą domeny komputera, na którym działa aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="e0d98-186">`DomainNameRoleInstanceTelemetryInitializer` updates the `RoleInstance` property of the `Device` context for all telemetry items with the domain name of the computer where the web application is running.</span></span>
* <span data-ttu-id="e0d98-187">`OperationNameTelemetryInitializer`aktualizacje `Name` właściwość `RequestTelemetry` i `Name` właściwość `Operation` kontekstu wszystkich elementów telemetrii oparte na metodę HTTP, jak również nazwy platformy ASP.NET MVC kontroler i akcja wywoływane w celu przetworzenia żądania.</span><span class="sxs-lookup"><span data-stu-id="e0d98-187">`OperationNameTelemetryInitializer` updates the `Name` property of the `RequestTelemetry` and the `Name` property of the `Operation` context of all telemetry items based on the HTTP method, as well as names of ASP.NET MVC controller and action invoked to process the request.</span></span>
* <span data-ttu-id="e0d98-188">`OperationIdTelemetryInitializer`lub `OperationCorrelationTelemetryInitializer` aktualizacje `Operation.Id` właściwości kontekstu wszystkich elementów telemetrii śledzone podczas obsługi żądania z automatycznie wygenerowanym `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="e0d98-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates the `Operation.Id` context property of all telemetry items tracked while handling a request with the automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="e0d98-189">`SessionTelemetryInitializer`aktualizacje `Id` właściwość `Session` kontekst dla wszystkich elementów danych telemetrycznych z wartością wyodrębniony z `ai_session` wygenerowane przez kod Instrumentacji ApplicationInsights JavaScript w przeglądarce plików cookie.</span><span class="sxs-lookup"><span data-stu-id="e0d98-189">`SessionTelemetryInitializer` updates the `Id` property of the `Session` context for all telemetry items with value extracted from the `ai_session` cookie generated by the ApplicationInsights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="e0d98-190">`SyntheticTelemetryInitializer`lub `SyntheticUserAgentTelemetryInitializer` aktualizacje `User`, `Session` i `Operation` kontekstów właściwości wszystkich elementów telemetrii śledzone podczas przetwarzania żądania z syntetycznego źródła, takich jak dostępności testu lub bot aparatu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="e0d98-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates the `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="e0d98-191">Domyślnie [Eksploratora metryk](app-insights-metrics-explorer.md) syntetycznych telemetrii nie są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="e0d98-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="e0d98-192">`<Filters>` Ustawić identyfikowanie właściwości żądania.</span><span class="sxs-lookup"><span data-stu-id="e0d98-192">The `<Filters>` set identifying properties of the requests.</span></span>
* <span data-ttu-id="e0d98-193">`UserAgentTelemetryInitializer`aktualizacje `UserAgent` właściwość `User` na podstawie kontekstu wszystkich elementów telemetrii `User-Agent` nagłówka HTTP żądania.</span><span class="sxs-lookup"><span data-stu-id="e0d98-193">`UserAgentTelemetryInitializer` updates the `UserAgent` property of the `User` context of all telemetry items based on the `User-Agent` HTTP header of the request.</span></span>
* <span data-ttu-id="e0d98-194">`UserTelemetryInitializer`aktualizacje `Id` i `AcquisitionDate` właściwości `User` kontekst dla wszystkich elementów danych telemetrycznych z wartościami wyodrębniony z `ai_user` wygenerowane przez kod instrumentacji aplikacji JavaScript wgląd w użytkownika w pliku cookie Przeglądarka.</span><span class="sxs-lookup"><span data-stu-id="e0d98-194">`UserTelemetryInitializer` updates the `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from the `ai_user` cookie generated by the Application Insights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="e0d98-195">`WebTestTelemetryInitializer`Ustawia identyfikator użytkownika, identyfikator sesji i właściwości syntetycznego źródła dla tego dostarczanych w żądaniach HTTP [testów dostępności](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="e0d98-195">`WebTestTelemetryInitializer` sets the user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="e0d98-196">`<Filters>` Ustawić identyfikowanie właściwości żądania.</span><span class="sxs-lookup"><span data-stu-id="e0d98-196">The `<Filters>` set identifying properties of the requests.</span></span>

<span data-ttu-id="e0d98-197">Dla aplikacji .NET działających w sieci szkieletowej usług, można dołączyć `Microsoft.ApplicationInsights.ServiceFabric` pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e0d98-197">For .NET applications running in Service Fabric, you can include the `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="e0d98-198">Ten pakiet zawiera `FabricTelemetryInitializer`, która dodaje właściwości sieci szkieletowej usług do elementów telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e0d98-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties to telemetry items.</span></span> <span data-ttu-id="e0d98-199">Aby uzyskać więcej informacji, zobacz [GitHub strony](https://go.microsoft.com/fwlink/?linkid=848457) o właściwościach dodane przez ten pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="e0d98-199">For more information, see the [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about the properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="e0d98-200">Dane telemetryczne procesorów (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="e0d98-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="e0d98-201">Dane telemetryczne procesorów można filtrować i zmodyfikować każdy element telemetrii tuż przed wysłaniem z zestawu SDK do portalu.</span><span class="sxs-lookup"><span data-stu-id="e0d98-201">Telemetry processors can filter and modify each telemetry item just before it is sent from the SDK to the portal.</span></span>

<span data-ttu-id="e0d98-202">Możesz [zapisu procesorów telemetrii](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="e0d98-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="e0d98-203">Procesor telemetrii próbkowania adaptacyjną (od 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="e0d98-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="e0d98-204">Ta opcja jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="e0d98-204">This is enabled by default.</span></span> <span data-ttu-id="e0d98-205">Jeśli aplikacja wyśle dużej ilości danych telemetrii, spowoduje usunięcie tego procesora, część z nich.</span><span class="sxs-lookup"><span data-stu-id="e0d98-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="e0d98-206">Parametr zawiera element docelowy, który algorytm próbuje osiągnąć.</span><span class="sxs-lookup"><span data-stu-id="e0d98-206">The parameter provides the target that the algorithm tries to achieve.</span></span> <span data-ttu-id="e0d98-207">Każde wystąpienie zestawu SDK działa niezależnie, więc jeśli serwer działa w klastrze kilka maszyn, rzeczywista ilość danych telemetrycznych będzie mnożona odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="e0d98-207">Each instance of the SDK works independently, so if your server is a cluster of several machines, the actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="e0d98-208">[Dowiedz się więcej o próbkowania](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="e0d98-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="e0d98-209">Procesor telemetrii stałej częstotliwość próbkowania (od 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="e0d98-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="e0d98-210">Istnieje również standard [próbkowanie procesora telemetrii](app-insights-api-filtering-sampling.md) (od 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="e0d98-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="e0d98-211">Parametrów kanału (Java)</span><span class="sxs-lookup"><span data-stu-id="e0d98-211">Channel parameters (Java)</span></span>
<span data-ttu-id="e0d98-212">Parametry te wpływa na sposób zestawu Java SDK należy przechowywać i opróżnić zbiera dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="e0d98-212">These parameters affect how the Java SDK should store and flush the telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="e0d98-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="e0d98-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="e0d98-214">Liczba elementów dane telemetryczne, które mogą być przechowywane w magazynie w pamięci w zestawie SDK.</span><span class="sxs-lookup"><span data-stu-id="e0d98-214">The number of telemetry items that can be stored in the SDK's in-memory storage.</span></span> <span data-ttu-id="e0d98-215">Po osiągnięciu tej liczby jest opróżniany buforu telemetrii — to znaczy elementy dane telemetryczne są wysyłane do serwera usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e0d98-215">When this number is reached, the telemetry buffer is flushed - that is, the telemetry items are sent to the Application Insights server.</span></span>

* <span data-ttu-id="e0d98-216">Min: 1</span><span class="sxs-lookup"><span data-stu-id="e0d98-216">Min: 1</span></span>
* <span data-ttu-id="e0d98-217">Maksymalna liczba: 1000</span><span class="sxs-lookup"><span data-stu-id="e0d98-217">Max: 1000</span></span>
* <span data-ttu-id="e0d98-218">Domyślne: 500</span><span class="sxs-lookup"><span data-stu-id="e0d98-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="e0d98-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="e0d98-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="e0d98-220">Określa, jak często dane, które są przechowywane w magazynie w pamięci mają zostać opróżnione (wysłane do usługi Application Insights).</span><span class="sxs-lookup"><span data-stu-id="e0d98-220">Determines how often the data that is stored in the in-memory storage should be flushed (sent to Application Insights).</span></span>

* <span data-ttu-id="e0d98-221">Min: 1</span><span class="sxs-lookup"><span data-stu-id="e0d98-221">Min: 1</span></span>
* <span data-ttu-id="e0d98-222">Maksymalna liczba: 300</span><span class="sxs-lookup"><span data-stu-id="e0d98-222">Max: 300</span></span>
* <span data-ttu-id="e0d98-223">Domyślne: 5</span><span class="sxs-lookup"><span data-stu-id="e0d98-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="e0d98-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="e0d98-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="e0d98-225">Określa maksymalny rozmiar w MB, który jest przydzielony do magazynu trwałego na dysku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="e0d98-225">Determines the maximum size in MB that is allotted to the persistent storage on the local disk.</span></span> <span data-ttu-id="e0d98-226">Magazyn ten jest używany dla trwałych elementów telemetrii, które nie mają być przekazywane do punktu końcowego usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e0d98-226">This storage is used for persisting telemetry items that failed to be transmitted to the Application Insights endpoint.</span></span> <span data-ttu-id="e0d98-227">Po spełnieniu rozmiar magazynu nowych elementów telemetrii zostaną odrzucone.</span><span class="sxs-lookup"><span data-stu-id="e0d98-227">When the storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="e0d98-228">Min: 1</span><span class="sxs-lookup"><span data-stu-id="e0d98-228">Min: 1</span></span>
* <span data-ttu-id="e0d98-229">Maksymalna: 100</span><span class="sxs-lookup"><span data-stu-id="e0d98-229">Max: 100</span></span>
* <span data-ttu-id="e0d98-230">Domyślny: 10</span><span class="sxs-lookup"><span data-stu-id="e0d98-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="e0d98-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="e0d98-231">InstrumentationKey</span></span>
<span data-ttu-id="e0d98-232">Określa zasób usługi Application Insights, w którym dane są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="e0d98-232">This determines the Application Insights resource in which your data appears.</span></span> <span data-ttu-id="e0d98-233">Zwykle tworzenia oddzielnych zasobu, za pomocą osobnych klucza dla poszczególnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0d98-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="e0d98-234">Jeśli chcesz ustawić klucz dynamicznie — na przykład, jeśli chcesz wysłać wyniki z aplikacji do różnych zasobów — można pominąć klucz z pliku konfiguracji i ustaw go w kodzie.</span><span class="sxs-lookup"><span data-stu-id="e0d98-234">If you want to set the key dynamically - for example if you want to send results from your application to different resources - you can omit the key from the configuration file, and set it in code instead.</span></span>

<span data-ttu-id="e0d98-235">Aby ustawić klucz dla wszystkich wystąpień TelemetryClient, moduły standardowe telemetrii ustawić klucza TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="e0d98-235">To set the key for all instances of TelemetryClient, including standard telemetry modules, set the key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="e0d98-236">Wykonaj następujące czynności w metodzie inicjowania, takich jak pliku global.aspx.cs w usługi ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="e0d98-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="e0d98-237">Jeśli chcesz wysłać określonych zdarzeń do różnych zasobów, można ustawić klucza dla określonych TelemetryClient:</span><span class="sxs-lookup"><span data-stu-id="e0d98-237">If you just want to send a specific set of events to a different resource, you can set the key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="e0d98-238">Aby uzyskać nowy klucz [utworzyć nowy zasób w portalu usługi Application Insights][new].</span><span class="sxs-lookup"><span data-stu-id="e0d98-238">To get a new key, [create a new resource in the Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0d98-239">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0d98-239">Next steps</span></span>
<span data-ttu-id="e0d98-240">[Dowiedz się więcej o interfejsie API][api].</span><span class="sxs-lookup"><span data-stu-id="e0d98-240">[Learn more about the API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
