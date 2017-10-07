---
title: "Samouczek aaaA przez analityka w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Krótki próbki wszystkie hello głównego kwerendy w module analiz, hello wyszukiwania zaawansowanego narzędzia Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="37440-103">Samouczek analizy w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="37440-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="37440-104">[Analiza](app-insights-analytics.md) to funkcja wyszukiwania zaawansowanego hello [usługi Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37440-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="37440-105">Te strony opisano język zapytań usługi Analiza dzienników.</span><span class="sxs-lookup"><span data-stu-id="37440-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="37440-106">**[Obejrzyj klip wideo wprowadzenia hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="37440-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="37440-107">**[Przetestuj Analytics na naszych danych symulowane](https://analytics.applicationinsights.io/demo)**  aplikacji nie jest jeszcze wysyłania danych tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="37440-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="37440-108">**[Ściągawka SQL użytkowników](https://aka.ms/sql-analytics)**  tłumaczy hello idioms najczęściej.</span><span class="sxs-lookup"><span data-stu-id="37440-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>

<span data-ttu-id="37440-109">Spójrzmy przechodzenia przez tooget niektórych podstawowych zapytań, uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="37440-109">Let's take a walk through some basic queries tooget you started.</span></span>

## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="37440-110">Połącz dane usługi Application Insights tooyour</span><span class="sxs-lookup"><span data-stu-id="37440-110">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="37440-111">Otwórz Analytics z aplikacji [bloku omówienie](app-insights-dashboards.md) w usłudze Application Insights:</span><span class="sxs-lookup"><span data-stu-id="37440-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![Otwórz portal.azure.com otworzyć zasobu usługi Application Insights, a następnie kliknij przycisk Analytics.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="37440-113">[Podejmij](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): Pokaż n wierszy</span><span class="sxs-lookup"><span data-stu-id="37440-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="37440-114">Punkty danych, którzy logują się operacji użytkownika (zwykle żądania HTTP odebrane przez aplikację sieci web) są przechowywane w tabeli o nazwie `requests`.</span><span class="sxs-lookup"><span data-stu-id="37440-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="37440-115">Każdy wiersz jest punkt danych telemetrii otrzymanych od hello zestaw SDK usługi Application Insights w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37440-115">Each row is a telemetry data point received from hello Application Insights SDK in your app.</span></span>

<span data-ttu-id="37440-116">Zacznijmy od badanie kilka przykładowych wiersze tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="37440-116">Let's start by examining a few sample rows of hello table:</span></span>

![wyniki](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="37440-118">Gdzieś umieść kursor hello w instrukcji hello przed kliknięciem przycisku Przejdź.</span><span class="sxs-lookup"><span data-stu-id="37440-118">Put hello cursor somewhere in hello statement before you click Go.</span></span> <span data-ttu-id="37440-119">Można podzielić instrukcję przez więcej niż jeden wiersz, ale nie należy umieszczać pustych wierszy w instrukcji.</span><span class="sxs-lookup"><span data-stu-id="37440-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="37440-120">Puste wiersze są tookeep wygodny sposób kilku oddzielnych zapytania w oknie hello.</span><span class="sxs-lookup"><span data-stu-id="37440-120">Blank lines are a convenient way tookeep several separate queries in hello window.</span></span>
>
>

<span data-ttu-id="37440-121">Wybierz kolumny, przeciągnij je Grupuj według kolumn i filtrowania:</span><span class="sxs-lookup"><span data-stu-id="37440-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Kliknij kolumnę zaznaczenia w prawym górnym rogu wyników](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="37440-123">Rozwiń żadnych szczegółów elementu toosee hello:</span><span class="sxs-lookup"><span data-stu-id="37440-123">Expand any item toosee hello detail:</span></span>

![Wybierz tabelę i użyj kolumn skonfigurować](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="37440-125">Kliknij nagłówek hello dostępnych w przeglądarce sieci web hello wyników hello toore kolejność kolumn.</span><span class="sxs-lookup"><span data-stu-id="37440-125">Click hello head of a column toore-order hello results available in hello web browser.</span></span> <span data-ttu-id="37440-126">Należy jednak pamiętać, że dla zestawu wyników dużych hello liczba wierszy pobrany toohello przeglądarki jest ograniczona.</span><span class="sxs-lookup"><span data-stu-id="37440-126">But be aware that for a large result set, hello number of rows downloaded toohello browser is limited.</span></span> <span data-ttu-id="37440-127">W ten sposób sortowania nie zawsze pokazuj hello rzeczywiste najwyższy lub najniższy elementów.</span><span class="sxs-lookup"><span data-stu-id="37440-127">Sorting this way doesn't always show you hello actual highest or lowest items.</span></span> <span data-ttu-id="37440-128">elementy toosort niezawodnie, użyj hello `top` lub `sort` operatora.</span><span class="sxs-lookup"><span data-stu-id="37440-128">toosort items reliably, use hello `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="37440-129">[TOP](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) i [sortowania](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="37440-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="37440-130">`take`jest przydatne tooget próbkę szybkie wyniku, ale zawiera wiersze z tabeli hello w losowej kolejności.</span><span class="sxs-lookup"><span data-stu-id="37440-130">`take` is useful tooget a quick sample of a result, but it shows rows from hello table in no particular order.</span></span> <span data-ttu-id="37440-131">Użyj tooget uporządkowanej widoku `top` (na przykład) lub `sort` (za pośrednictwem hello całej tabeli).</span><span class="sxs-lookup"><span data-stu-id="37440-131">tooget an ordered view, use `top` (for a sample) or `sort` (over hello whole table).</span></span>

<span data-ttu-id="37440-132">Pokaż hello pierwsze n wierszy, uporządkowanych według określonej kolumny:</span><span class="sxs-lookup"><span data-stu-id="37440-132">Show me hello first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="37440-133">*Składnia:* większość operatorów mieć — słowo kluczowe parametrów, takich jak `by`.</span><span class="sxs-lookup"><span data-stu-id="37440-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="37440-134">`desc`= w kolejności malejącej `asc` = rosnąca.</span><span class="sxs-lookup"><span data-stu-id="37440-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="37440-135">`top...`więcej możliwości wydajności z informacją o tym `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="37440-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="37440-136">Firma Microsoft może mieć zapisane:</span><span class="sxs-lookup"><span data-stu-id="37440-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="37440-137">Witaj nastąpiłoby hello takie same, ale może działać nieco wolniej.</span><span class="sxs-lookup"><span data-stu-id="37440-137">hello result would be hello same, but it would run a bit more slowly.</span></span> <span data-ttu-id="37440-138">(Można również napisać `order`, który jest aliasem `sort`.)</span><span class="sxs-lookup"><span data-stu-id="37440-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="37440-139">Hello nagłówków kolumn w widoku tabeli hello może być również używane toosort hello wyników na ekranie powitania.</span><span class="sxs-lookup"><span data-stu-id="37440-139">hello column headers in hello table view can also be used toosort hello results on hello screen.</span></span> <span data-ttu-id="37440-140">Oczywiście jeśli był używany, ale `take` lub `top` tooretrieve tylko część tabeli, będzie tylko zmienić kolejność hello rekordów została pobrana.</span><span class="sxs-lookup"><span data-stu-id="37440-140">But of course, if you've used `take` or `top` tooretrieve just part of a table, you'll only re-order hello records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="37440-141">[Gdzie](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtrowanie warunek</span><span class="sxs-lookup"><span data-stu-id="37440-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="37440-142">Zobaczmy, po prostu żądań, które zwróciło kod określonego wyniku:</span><span class="sxs-lookup"><span data-stu-id="37440-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="37440-143">Witaj `where` operator przyjmuje wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="37440-143">hello `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="37440-144">Poniżej przedstawiono niektóre najważniejszych o nich:</span><span class="sxs-lookup"><span data-stu-id="37440-144">Here are some key points about them:</span></span>

* <span data-ttu-id="37440-145">`and`, `or`: Operatory logiczne</span><span class="sxs-lookup"><span data-stu-id="37440-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="37440-146">`==`, `<>`, `!=` : równa i nie ma wartości</span><span class="sxs-lookup"><span data-stu-id="37440-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="37440-147">`=~`, `!~` : ciąg bez uwzględniania wielkości liter równy i różne.</span><span class="sxs-lookup"><span data-stu-id="37440-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="37440-148">Istnieje wiele więcej operatorów porównywania ciągów.</span><span class="sxs-lookup"><span data-stu-id="37440-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a><span data-ttu-id="37440-149">Pobieranie hello odpowiedniego typu.</span><span class="sxs-lookup"><span data-stu-id="37440-149">Getting hello right type</span></span>
<span data-ttu-id="37440-150">Znajdź żądania nie powiodło się:</span><span class="sxs-lookup"><span data-stu-id="37440-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="37440-151">Time</span><span class="sxs-lookup"><span data-stu-id="37440-151">Time</span></span>

<span data-ttu-id="37440-152">Domyślnie zapytania są ograniczone toohello ostatnich 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="37440-152">By default, your queries are restricted toohello last 24 hours.</span></span> <span data-ttu-id="37440-153">Można jednak zmienić ten zakres:</span><span class="sxs-lookup"><span data-stu-id="37440-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="37440-154">Zastąpienie zakres czasu hello pisząc każde zapytanie operacji uwzględniającą `timestamp` w klauzuli where.</span><span class="sxs-lookup"><span data-stu-id="37440-154">Override hello time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="37440-155">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="37440-155">For example:</span></span>

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

<span data-ttu-id="37440-156">Funkcja zakres czasu Hello jest równoważne tooa 'where' klauzuli wstawiane po każdej informację o jedną z tabel źródłowych hello.</span><span class="sxs-lookup"><span data-stu-id="37440-156">hello time range feature is equivalent tooa 'where' clause inserted after each mention of one of hello source tables.</span></span>

<span data-ttu-id="37440-157">`ago(3d)`oznacza, że "trzy dni temu".</span><span class="sxs-lookup"><span data-stu-id="37440-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="37440-158">Inne jednostki czasu obejmują godzin (`2h`, `2.5h`), minut (`25m`), a sekund (`10s`).</span><span class="sxs-lookup"><span data-stu-id="37440-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="37440-159">Inne przykłady:</span><span class="sxs-lookup"><span data-stu-id="37440-159">Other examples:</span></span>

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

<span data-ttu-id="37440-160">[Daty i godziny odwołanie](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="37440-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="37440-161">[Projekt](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): Wybierz, Zmień nazwę, a kolumny obliczeniowe</span><span class="sxs-lookup"><span data-stu-id="37440-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="37440-162">Użyj [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick się tylko kolumny hello chcesz:</span><span class="sxs-lookup"><span data-stu-id="37440-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out just hello columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="37440-163">Można również zmienić nazwy kolumny i zdefiniować nowe:</span><span class="sxs-lookup"><span data-stu-id="37440-163">You can also rename columns and define new ones:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![wynik](./media/app-insights-analytics-tour/270.png)

* <span data-ttu-id="37440-165">Nazwy kolumny może zawierać spacje lub symbole, jeśli są one oddzielona podobnie do następującej: `['...']` lub`["..."]`</span><span class="sxs-lookup"><span data-stu-id="37440-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="37440-166">`%`hello jest zwykle operatora modulo.</span><span class="sxs-lookup"><span data-stu-id="37440-166">`%` is hello usual modulo operator.</span></span>
* <span data-ttu-id="37440-167">`1d`(to cyfrę, jedną, a następnie miał ") jest wartość typu timespan literału oznacza jeden dzień.</span><span class="sxs-lookup"><span data-stu-id="37440-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="37440-168">Poniżej przedstawiono niektóre więcej literały timespan: `12h`, `30m`, `10s`, `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="37440-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="37440-169">`floor`(alias `bin`) zaokrągla wartość w dół toohello najbliższej wielokrotności wartości podstawowej hello, musisz podać.</span><span class="sxs-lookup"><span data-stu-id="37440-169">`floor` (alias `bin`) rounds a value down toohello nearest multiple of hello base value you provide.</span></span> <span data-ttu-id="37440-170">Dlatego `floor(aTime, 1s)` zaokrągla czasu dół toohello najbliższej sekundy.</span><span class="sxs-lookup"><span data-stu-id="37440-170">So `floor(aTime, 1s)` rounds a time down toohello nearest second.</span></span>

<span data-ttu-id="37440-171">Wyrażenia mogą zawierać wszystkie operatory zwykle hello (`+`, `-`,...), a istnieje szereg przydatne funkcje.</span><span class="sxs-lookup"><span data-stu-id="37440-171">Expressions can include all hello usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="37440-172">Rozszerzanie</span><span class="sxs-lookup"><span data-stu-id="37440-172">Extend</span></span>
<span data-ttu-id="37440-173">Po prostu toohello kolumn tooadd istniejące grupy, należy użyć [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="37440-173">If you just want tooadd columns toohello existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="37440-174">Przy użyciu [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) mniej szczegółowe niż [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) Jeśli chcesz tookeep hello wszystkie istniejące kolumny.</span><span class="sxs-lookup"><span data-stu-id="37440-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want tookeep all hello existing columns.</span></span>

### <a name="convert-toolocal-time"></a><span data-ttu-id="37440-175">Konwertuj toolocal czasu</span><span class="sxs-lookup"><span data-stu-id="37440-175">Convert toolocal time</span></span>

<span data-ttu-id="37440-176">Sygnatury czasowe są zawsze w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="37440-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="37440-177">Dlatego jeśli używasz wybrzeże Pacyfiku nam hello jest zima, może Cię zainteresować to:</span><span class="sxs-lookup"><span data-stu-id="37440-177">So if you're on hello US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="37440-178">[Podsumuj](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): agregacji grupy wierszy</span><span class="sxs-lookup"><span data-stu-id="37440-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="37440-179">`Summarize`zastosowanie określonej *funkcji agregacji* za pośrednictwem grupy wierszy.</span><span class="sxs-lookup"><span data-stu-id="37440-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="37440-180">Na przykład czasie hello aplikacji sieci web żądania tooa toorespond jest zgłaszany w polu hello `duration`.</span><span class="sxs-lookup"><span data-stu-id="37440-180">For example, hello time your web app takes toorespond tooa request is reported in hello field `duration`.</span></span> <span data-ttu-id="37440-181">Zobaczmy hello odpowiedzi średni czas żądania tooall:</span><span class="sxs-lookup"><span data-stu-id="37440-181">Let's see hello average response time tooall requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="37440-182">Lub wynik hello można oddzielić do żądań różne nazwy elementu:</span><span class="sxs-lookup"><span data-stu-id="37440-182">Or we could separate hello result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="37440-183">`Summarize`zbiera hello punktów danych w strumieniu hello w grupach, dla których hello `by` klauzuli ocenia jednakowo.</span><span class="sxs-lookup"><span data-stu-id="37440-183">`Summarize` collects hello data points in hello stream into groups for which hello `by` clause evaluates equally.</span></span> <span data-ttu-id="37440-184">Każda wartość w hello `by` wyrażenie - nazwy operacji w hello powyżej przykład — powoduje wiersz w tabeli wyników hello.</span><span class="sxs-lookup"><span data-stu-id="37440-184">Each value in hello `by` expression - each operation name in hello above example - results in a row in hello result table.</span></span>

<span data-ttu-id="37440-185">Lub firma Microsoft może grupowania wyników według pora dnia:</span><span class="sxs-lookup"><span data-stu-id="37440-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="37440-186">Zwróć uwagę, jak firma Microsoft korzysta z hello `bin` — funkcja (alias `floor`).</span><span class="sxs-lookup"><span data-stu-id="37440-186">Notice how we're using hello `bin` function (aka `floor`).</span></span> <span data-ttu-id="37440-187">Jeśli będziemy używać `by timestamp`, co wejściowych wiersza pojawiłyby w niewielkim grupy.</span><span class="sxs-lookup"><span data-stu-id="37440-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="37440-188">Dla dowolnego ciągłego skalarną podobnego razy lub numerów mamy toobreak hello ciągły zakres na zarządzaniu liczbę wartości dyskretnych.</span><span class="sxs-lookup"><span data-stu-id="37440-188">For any continuous scalar like times or numbers, we have toobreak hello continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="37440-189">`bin`— co jest po prostu hello znanych zaokrąglania rozwijanej `floor` funkcji — jest hello Najprostszym sposobem toodo który.</span><span class="sxs-lookup"><span data-stu-id="37440-189">`bin` - which is just hello familiar rounding-down `floor` function - is hello easiest way toodo that.</span></span>

<span data-ttu-id="37440-190">Możemy użyć hello tego samego zakresy tooreduce technika ciągów:</span><span class="sxs-lookup"><span data-stu-id="37440-190">We can use hello same technique tooreduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="37440-191">Należy zauważyć, że można użyć `name=` tooset hello nazwy kolumny wynik, w wyrażeniach agregacji hello lub hello przez klauzuli.</span><span class="sxs-lookup"><span data-stu-id="37440-191">Notice that you can use `name=` tooset hello name of a result column, either in hello aggregation expressions or hello by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="37440-192">Zliczanie próbce danych</span><span class="sxs-lookup"><span data-stu-id="37440-192">Counting sampled data</span></span>
<span data-ttu-id="37440-193">`sum(itemCount)`jest hello zalecane agregacji toocount zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="37440-193">`sum(itemCount)` is hello recommended aggregation toocount events.</span></span> <span data-ttu-id="37440-194">W wielu przypadkach wartość elementu itemCount == 1, dlatego funkcja powitania po prostu liczy w górę hello liczbę wierszy w grupie hello.</span><span class="sxs-lookup"><span data-stu-id="37440-194">In many cases, itemCount==1, so hello function simply counts up hello number of rows in hello group.</span></span> <span data-ttu-id="37440-195">Ale jeśli [próbkowania](app-insights-sampling.md) jest operacji, tylko część oryginalnego zdarzenia hello są przechowywane jako punkty danych w usłudze Application Insights, aby dla każdego punktu danych, zostanie wyświetlony, `itemCount` zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="37440-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of hello original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="37440-196">Na przykład, jeśli próbkowania odrzuca 75% hello oryginalnego zdarzenia, a następnie wartość elementu itemCount == 4 w rekordach hello zachowane - oznacza to, dla każdego rekordu zachowanych, były cztery oryginalnego rekordy.</span><span class="sxs-lookup"><span data-stu-id="37440-196">For example, if sampling discards 75% of hello original events, then itemCount==4 in hello retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="37440-197">Adaptacyjną próbkowania powoduje, że wartość elementu itemCount toobe wyższe w okresach, gdy aplikacja jest używana często.</span><span class="sxs-lookup"><span data-stu-id="37440-197">Adaptive sampling causes itemCount toobe higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="37440-198">W związku z tym sumowania wartość elementu itemCount zapewnia dobre oszacowanie hello oryginalna liczba zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="37440-198">Summing up itemCount therefore gives a good estimate of hello original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="37440-199">Istnieje również `count()` agregacji (i operacji liczby), w przypadku których na pewno chcesz toocount hello liczbę wierszy w grupie.</span><span class="sxs-lookup"><span data-stu-id="37440-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want toocount hello number of rows in a group.</span></span>

<span data-ttu-id="37440-200">Istnieje szereg [funkcje agregacji](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="37440-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-hello-results"></a><span data-ttu-id="37440-201">Wykresy wyników hello</span><span class="sxs-lookup"><span data-stu-id="37440-201">Charting hello results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="37440-202">Domyślnie wyniki są wyświetlane jako tabelę:</span><span class="sxs-lookup"><span data-stu-id="37440-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="37440-203">Możemy lepiej niż hello tabeli widoku.</span><span class="sxs-lookup"><span data-stu-id="37440-203">We can do better than hello table view.</span></span> <span data-ttu-id="37440-204">Przyjrzyjmy się hello wyniki w widoku wykresu hello z opcją pionowy pasek hello:</span><span class="sxs-lookup"><span data-stu-id="37440-204">Let's look at hello results in hello chart view with hello vertical bar option:</span></span>

![Kliknij wykres, a następnie wybrać wykres słupkowy pionowy i przypisać x i y osi](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="37440-206">Zwróć uwagę, że chociaż firma Microsoft nie sortowanie wyników hello czasu (jak widać w wyświetlanej tabeli hello), wyświetlania wykresu hello zawsze zawiera dat i godzin w odpowiedniej kolejności.</span><span class="sxs-lookup"><span data-stu-id="37440-206">Notice that although we didn't sort hello results by time (as you can see in hello table display), hello chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="37440-207">Timecharts</span><span class="sxs-lookup"><span data-stu-id="37440-207">Timecharts</span></span>
<span data-ttu-id="37440-208">Pokaż liczbę zdarzeń są każdej godziny:</span><span class="sxs-lookup"><span data-stu-id="37440-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="37440-209">Wybierz opcję wyświetlania wykresu hello:</span><span class="sxs-lookup"><span data-stu-id="37440-209">Select hello Chart display option:</span></span>

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="37440-211">Wiele serii</span><span class="sxs-lookup"><span data-stu-id="37440-211">Multiple series</span></span>
<span data-ttu-id="37440-212">Wiele wyrażeń w hello `summarize` klauzuli tworzy wiele kolumn.</span><span class="sxs-lookup"><span data-stu-id="37440-212">Multiple expressions in hello `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="37440-213">Wiele wyrażeń w hello `by` klauzuli tworzy wiele wierszy, po jednej dla każdej kombinacji wartości.</span><span class="sxs-lookup"><span data-stu-id="37440-213">Multiple expressions in hello `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabela żądań przez godzinę i lokalizację](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="37440-215">Segment wykresu wielowymiarowa</span><span class="sxs-lookup"><span data-stu-id="37440-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="37440-216">Jeśli wykresu tabeli zawierającej kolumny typu string i kolumny liczbowej ciąg hello może być używane toosplit hello dane liczbowe w oddzielnych serii punktów.</span><span class="sxs-lookup"><span data-stu-id="37440-216">If you chart a table that has a string column and a numeric column, hello string can be used toosplit hello numeric data into separate series of points.</span></span> <span data-ttu-id="37440-217">Jeśli istnieje więcej niż jednej kolumny typu string, toouse kolumny, które można wybrać jako dyskryminatora hello.</span><span class="sxs-lookup"><span data-stu-id="37440-217">If there's more than one string column, you can choose which column toouse as hello discriminator.</span></span>

![Segment wykres analizy](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="37440-219">Odbijanie szybkości</span><span class="sxs-lookup"><span data-stu-id="37440-219">Bounce rate</span></span>

<span data-ttu-id="37440-220">Konwertuj toouse ciąg logiczna tooa go jako dyskryminatora:</span><span class="sxs-lookup"><span data-stu-id="37440-220">Convert a boolean tooa string toouse it as a discriminator:</span></span>

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a><span data-ttu-id="37440-221">Wyświetlania wielu metryk</span><span class="sxs-lookup"><span data-stu-id="37440-221">Display multiple metrics</span></span>
<span data-ttu-id="37440-222">Jeśli wykresu tabeli, która ma więcej niż jednej kolumny liczbowe, w znaczników dodaniu toohello czasu, można wyświetlić dowolną kombinację.</span><span class="sxs-lookup"><span data-stu-id="37440-222">If you chart a table that has more than one numeric column, in addition toohello timestamp, you can display any combination of them.</span></span>

![Segment wykres analizy](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="37440-224">Musisz wybrać **nie podziału** zanim będzie można wybrać wiele kolumn liczbowych.</span><span class="sxs-lookup"><span data-stu-id="37440-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="37440-225">Nie można podzielić według kolumny ciągu na powitania sam czas jako wyświetlanie więcej niż jednej kolumny liczbowej.</span><span class="sxs-lookup"><span data-stu-id="37440-225">You can't split by a string column at hello same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="37440-226">Cykl średni dzienny</span><span class="sxs-lookup"><span data-stu-id="37440-226">Daily average cycle</span></span>
<span data-ttu-id="37440-227">Sposób użycia różne za pośrednictwem hello typowego dnia?</span><span class="sxs-lookup"><span data-stu-id="37440-227">How does usage vary over hello average day?</span></span>

<span data-ttu-id="37440-228">Liczba żądań przez czas hello modulo jeden dzień, binned na godziny:</span><span class="sxs-lookup"><span data-stu-id="37440-228">Count requests by hello time modulo one day, binned into hours:</span></span>

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Wykres liniowy godzin w typowego dnia](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> <span data-ttu-id="37440-230">Zwróć uwagę, że obecnie mamy tooconvert czas trwania toodatetimes w kolejności toodisplay wykres liniowy.</span><span class="sxs-lookup"><span data-stu-id="37440-230">Notice that we currently have tooconvert time durations toodatetimes in order toodisplay on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="37440-231">Porównywanie wielu serii codziennie</span><span class="sxs-lookup"><span data-stu-id="37440-231">Compare multiple daily series</span></span>
<span data-ttu-id="37440-232">Jak czy użycia różnią się od wraz z upływem czasu hello dnia w różnych krajach?</span><span class="sxs-lookup"><span data-stu-id="37440-232">How does usage vary over hello time of day in different countries?</span></span>

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![Podziel przez client_CountryOrRegion](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a><span data-ttu-id="37440-234">Wykreślenia dystrybucji</span><span class="sxs-lookup"><span data-stu-id="37440-234">Plot a distribution</span></span>
<span data-ttu-id="37440-235">Ile sesji są dostępne różne długości?</span><span class="sxs-lookup"><span data-stu-id="37440-235">How many sessions are there of different lengths?</span></span>

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

<span data-ttu-id="37440-236">ostatni wiersz Hello jest toodatetime tooconvert wymagane.</span><span class="sxs-lookup"><span data-stu-id="37440-236">hello last line is required tooconvert toodatetime.</span></span> <span data-ttu-id="37440-237">Obecnie hello x osi wykresu jest wyświetlana jako skalarnej tylko wtedy, gdy jest wartość datetime.</span><span class="sxs-lookup"><span data-stu-id="37440-237">Currently hello x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="37440-238">Witaj `where` klauzuli wyklucza jednorazowej sesji (sessionDuration == 0) i zestawy hello długość hello osi x.</span><span class="sxs-lookup"><span data-stu-id="37440-238">hello `where` clause excludes one-shot sessions (sessionDuration==0) and sets hello length of hello x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="37440-239">Percentylu</span><span class="sxs-lookup"><span data-stu-id="37440-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="37440-240">Jakie zakresów czasu trwania obejmują różne wartości procentowe sesji?</span><span class="sxs-lookup"><span data-stu-id="37440-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="37440-241">Użyj hello powyżej kwerendy, ale zastępuje hello ostatni wiersz:</span><span class="sxs-lookup"><span data-stu-id="37440-241">Use hello above query, but replace hello last line:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

<span data-ttu-id="37440-242">Również usunęliśmy hello górny limit hello, w którym klauzula w kolejności tooget poprawić rysunki w tym wszystkie sesje z więcej niż jedno żądanie:</span><span class="sxs-lookup"><span data-stu-id="37440-242">We also removed hello upper limit in hello where clause, in order tooget correct figures including all sessions with more than one request:</span></span>

![wynik](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="37440-244">Z którego możemy stwierdzić, że:</span><span class="sxs-lookup"><span data-stu-id="37440-244">From which we can see that:</span></span>

* <span data-ttu-id="37440-245">5% sesji ma czasu trwania z więcej niż trzy minuty 34s;</span><span class="sxs-lookup"><span data-stu-id="37440-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="37440-246">50% sesji ostatni 36 minut;</span><span class="sxs-lookup"><span data-stu-id="37440-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="37440-247">5% sesji ostatnie więcej niż 7 dni</span><span class="sxs-lookup"><span data-stu-id="37440-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="37440-248">tooget podział osobne dla każdego kraju mamy właśnie toobring hello client_CountryOrRegion kolumny z osobna za pomocą obu Podsumuj operatory:</span><span class="sxs-lookup"><span data-stu-id="37440-248">tooget a separate breakdown for each country, we just have toobring hello client_CountryOrRegion column separately through both summarize operators:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a><span data-ttu-id="37440-249">Join</span><span class="sxs-lookup"><span data-stu-id="37440-249">Join</span></span>
<span data-ttu-id="37440-250">Mamy dostęp tooseveral tabele wraz ze żądań i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="37440-250">We have access tooseveral tables, including requests and exceptions.</span></span>

<span data-ttu-id="37440-251">toofind hello wyjątki powiązane tooa żądania zwrócił odpowiedź awarii, firma Microsoft może dołączyć do tabel hello na `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="37440-251">toofind hello exceptions related tooa request that returned a failure response, we can join hello tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="37440-252">Jest dobrym rozwiązaniem toouse `project` tooselect hello tylko kolumny potrzebujemy przed wykonaniem hello sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="37440-252">It's good practice toouse `project` tooselect just hello columns we need before performing hello join.</span></span>
<span data-ttu-id="37440-253">W hello tego samego klauzule możemy zmienić nazwy kolumny znaczników czasu hello.</span><span class="sxs-lookup"><span data-stu-id="37440-253">In hello same clauses, we rename hello timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a><span data-ttu-id="37440-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): przypisano zmienną tooa wyników</span><span class="sxs-lookup"><span data-stu-id="37440-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result tooa variable</span></span>

<span data-ttu-id="37440-255">Użyj `let` tooseparate fragmenty hello hello poprzedniego wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="37440-255">Use `let` tooseparate out hello parts of hello previous expression.</span></span> <span data-ttu-id="37440-256">wyniki Hello uległy zmianie:</span><span class="sxs-lookup"><span data-stu-id="37440-256">hello results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="37440-257">W kliencie Analytics hello nie umieszczaj puste wiersze między częściami hello hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="37440-257">In hello Analytics client, don't put blank lines between hello parts of hello query.</span></span> <span data-ttu-id="37440-258">Upewnij się, że tooexecute wszystkie.</span><span class="sxs-lookup"><span data-stu-id="37440-258">Make sure tooexecute all of it.</span></span>
>

<span data-ttu-id="37440-259">Użyj `toscalar` tooconvert tooa wartości komórki pojedynczej tabeli:</span><span class="sxs-lookup"><span data-stu-id="37440-259">Use `toscalar` tooconvert a single table cell tooa value:</span></span>

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a><span data-ttu-id="37440-260">Funkcje</span><span class="sxs-lookup"><span data-stu-id="37440-260">Functions</span></span>

<span data-ttu-id="37440-261">Użyj *Let* toodefine funkcji:</span><span class="sxs-lookup"><span data-stu-id="37440-261">Use *Let* toodefine a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="37440-262">Uzyskiwanie dostępu do obiektów zagnieżdżonych</span><span class="sxs-lookup"><span data-stu-id="37440-262">Accessing nested objects</span></span>
<span data-ttu-id="37440-263">Zagnieżdżone obiekty są łatwo dostępne.</span><span class="sxs-lookup"><span data-stu-id="37440-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="37440-264">Na przykład w strumieniu wyjątki hello można wyświetlić obiekty strukturalne następująco:</span><span class="sxs-lookup"><span data-stu-id="37440-264">For example, in hello exceptions stream you can see structured objects like this:</span></span>

![wynik](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="37440-266">Można jej spłaszczenia, wybierając hello właściwości, które chcesz:</span><span class="sxs-lookup"><span data-stu-id="37440-266">You can flatten it by choosing hello properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="37440-267">Należy pamiętać, że należy toocast hello wynik toohello odpowiedniego typu.</span><span class="sxs-lookup"><span data-stu-id="37440-267">Note that you need toocast hello result toohello appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="37440-268">Właściwości niestandardowe i pomiarów</span><span class="sxs-lookup"><span data-stu-id="37440-268">Custom properties and measurements</span></span>
<span data-ttu-id="37440-269">Jeśli aplikacja łączy [niestandardowych wymiarów (właściwości) i niestandardowych miar](app-insights-api-custom-events-metrics.md#properties) tooevents, a następnie użytkownik będzie widział je w hello `customDimensions` i `customMeasurements` obiektów.</span><span class="sxs-lookup"><span data-stu-id="37440-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) tooevents, then you will see them in hello `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="37440-270">Na przykład, jeśli aplikacja zawiera:</span><span class="sxs-lookup"><span data-stu-id="37440-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="37440-271">tooextract te wartości w module analiz:</span><span class="sxs-lookup"><span data-stu-id="37440-271">tooextract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

<span data-ttu-id="37440-272">tooverify czy niestandardowych wymiarów jest określonego typu:</span><span class="sxs-lookup"><span data-stu-id="37440-272">tooverify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="37440-273">Pulpity nawigacyjne</span><span class="sxs-lookup"><span data-stu-id="37440-273">Dashboards</span></span>
<span data-ttu-id="37440-274">Pulpit nawigacyjny tooa wyniki w kolejności toobring można przypiąć ze sobą wszystkich najważniejszych wykresów i tabel.</span><span class="sxs-lookup"><span data-stu-id="37440-274">You can pin your results tooa dashboard in order toobring together all your most important charts and tables.</span></span>

* <span data-ttu-id="37440-275">[Azure udostępnionego pulpitu nawigacyjnego](app-insights-dashboards.md#share-dashboards): kliknij ikonę pinezki hello.</span><span class="sxs-lookup"><span data-stu-id="37440-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click hello pin icon.</span></span> <span data-ttu-id="37440-276">Zanim to zrobisz, musisz mieć udostępnionego pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="37440-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="37440-277">W portalu Azure hello otworzyć lub utworzyć pulpit nawigacyjny, a następnie kliknij przycisk Udostępnij.</span><span class="sxs-lookup"><span data-stu-id="37440-277">In hello Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="37440-278">[Pulpit nawigacyjny programu Power BI](app-insights-export-power-bi.md): kliknij przycisk Eksportuj, Power BI zapytania.</span><span class="sxs-lookup"><span data-stu-id="37440-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="37440-279">Zaletą to alternatywne jest, że można wyświetlić zapytania równolegle z innymi wyniki pochodzące z różnorodnych źródeł.</span><span class="sxs-lookup"><span data-stu-id="37440-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="37440-280">Łączenie z importowanych danych</span><span class="sxs-lookup"><span data-stu-id="37440-280">Combine with imported data</span></span>

<span data-ttu-id="37440-281">Raporty analizy wygląda świetnie na pulpicie nawigacyjnym hello, ale czasami trzeba tootranslate hello danych tooa więcej o wysokim strawności formularza.</span><span class="sxs-lookup"><span data-stu-id="37440-281">Analytics reports look great on hello dashboard, but sometimes you want tootranslate hello data tooa more digestible form.</span></span> <span data-ttu-id="37440-282">Na przykład załóżmy, że uwierzytelnieni użytkownicy są identyfikowane w telemetrii hello jako alias.</span><span class="sxs-lookup"><span data-stu-id="37440-282">For example, suppose your authenticated users are identified in hello telemetry by an alias.</span></span> <span data-ttu-id="37440-283">Chcesz tooshow ich rzeczywistym nazwy w wynikach.</span><span class="sxs-lookup"><span data-stu-id="37440-283">You'd like tooshow their real names in your results.</span></span> <span data-ttu-id="37440-284">toodo, potrzebujesz pliku CSV, który mapuje hello aliasy toohello rzeczywistej nazwy.</span><span class="sxs-lookup"><span data-stu-id="37440-284">toodo this, you need a CSV file that maps from hello aliases toohello real names.</span></span>

<span data-ttu-id="37440-285">Możesz zaimportować plik danych i używać go tak samo jak tabele standardowe hello (żądań, wyjątków i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="37440-285">You can import a data file and use it just like any of hello standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="37440-286">Zapytanie ją samodzielnie albo przyłączenie jej z innych tabel.</span><span class="sxs-lookup"><span data-stu-id="37440-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="37440-287">Na przykład, jeśli tabela o nazwie usermap i zawiera kolumn `realName` i `userId`, wówczas można użyć tootranslate hello `user_AuthenticatedId` w dane telemetryczne żądania hello:</span><span class="sxs-lookup"><span data-stu-id="37440-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it tootranslate hello `user_AuthenticatedId` field in hello request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="37440-288">tooimport tabelę, w bloku schematu hello, w obszarze **inne źródła danych**, wykonaj hello instrukcje tooadd nowe źródło danych, przekazując przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="37440-288">tooimport a table, in hello Schema blade, under **Other Data Sources**, follow hello instructions tooadd a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="37440-289">Następnie można użyć tej definicji tooupload tabel.</span><span class="sxs-lookup"><span data-stu-id="37440-289">Then you can use this definition tooupload tables.</span></span>

<span data-ttu-id="37440-290">Funkcja importowania Hello jest obecnie w przeglądzie, więc początkowo zobaczysz link "Skontaktuj się z nami" w obszarze "Innych źródeł danych."</span><span class="sxs-lookup"><span data-stu-id="37440-290">hello import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="37440-291">Użyj tego toosign toohello program w wersji zapoznawczej, a łącze hello następnie zostaną zastąpione przycisk "Dodaj nowe źródło danych".</span><span class="sxs-lookup"><span data-stu-id="37440-291">Use this toosign up toohello preview program, and hello link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="37440-292">Tabele</span><span class="sxs-lookup"><span data-stu-id="37440-292">Tables</span></span>
<span data-ttu-id="37440-293">strumień Hello telemetrii otrzymywanych z aplikacji jest dostępna za pośrednictwem kilku tabel.</span><span class="sxs-lookup"><span data-stu-id="37440-293">hello stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="37440-294">Schemat Hello właściwości dostępnych dla każdej tabeli jest widoczny po lewej stronie powitania hello okna.</span><span class="sxs-lookup"><span data-stu-id="37440-294">hello schema of properties available for each table is visible at hello left of hello window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="37440-295">Tabela żądań</span><span class="sxs-lookup"><span data-stu-id="37440-295">Requests table</span></span>
<span data-ttu-id="37440-296">Liczba żądań HTTP tooyour aplikacji sieci web i segmentów wg nazwy strony:</span><span class="sxs-lookup"><span data-stu-id="37440-296">Count HTTP requests tooyour web app and segment by page name:</span></span>

![Liczba żądań segmentem według nazwy](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="37440-298">Znajdź żądania hello, które nie są najczęściej:</span><span class="sxs-lookup"><span data-stu-id="37440-298">Find hello requests that fail most:</span></span>

![Liczba żądań segmentem według nazwy](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="37440-300">Tabela zdarzeń niestandardowych</span><span class="sxs-lookup"><span data-stu-id="37440-300">Custom events table</span></span>
<span data-ttu-id="37440-301">Jeśli używasz [funkcji TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend własne zdarzenia, będzie można je odczytać z tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="37440-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend your own events, you can read them from this table.</span></span>

<span data-ttu-id="37440-302">Spójrzmy na przykład gdy kodu aplikacji zawiera następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="37440-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="37440-303">Częstotliwość hello wyświetlania tych zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="37440-303">Display hello frequency of these events:</span></span>

![Częstotliwość wyświetlania zdarzeń niestandardowych](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="37440-305">Wyodrębnij miar i wymiary hello zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="37440-305">Extract measurements and dimensions from hello events:</span></span>

![Częstotliwość wyświetlania zdarzeń niestandardowych](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="37440-307">Metryki niestandardowe tabeli</span><span class="sxs-lookup"><span data-stu-id="37440-307">Custom metrics table</span></span>
<span data-ttu-id="37440-308">Jeśli używasz [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend własne wartości metryki znajdziesz wyniki w hello **customMetrics** strumienia.</span><span class="sxs-lookup"><span data-stu-id="37440-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend your own metric values, you’ll find its results in hello **customMetrics** stream.</span></span> <span data-ttu-id="37440-309">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="37440-309">For example:</span></span>  

![Metryki niestandardowe w module analiz usługi Application Insights](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="37440-311">W [Eksploratora metryk](app-insights-metrics-explorer.md), wszystkich miar niestandardowych dołączonych tooany typ telemetrii występować razem w bloku metryki hello wraz z metryki wysyłane przy użyciu `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="37440-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached tooany type of telemetry appear together in hello metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="37440-312">W module analiz, miary niestandardowe są nadal, ale dołączyć toowhichever typ telemetrii były przenoszone na — zdarzenia lub żądania i tak dalej — gdy metryki wysyłane przez TrackMetric pojawiają się w ich własnych strumienia.</span><span class="sxs-lookup"><span data-stu-id="37440-312">But in Analytics, custom measurements are still attached toowhichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="37440-313">Tabela liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="37440-313">Performance counters table</span></span>
<span data-ttu-id="37440-314">[Liczniki wydajności](app-insights-performance-counters.md) przedstawiają podstawowego systemu metryki dla aplikacji, na przykład procesora CPU, pamięci i wykorzystanie sieci.</span><span class="sxs-lookup"><span data-stu-id="37440-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="37440-315">Można skonfigurować hello SDK toosend dodatkowych liczników, w tym własne niestandardowe liczniki.</span><span class="sxs-lookup"><span data-stu-id="37440-315">You can configure hello SDK toosend additional counters, including your own custom counters.</span></span>

<span data-ttu-id="37440-316">Witaj **liczniki wydajności** schemat przedstawia hello `category`, `counter` nazwa, i `instance` nazwę każdego licznika wydajności.</span><span class="sxs-lookup"><span data-stu-id="37440-316">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="37440-317">Nazwy wystąpień liczników są tylko odpowiednie toosome liczniki wydajności i zwykle wskazują, że nazwa hello liczby hello procesu toowhich hello odnosi się.</span><span class="sxs-lookup"><span data-stu-id="37440-317">Counter instance names are only applicable toosome performance counters, and typically indicate hello name of hello process toowhich hello count relates.</span></span> <span data-ttu-id="37440-318">W danych telemetrycznych powitania dla każdej aplikacji zostanie wyświetlony tylko hello liczniki dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="37440-318">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="37440-319">Na przykład toosee jakie liczniki są dostępne:</span><span class="sxs-lookup"><span data-stu-id="37440-319">For example, toosee what counters are available:</span></span>

![Liczniki wydajności w module analiz usługi Application Insights](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="37440-321">tooget wykresu dostępnej pamięci na powitania wybrany okres:</span><span class="sxs-lookup"><span data-stu-id="37440-321">tooget a chart of available memory over hello selected period:</span></span>

![Timechart pamięci w module analiz usługi Application Insights](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="37440-323">Inne telemetrii, takich jak **liczniki wydajności** również zawiera kolumnę `cloud_RoleInstance` wskazujące hello tożsamość hello komputer hosta, na którym jest uruchomiona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="37440-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host machine on which your app is running.</span></span> <span data-ttu-id="37440-324">Na przykład toocompare hello wydajności aplikacji na różnych komputerach hello:</span><span class="sxs-lookup"><span data-stu-id="37440-324">For example, toocompare hello performance of your app on hello different machines:</span></span>

![Wydajność segmentowanych przez wystąpienie roli w usłudze Application Insights analityka](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="37440-326">Tabeli wyjątków</span><span class="sxs-lookup"><span data-stu-id="37440-326">Exceptions table</span></span>
<span data-ttu-id="37440-327">[Wyjątki zgłoszone przez aplikację](app-insights-asp-net-exceptions.md) są dostępne w tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="37440-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="37440-328">toofind hello żądania HTTP, która aplikacja była obsługa podczas został zgłoszony wyjątek hello, Dołącz do operation_Id:</span><span class="sxs-lookup"><span data-stu-id="37440-328">toofind hello HTTP request that your app was handling when hello exception was raised, join on operation_Id:</span></span>

![Dołącz do wyjątków z żądaniami operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="37440-330">Tabela chronometrażu przeglądarki</span><span class="sxs-lookup"><span data-stu-id="37440-330">Browser timings table</span></span>
<span data-ttu-id="37440-331">`browserTimings`przedstawia dane ładowania stron zebrane w przeglądarce użytkownika.</span><span class="sxs-lookup"><span data-stu-id="37440-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="37440-332">[Konfigurowanie aplikacji dla telemetrii po stronie klienta](app-insights-javascript.md) w celu toosee tych metryk.</span><span class="sxs-lookup"><span data-stu-id="37440-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order toosee these metrics.</span></span>

<span data-ttu-id="37440-333">zawiera schemat Hello [metryki wskazujący hello długości różne etapy procesu ładowania strony hello](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="37440-333">hello schema includes [metrics indicating hello lengths of different stages of hello page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="37440-334">(Nie wskazują one hello długość czasu, który użytkownicy odczytu strony.)</span><span class="sxs-lookup"><span data-stu-id="37440-334">(They don’t indicate hello length of time your users read a page.)</span></span>  

<span data-ttu-id="37440-335">Pokaż popularities hello z innej strony i załadować razy dla każdej strony:</span><span class="sxs-lookup"><span data-stu-id="37440-335">Show hello popularities of different pages, and load times for each page:</span></span>

![Czas ładowania strony w module analiz](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="37440-337">W tabeli wyników dostępność</span><span class="sxs-lookup"><span data-stu-id="37440-337">Availability results table</span></span>
<span data-ttu-id="37440-338">`availabilityResults`Pokazuje hello wyniki z [testów sieci web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="37440-338">`availabilityResults` shows hello results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="37440-339">Każdy Uruchom testy z każdej lokalizacji testu jest zgłaszana oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="37440-339">Each run of your tests from each test location is reported separately.</span></span>

![Czas ładowania strony w module analiz](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="37440-341">Tabela zależności</span><span class="sxs-lookup"><span data-stu-id="37440-341">Dependencies table</span></span>
<span data-ttu-id="37440-342">Wyniki wywołania zawiera czy aplikacji sprawia, że toodatabases i interfejsów API REST i inne wywołuje tooTrackDependency().</span><span class="sxs-lookup"><span data-stu-id="37440-342">Contains results of calls that your app makes toodatabases and REST APIs, and other calls tooTrackDependency().</span></span> <span data-ttu-id="37440-343">Zawiera również wywołania AJAX z hello przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="37440-343">Also includes AJAX calls made from hello browser.</span></span>

<span data-ttu-id="37440-344">Wywołania AJAX w przeglądarce hello:</span><span class="sxs-lookup"><span data-stu-id="37440-344">AJAX calls from hello browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="37440-345">Wywołania zależności z powitania serwera:</span><span class="sxs-lookup"><span data-stu-id="37440-345">Dependency calls from hello server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="37440-346">Zawsze pokazuj wyniki zależności po stronie serwera `success==False` Jeśli hello Application Insights Agent nie jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="37440-346">Server-side dependency results always show `success==False` if hello Application Insights Agent is not installed.</span></span> <span data-ttu-id="37440-347">Jednak hello innych danych są poprawne.</span><span class="sxs-lookup"><span data-stu-id="37440-347">However, hello other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="37440-348">Tabela danych śledzenia</span><span class="sxs-lookup"><span data-stu-id="37440-348">Traces table</span></span>
<span data-ttu-id="37440-349">Zawiera dane telemetryczne hello wysyłane przez aplikację przy użyciu TrackTrace(), lub [innych platform rejestrowania](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="37440-349">Contains hello telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="37440-350">Połączenia wideo</span><span class="sxs-lookup"><span data-stu-id="37440-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="37440-351">Zaawansowane zapytania:</span><span class="sxs-lookup"><span data-stu-id="37440-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="37440-352">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="37440-352">Next steps</span></span>
* [<span data-ttu-id="37440-353">Dokumentacja języka analityka</span><span class="sxs-lookup"><span data-stu-id="37440-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="37440-354">[Ściągawka SQL użytkowników](https://aka.ms/sql-analytics) tłumaczy hello idioms najczęściej.</span><span class="sxs-lookup"><span data-stu-id="37440-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates hello most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
