---
title: "aaaLimitations współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="814a3-103">Ograniczenia dotyczące współpracy B2B usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="814a3-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="814a3-104">Azure współpracy B2B usługi Active Directory (Azure AD) jest obecnie podmiotu toohello ograniczenia opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="814a3-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject toohello limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="814a3-105">Możliwe podwójne uwierzytelnianie wieloskładnikowe</span><span class="sxs-lookup"><span data-stu-id="814a3-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="814a3-106">Z B2B usługi Azure AD można wymusić uwierzytelnianie wieloskładnikowe w organizacji zasobów hello (hello zapraszanie organizacji).</span><span class="sxs-lookup"><span data-stu-id="814a3-106">With Azure AD B2B, you can enforce multi-factor authentication at hello resource organization (hello inviting organization).</span></span> <span data-ttu-id="814a3-107">Hello przyczyny tego podejścia wyszczególnione w [dostępu warunkowego dla użytkowników współpracy B2B](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="814a3-107">hello reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="814a3-108">Jeśli partnera już uwierzytelnianie wieloskładnikowe, konfigurowanie i wymuszane, ich użytkownicy mogą mieć uwierzytelniania hello tooperform raz w domu organizacji, a następnie ponownie w należy do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="814a3-108">If a partner already has multi-factor authentication set up and enforced, their users might have tooperform hello authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="814a3-109">Natychmiastowa</span><span class="sxs-lookup"><span data-stu-id="814a3-109">Instant-on</span></span>
<span data-ttu-id="814a3-110">Przepływów współpracy hello B2B możemy dodać katalog toohello użytkowników i dynamiczne aktualizowanie ich podczas realizacji zaproszenia, przypisanie aplikacji i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="814a3-110">In hello B2B collaboration flows, we add users toohello directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="814a3-111">aktualizacje Hello i zapisy zwykle się tak zdarzyć w przypadku jednego katalogu i musi zostać zreplikowana we wszystkich wystąpieniach.</span><span class="sxs-lookup"><span data-stu-id="814a3-111">hello updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="814a3-112">Gdy wszystkie wystąpienia są aktualizowane zakończeniem replikacji.</span><span class="sxs-lookup"><span data-stu-id="814a3-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="814a3-113">Czasami podczas zapisywane lub zaktualizowane w jedno wystąpienie obiektu hello i hello wywołać tooretrieve ten obiekt jest tooanother wystąpienia, mogą występować opóźnienia w replikacji.</span><span class="sxs-lookup"><span data-stu-id="814a3-113">Sometimes when hello object is written or updated in one instance and hello call tooretrieve this object is tooanother instance, replication latencies can occur.</span></span> <span data-ttu-id="814a3-114">Jeśli tak się stanie, Odśwież lub spróbuj ponownie toohelp.</span><span class="sxs-lookup"><span data-stu-id="814a3-114">If that happens, refresh or retry toohelp.</span></span> <span data-ttu-id="814a3-115">Podczas pisania aplikacji za pomocą naszych interfejsu API, a następnie ponownych prób z niektórymi wycofania jest tooalleviate praktyki obrony, właściwą ten problem.</span><span class="sxs-lookup"><span data-stu-id="814a3-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice tooalleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="814a3-116">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="814a3-116">Next steps</span></span>

<span data-ttu-id="814a3-117">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="814a3-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="814a3-118">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="814a3-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="814a3-119">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="814a3-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="814a3-120">Dodawanie roli tooa użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="814a3-120">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="814a3-121">Delegowanie B2bB współpracy zaproszenia</span><span class="sxs-lookup"><span data-stu-id="814a3-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="814a3-122">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="814a3-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="814a3-123">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="814a3-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="814a3-124">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="814a3-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="814a3-125">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="814a3-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="814a3-126">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="814a3-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="814a3-127">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="814a3-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
