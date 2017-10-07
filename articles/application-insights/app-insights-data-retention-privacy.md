---
title: "aaaData przechowywania i magazynu w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Deklaracja zasad przechowywania i ochrona prywatności"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: a6268811-c8df-42b5-8b1b-1d5a7e94cbca
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: bwren
ms.openlocfilehash: 7823431d03a57db5268d2724a0604e40666009f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-collection-retention-and-storage-in-application-insights"></a>Zbieranie, przechowywanie i magazynowanie danych w usłudze Application Insights


Po zainstalowaniu [Azure Application Insights] [ start] zestawu SDK w aplikacji, wysyła dane telemetryczne dotyczące Twojej aplikacji toohello chmury. Oczywiście odpowiedzialny deweloperzy mają tooknow dokładnie przesyłanych danych, co się stanie, toohello danych i jak można zachować kontrolę nad go. W szczególności mógł zostać wysłany poufnych danych, gdzie są przechowywane i jak bezpieczne jest? 

Najpierw hello krótkich odpowiedzi:

* Moduły standardowe telemetrii Hello, systemem "fabrycznej hello" są prawdopodobnie nie toosend danych poufnych toohello usługi. dane telemetryczne Hello dotyczy obciążenia, metryki wydajności i użycia wyjątek raportów i innych danych diagnostycznych. dane użytkownika głównego Hello widoczne w raportach diagnostycznych hello są adresami URL; ale aplikacji nie powinna w każdym przypadku poufne dane w postaci zwykłego tekstu w adresie URL.
* Napisać kod, który wysyła dodatkowe telemetria niestandardowa toohelp o dane diagnostyczne i użycia monitorowania. (Rozszerzania jest doskonałym funkcji usługi Application Insights). Będzie to możliwe, przez pomyłkę, toowrite tego kodu, co zawierają one osobistych i innych poufnych danych. Jeśli aplikacja działa z takich danych, należy zastosować kompleksowy przegląd procesów tooall hello kod.
* Podczas tworzenia i testowania aplikacji, jest łatwe tooinspect, co jest wysyłane przez hello zestawu SDK. Hello dane są wyświetlane w hello hello IDE i przeglądarki w oknie danych wyjściowych debugowania. 
* dane Hello jest przechowywane w [Microsoft Azure](http://azure.com) serwerów w hello USA i Europie. (Ale aplikację można uruchomić dowolnego miejsca). Platforma Azure ma [silne zabezpieczenie przetwarza i spełnia szeroką gamę standardów zgodności](https://azure.microsoft.com/support/trust-center/). Tylko dla Ciebie i Twojego zespołu wyznaczonych mają dostęp do danych tooyour. Pracownicy firmy Microsoft mogą mieć ograniczony tooit dostępu tylko w określonych okolicznościach ograniczone z wiedzy użytkownika. Szyfrowane podczas przesyłania, ale nie w hello serwerów.

Te odpowiedzi dokładniejszego rosnącego Hello dalszej części tego artykułu. Go zostało zaprojektowane toobe autonomiczna, dzięki czemu mogą być prezentowane toocolleagues, które nie są częścią Twojego zespołu natychmiastowego.

## <a name="what-is-application-insights"></a>Co to jest usługa Application Insights?
[Azure Application Insights] [ start] jest usługa firmy Microsoft, która pomaga zwiększyć wydajność hello i użyteczność działającej aplikacji. Monitoruje aplikację cały czas hello, który jest uruchomiony podczas testowania i po jej wdrożeniu lub opublikowane. Tworzy usługi Application Insights, wykresów i tabel, których opisano, na przykład, jakich porach dnia otrzymasz większość użytkowników, jak aplikacja hello reakcji jest i jak źródło, który jest obsługiwany przez żadnych zewnętrznych usług zależy. Jeśli występują awarie, awarii lub problemów z wydajnością, można przeszukiwać dane telemetryczne hello w Przyczyna hello toodiagnose szczegółów. I usługa hello otrzymasz wiadomości e-mail w przypadku zmiany w hello dostępności i wydajności aplikacji.

W kolejności tooget tej funkcji, należy zainstalować zestaw SDK usługi Application Insights w aplikacji, która staje się częścią kodu. Po uruchomieniu aplikacji hello SDK monitoruje jego działania i wysyła usługa Application Insights toohello telemetrii. Jest to usługa w chmurze hostowana przez [Microsoft Azure](http://azure.com). (Ale usługi Application Insights działa w przypadku dowolnej aplikacji, nie tylko te, które są hostowane na platformie Azure).

![Witaj zestawu SDK w aplikacji wysyła toohello telemetrii usługi Application Insights.](./media/app-insights-data-retention-privacy/01-scheme.png)

Usługa Application Insights Hello przechowuje i analizuje dane telemetryczne hello. toosee hello analizy lub wyszukiwania za pomocą hello przechowywane dane telemetryczne, możesz zarejestrować się w tooyour konto platformy Azure i otwórz hello zasobu usługi Application Insights dla aplikacji. Można również udziału dostępu toohello danych z innych członków zespołu lub z określonej subskrybenci platformy Azure.

Masz danymi wyeksportowanymi z hello usługa Application Insights, na przykład tooa bazy danych lub tooexternal narzędzia. Specjalny klucz, który można uzyskać z usługi hello zapewnia narzędzia. w razie potrzeby można odwołać Hello klucza. 

Zestawy SDK Insights aplikacji są dostępne w różnych typów aplikacji: sieci web usług hostowanych na własnych serwerach J2EE lub ASP.NET lub w środowisku Azure. Klienci w sieci Web - oznacza to, że kod hello działający na stronie sieci web; aplikacje komputerowe i usług. aplikacje urządzenia, takie jak Windows Phone, iOS i Android. Wszystkie dane telemetryczne toohello wysyłania tej samej usługi.

## <a name="what-data-does-it-collect"></a>Jakie dane go zbiera?
### <a name="how-is-hello-data-is-collected"></a>Jak to hello dane są zbierane?
Istnieją trzy źródła danych:

* zestaw SDK, który można zintegrować z aplikacji albo Hello [do rozwoju](app-insights-asp-net.md) lub [w czasie wykonywania](app-insights-monitor-performance-live-website-now.md). Istnieją różne zestawy SDK dla aplikacji różnych typów. Istnieje również [zestawu SDK dla stron sieci web](app-insights-javascript.md), który ładuje do przeglądarki hello użytkownika końcowego oraz hello strony.
  
  * Każdy zestaw SDK zawiera szereg [moduły](app-insights-configuration-with-applicationinsights-config.md), używających różnych technik toocollect różne typy danych telemetrycznych.
  * Programowanie zainstalowaniu hello zestawu SDK, można użyć jej toosend interfejsu API własne telemetrii w modułach standardowych toohello dodanie. Ta telemetria niestandardowa może zawierać żadnych danych ma toosend.
* W niektórych serwerów sieci web są również agentów, które są uruchamiane równolegle z aplikacji hello i wysłać dane telemetryczne dotyczące Procesora, pamięci i miejsce zajmowane przez sieć. Na przykład, maszynach wirtualnych platformy Azure, hostach Docker i [serwerów J2EE](app-insights-java-agent.md) mogą mieć takich czynników.
* [Badania dostępności](app-insights-monitor-web-app-availability.md) są procesy uruchamiane przez firmę Microsoft, który wysłać aplikacji sieci web tooyour żądań w regularnych odstępach czasu. Usługa Application Insights toohello wysyłane są wyniki Hello.

### <a name="what-kinds-of-data-are-collected"></a>Jakiego rodzaju dane są zbierane?
główne kategorie Hello są:

* [Dane telemetryczne serwera w sieci Web](app-insights-asp-net.md) -żądania HTTP.  Identyfikator URI żądania hello tooprocess czas trwania, kod odpowiedzi, adres IP klienta. Identyfikator sesji.
* [Strony sieci Web](app-insights-javascript.md) -liczby stron, użytkownika i sesji. Czas ładowania strony. Wyjątki. Wywołania AJAX.
* Wydajności. liczniki — pamięci, Procesora, we/wy, miejsce zajmowane przez sieć.
* Klient i serwer kontekst — systemu operacyjnego, ustawienia regionalne, typu urządzenia, przeglądarki, rozdzielczość ekranu.
* [Wyjątki](app-insights-asp-net-exceptions.md) i awariami - **zrzuty stosu**, kompilacji identyfikator, typ Procesora. 
* [Zależności](app-insights-asp-net-dependencies.md) -wywołuje tooexternal usług, takich jak REST, SQL, AJAX. Identyfikator URI lub parametry połączenia, czas trwania, Powodzenie, polecenia.
* [Badania dostępności](app-insights-monitor-web-app-availability.md) — czas trwania testu i kroki, odpowiedzi.
* [Dzienniki śledzenia](app-insights-asp-net-trace-logs.md) i [telemetria niestandardowa](app-insights-api-custom-events-metrics.md) - **niczego kodu do dzienników lub telemetrii**.

[Więcej szczegółów](#data-sent-by-application-insights).

## <a name="how-can-i-verify-whats-being-collected"></a>Jak sprawdzić, jakie zbierane?
Jeśli projektujesz aplikacji hello przy użyciu programu Visual Studio uruchamianie aplikacji hello w trybie debugowania (F5). dane telemetryczne Hello zostanie wyświetlony w oknie danych wyjściowych hello. Z tego miejsca można skopiować go i sformatuj go jako JSON do łatwego inspekcji. 

![](./media/app-insights-data-retention-privacy/06-vs.png)

W oknie diagnostyki hello również jest bardziej przejrzysta widoku.

Dla stron sieci web Otwórz okno debugowania w przeglądarce.

![Naciśnij klawisz F12, a następnie otwórz hello karty sieciowej.](./media/app-insights-data-retention-privacy/08-browser.png)

### <a name="can-i-write-code-toofilter-hello-telemetry-before-it-is-sent"></a>Napisać kod toofilter hello telemetrii przed wysłaniem?
Będzie to możliwe pisząc [telemetrii procesora wtyczki](app-insights-api-filtering-sampling.md).

## <a name="how-long-is-hello-data-kept"></a>Jak długo są przechowywane dane hello?
Punkty danych pierwotnych (to znaczy elementy, które można kwerendy w module analiz i inspekcji w wyszukiwaniu) są przechowywane się too90 dni. Jeśli potrzebujesz danych tookeep dłuższy niż czas, możesz użyć [Eksport ciągły](app-insights-export-telemetry.md) toocopy on tooa konta magazynu.

Zagregowane dane (czyli liczby, średnie oraz innych danych statystycznych, widoczny w Eksploratorze Metryka) są przechowywane w ziarno 1 minutę przez 90 dni.

## <a name="who-can-access-hello-data"></a>Kto ma dostęp do danych hello?
Witaj, dane są widoczne tooyou i, jeśli masz konto organizacji członków zespołu. 

Można wyeksportować przez Ciebie i Twojego zespołu i może być skopiowany tooother lokalizacji i przekazywane tooother osoby.

#### <a name="what-does-microsoft-do-with-hello-information-my-app-sends-tooapplication-insights"></a>Jakie ma Microsoft zrobić informacjami hello Moja aplikacja wysyła tooApplication Insights?
Firma Microsoft używa danych hello tylko w kolejności tooprovide hello usługi tooyou.

## <a name="where-is-hello-data-held"></a>Gdzie jest przechowywana hello danych
* W hello USA lub Europy. Można wybrać lokalizację hello, podczas tworzenia nowego zasobu usługi Application Insights. 


#### <a name="does-that-mean-my-app-has-toobe-hosted-in-hello-usa-or-europe"></a>Czy oznacza to, że Moja aplikacja ma toobe hostowanych w hello USA i Europy?
* Nie. Aplikację można uruchomić dowolnego miejsca, w hostach lokalnie lub w hello chmury.

## <a name="how-secure-is-my-data"></a>Jak bezpieczne jest danych?
Usługa Application Insights jest usługą platformy Azure. Zasady zabezpieczeń są opisane w hello [Azure zabezpieczeń, prywatności i zgodności oficjalny dokument](http://go.microsoft.com/fwlink/?linkid=392408).

Witaj dane są przechowywane na serwerach Microsoft Azure. Konta w portalu Azure hello, ograniczenia konta zostały opisane w hello [Azure zabezpieczeń, prywatności i zgodności dokumentu](http://go.microsoft.com/fwlink/?linkid=392408).

Dostęp do danych tooyour przez personel firmy Microsoft jest ograniczone. Możemy uzyskać dostęp do danych tylko za zgodą użytkownika i czy jest konieczne toosupport korzystanie z usługi Application Insights. 

Dane w agregacji w aplikacjach wszystkich klientów (np. przesyłania danych i średni rozmiar śladów) są używane tooimprove Application Insights.

#### <a name="could-someone-elses-telemetry-interfere-with-my-application-insights-data"></a>Dane telemetryczne do kogoś innego może kolidować z danych usługi Application Insights?
Dodatkowe dane telemetryczne tooyour konta można wysyłania za pomocą klucza Instrumentacji hello, który można znaleźć w kodzie hello stron sieci web. Za mało dodatkowych danych Twoje metryki może nie odzwierciedlać prawidłowo wydajności i użycia aplikacji.

Jeśli współużytkujesz kodu z innych projektów Pamiętaj tooremove klucz instrumentacji.

## <a name="is-hello-data-encrypted"></a>Witaj dane są szyfrowane?
Nie znajduje się w hello serwerów w chwili obecnej.

Wszystkie dane są szyfrowane podczas przenoszenia go między centrami danych.

#### <a name="is-hello-data-encrypted-in-transit-from-my-application-tooapplication-insights-servers"></a>Jest hello dane są szyfrowane podczas przesyłania z serwerów aplikacji tooApplication Insights?
Tak, użyj portalu toohello danych toosend https z niemal wszystkich zestawów SDK, w tym serwerów sieci web, urządzeń i stron sieci web protokołu HTTPS. Jedynym wyjątkiem Hello jest dane przesyłane z zwykłych stron sieci web HTTP. 

## <a name="personally-identifiable-information"></a>Dane osobowe
#### <a name="could-personally-identifiable-information-pii-be-sent-tooapplication-insights"></a>Zidentyfikowanie informacji osobowych, mógł zostać wysłany tooApplication Insights?
Tak, jest możliwe. 

Jako ogólne wytyczne:

* Większość standardowych telemetrii (to znaczy telemetrii wysyłane bez pisania żadnego kodu) nie ma jawnego dane osobowe. Jednak może być możliwe tooidentify osób przez wnioskowania z kolekcji zdarzeń.
* Komunikaty wyjątku i śledzenia mogą zawierać dane osobowe
* Telemetria niestandardowa — to znaczy wywołań takich jak TrackEvent napisany za pomocą hello interfejsu API lub dziennika śledzenia kodu — może zawierać żadnych danych, którą wybierzesz.

Tabela Hello na końcu hello tego dokumentu zawiera bardziej szczegółowe opisy zbieranych danych hello.

#### <a name="am-i-responsible-for-complying-with-laws-and-regulations-in-regard-toopii"></a>Mogę zobowiązani do przestrzegania przepisom eksportowym obowiązującym w zakresie tooPII?
Tak. Jest tooensure Twojego odpowiedzialność, który hello zbierania i używania danych hello jest zgodny z prawami i przepisami oraz postanowień hello Microsoft Online Services.

Klientów należy odpowiednio informuje o hello dane, które zbiera dane aplikacji i używania danych hello.

#### <a name="can-my-users-turn-off-application-insights"></a>Moi użytkownicy mogą wyłączyć funkcję usługi Application Insights?
Nie bezpośrednio. Firma Microsoft nie udostępniają przełącznikiem czy użytkownicy mogą pracować tooturn wyłączanie usługi Application Insights.

Jednak taka funkcja można zaimplementować w aplikacji. Witaj wszystkie zestawy SDK obejmują ustawienia interfejsu API, która wyłącza gromadzenia danych telemetrii. 

#### <a name="my-application-is-unintentionally-collecting-sensitive-information-can-application-insights-scrub-this-data-so-it-isnt-retained"></a>Moja aplikacja przypadkowo gromadzi informacje poufne. Można usługi Application Insights usunąć te dane, nie będzie on zachowane
Usługa Application Insights nie filtru lub usuwać dane. Należy odpowiednio zarządzać danymi hello i unikanie wysyłania tooApplication takich danych szczegółowych informacji.

## <a name="data-sent-by-application-insights"></a>Dane wysyłane przez usługę Application Insights
zestawy SDK Hello różnią się między platformami i jest wiele składników, które można zainstalować. (Zobacz zbyt[usługi Application Insights — omówienie][start].) Każdy składnik wysyła innych danych.

#### <a name="classes-of-data-sent-in-different-scenarios"></a>Klasy danych przesyłanych w różnych scenariuszy
| Twoja Akcja | Klasy danych zebranych (patrz tabela dalej) |
| --- | --- |
| [Dodaj projekt sieci web .NET tooa zestaw SDK usługi Application Insights][greenbrown] |Kontekstu serwera<br/>Wywnioskowane<br/>Liczniki wydajności<br/>Żądania<br/>**Wyjątki**<br/>Sesja<br/>użytkownicy |
| [Zainstaluj Monitor stanu na serwerze IIS][redfield] |Zależności<br/>Kontekstu serwera<br/>Wywnioskowane<br/>Liczniki wydajności |
| [Dodawanie aplikacji sieci web Java tooa zestaw SDK usługi Application Insights][java] |Kontekstu serwera<br/>Wywnioskowane<br/>Żądanie<br/>Sesja<br/>użytkownicy |
| [Dodaj stronę tooweb JavaScript SDK][client] |ClientContext <br/>Wywnioskowane<br/>Strona<br/>ClientPerf<br/>AJAX |
| [Definiowanie właściwości domyślne][apiproperties] |**Właściwości** na wszystkie standardowe i niestandardowe zdarzenia |
| [Wywołanie TrackMetric][api] |Wartości numeryczne<br/>**Właściwości** |
| [Wywołanie Śledź *][api] |Nazwa zdarzenia<br/>**Właściwości** |
| [Wywołanie TrackException][api] |**Wyjątki**<br/>Zrzut stosu<br/>**Właściwości** |
| Zestaw SDK nie można zebrać danych. Na przykład: <br/> -Nie można uzyskać dostępu do liczników wydajności<br/> -wyjątku w inicjatorze telemetrii |Diagnostyka zestawu SDK |

Aby uzyskać [zestawy SDK dla innych platform][platforms], zobacz swoje dokumenty.

#### <a name="hello-classes-of-collected-data"></a>klasy Hello zebranych danych
| Klasa zebranych danych | Obejmuje (nie stanowi wyczerpującej listy) |
| --- | --- |
| **Właściwości** |**Wszystkie dane - ustaleniami kodu** |
| DeviceContext |Identyfikator, adresu IP, ustawienia regionalne, model urządzenia, sieci, typ sieci, nazwa producenta OEM, rozdzielczość ekranu wystąpienia roli, nazwa roli, typu urządzenia |
| ClientContext |System operacyjny, ustawienia regionalne, języka, sieci, rozdzielczość okna |
| Sesja |Identyfikator sesji |
| Kontekstu serwera |Nazwa komputera, ustawienia regionalne, systemu operacyjnego, urządzenia, sesji użytkownika, kontekst użytkownika, operacji |
| Wywnioskowane |Lokalizacja geograficzna z adresu IP, timestamp, systemu operacyjnego, przeglądarki |
| Metryki |Nazwa metryki i wartości |
| Zdarzenia |Nazwa zdarzenia i wartości |
| PageViews |Nazwa adresu URL i strony lub ekranu |
| Wydajności klienta |Nazwa adresu URL/strony, czas ładowania przeglądarki |
| AJAX |Połączenia HTTP z tooserver strony sieci web |
| Żądania |Adres URL, czas trwania, kod odpowiedzi |
| Zależności |Typ (SQL, HTTP,...), parametry połączenia lub identyfikator URI, synchronizacji/asynchroniczne, czas trwania, Powodzenie, instrukcji SQL (za pomocą Monitora stanu) |
| **Wyjątki** |Typ, **komunikat**, stosy wywołań, plików i wierszy number, identyfikator wątku źródła |
| Awarii (Crash) |Identyfikator procesu, identyfikator procesu nadrzędnego, identyfikator wątku awarii; poprawka aplikacji, identyfikator kompilacji;  Typ wyjątku, adres, reason; symbole zaciemnionego i rejestrów, binarne początkowy i końcowy adres, nazwa pliku binarnego i ścieżki, typ procesora |
| Ślad |**Komunikat** i poziom ważności |
| Liczniki wydajności |Czas procesora, pamięci, liczby żądań, stawki wyjątek, bajtów prywatnych procesu, stawki we/wy, czas trwania żądania, długość kolejki żądań |
| Dostępność |Kod odpowiedzi testu sieci Web, czas trwania każdego kroku testu, nazwa testu, timestamp, Powodzenie, czas odpowiedzi, lokalizacji testu |
| Diagnostyka zestawu SDK |Komunikat śledzenia lub wyjątku |

Możesz [wyłącz niektóre dane hello ApplicationInsights.config edycji][config]

## <a name="credits"></a>Środki na korzystanie z
Ten produkt zawiera GeoLite2 dane utworzone przez MaxMind dostępnej w sklepie [http://www.maxmind.com](http://www.maxmind.com).



<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[client]: app-insights-javascript.md
[config]: app-insights-configuration-with-applicationinsights-config.md
[greenbrown]: app-insights-asp-net.md
[java]: app-insights-java-get-started.md
[platforms]: app-insights-platforms.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md

