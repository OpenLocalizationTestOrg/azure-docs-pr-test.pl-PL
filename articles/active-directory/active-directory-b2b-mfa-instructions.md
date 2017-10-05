---
title: "Dostęp warunkowy dla usługi Azure Active Directory B2B współpracy użytkowników | Dokumentacja firmy Microsoft"
description: "Azure współpracy B2B usługi Active Directory obsługuje uwierzytelnianie wieloskładnikowe (MFA) dla selektywny dostęp do aplikacji firmowych"
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
ms.openlocfilehash: d85f711d6551a68d1248ae8ec61e2ecc1ddc8ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="384cb-103">Dostęp warunkowy dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="384cb-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="384cb-104">Uwierzytelnianie wieloskładnikowe dla użytkowników B2B</span><span class="sxs-lookup"><span data-stu-id="384cb-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="384cb-105">Współpracy B2B usługi Azure AD organizacji można wymusić uwierzytelnianie wieloskładnikowe (MFA) zasad dla użytkowników B2B.</span><span class="sxs-lookup"><span data-stu-id="384cb-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="384cb-106">Te zasady można wymusić na poziomie indywidualnego użytkownika dzierżawcy, aplikacji lub ten sam sposób, że są włączone dla pełnoetatowych pracowników i członków organizacji.</span><span class="sxs-lookup"><span data-stu-id="384cb-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="384cb-107">Zasady MFA są wymuszane w organizacji zasobów.</span><span class="sxs-lookup"><span data-stu-id="384cb-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="384cb-108">Przykład:</span><span class="sxs-lookup"><span data-stu-id="384cb-108">Example:</span></span>
1. <span data-ttu-id="384cb-109">Administratora lub informacje pracownika z firmy, A zaprasza użytkownikowi aplikacji firmy B *Foo* w firmie A.</span><span class="sxs-lookup"><span data-stu-id="384cb-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span></span>
2. <span data-ttu-id="384cb-110">Aplikacja *Foo* w firmie A jest skonfigurowany do uwierzytelniania MFA można wymagać dostępu.</span><span class="sxs-lookup"><span data-stu-id="384cb-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="384cb-111">Próba dostępu aplikacji użytkownika z firmy B *Foo* firmy dzierżawcy, proszeni są o wykonać żądanie uwierzytelniania MFA.</span><span class="sxs-lookup"><span data-stu-id="384cb-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span></span>
4. <span data-ttu-id="384cb-112">Użytkownika można skonfigurować ich MFA z firmy A i wybierze opcję ich MFA.</span><span class="sxs-lookup"><span data-stu-id="384cb-112">The user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="384cb-113">W tym scenariuszu działa w przypadku tożsamości (Azure AD lub zarządzanych kont usług, na przykład, jeśli użytkownicy w firmie B uwierzytelniać za pomocą Identyfikatora społecznościowych)</span><span class="sxs-lookup"><span data-stu-id="384cb-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="384cb-114">Firmy, A musi mieć wystarczającą liczbę licencji usługi Azure AD Premium, które obsługują usługę MFA.</span><span class="sxs-lookup"><span data-stu-id="384cb-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="384cb-115">Ta licencja firmy A. zużywa użytkownika z firmy B</span><span class="sxs-lookup"><span data-stu-id="384cb-115">The user from company B consumes this license from company A.</span></span>

<span data-ttu-id="384cb-116">Zaproszenia dzierżawy jest odpowiedzialny za uwierzytelnianie wieloskładnikowe dla użytkowników w organizacji partnera zawsze, nawet w przypadku organizacji partnerskiej funkcję MFA.</span><span class="sxs-lookup"><span data-stu-id="384cb-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="384cb-117">Konfigurowanie usługi MFA dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="384cb-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="384cb-118">Aby dowiedzieć się, jak łatwo jest skonfigurować uwierzytelnianie wieloskładnikowe dla użytkowników współpracy B2B, zobacz temat jak w poniższym klipie wideo:</span><span class="sxs-lookup"><span data-stu-id="384cb-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="384cb-119">Użytkownicy B2B środowisko MFA oferują realizacji</span><span class="sxs-lookup"><span data-stu-id="384cb-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="384cb-120">Zapoznaj się z następujących animacji, aby zobaczyć realizacji środowisko:</span><span class="sxs-lookup"><span data-stu-id="384cb-120">Check out the following animation to see the redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="384cb-121">Resetuj dla użytkowników współpracy B2B usługi MFA</span><span class="sxs-lookup"><span data-stu-id="384cb-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="384cb-122">Obecnie administrator może wymagać współpracy B2B użytkownikom dowód się ponownie tylko za pomocą następujących poleceń cmdlet programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="384cb-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="384cb-123">Łączenie z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="384cb-123">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="384cb-124">Pobierz wszyscy użytkownicy dowód metod</span><span class="sxs-lookup"><span data-stu-id="384cb-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="384cb-125">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="384cb-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="384cb-126">Reset — metoda uwierzytelniania Wieloskładnikowego dla określonego użytkownika wymagać od użytkownika współpracy B2B ponownie ustawić metody potwierdzenia w górę.</span><span class="sxs-lookup"><span data-stu-id="384cb-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="384cb-127">Przykład:</span><span class="sxs-lookup"><span data-stu-id="384cb-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="384cb-128">Dlaczego możemy użyć uwierzytelniania MFA w dzierżawy zasobów?</span><span class="sxs-lookup"><span data-stu-id="384cb-128">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="384cb-129">W bieżącej wersji usługi MFA jest zawsze w dzierżawy zasobów, ze względu na przewidywalności.</span><span class="sxs-lookup"><span data-stu-id="384cb-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="384cb-130">Na przykład załóżmy, że użytkownik Contoso (Zosi) zachęca się do firmy Fabrikam ma włączone uwierzytelnianie wieloskładnikowe dla użytkowników B2B.</span><span class="sxs-lookup"><span data-stu-id="384cb-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="384cb-131">Jeżeli Contoso ma włączone zasady MFA na serwerze App1, ale nie App2, jeśli przyjrzymy się Contoso MFA oświadczenia w tokenie, firma Microsoft może zobacz następujący problem:</span><span class="sxs-lookup"><span data-stu-id="384cb-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span></span>

* <span data-ttu-id="384cb-132">Dzień 1: Użytkownik ma MFA w firmie Contoso i uzyskuje dostęp do komputera App1, a następnie nie dodatkowe uwierzytelnianie wieloskładnikowe monit jest wyświetlany w firmie Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="384cb-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="384cb-133">Dzień 2: Użytkownik uzyskiwał dostęp do 2 aplikacji w firmie Contoso, więc podczas uzyskiwania dostępu do firmy Fabrikam, muszą zarejestrować dla usługi MFA istnieje.</span><span class="sxs-lookup"><span data-stu-id="384cb-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="384cb-134">Ten proces może być trudne i może prowadzić do drop w zakończeń logowania.</span><span class="sxs-lookup"><span data-stu-id="384cb-134">This process can be confusing and could lead to drop in sign-in completions.</span></span>

<span data-ttu-id="384cb-135">Ponadto nawet jeśli firma Contoso ma możliwość uwierzytelniania MFA, nie zawsze jest sprawy firma Fabrikam może zaufanie zasady MFA firmy Contoso.</span><span class="sxs-lookup"><span data-stu-id="384cb-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="384cb-136">Na koniec zasobów dzierżawy MFA działa również MSA i identyfikatory społecznościowych oraz organizacjami partnera, bez konfigurowania uwierzytelniania Wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="384cb-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="384cb-137">W związku z tym dla usługi MFA dla użytkowników B2B zaleca się zawsze wymagają usługi MFA w dzierżawie zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="384cb-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span></span> <span data-ttu-id="384cb-138">Ten wymóg może prowadzić do podwójne MFA w niektórych przypadkach, ale zawsze, gdy dostęp do dzierżawy zaproszenia, środowisko użytkownika końcowego jest atrybutem wartości prognozowanych: Zosi musi zarejestrować w usłudze MFA z dzierżawcą zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="384cb-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="384cb-139">Oparta na urządzeniach, na podstawie lokalizacji i ryzyka dostępu warunkowego dla użytkowników B2B</span><span class="sxs-lookup"><span data-stu-id="384cb-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="384cb-140">Gdy Contoso włącza zasady dostępu warunkowego opartego na urządzenia do danych firmowych, dostępu nie urządzeń, które nie są zarządzane przez firmę Contoso i nie są zgodne z zasadami urządzenia firmy Contoso.</span><span class="sxs-lookup"><span data-stu-id="384cb-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span></span>

<span data-ttu-id="384cb-141">Jeśli urządzenie użytkownika B2B nie jest zarządzana przez firmy Contoso, dostęp użytkowników B2B z organizacji partnera jest zablokowany w dowolnym kontekście te zasady są wymuszane.</span><span class="sxs-lookup"><span data-stu-id="384cb-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="384cb-142">Jednak Contoso można utworzyć listy wykluczeń zawierających użytkowników partnera, aby wykluczyć je z zasad dostępu warunkowego opartego na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="384cb-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="384cb-143">Na podstawie lokalizacji dostępu warunkowego dla B2B</span><span class="sxs-lookup"><span data-stu-id="384cb-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="384cb-144">Jeśli zaproszenia organizacji jest możliwość tworzenia zaufany zakres adresów IP, który definiuje organizacji partnera można wymuszać zasady dostępu warunkowego na podstawie lokalizacji B2B użytkowników.</span><span class="sxs-lookup"><span data-stu-id="384cb-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="384cb-145">Dostęp warunkowy dla B2B ryzyka</span><span class="sxs-lookup"><span data-stu-id="384cb-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="384cb-146">Obecnie zasady oparte na ryzyko logowania nie można zastosować użytkownikom B2B oceny ryzyka jest wykonywana w organizacji macierzystej użytkownika B2B.</span><span class="sxs-lookup"><span data-stu-id="384cb-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="384cb-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="384cb-147">Next steps</span></span>

<span data-ttu-id="384cb-148">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="384cb-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="384cb-149">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="384cb-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="384cb-150">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="384cb-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="384cb-151">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="384cb-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="384cb-152">Elementy współpracy B2B zaproszenie</span><span class="sxs-lookup"><span data-stu-id="384cb-152">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="384cb-153">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="384cb-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="384cb-154">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="384cb-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="384cb-155">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="384cb-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="384cb-156">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="384cb-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="384cb-157">Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="384cb-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="384cb-158">Dodawanie użytkowników współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="384cb-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="384cb-159">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="384cb-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
