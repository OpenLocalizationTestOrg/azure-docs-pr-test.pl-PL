---
title: "aaaDelegate zaproszeń do współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="8bffb-103">Delegowanie zaproszeń do skorzystania z usługi Azure Active Directory B2B współpracy</span><span class="sxs-lookup"><span data-stu-id="8bffb-103">Delegate invitations for Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="8bffb-104">Ze współpracą między firmami (B2B) w usłudze Azure Active Directory (Azure AD) nie masz toobe zaproszenia toosend administratora globalnego.</span><span class="sxs-lookup"><span data-stu-id="8bffb-104">With Azure Active Directory (Azure AD) business-to-business (B2B) collaboration, you do not have toobe a global admin toosend invitations.</span></span> <span data-ttu-id="8bffb-105">Zamiast tego można użyć zasad i delegować toousers zaproszenia, których role zezwolić im toosend zaproszeń do skorzystania z.</span><span class="sxs-lookup"><span data-stu-id="8bffb-105">Instead, you can use policies and delegate invitations toousers whose roles allow them toosend invitations.</span></span> <span data-ttu-id="8bffb-106">Jest ważne nowy sposób toodelegate gościa użytkownika zaproszeń do skorzystania z za pomocą hello zapraszającej gościa roli.</span><span class="sxs-lookup"><span data-stu-id="8bffb-106">An important new way toodelegate guest user invitations is through hello Guest Inviter role.</span></span>

## <a name="guest-inviter-role"></a><span data-ttu-id="8bffb-107">Rola zapraszającej gościa</span><span class="sxs-lookup"><span data-stu-id="8bffb-107">Guest Inviter role</span></span>
<span data-ttu-id="8bffb-108">Firma Microsoft można przypisać tooGuest użytkownika hello toosend zaproszeń do skorzystania z zapraszającej roli.</span><span class="sxs-lookup"><span data-stu-id="8bffb-108">We can assign hello user tooGuest Inviter role toosend invitations.</span></span> <span data-ttu-id="8bffb-109">Nie ma elementu członkowskiego toobe zaproszeń toosend roli administratora globalnego hello.</span><span class="sxs-lookup"><span data-stu-id="8bffb-109">You don't have toobe member of hello global admin role toosend invitations.</span></span> <span data-ttu-id="8bffb-110">Domyślnie normalnych użytkowników można także wywoływać interfejs API zaproszenia hello, chyba że administrator globalny wyłączone zaproszeń do normalnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8bffb-110">By default, regular users can also invoke hello invite API unless a global admin disabled invitations for regular users.</span></span> <span data-ttu-id="8bffb-111">Użytkownik może również wywołać hello interfejsu API przy użyciu hello portalu Azure lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bffb-111">A user can also invoke hello API using hello Azure portal or PowerShell.</span></span>

<span data-ttu-id="8bffb-112">Oto przykład pokazujący sposób toouse PowerShell tooadd roli użytkownika gościa zapraszającej toohello:</span><span class="sxs-lookup"><span data-stu-id="8bffb-112">Here's an example that shows how toouse PowerShell tooadd a user toohello Guest Inviter role:</span></span>

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a><span data-ttu-id="8bffb-113">Formant, który można zaprosić</span><span class="sxs-lookup"><span data-stu-id="8bffb-113">Control who can invite</span></span>

![Formant jak tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

<span data-ttu-id="8bffb-115">Współpracy B2B usługi Azure AD administratora dzierżawy. można ustawić następujące zasady zaproszenia hello:</span><span class="sxs-lookup"><span data-stu-id="8bffb-115">With Azure AD B2B collaboration, a tenant admin can set hello following invitation policies:</span></span>

- <span data-ttu-id="8bffb-116">Wyłącz zaproszenia</span><span class="sxs-lookup"><span data-stu-id="8bffb-116">Turn off invitations</span></span>
- <span data-ttu-id="8bffb-117">Tylko administratorzy i użytkownicy w roli gościa zapraszającej hello można zaprosić</span><span class="sxs-lookup"><span data-stu-id="8bffb-117">Only admins and users in hello Guest Inviter role can invite</span></span>
- <span data-ttu-id="8bffb-118">Administratorzy, hello zapraszającej gościa roli i elementów członkowskich można zaprosić</span><span class="sxs-lookup"><span data-stu-id="8bffb-118">Admins, hello Guest Inviter role, and members can invite</span></span>
- <span data-ttu-id="8bffb-119">Wszyscy użytkownicy, w tym gości, można zaprosić</span><span class="sxs-lookup"><span data-stu-id="8bffb-119">All users, including guests, can invite</span></span>

<span data-ttu-id="8bffb-120">Dzierżawców są domyślnie zbyt #4.</span><span class="sxs-lookup"><span data-stu-id="8bffb-120">By default, tenants are set too#4.</span></span> <span data-ttu-id="8bffb-121">(Wszystkich użytkowników, w tym gości, można zaprosić użytkowników B2B).</span><span class="sxs-lookup"><span data-stu-id="8bffb-121">(All users, including guests, can invite B2B users.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bffb-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8bffb-122">Next steps</span></span>

<span data-ttu-id="8bffb-123">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="8bffb-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="8bffb-124">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="8bffb-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="8bffb-125">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="8bffb-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="8bffb-126">Dodawanie roli tooa użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="8bffb-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="8bffb-127">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="8bffb-127">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="8bffb-128">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bffb-128">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="8bffb-129">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="8bffb-129">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="8bffb-130">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="8bffb-130">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="8bffb-131">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="8bffb-131">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="8bffb-132">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="8bffb-132">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="8bffb-133">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="8bffb-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
