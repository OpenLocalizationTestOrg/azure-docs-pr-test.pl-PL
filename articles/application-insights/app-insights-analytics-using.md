---
title: "Przy użyciu Analytics — narzędzie wyszukiwania zaawansowanego w Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Przy użyciu Analytics, narzędzie zaawansowane wyszukiwanie diagnostycznych z usługi Application Insights. "
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
ms.openlocfilehash: 9f7c1744db52b1c2f374fd5655e2c66b5f61bacf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="39b80-103">Za pomocą analizy w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="39b80-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="39b80-104">[Analiza](app-insights-analytics.md) to funkcja wyszukiwania zaawansowanego [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39b80-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="39b80-105">Te strony opisano język zapytań usługi Analiza dzienników.</span><span class="sxs-lookup"><span data-stu-id="39b80-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="39b80-106">**[Obejrzyj klip wideo wprowadzenia](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="39b80-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="39b80-107">**[Przetestuj Analytics na naszych danych symulowane](https://analytics.applicationinsights.io/demo)**  aplikacji nie jest wysyłania danych do usługi Application Insights jeszcze.</span><span class="sxs-lookup"><span data-stu-id="39b80-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="39b80-108">Otwórz analityka</span><span class="sxs-lookup"><span data-stu-id="39b80-108">Open Analytics</span></span>
<span data-ttu-id="39b80-109">Macierzysty zasobów aplikacji w usłudze Application Insights kliknij Analytics.</span><span class="sxs-lookup"><span data-stu-id="39b80-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![Otwórz portal.azure.com otworzyć zasobu usługi Application Insights, a następnie kliknij przycisk Analytics.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="39b80-111">Samouczek wbudowany daje sugestii dotyczących co można zrobić.</span><span class="sxs-lookup"><span data-stu-id="39b80-111">The inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="39b80-112">Brak [szerszej samouczek tutaj](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="39b80-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="39b80-113">Zapytanie telemetrii</span><span class="sxs-lookup"><span data-stu-id="39b80-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="39b80-114">Napisz zapytanie</span><span class="sxs-lookup"><span data-stu-id="39b80-114">Write a query</span></span>
![Wyświetlanie schematu](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="39b80-116">Zaczyna się od nazwy tabel wymienionych po lewej stronie (lub [zakres](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) lub [Unii](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operatory).</span><span class="sxs-lookup"><span data-stu-id="39b80-116">Begin with the names of any of the tables listed on the left (or the [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="39b80-117">Użyj `|` można utworzyć potoku o [operatory](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="39b80-117">Use `|` to create a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="39b80-118">IntelliSense wyświetla operatory i elementy wyrażenia, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="39b80-118">IntelliSense prompts you with the operators and the expression elements that you can use.</span></span> <span data-ttu-id="39b80-119">Kliknij ikonę informacji (lub naciśnij klawisze CTRL + SPACJA) Aby uzyskać opis dłużej i przykłady sposobu używania poszczególnych elementów.</span><span class="sxs-lookup"><span data-stu-id="39b80-119">Click the information icon (or press CTRL+Space) to get a longer description and examples of how to use each element.</span></span>

<span data-ttu-id="39b80-120">Zobacz [samouczek języka Analytics](app-insights-analytics-tour.md) i [materiały referencyjne dotyczące języka](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="39b80-120">See the [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="39b80-121">Uruchamianie zapytania</span><span class="sxs-lookup"><span data-stu-id="39b80-121">Run a query</span></span>
![Wykonanie kwerendy](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="39b80-123">Pojedynczy podziały wierszy można użyć w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="39b80-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="39b80-124">Umieść kursor wewnątrz lub na końcu zapytania, który chcesz uruchomić.</span><span class="sxs-lookup"><span data-stu-id="39b80-124">Put the cursor inside or at the end of the query you want to run.</span></span>
3. <span data-ttu-id="39b80-125">Sprawdź zakres czasu zapytania.</span><span class="sxs-lookup"><span data-stu-id="39b80-125">Check the time range of your query.</span></span> <span data-ttu-id="39b80-126">(Można zmienić lub zmienić, umieszczając w niej własnych [ `where...timestamp...` ](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) klauzuli w zapytaniu.)</span><span class="sxs-lookup"><span data-stu-id="39b80-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="39b80-127">Kliknij polecenie Przejdź do uruchomienia zapytania.</span><span class="sxs-lookup"><span data-stu-id="39b80-127">Click Go to run the query.</span></span>
4. <span data-ttu-id="39b80-128">Nie umieszczaj pustych wierszy w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="39b80-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="39b80-129">Kilka zapytań rozdzielonych można przechowywać w jedną kartę zapytanie, rozdzielając je puste wiersze.</span><span class="sxs-lookup"><span data-stu-id="39b80-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="39b80-130">Uruchamia tylko kwerendy, w której znajduje się kursor.</span><span class="sxs-lookup"><span data-stu-id="39b80-130">Only the query that has the cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="39b80-131">Zapisz zapytanie</span><span class="sxs-lookup"><span data-stu-id="39b80-131">Save a query</span></span>
![Zapisywanie zapytania](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="39b80-133">Zapisz bieżący plik zapytania.</span><span class="sxs-lookup"><span data-stu-id="39b80-133">Save the current query file.</span></span>
2. <span data-ttu-id="39b80-134">Otwórz plik zapisanego zapytania.</span><span class="sxs-lookup"><span data-stu-id="39b80-134">Open a saved query file.</span></span>
3. <span data-ttu-id="39b80-135">Utwórz nowy plik zapytania.</span><span class="sxs-lookup"><span data-stu-id="39b80-135">Create a new query file.</span></span>

## <a name="see-the-details"></a><span data-ttu-id="39b80-136">Zobacz szczegóły</span><span class="sxs-lookup"><span data-stu-id="39b80-136">See the details</span></span>
<span data-ttu-id="39b80-137">Rozwiń wszystkie wiersze w wynikach, aby wyświetlić jego pełną listę właściwości.</span><span class="sxs-lookup"><span data-stu-id="39b80-137">Expand any row in the results to see its complete list of properties.</span></span> <span data-ttu-id="39b80-138">Można rozwinąć dowolnej właściwości, która jest wartością strukturalnych — na przykład, niestandardowe wymiary lub stosu w Wystąpił wyjątek.</span><span class="sxs-lookup"><span data-stu-id="39b80-138">You can further expand any property that is a structured value - for example, custom dimensions, or the stack listing in an exception.</span></span>

![Rozwiń węzeł wiersza](./media/app-insights-analytics-using/070.png)

## <a name="arrange-the-results"></a><span data-ttu-id="39b80-140">Rozmieszczenie wyników</span><span class="sxs-lookup"><span data-stu-id="39b80-140">Arrange the results</span></span>
<span data-ttu-id="39b80-141">Można sortować, filtrowanie, z podziałem na strony i grupy wyników zwróconych z zapytania.</span><span class="sxs-lookup"><span data-stu-id="39b80-141">You can sort, filter, paginate, and group the results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="39b80-142">Sortowanie, grupowanie i filtrowanie w przeglądarce nie ponownie uruchom zapytanie.</span><span class="sxs-lookup"><span data-stu-id="39b80-142">Sorting, grouping, and filtering in the browser don't re-run your query.</span></span> <span data-ttu-id="39b80-143">Rozmieszczanie one tylko wyników zwróconych przez kwerendę ostatniego.</span><span class="sxs-lookup"><span data-stu-id="39b80-143">They only rearrange the results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="39b80-144">Aby wykonać te zadania na serwerze przed są zwracane, zapisać zapytanie z [sortowania](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [Podsumuj](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) i [gdzie](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operatorów.</span><span class="sxs-lookup"><span data-stu-id="39b80-144">To perform these tasks in the server before the results are returned, write your query with the [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="39b80-145">Wybierz kolumny, które chcesz wyświetlić, przeciągnij nagłówek kolumny w celu ich ponownego rozmieszczenia i zmiana rozmiaru kolumn przez przeciągnięcie ich obramowania.</span><span class="sxs-lookup"><span data-stu-id="39b80-145">Pick the columns you'd like to see, drag column headers to rearrange them, and resize columns by dragging their borders.</span></span>

![Rozmieść kolumn](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="39b80-147">Sortowanie i filtrowanie elementów</span><span class="sxs-lookup"><span data-stu-id="39b80-147">Sort and filter items</span></span>
<span data-ttu-id="39b80-148">Posortować wyników, kliknij nagłówek kolumny.</span><span class="sxs-lookup"><span data-stu-id="39b80-148">Sort your results by clicking the head of a column.</span></span> <span data-ttu-id="39b80-149">Kliknij ponownie, aby posortować inny sposób, a następnie kliknij przycisk innej czasu, aby powrócić do oryginalnej kolejność zwracanych przez zapytanie.</span><span class="sxs-lookup"><span data-stu-id="39b80-149">Click again to sort the other way, and click a third time to revert to the original ordering returned by your query.</span></span>

<span data-ttu-id="39b80-150">Użyj ikony filtru, aby zawęzić kryteria wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="39b80-150">Use the filter icon to narrow your search.</span></span>

![Sortowanie i filtrowanie kolumn](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="39b80-152">Grupowanie elementów</span><span class="sxs-lookup"><span data-stu-id="39b80-152">Group items</span></span>
<span data-ttu-id="39b80-153">Aby posortować według więcej niż jedną kolumnę, użyj grupowania.</span><span class="sxs-lookup"><span data-stu-id="39b80-153">To sort by more than one column, use grouping.</span></span> <span data-ttu-id="39b80-154">Najpierw go włączyć, a następnie przeciągnij nagłówków kolumn na miejsce powyżej tabeli.</span><span class="sxs-lookup"><span data-stu-id="39b80-154">First enable it, and then drag column headers into the space above the table.</span></span>

![Grupa](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="39b80-156">Brakuje niektórych wyników?</span><span class="sxs-lookup"><span data-stu-id="39b80-156">Missing some results?</span></span>

<span data-ttu-id="39b80-157">Jeśli uważasz, że nie występują wszystkie wyniki, które miały, istnieje kilka możliwych przyczyn.</span><span class="sxs-lookup"><span data-stu-id="39b80-157">If you think you're not seeing all the results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="39b80-158">**Filtr zakresu czasu**.</span><span class="sxs-lookup"><span data-stu-id="39b80-158">**Time range filter**.</span></span> <span data-ttu-id="39b80-159">Domyślnie będą widoczne są tylko wyniki z ostatnich 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="39b80-159">By default, you will only see results from the last 24 hours.</span></span> <span data-ttu-id="39b80-160">Brak automatyczny filtr, który ogranicza zakres wyniki, które są pobierane z tabel źródłowych.</span><span class="sxs-lookup"><span data-stu-id="39b80-160">There is an automatic filter that limits the range of results that are retrieved from the source tables.</span></span> 

    <span data-ttu-id="39b80-161">Można jednak zmienić zakres czasu filtru przy użyciu menu rozwijanego.</span><span class="sxs-lookup"><span data-stu-id="39b80-161">However, you can change the time range filter by using the drop-down menu.</span></span>

    <span data-ttu-id="39b80-162">Lub zakresie automatycznego można zastąpić, umieszczając w niej własnych [ `where  ... timestamp ...` klauzuli](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) do zapytania.</span><span class="sxs-lookup"><span data-stu-id="39b80-162">Or you can override the automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="39b80-163">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="39b80-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="39b80-164">**Limit wyników**.</span><span class="sxs-lookup"><span data-stu-id="39b80-164">**Results limit**.</span></span> <span data-ttu-id="39b80-165">Ma limitu 10 wierszy k na wyniki zwrócone z portalu.</span><span class="sxs-lookup"><span data-stu-id="39b80-165">There's a limit of about 10k rows on the results returned from the portal.</span></span> <span data-ttu-id="39b80-166">Ostrzeżenie pokazuje, jeśli można przejść przekracza limit.</span><span class="sxs-lookup"><span data-stu-id="39b80-166">A warning shows if you go over the limit.</span></span> <span data-ttu-id="39b80-167">Jeśli tak się stanie, sortowanie wyników w tabeli nie będzie zawsze pokazywać wszystkie rzeczywiste pierwszego lub ostatniego wyniki.</span><span class="sxs-lookup"><span data-stu-id="39b80-167">If that happens, sorting your results in the table won't always show you all the actual first or last results.</span></span> 

    <span data-ttu-id="39b80-168">Dobrym rozwiązaniem, aby uniknąć naciśnięcie limit jest.</span><span class="sxs-lookup"><span data-stu-id="39b80-168">It's good practice to avoid hitting the limit.</span></span> <span data-ttu-id="39b80-169">Użyj filtru zakres czasu lub używać operatorów, takich jak:</span><span class="sxs-lookup"><span data-stu-id="39b80-169">Use the time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="39b80-170">100 najpopularniejszych przez sygnatury czasowej</span><span class="sxs-lookup"><span data-stu-id="39b80-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="39b80-171">podejmij 100</span><span class="sxs-lookup"><span data-stu-id="39b80-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="39b80-172">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="39b80-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="39b80-173">gdzie sygnatury czasowej > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="39b80-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="39b80-174">(Więcej niż 10 KB wierszy chcesz?</span><span class="sxs-lookup"><span data-stu-id="39b80-174">(Want more than 10k rows?</span></span> <span data-ttu-id="39b80-175">Należy rozważyć użycie [eksportu ciągłego](app-insights-export-telemetry.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="39b80-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="39b80-176">Analiza jest przeznaczona dla analizy, a nie podczas pobierania danych pierwotnych).</span><span class="sxs-lookup"><span data-stu-id="39b80-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="39b80-177">Diagramy</span><span class="sxs-lookup"><span data-stu-id="39b80-177">Diagrams</span></span>
<span data-ttu-id="39b80-178">Wybierz typ diagramu, który chcesz:</span><span class="sxs-lookup"><span data-stu-id="39b80-178">Select the type of diagram you'd like:</span></span>

![Wybierz typ diagramu](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="39b80-180">Jeśli masz kilka kolumn prawego typów można x i osi y, a kolumna wymiarów, aby podzielić wyniki według.</span><span class="sxs-lookup"><span data-stu-id="39b80-180">If you have several columns of the right types, you can choose the x and y axes, and a column of dimensions to split the results by.</span></span>

<span data-ttu-id="39b80-181">Domyślnie wyniki są początkowo wyświetlane jako tabelę i ręcznie wybrać diagramu.</span><span class="sxs-lookup"><span data-stu-id="39b80-181">By default, results are initially displayed as a table, and you select the diagram manually.</span></span> <span data-ttu-id="39b80-182">Jednak można użyć [renderowania dyrektywy](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) na końcu zapytania, aby wybrać diagram.</span><span class="sxs-lookup"><span data-stu-id="39b80-182">But you can use the [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at the end of a query to select a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="39b80-183">Diagnostyka analityka</span><span class="sxs-lookup"><span data-stu-id="39b80-183">Analytics diagnostics</span></span>


<span data-ttu-id="39b80-184">Na timechart w przypadku nagłego kolekcji lub krok danych, mogą pojawić się zaznaczony punkt w wierszu.</span><span class="sxs-lookup"><span data-stu-id="39b80-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on the line.</span></span> <span data-ttu-id="39b80-185">Oznacza to, Diagnostyka Analytics zidentyfikowane kombinację właściwości, które odfiltrowywania nagła zmiana.</span><span class="sxs-lookup"><span data-stu-id="39b80-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out the sudden change.</span></span> <span data-ttu-id="39b80-186">Kliknij punkt, aby uzyskać więcej szczegółów na temat filtr i aby zobaczyć filtrowana wersja.</span><span class="sxs-lookup"><span data-stu-id="39b80-186">Click the point to get more detail on the filter, and to see the filtered version.</span></span> <span data-ttu-id="39b80-187">To może pomóc w identyfikacji, co powoduje zmianę.</span><span class="sxs-lookup"><span data-stu-id="39b80-187">This may help you identify what caused the change.</span></span> 

[<span data-ttu-id="39b80-188">Dowiedz się więcej o diagnostyce analityka</span><span class="sxs-lookup"><span data-stu-id="39b80-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Diagnostyka analityka](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-to-dashboard"></a><span data-ttu-id="39b80-190">Przypnij do pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="39b80-190">Pin to dashboard</span></span>
<span data-ttu-id="39b80-191">Możesz przypinać diagramu lub tabeli do jednego z Twojej [udostępnionych pulpitów nawigacyjnych](app-insights-dashboards.md) — wystarczy kliknąć numer pin.</span><span class="sxs-lookup"><span data-stu-id="39b80-191">You can pin a diagram or table to one of your [shared dashboards](app-insights-dashboards.md) - just click the pin.</span></span> <span data-ttu-id="39b80-192">(Może być konieczne [uaktualniania aplikacji przez cennik pakietu](app-insights-pricing.md) Aby włączyć tę funkcję.)</span><span class="sxs-lookup"><span data-stu-id="39b80-192">(You might need to [upgrade your app's pricing package](app-insights-pricing.md) to turn on this feature.)</span></span> 

![Kliknij przycisk kod pin](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="39b80-194">Oznacza to, że jeśli Podsumowując pulpicie nawigacyjnym, aby ułatwić sobie monitorowanie wydajności lub użycia usług sieci web mogą być dość złożone analizy obok innych metryk.</span><span class="sxs-lookup"><span data-stu-id="39b80-194">This means that, when you put together a dashboard to help you monitor the performance or usage of your web services, you can include quite complex analysis alongside the other metrics.</span></span> 

<span data-ttu-id="39b80-195">Możesz przypinać tabeli do pulpitu nawigacyjnego, jeśli ma cztery lub mniejszą liczbę kolumn.</span><span class="sxs-lookup"><span data-stu-id="39b80-195">You can pin a table to the dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="39b80-196">Górne siedmiu wiersze są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="39b80-196">Only the top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="39b80-197">Odświeżanie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="39b80-197">Dashboard refresh</span></span>
<span data-ttu-id="39b80-198">Wykres przypięty do pulpitu nawigacyjnego jest automatycznie odświeżany przez ponowne uruchomienie zapytania co około godzin.</span><span class="sxs-lookup"><span data-stu-id="39b80-198">The chart pinned to the dashboard is refreshed automatically by re-running the query approximately every hours.</span></span> <span data-ttu-id="39b80-199">Można również kliknij przycisk Odśwież.</span><span class="sxs-lookup"><span data-stu-id="39b80-199">You can also click the Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="39b80-200">Automatyczne uproszczenia</span><span class="sxs-lookup"><span data-stu-id="39b80-200">Automatic simplifications</span></span>

<span data-ttu-id="39b80-201">Niektóre uproszczenia są stosowane do wykresu, gdy przypiąć go do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="39b80-201">Certain simplifications are applied to a chart when you pin it to a dashboard.</span></span>

<span data-ttu-id="39b80-202">**Czas ograniczeń:** zapytania są automatycznie ograniczony do ostatnich 14 dni.</span><span class="sxs-lookup"><span data-stu-id="39b80-202">**Time restriction:** Queries are automatically limited to the past 14 days.</span></span> <span data-ttu-id="39b80-203">Efekt jest taki sam jak, jeśli kwerenda zawiera `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="39b80-203">The effect is the same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="39b80-204">**Ograniczenie liczby bin:** podczas wyświetlania wykresu, który ma wiele odrębny bins (zazwyczaj wykres słupkowy), mniej wypełnione bins są automatycznie grupowane w pojedynczy "inne" bin.</span><span class="sxs-lookup"><span data-stu-id="39b80-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), the less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="39b80-205">Na przykład tego zapytania:</span><span class="sxs-lookup"><span data-stu-id="39b80-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="39b80-206">wygląda następująco w module analiz:</span><span class="sxs-lookup"><span data-stu-id="39b80-206">looks like this in Analytics:</span></span>

![Wykres z tail długa](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="39b80-208">Jednak gdy przypiąć go do pulpitu nawigacyjnego wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="39b80-208">but when you pin it to a dashboard, it looks like this:</span></span>

![Wykres z ograniczoną bins](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-to-excel"></a><span data-ttu-id="39b80-210">Eksportowanie do programu Excel</span><span class="sxs-lookup"><span data-stu-id="39b80-210">Export to Excel</span></span>
<span data-ttu-id="39b80-211">Po uruchomieniu kwerendy, można pobrać pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="39b80-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="39b80-212">Kliknij przycisk **wyeksportować Excel**.</span><span class="sxs-lookup"><span data-stu-id="39b80-212">Click **Export,  Excel**.</span></span>

## <a name="export-to-power-bi"></a><span data-ttu-id="39b80-213">Eksport do usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="39b80-213">Export to Power BI</span></span>
<span data-ttu-id="39b80-214">Umieść kursor w zapytaniu i wybierz polecenie **wyeksportować usługi Power BI**.</span><span class="sxs-lookup"><span data-stu-id="39b80-214">Put the cursor in a query and choose **Export, Power BI**.</span></span>

![Eksportowanie z Analytics z usługą Power BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="39b80-216">Możesz uruchomić zapytanie w usłudze Power BI.</span><span class="sxs-lookup"><span data-stu-id="39b80-216">You run the query in Power BI.</span></span> <span data-ttu-id="39b80-217">Można ustawić, aby odświeżyć zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="39b80-217">You can set it to refresh on a schedule.</span></span>

<span data-ttu-id="39b80-218">Usługa Power BI można tworzyć pulpity nawigacyjne, które zbieranie danych z różnych źródeł.</span><span class="sxs-lookup"><span data-stu-id="39b80-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="39b80-219">Dowiedz się więcej na temat eksportowania do usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="39b80-219">Learn more about export to Power BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="39b80-220">Głębokie łącze</span><span class="sxs-lookup"><span data-stu-id="39b80-220">Deep link</span></span>

<span data-ttu-id="39b80-221">Uzyskaj link w obszarze **eksportu, link udziału** wysyłanej do innego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="39b80-221">Get a link under **Export, Share link** that you can send to another user.</span></span> <span data-ttu-id="39b80-222">Podany użytkownik ma [dostępu do tej grupy zasobów](app-insights-resources-roles-access-control.md), zapytanie zostanie otwarty w Interfejsie użytkownika Analytics.</span><span class="sxs-lookup"><span data-stu-id="39b80-222">Provided the user has [access to your resource group](app-insights-resources-roles-access-control.md), the query will open in the Analytics UI.</span></span>

<span data-ttu-id="39b80-223">(Łącza, tekst zapytania jest umieszczany po "? q =" gzip skompresowane i algorytmem base-64.</span><span class="sxs-lookup"><span data-stu-id="39b80-223">(In the link, the query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="39b80-224">Można napisać kod, aby wygenerować głębokiego łącza, które zapewniają użytkownikom.</span><span class="sxs-lookup"><span data-stu-id="39b80-224">You could write code to generate deep links that you provide to users.</span></span> <span data-ttu-id="39b80-225">Jednak zalecanym sposobem Uruchom Analytics z kodu jest przy użyciu [interfejsu API REST](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="39b80-225">However, the recommended way to run Analytics from code is by using the [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="39b80-226">Automatyzacja</span><span class="sxs-lookup"><span data-stu-id="39b80-226">Automation</span></span>

<span data-ttu-id="39b80-227">Użyj [interfejsu API REST dostępu do danych](https://dev.applicationinsights.io/) do wykonywania kwerend Analytics.</span><span class="sxs-lookup"><span data-stu-id="39b80-227">Use the  [Data Access REST API](https://dev.applicationinsights.io/) to run Analytics queries.</span></span> <span data-ttu-id="39b80-228">[Na przykład](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (przy użyciu programu PowerShell):</span><span class="sxs-lookup"><span data-stu-id="39b80-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="39b80-229">W przeciwieństwie do interfejsu użytkownika analizy interfejsu API REST nie powoduje automatycznego dodania podlega żadnym ograniczeniom sygnatury czasowej do zapytania.</span><span class="sxs-lookup"><span data-stu-id="39b80-229">Unlike the Analytics UI, the REST API does not automatically add any timestamp limitation to your queries.</span></span> <span data-ttu-id="39b80-230">Pamiętaj, aby dodać własne-klauzuli where, aby uniknąć pobierania ogromnych odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="39b80-230">Remember to add your own where-clause, to avoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="39b80-231">Importowanie danych</span><span class="sxs-lookup"><span data-stu-id="39b80-231">Import data</span></span>

<span data-ttu-id="39b80-232">Dane można zaimportować z pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="39b80-232">You can import data from a CSV file.</span></span> <span data-ttu-id="39b80-233">Zwykle jest używane do importowania danych statycznych, które można połączyć z tabelami z telemetrii.</span><span class="sxs-lookup"><span data-stu-id="39b80-233">A typical usage is to import static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="39b80-234">Na przykład uwierzytelnieni użytkownicy są oznaczane w obrębie telemetrii alias lub zaciemnionego identyfikator, można zaimportować tabelę, która mapuje aliasów do rzeczywistej nazwy.</span><span class="sxs-lookup"><span data-stu-id="39b80-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases to real names.</span></span> <span data-ttu-id="39b80-235">Wykonując sprzężenie na dane telemetryczne żądania, można zidentyfikować użytkowników według ich rzeczywistym nazw w raportach analizy.</span><span class="sxs-lookup"><span data-stu-id="39b80-235">By performing a join on the request telemetry, you can identify users by their real names in the Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="39b80-236">Zdefiniuj schemat danych</span><span class="sxs-lookup"><span data-stu-id="39b80-236">Define your data schema</span></span>

1. <span data-ttu-id="39b80-237">Kliknij przycisk **ustawienia** (u góry po lewej), a następnie **źródeł danych**.</span><span class="sxs-lookup"><span data-stu-id="39b80-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="39b80-238">Dodawanie źródła danych, postępując zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="39b80-238">Add a data source, following the instructions.</span></span> <span data-ttu-id="39b80-239">Zostanie wyświetlona prośba o podanie przykładowych danych, który powinien zawierać co najmniej 10 wierszy.</span><span class="sxs-lookup"><span data-stu-id="39b80-239">You are asked to supply a sample of the data, which should include at least ten rows.</span></span> <span data-ttu-id="39b80-240">Następnie Popraw schemat.</span><span class="sxs-lookup"><span data-stu-id="39b80-240">You then correct the schema.</span></span>

<span data-ttu-id="39b80-241">Określa źródło danych, które można następnie zaimportować poszczególnych tabel.</span><span class="sxs-lookup"><span data-stu-id="39b80-241">This defines a data source, which you can then use to import individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="39b80-242">Importowanie tabeli</span><span class="sxs-lookup"><span data-stu-id="39b80-242">Import a table</span></span>

1. <span data-ttu-id="39b80-243">Otwórz z definicji źródła danych z listy.</span><span class="sxs-lookup"><span data-stu-id="39b80-243">Open your data source definition from the list.</span></span>
2. <span data-ttu-id="39b80-244">Kliknij przycisk "Przekaż", a następnie postępuj zgodnie z instrukcjami, aby przekazać tabeli.</span><span class="sxs-lookup"><span data-stu-id="39b80-244">Click "Upload" and follow the instructions to upload the table.</span></span> <span data-ttu-id="39b80-245">Obejmuje to wywołanie interfejsu API REST i dlatego jest łatwy do automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="39b80-245">This involves a call to a REST API, and so it is easy to automate.</span></span> 

<span data-ttu-id="39b80-246">Tabela jest teraz dostępna do użycia w zapytaniach Analytics.</span><span class="sxs-lookup"><span data-stu-id="39b80-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="39b80-247">Zostanie wyświetlony na analityka</span><span class="sxs-lookup"><span data-stu-id="39b80-247">It will appear in Analytics</span></span> 

### <a name="use-the-table"></a><span data-ttu-id="39b80-248">Skorzystaj z tabeli</span><span class="sxs-lookup"><span data-stu-id="39b80-248">Use the table</span></span>

<span data-ttu-id="39b80-249">Załóżmy, że Twoje definicji źródła danych jest nazywany `usermap`, i ma dwa pola `realName` i `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="39b80-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="39b80-250">`requests` Tabeli również zawiera pole o nazwie `user_AuthenticatedId`, dzięki czemu łatwiej je dołączyć:</span><span class="sxs-lookup"><span data-stu-id="39b80-250">The `requests` table also has a field named `user_AuthenticatedId`, so it's easy to join them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="39b80-251">Tabeli wynikowej żądania ma dodatkowe kolumny `realName`.</span><span class="sxs-lookup"><span data-stu-id="39b80-251">The resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="39b80-252">Importuj z LogStash</span><span class="sxs-lookup"><span data-stu-id="39b80-252">Import from LogStash</span></span>

<span data-ttu-id="39b80-253">Jeśli używasz [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), analizy służy do badania dzienników.</span><span class="sxs-lookup"><span data-stu-id="39b80-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics to query your logs.</span></span> <span data-ttu-id="39b80-254">Użyj [wtyczkę, która powoduje przekazanie w potoku danych do analizy](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="39b80-254">Use the [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="39b80-255">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="39b80-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

