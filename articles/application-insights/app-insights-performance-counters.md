---
title: "liczniki aaaPerformance w usłudze Application Insights | Dokumentacja firmy Microsoft"
description: "Monitorowanie systemu i niestandardowe liczniki wydajności .NET w usłudze Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="fa86a-103">Liczniki wydajności systemu w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="fa86a-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="fa86a-104">System Windows udostępnia wiele różnych [liczniki wydajności](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) takich jak zajęte Procesora, pamięci, dysku i użycia sieci.</span><span class="sxs-lookup"><span data-stu-id="fa86a-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="fa86a-105">Możesz również definiować własnych.</span><span class="sxs-lookup"><span data-stu-id="fa86a-105">You can also define your own.</span></span> <span data-ttu-id="fa86a-106">[Usługa Application Insights](app-insights-overview.md) mogą być prezentowane z tych liczników wydajności, jeśli aplikacja działa w środowisku usług IIS na lokalnym toowhich hosta lub maszyny wirtualnej należy mieć dostęp administracyjny.</span><span class="sxs-lookup"><span data-stu-id="fa86a-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine toowhich you have administrative access.</span></span> <span data-ttu-id="fa86a-107">Wykresy Hello wskazać hello zasoby dostępne tooyour działającej aplikacji i może ułatwić tooidentify obciążenia równowagi między wystąpieniami serwera.</span><span class="sxs-lookup"><span data-stu-id="fa86a-107">hello charts indicate hello resources available tooyour live application, and can help tooidentify unbalanced load between server instances.</span></span>

<span data-ttu-id="fa86a-108">Liczniki wydajności są wyświetlane w bloku serwerów hello, w tym segmentów zawiera tabelę przez wystąpienie serwera.</span><span class="sxs-lookup"><span data-stu-id="fa86a-108">Performance counters appear in hello Servers blade, which includes a table that segments by server instance.</span></span>

![Liczniki wydajności zgłoszonych w usłudze Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="fa86a-110">(Liczniki wydajności nie są dostępne dla aplikacji sieci Web Azure.</span><span class="sxs-lookup"><span data-stu-id="fa86a-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="fa86a-111">Ale możesz [wysyłania Insights tooApplication diagnostyki Azure](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="fa86a-111">But you can [send Azure Diagnostics tooApplication Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="fa86a-112">Wyświetlanie liczników</span><span class="sxs-lookup"><span data-stu-id="fa86a-112">View counters</span></span>
<span data-ttu-id="fa86a-113">Blok serwerów Hello Pokazuje domyślny zbiór liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="fa86a-113">hello Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="fa86a-114">toosee innych liczników edytowanie hello wykresów na powitania blok serwerów albo otwórz nowe [Eksploratora metryk](app-insights-metrics-explorer.md) bloku i dodawanie nowych schematów.</span><span class="sxs-lookup"><span data-stu-id="fa86a-114">toosee other counters, either edit hello charts on hello Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="fa86a-115">dostępne liczniki Hello są wyświetlane jako metryki podczas edytowania wykresu.</span><span class="sxs-lookup"><span data-stu-id="fa86a-115">hello available counters are listed as metrics when you edit a chart.</span></span>

![Liczniki wydajności zgłoszonych w usłudze Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="fa86a-117">Tworzenie wszystkich schematów najbardziej przydatne w jednym miejscu toosee [pulpitu nawigacyjnego](app-insights-dashboards.md) i przypiąć je tooit.</span><span class="sxs-lookup"><span data-stu-id="fa86a-117">toosee all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them tooit.</span></span>

## <a name="add-counters"></a><span data-ttu-id="fa86a-118">Dodawanie liczników</span><span class="sxs-lookup"><span data-stu-id="fa86a-118">Add counters</span></span>
<span data-ttu-id="fa86a-119">Jeśli hello licznika wydajności, które mają nie są wyświetlane w liście hello metryki, ponieważ hello zestaw SDK usługi Application Insights nie jest zbieranie go na serwerze sieci web.</span><span class="sxs-lookup"><span data-stu-id="fa86a-119">If hello performance counter you want isn't shown in hello list of metrics, that's because hello Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="fa86a-120">Można go skonfigurować toodo tak.</span><span class="sxs-lookup"><span data-stu-id="fa86a-120">You can configure it toodo so.</span></span>

1. <span data-ttu-id="fa86a-121">Sprawdzić, jakie liczniki są dostępne na serwerze za pomocą tego polecenia programu PowerShell na serwerze hello:</span><span class="sxs-lookup"><span data-stu-id="fa86a-121">Find out what counters are available in your server by using this PowerShell command at hello server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="fa86a-122">(Zobacz [ `Get-Counter` ](https://technet.microsoft.com/library/hh849685.aspx).)</span><span class="sxs-lookup"><span data-stu-id="fa86a-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="fa86a-123">Otwórz ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="fa86a-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="fa86a-124">Jeśli dodano usługę Application Insights tooyour aplikacji podczas tworzenia, edycji ApplicationInsights.config w projekcie, a następnie ponownie go wdrożyć serwery tooyour.</span><span class="sxs-lookup"><span data-stu-id="fa86a-124">If you added Application Insights tooyour app during development, edit ApplicationInsights.config in your project, and then re-deploy it tooyour servers.</span></span>
   * <span data-ttu-id="fa86a-125">Jeśli używasz tooinstrument Monitor stanu aplikacji sieci web w czasie wykonywania, można znaleźć pliku ApplicationInsights.config w katalogu głównym hello aplikacji hello w usługach IIS.</span><span class="sxs-lookup"><span data-stu-id="fa86a-125">If you used Status Monitor tooinstrument a web app at runtime, find ApplicationInsights.config in hello root directory of hello app in IIS.</span></span> <span data-ttu-id="fa86a-126">Zaktualizuj ją w tym miejscu w każdym wystąpieniu serwera.</span><span class="sxs-lookup"><span data-stu-id="fa86a-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="fa86a-127">Edytuj hello wydajności moduł zbierający dyrektywy:</span><span class="sxs-lookup"><span data-stu-id="fa86a-127">Edit hello performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="fa86a-128">Można przechwycić zarówno liczniki standard, jak i te zostały zaimplementowane samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="fa86a-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="fa86a-129">`\Objects\Processes`Przykładem standardowe licznika, dostępne we wszystkich systemach Windows.</span><span class="sxs-lookup"><span data-stu-id="fa86a-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="fa86a-130">`\Sales(photo)\# Items Sold`jest to przykład liczników niestandardowych, które można zaimplementować w usłudze sieci web.</span><span class="sxs-lookup"><span data-stu-id="fa86a-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="fa86a-131">Hello format jest `\Category(instance)\Counter"`, lub dla kategorii, które nie mają wystąpień, po prostu `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="fa86a-131">hello format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="fa86a-132">`ReportAs`jest wymagany dla nazwy liczników, które nie są zgodne `[a-zA-Z()/-_ \.]+` -oznacza to, zawiera znaki, które nie znajdują się w następujących zestawów hello: litery round nawiasy, ukośnik, łącznik, podkreślenie, miejsca, kropka.</span><span class="sxs-lookup"><span data-stu-id="fa86a-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in hello following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="fa86a-133">Jeśli określisz wystąpienia będą zbierane zgłoszonej wymiaru "CounterInstanceName" z hello metryki.</span><span class="sxs-lookup"><span data-stu-id="fa86a-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of hello reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="fa86a-134">Zbierania liczników wydajności w kodzie</span><span class="sxs-lookup"><span data-stu-id="fa86a-134">Collecting performance counters in code</span></span>
<span data-ttu-id="fa86a-135">wydajność systemu toocollect liczników i wysyłać je tooApplication Insights, można dostosować poniższy fragment hello:</span><span class="sxs-lookup"><span data-stu-id="fa86a-135">toocollect system performance counters and send them tooApplication Insights, you can adapt hello snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="fa86a-136">Lub możesz wykonać hello samo z tworzenia metryki niestandardowe:</span><span class="sxs-lookup"><span data-stu-id="fa86a-136">Or you can do hello same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="fa86a-137">Liczniki wydajności w module analiz</span><span class="sxs-lookup"><span data-stu-id="fa86a-137">Performance counters in Analytics</span></span>
<span data-ttu-id="fa86a-138">Można wyszukiwać i wyświetlać raporty licznika wydajności w [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="fa86a-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="fa86a-139">Witaj **liczniki wydajności** schemat przedstawia hello `category`, `counter` nazwa, i `instance` nazwę każdego licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="fa86a-139">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="fa86a-140">W danych telemetrycznych powitania dla każdej aplikacji zostanie wyświetlony tylko hello liczniki dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fa86a-140">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="fa86a-141">Na przykład toosee jakie liczniki są dostępne:</span><span class="sxs-lookup"><span data-stu-id="fa86a-141">For example, toosee what counters are available:</span></span> 

![Liczniki wydajności w module analiz usługi Application Insights](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="fa86a-143">(W tym miejscu "Instance" odwołuje się wystąpienia licznika wydajności toohello, nie hello rola lub serwer wystąpienie maszyny.</span><span class="sxs-lookup"><span data-stu-id="fa86a-143">('Instance' here refers toohello performance counter instance,  not hello role or server machine instance.</span></span> <span data-ttu-id="fa86a-144">Nazwa wystąpienia liczników wydajności Hello zwykle segmenty liczników, takie jak czas procesora według nazwy hello procesu hello lub aplikacji.)</span><span class="sxs-lookup"><span data-stu-id="fa86a-144">hello performance counter instance name typically segments counters such as processor time by hello name of hello process or application.)</span></span>

<span data-ttu-id="fa86a-145">tooget wykresu dostępnej pamięci na powitania ostatnim okresie:</span><span class="sxs-lookup"><span data-stu-id="fa86a-145">tooget a chart of available memory over hello recent period:</span></span> 

![Timechart pamięci w module analiz usługi Application Insights](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="fa86a-147">Inne telemetrii, takich jak **liczniki wydajności** również zawiera kolumnę `cloud_RoleInstance` wskazujące hello tożsamość hello hosta serwera wystąpienia, na którym działa aplikacja.</span><span class="sxs-lookup"><span data-stu-id="fa86a-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host server instance on which your app is running.</span></span> <span data-ttu-id="fa86a-148">Na przykład toocompare hello wydajności aplikacji na różnych komputerach hello:</span><span class="sxs-lookup"><span data-stu-id="fa86a-148">For example, toocompare hello performance of your app on hello different machines:</span></span> 

![Wydajność segmentowanych przez wystąpienie roli w usłudze Application Insights analityka](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="fa86a-150">ASP.NET i liczby usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="fa86a-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="fa86a-151">*Co to jest hello różnica między hello wyjątek szybkość i metryki wyjątki?*</span><span class="sxs-lookup"><span data-stu-id="fa86a-151">*What's hello difference between hello Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="fa86a-152">*Szybkość wyjątek* jest licznika wydajności systemu.</span><span class="sxs-lookup"><span data-stu-id="fa86a-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="fa86a-153">Witaj CLR zlicza wszystkie hello obsługiwane i nieobsługiwane wyjątki, które są zgłaszane i dzieli hello razem w interwale próbkowania przez długość interwału powitania hello.</span><span class="sxs-lookup"><span data-stu-id="fa86a-153">hello CLR counts all hello handled and unhandled exceptions that are thrown, and divides hello total in a sampling interval by hello length of hello interval.</span></span> <span data-ttu-id="fa86a-154">Witaj zestaw SDK usługi Application Insights zbiera wynik i wysyła je z toohello portalu.</span><span class="sxs-lookup"><span data-stu-id="fa86a-154">hello Application Insights SDK collects this result and sends it toohello portal.</span></span>
* <span data-ttu-id="fa86a-155">*Wyjątki* jest liczba hello raportów TrackException odebranych przez portal hello w interwale próbkowania hello hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="fa86a-155">*Exceptions* is a count of hello TrackException reports received by hello portal in hello sampling interval of hello chart.</span></span> <span data-ttu-id="fa86a-156">Obejmuje on tylko hello obsługi wyjątków, których napisano TrackException wywołuje w kodzie i nie zawiera wszystkich [nieobsługiwane wyjątki](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="fa86a-156">It includes only hello handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="fa86a-157">Alerty</span><span class="sxs-lookup"><span data-stu-id="fa86a-157">Alerts</span></span>
<span data-ttu-id="fa86a-158">Podobnie jak inne metryki, możesz [ustawić alert](app-insights-alerts.md) toowarn, jeśli licznik wydajności odbędzie się poza limit określisz.</span><span class="sxs-lookup"><span data-stu-id="fa86a-158">Like other metrics, you can [set an alert](app-insights-alerts.md) toowarn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="fa86a-159">Otwiera blok alerty hello, a następnie kliknij przycisk Dodaj alertu.</span><span class="sxs-lookup"><span data-stu-id="fa86a-159">Open hello Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="fa86a-160"><a name="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa86a-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="fa86a-161">Śledzenia zależności</span><span class="sxs-lookup"><span data-stu-id="fa86a-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="fa86a-162">Śledzenie wyjątków</span><span class="sxs-lookup"><span data-stu-id="fa86a-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

