---
title: "iOS v2 aaaAzure AD Getting Started — Konfigurowanie (ARP) | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e5087e13160243d808b1d02771fa66fb332cfad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="ae791-103">Dodawanie aplikacji hello rejestracji informacji tooyour aplikacji</span><span class="sxs-lookup"><span data-stu-id="ae791-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="ae791-104">W tym kroku należy tooadd hello identyfikator aplikacji tooyour projektu:</span><span class="sxs-lookup"><span data-stu-id="ae791-104">In this step, you need tooadd hello Application Id tooyour project:</span></span>

1.  <span data-ttu-id="ae791-105">W `ViewController.swift`, Zastąp hello wiersz rozpoczynający się "`let kClientID`" z:</span><span class="sxs-lookup"><span data-stu-id="ae791-105">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with:</span></span>
```swift
let kClientID = "[Enter hello application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="ae791-106">Kontrolowanie i kliknięcia, <code>Info.plist</code> toobring menu kontekstowe hello w górę, a następnie kliknij przycisk: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="ae791-106">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="ae791-107">W obszarze hello <code>dict</code> węzła głównego, należy dodać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ae791-107">Under hello <code>dict</code> root node, add hello following:</span></span>
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
            <string>msal[Enter hello application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
