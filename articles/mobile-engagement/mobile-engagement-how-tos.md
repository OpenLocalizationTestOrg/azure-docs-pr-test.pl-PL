---
title: "aaaAzure Mobile Engagement interfejsu użytkownika — osiągnąć How"
description: "Przegląd interfejsu użytkownika dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4b6dafd09d894214d4c386f5c6f157a77671606f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-using-and-managing-pushes-tooreach-out-tooyour-end-users"></a>Jak tooget uruchomiony przy użyciu i zarządzanie wypchnięcia tooreach tooyour użytkowników końcowych
Po hello zestawu SDK jest w pełni zintegrowany aplikacji, możesz rozpocząć pracę z sekcją hello hello Reach hello interfejsu użytkownika tooPush powiadomienia toohello użytkowników aplikacji.  

## <a name="do-your-first-push-notification-campaign"></a>Czy pierwszy kampanię powiadomień wypychanych
* Upewnij się, że zasięg jest zintegrowana z aplikacji za pomocą hello zestawu SDK. 
* Wybierz aplikację

![First1][1]

* Przejdź do sekcji "Reach" i kliknij przycisk "nowy anons" toohello

![First2][2]

* Utwórz nową kampanię i nadaj jej nazwę
  
![First3][3]

* Wybierz sposób hello powiadomienie ma zostać dostarczony, w aplikacji tylko

![First4][4]

* Utwórz wiadomość hello, które chcesz toopush

![First5][5]

* Tytuł mogą zapisywać na powitania powiadomienia (opcjonalnie).
* Zapisanie zawartości wiadomości wypychanych.
* Możesz przekazać obraz. Należy pamiętać, że rozmiar hello hello pliku nie może przekraczać 32 768 bajtów.
* Masz również tooselect możliwości hello dalsze opcje, ale dla zespołu hello tego samouczka, należy sprawdzić, które później.
* Wybierz typ zawartości hello tylko jako powiadomienie

![First6][6]

* Utworzyć kampanię powiadomień wypychanych i zostanie wyświetlony na liście kampanii.

![First7][7]

## <a name="test-your-push-notification-campaign"></a>Testowanie kampanię powiadomień wypychanych
![Test1][8]

* Zarejestruj urządzenie.
* Kliknij przycisk wyboru hello hello urządzenia ma toopush.
* Kliknij na powitania "Test" przycisk toosend hello wypychania toohello urządzenia.

![Test2][9]

* Aktywuj hello kampanii

![test3][10]

* Teraz, po utworzeniu kampanii wystarczy tooactivate dla toobe powiadomień hello wypychana tooyour użytkowników.

## <a name="send-personalized-pushes"></a>Wysyłanie spersonalizowanych Wypchnięć
* W tym przykładzie tworzy wypychania, w którym kod niestandardowy rabatów jest wprowadzany do powiadomień wypychanych hello.

![Personalize1][11]

Personalizacja działa przez zastąpienie znacznika przez z tagu informacje o aplikacji tak, będziesz mieć toomake się, że użytkownik hello ma hello odpowiednie informacje o aplikacji najpierw zdefiniowane. W tym hello przykład docelowych użytkownicy będą mieć tag informacje o aplikacji o nazwie rebate_code zdefiniowane.
Jak widać powyżej zawartości powiadomienia wypychanego hello obejmuje $ znacznika hello {rebate_code}, która oznacza, że jego toobe zastępuje hello rzeczywistej zawartości tagu informacje o aplikacji hello.

> [!WARNING]
> Tag informacje o aplikacji hello nie jest zdefiniowany dla użytkownika hello, hello użytkownika nie będą otrzymywać hello wypychania.

* wynik

![Personalize2][12]

### <a name="you-can-further-personalize-hello-text-your-notification"></a>Można dodatkowo spersonalizować tekst hello powiadomienia
![Personalize3][13]

* W tym tytuł hello powiadomień hello
* I hello treści wiadomości powitania.
* Wybierz typ hello anonsu (tekstu, widoku lub widok sieci Web)

![Personalize4][14]

### <a name="hello-body-of-an-announcement-may-also-be-personalized-with"></a>Witaj treść powiadomienia mogą również można spersonalizować z:
* adres URL akcji Hello, powinien ma hello toocustomize strona początkowa
* Tytuł Hello
* Treść wiadomości powitania Hello.

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a>Rozróżnianie Your Push Notification (w lub poza aplikacją)
* Wybierz typ hello powiadomień wypychanych, wybierz aplikację, przejdź do sekcji "Reach" toohello, wybierz lub utworzysz kampanii wypychania i przejdź do sekcji "Powiadomienia" toohello.
* Kliknij na "dostarczanie tryb" hello ma.
* Polecenie powitalne "Ograniczanie działania" wyboru Jeśli chcesz, aby powiadomienia hello występuje na określonych działaniami (ekranami).

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a>Dostawy "Tylko poza aplikacją"
![Differentiate2][16]

"Tylko poza aplikacją" tryb dostarczania zapewnia powiadomienie wypychane po zamknięciu aplikacji hello. To powiadomienie wypychane standardowe hello.
Po wybraniu "tylko poza aplikacją", musi już podano hello certyfikatów z hello platforma, która tworzy aplikację na (APN lub GCM).

### <a name="see-also"></a>Zobacz też
* [Certyfikatów Apple Push Notification Service —](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging — certyfikat](http://developer.android.com/google/gcm/index.html) 

### <a name="in-app-only-delivery-mode"></a>"w aplikacji tylko" dostawy
![Differentiate3][17]

Dostawy "W aplikacji tylko" zapewnia powiadomień wypychanych, gdy aplikacja hello jest uruchomiona.
Dla tego powiadomienia nie trzeba toogo za pośrednictwem hello APNS i GCM systemu.
Możesz użyć tooreach system dostarczania w aplikacji hello użytkowników końcowych.
Można w pełni dostosować hello powiadomień i zdecydować, w którym działanie (ekran) hello powiadomienie będzie wyświetlane.

### <a name="anytime-delivery-mode"></a>"W każdej chwili" dostawy
Można wybrać dostawy "W każdej chwili", zapewnia, że użytkownik końcowy czy hello tooreach lub nie jest uruchomiona aplikacja.
Po wybraniu opcji "W każdej chwili" musi już podano hello certyfikatów z hello platforma, która tworzy aplikację (APN lub GCM). 

## <a name="schedule-a-push-campaign"></a>Harmonogram kampanii wypychania
### <a name="plan-toostart-a-campaign"></a>Planowanie tooStart kampanii
![Shedule1][18]

Jest on hello 21 marca i masz toomake anons i być to planowane dla hello 22 marca o północy. Nie masz toostay przed toodo interfejsu hello wypychanej! Można zaplanować z wyprzedzeniem hello dokładne minutę będą wysyłane powiadomienia.

* Usuń zaznaczenie Witaj, "None" wyboru i wybierz czas rozpoczęcia 
* Wybierz hello daty i czasu hello ma toostart hello wypychania kampanii.

### <a name="plan-tooend-a-campaign"></a>Planowanie tooend kampanii
![Shedule2][19]

Ma toostop Twojego kampanii na powitania 25 marca godzinie 3:00, ale wiesz, że użytkownik nie będzie toodo go.
Nie masz toostay przed toopush interfejsu Witaj! Można zaplanować z wyprzedzeniem hello dokładne minutę kampania zostanie zatrzymana.

* Kliknij na powitania "None" wyboru lub wybierz czas zakończenia
* Wybierz hello daty i czasu hello ma toofinish hello wypychania kampanii.

### <a name="end-a-campaign-manually"></a>Ręcznie zakończenia kampanii
![Shedule3][20]

Domyślnie program hello "None" są zaznaczone pola wyboru.
To oznacza, że hello kampania rozpocznie się zaraz po aktywowaniu w hello osiągnąć sekcji i zakończenia, gdy przestanie na powitania osiągną sekcji.

> [!NOTE]
> Kampanie utworzone bez daty zakończenia przechowywania wypychania hello lokalnie na urządzeniu hello i pokazać hello następnym otwarciu aplikacji hello nawet wtedy, gdy kończy się ręcznie hello kampanii.

## <a name="enhance-a-push-notification-with-a-text-view"></a>Ulepszanie powiadomienie wypychane z widoku tekstu
### <a name="what-is-a-text-view"></a>Co to jest widoku tekstu?
![TextView1][21]

Widok tekstu jest okno podręczne z zawartością tekstu. Są one wyświetlane po hello użytkownik końcowy kliknie powiadomienie wypychane hello.
Widok tekstu umożliwia toopresent więcej zawartości tooyour użytkownika końcowego. Dotyczy to również hello możliwości toopresent tooaction wywołanie, takich jak przeskakiwanie tooa strony aplikacji, przekierowywanie magazynu tooa, otwarcie strony sieci web, wysyłanie wiadomości e-mail, uruchamianie wyszukiwania z lokalizacją geograficzną itp...

### <a name="example-text-view"></a>Przykład: Wyświetlanie tekstu
* Utworzyć kampanię powiadomień wypychanych w sekcji "Osiągnąć" hello i nadaj nazwę kampanii

![TextView2][22]

* Wpisz wiadomość hello, która będzie wyświetlana na hello powiadomień.
* Wybierz powiadomienia typ zawartości "tekst" hello

![TextView3][23]

> [!NOTE]
> Po naciśnięciu widoku tekstu, zawsze pochodzi z powiadomienie najpierw. 

* Zdefiniuj tekst hello (po dokonaniu wyboru hello tekst anons zawartości, pojawi się podsekcja hello, umożliwiając toodefine hello tekst, który ma toobe wyświetlane.)

![TextView4][24]

* Wpisz tytuł hello, który będzie wyświetlany u góry hello wiadomość hello.
* Zapisanie zawartości głównego hello hello widoku tekstu.
* Zapisu hello zawartości, który będzie wyświetlany na przycisku akcji hello (przycisku akcji umożliwia toomake aplikacji hello określonej akcji, takich jak otwieranie stron aplikacji hello, przekierowywanie tooan sklepu lub dowolnych źródeł, które można podać).
* Zawartość hello zapisu, który będzie wyświetlany na przycisku zakończenia hello (klikając przycisk Zakończ hello widoku tekstu hello zniknie.)
* Utworzyć kampanię powiadomień wypychanych i pojawi się na liście kampanii hello.

![TextView5][25]

* Aktywuj wypychania powiadomień kampanii toosend hello tekst widoku tooyour użytkowników.

![TextView6][26]

* wynik

![TextView7][27]

* Witaj użytkownik otrzymuje powiadomienie hello i kliknij go.
* Widok tekstu Hello jest wyświetlany jako wyskakujących zezwalanie hello użytkownika toointeract z nim.

## <a name="enhance-a-push-notification-with-a-web-view"></a>Ulepszanie powiadomienie wypychane z widoku sieci Web
### <a name="what-is-a-web-view"></a>Co to jest widok sieci Web?
![WebView1][28]

Widok sieci web jest okno podręczne z zawartością sieci web. Są one wyświetlane, gdy hello użytkownik końcowy kliknie powiadomienie wypychane hello.
Widok sieci web umożliwia toohave poszerzyć interakcję z hello przez użytkownika końcowego.
Dotyczy to również hello możliwości toopresent tooaction wywołanie, takich jak przekierowanie tooApp magazynu, otwarcie strony sieci web, wysyłanie wiadomości e-mail, uruchamianie wyszukiwania z lokalizacją geograficzną itp...

### <a name="example-web-view"></a>Przykład: Widoku sieci Web
* Utworzyć kampanię powiadomień wypychanych w sekcji "Osiągnąć" hello i nadaj nazwę kampanii.

![WebView2][29]

* Wpisz wiadomość hello, która będzie wyświetlana na hello powiadomień.
* Wybierz hello anonsu typu zawartości jako "web".

![WebView3][30]

### <a name="about-announcement-types"></a>O typach anonsu:
* Tylko powiadomienie: jest proste powiadomień w wersji standard. Co oznacza, że jeśli użytkownik go kliknie, bez dodatkowego widoku będą wyświetlane, ale tylko hello akcji skojarzonych tooit nastąpi.
* Tekst anonsu: to powiadomienie, które angażujący toohave użytkownika hello przyjrzeć się widoku tekstu.
* Sieci Web anonsu: to powiadomienie, które angażujący toohave użytkownika hello przyjrzeć się widok sieci web.
  Wybierz hello zawartość "Anonsu Web".

> [!NOTE]
> Po naciśnięciu widoku sieci web, zawsze pochodzi z powiadomienie najpierw.

* Zdefiniuj zawartość sieci web hello (po dokonaniu wyboru hello sieci web anonsu zawartości, pojawi się podsekcji hello, umożliwiając toodefine hello zawartości sieci web widoku ma toobe wyświetlane.)

![WebView4][31]

* Wpisz tytuł hello, który będzie wyświetlany u góry hello wiadomość hello (opcjonalnie).
* Wpisz tutaj swój kod HTML.
* Kliknij źródło hello edition tooswitch przycisk trybu edycji i zobacz, jak wygląda.
* Zapisu hello zawartości, który będzie wyświetlany na przycisku akcji hello (przycisku akcji umożliwia toomake aplikacji hello określonej akcji, takich jak otwieranie stron aplikacji hello, przekierowywanie tooa magazynu lub dowolny rodzaj źródeł, które można podać).
* Zawartość hello zapisu, który będzie wyświetlany na przycisku zakończenia hello (przez kliknięcie przycisku zakończenia hello, widoku sieci web hello zniknie).
* wynik

![WebView5][32]

* Użytkownik Hello hello powiadomienie i kliknij go.
* Widok tekstu Hello jest wyświetlany jako wyskakujących zezwalanie hello użytkownika toointeract z nim.

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

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

