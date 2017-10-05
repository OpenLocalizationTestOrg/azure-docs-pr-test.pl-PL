---
title: "Dostęp warunkowy usługi Azure Active Directory — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Odpowiedzi na często zadawane pytania dotyczące dostępu warunkowego w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: e9a5af41b08b593e4d97475f29da4e5fe8df7042
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="69cde-103">Dostęp warunkowy usługi Azure Active Directory — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="69cde-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="69cde-104">Aplikacje, które współpracuje z zasad dostępu warunkowego?</span><span class="sxs-lookup"><span data-stu-id="69cde-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="69cde-105">Aby uzyskać informacje o aplikacjach, które współpracują z zasadami dostępu warunkowego, zobacz [aplikacji i przeglądarki, które używały zasady dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="69cde-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="69cde-106">Zasady dostępu warunkowego są wymuszane dla współpracy B2B i gości?</span><span class="sxs-lookup"><span data-stu-id="69cde-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="69cde-107">Zasady są wymuszane dla biznesowych między firmami (B2B) współpracy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="69cde-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="69cde-108">Jednak w niektórych przypadkach użytkownik może nie umożliwiać spełnia wymagania zasad.</span><span class="sxs-lookup"><span data-stu-id="69cde-108">However, in some cases, a user might not be able to satisfy the policy requirements.</span></span> <span data-ttu-id="69cde-109">Na przykład organizacja użytkownika gościa mogą nie obsługiwać uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="69cde-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-to-onedrive-for-business"></a><span data-ttu-id="69cde-110">Czy zasady usługi SharePoint Online dotyczy również do usługi OneDrive dla firm?</span><span class="sxs-lookup"><span data-stu-id="69cde-110">Does a SharePoint Online policy also apply to OneDrive for Business?</span></span>

<span data-ttu-id="69cde-111">Tak.</span><span class="sxs-lookup"><span data-stu-id="69cde-111">Yes.</span></span> <span data-ttu-id="69cde-112">Zasady usługi SharePoint Online ma również zastosowanie do usługi OneDrive dla firm.</span><span class="sxs-lookup"><span data-stu-id="69cde-112">A SharePoint Online policy also applies to OneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="69cde-113">Dlaczego nie można ustawić zasad w aplikacjach klienckich, takich jak Word i Outlook?</span><span class="sxs-lookup"><span data-stu-id="69cde-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="69cde-114">Zasady dostępu warunkowego Ustawia wymagania dotyczące uzyskiwania dostępu do usługi.</span><span class="sxs-lookup"><span data-stu-id="69cde-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="69cde-115">Te funkcje są wprowadzane podczas uwierzytelniania do tej usługi.</span><span class="sxs-lookup"><span data-stu-id="69cde-115">It's enforced when authentication to that service occurs.</span></span> <span data-ttu-id="69cde-116">Nie ustawiono zasad bezpośrednio w aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="69cde-116">The policy is not set directly on a client application.</span></span> <span data-ttu-id="69cde-117">Zamiast tego jest stosowana, gdy klient wywołuje usługę.</span><span class="sxs-lookup"><span data-stu-id="69cde-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="69cde-118">Na przykład zasadami ustawionymi w usłudze SharePoint ma zastosowanie do klientów podczas wywoływania programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="69cde-118">For example, a policy set on SharePoint applies to clients calling SharePoint.</span></span> <span data-ttu-id="69cde-119">Zestaw na serwerze Exchange zasad dotyczy programu Outlook.</span><span class="sxs-lookup"><span data-stu-id="69cde-119">A policy set on Exchange applies to Outlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-to-service-accounts"></a><span data-ttu-id="69cde-120">Zasady dostępu warunkowego ma zastosowania do kont usług?</span><span class="sxs-lookup"><span data-stu-id="69cde-120">Does a conditional access policy apply to service accounts?</span></span>

<span data-ttu-id="69cde-121">Zasady dostępu warunkowego są stosowane do wszystkich kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="69cde-121">Conditional access policies apply to all user accounts.</span></span> <span data-ttu-id="69cde-122">Obejmuje to konta użytkowników, które są używane jako konta usługi.</span><span class="sxs-lookup"><span data-stu-id="69cde-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="69cde-123">Często konta usługi, który uruchamia instalacji nienadzorowanej nie może spełnić wymagań zasad dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="69cde-123">Often, a service account that runs unattended can't satisfy the requirements of a conditional access policy.</span></span> <span data-ttu-id="69cde-124">Na przykład uwierzytelnianie wieloskładnikowe może być wymagane.</span><span class="sxs-lookup"><span data-stu-id="69cde-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="69cde-125">Konta usług można wykluczyć z zasady przy użyciu ustawień zarządzania zasad dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="69cde-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="69cde-126">Interfejsy API Graph są dostępne do konfigurowania zasad dostępu warunkowego?</span><span class="sxs-lookup"><span data-stu-id="69cde-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="69cde-127">Aktualnie nie.</span><span class="sxs-lookup"><span data-stu-id="69cde-127">Currently, no.</span></span> 

## <a name="what-is-the-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="69cde-128">Co to jest domyślne zasady wykluczania dla platform nieobsługiwanego urządzenia?</span><span class="sxs-lookup"><span data-stu-id="69cde-128">What is the default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="69cde-129">Obecnie zasady dostępu warunkowego selektywnie są wymuszane dla użytkowników urządzeń iOS i Android.</span><span class="sxs-lookup"><span data-stu-id="69cde-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="69cde-130">Aplikacje na innych platformach urządzeń domyślnie nie dotyczy zasady dostępu warunkowego dla urządzeń iOS i Android.</span><span class="sxs-lookup"><span data-stu-id="69cde-130">Applications on other device platforms are, by default, not affected by the conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="69cde-131">Administrator dzierżawy możliwość zastąpienia globalnych zasad, aby uniemożliwić dostęp do użytkowników na platformach, które nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="69cde-131">A tenant admin can choose to override the global policy to disallow access to users on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="69cde-132">Jak działają zasady dostępu warunkowego dla Teams firmy Microsoft?</span><span class="sxs-lookup"><span data-stu-id="69cde-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="69cde-133">Microsoft Teams zależy od silnie usługi Exchange Online i SharePoint Online w podstawowe scenariusze wydajności, takich jak spotkania, kalendarzy i udostępnianie plików.</span><span class="sxs-lookup"><span data-stu-id="69cde-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="69cde-134">Zasady dostępu warunkowego, które są ustawione dla tych aplikacji w chmurze dotyczą Teams firmy Microsoft, gdy użytkownik zaloguje się.</span><span class="sxs-lookup"><span data-stu-id="69cde-134">Conditional access policies that are set for these cloud apps apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="69cde-135">Teams Microsoft również jest obsługiwane oddzielnie jako aplikacji w chmurze w usłudze Azure Active Directory zasady dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="69cde-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="69cde-136">Zasady urzędu certyfikatów, które są ustawione dla aplikacji w chmurze dotyczą Teams firmy Microsoft, gdy użytkownik zaloguje się.</span><span class="sxs-lookup"><span data-stu-id="69cde-136">Certificate authority policies that are set for a cloud app apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="69cde-137">Klienci usług pulpitu Teams firmy Microsoft dla systemu Windows i Mac obsługuje nowoczesnego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="69cde-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="69cde-138">Nowoczesne uwierzytelniane umożliwia logowanie oparte na Azure Active Directory Authentication Library (ADAL) dla aplikacji klienckich programu Microsoft Office na platformach.</span><span class="sxs-lookup"><span data-stu-id="69cde-138">Modern authentication brings sign-in based on the Azure Active Directory Authentication Library (ADAL) to Microsoft Office client applications across platforms.</span></span> 