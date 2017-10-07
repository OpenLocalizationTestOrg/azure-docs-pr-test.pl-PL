---
title: "aaaLive strumienia metryk niestandardowych metryk i diagnostyki w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Monitorowanie aplikacji sieci web w czasie rzeczywistym z metryki niestandardowe i diagnozowanie problemów z błędów, ślady i wydarzeń na żywo źródło danych."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a>Strumień na żywo metryki: Monitor & Diagnozuj z opóźnieniem 1 sekundę 

Sonda hello interwałów pulsu aplikacji sieci web na żywo, w środowisku produkcyjnym za pomocą strumień na żywo metryki z [usługi Application Insights](app-insights-overview.md). Wybierz i filtrować toowatch liczniki metryki i wydajności w czasie rzeczywistym, bez żadnej usługi tooyour zakłóceń. Sprawdź dane śledzenia stosu z żądań próbki nie powiodło się i wyjątki. Razem z [profilera](app-insights-profiler.md), [debugera migawki](app-insights-snapshot-debugger.md), i [testowania wydajności](app-insights-monitor-web-app-availability.md#performance-tests), strumień na żywo metryki udostępnia zaawansowane i nieinwazyjna narzędzie diagnostyczne dla sieci web na żywo lokacja.

Strumień na żywo metryki można:

* Sprawdź poprawność poprawkę podczas jego zwolnienia obserwując liczniki wydajności i niepowodzenie.
* Obejrzyj hello wpływu testu obciążenia i diagnozowanie problemów na żywo. 
* Skupić się na sesje poszczególnego testu lub odfiltrować znanych problemów, wybierając i metryki hello ma toowatch filtrowania.
* Pobierz dane śledzenia wyjątków, po ich wprowadzeniu.
* Doświadczenia z filtrami toofind hello najistotniejsza kluczowych wskaźników wydajności.
* Monitorowanie oknami wydajności licznika na żywo.
* Łatwo zidentyfikować serwera, na którym występują problemy i filtrować wszystkie hello na żywo/KPI źródła toojust tego serwera.

[![Metryki strumienia wideo na żywo](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)

Strumień na żywo metryki jest obecnie dostępna w aplikacji ASP.NET uruchomionych lokalnie lub w chmurze hello. 

## <a name="get-started"></a>Rozpoczęcie pracy

1. Jeśli nie jest jeszcze [zainstalowane usługi Application Insights](app-insights-asp-net.md) w aplikacji sieci web ASP.NET lub [aplikacji dla systemu Windows server](app-insights-windows-services.md), zrób to teraz. 
2. **Aktualizacja toohello najnowszej wersji** hello pakietu usługi Application Insights. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt i wybierz polecenie **pakiety zarządzania pakietami Nuget**. Otwórz hello **aktualizacje** karcie wyboru **Uwzględnij wersję wstępną**i wybrać wszystkie pakiety Microsoft.ApplicationInsights.* hello.

    Ponownie wdróż aplikację.

3. W hello [portalu Azure](https://portal.azure.com), otwórz hello zasobu usługi Application Insights dla aplikacji, a następnie strumień na żywo.

4. [Witaj bezpieczny kanał kontrolny](#secure-the-control-channel) Jeśli poufnych danych, takich jak nazwy klienta można użyć w filtry.


![W bloku omówienie powitania kliknij strumień na żywo](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a>Brak danych? Sprawdź zapory serwera

Sprawdź hello [wychodzące portów dla strumień na żywo metryki](app-insights-ip-addresses.md#outgoing-ports) są otwarte w zaporze hello serwerów. 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a>Jaka jest różnica strumień na żywo metryki z Eksploratora metryk i analiza?

| |Transmisja strumieniowa na żywo | Eksploratora metryk i analiza |
|---|---|---|
|Opóźnienie|Dane wyświetlane w ciągu sekundy|Zagregowane w ciągu minut|
|Brak okresu przechowywania|Danych będzie nadal występować, gdy znajduje się na powitania wykresu, a następnie zostaje odrzucone|[Dane przechowywane przez 90 dni](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|Na żądanie|Dane przesyłane strumieniowo podczas otwierania metryki na żywo|Dane są przesyłane przy każdym hello zestawu SDK jest zainstalowany i włączony|
|Bezpłatna|Bezpłatne strumień na żywo danych nie istnieje|Zbyt podmiotu[ceny](app-insights-pricing.md)
|Próbkowanie|Wszystkie wybrane metryki i liczniki są przesyłane. Błędy i ślady stosu są próbkowane. TelemetryProcessors nie są stosowane.|Zdarzenia mogą być [próbkowany](app-insights-api-filtering-sampling.md)|
|Kanał kontrolny|Sygnały formant filtru są wysyłane toohello zestawu SDK. Firma Microsoft zaleca [bezpiecznego kanału](#secure-channel).|Komunikacja jest jednokierunkowe toohello portalu|


## <a name="select-and-filter-your-metrics"></a>Wybierz i filtrowanie Twoje metryki

(Dostępne w klasycznej aplikacji ASP.NET przy użyciu hello najnowszej wersji zestawu SDK.)

Stosowanie filtrów dowolnego na dowolnym telemetrii usługi Application Insights z portalu hello można monitorować niestandardowych wskaźnik KPI na żywo. Kliknij formant filtru hello pokazujący, gdy użytkownik myszą żadnego z wykresami hello. powitania po wykresu jest kreślenia niestandardowych liczbę żądań wskaźnika KPI z filtrami na adres URL i czas trwania atrybutów. Sprawdź poprawność filtry z hello podglądu strumienia sekcja, która zawiera źródło danych na żywo dane telemetryczne, które spełniają kryteria hello, określone w dowolnym momencie w czasie. 

![Żądanie niestandardowego wskaźnika KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

Można monitorować wartość inna niż liczba. Opcje Hello są zależne od typu hello strumienia, który może być dowolnym telemetrii usługi Application Insights: żądań, zależności, wyjątki, śledzenie, zdarzenia lub metryki. Może być własną [niestandardowych miar](app-insights-api-custom-events-metrics.md#properties):

![Wartość opcji](./media/app-insights-live-stream/live-stream-valueoptions.png)

Ponadto tooApplication wgląd w dane telemetryczne, można również monitorować wszystkie licznika wydajności systemu Windows zaznaczając który hello strumienia opcje i podanie nazwy hello hello licznika wydajności.

Metryki na żywo są agregowane w dwóch miejscach: lokalnie na każdym serwerze, a następnie na wszystkich serwerach. Możesz zmienić domyślną hello w zaznaczając inne opcje w hello odpowiednich rozwijane.

## <a name="sample-telemetry-custom-live-diagnostic-events"></a>Przykładowe dane telemetryczne: Niestandardowych zdarzeń diagnostycznych na żywo
Domyślnie program hello na żywo źródło zdarzeń przedstawiono przykłady żądań zakończonych niepowodzeniem wywołania zależności, wyjątki, zdarzeń i śledzenia. Kliknij przycisk kryteria ikony filtru hello hello stosowane toosee w dowolnym momencie w czasie. 

![Źródła danych na żywo domyślne](./media/app-insights-live-stream/live-stream-eventsdefault.png)

Jako o metryki, można określić żadnych tooany dowolnego kryterium typów hello telemetrii usługi Application Insights. W tym przykładzie mamy wybierania określone żądanie błędów, ślady i zdarzeń. Możemy również wybierania wszystkie zależności błędy i wyjątki.

![Niestandardowego źródła danych na żywo](./media/app-insights-live-stream/live-stream-events.png)

Uwaga: Obecnie kryteriów na podstawie komunikatu wyjątku używać komunikat o wyjątku peryferyjnych hello. W hello poprzedzających przykład toofilter limit hello niegroźne wyjątek z komunikatem o wyjątku wewnętrznego (hello następujące "<--" ogranicznika) "hello klient został rozłączony." Użyj wiadomości nie zawiera kryteriów "Błąd podczas odczytu treści żądania".

Wyświetl szczegóły hello elementu hello na żywo źródła danych, klikając go. W przypadku wstrzymania hello źródła danych, klikając pozycję **wstrzymać** lub po prostu przewijania w dół lub klikając element. Źródła danych na żywo zostanie wznowiona po Przewiń wstecz toohello top lub klikając hello licznika elementów zebranych podczas została wstrzymana.

![Próbkowany awarii na żywo](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a>Filtruj według wystąpienia serwera

Jeśli chcesz toomonitor wystąpienia roli konkretnego serwera, można filtrować według serwera.

![Próbkowany awarii na żywo](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a>Wymagania dotyczące zestawu SDK
Niestandardowe strumień na żywo metryki jest dostępna z wersji 2.4.0-beta2 lub nowszej programu [zestaw SDK usługi Application Insights dla sieci web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Należy pamiętać, opcja "Uwzględnij wydanie wstępne" tooselect z Menedżera pakietów NuGet.

## <a name="secure-hello-control-channel"></a>Bezpieczny kanał kontrolny hello
Hello niestandardowe filtry kryteria są wysyłane toohello wstecz na żywo metryki składników w hello zestaw SDK usługi Application Insights. filtry Hello potencjalnie mogą zawierać poufne informacje, takie jak customerIDs. Możesz wprowadzić kanału hello zabezpieczyć za pomocą klucza tajnego interfejsu API dodatkowo toohello klucza instrumentacji.
### <a name="create-an-api-key"></a>Utwórz klucz interfejsu API

![Utwórz klucz interfejsu api](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a>Dodaj tooConfiguration klucza interfejsu API
W pliku applicationinsights.config hello Dodaj hello AuthenticationApiKey toohello QuickPulseTelemetryModule:
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
Lub w kodzie, ustaw ją na powitania QuickPulseTelemetryModule:

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

Jednak jeśli rozpoznaje i zaufania hello wszystkich połączonych serwerów, możesz spróbować filtry niestandardowe hello bez kanału hello uwierzytelniony. Ta opcja jest dostępna przez sześć miesięcy. To zastąpienie jest wymagana raz na nowej sesji, lub gdy nowy serwer przejściu do trybu online.

![Opcje uwierzytelniania metryki na żywo](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
>Zdecydowanie zaleca się skonfigurowanie kanału hello uwierzytelniony przed wprowadzeniem potencjalnie wrażliwe informacje, takie jak CustomerID w hello kryteria filtrowania.
>

## <a name="generating-a-performance-test-load"></a>Generowanie wydajności testu obciążenia

Jeśli chcesz toowatch hello wpływu obciążenia zwiększyć, użyj hello testu wydajności bloku. Symuluje ona żądań z liczba równoczesnych użytkowników. Można uruchomić albo "testy ręczne" (ping testy) pojedynczego adresu URL, lub można je uruchomić [testu wydajności sieci web wieloetapowych](app-insights-monitor-web-app-availability.md#multi-step-web-tests) przekazywania (w hello sam sposób jak dostępności testu).

> [!TIP]
> Po utworzeniu testu wydajności hello Otwórz hello testu i hello bloku strumień na żywo w oddzielnych okien. Zostanie wyświetlony, gdy hello w kolejce uruchamia test wydajności i obejrzyj strumień na żywo na powitania tym samym czasie.
>


## <a name="troubleshooting"></a>Rozwiązywanie problemów

Brak danych? Jeśli aplikacja znajduje się w sieci chronionej: strumień na żywo metryki korzysta z innych adresów IP, niż inne telemetrii usługi Application Insights. Upewnij się, że [adresów IP](app-insights-ip-addresses.md) w zaporze są otwarte.



## <a name="next-steps"></a>Następne kroki
* [Monitorowanie użycia za pomocą usługi Application Insights](app-insights-web-track-usage.md)
* [W wyszukiwaniu diagnostycznych](app-insights-diagnostic-search.md)
* [Profiler](app-insights-profiler.md)
* [Debuger migawki](app-insights-snapshot-debugger.md)
