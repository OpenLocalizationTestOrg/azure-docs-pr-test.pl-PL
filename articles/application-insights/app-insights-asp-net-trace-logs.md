---
title: "Dzienniki śledzenia platformy .NET aaaExplore w usłudze Application Insights"
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
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="e6981-103">Eksploruj dzienniki śledzenia platformy .NET w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="e6981-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="e6981-104">Jeśli używasz NLog, log4Net lub System.Diagnostics.Trace do śledzenia diagnostycznego w aplikacji programu ASP.NET może mieć dzienników wysłany[Azure Application Insights][start], gdzie można eksplorować i wyszukiwania je.</span><span class="sxs-lookup"><span data-stu-id="e6981-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent too[Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="e6981-105">Dzienniki zostaną scalone z hello inne dane telemetryczne pochodzące z aplikacji, dzięki czemu można zidentyfikować hello dane śledzenia skojarzone z obsługi każdego żądania użytkownika i skorelowania je za pomocą innych zdarzeń i raporty wyjątek.</span><span class="sxs-lookup"><span data-stu-id="e6981-105">Your logs will be merged with hello other telemetry coming from your application, so that you can identify hello traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="e6981-106">Potrzebujesz modułu przechwytywania dziennika hello?</span><span class="sxs-lookup"><span data-stu-id="e6981-106">Do you need hello log capture module?</span></span> <span data-ttu-id="e6981-107">Jest to przydatne karta dla firm 3rd rejestratorów, ale jeśli nie używasz już NLog, log4Net lub System.Diagnostics.Trace, należy wziąć pod uwagę tylko wywołania [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="e6981-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="e6981-108">Zainstaluj logowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="e6981-108">Install logging on your app</span></span>
<span data-ttu-id="e6981-109">Zainstaluj strukturę z wybranym rejestrowania w projekcie.</span><span class="sxs-lookup"><span data-stu-id="e6981-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="e6981-110">Powinno to spowodować, że wpis w pliku app.config lub web.config.</span><span class="sxs-lookup"><span data-stu-id="e6981-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="e6981-111">Jeśli używasz System.Diagnostics.Trace, należy tooadd tooweb.config wpis:</span><span class="sxs-lookup"><span data-stu-id="e6981-111">If you're using System.Diagnostics.Trace, you need tooadd an entry tooweb.config:</span></span>

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
## <a name="configure-application-insights-toocollect-logs"></a><span data-ttu-id="e6981-112">Konfigurowanie usługi Application Insights toocollect dzienników</span><span class="sxs-lookup"><span data-stu-id="e6981-112">Configure Application Insights toocollect logs</span></span>
<span data-ttu-id="e6981-113">**[Dodawanie projektu usługi Application Insights tooyour](app-insights-asp-net.md)**  Jeśli możesz jeszcze nie.</span><span class="sxs-lookup"><span data-stu-id="e6981-113">**[Add Application Insights tooyour project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="e6981-114">Moduł zbierający dzienniki opcja tooinclude hello jest widoczne.</span><span class="sxs-lookup"><span data-stu-id="e6981-114">You'll see an option tooinclude hello log collector.</span></span>

<span data-ttu-id="e6981-115">Lub **Konfiguruj usługę Application Insights** przez kliknięcie prawym przyciskiem myszy projekt w Eksploratorze rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="e6981-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="e6981-116">Wybierz opcję hello zbyt**Konfigurowanie zbierania danych śledzenia**.</span><span class="sxs-lookup"><span data-stu-id="e6981-116">Select hello option too**Configure trace collection**.</span></span>

<span data-ttu-id="e6981-117">*Brak usługi Application Insights menu lub dziennika modułu zbierającego opcji?*</span><span class="sxs-lookup"><span data-stu-id="e6981-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="e6981-118">Spróbuj [Rozwiązywanie problemów z](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="e6981-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="e6981-119">Instalacja ręczna</span><span class="sxs-lookup"><span data-stu-id="e6981-119">Manual installation</span></span>
<span data-ttu-id="e6981-120">Użyj tej metody, jeśli typ swojego projektu nie jest obsługiwany przez Instalatora usługi Application Insights hello (na przykład projekt pulpitu systemu Windows).</span><span class="sxs-lookup"><span data-stu-id="e6981-120">Use this method if your project type isn't supported by hello Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="e6981-121">Jeśli planujesz toouse log4Net lub NLog, należy go zainstalować w projekcie.</span><span class="sxs-lookup"><span data-stu-id="e6981-121">If you plan toouse log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="e6981-122">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e6981-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="e6981-123">Wyszukaj „Application Insights”</span><span class="sxs-lookup"><span data-stu-id="e6981-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="e6981-124">Wybierz odpowiedni pakiet hello — jeden z:</span><span class="sxs-lookup"><span data-stu-id="e6981-124">Select hello appropriate package - one of:</span></span>

   * <span data-ttu-id="e6981-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace wywołań)</span><span class="sxs-lookup"><span data-stu-id="e6981-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="e6981-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource zdarzeń)</span><span class="sxs-lookup"><span data-stu-id="e6981-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource events)</span></span>
   * <span data-ttu-id="e6981-127">Microsoft.ApplicationInsights.EtwListener (zdarzenia ETW toocapture)</span><span class="sxs-lookup"><span data-stu-id="e6981-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW events)</span></span>
   * <span data-ttu-id="e6981-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="e6981-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="e6981-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="e6981-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="e6981-130">Witaj pakiet NuGet instaluje konieczne zestawy hello, a także modyfikuje plik web.config lub app.config.</span><span class="sxs-lookup"><span data-stu-id="e6981-130">hello NuGet package installs hello necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="e6981-131">Wstawianie wywołania dziennik diagnostyczny</span><span class="sxs-lookup"><span data-stu-id="e6981-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="e6981-132">Jeśli używasz System.Diagnostics.Trace, będzie Typowe wywołania:</span><span class="sxs-lookup"><span data-stu-id="e6981-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="e6981-133">Jeśli wolisz, log4net lub NLog:</span><span class="sxs-lookup"><span data-stu-id="e6981-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="e6981-134">W przypadku używania zdarzeń źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="e6981-134">Using EventSource events</span></span>
<span data-ttu-id="e6981-135">Można skonfigurować [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) tooApplication toobe wysyłane zdarzenia Insights jako dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="e6981-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="e6981-136">Najpierw zainstaluj hello `Microsoft.ApplicationInsights.EventSourceListener` pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e6981-136">First, install hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="e6981-137">Następnie Edytuj `TelemetryModules` sekcji hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) pliku.</span><span class="sxs-lookup"><span data-stu-id="e6981-137">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="e6981-138">Dla każdego źródła można ustawić hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="e6981-138">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="e6981-139">`Name`Określa nazwę hello hello EventSource toocollect.</span><span class="sxs-lookup"><span data-stu-id="e6981-139">`Name` specifies hello name of hello EventSource toocollect.</span></span>
 * <span data-ttu-id="e6981-140">`Level`Określa hello toocollect poziomu rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="e6981-140">`Level` specifies hello logging level toocollect.</span></span> <span data-ttu-id="e6981-141">Może być jednym z `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="e6981-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="e6981-142">`Keywords`(Opcjonalnie) określa wartość całkowitą hello toouse kombinacji słów kluczowych.</span><span class="sxs-lookup"><span data-stu-id="e6981-142">`Keywords` (Optional) specifies hello integer value of keywords combinations toouse.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="e6981-143">W przypadku używania DiagnosticSource zdarzeń</span><span class="sxs-lookup"><span data-stu-id="e6981-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="e6981-144">Można skonfigurować [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) tooApplication toobe wysyłane zdarzenia Insights jako dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="e6981-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="e6981-145">Najpierw zainstaluj hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e6981-145">First, install hello [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="e6981-146">Następnie edytuj hello `TelemetryModules` sekcji hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) pliku.</span><span class="sxs-lookup"><span data-stu-id="e6981-146">Then edit hello `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="e6981-147">Dla każdego DiagnosticSource ma tootrace, Dodaj wpis z hello `Name` nazwę toohello Twojego DiagnosticSource ustawić atrybutu.</span><span class="sxs-lookup"><span data-stu-id="e6981-147">For each DiagnosticSource you want tootrace, add an entry with hello `Name` attribute  set toohello name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="e6981-148">W przypadku używania zdarzeń ETW.</span><span class="sxs-lookup"><span data-stu-id="e6981-148">Using ETW events</span></span>
<span data-ttu-id="e6981-149">Można skonfigurować toobe zdarzenia ETW wysyłane tooApplication Insights jako dane śledzenia.</span><span class="sxs-lookup"><span data-stu-id="e6981-149">You can configure ETW events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="e6981-150">Najpierw zainstaluj hello `Microsoft.ApplicationInsights.EtwCollector` pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="e6981-150">First, install hello `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="e6981-151">Następnie Edytuj `TelemetryModules` sekcji hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) pliku.</span><span class="sxs-lookup"><span data-stu-id="e6981-151">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="e6981-152">Zdarzenia ETW mogą być zbierane tylko, jeśli hello procesu hostingu hello zestawu SDK jest uruchomiona w ramach tożsamości, który jest członkiem grupy "Użytkownicy dzienników wydajności" lub Administratorzy.</span><span class="sxs-lookup"><span data-stu-id="e6981-152">ETW events can only be collected if hello process hosting hello SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="e6981-153">Dla każdego źródła można ustawić hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="e6981-153">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="e6981-154">`ProviderName`to nazwa hello toocollect dostawcy ETW hello.</span><span class="sxs-lookup"><span data-stu-id="e6981-154">`ProviderName` is hello name of hello ETW provider toocollect.</span></span>
 * <span data-ttu-id="e6981-155">`ProviderGuid`Określa hello GUID toocollect dostawcy ETW hello, można użyć zamiast `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="e6981-155">`ProviderGuid` specifies hello GUID of hello ETW provider toocollect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="e6981-156">`Level`Ustawia hello toocollect poziomu rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="e6981-156">`Level` sets hello logging level toocollect.</span></span> <span data-ttu-id="e6981-157">Może być jednym z `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="e6981-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="e6981-158">`Keywords`Zestawy (opcjonalnie) hello wartość całkowitą toouse kombinacji — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="e6981-158">`Keywords` (Optional) sets hello integer value of keyword combinations toouse.</span></span>

## <a name="using-hello-trace-api-directly"></a><span data-ttu-id="e6981-159">Przy użyciu interfejsu API śledzenia hello bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="e6981-159">Using hello Trace API directly</span></span>
<span data-ttu-id="e6981-160">Interfejs API śledzenia usługi Application Insights hello można wywołać bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="e6981-160">You can call hello Application Insights trace API directly.</span></span> <span data-ttu-id="e6981-161">Adaptery rejestrowania Hello używać tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e6981-161">hello logging adapters use this API.</span></span>

<span data-ttu-id="e6981-162">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e6981-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="e6981-163">Zaletą TrackTrace jest umieszczenie stosunkowo długo dane wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="e6981-163">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="e6981-164">Na przykład można zakodować danych POST.</span><span class="sxs-lookup"><span data-stu-id="e6981-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="e6981-165">Ponadto możesz dodać komunikat tooyour poziomu ważności.</span><span class="sxs-lookup"><span data-stu-id="e6981-165">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="e6981-166">I, podobnie jak inne dane telemetryczne, można dodać wartości właściwości, które można toohelp filtru lub wyszukiwania dla różnych zestawów danych śledzenia.</span><span class="sxs-lookup"><span data-stu-id="e6981-166">And, like other telemetry, you can add property values that you can use toohelp filter or search for different sets of traces.</span></span> <span data-ttu-id="e6981-167">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e6981-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="e6981-168">To, czy włączyć w [wyszukiwania][diagnostic], filtr tooeasily wszystkie wiadomości powitania poziomu ważności określonego dotyczących tooa określonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e6981-168">This would enable you, in [Search][diagnostic], tooeasily filter out all hello messages of a particular severity level relating tooa particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="e6981-169">Eksploruj dzienniki</span><span class="sxs-lookup"><span data-stu-id="e6981-169">Explore your logs</span></span>
<span data-ttu-id="e6981-170">Uruchamianie aplikacji, albo w trybie debugowania, albo wdrożyć go na żywo.</span><span class="sxs-lookup"><span data-stu-id="e6981-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="e6981-171">W bloku Przegląd aplikacji w [portalu Application Insights hello][portal], wybierz [wyszukiwania][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="e6981-171">In your app's overview blade in [hello Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![W usłudze Application Insights wybierz wyszukiwania](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Wyszukiwanie](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="e6981-174">Można na przykład:</span><span class="sxs-lookup"><span data-stu-id="e6981-174">You can, for example:</span></span>

* <span data-ttu-id="e6981-175">Odfiltrować ślady dziennika lub elementy o określonej właściwości</span><span class="sxs-lookup"><span data-stu-id="e6981-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="e6981-176">Sprawdź, czy konkretny element szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="e6981-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="e6981-177">Znajdź inne dane telemetryczne dotyczące toohello tego samego żądania użytkownika (czyli z hello sam OperationId)</span><span class="sxs-lookup"><span data-stu-id="e6981-177">Find other telemetry relating toohello same user request (that is, with hello same OperationId)</span></span>
* <span data-ttu-id="e6981-178">Zapisz konfigurację hello tej strony jako ulubione</span><span class="sxs-lookup"><span data-stu-id="e6981-178">Save hello configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="e6981-179">**Próbkowania.**</span><span class="sxs-lookup"><span data-stu-id="e6981-179">**Sampling.**</span></span> <span data-ttu-id="e6981-180">Jeśli używasz hello zestaw SDK usługi Application Insights dla platformy ASP.NET w wersji 2.0.0-beta3 lub nowszego aplikacji wysyła dużą ilość danych, funkcja adaptacyjną próbkowania hello może działać i wysłać określonego odsetka telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e6981-180">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="e6981-181">Dowiedz się więcej na temat próbkowania.</span><span class="sxs-lookup"><span data-stu-id="e6981-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="e6981-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e6981-182">Next steps</span></span>
<span data-ttu-id="e6981-183">[Diagnozowanie błędów i wyjątków w programie ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="e6981-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="e6981-184">[Dowiedz się więcej na temat wyszukiwania][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="e6981-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e6981-185">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="e6981-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="e6981-186">Jak to zrobić to dla języka Java?</span><span class="sxs-lookup"><span data-stu-id="e6981-186">How do I do this for Java?</span></span>
<span data-ttu-id="e6981-187">Użyj hello [kart dziennika Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e6981-187">Use hello [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a><span data-ttu-id="e6981-188">Nie jest dostępna opcja usługi Application Insights w menu kontekstowym hello projektu</span><span class="sxs-lookup"><span data-stu-id="e6981-188">There's no Application Insights option on hello project context menu</span></span>
* <span data-ttu-id="e6981-189">Sprawdź usługę Application Insights tools jest zainstalowany na tym komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="e6981-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="e6981-190">W programie Visual Studio menu Narzędzia, rozszerzenia i aktualizacje poszukaj Application Insights Tools.</span><span class="sxs-lookup"><span data-stu-id="e6981-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="e6981-191">Jeśli nie znajduje się w karcie zainstalowana hello, otwórz kartę hello w trybie Online, a następnie zainstaluj go.</span><span class="sxs-lookup"><span data-stu-id="e6981-191">If it isn't in hello Installed tab, open hello Online tab and install it.</span></span>
* <span data-ttu-id="e6981-192">Może to być typ projektu nie jest obsługiwane przez narzędzia Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e6981-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="e6981-193">Użyj [Instalacja ręczna](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="e6981-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a><span data-ttu-id="e6981-194">Brak opcji karty dziennika narzędzia konfiguracji hello</span><span class="sxs-lookup"><span data-stu-id="e6981-194">No log adapter option in hello configuration tool</span></span>
* <span data-ttu-id="e6981-195">Należy najpierw struktury tooinstall hello rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="e6981-195">You need tooinstall hello logging framework first.</span></span>
* <span data-ttu-id="e6981-196">Jeśli używasz System.Diagnostics.Trace, upewnij się, że [skonfigurowany w `web.config` ](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6981-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="e6981-197">Możesz znaleźć hello najnowszą wersję usługi Application Insights?</span><span class="sxs-lookup"><span data-stu-id="e6981-197">Have you got hello latest version of Application Insights?</span></span> <span data-ttu-id="e6981-198">W programie Visual Studio **narzędzia** menu, wybierz **rozszerzenia i aktualizacje**i otwórz hello **aktualizacje** kartę. W przypadku narzędzia Developer Analytics, kliknij przycisk tooupdate go.</span><span class="sxs-lookup"><span data-stu-id="e6981-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open hello **Updates** tab. If Developer Analytics tools is there, click tooupdate it.</span></span>

### <span data-ttu-id="e6981-199"><a name="emptykey"></a>Otrzymuję komunikat o błędzie "klucza Instrumentacji nie może być pusta"</span><span class="sxs-lookup"><span data-stu-id="e6981-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="e6981-200">Prawdopodobnie zainstalowano hello rejestrowania pakietu Nuget karty bez instalowania usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e6981-200">Looks like you installed hello logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="e6981-201">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy `ApplicationInsights.config` i wybierz polecenie **usługi Application Insights dla aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="e6981-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="e6981-202">Otrzymasz okna dialogowego, które można zaprasza toosign w tooAzure i Utwórz zasobu usługi Application Insights lub ponownego użycia istniejącej.</span><span class="sxs-lookup"><span data-stu-id="e6981-202">You'll get a dialog that invites you toosign in tooAzure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="e6981-203">Który powinno rozwiązać go.</span><span class="sxs-lookup"><span data-stu-id="e6981-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a><span data-ttu-id="e6981-204">Mogę Zobacz dane śledzenia diagnostycznego wyszukiwania, ale nie hello inne zdarzenia</span><span class="sxs-lookup"><span data-stu-id="e6981-204">I can see traces in diagnostic search, but not hello other events</span></span>
<span data-ttu-id="e6981-205">Czasami może upłynąć trochę czasu, zanim wszystkie hello zdarzenia i żądania tooget przez potok hello.</span><span class="sxs-lookup"><span data-stu-id="e6981-205">It can sometimes take a while for all hello events and requests tooget through hello pipeline.</span></span>

### <span data-ttu-id="e6981-206"><a name="limits"></a>Jak dużo danych jest zachowywana?</span><span class="sxs-lookup"><span data-stu-id="e6981-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="e6981-207">Istnieje kilka możliwych wpływ hello ilość danych przechowywane.</span><span class="sxs-lookup"><span data-stu-id="e6981-207">Several factors impact hello amount of data retained.</span></span> <span data-ttu-id="e6981-208">Zobacz hello [limity](app-insights-api-custom-events-metrics.md#limits) sekcji hello odbiorcy zdarzeń metryki strony, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e6981-208">See hello [limits](app-insights-api-custom-events-metrics.md#limits) section of hello customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a><span data-ttu-id="e6981-209">Nie widzę niektórych wpisów dziennika hello oczekiwanych</span><span class="sxs-lookup"><span data-stu-id="e6981-209">I'm not seeing some of hello log entries that I expect</span></span>
<span data-ttu-id="e6981-210">Jeśli używasz hello zestaw SDK usługi Application Insights dla platformy ASP.NET w wersji 2.0.0-beta3 lub nowszego aplikacji wysyła dużą ilość danych, funkcja adaptacyjną próbkowania hello może działać i wysłać określonego odsetka telemetrii.</span><span class="sxs-lookup"><span data-stu-id="e6981-210">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="e6981-211">Dowiedz się więcej na temat próbkowania.</span><span class="sxs-lookup"><span data-stu-id="e6981-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="e6981-212"><a name="add"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e6981-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="e6981-213">[Konfigurowanie dostępności i testy czasu odpowiedzi][availability]</span><span class="sxs-lookup"><span data-stu-id="e6981-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="e6981-214">[Rozwiązywanie problemów][qna]</span><span class="sxs-lookup"><span data-stu-id="e6981-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
