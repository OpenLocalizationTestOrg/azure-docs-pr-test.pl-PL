---
title: "Logowanie napotyka przy użyciu usługi Azure AD Identity Protection | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie środowiska użytkownika, gdy ochronę tożsamości ma skorygowane lub skorygowane przez użytkownika lub uwierzytelnianie wieloskładnikowe jest wymagany przez zasady."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e45936280b51fb2e54012a688fceddcc8dabe984
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="a3960-104">Logowanie, korzystając z usługi Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a3960-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="a3960-105">Za pomocą usługi Azure Active Directory Identity Protection można:</span><span class="sxs-lookup"><span data-stu-id="a3960-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="a3960-106">Wymagaj rejestracji w usłudze Multi-Factor authentication użytkowników</span><span class="sxs-lookup"><span data-stu-id="a3960-106">require users to register for multi-factor authentication</span></span>
* <span data-ttu-id="a3960-107">Obsługa ryzykowne logowania i użytkowników z naruszonymi zabezpieczeniami</span><span class="sxs-lookup"><span data-stu-id="a3960-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="a3960-108">Odpowiedź systemu te problemy ma wpływ na środowisko logowania użytkownika, ponieważ tylko bezpośrednio logowanie przez podanie nazwy użytkownika i hasło nie będzie możliwe już.</span><span class="sxs-lookup"><span data-stu-id="a3960-108">The response of the system to these issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="a3960-109">Aby bezpiecznie uzyskać użytkownika są wymagane dodatkowe kroki do firm.</span><span class="sxs-lookup"><span data-stu-id="a3960-109">Additional steps are required to get a user safely back into business.</span></span>

<span data-ttu-id="a3960-110">Ten temat zawiera omówienie środowiska użytkownika logowania dla wszystkich przypadków, które mogą wystąpić.</span><span class="sxs-lookup"><span data-stu-id="a3960-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="a3960-111">**Multi-Factor Authentication**</span><span class="sxs-lookup"><span data-stu-id="a3960-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="a3960-112">Uwierzytelnianie wieloskładnikowe rejestracji</span><span class="sxs-lookup"><span data-stu-id="a3960-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="a3960-113">**Logowanie na ryzyko**</span><span class="sxs-lookup"><span data-stu-id="a3960-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="a3960-114">Ryzykowne odzyskiwania logowania</span><span class="sxs-lookup"><span data-stu-id="a3960-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="a3960-115">Ryzykowne logowania zablokowane</span><span class="sxs-lookup"><span data-stu-id="a3960-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="a3960-116">Rejestracja usługi Multi-Factor authentication podczas ryzykowne logowanie</span><span class="sxs-lookup"><span data-stu-id="a3960-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="a3960-117">**Użytkownik na ryzyko**</span><span class="sxs-lookup"><span data-stu-id="a3960-117">**User at risk**</span></span>

* <span data-ttu-id="a3960-118">Zagrożone konto odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="a3960-118">Compromised account recovery</span></span>
* <span data-ttu-id="a3960-119">Zagrożone Konto zablokowane</span><span class="sxs-lookup"><span data-stu-id="a3960-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="a3960-120">Uwierzytelnianie wieloskładnikowe rejestracji</span><span class="sxs-lookup"><span data-stu-id="a3960-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="a3960-121">Najlepsze środowisko użytkownika w przypadku obu zagrożone konto przepływu odzyskiwania i ryzykowne przepływu logowania, jest, gdy użytkownik samodzielnie można odzyskać.</span><span class="sxs-lookup"><span data-stu-id="a3960-121">The best user experience for both, the compromised account recovery flow and the risky sign-in flow, is when the user can self-recover.</span></span> <span data-ttu-id="a3960-122">Jeśli użytkownicy są zarejestrowani w usłudze Multi-Factor authentication, mają numer telefonu skojarzony z użyciem konta, który może służyć do przekazywania trudności.</span><span class="sxs-lookup"><span data-stu-id="a3960-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used to pass security challenges.</span></span> <span data-ttu-id="a3960-123">Pomoc techniczna lub administrator udziałów jest niezbędne do odzyskanie konta naruszenia.</span><span class="sxs-lookup"><span data-stu-id="a3960-123">No help desk or administrator involvement is needed to recover from account compromise.</span></span> <span data-ttu-id="a3960-124">W związku z tym zdecydowanie zaleca się zachęcić użytkowników zarejestrowanych w usłudze Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="a3960-124">Thus, it’s highly recommended to get your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="a3960-125">Administratorzy mogą:</span><span class="sxs-lookup"><span data-stu-id="a3960-125">Administrators can:</span></span>

* <span data-ttu-id="a3960-126">ustawienie zasad, która wymaga od użytkowników skonfigurować swoje konta dodatkowej weryfikacji zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a3960-126">set a policy that requires users to set up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="a3960-127">umożliwia pomijanie usługi Multi-Factor authentication rejestracji przez maksymalnie 30 dni, w przypadku, gdy chcą, aby umożliwić użytkownikom okres prolongaty przed zarejestrowaniem.</span><span class="sxs-lookup"><span data-stu-id="a3960-127">allow skipping multi-factor authentication registration for up to 30 days, in case they want to give users a grace period before registering.</span></span>

<span data-ttu-id="a3960-128">**Rejestracja usługi Multi-Factor authentication ma trzy kroki:**</span><span class="sxs-lookup"><span data-stu-id="a3960-128">**The multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="a3960-129">W pierwszym kroku użytkownik otrzymuje powiadomienie o konieczności Skonfiguruj konto dla usługi Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="a3960-129">In the first step, the user gets a notification about the requirement to set the account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="a3960-130">![Korygowanie](./media/active-directory-identityprotection-flows/140.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a3960-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="a3960-131">Aby skonfigurować uwierzytelnianie wieloskładnikowe, należy umożliwić wiedzieć, jaki ma zostać można skontaktować się z systemu.</span><span class="sxs-lookup"><span data-stu-id="a3960-131">To set multi-factor authentication up, you need to let the system know how you want to be contacted.</span></span>
   
    <span data-ttu-id="a3960-132">![Korygowanie](./media/active-directory-identityprotection-flows/141.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a3960-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="a3960-133">System przesyła żądanie do i możesz muszą odpowiadać.</span><span class="sxs-lookup"><span data-stu-id="a3960-133">The system submits a challenge to you and you need to respond.</span></span>
   
    <span data-ttu-id="a3960-134">![Korygowanie](./media/active-directory-identityprotection-flows/142.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a3960-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="a3960-135">Ryzykowne odzyskiwania logowania</span><span class="sxs-lookup"><span data-stu-id="a3960-135">Risky sign-in recovery</span></span>
<span data-ttu-id="a3960-136">Jeśli administrator skonfigurował zasady logowania ryzyka, narażeni użytkownicy są powiadamiani o próby logowania.</span><span class="sxs-lookup"><span data-stu-id="a3960-136">When an administrator has configured a policy for sign-in risks, the affected users are notified when they try to sign-in.</span></span> 

<span data-ttu-id="a3960-137">**Ryzykowne przepływu logowania ma dwa kroki:**</span><span class="sxs-lookup"><span data-stu-id="a3960-137">**The risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="a3960-138">Użytkownik jest informowany nietypowe zachowanie wykryto o ich logowania, takich jak logowanie nastąpiło z nowej lokalizacji, urządzenia lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a3960-138">The user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="a3960-139">![Korygowanie](./media/active-directory-identityprotection-flows/120.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a3960-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="a3960-140">Użytkownik musi potwierdzić swoją tożsamość przy użyciu testu zabezpieczeń rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="a3960-140">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="a3960-141">Jeśli użytkownik jest zarejestrowany w usłudze Multi-Factor authentication muszą wyrównana kod zabezpieczeń w celu jego numeru telefonu.</span><span class="sxs-lookup"><span data-stu-id="a3960-141">If the user is registered for multi-factor authentication they need to round-trip a security code to their phone number.</span></span> <span data-ttu-id="a3960-142">Ponieważ jest to tylko ryzykowne logowania i zagrożone konto użytkownika nie będziesz mieć możliwość zmiany hasła w tym przepływie.</span><span class="sxs-lookup"><span data-stu-id="a3960-142">Since this is a just a risky sign in and not a compromised account, the user won’t have to change the password in this flow.</span></span> 
   
    <span data-ttu-id="a3960-143">![Korygowanie](./media/active-directory-identityprotection-flows/121.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a3960-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="a3960-144">Ryzykowne logowania zablokowane</span><span class="sxs-lookup"><span data-stu-id="a3960-144">Risky sign-in blocked</span></span>
<span data-ttu-id="a3960-145">Administratorzy mogą wybrać także ustawić zasady logowania ryzyka, aby uniemożliwić użytkownikom na logowanie się w zależności od poziomu zagrożenia.</span><span class="sxs-lookup"><span data-stu-id="a3960-145">Administrators can also choose to set a Sign-In Risk policy to block users upon sign-in depending on the risk level.</span></span> <span data-ttu-id="a3960-146">Uzyskanie odblokowany, użytkowników końcowych musisz skontaktować się z administratorem lub pomocą techniczną lub próbują można logować się z lokalizacji znanych lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a3960-146">To get unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="a3960-147">Własnym odzyskiwanie przy rozwiązywaniu usługi Multi-Factor authentication nie jest opcją w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="a3960-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="a3960-148">![Korygowanie](./media/active-directory-identityprotection-flows/200.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a3960-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="a3960-149">Zagrożone konto odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="a3960-149">Compromised account recovery</span></span>
<span data-ttu-id="a3960-150">Gdy skonfigurowano zasady zabezpieczeń użytkownika ryzyka, użytkowników, którzy spełniają użytkownika ryzyka poziom określonym w zasadach (i w związku z tym są uznawane za naruszenia zabezpieczeń) musi przejść przepływu odzyskiwania naruszenia użytkownika przed ich można logowania.</span><span class="sxs-lookup"><span data-stu-id="a3960-150">When a user risk security policy has been configured, users who meet the user risk level specified in the policy (and are therefore assumed compromised) must go through the user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="a3960-151">**Przepływ odzyskiwania naruszenia użytkownik ma trzy kroki:**</span><span class="sxs-lookup"><span data-stu-id="a3960-151">**The user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="a3960-152">Użytkownik jest informowany, że ich bezpieczeństwo konta jest zablokowana z powodu podejrzanej aktywności lub ujawnione poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="a3960-152">The user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="a3960-153">![Korygowanie](./media/active-directory-identityprotection-flows/101.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a3960-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="a3960-154">Użytkownik musi potwierdzić swoją tożsamość przy użyciu testu zabezpieczeń rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="a3960-154">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="a3960-155">Jeśli użytkownik jest zarejestrowany w usłudze Multi-Factor authentication będą oni mogli samodzielnie odzyskiwać złamaniu.</span><span class="sxs-lookup"><span data-stu-id="a3960-155">If the user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="a3960-156">Należy wyrównana kod zabezpieczeń w celu jego numeru telefonu.</span><span class="sxs-lookup"><span data-stu-id="a3960-156">They will need to round-trip a security code to their phone number.</span></span> 
   
   <span data-ttu-id="a3960-157">![Korygowanie](./media/active-directory-identityprotection-flows/110.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a3960-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="a3960-158">Ponadto użytkownik będzie zmuszony do zmiany hasła, ponieważ ktoś inny ma dostęp do swojego konta.</span><span class="sxs-lookup"><span data-stu-id="a3960-158">Finally, the user is forced to change their password since someone else may have had access to their account.</span></span> 
   <span data-ttu-id="a3960-159">Zrzuty ekranu to obsługi są poniżej.</span><span class="sxs-lookup"><span data-stu-id="a3960-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="a3960-160">![Korygowanie](./media/active-directory-identityprotection-flows/111.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a3960-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="a3960-161">Zagrożone Konto zablokowane</span><span class="sxs-lookup"><span data-stu-id="a3960-161">Compromised account blocked</span></span>
<span data-ttu-id="a3960-162">Aby uzyskać użytkownika, który został zablokowany przez zasady zabezpieczeń użytkownika ryzyka odblokowany, użytkownik musi skontaktować się z administratorem lub pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="a3960-162">To get a user that was blocked by a user risk security policy unblocked, the user must contact an administrator or help desk.</span></span> <span data-ttu-id="a3960-163">Własnym odzyskiwanie przy rozwiązywaniu usługi Multi-Factor authentication nie jest opcją w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="a3960-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="a3960-164">![Korygowanie](./media/active-directory-identityprotection-flows/104.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a3960-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="a3960-165">Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="a3960-165">Reset password</span></span>
<span data-ttu-id="a3960-166">Jeśli ze złamanymi zabezpieczeniami użytkownicy są blokowani logowanie, administrator może generować hasło tymczasowe dla nich.</span><span class="sxs-lookup"><span data-stu-id="a3960-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="a3960-167">Użytkownicy mają do zmiany hasła podczas następnego logowania.</span><span class="sxs-lookup"><span data-stu-id="a3960-167">The users will have to change their password during a next sign-in.</span></span>

<span data-ttu-id="a3960-168">![Korygowanie](./media/active-directory-identityprotection-flows/160.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a3960-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="a3960-169">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a3960-169">See also</span></span>
* [<span data-ttu-id="a3960-170">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a3960-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

