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
ms.openlocfilehash: 8f5703d15766f221517cd89352d41685652d32d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="127cf-102">Usługa Azure Active Directory B2C: Zarządzanie logowania jednokrotnego i tokenu możliwości dostosowania za pomocą zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="127cf-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="127cf-103">Za pomocą niestandardowych zasad zapewnia kontrolę tego samego tokenu, sesjami i jednej konfiguracji logowania jednokrotnego (SSO) jako za pomocą wbudowanych zasad.</span><span class="sxs-lookup"><span data-stu-id="127cf-103">Using custom policies provides you the same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="127cf-104">Aby dowiedzieć się, co oznacza każdego ustawienia, można znaleźć w dokumentacji [tutaj](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="127cf-104">To learn what each setting does, please see the documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="127cf-105">Token konfiguracji okresy istnienia i oświadczenia</span><span class="sxs-lookup"><span data-stu-id="127cf-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="127cf-106">Aby zmienić ustawienia na Twojego tokenu okresy istnienia, musisz dodać `<ClaimsProviders>` elementu w pliku strony jednostki uzależnionej zasady będą miały wpływ.</span><span class="sxs-lookup"><span data-stu-id="127cf-106">To change the settings on your token lifetimes, you need to add a `<ClaimsProviders>` element in the relying party file of the policy you want to impact.</span></span>  <span data-ttu-id="127cf-107">`<ClaimsProviders>` Element jest elementem podrzędnym `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="127cf-107">The `<ClaimsProviders>` element is a child of the `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="127cf-108">Wewnątrz należy umieścić informacje, które ma wpływ na Twoje istnienia tokenu.</span><span class="sxs-lookup"><span data-stu-id="127cf-108">Inside you'll need to put the information that affects your token lifetimes.</span></span>  <span data-ttu-id="127cf-109">Plik XML wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="127cf-109">The XML looks like this:</span></span>

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

<span data-ttu-id="127cf-110">**Okresy istnienia tokenu dostępu** okres istnienia tokenu dostępu można zmienić, modyfikując wartość wewnątrz `<Item>` klucz = "token_lifetime_secs" w sekundach.</span><span class="sxs-lookup"><span data-stu-id="127cf-110">**Access token lifetimes** The access token lifetime can be changed by modifying the value inside the `<Item>` with the Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="127cf-111">Wartość domyślna w wbudowane to 3600 sekund (60 minut).</span><span class="sxs-lookup"><span data-stu-id="127cf-111">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="127cf-112">**Okres istnienia tokenu identyfikator** identyfikator okres istnienia tokenu można zmienić, modyfikując wartość wewnątrz `<Item>` klucz = "id_token_lifetime_secs" w sekundach.</span><span class="sxs-lookup"><span data-stu-id="127cf-112">**ID token lifetime** The ID token lifetime can be changed by modifying the value inside the `<Item>` with the Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="127cf-113">Wartość domyślna w wbudowane to 3600 sekund (60 minut).</span><span class="sxs-lookup"><span data-stu-id="127cf-113">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="127cf-114">**Okres istnienia tokenu odświeżania** okres istnienia tokenu odświeżania można zmienić, modyfikując wartość wewnątrz `<Item>` klucz = "refresh_token_lifetime_secs" w sekundach.</span><span class="sxs-lookup"><span data-stu-id="127cf-114">**Refresh token lifetime** The refresh token lifetime can be changed by modifying the value inside the `<Item>` with the Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="127cf-115">Wartość domyślna w wbudowane to 1209600 sekund (14 dni).</span><span class="sxs-lookup"><span data-stu-id="127cf-115">The default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="127cf-116">**Odśwież okres istnienia tokenu przesuwanego okna** Jeśli chcesz ustawić zmienną okres istnienia okna token odświeżania, zmodyfikuj wartość wewnątrz `<Item>` klucz = "rolling_refresh_token_lifetime_secs" w sekundach.</span><span class="sxs-lookup"><span data-stu-id="127cf-116">**Refresh token sliding window lifetime** If you would like to set a sliding window lifetime to your refresh token, modify the value inside `<Item>` with the Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="127cf-117">Wartość domyślna w wbudowane to 7776000 (90 dni).</span><span class="sxs-lookup"><span data-stu-id="127cf-117">The default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="127cf-118">Jeśli nie chcesz enfore przesuwania okres istnienia okna, Zastąp ten wiersz:</span><span class="sxs-lookup"><span data-stu-id="127cf-118">If you don't want to enfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="127cf-119">**Oświadczenia wystawcy (iss)** Jeśli chcesz zmienić oświadczenia wystawcy (iss), zmodyfikuj wartość w `<Item>` z kluczem = "IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="127cf-119">**Issuer (iss) claim** If you want to change the Issuer (iss) claim, modify the value inside the `<Item>` with the Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="127cf-120">Są stosowane wartości `AuthorityAndTenantGuid` i `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="127cf-120">The applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="127cf-121">**Ustawienie oświadczeń reprezentujący identyfikator zasad** opcje ustawienie tej wartości są TFP (zasady zaufania framework) i ACR (odwołanie w kontekście uwierzytelniania).</span><span class="sxs-lookup"><span data-stu-id="127cf-121">**Setting claim representing policy ID** The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="127cf-122">Zalecamy skonfigurowanie w tym TFP, aby to zrobić, upewnij się, `<Item>` z Key = "AuthenticationContextReferenceClaimPattern" istnieje, a wartość to `None`.</span><span class="sxs-lookup"><span data-stu-id="127cf-122">We recommend setting this to TFP, to do this, ensure the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern" exists and the value is `None`.</span></span>
<span data-ttu-id="127cf-123">W Twojej `<OutputClaims>` elementu, należy dodać tego elementu:</span><span class="sxs-lookup"><span data-stu-id="127cf-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="127cf-124">W przypadku ACR, usunąć `<Item>` klucz = "AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="127cf-124">For ACR, remove the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="127cf-125">**Oświadczenia podmiotu (sub)** ta opcja jest ustawiana domyślnie ObjectID, jeśli chcesz przełączyć się na `Not Supported`, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="127cf-125">**Subject (sub) claim** This option is defaulted to ObjectID, if you would like to switch this to `Not Supported`, do the following:</span></span>

<span data-ttu-id="127cf-126">Zastąp ten wiersz</span><span class="sxs-lookup"><span data-stu-id="127cf-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="127cf-127">w tym:</span><span class="sxs-lookup"><span data-stu-id="127cf-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="127cf-128">Zachowanie sesji i logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="127cf-128">Session behavior and SSO</span></span>
<span data-ttu-id="127cf-129">Aby zmienić zachowanie sesji i konfiguracje logowania jednokrotnego, musisz dodać `<UserJourneyBehaviors>` wewnątrz elementu `<RelyingParty>` elementu.</span><span class="sxs-lookup"><span data-stu-id="127cf-129">To change your session behavior and SSO configurations, you need to add a `<UserJourneyBehaviors>` element inside of the `<RelyingParty>` element.</span></span>  <span data-ttu-id="127cf-130">`<UserJourneyBehaviors>` Elementu musi występować zaraz po `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="127cf-130">The `<UserJourneyBehaviors>` element must immediately follow the `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="127cf-131">Wewnątrz sieci `<UserJourneyBehavors>` element powinien wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="127cf-131">The inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="127cf-132">**Konfiguracja rejestracji jednokrotnej (SSO)** do zmiany konfiguracji pojedynczego logowania, należy zmodyfikować wartość `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="127cf-132">**Single sign-on (SSO) configuration** To change the single sign-on configuration, you need to modify the value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="127cf-133">Są stosowane wartości `Tenant`, `Application`, `Policy` i `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="127cf-133">The applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="127cf-134">**Aplikacja sieci Web okres istnienia sesji (w minutach)** zmienić aplikacji sieci web okres istnienia sesji, należy zmodyfikować wartość `<SessionExpiryInSeconds>` elementu.</span><span class="sxs-lookup"><span data-stu-id="127cf-134">**Web app session lifetime (minutes)** To change the the web app session lifetime, you need to modify value of the `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="127cf-135">Wartość domyślna w ramach zasad wbudowany to 86400 sekund (1440 minut).</span><span class="sxs-lookup"><span data-stu-id="127cf-135">The default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="127cf-136">**Limit czasu sesji aplikacji sieci Web** Aby zmienić limit czasu sesji dla aplikacji sieci web, należy zmodyfikować wartość `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="127cf-136">**Web app session timeout** To change the web app session timeout, you need to modify the value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="127cf-137">Są stosowane wartości `Absolute` i `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="127cf-137">The applicable values are `Absolute` and `Rolling`.</span></span>
