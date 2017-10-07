---
title: "Monitorowanie wydajności aplikacji aaaWeb - Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Jak usługi Application Insights dopasowuje się do hello cyklu opracowywania oprogramowania"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 479522a9-ff5c-471e-a405-b8fa221aedb3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: bba2d6c59de1794adcbf8e298d0ef4f0dbaa700f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deep-diagnostics-for-web-apps-and-services-with-application-insights"></a>Szczegółowa diagnostyka dla aplikacji sieci Web i usług dzięki usłudze Application Insights
## <a name="why-do-i-need-application-insights"></a>Dlaczego muszę usługi Application Insights?
Usługa Application Insights monitoruje uruchomionej aplikacji sieci web. Informuje o awarii i problemy z wydajnością i pomaga analizować, jak klienci korzystają z aplikacji. Ponieważ działa aplikacji działających na wiele platform (ASP.NET, J2EE, Node.js,...) i znajduje się w chmurze hello lub lokalnymi. 

![Aspekty hello złożoności opracowywania aplikacji sieci web](./media/app-insights-devops/010.png)

Jest ważne toomonitor nowoczesnych aplikacji jest uruchomiona. Przede wszystkim ma błędy toodetect wcześniej większość klientów. Również mają toodiscover i rozwiązywanie problemów z wydajnością, które, gdy nie krytycznego, być może spowolnić rzeczy lub powodować pewne niedogodności tooyour użytkowników. I przeprowadzania systemu hello jest zadowalającym tooyour, ma tooknow robią użytkownicy hello z nim: są one przy użyciu najnowszych funkcji hello? Są one pomyślne z nim?

Nowoczesnych aplikacji sieci web są tworzone w cyklu ciągłego dostarczania: wydania nowej funkcji lub ulepszenia; Sprawdź, jak działa hello użytkowników. Zaplanuj hello kolejny krok Programowanie oparte na wiedzy. Część klucza cyklu jest hello obserwacji fazy. Usługa Application Insights udostępnia hello narzędzia toomonitor aplikacji sieci web, wydajności i użycia.

Najważniejszym aspektem Hello tego procesu jest diagnostyki i diagnostyki. W przypadku niepowodzenia aplikacji hello firm są są tracone. podstawową rolą Hello monitorowania Framework dlatego błędów toodetect niezawodnie, powiadomi możesz od razu i toopresent hello informacje potrzebne toodiagnose hello problem. Jest to dokładnie, czego usługi Application Insights.

### <a name="where-do-bugs-come-from"></a>Skąd pochodzą usterki?
Awarie w sieci web systemów wynikają zwykle z powodu problemów z konfiguracją lub zły interakcje między ich wiele składników. Hello pierwszego zadania podczas działania zdarzenia na żywo lokacji w związku z tym jest locus hello tooidentify problemu hello: które składnika lub relacji jest przyczyną hello?

Niektórzy, z szarym włosów do zapamiętania ery prostsze, w którym program komputerowy były uruchamiane w jednym komputerze. Deweloperzy Hello może przetestować go dokładnie przed wysłaniem i o wysłane, czy Zobacz lub rzadko traktować go ponownie. Użytkownicy Hello musi tooput z usterkami pozostałych hello przez wiele lat. 

Dlatego bardzo różnią się teraz rzeczy. Aplikacja ma nadmiar toorun różnych urządzeń i może być trudne tooguarantee hello dokładnie takie samo zachowanie na każdej z nich. Hosting aplikacji w chmurze hello oznacza fast można naprawić błędy, ale oznacza to również ciągłego konkurencji i hello oczekiwania dotyczące nowych funkcji w częstych odstępach czasu. 

W tych warunkach hello tylko tookeep sposób ostateczne formantu liczba błędów hello jest automatyczne testy jednostkowe. Nie można wysyłać toomanually ponownie wszystko co pobraniem testu. Testu jednostkowego jest teraz częścią popularne hello proces kompilacji. Narzędzia, takie jak hello chmury testowej Xamarin pomaga, zapewniając automatyczne interfejsu użytkownika, testów na wielu wersji przeglądarki. Umożliwiają one testowania systemów, nam toohope ta stawka hello usterki znajduje się w aplikacji można przechowywać tooa minimalne.

Aplikacje sieci web typowe ma wiele składników na żywo. Dodanie toohello klienta (w aplikacji przeglądarki lub urządzenia) i serwera sieci web hello jest prawdopodobnie toobe przetwarzania znacznej wewnętrznej bazy danych. Prawdopodobnie hello wewnętrznej bazy danych jest potoku składników lub zbiór im brać części. I wiele z nich nie będzie formantu — są one usług zewnętrznych, na których jest zależna.

W konfiguracji, takich jak te on być trudny i uneconomical tootest, lub przewiduje się, co trybu awaryjnego możliwe, inne niż w hello na żywo sam system. 

### <a name="questions-"></a>Pytania...
Pytaniami poprosimy, gdy jest tworzenie system sieci web:

* Moja aplikacja awarii 
* Dokładnie naturę? — Jeśli go nie powiodło się żądanie ma tooknow jak uzyskano istnieje. Potrzebujemy śledzenia zdarzeń...
* Czy Moja aplikacja tyle szybko? Jak długo trwa żądań tootypical toorespond?
* Witaj Witaj dojścia serwera można załadować? Gdy hello liczba żądań wzrośnie, ma czas odpowiedzi hello praw stałą?
* Stopień reakcji są moje zależności - hello interfejsów API REST, baz danych i innymi składnikami, które wywołuje Moja aplikacja. W szczególności hello system przebiega powoli, jest mój składnik, czy otrzymuję powolne odpowiedzi od kogoś innego?
* Jest Moja aplikacja w górę lub w dół? Można go zobaczyć wokół Witaj świecie? Powiadom mnie, jeśli zatrzymuje...
* Co to jest hello głównej przyczyny? Był błąd hello w mojej składnika lub zależność? Jest to problem komunikacji?
* Wpływ na ilu użytkowników? Jeśli jest ma więcej niż jeden tootackle problem, który jest hello najważniejszych?

## <a name="what-is-application-insights"></a>Co to jest usługa Application Insights?
![Podstawowy przepływ pracy z usługi Application Insights](./media/app-insights-devops/020.png)

1. Usługa Application Insights instruments aplikacji i wysyła dane telemetryczne dotyczące jej aplikacji hello jest uruchomiona. Można tworzyć hello zestaw SDK usługi Application Insights do aplikacji hello albo można zastosować Instrumentacji w czasie wykonywania. Hello pierwszej metody jest bardziej elastyczne, jak dodać własne moduły regularne toohello telemetrii.
2. dane telemetryczne Hello są wysyłane toohello portalu Application Insights, gdzie są przechowywane i przetwarzane. (Mimo że usługi Application Insights jest hostowana na platformie Microsoft Azure, może monitorować wszystkich aplikacji sieci web — nie tylko Azure aplikacji).
3. dane telemetryczne Hello są prezentowane tooyou w formie hello wykresów i tabel zdarzeń.

Istnieją dwa główne rodzaje danych telemetrii: wystąpień zagregowane i raw. 

* Na przykład dane wystąpienia obejmuje raportu żądania, które zostały odebrane przez aplikację sieci web. Można znaleźć i sprawdzić szczegóły hello żądania przy użyciu narzędzia wyszukiwania hello w portalu usługi Application Insights hello. wystąpienie Hello będzie zawierać dane, takie jak czas aplikacji trwało toorespond toohello żądania, a także hello żądanego adresu URL, przybliżonej lokalizacji powitania klienta i innych danych.
* Zagregowane dane obejmuje liczby zdarzeń na jednostkę czasu, tak, aby można było porównać hello stopień żądań z hello czasy odpowiedzi. Obejmuje on też średnie metryk, takich jak czas odpowiedzi na żądanie.

główne kategorie Hello danych są:

* Żądania tooyour aplikacji (zwykle żądań HTTP), z danymi na adres URL, czas odpowiedzi i powodzenie lub niepowodzenie.
* Zależności - SQL i REST wywołań przez aplikację, a także z identyfikatora URI, czas reakcji i Powodzenie
* Wyjątki, w tym śladów stosu.
* Dane widoku strony pochodzące z przeglądarek hello użytkowników.
* Metryki, np. liczniki wydajności, a także metryki pisania samodzielnie. 
* Niestandardowe zdarzenia służy tootrack zdarzeń biznesowych
* Ślady dziennika używane do debugowania.

## <a name="case-study-real-madrid-fc"></a>— Analiza przypadków: F.C. rzeczywistych Madrycie
Witaj usługi sieci web [rzeczywistych klub Football Madrycie](http://www.realmadrid.com/) służy wentylatory około 450 milionów wokół hello world. Wentylatory dostęp zarówno za pośrednictwem przeglądarki sieci web i aplikacji mobilnych firmy klub hello. Wentylatory można nie tylko zarezerwować biletów, ale także uzyskać dostęp do informacji i wideo klipy na wyniki, odtwarzaczach i gry nadchodzących. Mogą one wyszukiwania z filtrami, takie jak numery celów oceny. Dostępne są także linki toosocial nośnika. środowisko użytkownika Hello jest wysoce spersonalizowanych i został zaprojektowany jako wentylatory tooengage dwukierunkowej komunikacji.

Witaj rozwiązania [to system usług i aplikacji w systemie Microsoft Azure](https://www.microsoft.com/en-us/enterprise/microsoftcloud/realmadrid.aspx). Skalowalność to decydujące znaczenie: ruch jest zmienną i mogą dotrzeć bardzo dużej ilości, podczas i wokół dopasowań.

Rzeczywiste madryckiego jest wydajność najważniejszych toomonitor hello systemu. Azure Application Insights udostępnia obszerne przez hello system, zapewniając niezawodne i wysoki poziom usług. 

Hello klub również pobiera szczegółowy opis jego wentylatorów: gdy są one (w Hiszpanii są tylko % 3), jakie odsetek mają w odtwarzaczy, historycznych wyniki i gry nadchodzących i jak one odpowiadać toomatch wyników.

Większość tych danych telemetrycznych automatycznie są zbierane z nie dodano kod, który uproszczone rozwiązanie hello i zmniejszyć złożoność działania.  Rzeczywiste Madryt, usługi Application Insights zajmuje się punkty telemetrii MLD 3.8 każdego miesiąca.

Rzeczywiste Madrycie używa tooview modułu usługi Power BI hello ich telemetrii.

![Power BI widok telemetrii usługi Application Insights](./media/app-insights-devops/080.png)

## <a name="smart-detection"></a>Wykrywanie inteligentne
[Proaktywna Diagnostyka](app-insights-proactive-diagnostics.md) jest funkcją ostatnie. Bez żadnej specjalnej konfiguracji przez użytkownika usługi Application Insights automatycznie wykrywa i ostrzega o nietypowych wzrostu w awariami w aplikacji. Jest wystarczająco inteligentne tooignore tła sporadycznych błędów, a także wzrostu, które są po prostu współmierne tooa wzrost żądania. Tak na przykład w przypadku awarii jednego hello usług, które zależą od lub jeśli hello nowej kompilacji można wdrożyć tylko nie działa tak dobrze, a następnie będzie wiadomo o nim, jak przyjrzeć się poczty e-mail. (I istnieją elementów webhook, dzięki czemu możesz wyzwolić innych aplikacji.)

Innym aspektem tej funkcji wykonuje codzienne dokładnych analiz telemetrii, wyszukiwanie nietypowe wzorce wydajności, które są toodiscover twardych. Na przykład może znaleźć wydajności skojarzonego z określonym obszarze geograficznym lub w wersji przeglądarki.

W obu przypadkach hello alert informuje nie tylko hello objawy okaże się, ale również zapewnia dane, które należy toohelp zdiagnozowaniu hello problem, takie jak raporty odpowiedni wyjątek.

![Wiadomości e-mail z proaktywna Diagnostyka](./media/app-insights-devops/030.png)

Samtec klienta powiedzieć: "podczas ostatnie funkcji cutover znaleziono-skalowania bazy danych naciśnięcie limit zasobów i powoduje przekroczeń limitu czasu. Alerty o wykryciu aktywnego dostarczone dosłownie anonsowanej możemy zostały klasyfikowane problem hello, bardzo blisko czasu rzeczywistego. Ten alert w połączeniu z alertami platformy Azure hello pomogły niemal natychmiast rozwiązać problem hello. Łączny czas przestojów spowodowanych < 10 minut."

## <a name="live-metrics-stream"></a>Metryki strumień na żywo
Wdrażanie hello ostatniej kompilacji może być trosce środowisko. Jeśli występują problemy, mają tooknow o nich od razu, aby można Wycofaj w razie potrzeby. Strumień na żywo metryk umożliwia kluczowych metryk z opóźnieniem około jednej sekundy.

![Metryki na żywo](./media/app-insights-devops/040.png)

I pozwala bezpośrednio sprawdzić przykładowe jakiekolwiek błędy lub wyjątki.

![Zdarzenia błędów na żywo](./media/app-insights-devops/live-stream-failures.png)

## <a name="application-map"></a>Mapa aplikacji
Mapowanie aplikacji automatycznie odnajduje topologii aplikacji r. hello informacje o wydajności na nim toolet łatwo zidentyfikować wąskich gardeł zmniejszających wydajność i przepływów powodować problemy w środowisku rozproszonym. Pozwala ona toodiscover zależności aplikacji w usługach Azure. Możesz klasyfikowanie hello problem opis, jeśli jest związane z kodu lub zależności powiązane i z jednego miejsca Przechodzenie do szczegółów w powiązanych diagnostyki wystąpić. Na przykład aplikacji mogą nie powodu tooperformance spadek wydajności warstwy SQL. Mapowanie aplikacji możesz od razu zobacz temat i przejść do szczegółów w środowisko hello Doradcę w zakresie indeksowania SQL lub szczegółowe informacje o zapytań.

![Mapa aplikacji](./media/app-insights-devops/050.png)

## <a name="application-insights-analytics"></a>Application Insights analityka
Z [Analytics](app-insights-analytics.md), możesz pisać zapytania dowolnego zaawansowanych języka przypominającego SQL.  Diagnozowanie przez stos całej aplikacji hello staje się łatwe zgodnie z różnych perspektyw nawiązywanie połączeń i poproś toocorrelate odpowiednie pytania hello wydajność usługi z metryki biznesowe i obsługi klienta. 

Wszystkie wystąpienia telemetrii oraz metryki nieprzetworzone dane przechowywane w portalu hello można zapytania. język Hello obejmuje filtr sprzężenia, agregacji i innych operacji. Można obliczyć pola i wykonywać analizy statystycznej. Brak wizualizacji zarówno tabelarycznej i graficznej.

![Wykres zapytania i wyniki analizy](./media/app-insights-devops/025.png)

Na przykład jest łatwe:

* Segmentu danych wydajności przez klienta tiers toounderstand ich obsługi żądania aplikacji.
* Wyszukiwanie określonych kodów błędów lub nazwy niestandardowe zdarzenie podczas badania działającą witrynę.
* Przejdź do szczegółów użycie aplikacji hello toounderstand specyficznych klientów jak zakupione i przyjęte funkcji.
* Śledzenie sesji i czas odpowiedzi dla określonych użytkowników tooenable obsługi i operacje zespoły tooprovide błyskawicznych techniczną.
* Ustal, często używanych aplikacji funkcji tooanswer funkcji priorytetyzacji pytania.

Dana klienta DNN: "usługi Application Insights podał z hello brakuje części równanie hello jest w stanie toocombine, sortowania, kwerendy i filtrowanie danych zgodnie z potrzebami. Stosowanie toouse naszego zespołu własnych toofind ingenuity i obsługi danych za pomocą języka zaawansowanych zapytań pozwoliło nam toofind insights i rozwiązywania problemów, które nie zostały jeszcze wiemy, że było. Wiele odpowiedzi interesujące pochodzą z pytania hello począwszy *"I swoje if...".*"

## <a name="development-tools-integration"></a>Programowanie narzędzia integracji
### <a name="configuring-application-insights"></a>Konfigurowanie usługi Application Insights
Visual Studio i Eclipse ma narzędzia tooconfigure hello poprawne SDK pakietów dla projektu hello, które tworzysz. Brak tooadd polecenia menu usługi Application Insights.

W przypadku toobe przy użyciu struktury rejestrowania śledzenia, takie jak Log4N, NLog lub System.Diagnostics.Trace, uzyskuje hello opcja toosend hello dzienniki tooApplication Insights wraz z hello inne dane telemetryczne, dzięki czemu można łatwo korelowanie śladów hello z żądaniami , wywołań zależności i wyjątki.

### <a name="search-telemetry-in-visual-studio"></a>Wyszukaj dane telemetryczne w programie Visual Studio
Podczas opracowywania i debugowania funkcji, można wyświetlić i wyszukiwać dane telemetryczne bezpośrednio w programie Visual Studio przy użyciu hello sam wyszukiwanie urządzeń jako w portalu sieci web hello hello.

I po zalogowaniu się wyjątku usługi Application Insights, można wyświetlić hello punktu danych w programie Visual Studio i przejść proste toohello odpowiedni kod.

![Visual Studio wyszukiwania](./media/app-insights-devops/060.png)

Podczas debugowania, masz hello opcja tookeep hello telemetrii w komputerze deweloperskim przeglądania go w programie Visual Studio, ale bez wysyłania go toohello portalu. Ta opcja lokalnego pozwala uniknąć mieszanie debugowania o telemetrii produkcji.

### <a name="build-annotations"></a>Tworzenie adnotacji
Jeśli używasz programu Visual Studio Team Services toobuild i wdrażanie aplikacji, wdrożenie adnotacje wyświetlane na wykresach w portalu hello. Jeśli z najnowszej wersji miała wpływu na powitania metryki, staje się oczywiste.

![Tworzenie adnotacji](./media/app-insights-devops/070.png)

### <a name="work-items"></a>Elementy robocze
Gdy zostanie zgłoszony alert, usługi Application Insights może automatycznie tworzyć elementu roboczego pracy śledzenia systemu.

## <a name="but-what-about"></a>Ale co zrobić...?
* [Prywatność i magazynu](app-insights-data-retention-privacy.md) -telemetrii jest przechowywana na serwerach Azure bezpieczne.
* Wydajność — wpływ hello jest bardzo niskie. Dane telemetryczne jest umieścić w zadaniu wsadowym.
* [Cennik](app-insights-pricing.md) — możesz rozpocząć pracę bezpłatnie i który będzie kontynuowane, podczas pracy w niskim poziomie.


## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Następne kroki
Wprowadzenie do korzystania z usługi Application Insights jest bardzo proste. dostępne są opcje głównego Hello:

* Instrumentacja aplikacji sieci web już uruchomiona. Dzięki temu wszystkie dane telemetryczne wydajności wbudowanych hello. Nie jest dostępny do [Java](app-insights-java-live.md) i [serwery IIS](app-insights-monitor-performance-live-website-now.md), a także do [aplikacje sieci web Azure](app-insights-azure.md).
* Instrumentacja projektu w czasie projektowania. Można to zrobić [ASP.NET](app-insights-asp-net.md) lub [Java](app-insights-java-get-started.md) aplikacji, a także [Node.js](app-insights-nodejs.md) i hosta [innych typów](app-insights-platforms.md). 
* Instrumentem [dowolną stronę sieci web](app-insights-javascript.md) przez dodanie fragment kodu krótki.

