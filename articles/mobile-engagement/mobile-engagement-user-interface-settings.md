---
title: "aaaAzure Mobile Engagement interfejsu użytkownika — ustawienia"
description: "Dowiedz się, jak toomanage hello globalne ustawienia aplikacji przy użyciu usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 858f4cb4-14de-4bb5-826f-28cadbfc928b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02d4a36c591fc5e097410b7e931d1c9ce81d68d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-global-settings-of-your-application"></a>Jak toomanage hello globalne ustawienia aplikacji
Witaj **ustawienia** menu opcji dostępnych dla aplikacji mogą być różne, w zależności od platformy hello aplikacji hello i uprawnień hello przyznano Ci dla aplikacji hello. Ustawienia obejmują następujące hello: szczegóły, projektów natywnych powiadomień wypychanych, szybkość wypychania, Tag (app-info) i nacisku komercyjnego. Witaj Tag (app-info) menu opcji hello w sekcji Ustawienia można zarządzać przez aplikację (przy użyciu hello zestawu SDK) lub serwera (przy użyciu hello interfejsu API urządzenia). 

> [!NOTE]
> Wiele sekcji hello **Mobile Engagement** interfejsu użytkownika portalu zawierają hello **Pokaż Pomoc** przycisku. Naciśnij ten przycisk tooget więcej informacje kontekstowe dotyczące sekcji.
> 
> 

## <a name="details"></a>Szczegóły
Umożliwia toochange hello nazwę i opis Twojej aplikacji, właściciela hello widoku aplikacji i uprawnień roli. 

Konfiguracja Analytics umożliwia tooview lub zmień dzień hello tygodni uruchomić na komputerze i hello czas przechowywania w dni.

  ![settings1][46]

## <a name="projects"></a>Projekty
Pozwala tooselect wszystkie projekty mają tooappear Twojej aplikacji. 

Możesz również wyszukać projektu i widoku hello nazwę, opis, właściciela i uprawnień roli projektu aplikacji jest częścią.

Aby uzyskać więcej informacji, zobacz: [dokumentacji interfejsu użytkownika — strona główna][Link 13]

  ![settings3][48]

## <a name="native-push"></a>Natywnych powiadomień wypychanych
Umożliwia tooregister nowego certyfikatu lub Usuń, a istniejący certyfikat na potrzeby korzystać z natywnych powiadomień wypychanych. Natywnych powiadomień wypychanych umożliwia aplikacji tooyour toopush usługi Azure Mobile Engagement w dowolnym momencie, nawet jeśli nie jest uruchomiona. 

Po podaniu poświadczeń lub certyfikaty dla co najmniej jedną usługę natywnych powiadomień wypychanych, możesz wybrać "W dowolnym momencie" podczas tworzenia osiągnąć kampanii i użyj parametru "zgłaszający" hello w hello PUSH interfejsu API.

### <a name="apple-push-notification-service-apns"></a>Apple Push Notification Service (APNS)
tooenable wypychanie natywne przy użyciu hello Apple Push Notification Service należy tooregister certyfikatu. Konieczne będzie toospecify hello typu certyfikatu jako Programowanie (deweloperów) lub produkcyjnym (produkcyjną). Następnie możesz należy przekazać certyfikat i hello hasła.

Aby uzyskać więcej informacji, zobacz: [dokumentacji zestawu SDK — dla systemu iOS — jak tooPrepare aplikacji dla powiadomień wypychanych firmy Apple][Link 5]

![settings4][49]

### <a name="windows-push-notification-service-wpns"></a>Usługa powiadomień wypychanych systemu Windows (WPNS)
tooenable wypychanie natywne przy użyciu usługi powiadomień systemu Windows, musisz podać poświadczenia aplikacji. Konieczne będzie identyfikator zabezpieczeń (SID) pakietu i klucz tajny.

![settings5][50]

### <a name="google-cloud-messaging-for-android-gcm"></a>Usługa Google Cloud Messaging dla systemu Android (GCM)
tooenable natywnych powiadomień wypychanych przy użyciu usługi GCM, należy toofollow hello instrukcje od firmy Google. Następnie musisz wkleić prosty klucz interfejsu API serwera, skonfigurowany bez ograniczeń adresu IP. Wymaga integracji z hello zestawu SDK dla systemu Android v1.12.0 +.

Aby uzyskać więcej informacji, zobacz: 

* [Zestaw SDK dokumentacji Android jak GCM tooIntegrate][Link 5]
* [Przewodnik dewelopera Google GCM po](http://developer.android.com/guide/google/gcm/gs.html)

### <a name="amazon-device-messaging-for-android-adm"></a>Urządzenie Amazon Messaging dla systemu Android (ADM)
tooenable Native Push przy użyciu usługi ADM, musisz podać Amazon <OAuth credentials> składające się z Identyfikatorem klienta i klucz tajny klienta (wymaga integracji z zestawem SDK dla systemu Android v2.1.0 +).

Aby uzyskać więcej informacji, zobacz: 

* [Zestaw SDK dokumentacji Android jak tooIntegrate ADM][Link 5]
* [Dokumentacja usługi ADM dla deweloperów firmy Amazon](https://developer.amazon.com/sdk/adm/credentials.html#Getting)

![settings6][51]

## <a name="push-speed"></a>Szybkość wypychania
Pokazuje hello bieżąca szybkość wypychania dla aplikacji i pozwala szybkość wypychania hello toodefine aplikacji.

  ![settings7][52]

## <a name="tag-app-info"></a>Tag (app-info):
![settings11][56]

## <a name="commercial-pressure"></a>Nacisku komercyjnego
![settings12][57]

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

