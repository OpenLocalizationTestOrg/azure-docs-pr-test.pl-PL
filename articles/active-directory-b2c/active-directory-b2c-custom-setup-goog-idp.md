---
title: "Usługa Azure Active Directory B2C: Dodawanie Google + funkcję dostawcy tożsamości OAuth2 przy użyciu zasad niestandardowych"
description: "Przykładowe przy użyciu usługi Google + jako dostawca tożsamości za pomocą protokołu OAuth2"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a>Usługa Azure Active Directory B2C: Dodawanie Google + funkcję dostawcy tożsamości OAuth2 przy użyciu zasad niestandardowych

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

W tym przewodniku przedstawiono sposób tooenable logowania użytkowników z konta Google + przy użyciu hello [niestandardowych zasad](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Wymagania wstępne

Zakończenie hello etapami hello [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) artykułu.

Kroki te obejmują:

1.  Tworzenie aplikacji konto Google +.
2.  Dodawanie hello Google + konto aplikacji klucza tooAzure AD B2C
3.  Dodawanie zasad tooa dostawcy oświadczeń
4.  Rejestrowanie hello Google + konto oświadczeń dostawcy tooa użytkownika podróży
5.  Przekazywanie hello tooan zasad usługi Azure AD B2C dzierżawy i przetestować go

## <a name="create-a-google-account-application"></a>Tworzenie aplikacji konto Google +
toouse Google + jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji Google + i dostarczyć hello prawo parametrów. Możesz zarejestrować Google + aplikacją w tym miejscu: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)

1.  Przejdź toohello [konsoli deweloperów Google](https://console.developers.google.com/) i zaloguj się przy użyciu poświadczeń konta Google +.
2.  Kliknij przycisk **Tworzenie projektu**, wprowadź **Nazwa projektu**, a następnie kliknij przycisk **Utwórz**.

3.  Polecenie hello **menu projekty**.

    ![Google + konto — wybierz projekt](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  Polecenie hello  **+**  przycisku.

    ![Google + konto — Utwórz nowy projekt](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  Wprowadź **Nazwa projektu**, a następnie kliknij przycisk **Utwórz**.

    ![Google + konto — nowy projekt](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  Poczekaj, aż projekt hello jest gotowy, a następnie kliknij przycisk na powitania **menu projekty**.

    ![Zaczekaj, aż nowy projekt jest gotowy toouse Google + konto-](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  Kliknij nazwę projektu.

    ![Google + konto - hello wybierz nowy projekt](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  Kliknij przycisk **Menedżer interfejsu API** , a następnie kliknij przycisk **poświadczenia** w hello lewy pasek nawigacyjny.
9.  Kliknij przycisk hello **ekranu zgoda OAuth** u góry hello.

    ![Google + konto — Ustaw OAuth zgody ekranu](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  Wybierz lub określ prawidłowe **adres E-mail**, podaj **nazwa produktu**i kliknij przycisk **zapisać**.

    ![Google + - poświadczeń aplikacji](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  Kliknij przycisk **nowe poświadczenia** , a następnie wybierz **identyfikator klienta OAuth**.

    ![Google + - Utwórz nowe poświadczenia aplikacji](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  W obszarze **typu aplikacji**, wybierz pozycję **aplikacji sieci Web**.

    ![Google + — Wybieranie typu aplikacji](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  Podaj **nazwa** dla aplikacji, wprowadź `https://login.microsoftonline.com` w hello **źródeł autoryzowany JavaScript** pola i `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **autoryzowanych przekierowania URI**pola. Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com). Witaj **{dzierżawa}** wartość jest rozróżniana wielkość liter. Kliknij przycisk **Utwórz**.

    ![Google + - zapewniają autoryzację JavaScript źródeł i Przekierowanie URI](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  Skopiuj wartości hello **identyfikator klienta** i **klucz tajny klienta**. Należy obu tooconfigure Google + funkcję dostawcy tożsamości w dzierżawie. **Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.

    ![Google + - wartości hello kopii klucza tajnego identyfikator i klienta klienta](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a>Dodaj hello Google + konto aplikacji klucza tooAzure AD B2C
Federacja z konta Google + wymaga klucz tajny klienta konta Google + tootrust usługi Azure AD B2C w imieniu aplikacji hello. Należy toostore Twojego Google + klucz tajny aplikacji w dzierżawie usługi Azure AD B2C:  

1.  Przejdź do dzierżawy usługi Azure AD B2C tooyour i wybierz **ustawieniami B2C** > **Framework obsługi tożsamości**
2.  Wybierz **zasad kluczy** klawiszy hello tooview dostępnych w dzierżawie.
3.  Kliknij przycisk **+ Dodaj**.
4.  Aby uzyskać **opcje**, użyj **ręcznego**.
5.  Aby uzyskać **nazwa**, użyj `GoogleSecret`.  
    Prefiks Hello `B2C_1A_` mogą być dodawane automatycznie.
6.  W hello **klucz tajny** wprowadź klucz tajny aplikacji firmy Microsoft z https://apps.dev.microsoft.com
7.  Aby uzyskać **użycie klucza**, użyj **podpisu**.
8.  Kliknij przycisk **Utwórz**
9.  Upewnij się, że utworzono klucz hello `B2C_1A_GoogleSecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Dodawanie dostawcy oświadczeń w zasadach rozszerzenia

Jeśli chcesz toosign użytkowników przy użyciu konta Google +, musisz mieć toodefine Google + konto jako dostawcy oświadczeń. Innymi słowy należy toospecify punktu końcowego, który komunikuje się usługi Azure AD B2C. punkt końcowy Hello zawiera zestaw oświadczeń, które są używane przez usługi Azure AD B2C tooverify, który został uwierzytelniony określonego użytkownika.

Zdefiniuj konto Google + jako dostawcy oświadczeń, dodając `<ClaimsProvider>` węzeł rozszerzenia pliku zasad:

1.  Otwórz plik zasad rozszerzenia hello (TrustFrameworkExtensions.xml) z katalogu roboczego. Jeśli potrzebujesz edytora XML [spróbuj Visual Studio Code](https://code.visualstudio.com/download), lekkie edytora i platform.
2.  Znajdź hello `<ClaimsProviders>` sekcji
3.  Dodaj następujące fragment kodu XML w obszarze hello hello `ClaimsProviders` elementu i zastępowanie `client_id` wartość przy użyciu usługi Google + konto aplikacji Identyfikatora klienta przed zapisaniem pliku hello.  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Zarejestruj hello Google + konto oświadczeń dostawcy tooSign się lub zaloguj się w podróży użytkownika

Dostawca tożsamości Hello nie został skonfigurowany.  Jednak nie jest dostępna w żadnym hello konta-konta/logowania ekranów. Dodaj hello Google + konto tożsamości użytkownika dostawcy usług tooyour `SignUpOrSignIn` podróży użytkownika. toomake ją, utworzymy duplikatem istniejącej przebieg użytkownika szablonu.  Następnie dodaj hello Google + dostawcy tożsamości konta:

>[!NOTE]
>
>Jeśli został skopiowany hello `<UserJourneys>` elementu z pliku podstawowego zasad toohello rozszerzenie pliku (TrustFrameworkExtensions.xml), możesz pominąć toothis sekcję.

1.  Otwórz plik podstawowy hello zasad (na przykład TrustFrameworkBase.xml).
2.  Znajdź hello `<UserJourneys>` element kopiowania hello całej zawartości i `<UserJourneys>` węzła.
3.  Otwórz plik rozszerzenia hello (na przykład TrustFrameworkExtensions.xml) i Znajdź hello `<UserJourneys>` elementu. Jeśli hello element nie istnieje, dodaj je.
4.  Wklej zawartość całego hello `<UserJournesy>` węzła, który został skopiowany jako element podrzędny hello `<UserJourneys>` elementu.

### <a name="display-hello-button"></a>Przycisk hello wyświetlania
Witaj `<ClaimsProviderSelections>` element definiuje listę hello opcje wyboru dostawcy oświadczeń i ich kolejność.  `<ClaimsProviderSelection>`element jest przycisku dostawcy tożsamości analogiczne tooan na stronie konta-konta/logowania. Jeśli dodasz `<ClaimsProviderSelection>` elementu dla konta Google + nowy przycisk zostaną wyświetlone po wyładowuje użytkownika na stronie powitania. tooadd tego elementu:

1.  Znajdź hello `<UserJourney>` węzła, który zawiera `Id="SignUpOrSignIn"` w podróży użytkownika hello, które zostały skopiowane.
2.  Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`
3.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Akcja tooan przycisku hello łącza
Teraz, gdy masz przycisku w miejscu, należy toolink go tooan akcji. Akcja Hello jest dla usługi Azure AD B2C toocommunicate z tooreceive konto Google + w takim przypadku tokenu.

1.  Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.
2.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * Upewnij się, hello `Id` ma takie same wartości jak hello `TargetClaimsExchangeId` w powyższej sekcji hello
> * Upewnij się, `TechnicalProfileReferenceId` ustawiono Identyfikatora profilu techniczne toohello utworzonego wcześniej (Google-OAUTH).

## <a name="upload-hello-policy-tooyour-tenant"></a>Przekaż hello zasad tooyour dzierżawy
1.  W hello [portalu Azure](https://portal.azure.com), przejdź do hello [kontekstu dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)i otwórz hello **usługi Azure AD B2C** bloku.
2.  Wybierz **Framework obsługi tożsamości**.
3.  Otwórz hello **wszystkie zasady** bloku.
4.  Wybierz **przekazywać zasady**.
5.  Sprawdź **zastąpić hello zasady, jeśli istnieje** pole.
6.  **Przekaż** TrustFrameworkExtensions.xml i upewnij się, że nie wystąpi niepowodzenie weryfikacji hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Testowanie zasad niestandardowych hello przy użyciu Uruchom teraz
1.  Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.

    >[!NOTE]
    >
    >    **Uruchom teraz** wymaga co najmniej jedną aplikację toobe preregistered hello dzierżawcy. 
    >    toolearn tooregister aplikacji, zobacz temat hello Azure AD B2C [wprowadzenie](active-directory-b2c-get-started.md) artykułu lub hello [Rejestracja aplikacji](active-directory-b2c-app-registration.md) artykułu.


2.  Otwórz **B2C_1A_signup_signin**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany. Wybierz **Uruchom teraz**.
3.  Powinno być możliwe toosign za pomocą konta Google +.

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a>[Opcjonalnie] Zarejestruj hello Google + konto oświadczeń dostawcy tooProfile Edycja użytkownika podróży
Możesz tooadd hello Google + konto dostawcy tożsamości również użytkownika tooyour `ProfileEdit` podróży użytkownika. toomake ją, powtórz firma Microsoft hello ostatnie dwa kroki:

### <a name="display-hello-button"></a>Przycisk hello wyświetlania
1.  Otwórz plik rozszerzenia hello zasad (na przykład TrustFrameworkExtensions.xml).
2.  Znajdź hello `<UserJourney>` węzła, który zawiera `Id="ProfileEdit"` w podróży użytkownika hello, które zostały skopiowane.
3.  Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`
4.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Akcja tooan przycisku hello łącza
1.  Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.
2.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Testowanie zasad niestandardowych edycji profilu hello przy użyciu Uruchom teraz

1.  Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.
2.  Otwórz **B2C_1A_ProfileEdit**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany. Wybierz **Uruchom teraz**.
3.  Powinno być możliwe toosign za pomocą konta Google +.

## <a name="download-hello-complete-policy-files"></a>Pobierz pliki zasad pełną hello
Opcjonalnie: Zaleca się tworzenie scenariusz przy użyciu własnych niestandardowych zasad plików po zakończeniu hello wprowadzenie zasady niestandardowe przeprowadzenie zamiast te przykładowe pliki.  [Przykładowe pliki zasad dla odwołania](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
