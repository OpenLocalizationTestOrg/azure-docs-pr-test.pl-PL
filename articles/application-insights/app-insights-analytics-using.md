---
title: "aaaUsing Analytics — narzędzie wyszukiwania zaawansowanego hello Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Przy użyciu hello Analytics, hello wydajne diagnostycznych narzędzie do wyszukiwania usługi Application insights. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="54ef6-103">Za pomocą analizy w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="54ef6-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="54ef6-104">[Analiza](app-insights-analytics.md) to funkcja wyszukiwania zaawansowanego hello [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54ef6-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="54ef6-105">Te strony opisano język zapytań usługi Analiza dzienników.</span><span class="sxs-lookup"><span data-stu-id="54ef6-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="54ef6-106">**[Obejrzyj klip wideo wprowadzenia hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="54ef6-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="54ef6-107">**[Przetestuj Analytics na naszych danych symulowane](https://analytics.applicationinsights.io/demo)**  aplikacji nie jest jeszcze wysyłania danych tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="54ef6-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="54ef6-108">Otwórz analityka</span><span class="sxs-lookup"><span data-stu-id="54ef6-108">Open Analytics</span></span>
<span data-ttu-id="54ef6-109">Macierzysty zasobów aplikacji w usłudze Application Insights kliknij Analytics.</span><span class="sxs-lookup"><span data-stu-id="54ef6-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![Otwórz portal.azure.com otworzyć zasobu usługi Application Insights, a następnie kliknij przycisk Analytics.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="54ef6-111">Samouczek wbudowanego Hello daje sugestii dotyczących co można zrobić.</span><span class="sxs-lookup"><span data-stu-id="54ef6-111">hello inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="54ef6-112">Brak [szerszej samouczek tutaj](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="54ef6-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="54ef6-113">Zapytanie telemetrii</span><span class="sxs-lookup"><span data-stu-id="54ef6-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="54ef6-114">Napisz zapytanie</span><span class="sxs-lookup"><span data-stu-id="54ef6-114">Write a query</span></span>
![Wyświetlanie schematu](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="54ef6-116">Zaczyna się od nazwy hello dowolnego hello tabel wymienionych po lewej stronie powitania (lub hello [zakres](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) lub [Unii](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operatory).</span><span class="sxs-lookup"><span data-stu-id="54ef6-116">Begin with hello names of any of hello tables listed on hello left (or hello [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="54ef6-117">Użyj `|` toocreate a planowanej sprzedaży [operatory](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="54ef6-117">Use `|` toocreate a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="54ef6-118">IntelliSense wyświetla hello operatory i hello elementy wyrażenia, których można użyć.</span><span class="sxs-lookup"><span data-stu-id="54ef6-118">IntelliSense prompts you with hello operators and hello expression elements that you can use.</span></span> <span data-ttu-id="54ef6-119">Kliknij ikonę informacji o hello (lub naciśnij klawisze CTRL + SPACJA) tooget dłuższy opis i przykłady toouse każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="54ef6-119">Click hello information icon (or press CTRL+Space) tooget a longer description and examples of how toouse each element.</span></span>

<span data-ttu-id="54ef6-120">Zobacz hello [samouczek języka Analytics](app-insights-analytics-tour.md) i [materiały referencyjne dotyczące języka](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="54ef6-120">See hello [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="54ef6-121">Uruchamianie zapytania</span><span class="sxs-lookup"><span data-stu-id="54ef6-121">Run a query</span></span>
![Wykonanie kwerendy](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="54ef6-123">Pojedynczy podziały wierszy można użyć w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="54ef6-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="54ef6-124">Umieść kursor hello wewnątrz lub na końcu hello hello zapytania, które chcesz toorun.</span><span class="sxs-lookup"><span data-stu-id="54ef6-124">Put hello cursor inside or at hello end of hello query you want toorun.</span></span>
3. <span data-ttu-id="54ef6-125">Sprawdź hello przedział czasu zapytania.</span><span class="sxs-lookup"><span data-stu-id="54ef6-125">Check hello time range of your query.</span></span> <span data-ttu-id="54ef6-126">(Można zmienić lub zmienić, umieszczając w niej własnych [ `where...timestamp...` ](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) klauzuli w zapytaniu.)</span><span class="sxs-lookup"><span data-stu-id="54ef6-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="54ef6-127">Kliknij przycisk Przejdź toorun hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="54ef6-127">Click Go toorun hello query.</span></span>
4. <span data-ttu-id="54ef6-128">Nie umieszczaj pustych wierszy w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="54ef6-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="54ef6-129">Kilka zapytań rozdzielonych można przechowywać w jedną kartę zapytanie, rozdzielając je puste wiersze.</span><span class="sxs-lookup"><span data-stu-id="54ef6-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="54ef6-130">Uruchamia tylko zapytania hello ma hello kursora.</span><span class="sxs-lookup"><span data-stu-id="54ef6-130">Only hello query that has hello cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="54ef6-131">Zapisz zapytanie</span><span class="sxs-lookup"><span data-stu-id="54ef6-131">Save a query</span></span>
![Zapisywanie zapytania](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="54ef6-133">Zapisz bieżący plik zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="54ef6-133">Save hello current query file.</span></span>
2. <span data-ttu-id="54ef6-134">Otwórz plik zapisanego zapytania.</span><span class="sxs-lookup"><span data-stu-id="54ef6-134">Open a saved query file.</span></span>
3. <span data-ttu-id="54ef6-135">Utwórz nowy plik zapytania.</span><span class="sxs-lookup"><span data-stu-id="54ef6-135">Create a new query file.</span></span>

## <a name="see-hello-details"></a><span data-ttu-id="54ef6-136">Zobacz szczegóły hello</span><span class="sxs-lookup"><span data-stu-id="54ef6-136">See hello details</span></span>
<span data-ttu-id="54ef6-137">Rozwiń wszystkie wiersze w toosee wyniki hello jego pełną listę właściwości.</span><span class="sxs-lookup"><span data-stu-id="54ef6-137">Expand any row in hello results toosee its complete list of properties.</span></span> <span data-ttu-id="54ef6-138">Można rozwinąć wszystkie właściwości, która jest wartością strukturalnych — na przykład, niestandardowe wymiary lub stosu hello w Wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="54ef6-138">You can further expand any property that is a structured value - for example, custom dimensions, or hello stack listing in an exception.</span></span>

![Rozwiń węzeł wiersza](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a><span data-ttu-id="54ef6-140">Rozmieść hello wyników</span><span class="sxs-lookup"><span data-stu-id="54ef6-140">Arrange hello results</span></span>
<span data-ttu-id="54ef6-141">Można sortować, filtrowanie, z podziałem na strony i hello wyniki zwracane z kwerendy grupy.</span><span class="sxs-lookup"><span data-stu-id="54ef6-141">You can sort, filter, paginate, and group hello results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="54ef6-142">Sortowanie, grupowanie i filtrowanie w przeglądarce hello nie ponownie uruchom zapytanie.</span><span class="sxs-lookup"><span data-stu-id="54ef6-142">Sorting, grouping, and filtering in hello browser don't re-run your query.</span></span> <span data-ttu-id="54ef6-143">Rozmieszczanie one tylko hello wyników zwróconych przez zapytanie ostatniego.</span><span class="sxs-lookup"><span data-stu-id="54ef6-143">They only rearrange hello results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="54ef6-144">tooperform te zadania na serwerze hello przed hello są zwracane, zapisać zapytanie z hello [sortowania](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [Podsumuj](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) i [gdzie](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operatorów.</span><span class="sxs-lookup"><span data-stu-id="54ef6-144">tooperform these tasks in hello server before hello results are returned, write your query with hello [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="54ef6-145">Wybierz kolumny hello jak jak toosee, przeciągnij toorearrange nagłówki kolumn, a zmiany rozmiaru kolumn przez przeciąganie ich obramowania.</span><span class="sxs-lookup"><span data-stu-id="54ef6-145">Pick hello columns you'd like toosee, drag column headers toorearrange them, and resize columns by dragging their borders.</span></span>

![Rozmieść kolumn](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="54ef6-147">Sortowanie i filtrowanie elementów</span><span class="sxs-lookup"><span data-stu-id="54ef6-147">Sort and filter items</span></span>
<span data-ttu-id="54ef6-148">Sortuj wyniki, klikając hello nagłówek kolumny.</span><span class="sxs-lookup"><span data-stu-id="54ef6-148">Sort your results by clicking hello head of a column.</span></span> <span data-ttu-id="54ef6-149">Kliknij ponownie przycisk toosort hello w inny sposób, i kliknij przycisk innej godziny toorevert toohello oryginalnego kolejność zwracanych przez zapytanie.</span><span class="sxs-lookup"><span data-stu-id="54ef6-149">Click again toosort hello other way, and click a third time toorevert toohello original ordering returned by your query.</span></span>

<span data-ttu-id="54ef6-150">Użyj toonarrow ikonę filtru hello wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="54ef6-150">Use hello filter icon toonarrow your search.</span></span>

![Sortowanie i filtrowanie kolumn](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="54ef6-152">Grupowanie elementów</span><span class="sxs-lookup"><span data-stu-id="54ef6-152">Group items</span></span>
<span data-ttu-id="54ef6-153">toosort przez więcej niż jedną kolumnę, za pomocą grupowania.</span><span class="sxs-lookup"><span data-stu-id="54ef6-153">toosort by more than one column, use grouping.</span></span> <span data-ttu-id="54ef6-154">Najpierw go włączyć, a następnie przeciągnij nagłówków kolumn na powitania miejsce powyżej hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="54ef6-154">First enable it, and then drag column headers into hello space above hello table.</span></span>

![Grupa](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="54ef6-156">Brakuje niektórych wyników?</span><span class="sxs-lookup"><span data-stu-id="54ef6-156">Missing some results?</span></span>

<span data-ttu-id="54ef6-157">Jeśli uważasz, że nie występują wszystkie wyniki hello oczekiwane, istnieje kilka możliwych przyczyn.</span><span class="sxs-lookup"><span data-stu-id="54ef6-157">If you think you're not seeing all hello results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="54ef6-158">**Filtr zakresu czasu**.</span><span class="sxs-lookup"><span data-stu-id="54ef6-158">**Time range filter**.</span></span> <span data-ttu-id="54ef6-159">Domyślnie będzie widoczne są tylko wyniki z hello ostatnich 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="54ef6-159">By default, you will only see results from hello last 24 hours.</span></span> <span data-ttu-id="54ef6-160">Brak automatyczny filtr, który ogranicza zakres hello wyników, które są pobierane z tabel źródłowych hello.</span><span class="sxs-lookup"><span data-stu-id="54ef6-160">There is an automatic filter that limits hello range of results that are retrieved from hello source tables.</span></span> 

    <span data-ttu-id="54ef6-161">Jednak można zmienić zakres czasowy hello filtru przy użyciu menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="54ef6-161">However, you can change hello time range filter by using hello drop-down menu.</span></span>

    <span data-ttu-id="54ef6-162">Lub zakresu automatycznego hello można zastąpić, umieszczając w niej własnych [ `where  ... timestamp ...` klauzuli](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) do zapytania.</span><span class="sxs-lookup"><span data-stu-id="54ef6-162">Or you can override hello automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="54ef6-163">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="54ef6-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="54ef6-164">**Limit wyników**.</span><span class="sxs-lookup"><span data-stu-id="54ef6-164">**Results limit**.</span></span> <span data-ttu-id="54ef6-165">Ma limitu 10 wierszy k na powitania wyniki zwrócone z hello portalu.</span><span class="sxs-lookup"><span data-stu-id="54ef6-165">There's a limit of about 10k rows on hello results returned from hello portal.</span></span> <span data-ttu-id="54ef6-166">Ostrzeżenie pokazuje, jeśli można przejść, przekraczając hello limit.</span><span class="sxs-lookup"><span data-stu-id="54ef6-166">A warning shows if you go over hello limit.</span></span> <span data-ttu-id="54ef6-167">Jeśli tak się stanie, sortowanie wyników w tabeli hello zawsze niewidoczne wszystkie hello rzeczywiste pierwszego lub ostatniego wyniki.</span><span class="sxs-lookup"><span data-stu-id="54ef6-167">If that happens, sorting your results in hello table won't always show you all hello actual first or last results.</span></span> 

    <span data-ttu-id="54ef6-168">Należy dobrze tooavoid naciśnięcie hello limit.</span><span class="sxs-lookup"><span data-stu-id="54ef6-168">It's good practice tooavoid hitting hello limit.</span></span> <span data-ttu-id="54ef6-169">Użyj filtru zakresu czasu hello lub używać operatorów, takich jak:</span><span class="sxs-lookup"><span data-stu-id="54ef6-169">Use hello time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="54ef6-170">100 najpopularniejszych przez sygnatury czasowej</span><span class="sxs-lookup"><span data-stu-id="54ef6-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="54ef6-171">podejmij 100</span><span class="sxs-lookup"><span data-stu-id="54ef6-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="54ef6-172">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="54ef6-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="54ef6-173">gdzie sygnatury czasowej > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="54ef6-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="54ef6-174">(Więcej niż 10 KB wierszy chcesz?</span><span class="sxs-lookup"><span data-stu-id="54ef6-174">(Want more than 10k rows?</span></span> <span data-ttu-id="54ef6-175">Należy rozważyć użycie [eksportu ciągłego](app-insights-export-telemetry.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="54ef6-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="54ef6-176">Analiza jest przeznaczona dla analizy, a nie podczas pobierania danych pierwotnych).</span><span class="sxs-lookup"><span data-stu-id="54ef6-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="54ef6-177">Diagramy</span><span class="sxs-lookup"><span data-stu-id="54ef6-177">Diagrams</span></span>
<span data-ttu-id="54ef6-178">Wybierz typ hello diagramu, który chcesz:</span><span class="sxs-lookup"><span data-stu-id="54ef6-178">Select hello type of diagram you'd like:</span></span>

![Wybierz typ diagramu](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="54ef6-180">Jeśli masz kilka kolumn prawego typów hello można hello x i osi y i kolumnę wymiary toosplit hello wyniki według.</span><span class="sxs-lookup"><span data-stu-id="54ef6-180">If you have several columns of hello right types, you can choose hello x and y axes, and a column of dimensions toosplit hello results by.</span></span>

<span data-ttu-id="54ef6-181">Domyślnie wyniki są początkowo wyświetlane jako tabelę i ręcznie wybrać hello diagramu.</span><span class="sxs-lookup"><span data-stu-id="54ef6-181">By default, results are initially displayed as a table, and you select hello diagram manually.</span></span> <span data-ttu-id="54ef6-182">Można używać hello [renderowania dyrektywy](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) na końcu hello tooselect zapytania diagramu.</span><span class="sxs-lookup"><span data-stu-id="54ef6-182">But you can use hello [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at hello end of a query tooselect a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="54ef6-183">Diagnostyka analityka</span><span class="sxs-lookup"><span data-stu-id="54ef6-183">Analytics diagnostics</span></span>


<span data-ttu-id="54ef6-184">Na timechart przypadku nagłego kolekcji lub krok danych, mogą pojawić się zaznaczony punkt hello wiersza.</span><span class="sxs-lookup"><span data-stu-id="54ef6-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on hello line.</span></span> <span data-ttu-id="54ef6-185">Oznacza to, Diagnostyka Analytics zidentyfikowane kombinację właściwości, które odfiltrowywania hello nagła zmiana.</span><span class="sxs-lookup"><span data-stu-id="54ef6-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out hello sudden change.</span></span> <span data-ttu-id="54ef6-186">Kliknij przycisk tooget punktu hello bardziej szczegółowo na powitania filtru i toosee hello filtrowana wersja.</span><span class="sxs-lookup"><span data-stu-id="54ef6-186">Click hello point tooget more detail on hello filter, and toosee hello filtered version.</span></span> <span data-ttu-id="54ef6-187">To może pomóc w zidentyfikowaniu jaka zmiana spowodowane hello.</span><span class="sxs-lookup"><span data-stu-id="54ef6-187">This may help you identify what caused hello change.</span></span> 

[<span data-ttu-id="54ef6-188">Dowiedz się więcej o diagnostyce analityka</span><span class="sxs-lookup"><span data-stu-id="54ef6-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Diagnostyka analityka](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a><span data-ttu-id="54ef6-190">Toodashboard numeru PIN</span><span class="sxs-lookup"><span data-stu-id="54ef6-190">Pin toodashboard</span></span>
<span data-ttu-id="54ef6-191">Można przypiąć diagramu lub tabeli tooone z Twojej [udostępnionych pulpitów nawigacyjnych](app-insights-dashboards.md) — wystarczy kliknąć hello numeru pin.</span><span class="sxs-lookup"><span data-stu-id="54ef6-191">You can pin a diagram or table tooone of your [shared dashboards](app-insights-dashboards.md) - just click hello pin.</span></span> <span data-ttu-id="54ef6-192">(Może być konieczne zbyt[uaktualniania aplikacji przez cennik pakietu](app-insights-pricing.md) tooturn tę funkcję.)</span><span class="sxs-lookup"><span data-stu-id="54ef6-192">(You might need too[upgrade your app's pricing package](app-insights-pricing.md) tooturn on this feature.)</span></span> 

![Kliknij polecenie Przypnij hello](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="54ef6-194">Oznacza to, że podczas Podsumowując toohelp pulpitu nawigacyjnego, można monitorować wydajność hello lub użycia usług sieci web można dołączyć dość złożone analizy obok hello innych metryk.</span><span class="sxs-lookup"><span data-stu-id="54ef6-194">This means that, when you put together a dashboard toohelp you monitor hello performance or usage of your web services, you can include quite complex analysis alongside hello other metrics.</span></span> 

<span data-ttu-id="54ef6-195">Na pulpicie nawigacyjnym toohello tabeli można przypiąć, jeśli ma cztery lub mniejszą liczbę kolumn.</span><span class="sxs-lookup"><span data-stu-id="54ef6-195">You can pin a table toohello dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="54ef6-196">Tylko hello górne siedmiu wiersze są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="54ef6-196">Only hello top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="54ef6-197">Odświeżanie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="54ef6-197">Dashboard refresh</span></span>
<span data-ttu-id="54ef6-198">pulpit nawigacyjny toohello wykresu przypięty Hello jest automatycznie odświeżany przez ponowne uruchomienie zapytania hello co około godzin.</span><span class="sxs-lookup"><span data-stu-id="54ef6-198">hello chart pinned toohello dashboard is refreshed automatically by re-running hello query approximately every hours.</span></span> <span data-ttu-id="54ef6-199">Można także kliknąć przycisk Odśwież hello.</span><span class="sxs-lookup"><span data-stu-id="54ef6-199">You can also click hello Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="54ef6-200">Automatyczne uproszczenia</span><span class="sxs-lookup"><span data-stu-id="54ef6-200">Automatic simplifications</span></span>

<span data-ttu-id="54ef6-201">Niektórych uproszczenia są stosowane tooa wykresu po przypięciu tooa pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="54ef6-201">Certain simplifications are applied tooa chart when you pin it tooa dashboard.</span></span>

<span data-ttu-id="54ef6-202">**Czas ograniczeń:** zapytania są automatycznie ograniczony toohello w ciągu ostatnich 14 dni.</span><span class="sxs-lookup"><span data-stu-id="54ef6-202">**Time restriction:** Queries are automatically limited toohello past 14 days.</span></span> <span data-ttu-id="54ef6-203">Hello efekt jest hello takie same jak, jeśli kwerenda zawiera `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="54ef6-203">hello effect is hello same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="54ef6-204">**Ograniczenie liczby bin:** podczas wyświetlania wykresu, który ma wiele odrębny bins (zazwyczaj wykresu słupkowego) hello mniej bins wypełnione automatycznie są pogrupowane w jednej "inne" bin.</span><span class="sxs-lookup"><span data-stu-id="54ef6-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), hello less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="54ef6-205">Na przykład tego zapytania:</span><span class="sxs-lookup"><span data-stu-id="54ef6-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="54ef6-206">wygląda następująco w module analiz:</span><span class="sxs-lookup"><span data-stu-id="54ef6-206">looks like this in Analytics:</span></span>

![Wykres z tail długa](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="54ef6-208">Jednak gdy przypiąć pulpitu nawigacyjnego tooa go wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="54ef6-208">but when you pin it tooa dashboard, it looks like this:</span></span>

![Wykres z ograniczoną bins](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a><span data-ttu-id="54ef6-210">TooExcel eksportu</span><span class="sxs-lookup"><span data-stu-id="54ef6-210">Export tooExcel</span></span>
<span data-ttu-id="54ef6-211">Po uruchomieniu kwerendy, można pobrać pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="54ef6-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="54ef6-212">Kliknij przycisk **wyeksportować Excel**.</span><span class="sxs-lookup"><span data-stu-id="54ef6-212">Click **Export,  Excel**.</span></span>

## <a name="export-toopower-bi"></a><span data-ttu-id="54ef6-213">Eksportuj tooPower analizy Biznesowej</span><span class="sxs-lookup"><span data-stu-id="54ef6-213">Export tooPower BI</span></span>
<span data-ttu-id="54ef6-214">Umieść kursor hello w zapytaniu i wybierz polecenie **wyeksportować usługi Power BI**.</span><span class="sxs-lookup"><span data-stu-id="54ef6-214">Put hello cursor in a query and choose **Export, Power BI**.</span></span>

![Eksportowanie z tooPower Analytics analizy Biznesowej](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="54ef6-216">Możesz uruchomić hello zapytania w usłudze Power BI.</span><span class="sxs-lookup"><span data-stu-id="54ef6-216">You run hello query in Power BI.</span></span> <span data-ttu-id="54ef6-217">Możesz ustawić toorefresh zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="54ef6-217">You can set it toorefresh on a schedule.</span></span>

<span data-ttu-id="54ef6-218">Usługa Power BI można tworzyć pulpity nawigacyjne, które zbieranie danych z różnych źródeł.</span><span class="sxs-lookup"><span data-stu-id="54ef6-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="54ef6-219">Więcej informacji na temat eksportowania tooPower analizy Biznesowej</span><span class="sxs-lookup"><span data-stu-id="54ef6-219">Learn more about export tooPower BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="54ef6-220">Głębokie łącze</span><span class="sxs-lookup"><span data-stu-id="54ef6-220">Deep link</span></span>

<span data-ttu-id="54ef6-221">Uzyskaj link w obszarze **eksportu, link udziału** wysłanie tooanother użytkownika.</span><span class="sxs-lookup"><span data-stu-id="54ef6-221">Get a link under **Export, Share link** that you can send tooanother user.</span></span> <span data-ttu-id="54ef6-222">Podany użytkownik hello ma [grupy zasobów tooyour dostępu](app-insights-resources-roles-access-control.md), hello kwerendy będą otwierane w hello interfejsu użytkownika analizy.</span><span class="sxs-lookup"><span data-stu-id="54ef6-222">Provided hello user has [access tooyour resource group](app-insights-resources-roles-access-control.md), hello query will open in hello Analytics UI.</span></span>

<span data-ttu-id="54ef6-223">(Łącze hello hello tekst zapytania jest umieszczany po "? q =" gzip skompresowane i algorytmem base-64.</span><span class="sxs-lookup"><span data-stu-id="54ef6-223">(In hello link, hello query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="54ef6-224">Można napisać kod toogenerate głębokiego łącza musisz zapewnić toousers.</span><span class="sxs-lookup"><span data-stu-id="54ef6-224">You could write code toogenerate deep links that you provide toousers.</span></span> <span data-ttu-id="54ef6-225">Jednak zalecane jest sposób toorun Analytics z kodu za pomocą hello hello [interfejsu API REST](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="54ef6-225">However, hello recommended way toorun Analytics from code is by using hello [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="54ef6-226">Automatyzacja</span><span class="sxs-lookup"><span data-stu-id="54ef6-226">Automation</span></span>

<span data-ttu-id="54ef6-227">Użyj hello [interfejsu API REST dostępu do danych](https://dev.applicationinsights.io/) toorun Analytics zapytania.</span><span class="sxs-lookup"><span data-stu-id="54ef6-227">Use hello  [Data Access REST API](https://dev.applicationinsights.io/) toorun Analytics queries.</span></span> <span data-ttu-id="54ef6-228">[Na przykład](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (przy użyciu programu PowerShell):</span><span class="sxs-lookup"><span data-stu-id="54ef6-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="54ef6-229">W odróżnieniu od hello interfejsu użytkownika analizy hello interfejsu API REST nie powoduje automatycznego dodania kwerendy tooyour ograniczenia sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="54ef6-229">Unlike hello Analytics UI, hello REST API does not automatically add any timestamp limitation tooyour queries.</span></span> <span data-ttu-id="54ef6-230">Pamiętaj, aby tooadd własne klauzuli where, tooavoid Uzyskiwanie dużych odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="54ef6-230">Remember tooadd your own where-clause, tooavoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="54ef6-231">Importowanie danych</span><span class="sxs-lookup"><span data-stu-id="54ef6-231">Import data</span></span>

<span data-ttu-id="54ef6-232">Dane można zaimportować z pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="54ef6-232">You can import data from a CSV file.</span></span> <span data-ttu-id="54ef6-233">Zwykle jest tooimport dane statyczne, które można połączyć z tabelami z telemetrii.</span><span class="sxs-lookup"><span data-stu-id="54ef6-233">A typical usage is tooimport static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="54ef6-234">Na przykład uwierzytelnionym użytkownikom są oznaczane w obrębie telemetrii alias lub zaciemnionego identyfikator, można zaimportować tabelę, która mapuje nazwy tooreal aliasy.</span><span class="sxs-lookup"><span data-stu-id="54ef6-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases tooreal names.</span></span> <span data-ttu-id="54ef6-235">Wykonując sprzężenie na dane telemetryczne żądania hello, można zidentyfikować użytkowników według ich rzeczywistym nazw w raportach analizy hello.</span><span class="sxs-lookup"><span data-stu-id="54ef6-235">By performing a join on hello request telemetry, you can identify users by their real names in hello Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="54ef6-236">Zdefiniuj schemat danych</span><span class="sxs-lookup"><span data-stu-id="54ef6-236">Define your data schema</span></span>

1. <span data-ttu-id="54ef6-237">Kliknij przycisk **ustawienia** (u góry po lewej), a następnie **źródeł danych**.</span><span class="sxs-lookup"><span data-stu-id="54ef6-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="54ef6-238">Dodawanie źródła danych, postępując zgodnie z instrukcjami hello.</span><span class="sxs-lookup"><span data-stu-id="54ef6-238">Add a data source, following hello instructions.</span></span> <span data-ttu-id="54ef6-239">Jesteś zadawane toosupply próbkę danych hello, który powinien zawierać co najmniej 10 wierszy.</span><span class="sxs-lookup"><span data-stu-id="54ef6-239">You are asked toosupply a sample of hello data, which should include at least ten rows.</span></span> <span data-ttu-id="54ef6-240">Następnie poprawić hello schematu.</span><span class="sxs-lookup"><span data-stu-id="54ef6-240">You then correct hello schema.</span></span>

<span data-ttu-id="54ef6-241">Określa źródło danych, które można następnie użyć tooimport poszczególnych tabel.</span><span class="sxs-lookup"><span data-stu-id="54ef6-241">This defines a data source, which you can then use tooimport individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="54ef6-242">Importowanie tabeli</span><span class="sxs-lookup"><span data-stu-id="54ef6-242">Import a table</span></span>

1. <span data-ttu-id="54ef6-243">Otwórz z definicji źródła danych z listy hello.</span><span class="sxs-lookup"><span data-stu-id="54ef6-243">Open your data source definition from hello list.</span></span>
2. <span data-ttu-id="54ef6-244">Kliknij przycisk "Przekaż" i wykonaj hello instrukcje tooupload hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="54ef6-244">Click "Upload" and follow hello instructions tooupload hello table.</span></span> <span data-ttu-id="54ef6-245">Obejmuje to tooa wywołania interfejsu API REST i dlatego jest łatwe tooautomate.</span><span class="sxs-lookup"><span data-stu-id="54ef6-245">This involves a call tooa REST API, and so it is easy tooautomate.</span></span> 

<span data-ttu-id="54ef6-246">Tabela jest teraz dostępna do użycia w zapytaniach Analytics.</span><span class="sxs-lookup"><span data-stu-id="54ef6-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="54ef6-247">Zostanie wyświetlony na analityka</span><span class="sxs-lookup"><span data-stu-id="54ef6-247">It will appear in Analytics</span></span> 

### <a name="use-hello-table"></a><span data-ttu-id="54ef6-248">Tabela hello</span><span class="sxs-lookup"><span data-stu-id="54ef6-248">Use hello table</span></span>

<span data-ttu-id="54ef6-249">Załóżmy, że Twoje definicji źródła danych jest nazywany `usermap`, i ma dwa pola `realName` i `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="54ef6-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="54ef6-250">Witaj `requests` tabeli również zawiera pole o nazwie `user_AuthenticatedId`, więc jest łatwe toojoin je:</span><span class="sxs-lookup"><span data-stu-id="54ef6-250">hello `requests` table also has a field named `user_AuthenticatedId`, so it's easy toojoin them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="54ef6-251">Witaj tabeli wynikowej żądań ma dodatkowe kolumny `realName`.</span><span class="sxs-lookup"><span data-stu-id="54ef6-251">hello resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="54ef6-252">Importuj z LogStash</span><span class="sxs-lookup"><span data-stu-id="54ef6-252">Import from LogStash</span></span>

<span data-ttu-id="54ef6-253">Jeśli używasz [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), można użyć tooquery analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="54ef6-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics tooquery your logs.</span></span> <span data-ttu-id="54ef6-254">Użyj hello [wtyczkę, która powoduje przekazanie w potoku danych do analizy](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="54ef6-254">Use hello [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="54ef6-255">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="54ef6-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

