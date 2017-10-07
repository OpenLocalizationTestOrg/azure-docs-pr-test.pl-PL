---
title: iOS v2 aaaAzure AD Getting Started - Test | Dokumentacja firmy Microsoft
description: "Jak aplikacje systemu iOS (Swift) można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a>Test zapytań hello Microsoft Graph API z poziomu aplikacji systemu iOS

Naciśnij klawisz `Command`  +  `R` toorun hello kodu w symulatorze hello.

![Zrzut ekranu przedstawiający przykładowy](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

Jeśli wszystko jest gotowe tootest, naciśnij przycisk *"Wywołaj Microsoft interfejsu API programu Graph"* i będzie tootype zostanie wyświetlony monit o nazwę użytkownika i hasło.

### <a name="consent"></a>Zgody
Hello po raz pierwszy zalogować stosując tooyour, zostaną wyświetlone z ekranu zgody o poniżej podobne toohello, gdzie należy zaakceptować tooexplicitly:

![Zgoda ekranu](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a>Oczekiwanych rezultatów
Powinny być widoczne informacje o profilu użytkownika zwrócony przez wywołanie interfejsu API Graph usługi Microsoft hello w hello *rejestrowanie* sekcji.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Więcej informacji o zakresach i uprawnień delegowanych

Witaj interfejsu API programu Microsoft Graph wymaga hello `user.read` zakres tooread hello profilu użytkownika. Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, jest zarejestrowany w portalu rejestracji. Niektóre inne interfejsy API dla programu Microsoft Graph, a także niestandardowych interfejsów API dla serwera wewnętrznej bazy danych może wymagać dodatkowych zakresów. Na przykład dla programu Microsoft Graph hello zakresu `Calendars.Read` jest kalendarzy wymagane toolist hello użytkownika. W kolejności tooaccess hello kalendarza użytkownika w kontekście aplikacji, należy tooadd hello `Calendars.Read` delegowane informacje rejestracyjne uprawnienia toohello aplikacji, a następnie dodaj hello `Calendars.Read` toohello zakres `acquireTokenSilent` wywołania. Hello użytkownika może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę hello zakresów.

<!--end-collapse-->



