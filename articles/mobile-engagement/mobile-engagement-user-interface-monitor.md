---
title: "aaaAzure Mobile Engagement interfejsu użytkownika — Monitor"
description: "Dowiedz się, jak toomonitor w czasie rzeczywistym danych aplikacji przy użyciu usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: b91ad89a-b89d-4377-abb0-cc2d16a2836d
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3a581e4166bc88e6ee7aa784d4047c94533685b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-real-time-data-about-your-application"></a>Jak toomonitor w czasie rzeczywistym danych aplikacji
W tym artykule opisano hello **MONITOR** kartę hello **Mobile Engagement** portalu. Użyj hello **Mobile Engagement** toomonitor portalu i zarządzania aplikacjami mobilnymi. Należy pamiętać, że toostart przy użyciu portalu hello, musisz najpierw toocreate **usługi Azure Mobile Engagement** konta. 

Hello Monitor części hello interfejsu użytkownika zawiera informacje analiz w czasie rzeczywistym oraz umożliwia tooset alerty po osiągnięciu progów ilości dla większości hello takie same informacje, które są dostępne w przeszłości w hello [ANALYTICS](mobile-engagement-user-interface-analytics.md) sekcji Witaj interfejsu użytkownika. Zobacz hello **słownik** części hello [pojęcia](http://go.microsoft.com/fwlink/?LinkId=525555) tematu definicje terminów i skrótów, analizy i monitorowanie (takie jak następujące hello: aktywnego użytkownika, nowy użytkownik zachowane użytkowników, sesji, Wykres ścieżki użytkownika, mapy użytkowników, adresy URL śledzenia, trendów, działania, zdarzenie, zadania, błąd, dodatkowe informacje, awarii i App-info).

> [!NOTE]
> Wiele sekcji hello **Mobile Engagement** interfejsu użytkownika portalu zawierają hello **Pokaż Pomoc** przycisku. Naciśnij ten przycisk tooget więcej informacje kontekstowe dotyczące sekcji.
> 
> 

## <a name="monitor---sessions-jobs-events-errors-and-crashes"></a>Monitor — sesji, zadania zdarzeń, błędów i awarii (Crash)
Widać, ilu użytkowników są obecnie w sesji i w określonym ekrany lub wykonanie określonych czynności. Można wyświetlić rozdzielonych sesji, zadania zdarzeń, błędów i awarii aktywności użytkownika. Możesz wyświetlić informacji o bieżącym hello i Pokaż hello informacje z hello ostatniej godziny, dnia lub tygodnia. Można wyświetlić wszystkie informacje hello w każdej kategorii, lub sortować hello określonej sesji, zadania zdarzeń, błędów i awarii.  Monitorowanie na żywo wynosi toouse przydatne podczas zdarzenia, takie jak toosee kampanii wypychania uptick w akcji prawo po wysłaniu powiadomienia wypychane.

![Monitor1][14]  

## <a name="troubleshooting-with-monitor---events---details"></a>Rozwiązywanie problemów z monitora - zdarzenia — szczegóły
Generowanie zdarzeń w aplikacji z urządzenia testu i znalezieniem w szczegółach monitora - zdarzenia - jest jednym z hello najprostszym toofind sposoby urządzenia IDENTYFIKATORA urządzenie testowe i tooconfirm tej integracji usługi Azure Mobile Engagement analizy, monitorowanie, i Segmenty współpracuje z aplikacji. Po utworzeniu hello identyfikator urządzenia urządzenia testu, można dodać tooyour urządzeń testowych w "Moje urządzenia — konto". Jeśli nie można wygenerować zdarzenie, upewnij się, że usługi Azure Mobile Engagement jest poprawnie zintegrowane z aplikacji systemu Android/iOS/Web/Windows/Windows Phone za pomocą hello zestawu SDK.

Aby uzyskać więcej informacji, zobacz: [dokumentacji zestawu SDK][Link 5]

![Monitor 2][15]  

## <a name="troubleshooting-with-monitor---crashes---details"></a>Rozwiązywanie problemów z monitorem - awarii — szczegóły
Możesz przejrzeć informacje o awariach aplikacji z monitora - awarii — szczegóły toohelp ustalić przyczyny awarii aplikacji. Należy również wyszukać znane problemy z poszczególnymi wersjami hello zestawu SDK w wersji powitania dla każdej wersji hello zestawu SDK dla systemu Android/iOS/Web/Windows/Windows Phone.

Aby uzyskać więcej informacji, zobacz: [dokumentacji zestawu SDK — informacje o wersji][Link 5]

![Monitor3][16]

## <a name="monitor---alerts"></a>Monitor — alerty
Można również określić warunków alertów, które będą automatycznie wysyłane tooyou za pośrednictwem poczty e-mail lub wiadomości błyskawicznych. (Wszystkie usługi zgodne z protokołem XMPP, takich jak GTalk firmy Google lub iChat firmy Apple są obsługiwane). Alerty są oparte na wykrywanie wstępnie zdefiniowane wartości progowej większości (>) i mniejszości (<) określoną liczbę sesji, zadania, zdarzeń, błędów lub awarii (Crash) na sekundę, minuty lub godzinę. Alerty można monitorować wszystkie działania danego typu lub po prostu monitorowanie określonego działania zadania, zdarzenia lub błąd. 

Można również określić minimalna częstotliwość wykrywania, czyli hello minimalna ilość musi upłynąć między dwoma powiadomieniami w ramach hello sam alert toomake się upewnić, że po wyzwoleniu alertu nigdy nie otrzymasz więcej niż 1 powiadomień na interwał określony w minutach.

![Monitor4][17]

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
