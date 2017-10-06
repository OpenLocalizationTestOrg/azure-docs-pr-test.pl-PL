---
title: "w aaaSign, korzystając z usługi Azure AD Identity Protection | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie hello środowisko użytkownika podczas ochrony tożsamości skorygowane lub skorygowane przez użytkownika lub gdy uwierzytelnianie wieloskładnikowe jest wymagany przez zasady."
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
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="a846e-104">Logowanie, korzystając z usługi Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="a846e-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="a846e-105">Za pomocą usługi Azure Active Directory Identity Protection można:</span><span class="sxs-lookup"><span data-stu-id="a846e-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="a846e-106">Wymagaj uwierzytelniania wieloskładnikowego tooregister użytkowników</span><span class="sxs-lookup"><span data-stu-id="a846e-106">require users tooregister for multi-factor authentication</span></span>
* <span data-ttu-id="a846e-107">Obsługa ryzykowne logowania i użytkowników z naruszonymi zabezpieczeniami</span><span class="sxs-lookup"><span data-stu-id="a846e-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="a846e-108">odpowiedź Hello hello systemu toothese problemów ma wpływ na środowiska logowania użytkownika, ponieważ tylko bezpośrednio logowanie przez podanie nazwy użytkownika i hasło nie będzie możliwe już.</span><span class="sxs-lookup"><span data-stu-id="a846e-108">hello response of hello system toothese issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="a846e-109">Dodatkowe kroki są wymagane tooget użytkownika bezpiecznie z powrotem do firm.</span><span class="sxs-lookup"><span data-stu-id="a846e-109">Additional steps are required tooget a user safely back into business.</span></span>

<span data-ttu-id="a846e-110">Ten temat zawiera omówienie środowiska użytkownika logowania dla wszystkich przypadków, które mogą wystąpić.</span><span class="sxs-lookup"><span data-stu-id="a846e-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="a846e-111">**Multi-Factor Authentication**</span><span class="sxs-lookup"><span data-stu-id="a846e-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="a846e-112">Uwierzytelnianie wieloskładnikowe rejestracji</span><span class="sxs-lookup"><span data-stu-id="a846e-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="a846e-113">**Logowanie na ryzyko**</span><span class="sxs-lookup"><span data-stu-id="a846e-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="a846e-114">Ryzykowne odzyskiwania logowania</span><span class="sxs-lookup"><span data-stu-id="a846e-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="a846e-115">Ryzykowne logowania zablokowane</span><span class="sxs-lookup"><span data-stu-id="a846e-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="a846e-116">Rejestracja usługi Multi-Factor authentication podczas ryzykowne logowanie</span><span class="sxs-lookup"><span data-stu-id="a846e-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="a846e-117">**Użytkownik na ryzyko**</span><span class="sxs-lookup"><span data-stu-id="a846e-117">**User at risk**</span></span>

* <span data-ttu-id="a846e-118">Zagrożone konto odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="a846e-118">Compromised account recovery</span></span>
* <span data-ttu-id="a846e-119">Zagrożone Konto zablokowane</span><span class="sxs-lookup"><span data-stu-id="a846e-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="a846e-120">Uwierzytelnianie wieloskładnikowe rejestracji</span><span class="sxs-lookup"><span data-stu-id="a846e-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="a846e-121">Witaj najlepsze środowisko użytkownika dla obu, hello zagrożone konto przepływu odzyskiwania i hello ryzykowne przepływu logowania, jest, gdy użytkownik hello własnym można odzyskać.</span><span class="sxs-lookup"><span data-stu-id="a846e-121">hello best user experience for both, hello compromised account recovery flow and hello risky sign-in flow, is when hello user can self-recover.</span></span> <span data-ttu-id="a846e-122">Jeśli użytkownicy są zarejestrowani w usłudze Multi-Factor authentication, mają numer telefonu skojarzony z użyciem konta, które mogą być używane toopass trudności.</span><span class="sxs-lookup"><span data-stu-id="a846e-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used toopass security challenges.</span></span> <span data-ttu-id="a846e-123">Pomoc techniczna lub administrator udziałów jest wymagane toorecover przed złamaniem konta.</span><span class="sxs-lookup"><span data-stu-id="a846e-123">No help desk or administrator involvement is needed toorecover from account compromise.</span></span> <span data-ttu-id="a846e-124">W związku z tym zdecydowanie zaleca tooget użytkowników zarejestrowanych w usłudze Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="a846e-124">Thus, it’s highly recommended tooget your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="a846e-125">Administratorzy mogą:</span><span class="sxs-lookup"><span data-stu-id="a846e-125">Administrators can:</span></span>

* <span data-ttu-id="a846e-126">Ustaw zasady, które wymaga tooset użytkownikom ich kont do dodatkowej weryfikacji zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a846e-126">set a policy that requires users tooset up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="a846e-127">umożliwia pomijanie rejestracji usługi Multi-Factor authentication dla się too30 dni, w przypadku, gdy mają one użytkownikom toogive okres prolongaty przed zarejestrowaniem.</span><span class="sxs-lookup"><span data-stu-id="a846e-127">allow skipping multi-factor authentication registration for up too30 days, in case they want toogive users a grace period before registering.</span></span>

<span data-ttu-id="a846e-128">**Witaj rejestracji usługi Multi-Factor authentication ma trzy kroki:**</span><span class="sxs-lookup"><span data-stu-id="a846e-128">**hello multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="a846e-129">W pierwszym kroku hello hello użytkownik otrzymuje powiadomienie o hello wymaganie tooset hello koncie dla usługi Multi-Factor authentication.</span><span class="sxs-lookup"><span data-stu-id="a846e-129">In hello first step, hello user gets a notification about hello requirement tooset hello account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="a846e-130">![Korygowanie](./media/active-directory-identityprotection-flows/140.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a846e-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="a846e-131">uwierzytelnianie wieloskładnikowe tooset zapasowej, należy toolet hello systemu znać sposób toobe nawiązać z nią kontaktu.</span><span class="sxs-lookup"><span data-stu-id="a846e-131">tooset multi-factor authentication up, you need toolet hello system know how you want toobe contacted.</span></span>
   
    <span data-ttu-id="a846e-132">![Korygowanie](./media/active-directory-identityprotection-flows/141.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a846e-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="a846e-133">Hello system przesyła tooyou żądania i należy toorespond.</span><span class="sxs-lookup"><span data-stu-id="a846e-133">hello system submits a challenge tooyou and you need toorespond.</span></span>
   
    <span data-ttu-id="a846e-134">![Korygowanie](./media/active-directory-identityprotection-flows/142.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a846e-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="a846e-135">Ryzykowne odzyskiwania logowania</span><span class="sxs-lookup"><span data-stu-id="a846e-135">Risky sign-in recovery</span></span>
<span data-ttu-id="a846e-136">Jeśli administrator skonfigurował zasady logowania ryzyka, hello wpływ użytkownicy są powiadamiani próbują toosign w.</span><span class="sxs-lookup"><span data-stu-id="a846e-136">When an administrator has configured a policy for sign-in risks, hello affected users are notified when they try toosign-in.</span></span> 

<span data-ttu-id="a846e-137">**Witaj ryzykowne logowania przepływu obejmuje dwa kroki:**</span><span class="sxs-lookup"><span data-stu-id="a846e-137">**hello risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="a846e-138">Witaj, użytkownik jest informowany, nietypowe zachowanie wykryto o ich logowania, takich jak logowanie nastąpiło z nowej lokalizacji, urządzenia lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a846e-138">hello user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="a846e-139">![Korygowanie](./media/active-directory-identityprotection-flows/120.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a846e-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="a846e-140">Witaj użytkownika jest wymagane tooprove swoją tożsamość przy użyciu testu zabezpieczeń rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="a846e-140">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="a846e-141">Jeśli użytkownik hello jest zarejestrowany w usłudze Multi-Factor authentication muszą tooround podróży służbowej numeru telefonu tootheir kodu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a846e-141">If hello user is registered for multi-factor authentication they need tooround-trip a security code tootheir phone number.</span></span> <span data-ttu-id="a846e-142">Ponieważ jest to tylko ryzykowne logowania i nie zagrożone konto użytkownika hello nie będziesz mieć hasłem hello toochange w tym przepływie.</span><span class="sxs-lookup"><span data-stu-id="a846e-142">Since this is a just a risky sign in and not a compromised account, hello user won’t have toochange hello password in this flow.</span></span> 
   
    <span data-ttu-id="a846e-143">![Korygowanie](./media/active-directory-identityprotection-flows/121.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a846e-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="a846e-144">Ryzykowne logowania zablokowane</span><span class="sxs-lookup"><span data-stu-id="a846e-144">Risky sign-in blocked</span></span>
<span data-ttu-id="a846e-145">Administratorzy mogą również wybrać tooset tooblock zasad ryzyka logowania użytkowników na logowanie się w zależności od poziomu zagrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="a846e-145">Administrators can also choose tooset a Sign-In Risk policy tooblock users upon sign-in depending on hello risk level.</span></span> <span data-ttu-id="a846e-146">tooget odblokowany, użytkownicy końcowi muszą skontaktuj się z administratorem lub pomocą techniczną lub próbują można logować się z lokalizacji znanych lub urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a846e-146">tooget unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="a846e-147">Własnym odzyskiwanie przy rozwiązywaniu usługi Multi-Factor authentication nie jest opcją w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="a846e-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="a846e-148">![Korygowanie](./media/active-directory-identityprotection-flows/200.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a846e-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="a846e-149">Zagrożone konto odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="a846e-149">Compromised account recovery</span></span>
<span data-ttu-id="a846e-150">Gdy skonfigurowano zasady zabezpieczeń użytkownika ryzyka, użytkowników, którzy spełniają użytkownika hello ryzyka poziom określonym w zasadach hello (i w związku z tym są uznawane za naruszenia zabezpieczeń) musi przejść hello użytkownika naruszenia odzyskiwania przepływu, przed ich można logowania.</span><span class="sxs-lookup"><span data-stu-id="a846e-150">When a user risk security policy has been configured, users who meet hello user risk level specified in hello policy (and are therefore assumed compromised) must go through hello user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="a846e-151">**Witaj użytkownika naruszenia odzyskiwania przepływu ma trzy kroki:**</span><span class="sxs-lookup"><span data-stu-id="a846e-151">**hello user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="a846e-152">Witaj, użytkownik jest informowany, że ich bezpieczeństwo konta jest zablokowana z powodu podejrzanej aktywności lub ujawnione poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="a846e-152">hello user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="a846e-153">![Korygowanie](./media/active-directory-identityprotection-flows/101.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a846e-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="a846e-154">Witaj użytkownika jest wymagane tooprove swoją tożsamość przy użyciu testu zabezpieczeń rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="a846e-154">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="a846e-155">Witaj użytkownik jest zarejestrowany w usłudze Multi-Factor authentication będą oni mogli samodzielnie odzyskiwać złamaniu.</span><span class="sxs-lookup"><span data-stu-id="a846e-155">If hello user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="a846e-156">Należy tooround podróży służbowej numeru telefonu tootheir kodu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a846e-156">They will need tooround-trip a security code tootheir phone number.</span></span> 
   
   <span data-ttu-id="a846e-157">![Korygowanie](./media/active-directory-identityprotection-flows/110.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a846e-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="a846e-158">Na koniec hello użytkownika jest wymuszone toochange swojego hasła, ponieważ ktoś inny ma dostęp do konta tootheir.</span><span class="sxs-lookup"><span data-stu-id="a846e-158">Finally, hello user is forced toochange their password since someone else may have had access tootheir account.</span></span> 
   <span data-ttu-id="a846e-159">Zrzuty ekranu to obsługi są poniżej.</span><span class="sxs-lookup"><span data-stu-id="a846e-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="a846e-160">![Korygowanie](./media/active-directory-identityprotection-flows/111.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a846e-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="a846e-161">Zagrożone Konto zablokowane</span><span class="sxs-lookup"><span data-stu-id="a846e-161">Compromised account blocked</span></span>
<span data-ttu-id="a846e-162">tooget użytkownika, który został zablokowany przez zasady zabezpieczeń użytkownika ryzyka odblokowany hello użytkownik musi skontaktować się administratora lub pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="a846e-162">tooget a user that was blocked by a user risk security policy unblocked, hello user must contact an administrator or help desk.</span></span> <span data-ttu-id="a846e-163">Własnym odzyskiwanie przy rozwiązywaniu usługi Multi-Factor authentication nie jest opcją w tym przypadku.</span><span class="sxs-lookup"><span data-stu-id="a846e-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="a846e-164">![Korygowanie](./media/active-directory-identityprotection-flows/104.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a846e-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="a846e-165">Resetowanie hasła</span><span class="sxs-lookup"><span data-stu-id="a846e-165">Reset password</span></span>
<span data-ttu-id="a846e-166">Jeśli ze złamanymi zabezpieczeniami użytkownicy są blokowani logowanie, administrator może generować hasło tymczasowe dla nich.</span><span class="sxs-lookup"><span data-stu-id="a846e-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="a846e-167">Witaj, użytkownicy będą mieli toochange swoje hasło podczas następnego logowania.</span><span class="sxs-lookup"><span data-stu-id="a846e-167">hello users will have toochange their password during a next sign-in.</span></span>

<span data-ttu-id="a846e-168">![Korygowanie](./media/active-directory-identityprotection-flows/160.png "korygowania")</span><span class="sxs-lookup"><span data-stu-id="a846e-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="a846e-169">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a846e-169">See also</span></span>
* [<span data-ttu-id="a846e-170">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a846e-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

