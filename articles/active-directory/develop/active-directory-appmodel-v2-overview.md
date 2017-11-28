---
title: "Punktu końcowego v2.0 usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do kompilowania aplikacji za pomocą logowanie zarówno Account firmy Microsoft, jak i usługi Azure Active Directory."
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
ms.openlocfilehash: 1e286044fb1a1b367fcac2dc14c47f68d5ed120d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="6d9c7-103">Logowanie użytkowników usługi Azure AD w jednej aplikacji & Account firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="6d9c7-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="6d9c7-104">W przeszłości Deweloper aplikacji, którzy chcieli obsługuje oba osobistego konta Microsoft i działać kont z usługi Azure Active Directory było wymagane do integracji z dwóch oddzielnych systemach.</span><span class="sxs-lookup"><span data-stu-id="6d9c7-104">In the past, an app developer who wanted to support both personal Microsoft accounts and work accounts from Azure Active Directory was required to integrate with two separate systems.</span></span>  <span data-ttu-id="6d9c7-105">**Punktu końcowego v2.0 usługi Azure AD** wprowadziła nową wersję interfejsu API uwierzytelniania, umożliwiający Zaloguj się w obu typów kont przy użyciu jednego prostą integrację.</span><span class="sxs-lookup"><span data-stu-id="6d9c7-105">The **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you to sign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="6d9c7-106">Aplikacje korzystające z punktem końcowym v2.0 można również korzystać z interfejsów API REST z [Microsoft Graph](https://graph.microsoft.io) za pomocą dowolnego typu konta.</span><span class="sxs-lookup"><span data-stu-id="6d9c7-106">Apps that use the v2.0 endpoint can also consume REST APIs from the [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6d9c7-107">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="6d9c7-107">Getting Started</span></span>
<span data-ttu-id="6d9c7-108">Wybierz preferowaną platformę z poniższej listy kompilowania aplikacji za pomocą naszych typu open source bibliotek i platform.</span><span class="sxs-lookup"><span data-stu-id="6d9c7-108">Choose your favorite platform from the following list to build an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="6d9c7-109">Alternatywnie można użyć naszej dokumentacji protokołu OAuth 2.0 & OpenID Connect do wysyłania i odbierania wiadomości protokołu bezpośrednio, bez przy użyciu biblioteki uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="6d9c7-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation to send & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="6d9c7-110">Co nowego</span><span class="sxs-lookup"><span data-stu-id="6d9c7-110">What's New</span></span>
<span data-ttu-id="6d9c7-111">Informacje w tym miejscu będą przydatne zrozumieć, co to jest & co nie jest możliwe z punktem końcowym v2.0.</span><span class="sxs-lookup"><span data-stu-id="6d9c7-111">The information here will be useful in understanding what is & what isn't possible with the v2.0 endpoint.</span></span>

* <span data-ttu-id="6d9c7-112">Dowiedz się więcej o [typy aplikacji, można tworzyć z punktem końcowym v2.0](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="6d9c7-112">Learn about the [types of apps you can build with the v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="6d9c7-113">Zrozumienie [ograniczenia, ograniczenia i ograniczenia](active-directory-v2-limitations.md) z punktem końcowym v2.0.</span><span class="sxs-lookup"><span data-stu-id="6d9c7-113">Understand the [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with the v2.0 endpoint.</span></span>
* <span data-ttu-id="6d9c7-114">Wyewidencjonuj ten przegląd wideo dla punktu końcowego v2.0:</span><span class="sxs-lookup"><span data-stu-id="6d9c7-114">Check out this overview video for the v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="6d9c7-115">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="6d9c7-115">Reference</span></span>
<span data-ttu-id="6d9c7-116">Te linki przydadzą się do eksplorowania platform szczegółowo:</span><span class="sxs-lookup"><span data-stu-id="6d9c7-116">These links will be useful for exploring the platform in depth:</span></span>

* [<span data-ttu-id="6d9c7-117">Dokumentacja protokołu v2.0</span><span class="sxs-lookup"><span data-stu-id="6d9c7-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="6d9c7-118">Odwołania do tokenu w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="6d9c7-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="6d9c7-119">Odwołanie do biblioteki w wersji 2.0</span><span class="sxs-lookup"><span data-stu-id="6d9c7-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="6d9c7-120">Zakresy i zgody w punkcie końcowym v2.0</span><span class="sxs-lookup"><span data-stu-id="6d9c7-120">Scopes and Consent in the v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="6d9c7-121">Program Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="6d9c7-121">The Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="6d9c7-122">Pomoc i obsługa techniczna</span><span class="sxs-lookup"><span data-stu-id="6d9c7-122">Help & Support</span></span>
<span data-ttu-id="6d9c7-123">To są najlepsze miejsca, aby uzyskać pomoc w programowaniu dla usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6d9c7-123">These are the best places to get help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="6d9c7-124">Tagi `azure-active-directory` i `adal` w witrynie Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="6d9c7-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="6d9c7-125">Opinia o usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d9c7-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="6d9c7-126">Jeśli wymagane jest tylko do logowania do kont służbowych z usługi Azure Active Directory, należy zacząć z naszych [przewodnik dewelopera usługi Azure AD](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="6d9c7-126">If you only need to sign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="6d9c7-127">Punktem końcowym v2.0 jest przeznaczony do użycia przez deweloperów, którzy jawnie konieczne logowanie w osobistego konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6d9c7-127">The v2.0 endpoint is intended for use by developers who explicitly need to sign in Microsoft personal accounts.</span></span>

