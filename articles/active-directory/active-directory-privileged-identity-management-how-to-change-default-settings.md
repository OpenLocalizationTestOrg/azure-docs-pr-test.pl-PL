---
title: "Jak zarządzać ustawienia aktywacji dla roli | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zmienić ustawienia domyślne dla uprzywilejowanymi tożsamościami przy rozszerzenia usługi Azure Active Directory Privileged Identity Management."
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
ms.openlocfilehash: 23605e89cd1846d2e06e48cb5d3e0191cb9e9b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="461e6-103">Jak zarządzać ustawienia roli aktywacji w usłudze Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="461e6-103">How to manage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="461e6-104">Administrator ról uprzywilejowanych można dostosować w usłudze Azure AD Privileged Identity Management (PIM) w organizacji, łącznie ze zmianą środowisko dla użytkownika, który jest aktywowanie przypisania roli kwalifikujących się.</span><span class="sxs-lookup"><span data-stu-id="461e6-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-the-role-activation-settings"></a><span data-ttu-id="461e6-105">Zarządzanie ustawieniami aktywacji roli</span><span class="sxs-lookup"><span data-stu-id="461e6-105">Manage the role activation settings</span></span>
1. <span data-ttu-id="461e6-106">Przejdź do [portalu Azure](https://portal.azure.com) i wybierz **Azure AD Privileged Identity Management** aplikacji z poziomu pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="461e6-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span></span>
2. <span data-ttu-id="461e6-107">Wybierz **Zarządzanie ról uprzywilejowanych** > **ustawienia** > **ról uprzywilejowanych**.</span><span class="sxs-lookup"><span data-stu-id="461e6-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="461e6-108">Wybierz rolę, którego ustawienia chcesz zarządzać.</span><span class="sxs-lookup"><span data-stu-id="461e6-108">Choose the role whose settings you want to manage.</span></span>

<span data-ttu-id="461e6-109">Na stronie Ustawienia dla każdej roli istnieje wiele ustawień, które można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="461e6-109">On the settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="461e6-110">Te ustawienia dotyczą tylko użytkownicy, którzy są kwalifikujących się Administratorzy, Administratorzy nie trwałych.</span><span class="sxs-lookup"><span data-stu-id="461e6-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="461e6-111">**Aktywacje**: czas, w godzinach, które roli pozostaje aktywne, przed jego wygaśnięciem.</span><span class="sxs-lookup"><span data-stu-id="461e6-111">**Activations**: The time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="461e6-112">Może to być w przedziale od 1 do 72 godzin.</span><span class="sxs-lookup"><span data-stu-id="461e6-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="461e6-113">**Powiadomienia**: można wybrać, czy system wysyła wiadomości e-mail do administratorów potwierdzenie ich uaktywniono rolę.</span><span class="sxs-lookup"><span data-stu-id="461e6-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span></span> <span data-ttu-id="461e6-114">Może to być przydatne do wykrywania nieautoryzowanego lub nielegalne aktywacji.</span><span class="sxs-lookup"><span data-stu-id="461e6-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="461e6-115">**Zdarzenie/żądania biletu**: można wybrać, czy należy wymagać Administratorzy kwalifikujących się do dołączenia numer biletu, gdy aktywują ich roli.</span><span class="sxs-lookup"><span data-stu-id="461e6-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span></span> <span data-ttu-id="461e6-116">Może to być przydatne podczas wykonywania inspekcji dostępu do roli.</span><span class="sxs-lookup"><span data-stu-id="461e6-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="461e6-117">**Uwierzytelnianie wieloskładnikowe**: można wybrać, czy należy wymagać od użytkowników zweryfikować swoją tożsamość za pomocą usługi MFA aktywować ich ról.</span><span class="sxs-lookup"><span data-stu-id="461e6-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="461e6-118">Mają można zweryfikować tego raz dla sesji, nie za każdym razem, gdy ich aktywowania roli.</span><span class="sxs-lookup"><span data-stu-id="461e6-118">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="461e6-119">Istnieją dwa porady należy wziąć pod uwagę podczas włączania uwierzytelniania Wieloskładnikowego:</span><span class="sxs-lookup"><span data-stu-id="461e6-119">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="461e6-120">Użytkownicy, którzy mają konta Microsoft do ich adresów e-mail (zazwyczaj @outlook.com, ale nie zawsze) nie można zarejestrować w usłudze Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="461e6-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="461e6-121">Jeśli chcesz przypisać role do użytkowników z kontami Microsoft, możesz były administratorów trwałych lub Wyłącz uwierzytelnianie wieloskładnikowe dla tej roli.</span><span class="sxs-lookup"><span data-stu-id="461e6-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="461e6-122">Nie można wyłączyć usługi MFA dla wysoko uprzywilejowane ról dla usługi Azure AD i usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="461e6-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="461e6-123">Jest to zabezpieczenie, ponieważ te role powinny być starannie chronione:</span><span class="sxs-lookup"><span data-stu-id="461e6-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="461e6-124">Administrator aplikacji</span><span class="sxs-lookup"><span data-stu-id="461e6-124">Application administrator</span></span>
  * <span data-ttu-id="461e6-125">Administrator serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="461e6-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="461e6-126">Administrator rozliczeń</span><span class="sxs-lookup"><span data-stu-id="461e6-126">Billing administrator</span></span>  
  * <span data-ttu-id="461e6-127">Administrator zgodności</span><span class="sxs-lookup"><span data-stu-id="461e6-127">Compliance administrator</span></span>  
  * <span data-ttu-id="461e6-128">Administrator programu CRM usługi</span><span class="sxs-lookup"><span data-stu-id="461e6-128">CRM service administrator</span></span>
  * <span data-ttu-id="461e6-129">Osoba zatwierdzająca dostępu skrytki klienta</span><span class="sxs-lookup"><span data-stu-id="461e6-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="461e6-130">Składnik zapisywania katalogu</span><span class="sxs-lookup"><span data-stu-id="461e6-130">Directory writer</span></span>  
  * <span data-ttu-id="461e6-131">Administrator programu Exchange</span><span class="sxs-lookup"><span data-stu-id="461e6-131">Exchange administrator</span></span>  
  * <span data-ttu-id="461e6-132">Administrator globalny</span><span class="sxs-lookup"><span data-stu-id="461e6-132">Global administrator</span></span>
  * <span data-ttu-id="461e6-133">Administrator usługi Intune</span><span class="sxs-lookup"><span data-stu-id="461e6-133">Intune service administrator</span></span>
  * <span data-ttu-id="461e6-134">Skrzynki pocztowej administratora</span><span class="sxs-lookup"><span data-stu-id="461e6-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="461e6-135">Obsługa tier1 partnera</span><span class="sxs-lookup"><span data-stu-id="461e6-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="461e6-136">Obsługa tier2 partnera</span><span class="sxs-lookup"><span data-stu-id="461e6-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="461e6-137">Administrator ról uprzywilejowanych</span><span class="sxs-lookup"><span data-stu-id="461e6-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="461e6-138">Administrator zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="461e6-138">Security administrator</span></span>  
  * <span data-ttu-id="461e6-139">Administrator programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="461e6-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="461e6-140">Administrator programu Skype dla firm</span><span class="sxs-lookup"><span data-stu-id="461e6-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="461e6-141">Administrator konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="461e6-141">User account administrator</span></span>  

<span data-ttu-id="461e6-142">Aby uzyskać więcej informacji na temat przy użyciu usługi MFA w usłudze PIM zobacz [sposobu wymagać uwierzytelniania MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="461e6-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="461e6-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="461e6-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

