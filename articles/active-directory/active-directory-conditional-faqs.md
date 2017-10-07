---
title: "aaaAzure dostępu warunkowego w usłudze Active Directory — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi toofrequently zadawane pytania dotyczące dostępu warunkowego w usłudze Azure Active Directory."
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
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="92395-103">Dostęp warunkowy usługi Azure Active Directory — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="92395-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="92395-104">Aplikacje, które współpracuje z zasad dostępu warunkowego?</span><span class="sxs-lookup"><span data-stu-id="92395-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="92395-105">Aby uzyskać informacje o aplikacjach, które współpracują z zasadami dostępu warunkowego, zobacz [aplikacji i przeglądarki, które używały zasady dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="92395-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="92395-106">Zasady dostępu warunkowego są wymuszane dla współpracy B2B i gości?</span><span class="sxs-lookup"><span data-stu-id="92395-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="92395-107">Zasady są wymuszane dla biznesowych między firmami (B2B) współpracy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="92395-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="92395-108">Jednak w niektórych przypadkach użytkownik nie może być wymagań zasad hello toosatisfy stanie.</span><span class="sxs-lookup"><span data-stu-id="92395-108">However, in some cases, a user might not be able toosatisfy hello policy requirements.</span></span> <span data-ttu-id="92395-109">Na przykład organizacja użytkownika gościa mogą nie obsługiwać uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="92395-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a><span data-ttu-id="92395-110">Zasady usługi SharePoint Online również dotyczy tooOneDrive dla firm?</span><span class="sxs-lookup"><span data-stu-id="92395-110">Does a SharePoint Online policy also apply tooOneDrive for Business?</span></span>

<span data-ttu-id="92395-111">Tak.</span><span class="sxs-lookup"><span data-stu-id="92395-111">Yes.</span></span> <span data-ttu-id="92395-112">Zasady usługi SharePoint Online ma również zastosowanie tooOneDrive dla firm.</span><span class="sxs-lookup"><span data-stu-id="92395-112">A SharePoint Online policy also applies tooOneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="92395-113">Dlaczego nie można ustawić zasad w aplikacjach klienckich, takich jak Word i Outlook?</span><span class="sxs-lookup"><span data-stu-id="92395-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="92395-114">Zasady dostępu warunkowego Ustawia wymagania dotyczące uzyskiwania dostępu do usługi.</span><span class="sxs-lookup"><span data-stu-id="92395-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="92395-115">Te funkcje są wprowadzane podczas uwierzytelniania toothat usługi.</span><span class="sxs-lookup"><span data-stu-id="92395-115">It's enforced when authentication toothat service occurs.</span></span> <span data-ttu-id="92395-116">Nie ustawiono zasad Hello bezpośrednio w aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="92395-116">hello policy is not set directly on a client application.</span></span> <span data-ttu-id="92395-117">Zamiast tego jest stosowana, gdy klient wywołuje usługę.</span><span class="sxs-lookup"><span data-stu-id="92395-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="92395-118">Na przykład zasadami ustawionymi w usłudze SharePoint dotyczy tooclients wywoływania programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="92395-118">For example, a policy set on SharePoint applies tooclients calling SharePoint.</span></span> <span data-ttu-id="92395-119">Zestaw na serwerze Exchange zasad dotyczy tooOutlook.</span><span class="sxs-lookup"><span data-stu-id="92395-119">A policy set on Exchange applies tooOutlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a><span data-ttu-id="92395-120">Zasady dostępu warunkowego dotyczy tooservice kont?</span><span class="sxs-lookup"><span data-stu-id="92395-120">Does a conditional access policy apply tooservice accounts?</span></span>

<span data-ttu-id="92395-121">Zasady dostępu warunkowego są stosowane tooall kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="92395-121">Conditional access policies apply tooall user accounts.</span></span> <span data-ttu-id="92395-122">Obejmuje to konta użytkowników, które są używane jako konta usługi.</span><span class="sxs-lookup"><span data-stu-id="92395-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="92395-123">Często konta usługi, który uruchamia instalacji nienadzorowanej nie spełnia wymagania hello zasady dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="92395-123">Often, a service account that runs unattended can't satisfy hello requirements of a conditional access policy.</span></span> <span data-ttu-id="92395-124">Na przykład uwierzytelnianie wieloskładnikowe może być wymagane.</span><span class="sxs-lookup"><span data-stu-id="92395-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="92395-125">Konta usług można wykluczyć z zasady przy użyciu ustawień zarządzania zasad dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="92395-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="92395-126">Interfejsy API Graph są dostępne do konfigurowania zasad dostępu warunkowego?</span><span class="sxs-lookup"><span data-stu-id="92395-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="92395-127">Aktualnie nie.</span><span class="sxs-lookup"><span data-stu-id="92395-127">Currently, no.</span></span> 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="92395-128">Co to jest hello domyślne wykluczenia zasady dla platform nieobsługiwanego urządzenia?</span><span class="sxs-lookup"><span data-stu-id="92395-128">What is hello default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="92395-129">Obecnie zasady dostępu warunkowego selektywnie są wymuszane dla użytkowników urządzeń iOS i Android.</span><span class="sxs-lookup"><span data-stu-id="92395-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="92395-130">Aplikacje na innych platformach urządzeń domyślnie nie dotyczy hello zasady dostępu warunkowego dla urządzeń iOS i Android.</span><span class="sxs-lookup"><span data-stu-id="92395-130">Applications on other device platforms are, by default, not affected by hello conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="92395-131">Administrator dzierżawy można wybrać toooverride hello globalne zasady toodisallow dostępu toousers na platformach, które nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="92395-131">A tenant admin can choose toooverride hello global policy toodisallow access toousers on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="92395-132">Jak działają zasady dostępu warunkowego dla Teams firmy Microsoft?</span><span class="sxs-lookup"><span data-stu-id="92395-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="92395-133">Microsoft Teams zależy od silnie usługi Exchange Online i SharePoint Online w podstawowe scenariusze wydajności, takich jak spotkania, kalendarzy i udostępnianie plików.</span><span class="sxs-lookup"><span data-stu-id="92395-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="92395-134">Zasady dostępu warunkowego, które są ustawione dla tych aplikacji w chmurze zastosować tooMicrosoft zespołów po zalogowaniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92395-134">Conditional access policies that are set for these cloud apps apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="92395-135">Teams Microsoft również jest obsługiwane oddzielnie jako aplikacji w chmurze w usłudze Azure Active Directory zasady dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="92395-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="92395-136">Zasady urzędu certyfikatów, które są ustawione dla aplikacji w chmurze zastosować tooMicrosoft zespołów po zalogowaniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92395-136">Certificate authority policies that are set for a cloud app apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="92395-137">Klienci usług pulpitu Teams firmy Microsoft dla systemu Windows i Mac obsługuje nowoczesnego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="92395-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="92395-138">Nowoczesne uwierzytelniane umożliwia logowanie oparte na aplikacje klienckie pakietu Office tooMicrosoft interfejsów Azure Active Directory Authentication Library (ADAL) hello na platformach.</span><span class="sxs-lookup"><span data-stu-id="92395-138">Modern authentication brings sign-in based on hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office client applications across platforms.</span></span> 
