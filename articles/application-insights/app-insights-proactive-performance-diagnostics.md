---
title: "aaaSmart wykrywania - anomalii wydajności | Dokumentacja firmy Microsoft"
description: "Usługa Application Insights wykonuje inteligentne analizy telemetrii aplikacji i ostrzega o potencjalnych problemach. Ta funkcja wymaga ustawień."
services: application-insights
documentationcenter: windows
author: antonfrMSFT
manager: carmonm
ms.assetid: 6acd41b9-fbf0-45b8-b83b-117e19062dd2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: bwren
ms.openlocfilehash: 60f10612188920330030129f7464e2f398ef1f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---performance-anomalies"></a>Inteligentne wykrywanie - anomalii wydajności

[Usługa Application Insights](app-insights-overview.md) automatycznie analizuje hello wydajność aplikacji sieci web i może zostać wyświetlone ostrzeżenie o potencjalnych problemach. Możesz może być odczytu to ponieważ jeden z naszych wykrywania inteligentne powiadomienia odbierane.

Ta funkcja wymaga specjalnych ustawień, niż Konfigurowanie aplikacji dla usługi Application Insights (na [ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), lub [Node.js](app-insights-nodejs.md), a następnie w [kodu strony sieci web](app-insights-javascript.md)). Jest aktywna, kiedy aplikacja generuje za mało danych telemetrii.

## <a name="when-would-i-get-a-smart-detection-notification"></a>Gdy otrzyma powiadomienie o inteligentne wykrywanie?

Usługi Application Insights wykrył, że wydajność aplikacji hello ma obniżoną w jeden z następujących sposobów:

* **Degradacji czasu odpowiedzi** — aplikacja została uruchomiona wolniej niż odpowiada toorequests. Zmień Hello mogły zostać szybkie, na przykład powodu regresji we wdrożeniu najnowsze. Lub było stopniowe, może być spowodowany przeciek pamięci. 
* **Zależności czas trwania degradacji** -aplikacji sprawia, że interfejs API REST tooa wywołania, bazy danych lub innych zależności. zależności Hello odpowiada wolniej niż.
* **Niska wydajność wzorzec** — aplikacja zostanie wyświetlona toohave wystawia wydajności, które ma wpływ na tylko niektórych żądań. Na przykład strony są ładowane wolniej na jeden typ przeglądarki niż inne; lub żądania są podawane wolniej z jednego określonego serwera. Obecnie nasze algorytmy przyjrzeć się czas ładowania strony, czas odpowiedzi na żądanie i czasy odpowiedzi zależności.  

Wykrywanie inteligentne wymaga co najmniej 8 dni dane telemetryczne głośność możliwego w kolejności tooestablish linii bazowej normalnej wydajności. Tak po aplikacja została uruchomiona w tym okresie, wszelkie istotne problemy w wyniku powiadomienia.


## <a name="does-my-app-definitely-have-a-problem"></a>Aplikacja my uwielbiamy ma problem?

Nie, powiadomienia nie oznacza, że aplikacja ma ostatecznie problem. Jest po prostu sugestii dotyczących coś, co może być toolook na dokładniejsze.

## <a name="how-do-i-fix-it"></a>Jak rozwiązać ten problem?

Witaj powiadomienia obejmują informacje diagnostyczne. Oto przykład:


![Oto przykład wykrywania degradacji czas odpowiedzi serwera](./media/app-insights-proactive-diagnostics/server_response_time_degradation.png)

1. **Klasyfikacja**. Hello powiadomień przedstawia liczbę użytkowników lub dotyczy ile operacji. Może to ułatwić możesz przypisać problem toohello priorytet.
2. **Zakres**. Witaj problem wpływa na cały ruch lub tylko do niektórych strony? Jest ograniczone it tooparticular przeglądarki lub lokalizacji? Te informacje można uzyskać z hello powiadomienia.
3. **Diagnozowanie**. Często hello informacje diagnostyczne w powiadomieniu hello sugeruje hello rodzaj hello problem. Na przykład, jeśli czas reakcji spowalnia po wysoki współczynnik żądań, które sugeruje się, że serwer lub zależności są przeciążone. 

    W przeciwnym razie otwarcie bloku wydajności hello w usłudze Application Insights. Istnieje, można znaleźć [profilera](app-insights-profiler.md) danych. Jeśli istnieją wyjątki zgłaszane, możesz również spróbować hello [debugera migawki](app-insights-snapshot-debugger.md).



## <a name="configure-email-notifications"></a>Skonfiguruj powiadomienia E-mail

Inteligentne powiadomienia wykrywania są domyślnie włączone i wysyłane toothose, którzy mają [właściciele, współautorzy i czytelnicy dostęp do zasobu usługi Application Insights toohello](app-insights-resources-roles-access-control.md). toochange to kliknąć **Konfiguruj** w hello powiadomienia e-mail, lub Otwórz ustawienia inteligentnego wykrywania w usłudze Application Insights. 
  
  ![Inteligentne wykrywania ustawień](./media/app-insights-proactive-diagnostics/smart_detection_configuration.png)
  
  * Można użyć hello **subskrypcję** łącze w toostop e-mail inteligentne wykrywanie hello odbierania powiadomień e-mail hello.

Wiadomości e-mail o inteligentne wykrywania anomalii wydajności są ograniczone tooone e-mail dziennie według zasobu usługi Application Insights. Witaj wiadomości e-mail będą wysyłane tylko wtedy, gdy istnieje co najmniej jeden nowy problem, która została wykryta w tym dniu. Użytkownik nie będzie otrzymywał powtarza wiadomości. 

## <a name="faq"></a>Często zadawane pytania

* *Tak guys przeglądania danych?*
  * Nie. Usługa Hello jest całkowicie automatyczne. Tylko otrzymasz hello powiadomienia. Twoje dane są [prywatnej](app-insights-data-retention-privacy.md).
* *Czy można analizować hello dane zbierane przez usługę Application Insights?*
  * Nie w chwili obecnej. Obecnie możemy analizowanie żądania czas reakcji i czas odpowiedzi zależności czas ładowania. Analiza dodatkowe metryki znajduje się na naszych zaległości wyszukiwania do przodu.

* Jakie typy aplikacji jest to odpowiednie dla?
  * Te degradations są wykrywane w dowolnej aplikacji, która generuje hello odpowiednie dane telemetryczne. Po zainstalowaniu usługi Application Insights w aplikacji sieci web, następnie żądania i zależności są automatycznie śledzone. Ale w usługi wewnętrznej bazy danych lub innych aplikacjach zbyt dodaje wywołania[TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) lub [TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency), Inteligentne wykrywanie będzie działać w hello sam sposób.

* *Można utworzyć własny anomalii reguł wykrywania lub dostosować istniejące zasady?*

  * Nie została jeszcze ale można wykonywać następujące czynności:
    * [Konfigurowanie alertów](app-insights-alerts.md) który informujące, gdy metryki przekracza próg.
    * [Eksportuj dane telemetryczne](app-insights-export-telemetry.md) tooa [bazy danych](app-insights-code-sample-export-sql-stream-analytics.md) lub [tooPowerBI](app-insights-export-power-bi.md), gdzie można analizować je samodzielnie.
* *Jak często jest wykonywane hello analizy*

  * Witaj analiza przeprowadzana codziennie na powitania dane telemetryczne z hello poprzedniego dnia (pełny dzień w strefie czasowej UTC).
* *To samo dzieje się to replace [metryki alerty](app-insights-alerts.md)?*
  * Nie.  Nie możemy przekazać toodetecting co warto rozważyć nietypowe zachowanie.


* *Jeśli I nie wykonuj żadnych czynności w odpowiedzi tooa powiadomienia, I otrzyma monitu?*
  * Nie, pojawi się komunikat o każdym tylko raz. Jeśli hello problem będzie się powtarzać zostaną zaktualizowane w powitalne inteligentne wykrywanie źródła bloku.
* *Utratą hello poczty e-mail. Gdzie można znaleźć hello powiadomienia w portalu hello?*
  * W obszarze Przegląd usługi Application Insights hello aplikacji, kliknij przycisk hello **inteligentne wykrywanie** kafelka. Będziesz w stanie toofind, wszystkie powiadomienia się dni too90 z powrotem.

## <a name="how-can-i-improve-performance"></a>Jak może poprawić wydajność?
Powolne i nie powiodło się odpowiedzi są jedną z największych frustrations hello użytkowników witryny sieci web, ponieważ znasz z własnego środowiska. Dlatego ważne jest tooaddress hello problemy.

### <a name="triage"></a>Klasyfikacja
Najpierw czy ma znaczenie? Jeśli strona jest zawsze tooload powolne, ale tylko 1% użytkowników witryny istniało toolook jego, być może masz ważniejsze toothink rzeczy o. Na hello drugiej strony, jeśli tylko 1% użytkowników go otworzyć, ale zawsze, które mogą być warto badanie zgłasza wyjątków.

Instrukcja hello wpływ (narażeni użytkownicy lub % ruchu) jako ogólne wytyczne, ale należy pamiętać, że nie jest on hello cały artykuł. Zbierać inne tooconfirm dowód.

Należy wziąć pod uwagę parametry hello hello problemu. Jeśli jest zależny od lokalizacji geograficznej, skonfiguruj [testów dostępności](app-insights-monitor-web-app-availability.md) łącznie tego regionu: może po prostu występować problemy z siecią w tym obszarze.

### <a name="diagnose-slow-page-loads"></a>Diagnozowanie ładunków strona powolne
Gdzie jest hello problem? Jest toorespond powolne powitania serwera, jest bardzo dużo strony hello lub przeglądarki hello ma toodo dużo pracy toodisplay go?

Otwiera blok metryki hello przeglądarki. Witaj segmentem wyświetlanej w przeglądarce strony obciążenia czasu wskazuje, gdzie będzie hello czasu. 

* Jeśli **czas wysyłania żądania** jest wysoka, albo hello serwer odpowiada powoli lub hello żądanie jest żądaniem post z dużą ilością danych. Przyjrzyj się hello [metryki wydajności](app-insights-web-monitor-performance.md#metrics) tooinvestigate czasy odpowiedzi.
* Konfigurowanie [śledzenia zależności](app-insights-asp-net-dependencies.md) toosee czy powolność hello jest tooexternal usług lub bazy danych.
* Jeśli **odbierania odpowiedzi** jest dominujący, strony i jego zależne elementy - JavaScript, CSS, obrazy i tak dalej (ale nie asynchronicznie załadowanych danych) jest długa. Konfigurowanie [test dostępności](app-insights-monitor-web-app-availability.md), i być tooset się, że opcja hello tooload zależne elementy. Po wyświetleniu okna pewnych wyników, otwórz hello szczegóły wyniku i rozwiń go toosee hello załadować razy różne pliki.
* Wysoka **czasu przetwarzania klienta** sugeruje skrypty działają wolno. Jeśli hello Przyczyna nie jest widoczne, należy dodać kodu czasu i wysłać hello razy w wywołaniach trackMetric.

### <a name="improve-slow-pages"></a>Poprawa powolne strony
Brak pełnej porady na temat zwiększania odpowiedzi serwera, a czas ładowania strony, więc nie zostanie podjęta toorepeat sieci web wszystkie tu. Poniżej przedstawiono kilka wskazówek, które prawdopodobnie już wiedzę na temat tooget tylko użytkownik myśląc:

* Powolne ładowanie ze względu na duże pliki: ładowanie skryptów hello i innymi częściami asynchronicznie. Użyj skryptu tworzenie pakietów. Podziel strony głównej hello na elementy widget, które oddzielnie załadować ich danych. Nie wysyłaj zwykły stary kod HTML pod kątem długich tabel: Użyj danych hello toorequest skryptu jako JSON lub w innym formacie kompaktowym, a następnie wypełnij hello tabeli w miejscu. Brak struktur dużą toohelp wszystkie te. (One również pociąga za sobą big skrypty oczywiście.)
* Powolna zależności serwera: należy wziąć pod uwagę hello lokalizacjach geograficznych składników. Na przykład, jeśli używasz platformy Azure, upewnij się, powitania serwera sieci web i hello bazy danych znajdują się w hello tego samego regionu. Czy zapytania pobierają więcej informacji, niż jest to wymagane? Czy buforowanie lub przetwarzania wsadowego pomocy?
* Problemy dotyczące pojemności: Spójrz na powitania serwera metryki czasów odpowiedzi i liczby żądań. Jeśli czas reakcji nieproporcjonalnie szczytowa z szczytów żądań, jest prawdopodobne, że serwery są rozciągana.


## <a name="server-response-time-degradation"></a>Degradacji czas odpowiedzi serwera

powiadomienia o degradacji czasu odpowiedzi Hello zawiera:

* czas odpowiedzi Hello porównywany toonormal czas odpowiedzi dla tej operacji.
* Ilu użytkowników są zagrożone.
* Średni czas odpowiedzi i 90-procentowy czas odpowiedzi dla tej operacji na dzień hello hello wykrywania i 7 dni przed. 
* Liczba ta operacja żądań w dniu hello hello wykrywania i 7 dni przed.
* Korelacja degradacji w tej operacji i degradations w powiązanych zależności. 
* Diagnozowanie problemu hello toohelp łącza.
  * Profiler śledzi toohelp można wyświetlić, gdzie jest zużywany czas operacji (łącze hello jest dostępna, ponieważ Profiler śledzenia przykłady zostały pobrane dla tej operacji w okresie wykrywania hello). 
  * Raporty wydajności w Eksploratorze metryki, gdy użytkownik może kątami filtrów zakresu czasu dla tej operacji.
  * To wyszukiwanie wywołuje tooview właściwości określonych wywołań.
  * Zgłasza błąd — jeśli count > 1 oznacza to, że wystąpiły błędy w tej operacji, która może przyczynić się spadku tooperformance.

## <a name="dependency-duration-degradation"></a>Zależności degradacji czas trwania

Nowoczesnych aplikacji bardziej przyjąć podejście do projektowania micro usług, które w wielu przypadkach prowadzi tooheavy niezawodności na usług zewnętrznych. Na przykład jeśli aplikacja opiera się na platformie niektórych danych, lub nawet w przypadku tworzenia własnych bot usługi prawdopodobnie będzie przekazywał na niektórych tooenable dostawcy usług kognitywnych toointeract Twojego robotów w sposób bardziej człowieka i niektóre dane są przechowywane usługi dla bot toopull hello odpowiedzi.  

Przykładowe powiadomienie degradacji zależności:

![Oto przykład wykrywania degradacji czas trwania zależności](./media/app-insights-proactive-diagnostics/dependency_duration_degradation.png)

Należy zauważyć, że informuje o tym:

* czas trwania Hello porównaniu toonormal czas odpowiedzi dla tej operacji
* Ilu użytkowników ma wpływ
* Średni czas trwania i 90-procentowy czas trwania tej zależności w dniu hello hello wykrywania i 7 dni przed
* Liczba zależności wywołań w dniu hello hello wykrywania i 7 dni przed
* Diagnozowanie problemu hello toohelp łącza
  * Raporty wydajności w Eksploratorze Metryka tej zależności
  * Wyszukaj tę zależność wywołuje tooview właściwości wywołań
  * Raporty błąd — jeśli wykrywania hello count > 1 wywołuje oznacza to, że wystąpiły zależności nie powiodło się podczas okresu, który może przyczynić się spadku tooduration. 
  * Otwórz Analytics z kwerendy obliczające ten czas trwania zależności i liczby  

## <a name="smart-detection-of-slow-performing-patterns"></a>Inteligentne wykrywanie powolnego wzorce wykonywania 

Usługa Application Insights umożliwia znalezienie problemy z wydajnością, które mogłyby dotyczą tylko części użytkowników, lub dotyczą tylko użytkownicy w niektórych przypadkach. Na przykład powiadomienia o ładowania stron jest slowler na jeden typ przeglądarki niż na inne typy przeglądarek, lub jeśli żądania są wolniej podawana z określonego serwera. Umożliwia również odnajdywanie problemów związanych z kombinacji właściwości, takie jak powolne ładuje w jednym obszarze geograficznym w przypadku klientów z określonym systemem operacyjnym.  

Anomalie, takich jak te są bardzo trudne toodetect właśnie, sprawdzając hello danych, ale są częściej niż się wydaje. Często ich powierzchni tylko, gdy klienci skarżą się. Do tego czasu jest za późno: hello wpływ na użytkowników są już przełączania konkurencji tooyour!

Obecnie nasze algorytmy przyjrzeć się czas ładowania strony, czas odpowiedzi na żądanie na powitania serwera i czasy odpowiedzi zależności.  

Nie masz tooset wszelkie progi lub skonfigurować reguły. Uczenie maszynowe i algorytmy wyszukiwania danych są używane toodetect nietypowe wzorce.

![Alerty e-mail hello kliknij hello łącze tooopen hello raport diagnostyczny na platformie Azure](./media/app-insights-proactive-performance-diagnostics/03.png)

* **Gdy** pokazuje wykrycia problemu hello czasu hello.
* **Co** opisano:

  * problem Hello, który został wykryty;
  * właściwości Hello hello zestaw zdarzeń, które znaleziono wyświetlane hello problem zachowanie.
* Witaj tabeli porównano hello niskiej zestaw o hello średni zachowanie inne zdarzenia.

Kliknij odpowiednie raporty filtrowane wg czasu hello i właściwości hello powolne wykonywania zestawu hello łącza tooopen Explorer metryki i wyszukiwania.

Zmodyfikuj hello czasu zakresu i filtry tooexplore hello telemetrii.

## <a name="next-steps"></a>Następne kroki
Te narzędzia diagnostyczne pomóc sprawdzić telemetrii hello z aplikacji:

* [Profiler](app-insights-profiler.md) 
* [Debuger migawki](app-insights-snapshot-debugger.md)
* [Analiza](app-insights-analytics-tour.md)
* [Diagnostyka inteligentne analityka](app-insights-analytics-diagnostics.md)

Inteligentne wykryć są całkowicie automatyczne. A może chcesz tooset niektóre alerty więcej?

* [Ręcznie skonfigurowanej metryki alertów](app-insights-alerts.md)
* [Dostępność testy sieci web](app-insights-monitor-web-app-availability.md)
