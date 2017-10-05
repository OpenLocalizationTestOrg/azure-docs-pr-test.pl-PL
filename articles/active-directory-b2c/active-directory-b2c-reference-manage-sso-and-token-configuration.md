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
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Usługa Azure Active Directory B2C: Zarządzanie logowania jednokrotnego i tokenu możliwości dostosowania za pomocą zasad niestandardowych
Za pomocą niestandardowych zasad zapewnia kontrolę tego samego tokenu, sesjami i jednej konfiguracji logowania jednokrotnego (SSO) jako za pomocą wbudowanych zasad.  Aby dowiedzieć się, co oznacza każdego ustawienia, można znaleźć w dokumentacji [tutaj](#active-directory-b2c-token-session-sso).

## <a name="token-lifetimes-and-claims-configuration"></a>Token konfiguracji okresy istnienia i oświadczenia
Aby zmienić ustawienia na Twojego tokenu okresy istnienia, musisz dodać `<ClaimsProviders>` elementu w pliku strony jednostki uzależnionej zasady będą miały wpływ.  `<ClaimsProviders>` Element jest elementem podrzędnym `<TrustFrameworkPolicy>`.  Wewnątrz należy umieścić informacje, które ma wpływ na Twoje istnienia tokenu.  Plik XML wygląda następująco:

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

**Okresy istnienia tokenu dostępu** okres istnienia tokenu dostępu można zmienić, modyfikując wartość wewnątrz `<Item>` klucz = "token_lifetime_secs" w sekundach.  Wartość domyślna w wbudowane to 3600 sekund (60 minut).

**Okres istnienia tokenu identyfikator** identyfikator okres istnienia tokenu można zmienić, modyfikując wartość wewnątrz `<Item>` klucz = "id_token_lifetime_secs" w sekundach.  Wartość domyślna w wbudowane to 3600 sekund (60 minut).

**Okres istnienia tokenu odświeżania** okres istnienia tokenu odświeżania można zmienić, modyfikując wartość wewnątrz `<Item>` klucz = "refresh_token_lifetime_secs" w sekundach.  Wartość domyślna w wbudowane to 1209600 sekund (14 dni).

**Odśwież okres istnienia tokenu przesuwanego okna** Jeśli chcesz ustawić zmienną okres istnienia okna token odświeżania, zmodyfikuj wartość wewnątrz `<Item>` klucz = "rolling_refresh_token_lifetime_secs" w sekundach.  Wartość domyślna w wbudowane to 7776000 (90 dni).  Jeśli nie chcesz enfore przesuwania okres istnienia okna, Zastąp ten wiersz:
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**Oświadczenia wystawcy (iss)** Jeśli chcesz zmienić oświadczenia wystawcy (iss), zmodyfikuj wartość w `<Item>` z kluczem = "IssuanceClaimPattern".  Są stosowane wartości `AuthorityAndTenantGuid` i `AuthorityWithTfp`.

**Ustawienie oświadczeń reprezentujący identyfikator zasad** opcje ustawienie tej wartości są TFP (zasady zaufania framework) i ACR (odwołanie w kontekście uwierzytelniania).  
Zalecamy skonfigurowanie w tym TFP, aby to zrobić, upewnij się, `<Item>` z Key = "AuthenticationContextReferenceClaimPattern" istnieje, a wartość to `None`.
W Twojej `<OutputClaims>` elementu, należy dodać tego elementu:
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
W przypadku ACR, usunąć `<Item>` klucz = "AuthenticationContextReferenceClaimPattern".

**Oświadczenia podmiotu (sub)** ta opcja jest ustawiana domyślnie ObjectID, jeśli chcesz przełączyć się na `Not Supported`, wykonaj następujące czynności:

Zastąp ten wiersz 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
w tym:
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>Zachowanie sesji i logowania jednokrotnego
Aby zmienić zachowanie sesji i konfiguracje logowania jednokrotnego, musisz dodać `<UserJourneyBehaviors>` wewnątrz elementu `<RelyingParty>` elementu.  `<UserJourneyBehaviors>` Elementu musi występować zaraz po `<DefaultUserJourney>`.  Wewnątrz sieci `<UserJourneyBehavors>` element powinien wyglądać następująco:

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Konfiguracja rejestracji jednokrotnej (SSO)** do zmiany konfiguracji pojedynczego logowania, należy zmodyfikować wartość `<SingleSignOn>`.  Są stosowane wartości `Tenant`, `Application`, `Policy` i `Disabled`. 

**Aplikacja sieci Web okres istnienia sesji (w minutach)** zmienić aplikacji sieci web okres istnienia sesji, należy zmodyfikować wartość `<SessionExpiryInSeconds>` elementu.  Wartość domyślna w ramach zasad wbudowany to 86400 sekund (1440 minut).

**Limit czasu sesji aplikacji sieci Web** Aby zmienić limit czasu sesji dla aplikacji sieci web, należy zmodyfikować wartość `<SessionExpiryType>`.  Są stosowane wartości `Absolute` i `Rolling`.
