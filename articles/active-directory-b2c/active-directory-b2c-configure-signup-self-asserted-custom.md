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
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a><span data-ttu-id="65256-103">Usługa Azure Active Directory B2C: Zmodyfikuj rejestracji tooadd nowych oświadczeń i skonfigurować dane wejściowe użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65256-103">Azure Active Directory B2C: Modify sign up tooadd new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="65256-104">W tym artykule spowoduje dodanie nowego podane przez użytkownika wpis (oświadczenie) tooyour rejestracja użytkownika podróży.</span><span class="sxs-lookup"><span data-stu-id="65256-104">In this article, you will add a new user provided entry (a claim) tooyour signup user journey.</span></span>  <span data-ttu-id="65256-105">Skonfigurujesz hello wpis jako listy rozwijanej i umożliwia określenie, czy jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="65256-105">You will configure hello entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="65256-106">Edytowany przez Sipi tootrigger testu przekazaniem.</span><span class="sxs-lookup"><span data-stu-id="65256-106">Edited by Sipi tootrigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65256-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="65256-107">Prerequisites</span></span>

* <span data-ttu-id="65256-108">Hello pełną kroki opisane w artykule hello [wprowadzenie zasady niestandardowe](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="65256-108">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="65256-109">Przetestuj hello signup/logowanie użytkownika podróży toosignup nowego konta lokalnego, przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="65256-109">Test hello signup/signin user journey toosignup a new local account before proceeding.</span></span>


<span data-ttu-id="65256-110">Gromadzenia danych początkowych z użytkowników odbywa się za pośrednictwem signup/signin.</span><span class="sxs-lookup"><span data-stu-id="65256-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="65256-111">Dodatkowe oświadczenia można zbierać później za pomocą podróże użytkownika edycji profilu.</span><span class="sxs-lookup"><span data-stu-id="65256-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="65256-112">W dowolnym momencie usługi Azure AD B2C interaktywnie zbiera informacje bezpośrednio z hello użytkownika, hello Framework obsługi tożsamości używa jej `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="65256-112">Anytime Azure AD B2C gathers information directly from hello user interactively, hello Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="65256-113">Poniższe kroki Hello mają zastosowanie w dowolnym momencie ten dostawca jest używany.</span><span class="sxs-lookup"><span data-stu-id="65256-113">hello steps below apply anytime this provider is used.</span></span>


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a><span data-ttu-id="65256-114">Zdefiniuj hello oświadczenia, jego nazwa wyświetlana i hello typu danych wprowadzonych przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="65256-114">Define hello claim, its display name and hello user input type</span></span>
<span data-ttu-id="65256-115">Umożliwia poprosić użytkownika hello ich miastu.</span><span class="sxs-lookup"><span data-stu-id="65256-115">Lets ask hello user for their city.</span></span>  <span data-ttu-id="65256-116">Dodaj hello następującego elementu toohello `<ClaimsSchema>` elementu w pliku zasad TrustFrameWorkExtensions hello:</span><span class="sxs-lookup"><span data-stu-id="65256-116">Add hello following element toohello `<ClaimsSchema>` element in hello TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="65256-117">Dostępne są dodatkowe opcje, które możesz wprowadzić tutaj hello toocustomize oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="65256-117">There are additional choices you can make here toocustomize hello claim.</span></span>  <span data-ttu-id="65256-118">Pełny schemat, można znaleźć w temacie toohello **tożsamości środowiska Framework techniczne podręcznik**.</span><span class="sxs-lookup"><span data-stu-id="65256-118">For a full schema, refer toohello **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="65256-119">W tym przewodniku wkrótce zostaną opublikowane w sekcji odwołania hello.</span><span class="sxs-lookup"><span data-stu-id="65256-119">This guide will be published soon in hello reference section.</span></span>

* <span data-ttu-id="65256-120">`<DisplayName>`ciąg, który definiuje uwzględniającym działania użytkownika hello jest *etykiety*</span><span class="sxs-lookup"><span data-stu-id="65256-120">`<DisplayName>` is a string that defines hello user-facing *label*</span></span>

* <span data-ttu-id="65256-121">`<UserHelpText>`pomaga użytkownika hello Poznaj, co jest wymagane</span><span class="sxs-lookup"><span data-stu-id="65256-121">`<UserHelpText>` helps hello user understand what is required</span></span>

* <span data-ttu-id="65256-122">`<UserInputType>`Witaj następujących opcji ujawniło poniżej:</span><span class="sxs-lookup"><span data-stu-id="65256-122">`<UserInputType>` has hello following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="65256-123">`RadioSingleSelectduration`-Wymusza pojedynczego wyboru.</span><span class="sxs-lookup"><span data-stu-id="65256-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
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

    * <span data-ttu-id="65256-124">`DropdownSingleSelect`— Umożliwia wybór hello tylko prawidłowe wartości.</span><span class="sxs-lookup"><span data-stu-id="65256-124">`DropdownSingleSelect` - Allows hello selection of only valid value.</span></span>

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


* <span data-ttu-id="65256-126">`CheckboxMultiSelect`Umożliwia wybór hello co najmniej jedną wartość.</span><span class="sxs-lookup"><span data-stu-id="65256-126">`CheckboxMultiSelect` Allows for hello selection of one or more values.</span></span>

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

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a><span data-ttu-id="65256-128">Dodaj znak toohello oświadczeń hello w górę/znak w podróży użytkownika</span><span class="sxs-lookup"><span data-stu-id="65256-128">Add hello claim toohello sign up/sign in user journey</span></span>

1. <span data-ttu-id="65256-129">Dodaj oświadczenie hello jako `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (które można znaleźć w pliku zasad TrustFrameworkBase hello).</span><span class="sxs-lookup"><span data-stu-id="65256-129">Add hello claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in hello TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="65256-130">Należy zauważyć, że ta TechnicalProfile używa hello SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="65256-130">Note this TechnicalProfile uses hello SelfAssertedAttributeProvider.</span></span>

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

2. <span data-ttu-id="65256-131">Dodaj hello oświadczeń toohello AAD UserWriteUsingLogonEmail jako `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello oświadczeń toohello AAD katalogu po zebraniu go z hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="65256-131">Add hello claim toohello AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello claim toohello AAD directory after collecting it from hello user.</span></span> <span data-ttu-id="65256-132">Jeśli wolisz nie toopersist hello oświadczeń w katalogu hello do użytku w przyszłości może pominąć ten krok.</span><span class="sxs-lookup"><span data-stu-id="65256-132">You may skip this step if you prefer not toopersist hello claim in hello directory for future use.</span></span>

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

3. <span data-ttu-id="65256-133">Dodaj hello oświadczeń toohello TechnicalProfile odczytująca hello katalogu, gdy użytkownik zaloguje się jako`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="65256-133">Add hello claim toohello TechnicalProfile that reads from hello directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

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

4. <span data-ttu-id="65256-134">Dodaj hello `<OutputClaim ClaimTypeReferenceId="city" />` pliku zasad RP toohello SignUporSignIn.xml tak tego oświadczenia wysyłane toohello aplikacji hello token po przebieg użytkownika powiodło się.</span><span class="sxs-lookup"><span data-stu-id="65256-134">Add hello `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP policy file SignUporSignIn.xml so this claim is sent toohello application in hello token after a successful user journey.</span></span>

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

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="65256-135">Zasady niestandardowe hello testu przy użyciu "opcji Uruchom teraz"</span><span class="sxs-lookup"><span data-stu-id="65256-135">Test hello custom policy using "Run Now"</span></span>

1. <span data-ttu-id="65256-136">Otwórz hello **bloku usługi Azure AD B2C** i przejdź zbyt**tożsamości środowiska Framework > zasady niestandardowe**.</span><span class="sxs-lookup"><span data-stu-id="65256-136">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="65256-137">Wybierz zasady niestandardowe hello, który został przekazany, a następnie kliknij przycisk hello **Uruchom teraz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="65256-137">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="65256-138">Powinno być możliwe toosign przy użyciu adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="65256-138">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="65256-139">ekran rejestracji Hello w trybie testowym powinien wyglądać podobnie toothis:</span><span class="sxs-lookup"><span data-stu-id="65256-139">hello signup screen in test mode should look similar toothis:</span></span>

![Zrzut ekranu przedstawiający zmodyfikowane opcją](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="65256-141">Witaj tooyour tyłu tokenu aplikacji będzie zawierają teraz hello `city` oświadczenia, jak pokazano poniżej</span><span class="sxs-lookup"><span data-stu-id="65256-141">hello token back tooyour application will now include hello `city` claim as shown below</span></span>
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

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="65256-142">Opcjonalnie: Usuń e-mail weryfikacji w podróży rejestracji</span><span class="sxs-lookup"><span data-stu-id="65256-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="65256-143">Weryfikacja adresu e-mail tooskip, hello autor zasad można wybrać tooremove `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="65256-143">tooskip email verification, hello policy author can choose tooremove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="65256-144">Witaj adres e-mail zostanie wymagane, ale nie zweryfikowane, chyba że "Wymagane" = true zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="65256-144">hello email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="65256-145">Należy rozważyć, jeśli ta opcja jest odpowiednia dla Twojej przypadki użycia!</span><span class="sxs-lookup"><span data-stu-id="65256-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="65256-146">Zweryfikować adres e-mail jest domyślnie włączone w hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` w pliku zasad TrustFrameworkBase hello w pakiecie starter hello:</span><span class="sxs-lookup"><span data-stu-id="65256-146">Verified email is enabled by default in hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in hello TrustFrameworkBase policy file in hello starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="65256-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65256-147">Next steps</span></span>

<span data-ttu-id="65256-148">Dodaj hello nowe oświadczenie toohello przepływów społecznościowych konta logowania, zmieniając powitalne TechnicalProfiles wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="65256-148">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed below.</span></span> <span data-ttu-id="65256-149">Są używane przez toowrite logowania do konta społecznego/federacyjnych i odczytywania danych użytkowników hello przy użyciu hello alternativeSecurityId hello lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="65256-149">These are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
