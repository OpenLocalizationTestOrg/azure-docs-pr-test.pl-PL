---
title: "Grupami dynamicznymi i współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "Azure współpracy B2B usługi Active Directory mogą być używane z grupami dynamicznymi w usłudze Azure AD"
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: 5818c41610c8c5df89abcb0dcd058bcbe9579ce7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="90cd8-103">Grupami dynamicznymi i współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="90cd8-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="90cd8-104">Co to są grupami dynamicznymi?</span><span class="sxs-lookup"><span data-stu-id="90cd8-104">What are dynamic groups?</span></span>
<span data-ttu-id="90cd8-105">Dynamicznej konfiguracji przynależności do grupy zabezpieczeń usługi Azure Active Directory (Azure AD) jest dostępna w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="90cd8-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [the Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="90cd8-106">Administratorzy mogą ustawić reguły do wypełniania grupy, które są tworzone w usłudze Azure Active Directory na podstawie atrybutów użytkownika (na przykład userType, działu lub kraju).</span><span class="sxs-lookup"><span data-stu-id="90cd8-106">Administrators can set rules to populate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="90cd8-107">Automatycznie dodawane do elementów członkowskich lub usunięte z grupy zabezpieczeń na podstawie ich atrybutów.</span><span class="sxs-lookup"><span data-stu-id="90cd8-107">Members can be automatically added to or removed from a security group based on their attributes.</span></span> <span data-ttu-id="90cd8-108">Te grupy mogą umożliwiać dostęp do aplikacji lub zasobów w chmurze (witryny programu SharePoint, dokumenty) i przypisywanie licencji do elementów członkowskich.</span><span class="sxs-lookup"><span data-stu-id="90cd8-108">These groups can provide access to applications or cloud resources (SharePoint sites, documents) and to assign licenses to members.</span></span> <span data-ttu-id="90cd8-109">Przeczytaj więcej na temat grup dynamicznych w [grup w usłudze Azure Active Directory w wersji dedykowanej](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="90cd8-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="90cd8-110">Odpowiednie [licencjonowania usługi Azure AD Premium P1 lub P2](https://azure.microsoft.com/pricing/details/active-directory/) jest wymagany do tworzenia i używania grup dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="90cd8-110">The appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required to create and use dynamic groups.</span></span> <span data-ttu-id="90cd8-111">Dowiedz się więcej informacji, zobacz artykuł [tworzenia reguł opartych na atrybutach dynamiczne członkostwo w grupie w usłudze Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="90cd8-111">Learn more in the article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-the-built-in-dynamic-groups"></a><span data-ttu-id="90cd8-112">Co to są wbudowane grupy dynamiczne?</span><span class="sxs-lookup"><span data-stu-id="90cd8-112">What are the built-in dynamic groups?</span></span>
<span data-ttu-id="90cd8-113">**Wszyscy użytkownicy** Dynamiczna grupa umożliwia administratorom dzierżawy utworzenie grupy zawierającej wszystkich użytkowników w dzierżawie za pomocą jednego kliknięcia.</span><span class="sxs-lookup"><span data-stu-id="90cd8-113">The **All users** dynamic group enables tenant admins to create a group containing all users in the tenant with a single click.</span></span> <span data-ttu-id="90cd8-114">Domyślnie **wszyscy użytkownicy** grupy należą wszyscy użytkownicy w katalogu, w tym elementów członkowskich i gości.</span><span class="sxs-lookup"><span data-stu-id="90cd8-114">By default, the **All users** group includes all users in the directory, including Members and Guests.</span></span>
<span data-ttu-id="90cd8-115">W ramach nowego portalu administracyjnego usługi Azure Active Directory, możesz włączyć **wszyscy użytkownicy** w widoku ustawienia grupy.</span><span class="sxs-lookup"><span data-stu-id="90cd8-115">Within the new Azure Active Directory admin portal, you can choose to enable the **All users** group in the Group Settings view.</span></span>

![grupy wbudowane](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-the-all-users-dynamic-group"></a><span data-ttu-id="90cd8-117">Ograniczenie funkcjonalności wszystkich Dynamiczna grupa użytkowników</span><span class="sxs-lookup"><span data-stu-id="90cd8-117">Hardening the All users dynamic group</span></span>
<span data-ttu-id="90cd8-118">Domyślnie **wszyscy użytkownicy** grupa zawiera również użytkowników (Gość) współpracy B2B.</span><span class="sxs-lookup"><span data-stu-id="90cd8-118">By default, the **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="90cd8-119">Można dodatkowo zabezpieczyć Twoje **wszyscy użytkownicy** grupy przy użyciu reguły, aby usunąć gości.</span><span class="sxs-lookup"><span data-stu-id="90cd8-119">You can further secure your **All users** group by using a rule to remove guest users.</span></span> <span data-ttu-id="90cd8-120">Na poniższej ilustracji pokazano **wszyscy użytkownicy** grupy zmodyfikowane w celu wykluczenia gości.</span><span class="sxs-lookup"><span data-stu-id="90cd8-120">The following illustration shows the **All users** group modified to exclude guests.</span></span>

![Włącz wszystkie grupy użytkowników](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="90cd8-122">Użytkownik może być również bardzo przydatne do tworzenia nowej grupy dynamicznej, zawierający tylko gości, dzięki czemu można zastosować zasad (np. zasady dostępu warunkowego AD Azure) do nich.</span><span class="sxs-lookup"><span data-stu-id="90cd8-122">You might also find it useful to create a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) to them.</span></span>
<span data-ttu-id="90cd8-123">Jakie takiej grupy może wyglądać tak:</span><span class="sxs-lookup"><span data-stu-id="90cd8-123">What such a group might look like:</span></span>

![Wyklucz gości](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="90cd8-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90cd8-125">Next steps</span></span>

<span data-ttu-id="90cd8-126">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="90cd8-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="90cd8-127">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="90cd8-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="90cd8-128">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="90cd8-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="90cd8-129">Dodawanie do roli użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="90cd8-129">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="90cd8-130">Delegowanie zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="90cd8-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="90cd8-131">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="90cd8-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="90cd8-132">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="90cd8-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="90cd8-133">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="90cd8-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="90cd8-134">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="90cd8-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="90cd8-135">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="90cd8-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="90cd8-136">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="90cd8-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
