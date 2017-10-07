---
title: "aaaTelemetry próbkowania w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Jak tookeep hello ilość danych telemetrycznych pod kontrolą."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a>Próbkowanie w usłudze Application Insights


Próbkowanie to funkcja [Azure Application Insights](app-insights-overview.md). Jest to hello zalecany sposób tooreduce telemetrii ruchu i magazynu, przy zachowaniu statystycznie prawidłową analizy danych aplikacji. Filtr Hello wybiera elementy, które są powiązane, dzięki czemu można przechodzić między elementami podczas wykonywania badań diagnostycznych.
Gdy metryki liczby są przedstawiane tooyou w portalu hello, są renormalized tootake konto hello próbkowania toominimize żadnego wpływu na powitania statystyk.

Próbkowania powoduje zmniejszenie kosztów ruchu i dane i pomaga uniknąć ograniczania.

## <a name="in-brief"></a>Krótko mówiąc:
* Próbkowanie zachowuje 1 w  *n*  rejestruje i odrzuca hello rest. Na przykład mogą go zachować zdarzenia 1 do 5, częstotliwość próbkowania, 20%. 
* Próbkowanie odbywa się automatycznie, jeśli aplikacja wyśle dużej ilości danych telemetrii, w aplikacji serwera sieci web ASP.NET.
* Można również ustawić próbkowania ręcznie, albo hello w portalu na powitania cennikiem; lub w hello zestawu SDK platformy ASP.NET w pliku .config hello tooalso zmniejszenie ruchu w sieci hello.
* Jeśli dziennika zdarzeń niestandardowych, i chcesz toomake się, że zestaw zdarzeń jest zachowywana lub odrzucone ze sobą, upewnij się, że zostały one hello tę samą wartość OperationId.
* dzielnik próbkowania Hello  *n*  jest zgłaszany we wszystkich rekordach we właściwości hello `itemCount`, w wyszukiwaniu widocznego w obszarze hello przyjazna nazwa "liczbę żądań" lub "liczba zdarzeń". Podczas pobierania próbek nie jest w operacji `itemCount==1`.
* Jeśli piszesz zapytania analityczne, [uwzględnienia próbkowania](app-insights-analytics-tour.md#counting-sampled-data). W szczególności, zamiast po prostu zliczanie rekordów, należy użyć `summarize sum(itemCount)`.

## <a name="types-of-sampling"></a>Typy pobierania próbek
Istnieją trzy metody alternatywne próbkowania:

* **Próbkowanie adaptacyjną** automatycznie dostosowuje hello ilość danych telemetrycznych wysłanych z hello zestawu SDK w aplikacji ASP.NET. Domyślnie z 2.0.0-beta3 v zestawu SDK. Obecnie dostępne dla platformy ASP.NET tylko telemetrii po stronie serwera. 
* **Próbkowanie stałej stawki** zmniejsza hello ilość danych telemetrycznych wysłanych z serwera programu ASP.NET oraz z przeglądarki użytkownika. Możesz ustawić częstotliwość hello. powitania klienta i serwera będzie synchronizować ich próbkowania tak, w wyszukiwania, można przechodzić między wyświetleń strony powiązane i żądań.
* **Wprowadzanie próbkowania** działa w hello portalu Azure. Odrzuca niektóre dane telemetryczne hello dociera z aplikacji, z szybkością ustawieniu. Nie zmniejszenie ruchu telemetrii, ale pomaga zachować w wykorzystaniu całego przydziału miesięcznego. Witaj dużą zaletą próbkowania wprowadzanie jest bez ponownego wdrażania aplikacji można ją ustawić, czy działa on jednakowo do wszystkich serwerów i klientów. 

W przypadku adaptacyjną lub stała częstotliwość próbkowania w operacji, wprowadzanie próbek jest wyłączone.

## <a name="ingestion-sampling"></a>Wprowadzanie próbkowania
Ta forma pobierania próbek działa w momencie hello gdzie telemetrii hello z serwera sieci web, przeglądarki i urządzenia osiąga punkt końcowy usługi Application Insights hello. Chociaż nie redukują hello telemetrii wysyłania danych z aplikacji, Zmniejsz ilość hello przetwarzane i przechowywane (i naliczona opłata za) przez usługę Application Insights.

Użyj tego typu próbkowania, jeśli aplikacja często przechodzi przez jego przydział miesięczny i nie ma możliwości hello przy użyciu jednego z typów na podstawie zestawu SDK hello pobierania próbek. 

Ustaw częstotliwość próbkowania hello w hello przydziałów i cennik bloku:

![W bloku Omówienie aplikacji hello kliknij ustawienia, przydziału, próbek, a następnie wybierz częstotliwość próbkowania, a następnie kliknij przycisk Aktualizuj.](./media/app-insights-sampling/04.png)

Podobnie jak inne rodzaje próbkowania algorytm hello zachowuje elementy powiązane dane telemetryczne. Na przykład, gdy jest sprawdzanie hello telemetrii w wyszukiwania, będzie możliwe toofind hello powiązana tooa określonego wyjątku. Metryka liczby takich jak liczby żądań i szybkość wyjątek poprawnie zostaną zachowane.

Punkty danych, które są odrzucane przez pobieranie próbek nie są dostępne w dowolnej funkcji usługi Application Insights, takich jak [eksportu ciągłego](app-insights-export-telemetry.md).

Wprowadzanie próbkowania nie działa podczas operacji SDK próbkowania adaptacyjną lub stałej stawki. Częstotliwość próbkowania hello na powitania zestawu SDK jest mniejsza niż 100%, następnie hello wprowadzanie próbkowania ustawione jest ignorowana.

> [!WARNING]
> Witaj wartości wyświetlane na kafelku hello wskazuje wartość hello, dla wprowadzanie próbkowania. Jeśli jest używany w operacji pobierania zestawu SDK nie reprezentuje hello rzeczywiste próbkowania.
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a>Adaptacyjną próbkowania na serwerze sieci web
Adaptacyjną próbkowania jest dostępna dla hello zestaw SDK usługi Application Insights dla platformy ASP.NET v 2.0.0-beta3 i nowszych i jest domyślnie włączona. 

Próbkowanie adaptacyjną ma wpływ na powitania ilość danych telemetrycznych wysłanych z Twojej toohello aplikacji serwera sieci web usługi Application Insights. Witaj woluminu jest automatycznie korygowane tookeep w ramach określonej maksymalna szybkość ruchu.

Go nie działa niewielki dane telemetryczne, więc w debugowaniu aplikacji lub witryny sieci Web z użyciem niski nie będzie to mieć wpływ na.

wolumin docelowy hello tooachieve, niektóre dane telemetryczne hello generowane są usuwane. Zachowując podobnie jak inne rodzaje próbkowania algorytm hello elementy powiązane dane telemetryczne. Na przykład, gdy jest sprawdzanie hello telemetrii w wyszukiwania, będzie możliwe toofind hello powiązana tooa określonego wyjątku. 

Metryka zlicza, takich jak liczby żądań i szybkość wyjątek są skorygowaną toocompensate dla hello próbkowania szybkości, tak aby pokazywały około poprawne wartości w Eksploratorze metryki.

**Aktualizacja projektu NuGet** najnowsza wersja pakietów toohello *wersji wstępnej* wersji usługi Application Insights: kliknij prawym przyciskiem myszy projekt hello w Eksploratorze rozwiązań, wybierz polecenie Zarządzaj pakietami NuGet Sprawdź **Include wstępna** i wyszukaj Microsoft.ApplicationInsights.Web. 

W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), można dostosować kilku parametrów w hello `AdaptiveSamplingTelemetryProcessor` węzła. rysunki Hello wyświetlane są wartościami domyślnymi hello:

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    Witaj docelowej szybkość, z której hello adaptacyjną algorytm ma dla **na każdym hoście serwera**. Jeśli aplikacja sieci web jest uruchomiony na wielu hostach, tak tooremain w szybkość docelowy ruchu w portalu usługi Application Insights hello Zmniejsz tę wartość.
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    Interwał powitania, w których hello jest ponownie oceniane bieżącej szybkości telemetrii. Ocena jest wykonywane średniej ruchomej. Możesz tooshorten ten interwał Jeśli seria odpowiedzialności za toosudden telemetrii.
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    W przypadku zmiany wartości wartości procentowej pobierania próbek, jak najszybciej po firma Microsoft może toolower ponownie próbkowania procent toocapture mniejsza ilość danych.
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    W przypadku zmiany wartości wartości procentowej pobierania próbek, jak najszybciej po firma Microsoft może tooincrease ponownie próbkowania procent toocapture większej ilości danych.
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    Jako wartość procentowa próbek różni się to minimalny hello jest firma Microsoft może tooset.
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    Jako wartość procentowa próbek różni się to maksymalna wartość hello jest firma Microsoft może tooset.
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    Hello obliczania średniej ruchomej hello waga hello przypisaną wartość najnowszych toohello. Użyj tooor równy wartość mniejszą niż 1. Mniejsze wartości zmiany algorytm hello mniej reaktywne toosudden.
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    wartość Hello przypisany podczas aplikacji hello właśnie zostało uruchomione. Nie zmniejsza to podczas debugowania kodu. 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    Lista typów, które nie mają toobe próbkowany rozdzielany średnikami. Rozpoznawane są typy: zależność, zdarzenia, wyjątek, widok strony, żądanie, śledzenia. Wszystkie wystąpienia hello określone typy są przesyłane; próbkowanych Hello typy, które nie zostały określone.

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    Lista typów, które mają toobe próbkowany rozdzielany średnikami. Rozpoznawane są typy: zależność, zdarzenia, wyjątek, widok strony, żądanie, śledzenia. Witaj określone typy są próbkowane; wszystkie wystąpienia elementu hello będą zawsze przesyłane innych typów.


**tooswitch poza** adaptacyjną próbkowania, Usuń hello AdaptiveSamplingTelemetryProcessor węzła z applicationinsights-config.

### <a name="alternative-configure-adaptive-sampling-in-code"></a>Alternatywa: Konfigurowanie adaptacyjną próbkowania w kodzie
Zamiast dostosowywania próbkowania w pliku .config hello, możesz użyć kodu. Dzięki temu toospecify funkcję wywołania zwrotnego, które jest wywoływane zawsze, gdy częstotliwość próbkowania hello jest ponownie oceniane. Można go użyć, na przykład toofind się, jakie częstotliwość próbkowania jest używany.

Usuń hello `AdaptiveSamplingTelemetryProcessor` węzeł z pliku .config hello.

*C#*

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Dowiedz się więcej o telemetrii procesorów](app-insights-api-filtering-sampling.md#filtering).)

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a>Próbkowania dla stron sieci web w języku JavaScript
Można skonfigurować stron sieci web do pobierania próbek stałej stawki z dowolnego serwera. 

Gdy możesz [skonfigurować hello stron sieci web dla usługi Application Insights](app-insights-javascript.md), zmodyfikować fragment hello, który można pobrać z portalu Application Insights hello. (W aplikacjach ASP.NET, fragment hello zazwyczaj znajduje się w _Layout.cshtml.)  Wstaw wiersz, takich jak `samplingPercentage: 10,` przed klucza Instrumentacji hello:

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

W przypadku wartości procentowej pobierania próbek hello wybierz wartość procentową, która jest Zamknij too100/N, gdzie N to liczba całkowita.  Próbkowanie aktualnie nie obsługuje innych wartości.

Włączenie próbkowania stałej stawki na powitania serwera, hello klientami a serwerem będzie synchronizować tak, w wyszukiwania, można przechodzić między wyświetleń strony powiązane i żądań.

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a>Stałej częstotliwość próbkowania dla witryn sieci web ASP.NET
Stały częstotliwość próbkowania zmniejsza ruch hello wysłanych z serwera sieci web i przeglądarki sieci web. W przeciwieństwie do próbkowania adaptacyjną zmniejsza telemetrii według stałej stawki ustalanej określone przez użytkownika. Również synchronizacji powitania klienta i serwera próbkowania, tak aby elementy powiązane są zachowywane — na przykład, jeśli przyjrzymy widoku strony w wyszukiwaniu mogły zostać odnalezione jego powiązanego żądania.

Algorytm próbkowania Hello zachowuje elementy powiązane. Dla każdego żądania HTTP zdarzeń, go i jego zdarzenia powiązane są odrzucane albo przesyłane. 

W Eksploratorze metryk stawki, takich jak liczby żądań i wyjątków są pomnożona przez współczynnik toocompensate dla hello próbkowania, dzięki czemu są one poprawne około.

1. **Aktualizację pakietów NuGet projektu** toohello najnowszych *wstępną* wersji usługi Application Insights. Kliknij prawym przyciskiem myszy projekt hello w Eksploratorze rozwiązań, wybierz polecenie Zarządzaj pakietami NuGet Sprawdź **Uwzględnij wersję wstępną** i wyszukaj Microsoft.ApplicationInsights.Web. 
2. **Wyłącz adaptacyjną próbkowania**: W [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), usunąć lub komentarz hello `AdaptiveSamplingTelemetryProcessor` węzła.
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. **Włącz moduł próbkowania stałej stawki hello.** Dodaj ten fragment zbyt[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> W przypadku wartości procentowej pobierania próbek hello wybierz wartość procentową, która jest Zamknij too100/N, gdzie N to liczba całkowita.  Próbkowanie aktualnie nie obsługuje innych wartości.
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a>Alternatywa: Włącz stałej częstotliwość próbkowania w kodzie serwera
Zamiast ustawienie parametru próbkowania hello w pliku .config hello, możesz użyć kodu. 

*C#*

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Dowiedz się więcej o telemetrii procesorów](app-insights-api-filtering-sampling.md#filtering).)

## <a name="when-toouse-sampling"></a>Podczas pobierania próbek toouse?
Jeśli używasz hello 2.0.0-beta3 wersji zestawu SDK platformy ASP.NET jest automatycznie włączone adaptacyjną próbkowania lub nowszym. Niezależnie od tego, jakiego używasz wersja zestawu SDK można użyć próbkowania wprowadzanie (w naszym serwera).

Nie trzeba próbkowania dla większości aplikacji małych i średnich. najbardziej przydatne informacje diagnostyczne Hello i najbardziej dokładna statystyki są pobierane przez zbierania danych dotyczących wszystkich działań użytkownika. 

główne zalety próbkowania Hello są następujące:

* Aplikacja Insights usługi porzucania ("ogranicza") danych punktów aplikacji wysyła bardzo wysoki współczynnik dane telemetryczne w skrócie czasu interwału. 
* tookeep w hello [przydziału](app-insights-pricing.md) punktów danych dla warstwy cenowej. 
* ruch sieciowy tooreduce z kolekcji hello telemetrii. 

### <a name="which-type-of-sampling-should-i-use"></a>Jakiego typu próbkowania należy używać?
**Użyj wprowadzanie próbkowania, jeśli:**

* Często przejść przez wykorzystaniu całego przydziału miesięcznego dane telemetryczne.
* Używasz wersji hello zestawu SDK, który nie obsługuje pobierania próbek — na przykład, hello zestawu Java SDK lub wersji platformy ASP.NET starszych niż 2.
* Otrzymujesz dużej ilości danych telemetrycznych z przeglądarki sieci web użytkownika.

**Użyj stałej stawki próbkowania, jeśli:**

* Używasz hello zestaw SDK usługi Application Insights dla usług sieci web ASP.NET w wersji 2.0.0 lub nowszej, a
* Ma próbkowania synchronizowane między klientem a serwerem, dzięki czemu możesz podczas analizowania zdarzenia w [wyszukiwania](app-insights-diagnostic-search.md), można przechodzić między powiązanych zdarzeń na powitania klienta i serwera, takie jak liczba wyświetleń strony i żądań http.
* Upewnieniu się wartości procentowej pobierania próbek hello aplikacji. Powinien być wystarczająco duża tooget dokładnych metryk, ale poniżej hello szybkość, z której przekracza przydział cenową i hello ograniczenie. 

**Użyj adaptacyjną próbkowania:**

W przeciwnym razie zalecamy adaptacyjną próbkowania. Ta opcja jest włączona domyślnie w hello ASP.NET server SDK w wersji 2.0.0-beta3 lub nowszej. Do niektórych minimalna częstotliwość nie redukują ruchu, nie będzie to miało wpływ na lokacji niskiego użycia.

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a>Jak sprawdzić, czy w operacji pobierania próbek
rzeczywiste hello toodiscover próbkowania szybkość niezależnie od tego, gdzie ma zastosowane, użyj [Analytics query](app-insights-analytics.md) takich jak ta:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

W każdym zachowane rekordu, `itemCount` wskazuje liczbę hello oryginalnego rekordów, które reprezentuje on równy too1 + hello liczbę poprzednich odrzuconych rekordów. 

## <a name="how-does-sampling-work"></a>Jak działa pobierania próbek
Stałej stawki i adaptacyjną próbkowania są funkcją hello zestawu SDK w wersji platformy ASP.NET z 2.0.0 i jego nowszych wersjach. Wprowadzanie próbkowania jest funkcją hello usługa Application Insights i można w operacji hello zestawu SDK nie wykonuje próbkowania. 

Algorytm próbkowania Hello decyduje o tym, które toodrop elementów telemetrii i które tych tookeep (czy jest hello zestawu SDK lub usługa Application Insights hello). decyzja próbkowania Hello opiera się na kilka reguł, które mają toopreserve wszystkie punkty danych powiązane ze sobą nienaruszone, obsługa diagnostycznych doświadczenie w usłudze Application Insights jest efektywna i niezawodne nawet w przypadku ograniczonego zestawu danych. Na przykład jeśli niepomyślnych żądań aplikacji są wysyłane dodatkowe dane telemetryczne elementy (takie jak wyjątku i ślady zarejestrowane z tym żądaniem), pobierania próbek nie zostaną podzielone tego żądania i inne dane telemetryczne. Ją zachowuje lub porzuca je wszystkie razem. W związku z tym sprawdzając szczegóły żądania hello w usłudze Application Insights, należy zawsze widzieć żądania hello wraz z jego elementy skojarzone dane telemetryczne. 

Dla aplikacji, które definiują "użytkownika" (czyli najbardziej typowych aplikacji sieci web), decyzja próbkowania hello jest oparta na skrót hello hello identyfikator użytkownika, co oznacza, że wszystkie dane telemetryczne dla każdego konkretnego użytkownika jest zachowywana lub porzucony. Dla hello typów aplikacji, które nie określają użytkowników (np. usługi sieci web) decyzja próbkowania hello jest oparta na identyfikator operacji hello hello żądania. Na koniec hello telemetrii elementów, które nie ma identyfikatora użytkownika ani operacji Ustaw (na przykład elementów dane telemetryczne zgłoszone asynchronicznych wątków nie kontekst http) próbkowania po prostu przechwytuje procent elementów telemetrii każdego typu. 

Prezentując tooyou wstecz telemetrii usługi Application Insights hello usługi można dostosować metryki hello przez hello tej samej wartości procentowej pobierania próbek użytej w czasie hello kolekcji, toocompensate dla hello brakujących punktów danych. W związku z tym podczas przeglądania hello telemetrii w usłudze Application Insights, użytkownicy hello jest wyświetlany statystycznie prawidłową przybliżenia, które są bardzo Zamknij toohello liczb rzeczywistych.

dokładność Hello zbliżenia hello zależy przede wszystkim wartości procentowej pobierania próbek hello skonfigurowane. Dokładność hello zwiększa się również, dla aplikacji, które obsługi dużej liczby zazwyczaj podobne żądania z partii użytkowników. Na hello drugiej strony, aplikacji, które nie działają z znaczne obciążenie, próbkowanie nie jest potrzebna, jak te aplikacje zazwyczaj można wysłać ich dane telemetryczne pozostając w ramach limitu przydziału hello, nie powodując utraty danych z przepustowości. 

Należy pamiętać, że usługi Application Insights nie przykładowe typy telemetrii metryki i sesji od dla tych typów zmniejszenie precyzji hello można zdecydowanie niepożądane. 

### <a name="adaptive-sampling"></a>Adaptacyjną pobierania próbek
Adaptacyjną próbkowania dodaje składnik tego monitorów hello bieżąca szybkość transmisji z hello zestawu SDK i dostosowuje hello próbkowania procent tootry toostay w hello docelowy maksymalna szybkość. dostosowanie Hello są przeliczane w regularnych odstępach czasu i opierają się na to ruchoma średnia hello szybkość transmisji wychodzących.

## <a name="sampling-and-hello-javascript-sdk"></a>Pobieranie próbek i hello JavaScript SDK
powitania klienta (JavaScript) zestawu SDK uczestniczy w stałej częstotliwość próbkowania w połączeniu z powitania po stronie serwera zestawu SDK. Hello Instrumentacji stron wysyła dane telemetryczne po stronie klienta z hello tych samych użytkowników, których powitania po stronie serwera wprowadzono decyzji zbyt "sample w." Tę logikę jest zaprojektowana toomaintain integralność sesji użytkownika na stronach klienta i serwera. W związku z tym z dowolnym elemencie określonego telemetrii usługi Application Insights, można znaleźć wszystkie pozostałe elementy danych telemetrycznych dla tego użytkownika lub sesję. 

*Moje klienta i dane telemetryczne po stronie serwera nie pokazuj przykłady skoordynowany sposób, jak opisano powyżej.*

* Sprawdź czy jest włączony próbkowania stałej stawki zarówno na serwerze i kliencie.
* Upewnij się, że ta wersja zestawu SDK hello jest 2.0 lub nowszej.
* Sprawdź, czy możesz ustawić hello samej próbkowania wartość procentowa w powitania klienta i serwera.

## <a name="frequently-asked-questions"></a>Często zadawane pytania
*Dlaczego nie jest próbkowania proste "zbieranie X procent każdego typu danych telemetrycznych"?*

* Gdy ta metoda pobierania próbek będzie dostarczać bardzo wysokiej precyzji w przybliżenia metryki, go spowoduje przerwanie możliwości toocorrelate danych diagnostycznych na użytkowników, sesji i żądań, co jest szczególnie ważne dla diagnostyki. W związku z tym pobierania próbek działa lepiej "Zbieraj wszystkie dane telemetryczne elementy X procent użytkowników aplikacji" lub "Zbieraj wszystkie dane telemetryczne dotyczące X Procent żądań aplikacji" logiki. Dla elementów telemetrii hello nie są skojarzone z żądaniami hello (na przykład asynchronicznego przetwarzania w tle) spadek hello jest zbyt "zbieranie X procent wszystkie elementy dla każdego typu danych telemetrycznych." 

*Mogą ulec zmianie wartości procentowej pobierania próbek hello?*

* Tak, adaptacyjną próbkowania stopniowo zmienia wartości procentowej pobierania próbek hello, oparte na powitania obecnie obserwowanych ilość danych telemetrycznych hello.

*Użycie stałej stawki próbkowania, jak sprawdzić, które próbkowania procent działa hello najlepsze w przypadku mojej aplikacji?*

* Jednym ze sposobów jest toostart z adaptacyjną próbkowania, sprawdź, co Oceń to reguluje na (zobacz hello powyżej pytanie), a następnie przełącznika toofixed częstotliwość próbkowania przy użyciu tego kursu. 
  
    W przeciwnym razie należy tooguess. Analizowanie bieżącego użycia telemetrii w AI, obserwować żadnego ograniczania przepustowości, czyli występujących i szacowania hello ilość danych telemetrycznych hello zbierane. Te trzy wejść, wraz z wybranej warstwy cenowej, sugerują, jaka może być tooreduce hello ilość danych telemetrycznych hello zbierane. Jednak wzrost liczby hello użytkowników lub niektóre shift, w hello ilość danych telemetrycznych może unieważnić oszacować.

*Co się stanie, jeśli można skonfigurować wartości procentowej pobierania próbek zbyt niska?*

* Procent próbkowania zbyt niski (próbkowanie over-aggressive) zmniejsza hello dokładność przybliżenia hello toocompensate hello wizualizacji danych hello hello danych woluminu redukcji próbujący usługi Application Insights. Ponadto czynności diagnostycznych może być obniżona, jako część hello rzadko niepowodzeniem lub powolne żądań próbkować można się.

*Co się stanie, jeśli można skonfigurować zbyt wysokiej wartości procentowej pobierania próbek?*

* Konfigurowanie próbkowania zbyt wysoki procent (nie agresywne wystarczająco) powoduje niewystarczające redukcję ilości hello hello zbieranych danych telemetrycznych. Nadal może się okazać dane telemetryczne utraty danych związane z toothrottling i koszt hello przy użyciu usługi Application Insights mogą być wyższe niż planowana powodu toooverage opłat.

*Na platformach, które mogą używać próbkowania?*

* Wprowadzanie próbkowanie może być spowodowany automatycznie dla dowolnego telemetrii powyżej woluminu hello zestawu SDK nie wykonuje próbkowanie. To będzie działać, na przykład, jeśli aplikacja korzysta z serwera Java lub jeśli używasz starszej wersji hello zestawu SDK platformy ASP.NET.
* Jeśli używasz zestawu SDK platformy ASP.NET w wersji 2.0.0 lub nowszym (hostowanego na platformie Azure lub na danym serwerze), możesz uzyskać adaptacyjną próbkowania domyślnie, ale szybkość toofixed można przełączać się zgodnie z powyższym opisem. Z włączonym próbkowaniem stałej stawki, hello przeglądarkę zestawu SDK automatycznie synchronizuje toosample zdarzenia związane z. 

*Brak niektórych zdarzeń rzadkich zawsze ma toosee. Jak można je poza próbkowania hello modułu?*

* Inicjowanie oddzielnego wystąpienia TelemetryClient z nowego TelemetryConfiguration (nie hello domyślnie aktywny). Użyj tego toosend rzadkich zdarzeń.

## <a name="next-steps"></a>Następne kroki
* [Filtrowanie](app-insights-api-filtering-sampling.md) zapewniają więcej ścisłej kontroli wysyła zestawu SDK.

