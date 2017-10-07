---
title: "aaaAzure Mobile Engagement interfejsu użytkownika — osiągnąć zawartości"
description: "Dowiedz się, jak kampanie toomanage hello unikatową zawartość hello różnych typów powiadomień wypychanych w usłudze Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a>Jak toomanage hello unikatową zawartość różnych typów hello kampanii obejmujących wysyłanie powiadomień wypychanych
Można użyć sekcji zawartości hello nowe reach kampanii toomodify hello zawartości anonse, ankiety, dane wypychane i Kafelki (tylko Windows Phone). ustawienie zawartości Hello kampanie wypychania jest typu toohello określonej kampanii. 

### <a name="content-types"></a>Typy zawartości:
* Anonse
* Ankiety
* Wypychania danych
* Kafelki (tylko Windows Phone)

## <a name="content-of-announcements"></a>Zawartość anonsów
 ![Reach Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a>Wybierz typ hello anonsu:
* Tylko powiadomienie: jest proste powiadomień w wersji standard. Co oznacza, że jeśli użytkownik go kliknie, bez dodatkowego widoku będą wyświetlane, ale tylko hello akcji skojarzonych tooit nastąpi.
* Tekst anonsu: to powiadomienie, które angażujący toohave użytkownika hello przyjrzeć się widoku tekstu.
* Sieci Web anonsu: to powiadomienie, które angażujący toohave użytkownika hello przyjrzeć się widok sieci web.

### <a name="see-also"></a>Zobacz też
* [Osiągnąć — jak OT - anonsów][Link 3] 

### <a name="about-web-view-announcements"></a>O anonsach widoku sieci Web:
Wystąpienia wzorca hello "{deviceid}" w kodzie hello HTML lub kod JavaScript podana tutaj zostaną automatycznie zastąpione hello identyfikator hello urządzenia wyświetlającego anons hello. Jest to identyfikatory urządzeń łatwy sposób tooretrieve usługi Azure Mobile Engagement w zewnętrznej sieci web usługi hostowanej w zapleczu biura.
Jeśli chcesz, aby toocreate pełnego ekranu widoku sieci web (bez hello domyślnych przycisków akcji i wyjścia udostępniamy) można użyć następujących funkcji z kodu JavaScript anonsu widoku sieci web hello: 

* Wykonaj akcję anonsu hello: ReachContent.actionContent()
* wyjść z anonsów hello: ReachContent.exitContent()

### <a name="choose-your-action"></a>Wybierz akcję:
### <a name="about-action-urls"></a>O adresach URL akcji:
Każdy adres URL, który może zostać zinterpretowany przez system operacyjny urządzenia docelowego, może być używany jako adres URL akcji.
Każdy dedykowany adres URL aplikacji może pomocy technicznej (np. użytkownicy toomake skoku tooa konkretnego ekranu) również może służyć jako adres URL akcji.
Każde wystąpienie wzorca hello {deviceid} jest automatycznie zastępowane hello identyfikator hello urządzenia wykonującego akcję hello. Może to być identyfikatory urządzeń usługi Azure Mobile Engagement używane tooeasily pobrać za pomocą zewnętrznej usługi sieci web hostowanej na zapleczu biura.

* **Android i iOS akcje**
  * Otwórz stronę sieci web
  * http://\[domeny w przypadku witryny sieci web\] 
  * Przykład: http://www.azure.com
  * Wyślij wiadomość e-mail
  * mailto:\[e-mail poczty e-mail odbiorcy\]? podmiotu =\[podmiotu\]& body =\[wiadomości\] 
  * Example:mailto:foo@example.com? podmiotu = pozdrowienia % 20from % 20Azure % 20Mobile % 20Engagement! & body = 20stuff dobrej %!
  * Wyślij wiadomość SMS
  * SMS:\[numer telefonu\] 
  * Przykład: sms:2125551212
  * Wybierz numer telefonu
  * Tel.:\[numer telefonu\] 
  * Przykład: tel:2125551212
* **Android tylko akcje**
  * Pobierz aplikację ze sklepu Play hello
  * Market://details?ID=\[pakiet aplikacji\] 
  * Przykład: market://details?id=com.microsoft.office.word
  * Rozpocznij wyszukiwanie z określoną lokalizacją geograficzną
  * Geo:0, 0? q =\[zapytania wyszukiwania\] 
  * Przykład: geo:0, 0? q = starbucks, Paryża
* **tylko akcje dla systemu iOS**
  * Pobierz aplikację ze sklepu z aplikacjami hello
  * http://iTunes.Apple.com/ [Kraj] /app/ [Nazwa aplikacji] /id [identyfikator aplikacji]? mt = 8 
  * Przykład: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8
  * Akcje systemu Windows
  * Otwórz stronę sieci web
  * http://\[domeny w przypadku witryny sieci web\] 
  * Przykład: http://www.azure.com
  * Wyślij wiadomość e-mail
  * mailto:\[e-mail poczty e-mail odbiorcy\]? podmiotu =\[podmiotu\]& body =\[wiadomości\] 
  * Example:mailto:foo@example.com? podmiotu = pozdrowienia % 20from % 20Azure % 20Mobile % 20Engagement! & body = 20stuff dobrej %!
  * Wyślij wiadomość SMS (wymagana jest aplikacja Skype ze Sklepu)
  * SMS:\[numer telefonu\] 
  * Przykład: sms:2125551212
  * Wybierz numer telefonu (wymagana jest aplikacja Skype ze Sklepu)
  * Tel.:\[numer telefonu\] 
  * Przykład: tel:2125551212
  * Pobierz aplikację ze sklepu Play hello
  * MS-windows-magazynu: strony szczegółów projektu? PFN =\[identyfikator pakietu aplikacji\] 
  * Przykład: ms-windows-magazynu: strony szczegółów projektu? PFN = 4d91298a-07cb-40fb-aecc-4cb5615d53c1
  * Rozpocznij wyszukiwanie na mapach Bing
  * bingmaps:? q =\[zapytania wyszukiwania\] 
  * Przykład: bingmaps:? q = starbucks, Paryża
  * Użyj schematu niestandardowego
  * \[schemat niestandardowy\]://\[parametry schematu niestandardowego\] 
  * Przykład: myCustomProtocol://myCustomParams
  * Użyj danych pakietu (w sklepie dla rozszerzenia odczytu wymagane)
  * \[folder\]\[danych\].\[ rozszerzenia\] 
  * Example:myfolderdata.txt

### <a name="build-a-tracking-url"></a>Utwórz adres URL śledzenia:
* Zobacz sekcję "Ustawienia" hello hello <UI Documentation> dla instrukcje dotyczące tworzenia adres URL śledzenia, który umożliwi użytkownikom toodownload jednego z innych aplikacji.

### <a name="define-hello-texts-of-your-announcement"></a>Zdefiniuj Teksty anonsu hello
Wprowadź tytuł hello, zawartość i przycisk teksty anonsu. Możesz zastosować odbiorców przyszłych kampanii na podstawie opinii reach hello o jak użytkownicy odpowiedział toothis kampanii. Określenie grupy docelowej odbiorców może bazować na powitania opinie o czy ta kampania została właśnie wypychana, odpowiedzi, akcje lub Zakończono.

### <a name="see-also"></a>Zobacz też
* [Nowe kryterium wypychania - Reach — dokumentacja interfejsu użytkownika][Link 28]

## <a name="content-of-polls"></a>Zawartość sond
![Reach Content2][31] 

Wypełnij hello tytuł, opis i przycisk teksty anonsu. Następnie należy dodać pytania i możliwości tooyour hello odpowiedzi na pytania.
Możesz zastosować odbiorców przyszłych kampanii na podstawie opinii reach hello o jak użytkownicy odpowiedział toothis kampanii. Określenie grupy docelowej odbiorców może bazować na czy ta kampania została właśnie wypychana, odpowiedzi, akcje lub Zakończono. Określenie grupy docelowej odbiorców mogą być również oparte na sondowania odpowiedzi opinii, gdy wybór pytanie i odpowiedź hello są używane jako kryteria.

### <a name="see-also"></a>Zobacz też
* [Nowe kryterium wypychania - Reach — dokumentacja interfejsu użytkownika][Link 28]

## <a name="content-of-data-pushes"></a>Zawartość wypychania danych
![Reach Content3][32] 

### <a name="choose-hello-type-of-your-data"></a>Wybierz typ hello danych:
* Tekst
* Dane binarne
* Dane w formacie Base64

### <a name="define-hello-content-of-your-data"></a>Zdefiniuj zawartość danych hello
* Jeśli wybrane dane tekstowe toopush, skopiuj i Wklej hello tekst w polu "zawartość" hello.
* W przypadku wybrania toopush danych binarnych lub base64, użyj tooupload przycisk "Przekaż plik" hello pliku.
* Możesz zastosować odbiorców przyszłych kampanii na podstawie opinii reach hello o jak użytkownicy odpowiedział toothis kampanii. Określenie grupy docelowej odbiorców może bazować na czy ta kampania została właśnie wypychana, odpowiedzi, akcje lub Zakończono.

### <a name="see-also"></a>Zobacz też
* [Nowe kryterium wypychania - Reach — dokumentacja interfejsu użytkownika][Link 28]

## <a name="content-of-tiles-windows-phone-only"></a>Zawartość Kafelki (tylko Windows Phone)
![Reach Content4][33]

### <a name="define-hello-content-of-your-tile"></a>Zdefiniuj zawartość kafelka hello
ładunek kafelka Hello jest hello toobe tekst wyświetlany w kafelku hello aplikacji na urządzeniach Windows Phone.
Wypychania kafelka jest wersja usługi powiadomień wypychanych firmy Microsoft (MPNS) hello natywnych powiadomień wypychanych dla Windows Phone. typu wypychania kafelka Hello jest hello tylko wypychania typ, który nie ma odpowiedzi i tak odbiorców hello przyszłych kampanii nie może być oparty na hello wyniki kampanii wypychania kafelka. 

### <a name="see-also"></a>Zobacz też
* [Natywnych powiadomień wypychanych - API Reach — dokumentacja interfejsu API][Link 4]

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

