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
# <a name="analytics-in-application-insights"></a><span data-ttu-id="ba04f-103">Analityka w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="ba04f-103">Analytics in Application Insights</span></span>
<span data-ttu-id="ba04f-104">[Analiza](app-insights-analytics.md) to funkcja wyszukiwania zaawansowanego [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba04f-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="ba04f-105">Te strony opisano język zapytań usługi Analiza dzienników.</span><span class="sxs-lookup"><span data-stu-id="ba04f-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="ba04f-106">**[Obejrzyj klip wideo wprowadzenia](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="ba04f-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="ba04f-107">**[Przetestuj Analytics na naszych danych symulowane](https://analytics.applicationinsights.io/demo)**  aplikacji nie jest wysyłania danych do usługi Application Insights jeszcze.</span><span class="sxs-lookup"><span data-stu-id="ba04f-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="ba04f-108">**[Ściągawka SQL użytkowników](https://aka.ms/sql-analytics)**  tłumaczy idioms najczęściej.</span><span class="sxs-lookup"><span data-stu-id="ba04f-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>
* <span data-ttu-id="ba04f-109">**[Dokumentacja języka](app-insights-analytics-reference.md)**  informacje o sposobie korzystania z zaawansowanych funkcji języka zapytań usługi Analiza dzienników.</span><span class="sxs-lookup"><span data-stu-id="ba04f-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how to use all the powerful features of the Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="ba04f-110">Kwerendy w module analiz</span><span class="sxs-lookup"><span data-stu-id="ba04f-110">Queries in Analytics</span></span>
<span data-ttu-id="ba04f-111">Typowe zapytania jest *źródła* tabeli następuje szereg *operatory* rozdzielone `|`.</span><span class="sxs-lookup"><span data-stu-id="ba04f-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="ba04f-112">Na przykład załóżmy sprawdzić pory dnia obywateli Hyderabad spróbuj swoją aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="ba04f-112">For example, let's find out what time of day the citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="ba04f-113">I są nam Zobaczmy, jakie kody wyników są zwracane do ich żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="ba04f-113">And while we're there, let's see what result codes are returned to their HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="ba04f-114">Firma Microsoft liczba adresów IP klientów distinct, zgrupować je za godzinę dnia w ciągu ostatnich 7 dni.</span><span class="sxs-lookup"><span data-stu-id="ba04f-114">We count distinct client IP addresses, grouping them by the hour of the day over the past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="ba04f-115">Aby uzyskać wyniki poza poprzednich 24 godzin, jawnie zawierały "timestamp" w zapytaniu albo użyj menu rozwijanego zakresu czasu.</span><span class="sxs-lookup"><span data-stu-id="ba04f-115">To get results outside the previous 24h, either include 'timestamp' explicitly in your query, or use the time range drop-down menu.</span></span>
>

<span data-ttu-id="ba04f-116">Umożliwia wyświetlanie wyników z prezentacją wykres słupkowy, wybierając stosu wyników z kodów odpowiedzi różne:</span><span class="sxs-lookup"><span data-stu-id="ba04f-116">Let's display the results with the bar chart presentation, choosing to stack the results from different response codes:</span></span>

![Wybierz wykres słupkowy, x i y osi, a następnie segmentacji](./media/app-insights-analytics/020.png)

<span data-ttu-id="ba04f-118">Wygląda na to lunchtime i bielizny czasu w Hyderabad aplikacji cieszy się największą popularnością.</span><span class="sxs-lookup"><span data-stu-id="ba04f-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="ba04f-119">(I firma Microsoft powinien być sprawdzony tych kodów 500.)</span><span class="sxs-lookup"><span data-stu-id="ba04f-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="ba04f-120">Dostępne są również zaawansowane operacje statystyczne:</span><span class="sxs-lookup"><span data-stu-id="ba04f-120">There are also powerful statistical operations:</span></span>

![Wyniki zapytania statystyczne](./media/app-insights-analytics/025.png)

<span data-ttu-id="ba04f-122">Język ma wiele atrakcyjne funkcje:</span><span class="sxs-lookup"><span data-stu-id="ba04f-122">The language has many attractive features:</span></span>


* <span data-ttu-id="ba04f-123">[Filtr](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) telemetrii raw aplikacji przez wszystkie pola, w tym właściwości niestandardowych i metryki.</span><span class="sxs-lookup"><span data-stu-id="ba04f-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="ba04f-124">[Dołącz](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) wielu tabel — korelując żądania z wyświetleń strony, wywołania zależności, wyjątków i ślady dziennika.</span><span class="sxs-lookup"><span data-stu-id="ba04f-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="ba04f-125">Zaawansowane statystyczne [agregacji](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="ba04f-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="ba04f-126">Równie wydajne jako SQL, ale znacznie łatwiejsze w przypadku złożonych zapytań: zamiast instrukcji zagnieżdżenia potoku danych z jednej operacji podstawowe do następnego.</span><span class="sxs-lookup"><span data-stu-id="ba04f-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe the data from one elementary operation to the next.</span></span>
* <span data-ttu-id="ba04f-127">Natychmiastowe i zaawansowane wizualizacje.</span><span class="sxs-lookup"><span data-stu-id="ba04f-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="ba04f-128">[Przypnij wykresy, aby pulpity nawigacyjne Azure](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="ba04f-128">[Pin charts to Azure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="ba04f-129">[Eksportuj zapytania do usługi Power BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="ba04f-129">[Export queries to Power BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="ba04f-130">Brak [interfejsu API REST](https://dev.applicationinsights.io/) czy służy do wykonywania kwerend programowo, na przykład z programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="ba04f-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use to run queries programmatically, for example from Powershell.</span></span>


## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="ba04f-131">Połącz z danymi usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="ba04f-131">Connect to your Application Insights data</span></span>
<span data-ttu-id="ba04f-132">Otwórz Analytics z aplikacji [bloku omówienie](app-insights-dashboards.md) w usłudze Application Insights:</span><span class="sxs-lookup"><span data-stu-id="ba04f-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![Otwórz portal.azure.com otworzyć zasobu usługi Application Insights, a następnie kliknij przycisk Analytics.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="ba04f-134">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="ba04f-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="ba04f-135">Przykłady zapytań</span><span class="sxs-lookup"><span data-stu-id="ba04f-135">Query examples</span></span>

<span data-ttu-id="ba04f-136">Wypróbuj te wskazówki ilustrujący możliwości za pomocą analizy:</span><span class="sxs-lookup"><span data-stu-id="ba04f-136">Try these walkthroughs to illustrate the power of using Analytics:</span></span>

 *  [<span data-ttu-id="ba04f-137">Automatyczne diagnostyki wzrostów i krok przechodzi w czas trwania żądania</span><span class="sxs-lookup"><span data-stu-id="ba04f-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="ba04f-138">Analizowanie wydajności degradations z analizy serii czasowych</span><span class="sxs-lookup"><span data-stu-id="ba04f-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="ba04f-139">Analizowanie błędów aplikacji z autocluster i diffpatterns</span><span class="sxs-lookup"><span data-stu-id="ba04f-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="ba04f-140">Wykryć zaawansowane kształt z analizy serii czasowych</span><span class="sxs-lookup"><span data-stu-id="ba04f-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="ba04f-141">Za pomocą przesuwanego okna operacji do analizy użycia aplikacji (przewijane MAU/DAU itp.)</span><span class="sxs-lookup"><span data-stu-id="ba04f-141">Using sliding window operations to analyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="ba04f-142">[Wykrywanie zakłócenia w świadczeniu usług, oparte na analizie dzienników debugowania](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="ba04f-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="ba04f-143">[Profilowanie wydajności aplikacji za pomocą prostego dzienniki](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="ba04f-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="ba04f-144">[Pomiar czasu trwania dla każdego kroku w Twojej przepływu kodu przy użyciu dzienników debugowania proste](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="ba04f-144">[Measuring the duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="ba04f-145">[Analizowanie danych współbieżności przy użyciu dzienników debugowania proste](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="ba04f-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="ba04f-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ba04f-146">Next steps</span></span>
* <span data-ttu-id="ba04f-147">Zalecamy rozpocząć od [samouczek języka](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="ba04f-147">We recommend you start with the [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="ba04f-148">Więcej informacji o [przy użyciu Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="ba04f-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="ba04f-149">[Dokumentacja języka](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ba04f-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
