---
title: "Rola tooa użytkownika współpracy B2B usługi Azure Active Directory aaaAdd | Dokumentacja firmy Microsoft"
description: "Dodaj rolę tooa użytkownika gościa w usłudze Azure Active Directory"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ccc58a0c8ecc73f8e79a8d827efdc0ff93846a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permissions-toousers-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="c5d5d-103">Udziel uprawnień toousers z organizacji partnera w dzierżawie usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5d5d-103">Grant permissions toousers from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="c5d5d-104">Azure użytkowników współpracy B2B usługi Active Directory (Azure AD) są dodawane jako katalog toohello użytkowników gościa, a uprawnienia w katalogu hello są ograniczone przez domyślny.</span><span class="sxs-lookup"><span data-stu-id="c5d5d-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users toohello directory, and guest permissions in hello directory are restricted by default.</span></span> <span data-ttu-id="c5d5d-105">Firma może być konieczne niektórych gościa użytkowników toofill wyższych uprawnień ról w organizacji.</span><span class="sxs-lookup"><span data-stu-id="c5d5d-105">Your business may need some guest users toofill higher-privilege roles in your organization.</span></span> <span data-ttu-id="c5d5d-106">zdefiniowanie ról wyższych uprawnień toosupport goście mogą być dodane tooany ról wymaganych, w zależności od potrzeb organizacji.</span><span class="sxs-lookup"><span data-stu-id="c5d5d-106">toosupport defining higher-privilege roles, guest users can be added tooany roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="c5d5d-107">Domyślna rola</span><span class="sxs-lookup"><span data-stu-id="c5d5d-107">Default role</span></span>

![Domyślna rola](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="c5d5d-109">Rola administratora globalnego</span><span class="sxs-lookup"><span data-stu-id="c5d5d-109">Global Administrator Role</span></span>

![Rola administratora globalnego](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="c5d5d-111">Rola administratora ograniczone</span><span class="sxs-lookup"><span data-stu-id="c5d5d-111">Limited Administrator Role</span></span>

![Rola administratora ograniczone](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="c5d5d-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c5d5d-113">Next steps</span></span>

<span data-ttu-id="c5d5d-114">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c5d5d-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c5d5d-115">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="c5d5d-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c5d5d-116">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c5d5d-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="c5d5d-117">Delegowanie B2bB współpracy zaproszenia</span><span class="sxs-lookup"><span data-stu-id="c5d5d-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="c5d5d-118">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c5d5d-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="c5d5d-119">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5d5d-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="c5d5d-120">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c5d5d-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="c5d5d-121">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c5d5d-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="c5d5d-122">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="c5d5d-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="c5d5d-123">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="c5d5d-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="c5d5d-124">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="c5d5d-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
