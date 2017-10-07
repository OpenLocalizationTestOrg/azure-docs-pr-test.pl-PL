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
ms.openlocfilehash: eaa41805c92212154ee8d51d3eb3aee1202eef1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Dodawanie aplikacji hello rejestracji informacji tooyour aplikacji

W tym kroku należy tooadd hello identyfikator klienta tooyour projektu.

1.  Otwórz `MainActivity` (w obszarze `app`  >  `java`  >   *`{host}.{namespace}`* )
2.  Zastąp hello wiersz rozpoczynający się `final static String CLIENT_ID` z:
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. Otwórz:`app` > `manifests` > `AndroidManifest.xml`
4. Dodaj hello następujące działania zbyt`manifest\application` węzła. Rejestr `BrowserTabActivity` tooallow hello OS tooresume aplikacji po zakończeniu uwierzytelniania hello:

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

### <a name="what-is-next"></a>Co to jest dalej

[Testowanie i weryfikowanie](active-directory-mobileanddesktopapp-android-test.md)
