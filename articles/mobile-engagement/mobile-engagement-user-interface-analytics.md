---
title: "aaaAzure Mobile Engagement interfejsu użytkownika — analiza"
description: "Dowiedz się, jak tooanalyze danych historycznych dotyczących aplikacji za pomocą usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4a9df11226fed6710cfb1337ae84ece7596d482f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooanalyze-historical-data-about-your-application"></a>Jak tooanalyze danych historycznych dotyczących aplikacji
W tym artykule opisano hello **ANALYTICS** kartę hello **Mobile Engagement** portalu. Użyj hello **Mobile Engagement** toomonitor portalu i zarządzania aplikacjami mobilnymi. Należy pamiętać, że toostart przy użyciu portalu hello, musisz najpierw toocreate **usługi Azure Mobile Engagement** konta.

Hello Analytics części hello interfejsu użytkownika zawiera zagregowane informacje na temat aplikacji na podstawie danych historycznych, która jest aktualizowana co 24 godziny. Witaj informacje są wyświetlane na różnych pulpity nawigacyjne składa się z wykresy kołowe/paska/linii siatki i mapy. można również pobrać Hello danych jako pliki CSV. Większość tych informacji jest dostępnych w czasie rzeczywistym w hello Monitor części hello interfejsu użytkownika i mogą również uzyskiwać z hello analizy interfejsu API.

> [!NOTE]
> Wiele sekcji hello **Mobile Engagement** interfejsu użytkownika portalu zawierają hello **Pokaż Pomoc** przycisku. Naciśnij ten przycisk tooget więcej informacje kontekstowe dotyczące sekcji.

## <a name="standard-and-custom-analytics"></a>Standardowe i niestandardowe analityka
Usługa Azure Mobile Engagement udostępnia zestaw podstawowa, standardowa analityczne informacji o aplikacjach, które mogą zostać wyświetlone na wykresie zaraz po zintegrowaniu z hello zestawu SDK aplikacji. Usługa Azure Mobile Engagement udostępnia również hello możliwości toogather dalszej analizy niestandardowych informacji dotyczących zachowania użytkowników końcowych. Można to zrobić przez utworzenie planu tagu "Znaczniki niestandardowe (app-info)", utworzone na podstawie **ustawienia** tak, aby zebrać dodatkowe dane usługi Azure Mobile Engagement dla Ciebie.

## <a name="analytics"></a>Analiza
* Pulpit nawigacyjny: Zawiera ogólne informacje o nowych i uaktywnia użytkowników i ich trendów.
* Użytkownicy: Użytkownicy są identyfikowani na podstawie identyfikatora urządzenia: ten identyfikator jest unikatowy dla każdego urządzenia (jeden nowy użytkownik to w rzeczywistości jedno nowe urządzenie). Użytkownik jest uznawany co nowego w danym przedziale czasu, jeśli wykonał swoją pierwszą sesję w tym przedziale czasu. Użytkownik jest uznawany za zachowanego, jeśli wykonał co najmniej jedną sesję w ciągu hello ostatnich 7 dni. Aktywni użytkownicy są użytkownikami, wprowadzone w co najmniej jedną sesję w danym okresie. Można sortować według, co miesiąc, co tydzień, codziennie lub co godzinę okresów. Wszystkie wykresy hello wyglądać podobnie, ale pozwala toofilter przez różne funkcje, takie jak hello wersji aplikacji, a następnie toosort przez pewien czas. Witaj standardowe informacje zebrane przez integrację hello SDK zawiera następujące hello: aktywni użytkownicy, nowy użytkownik, liczbę sesji, długość każdej sesji, informacje techniczne dotyczące kraju hello, zmienne lokalne, lokalizacji, operator języka, urządzeń, oprogramowania układowego, sieć (Wi-Fi), wersje aplikacji hello i zestawu SDK, używanych przez klientów. Informacje te można wyświetlić w czasie rzeczywistym z sekcji monitor hello.

> [!NOTE]
> Hello przedziale czasu opiera się na datę hello z ustawień urządzenia użytkownika hello, więc użytkownika, którego telefon ma niepoprawnie ustawione Data hello mogą pojawiać się w hello niewłaściwy przedziale czasu.

* Przechowywania: Użytkownik jest uznawany za zachowanego w danym przedziale czasu, jeśli wykonał swoją pierwszą sesję w tym przedziale czasu. Można zmienić hello przedziały czasu, w których zachowanych użytkowników (i nowi użytkownicy) są zliczane toohours, dni, tygodnie lub miesiące. analizowanie przechowywania użytkowników Hello jest oparty na stado. Kohorty jest zestawem hello wszyscy hello nowi użytkownicy wykryto dla danego okresu (tj. hello zbiór użytkowników wykonywania ich pierwszej sesji podczas tego okresu). Używamy stado 1-dniowego, 2-dniowego, 4-dniowego, 7-dniowe lub 1-miesięcznego. Podany kohorty, każdego dnia 1, 2-dniowego, 4-dniowego, 7-dniowe lub 1-miesięcznego usługi Azure Mobile Engagement oblicza hello zbiór wszystkich użytkowników, który należy kohorty toohello i są nadal aktywne (tj. hello zbiór użytkowników, którzy wykonać co najmniej jedną sesję w okresie hello). Ten zbiór użytkowników, nosi nazwę wersji kohorty. (Usługa azure Mobile Engagement można stwierdzić, ile użytkownicy nadal używają aplikacji, ale tylko magazynu określonych platform hello pomagają stwierdzić, ile użytkowników odinstalowywania programu iTunes app — na przykład GooglePlay, Sklep Windows, itp.).
* Sesje: Jedno użycie aplikacji hello przez użytkownika. Sesje są generowane na podstawie hello sekwencji działań wykonywanych przez użytkowników (działanie jest zazwyczaj skojarzony toohello użycie jednego ekranu aplikacji hello, a to może się różnić w zależności od hello sposób hello został zintegrowany zestaw SDK aplikacji hello). Użytkownik naraz może wykonywać tylko jedno działanie: sesja rozpoczyna się natychmiast hello użytkownik rozpoczyna swoje pierwsze działanie i zatrzymywana, gdy użytkownik kończy swoje ostatnie działanie. Jeśli użytkownik pozostaje więcej niż kilka sekund, bez wykonywania żadnych działań, sekwencja działań jest podzielony na dwie różne sesje.
* Działania: hello nazwy każdego ekranu w aplikacji i długość hello użytkowników spędzają na każdym ekranie. Działania są niestandardowych opcji analityczne odpowiadające toohello "informacje o aplikacji" tagów, które zostały skonfigurowane dla aplikacji:
* Ścieżka użytkownika: Pokazuje, jak użytkownicy nawigują między działaniami aplikacji (ekranami). Można przenieść hello suwaka tooadjust hello poziom szczegółów. Niebieskie węzły reprezentują działania aplikacji. Ich rozmiar jest proporcjonalny toohello czas, jaki użytkownik poświęcił na ich. Białe węzły reprezentują rozpoczęcie i zakończenie sesji. Czerwone węzły reprezentują awarie. Połączenia reprezentują przejścia między działaniami aplikacji (lub między działaniami i awariami). Kliknij węzeł lub toodisplay łącze etykietkę zawierającą więcej informacji na temat danych: hello czas spędzony na konkretnym ekranie, hello liczbę przejść i procent przejść z działania docelowego toohello działania źródłowego hello hello. (---60%---> B oznacza, że użytkownicy z działania umieszczane tooactivity B 60% przypadków hello.) Reorganizować hello wykres można dowolnie tooclarify; jego położenie jest zapisywane po każdej dokonanej zmianie. Możesz wyświetlić lub ukryć hello awarii toolighten hello wykresu.
* Zdarzenia: Określone akcje wykonywane przez użytkownika w aplikacji hello. Witaj dystrybucję zdarzeń jest wyświetlany jako hello liczba zdarzeń na użytkownika na sesji. Zdarzenie reprezentuje natychmiastową akcję, na przykład kliknięcie przycisku lub hello odebranie powiadomienia. (znaczenie hello zdarzeń zależy sposób hello SDK został zintegrowany aplikacji hello.) Zdarzenie może wystąpić podczas sesji, zadania lub być autonomiczne.
* Zadania: Tooevents podobny, z wyjątkiem one skupić się na długość hello hello akcji. Na przykład zadania można zorientować się informacje techniczne dotyczące czasu wykonywania tooload zawartości lub usługi tooweb wywołania. Go można również pokazać, jak długo trwa toofill użytkownika, formularz, tworzenie konta usługi lub jej zakup. Zadanie reprezentuje hello czas trwania zadania, na przykład hello czas trwania zadania pobierania lub hello czasu transparentu jest wyświetlany na ekranie powitania. (znaczenie hello zadań zależy sposób hello SDK został zintegrowany aplikacji hello.) Zadania są zwykle skojarzone z zadaniami w tle, które są wykonywane poza zakresem hello sesji (tzn. bez żadnego działania użytkownika).
* Technicals: Informacje techniczne o urządzeniach hello hello użytkowników aplikacji można śledzić, takie jak hello rozmiar ustawień regionalnych, operatora sieci, urządzenia, oprogramowania układowego i ekranu urządzenia użytkowników hello i hello wersji aplikacji i hello używana wersja zestawu SDK w aplikacji.
* Błędy: Informacje na temat błędów technicznych wewnątrz aplikacji hello, które nie powodują hello toocrash aplikacji. (Error) reprezentuje natychmiastowy problem, na przykład awaria sieci lub zła manipulacja. (znaczenie hello zdarzeń zależy sposób hello SDK został zintegrowany aplikacji hello.) Wystąpił błąd może wystąpić podczas sesji, zadania lub być autonomiczne.
* Awarii (Crash): Informacje o błędach, które powodują toocrash Twojej aplikacji. Awaria jest nieoczekiwany warunek, w którym aplikacji hello przestaje wykonywać oczekiwane funkcje i musi zostać zatrzymana. Awaria jest zwykle powodu usterki tooa w aplikacji hello.

![Analytics2][11]

## <a name="accessing-hello-retention-overview"></a>Uzyskiwanie dostępu do hello przechowywania — omówienie
![Analytics3][12]

Omówienie przechowywania Hello dzieli się w środku hello na kilka kart, omówienie hello przedstawiający każdego okresu przechowywania. okres przechowywania 2-dniowego Hello jest widoczna w przykładzie hello. Witaj inne karty Pokaż okresów przechowywania 4-dniowego i 7-dniowe hello.

## <a name="understanding-hello-retention-overview-cards"></a>Opis hello omówienie przechowywania kart
![Analytics4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a>Każda karta składa się z 3 główne części:
1. 1: hello kohorty i okres hello traktowane jako
2. 2-4: hello bieżącego okresu przechowywania dla hello
3. 5: wykres przebiegu w czasie hello historii

### <a name="here-is-detailed-information-about-each-element"></a>Poniżej przedstawiono szczegółowe informacje o każdym elemencie:
1. Kohorty i okres: hello typu kohorty daje tego nagłówka. W tym miejscu "2-dniowego okresu" oznacza, że zajmiemy hello zachowania użytkowników ponad 2 dni, użytkowników, które dotarły w okresie 2 dni oraz tego, czy łączą w powitania po bloki 2 dni. w powyższym przykładzie Hello uwzględnia hello aktywności użytkowników na powitania 21 i 22 listopada.
2. Dzięki temu częstotliwość przechowywania hello za pośrednictwem hello 21 i 22 listopada dla użytkowników hello w 19 i 20 listopada. W tym miejscu było 1 aktywnego użytkownika między hello 21 i 22, za pośrednictwem hello 3, które były nowych użytkowników między hello 19th i 20.
3. To zapewnia wizualnej hello tych samych informacji dotyczących powyżej zaprezentowana graficznie. (hello trzecia programu hello okrąg ma wartość numeru 33% hello.) kolor Hello zapewnia dodatkowe informacje: zielony oznacza rośnie z poprzednich obliczenia hello ten numer. Żółty oznacza stabilny, a czerwony oznacza zmniejszenie.
4. To ustawienie określa hello wartości używane do obliczania hello.
5. Jest to wykres przebiegu w czasie historii hello hello przechowywania wartości. Umożliwia toosee hello wartości w hello poza toohave szeroki obraz jak ewoluował.

## <a name="see-also"></a>Zobacz też
* [Pojęcia][Link 6]
* [Usługa Przewodnik rozwiązywania problemów][Link 24]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md
