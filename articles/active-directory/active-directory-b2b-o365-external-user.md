---
title: "Udostępnianie zewnętrzne usługi Office 365 i Azure Active Directory B2B współpracy | Dokumentacja firmy Microsoft"
description: "mapowanie odwołania do usługi Azure Active Directory B2B współpracy oświadczeń"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: cad0ce8f745f3d6ca14436fd714b08c60de0e459
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="6d10c-103">Udostępnianie zewnętrzne usługi Office 365 i Azure Active Directory B2B współpracy</span><span class="sxs-lookup"><span data-stu-id="6d10c-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="6d10c-104">Zewnętrzne udostępnianie w usłudze Office 365 (OneDrive, SharePoint Online, Unified grup itp.) i współpracy B2B usługi Azure Active Directory (Azure AD) są pod względem technicznym to samo.</span><span class="sxs-lookup"><span data-stu-id="6d10c-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically the same thing.</span></span> <span data-ttu-id="6d10c-105">Udostępnianie zewnętrzne wszystkich (oprócz OneDrive/usługi SharePoint Online), łącznie z gośćmi grupy usługi Office 365, używa już zaproszenia współpracy B2B usługi Azure AD interfejsów API do udostępniania.</span><span class="sxs-lookup"><span data-stu-id="6d10c-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="6d10c-106">OneDrive/usługi SharePoint Online ma menedżera oddzielne zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="6d10c-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="6d10c-107">Obsługa udostępnianie zewnętrzne w usłudze OneDrive/SharePoint Online zostało uruchomione przed jego obsługę opracowany usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d10c-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="6d10c-108">Wraz z upływem czasu OneDrive/usługi SharePoint Online udostępnianie zewnętrzne uzyskano kilka funkcji i milionów użytkowników, którzy korzystają z produktu obiektu w zbudowany udostępnianie wzorzec.</span><span class="sxs-lookup"><span data-stu-id="6d10c-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span></span> <span data-ttu-id="6d10c-109">Istnieją pewne niewielkie różnice między jak OneDrive/usługi SharePoint Online udostępnianie zewnętrzne działa i jak działa współpracy B2B usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="6d10c-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="6d10c-110">OneDrive/usługi SharePoint Online dodaje użytkowników do katalogu po użytkowników zostały zrealizowane zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="6d10c-110">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span></span> <span data-ttu-id="6d10c-111">Dlatego przed realizacji, nie widzisz użytkownika w portalu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d10c-111">So, before redemption, you don't see the user in Azure AD portal.</span></span> <span data-ttu-id="6d10c-112">Jeśli inna witryna zaprasza użytkownika w tym samym czasie, generowany jest nowe zaproszenie.</span><span class="sxs-lookup"><span data-stu-id="6d10c-112">If another site invites a user in the meantime, a new invitation is generated.</span></span> <span data-ttu-id="6d10c-113">Użycie współpracy B2B usługi Azure AD, użytkownicy zostaną jednak dodane bezpośrednio na zaproszenia, tak aby pokazywały się wszędzie.</span><span class="sxs-lookup"><span data-stu-id="6d10c-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="6d10c-114">Środowisko realizacji OneDrive/usługi SharePoint Online wygląda inaczej niż środowisko współpracy B2B usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d10c-114">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="6d10c-115">Po użytkownika umarza zaproszenia, procesy wyglądają podobnie.</span><span class="sxs-lookup"><span data-stu-id="6d10c-115">After a user redeems an invitation, the experiences look alike.</span></span>

- <span data-ttu-id="6d10c-116">Azure AD B2B współpracy zaproszonych użytkowników mogą być pobierane z usługi OneDrive/usługi SharePoint Online udostępnianie okien dialogowych.</span><span class="sxs-lookup"><span data-stu-id="6d10c-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="6d10c-117">OneDrive/SharePoint Online zaproszonych użytkowników również wyświetlane w usłudze Azure AD po ich zrealizować zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="6d10c-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="6d10c-118">Aby zarządzać udostępnianie zewnętrzne w usłudze OneDrive/SharePoint Online z współpracy B2B usługi Azure AD, ustaw OneDrive/SharePoint Online zewnętrznego udostępnianie ustawienie, aby **Zezwalaj tylko na udostępniania użytkownikom zewnętrznym już w katalogu**.</span><span class="sxs-lookup"><span data-stu-id="6d10c-118">To manage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span></span> <span data-ttu-id="6d10c-119">Użytkownicy mogą przejdź do witryny zewnętrznie udostępnione i wybierz z zewnętrznym współpracownikom, dodane przez administratora.</span><span class="sxs-lookup"><span data-stu-id="6d10c-119">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span></span> <span data-ttu-id="6d10c-120">Administrator może dodać zewnętrznych współpracowników za pośrednictwem interfejsów API zaproszenia współpracy B2B.</span><span class="sxs-lookup"><span data-stu-id="6d10c-120">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span></span>

![OneDrive/SharePoint Online zewnętrznego współużytkuje](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="6d10c-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d10c-122">Next steps</span></span>

<span data-ttu-id="6d10c-123">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="6d10c-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="6d10c-124">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="6d10c-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="6d10c-125">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="6d10c-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="6d10c-126">Dodawanie do roli użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="6d10c-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="6d10c-127">Delegowanie zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="6d10c-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="6d10c-128">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="6d10c-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="6d10c-129">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d10c-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="6d10c-130">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="6d10c-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="6d10c-131">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="6d10c-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="6d10c-132">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="6d10c-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="6d10c-133">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="6d10c-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
