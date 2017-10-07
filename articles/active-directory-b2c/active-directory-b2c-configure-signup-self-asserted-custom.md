---
title: "Usługa Azure Active Directory B2C: Zmodyfikować logowania się w zasadach niestandardowych i skonfigurować własny potwierdzone dostawcy"
description: "Wskazówki dotyczące dodawania oświadczeń toosign się i skonfigurować hello dane wejściowe użytkownika"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: tbd
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/29/2017
ms.author: joroja
ms.openlocfilehash: c31d737263fef3e771bdf451b809b0ca522c8fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a>Usługa Azure Active Directory B2C: Zmodyfikuj rejestracji tooadd nowych oświadczeń i skonfigurować dane wejściowe użytkownika.

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

W tym artykule spowoduje dodanie nowego podane przez użytkownika wpis (oświadczenie) tooyour rejestracja użytkownika podróży.  Skonfigurujesz hello wpis jako listy rozwijanej i umożliwia określenie, czy jest to wymagane.

Edytowany przez Sipi tootrigger testu przekazaniem.

## <a name="prerequisites"></a>Wymagania wstępne

* Hello pełną kroki opisane w artykule hello [wprowadzenie zasady niestandardowe](active-directory-b2c-get-started-custom.md).  Przetestuj hello signup/logowanie użytkownika podróży toosignup nowego konta lokalnego, przed kontynuowaniem.


Gromadzenia danych początkowych z użytkowników odbywa się za pośrednictwem signup/signin.  Dodatkowe oświadczenia można zbierać później za pomocą podróże użytkownika edycji profilu. W dowolnym momencie usługi Azure AD B2C interaktywnie zbiera informacje bezpośrednio z hello użytkownika, hello Framework obsługi tożsamości używa jej `selfasserted provider`. Poniższe kroki Hello mają zastosowanie w dowolnym momencie ten dostawca jest używany.


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a>Zdefiniuj hello oświadczenia, jego nazwa wyświetlana i hello typu danych wprowadzonych przez użytkownika
Umożliwia poprosić użytkownika hello ich miastu.  Dodaj hello następującego elementu toohello `<ClaimsSchema>` elementu w pliku zasad TrustFrameWorkExtensions hello:

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
Dostępne są dodatkowe opcje, które możesz wprowadzić tutaj hello toocustomize oświadczeń.  Pełny schemat, można znaleźć w temacie toohello **tożsamości środowiska Framework techniczne podręcznik**.  W tym przewodniku wkrótce zostaną opublikowane w sekcji odwołania hello.

* `<DisplayName>`ciąg, który definiuje uwzględniającym działania użytkownika hello jest *etykiety*

* `<UserHelpText>`pomaga użytkownika hello Poznaj, co jest wymagane

* `<UserInputType>`Witaj następujących opcji ujawniło poniżej:
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * `RadioSingleSelectduration`-Wymusza pojedynczego wyboru.
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

    * `DropdownSingleSelect`— Umożliwia wybór hello tylko prawidłowe wartości.

![Zrzut ekranu opcji listy rozwijanej](./media/active-directory-b2c-configure-signup-self-asserted-custom/dropdown-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```


* `CheckboxMultiSelect`Umożliwia wybór hello co najmniej jedną wartość.

![Zrzut ekranu opcji wyboru wielokrotnego](./media/active-directory-b2c-configure-signup-self-asserted-custom/multiselect-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>Receive updates from which cities?</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a>Dodaj znak toohello oświadczeń hello w górę/znak w podróży użytkownika

1. Dodaj oświadczenie hello jako `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (które można znaleźć w pliku zasad TrustFrameworkBase hello).  Należy zauważyć, że ta TechnicalProfile używa hello SelfAssertedAttributeProvider.

  ```xml
  <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
    <DisplayName>Email signup</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
      <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
      <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
      <Item Key="language.button_continue">Create</Item>
    </Metadata>
    <CryptographicKeys>
      <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
    </CryptographicKeys>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
      <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" />
      <OutputClaim ClaimTypeReferenceId="newUser" />
      <!-- Optional claims, toobe collected from hello user -->
      <OutputClaim ClaimTypeReferenceId="givenName" />
      <OutputClaim ClaimTypeReferenceId="surName" />
      <OutputClaim ClaimTypeReferenceId="city"/>
    </OutputClaims>
    <ValidationTechnicalProfiles>
      <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
    </ValidationTechnicalProfiles>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

2. Dodaj hello oświadczeń toohello AAD UserWriteUsingLogonEmail jako `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello oświadczeń toohello AAD katalogu po zebraniu go z hello użytkownika. Jeśli wolisz nie toopersist hello oświadczeń w katalogu hello do użytku w przyszłości może pominąć ten krok.

  ```xml
  <!-- Technical profiles for local accounts -->
  <TechnicalProfile Id="AAD-UserWriteUsingLogonEmail">
    <Metadata>
      <Item Key="Operation">Write</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" Required="true" />
    </InputClaims>
    <PersistedClaims>
      <!-- Required claims -->
      <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
      <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password" />
      <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
      <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />
      <!-- Optional claims. -->
      <PersistedClaim ClaimTypeReferenceId="givenName" />
      <PersistedClaim ClaimTypeReferenceId="surname" />
      <PersistedClaim ClaimTypeReferenceId="city" />
    </PersistedClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

3. Dodaj hello oświadczeń toohello TechnicalProfile odczytująca hello katalogu, gdy użytkownik zaloguje się jako`<OutputClaim ClaimTypeReferenceId="city" />`

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for hello provided user ID.</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames" Required="true" />
    </InputClaims>
    <OutputClaims>
      <!-- Required claims -->
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <!-- Optional claims -->
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="displayName" />
      <OutputClaim ClaimTypeReferenceId="otherMails" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  </TechnicalProfile>
  ```

4. Dodaj hello `<OutputClaim ClaimTypeReferenceId="city" />` pliku zasad RP toohello SignUporSignIn.xml tak tego oświadczenia wysyłane toohello aplikacji hello token po przebieg użytkownika powiodło się.

  ```xml
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="city" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ```

## <a name="test-hello-custom-policy-using-run-now"></a>Zasady niestandardowe hello testu przy użyciu "opcji Uruchom teraz"

1. Otwórz hello **bloku usługi Azure AD B2C** i przejdź zbyt**tożsamości środowiska Framework > zasady niestandardowe**.
2. Wybierz zasady niestandardowe hello, który został przekazany, a następnie kliknij przycisk hello **Uruchom teraz** przycisku.
3. Powinno być możliwe toosign przy użyciu adresu e-mail.

ekran rejestracji Hello w trybie testowym powinien wyglądać podobnie toothis:

![Zrzut ekranu przedstawiający zmodyfikowane opcją](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  Witaj tooyour tyłu tokenu aplikacji będzie zawierają teraz hello `city` oświadczenia, jak pokazano poniżej
```json
{
  "exp": 1493596822,
  "nbf": 1493593222,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "9c2a3a9e-ac65-4e46-a12d-9557b63033a9",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustf_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1493593222,
  "auth_time": 1493593222,
  "email": "joe@outlook.com",
  "given_name": "Joe",
  "family_name": "Ras",
  "city": "Bellevue",
  "name": "unknown"
}
```

## <a name="optional-remove-email-verification-from-signup-journey"></a>Opcjonalnie: Usuń e-mail weryfikacji w podróży rejestracji

Weryfikacja adresu e-mail tooskip, hello autor zasad można wybrać tooremove `PartnerClaimType="Verified.Email"`. Witaj adres e-mail zostanie wymagane, ale nie zweryfikowane, chyba że "Wymagane" = true zostanie usunięta.  Należy rozważyć, jeśli ta opcja jest odpowiednia dla Twojej przypadki użycia!

Zweryfikować adres e-mail jest domyślnie włączone w hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` w pliku zasad TrustFrameworkBase hello w pakiecie starter hello:
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a>Następne kroki

Dodaj hello nowe oświadczenie toohello przepływów społecznościowych konta logowania, zmieniając powitalne TechnicalProfiles wymienionych poniżej. Są używane przez toowrite logowania do konta społecznego/federacyjnych i odczytywania danych użytkowników hello przy użyciu hello alternativeSecurityId hello lokalizatora.
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
