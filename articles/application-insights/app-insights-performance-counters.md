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
# <a name="system-performance-counters-in-application-insights"></a>Liczniki wydajności systemu w usłudze Application Insights
System Windows udostępnia wiele różnych [liczniki wydajności](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) takich jak zajęte Procesora, pamięci, dysku i użycia sieci. Możesz również definiować własnych. [Usługa Application Insights](app-insights-overview.md) mogą być prezentowane z tych liczników wydajności, jeśli aplikacja działa w środowisku usług IIS na lokalnym toowhich hosta lub maszyny wirtualnej należy mieć dostęp administracyjny. Wykresy Hello wskazać hello zasoby dostępne tooyour działającej aplikacji i może ułatwić tooidentify obciążenia równowagi między wystąpieniami serwera.

Liczniki wydajności są wyświetlane w bloku serwerów hello, w tym segmentów zawiera tabelę przez wystąpienie serwera.

![Liczniki wydajności zgłoszonych w usłudze Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

(Liczniki wydajności nie są dostępne dla aplikacji sieci Web Azure. Ale możesz [wysyłania Insights tooApplication diagnostyki Azure](app-insights-azure-diagnostics.md).)

## <a name="view-counters"></a>Wyświetlanie liczników
Blok serwerów Hello Pokazuje domyślny zbiór liczników wydajności. 

toosee innych liczników edytowanie hello wykresów na powitania blok serwerów albo otwórz nowe [Eksploratora metryk](app-insights-metrics-explorer.md) bloku i dodawanie nowych schematów. 

dostępne liczniki Hello są wyświetlane jako metryki podczas edytowania wykresu.

![Liczniki wydajności zgłoszonych w usłudze Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

Tworzenie wszystkich schematów najbardziej przydatne w jednym miejscu toosee [pulpitu nawigacyjnego](app-insights-dashboards.md) i przypiąć je tooit.

## <a name="add-counters"></a>Dodawanie liczników
Jeśli hello licznika wydajności, które mają nie są wyświetlane w liście hello metryki, ponieważ hello zestaw SDK usługi Application Insights nie jest zbieranie go na serwerze sieci web. Można go skonfigurować toodo tak.

1. Sprawdzić, jakie liczniki są dostępne na serwerze za pomocą tego polecenia programu PowerShell na serwerze hello:
   
    `Get-Counter -ListSet *`
   
    (Zobacz [ `Get-Counter` ](https://technet.microsoft.com/library/hh849685.aspx).)
2. Otwórz ApplicationInsights.config.
   
   * Jeśli dodano usługę Application Insights tooyour aplikacji podczas tworzenia, edycji ApplicationInsights.config w projekcie, a następnie ponownie go wdrożyć serwery tooyour.
   * Jeśli używasz tooinstrument Monitor stanu aplikacji sieci web w czasie wykonywania, można znaleźć pliku ApplicationInsights.config w katalogu głównym hello aplikacji hello w usługach IIS. Zaktualizuj ją w tym miejscu w każdym wystąpieniu serwera.
3. Edytuj hello wydajności moduł zbierający dyrektywy:
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

Można przechwycić zarówno liczniki standard, jak i te zostały zaimplementowane samodzielnie. `\Objects\Processes`Przykładem standardowe licznika, dostępne we wszystkich systemach Windows. `\Sales(photo)\# Items Sold`jest to przykład liczników niestandardowych, które można zaimplementować w usłudze sieci web. 

Hello format jest `\Category(instance)\Counter"`, lub dla kategorii, które nie mają wystąpień, po prostu `\Category\Counter`.

`ReportAs`jest wymagany dla nazwy liczników, które nie są zgodne `[a-zA-Z()/-_ \.]+` -oznacza to, zawiera znaki, które nie znajdują się w następujących zestawów hello: litery round nawiasy, ukośnik, łącznik, podkreślenie, miejsca, kropka.

Jeśli określisz wystąpienia będą zbierane zgłoszonej wymiaru "CounterInstanceName" z hello metryki.

### <a name="collecting-performance-counters-in-code"></a>Zbierania liczników wydajności w kodzie
wydajność systemu toocollect liczników i wysyłać je tooApplication Insights, można dostosować poniższy fragment hello:


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

Lub możesz wykonać hello samo z tworzenia metryki niestandardowe:

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a>Liczniki wydajności w module analiz
Można wyszukiwać i wyświetlać raporty licznika wydajności w [Analytics](app-insights-analytics.md).

Witaj **liczniki wydajności** schemat przedstawia hello `category`, `counter` nazwa, i `instance` nazwę każdego licznika wydajności.  W danych telemetrycznych powitania dla każdej aplikacji zostanie wyświetlony tylko hello liczniki dla tej aplikacji. Na przykład toosee jakie liczniki są dostępne: 

![Liczniki wydajności w module analiz usługi Application Insights](./media/app-insights-performance-counters/analytics-performance-counters.png)

(W tym miejscu "Instance" odwołuje się wystąpienia licznika wydajności toohello, nie hello rola lub serwer wystąpienie maszyny. Nazwa wystąpienia liczników wydajności Hello zwykle segmenty liczników, takie jak czas procesora według nazwy hello procesu hello lub aplikacji.)

tooget wykresu dostępnej pamięci na powitania ostatnim okresie: 

![Timechart pamięci w module analiz usługi Application Insights](./media/app-insights-performance-counters/analytics-available-memory.png)

Inne telemetrii, takich jak **liczniki wydajności** również zawiera kolumnę `cloud_RoleInstance` wskazujące hello tożsamość hello hosta serwera wystąpienia, na którym działa aplikacja. Na przykład toocompare hello wydajności aplikacji na różnych komputerach hello: 

![Wydajność segmentowanych przez wystąpienie roli w usłudze Application Insights analityka](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a>ASP.NET i liczby usługi Application Insights
*Co to jest hello różnica między hello wyjątek szybkość i metryki wyjątki?*

* *Szybkość wyjątek* jest licznika wydajności systemu. Witaj CLR zlicza wszystkie hello obsługiwane i nieobsługiwane wyjątki, które są zgłaszane i dzieli hello razem w interwale próbkowania przez długość interwału powitania hello. Witaj zestaw SDK usługi Application Insights zbiera wynik i wysyła je z toohello portalu.
* *Wyjątki* jest liczba hello raportów TrackException odebranych przez portal hello w interwale próbkowania hello hello wykresu. Obejmuje on tylko hello obsługi wyjątków, których napisano TrackException wywołuje w kodzie i nie zawiera wszystkich [nieobsługiwane wyjątki](app-insights-asp-net-exceptions.md). 

## <a name="alerts"></a>Alerty
Podobnie jak inne metryki, możesz [ustawić alert](app-insights-alerts.md) toowarn, jeśli licznik wydajności odbędzie się poza limit określisz. Otwiera blok alerty hello, a następnie kliknij przycisk Dodaj alertu.

## <a name="next"></a>Następne kroki
* [Śledzenia zależności](app-insights-asp-net-dependencies.md)
* [Śledzenie wyjątków](app-insights-asp-net-exceptions.md)

