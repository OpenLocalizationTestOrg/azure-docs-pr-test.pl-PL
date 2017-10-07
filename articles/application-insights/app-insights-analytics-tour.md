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
# <a name="a-tour-of-analytics-in-application-insights"></a>Samouczek analizy w usłudze Application Insights
[Analiza](app-insights-analytics.md) to funkcja wyszukiwania zaawansowanego hello [usługi Application Insights](app-insights-overview.md). Te strony opisano język zapytań usługi Analiza dzienników.

* **[Obejrzyj klip wideo wprowadzenia hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Przetestuj Analytics na naszych danych symulowane](https://analytics.applicationinsights.io/demo)**  aplikacji nie jest jeszcze wysyłania danych tooApplication szczegółowych informacji.
* **[Ściągawka SQL użytkowników](https://aka.ms/sql-analytics)**  tłumaczy hello idioms najczęściej.

Spójrzmy przechodzenia przez tooget niektórych podstawowych zapytań, uruchamiany.

## <a name="connect-tooyour-application-insights-data"></a>Połącz dane usługi Application Insights tooyour
Otwórz Analytics z aplikacji [bloku omówienie](app-insights-dashboards.md) w usłudze Application Insights:

![Otwórz portal.azure.com otworzyć zasobu usługi Application Insights, a następnie kliknij przycisk Analytics.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a>[Podejmij](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): Pokaż n wierszy
Punkty danych, którzy logują się operacji użytkownika (zwykle żądania HTTP odebrane przez aplikację sieci web) są przechowywane w tabeli o nazwie `requests`. Każdy wiersz jest punkt danych telemetrii otrzymanych od hello zestaw SDK usługi Application Insights w aplikacji.

Zacznijmy od badanie kilka przykładowych wiersze tabeli hello:

![wyniki](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> Gdzieś umieść kursor hello w instrukcji hello przed kliknięciem przycisku Przejdź. Można podzielić instrukcję przez więcej niż jeden wiersz, ale nie należy umieszczać pustych wierszy w instrukcji. Puste wiersze są tookeep wygodny sposób kilku oddzielnych zapytania w oknie hello.
>
>

Wybierz kolumny, przeciągnij je Grupuj według kolumn i filtrowania:

![Kliknij kolumnę zaznaczenia w prawym górnym rogu wyników](./media/app-insights-analytics-tour/030.png)

Rozwiń żadnych szczegółów elementu toosee hello:

![Wybierz tabelę i użyj kolumn skonfigurować](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> Kliknij nagłówek hello dostępnych w przeglądarce sieci web hello wyników hello toore kolejność kolumn. Należy jednak pamiętać, że dla zestawu wyników dużych hello liczba wierszy pobrany toohello przeglądarki jest ograniczona. W ten sposób sortowania nie zawsze pokazuj hello rzeczywiste najwyższy lub najniższy elementów. elementy toosort niezawodnie, użyj hello `top` lub `sort` operatora.
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a>[TOP](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) i [sortowania](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)
`take`jest przydatne tooget próbkę szybkie wyniku, ale zawiera wiersze z tabeli hello w losowej kolejności. Użyj tooget uporządkowanej widoku `top` (na przykład) lub `sort` (za pośrednictwem hello całej tabeli).

Pokaż hello pierwsze n wierszy, uporządkowanych według określonej kolumny:

```AIQL

    requests | top 10 by timestamp desc
```

* *Składnia:* większość operatorów mieć — słowo kluczowe parametrów, takich jak `by`.
* `desc`= w kolejności malejącej `asc` = rosnąca.

![](./media/app-insights-analytics-tour/260.png)

`top...`więcej możliwości wydajności z informacją o tym `sort ... | take...`. Firma Microsoft może mieć zapisane:

```AIQL

    requests | sort by timestamp desc | take 10
```

Witaj nastąpiłoby hello takie same, ale może działać nieco wolniej. (Można również napisać `order`, który jest aliasem `sort`.)

Hello nagłówków kolumn w widoku tabeli hello może być również używane toosort hello wyników na ekranie powitania. Oczywiście jeśli był używany, ale `take` lub `top` tooretrieve tylko część tabeli, będzie tylko zmienić kolejność hello rekordów została pobrana.

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a>[Gdzie](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtrowanie warunek

Zobaczmy, po prostu żądań, które zwróciło kod określonego wyniku:

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

Witaj `where` operator przyjmuje wyrażenie logiczne. Poniżej przedstawiono niektóre najważniejszych o nich:

* `and`, `or`: Operatory logiczne
* `==`, `<>`, `!=` : równa i nie ma wartości
* `=~`, `!~` : ciąg bez uwzględniania wielkości liter równy i różne. Istnieje wiele więcej operatorów porównywania ciągów.

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a>Pobieranie hello odpowiedniego typu.
Znajdź żądania nie powiodło się:

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a>Time

Domyślnie zapytania są ograniczone toohello ostatnich 24 godzin. Można jednak zmienić ten zakres:

![](./media/app-insights-analytics-tour/change-time-range.png)

Zastąpienie zakres czasu hello pisząc każde zapytanie operacji uwzględniającą `timestamp` w klauzuli where. Na przykład:

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

Funkcja zakres czasu Hello jest równoważne tooa 'where' klauzuli wstawiane po każdej informację o jedną z tabel źródłowych hello.

`ago(3d)`oznacza, że "trzy dni temu". Inne jednostki czasu obejmują godzin (`2h`, `2.5h`), minut (`25m`), a sekund (`10s`).

Inne przykłady:

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

[Daty i godziny odwołanie](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a>[Projekt](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): Wybierz, Zmień nazwę, a kolumny obliczeniowe
Użyj [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick się tylko kolumny hello chcesz:

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

Można również zmienić nazwy kolumny i zdefiniować nowe:

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

* Nazwy kolumny może zawierać spacje lub symbole, jeśli są one oddzielona podobnie do następującej: `['...']` lub`["..."]`
* `%`hello jest zwykle operatora modulo.
* `1d`(to cyfrę, jedną, a następnie miał ") jest wartość typu timespan literału oznacza jeden dzień. Poniżej przedstawiono niektóre więcej literały timespan: `12h`, `30m`, `10s`, `0.01s`.
* `floor`(alias `bin`) zaokrągla wartość w dół toohello najbliższej wielokrotności wartości podstawowej hello, musisz podać. Dlatego `floor(aTime, 1s)` zaokrągla czasu dół toohello najbliższej sekundy.

Wyrażenia mogą zawierać wszystkie operatory zwykle hello (`+`, `-`,...), a istnieje szereg przydatne funkcje.

## <a name="extend"></a>Rozszerzanie
Po prostu toohello kolumn tooadd istniejące grupy, należy użyć [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

Przy użyciu [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) mniej szczegółowe niż [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) Jeśli chcesz tookeep hello wszystkie istniejące kolumny.

### <a name="convert-toolocal-time"></a>Konwertuj toolocal czasu

Sygnatury czasowe są zawsze w formacie UTC. Dlatego jeśli używasz wybrzeże Pacyfiku nam hello jest zima, może Cię zainteresować to:

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a>[Podsumuj](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): agregacji grupy wierszy
`Summarize`zastosowanie określonej *funkcji agregacji* za pośrednictwem grupy wierszy.

Na przykład czasie hello aplikacji sieci web żądania tooa toorespond jest zgłaszany w polu hello `duration`. Zobaczmy hello odpowiedzi średni czas żądania tooall:

![](./media/app-insights-analytics-tour/410.png)

Lub wynik hello można oddzielić do żądań różne nazwy elementu:

![](./media/app-insights-analytics-tour/420.png)

`Summarize`zbiera hello punktów danych w strumieniu hello w grupach, dla których hello `by` klauzuli ocenia jednakowo. Każda wartość w hello `by` wyrażenie - nazwy operacji w hello powyżej przykład — powoduje wiersz w tabeli wyników hello.

Lub firma Microsoft może grupowania wyników według pora dnia:

![](./media/app-insights-analytics-tour/430.png)

Zwróć uwagę, jak firma Microsoft korzysta z hello `bin` — funkcja (alias `floor`). Jeśli będziemy używać `by timestamp`, co wejściowych wiersza pojawiłyby w niewielkim grupy. Dla dowolnego ciągłego skalarną podobnego razy lub numerów mamy toobreak hello ciągły zakres na zarządzaniu liczbę wartości dyskretnych. `bin`— co jest po prostu hello znanych zaokrąglania rozwijanej `floor` funkcji — jest hello Najprostszym sposobem toodo który.

Możemy użyć hello tego samego zakresy tooreduce technika ciągów:

![](./media/app-insights-analytics-tour/440.png)

Należy zauważyć, że można użyć `name=` tooset hello nazwy kolumny wynik, w wyrażeniach agregacji hello lub hello przez klauzuli.

## <a name="counting-sampled-data"></a>Zliczanie próbce danych
`sum(itemCount)`jest hello zalecane agregacji toocount zdarzenia. W wielu przypadkach wartość elementu itemCount == 1, dlatego funkcja powitania po prostu liczy w górę hello liczbę wierszy w grupie hello. Ale jeśli [próbkowania](app-insights-sampling.md) jest operacji, tylko część oryginalnego zdarzenia hello są przechowywane jako punkty danych w usłudze Application Insights, aby dla każdego punktu danych, zostanie wyświetlony, `itemCount` zdarzenia.

Na przykład, jeśli próbkowania odrzuca 75% hello oryginalnego zdarzenia, a następnie wartość elementu itemCount == 4 w rekordach hello zachowane - oznacza to, dla każdego rekordu zachowanych, były cztery oryginalnego rekordy.

Adaptacyjną próbkowania powoduje, że wartość elementu itemCount toobe wyższe w okresach, gdy aplikacja jest używana często.

W związku z tym sumowania wartość elementu itemCount zapewnia dobre oszacowanie hello oryginalna liczba zdarzeń.

![](./media/app-insights-analytics-tour/510.png)

Istnieje również `count()` agregacji (i operacji liczby), w przypadku których na pewno chcesz toocount hello liczbę wierszy w grupie.

Istnieje szereg [funkcje agregacji](https://docs.loganalytics.io/learn/tutorials/aggregations.html).

## <a name="charting-hello-results"></a>Wykresy wyników hello
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

Domyślnie wyniki są wyświetlane jako tabelę:

![](./media/app-insights-analytics-tour/225.png)

Możemy lepiej niż hello tabeli widoku. Przyjrzyjmy się hello wyniki w widoku wykresu hello z opcją pionowy pasek hello:

![Kliknij wykres, a następnie wybrać wykres słupkowy pionowy i przypisać x i y osi](./media/app-insights-analytics-tour/230.png)

Zwróć uwagę, że chociaż firma Microsoft nie sortowanie wyników hello czasu (jak widać w wyświetlanej tabeli hello), wyświetlania wykresu hello zawsze zawiera dat i godzin w odpowiedniej kolejności.


## <a name="timecharts"></a>Timecharts
Pokaż liczbę zdarzeń są każdej godziny:

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

Wybierz opcję wyświetlania wykresu hello:

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a>Wiele serii
Wiele wyrażeń w hello `summarize` klauzuli tworzy wiele kolumn.

Wiele wyrażeń w hello `by` klauzuli tworzy wiele wierszy, po jednej dla każdej kombinacji wartości.

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabela żądań przez godzinę i lokalizację](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a>Segment wykresu wielowymiarowa
Jeśli wykresu tabeli zawierającej kolumny typu string i kolumny liczbowej ciąg hello może być używane toosplit hello dane liczbowe w oddzielnych serii punktów. Jeśli istnieje więcej niż jednej kolumny typu string, toouse kolumny, które można wybrać jako dyskryminatora hello.

![Segment wykres analizy](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a>Odbijanie szybkości

Konwertuj toouse ciąg logiczna tooa go jako dyskryminatora:

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

### <a name="display-multiple-metrics"></a>Wyświetlania wielu metryk
Jeśli wykresu tabeli, która ma więcej niż jednej kolumny liczbowe, w znaczników dodaniu toohello czasu, można wyświetlić dowolną kombinację.

![Segment wykres analizy](./media/app-insights-analytics-tour/110.png)

Musisz wybrać **nie podziału** zanim będzie można wybrać wiele kolumn liczbowych. Nie można podzielić według kolumny ciągu na powitania sam czas jako wyświetlanie więcej niż jednej kolumny liczbowej.

## <a name="daily-average-cycle"></a>Cykl średni dzienny
Sposób użycia różne za pośrednictwem hello typowego dnia?

Liczba żądań przez czas hello modulo jeden dzień, binned na godziny:

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
> Zwróć uwagę, że obecnie mamy tooconvert czas trwania toodatetimes w kolejności toodisplay wykres liniowy.
>
>

## <a name="compare-multiple-daily-series"></a>Porównywanie wielu serii codziennie
Jak czy użycia różnią się od wraz z upływem czasu hello dnia w różnych krajach?

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

## <a name="plot-a-distribution"></a>Wykreślenia dystrybucji
Ile sesji są dostępne różne długości?

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

ostatni wiersz Hello jest toodatetime tooconvert wymagane. Obecnie hello x osi wykresu jest wyświetlana jako skalarnej tylko wtedy, gdy jest wartość datetime.

Witaj `where` klauzuli wyklucza jednorazowej sesji (sessionDuration == 0) i zestawy hello długość hello osi x.

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[Percentylu](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
Jakie zakresów czasu trwania obejmują różne wartości procentowe sesji?

Użyj hello powyżej kwerendy, ale zastępuje hello ostatni wiersz:

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

Również usunęliśmy hello górny limit hello, w którym klauzula w kolejności tooget poprawić rysunki w tym wszystkie sesje z więcej niż jedno żądanie:

![wynik](./media/app-insights-analytics-tour/180.png)

Z którego możemy stwierdzić, że:

* 5% sesji ma czasu trwania z więcej niż trzy minuty 34s;
* 50% sesji ostatni 36 minut;
* 5% sesji ostatnie więcej niż 7 dni

tooget podział osobne dla każdego kraju mamy właśnie toobring hello client_CountryOrRegion kolumny z osobna za pomocą obu Podsumuj operatory:

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

## <a name="join"></a>Join
Mamy dostęp tooseveral tabele wraz ze żądań i wyjątki.

toofind hello wyjątki powiązane tooa żądania zwrócił odpowiedź awarii, firma Microsoft może dołączyć do tabel hello na `session_Id`:

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


Jest dobrym rozwiązaniem toouse `project` tooselect hello tylko kolumny potrzebujemy przed wykonaniem hello sprzężenia.
W hello tego samego klauzule możemy zmienić nazwy kolumny znaczników czasu hello.

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a>[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): przypisano zmienną tooa wyników

Użyj `let` tooseparate fragmenty hello hello poprzedniego wyrażenia. wyniki Hello uległy zmianie:

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> W kliencie Analytics hello nie umieszczaj puste wiersze między częściami hello hello zapytania. Upewnij się, że tooexecute wszystkie.
>

Użyj `toscalar` tooconvert tooa wartości komórki pojedynczej tabeli:

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


### <a name="functions"></a>Funkcje

Użyj *Let* toodefine funkcji:

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a>Uzyskiwanie dostępu do obiektów zagnieżdżonych
Zagnieżdżone obiekty są łatwo dostępne. Na przykład w strumieniu wyjątki hello można wyświetlić obiekty strukturalne następująco:

![wynik](./media/app-insights-analytics-tour/520.png)

Można jej spłaszczenia, wybierając hello właściwości, które chcesz:

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

Należy pamiętać, że należy toocast hello wynik toohello odpowiedniego typu.


## <a name="custom-properties-and-measurements"></a>Właściwości niestandardowe i pomiarów
Jeśli aplikacja łączy [niestandardowych wymiarów (właściwości) i niestandardowych miar](app-insights-api-custom-events-metrics.md#properties) tooevents, a następnie użytkownik będzie widział je w hello `customDimensions` i `customMeasurements` obiektów.

Na przykład, jeśli aplikacja zawiera:

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

tooextract te wartości w module analiz:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

tooverify czy niestandardowych wymiarów jest określonego typu:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a>Pulpity nawigacyjne
Pulpit nawigacyjny tooa wyniki w kolejności toobring można przypiąć ze sobą wszystkich najważniejszych wykresów i tabel.

* [Azure udostępnionego pulpitu nawigacyjnego](app-insights-dashboards.md#share-dashboards): kliknij ikonę pinezki hello. Zanim to zrobisz, musisz mieć udostępnionego pulpitu nawigacyjnego. W portalu Azure hello otworzyć lub utworzyć pulpit nawigacyjny, a następnie kliknij przycisk Udostępnij.
* [Pulpit nawigacyjny programu Power BI](app-insights-export-power-bi.md): kliknij przycisk Eksportuj, Power BI zapytania. Zaletą to alternatywne jest, że można wyświetlić zapytania równolegle z innymi wyniki pochodzące z różnorodnych źródeł.

## <a name="combine-with-imported-data"></a>Łączenie z importowanych danych

Raporty analizy wygląda świetnie na pulpicie nawigacyjnym hello, ale czasami trzeba tootranslate hello danych tooa więcej o wysokim strawności formularza. Na przykład załóżmy, że uwierzytelnieni użytkownicy są identyfikowane w telemetrii hello jako alias. Chcesz tooshow ich rzeczywistym nazwy w wynikach. toodo, potrzebujesz pliku CSV, który mapuje hello aliasy toohello rzeczywistej nazwy.

Możesz zaimportować plik danych i używać go tak samo jak tabele standardowe hello (żądań, wyjątków i tak dalej). Zapytanie ją samodzielnie albo przyłączenie jej z innych tabel. Na przykład, jeśli tabela o nazwie usermap i zawiera kolumn `realName` i `userId`, wówczas można użyć tootranslate hello `user_AuthenticatedId` w dane telemetryczne żądania hello:

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

tooimport tabelę, w bloku schematu hello, w obszarze **inne źródła danych**, wykonaj hello instrukcje tooadd nowe źródło danych, przekazując przykładowych danych. Następnie można użyć tej definicji tooupload tabel.

Funkcja importowania Hello jest obecnie w przeglądzie, więc początkowo zobaczysz link "Skontaktuj się z nami" w obszarze "Innych źródeł danych." Użyj tego toosign toohello program w wersji zapoznawczej, a łącze hello następnie zostaną zastąpione przycisk "Dodaj nowe źródło danych".


## <a name="tables"></a>Tabele
strumień Hello telemetrii otrzymywanych z aplikacji jest dostępna za pośrednictwem kilku tabel. Schemat Hello właściwości dostępnych dla każdej tabeli jest widoczny po lewej stronie powitania hello okna.

### <a name="requests-table"></a>Tabela żądań
Liczba żądań HTTP tooyour aplikacji sieci web i segmentów wg nazwy strony:

![Liczba żądań segmentem według nazwy](./media/app-insights-analytics-tour/analytics-count-requests.png)

Znajdź żądania hello, które nie są najczęściej:

![Liczba żądań segmentem według nazwy](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a>Tabela zdarzeń niestandardowych
Jeśli używasz [funkcji TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend własne zdarzenia, będzie można je odczytać z tej tabeli.

Spójrzmy na przykład gdy kodu aplikacji zawiera następujące wiersze:

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

Częstotliwość hello wyświetlania tych zdarzeń:

![Częstotliwość wyświetlania zdarzeń niestandardowych](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

Wyodrębnij miar i wymiary hello zdarzeń:

![Częstotliwość wyświetlania zdarzeń niestandardowych](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a>Metryki niestandardowe tabeli
Jeśli używasz [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend własne wartości metryki znajdziesz wyniki w hello **customMetrics** strumienia. Na przykład:  

![Metryki niestandardowe w module analiz usługi Application Insights](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> W [Eksploratora metryk](app-insights-metrics-explorer.md), wszystkich miar niestandardowych dołączonych tooany typ telemetrii występować razem w bloku metryki hello wraz z metryki wysyłane przy użyciu `TrackMetric()`. W module analiz, miary niestandardowe są nadal, ale dołączyć toowhichever typ telemetrii były przenoszone na — zdarzenia lub żądania i tak dalej — gdy metryki wysyłane przez TrackMetric pojawiają się w ich własnych strumienia.
>
>

### <a name="performance-counters-table"></a>Tabela liczniki wydajności
[Liczniki wydajności](app-insights-performance-counters.md) przedstawiają podstawowego systemu metryki dla aplikacji, na przykład procesora CPU, pamięci i wykorzystanie sieci. Można skonfigurować hello SDK toosend dodatkowych liczników, w tym własne niestandardowe liczniki.

Witaj **liczniki wydajności** schemat przedstawia hello `category`, `counter` nazwa, i `instance` nazwę każdego licznika wydajności. Nazwy wystąpień liczników są tylko odpowiednie toosome liczniki wydajności i zwykle wskazują, że nazwa hello liczby hello procesu toowhich hello odnosi się. W danych telemetrycznych powitania dla każdej aplikacji zostanie wyświetlony tylko hello liczniki dla tej aplikacji. Na przykład toosee jakie liczniki są dostępne:

![Liczniki wydajności w module analiz usługi Application Insights](./media/app-insights-analytics-tour/analytics-performance-counters.png)

tooget wykresu dostępnej pamięci na powitania wybrany okres:

![Timechart pamięci w module analiz usługi Application Insights](./media/app-insights-analytics-tour/analytics-available-memory.png)

Inne telemetrii, takich jak **liczniki wydajności** również zawiera kolumnę `cloud_RoleInstance` wskazujące hello tożsamość hello komputer hosta, na którym jest uruchomiona aplikacja. Na przykład toocompare hello wydajności aplikacji na różnych komputerach hello:

![Wydajność segmentowanych przez wystąpienie roli w usłudze Application Insights analityka](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a>Tabeli wyjątków
[Wyjątki zgłoszone przez aplikację](app-insights-asp-net-exceptions.md) są dostępne w tej tabeli.

toofind hello żądania HTTP, która aplikacja była obsługa podczas został zgłoszony wyjątek hello, Dołącz do operation_Id:

![Dołącz do wyjątków z żądaniami operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a>Tabela chronometrażu przeglądarki
`browserTimings`przedstawia dane ładowania stron zebrane w przeglądarce użytkownika.

[Konfigurowanie aplikacji dla telemetrii po stronie klienta](app-insights-javascript.md) w celu toosee tych metryk.

zawiera schemat Hello [metryki wskazujący hello długości różne etapy procesu ładowania strony hello](app-insights-javascript.md#page-load-performance). (Nie wskazują one hello długość czasu, który użytkownicy odczytu strony.)  

Pokaż popularities hello z innej strony i załadować razy dla każdej strony:

![Czas ładowania strony w module analiz](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a>W tabeli wyników dostępność
`availabilityResults`Pokazuje hello wyniki z [testów sieci web](app-insights-monitor-web-app-availability.md). Każdy Uruchom testy z każdej lokalizacji testu jest zgłaszana oddzielnie.

![Czas ładowania strony w module analiz](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a>Tabela zależności
Wyniki wywołania zawiera czy aplikacji sprawia, że toodatabases i interfejsów API REST i inne wywołuje tooTrackDependency(). Zawiera również wywołania AJAX z hello przeglądarki.

Wywołania AJAX w przeglądarce hello:

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

Wywołania zależności z powitania serwera:

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

Zawsze pokazuj wyniki zależności po stronie serwera `success==False` Jeśli hello Application Insights Agent nie jest zainstalowany. Jednak hello innych danych są poprawne.

### <a name="traces-table"></a>Tabela danych śledzenia
Zawiera dane telemetryczne hello wysyłane przez aplikację przy użyciu TrackTrace(), lub [innych platform rejestrowania](app-insights-asp-net-trace-logs.md).

## <a name="video"></a>Połączenia wideo 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

Zaawansowane zapytania:

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a>Następne kroki
* [Dokumentacja języka analityka](app-insights-analytics-reference.md)
* [Ściągawka SQL użytkowników](https://aka.ms/sql-analytics) tłumaczy hello idioms najczęściej.

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
