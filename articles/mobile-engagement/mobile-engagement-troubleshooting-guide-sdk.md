---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
description: "Rozwiązywanie problemów integracji zestawu SDK usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a>Przewodnik rozwiązywania problemów integracji zestawu SDK
Witaj poniżej przedstawiono możliwe problemy, które mogą się pojawić w sposób integruje aplikacji usługi Azure Mobile Engagement.

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a>Problemy z zestawu SDK odnalezione awaria w innym miejscu aplikacji
### <a name="issue"></a>Problem
* Błąd zbierania danych interfejsu użytkownika (w analizy, monitorowanie, segmentacji lub pulpity).
* Wypychanie błędów (Wypchnięć nie działają w aplikacji poza aplikacji lub obie).
* Zaawansowane błędy funkcji (śledzenia, używanie funkcji Geolokalizacji lub platformy, którą określonych Wypchnięć nie działają).
* Błędy interfejsu API (interfejsy API niepowodzenie często trybie cichym bez komunikaty o błędach).
* Awarie usługi (Brak usługi Azure Mobile Engagement działa w przypadku aplikacji).

### <a name="causes"></a>Powoduje, że
* Błąd w aplikacji (na przykład błąd zbierania danych interfejsu użytkownika, Niepowodzenie wypychania, Niepowodzenie zaawansowanych funkcji, błąd interfejsu API, awarii aplikacji lub usługi jawnego spowoduje odnalezienie większości problemów, które trzeba toobe został rozwiązany za pomocą hello zestaw SDK usługi Azure Mobile Engagement awarii).  
* Jeśli w aplikacji przed nigdy nie działał poszczególnych funkcji usługi Azure Mobile Engagement, należy toocomplete hello integracji. 
* Jeśli poszczególnych funkcji usługi Azure Mobile Engagement pracy i zatrzymanie, może być konieczne tooupgrade toohello ostatniej wersji z hello zestaw SDK usługi Azure Mobile Engagement. Należy pamiętać, że jest inna wersja hello Azure Mobile Engagement SDK dla każdej platformy obsługiwane przez usługi Azure Mobile Engagement (Android, iOS, Windows i Windows Phone).

#### <a name="sdk-integration"></a>Integracja z zestawem SDK
* Usługa Azure Mobile Engagement prawidłowo zintegrowane w zestawie SDK (Analytics).
* Łączność prawidłowo zintegrowany zestaw SDK (w aplikacji i poza wypchnięcia aplikacji).
* Certyfikat wygasły lub niepoprawne vs produkcyjną. Deweloperów (tylko iOS).
* GCM lub ADM prawidłowo zintegrowany zestaw SDK (Android tylko — usługa określonych wypchnięcia).
* Śledzenie prawidłowo zintegrowane w zestawie SDK (magazyn instalacji śledzenia).
* Opóźnieniem lokalizacji lub lokalizacji GPS prawidłowo zintegrowane w zestawie SDK (docelowych według lokalizacji geograficznej).

**Zobacz też:**

* [Dokumentacja zestawu SDK — przewodniki integracji][Link 5] 
* [Przewodnik rozwiązywania problemów - wypychania][Link 23]

#### <a name="sdk-upgrade"></a>Uaktualnianie zestawu SDK
* Należy tooupgrade SDK tooresolve problemy ze starszymi wersjami hello SDK (często powiązane toonewer wersje systemu operacyjnego urządzenia hello).
* Odinstaluj wszystkie wcześniejsze wersje aplikacji z urządzenia i zainstaluj ponownie najnowszą wersję aplikacji hello, hello ponownie zarejestrować identyfikator urządzenia z hello Azure Mobile Engagement UI tooconfirm urządzenie używa hello najnowszej wersji aplikacji.

**Zobacz też:**

* [Dokumentacja zestawu SDK — informacje o wersji](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [Dokumentacja zestawu SDK — przewodniki uaktualnienia](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a>Zestaw SDK innych
* Błędy w manifeście aplikacji "AndroidManifest.xml" może spowodować usługi Azure Mobile Engagement toowork (tylko Android).
* Typowym problemem z integracji zestawu SDK i użycia interfejsu API jest tooconfuse hello klucza zestawu SDK i hello klucz interfejsu API.

**Zobacz też:**

* [Pojęcia — słownik][Link 6]

## <a name="advanced-coding-issues"></a>Zaawansowane kodowania problemów
### <a name="issue"></a>Problem
* Kod platformy nie bezpośrednio powiązane tooAzure Mobile Engagement może spowodować problemy w systemie iOS, Android i Windows Phone.

### <a name="causes"></a>Powoduje, że
* Wiele zaawansowanych kodowania problemy z usługi Azure Mobile Engagement są spowodowane przez niepoprawnie napisane platformy określony kod nie są bezpośrednio związane z tooAzure Mobile Engagement. Konieczne będzie tooconsult dokumentacji toohello określonych platform opracowywanej dla dodatkowo dokumentacji usługi Mobile Engagement tooAzure (Android, iOS, sieci Web, Windows i Windows Phone).
* Konfigurowanie prawidłowo "kategorie", uniemożliwia łączenie z lokalizacji tooanother powiadomień wewnątrz lub na zewnątrz aplikacji hello (tylko Android). 
* To ustawienie nie zostanie "UIKit.framework" za "opcjonalne" w kodzie systemu iOS pokazuje "Błąd: nie odnaleziono symbolu" i/lub ulega awarii na starszych urządzeń z systemem iOS (tylko iOS).
* Wygasłe certyfikaty lub prawidłowo przy użyciu hello deweloperów lub wersję produkcyjną hello certyfikatu, wypychania przyczyny problemów (tylko iOS).
* Brak niektórych platforma związanego z używaniem tooa ograniczenia usługi Azure Mobile Engagement nie może kontrolować (tak jak wypycha działania hello system center dla aplikacji w systemach Android i iOS).
* Usługa Azure Mobile Engagement publikuje pełną listę hello pakietów wewnętrzny używany przez usługi Azure Mobile Engagement dla systemów iOS i Android odwołania. Należy pamiętać, że niektóre funkcje usługi Azure Mobile Engagement są toohello określonych platform (Android, iOS, sieci Web, Windows i Windows Phone).

### <a name="see-also"></a>Zobacz też
* [Przewodnik rozwiązywania problemów - wypychania][Link 23] 
* [Dokumentacja zestawu SDK — informacje o wersji][Link 5]
* [Dokumentacja zestawu SDK — przewodniki uaktualnienia][Link 5]

## <a name="application-crashes"></a>Awarii aplikacji
### <a name="issue"></a>Problem
* Na urządzeniach użytkowników końcowych hello ulega awarii aplikacji.

### <a name="causes"></a>Powoduje, że
* Informacje o awarii można wyświetlić w hello *interfejsu użytkownika analizy* lub hello *analizy interfejsu API*
* Witaj identyfikator urządzenia urządzenia testu i podjąć hello można znaleźć tę samą akcję, która spowodowała toocrash Twojej aplikacji dla użytkownika końcowego toohelp zidentyfikować hello przyczynę awarii sieci.
* Znane problemy z hello Azure Mobile Engagement SDK, które powodują toocrash aplikacji są czasami rozwiązać przez uaktualnienie toohello najnowszą wersję hello zestawu SDK. Podczas badania awarii (Crash), upewnij się, że toocheck hello informacje o wersji dotyczące platformy.

### <a name="see-also"></a>Zobacz też
* [Dokumentacja zestawu SDK — informacje o wersji][Link 5]
* [Dokumentacja zestawu SDK — przewodniki uaktualnienia][Link 5]

## <a name="app-store-upload-failures"></a>Aplikacji sklepu przekazywania błędów
### <a name="issue"></a>Problem
* Błędy związane z toouploading hello najnowszą wersję aplikacji tooApple, Google lub sklepu z aplikacjami systemu Windows hello.

### <a name="causes"></a>Powoduje, że
* Aplikacja przechowuje czasami blok aplikacje z niektórych z włączonymi funkcjami (np. hello sklepu Apple uniemożliwia użycie hello IDFV w aplikacjach w sklepie hello i uniemożliwia magazynu GooglePlay hello hello udostępnianie informacji o aplikacji między aplikacjami). 
* Upewnij się, sprawdź hello informacje o wersji dotyczące platformy i bieżącej wersji zestawu SDK hello, jeśli masz trudności przekazywania toohello sklepu z aplikacjami.

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
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

