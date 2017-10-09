---
title: "punktu końcowego v2.0 usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toobuilding aplikacje z logowaniem zarówno Account firmy Microsoft, jak i usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="524f3-103">Logowanie użytkowników usługi Azure AD w jednej aplikacji & Account firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="524f3-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="524f3-104">W hello poza Deweloper aplikacji, którzy chcieli toosupport oba osobistego konta Microsoft i konta pracy z usługą Azure Active Directory była wymagana toointegrate w dwóch osobnych systemach.</span><span class="sxs-lookup"><span data-stu-id="524f3-104">In hello past, an app developer who wanted toosupport both personal Microsoft accounts and work accounts from Azure Active Directory was required toointegrate with two separate systems.</span></span>  <span data-ttu-id="524f3-105">Witaj **punktu końcowego v2.0 usługi Azure AD** wprowadziła nową wersję interfejsu API uwierzytelniania, umożliwiający toosign w obu typów kont przy użyciu jednego prostą integrację.</span><span class="sxs-lookup"><span data-stu-id="524f3-105">hello **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you toosign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="524f3-106">Aplikacji korzystających z punktu końcowego v2.0 hello można również używać interfejsów API REST z hello [Microsoft Graph](https://graph.microsoft.io) za pomocą dowolnego typu konta.</span><span class="sxs-lookup"><span data-stu-id="524f3-106">Apps that use hello v2.0 endpoint can also consume REST APIs from hello [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="524f3-107">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="524f3-107">Getting Started</span></span>
<span data-ttu-id="524f3-108">Wybierz preferowaną platformę z powitania po toobuild listę aplikacji za pomocą naszych biblioteki typu open source & struktury.</span><span class="sxs-lookup"><span data-stu-id="524f3-108">Choose your favorite platform from hello following list toobuild an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="524f3-109">Alternatywnie możesz użyć naszych OAuth 2.0 & OpenID Connect toosend dokumentacji protokołu i odbierać komunikaty protokołu bezpośrednio, bez przy użyciu biblioteki uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="524f3-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation toosend & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="524f3-110">Co nowego</span><span class="sxs-lookup"><span data-stu-id="524f3-110">What's New</span></span>
<span data-ttu-id="524f3-111">tutaj informacje Hello będzie przydatna zrozumieć, co to jest & co nie jest możliwe z punktem końcowym v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="524f3-111">hello information here will be useful in understanding what is & what isn't possible with hello v2.0 endpoint.</span></span>

* <span data-ttu-id="524f3-112">Dowiedz się więcej o hello [typy aplikacji, można tworzyć za pomocą punktu końcowego v2.0 hello](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="524f3-112">Learn about hello [types of apps you can build with hello v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="524f3-113">Zrozumienie hello [ograniczenia, ograniczenia i ograniczenia](active-directory-v2-limitations.md) z punktem końcowym v2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="524f3-113">Understand hello [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with hello v2.0 endpoint.</span></span>
* <span data-ttu-id="524f3-114">Wyewidencjonuj ten przegląd wideo dla punktu końcowego v2.0 hello:</span><span class="sxs-lookup"><span data-stu-id="524f3-114">Check out this overview video for hello v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="524f3-115">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="524f3-115">Reference</span></span>
<span data-ttu-id="524f3-116">Te linki przydadzą się do eksplorowania hello platform szczegółowo:</span><span class="sxs-lookup"><span data-stu-id="524f3-116">These links will be useful for exploring hello platform in depth:</span></span>

* [<span data-ttu-id="524f3-117">Dokumentacja protokołu v2.0</span><span class="sxs-lookup"><span data-stu-id="524f3-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="524f3-118">Odwołania do tokenu w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="524f3-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="524f3-119">Odwołanie do biblioteki w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="524f3-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="524f3-120">Zakresy i zgody w hello punktu końcowego v2.0</span><span class="sxs-lookup"><span data-stu-id="524f3-120">Scopes and Consent in hello v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="524f3-121">Witaj Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="524f3-121">hello Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="524f3-122">Pomoc i obsługa techniczna</span><span class="sxs-lookup"><span data-stu-id="524f3-122">Help & Support</span></span>
<span data-ttu-id="524f3-123">Są to hello najlepsze miejsca tooget pomoc dotyczącą tworzenia w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="524f3-123">These are hello best places tooget help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="524f3-124">Tagi `azure-active-directory` i `adal` w witrynie Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="524f3-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="524f3-125">Opinia o usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="524f3-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="524f3-126">Jeśli wymagane jest tylko toosign kont służbowych z usługą Azure Active Directory, należy zacząć z naszych [przewodnik dewelopera usługi Azure AD](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="524f3-126">If you only need toosign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="524f3-127">punktu końcowego v2.0 Hello jest przeznaczony do użycia przez deweloperów, którzy muszą jawnie toosign osobistego konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="524f3-127">hello v2.0 endpoint is intended for use by developers who explicitly need toosign in Microsoft personal accounts.</span></span>

