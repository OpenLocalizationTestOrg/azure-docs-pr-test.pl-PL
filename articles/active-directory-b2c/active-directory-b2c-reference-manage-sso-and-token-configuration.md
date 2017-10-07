---
title: "Usługa Azure Active Directory B2C: Zarządzanie logowania jednokrotnego i dostosowywania tokenu z niestandardowych zasad | Dokumentacja firmy Microsoft"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="4c425-102">Usługa Azure Active Directory B2C: Zarządzanie logowania jednokrotnego i tokenu możliwości dostosowania za pomocą zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="4c425-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="4c425-103">Za pomocą niestandardowych zasad zapewnia hello tego samego kontrolę nad token, sesjami i jednej konfiguracji logowania jednokrotnego (SSO) jako za pomocą wbudowanych zasad.</span><span class="sxs-lookup"><span data-stu-id="4c425-103">Using custom policies provides you hello same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="4c425-104">toolearn jest każdego ustawienia, zobacz dokumentację hello [tutaj](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="4c425-104">toolearn what each setting does, please see hello documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="4c425-105">Token konfiguracji okresy istnienia i oświadczenia</span><span class="sxs-lookup"><span data-stu-id="4c425-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="4c425-106">Ustawienia hello toochange na Twojego tokenu okresy istnienia, należy tooadd `<ClaimsProviders>` elementu w pliku jednostki uzależnionej strony hello zasad hello ma tooimpact.</span><span class="sxs-lookup"><span data-stu-id="4c425-106">toochange hello settings on your token lifetimes, you need tooadd a `<ClaimsProviders>` element in hello relying party file of hello policy you want tooimpact.</span></span>  <span data-ttu-id="4c425-107">Witaj `<ClaimsProviders>` element jest elementem podrzędnym hello `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="4c425-107">hello `<ClaimsProviders>` element is a child of hello `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="4c425-108">Wewnątrz należy tooput hello informacje, które ma wpływ na Twoje istnienia tokenu.</span><span class="sxs-lookup"><span data-stu-id="4c425-108">Inside you'll need tooput hello information that affects your token lifetimes.</span></span>  <span data-ttu-id="4c425-109">Witaj XML wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4c425-109">hello XML looks like this:</span></span>

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

<span data-ttu-id="4c425-110">**Okresy istnienia tokenu dostępu** hello dostępu okres istnienia tokenu można zmienić, modyfikując wartość hello wewnątrz hello `<Item>` z hello Key = "token_lifetime_secs" w sekundach.</span><span class="sxs-lookup"><span data-stu-id="4c425-110">**Access token lifetimes** hello access token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="4c425-111">Wartość domyślna Hello w wbudowane to 3600 sekund (60 minut).</span><span class="sxs-lookup"><span data-stu-id="4c425-111">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="4c425-112">**Okres istnienia tokenu identyfikator** okres istnienia tokenu identyfikator hello można zmienić, modyfikując wartość hello wewnątrz hello `<Item>` z hello Key = "id_token_lifetime_secs" w sekundach.</span><span class="sxs-lookup"><span data-stu-id="4c425-112">**ID token lifetime** hello ID token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="4c425-113">Wartość domyślna Hello w wbudowane to 3600 sekund (60 minut).</span><span class="sxs-lookup"><span data-stu-id="4c425-113">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="4c425-114">**Okres istnienia tokenu odświeżania** okres istnienia tokenu odświeżania hello można zmienić, modyfikując wartość hello wewnątrz hello `<Item>` z hello Key = "refresh_token_lifetime_secs" w sekundach.</span><span class="sxs-lookup"><span data-stu-id="4c425-114">**Refresh token lifetime** hello refresh token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="4c425-115">Wartość domyślna Hello w wbudowane to 1209600 sekund (14 dni).</span><span class="sxs-lookup"><span data-stu-id="4c425-115">hello default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="4c425-116">**Odśwież okres istnienia tokenu przesuwanego okna** Jeśli chcesz tooset token odświeżania tooyour okres istnienia w usłudze przesuwanego okna, zmodyfikuj wartość hello wewnątrz `<Item>` z hello Key = "rolling_refresh_token_lifetime_secs" w sekundach.</span><span class="sxs-lookup"><span data-stu-id="4c425-116">**Refresh token sliding window lifetime** If you would like tooset a sliding window lifetime tooyour refresh token, modify hello value inside `<Item>` with hello Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="4c425-117">Wartość domyślna Hello w wbudowane to 7776000 (90 dni).</span><span class="sxs-lookup"><span data-stu-id="4c425-117">hello default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="4c425-118">Jeśli nie chcesz tooenfore przedłużanie okres istnienia okna, Zastąp ten wiersz:</span><span class="sxs-lookup"><span data-stu-id="4c425-118">If you don't want tooenfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="4c425-119">**Oświadczenia wystawcy (iss)** toochange Witaj wystawca (iss) oświadczenia, zmodyfikuj wartość hello wewnątrz hello `<Item>` z hello Key = "IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="4c425-119">**Issuer (iss) claim** If you want toochange hello Issuer (iss) claim, modify hello value inside hello `<Item>` with hello Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="4c425-120">są stosowane wartości Hello `AuthorityAndTenantGuid` i `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="4c425-120">hello applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="4c425-121">**Ustawienie oświadczeń reprezentujący identyfikator zasad** opcje hello ustawienie tej wartości to TFP (zasady zaufania framework) i ACR (odwołanie w kontekście uwierzytelniania).</span><span class="sxs-lookup"><span data-stu-id="4c425-121">**Setting claim representing policy ID** hello options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="4c425-122">Firma Microsoft zaleca ustawienie to tooTFP toodo, upewnij się, hello `<Item>` z hello Key = "AuthenticationContextReferenceClaimPattern" istnieje i jest wartość hello `None`.</span><span class="sxs-lookup"><span data-stu-id="4c425-122">We recommend setting this tooTFP, toodo this, ensure hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern" exists and hello value is `None`.</span></span>
<span data-ttu-id="4c425-123">W Twojej `<OutputClaims>` elementu, należy dodać tego elementu:</span><span class="sxs-lookup"><span data-stu-id="4c425-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="4c425-124">Dla ACR, Usuń hello `<Item>` z hello Key = "AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="4c425-124">For ACR, remove hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="4c425-125">**Oświadczenia podmiotu (sub)** ta opcja jest domyślnie tooObjectID, jeśli chcesz tooswitch to zbyt`Not Supported`, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="4c425-125">**Subject (sub) claim** This option is defaulted tooObjectID, if you would like tooswitch this too`Not Supported`, do hello following:</span></span>

<span data-ttu-id="4c425-126">Zastąp ten wiersz</span><span class="sxs-lookup"><span data-stu-id="4c425-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="4c425-127">w tym:</span><span class="sxs-lookup"><span data-stu-id="4c425-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="4c425-128">Zachowanie sesji i logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="4c425-128">Session behavior and SSO</span></span>
<span data-ttu-id="4c425-129">toochange konfiguracji logowania jednokrotnego i zachowanie sesji, na których należy tooadd `<UserJourneyBehaviors>` element wewnątrz hello `<RelyingParty>` elementu.</span><span class="sxs-lookup"><span data-stu-id="4c425-129">toochange your session behavior and SSO configurations, you need tooadd a `<UserJourneyBehaviors>` element inside of hello `<RelyingParty>` element.</span></span>  <span data-ttu-id="4c425-130">Witaj `<UserJourneyBehaviors>` elementu musi występować zaraz po hello `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="4c425-130">hello `<UserJourneyBehaviors>` element must immediately follow hello `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="4c425-131">Witaj w Twojej `<UserJourneyBehavors>` element powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="4c425-131">hello inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="4c425-132">**Konfiguracja rejestracji jednokrotnej (SSO)** toochange hello jednej logowania jednokrotnego konfiguracji, należy wartość hello toomodify `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="4c425-132">**Single sign-on (SSO) configuration** toochange hello single sign-on configuration, you need toomodify hello value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="4c425-133">są stosowane wartości Hello `Tenant`, `Application`, `Policy` i `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="4c425-133">hello applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="4c425-134">**Aplikacja sieci Web okres istnienia sesji (w minutach)** aplikacji sieci web hello hello toochange okres istnienia sesji, należy toomodify wartość hello `<SessionExpiryInSeconds>` elementu.</span><span class="sxs-lookup"><span data-stu-id="4c425-134">**Web app session lifetime (minutes)** toochange hello hello web app session lifetime, you need toomodify value of hello `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="4c425-135">Wartość domyślna Hello w wbudowane zasady to 86400 sekund (1440 minut).</span><span class="sxs-lookup"><span data-stu-id="4c425-135">hello default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="4c425-136">**Limit czasu sesji aplikacji sieci Web** toochange hello sieci web aplikacji limit czasu sesji, należy wartość hello toomodify `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="4c425-136">**Web app session timeout** toochange hello web app session timeout, you need toomodify hello value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="4c425-137">są stosowane wartości Hello `Absolute` i `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="4c425-137">hello applicable values are `Absolute` and `Rolling`.</span></span>
