---
title: "Usługa Azure Active Directory B2C: Dodawanie dostawcy usług Salesforce SAML za pomocą niestandardowych zasad | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toocreate zasad niestandardowych usługi Azure Active Directory B2C i zarządzanie nimi."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a>Usługa Azure Active Directory B2C: Zaloguj się przy użyciu konta usług Salesforce za pośrednictwem SAML

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

W tym artykule opisano sposób toouse [zasady niestandardowe](active-directory-b2c-overview-custom.md) tooset się logowania użytkowników z określonych organizacji Salesforce.

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="azure-ad-b2c-setup"></a>Instalacja usługi Azure AD B2C

Upewnij się, że zostały wykonane wszystkie kroki hello, przedstawiających sposób zbyt[wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) w usłudze Azure Active Directory B2C (Azure AD B2C).

Należą do nich:

* Tworzenie dzierżawy usługi Azure AD B2C.
* Tworzenie aplikacji usługi Azure AD B2C.
* Zarejestruj dwie aplikacje aparatu zasad.
* Konfigurowanie kluczy.
* Konfigurowanie hello początkowego pakietu.

### <a name="salesforce-setup"></a>Instalator usług SalesForce

W tym artykule przyjęto założenie, jeszcze hello następujące czynności:

* Konta konta usług Salesforce. Możesz zarejestrować się w celu [bezpłatne konto Developer Edition](https://developer.salesforce.com/signup).
* [Konfigurowanie domeny Moje](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) organizacji Salesforce.

## <a name="set-up-salesforce-so-users-can-federate"></a>Konfigurowanie usług Salesforce, umożliwiające użytkownikom można było wykonać Federację

toohelp usługi Azure AD B2C komunikować się z usług Salesforce, należy tooget hello Salesforce metadanych z adresu URL.

### <a name="set-up-salesforce-as-an-identity-provider"></a>Konfigurowanie usług Salesforce jako dostawca tożsamości

> [!NOTE]
> W tym artykule przyjęto założenie, używane są [Salesforce Lightning środowisko](https://developer.salesforce.com/page/Lightning_Experience_FAQ).

1. [Zaloguj się tooSalesforce](https://login.salesforce.com/). 
2. Na powitania pozostałych menu, w obszarze **ustawienia**, rozwiń węzeł **tożsamości**, a następnie kliknij przycisk **dostawcy tożsamości**.
3. Kliknij przycisk **włączenia dostawcy tożsamości**.
4. W obszarze **certyfikatu wybierz hello**, wybierz pozycję hello certyfikatów, które mają toocommunicate toouse Salesforce w usłudze Azure AD B2C. (Możesz użyć hello domyślnego certyfikatu). Kliknij pozycję **Zapisz**. 

### <a name="create-a-connected-app-in-salesforce"></a>Tworzenie połączonej aplikacji w usłudze Salesforce

1. Na powitania **dostawcy tożsamości** strony znajduje się zbyt**usługodawców**.
2. Kliknij przycisk **usługodawców zostaną utworzone za pośrednictwem połączenia aplikacji. Kliknij tutaj.**
3. W obszarze **podstawowe informacje**, wprowadź wartości hello wymagane dla połączonych aplikacji.
4. W obszarze **ustawień aplikacji sieci Web**, wybierz pozycję hello **Włącz SAML** pole wyboru.
5. W hello **identyfikator jednostki** wprowadź hello następującego adresu URL. Upewnij się, czy zastąpić wartość hello `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. W hello **adres URL usługi ACS** wprowadź hello następującego adresu URL. Upewnij się, czy zastąpić wartość hello `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. Pozostaw hello wartości domyślne dla wszystkich innych ustawień.
8. Przewiń toohello dolnej części listy hello, a następnie kliknij przycisk **zapisać**.

### <a name="get-hello-metadata-url"></a>Pobierz adres URL metadanych hello

1. Na stronie Przegląd hello połączonych aplikacji, kliknij przycisk **Zarządzaj**.
2. Skopiuj wartość hello **punkt końcowy odnajdowania metadanych**, a następnie zapisz je. Będzie on używany w dalszej części tego artykułu.

### <a name="set-up-salesforce-users-toofederate"></a>Konfigurowanie usług Salesforce toofederate użytkowników

1. Na powitania **Zarządzaj** strony połączonych aplikacji, przejdź zbyt**profile**.
2. Kliknij przycisk **zarządzania profilami**.
3. Wybierz profile hello (lub grupom użytkowników), które mają toofederate z usługi Azure AD B2C. Administrator systemu, wybierz hello **administratorem** Sprawdź okno, tak aby można było wykonać Federację przy użyciu konta usług Salesforce.

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a>Generuj certyfikat podpisywania dla usługi Azure AD B2C

Żądania wysyłane toobe potrzeby tooSalesforce podpisanego przez usługi Azure AD B2C. toogenerate certyfikatu podpisywania, Otwórz program Azure PowerShell, a następnie uruchom następujące polecenia hello.

> [!NOTE]
> Upewnij się, należy zaktualizować hello dzierżawy nazwy i hasła w hello top dwa wiersze.

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a>Dodaj hello SAML podpisywania certyfikatu tooAzure AD B2C

Przekaż hello dzierżawy usługi Azure AD B2C tooyour certyfikatu podpisywania: 

1. Przejdź dzierżawy tooyour usługi Azure AD B2C. Kliknij przycisk **ustawienia** > **Framework obsługi tożsamości** > **klucze zasad**.
2. Kliknij przycisk **+ Dodaj**, a następnie:
    1. Kliknij przycisk **opcje** > **przekazać**.
    2. Wprowadź **nazwa** (na przykład SAMLSigningCert). Prefiks Hello *B2C_1A_* zostanie automatycznie dodana nazwę toohello klucza.
    3. tooselect certyfikat, wybierz opcję **przekazać formant pliku**. 
    4. Wprowadź hasło certyfikatu hello ustawione w skrypcie programu PowerShell hello.
3. Kliknij przycisk **Utwórz**.
4. Sprawdź, czy utworzono klucz (na przykład B2C_1A_SAMLSigningCert). Zwróć uwagę na powitania Pełna nazwa (włącznie z *B2C_1A_*). Będzie można znaleźć klucza toothis później w zasadach hello.

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a>Utwórz hello Salesforce SAML dostawcy oświadczeń w zasadach podstawowej

Należy toodefine Salesforce jako dostawcy oświadczeń, użytkownicy mogą zarejestrować się przy użyciu Salesforce. Innymi słowy należy punktu końcowego hello toospecify, który usługi Azure AD B2C będzie komunikować się z. punkt końcowy Hello będzie *podaj* zestaw *oświadczeń* używany tooverify, do którego określony użytkownik został uwierzytelniony w usłudze Azure AD B2C. toodo, Dodaj `<ClaimsProvider>` dla usług Salesforce w hello rozszerzenia pliku zasad:

1. W katalogu roboczym otwórz plik rozszerzenia hello (TrustFrameworkExtensions.xml).
2. Znajdź hello `<ClaimsProviders>` sekcji. Jeśli nie istnieje, utwórz je w węźle głównym hello.
3. Dodaj nową `<ClaimsProvider>`:

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
          </OutputClaims>
          <OutputClaimsTransformations>
            <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
            <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
            <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
            <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
          </OutputClaimsTransformations>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    ```

W obszarze hello `<ClaimsProvider>` węzła:

1. Zmień wartość hello `<Domain>` tooa unikatowa wartość odróżniająca `<ClaimsProvider>` od innych dostawców tożsamości.
2. Zaktualizuj wartość hello `<DisplayName>` tooa nazwę wyświetlaną hello dostawcy oświadczeń. Ta wartość nie jest obecnie używana.

### <a name="update-hello-technical-profile"></a>Aktualizuj profil techniczne hello

tooget tokenu SAML z usług Salesforce, zdefiniuj protokołów hello Azure AD B2C będzie używać toocommunicate z usługą Azure Active Directory (Azure AD). To zrobić w hello `<TechnicalProfile>` elementu `<ClaimsProvider>`:

1. Aktualizacja Identyfikatora hello hello `<TechnicalProfile>` węzła. Ten identyfikator jest używane toorefer toothis techniczne profil z innymi częściami hello zasad.
2. Zaktualizuj wartość hello `<DisplayName>`. Ta wartość jest wyświetlana na powitania przycisk Zarejestruj się na stronie logowania.
3. Zaktualizuj wartość hello `<Description>`.
4. Usługa SalesForce używa protokołu hello SAML 2.0. Upewnij się, wartość tego hello `<Protocol>` jest **SAML2**.

Aktualizacja hello `<Metadata>` części hello poprzedzających XML tooreflect hello ustawienia dla określonego konta usług Salesforce. W hello XML zaktualizuj wartości metadanych hello:

1. Zaktualizuj wartość hello `<Item Key="PartnerEntity">` z hello Salesforce metadanych adresu URL skopiowanego wcześniej. Ma hello następującego formatu: 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. W hello `<CryptographicKeys>` sekcji aktualizacji hello wartość dla obu wystąpień `StorageReferenceId` toohello nazwa hello klucza certyfikatu podpisywania (na przykład B2C_1A_SAMLSigningCert).

### <a name="upload-hello-extension-file-for-verification"></a>Przekaż plik rozszerzenia hello do weryfikacji

Zgodnie z zasadami został skonfigurowany tak, aby usługi Azure AD B2C wie jak toocommunicate z usług Salesforce. Spróbuj przekazać plik rozszerzenia hello zasad, czy nie ma żadnych problemów wykonanej do tej pory tooverify. tooupload hello rozszerzenia pliku zasad:

1. W dzierżawie usługi Azure AD B2C, przejdź do pozycji toohello **wszystkie zasady** bloku.
2. Wybierz hello **zastąpić hello zasady, jeśli istnieje** pole wyboru.
3. Przekaż plik rozszerzenia hello (TrustFrameworkExtensions.xml). Upewnij się, że nie wystąpi niepowodzenie weryfikacji.

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a>Zarejestruj hello Salesforce SAML oświadczeń dostawcy tooa użytkownika podróży

Następnie dodaj hello tooone dostawca tożsamości Salesforce SAML podróży z użytkownika. W tym momencie hello dostawcy tożsamości nie został skonfigurowany, ale nie jest dostępna w żadnym z hello strony rejestracji i logowania użytkownika. tooadd hello tożsamości dostawcy tooa strony logowania, najpierw utwórz duplikatem istniejącej przebieg użytkownika szablonu. Następnie należy zmodyfikować szablon hello, tak aby ma również dostawcy tożsamości usługi Azure AD hello.

1. Otwórz plik podstawowy hello zasad (na przykład TrustFrameworkBase.xml).
2. Znajdź hello `<UserJourneys>` elementu, a następnie hello kopii całego `<UserJourney>` wartość, tym Id = "SignUpOrSignIn".
3. Otwórz plik rozszerzenia hello (na przykład TrustFrameworkExtensions.xml). Znajdź hello `<UserJourneys>` elementu. Jeśli hello element nie istnieje, utwórz je.
4. Wklej hello całego skopiowane `<UserJourney>` jako element podrzędny hello `<UserJourneys>` elementu.
5. Zmień nazwę hello identyfikator nowego hello `<UserJourney>` (na przykład SignUpOrSignUsingContoso).

### <a name="display-hello-identity-provider-button"></a>Przycisk dostawcy tożsamości hello wyświetlania

Witaj `<ClaimsProviderSelection>` element jest analogiczne tooan przycisk dostawcę tożsamości na stronie tworzenia konta lub logowania. Dodając `<ClaimsProviderSelection>` elementu Salesforce, nowy przycisk jest wyświetlany, gdy użytkownik przejdzie do strony toothis. przycisk dostawcy tożsamości hello toodisplay:

1. W hello `<UserJourney>` utworzony, Znajdź hello `<OrchestrationStep>` z `Order="1"`.
2. Dodaj następujące XML hello:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. Ustaw `TargetClaimsExchangeId` tooa wartość logiczną. Zaleca się następujące hello sam Konwencji jako innych (na przykład  *\[ClaimProviderName\]Exchange*).

### <a name="link-hello-identity-provider-button-tooan-action"></a>Akcja tooan przycisku dostawcy tożsamości hello łącza

Teraz, gdy masz przycisk dostawcy tożsamości w miejscu połączyć je tooan akcji. W takim przypadku akcja hello jest dla usługi Azure AD B2C toocommunicate z tooreceive Salesforce tokenu SAML. Można to zrobić przez łączenie hello techniczne profilu dla użytkownika SAML Salesforce dostawcy oświadczeń:

1. W hello `<UserJourney>` węzła, Znajdź hello `<OrchestrationStep>` z `Order="2"`.
2. Dodaj następujące XML hello:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. Aktualizacja `Id` toohello samą wartość tego używanego wcześniej dla `TargetClaimsExchangeId`.
4. Aktualizacja `TechnicalProfileReferenceId` toohello `Id` hello techniczne profilu utworzonego wcześniej (na przykład ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Przekaż hello zaktualizowane rozszerzenie pliku

Po zakończeniu modyfikowania hello rozszerzenia pliku. Zapisz i przekazywanie tego pliku. Upewnij się, że wszystkie operacje sprawdzania poprawności powiodło się.

### <a name="update-hello-relying-party-file"></a>Zaktualizuj hello jednostki uzależnionej strony plik

Następnie zaktualizuj hello jednostki uzależnionej strony (RP) pliku, który inicjuje przebieg użytkownika hello, utworzony:

1. Utwórz kopię SignUpOrSignIn.xml w katalogu roboczym. Następnie należy zmienić jego nazwę (na przykład SignUpOrSignInWithAAD.xml).
2. Nowy plik i aktualizacji hello hello Otwórz `PolicyId` atrybutu dla `<TrustFrameworkPolicy>` z unikatową wartość. Jest to nazwa hello zasady (na przykład SignUpOrSignInWithAAD).
3. Modyfikowanie hello `ReferenceId` atrybutu w `<DefaultUserJourney>` toomatch hello `Id` hello nowego użytkownika podróży utworzony (na przykład SignUpOrSignUsingContoso).
4. Zapisz zmiany, a następnie przekaż plik hello.

## <a name="test-and-troubleshoot"></a>Testowanie i rozwiązywanie problemów

tootest hello niestandardowych zasad, które przekazanym właśnie, w hello portalu Azure, przejdź do bloku zasad toohello, a następnie kliknij **Uruchom teraz**. Jeśli nie powiedzie się, zobacz [Rozwiązywanie problemów dotyczących zasad niestandardowych](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Następne kroki

Wyrazić swoją opinię za[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
