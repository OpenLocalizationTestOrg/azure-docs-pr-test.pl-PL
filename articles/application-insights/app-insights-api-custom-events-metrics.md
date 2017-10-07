---
title: "aaaApplication Insights interfejsu API dla niestandardowych zdarzeń i metryk | Dokumentacja firmy Microsoft"
description: "Wstaw kilku wierszy kodu w sposób użycia tootrack urządzenia lub aplikacji komputerowej, strony sieci Web lub usługi i diagnozowanie problemów."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a>Aplikacji interfejsu API Insights dla niestandardowych zdarzeń i metryk

Wstaw kilku wierszy kodu w Twojej aplikacji toofind się, co robią użytkownicy z nim lub toohelp diagnozowanie problemów. Może wysłać dane telemetryczne z aplikacji urządzenia i pulpitu, klientów w sieci web i serwerów sieci web. Użyj hello [Azure Application Insights](app-insights-overview.md) podstawowe interfejsu API telemetrii toosend niestandardowe zdarzenia i metryki i własnych wersji standard telemetrii. Ten interfejs API jest hello tego samego interfejsu API standardzie hello używanego przez moduły zbierające dane usługi Application Insights.

## <a name="api-summary"></a>Podsumowanie interfejsu API
Witaj interfejsu API jest jednolita na wszystkich platformach, oprócz kilku małe różnice.

| Metoda | Używany do |
| --- | --- |
| [`TrackPageView`](#page-views) |Stron, ekrany, bloków lub formularzy. |
| [`TrackEvent`](#trackevent) |Akcje użytkownika oraz inne zdarzenia. Wydajność zachowanie lub toomonitor używane tootrack użytkownika. |
| [`TrackMetric`](#trackmetric) |Wskaźników wydajności, takich jak długości kolejki nie powiązane zdarzenia toospecific. |
| [`TrackException`](#trackexception) |Wyjątki rejestrowania diagnostyki. Gdzie występują w relacji tooother zdarzeń i przejrzyj śladów stosu śledzenia. |
| [`TrackRequest`](#trackrequest) |Rejestrowanie hello częstotliwość i czas trwania żądania serwera do analizy wydajności. |
| [`TrackTrace`](#tracktrace) |Komunikaty dziennika diagnostycznego. Istnieje również możliwość przechwytywania dzienniki innych firm. |
| [`TrackDependency`](#trackdependency) |Czas trwania hello rejestrowania i częstotliwość wywołań tooexternal składników, które zależy od aplikacji. |

Możesz [dołączanie właściwości i metryki](#properties) toomost tych wywołań telemetrii.

## <a name="prep"></a>Przed rozpoczęciem
Jeśli to odwołanie nie ma jeszcze na zestaw SDK usługi Application Insights:

* Dodaj projekt tooyour zestaw SDK usługi Application Insights hello:

  * [Projektu programu ASP.NET](app-insights-asp-net.md)
  * [Projekt języka Java](app-insights-java-get-started.md)
  * [Język JavaScript w każdej strony sieci Web](app-insights-javascript.md) 
* W kodzie serwera sieci web lub urządzenia obejmują:

    *C#:*`using Microsoft.ApplicationInsights;`

    *Visual Basic:*`Imports Microsoft.ApplicationInsights`

    *Java:*`import com.microsoft.applicationinsights.TelemetryClient;`

## <a name="constructing-a-telemetryclient-instance"></a>Utworzenie wystąpienia TelemetryClient
Skonstruować wystąpienia `TelemetryClient` (z wyjątkiem w języku JavaScript, na stronach sieci Web):

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();

TelemetryClient jest wątkowo.

Zalecane jest użycie wystąpienia TelemetryClient dla każdego modułu aplikacji. Na przykład może mieć jedno wystąpienie TelemetryClient w Twojej przychodzących żądań HTTP sieci web usługi tooreport i drugą w zdarzeń klasy logiki biznesowej tooreport oprogramowania pośredniczącego. Można ustawić właściwości, takie jak `TelemetryClient.Context.User.Id` tootrack użytkowników i sesji, lub `TelemetryClient.Context.Device.Id` tooidentify hello maszyny. Te informacje są dołączone tooall zdarzenia, które hello wysyła wystąpienia.

## <a name="trackevent"></a>TrackEvent
W usłudze Application Insights *zdarzenie niestandardowe* jest punkt danych, które można wyświetlić w [Eksploratora metryk](app-insights-metrics-explorer.md) jako zagregowanej liczby, a następnie w [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md) jako poszczególnych wystąpień. (Nie jest powiązane tooMVC lub inne framework "zdarzenia.")

Wstaw `TrackEvent` Twojego toocount kod odwołuje się różne zdarzenia. Jak często użytkownicy wybrać określonej funkcji, jak często one celach określonego lub może być częstotliwość tworzenia poszczególnych typów błędów.

Na przykład w aplikacji gry, należy wysłać zdarzenie w przypadku użytkownik wins gry hello:

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a>Wyświetlanie zdarzeń w portalu Microsoft Azure hello
toosee liczbę zdarzeń, otwórz [Eksploratora metryk](app-insights-metrics-explorer.md) bloku, Dodaj nowy wykres i wybierz **zdarzenia**.  

![Liczba zdarzeń niestandardowych w temacie](./media/app-insights-api-custom-events-metrics/01-custom.png)

toocompare hello liczby różnych zdarzeń, Ustaw typ wykresu hello zbyt**siatki**i grupę o nazwie zdarzenia:

![Ustaw typ wykresu hello i grupowania](./media/app-insights-api-custom-events-metrics/07-grid.png)

Na siatce powitania kliknij zdarzenie nazwa toosee poszczególnych wystąpień tego zdarzenia. toosee bardziej szczegółowe - kliknij każde zdarzenie w hello listy.

![Drążenie wskroś hello zdarzenia](./media/app-insights-api-custom-events-metrics/03-instances.png)

toofocus na określonych zdarzeń w wyszukiwania lub Eksploratora metryk zestaw hello bloku filtru toohello zdarzeń nazw, które interesują Cię:

![Otwórz filtrów, rozwiń nazwę zdarzenia, a następnie wybierz co najmniej jedną wartość](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>Niestandardowe zdarzenia w module analiz

dane telemetryczne Hello jest dostępna w hello `customEvents` tabeli w [Application Insights Analytics](app-insights-analytics.md). Każdy wiersz reprezentuje wywołanie za`trackEvent(..)` w aplikacji. 

Jeśli [próbkowania](app-insights-sampling.md) jest używany w operacji, właściwości wartość elementu itemCount hello wskazuje wartość większą niż 1. Na przykład wartość elementu itemCount == 10 oznacza, że z tootrackEvent() 10 wywołania procesu pobierania próbek hello jedynie przesyłane, jeden z nich. tooget poprawne liczba zdarzeń niestandardowych, należy użyć w związku z tym kod wykorzystania, takich jak `customEvent | summarize sum(itemCount)`.


## <a name="trackmetric"></a>TrackMetric

Usługa Application Insights można wykresu metryk, które nie są dołączone tooparticular zdarzenia. Na przykład można monitorować długość kolejki w regularnych odstępach czasu. O metryki hello pojedynczych pomiarów mogą być przydatne, mniej niż hello zmian i trendów i wykresy tak statystyczne są przydatne.

Kolejność metryki toosend tooApplication Insights, można użyć hello `TrackMetric(..)` interfejsu API. Istnieją dwa sposoby toosend metryki: 

* Pojedyncza wartość. Za każdym razem, gdy miary są wykonywane w aplikacji, możesz wysłać hello odpowiadającej jej wartości tooApplication szczegółowych informacji. Załóżmy na przykład, że masz metrykę opisujące hello liczba elementów w kontenerze. W określonym czasie umieść trzy elementy do kontenera hello, a następnie usuń dwa elementy. W związku z tym spowodowałoby wywołanie `TrackMetric` dwa razy: najpierw przekazywanie wartości hello `3` , a następnie hello wartość `-2`. Usługa Application Insights przechowuje obie wartości w Twoim imieniu. 

* Agregacji. Podczas pracy z metryki, co pojedynczego pomiaru jest rzadko. Zamiast tego ważne jest podsumowanie co się stało w określonym przedziale czasu. Taki skrót jest nazywany _agregacji_. W hello powyżej przykładzie, jest hello agregacji sum metryki dla tego okresu `1` i hello liczba wartości metryki hello jest `2`. Korzystając z metody agregacji hello, można tylko wywołać `TrackMetric` raz w czasie okresu i wysyłania hello wartości zagregowanych. Jest to hello zalecane podejście, ponieważ mogą znacznie zmniejszyć koszt hello i wydajności nakładów pracy, wysyłając mniej danych punktów tooApplication Insights podczas nadal zbierania wszystkich odpowiednich informacji.

### <a name="examples"></a>Przykłady:

#### <a name="single-values"></a>Pojedynczych wartości

toosend pojedynczą wartość metryki:

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

*C#, Java*

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a>Agregowanie metryk

Przed wysłaniem do nich z aplikację, tooreduce przepustowości, kosztów i tooimprove wydajności zalecane jest tooaggregate metryki.
Oto przykład agregację kodu:

*C#*

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a>Metryki niestandardowe w Eksploratorze metryk

wyniki hello toosee, otwórz Eksploratora metryk i Dodaj nowy wykres. Edytuj hello wykresu tooshow Twojego metryki.

> [!NOTE]
> Twoje niestandardowa Metryka może potrwać kilka minut tooappear hello liście dostępne metryki.
>

![Dodawanie nowego wykresu lub wybierz wykres, a w obszarze niestandardowe, wybierz Twoje metryki](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>Metryki niestandardowe w module analiz

dane telemetryczne Hello jest dostępna w hello `customMetrics` tabeli w [Application Insights Analytics](app-insights-analytics.md). Każdy wiersz reprezentuje wywołanie za`trackMetric(..)` w aplikacji.
* `valueSum`-Jest suma hello hello pomiarów. tooget wartości średniej hello, dzielenie przez `valueCount`.
* `valueCount`-hello liczba pomiarów, które zostały zagregowane w to `trackMetric(..)` wywołania.

## <a name="page-views"></a>Liczba wyświetleń strony
W aplikacji lub strony sieci Web urządzenia po załadowaniu każdej ekranu lub strony, domyślnie jest wysyłane dane telemetryczne wyświetleń strony. Ale można zmienić tego tootrack wyświetleń strony w czasie dodatkowych lub innych. Na przykład w aplikacji, która zawiera tabulatory lub bloków, można tootrack strony zawsze, gdy użytkownik hello otwiera nowy blok.

![Obiektyw użycia w bloku — omówienie](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

Dane użytkownika i sesji są wysyłane jako właściwości wraz z wyświetleń strony, dlatego hello użytkownika i sesji wykresy pochodzić aktywności, po dane telemetryczne wyświetleń strony.

### <a name="custom-page-views"></a>Widoki niestandardowe strony
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


Jeśli masz kilka kart w różnych stron HTML, można określić hello adresu URL za:

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>Liczba wyświetleń strony chronometrażu
Domyślnie razy hello raportowane klientowi jako **czas ładowania strony widoku** są mierzone od, gdy przeglądarka hello wysyła żądanie hello, dopóki zdarzeń ładowania strony przeglądarki hello jest wywoływana.

Zamiast tego możesz:

* Ustaw jawne czasu trwania w hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) wywołania: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.
* Użyj wywołań chronometrażu widoku strony hello `startTrackPage` i `stopTrackPage`.

*JavaScript*

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

Przyciski ...

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

Witaj nazwy używanej jako pierwszy parametr hello kojarzy hello start i Zatrzymaj wywołania. Domyślnie nazwa toohello bieżącej strony.

Hello wynikowy ładowania strony okresów wyświetlana w Eksploratorze metryk pochodzą od interwału powitania między hello uruchamianie i zatrzymywanie wywołania. Jest zapasowej tooyou jakie interwał czasu rzeczywistego.

### <a name="page-telemetry-in-analytics"></a>Dane telemetryczne strony w module analiz

W [Analytics](app-insights-analytics.md) dwóch tabel wyświetlane dane z operacji przeglądarki:

* Witaj `pageViews` tabela zawiera dane o hello adresu URL i tytuł strony
* Witaj `browserTimings` tabeli zawiera dane dotyczące wydajności klienta, takich jak tooprocess czas poświęcony na powitania hello przychodzących danych.

toofind jak długo przeglądarki hello przyjmuje tooprocess różne strony:

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

popularities hello toodiscover różnych przeglądarek:

```
pageViews | summarize count() by client_Browser
```

Dołącz tooassociate strony widoki tooAJAX wywołania zależności:

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest
Serwer Hello SDK używa TrackRequest toolog HTTP żądania.

Możesz można także wywołać ją samodzielnie Chcąc toosimulate żądania w kontekście gdzie nie ma uruchomiony moduł usługi sieci web hello.

Jednak zalecane jest dane telemetryczne żądania toosend sposób gdzie żądania hello działa jako hello <a href="#operation-context">kontekstu operacji</a>.

## <a name="operation-context"></a>Operacja kontekstu
Elementy danych telemetrycznych można skojarzyć razem dołączając toothem identyfikatora typowych operacji Standardowy moduł żądania śledzenia Hello robi to wyjątków i inne zdarzenia, które są wysyłane podczas przetwarzania żądania HTTP. W [wyszukiwania](app-insights-diagnostic-search.md) i [Analytics](app-insights-analytics.md), można użyć hello identyfikator tooeasily Znajdź wszystkie zdarzenia związane z hello żądania.

Identyfikator hello tooset Najprostszym sposobem Hello jest tooset kontekstu operacji za pomocą tego wzorca:

*C#*

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

Wraz z ustawienie kontekstu operacji `StartOperation` tworzy element telemetrii hello typu, który określisz. Element wysyła dane telemetryczne hello podczas usuwania operacji hello lub jawnie wywołać `StopOperation`. Jeśli używasz `RequestTelemetry` jako typ danych telemetrycznych hello, jego długość ustawiono interwał toohello upłynął czasu rozpoczęcia i zakończenia.

Nie można zagnieżdżać kontekstów operacji. Jeśli istnieje już kontekstu operacji, a następnie jego identyfikator jest skojarzony z wszystkie elementy zawarte hello, w tym utworzone za pomocą elementu hello `StartOperation`.

W polu Wyszukaj hello operacji kontekst jest używane toocreate hello **elementy pokrewne** listy:

![Elementy pokrewne](./media/app-insights-api-custom-events-metrics/21.png)

Zobacz [aplikacji — szczegółowe informacje — niestandardowy operacji tracking.md] uzyskać więcej informacji o niestandardowych operacji śledzenia.

### <a name="requests-in-analytics"></a>Żądań w module analiz 

W [Application Insights Analytics](app-insights-analytics.md), żądań Pokaż w górę w hello `requests` tabeli.

Jeśli [próbkowania](app-insights-sampling.md) jest w operacji właściwości wartość elementu itemCount hello wyświetli wartość większą niż 1. Na przykład wartość elementu itemCount == 10 oznacza, że z tootrackRequest() 10 wywołania procesu pobierania próbek hello jedynie przesyłane, jeden z nich. tooget poprawną liczbę żądań i Średni czas trwania segmentowanych przez żądanie nazwy, takie jak użyć kodu:

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException
Wyślij wyjątki tooApplication Insights:

* zbyt[policzyć](app-insights-metrics-explorer.md), jako informacje o częstotliwości hello problemu.
* zbyt[Sprawdź indywidualne wystąpienia](app-insights-diagnostic-search.md).

Witaj raporty zawierają hello śladów stosu.

*C#*

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

*JavaScript*

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

zestawy SDK Hello catch wiele wyjątków automatycznie, więc nie zawsze są toocall TrackException jawnie.

* ASP.NET: [napisać kod wyjątki toocatch](app-insights-asp-net-exceptions.md).
* J2EE: [wyjątki są przechwytywane automatycznie](app-insights-java-get-started.md#exceptions-and-request-failures).
* JavaScript: Wyjątki są przechwytywane automatycznie. Automatyczne zbieranie toodisable, dodać fragment kodu toohello wiersza wstawiany strony sieci Web:

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>Wyjątki w module analiz

W [Application Insights Analytics](app-insights-analytics.md), wyjątki widoczne w hello `exceptions` tabeli.

Jeśli [próbkowania](app-insights-sampling.md) jest używany w operacji, hello `itemCount` właściwość wskazuje wartość większą niż 1. Na przykład wartość elementu itemCount == 10 oznacza, że z tootrackException() 10 wywołania procesu pobierania próbek hello jedynie przesyłane, jeden z nich. tooget poprawne liczba wyjątków segmentowanych przez typ wyjątku, takie jak użyć kodu:

```
exceptions | summarize sum(itemCount) by type
```

Większość hello ważne informacje stosu już jest wyodrębniany do oddzielnych zmiennych, ale można ściągnąć powitania od siebie `details` struktury tooget więcej. Ponieważ ta struktura jest dynamiczny, należy rzutować hello wynik toohello typu oczekiwane. Na przykład:

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

Wyjątki tooassociate z ich powiązanego żądania użyć sprzężenia:

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace
Użyj TrackTrace toohelp diagnozować problemy, wysyłając tooApplication "nawigacją dziennik" szczegółowych informacji. Umożliwia wysyłanie fragmentów danych diagnostycznych i sprawdzać ich w [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md).

[Zaloguj się kart](app-insights-asp-net-trace-logs.md) za pomocą tego portalu toohello interfejsu API toosend dzienniki innych firm.

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


Można wyszukiwać w treści wiadomości, ale (w przeciwieństwie do wartości właściwości) nie można filtrować na nim.

limit rozmiaru Hello na `message` jest znacznie wyższa niż limit hello właściwości.
Zaletą TrackTrace jest umieszczenie stosunkowo długo dane wiadomość hello. Na przykład można zakodować danych POST.  

Ponadto możesz dodać komunikat tooyour poziomu ważności. I, podobnie jak inne dane telemetryczne, możesz dodać toohelp wartości właściwości, które można filtrować lub wyszukiwania dla różnych zestawów danych śledzenia. Na przykład:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

W [wyszukiwania](app-insights-diagnostic-search.md), następnie można łatwo filtrować wszystkie wiadomości powitania poziomu ważności określonego związane tooa określonej bazy danych.


### <a name="traces-in-analytics"></a>Dane śledzenia w analityka

W [Application Insights Analytics](app-insights-analytics.md), odwołuje Pokaż tooTrackTrace hello `traces` tabeli.

Jeśli [próbkowania](app-insights-sampling.md) jest używany w operacji, właściwości wartość elementu itemCount hello wskazuje wartość większą niż 1. Na przykład wartość elementu itemCount == 10 oznacza, że 10 wymaga zbyt`trackTrace()`, proces pobierania próbek hello przesyłane tylko jeden z nich. tooget poprawną liczbę wywołań śledzenia, należy używać w związku z tym kod takich jak `traces | summarize sum(itemCount)`.

## <a name="trackdependency"></a>TrackDependency
Użyj hello TrackDependency wywołać czas reakcji hello tootrack i odsetka pomyślnych wywołań zewnętrznego fragmentu tooan kodu. Witaj wyniki są wyświetlane na wykresach zależności hello w portalu hello.

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

Pamiętaj serwera hello zawierają zestawy SDK [modułu zależności](app-insights-asp-net-dependencies.md) która wykrywa i śledzi pewne wywołania zależności automatycznie — na przykład toodatabases i interfejsów API REST. Masz tooinstall agenta w module hello toomake serwer działa. Używasz to wywołanie nie przechwytuje wywołań tootrack hello automatycznego śledzenia, lub jeśli nie chcesz tooinstall hello agenta.

Edytuj tooturn poza hello standardowy moduł śledzenia zależności, [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) i Usuń odwołanie hello zbyt`DependencyCollector.DependencyTrackingTelemetryModule`.

### <a name="dependencies-in-analytics"></a>Zależności w module analiz

W [Application Insights Analytics](app-insights-analytics.md), wywołania trackDependency widoczne w hello `dependencies` tabeli.

Jeśli [próbkowania](app-insights-sampling.md) jest używany w operacji, właściwości wartość elementu itemCount hello wskazuje wartość większą niż 1. Na przykład wartość elementu itemCount == 10 oznacza, że z tootrackDependency() 10 wywołania procesu pobierania próbek hello jedynie przesyłane, jeden z nich. tooget poprawną liczbę zależności segmentowanych przez składnik docelowy, takich jak użyć kodu:

```
dependencies | summarize sum(itemCount) by target
```

zależności tooassociate z ich żądań powiązane, należy użyć sprzężenia:

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>Opróżnienie danych
Zwykle hello SDK wysyła dane w czasie wybrany toominimize hello wpływ na powitania użytkownika. Jednak w niektórych przypadkach można buforu hello tooflush — na przykład, jeśli używasz hello zestawu SDK w aplikacji, która kończy pracę.

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

Należy pamiętać, że funkcja hello asynchronicznego dla hello [kanału dane telemetryczne serwera](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).

## <a name="authenticated-users"></a>Użytkownicy uwierzytelnieni
W aplikacji sieci web użytkownicy są (domyślnie) identyfikowani na podstawie plików cookie. Użytkownik może być traktowane więcej niż raz, jeśli uzyskują oni dostęp do aplikacji z innego komputera lub przeglądarki lub one usunąć pliki cookie.

Jeśli aplikacja tooyour logowania użytkownika, można uzyskać dokładniejsze liczba przez ustawienie Identyfikatora użytkownika hello uwierzytelniony w kodzie przeglądarki hello:

*JavaScript*

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

W sieci web platformy ASP.NET MVC aplikacji, na przykład:

*Razor*

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

Nie jest konieczne toouse hello użytkownika rzeczywistej nazwy logowania. Ma tylko toobe identyfikator unikatowy toothat użytkownika. Nie może zawierać spacji ani żadnego ze znaków hello `,;=|`.

Identyfikator użytkownika Hello jest również ustawiona w pliku cookie sesji i wysyłane toohello serwera. Po zainstalowaniu serwera hello SDK hello uwierzytelnić użytkownika, którego identyfikator jest wysyłany jako część właściwości kontekstu powitania klienta i serwera telemetrii. Następnie można filtrować i wyszukaj w nim.

Aplikacji do konta grupy, użytkownicy, można również przesłać identyfikator konta hello (z hello sam znak ograniczenia).

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

W [Eksploratora metryk](app-insights-metrics-explorer.md), można utworzyć wykres obliczającej **uwierzytelnieni użytkownicy,**, i **kont użytkowników**.

Możesz również [wyszukiwania](app-insights-diagnostic-search.md) dla punktów danych klienta z nazwami użytkowników i kont.

## <a name="properties"></a>Filtrowanie, wyszukiwanie i podzielenie danych za pomocą właściwości
Możesz dołączyć właściwości i pomiarów tooyour zdarzenia (i również toometrics wyświetleń strony, wyjątków i innych danych telemetrycznych).

*Właściwości* są wartości ciągu, której można toofilter telemetrii w raportach użycia hello. Na przykład jeśli aplikacja udostępnia kilka gier, możesz dołączyć nazwę hello hello gier tooeach zdarzenia tak aby były widoczne, które gry są bardziej popularne.

Ma limitu 8192 na powitania długość ciągu. (Toosend duże zestawy danych, należy użyć parametru wiadomość hello [TrackTrace](#track-trace).)

*Metryki* są wartości liczbowe, które mogą być prezentowane w postaci graficznej. Na przykład można toosee przypadku stopniowego zwiększenia hello wyniki, które osiągnięcia Twojej graczy. Wykresy Hello można segmentowanych przez powitalne oddzielnych właściwości, które są wysyłane z zdarzeń hello, dzięki czemu można uzyskać lub skumulowany wykresy dotyczące różnych gier.

Wartości metryki toobe prawidłowo wyświetlany powinny one być większy lub równy too0.

Brak niektórych [limity liczby hello właściwości, wartości właściwości i metryki](#limits) pomocne.

*JavaScript*

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


*C#*

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


*Java*

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> Zajmie się toolog dane osobowe lub informacje we właściwościach.
>
>

*Jeśli używasz metryki*, otwórz Eksploratora metryk i wybierz metrykę hello z hello **niestandardowy** grupy:

![Otwórz Eksploratora metryk, wybierz hello wykresu i wybierz metrykę hello](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> Jeśli nie zostanie wyświetlone Twoje metryki lub hello **niestandardowy** pozycji nie ma, zamknij hello wybór bloku i spróbuj ponownie później. Metryki czasami może zająć godzinę toobe agregowana przez potok hello.

*Jeśli używasz właściwości i metryki*, podzielić Metryka hello przez właściwość hello:

![Ustaw grupowanie, a następnie wybierz właściwość hello Grupuj według](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

*W wyszukiwaniu diagnostycznych*, można wyświetlić właściwości hello i metryki poszczególnych wystąpień tego zdarzenia.

![Wybierz wystąpienie, a następnie wybierz pozycję "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

Użyj hello **wyszukiwania** pola toosee wystąpienia zdarzenia, które mają określoną wartość właściwości.

![Wpisz termin do wyszukiwania](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[Dowiedz się więcej o wyrażeniach wyszukiwania](app-insights-diagnostic-search.md).

### <a name="alternative-way-tooset-properties-and-metrics"></a>Alternatywna metoda tooset właściwości i metryki
Jeśli jest to bardziej wygodne, można zebrać parametry hello zdarzenia w oddzielnych obiektów:

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> Nie należy używać ponownie hello tego samego wystąpienia elementu telemetrii (`event` w tym przykładzie) toocall Track*() wiele razy. Może to spowodować toobe danych telemetrycznych wysłanych z nieprawidłowej konfiguracji.
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>Niestandardowe pomiarów i właściwości w module analiz

W [Analytics](app-insights-analytics.md), właściwości i metryki niestandardowe Pokaż w hello `customMeasurements` i `customDimensions` atrybuty każdego rekordu telemetrii.

Na przykład po dodaniu właściwość o nazwie "gier" tooyour dane telemetryczne żądania to zapytanie liczby wystąpień różne wartości "gry" hello i Pokaż średnią hello hello metryki niestandardowe "wynik":

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

Zwróć uwagę, że:

* Podczas wyodrębniania wartości z hello customDimensions lub customMeasurements JSON, ma typ dynamiczne i dlatego należy rzutować go `tostring` lub `todouble`.
* Konto tootake możliwości hello [próbkowania](app-insights-sampling.md), należy użyć `sum(itemCount)`, a nie `count()`.



## <a name="timed"></a>Zdarzenia czasowe
Czasami ma toochart, jak długo trwa tooperform akcji. Na przykład może być tooknow jak długo użytkowników zająć tooconsider wyborów w grę. Można użyć parametru pomiaru hello tego.

*C#*

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <a name="defaults"></a>Właściwości domyślne telemetria niestandardowa
Jeśli chcesz tooset domyślne wartości właściwości dla niektórych hello zdarzeń niestandardowych, które należy zapisać można ustawić je w wystąpieniu TelemetryClient. Są one dołączone tooevery telemetrii elementu, który został wysłany przez klienta.

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



Wywołania poszczególnych danych telemetrycznych można zastąpić wartości domyślne hello w słownikach ich właściwości.

*Dla języka JavaScript sieci web klientów*, [Użyj inicjatory telemetrii JavaScript](#js-initializer).

*dane telemetryczne tooall właściwości tooadd*, włącznie z danymi hello z modułów kolekcji standardowych [zaimplementować `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).

## <a name="sampling-filtering-and-processing-telemetry"></a>Próbkowanie, filtrowania i przetwarzanie telemetrii
Można napisać kod tooprocess telemetrii przed wysłaniem z hello zestawu SDK. Przetwarzanie Hello zawiera dane są przesyłane z modułów standardowe telemetrii hello, takich jak kolekcji żądania HTTP i zależności kolekcji.

[Dodaj właściwości](app-insights-api-filtering-sampling.md#add-properties) tootelemetry zaimplementowanie `ITelemetryInitializer`. Na przykład można dodać numery wersji lub wartości, które mają być obliczane od innych właściwości.

[Filtrowanie](app-insights-api-filtering-sampling.md#filtering) można zmodyfikować lub odrzucić telemetrii przed wysłaniem z hello SDK zaimplementowanie `ITelemetryProcesor`. Możesz kontrolować, co jest wysyłana lub odrzucone, ale masz tooaccount dla hello wpływu na Twoje metryki. W zależności od tego, jak można odrzucić elementów może spowodować utratę toonavigate możliwości hello między elementy powiązane.

[Próbkowanie](app-insights-api-filtering-sampling.md) jest woluminem spakowanych rozwiązania tooreduce hello danych, które są wysyłane z portalem toohello aplikacji. Robi to bez wpływu na powitania wyświetlane metryki. I kopiuje je bez wpływu na możliwość problemów toodiagnose przechodzenie między powiązane elementy, takie jak wyjątki, żądania i wyświetleń strony.

[Dowiedz się więcej](app-insights-api-filtering-sampling.md).

## <a name="disabling-telemetry"></a>Wyłączanie telemetrii
zbyt*dynamicznie zatrzymywania i uruchamiania* hello zbierania i przekazywania danych telemetrii:

*C#*

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

zbyt*wyłączyć wybranego standardowe moduły zbierające*— na przykład liczniki wydajności żądań HTTP i zależności — Usuń lub komentarz hello odpowiednich wierszy w [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Można to zrobisz, na przykład, jeśli chcesz toosend danych TrackRequest.

## <a name="debug"></a>Tryb dewelopera
Podczas debugowania, jest przydatne toohave telemetrii przyspieszone przez potok hello tak, aby od razu Zobacz wyniki. Możesz również get przejrzeć dodatkowe komunikaty ułatwiające śledzenia problemów z hello telemetrii. Wyłącz go w środowisku produkcyjnym, ponieważ może to spowolnić aplikacji.

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a>Ustawienie hello klucza instrumentacji dla wybranego telemetria niestandardowa
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a>Klucz Instrumentacji dynamiczne
łączenie się dane telemetryczne z programowanie, testów i środowisk produkcyjnych tooavoid można [utworzyć oddzielne zasobów usługi Application Insights](app-insights-create-new-resource.md) i zmiany ich kluczy, w zależności od środowiska hello.

Zamiast pobierania klucza Instrumentacji hello hello pliku konfiguracji, możesz ustawić w kodzie. Ustaw klucz hello w metodzie inicjowania, takich jak pliku global.aspx.cs w usługi ASP.NET:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

*JavaScript*

    appInsights.config.instrumentationKey = myKey;



Na stronach sieci Web, może być tooset go z serwera sieci web hello stanu zamiast kodowania go dosłownie w hello skryptu. Na przykład na stronie sieci Web wygenerowane w aplikacji ASP.NET:

*Język JavaScript w Razor*

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a>TelemetryContext
TelemetryClient ma właściwość kontekstu, która zawiera wartości, które są wysyłane oraz wszystkie dane telemetryczne. Zwykle są ustawione przez moduły standardowe telemetrii hello, ale można również ustawić je samodzielnie. Na przykład:

    telemetry.Context.Operation.Name = "MyOperationName";

Jeśli ustawisz dowolne z tych wartości samodzielnie, rozważ usunięcie hello odpowiedni wiersz z [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), dzięki czemu hello standardowe wartości i wartości, na których nie pobrać pomylić.

* **Składnik**: hello aplikacji i jej wersję.
* **Urządzenie**: dane dotyczące urządzenia hello, gdzie aplikacja hello jest uruchomiona. (W aplikacjach sieci web jest powitania serwera lub klienta urządzenia, które telemetrii hello są wysyłane z).
* **InstrumentationKey**: hello zasobu usługi Application Insights, w którym są wyświetlane dane telemetryczne hello Azure. On zwykle jest pobierany z ApplicationInsights.config.
* **Lokalizacja**: hello lokalizację geograficzną urządzenia hello.
* **Operacja**: W aplikacji sieci web, hello bieżącego żądania HTTP. W innych typów aplikacji można ustawić tego zdarzenia toogroup ze sobą.
  * **Identyfikator**: wartość wygenerowaną odpowiadająca różnych zdarzeń, dzięki czemu inspekcji żadnych zdarzeń diagnostycznych wyszukiwania można znaleźć powiązanych elementów.
  * **Nazwa**: identyfikator zwykle hello adres URL żądania hello HTTP.
  * **SyntheticSource**: Jeśli nie wartość null lub jest pusty, ciąg, który wskazuje źródła hello hello żądania został zidentyfikowany jako test robota lub sieci web. Domyślnie jest ona wykluczana z obliczeń w Eksploratorze metryk.
* **Właściwości**: właściwości, które są wysyłane z wszystkich danych telemetrycznych. Może zostać zastąpiona w poszczególnych Śledź * wywołania.
* **Sesja**: hello sesja. Identyfikator Hello jest ustawiony tooa wygenerowany wartość, która jest zmieniany, gdy użytkownik hello nie była aktywna przez pewien czas.
* **Użytkownik**: informacje o użytkowniku.

## <a name="limits"></a>Limity
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

Naciśnięcie limit szybkości danych hello, użyj tooavoid [próbkowania](app-insights-sampling.md).

toodetermine, jak długo dane są przechowywane, zobacz [przechowywanie danych i ochrona prywatności](app-insights-data-retention-privacy.md).

## <a name="reference-docs"></a>Dokumentacja
* [Platformy ASP.NET — dokumentacja](https://msdn.microsoft.com/library/dn817570.aspx)
* [Dokumentacja programu Java](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [JavaScript — odwołanie](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [Zestaw SDK systemu Android](https://github.com/Microsoft/ApplicationInsights-Android)
* [Zestaw SDK systemu iOS](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>Kod zestawu SDK
* [Platformy ASP.NET Core SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Pakiety systemu Windows Server](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [Zestaw SDK Java](https://github.com/Microsoft/ApplicationInsights-Java)
* [Zestaw SDK dla języka JavaScript](https://github.com/Microsoft/ApplicationInsights-JS)
* [Wszystkie platformy](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>Pytania
* *Jakie wyjątki może zgłosić Track_() wywołania*

    Brak. Nie ma potrzeby toowrap ich w klauzulach try-catch. Jeśli hello SDK napotyka problemy, będzie rejestrować wiadomości w danych wyjściowych konsoli debugowania hello i — jeśli hello wiadomości uzyskać za pomocą — diagnostycznych wyszukiwania.
* *Czy istnieje danych tooget interfejsu API REST z portalu hello?*

    Tak, hello [dostępu do danych interfejsu API](https://dev.applicationinsights.io/). Inne sposoby tooextract dane obejmują [wyeksportować z Analytics tooPower BI](app-insights-export-power-bi.md) i [Eksport ciągły](app-insights-export-telemetry.md).

## <a name="next"></a>Następne kroki
* [Wyszukiwanie zdarzeń i dzienniki](app-insights-diagnostic-search.md)

* [Rozwiązywanie problemów](app-insights-troubleshoot-faq.md)


