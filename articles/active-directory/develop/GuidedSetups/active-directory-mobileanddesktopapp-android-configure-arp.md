---
title: "Usługi Azure AD w wersji 2 dla systemu Android pobieranie rozpoczęte — Konfigurowanie | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c09937582118ebcc5b8cbc1f43a0a2019f2f7a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="dd598-103">Dodawanie informacji o rejestracji aplikacji do aplikacji</span><span class="sxs-lookup"><span data-stu-id="dd598-103">Add the application’s registration information to your app</span></span>

<span data-ttu-id="dd598-104">W tym kroku musisz dodać identyfikator klienta do projektu.</span><span class="sxs-lookup"><span data-stu-id="dd598-104">In this step, you need to add the Client ID to your project.</span></span>

1.  <span data-ttu-id="dd598-105">Otwórz `MainActivity` (w obszarze `app`  >  `java`  >   *`{host}.{namespace}`* )</span><span class="sxs-lookup"><span data-stu-id="dd598-105">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
2.  <span data-ttu-id="dd598-106">Zastąp wiersz rozpoczynający się `final static String CLIENT_ID` z:</span><span class="sxs-lookup"><span data-stu-id="dd598-106">Replace the line starting with `final static String CLIENT_ID` with:</span></span>
```java
final static String CLIENT_ID = "[Enter the application Id here]";
```
3. <span data-ttu-id="dd598-107">Otwórz:`app` > `manifests` > `AndroidManifest.xml`</span><span class="sxs-lookup"><span data-stu-id="dd598-107">Open: `app` > `manifests` > `AndroidManifest.xml`</span></span>
4. <span data-ttu-id="dd598-108">Dodaj na wykonywanie następujących czynności `manifest\application` węzła.</span><span class="sxs-lookup"><span data-stu-id="dd598-108">Add the following activity to `manifest\application` node.</span></span> <span data-ttu-id="dd598-109">Rejestr `BrowserTabActivity` umożliwia systemu operacyjnego można wznowić aplikacji po zakończeniu uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="dd598-109">This register a `BrowserTabActivity` to allow the OS to resume your application after completing the authentication:</span></span>

```xml
<!--Intent filter to capture System Browser calling back to our app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />

        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, the scheme should be similar to 'msal[appId]' -->
        <data android:scheme="msal[Enter the application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```

### <a name="what-is-next"></a><span data-ttu-id="dd598-110">Co to jest dalej</span><span class="sxs-lookup"><span data-stu-id="dd598-110">What is Next</span></span>

[<span data-ttu-id="dd598-111">Testowanie i weryfikowanie</span><span class="sxs-lookup"><span data-stu-id="dd598-111">Test and Validate</span></span>](active-directory-mobileanddesktopapp-android-test.md)
