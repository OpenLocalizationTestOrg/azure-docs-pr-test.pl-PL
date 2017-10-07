---
title: ustawienia aktywacji roli toomanage aaaHow | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toochange hello domyślne ustawienia dla tożsamości uprzywilejowanych z hello rozszerzenia usługi Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="25372-103">Jak ustawienia aktywacji roli toomanage w usłudze Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="25372-103">How toomanage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="25372-104">Administrator ról uprzywilejowanych można dostosować w usłudze Azure AD Privileged Identity Management (PIM) w organizacji, łącznie ze zmianą hello środowisko dla użytkownika, który jest aktywowanie przypisania roli kwalifikujących się.</span><span class="sxs-lookup"><span data-stu-id="25372-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing hello experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-hello-role-activation-settings"></a><span data-ttu-id="25372-105">Zarządzanie ustawieniami aktywacji roli hello</span><span class="sxs-lookup"><span data-stu-id="25372-105">Manage hello role activation settings</span></span>
1. <span data-ttu-id="25372-106">Przejdź toohello [portalu Azure](https://portal.azure.com) i wybierz hello **Azure AD Privileged Identity Management** aplikacji z hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="25372-106">Go toohello [Azure portal](https://portal.azure.com) and select hello **Azure AD Privileged Identity Management** app from hello dashboard.</span></span>
2. <span data-ttu-id="25372-107">Wybierz **Zarządzanie ról uprzywilejowanych** > **ustawienia** > **ról uprzywilejowanych**.</span><span class="sxs-lookup"><span data-stu-id="25372-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="25372-108">Wybierz rolę hello, którego ustawienia chcesz toomanage.</span><span class="sxs-lookup"><span data-stu-id="25372-108">Choose hello role whose settings you want toomanage.</span></span>

<span data-ttu-id="25372-109">Na stronie Ustawienia powitania dla każdej roli istnieje wiele ustawień, które można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="25372-109">On hello settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="25372-110">Te ustawienia dotyczą tylko użytkownicy, którzy są kwalifikujących się Administratorzy, Administratorzy nie trwałych.</span><span class="sxs-lookup"><span data-stu-id="25372-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="25372-111">**Aktywacje**: hello czasu, w godzinach, które roli pozostaje aktywne, przed jego wygaśnięciem.</span><span class="sxs-lookup"><span data-stu-id="25372-111">**Activations**: hello time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="25372-112">Może to być w przedziale od 1 do 72 godzin.</span><span class="sxs-lookup"><span data-stu-id="25372-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="25372-113">**Powiadomienia**: można wybrać, czy hello system wysyła potwierdzenie, że ich uaktywniono rolę tooadmins wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="25372-113">**Notifications**: You can choose whether or not hello system sends emails tooadmins confirming that they have activated a role.</span></span> <span data-ttu-id="25372-114">Może to być przydatne do wykrywania nieautoryzowanego lub nielegalne aktywacji.</span><span class="sxs-lookup"><span data-stu-id="25372-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="25372-115">**Zdarzenie/żądania biletu**: można wybrać, czy toorequire tooinclude kwalifikujących się administratorów biletu numerów podczas aktywują ich roli.</span><span class="sxs-lookup"><span data-stu-id="25372-115">**Incident/Request Ticket**: You can choose whether or not toorequire eligible admins tooinclude a ticket number when they activate their role.</span></span> <span data-ttu-id="25372-116">Może to być przydatne podczas wykonywania inspekcji dostępu do roli.</span><span class="sxs-lookup"><span data-stu-id="25372-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="25372-117">**Uwierzytelnianie wieloskładnikowe**: można wybrać, czy toorequire tooverify użytkowników tożsamości za pomocą usługi MFA aktywować ich ról.</span><span class="sxs-lookup"><span data-stu-id="25372-117">**Multi-Factor Authentication**: You can choose whether or not toorequire users tooverify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="25372-118">Tylko mają tooverify tego raz dla sesji, nie za każdym razem, gdy ich aktywowania roli.</span><span class="sxs-lookup"><span data-stu-id="25372-118">They only have tooverify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="25372-119">Istnieją dwa tookeep porady na uwadze, po włączeniu usługi MFA:</span><span class="sxs-lookup"><span data-stu-id="25372-119">There are two tips tookeep in mind when you enable MFA:</span></span>

* <span data-ttu-id="25372-120">Użytkownicy, którzy mają konta Microsoft do ich adresów e-mail (zazwyczaj @outlook.com, ale nie zawsze) nie można zarejestrować w usłudze Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="25372-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="25372-121">Chcesz tooassign toousers ról z kontami Microsoft, należy były administratorów trwałych lub Wyłącz uwierzytelnianie wieloskładnikowe dla tej roli.</span><span class="sxs-lookup"><span data-stu-id="25372-121">If you want tooassign roles toousers with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="25372-122">Nie można wyłączyć usługi MFA dla wysoko uprzywilejowane ról dla usługi Azure AD i usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="25372-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="25372-123">Jest to zabezpieczenie, ponieważ te role powinny być starannie chronione:</span><span class="sxs-lookup"><span data-stu-id="25372-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="25372-124">Administrator aplikacji</span><span class="sxs-lookup"><span data-stu-id="25372-124">Application administrator</span></span>
  * <span data-ttu-id="25372-125">Administrator serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="25372-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="25372-126">Administrator rozliczeń</span><span class="sxs-lookup"><span data-stu-id="25372-126">Billing administrator</span></span>  
  * <span data-ttu-id="25372-127">Administrator zgodności</span><span class="sxs-lookup"><span data-stu-id="25372-127">Compliance administrator</span></span>  
  * <span data-ttu-id="25372-128">Administrator programu CRM usługi</span><span class="sxs-lookup"><span data-stu-id="25372-128">CRM service administrator</span></span>
  * <span data-ttu-id="25372-129">Osoba zatwierdzająca dostępu skrytki klienta</span><span class="sxs-lookup"><span data-stu-id="25372-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="25372-130">Składnik zapisywania katalogu</span><span class="sxs-lookup"><span data-stu-id="25372-130">Directory writer</span></span>  
  * <span data-ttu-id="25372-131">Administrator programu Exchange</span><span class="sxs-lookup"><span data-stu-id="25372-131">Exchange administrator</span></span>  
  * <span data-ttu-id="25372-132">Administrator globalny</span><span class="sxs-lookup"><span data-stu-id="25372-132">Global administrator</span></span>
  * <span data-ttu-id="25372-133">Administrator usługi Intune</span><span class="sxs-lookup"><span data-stu-id="25372-133">Intune service administrator</span></span>
  * <span data-ttu-id="25372-134">Skrzynki pocztowej administratora</span><span class="sxs-lookup"><span data-stu-id="25372-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="25372-135">Obsługa tier1 partnera</span><span class="sxs-lookup"><span data-stu-id="25372-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="25372-136">Obsługa tier2 partnera</span><span class="sxs-lookup"><span data-stu-id="25372-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="25372-137">Administrator ról uprzywilejowanych</span><span class="sxs-lookup"><span data-stu-id="25372-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="25372-138">Administrator zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="25372-138">Security administrator</span></span>  
  * <span data-ttu-id="25372-139">Administrator programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="25372-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="25372-140">Administrator programu Skype dla firm</span><span class="sxs-lookup"><span data-stu-id="25372-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="25372-141">Administrator konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="25372-141">User account administrator</span></span>  

<span data-ttu-id="25372-142">Aby uzyskać więcej informacji na temat przy użyciu usługi MFA w usłudze PIM zobacz [jak tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="25372-142">For more information about using MFA with PIM see [How tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="25372-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25372-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

