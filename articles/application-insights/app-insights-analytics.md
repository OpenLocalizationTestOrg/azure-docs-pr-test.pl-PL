---
title: "aaaAnalytics — narzędzie wyszukiwania zaawansowanego hello Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Omówienie usługi Analytics, hello wydajne diagnostycznych narzędzie do wyszukiwania usługi Application insights. "
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
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a>Analityka w usłudze Application Insights
[Analiza](app-insights-analytics.md) to funkcja wyszukiwania zaawansowanego hello [usługi Application Insights](app-insights-overview.md). Te strony opisano język zapytań usługi Analiza dzienników. 

* **[Obejrzyj klip wideo wprowadzenia hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Przetestuj Analytics na naszych danych symulowane](https://analytics.applicationinsights.io/demo)**  aplikacji nie jest jeszcze wysyłania danych tooApplication szczegółowych informacji.
* **[Ściągawka SQL użytkowników](https://aka.ms/sql-analytics)**  tłumaczy hello idioms najczęściej.
* **[Dokumentacja języka](app-insights-analytics-reference.md)**  Dowiedz się, jak wszystkie toouse hello zaawansowanych funkcji hello język zapytań usługi Analiza dzienników.


## <a name="queries-in-analytics"></a>Kwerendy w module analiz
Typowe zapytania jest *źródła* tabeli następuje szereg *operatory* rozdzielone `|`. 

Na przykład załóżmy Dowiedz się pory dnia obywateli hello Hyderabad spróbuj swoją aplikację sieci web. I są nam Zobaczmy, jakie kody wyników są zwracane tootheir HTTP żądania. 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

Firma Microsoft liczba adresów IP unikatowych klientów, ich grupowanie hello godzinę dnia hello za pośrednictwem hello w ciągu ostatnich 7 dni. 

> [!NOTE]
> wyniki tooget poza hello poprzednich 24 godzin, jawnie zawierały "timestamp" w zapytaniu, albo użyj menu rozwijanego zakres czasu hello.
>

Umożliwia wyświetlenie hello wyniki z hello paska prezentacji wykresu, wybierając toostack hello wyników z kodów odpowiedzi różnych:

![Wybierz wykres słupkowy, x i y osi, a następnie segmentacji](./media/app-insights-analytics/020.png)

Wygląda na to lunchtime i bielizny czasu w Hyderabad aplikacji cieszy się największą popularnością. (I firma Microsoft powinien być sprawdzony tych kodów 500.)

Dostępne są również zaawansowane operacje statystyczne:

![Wyniki zapytania statystyczne](./media/app-insights-analytics/025.png)

język Hello oferuje wiele funkcji atrakcyjne:


* [Filtr](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) telemetrii raw aplikacji przez wszystkie pola, w tym właściwości niestandardowych i metryki.
* [Dołącz](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) wielu tabel — korelując żądania z wyświetleń strony, wywołania zależności, wyjątków i ślady dziennika.
* Zaawansowane statystyczne [agregacji](https://docs.loganalytics.io/learn/tutorials/aggregations.html).
* Równie wydajne jako SQL, ale znacznie łatwiejsze w przypadku złożonych zapytań: zamiast zagnieżdżenia instrukcje należy przekazać w potoku hello danych z jednego toohello podstawowych operacji obok.
* Natychmiastowe i zaawansowane wizualizacje.
* [Numer PIN wykresy, pulpity nawigacyjne tooAzure](app-insights-analytics-using.md#pin-to-dashboard).
* [Eksportuj tooPower zapytania BI](app-insights-analytics-using.md#export-to-power-bi).
* Brak [interfejsu API REST](https://dev.applicationinsights.io/) służącego zapytania toorun programowo, na przykład z programu Powershell.


## <a name="connect-tooyour-application-insights-data"></a>Połącz dane usługi Application Insights tooyour
Otwórz Analytics z aplikacji [bloku omówienie](app-insights-dashboards.md) w usłudze Application Insights: 

![Otwórz portal.azure.com otworzyć zasobu usługi Application Insights, a następnie kliknij przycisk Analytics.](./media/app-insights-analytics/001.png)


## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a>Przykłady zapytań

Wypróbuj te wskazówki tooillustrate hello możliwości przy użyciu Analytics:

 *  [Automatyczne diagnostyki wzrostów i krok przechodzi w czas trwania żądania](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [Analizowanie wydajności degradations z analizy serii czasowych](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [Analizowanie błędów aplikacji z autocluster i diffpatterns](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [Wykryć zaawansowane kształt z analizy serii czasowych](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [Użycie przesuwanego okna operacji tooanalyze aplikacji (przewijane MAU/DAU itp.)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  [Wykrywanie zakłócenia w świadczeniu usług, oparte na analizie dzienników debugowania](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).
 *  [Profilowanie wydajności aplikacji za pomocą prostego dzienniki](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)
 *  [Pomiar czasu trwania powitania dla każdego kroku w Twojej przepływu kodu przy użyciu dzienników debugowania proste](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *  [Analizowanie danych współbieżności przy użyciu dzienników debugowania proste](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)



## <a name="next-steps"></a>Następne kroki
* Zaleca się rozpoczynać hello [samouczek języka](app-insights-analytics-tour.md). 
* Więcej informacji o [przy użyciu Analytics](app-insights-analytics-using.md). 
* [Dokumentacja języka](app-insights-analytics-reference.md). 
