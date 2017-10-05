---
title: "Ograniczenia współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "Bieżących ograniczeń dotyczących współpracy usługi Azure Active Directory B2B"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 581e5d1fb5fb08d0dc89ed2c85edcb5f0005650b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="c3b0f-103">Ograniczenia dotyczące współpracy B2B usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3b0f-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="c3b0f-104">Azure współpracy B2B usługi Active Directory (Azure AD) podlega obecnie ograniczenia opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="c3b0f-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="c3b0f-105">Możliwe podwójne uwierzytelnianie wieloskładnikowe</span><span class="sxs-lookup"><span data-stu-id="c3b0f-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="c3b0f-106">Z B2B usługi Azure AD można wymusić uwierzytelnianie wieloskładnikowe w organizacji zasobów (zaproszenia organizacji).</span><span class="sxs-lookup"><span data-stu-id="c3b0f-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="c3b0f-107">Przyczyny tego podejścia wyszczególnione w [dostępu warunkowego dla użytkowników współpracy B2B](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="c3b0f-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="c3b0f-108">Jeśli partnera już uwierzytelnianie wieloskładnikowe, konfigurowanie i wymuszane, użytkowników może być konieczne przeprowadzenie uwierzytelniania raz w domu organizacji, a następnie ponownie w należy do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="c3b0f-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="c3b0f-109">Natychmiastowa</span><span class="sxs-lookup"><span data-stu-id="c3b0f-109">Instant-on</span></span>
<span data-ttu-id="c3b0f-110">W przepływach współpracy B2B możemy dodać użytkowników do katalogu i dynamiczne aktualizowanie ich podczas realizacji zaproszenia, przypisanie aplikacji i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c3b0f-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="c3b0f-111">Aktualizacje i zapisy zwykle się tak zdarzyć w przypadku jednego katalogu i musi zostać zreplikowana we wszystkich wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="c3b0f-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="c3b0f-112">Gdy wszystkie wystąpienia są aktualizowane zakończeniem replikacji.</span><span class="sxs-lookup"><span data-stu-id="c3b0f-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="c3b0f-113">Czasami, gdy obiekt jest zapisywane lub zaktualizowane w jedno wystąpienie, a wywołanie do pobrania tego obiektu jest do innego wystąpienia, może wystąpić opóźnienia w replikacji.</span><span class="sxs-lookup"><span data-stu-id="c3b0f-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span></span> <span data-ttu-id="c3b0f-114">Jeśli tak się stanie, Odśwież lub ponów próbę, aby pomóc.</span><span class="sxs-lookup"><span data-stu-id="c3b0f-114">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="c3b0f-115">Jeśli piszesz aplikację przy użyciu naszego interfejsu API ponownych prób z niektórych wycofania jest rozwiązaniem obrony, właściwą rozwiązanie tego problemu.</span><span class="sxs-lookup"><span data-stu-id="c3b0f-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3b0f-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3b0f-116">Next steps</span></span>

<span data-ttu-id="c3b0f-117">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c3b0f-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c3b0f-118">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="c3b0f-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c3b0f-119">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c3b0f-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="c3b0f-120">Dodawanie do roli użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c3b0f-120">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="c3b0f-121">Delegowanie B2bB współpracy zaproszenia</span><span class="sxs-lookup"><span data-stu-id="c3b0f-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="c3b0f-122">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c3b0f-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="c3b0f-123">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3b0f-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="c3b0f-124">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c3b0f-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="c3b0f-125">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c3b0f-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="c3b0f-126">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="c3b0f-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="c3b0f-127">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="c3b0f-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
