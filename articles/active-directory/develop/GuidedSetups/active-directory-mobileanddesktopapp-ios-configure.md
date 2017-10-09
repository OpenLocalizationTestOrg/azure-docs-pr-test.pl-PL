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
## <a name="create-an-application-express"></a>Tworzenie aplikacji (Express)
Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:
1. Zarejestrować aplikację za pośrednictwem hello [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)
2.  Wprowadź nazwę aplikacji i poczty e-mail
3.  Upewnij się, że jest zaznaczona opcja hello z przewodnikiem instalacji
4.  Wykonaj identyfikator aplikacji hello hello instrukcje tooobtain i wklej go w kodzie

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Dodawanie rozwiązania tooyour informacji o rejestracji aplikacji (zaawansowane)

1.  Przejdź do zbyt[portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app)
2.  Wprowadź nazwę aplikacji i poczty e-mail
3.  Upewnij się, że jest zaznaczona opcja hello instrukcje konfiguracji
4.  Kliknij przycisk `Add Platform`, a następnie wybierz pozycję `Native Application` i kliknij przycisk`Save`
5.  Przejdź wstecz tooXcode. W `ViewController.swift`, Zastąp hello wiersz rozpoczynający się "`let kClientID`" został zarejestrowany identyfikator aplikacji hello:

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Kontrolowanie i kliknięcia, <code>Info.plist</code> toobring menu kontekstowe hello w górę, a następnie kliknij przycisk: <code>Open As</code>> <code>Source Code</code>
</li>
<li>
W obszarze hello <code>dict</code> węzła głównego, należy dodać następujące hello:
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
Zastąp <i> <code>[Your_Application_Id_Here]</code> </i> z hello został zarejestrowany identyfikator aplikacji
</li>
</ol>
