---
title: aaaFilter Azure Application Insights telemetrii w aplikacji sieci web Java | Dokumentacja firmy Microsoft
description: "Zmniejszenie ruchu telemetrii przez filtrowanie hello zdarzeń nie ma potrzeby toomonitor."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 95713e11d5f86472777c67e4e7f3177fbf2cd0b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="3f7f0-103">Filtr telemetrii w aplikacji sieci web Java</span><span class="sxs-lookup"><span data-stu-id="3f7f0-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="3f7f0-104">Filtry zapewniają sposób tooselect hello telemetrii z [aplikacji sieci web Java wysyła tooApplication Insights](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3f7f0-104">Filters provide a way tooselect hello telemetry that your [Java web app sends tooApplication Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="3f7f0-105">Brak niektórych filtrów poza pole, które można użyć, a można również napisać własny filtry niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="3f7f0-106">dostępne są następujące filtry poza pole Hello:</span><span class="sxs-lookup"><span data-stu-id="3f7f0-106">hello out-of-the-box filters include:</span></span>

* <span data-ttu-id="3f7f0-107">Poziom ważności śledzenia</span><span class="sxs-lookup"><span data-stu-id="3f7f0-107">Trace severity level</span></span>
* <span data-ttu-id="3f7f0-108">Określone adresy URL, słowa kluczowe lub kodów odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="3f7f0-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="3f7f0-109">Krótkie czasy odpowiedzi — to znaczy żądań toowhich tooquickly odpowiedzi aplikacji</span><span class="sxs-lookup"><span data-stu-id="3f7f0-109">Fast responses - that is, requests toowhich your app responded tooquickly</span></span>
* <span data-ttu-id="3f7f0-110">Nazwy określonego zdarzenia</span><span class="sxs-lookup"><span data-stu-id="3f7f0-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="3f7f0-111">Filtry pochylanie metryki hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-111">Filters skew hello metrics of your app.</span></span> <span data-ttu-id="3f7f0-112">Na przykład można zdecydować, że w kolejności toodiagnose powolne odpowiedzi spowoduje ustawienie filtru toodiscard krótszych czasów reakcji.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-112">For example, you might decide that, in order toodiagnose slow responses, you will set a filter toodiscard fast response times.</span></span> <span data-ttu-id="3f7f0-113">Jednak należy pamiętać, że czasy odpowiedzi średni hello zgłoszone przez usługę Application Insights będzie mniejsza niż szybkość true hello i hello liczba żądań będą mniejsze niż rzeczywista liczba hello.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-113">But you must be aware that hello average response times reported by Application Insights will then be slower than hello true speed, and hello count of requests will be smaller than hello real count.</span></span>
> <span data-ttu-id="3f7f0-114">W przypadku wątpliwości dotyczących użycia [próbkowania](app-insights-sampling.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="3f7f0-115">Filtry</span><span class="sxs-lookup"><span data-stu-id="3f7f0-115">Setting filters</span></span>

<span data-ttu-id="3f7f0-116">W ApplicationInsights.xml, Dodaj `TelemetryProcessors` sekcji tak jak ten przykład:</span><span class="sxs-lookup"><span data-stu-id="3f7f0-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want toosee -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




<span data-ttu-id="3f7f0-117">[Sprawdź hello pełny zestaw wbudowanych procesorów](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="3f7f0-117">[Inspect hello full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="3f7f0-118">Filtry wbudowane</span><span class="sxs-lookup"><span data-stu-id="3f7f0-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="3f7f0-119">Filtr dane telemetryczne metryki</span><span class="sxs-lookup"><span data-stu-id="3f7f0-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="3f7f0-120">`NotNeeded`-Rozdzielana przecinkami lista nazw metryki niestandardowe.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="3f7f0-121">Filtr dane telemetryczne wyświetleń strony</span><span class="sxs-lookup"><span data-stu-id="3f7f0-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="3f7f0-122">`DurationThresholdInMS`— Czas trwania odnosi się czas toohello tooload hello strony.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-122">`DurationThresholdInMS` - Duration refers toohello time taken tooload hello page.</span></span> <span data-ttu-id="3f7f0-123">Jeśli ta opcja jest ustawiona, nie są zgłaszane stron, które szybciej niż w tej chwili załadowane.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="3f7f0-124">`NotNeededNames`-Rozdzielana przecinkami lista nazw strony.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="3f7f0-125">`NotNeededUrls`— Fragmenty rozdzielana przecinkami lista adresów URL.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="3f7f0-126">Na przykład `"home"` odfiltrowuje wszystkie strony, które mają "Strona główna" w adresie URL hello.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-126">For example, `"home"` filters out all pages that have "home" in hello URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="3f7f0-127">Żądanie Telemetrii filtru</span><span class="sxs-lookup"><span data-stu-id="3f7f0-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="3f7f0-128">Syntetyczne Filtr źródła</span><span class="sxs-lookup"><span data-stu-id="3f7f0-128">Synthetic Source filter</span></span>

<span data-ttu-id="3f7f0-129">Odfiltrowuje wszystkie dane telemetryczne, te wartości w hello SyntheticSource właściwości.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-129">Filters out all telemetry that have values in hello SyntheticSource property.</span></span> <span data-ttu-id="3f7f0-130">Obejmują one żądań z robotów, przeszukiwarki i testów dostępności.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="3f7f0-131">Odfiltrować dane telemetryczne dla wszystkich żądań syntetycznych:</span><span class="sxs-lookup"><span data-stu-id="3f7f0-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="3f7f0-132">Odfiltrować dane telemetryczne dla konkretnych źródeł syntetycznych:</span><span class="sxs-lookup"><span data-stu-id="3f7f0-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="3f7f0-133">`NotNeeded`-Rozdzielana przecinkami lista nazw syntetycznego źródła.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="3f7f0-134">Filtr zdarzeń telemetrii</span><span class="sxs-lookup"><span data-stu-id="3f7f0-134">Telemetry Event filter</span></span>

<span data-ttu-id="3f7f0-135">Filtruje zdarzenia niestandardowe (zarejestrowane przy użyciu [funkcji TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="3f7f0-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="3f7f0-136">`NotNeededNames`-Rozdzielana przecinkami lista nazw zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="3f7f0-137">Filtr dane telemetryczne śledzenia</span><span class="sxs-lookup"><span data-stu-id="3f7f0-137">Trace Telemetry filter</span></span>

<span data-ttu-id="3f7f0-138">Filtry dziennika śledzenia (zarejestrowane przy użyciu [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lub [moduł zbierający framework rejestrowania](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="3f7f0-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="3f7f0-139">`FromSeverityLevel`Prawidłowe wartości to:</span><span class="sxs-lookup"><span data-stu-id="3f7f0-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="3f7f0-140">WYŁĄCZONE — odfiltrować wszystkie ślady</span><span class="sxs-lookup"><span data-stu-id="3f7f0-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="3f7f0-141">TRACE — bez filtrowania.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-141">TRACE           - No filtering.</span></span> <span data-ttu-id="3f7f0-142">poziom tooTrace Equals</span><span class="sxs-lookup"><span data-stu-id="3f7f0-142">equals tooTrace level</span></span>
 *  <span data-ttu-id="3f7f0-143">Informacje o — filtr się poziom śledzenia</span><span class="sxs-lookup"><span data-stu-id="3f7f0-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="3f7f0-144">OSTRZEGAJ - filtru śledzenia i informacji</span><span class="sxs-lookup"><span data-stu-id="3f7f0-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="3f7f0-145">Błąd — filtr limit OSTRZEGAJ, INFO, śledzenia</span><span class="sxs-lookup"><span data-stu-id="3f7f0-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="3f7f0-146">KRYTYCZNY - filtru limit wszystkie krytyczne</span><span class="sxs-lookup"><span data-stu-id="3f7f0-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="3f7f0-147">Filtry niestandardowe</span><span class="sxs-lookup"><span data-stu-id="3f7f0-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="3f7f0-148">1. Kod filtru</span><span class="sxs-lookup"><span data-stu-id="3f7f0-148">1. Code your filter</span></span>

<span data-ttu-id="3f7f0-149">W kodzie, Utwórz klasę, która implementuje `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="3f7f0-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required toosupport hello filter.*/
       private final String successful;

       /* Initializers for hello parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry toobe sent.
          Return false toodiscard it.
          Return true tooallow other processors tooinspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a><span data-ttu-id="3f7f0-150">2. Wywołania z filtrem w pliku konfiguracyjnym hello</span><span class="sxs-lookup"><span data-stu-id="3f7f0-150">2. Invoke your filter in hello configuration file</span></span>

<span data-ttu-id="3f7f0-151">W ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="3f7f0-151">In ApplicationInsights.xml:</span></span>

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a><span data-ttu-id="3f7f0-152">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="3f7f0-152">Troubleshooting</span></span>

<span data-ttu-id="3f7f0-153">*Moje filtru nie działa.*</span><span class="sxs-lookup"><span data-stu-id="3f7f0-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="3f7f0-154">Sprawdź, czy podano prawidłowymi wartościami parametrów.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="3f7f0-155">Na przykład czas trwania powinny być liczbami całkowitymi.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-155">For example, durations should be integers.</span></span> <span data-ttu-id="3f7f0-156">Nieprawidłowe wartości spowoduje, że toobe filtru hello ignorowane.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-156">Invalid values will cause hello filter toobe ignored.</span></span> <span data-ttu-id="3f7f0-157">Niestandardowy filtr zgłasza wyjątek konstruktora lub metody set, zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f7f0-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f7f0-158">Next steps</span></span>

* <span data-ttu-id="3f7f0-159">[Próbkowanie](app-insights-sampling.md) — należy wziąć pod uwagę próbkowania jako alternatywę nie pochylanie Twoje metryki.</span><span class="sxs-lookup"><span data-stu-id="3f7f0-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
