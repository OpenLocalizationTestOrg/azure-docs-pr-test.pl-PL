---
title: "aaaConditional dostęp do usługi Azure Active Directory B2B współpracy użytkownikom | Dokumentacja firmy Microsoft"
description: "Azure współpracy B2B usługi Active Directory obsługuje uwierzytelnianie wieloskładnikowe (MFA) dla aplikacji firmowych tooyour selektywny dostęp"
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
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="0699a-103">Dostęp warunkowy dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0699a-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="0699a-104">Uwierzytelnianie wieloskładnikowe dla użytkowników B2B</span><span class="sxs-lookup"><span data-stu-id="0699a-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="0699a-105">Współpracy B2B usługi Azure AD organizacji można wymusić uwierzytelnianie wieloskładnikowe (MFA) zasad dla użytkowników B2B.</span><span class="sxs-lookup"><span data-stu-id="0699a-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="0699a-106">Te zasady mogą być wymuszane w hello dzierżawy, aplikacji lub na poziomie indywidualnego użytkownika, hello taki sam sposób, że są włączone dla pełnoetatowych pracowników i członków organizacji hello.</span><span class="sxs-lookup"><span data-stu-id="0699a-106">These policies can be enforced at hello tenant, app, or individual user level, hello same way that they are enabled for full-time employees and members of hello organization.</span></span> <span data-ttu-id="0699a-107">Zasady MFA są wymuszane na powitania zasobów organizacji.</span><span class="sxs-lookup"><span data-stu-id="0699a-107">MFA policies are enforced at hello resource organization.</span></span>

<span data-ttu-id="0699a-108">Przykład:</span><span class="sxs-lookup"><span data-stu-id="0699a-108">Example:</span></span>
1. <span data-ttu-id="0699a-109">Użytkownik z aplikacji tooan firmy B zaprasza administratora lub informacje pracownika z firmy, A *Foo* w firmie A.</span><span class="sxs-lookup"><span data-stu-id="0699a-109">Admin or information worker in Company A invites user from company B tooan application *Foo* in company A.</span></span>
2. <span data-ttu-id="0699a-110">Aplikacja *Foo* w firmie, A jest skonfigurowany toorequire MFA na dostęp.</span><span class="sxs-lookup"><span data-stu-id="0699a-110">Application *Foo* in company A is configured toorequire MFA on access.</span></span>
3. <span data-ttu-id="0699a-111">Gdy użytkownik hello firmy B próbuje aplikacji tooaccess *Foo* firmy hello dzierżawcy, są one zadawane toocomplete żądanie uwierzytelniania MFA.</span><span class="sxs-lookup"><span data-stu-id="0699a-111">When hello user from company B attempts tooaccess app *Foo* in hello company A tenant, they are asked toocomplete an MFA challenge.</span></span>
4. <span data-ttu-id="0699a-112">Witaj użytkownika można skonfigurować ich MFA z firmy A i wybierze opcję ich MFA.</span><span class="sxs-lookup"><span data-stu-id="0699a-112">hello user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="0699a-113">W tym scenariuszu działa w przypadku tożsamości (Azure AD lub zarządzanych kont usług, na przykład, jeśli użytkownicy w firmie B uwierzytelniać za pomocą Identyfikatora społecznościowych)</span><span class="sxs-lookup"><span data-stu-id="0699a-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="0699a-114">Firmy, A musi mieć wystarczającą liczbę licencji usługi Azure AD Premium, które obsługują usługę MFA.</span><span class="sxs-lookup"><span data-stu-id="0699a-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="0699a-115">Użytkownik Hello firmy B zużywa tej licencji od firmy A.</span><span class="sxs-lookup"><span data-stu-id="0699a-115">hello user from company B consumes this license from company A.</span></span>

<span data-ttu-id="0699a-116">dzierżawy zaproszenia Hello jest odpowiedzialny za uwierzytelnianie wieloskładnikowe dla użytkowników w organizacji partnera hello, zawsze, nawet w przypadku organizacji partnerskiej hello funkcję MFA.</span><span class="sxs-lookup"><span data-stu-id="0699a-116">hello inviting tenancy is always responsible for MFA for users from hello partner organization, even if hello partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="0699a-117">Konfigurowanie usługi MFA dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0699a-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="0699a-118">toodiscover, jak łatwo jest tooset się uwierzytelnianie wieloskładnikowe dla użytkowników współpracy B2B, zobacz temat jak w hello następujących wideo:</span><span class="sxs-lookup"><span data-stu-id="0699a-118">toodiscover how easy it is tooset up MFA for B2B collaboration users, see how in hello following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="0699a-119">Użytkownicy B2B środowisko MFA oferują realizacji</span><span class="sxs-lookup"><span data-stu-id="0699a-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="0699a-120">Wyewidencjonuj powitania po animacji toosee hello realizacji środowisko:</span><span class="sxs-lookup"><span data-stu-id="0699a-120">Check out hello following animation toosee hello redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="0699a-121">Resetuj dla użytkowników współpracy B2B usługi MFA</span><span class="sxs-lookup"><span data-stu-id="0699a-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="0699a-122">Obecnie Witaj, Administratorze może wymagać tooproof użytkowników współpracy B2B się ponownie tylko za pomocą następującego polecenia cmdlet programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="0699a-122">Currently, hello admin can require B2B collaboration users tooproof up again only by using hello following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="0699a-123">Połącz tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="0699a-123">Connect tooAzure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="0699a-124">Pobierz wszyscy użytkownicy dowód metod</span><span class="sxs-lookup"><span data-stu-id="0699a-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="0699a-125">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="0699a-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="0699a-126">Resetuj hello MFA metoda dla określonego użytkownika toorequire hello B2B współpracy użytkownika tooset up dowód metod ponownie.</span><span class="sxs-lookup"><span data-stu-id="0699a-126">Reset hello MFA method for a specific user toorequire hello B2B collaboration user tooset proof-up methods again.</span></span> <span data-ttu-id="0699a-127">Przykład:</span><span class="sxs-lookup"><span data-stu-id="0699a-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a><span data-ttu-id="0699a-128">Dlaczego możemy wykonywać uwierzytelnianie wieloskładnikowe na powitania zasobów dzierżawy?</span><span class="sxs-lookup"><span data-stu-id="0699a-128">Why do we perform MFA at hello resource tenancy?</span></span>

<span data-ttu-id="0699a-129">W bieżącej wersji hello MFA jest zawsze w hello zasobów dzierżawy, ze względu na przewidywalności.</span><span class="sxs-lookup"><span data-stu-id="0699a-129">In hello current release, MFA is always in hello resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="0699a-130">Na przykład załóżmy, że użytkownik Contoso (Zosi) jest tooFabrikam zaproszonych Fabrikam ma włączone uwierzytelnianie wieloskładnikowe dla użytkowników B2B.</span><span class="sxs-lookup"><span data-stu-id="0699a-130">For example, let’s say a Contoso user (Sally) is invited tooFabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="0699a-131">Jeżeli Contoso ma włączone zasady MFA na serwerze App1, ale nie App2, jeśli przyjrzymy się hello Contoso MFA oświadczenia w tokenie hello, firma Microsoft może zobacz hello następującego problemu:</span><span class="sxs-lookup"><span data-stu-id="0699a-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at hello Contoso MFA claim in hello token, we might see hello following issue:</span></span>

* <span data-ttu-id="0699a-132">Dzień 1: Użytkownik ma MFA w firmie Contoso i uzyskuje dostęp do komputera App1, a następnie nie dodatkowe uwierzytelnianie wieloskładnikowe monit jest wyświetlany w firmie Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="0699a-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="0699a-133">Dzień 2: hello użytkownik uzyskiwał dostęp do 2 aplikacji w firmie Contoso, więc podczas uzyskiwania dostępu do firmy Fabrikam, muszą zarejestrować dla usługi MFA istnieje.</span><span class="sxs-lookup"><span data-stu-id="0699a-133">Day 2: hello user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="0699a-134">Ten proces może być trudne i może prowadzić toodrop w zakończeń logowania.</span><span class="sxs-lookup"><span data-stu-id="0699a-134">This process can be confusing and could lead toodrop in sign-in completions.</span></span>

<span data-ttu-id="0699a-135">Ponadto nawet jeśli firma Contoso ma możliwość uwierzytelniania MFA, nie zawsze jest hello hello sprawy firma Fabrikam może zaufanie hello zasad MFA firmy Contoso.</span><span class="sxs-lookup"><span data-stu-id="0699a-135">Moreover, even if Contoso has MFA capability, it is not always hello case hello Fabrikam would trust hello Contoso MFA policy.</span></span>

<span data-ttu-id="0699a-136">Na koniec zasobów dzierżawy MFA działa również MSA i identyfikatory społecznościowych oraz organizacjami partnera, bez konfigurowania uwierzytelniania Wieloskładnikowego.</span><span class="sxs-lookup"><span data-stu-id="0699a-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="0699a-137">W związku z tym hello zalecenia dla usługi MFA dla użytkowników B2B jest tooalways wymagają usługi MFA w hello zapraszanie dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="0699a-137">Therefore, hello recommendation for MFA for B2B users is tooalways require MFA in hello inviting tenant.</span></span> <span data-ttu-id="0699a-138">Ten wymóg może prowadzić toodouble MFA w niektórych przypadkach, ale zawsze, gdy dostęp do dzierżawy zaproszenia hello, środowisko użytkownika końcowego hello jest atrybutem wartości prognozowanych: Zosi musi zarejestrować w usłudze MFA z dzierżawcą zaproszenia hello.</span><span class="sxs-lookup"><span data-stu-id="0699a-138">This requirement could lead toodouble MFA in some cases, but whenever accessing hello inviting tenant, hello end-users experience is predictable: Sally must register for MFA with hello inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="0699a-139">Oparta na urządzeniach, na podstawie lokalizacji i ryzyka dostępu warunkowego dla użytkowników B2B</span><span class="sxs-lookup"><span data-stu-id="0699a-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="0699a-140">Gdy Contoso włącza zasady dostępu warunkowego opartego na urządzenia do danych firmowych, dostępu nie urządzeń, które nie są zarządzane przez firmę Contoso i nie są zgodne z zasadami urządzenia Contoso hello.</span><span class="sxs-lookup"><span data-stu-id="0699a-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with hello Contoso device policies.</span></span>

<span data-ttu-id="0699a-141">Jeśli urządzenie hello B2B użytkownika nie jest zarządzana przez firmy Contoso, dostęp użytkowników B2B z organizacji partnerskiej hello jest zablokowany w dowolnym kontekście te zasady są wymuszane.</span><span class="sxs-lookup"><span data-stu-id="0699a-141">If hello B2B user’s device isn't managed by Contoso, access of B2B users from hello partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="0699a-142">Jednak Contoso utworzyć wykluczenie list zawierających tooexclude użytkowników partnera hello je z zasad dostępu warunkowego opartego na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="0699a-142">However, Contoso can create exclusion lists containing specific partner users tooexclude them from hello device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="0699a-143">Na podstawie lokalizacji dostępu warunkowego dla B2B</span><span class="sxs-lookup"><span data-stu-id="0699a-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="0699a-144">Jeśli organizacja zaproszenia hello jest możliwe toocreate zaufany zakres adresów IP, który definiuje organizacji partnera można wymuszać zasady dostępu warunkowego na podstawie lokalizacji dla użytkowników B2B.</span><span class="sxs-lookup"><span data-stu-id="0699a-144">Location-based conditional access policies can be enforced for B2B users if hello inviting organization is able toocreate a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="0699a-145">Dostęp warunkowy dla B2B ryzyka</span><span class="sxs-lookup"><span data-stu-id="0699a-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="0699a-146">Obecnie zasady oparte na ryzyko logowania nie może być zastosowane tooB2B użytkowników oceny ryzyka hello jest wykonywana w organizacji macierzystej hello B2B użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0699a-146">Currently, risk-based sign-in policies cannot be applied tooB2B users because hello risk evaluation is performed at hello B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0699a-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0699a-147">Next steps</span></span>

<span data-ttu-id="0699a-148">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="0699a-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="0699a-149">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="0699a-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="0699a-150">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="0699a-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="0699a-151">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="0699a-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="0699a-152">elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0699a-152">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="0699a-153">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="0699a-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="0699a-154">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="0699a-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="0699a-155">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="0699a-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="0699a-156">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="0699a-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="0699a-157">Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="0699a-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="0699a-158">Dodawanie użytkowników współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="0699a-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="0699a-159">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0699a-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
