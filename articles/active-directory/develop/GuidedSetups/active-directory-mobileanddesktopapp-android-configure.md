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
## <a name="create-an-application-express"></a><span data-ttu-id="73c15-103">Tworzenie aplikacji (Express)</span><span class="sxs-lookup"><span data-stu-id="73c15-103">Create an application (Express)</span></span>
<span data-ttu-id="73c15-104">Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="73c15-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="73c15-105">Zarejestrować aplikację za pośrednictwem hello [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="73c15-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="73c15-106">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="73c15-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="73c15-107">Upewnij się, że jest zaznaczona opcja hello z przewodnikiem instalacji</span><span class="sxs-lookup"><span data-stu-id="73c15-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="73c15-108">Wykonaj identyfikator aplikacji hello hello instrukcje tooobtain i wklej go w kodzie</span><span class="sxs-lookup"><span data-stu-id="73c15-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="73c15-109">Dodawanie rozwiązania tooyour informacji o rejestracji aplikacji (zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="73c15-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="73c15-110">Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="73c15-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="73c15-111">Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister aplikacji</span><span class="sxs-lookup"><span data-stu-id="73c15-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="73c15-112">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="73c15-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="73c15-113">Upewnij się, że jest zaznaczona opcja hello instrukcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="73c15-113">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="73c15-114">Kliknij przycisk `Add Platform`, a następnie wybierz pozycję `Native Application` i kliknij przycisk Zapisz</span><span class="sxs-lookup"><span data-stu-id="73c15-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="73c15-115">Otwórz `MainActivity` (w obszarze `app`  >  `java`  >   *`{host}.{namespace}`* )</span><span class="sxs-lookup"><span data-stu-id="73c15-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="73c15-116">Zastąp hello *[hello aplikacji o identyfikatorze tutaj wprowadź]* w hello wiersz rozpoczynający się `final static String CLIENT_ID` został zarejestrowany identyfikator aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="73c15-116">Replace hello *[Enter hello application Id here]* in hello line starting with `final static String CLIENT_ID` with hello application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="73c15-117">Otwórz `AndroidManifest.xml` (w obszarze `app`  >  `manifests`) hello Dodaj następujące działania zbyt`manifest\application` węzła.</span><span class="sxs-lookup"><span data-stu-id="73c15-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="73c15-118">Rejestruje to `BrowserTabActivity` tooallow hello OS tooresume aplikacji po zakończeniu uwierzytelniania hello:</span><span class="sxs-lookup"><span data-stu-id="73c15-118">This registers a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>
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
<span data-ttu-id="73c15-119">W hello `BrowserTabActivity`, Zastąp `[Enter hello application Id here]` z identyfikatorem aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="73c15-119">In hello `BrowserTabActivity`, replace `[Enter hello application Id here]` with hello application ID.</span></span>
</li>
</ol>
