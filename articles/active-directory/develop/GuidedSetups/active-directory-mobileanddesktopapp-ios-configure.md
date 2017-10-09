---
title: "Wprowadzenie aaaAzure AD iOS w wersji 2 — Konfigurowanie | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="7f0ef-103">Tworzenie aplikacji (Express)</span><span class="sxs-lookup"><span data-stu-id="7f0ef-103">Create an application (Express)</span></span>
<span data-ttu-id="7f0ef-104">Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="7f0ef-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="7f0ef-105">Zarejestrować aplikację za pośrednictwem hello [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="7f0ef-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="7f0ef-106">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="7f0ef-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="7f0ef-107">Upewnij się, że jest zaznaczona opcja hello z przewodnikiem instalacji</span><span class="sxs-lookup"><span data-stu-id="7f0ef-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="7f0ef-108">Wykonaj identyfikator aplikacji hello hello instrukcje tooobtain i wklej go w kodzie</span><span class="sxs-lookup"><span data-stu-id="7f0ef-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="7f0ef-109">Dodawanie rozwiązania tooyour informacji o rejestracji aplikacji (zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="7f0ef-109">Add your application registration information tooyour solution (Advanced)</span></span>

1.  <span data-ttu-id="7f0ef-110">Przejdź do zbyt[portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="7f0ef-110">Go too[Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="7f0ef-111">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="7f0ef-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="7f0ef-112">Upewnij się, że jest zaznaczona opcja hello instrukcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7f0ef-112">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="7f0ef-113">Kliknij przycisk `Add Platform`, a następnie wybierz pozycję `Native Application` i kliknij przycisk`Save`</span><span class="sxs-lookup"><span data-stu-id="7f0ef-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="7f0ef-114">Przejdź wstecz tooXcode.</span><span class="sxs-lookup"><span data-stu-id="7f0ef-114">Go back tooXcode.</span></span> <span data-ttu-id="7f0ef-115">W `ViewController.swift`, Zastąp hello wiersz rozpoczynający się "`let kClientID`" został zarejestrowany identyfikator aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="7f0ef-115">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with hello application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="7f0ef-116">Kontrolowanie i kliknięcia, <code>Info.plist</code> toobring menu kontekstowe hello w górę, a następnie kliknij przycisk: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="7f0ef-116">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="7f0ef-117">W obszarze hello <code>dict</code> węzła głównego, należy dodać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="7f0ef-117">Under hello <code>dict</code> root node, add hello following:</span></span>
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
<span data-ttu-id="7f0ef-118">Zastąp <i> <code>[Your_Application_Id_Here]</code> </i> z hello został zarejestrowany identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="7f0ef-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with hello Application Id you just registered</span></span>
</li>
</ol>
