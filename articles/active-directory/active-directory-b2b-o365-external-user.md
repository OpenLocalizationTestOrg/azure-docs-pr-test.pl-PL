---
title: "aaaOffice 365 udostępnianie zewnętrzne i współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="0dc90-103">Udostępnianie zewnętrzne usługi Office 365 i Azure Active Directory B2B współpracy</span><span class="sxs-lookup"><span data-stu-id="0dc90-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="0dc90-104">Zewnętrzne udostępnianie w usłudze Office 365 (OneDrive, SharePoint Online, Unified grup itp.) i B2B usługi Azure Active Directory (Azure AD) współpracy są technicznie hello sam element.</span><span class="sxs-lookup"><span data-stu-id="0dc90-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically hello same thing.</span></span> <span data-ttu-id="0dc90-105">Udostępnianie zewnętrzne wszystkich (oprócz OneDrive/usługi SharePoint Online), łącznie z gośćmi grupy usługi Office 365, używa już zaproszenia współpracy B2B usługi Azure AD hello interfejsów API do udostępniania.</span><span class="sxs-lookup"><span data-stu-id="0dc90-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses hello Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="0dc90-106">OneDrive/usługi SharePoint Online ma menedżera oddzielne zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="0dc90-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="0dc90-107">Obsługa udostępnianie zewnętrzne w usłudze OneDrive/SharePoint Online zostało uruchomione przed jego obsługę opracowany usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dc90-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="0dc90-108">Wraz z upływem czasu OneDrive/usługi SharePoint Online udostępnianie zewnętrzne uzyskano kilka funkcji i milionów użytkowników, którzy korzystają produktu hello obiektu w — zbudowany udostępnianie wzorzec.</span><span class="sxs-lookup"><span data-stu-id="0dc90-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use hello product's in-built sharing pattern.</span></span> <span data-ttu-id="0dc90-109">Istnieją pewne niewielkie różnice między jak OneDrive/usługi SharePoint Online udostępnianie zewnętrzne działa i jak działa współpracy B2B usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="0dc90-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="0dc90-110">OneDrive/usługi SharePoint Online dodaje katalog toohello użytkowników po użytkowników zostały zrealizowane zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="0dc90-110">OneDrive/SharePoint Online adds users toohello directory after users have redeemed their invitations.</span></span> <span data-ttu-id="0dc90-111">Dlatego przed realizacji, nie widzisz hello użytkownika w portalu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dc90-111">So, before redemption, you don't see hello user in Azure AD portal.</span></span> <span data-ttu-id="0dc90-112">Jeśli inna witryna zaprasza użytkownika w hello międzyczasie, generowany jest nowe zaproszenie.</span><span class="sxs-lookup"><span data-stu-id="0dc90-112">If another site invites a user in hello meantime, a new invitation is generated.</span></span> <span data-ttu-id="0dc90-113">Użycie współpracy B2B usługi Azure AD, użytkownicy zostaną jednak dodane bezpośrednio na zaproszenia, tak aby pokazywały się wszędzie.</span><span class="sxs-lookup"><span data-stu-id="0dc90-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="0dc90-114">środowisko realizacji Hello w usłudze OneDrive/usługi SharePoint Online wygląda inaczej niż hello środowisko współpracy B2B usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dc90-114">hello redemption experience in OneDrive/SharePoint Online looks different from hello experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="0dc90-115">Po użytkownika umarza zaproszenia, napotyka hello wyglądają podobnie.</span><span class="sxs-lookup"><span data-stu-id="0dc90-115">After a user redeems an invitation, hello experiences look alike.</span></span>

- <span data-ttu-id="0dc90-116">Azure AD B2B współpracy zaproszonych użytkowników mogą być pobierane z usługi OneDrive/usługi SharePoint Online udostępnianie okien dialogowych.</span><span class="sxs-lookup"><span data-stu-id="0dc90-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="0dc90-117">OneDrive/SharePoint Online zaproszonych użytkowników również wyświetlane w usłudze Azure AD po ich zrealizować zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="0dc90-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="0dc90-118">toomanage zewnętrznych udostępnianie współpracy B2B usługi Azure AD w usłudze OneDrive/SharePoint Online, ustaw hello OneDrive/usługi SharePoint Online będzie zewnętrznych udostępnianie ustawienie zbyt**Zezwalaj tylko na udostępniania użytkownikom zewnętrznym już w katalogu hello**.</span><span class="sxs-lookup"><span data-stu-id="0dc90-118">toomanage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set hello OneDrive/SharePoint Online external sharing setting too**Only allow sharing with external users already in hello directory**.</span></span> <span data-ttu-id="0dc90-119">Dla użytkowników tooexternally udostępnione Lokacje i pobranie z zewnętrznym współpracownikom, które hello admin został dodany.</span><span class="sxs-lookup"><span data-stu-id="0dc90-119">Users can go tooexternally shared sites and pick from external collaborators that hello admin has added.</span></span> <span data-ttu-id="0dc90-120">Witaj, Administratorze można dodać hello zewnętrznych współpracowników za pośrednictwem hello zaproszenia współpracy B2B interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="0dc90-120">hello admin can add hello external collaborators through hello B2B collaboration invitation APIs.</span></span>

![Witaj OneDrive/usługi SharePoint Online zewnętrznego współużytkuje](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="0dc90-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0dc90-122">Next steps</span></span>

<span data-ttu-id="0dc90-123">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="0dc90-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="0dc90-124">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="0dc90-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="0dc90-125">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0dc90-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="0dc90-126">Dodawanie roli tooa użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0dc90-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="0dc90-127">Delegowanie zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0dc90-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="0dc90-128">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0dc90-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="0dc90-129">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="0dc90-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="0dc90-130">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0dc90-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="0dc90-131">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0dc90-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="0dc90-132">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="0dc90-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="0dc90-133">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0dc90-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
