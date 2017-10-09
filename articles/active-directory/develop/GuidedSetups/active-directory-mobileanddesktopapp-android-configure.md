---
title: "v2 aaaAzure AD Android wprowadzenie — Konfigurowanie | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Tworzenie aplikacji (Express)
Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:
1. Zarejestrować aplikację za pośrednictwem hello [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)
2.  Wprowadź nazwę aplikacji i poczty e-mail
3.  Upewnij się, że jest zaznaczona opcja hello z przewodnikiem instalacji
4.  Wykonaj identyfikator aplikacji hello hello instrukcje tooobtain i wklej go w kodzie

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Dodawanie rozwiązania tooyour informacji o rejestracji aplikacji (zaawansowane)
Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:
1. Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister aplikacji
2. Wprowadź nazwę aplikacji i poczty e-mail 
3. Upewnij się, że jest zaznaczona opcja hello instrukcje konfiguracji
4. Kliknij przycisk `Add Platform`, a następnie wybierz pozycję `Native Application` i kliknij przycisk Zapisz
5.  Otwórz `MainActivity` (w obszarze `app`  >  `java`  >   *`{host}.{namespace}`* )
6.  Zastąp hello *[hello aplikacji o identyfikatorze tutaj wprowadź]* w hello wiersz rozpoczynający się `final static String CLIENT_ID` został zarejestrowany identyfikator aplikacji hello:

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Otwórz `AndroidManifest.xml` (w obszarze `app`  >  `manifests`) hello Dodaj następujące działania zbyt`manifest\application` węzła. Rejestruje to `BrowserTabActivity` tooallow hello OS tooresume aplikacji po zakończeniu uwierzytelniania hello:
</li>
</ol>

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        
        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
W hello `BrowserTabActivity`, Zastąp `[Enter hello application Id here]` z identyfikatorem aplikacji hello.
</li>
</ol>
