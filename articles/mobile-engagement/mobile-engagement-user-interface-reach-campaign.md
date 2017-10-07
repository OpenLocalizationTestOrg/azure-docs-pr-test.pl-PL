---
title: "aaaAzure Mobile Engagement interfejsu użytkownika — osiągnąć kampanii"
description: "Laern jak toocreate i zarządzać nimi za pomocą usługi Azure Mobile Engagement kampanii obejmujących wysyłanie powiadomień wypychanych"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a>Jak toocreate kampanii powiadomień wypychanych i zarządzanie nimi
Za pomocą hello Reach części toocreate interfejsu użytkownika hello nową kampanię wypychania i złożone formuły podając wszystkie informacje hello potrzebne toosend powiadomienie wypychane. Witaj opcje kampanii wypychania się nieco różnić w zależności od typów kampanii hello czterech: anonsów, ankiety, dane wypychane i Kafelki (tylko Windows Phone).

### <a name="option-applies-to"></a>Opcja ma zastosowanie do:
* Języki: Wszystkie (anonse, ankiety, wypychania danych, Kafelki)
* Kampania: Wszystkie (anonse, ankiety, wypychania danych, Kafelki)
* Powiadomienie: Anonse, ankiety
* Zawartość: Unikatowy dla każdego typu kampanii
* Grupy odbiorców: Wszystkie (anonse, ankiety, wypychania danych, Kafelki)
* Przedział czasu: Kafelki anonse, ankiety,
* Testowanie: Wszystkie (anonse, ankiety, wypychania danych, Kafelki)

![Reach Campaign1][20]

## <a name="languages"></a>Języki
Możesz użyć toosend menu hello rozwijanej języki innej wersji toodevices Twojego wypychania, są ustawione toouse w różnych językach. Domyślnie wszystkie urządzenia będą otrzymywać hello Push sama niezależnie od tego, jakie są ustawione toouse. Użytkownicy z ich urządzeń zestaw tooa innego języka będą otrzymywać wersji język domyślny hello hello wypychania. Wiele opcji kampanii wypychania hello pozwalają toospecify alternatywny zawartości dla każdego z języków dodatkowe hello, którą wybierzesz. 

![Reach Campaign2][21]

### <a name="language-differences-apply-to"></a>Różnice języka dotyczą:
* Języki: Unikatowy języków można wybrać w języku domyślnym toohello dodanie
* Kampania: Takie Same dla wszystkich języków
* Powiadomienie: Unikatowy dla każdego języka dodatkowo toohello język domyślny
* Zawartość: Unikatowy dla każdego języka dodatkowo toohello język domyślny
* Grupy odbiorców: Mogą być filtrowane według kryterium oddzielne języka
* Przedział czasu: tej samej dla wszystkich języków
* Testowanie: Mogą być wysyłane języka tooeach naraz

### <a name="supported-languages"></a>Obsługiwane języki:
* Arabski (ar) 
* Bułgarski (bg) 
* Katalońskim (ca) 
* Chiński (zh) 
* Chorwacki (hr) 
* Czech (CS) 
* Duński (da) 
* Holenderski (Holandia) 
* Angielski (en) 
* Fiński (fi) 
* Francuski (fr) 
* Niemiecki (de) 
* Grecki (el) 
* Hebrajski (osoba) 
* Hindi (cześć) 
* Węgierski (hu) 
* Indonezyjski (id) 
* Włoski (go) 
* Japoński (ja) 
* Koreański (ko) 
* Łotewski (lv) 
* Litewski (lt) 
* Malajski (macrolanguage) (ms) 
* Norweski, Bokmål (nb) 
* Polski (pl) 
* Portugalski (pt) 
* Rumuński (ro) 
* Rosyjski (ru) 
* Serbski (sr) 
* Słowacki (sk) 
* Słoweński (sl) 
* Hiszpański (es) 
* Szwedzki (sv) 
* Tagalski (tl) 
* Tajski (th) 
* Turecki (tr) 
* Ukraiński (Zjednoczone Królestwo) 
* Wietnamski (IV) 

## <a name="campaign"></a>Kampanii
Używając hello kampanii sekcji tooset hello nazwy i Kategoria kampanii również tak, jakby planowanie tooignore hello odbiorców sekcji kampanii wypychania i zamiast tego Wyślij kampanii za pośrednictwem interfejsu API Reach hello (i niektóre elementy z niskim poziomem hello Push interfejsu API). Kategorie można łączyć z szablonu niestandardowego powiadomień toocontrol powiadomienia w aplikacji na podstawie wstępnie zdefiniowanych ustawień. Można uzyskać listę istniejących "kategorii" za pośrednictwem interfejsu API Reach hello.

> [!WARNING]
> Jeśli używasz opcji "Ignoruj odbiorców, powiadomienia wypychane będą wysyłane toousers za pośrednictwem interfejsu API hello" hello w sekcji "Kampanii" hello kampanii Reach kampanii hello nie będzie automatycznie wysyłać, konieczne będzie toosend go ręcznie za pomocą interfejsu API Reach hello.

![Reach Campaign3][22]

### <a name="option-applies-to"></a>Opcja ma zastosowanie do:
* Nazwa: wszystkie
* Kategoria: Anonse, ankiety
* Ignoruj odbiorców, wypychane będą wysyłane toousers za pośrednictwem interfejsu API hello: wszystkie

## <a name="notification"></a>Powiadomienia
Umożliwia hello powiadomień sekcji tooset podstawowych ustawień z tym wypychania: hello tytuł hello wypychanie, wiadomość hello, obrazu w aplikacji, czy jest możliwe do odrzucenia. Wiele ustawień powiadomień są platformy toohello określonego urządzenia. Można wybrać, czy Twoje wypychane będą wysyłane "w aplikacji" lub "poza aplikacją" lub oba. (Pamiętać, że użytkownicy mogą "opt w" lub "Wypisz" "poza aplikacji" wypchnięcia na powitania systemu operacyjnego poziomu na ich urządzeniach i usługi Azure Mobile Engagement nie będą się mogli toooverride to ustawienie. Również należy pamiętać, że obsługi interfejsu API Reach hello "w aplikacji" i "out aplikacji" wypchnięcia. Hello Push interfejsu API może być używane toohandle "mieszczą się w aplikacji" zbyt wypchnięcia). Wypchnięcia można dostosować za pomocą obrazów lub zawartość HTML, w tym linków bezpośrednich do konsolidacji poza Twojej aplikacji lub tooanother lokalizacji w aplikacji (zestaw SDK systemu Android 2.1.0 lub nowsze kategorii konwersji wymagane). Możesz zmienić identyfikator ikony lub iOS hello i wysyłania zawartości tekstu lub w sieci web (podręcznego html, adres URL łącza tooanother lokalizacji zawartości wewnątrz lub na zewnątrz aplikacji hello). Można również dzwonek urządzenia z systemem Android lub też z hello wypychania. (Należy pamiętać, że można będzie konieczne hello poprawne uprawnienia zestawu SDK dla systemu Android tooring pliku manifestu lub Włącz wibrację urządzenia). Nie ma żadnych branży standardowe dla systemu Android "szerszej" rozmiary, od rozmiaru ekranu różnią się na każdym urządzeniu, ale obrazy 400 x 100 pracować z prawie każdego rozmiaru ekranu.

### <a name="delivery-types"></a>Typy dostarczania:
* Tylko poza aplikacją: hello powiadomień zostanie dostarczona, gdy użytkownik hello nie korzysta z aplikacji hello.
* Witaj poza tylko powiadomienie aplikacji wymaga certyfikatu od firmy Apple lub Google (certyfikat usługi APNS lub GCM).
* W aplikacji tylko: hello powiadomień zostanie wyświetlona tylko wtedy, gdy aplikacja hello jest uruchomiona.
* powiadomienie Hello używa hello Capptain system dostarczania tooreach hello użytkownika. Witaj układu/wyświetlanie Twoje zamówienie pełni można dostosować.
* Zawsze: Ta opcja zapewnia wysyłanie powiadomień, który aplikacja hello jest uruchomiona lub nie.

![Reach Campaign4][23]

### <a name="option-applies-to"></a>Opcja ma zastosowanie do:
* Powiadomienie: Anonse, ankiety

## <a name="content"></a>Zawartość
Możesz użyć hello sekcji zawartości toomodify hello zawartości anonse, ankiety, dane wypychane i Kafelki (tylko Windows Phone). ustawienie zawartości Hello kampanie wypychania jest typu toohello określonej kampanii. 

### <a name="see-also"></a>Zobacz też
* [Dokumentacja interfejsu użytkownika — osiągnąć — wypychania zawartości][Link 29]

![Reach Campaign5][24]

## <a name="audience"></a>Grupy odbiorców
Możesz użyć hello odbiorców sekcji toodefine listę standardowych elementów toolimit kampanii lub limity kampanii na podstawie niestandardowych kryteriów. Standardowy zestaw opcji tooLimit Hello odbiorców pozwala toopush tooeither nowej lub starej użytkowników czy tylko użytkowników natywnych powiadomień wypychanych. Można również ustawić limit przydziału toolimit hello szereg użytkownicy, którzy otrzymają hello wypychania. Można ręcznie edytować wyrażenie hello jak kampanii jest filtrowany tooinclude co najmniej jednego kryterium tootarget użytkownika. Można ręcznie wpisz wyrażenie odbiorców. Takie wyrażenie musi jawnie definiować hello relację między kryteriami. Kryterium jest opisane przez identyfikator, który musi rozpoczynać się wielką literą i nie może zawierać spacji. Witaj relację między kryteriami hello można opisać za pomocą "i", "lub" operatory "nie", a także "(",")". Przykład: "Criterion1 lub (Criterion1 i nie Criterion2)".

> [!NOTE]
> Wiele osób zawarte w kampanie, po stronie serwera hello przeznaczonych dla skanowania może działać powoli, zwłaszcza, jeśli próba toostart wiele kampanii w hello sam czas.

* Jeśli to możliwe tylko należy uruchomić jeden kampanii.
* W hello najbardziej, tylko rozpoczęcia kampanii cztery naraz.
* Push tylko tooyour aktywnych użytkowników (pole wyboru "Uwzględnij tylko użytkowników osiągalnych przy użyciu natywnych powiadomień wypychanych" i "Uwzględnij tylko aktywnych użytkowników"), aby tylko użytkownikom, którzy nadal mieć zainstalowanej aplikacji hello i korzystać z niego potrzebne toobe skanowania.
  Po zdefiniowaniu odbiorców można użyć hello symulować toofind przycisk limit ile użytkownicy otrzymają ten wypychania. Spowoduje to obliczeniowe hello liczby znanych użytkowników potencjalnie docelowe w ramach tych odbiorców (jest to wartość szacowana na podstawie losowej próbki użytkowników). Należy pamiętać, że użytkownicy, którzy odinstalowali aplikacji hello będą również należeli do tych odbiorców, ale nie można nawiązać połączenia.

### <a name="see-also"></a>Zobacz też
* [Nowe kryterium wypychania - Reach — dokumentacja interfejsu użytkownika][Link 28]

![Reach Campaign6][25]

### <a name="edit-expression"></a>Edytowanie wyrażeń
![Reach Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a>Limit Twojego odbiorców opcja ma zastosowanie do:
* Uwzględnij tylko podzestaw użytkowników: wszystkie (anonse, ankiety, wypycha dane, Kafelki)
* Uwzględnij tylko starych użytkowników: wszystkie (anonse, ankiety, wypycha dane, Kafelki)
* Uwzględnij tylko nowych użytkowników: wszystkie (anonse, ankiety, wypycha dane, Kafelki)
* Uwzględnij tylko bezczynnych użytkowników: Kafelki anonse, ankiety,
* Uwzględnij tylko aktywnych użytkowników: wszystkie (anonse, ankiety, wypycha dane, Kafelki)
* Uwzględnij tylko użytkowników osiągalnych przy użyciu natywnych powiadomień wypychanych: anonse, ankiety

## <a name="time-frame"></a>Przedział czasu
Użyciem hello okresie sekcji tooset hello wypychane będą wysyłane można także pozostawić hello okresie puste toostart hello kampanii natychmiast. Należy pamiętać, że przy użyciu strefy czasowej użytkownicy końcowi hello może rozpocząć kampanii hello dzień wcześniej, niż oczekiwano dla użytkowników końcowych w Azji, a małych partii wypchnięć jednocześnie do wszystkich stref czasowych w przedziale czasu hello hello world dopasowania kampanii wysyłania. Przy użyciu strefy czasowej użytkownicy końcowi hello mogą powodować opóźnienia w kampaniach ponieważ ma ona toorequest hello czasu z telefonu hello przed rozpoczęciem hello wypychania.

> [!NOTE]
> Kampanie, bez daty zakończenia może buforować wypchnięć lokalnie i nadal wyświetlane po ręcznie pełną kampanii. tooavoid tego zachowania, określonej godziny zakończenia kampanii.

### <a name="see-also"></a>Zobacz też
* [Osiągnąć — jak Tos — Planowanie][Link 3] 

![Reach Campaign8][27]

### <a name="settings-apply-to"></a>Ustawienia mają zastosowanie do:
* Przedział czasu: Kafelki anonse, ankiety,

## <a name="test"></a>Testowanie
Można użyć hello testu sekcji toosend urządzenia własne testu tooyour wypychania przed zapisaniem hello kampanii. Jeśli skonfigurowano wszelkie niestandardowe języków dla kampanii, można przetestować wypychania hello w każdego języka. Możesz skonfigurować urządzenia testu z "Moje konto".

> [!NOTE]
> Wypchnięcia nie po stronie serwera, którego dane są rejestrowane, korzystając z przycisku hello zbyt "test", tylko rejestrowane są dane dla kampanie wypychania prawdziwe.

### <a name="see-also"></a>Zobacz też
* [Dokumentacja interfejsu użytkownika — Moje konto][Link 14]

![Reach Campaign9][28]

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

