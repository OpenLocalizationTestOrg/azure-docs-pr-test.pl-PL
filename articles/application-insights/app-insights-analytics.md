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
# <a name="analytics-in-application-insights"></a><span data-ttu-id="edf00-103">Analityka w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="edf00-103">Analytics in Application Insights</span></span>
<span data-ttu-id="edf00-104">[Analiza](app-insights-analytics.md) to funkcja wyszukiwania zaawansowanego hello [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="edf00-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="edf00-105">Te strony opisano język zapytań usługi Analiza dzienników.</span><span class="sxs-lookup"><span data-stu-id="edf00-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="edf00-106">**[Obejrzyj klip wideo wprowadzenia hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="edf00-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="edf00-107">**[Przetestuj Analytics na naszych danych symulowane](https://analytics.applicationinsights.io/demo)**  aplikacji nie jest jeszcze wysyłania danych tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="edf00-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="edf00-108">**[Ściągawka SQL użytkowników](https://aka.ms/sql-analytics)**  tłumaczy hello idioms najczęściej.</span><span class="sxs-lookup"><span data-stu-id="edf00-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>
* <span data-ttu-id="edf00-109">**[Dokumentacja języka](app-insights-analytics-reference.md)**  Dowiedz się, jak wszystkie toouse hello zaawansowanych funkcji hello język zapytań usługi Analiza dzienników.</span><span class="sxs-lookup"><span data-stu-id="edf00-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how toouse all hello powerful features of hello Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="edf00-110">Kwerendy w module analiz</span><span class="sxs-lookup"><span data-stu-id="edf00-110">Queries in Analytics</span></span>
<span data-ttu-id="edf00-111">Typowe zapytania jest *źródła* tabeli następuje szereg *operatory* rozdzielone `|`.</span><span class="sxs-lookup"><span data-stu-id="edf00-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="edf00-112">Na przykład załóżmy Dowiedz się pory dnia obywateli hello Hyderabad spróbuj swoją aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="edf00-112">For example, let's find out what time of day hello citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="edf00-113">I są nam Zobaczmy, jakie kody wyników są zwracane tootheir HTTP żądania.</span><span class="sxs-lookup"><span data-stu-id="edf00-113">And while we're there, let's see what result codes are returned tootheir HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="edf00-114">Firma Microsoft liczba adresów IP unikatowych klientów, ich grupowanie hello godzinę dnia hello za pośrednictwem hello w ciągu ostatnich 7 dni.</span><span class="sxs-lookup"><span data-stu-id="edf00-114">We count distinct client IP addresses, grouping them by hello hour of hello day over hello past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="edf00-115">wyniki tooget poza hello poprzednich 24 godzin, jawnie zawierały "timestamp" w zapytaniu, albo użyj menu rozwijanego zakres czasu hello.</span><span class="sxs-lookup"><span data-stu-id="edf00-115">tooget results outside hello previous 24h, either include 'timestamp' explicitly in your query, or use hello time range drop-down menu.</span></span>
>

<span data-ttu-id="edf00-116">Umożliwia wyświetlenie hello wyniki z hello paska prezentacji wykresu, wybierając toostack hello wyników z kodów odpowiedzi różnych:</span><span class="sxs-lookup"><span data-stu-id="edf00-116">Let's display hello results with hello bar chart presentation, choosing toostack hello results from different response codes:</span></span>

![Wybierz wykres słupkowy, x i y osi, a następnie segmentacji](./media/app-insights-analytics/020.png)

<span data-ttu-id="edf00-118">Wygląda na to lunchtime i bielizny czasu w Hyderabad aplikacji cieszy się największą popularnością.</span><span class="sxs-lookup"><span data-stu-id="edf00-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="edf00-119">(I firma Microsoft powinien być sprawdzony tych kodów 500.)</span><span class="sxs-lookup"><span data-stu-id="edf00-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="edf00-120">Dostępne są również zaawansowane operacje statystyczne:</span><span class="sxs-lookup"><span data-stu-id="edf00-120">There are also powerful statistical operations:</span></span>

![Wyniki zapytania statystyczne](./media/app-insights-analytics/025.png)

<span data-ttu-id="edf00-122">język Hello oferuje wiele funkcji atrakcyjne:</span><span class="sxs-lookup"><span data-stu-id="edf00-122">hello language has many attractive features:</span></span>


* <span data-ttu-id="edf00-123">[Filtr](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) telemetrii raw aplikacji przez wszystkie pola, w tym właściwości niestandardowych i metryki.</span><span class="sxs-lookup"><span data-stu-id="edf00-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="edf00-124">[Dołącz](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) wielu tabel — korelując żądania z wyświetleń strony, wywołania zależności, wyjątków i ślady dziennika.</span><span class="sxs-lookup"><span data-stu-id="edf00-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="edf00-125">Zaawansowane statystyczne [agregacji](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="edf00-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="edf00-126">Równie wydajne jako SQL, ale znacznie łatwiejsze w przypadku złożonych zapytań: zamiast zagnieżdżenia instrukcje należy przekazać w potoku hello danych z jednego toohello podstawowych operacji obok.</span><span class="sxs-lookup"><span data-stu-id="edf00-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe hello data from one elementary operation toohello next.</span></span>
* <span data-ttu-id="edf00-127">Natychmiastowe i zaawansowane wizualizacje.</span><span class="sxs-lookup"><span data-stu-id="edf00-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="edf00-128">[Numer PIN wykresy, pulpity nawigacyjne tooAzure](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="edf00-128">[Pin charts tooAzure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="edf00-129">[Eksportuj tooPower zapytania BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="edf00-129">[Export queries tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="edf00-130">Brak [interfejsu API REST](https://dev.applicationinsights.io/) służącego zapytania toorun programowo, na przykład z programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="edf00-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use toorun queries programmatically, for example from Powershell.</span></span>


## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="edf00-131">Połącz dane usługi Application Insights tooyour</span><span class="sxs-lookup"><span data-stu-id="edf00-131">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="edf00-132">Otwórz Analytics z aplikacji [bloku omówienie](app-insights-dashboards.md) w usłudze Application Insights:</span><span class="sxs-lookup"><span data-stu-id="edf00-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![Otwórz portal.azure.com otworzyć zasobu usługi Application Insights, a następnie kliknij przycisk Analytics.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="edf00-134">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="edf00-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="edf00-135">Przykłady zapytań</span><span class="sxs-lookup"><span data-stu-id="edf00-135">Query examples</span></span>

<span data-ttu-id="edf00-136">Wypróbuj te wskazówki tooillustrate hello możliwości przy użyciu Analytics:</span><span class="sxs-lookup"><span data-stu-id="edf00-136">Try these walkthroughs tooillustrate hello power of using Analytics:</span></span>

 *  [<span data-ttu-id="edf00-137">Automatyczne diagnostyki wzrostów i krok przechodzi w czas trwania żądania</span><span class="sxs-lookup"><span data-stu-id="edf00-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="edf00-138">Analizowanie wydajności degradations z analizy serii czasowych</span><span class="sxs-lookup"><span data-stu-id="edf00-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="edf00-139">Analizowanie błędów aplikacji z autocluster i diffpatterns</span><span class="sxs-lookup"><span data-stu-id="edf00-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="edf00-140">Wykryć zaawansowane kształt z analizy serii czasowych</span><span class="sxs-lookup"><span data-stu-id="edf00-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="edf00-141">Użycie przesuwanego okna operacji tooanalyze aplikacji (przewijane MAU/DAU itp.)</span><span class="sxs-lookup"><span data-stu-id="edf00-141">Using sliding window operations tooanalyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="edf00-142">[Wykrywanie zakłócenia w świadczeniu usług, oparte na analizie dzienników debugowania](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="edf00-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="edf00-143">[Profilowanie wydajności aplikacji za pomocą prostego dzienniki](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="edf00-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="edf00-144">[Pomiar czasu trwania powitania dla każdego kroku w Twojej przepływu kodu przy użyciu dzienników debugowania proste](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="edf00-144">[Measuring hello duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="edf00-145">[Analizowanie danych współbieżności przy użyciu dzienników debugowania proste](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) i pasujące wpis w blogu [tutaj](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="edf00-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="edf00-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="edf00-146">Next steps</span></span>
* <span data-ttu-id="edf00-147">Zaleca się rozpoczynać hello [samouczek języka](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="edf00-147">We recommend you start with hello [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="edf00-148">Więcej informacji o [przy użyciu Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="edf00-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="edf00-149">[Dokumentacja języka](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="edf00-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
