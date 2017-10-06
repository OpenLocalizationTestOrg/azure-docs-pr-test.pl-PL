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
# <a name="filter-telemetry-in-your-java-web-app"></a>Filtr telemetrii w aplikacji sieci web Java

Filtry zapewniają sposób tooselect hello telemetrii z [aplikacji sieci web Java wysyła tooApplication Insights](app-insights-java-get-started.md). Brak niektórych filtrów poza pole, które można użyć, a można również napisać własny filtry niestandardowe.

dostępne są następujące filtry poza pole Hello:

* Poziom ważności śledzenia
* Określone adresy URL, słowa kluczowe lub kodów odpowiedzi
* Krótkie czasy odpowiedzi — to znaczy żądań toowhich tooquickly odpowiedzi aplikacji
* Nazwy określonego zdarzenia

> [!NOTE]
> Filtry pochylanie metryki hello aplikacji. Na przykład można zdecydować, że w kolejności toodiagnose powolne odpowiedzi spowoduje ustawienie filtru toodiscard krótszych czasów reakcji. Jednak należy pamiętać, że czasy odpowiedzi średni hello zgłoszone przez usługę Application Insights będzie mniejsza niż szybkość true hello i hello liczba żądań będą mniejsze niż rzeczywista liczba hello.
> W przypadku wątpliwości dotyczących użycia [próbkowania](app-insights-sampling.md) zamiast tego.

## <a name="setting-filters"></a>Filtry

W ApplicationInsights.xml, Dodaj `TelemetryProcessors` sekcji tak jak ten przykład:


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




[Sprawdź hello pełny zestaw wbudowanych procesorów](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).

## <a name="built-in-filters"></a>Filtry wbudowane

### <a name="metric-telemetry-filter"></a>Filtr dane telemetryczne metryki

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* `NotNeeded`-Rozdzielana przecinkami lista nazw metryki niestandardowe.


### <a name="page-view-telemetry-filter"></a>Filtr dane telemetryczne wyświetleń strony

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* `DurationThresholdInMS`— Czas trwania odnosi się czas toohello tooload hello strony. Jeśli ta opcja jest ustawiona, nie są zgłaszane stron, które szybciej niż w tej chwili załadowane.
* `NotNeededNames`-Rozdzielana przecinkami lista nazw strony.
* `NotNeededUrls`— Fragmenty rozdzielana przecinkami lista adresów URL. Na przykład `"home"` odfiltrowuje wszystkie strony, które mają "Strona główna" w adresie URL hello.


### <a name="request-telemetry-filter"></a>Żądanie Telemetrii filtru


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a>Syntetyczne Filtr źródła

Odfiltrowuje wszystkie dane telemetryczne, te wartości w hello SyntheticSource właściwości. Obejmują one żądań z robotów, przeszukiwarki i testów dostępności.

Odfiltrować dane telemetryczne dla wszystkich żądań syntetycznych:


```XML

           <Processor type="SyntheticSourceFilter" />
```

Odfiltrować dane telemetryczne dla konkretnych źródeł syntetycznych:


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* `NotNeeded`-Rozdzielana przecinkami lista nazw syntetycznego źródła.

### <a name="telemetry-event-filter"></a>Filtr zdarzeń telemetrii

Filtruje zdarzenia niestandardowe (zarejestrowane przy użyciu [funkcji TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* `NotNeededNames`-Rozdzielana przecinkami lista nazw zdarzeń.


### <a name="trace-telemetry-filter"></a>Filtr dane telemetryczne śledzenia

Filtry dziennika śledzenia (zarejestrowane przy użyciu [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lub [moduł zbierający framework rejestrowania](app-insights-java-trace-logs.md)).

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* `FromSeverityLevel`Prawidłowe wartości to:
 *  WYŁĄCZONE — odfiltrować wszystkie ślady
 *  TRACE — bez filtrowania. poziom tooTrace Equals
 *  Informacje o — filtr się poziom śledzenia
 *  OSTRZEGAJ - filtru śledzenia i informacji
 *  Błąd — filtr limit OSTRZEGAJ, INFO, śledzenia
 *  KRYTYCZNY - filtru limit wszystkie krytyczne


## <a name="custom-filters"></a>Filtry niestandardowe

### <a name="1-code-your-filter"></a>1. Kod filtru

W kodzie, Utwórz klasę, która implementuje `TelemetryProcessor`:

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


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a>2. Wywołania z filtrem w pliku konfiguracyjnym hello

W ApplicationInsights.xml:

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

## <a name="troubleshooting"></a>Rozwiązywanie problemów

*Moje filtru nie działa.*

* Sprawdź, czy podano prawidłowymi wartościami parametrów. Na przykład czas trwania powinny być liczbami całkowitymi. Nieprawidłowe wartości spowoduje, że toobe filtru hello ignorowane. Niestandardowy filtr zgłasza wyjątek konstruktora lub metody set, zostaną zignorowane.

## <a name="next-steps"></a>Następne kroki

* [Próbkowanie](app-insights-sampling.md) — należy wziąć pod uwagę próbkowania jako alternatywę nie pochylanie Twoje metryki.
