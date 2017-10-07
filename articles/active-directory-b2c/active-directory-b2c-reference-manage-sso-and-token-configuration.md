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
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Usługa Azure Active Directory B2C: Zarządzanie logowania jednokrotnego i tokenu możliwości dostosowania za pomocą zasad niestandardowych
Za pomocą niestandardowych zasad zapewnia hello tego samego kontrolę nad token, sesjami i jednej konfiguracji logowania jednokrotnego (SSO) jako za pomocą wbudowanych zasad.  toolearn jest każdego ustawienia, zobacz dokumentację hello [tutaj](#active-directory-b2c-token-session-sso).

## <a name="token-lifetimes-and-claims-configuration"></a>Token konfiguracji okresy istnienia i oświadczenia
Ustawienia hello toochange na Twojego tokenu okresy istnienia, należy tooadd `<ClaimsProviders>` elementu w pliku jednostki uzależnionej strony hello zasad hello ma tooimpact.  Witaj `<ClaimsProviders>` element jest elementem podrzędnym hello `<TrustFrameworkPolicy>`.  Wewnątrz należy tooput hello informacje, które ma wpływ na Twoje istnienia tokenu.  Witaj XML wygląda następująco:

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

**Okresy istnienia tokenu dostępu** hello dostępu okres istnienia tokenu można zmienić, modyfikując wartość hello wewnątrz hello `<Item>` z hello Key = "token_lifetime_secs" w sekundach.  Wartość domyślna Hello w wbudowane to 3600 sekund (60 minut).

**Okres istnienia tokenu identyfikator** okres istnienia tokenu identyfikator hello można zmienić, modyfikując wartość hello wewnątrz hello `<Item>` z hello Key = "id_token_lifetime_secs" w sekundach.  Wartość domyślna Hello w wbudowane to 3600 sekund (60 minut).

**Okres istnienia tokenu odświeżania** okres istnienia tokenu odświeżania hello można zmienić, modyfikując wartość hello wewnątrz hello `<Item>` z hello Key = "refresh_token_lifetime_secs" w sekundach.  Wartość domyślna Hello w wbudowane to 1209600 sekund (14 dni).

**Odśwież okres istnienia tokenu przesuwanego okna** Jeśli chcesz tooset token odświeżania tooyour okres istnienia w usłudze przesuwanego okna, zmodyfikuj wartość hello wewnątrz `<Item>` z hello Key = "rolling_refresh_token_lifetime_secs" w sekundach.  Wartość domyślna Hello w wbudowane to 7776000 (90 dni).  Jeśli nie chcesz tooenfore przedłużanie okres istnienia okna, Zastąp ten wiersz:
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**Oświadczenia wystawcy (iss)** toochange Witaj wystawca (iss) oświadczenia, zmodyfikuj wartość hello wewnątrz hello `<Item>` z hello Key = "IssuanceClaimPattern".  są stosowane wartości Hello `AuthorityAndTenantGuid` i `AuthorityWithTfp`.

**Ustawienie oświadczeń reprezentujący identyfikator zasad** opcje hello ustawienie tej wartości to TFP (zasady zaufania framework) i ACR (odwołanie w kontekście uwierzytelniania).  
Firma Microsoft zaleca ustawienie to tooTFP toodo, upewnij się, hello `<Item>` z hello Key = "AuthenticationContextReferenceClaimPattern" istnieje i jest wartość hello `None`.
W Twojej `<OutputClaims>` elementu, należy dodać tego elementu:
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
Dla ACR, Usuń hello `<Item>` z hello Key = "AuthenticationContextReferenceClaimPattern".

**Oświadczenia podmiotu (sub)** ta opcja jest domyślnie tooObjectID, jeśli chcesz tooswitch to zbyt`Not Supported`, hello następujące:

Zastąp ten wiersz 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
w tym:
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>Zachowanie sesji i logowania jednokrotnego
toochange konfiguracji logowania jednokrotnego i zachowanie sesji, na których należy tooadd `<UserJourneyBehaviors>` element wewnątrz hello `<RelyingParty>` elementu.  Witaj `<UserJourneyBehaviors>` elementu musi występować zaraz po hello `<DefaultUserJourney>`.  Witaj w Twojej `<UserJourneyBehavors>` element powinien wyglądać następująco:

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Konfiguracja rejestracji jednokrotnej (SSO)** toochange hello jednej logowania jednokrotnego konfiguracji, należy wartość hello toomodify `<SingleSignOn>`.  są stosowane wartości Hello `Tenant`, `Application`, `Policy` i `Disabled`. 

**Aplikacja sieci Web okres istnienia sesji (w minutach)** aplikacji sieci web hello hello toochange okres istnienia sesji, należy toomodify wartość hello `<SessionExpiryInSeconds>` elementu.  Wartość domyślna Hello w wbudowane zasady to 86400 sekund (1440 minut).

**Limit czasu sesji aplikacji sieci Web** toochange hello sieci web aplikacji limit czasu sesji, należy wartość hello toomodify `<SessionExpiryType>`.  są stosowane wartości Hello `Absolute` i `Rolling`.
