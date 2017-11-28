---
title: "aaaDynamic grup i współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="addd6-103">Grupami dynamicznymi i współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="addd6-103">Dynamic groups and Azure Active Directory B2B collaboration</span></span>

## <a name="what-are-dynamic-groups"></a><span data-ttu-id="addd6-104">Co to są grupami dynamicznymi?</span><span class="sxs-lookup"><span data-stu-id="addd6-104">What are dynamic groups?</span></span>
<span data-ttu-id="addd6-105">Dynamicznej konfiguracji przynależności do grupy zabezpieczeń usługi Azure Active Directory (Azure AD) jest dostępna w [hello portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="addd6-105">Dynamic configuration of security group membership for Azure Active Directory (Azure AD) is available in [hello Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="addd6-106">Administratorzy mogą ustawiać zasady grupy toopopulate, które zostały utworzone w usłudze Azure Active Directory na podstawie atrybutów użytkownika (na przykład userType, działu lub kraju).</span><span class="sxs-lookup"><span data-stu-id="addd6-106">Administrators can set rules toopopulate groups that are created in Azure Active Directory based on user attributes (such as userType, department, or country).</span></span> <span data-ttu-id="addd6-107">Elementy Członkowskie mogą być automatycznie dodawane tooor usunięte z grupy zabezpieczeń na podstawie ich atrybutów.</span><span class="sxs-lookup"><span data-stu-id="addd6-107">Members can be automatically added tooor removed from a security group based on their attributes.</span></span> <span data-ttu-id="addd6-108">Te grupy może zapewnić dostęp do zasobów tooapplications lub w chmurze (witryny programu SharePoint, dokumenty) i tooassign licencje toomembers.</span><span class="sxs-lookup"><span data-stu-id="addd6-108">These groups can provide access tooapplications or cloud resources (SharePoint sites, documents) and tooassign licenses toomembers.</span></span> <span data-ttu-id="addd6-109">Przeczytaj więcej na temat grup dynamicznych w [grup w usłudze Azure Active Directory w wersji dedykowanej](active-directory-accessmanagement-dedicated-groups.md).</span><span class="sxs-lookup"><span data-stu-id="addd6-109">Read more about dynamic groups in [Dedicated groups in Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).</span></span>

<span data-ttu-id="addd6-110">Witaj odpowiednie [licencjonowania usługi Azure AD Premium P1 lub P2](https://azure.microsoft.com/pricing/details/active-directory/) jest wymagane toocreate i używania grup dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="addd6-110">hello appropriate [Azure AD Premium P1 or P2 licensing](https://azure.microsoft.com/pricing/details/active-directory/) is required toocreate and use dynamic groups.</span></span> <span data-ttu-id="addd6-111">Dowiedz się więcej informacji, zobacz artykuł hello [tworzenia reguł opartych na atrybutach dynamiczne członkostwo w grupie w usłudze Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="addd6-111">Learn more in hello article [Create attribute-based rules for dynamic group membership in Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

## <a name="what-are-hello-built-in-dynamic-groups"></a><span data-ttu-id="addd6-112">Co to są hello wbudowane grupy dynamiczne?</span><span class="sxs-lookup"><span data-stu-id="addd6-112">What are hello built-in dynamic groups?</span></span>
<span data-ttu-id="addd6-113">Witaj **wszyscy użytkownicy** grupa dynamiczna umożliwia toocreate Administratorzy dzierżawy kliknij zawierającego wszystkich użytkowników w dzierżawie powitalnych za pomocą jednej grupy.</span><span class="sxs-lookup"><span data-stu-id="addd6-113">hello **All users** dynamic group enables tenant admins toocreate a group containing all users in hello tenant with a single click.</span></span> <span data-ttu-id="addd6-114">Domyślnie program hello **wszyscy użytkownicy** grupy należą wszyscy użytkownicy w katalogu hello, w tym elementów członkowskich i gości.</span><span class="sxs-lookup"><span data-stu-id="addd6-114">By default, hello **All users** group includes all users in hello directory, including Members and Guests.</span></span>
<span data-ttu-id="addd6-115">Witaj nowego portalu administracyjnego usługi Azure Active Directory, można wybrać tooenable hello **wszyscy użytkownicy** w hello wyświetlić ustawienia grupy.</span><span class="sxs-lookup"><span data-stu-id="addd6-115">Within hello new Azure Active Directory admin portal, you can choose tooenable hello **All users** group in hello Group Settings view.</span></span>

![grupy wbudowane](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a><span data-ttu-id="addd6-117">Ograniczanie funkcjonalności hello wszystkich Dynamiczna grupa użytkowników</span><span class="sxs-lookup"><span data-stu-id="addd6-117">Hardening hello All users dynamic group</span></span>
<span data-ttu-id="addd6-118">Domyślnie program hello **wszyscy użytkownicy** grupa zawiera również użytkowników (Gość) współpracy B2B.</span><span class="sxs-lookup"><span data-stu-id="addd6-118">By default, hello **All users** group contains your B2B collaboration (guest) users as well.</span></span> <span data-ttu-id="addd6-119">Można dodatkowo zabezpieczyć Twoje **wszyscy użytkownicy** grupy przy użyciu reguły tooremove gości.</span><span class="sxs-lookup"><span data-stu-id="addd6-119">You can further secure your **All users** group by using a rule tooremove guest users.</span></span> <span data-ttu-id="addd6-120">Witaj poniższej ilustracji przedstawiono hello **wszyscy użytkownicy** modyfikacja grupy Goście tooexclude.</span><span class="sxs-lookup"><span data-stu-id="addd6-120">hello following illustration shows hello **All users** group modified tooexclude guests.</span></span>

![Włącz wszystkie grupy użytkowników](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

<span data-ttu-id="addd6-122">Można także znaleźć go przydatne toocreate nową grupę dynamicznych, zawierającą tylko gości, dzięki czemu można zastosować toothem zasad (np. zasady dostępu warunkowego AD Azure).</span><span class="sxs-lookup"><span data-stu-id="addd6-122">You might also find it useful toocreate a new dynamic group that contains only guest users, so that you can apply policies (such as Azure AD Conditional Access policies) toothem.</span></span>
<span data-ttu-id="addd6-123">Jakie takiej grupy może wyglądać tak:</span><span class="sxs-lookup"><span data-stu-id="addd6-123">What such a group might look like:</span></span>

![Wyklucz gości](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a><span data-ttu-id="addd6-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="addd6-125">Next steps</span></span>

<span data-ttu-id="addd6-126">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="addd6-126">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="addd6-127">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="addd6-127">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="addd6-128">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="addd6-128">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="addd6-129">Dodawanie roli tooa użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="addd6-129">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="addd6-130">Delegowanie zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="addd6-130">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="addd6-131">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="addd6-131">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="addd6-132">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="addd6-132">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="addd6-133">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="addd6-133">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="addd6-134">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="addd6-134">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="addd6-135">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="addd6-135">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="addd6-136">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="addd6-136">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
