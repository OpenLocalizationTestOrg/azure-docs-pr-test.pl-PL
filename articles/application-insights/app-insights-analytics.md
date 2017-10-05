---
title: "Analityka — narzędzie wyszukiwania zaawansowanego w Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Przegląd analizowanie narzędziu zaawansowane wyszukiwanie diagnostycznych z usługi Application Insights. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8174745a00a107eea648b223a00466b6a7f37331
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="analytics-in-application-insights"></a>Analityka w usłudze Application Insights
[Analiza](app-insights-analytics.md) to funkcja wyszukiwania zaawansowanego [usługi Application Insights](app-insights-overview.md). Te strony opisano język zapytań usługi Analiza dzienników. 

* **[Obejrzyj klip wideo wprowadzenia](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Przetestuj Analytics na naszych danych symulowane](https://analytics.applicationinsights.io/demo)**  aplikacji nie jest wysyłania danych do usługi Application Insights jeszcze.
* **[Ściągawka SQL użytkowników](https://aka.ms/sql-analytics)**  tłumaczy idioms najczęściej.
* **[Dokumentacja języka](app-insights-analytics-reference.md)**  informacje o sposobie korzystania z zaawansowanych funkcji języka zapytań usługi Analiza dzienników.


## <a name="queries-in-analytics"></a>Kwerendy w module analiz
Typowe zapytania jest *źródła* tabeli następuje szereg *operatory* rozdzielone `|`. 

Na przykład załóżmy sprawdzić pory dnia obywateli Hyderabad spróbuj swoją aplikację sieci web. I są nam Zobaczmy, jakie kody wyników są zwracane do ich żądania HTTP. 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

Firma Microsoft liczba adresów IP klientów distinct, zgrupować je za godzinę dnia w ciągu ostatnich 7 dni. 

> [!NOTE]
> Aby uzyskać wyniki poza poprzednich 24 godzin, jawnie zawierały "timestamp" w zapytaniu albo użyj menu rozwijanego zakresu czasu.
>

Umożliwia wyświetlanie wyników z prezentacją wykres słupkowy, wybierając stosu wyników z kodów odpowiedzi różne:

![Wybierz wykres słupkowy, x i y osi, a następnie segmentacji](./media/app-insights-analytics/020.png)

Wygląda na to lunchtime i bielizny czasu w Hyderabad aplikacji cieszy się największą popularnością. (I firma Microsoft powinien być sprawdzony tych kodów 500.)

Dostępne są również zaawansowane operacje statystyczne:

![Wyniki zapytania statystyczne](./media/app-insights-analytics/025.png)

Język ma wiele atrakcyjne funkcje:


* [Filtr](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) telemetrii raw aplikacji przez wszystkie pola, w tym właściwości niestandardowych i metryki.
* [Dołącz](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) wielu tabel — korelując żądania z wyświetleń strony, wywołania zależności, wyjątków i ślady dziennika.
* Zaawansowane statystyczne [agregacji](https://docs.loganalytics.io/learn/tutorials/aggregations.html).
* Równie wydajne jako SQL, ale znacznie łatwiejsze w przypadku złożonych zapytań: zamiast instrukcji zagnieżdżenia potoku danych z jednej operacji podstawowe do następnego.
* Natychmiastowe i zaawansowane wizualizacje.
* [Przypnij wykresy, aby pulpity nawigacyjne Azure](app-insights-analytics-using.md#pin-to-dashboard).
* [Eksportuj zapytania do usługi Power BI](app-insights-analytics-using.md#export-to-power-bi).
* Brak [interfejsu API REST](https://dev.applicationinsights.io/) czy służy do wykonywania kwerend programowo, na przykład z programu Powershell.


## <a name="connect-to-your-application-insights-data"></a>Połącz z danymi usługi Application Insights
Otwórz Analytics z aplikacji [bloku omówienie](app-insights-dashboards.md) w usłudze Application Insights: 

![Otwórz portal.azure.com otworzyć zasobu usługi Application Insights, a następnie kliknij przycisk Analytics.](./media/app-insights-analytics/001.png)


## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a>Przykłady zapytań

Wypróbuj te wskazówki ilustrujący możliwości za pomocą analizy:

 *  [Automatyczne diagnostyki wzrostów i krok przechodzi w czas trwania żądania](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [Analizowanie wydajności degradations z analizy serii czasowych](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [Analizowanie błędów aplikacji z autocluster i diffpatterns](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [Wykryć zaawansowane kształt z analizy serii czasowych](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [Za pomocą przesuwanego okna operacji do analizy użycia aplikacji (przewijane MAU/DAU itp.)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  [Wykrywanie zakłócenia w świadczeniu usług, oparte na analizie dzienników debugowania](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).
 *  [Profilowanie wydajności aplikacji za pomocą prostego dzienniki](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)
 *  [Pomiar czasu trwania dla każdego kroku w Twojej przepływu kodu przy użyciu dzienników debugowania proste](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *  [Analizowanie danych współbieżności przy użyciu dzienników debugowania proste](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)



## <a name="next-steps"></a>Następne kroki
* Zalecamy rozpocząć od [samouczek języka](app-insights-analytics-tour.md). 
* Więcej informacji o [przy użyciu Analytics](app-insights-analytics-using.md). 
* [Dokumentacja języka](app-insights-analytics-reference.md). 
