---
title: aaaAzure AD w wersji 2 dla systemu Android wprowadzenie - Test | Dokumentacja firmy Microsoft
description: "Jak uzyskać token dostępu i wywołania interfejsu API programu Microsoft Graph lub interfejsów API, które wymagają tokenów dostępu z punktu końcowego w wersji 2 usługi Azure Active Directory aplikacji systemu Android"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testowanie kodu

1. Wdrażanie z kodu tooyour urządzeniu/emulatorze.
2. Gdy wszystko będzie gotowe tootest, za pomocą usługi Microsoft Azure Active Directory (konto organizacyjne) lub toosign konta Account Microsoft (live.com, outlook.com), w. 

![Zrzut ekranu przedstawiający przykładowy](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
<br/><br/>
![Logowanie](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)

### <a name="consent"></a>Zgody
Witaj po raz pierwszy użytkownik loguje się aplikacji tooyour one zostanie wyświetlone zgody ekran podobny toohello poniżej, gdzie muszą zaakceptować tooexplicitly: 

![Zgody](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a>Oczekiwanych rezultatów
Powinny pojawić się wyniki hello tooMicrosoft wywołania interfejsu API programu Graph 'me' punkt końcowy jest używany profil użytkownika hello tootooobtain — https://graph.microsoft.com/v1.0/me. Listę typowych Microsoft Graph punktów końcowych, zobacz to [artykułu](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Więcej informacji o zakresach i uprawnień delegowanych

Witaj interfejsu API programu Microsoft Graph wymaga hello `user.read` zakres tooread hello profilu użytkownika. Ten zakres jest automatycznie dodawany domyślnie w każdej aplikacji, jest zarejestrowany w portalu rejestracji. Niektóre inne interfejsy API dla programu Microsoft Graph, a także niestandardowych interfejsów API dla serwera wewnętrznej bazy danych może wymagać dodatkowych zakresów. Na przykład dla programu Microsoft Graph hello zakresu `Calendars.Read` jest kalendarzy wymagane toolist hello użytkownika. W kolejności tooaccess hello kalendarza użytkownika w kontekście aplikacji, należy tooadd hello `Calendars.Read` delegowane informacje rejestracyjne uprawnienia toohello aplikacji, a następnie dodaj hello `Calendars.Read` toohello zakres `acquireTokenSilentAsync` wywołania. Hello użytkownika może zostać wyświetlony monit dla dodatkowych zgody, jak zwiększyć liczbę hello zakresów.

<!--end-collapse-->
