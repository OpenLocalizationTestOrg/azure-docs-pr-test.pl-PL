---
title: "dostępność aaaMonitor i elastyczność w dowolnej witrynie sieci web | Dokumentacja firmy Microsoft"
description: "Konfigurowanie testów sieci Web w usłudze Application Insights. Otrzymywanie alertów, kiedy witryna sieci Web staje się niedostępna lub wolno odpowiada."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a>Monitorowanie dostępności i czasu odpowiedzi dowolnej witryny sieci Web
Po wdrożeniu aplikację sieci web lub serwera tooany witryny sieci web, można skonfigurować toomonitor testy jego dostępność i elastyczność. [Azure Application Insights](app-insights-overview.md) wysyła żądania sieci web aplikacji tooyour w regularnych odstępach czasu z punktów wokół hello world. Jeśli aplikacja będzie odpowiadać powoli lub wcale, usługa powiadomi Cię o tym za pomocą alertu.

Testów dostępności można skonfigurować dla dowolnej protokołu HTTP lub HTTPS punktu końcowego, który jest dostępny z hello publicznej sieci internet. Nie masz tooadd cokolwiek toohello witryny sieci web, które w przypadku testowania. Nie jest on nawet z toobe witryny: można przetestować usługi interfejsu API REST, na którym jest zależna.

Istnieją dwa rodzaje testów dostępności:

* [Test adresu URL ping](#create): prosty test, który można utworzyć w hello portalu Azure.
* [Test sieci web wieloetapowych](#multi-step-web-tests): tworzony w Visual Studio Enterprise i przekazywania toohello portalu.

Możesz utworzyć zapasowej too25 testów dostępności poszczególnych zasobów aplikacji.

## <a name="create"></a>1. Otwieranie zasobu dla własnych raportów testów dostępności

**Jeśli skonfigurowano już program Application Insights** dla aplikacji sieci web, otwórz jego zasobu usługi Application Insights w hello [portalu Azure](https://portal.azure.com).

**Lub, jeśli chcesz toosee raportów w nowego zasobu** Zarejestruj zbyt[Microsoft Azure](http://azure.com), przejdź toohello [portalu Azure](https://portal.azure.com)i utworzyć zasobu usługi Application Insights.

![Nowy > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

Kliknij przycisk **wszystkie zasoby** tooopen hello omówienie bloku hello nowy zasób.

## <a name="setup"></a>2. Tworzenie testu ping adresu URL
Otwarcie bloku dostępności hello i dodać testu.

![Wypełnienie co najmniej hello adres URL witryny sieci Web](./media/app-insights-monitor-web-app-availability/13-availability.png)

* **adres URL Hello** może być dowolną stronę sieci web ma tootest, ale musi być widoczny z hello publicznej sieci internet. adres URL Hello może zawierać ciągu zapytania. Możesz więc np. szybko sprawdzić działanie bazy danych. Jeśli adres URL hello rozpoznaje przekierowania tooa, możemy go wykonać kolejne czynności too10 przekierowania.
* **Przeanalizować zależnych żądań**: Jeśli ta opcja jest zaznaczona, hello test żądań obrazów, skryptów, plików w stylu i innych plików, które są częścią hello strony sieci web w ramach testu. Witaj czas odpowiedzi zarejestrowane obejmuje tooget czas poświęcony na powitania tych plików. Witaj test zakończy się niepowodzeniem, jeśli te zasoby nie może pomyślnie pobrane w ciągu limitu czasu hello hello całego testu. 

    Jeśli nie zaznaczono opcji hello, hello testu tylko żąda pliku hello na określony adres URL hello.
* **Włącz ponawianie próby**: Jeśli ta opcja jest zaznaczona, gdy hello test zakończy się niepowodzeniem, jest ponowiona po krótkim interwale. Błąd jest zgłaszany dopiero wtedy, gdy trzy kolejne próby się nie powiodą. Kolejne testy są następnie wykonywane na częstotliwość testów zwykle hello. Ponów próbę jest tymczasowo wstrzymane do czasu następnego pomyślnego hello. Ta reguła jest stosowana niezależnie w każdej lokalizacji testu. Ta opcja jest zalecana. Średnio około 80% błędów znika po ponowieniu testu.
* **Częstotliwość testów**: Określa, jak często hello test jest uruchamiany z każdej lokalizacji testu. Przy częstotliwości równej 5 minut i 5 lokalizacjach testu witryna będzie testowana średnio co minutę.
* **Testowanie lokalizacje** są hello umieszczenie z gdzie nasze serwery wysłać adres URL tooyour żądania sieci web. Wybierz więcej niż jedną lokalizację, aby móc odróżnić problemy z witryną od problemów z siecią. Możesz wybrać się too16 lokalizacji.
* **Kryteria powodzenia**:

    **Limit czasu testu**: zmniejszyć to toobe wartość alerty powolne odpowiedzi. Hello test jest liczone jako awarii, jeśli w tym czasie nie odebrano odpowiedzi hello z witryny. W przypadku wybrania **przeanalizować zależnych żądań**, następnie hello wszystkich obrazów, plików w stylu, skrypty i inne zasoby zależne muszą zostały odebrane w tym czasie.

    **Odpowiedź HTTP**: hello spowodowało zwrócenie kodu stanu, który będzie traktowany jako sukcesu. 200 jest hello kod, który wskazuje zwrócono normalne strony sieci web.

    **Zgodność zawartości**: ciąg znaków, np. „Witaj!” Sprawdzamy, czy w każdej odpowiedzi występuje dokładna zgodność pod względem wielkości liter. Musi to być zwykły ciąg znaków bez symboli wieloznacznych. Pamiętaj, że jeśli strony zmiany zawartości mogą mieć tooupdate go.
* **Alerty** domyślnie wysyłane tooyou Jeśli błędy występują w trzech miejscach ponad pięć minut. Błąd w jednej lokalizacji jest toobe prawdopodobnie problem z siecią, a nie na problem z witryną. Ale można zmienić toobe próg hello więcej lub mniej liter, a można też zmian, który hello wiadomości e-mail powinny być przesyłane do.

    Skonfigurować można również [element webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md), który jest wywoływany w momencie zgłoszenia alertu. Należy jednak pamiętać, że obecnie parametry zapytania nie są przekazywane jako właściwości.

### <a name="test-more-urls"></a>Testowanie większej liczby adresów URL
Dodaj więcej testów. Na przykład w tootesting dodanie strony głównej możesz mieć pewność, że baza danych działa testując URL hello wyszukiwania.


## <a name="monitor"></a>3. Wyświetlanie wyników testów dostępności

Po kilku minutach, kliknij przycisk **Odśwież** toosee wyników testu. 

![Podsumowanie wyników w bloku macierzystego hello](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

Witaj scatterplot przedstawiono przykłady hello wyniki testów, które mają szczegółów diagnostycznych krok testu w nich. Hello aparatu testów są przechowywane szczegóły diagnostyczne dla testów z błędami. Pomyślnie testy dla podzbioru wykonaniami hello są przechowywane szczegóły diagnostyczne. Umieść kursor na jeden z sygnatury czasowej hello punktów zielony i czerwony toosee hello testu, czas trwania testu, lokalizację i nazwę testu. Kliknij przycisk za pomocą dowolnego kropką w hello punktowy kreślenia toosee hello szczegóły wyniku testu hello.  

Wybierz poszczególnego testu, lokalizacji, lub Zmniejsz czas hello okresu toosee więcej wyników wokół hello okresie zainteresowań. Użyć Eksploratora wyszukiwania toosee wyniki wszystkich wykonaniami lub analityka zapytania toorun niestandardowych raportów na tych danych.

W dodatku toohello nieprzetworzone wyniki istnieją dwa metryki dostępności w Eksploratorze metryk: 

1. Dostępności: Procent hello testów, które zakończyły się pomyślnie we wszystkich wykonania testu. 
2. Czas trwania testu: średni czas trwania testu dla wszystkich wykonań testów.

Filtry można stosować na powitania nazwa testu, trendów tooanalyze lokalizacji poszczególnego testu i/lub lokalizacji.

## <a name="edit"></a> Sprawdzanie i edytowanie testów

Na stronie Podsumowanie hello wybierz specyficznego testu. Strona ta będzie zawierać określone wyniki, można ją również edytować lub wyłączać.

![Edytowanie lub wyłączanie testu sieci Web](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

Możesz toodisable testów dostępności lub alertu hello reguł skojarzonych z nimi podczas wykonywania konserwacji w usłudze. 

## <a name="failures"></a>Jeśli widzisz błędy
Kliknij czerwoną kropkę.

![Kliknij czerwoną kropkę](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


Na podstawie wyniku testu dostępności możesz:

* Sprawdź, czy odpowiedź hello otrzymanego z serwera.
* Otwórz hello danych telemetrycznych wysłanych przez serwer aplikacji podczas przetwarzania wystąpienia nieudanych żądań hello.
* Logowania problemu lub element roboczy w problemu hello tootrack Git lub VSTS. Błąd Hello będzie zawierać zdarzenie toothis łącze.
* Otwórz hello wyniku testu sieci web w programie Visual Studio.


*Test wygląda dobrze, ale jest raportowany jako błąd?* Sprawdź wszystkie obrazy hello, skryptów, arkusze stylów i inne pliki załadowanych przez hello strony. Żadnego z nich nie powiedzie się, testu hello jest zgłaszane jako zakończony niepowodzeniem, nawet w przypadku ładowania strony głównej html hello OK.

*Brak powiązanych elementów?* Jeśli usługa Application Insights została skonfigurowana dla aplikacji po stronie serwera, może to być spowodowane trwaniem [próbkowania](app-insights-sampling.md). 

## <a name="multi-step-web-tests"></a>Wieloetapowe testy sieci Web
Możliwe jest monitorowanie scenariusza, który obejmuje sekwencję adresów URL. Na przykład jeśli monitorowany sprzedaży witryny sieci Web, można sprawdzić czy dodawanie elementów toohello koszyk działa poprawnie.

> [!NOTE] 
> Za wieloetapowe testy sieci Web są naliczane opłaty. [Schemat cennika](http://azure.microsoft.com/pricing/details/application-insights/).
> 

toocreate badanie wieloetapowych, z należy zarejestrować hello scenariusza za pomocą programu Visual Studio Enterprise, a następnie przekaż hello rejestrowania tooApplication szczegółowych informacji. Usługi Application Insights odtwarzaniem scenariusz hello w odstępach czasu i weryfikuje hello odpowiedzi.

> [!NOTE]
> W testach nie można używać pętli ani funkcji kodowanych. Hello testu musi być całkowicie zawarty w hello .webtest skryptu. Można jednak używać wtyczek standardowych.
>

#### <a name="1-record-a-scenario"></a>1. Nagrywanie scenariusza
Użyj programu Visual Studio Enterprise toorecord sesji sieci web.

1. Utwórz projekt testu wydajności sieci Web.

    ![W programie Visual Studio Enterprise edition Utwórz projekt z szablonu hello wydajności sieci Web i testów obciążenia.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * *Nie widzisz hello wydajności sieci Web i testów obciążenia szablonu?* — Zamknij program Visual Studio Enterprise. Otwórz **Instalator programu Visual Studio** toomodify instalację programu Visual Studio Enterprise. W obszarze **Poszczególne składniki** wybierz pozycję **Narzędzia do testowania obciążenia witryn sieci Web i aplikacji**.

2. Otwórz plik .webtest hello i rozpocząć nagrywanie.

    ![Otwórz plik .webtest hello i kliknij przycisk Zarejestruj.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. Witaj akcje użytkownika, które mają toosimulate w teście sieci: Otwórz witryny sieci Web, Dodaj do koszyka toohello produktu i tak dalej. Następnie zatrzymaj test.

    ![Witaj w sieci web testów uruchamia Rejestrator w programie Internet Explorer.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    Scenariusz nie powinien być długi. Jest ograniczony do 100 kroków i 2 minut.
4. Edytuj test hello w celu:

   * Dodawanie operacji sprawdzania poprawności toocheck hello Odebrano tekst i odpowiedzi kodów.
   * Usunąć zbędne interakcje. Można również usunąć zależnych żądań dla obrazów lub tooad lub śledzenia witryny.

     Należy pamiętać, można edytować tylko hello skryptu test - nie można dodać kod niestandardowy lub wywołać inne testy sieci web. Nie należy wstawić pętle hello testu. Możesz używać standardowych wtyczek testów sieci Web.
5. Uruchom hello test w Visual Studio toomake się, że działa.

    Moduł uruchamiający Hello sieci web otwiera w przeglądarce sieci web i powtarza hello akcje zarejestrowane. Upewnij się, że działanie jest zgodne z oczekiwaniami.

    ![W programie Visual Studio Otwórz plik .webtest hello i kliknij przycisk Uruchom.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a>2. Przekaż tooApplication testu sieci web hello Insights
1. W portalu usługi Application Insights hello Utwórz test sieci web.

    ![W bloku testy sieci web hello wybierz przycisk Dodaj.](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. Wybierz badanie wieloetapowych i przekazać plik .webtest hello.

    ![Wybieranie wieloetapowego testu sieci Web.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    Zestaw hello testu lokalizacje, częstotliwość oraz parametry alertu w hello sam sposób jak w przypadku ping testy.

#### <a name="3-see-hello-results"></a>3. Zobacz hello wyników

Wyświetl test wyników i niepowodzeniach hello sam sposób jak jednym — testami adresu url.

Ponadto możesz pobrać tooview wyników testu hello je w programie Visual Studio.

#### <a name="too-many-failures"></a>Zbyt wiele niepowodzeń?

* Typową przyczyną błędu jest hello test działa zbyt długo. Nie może trwać dłużej niż dwie minuty.

* Pamiętaj, że wszystkie zasoby hello strony należy poprawnie załadować dla hello toosucceed testu, w tym skrypty, arkusze stylów, obrazy i tak dalej.

* Witaj testu sieci web musi być całkowicie zawarty w hello .webtest skryptu: nie można użyć funkcji kodowane w teście hello.

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a>Dodawanie wtyczek czasu i liczb losowych do testu wieloetapowego
Załóżmy, że testujesz narzędzie, które pobiera dane zależne od czasu (np. ceny akcji) z zewnętrznego źródła. Podczas rejestrowania testu sieci web ma toouse w określonym czasie, ale ustawienia jako parametry hello przetestować, wartości StartTime i EndTime.

![Test sieci Web z parametrami.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

Po uruchomieniu testu hello, chcesz EndTime zawsze toobe hello przedstawia czas, i wartość StartTime powinna być 15 minut temu.

Wtyczki testu sieci Web pozwalają hello toodo parametryzacja razy.

1. Dodaj wtyczkę testu sieci Web do każdej wartości parametru zmiennej, która jest potrzebna. Witaj narzędzi testu sieci web, wybierz **Dodaj wtyczkę testu sieci Web**.

    ![Wybierz polecenie Dodaj wtyczkę testu sieci Web i wskaż jej typ.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    W tym przykładzie używamy dwa wystąpienia hello daty czasu wtyczek. Jedno wystąpienie odpowiada wartości „15 minut temu”, a drugie „teraz”.
2. Otwórz właściwości hello każdy dodatek plug-in. Nadaj mu nazwę i ustaw ją toouse hello bieżącego czasu. W jednej z wtyczek ustaw właściwość Dodaj minuty = -15.

    ![Ustawianie właściwości Nazwa, Użyj czasu bieżącego i Dodaj minuty.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. W hello parametry testu sieci web Użyj {{nazwa wtyczki}} tooreference nazwa dodatku.

    ![W parametrze testu hello Użyj {{nazwa wtyczki}}.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

Teraz Przekaż portalem toohello testu. Używa wartości dynamiczne hello każdym uruchomieniu testu hello.

## <a name="dealing-with-sign-in"></a>Obsługa logowania
Jeśli użytkownicy logują się tooyour aplikacji, istnieją różne opcje symulacji logowania, dzięki czemu można przetestować strony logowania hello. podejście Hello, którego używasz, zależy od typu hello zabezpieczenia zapewniane przez aplikacji hello.

We wszystkich przypadkach należy utworzyć konto w aplikacji tylko w celu hello testów. Jeśli to możliwe uprawnienia hello tego konta testu, aby nie było możliwości testów sieci web hello wpływających na rzeczywistych użytkowników.

### <a name="simple-username-and-password"></a>Prosta nazwa użytkownika i hasło
Rejestrowania testu sieci web w hello zwykły sposób. Najpierw usuń pliki cookie.

### <a name="saml-authentication"></a>Uwierzytelnianie SAML
Użyj hello SAML wtyczkę, która jest dostępna dla testów sieci web.

### <a name="client-secret"></a>Klucz tajny klienta
Jeśli aplikacja ma trasę logowania, która obejmuje klucz tajny klienta, użyj tej trasy. Azure Active Directory (AAD) to przykład usługi, która umożliwia logowanie za pomocą klucza tajnego klienta. W usłudze AAD klucz tajny klienta hello jest hello klucz aplikacji.

Poniżej przedstawiono przykładowy test sieci Web aplikacji sieci Web platformy Azure przy użyciu klucza aplikacji:

![Przykład klucza tajnego klienta](./media/app-insights-monitor-web-app-availability/110.png)

1. Pobierz token z usługi AAD przy użyciu klucza tajnego klienta (AppKey).
2. Wyodrębnij token elementu nośnego z odpowiedzi.
3. Wywołanie interfejsu API w nagłówku autoryzacji hello przy użyciu tokenu elementu nośnego.

Upewnij się, że test sieci web hello jest klienta faktycznie - oznacza to, że ma własną aplikację w usłudze AAD - i użyj jej clientId + appkey. Usługi w ramach testu ma również własnej aplikacji w usłudze AAD: hello appID URI tej aplikacji jest widoczny w hello testu sieci web w polu "zasobu" hello.

### <a name="open-authentication"></a>Uwierzytelnianie otwarte
Przykładem uwierzytelniania otwartego jest logowanie przy użyciu konta Microsoft lub Google. Wiele aplikacji czy zastosowaniem OAuth hello zamiast tajny klienta, więc Twoje pierwsze działanie powinno być tooinvestigate tej możliwości.

Jeśli test muszą logować się za pomocą uwierzytelniania OAuth, hello ogólne podejście jest:

* Za pomocą narzędzia, takie jak Fiddler tooexamine hello ruch między przeglądarki sieci web, hello uwierzytelniania witryn i aplikacji.
* Wykonaj co najmniej dwa logowania przy użyciu różnych maszyn lub przeglądarki, lub w odstępach długi (tooallow tokenów tooexpire).
* Porównując różne sesje zidentyfikować tokenu hello przekazanego z hello uwierzytelniania lokacji, które są następnie przekazywane tooyour serwera aplikacji po zalogowaniu.
* Nagraj test sieci Web przy użyciu programu Visual Studio.
* Parametryzacja hello tokenów, ustawienie dla parametru hello, gdy hello token jest zwracany z Witaj wystawca uwierzytelnienia i używanie go na powitania zapytania toohello lokacji.
  (Visual Studio prób tooparameterize hello testu, ale poprawnie nie parametryzacja tokeny hello).


## <a name="performance-tests"></a>Testy wydajności
W witrynie sieci Web można uruchomić test obciążenia. Jak hello test dostępności możesz wysłać żądania prostego lub wieloetapowych żądań z naszych punktów wokół hello world. W przeciwieństwie do testu dostępności wysyłanych jest wiele żądań symulujących wielu równoczesnych użytkowników.

W bloku omówienie hello Otwórz **ustawienia**, **testy wydajności**. Podczas tworzenia testu zaproszono Cię tooconnect tooor Utwórz konto Visual Studio Team Services.

Po zakończeniu testu hello są wyświetlane czasów odpowiedzi i odsetka pomyślnych.


![Test wydajności](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> Użyj tooobserve hello skutków w teście wydajności [strumień na żywo](app-insights-live-stream.md) i [profilera](app-insights-profiler.md).
>

## <a name="automation"></a>Automatyzacja
* [Użyj tooset skrypty programu PowerShell w górę test dostępności](app-insights-powershell.md#add-an-availability-test) automatycznie.
* Konfigurowanie [elementu webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) który jest wywoływany przy zgłaszaniu alertu.

## <a name="qna"></a>Pytania? Problemy?
* *Czy mogę wywołać kod z mojego testu sieci Web?*

    Nie. kroki Hello hello testu musi być w pliku .webtest hello. Nie można też wywoływać innych testów sieci Web ani używać pętli. Istnieje jednak kilka wtyczek, które mogą być przydatne.
* *Czy jest obsługiwany protokół HTTPS?*

    Obsługujemy protokół TLS 1.1 i TLS 1.2.
* *Czym różnią się „testy sieci Web” i „testy dostępności”?*

    Witaj dwie warunki można odwoływać się zamiennie. Badania dostępności jest terminem bardziej ogólnym, zawierającą hello pojedynczego adresu URL ping Ponadto testy testy sieci web wieloetapowych toohello.
* *Chcę testów dostępności toouse na naszym wewnętrznego serwera, który uruchamia się za zaporą.*

    Istnieją dwa możliwe rozwiązania:
    
    * Skonfiguruj swoje zapory toopermit żądania przychodzące z hello [agenci testowi adresów IP z naszych web](app-insights-ip-addresses.md).
    * Napisać własny kod testu tooperiodically wewnętrznego serwera. Uruchom kod hello jako proces w tle na serwerze testowym za zaporą. Procesu testowania można wysyłać wyniki tooApplication Insights przy użyciu [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) interfejsu API w pakiecie SDK hello core. Wymaga to testu serwera toohave wychodzących dostępu toohello usługi Application Insights wprowadzanie punktu końcowego, ale jest to znacznie mniejszy zagrożenie bezpieczeństwa niż alternatywna hello zezwalającego żądań przychodzących. Witaj wyniki nie będą wyświetlane w blokach testy sieci web dostępności hello, ale pojawia się jako wyniki dostępności w Analytics, wyszukiwanie i Eksplorator metryki.
* *Przekazywanie wieloetapowego testu sieci Web kończy się niepowodzeniem*

    Limit rozmiaru to 300 KB.

    Pętle nie są obsługiwane.

    Testy sieci web tooother odwołań nie są obsługiwane.

    Źródła danych nie są obsługiwane.
* *Mój test wieloetapowy nie jest wykonywany w całości*

    Istnieje limit 100 żądań na test.

    Hello test jest zatrzymana, jeśli jest uruchomione dłużej niż dwie minuty.
* *Jak uruchomić test z wykorzystaniem certyfikatów klienta?*

    Niestety nie jest to obsługiwane.


## <a name="next"></a>Następne kroki
[Dzienniki diagnostyczne usługi Search][diagnostic]

[Rozwiązywanie problemów][qna]

[Adresy IP agentów testów sieci Web](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
