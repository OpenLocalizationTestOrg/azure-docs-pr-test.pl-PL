---
title: "Eksploruj dzienniki śledzenia platformy .NET w usłudze Application Insights"
description: "Wyszukaj dzienniki generowane z śledzenia, NLog i Log4Net."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 68e03bf10167ecde675d62782de7063aea9e81d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="c3259-103">Eksploruj dzienniki śledzenia platformy .NET w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="c3259-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="c3259-104">Jeśli używasz NLog, log4Net lub System.Diagnostics.Trace do śledzenia diagnostycznego w aplikacji programu ASP.NET może mieć dzienniki wysyłane do [Azure Application Insights][start], gdzie można eksplorować i ich wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="c3259-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="c3259-105">Dzienniki zostaną scalone z innymi telemetrii pochodzące z aplikacji, aby zidentyfikować dane śledzenia skojarzone z obsługi każdego żądania użytkownika i skorelowania je za pomocą innych zdarzeń i raporty wyjątek.</span><span class="sxs-lookup"><span data-stu-id="c3259-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="c3259-106">Potrzebujesz modułu przechwytywania dziennika?</span><span class="sxs-lookup"><span data-stu-id="c3259-106">Do you need the log capture module?</span></span> <span data-ttu-id="c3259-107">Jest to przydatne karta dla firm 3rd rejestratorów, ale jeśli nie używasz już NLog, log4Net lub System.Diagnostics.Trace, należy wziąć pod uwagę tylko wywołania [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="c3259-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="c3259-108">Zainstaluj logowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="c3259-108">Install logging on your app</span></span>
<span data-ttu-id="c3259-109">Zainstaluj strukturę z wybranym rejestrowania w projekcie.</span><span class="sxs-lookup"><span data-stu-id="c3259-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="c3259-110">Powinno to spowodować, że wpis w pliku app.config lub web.config.</span><span class="sxs-lookup"><span data-stu-id="c3259-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="c3259-111">Jeśli używasz System.Diagnostics.Trace, należy dodać wpis do pliku web.config:</span><span class="sxs-lookup"><span data-stu-id="c3259-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span></span>

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-to-collect-logs"></a><span data-ttu-id="c3259-112">Konfiguruj usługę Application Insights do zbierania dzienników</span><span class="sxs-lookup"><span data-stu-id="c3259-112">Configure Application Insights to collect logs</span></span>
<span data-ttu-id="c3259-113">**[Dodawanie usługi Application Insights do projektu](app-insights-asp-net.md)**  Jeśli możesz jeszcze nie.</span><span class="sxs-lookup"><span data-stu-id="c3259-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="c3259-114">Zobaczysz opcję uwzględniania modułu zbierającego dzienniki.</span><span class="sxs-lookup"><span data-stu-id="c3259-114">You'll see an option to include the log collector.</span></span>

<span data-ttu-id="c3259-115">Lub **Konfiguruj usługę Application Insights** przez kliknięcie prawym przyciskiem myszy projekt w Eksploratorze rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="c3259-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="c3259-116">Wybierz opcję **Konfigurowanie zbierania danych śledzenia**.</span><span class="sxs-lookup"><span data-stu-id="c3259-116">Select the option to **Configure trace collection**.</span></span>

<span data-ttu-id="c3259-117">*Brak usługi Application Insights menu lub dziennika modułu zbierającego opcji?*</span><span class="sxs-lookup"><span data-stu-id="c3259-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="c3259-118">Spróbuj [Rozwiązywanie problemów z](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="c3259-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="c3259-119">Instalacja ręczna</span><span class="sxs-lookup"><span data-stu-id="c3259-119">Manual installation</span></span>
<span data-ttu-id="c3259-120">Użyj tej metody, jeśli typ swojego projektu nie jest obsługiwany przez Instalatora usługi Application Insights (na przykład projekt pulpitu systemu Windows).</span><span class="sxs-lookup"><span data-stu-id="c3259-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="c3259-121">Jeśli planujesz użyć log4Net, NLog, należy go zainstalować w projekcie.</span><span class="sxs-lookup"><span data-stu-id="c3259-121">If you plan to use log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="c3259-122">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c3259-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="c3259-123">Wyszukaj „Application Insights”</span><span class="sxs-lookup"><span data-stu-id="c3259-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="c3259-124">Wybierz odpowiedni pakiet — jeden z:</span><span class="sxs-lookup"><span data-stu-id="c3259-124">Select the appropriate package - one of:</span></span>

   * <span data-ttu-id="c3259-125">Microsoft.ApplicationInsights.TraceListener (do przechwytywania System.Diagnostics.Trace wywołań)</span><span class="sxs-lookup"><span data-stu-id="c3259-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="c3259-126">Microsoft.ApplicationInsights.EventSourceListener (do przechwytywania zdarzeń EventSource)</span><span class="sxs-lookup"><span data-stu-id="c3259-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span></span>
   * <span data-ttu-id="c3259-127">Microsoft.ApplicationInsights.EtwListener (do przechwytywania zdarzeń ETW)</span><span class="sxs-lookup"><span data-stu-id="c3259-127">Microsoft.ApplicationInsights.EtwListener (to capture ETW events)</span></span>
   * <span data-ttu-id="c3259-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="c3259-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="c3259-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="c3259-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="c3259-130">Pakiet NuGet instaluje konieczne zestawy, a także modyfikuje plik web.config lub app.config.</span><span class="sxs-lookup"><span data-stu-id="c3259-130">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="c3259-131">Wstawianie wywołania dziennik diagnostyczny</span><span class="sxs-lookup"><span data-stu-id="c3259-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="c3259-132">Jeśli używasz System.Diagnostics.Trace, będzie Typowe wywołania:</span><span class="sxs-lookup"><span data-stu-id="c3259-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="c3259-133">Jeśli wolisz, log4net lub NLog:</span><span class="sxs-lookup"><span data-stu-id="c3259-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="c3259-134">W przypadku używania zdarzeń źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c3259-134">Using EventSource events</span></span>
<span data-ttu-id="c3259-135">Można skonfigurować [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) zdarzenia mają być wysyłane do usługi Application Insights jako dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="c3259-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="c3259-136">Najpierw zainstaluj `Microsoft.ApplicationInsights.EventSourceListener` pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="c3259-136">First, install the `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="c3259-137">Następnie Edytuj `TelemetryModules` sekcji [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) pliku.</span><span class="sxs-lookup"><span data-stu-id="c3259-137">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="c3259-138">Dla każdego źródła można ustawić następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="c3259-138">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="c3259-139">`Name`Określa nazwę elementu EventSource do zbierania.</span><span class="sxs-lookup"><span data-stu-id="c3259-139">`Name` specifies the name of the EventSource to collect.</span></span>
 * <span data-ttu-id="c3259-140">`Level`Określa poziom rejestrowania do zbierania.</span><span class="sxs-lookup"><span data-stu-id="c3259-140">`Level` specifies the logging level to collect.</span></span> <span data-ttu-id="c3259-141">Może być jednym z `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="c3259-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="c3259-142">`Keywords`(Opcjonalnie) określa wartość całkowita kombinacji słowa kluczowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="c3259-142">`Keywords` (Optional) specifies the integer value of keywords combinations to use.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="c3259-143">W przypadku używania DiagnosticSource zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c3259-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="c3259-144">Można skonfigurować [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) zdarzenia mają być wysyłane do usługi Application Insights jako dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="c3259-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="c3259-145">Najpierw zainstaluj [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="c3259-145">First, install the [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="c3259-146">Następnie Edytuj `TelemetryModules` sekcji [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) pliku.</span><span class="sxs-lookup"><span data-stu-id="c3259-146">Then edit the `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="c3259-147">Dla każdego DiagnosticSource do śledzenia, Dodaj wpis z `Name` atrybutu Ustaw nazwę sieci DiagnosticSource.</span><span class="sxs-lookup"><span data-stu-id="c3259-147">For each DiagnosticSource you want to trace, add an entry with the `Name` attribute  set to the name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="c3259-148">W przypadku używania zdarzeń ETW.</span><span class="sxs-lookup"><span data-stu-id="c3259-148">Using ETW events</span></span>
<span data-ttu-id="c3259-149">Można skonfigurować zdarzenia ETW mają być wysyłane do usługi Application Insights jako dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="c3259-149">You can configure ETW events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="c3259-150">Najpierw zainstaluj `Microsoft.ApplicationInsights.EtwCollector` pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="c3259-150">First, install the `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="c3259-151">Następnie Edytuj `TelemetryModules` sekcji [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) pliku.</span><span class="sxs-lookup"><span data-stu-id="c3259-151">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="c3259-152">Zdarzenia ETW mogą być zbierane tylko, jeśli proces obsługujący zestawu SDK jest uruchomiona w ramach tożsamości, który jest członkiem grupy "Użytkownicy dzienników wydajności" lub Administratorzy.</span><span class="sxs-lookup"><span data-stu-id="c3259-152">ETW events can only be collected if the process hosting the SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="c3259-153">Dla każdego źródła można ustawić następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="c3259-153">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="c3259-154">`ProviderName`jest nazwą dostawcy ETW do zbierania.</span><span class="sxs-lookup"><span data-stu-id="c3259-154">`ProviderName` is the name of the ETW provider to collect.</span></span>
 * <span data-ttu-id="c3259-155">`ProviderGuid`Określa identyfikator GUID dostawców ETW, aby zebrać, można użyć zamiast `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="c3259-155">`ProviderGuid` specifies the GUID of the ETW provider to collect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="c3259-156">`Level`Ustawia poziom rejestrowania do zbierania.</span><span class="sxs-lookup"><span data-stu-id="c3259-156">`Level` sets the logging level to collect.</span></span> <span data-ttu-id="c3259-157">Może być jednym z `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="c3259-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="c3259-158">`Keywords`(Opcjonalnie) ustawia całkowitą kombinacji — słowo kluczowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="c3259-158">`Keywords` (Optional) sets the integer value of keyword combinations to use.</span></span>

## <a name="using-the-trace-api-directly"></a><span data-ttu-id="c3259-159">Bezpośrednio za pomocą śledzenia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="c3259-159">Using the Trace API directly</span></span>
<span data-ttu-id="c3259-160">Śledzenia usługi Application Insights interfejsu API można wywołać bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="c3259-160">You can call the Application Insights trace API directly.</span></span> <span data-ttu-id="c3259-161">Adaptery rejestrowania użycia tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c3259-161">The logging adapters use this API.</span></span>

<span data-ttu-id="c3259-162">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c3259-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="c3259-163">Zaletą TrackTrace jest umieszczenie danych stosunkowo długo w komunikacie.</span><span class="sxs-lookup"><span data-stu-id="c3259-163">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="c3259-164">Na przykład można zakodować danych POST.</span><span class="sxs-lookup"><span data-stu-id="c3259-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="c3259-165">Ponadto można dodać poziomu ważności do wiadomości.</span><span class="sxs-lookup"><span data-stu-id="c3259-165">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="c3259-166">I, podobnie jak inne dane telemetryczne, można dodać wartości właściwości, które można użyć filtru lub wyszukiwania dla różnych zestawów danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="c3259-166">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span></span> <span data-ttu-id="c3259-167">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c3259-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="c3259-168">To, czy włączyć w [wyszukiwania][diagnostic], aby łatwo filtrować komunikaty poziom ważności określonego odnoszących się do określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c3259-168">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="c3259-169">Eksploruj dzienniki</span><span class="sxs-lookup"><span data-stu-id="c3259-169">Explore your logs</span></span>
<span data-ttu-id="c3259-170">Uruchamianie aplikacji, albo w trybie debugowania, albo wdrożyć go na żywo.</span><span class="sxs-lookup"><span data-stu-id="c3259-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="c3259-171">W bloku Przegląd aplikacji w [portalu Application Insights][portal], wybierz [wyszukiwania][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="c3259-171">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![W usłudze Application Insights wybierz wyszukiwania](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Wyszukiwanie](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="c3259-174">Można na przykład:</span><span class="sxs-lookup"><span data-stu-id="c3259-174">You can, for example:</span></span>

* <span data-ttu-id="c3259-175">Odfiltrować ślady dziennika lub elementy o określonej właściwości</span><span class="sxs-lookup"><span data-stu-id="c3259-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="c3259-176">Sprawdź, czy konkretny element szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="c3259-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="c3259-177">Znajdź inne dane telemetryczne odnoszących się do tego samego żądania użytkownika (czyli z tego samego OperationId)</span><span class="sxs-lookup"><span data-stu-id="c3259-177">Find other telemetry relating to the same user request (that is, with the same OperationId)</span></span>
* <span data-ttu-id="c3259-178">Zapisywanie konfiguracji tej strony jako ulubione</span><span class="sxs-lookup"><span data-stu-id="c3259-178">Save the configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="c3259-179">**Próbkowania.**</span><span class="sxs-lookup"><span data-stu-id="c3259-179">**Sampling.**</span></span> <span data-ttu-id="c3259-180">Jeśli aplikacja wysyła dużo danych, a używasz zestawu SDK usługi Application Insights dla technologii ASP.NET w wersji 2.0.0-beta3 lub nowszej, może działać funkcja adaptacyjnego próbkowania, powodując wysyłanie tylko ułamka telemetrii.</span><span class="sxs-lookup"><span data-stu-id="c3259-180">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="c3259-181">Dowiedz się więcej na temat próbkowania.</span><span class="sxs-lookup"><span data-stu-id="c3259-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="c3259-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3259-182">Next steps</span></span>
<span data-ttu-id="c3259-183">[Diagnozowanie błędów i wyjątków w programie ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="c3259-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="c3259-184">[Dowiedz się więcej na temat wyszukiwania][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="c3259-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c3259-185">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="c3259-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="c3259-186">Jak to zrobić to dla języka Java?</span><span class="sxs-lookup"><span data-stu-id="c3259-186">How do I do this for Java?</span></span>
<span data-ttu-id="c3259-187">Użyj [kart dziennika Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="c3259-187">Use the [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-the-project-context-menu"></a><span data-ttu-id="c3259-188">Nie ma opcji menu kontekstowego projektu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="c3259-188">There's no Application Insights option on the project context menu</span></span>
* <span data-ttu-id="c3259-189">Sprawdź usługę Application Insights tools jest zainstalowany na tym komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="c3259-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="c3259-190">W programie Visual Studio menu Narzędzia, rozszerzenia i aktualizacje poszukaj Application Insights Tools.</span><span class="sxs-lookup"><span data-stu-id="c3259-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="c3259-191">Jeśli nie jest zainstalowana karta, otwórz kartę Online, a następnie zainstaluj go.</span><span class="sxs-lookup"><span data-stu-id="c3259-191">If it isn't in the Installed tab, open the Online tab and install it.</span></span>
* <span data-ttu-id="c3259-192">Może to być typ projektu nie jest obsługiwane przez narzędzia Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c3259-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="c3259-193">Użyj [Instalacja ręczna](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="c3259-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-the-configuration-tool"></a><span data-ttu-id="c3259-194">Brak opcji karty dziennika narzędzia konfiguracji</span><span class="sxs-lookup"><span data-stu-id="c3259-194">No log adapter option in the configuration tool</span></span>
* <span data-ttu-id="c3259-195">Należy najpierw zainstalować struktury rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="c3259-195">You need to install the logging framework first.</span></span>
* <span data-ttu-id="c3259-196">Jeśli używasz System.Diagnostics.Trace, upewnij się, że [skonfigurowany w `web.config` ](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3259-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="c3259-197">Możesz znaleźć najnowszej wersji usługi Application Insights?</span><span class="sxs-lookup"><span data-stu-id="c3259-197">Have you got the latest version of Application Insights?</span></span> <span data-ttu-id="c3259-198">W programie Visual Studio **narzędzia** menu, wybierz **rozszerzenia i aktualizacje**i Otwórz **aktualizacje** kartę. W przypadku narzędzia Developer Analytics, kliknij, aby go zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="c3259-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span></span>

### <span data-ttu-id="c3259-199"><a name="emptykey"></a>Otrzymuję komunikat o błędzie "klucza Instrumentacji nie może być pusta"</span><span class="sxs-lookup"><span data-stu-id="c3259-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="c3259-200">Prawdopodobnie zainstalowano pakiet Nuget adapter rejestrowania bez instalowania usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c3259-200">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="c3259-201">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy `ApplicationInsights.config` i wybierz polecenie **usługi Application Insights dla aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="c3259-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="c3259-202">Okno dialogowe, które umożliwiające logowanie do platformy Azure, zostanie wyświetlony i Utwórz zasobu usługi Application Insights lub ponownego użycia istniejącej.</span><span class="sxs-lookup"><span data-stu-id="c3259-202">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="c3259-203">Który powinno rozwiązać go.</span><span class="sxs-lookup"><span data-stu-id="c3259-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-the-other-events"></a><span data-ttu-id="c3259-204">Wyświetlane dane śledzenia diagnostycznego wyszukiwania, ale nie innych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="c3259-204">I can see traces in diagnostic search, but not the other events</span></span>
<span data-ttu-id="c3259-205">Czasami może upłynąć trochę czasu zanim wszystkie zdarzenia i żądania można uzyskać za pośrednictwem potoku.</span><span class="sxs-lookup"><span data-stu-id="c3259-205">It can sometimes take a while for all the events and requests to get through the pipeline.</span></span>

### <span data-ttu-id="c3259-206"><a name="limits"></a>Jak dużo danych jest zachowywana?</span><span class="sxs-lookup"><span data-stu-id="c3259-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="c3259-207">Istnieje kilka możliwych wpływ na ilość danych przechowywane.</span><span class="sxs-lookup"><span data-stu-id="c3259-207">Several factors impact the amount of data retained.</span></span> <span data-ttu-id="c3259-208">Zobacz [limity](app-insights-api-custom-events-metrics.md#limits) części strony metryki zdarzenia klienta, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="c3259-208">See the [limits](app-insights-api-custom-events-metrics.md#limits) section of the customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-the-log-entries-that-i-expect"></a><span data-ttu-id="c3259-209">Nie widzę niektórych oczekiwanych wpisów dziennika</span><span class="sxs-lookup"><span data-stu-id="c3259-209">I'm not seeing some of the log entries that I expect</span></span>
<span data-ttu-id="c3259-210">Jeśli aplikacja wysyła dużo danych, a używasz zestawu SDK usługi Application Insights dla technologii ASP.NET w wersji 2.0.0-beta3 lub nowszej, może działać funkcja adaptacyjnego próbkowania, powodując wysyłanie tylko ułamka telemetrii.</span><span class="sxs-lookup"><span data-stu-id="c3259-210">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="c3259-211">Dowiedz się więcej na temat próbkowania.</span><span class="sxs-lookup"><span data-stu-id="c3259-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="c3259-212"><a name="add"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3259-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="c3259-213">[Konfigurowanie dostępności i testy czasu odpowiedzi][availability]</span><span class="sxs-lookup"><span data-stu-id="c3259-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="c3259-214">[Rozwiązywanie problemów][qna]</span><span class="sxs-lookup"><span data-stu-id="c3259-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
