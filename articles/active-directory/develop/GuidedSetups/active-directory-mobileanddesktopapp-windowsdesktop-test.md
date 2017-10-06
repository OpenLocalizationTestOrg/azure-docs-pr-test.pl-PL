---
title: aaaAzure AD v2 Windows Desktop wprowadzenie - Test | Dokumentacja firmy Microsoft
description: "Jak aplikacje .NET pulpitu systemu Windows (XAML) można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testowanie kodu

W celu tootest aplikacji, naciśnij klawisz `F5` toorun projektu w programie Visual Studio. Powinna zostać wyświetlona okno główne:

![Zrzut ekranu przedstawiający przykładowy](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

Jeśli wszystko jest gotowe tootest, kliknij przycisk *wywołać Microsoft interfejsu API programu Graph* i za pomocą usługi Microsoft Azure Active Directory (konto organizacyjne) lub toosign konta Account Microsoft (live.com, outlook.com), w. Go powitania po raz pierwszy, zostanie wyświetlone okno z zapytaniem toosign użytkownika w:

![Logowanie](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a>Zgody
Hello po raz pierwszy zalogować stosując tooyour, zostaną wyświetlone z ekranu zgody o poniżej podobne toohello, gdzie należy zaakceptować tooexplicitly:

![Zgoda ekranu](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a>Oczekiwanych rezultatów
Informacje o profilu użytkownika zwrócony przez wywołanie interfejsu API Graph usługi Microsoft hello na ekranie wyniki wywołania interfejsu API hello powinna zostać wyświetlona.

Podstawowe informacje o nabyte za pośrednictwem tokenu hello powinno również zostać wyświetlone `AcquireTokenAsync` lub `AcquireTokenSilentAsync` w polu informacji o tokenie hello:

|Właściwość  |Format  |Opis |
|---------|---------|---------|
|Nazwa | {Pełna nazwa użytkownika} |Użytkownik Hello na imię i nazwisko|
|Nazwa użytkownika |<span>user@domain.com</span> |używana nazwa Hello tooidentify hello użytkownika|
|Wygaśnięcia tokenu |{DateTime}         |czas Hello, na które hello wygaśnięcia tokenu. MSAL rozszerzy Data wygaśnięcia hello za odnowienie hello token, gdy jest to konieczne|
|Token dostępu |{Ciąg}         |ciąg tokenu Hello wysłane który będą wysyłane żądania tooHTTP, które wymagają nagłówek autoryzacji|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Więcej informacji o zakresach i uprawnień delegowanych
Interfejs API Graph wymaga hello `user.read` zakres tooread profilu użytkownika. Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, jest zarejestrowany w portalu rejestracji. Niektóre inne interfejsy API Graph, a także niestandardowych interfejsów API dla serwera wewnętrznej bazy danych wymaga dodatkowych zakresów. Na przykład do wykresu `Calendars.Read` jest wymagane toolist kalendarzach. W kolejności tooaccess hello kalendarza użytkownika w kontekście aplikacji, należy tooadd `Calendars.Read` delegowane informacji o rejestracji aplikacji, a następnie dodaj `Calendars.Read` toohello `AcquireTokenAsync` wywołania. Użytkownik może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę hello zakresów.

<!--end-collapse-->



