---
title: "Wprowadzenie Azure AD w wersji 2 dla systemu iOS — Konfigurowanie | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 0ebca65585fc87bd4a85ba092cd423fce9540f58
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="7d69f-103">Tworzenie aplikacji (Express)</span><span class="sxs-lookup"><span data-stu-id="7d69f-103">Create an application (Express)</span></span>
<span data-ttu-id="7d69f-104">Teraz musisz zarejestrować aplikację w *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="7d69f-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="7d69f-105">Zarejestrować aplikację za pośrednictwem [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="7d69f-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="7d69f-106">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="7d69f-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="7d69f-107">Upewnij się, że zaznaczono opcję instrukcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7d69f-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="7d69f-108">Postępuj zgodnie z instrukcjami, aby uzyskać identyfikator aplikacji i wklej go w kodzie</span><span class="sxs-lookup"><span data-stu-id="7d69f-108">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="7d69f-109">Dodaj swoje informacje rejestracyjne aplikacji do rozwiązania (zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="7d69f-109">Add your application registration information to your solution (Advanced)</span></span>

1.  <span data-ttu-id="7d69f-110">Przejdź do [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="7d69f-110">Go to [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="7d69f-111">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="7d69f-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="7d69f-112">Upewnij się, że jest zaznaczona opcja instrukcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7d69f-112">Make sure the option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="7d69f-113">Kliknij przycisk `Add Platform`, a następnie wybierz pozycję `Native Application` i kliknij przycisk`Save`</span><span class="sxs-lookup"><span data-stu-id="7d69f-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="7d69f-114">Wróć do Xcode.</span><span class="sxs-lookup"><span data-stu-id="7d69f-114">Go back to Xcode.</span></span> <span data-ttu-id="7d69f-115">W `ViewController.swift`, Zastąp wiersz rozpoczynający się "`let kClientID`" z Identyfikatorem aplikacji został zarejestrowany:</span><span class="sxs-lookup"><span data-stu-id="7d69f-115">In `ViewController.swift`, replace the line starting with '`let kClientID`' with the application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="7d69f-116">Kontrolowanie i kliknięcia, <code>Info.plist</code> wyświetlić menu kontekstowe, a następnie kliknij przycisk: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="7d69f-116">Control+click <code>Info.plist</code> to bring up the contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="7d69f-117">W obszarze <code>dict</code> węzła głównego, należy dodać następujące:</span><span class="sxs-lookup"><span data-stu-id="7d69f-117">Under the <code>dict</code> root node, add the following:</span></span>
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
<span data-ttu-id="7d69f-118">Zastąp <i> <code>[Your_Application_Id_Here]</code> </i> z identyfikatorem aplikacji został zarejestrowany</span><span class="sxs-lookup"><span data-stu-id="7d69f-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with the Application Id you just registered</span></span>
</li>
</ol>
