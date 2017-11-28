---
title: "Azure AD w wersji 2 dla systemu iOS Getting Started — Konfigurowanie (ARP) | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 50cb4a2803b6aebe8b39ec9fb02da2293c1065fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="3f151-103">Dodawanie informacji o rejestracji aplikacji do aplikacji</span><span class="sxs-lookup"><span data-stu-id="3f151-103">Add the application’s registration information to your app</span></span>

<span data-ttu-id="3f151-104">W tym kroku musisz dodać identyfikator aplikacji do projektu:</span><span class="sxs-lookup"><span data-stu-id="3f151-104">In this step, you need to add the Application Id to your project:</span></span>

1.  <span data-ttu-id="3f151-105">W `ViewController.swift`, Zastąp wiersz rozpoczynający się "`let kClientID`" z:</span><span class="sxs-lookup"><span data-stu-id="3f151-105">In `ViewController.swift`, replace the line starting with '`let kClientID`' with:</span></span>
```swift
let kClientID = "[Enter the application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="3f151-106">Kontrolowanie i kliknięcia, <code>Info.plist</code> wyświetlić menu kontekstowe, a następnie kliknij przycisk: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="3f151-106">Control+click <code>Info.plist</code> to bring up the contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="3f151-107">W obszarze <code>dict</code> węzła głównego, należy dodać następujące:</span><span class="sxs-lookup"><span data-stu-id="3f151-107">Under the <code>dict</code> root node, add the following:</span></span>
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
            <string>msal[Enter the application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
