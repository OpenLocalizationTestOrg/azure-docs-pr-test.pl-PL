---
title: "Usługa Azure Active Directory B2C: Zmodyfikować logowania się w zasadach niestandardowych i skonfigurować własny potwierdzone dostawcy"
description: "Wskazówki dotyczące dodawania oświadczeń utworzyć konto i skonfigurować dane wejściowe użytkownika"
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
ms.openlocfilehash: 64b9d904d7d070052e125b479f4719d208c9ff85
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/28/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-to-add-new-claims-and-configure-user-input"></a><span data-ttu-id="10d0c-103">Usługa Azure Active Directory B2C: Zmodyfikuj logowania się do dodawania nowych oświadczeń i skonfigurować dane wejściowe użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10d0c-103">Azure Active Directory B2C: Modify sign up to add new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="10d0c-104">W tym artykule nowy wpis podane przez użytkownika (oświadczenie) doda do zapisywania podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10d0c-104">In this article, you will add a new user provided entry (a claim) to your signup user journey.</span></span>  <span data-ttu-id="10d0c-105">Skonfigurujesz wpis jako listy rozwijanej i umożliwia określenie, czy jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="10d0c-105">You will configure the entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="10d0c-106">Edytowany przez Sipi do wyzwolenia przekazaniem testu.</span><span class="sxs-lookup"><span data-stu-id="10d0c-106">Edited by Sipi to trigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10d0c-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="10d0c-107">Prerequisites</span></span>

* <span data-ttu-id="10d0c-108">Wykonaj kroki w artykule [wprowadzenie zasady niestandardowe](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="10d0c-108">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="10d0c-109">Przetestuj podróży signup/logowanie użytkownika do zapisywania nowego konta lokalnego, przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="10d0c-109">Test the signup/signin user journey to signup a new local account before proceeding.</span></span>


<span data-ttu-id="10d0c-110">Gromadzenia danych początkowych z użytkowników odbywa się za pośrednictwem signup/signin.</span><span class="sxs-lookup"><span data-stu-id="10d0c-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="10d0c-111">Dodatkowe oświadczenia można zbierać później za pomocą podróże użytkownika edycji profilu.</span><span class="sxs-lookup"><span data-stu-id="10d0c-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="10d0c-112">Zastosowano w ramach obsługi tożsamości w dowolnym momencie usługi Azure AD B2C interaktywnie zbiera informacje bezpośrednio od użytkownika, jego `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="10d0c-112">Anytime Azure AD B2C gathers information directly from the user interactively, the Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="10d0c-113">Poniższe kroki mają zastosowanie w dowolnym momencie ten dostawca jest używany.</span><span class="sxs-lookup"><span data-stu-id="10d0c-113">The steps below apply anytime this provider is used.</span></span>


## <a name="define-the-claim-its-display-name-and-the-user-input-type"></a><span data-ttu-id="10d0c-114">Zdefiniuj oświadczenia, jego nazwa wyświetlana i typ danych wejściowych użytkownika</span><span class="sxs-lookup"><span data-stu-id="10d0c-114">Define the claim, its display name and the user input type</span></span>
<span data-ttu-id="10d0c-115">Umożliwia poprosić użytkownika o ich miasta.</span><span class="sxs-lookup"><span data-stu-id="10d0c-115">Lets ask the user for their city.</span></span>  <span data-ttu-id="10d0c-116">Dodaj następujący element do `<ClaimsSchema>` elementu w pliku zasad TrustFrameWorkExtensions:</span><span class="sxs-lookup"><span data-stu-id="10d0c-116">Add the following element to the `<ClaimsSchema>` element in the TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="10d0c-117">Dostępne są dodatkowe opcje, które można wprowadzać w tym miejscu dostosować oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="10d0c-117">There are additional choices you can make here to customize the claim.</span></span>  <span data-ttu-id="10d0c-118">Pełny schemat, można znaleźć w temacie **tożsamości środowiska Framework techniczne podręcznik**.</span><span class="sxs-lookup"><span data-stu-id="10d0c-118">For a full schema, refer to the **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="10d0c-119">W tym przewodniku wkrótce zostaną opublikowane zamieszczone w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="10d0c-119">This guide will be published soon in the reference section.</span></span>

* <span data-ttu-id="10d0c-120">`<DisplayName>`ciąg, który definiuje dla użytkownika jest *etykiety*</span><span class="sxs-lookup"><span data-stu-id="10d0c-120">`<DisplayName>` is a string that defines the user-facing *label*</span></span>

* <span data-ttu-id="10d0c-121">`<UserHelpText>`ułatwia użytkownikom zrozumienie, co jest wymagane</span><span class="sxs-lookup"><span data-stu-id="10d0c-121">`<UserHelpText>` helps the user understand what is required</span></span>

* <span data-ttu-id="10d0c-122">`<UserInputType>`czy ukończona ma następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="10d0c-122">`<UserInputType>` has the following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="10d0c-123">`RadioSingleSelectduration`-Wymusza pojedynczego wyboru.</span><span class="sxs-lookup"><span data-stu-id="10d0c-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
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

    * <span data-ttu-id="10d0c-124">`DropdownSingleSelect`— Umożliwia zaznaczenie tylko prawidłowe wartości.</span><span class="sxs-lookup"><span data-stu-id="10d0c-124">`DropdownSingleSelect` - Allows the selection of only valid value.</span></span>

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


* <span data-ttu-id="10d0c-126">`CheckboxMultiSelect`Umożliwia wybór co najmniej jedną wartość.</span><span class="sxs-lookup"><span data-stu-id="10d0c-126">`CheckboxMultiSelect` Allows for the selection of one or more values.</span></span>

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

## <a name="add-the-claim-to-the-sign-upsign-in-user-journey"></a><span data-ttu-id="10d0c-128">Dodawanie oświadczenia do logowania w górę/logowania użytkownika podróży</span><span class="sxs-lookup"><span data-stu-id="10d0c-128">Add the claim to the sign up/sign in user journey</span></span>

1. <span data-ttu-id="10d0c-129">Dodaj oświadczenie jako `<OutputClaim ClaimTypeReferenceId="city"/>` do TechnicalProfile `LocalAccountSignUpWithLogonEmail` (które można znaleźć w pliku zasad TrustFrameworkBase).</span><span class="sxs-lookup"><span data-stu-id="10d0c-129">Add the claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` to the TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in the TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="10d0c-130">Należy zauważyć, że ta TechnicalProfile używa SelfAssertedAttributeProvider.</span><span class="sxs-lookup"><span data-stu-id="10d0c-130">Note this TechnicalProfile uses the SelfAssertedAttributeProvider.</span></span>

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
      <!-- Optional claims, to be collected from the user -->
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

2. <span data-ttu-id="10d0c-131">Dodawanie oświadczenia do usługi AAD-UserWriteUsingLogonEmail jako `<PersistedClaim ClaimTypeReferenceId="city" />` zapisu oświadczenia do katalogu usługi AAD po zebraniu go przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10d0c-131">Add the claim to the AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` to write the claim to the AAD directory after collecting it from the user.</span></span> <span data-ttu-id="10d0c-132">Może pominąć ten krok, jeśli nie chcesz zachować oświadczeń w katalogu do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="10d0c-132">You may skip this step if you prefer not to persist the claim in the directory for future use.</span></span>

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

3. <span data-ttu-id="10d0c-133">Dodawanie oświadczenia do TechnicalProfile, która odczytuje z katalogu, gdy użytkownik zaloguje się jako`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="10d0c-133">Add the claim to the TechnicalProfile that reads from the directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for the provided user ID.</Item>
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

4. <span data-ttu-id="10d0c-134">Dodaj `<OutputClaim ClaimTypeReferenceId="city" />` zasad RP pliku SignUporSignIn.xml, więc tego oświadczenia są wysyłane do aplikacji w tokenie po przebieg pomyślne użytkownika.</span><span class="sxs-lookup"><span data-stu-id="10d0c-134">Add the `<OutputClaim ClaimTypeReferenceId="city" />` to the RP policy file SignUporSignIn.xml so this claim is sent to the application in the token after a successful user journey.</span></span>

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

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="10d0c-135">Testowanie zasad niestandardowych za pomocą "Uruchom teraz"</span><span class="sxs-lookup"><span data-stu-id="10d0c-135">Test the custom policy using "Run Now"</span></span>

1. <span data-ttu-id="10d0c-136">Otwórz **bloku usługi Azure AD B2C** i przejdź do **tożsamości środowiska Framework > zasady niestandardowe**.</span><span class="sxs-lookup"><span data-stu-id="10d0c-136">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="10d0c-137">Wybierz zasady niestandardowe przekazywane i kliknij przycisk **Uruchom teraz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="10d0c-137">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="10d0c-138">Należy zalogowanie przy użyciu adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="10d0c-138">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="10d0c-139">Ekran rejestracji w trybie testowym powinny wyglądać podobnie do poniższego:</span><span class="sxs-lookup"><span data-stu-id="10d0c-139">The signup screen in test mode should look similar to this:</span></span>

![Zrzut ekranu przedstawiający zmodyfikowane opcją](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="10d0c-141">Token do aplikacji będzie zawierają teraz `city` oświadczenia, jak pokazano poniżej</span><span class="sxs-lookup"><span data-stu-id="10d0c-141">The token back to your application will now include the `city` claim as shown below</span></span>
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

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="10d0c-142">Opcjonalnie: Usuń e-mail weryfikacji w podróży rejestracji</span><span class="sxs-lookup"><span data-stu-id="10d0c-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="10d0c-143">Aby pominąć Weryfikacja adresu e-mail, tworzenie zasad może być usunięty `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="10d0c-143">To skip email verification, the policy author can choose to remove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="10d0c-144">Adres e-mail zostanie wymagane, ale nie zweryfikowane, chyba że "Wymagane" = true zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="10d0c-144">The email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="10d0c-145">Należy rozważyć, jeśli ta opcja jest odpowiednia dla Twojej przypadki użycia!</span><span class="sxs-lookup"><span data-stu-id="10d0c-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="10d0c-146">Zweryfikować adres e-mail jest domyślnie włączone w `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` w pliku zasad TrustFrameworkBase w pakiecie starter:</span><span class="sxs-lookup"><span data-stu-id="10d0c-146">Verified email is enabled by default in the `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in the TrustFrameworkBase policy file in the starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="10d0c-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10d0c-147">Next steps</span></span>

<span data-ttu-id="10d0c-148">Dodaj nowe oświadczenie do przepływów dla logowania do kont społecznościowych, zmieniając TechnicalProfiles wymienionych poniżej.</span><span class="sxs-lookup"><span data-stu-id="10d0c-148">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed below.</span></span> <span data-ttu-id="10d0c-149">Są one używane przez federacyjne/społecznego konto logowania do zapisu i odczytu danych użytkownika za pomocą alternativeSecurityId jako Lokalizator.</span><span class="sxs-lookup"><span data-stu-id="10d0c-149">These are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
