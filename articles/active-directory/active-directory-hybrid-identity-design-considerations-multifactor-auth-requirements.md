---
title: "Azure Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących uwierzytelniania wieloskładnikowego"
description: "Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza określonych warunków, można wybrać podczas uwierzytelniania użytkownika i przed zezwoleniem na dostęp do aplikacji. Gdy te warunki są spełnione, użytkownik jest uwierzytelniony i zezwolenie na dostęp do aplikacji."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 5b3a8ce6e4203dfb3700f324e32687dd910118af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="871a4-104">Określić wymagania dotyczące rozwiązania z tożsamością hybrydową uwierzytelniania wieloskładnikowego</span><span class="sxs-lookup"><span data-stu-id="871a4-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="871a4-105">W tym świecie mobilności użytkownikom uzyskiwanie dostępu do danych i aplikacji w chmurze i na dowolnym urządzeniu zabezpieczanie informacji stał się podstawowym.</span><span class="sxs-lookup"><span data-stu-id="871a4-105">In this world of mobility, with users accessing data and applications in the cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="871a4-106">Codziennie jest nowy nagłówek o naruszenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="871a4-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="871a4-107">Mimo że nie ma żadnej gwarancji przed takie naruszenia, uwierzytelnianie wieloskładnikowe, zapewnia dodatkową warstwę zabezpieczeń, aby uniknąć tych naruszeń.</span><span class="sxs-lookup"><span data-stu-id="871a4-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security to help prevent these breaches.</span></span>
<span data-ttu-id="871a4-108">Rozpocznij od Trwa szacowanie wymagań organizacji w usłudze Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="871a4-108">Start by evaluating the organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="871a4-109">Oznacza to co jest organizacji próby zabezpieczenia.</span><span class="sxs-lookup"><span data-stu-id="871a4-109">That is, what is the organization trying to secure.</span></span>  <span data-ttu-id="871a4-110">Ocena ważne jest, aby zdefiniować wymagania techniczne dotyczące konfigurowania i umożliwienie użytkownikom organizacji uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="871a4-110">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="871a4-111">Jeśli nie masz doświadczenia z usługami MFA i jakie operacje, zdecydowanie zaleca się przeczytanie artykułu [co to jest usługa Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) przed kontynuować odczytu w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="871a4-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read the article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior to continue reading this section.</span></span>
> 
> 

<span data-ttu-id="871a4-112">Upewnij się, że odpowiedzi na następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="871a4-112">Make sure to answer the following:</span></span>

* <span data-ttu-id="871a4-113">Firma chce do zabezpieczania aplikacji firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="871a4-113">Is your company trying to secure Microsoft apps?</span></span> 
* <span data-ttu-id="871a4-114">Jak te aplikacje są publikowane?</span><span class="sxs-lookup"><span data-stu-id="871a4-114">How these apps are published?</span></span>
* <span data-ttu-id="871a4-115">Firma zapewnia dostępu zdalnego, aby umożliwić pracownikom dostęp do lokalnych aplikacji?</span><span class="sxs-lookup"><span data-stu-id="871a4-115">Does your company provide remote access to allow employees to access on-premises apps?</span></span>

<span data-ttu-id="871a4-116">Jeśli tak, jakiego typu dostępu zdalnego? Należy również ocenić, gdzie zostaną umieszczone użytkowników, którzy uzyskują dostęp do tych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="871a4-116">If yes, what type of remote access?You also need to evaluate where the users who are accessing these applications will be located.</span></span> <span data-ttu-id="871a4-117">Tej oceny jest innym ważnym krokiem do definiowania strategii odpowiednie uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="871a4-117">This evaluation is another important step to define the proper multi-factor authentication strategy.</span></span> <span data-ttu-id="871a4-118">Upewnij się, że należy odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="871a4-118">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="871a4-119">Gdzie użytkownicy będą znajdować się?</span><span class="sxs-lookup"><span data-stu-id="871a4-119">Where are the users going to be located?</span></span>
* <span data-ttu-id="871a4-120">Mogą one znajdować się w dowolnym?</span><span class="sxs-lookup"><span data-stu-id="871a4-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="871a4-121">Czy firma chce nawiązać ograniczenia zgodnie z lokalizacją użytkownika?</span><span class="sxs-lookup"><span data-stu-id="871a4-121">Does your company want to establish restrictions according to the user’s location?</span></span>

<span data-ttu-id="871a4-122">Po zrozumieniu wymagań, należy również ocenić wymagań użytkownika usługi Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="871a4-122">Once you understand these requirements, it is important to also evaluate the user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="871a4-123">Tej oceny jest ważne, ponieważ będzie definiował wymagania dotyczące wdrażania usługi Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="871a4-123">This evaluation is important because it will define the requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="871a4-124">Upewnij się, że należy odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="871a4-124">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="871a4-125">Znasz użytkowników usługi Multi-Factor authentication?</span><span class="sxs-lookup"><span data-stu-id="871a4-125">Are the users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="871a4-126">Niektóre zastosowania będą wymagane w celu zapewnienia dodatkowego uwierzytelniania?</span><span class="sxs-lookup"><span data-stu-id="871a4-126">Will some uses be required to provide additional authentication?</span></span>  
  * <span data-ttu-id="871a4-127">Jeśli tak, zawsze, gdy pochodzących z sieci zewnętrznych lub podczas uzyskiwania dostępu do określonych aplikacji lub w innych warunkach?</span><span class="sxs-lookup"><span data-stu-id="871a4-127">If yes, all the time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="871a4-128">Użytkownicy wymaga szkolenia dotyczące sposobu instalacji i zaimplementować uwierzytelnianie wieloskładnikowe?</span><span class="sxs-lookup"><span data-stu-id="871a4-128">Will the users require training on how to setup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="871a4-129">Jakie są najważniejsze scenariusze, które firma chce włączyć uwierzytelnianie wieloskładnikowe dla użytkowników?</span><span class="sxs-lookup"><span data-stu-id="871a4-129">What are the key scenarios that your company wants to enable multi-factor authentication for their users?</span></span>

<span data-ttu-id="871a4-130">Po odpowiedzi na pytania Wstecz, można określić, czy istnieją już zaimplementowany uwierzytelnianie wieloskładnikowe lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="871a4-130">After answering the previous questions, you will be able to understand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="871a4-131">Ocena ważne jest, aby zdefiniować wymagania techniczne dotyczące konfigurowania i umożliwienie użytkownikom organizacji uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="871a4-131">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span> <span data-ttu-id="871a4-132">Upewnij się, że należy odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="871a4-132">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="871a4-133">Czy firma musi ochronę uprzywilejowanych kont za pomocą usługi MFA?</span><span class="sxs-lookup"><span data-stu-id="871a4-133">Does your company need to protect privileged accounts with MFA?</span></span>
* <span data-ttu-id="871a4-134">Czy firma musi włączyć uwierzytelnianie wieloskładnikowe dla niektórych aplikacji dla zachowania zgodności?</span><span class="sxs-lookup"><span data-stu-id="871a4-134">Does your company need to enable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="871a4-135">Czy firma musi włączyć uwierzytelnianie wieloskładnikowe dla wszystkich kwalifikujących się użytkowników z tych aplikacji lub tylko administratorzy?</span><span class="sxs-lookup"><span data-stu-id="871a4-135">Does your company need to enable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="871a4-136">Czy konieczne jest zawsze włączone uwierzytelnianie MFA lub tylko, gdy użytkownicy są zalogowani poza siecią firmową?</span><span class="sxs-lookup"><span data-stu-id="871a4-136">Do you need have MFA always enabled or only when the users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="871a4-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="871a4-137">Next steps</span></span>
[<span data-ttu-id="871a4-138">Definiowanie strategii wdrażania tożsamości hybrydowej</span><span class="sxs-lookup"><span data-stu-id="871a4-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="871a4-139">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="871a4-139">See also</span></span>
[<span data-ttu-id="871a4-140">Omówienie zagadnień dotyczących projektowania</span><span class="sxs-lookup"><span data-stu-id="871a4-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

