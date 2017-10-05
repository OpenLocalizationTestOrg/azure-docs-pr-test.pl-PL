---
title: "Delegowanie zaproszeń do skorzystania z usługi Azure Active Directory B2B współpracy | Dokumentacja firmy Microsoft"
description: "Właściwości użytkownika współpraca w usłudze Azure Active Directory B2B są konfigurowane"
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
ms.openlocfilehash: 78613cc978b585a98d235245194c02371f7f3849
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="7ec48-103">Delegowanie zaproszeń do skorzystania z usługi Azure Active Directory B2B współpracy</span><span class="sxs-lookup"><span data-stu-id="7ec48-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="7ec48-104">Ze współpracą między firmami (B2B) w usłudze Azure Active Directory (Azure AD) nie trzeba być administratorem globalnym, aby wysłać zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="7ec48-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have to be a global admin to send invitations.</span></span> <span data-ttu-id="7ec48-105">Można użyć zasad i delegować zaproszeń do użytkowników, których role zezwolić im na wysyłanie zaproszeń do skorzystania z.</span><span class="sxs-lookup"><span data-stu-id="7ec48-105">Instead, you can use policies and delegate invitations to users whose roles allow them to send invitations.</span></span> <span data-ttu-id="7ec48-106">Jest ważne nowy sposób, aby delegować zaproszenia użytkownika gościa za pomocą roli zapraszającej gościa.</span><span class="sxs-lookup"><span data-stu-id="7ec48-106">An important new way to delegate guest user invitations is through the Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="7ec48-107">Rola zapraszającej gościa</span><span class="sxs-lookup"><span data-stu-id="7ec48-107">Guest Inviter role</span></span>
<span data-ttu-id="7ec48-108">Użytkownika można przypisać do roli zapraszającej gościa, aby wysłać zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="7ec48-108">We can assign the user to Guest Inviter role to send invitations.</span></span> <span data-ttu-id="7ec48-109">Nie trzeba być członkiem roli administratora globalnego Wyślij zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="7ec48-109">You don't have to be member of the global admin role to send invitations.</span></span> <span data-ttu-id="7ec48-110">Domyślnie normalnych użytkowników można także wywoływać interfejs API zaproszenia, chyba że administrator globalny wyłączone zaproszeń do normalnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7ec48-110">By default, regular users can also invoke the invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="7ec48-111">Użytkownik może również wywołać interfejsu API przy użyciu portalu Azure lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ec48-111">A user can also invoke the API using the Azure portal or PowerShell.</span></span>

<span data-ttu-id="7ec48-112">Oto przykład pokazujący sposób, aby dodać użytkownika do roli zapraszającej gościa za pomocą programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7ec48-112">Here's an example that shows how to use PowerShell to add a user to the Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="7ec48-113">Formant, który można zaprosić</span><span class="sxs-lookup"><span data-stu-id="7ec48-113">Control who can invite</span></span>

![Kontrolowanie sposobu zaprosić](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="7ec48-115">Współpracy B2B usługi Azure AD administratora dzierżawy. można ustawić następujące zasady zaproszenia:</span><span class="sxs-lookup"><span data-stu-id="7ec48-115">With Azure AD B2B collaboration, a tenant admin can set the following invitation policies:</span></span>

- <span data-ttu-id="7ec48-116">Wyłącz zaproszenia</span><span class="sxs-lookup"><span data-stu-id="7ec48-116">Turn off invitations</span></span>
- <span data-ttu-id="7ec48-117">Tylko administratorzy i użytkownicy w roli zapraszającej gościa można zaprosić</span><span class="sxs-lookup"><span data-stu-id="7ec48-117">Only admins and users in the Guest Inviter role can invite</span></span>
- <span data-ttu-id="7ec48-118">Zaprosić administratorów, roli zapraszającej Gość i członków</span><span class="sxs-lookup"><span data-stu-id="7ec48-118">Admins, the Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="7ec48-119">Wszyscy użytkownicy, w tym gości, można zaprosić</span><span class="sxs-lookup"><span data-stu-id="7ec48-119">All users, including guests, can invite</span></span>

<span data-ttu-id="7ec48-120">Domyślnie dzierżaw są ustawione na #4.</span><span class="sxs-lookup"><span data-stu-id="7ec48-120">By default, tenants are set to #4.</span></span> <span data-ttu-id="7ec48-121">(Wszystkich użytkowników, w tym gości, można zaprosić użytkowników B2B).</span><span class="sxs-lookup"><span data-stu-id="7ec48-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ec48-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ec48-122">Next steps</span></span>

<span data-ttu-id="7ec48-123">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="7ec48-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="7ec48-124">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="7ec48-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="7ec48-125">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7ec48-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="7ec48-126">Dodawanie do roli użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7ec48-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="7ec48-127">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7ec48-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="7ec48-128">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ec48-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="7ec48-129">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7ec48-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="7ec48-130">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7ec48-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="7ec48-131">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="7ec48-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="7ec48-132">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="7ec48-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="7ec48-133">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7ec48-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
