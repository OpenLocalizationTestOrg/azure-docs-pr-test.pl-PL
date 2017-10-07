---
title: "aaaAzure Application Insights — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące usługi Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0e3b103c-6e2a-4634-9e8c-8b85cf5e9c84
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: e27ee9b7d040a04828a9892865a6681b83f94326
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-frequently-asked-questions"></a>Usługa Application Insights: Często zadawane pytania

## <a name="configuration-problems"></a>Problemy z konfiguracją
*Mam problemy ustawienie mojej:*

* [Aplikacja .NET](app-insights-asp-net-troubleshoot-no-data.md)
* [Monitorowanie aplikacji już uruchomione](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)
* [Diagnostyka Azure](app-insights-azure-diagnostics.md)
* [Aplikacje sieci Web w języku Java](app-insights-java-troubleshoot.md)

*Pobrać żadnych danych z serwerem*

* [Wyjątki zapory zestawu](app-insights-ip-addresses.md)
* [Konfigurowanie serwera ASP.NET](app-insights-monitor-performance-live-website-now.md)
* [Konfigurowanie serwera Java](app-insights-java-agent.md)

## <a name="can-i-use-application-insights-with-"></a>Czy za pomocą usługi Application Insights z...?

* [Aplikacje sieci Web na serwerze IIS — lokalnie lub na maszynie wirtualnej](app-insights-asp-net.md)
* [Aplikacje sieci web Java](app-insights-java-get-started.md)
* [Aplikacje Node.js](app-insights-nodejs.md)
* [Aplikacje sieci Web na platformie Azure](app-insights-azure-web-apps.md)
* [Usługi w chmurze na platformie Azure](app-insights-cloudservices.md)
* [Serwery aplikacji uruchomionych w Docker](app-insights-docker.md)
* [Aplikacje jednej strony sieci web](app-insights-javascript.md)
* [Program SharePoint](app-insights-sharepoint.md)
* [Aplikacji klasycznej systemu Windows](app-insights-windows-desktop.md)
* [Inne platformy](app-insights-platforms.md)

## <a name="is-it-free"></a>Jest bezpłatny?

Tak, użyj eksperymentalne. W hello podstawowe ceny planu aplikację można wysyłać niektórych dodatku danych miesięcznie bezpłatnie. Dodatek wolnego Hello jest wystarczająco duży toocover projektowanie i publikowanie aplikacji dla niewielkiej liczby użytkowników. Można ustawić tooprevent zakończenia ponad określona ilość danych z przetwarzane.

Większych ilości danych telemetrycznych są naliczane za hello Gb. Udostępniamy porady na temat zbyt[ograniczyć Twojej opłat](app-insights-pricing.md).

Hello Enterprise plan wiąże opłat codziennie każdego węzła serwera sieci web wysyła dane telemetryczne. Jest on odpowiedni, jeśli chcesz, aby toouse eksportu ciągłego na dużą skalę.

[Cennik planu hello odczytu](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="how-much-is-it-costing"></a>Jaka jest wyceny?

* Otwórz hello **funkcje + cennik** strony w zasobu usługi Application Insights. Brak wykres ostatnie informacje o użyciu. Ograniczenie wolumin danych, można ustawić, jeśli chcesz.
* Otwórz hello [bloku rozliczenia Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade/Overview) toosee rachunków we wszystkich zasobów.

## <a name="q14"></a>Co to usługa Application Insights zmodyfikować w projekcie?
Szczegóły Hello są zależne od typu hello projektu. Dla aplikacji sieci web:

* Dodaje projekt tooyour tych plików:

  * ApplicationInsights.config.
  * AI.js
* Instaluje te pakiety NuGet:

  * *Interfejsu API usługi Application Insights* — Witaj podstawowe interfejsu API
  * *Interfejsu API usługi Application Insights dla aplikacji sieci Web* — używane dane telemetryczne toosend z powitania serwera
  * *Aplikacja interfejsu API Insights dla aplikacji JavaScript* — używane dane telemetryczne toosend z powitania klienta

    pakiety Hello zawierają te zestawy:
  * Microsoft.ApplicationInsights
  * Microsoft.ApplicationInsights.Platform
* Wstawia elementy do:

  * Web.config
  * pliku Packages.config
* (Nowe projekty tylko — jeśli możesz [Dodaj istniejący projekt tooan usługi Application Insights][start], trzeba toodo to ręcznie.) Wstawia wstawki na powitania klienta i serwera tooinitialize kodu z hello usługi Application Insights z identyfikatorem zasobu. Na przykład w aplikacji MVC kodu zostaną wstawione do strony głównej hello Views/Shared/_Layout.cshtml

## <a name="how-do-i-upgrade-from-older-sdk-versions"></a>Jak uaktualnić ze starszych wersji zestawu SDK?
Zobacz hello [informacje o wersji](app-insights-release-notes.md) dla hello SDK odpowiednie tooyour typu aplikacji.

## <a name="update"></a>Jak zmienić projektu wysyła dane do zasobów platformy Azure?
W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy `ApplicationInsights.config` i wybierz polecenie **usługi Application Insights dla aktualizacji**. Na platformie Azure, możesz wysłać hello danych tooan istniejącego lub nowego zasobu. zmiany w Kreatorze aktualizacji Hello hello klucza Instrumentacji w ApplicationInsights.config, która określa, gdzie serwer hello SDK wysyła dane. Jeśli nie możesz usunąć zaznaczenie "Aktualizuj wszystkie", spowoduje również zmianę klucza hello, gdzie jest dostępny na stronach sieci web.

## <a name="what-is-status-monitor"></a>Co to jest monitor stanu?

Aplikacja klasyczna, używanego w Twojej toohelp serwera sieci web usług IIS Konfiguruj usługę Application Insights w aplikacjach sieci web. Nie zbieraj danych telemetrii: zostanie ona zatrzymana, gdy nie konfigurujesz aplikacji. 

[Dowiedz się więcej](app-insights-monitor-performance-live-website-now.md#questions).

## <a name="what-telemetry-is-collected-by-application-insights"></a>Jakie dane telemetryczne są zbierane przez usługę Application Insights?

Z aplikacji sieci web serwera:

* Żądania HTTP
* [Zależności](app-insights-asp-net-dependencies.md). Wywołania: baz danych; HTTP wywołuje tooexternal usługi; Azure DB rozwiązania Cosmos, tabeli magazynu obiektów blob i kolejki. 
* [Wyjątki](app-insights-asp-net-exceptions.md) i ślady stosu.
* [Liczniki wydajności](app-insights-performance-counters.md) — Jeśli używasz [Monitor stanu](app-insights-monitor-performance-live-website-now.md), Azure monitoring(app-insights-azure-web-apps.md) lub hello [zapisywania collectd usługi Application Insights](app-insights-java-collectd.md).
* [Niestandardowe zdarzenia i metryki](app-insights-api-custom-events-metrics.md) czy kodu.
* [Dzienniki śledzenia](app-insights-asp-net-trace-logs.md) skonfigurowania hello odpowiedniego modułu zbierającego.

Z [stron sieci web klienta](app-insights-javascript.md):

* [Zlicza widoku strony](app-insights-web-track-usage.md)
* [Wywołania AJAX](app-insights-asp-net-dependencies.md) żądań z uruchamianie skryptu.
* Dane ładowania stron widoku
* Liczba użytkowników i sesji
* [Uwierzytelniony użytkownik identyfikatorów](app-insights-api-custom-events-metrics.md#authenticated-users)

Z innych źródeł, jeśli je skonfigurować:

* [Diagnostyka Azure](app-insights-azure-diagnostics.md)
* [Kontenery docker](app-insights-docker.md)
* [Importuj tabele tooAnalytics](app-insights-analytics-import.md)
* [OMS (Log Analytics)](https://azure.microsoft.com/blog/omssolutionforappinsightspublicpreview/)
* [Logstash](app-insights-analytics-import.md)

## <a name="can-i-filter-out-or-modify-some-telemetry"></a>Można odfiltrować lub zmodyfikować niektóre telemetrii?

Tak, na serwerze hello można napisać:

* Dane telemetryczne toofilter procesora lub Dodaj elementy telemetrii tooselected właściwości przed ich wysłaniem z aplikacji.
* Dane telemetryczne inicjatora tooadd właściwości tooall elementów telemetrii.

Dowiedz się więcej na [ASP.NET](app-insights-api-filtering-sampling.md) lub [Java](app-insights-java-filter-telemetry.md).

## <a name="how-are-city-country-and-other-geo-location-data-calculated"></a>Sposób Miasto, kraj i innych danych lokalizacji geo obliczania?

Możemy odszukać hello adres IP (IPv4 lub IPv6) powitania klienta sieci web przy użyciu [GeoLite2](http://dev.maxmind.com/geoip/geoip2/geolite2/).

* Dane telemetryczne przeglądarki: zbieramy hello adres IP komputera.
* Dane telemetryczne serwera: adres IP klienta hello zbiera hello modułu usługi Application Insights. Nie są zbierane, jeśli `X-Forwarded-For` jest ustawiona.

Można skonfigurować hello `ClientIpHeaderTelemetryInitializer` tootake adres IP hello z innej nagłówka. W niektórych systemach, na przykład jest przenoszony przez serwer proxy, należy załadować równoważenia lub CDN zbyt`X-Originating-IP`. [Dowiedz się więcej](http://apmtips.com/blog/2016/07/05/client-ip-address/).

Możesz [przy użyciu usługi Power BI](app-insights-export-power-bi.md) toodisplay telemetrii żądania na mapie.


## <a name="data"></a>Jak długo dane są przechowywane w portalu hello? Czy jest bezpieczna?
Spójrz na [przechowywanie danych i ochrona prywatności][data].

## <a name="might-personally-identifiable-information-pii-be-sent-in-hello-telemetry"></a>Identyfikowalne dane osobowe (dane osobowe) zostaną wysłane dane telemetryczne hello?

Jest to możliwe, jeśli takie dane są wysyłane kodu. Możliwe również, czy zmienne w śladów stosu zawierają dane osobowe. Zespół deweloperów należy przeprowadzić tooensure oceny ryzyka poprawną obsługę dane osobowe. [Dowiedz się więcej o przechowywanie danych i ochrony prywatności](app-insights-data-retention-privacy.md).

ostatni oktet Hello powitania klienta sieci web adresu ma zawsze wartość too0 po wprowadzanie przez hello portal.

## <a name="my-ikey-is-visible-in-my-web-page-source"></a>Moje iKey jest widoczna w źródle strony sieci web. 

* To jest typowym rozwiązaniem w monitorowanie rozwiązań.
* Go nie może być toosteal używanych danych.
* Go może być używane tooskew alerty danych lub wyzwalacza.
* Firma Microsoft nie podano miał żadnych odbiorca takich problemów.

Można:

* Dwa oddzielne iKeys (oddzielnie zasobów usługi Application Insights), należy użyć danych klienta i serwera. Lub
* Napisz serwer proxy, który jest uruchamiany na serwerze, a powitania klienta sieci web przesyłania danych za pośrednictwem tego serwera proxy.

## <a name="post"></a>Jak wyświetlić dane POST w wyszukiwaniu diagnostyczne?
Dane POST nie rejestrowane automatycznie, ale może użyć wywołania TrackTrace: umieszczanie danych hello w parametrze wiadomość hello. Ma ograniczenie dłużej niż limity hello właściwości ciągów, chociaż nie można filtrować na nim.

## <a name="should-i-use-single-or-multiple-application-insights-resources"></a>Należy użyć jednego lub wielu zasobów usługi Application Insights?

Użyj pojedynczego zasobu dla wszystkich składników hello lub ról w systemie biznesowej. Rozwoju, testów oraz wersji i niezależnie od aplikacji należy używać oddzielnych zasobów.

* [Zobacz opis hello tutaj](app-insights-separate-resources.md)
* [Przykład — usługa w chmurze z rolami sieci web i proces roboczy](app-insights-cloudservices.md)

## <a name="how-do-i-dynamically-change-hello-instrumentation-key"></a>Jak dynamicznie zmienić klucza Instrumentacji hello?

* [Omówienie tutaj](app-insights-separate-resources.md)
* [Przykład — usługa w chmurze z rolami sieci web i proces roboczy](app-insights-cloudservices.md)

## <a name="what-are-hello-user-and-session-counts"></a>Co to są hello użytkownika i sesji liczby?

* Witaj JavaScript SDK ustawia plik cookie użytkownika na powitania klienta sieci web, tooidentify zwracająca użytkowników i działania toogroup pliku cookie sesji.
* Jeśli nie ma żadnego skryptu po stronie klienta, możesz [umieszczania plików cookie na serwerze hello](http://apmtips.com/blog/2016/07/09/tracking-users-in-api-apps/).
* Jeśli jeden rzeczywistych użytkownik korzysta z witryną w różnych przeglądarkach, albo za pomocą przeglądania w prywatnego/incognito lub różnych komputerach, a następnie ich będzie zliczenia więcej niż raz.
* tooidentify zalogowanego użytkownika wiele maszyn i przeglądarki, dodaj wywołanie za[setAuthenticatedUserContect()](app-insights-api-custom-events-metrics.md#authenticated-users).

## <a name="q17"></a>I włączono wszystko w usłudze Application Insights?
| Należy wyświetlić | Jak tooget go | Dlaczego chcesz |
| --- | --- | --- |
| Wykresy dostępności |[Testy sieci Web](app-insights-monitor-web-app-availability.md) |Wiedzieć, że aplikacja sieci web |
| Wydajności aplikacji serwera: czas reakcji... |[Dodawanie projektu usługi Application Insights tooyour](app-insights-asp-net.md) lub [Zainstaluj Monitor stanu AI na serwerze](app-insights-monitor-performance-live-website-now.md) (lub napisać własny kod zbyt[śledzić zależności](app-insights-api-custom-events-metrics.md#trackdependency)) |Wykryj problemy dotyczące wydajności |
| Dane telemetryczne zależności |[Zainstaluj Monitor stanu usługi AI na serwerze](app-insights-monitor-performance-live-website-now.md) |Diagnozowanie problemów z bazy danych lub innych składników zewnętrznych |
| Uzyskanie śladów stosu wyjątków |[Wstawianie wywołania TrackException w kodzie](app-insights-asp-net-exceptions.md) (ale niektóre są raportowane automatycznie) |Wykrywanie i diagnozowanie wyjątków |
| Ślady dziennika wyszukiwania |[Dodaj kartę rejestrowania](app-insights-asp-net-trace-logs.md) |Diagnozowanie wyjątków, problemy dotyczące wydajności |
| Podstawowe informacje dotyczące użycia klienta: wyświetleń strony, sesje,... |[Inicjator JavaScript na stronach sieci web](app-insights-javascript.md) |Analiza użycia |
| Metryki niestandardowe klienta |[Śledzenie wywołuje na stronach sieci web](app-insights-api-custom-events-metrics.md) |Ulepszanie środowiska użytkownika |
| Metryki niestandardowe serwera |[Śledzenie wywołań serwera](app-insights-api-custom-events-metrics.md) |Analiza biznesowa |

## <a name="why-are-hello-counts-in-search-and-metrics-charts-unequal"></a>Dlaczego są hello liczby wykresach wyszukiwania i metryki nierówne?

[Próbkowanie](app-insights-sampling.md) zmniejsza liczbę hello elementów telemetrii (żądania, niestandardowych zdarzeń itd.), które faktycznie są wysyłane z portalem toohello aplikacji. W wyszukiwaniu zostanie wyświetlony hello liczba elementów w rzeczywistości odebrane. Na wykresach metryki, które wyświetla liczbę zdarzeń zostanie wyświetlony hello liczba oryginalnego zdarzenia, które wystąpiły. 

Każdy element, który jest posiada transmmitted `itemCount` reprezentuje właściwość, która zawiera liczbę zdarzeń oryginalnego elementu. tooobserve pobierania próbek w operacji, można uruchomić tej kwerendy w module analiz:

```
    requests | summarize original_events = sum(itemCount), transmitted_events = count()
```


## <a name="automation"></a>Automatyzacja

### <a name="configuring-application-insights"></a>Konfigurowanie usługi Application Insights

Możesz [pisanie skryptów PowerShell](app-insights-powershell.md) za pomocą Monitora zasobów platformy Azure do:

* Tworzenie i aktualizowanie zasobów usługi Application Insights.
* Ustaw hello cenową planu.
* Pobierz klucz Instrumentacji hello.
* Dodawanie metryki alertu.
* Dodaj test dostępności.

Nie można skonfigurować raportu metryki Explorer lub ustawienie Eksport ciągły.

### <a name="querying-hello-telemetry"></a>Wykonywanie zapytania hello telemetrii

Użyj hello [interfejsu API REST](https://dev.applicationinsights.io/) toorun [Analytics](app-insights-analytics.md) zapytania.

## <a name="how-can-i-set-an-alert-on-an-event"></a>Jak ustawić alert na zdarzenia?

Azure alerty są tylko dla metryki. Utwórz niestandardową metrykę przecina wartości progowej, przy każdym wystąpieniu wydarzenia. Następnie należy ustawić alert na powitania metryki. Należy pamiętać, że: otrzymasz powiadomienie, zawsze, gdy metryki hello przekracza próg hello w żadnym kierunku; użytkownik nie będzie otrzymywał powiadomienia do hello pierwszy przecięcia, niezależnie od tego, czy wartość początkowa hello jest wysokie lub niskie; jest zawsze opóźnienie za kilka minut.

## <a name="are-there-data-transfer-charges-between-an-azure-web-app-and-application-insights"></a>Czy istnieją opłat za transfer danych między aplikacją sieci web platformy Azure i usługi Application Insights?

* Jeśli aplikacja sieci Azure web znajduje się w centrum danych w przypadku punktu końcowego zbierania danych usługi Application Insights jest bez dodatkowych opłat. 
* Jeśli istnieje żaden punkt końcowy z kolekcji w centrum danych hosta, a następnie telemetrii aplikacji będą naliczane [Azure wychodzące opłat](https://azure.microsoft.com/pricing/details/bandwidth/).

To nie jest zależny od gdzie jest hostowana zasobu usługi Application Insights. Zależy tylko dystrybucji hello naszych punktów końcowych.

## <a name="can-i-send-telemetry-toohello-application-insights-portal"></a>Czy można wysłać portalu Application Insights toohello telemetrii?

Firma Microsoft zaleca, możesz użyć nasze zestawy SDK i użyć hello interfejsu API zestawu SDK (app-insights-api-custom-events-metrics.md). Istnieje wariantów hello zestawu SDK dla różnych [platform](app-insights-platforms.md). Te zestawy SDK obsługuje buforowanie, kompresji, ograniczania przepustowości, ponownych prób i tak dalej. Jednak hello [schematu wprowadzanie](https://github.com/Microsoft/ApplicationInsights-dotnet/tree/develop/Schema/PublicSchema) i [punktu końcowego protokołu](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/ENDPOINT-PROTOCOL.md) są publiczne.

## <a name="can-i-monitor-an-intranet-web-server"></a>Można monitorować intranetowego serwera sieci web?

Poniżej przedstawiono dwie metody:

### <a name="firewall-door"></a>Drzwi zapory

Zezwalaj na sieci web server toosend telemetrii tooour punkty końcowe https://dc.services.visualstudio.com:443 i https://rt.services.visualstudio.com:443. 

### <a name="proxy"></a>Serwer proxy

Kierować ruchem z serwera bramy tooa w intranecie, ustawiając to ApplicationInsights.config:

```XML
<TelemetryChannel>
    <EndpointAddress>your gateway endpoint</EndpointAddress>
</TelemetryChannel>
```

Bramy należy kierować ruchu hello toohttps://dc.services.visualstudio.com:443/v2/ścieżki

## <a name="can-i-run-availability-web-tests-on-an-intranet-server"></a>Na serwerze sieci intranet można uruchomić testów sieci web dostępności?

Nasze [testów sieci web](app-insights-monitor-web-app-availability.md) uruchomić w punktach obecności, które są dystrybuowane w całym Witaj świecie. Istnieją dwa rozwiązania:

* Zapory drzwi — Zezwalaj na żądania serwera tooyour z [hello długie i zmienić listę web agenci testowi](app-insights-ip-addresses.md).
* Napisać własny kod toosend żądań okresowych tooyour serwer z wewnątrz sieci intranet. Można uruchomić testów sieci web programu Visual Studio, w tym celu. Hello tester może wysłać wyniki hello Insights tooApplication przy użyciu hello TrackAvailability() interfejsu API.

## <a name="more-answers"></a>Więcej odpowiedzi
* [Application Insights forum](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

<!--Link references-->

[data]: app-insights-data-retention-privacy.md
[platforms]: app-insights-platforms.md
[start]: app-insights-overview.md
[windows]: app-insights-windows-get-started.md
