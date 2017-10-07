---
title: aaaAzure Mobile Engagement interfejs - Reach
description: "Dowiedz się, jak tooreach toohello użytkowników aplikacji za pomocą powiadomień wypychanych przy użyciu usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a>Jak tooreach toohello użytkowników aplikacji za pomocą powiadomień wypychanych
W tym artykule opisano hello **OSIĄGNĄĆ** kartę hello **Mobile Engagement** portalu. Użyj hello **Mobile Engagement** toomonitor portalu i zarządzania aplikacjami mobilnymi. Należy pamiętać, że toostart przy użyciu portalu hello, musisz najpierw toocreate **usługi Azure Mobile Engagement** konta. Aby uzyskać więcej informacji, zobacz [utworzyć konto usługi Azure Mobile Engagement](mobile-engagement-create.md).

Hello osiągnąć sekcji powitalne interfejsu użytkownika jest hello wypychania kampanii narzędzie do zarządzania można utworzyć/edytowanie/aktywować/Zakończ/monitor i uzyskać statystyki kampanii obejmujących wysyłanie powiadomień wypychanych i funkcji, które są dostępne za pośrednictwem interfejsu API Reach hello (i niektóre elementy hello niski poziom Push interfejsu API). Należy pamiętać, że zarówno w przypadku korzystania z interfejsów API hello lub hello interfejsu użytkownika należy toointegrate zarówno usługi Azure Mobile Engagement i Reach do aplikacji dla poszczególnych platform z hello SDK przed użyciem osiągnąć kampanii.

> [!NOTE]
> Wiele sekcji hello **Mobile Engagement** interfejsu użytkownika portalu zawierają hello **Pokaż Pomoc** przycisku. Naciśnij ten przycisk tooget więcej informacje kontekstowe dotyczące sekcji.
> 
> 

## <a name="four-types-of-push-notifications"></a>Cztery typy powiadomień wypychanych
1. Anonse — Zezwalaj toosend toousers wiadomości reklamy, który przekierowanie tooanother położenie wewnątrz aplikację lub toosend ich tooa strony sieci Web ani do przechowywania poza aplikacji. 
2. Ankiety — Zezwalaj toogather informacji od użytkowników końcowych za pośrednictwem pytań.
3. Wypychania danych - pozwalają toosend pliku danych binarnych lub base64. Witaj informacje zawarte w wypychanych danych są wysyłane toomodify aplikacji tooyour bieżącego środowiska użytkowników w aplikacji. Aplikacja wymaga toobe tooprocess stanie hello danych w wypychanych danych.

## <a name="campaign-details"></a>Szczegóły kampanii
Można edytować, klonowanie, usunąć lub aktywowania kampanii, które nie zostały jeszcze aktywowane, ustawiając kursor nad ich nazwy lub kliknięciu tooopen je. Można sklonować kampanii, które zostały już aktywowana, ustawiając kursor nad ich nazwy lub kliknięciu tooopen je. Jednak nie można zmienić kampanii, gdy został już aktywowany.

![Reach1][18]

## <a name="reach-feedback"></a>Osiągnąć opinii
Polecenie **statystyki** toosee hello szczegóły kampanii Reach. Witaj **proste** widok zawiera wizualną reprezentację w postaci hello wykres słupkowy kolumny o co się stało po kampanii został aktywowany. Witaj **zaawansowane** widoku szczegółowe bardziej szczegółowe informacje na temat hello wypychania kampanii. Te informacje nie będą dostępne w przypadku wysyłania kampanii testowej np. urządzenie testowe wysłane tooa wypychania. Oto, jak należy interpretować te szczegóły:

1. **Wypychana** — określa hello liczba komunikatów wypchniętych toohello urządzeń. Ta liczba będzie zależeć od hello docelowych odbiorców określone podczas tworzenia hello wypychania kampanii. Jeśli nie określono żadnych docelowych odbiorców, to wypychane będą wysyłane w tooall hello zarejestrowanych urządzeń. Podobnie jak inne usługi wypychania, firma Microsoft nie hello powiadomienia wypychane bezpośrednio toohello urządzenia, ale zamiast tego wypychanie ich odpowiednich platform toohello określonych usług powiadomień wypychanych (PNS - WNS-APNS/GCM) tak, aby ich dostarczenia powiadomienia hello toohello urządzeń. 
2. **Dostarczone** — określa hello liczbę wiadomości, które są pomyślnie dostarczone przez urządzenie toohello systemu powiadomień platformy hello i potwierdzone jako odebrane przez zestaw SDK usługi Mobile Engagement. 
   
   *Przyczyny dostarczone liczba była mniejsza niż liczba wciśnięcia:*
   
   1. Jeśli użytkownik hello odinstalował aplikacji hello z urządzenia hello, ale hello systemu powiadomień platformy nie wiesz w czasie hello wyślemy hello wypychania toohello systemu powiadomień platformy wiadomość hello zostaną usunięte.
   2. Jeśli urządzenie hello jest aplikacja hello, ale samymi urządzeniami hello były w trybie offline przez dłuższy czas, następnie hello systemu powiadomień platformy zakończy się niepowodzeniem urządzenia toohello wiadomość hello toodeliver. 
   3. Jeśli wiadomość hello dostarczenie toohello urządzenia, ale hello zestaw Mobile Engagement SDK w aplikacji hello nie rozpoznaje zawartości hello wiadomość hello, jego porzuca tej wiadomości. Może to się zdarzyć, jeśli dostosowania hello hello powiadomienia w aplikacji hello generuje wyjątek, który mamy catch w wiadomość hello zestawu SDK i upuszczanie powitania. Może to także wystąpić, jeśli aplikacja hello na urządzeniu hello jest przy użyciu wersji hello zestaw Mobile Engagement SDK, który nie jest możliwe toounderstand hello nowszej wersji wiadomości wypychanych hello wysyłane z platformy hello, ale jest to tylko wtedy, gdy aplikacja hello został uaktualniony po powiadomieniu hello została wysłana z hello usługi platformy. Witaj **zaawansowane** kartę informuje, ile komunikatów zostały usunięte. 
   4. Na urządzeniach z systemem iOS wiadomości czasami nie dostarczenie albo urządzenia hello znajduje się na niskim poziomie naładowania baterii lub aplikacji hello zajmuje dużo mocy podczas przetwarzania zdalnego powiadomienia. Jest to ograniczenie hello urządzeń z systemem iOS.   
3. **Wyświetlane** — określa hello liczbę wiadomości, które pomyślnie toohello aplikacji użytkownika na urządzeniu hello w postaci hello systemu powiadomienie wypychane/out z — aplikacji w Centrum powiadomień hello lub powiadomienie w aplikacji w ramach hello przenośnych aplikacja.  Witaj **zaawansowane** kartę informuje o ile zostały powiadomień systemowych i ile były powiadomienia w aplikacji. 
   
   *Liczba powody mogą być wyświetlane jest mniejsza niż liczba dostarczone (wyświetlane toobe oczekiwania)*
   
   1. Jeśli kampanię z użyciem powiadomień hello ma datę końcową w nim, a następnie jest możliwe, że hello powiadomienie zostało dostarczone, ale jeśli czas hello pochodzi tooopen i wyświetl ją toohello aplikacji użytkownika, już została usunięta, nigdy nie została wyświetlona.   
   2. Jeśli powiadomienia hello jest powiadomienie w aplikacji hello powiadomień zostanie wyświetlony tylko po otwarciu użytkownika aplikacji hello aplikacji hello. W przypadkach, gdy użytkownik aplikacji hello nie otworzyła aplikacji hello hello SDK będzie zgłaszać czy hello powiadomienie zostało dostarczone, ale nie została jeszcze wyświetlany, dopóki aplikacja hello jest otwarty. 
   3. Jeśli powiadomienie hello jest powiadomienie w aplikacji i skonfigurować toobe wyświetlany na określone działanie/ekran również hello powiadomień zostanie zgłoszone jako wydana, ale nie zostały jeszcze dostarczone do hello otwarciu aplikacji hello na ekranie określonego. 
4. **Interakcje użytkownika** — określa hello liczba wiadomości, który użytkownik aplikacji hello treść instrukcji i będzie zawierać wiadomości powitania, które są akcje lub Zakończono. 
   
   * *użytkownik aplikacji Hello może wykonać akcję powiadomień w jednej z hello następujące sposoby:*
     
     1. Jeśli hello powiadomień jest powiadomienie systemu/out elementu aplikacji lub wysyłane powiadomienie w aplikacji jako tylko do powiadomienia, hello aplikacji użytkownik kliknie powiadomienie hello.
     2. Jeśli powiadomienia hello jest powiadomienie w aplikacji z tekstem lub widok sieci web lub sond następnie hello użytkownika aplikacji kliknie hello przycisku akcji hello powiadomienia.
     3. Jeśli powiadomienie o hello powiadomienie w aplikacji z widoku sieci web następnie hello kliknięć użytkowników aplikacji przy użyciu adresu URL hello sieci web tylko w widoku [Android]
   * *użytkownik aplikacji Hello może wyjść powiadomień w jednej z hello następujące sposoby:*
     
     1. Kliknięcie przycisku Zamknij hello na powitania powiadomienia bezpośrednio. 
     2. Szybko przesuwając optymalizacji lub usunięcie hello powiadomienia. 
     3. Powiadomienia w aplikacji z zawartością tekstu/sieci web i sond są zwykle wyświetlane toohello aplikacji użytkownika w dwóch etapach. Najpierw widzą powiadomienie, a po kliknięciu na nim, zobacz temat hello kolejnych zawartości tekstu/sieci web/sondowania. użytkownik aplikacji Hello może wyjść powiadomień w jednej z następujących czynności i hello szczegółów w widoku Zaawansowane hello przechwytuje to. 
5. **Których wykonano akcje** — określa hello liczba wiadomości, które zostały jawnie których wykonano akcje przez użytkownika aplikacji hello. Jest to numer najbardziej interesujące hello informuje ilu użytkowników aplikacji zostały zainteresowanych przez wiadomość hello wypchnięty hello powiadomienia. 

> [!NOTE]
> Dla systemu iOS & platformy systemu Windows, jeśli użytkownik hello ma aplikacji hello otwarte i kampanii hello został kampanii "W każdej chwili", możliwe, zarówno z aplikacji i w aplikacji Powiadomienia są wyświetlane pod kątem hello jest tym samym czasie. Może to spowodować liczbą wyświetlane wyższe niż hello dostarczone. Jeśli użytkownik hello wchodzi w interakcję lub akcje hello powiadomień, następnie nawet hello Liczba interakcji użytkownika/Actioned może być większa niż dostarczone. 
> 
> 

![Reach2][19]

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

