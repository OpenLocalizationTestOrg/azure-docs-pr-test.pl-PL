---
title: "Dodaj do roli użytkownika współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "Dodaj użytkownika gościa do roli w usłudze Azure Active Directory"
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
ms.openlocfilehash: e816349ea971c997f655b4d51672dba666bc3e89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permissions-to-users-from-partner-organizations-in-your-azure-active-directory-tenant"></a><span data-ttu-id="44eac-103">Przyznawanie uprawnień użytkownikom w organizacji partnera w dzierżawie usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44eac-103">Grant permissions to users from partner organizations in your Azure Active Directory tenant</span></span>

<span data-ttu-id="44eac-104">Azure użytkowników współpracy B2B usługi Active Directory (Azure AD) są dodawane jako goście w katalogu, a uprawnienia w katalogu są ograniczone przez domyślny.</span><span class="sxs-lookup"><span data-stu-id="44eac-104">Azure Active Directory (Azure AD) B2B collaboration users are added as guest users to the directory, and guest permissions in the directory are restricted by default.</span></span> <span data-ttu-id="44eac-105">Firma może być konieczne niektórzy użytkownicy gościa do pełnienia ról wyższych uprawnień w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="44eac-105">Your business may need some guest users to fill higher-privilege roles in your organization.</span></span> <span data-ttu-id="44eac-106">Do obsługi, zdefiniowanie ról wyższych uprawnień, goście mogą być dodawane do żadnej roli, które chcesz, w zależności od potrzeb organizacji.</span><span class="sxs-lookup"><span data-stu-id="44eac-106">To support defining higher-privilege roles, guest users can be added to any roles you desire, based on your organization's needs.</span></span>

## <a name="default-role"></a><span data-ttu-id="44eac-107">Domyślna rola</span><span class="sxs-lookup"><span data-stu-id="44eac-107">Default role</span></span>

![Domyślna rola](./media/active-directory-b2b-add-guest-to-role/default-role.png)

## <a name="global-administrator-role"></a><span data-ttu-id="44eac-109">Rola administratora globalnego</span><span class="sxs-lookup"><span data-stu-id="44eac-109">Global Administrator Role</span></span>

![Rola administratora globalnego](./media/active-directory-b2b-add-guest-to-role/global-admin-role.png)

## <a name="limited-administrator-role"></a><span data-ttu-id="44eac-111">Rola administratora ograniczone</span><span class="sxs-lookup"><span data-stu-id="44eac-111">Limited Administrator Role</span></span>

![Rola administratora ograniczone](./media/active-directory-b2b-add-guest-to-role/limited-admin-role.png)

## <a name="next-steps"></a><span data-ttu-id="44eac-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="44eac-113">Next steps</span></span>

<span data-ttu-id="44eac-114">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="44eac-114">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="44eac-115">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="44eac-115">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="44eac-116">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="44eac-116">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="44eac-117">Delegowanie B2bB współpracy zaproszenia</span><span class="sxs-lookup"><span data-stu-id="44eac-117">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="44eac-118">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="44eac-118">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="44eac-119">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="44eac-119">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="44eac-120">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="44eac-120">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="44eac-121">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="44eac-121">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="44eac-122">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="44eac-122">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="44eac-123">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="44eac-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="44eac-124">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="44eac-124">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
