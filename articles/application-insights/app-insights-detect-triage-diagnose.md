---
title: aaaOverview Azure Application Insights dla DevOps | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse usługi Application Insights w środowisku Ops deweloperów."
author: CFreemanwa
services: application-insights
documentationcenter: 
manager: carmonm
ms.assetid: 6ccab5d4-34c4-4303-9d3b-a0f1b11e6651
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: bwren
ms.openlocfilehash: 42139f4645e815f26378726f4716a9bfbdc78551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-insights-for-devops"></a>Omówienie usługi Application Insights dla opracowywania oprogramowania

Z [usługi Application Insights](app-insights-overview.md), można szybko znaleźć się, jak aplikacja działa i jest używany w przypadku na żywo. W przypadku problemu go informuje o go, pomaga ocenić wpływ hello i pozwalają określić przyczynę hello.

Oto konta od zespołu rozwija aplikacji sieci web:

* *"Kilku dni temu, wdrożyliśmy"drobna"poprawki. Firma Microsoft nie został uruchomiony przebiegu testowego szerokie, ale Niestety niektórych nieoczekiwane zmiany otrzymano scalone hello ładunek, co powoduje niezgodność między przodu hello i zaplecza. Natychmiast uruchamiany naszych alert wzrósł wyjątki serwera, i zostały wprowadziliśmy świadome sytuacji hello. Kilka kliknięć optymalizacji w portalu usługi Application Insights hello dotarliśmy wystarczających informacji z toonarrow callstacks wyjątek w dół hello problem. Firma Microsoft wycofana natychmiast i ograniczone hello uszkodzenia. Application Insights wprowadził ta część hello devops cykl bardzo łatwe i możliwością."*

W tym artykule możemy wykonaj zespołu w banku firmy Fabrikam, że osiąga hello online banków toosee systemu (OBS), jak używać usługi Application Insights tooquickly odpowiadają toocustomers i aktualizacje.  

Hello zespołu działa w cyklu opracowywania oprogramowania pokazana na następującej ilustracji hello:

![Cyklu opracowywania oprogramowania](./media/app-insights-detect-triage-diagnose/00-devcycle.png)

Wymagania dotyczące źródła danych do ich programowanie zaległości (Lista zadań). Funkcje te działają w skrócie przebiegów, które często dostarczają oprogramowania pracy — zwykle w formie hello istniejącej aplikacji toohello ulepszenia i rozszerzenia. aktywnej aplikacji Hello jest często aktualizowana o nowe funkcje. Mimo że jest na żywo, zespołu hello monitoruje wydajności i użycia za pomocą hello usługi Application Insights. Źródła danych APM do ich zaległości programowanie.

zespół Hello używa usługi Application Insights toomonitor hello sieci web aplikacji ściśle dla:

* Wydajność. Mają one toounderstand jak czas reakcji zależy od liczby żądań; ile procesora CPU, sieci, dysku i inne zasoby są używane; i gdzie hello wąskich gardeł.
* Błędy. Jeśli istnieją wyjątki żądań zakończonych niepowodzeniem lub jeśli licznik wydajności nie jest poza zakresem doświadczenia, hello tooknow potrzeb zespołu szybko, aby potencjalnie akcji.
* Użycie. Przypadku nową funkcję, zespołu hello mają tooknow toowhat zakresu, który jest używany i czy użytkownicy mają trudności z nim.

Ta funkcja pozwala skupić się na hello opinii część cyklu hello:

![Wykryj klasyfikacji diagnozowanie](./media/app-insights-detect-triage-diagnose/01-pipe1.png)

## <a name="detect-poor-availability"></a>Wykryj niską dostępności
Marcela Markova jest starszy developer hello OBS zespołu i Trwa liderem hello monitorowania wydajności w trybie online. Użytkownik konfiguruje kilka [testów dostępności](app-insights-monitor-web-app-availability.md):

* Test adresu URL jednym hello strony głównej docelowej dla aplikacji hello http://fabrikambank.com/onlinebanking/. Ustawia ona kryteria HTTP o kodzie 200 i tekst "Witaj!". W przypadku niepowodzenia tego testu jest poważny problem ze hello sieć, serwery hello lub może być problem wdrażania. (Lub ktoś zmienił hello Zapraszamy! komunikat na stronie powitania bez umożliwienie jej znanych).
* Lepszy badanie wieloetapowych, loguje i pobiera bieżącego konta wyświetlania, sprawdzanie kilku szczegółów klucza na każdej stronie. Ten test sprawdza, czy działa baza danych tego hello łączy toohello kont. Używa identyfikatora klienta fikcyjne: niektóre z nich, które są obsługiwane dla celów testowych.

Te testy Konfigurowanie Marcela to pewność, że tego zespołu hello szybko dowiedzieć się o wszelkich awarii.  

Błędy wyświetlane jako czerwone kropki na wykresie testu sieci web hello:

![Wyświetlanie uruchomionych na powitania poprzedzający okres testów sieci web](./media/app-insights-detect-triage-diagnose/04-webtests.png)

Ale co ważniejsze, alert o niezgodności wysyłany pocztą e-mail toohello zespół deweloperów. W ten sposób wiedzą o tym przed hello niemal wszystkich klientów.

## <a name="monitor-performance"></a>Monitorowanie wydajności
Na stronie Przegląd hello w usłudze Application Insights jest wykres przedstawiający różnych [kluczowe metryki](app-insights-web-monitor-performance.md).

![Różnych metryk](./media/app-insights-detect-triage-diagnose/05-perfMetrics.png)

Czas ładowania strony przeglądarki jest pochodną telemetrii wysyłane bezpośrednio ze stron sieci web. Czas odpowiedzi serwera, liczba żądań na serwerze i liczba nieudanych żądań są wszystkie mierzony w powitania serwera sieci web i wysyłane tooApplication szczegółowych informacji z tego miejsca.

Marcela jest nieco związane z powitania serwera odpowiedzi wykresu. Ten wykres pokazuje średni czas powitania od kiedy hello serwer odbiera żądanie HTTP z przeglądarki użytkownika i kiedy zwraca odpowiedź hello. Jak obciążenia na powitania systemu nie jest toosee nietypowe zachowanie podczas zmiany na tym wykresie. Jednak w takim przypadku wydaje się, że toobe korelacja małych wzrostu hello liczba żądań, a big wzrośnie hello czas odpowiedzi. Który może wskazywać, że hello system działa tylko podczas pracy z maksymalną wydajnością.

Użytkownik otwiera hello wykresy serwerów:

![Różnych metryk](./media/app-insights-detect-triage-diagnose/06.png)

Prawdopodobnie toobe nie znak ograniczenia zasobów, dlatego może być nierówności hello na wykresach odpowiedzi serwera hello są właśnie zbieżność.

## <a name="set-alerts-toomeet-goals"></a>Ustaw alerty toomeet cele
Niemniej jednak użytkownik chcieliby tookeep oka na powitania czasy odpowiedzi. Jeśli komputery przechodzą zbyt duże, chce tooknow informacji na ten temat natychmiast.

Dlatego użytkownik ustawia [alert](app-insights-metrics-explorer.md), dla większy niż próg typowy czas odpowiedzi. Dzięki temu jej pewność, że użytkownik będzie wiadomo o nim gdy czas reakcji wolno.

![Dodawanie bloku alertu](./media/app-insights-detect-triage-diagnose/07-alerts.png)

Alerty można ustawić na różnych innych metryk. Na przykład można otrzymywać wiadomości e-mail, jeśli wzrośnie liczba wyjątków hello lub niski przechodzi hello dostępnej pamięci lub brak szczytu w żądań klientów.

## <a name="stay-informed-with-smart-detection-alerts"></a>Poinformują Cię o alerty o wykryciu inteligentne
Następnego dnia alertów e-mail odbierane z usługi Application Insights. Jednak gdy użytkownik otwiera, użytkownik stwierdza, że nie jest alertu czasu odpowiedzi hello ona ustawiona. Zamiast tego informuje o tym jej czy został nagły wzrost nieudanych żądań — to znaczy żądań, które zwrócone kodów błędu 500 lub więcej.

Żądań zakończonych niepowodzeniem są, gdzie umieścić błąd — zwykle po wyjątek w kodzie hello użytkowników. Może być zobaczy komunikat informujący o tym "Niestety nie można teraz zaktualizować szczegóły". Lub bezwzględną najgorszy Zakłopotanie, zrzut stosu wydaje na ekranie powitania użytkownika dzięki uprzejmości: hello serwera sieci web.

Ten alert jest zaskoczeniem, ponieważ hello czasu, gdy użytkownik przeglądał, hello nie powiodło się żądanie count była encouragingly niski. Mała liczba błędów jest toobe oczekiwane na serwerze zajęty.

Również nieco zaskoczeniem dla jej ponieważ użytkownik nie ma tooconfigure ten alert. Usługa Application Insights obejmują wykrywanie inteligentne. Automatycznie dostosowuje tooyour aplikacji zwykle awarii wzorzec, "jest używany do" błędy i na konkretnej stronie, lub wysokie obciążenie albo połączonego tooother metryki. Uruchamia hello alarm tylko wtedy, gdy wzrost powyżej jakie pochodzi tooexpect.

![proaktywna Diagnostyka poczty e-mail](./media/app-insights-detect-triage-diagnose/21.png)

Jest to bardzo przydatne wiadomości e-mail. Go nie tylko podnieść alarmu. Robi zbyt wiele hello klasyfikacji i diagnostycznych pracy.

Przedstawia on dotyczy ilu użytkowników i strony sieci web lub operacji. Marcela można zdecydować, czy potrzebuje tooget hello całego zespołu pracujących na tym, jak szczegółowego fire, lub czy można go zignorować dopiero w następnym tygodniu.

Hello poczty e-mail zawiera także określonego wyjątek wystąpił, czy - jeszcze bardziej interesującego — awarii hello jest skojarzony z określoną bazę danych tooa wywołania nie powiodło się. W tej sekcji wyjaśniono, dlaczego błędów hello nagle pojawił się nawet zespołu w Marcela ostatnio nie wdrożono żadnych aktualizacji.

Wiodącymi hello polecenia ping Marcella hello zespołu bazy danych na podstawie tej wiadomości e-mail. Użytkownik uzyskuje informacje o ich zwolnienie poprawki w hello ostatnich pół godziny; i Niestety, może być mogło być zmiany schematu pomocnicza...

Dlatego hello problem znajduje się na toobeing sposób hello stałej, nawet przed badania dzienników i w ciągu 15 minut, jego wynikające. Jednak Marcela kliknie hello łącze tooopen usługi Application Insights. Użytkownik może uzyskać bazy danych nie powiodło się wywołanie hello skojarzone liście wywołania zależności i otwiera bezpośrednio na żądanie nie powiodło się.

![żądanie nie powiodło się](./media/app-insights-detect-triage-diagnose/23.png)

## <a name="detect-exceptions"></a>Wykryj wyjątków
Z niewielki instalacji [wyjątki](app-insights-asp-net-exceptions.md) są automatycznie zgłoszony tooApplication szczegółowych informacji. One również można przechwycić jawnie przez zbyt Wstawianie wywołania[funkcji TrackException()](app-insights-api-custom-events-metrics.md#trackexception) hello kodu:  

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }


zespołu Fabrikam Bank Hello powstał praktyki hello zawsze wysyłania danych telemetrycznych z powodu wyjątku braku oczywista odzyskiwania.  

W rzeczywistości jest szersze niż ich strategii: wysyłają dane telemetryczne w każdej sytuacji, gdy powitania klienta są sfrustrowani, w jaki chcieli toodo, czy odpowiadający mu tooan wyjątek w kodzie hello, lub nie. Na przykład jeśli system zewnętrzny transferu między bank hello zwraca komunikat "nie można ukończyć tej transakcji" jakiegoś powodu operacyjne (nie odporności powitania klienta) następnie śledzą tego zdarzenia.

    var successCode = AttemptTransfer(transferAmount, ...);
    if (successCode < 0)
    {
       var properties = new Dictionary <string, string>
            {{ "Code", returnCode, ... }};
       var measurements = new Dictionary <string, double>
         {{"Value", transferAmount}};
       telemetry.TrackEvent("transfer failed", properties, measurements);
    }

TrackException jest używane tooreport wyjątki, ponieważ wysyła kopię stosu hello. TrackEvent jest tooreport używane inne zdarzenia. Możesz dołączyć wszystkie właściwości, które mogą być przydatne do rozpoznania.

Wyjątki i zdarzenia wyświetlane w hello [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md) bloku. Można przejść do szczegółów w nich toosee hello dodatkowe właściwości i ślad stosu.

![W wyszukiwaniu diagnostycznych Użyj filtrów tooshow określonego typu danych](./media/app-insights-detect-triage-diagnose/appinsights-333facets.png)


## <a name="monitor-proactively"></a>Aktywne monitorowanie
Marcela nie tylko znajdują się wokół oczekiwanie na alerty. Wkrótce po każdym ponownego wdrażania, klika przedstawia [czas reakcji](app-insights-web-monitor-performance.md) — zarówno hello ogólną rysunek i liczby tabeli hello najwolniejsze żądania, a także wyjątek.  

![Wykres czasu odpowiedzi i siatki czas odpowiedzi serwera.](./media/app-insights-detect-triage-diagnose/09-dependencies.png)

Użytkownik ocenić wpływ na wydajność hello każdego wdrożenia zwykle porównanie każdej tydzień z hello ostatnio. W przypadku nagłego pogorszenia, klika który zgłasza z deweloperami odpowiednich hello.

## <a name="triage-issues"></a>Klasyfikacji problemów
Klasyfikacja — ocenę ważności hello i zakres problem — jest pierwszym krokiem hello po wykryciu. Należy nazywamy limit zespołu hello o północy? Lub może on pozostać do hello dalej wygodny przerwa w hello zaległości? Istnieją pewne ważne pytania w klasyfikacji.

Jak często jest wykonywane? Wykresy Hello w bloku omówienie hello nadaj pewien problem tooa perspektywy. Na przykład hello aplikacji firmy Fabrikam wygenerowanych cztery alerty testu sieci web co noc. Spojrzenie na wykresie hello w rano hello, zespołu hello mogliby zobaczyć wystąpiły w rzeczywistości niektóre czerwone kropki, jakby nadal większość hello testy zostały zielony. Przechodzenia do wykresu dostępności hello szczegółów, jest jasne, czy zostały wszystkie te sporadyczne problemy z lokalizacji jeden test. Oczywiście była wpływające na tylko jedną trasę problem z siecią i najprawdopodobniej będzie wyczyść samej siebie.  

Z kolei znacznej i stabilnego wzrost wykres hello liczby wyjątków lub czas odpowiedzi to oczywiście element toopanic o.

Działanie przydatne Klasyfikacja jest spróbuj ją samodzielnie. Jeśli napotkasz hello sam problem, wiadomo, jest prawdziwe.

Jaka część użytkowników dotyczy? tooobtain nierównej odpowiedzi, dzielenia współczynnik awaryjności hello przez hello liczba sesji.

![Wykresy sesji i żądań zakończonych niepowodzeniem](./media/app-insights-detect-triage-diagnose/10-failureRate.png)

W przypadku odpowiedzi powolne porównania tabeli hello najwolniejsze odpowiada żądań z hello użycia częstotliwość każdej strony.

Jak ważna jest scenariusz hello zablokowane? Jeśli jest to problem funkcjonalności blokuje konkretnego scenariusza, czy ma znaczenie znacznie? Jeśli klienci nie mogą ich rachunków, jest to poważny; Jeśli nie mogą zmieniać swoje preferencje kolorów ekranu, może być go wykonać. Witaj szczegółów zdarzenia hello lub wyjątek lub tożsamości hello hello powolne strony, informuje, gdy występują problemy dotyczące klientów.

## <a name="diagnose-issues"></a>Diagnozowanie problemów
Diagnostyka nie jest dość hello jak w przypadku debugowania. Przed rozpoczęciem śledzenia hello kod powinien mieć wstępne informacje o tym, dlaczego, gdzie i kiedy występuje problem hello.

**Gdy jest wykonywana?**  hello widok historycznych podał wykresów zdarzenia i metryki hello umożliwia łatwe toocorrelate efekty z możliwych przyczyn. Jeśli występują sporadyczne pików kursów czas lub wyjątku odpowiedzi, obejrzyj liczbę żądań hello: jeśli jego pików na powitania sam czasu, a następnie prawdopodobnie problem z zasobów. Potrzebujesz tooassign więcej procesorów ani pamięci? Czy jest zależność, która nie może zarządzać hello obciążenia?

**Jest to nam?**  Ma gwałtowny spadek wydajności danego typu żądania — na przykład gdy hello odbiorca chce otrzymywać instrukcji konta -, istnieje możliwość może być zewnętrzny podsystemu zamiast aplikacji sieci web. W Eksploratorze metryk wybierz współczynnik awaryjności zależności hello i czas trwania zależności stawki i porównywanie ich historii hello poza kilka godzin lub dni w przypadku problemu hello zostało wykryte. Jeśli są korelowanie zmiany, zewnętrznych podsystemu może być tooblame.  

![Wykresy zależności awarii i czas trwania wywołań toodependencies](./media/app-insights-detect-triage-diagnose/11-dependencies.png)

Niektóre problemy powolne zależności są problemy używanie funkcji geolokalizacji. Bank firmy Fabrikam używa maszyn wirtualnych platformy Azure i wykryte, że ma przypadkowo się one serwera sieci web i serwer kont w różnych krajach. Znacznej poprawy został przełączony w tryb przy użyciu funkcji migracji jeden z nich.

**Do czego możemy?** Jeśli hello problem nie zostanie wyświetlone toobe w zależności, a jeśli go nie zawsze istnieje, prawdopodobnie jest spowodowany przez ostatnich zmian. Hello historycznych perspektywy podał hello wykresy metryk i zdarzeń umożliwia łatwe toocorrelate nagły zmiany z wdrożeniami. Który zawęża hello Wyszukaj hello problem.

**Co się dzieje?** Niektóre problemy występują rzadko i może być trudne tootrack dół testując w trybie offline. Wszystko, co można zrobić jest tootry toocapture hello błąd, jeśli występuje on na żywo. Możesz sprawdzić hello zrzuty stosu w raportach wyjątku. Ponadto można napisać śledzenia wywołań, Twoje struktury rejestrowania ulubionych albo TrackTrace() lub funkcji TrackEvent().  

Firma Fabrikam miał problem tymczasowy w przypadku transferów między kontami, ale tylko w przypadku niektórych typów kont. lepsze toounderstand została co dzieje, ich wstawione wywołania TrackTrace() w najważniejszych w kodzie hello dołączanie hello typu konta jako wywołanie tooeach właściwości. Który wprowadzone go łatwo toofilter się tylko te dane śledzenia w wyszukiwaniu diagnostycznych. Wartości parametrów one również dołączone jako właściwości i środki toohello śledzenie wywołań.

## <a name="respond-toodiscovered-issues"></a>Odpowiedź toodiscovered problemów
Gdy po zdiagnozowaniu problemu hello, możesz wprowadzić toofix planu go. Może być konieczne tooroll ponownie zmiany lub może być można po prostu przejdź dalej i rozwiąż problem. Po zakończeniu poprawka hello usługi Application Insights informuje, czy powiodło się.  

Zespół deweloperów Fabrikam Bank zająć więcej podejście tooperformance pomiaru niż kiedyś toobefore używały usługi Application Insights.

* Na stronie przeglądu usługi Application Insights hello one wyznaczać cele pod względem określonej miary.
* Projekt miary wydajności do aplikacji hello od początku hello, takich jak hello metryki pomiaru postępu użytkownika za pośrednictwem "lejki."  


## <a name="monitor-user-activity"></a>Monitorowanie aktywności użytkownika
Gdy czas odpowiedzi jest stale prawidłowy i istnieje kilka wyjątków, zespół deweloperów hello może zająć toousability. Można traktować jak tooimprove hello użytkowników i sposób tooencourage więcej użytkowników tooachieve hello potrzeby celów.

Usługi Application Insights mogą być również używane toolearn, czy użytkownicy z aplikacją. Po uruchomieniu sprawnie, co użytkowników, takich jak lub mieć trudności z i jak często wracają zespołu hello chcieliby tooknow funkcji, które są najbardziej popularnych hello. Która będzie ułatwiała ich priorytety nadchodzących pracy. I ich zaplanować Powodzenie hello toomeasure każdej funkcji jako część hello programowanie cyklu. 

Na przykład za pośrednictwem witryny sieci web hello podróży typowy użytkownik ma Wyczyść "lejka." Wielu klientów przyjrzeć się stawki hello różnego rodzaju pożyczki. Mniejsza liczba Przejdź toofill w postaci oferty hello. Tych, którzy pobrać oferty kilka Przejdź dalej i wyjmij hello pożyczki.

![Zlicza widoku strony](./media/app-insights-detect-triage-diagnose/12-funnel.png)

Biorąc pod uwagę, gdy hello największej liczby klientów porzucić, hello business można pracować się jak tooget więcej użytkowników za pomocą toohello dołu hello lejkowy. W niektórych przypadkach może być błąd środowiska (UX) użytkownika — na przykład przycisk 'Dalej' hello jest toofind twardym lub instrukcje hello nie są oczywiste. Bardziej prawdopodobne są bardziej znaczących powodów biznesowych do listy dokumentów: może być stawki pożyczki hello są zbyt duże.

Niezależnie od przyczyn hello danych hello pomaga zespołu hello wyglądają co robią użytkownicy. Więcej śledzenia wywołania mogą być wstawiane toowork szczegółowe. Funkcji TrackEvent() mogą być używane toocount wszystkie akcje użytkownika z hello dokładniej z klika przycisk poszczególnych, osiągnięć toosignificant, takich jak płatności poza pożyczki.

zespół Hello otrzymuje toohaving używane informacje dotyczące działań użytkownika. Dzisiaj zawsze, gdy projekt nową funkcję, działają się, jak będzie uzyskują swoją opinię na temat jej użycia. Projekt śledzenia wywołań funkcji powitania od początku hello. One funkcja hello opinii tooimprove hello w każdym cyklu programowania.

[Przeczytaj więcej na temat śledzenia użycia](app-insights-usage-overview.md).

## <a name="apply-hello-devops-cycle"></a>Zastosuj hello cyklu opracowywania oprogramowania
To jest tak jak jedno użycie zespołu usługi Application Insights nie tylko toofix poszczególne problemy, ale tooimprove ich cyklu programistycznym. Mam nadzieję, że jej została podana sugestii dotyczących sposobu usługi Application Insights ułatwia zarządzanie aplikacjami wydajności w aplikacjach.

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Następne kroki
Możesz rozpocząć pracę na kilka sposobów, w zależności od właściwości hello aplikacji. Wybierz, co dogodny:

* [Aplikacja sieci web ASP.NET](app-insights-asp-net.md)
* [Aplikacja sieci web Java](app-insights-java-get-started.md)
* [Aplikacja sieci web node.js](app-insights-nodejs.md)
* Już wdrożone aplikacje hostowane na [IIS](app-insights-monitor-web-app-availability.md), [J2EE](app-insights-java-live.md), lub [Azure](app-insights-azure.md).
* [Strony sieci Web](app-insights-javascript.md) -jednej strony, aplikacji lub strony sieci web zwykłej — Użyj tej samodzielnie lub w tooany dodanie hello opcji serwera.
* [Badania dostępności](app-insights-monitor-web-app-availability.md) tootest aplikacji z hello publicznej sieci internet.
