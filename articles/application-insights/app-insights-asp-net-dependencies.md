---
title: "aaaDependency śledzenia w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Analizowanie użycia, dostępności i wydajności aplikacji lokalnej lub aplikacji sieci Web na platformie Microsoft Azure za pomocą usługi Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a>Skonfiguruj usługę Application Insights: Śledzenie zależności
A *zależności* jest składnik zewnętrzny, który jest wywoływany przez aplikację. Usługa ta jest zazwyczaj wywoływana przy użyciu protokołu HTTP, lub bazy danych lub systemu plików. [Usługa Application Insights](app-insights-overview.md) mierzy czas oczekiwania zależności aplikacji i jak często wywołanie zależności nie powiedzie się. Zbadaj określonych wywołań i łączyć je toorequests i wyjątki.

![przykładowe wykresy](./media/app-insights-asp-net-dependencies/10-intro.png)

monitor zależności poza pole Hello raportów obecnie typy toothese wywołania zależności:

* Serwer
  * Bazy danych SQL
  * Sieci web ASP.NET i usługi WCF, które używają powiązania oparte na protokole HTTP
  * Lokalne lub zdalne wywołania HTTP
  * Azure DB rozwiązania Cosmos, tabeli magazynu obiektów blob i kolejki
* Strony sieci Web
  * Wywołania AJAX

Monitorowanie działania za pomocą [Instrumentacji kodu bajtów](https://msdn.microsoft.com/library/z9z62c29.aspx) wokół wybrane metody zostaną usunięte. Obciążenie jest minimalne.

Można również napisać własny zestaw SDK wymaga toomonitor innych zależności, zarówno w hello kod klienta i serwera, jak za pomocą hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

## <a name="set-up-dependency-monitoring"></a>Konfigurowanie monitorowania zależności
Informacje o zależnościach częściowe są zbierane automatycznie przez hello [zestaw SDK usługi Application Insights](app-insights-asp-net.md). tooget pełnych danych, zainstaluj hello odpowiedniego agenta dla powitania serwera hosta.

| Platforma | Instalowanie |
| --- | --- |
| Serwer usług IIS |Albo [Zainstaluj Monitor stanu na serwerze](app-insights-monitor-performance-live-website-now.md) lub [uaktualnienia struktury too.NET aplikacji 4.6 lub nowszy](http://go.microsoft.com/fwlink/?LinkId=528259) i zainstaluj hello [zestaw SDK usługi Application Insights](app-insights-asp-net.md) w aplikacji. |
| Aplikacja sieci Web platformy Azure |W Panelu sterowania aplikacji sieci web [hello Otwórz blok usługi Application Insights w Panelu sterowania aplikacji sieci web](app-insights-azure-web-apps.md) i wybierz opcję instalacji, jeśli zostanie wyświetlony monit. |
| Usługi w chmurze Azure |[Zadanie uruchamiania użyj](app-insights-cloudservices.md) lub [zainstalowania środowiska .NET framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md) |

## <a name="where-toofind-dependency-data"></a>Gdy dane zależności toofind
* [Mapowanie aplikacji](#application-map) wizualizuje zależności między aplikacji i składniki pokrewne.
* [Bloki wydajności, przeglądarki oraz Niepowodzenie](#performance-and-blades) przedstawiono dane zależności serwera.
* [Blok przeglądarki](#ajax-calls) pokazuje wywołania AJAX z przeglądarki użytkownika.
* [Kliknij go, z powolnym działaniem lub nieudanych żądań](#diagnose-slow-requests) toocheck wywołania ich zależności.
* [Analiza](#analytics) mogą być używane tooquery zależności danych.

## <a name="application-map"></a>Mapa aplikacji
Mapowanie aplikacji działa jako pomoc visual toodiscovering zależności między składnikami aplikacji hello. Jest automatycznie generowany na podstawie danych telemetrycznych hello z aplikacji. Ten przykład przedstawia wywołania AJAX hello przeglądarki skryptów i wywołania REST z powitania serwera usług zewnętrznych tootwo aplikacji.

![Mapa aplikacji](./media/app-insights-asp-net-dependencies/08.png)

* **Przejdź z pól hello** toorelevant zależności oraz inne wykresy.
* **Numer PIN hello mapy** toohello [pulpitu nawigacyjnego](app-insights-dashboards.md), gdzie będzie pełną funkcjonalność.

[Dowiedz się więcej](app-insights-app-map.md).

## <a name="performance-and-failure-blades"></a>Wydajność i niepowodzenie bloków
Blok wydajności Hello pokazuje hello czas trwania wywołania zależności przez powitania serwera aplikacji. Brak podsumowania wykres i tabelę segmentowanych przez wywołanie.

![Wykresy zależności bloku wydajności](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

Kliknij wykresy podsumowań hello lub hello tabeli elementów toosearch raw wystąpień tych wywołań.

![Wystąpienia wywołanie zależności](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

**Liczba awarii** są wyświetlane na powitania **błędów** bloku. Błąd jest kod powrotny, który nie znajduje się w hello zakresu 200 – 399, lub nieznany.

> [!NOTE]
> **100% błędów?** -Prawdopodobnie oznacza to są dane z częściowa zależności tylko pierwsze. Należy zbyt[Konfigurowanie monitorowania tooyour odpowiednie platformy zależności](#set-up-dependency-monitoring).
>
>

## <a name="ajax-calls"></a>Wywołania AJAX
Blok przeglądarki Hello pokazuje czas trwania hello i częstość niepowodzeń AJAX wywołuje z [JavaScript na stronach sieci web](app-insights-javascript.md). Są wyświetlane jako zależności.

## <a name="diagnosis"></a>Diagnozowanie powolne żądań
Każde zdarzenie żądania jest powiązany z wywołania zależności hello, wyjątków i inne zdarzenia, które są śledzone podczas przetwarzania aplikacji hello żądania. Dlatego nieprawidłowo wykonywania niektórych żądań można ustalić czy jest powodu tooslow odpowiedzi z zależności.

Przejdźmy przykład tego.

### <a name="tracing-from-requests-toodependencies"></a>Śledzenie za pomocą toodependencies żądań
Otwarcie bloku wydajności hello i przyjrzyj się siatki hello żądań:

![Lista żądań ze średnimi lub liczby](./media/app-insights-asp-net-dependencies/02-reqs.png)

Witaj top, który jest zbyt długa. Zobaczmy, jeśli firma Microsoft można ustalić, gdzie jest zużywany czas hello.

Kliknij ten wiersz toosee oddzielne żądanie zdarzenia:

![Lista wystąpień żądania](./media/app-insights-asp-net-dependencies/03-instances.png)

Kliknij tooinspect wystąpienia dowolnego długotrwałe dalszego i przewiń w dół toohello zależności zdalne wywołania toothis pokrewne żądanie:

![Znajdź wywołania zależności tooRemote, zidentyfikować nietypowe czas trwania](./media/app-insights-asp-net-dependencies/04-dependencies.png)

Wygląda jak większość hello obsługi czasu poświęconego tego żądania w usłudze lokalnej tooa wywołania.

Wybierz ten wiersz tooget więcej informacji:

![Kliknij przycisk za pośrednictwem tego culprit hello tooidentify zależności zdalne](./media/app-insights-asp-net-dependencies/05-detail.png)

Wygląda na to, gdzie jest hello problem. Firma Microsoft już przeprowadzana na powitania problem. należy więc teraz możemy just toofind się, dlaczego tego wywołania trwa tak długo.

### <a name="request-timeline"></a>Oś czasu żądania
W przypadku różnych nie ma żadnych wywołanie zależności, które są szczególnie długie. Ale przełączając toohello widoku osi czasu, możemy stwierdzić, których opóźnienie hello wystąpiła w naszym wewnętrzne przetwarzanie:

![Znajdź wywołania zależności tooRemote, zidentyfikować nietypowe czas trwania](./media/app-insights-asp-net-dependencies/04-1.png)

Prawdopodobnie toobe big przerwę po pierwszym wywołaniu zależności hello, więc należy przyjrzymy się naszego kodu toosee dlatego oznacza to.

### <a name="profile-your-live-site"></a>Profil witryny na żywo

Nie wiadomo, gdzie czas hello przechodzi? Witaj [profilera usługi Application Insights](app-insights-profiler.md) najdłużej hello trwało śladów HTTP wywołuje tooyour witryny na żywo i zawiera funkcje, które w kodzie.

## <a name="failed-requests"></a>Żądań zakończonych niepowodzeniem
Żądań zakończonych niepowodzeniem może też być skojarzone z toodependencies wywołania nie powiodło się. Firma Microsoft ponownie, kliknij go, tootrack dół hello problem.

![Kliknij przycisk hello wykres nieudanych żądań](./media/app-insights-asp-net-dependencies/06-fail.png)

Kliknij go, wystąpienie tooan nieudanych żądań i przyjrzyj się jego skojarzonego zdarzenia.

![Kliknij typ żądania, kliknij przycisk hello tooget tooa inny widok wystąpienia hello tego samego wystąpienia, kliknij go tooget szczegóły wyjątku.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a>Analiza
Można śledzić zależności w hello [języka zapytań usługi Analiza dzienników](https://docs.loganalytics.io/). Oto kilka przykładów.

* Znajdź wszystkie wywołania zależności nie powiodło się:

```

    dependencies | where success != "True" | take 10
```

* Znajdź wywołania AJAX:

```

    dependencies | where client_Type == "Browser" | take 10
```

* Znajdź związanych z żądaniami wywołania zależności:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* Znajdź wywołania AJAX skojarzone z wyświetleń strony:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a>Niestandardowe śledzenia zależności
Standardowy moduł śledzenia zależności Hello automatycznie odnajduje zależności zewnętrzne, takie jak bazy danych i interfejsów API REST. Może być toobe niektóre dodatkowe składniki używane w hello sam sposób.

Można napisać kod, który wysyła informacje o zależnościach, przy użyciu hello sam [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) używany przez moduły standardowe hello.

Na przykład że nie są pisane samodzielnie, można czasu wszystkie tooit wywołania hello w przypadku tworzenia kodu z zestawem toofind się, jakie wkład ułatwia tooyour odpowiedzi czasu. toohave wysyłać te dane wyświetlane na wykresach zależności hello w usłudze Application Insights, za pomocą `TrackDependency`.

```C#

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

Tooswitch poza modułu śledzenia zależności standardowe hello, usunąć hello tooDependencyTrackingTelemetryModule odwołania w [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
*Powodzenie zależności Flaga zawsze wyświetla wartość PRAWDA lub FAŁSZ.*

*Zapytania SQL nie są wyświetlane w całości.*

* Uaktualnij toohello najnowszą wersję hello zestawu SDK. Jeśli wersja .NET jest mniejsza niż 4.6:
  * Host usługi IIS: Zainstaluj [agenta Application Insights](app-insights-monitor-performance-live-website-now.md) na serwerach hostów hello.
  * Aplikacja sieci web platformy Azure: Otwórz Application Insights w Panelu sterowania aplikacji hello w sieci web, a następnie zainstaluj usługę Application Insights.

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Następne kroki
* [Wyjątki](app-insights-asp-net-exceptions.md)
* [Dane użytkownika i strony](app-insights-javascript.md)
* [Dostępność](app-insights-monitor-web-app-availability.md)
