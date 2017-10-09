---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących uwierzytelniania wieloskładnikowego"
description: "Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza hello określonych warunków, można wybrać podczas uwierzytelniania użytkownika hello i przed zezwoleniem na dostęp toohello aplikacji. Gdy te warunki są spełnione, użytkownik hello uwierzytelniony i dozwolone dostępu toohello aplikacji."
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
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="90305-104">Określić wymagania dotyczące rozwiązania z tożsamością hybrydową uwierzytelniania wieloskładnikowego</span><span class="sxs-lookup"><span data-stu-id="90305-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="90305-105">W tym świecie mobilności użytkownikom uzyskiwanie dostępu do danych i aplikacji w chmurze hello i na dowolnym urządzeniu zabezpieczanie informacji stał się podstawowym.</span><span class="sxs-lookup"><span data-stu-id="90305-105">In this world of mobility, with users accessing data and applications in hello cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="90305-106">Codziennie jest nowy nagłówek o naruszenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="90305-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="90305-107">Mimo że nie ma żadnej gwarancji przed takie naruszenia, uwierzytelnianie wieloskładnikowe, zapewnia dodatkową warstwę zabezpieczeń toohelp zapobiec tych naruszeń.</span><span class="sxs-lookup"><span data-stu-id="90305-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security toohelp prevent these breaches.</span></span>
<span data-ttu-id="90305-108">Rozpocznij od Trwa szacowanie wymagań organizacji hello uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="90305-108">Start by evaluating hello organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="90305-109">Co to jest toosecure w trakcie hello organizacji.</span><span class="sxs-lookup"><span data-stu-id="90305-109">That is, what is hello organization trying toosecure.</span></span>  <span data-ttu-id="90305-110">Tej oceny jest ważne toodefine hello wymagania techniczne dotyczące konfigurowania i umożliwienie użytkownikom organizacje hello uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="90305-110">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="90305-111">Jeśli nie masz doświadczenia z usługami MFA i jakie operacje, zdecydowanie zaleca się przeczytanie artykułu hello [co to jest usługa Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) toocontinue przed przeczytaniem tej części.</span><span class="sxs-lookup"><span data-stu-id="90305-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read hello article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior toocontinue reading this section.</span></span>
> 
> 

<span data-ttu-id="90305-112">Upewnij się, że tooanswer hello następujące:</span><span class="sxs-lookup"><span data-stu-id="90305-112">Make sure tooanswer hello following:</span></span>

* <span data-ttu-id="90305-113">Firma chce toosecure aplikacji firmy Microsoft?</span><span class="sxs-lookup"><span data-stu-id="90305-113">Is your company trying toosecure Microsoft apps?</span></span> 
* <span data-ttu-id="90305-114">Jak te aplikacje są publikowane?</span><span class="sxs-lookup"><span data-stu-id="90305-114">How these apps are published?</span></span>
* <span data-ttu-id="90305-115">Firma oferuje dostępu zdalnego tooallow pracowników tooaccess lokalnej aplikacji?</span><span class="sxs-lookup"><span data-stu-id="90305-115">Does your company provide remote access tooallow employees tooaccess on-premises apps?</span></span>

<span data-ttu-id="90305-116">Jeśli tak, jakiego typu dostępu zdalnego? Należy również tooevaluate, w której zostaną umieszczone hello użytkowników, którzy uzyskują dostęp do tych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="90305-116">If yes, what type of remote access?You also need tooevaluate where hello users who are accessing these applications will be located.</span></span> <span data-ttu-id="90305-117">Tej oceny jest kolejną strategią odpowiednie uwierzytelnianie wieloskładnikowe, ważnym krokiem toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="90305-117">This evaluation is another important step toodefine hello proper multi-factor authentication strategy.</span></span> <span data-ttu-id="90305-118">Upewnij się, że hello tooanswer następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="90305-118">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="90305-119">Gdzie znajdują się użytkownicy hello przechodzi toobe?</span><span class="sxs-lookup"><span data-stu-id="90305-119">Where are hello users going toobe located?</span></span>
* <span data-ttu-id="90305-120">Mogą one znajdować się w dowolnym?</span><span class="sxs-lookup"><span data-stu-id="90305-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="90305-121">Czy firma chce ograniczenia tooestablish zgodnie z lokalizacją użytkownika toohello?</span><span class="sxs-lookup"><span data-stu-id="90305-121">Does your company want tooestablish restrictions according toohello user’s location?</span></span>

<span data-ttu-id="90305-122">Po zrozumieniu wymagań, ważne jest tooalso oceny wymagań dotyczących hello użytkownika usługi Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="90305-122">Once you understand these requirements, it is important tooalso evaluate hello user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="90305-123">Tej oceny jest ważne, ponieważ będzie definiował hello wymagania dotyczące wdrażania usługi Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="90305-123">This evaluation is important because it will define hello requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="90305-124">Upewnij się, że hello tooanswer następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="90305-124">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="90305-125">Znasz hello użytkowników usługi Multi-Factor authentication?</span><span class="sxs-lookup"><span data-stu-id="90305-125">Are hello users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="90305-126">Niektóre zastosowania będzie tooprovide wymagane dodatkowe uwierzytelnianie?</span><span class="sxs-lookup"><span data-stu-id="90305-126">Will some uses be required tooprovide additional authentication?</span></span>  
  * <span data-ttu-id="90305-127">Jeśli tak, wszystkie hello czas, po wznowieniu z sieci zewnętrznych lub podczas uzyskiwania dostępu do określonych aplikacji lub w innych warunkach?</span><span class="sxs-lookup"><span data-stu-id="90305-127">If yes, all hello time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="90305-128">Użytkownicy hello wymaga szkolenia dotyczące toosetup i wdrożenie usługi Multi-Factor authentication?</span><span class="sxs-lookup"><span data-stu-id="90305-128">Will hello users require training on how toosetup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="90305-129">Jakie są najważniejsze scenariusze hello, że firma chce tooenable uwierzytelnianie wieloskładnikowe dla użytkowników?</span><span class="sxs-lookup"><span data-stu-id="90305-129">What are hello key scenarios that your company wants tooenable multi-factor authentication for their users?</span></span>

<span data-ttu-id="90305-130">Po odpowiedzi na pytania wstecz hello, będzie możliwe toounderstand przypadku lokalne uwierzytelnianie wieloskładnikowe już zaimplementowany.</span><span class="sxs-lookup"><span data-stu-id="90305-130">After answering hello previous questions, you will be able toounderstand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="90305-131">Tej oceny jest ważne toodefine hello wymagania techniczne dotyczące konfigurowania i umożliwienie użytkownikom organizacje hello uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="90305-131">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span> <span data-ttu-id="90305-132">Upewnij się, że hello tooanswer następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="90305-132">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="90305-133">Czy firma potrzebuje tooprotect uprzywilejowane konta za pomocą usługi MFA?</span><span class="sxs-lookup"><span data-stu-id="90305-133">Does your company need tooprotect privileged accounts with MFA?</span></span>
* <span data-ttu-id="90305-134">Czy firma musi tooenable MFA dla niektórych aplikacji dla zachowania zgodności?</span><span class="sxs-lookup"><span data-stu-id="90305-134">Does your company need tooenable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="90305-135">Czy firma musi tooenable MFA dla wszystkich kwalifikujących się użytkowników z tych aplikacji lub tylko administratorzy</span><span class="sxs-lookup"><span data-stu-id="90305-135">Does your company need tooenable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="90305-136">Czy konieczne jest zawsze włączone uwierzytelnianie MFA lub tylko wtedy, gdy hello użytkownicy są zalogowani poza siecią firmową?</span><span class="sxs-lookup"><span data-stu-id="90305-136">Do you need have MFA always enabled or only when hello users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="90305-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="90305-137">Next steps</span></span>
[<span data-ttu-id="90305-138">Definiowanie strategii wdrażania tożsamości hybrydowej</span><span class="sxs-lookup"><span data-stu-id="90305-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="90305-139">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="90305-139">See also</span></span>
[<span data-ttu-id="90305-140">Omówienie zagadnień dotyczących projektowania</span><span class="sxs-lookup"><span data-stu-id="90305-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

