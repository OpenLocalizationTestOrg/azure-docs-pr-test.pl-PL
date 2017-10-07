---
title: "Usługa Azure Active Directory B2C: Dodawanie konta Microsoft (MSA) jako dostawca tożsamości za pomocą zasad niestandardowych"
description: "Przykładowe za pomocą programu Microsoft jako dostawca tożsamości za pomocą protokołu OpenID Connect (OIDC)"
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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a>Usługa Azure Active Directory B2C: Dodawanie konta Microsoft (MSA) jako dostawca tożsamości za pomocą zasad niestandardowych

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

W tym artykule opisano sposób tooenable logowania użytkowników z konta Microsoft (MSA) przy użyciu hello [niestandardowych zasad](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Wymagania wstępne
Zakończenie hello etapami hello [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) artykułu.

Kroki te obejmują:

1.  Tworzenie aplikacji konta Microsoft.
2.  Dodawanie hello Microsoft konta aplikacji klucza tooAzure AD B2C
3.  Dodawanie zasad tooa dostawcy oświadczeń
4.  Rejestrowanie hello Account Microsoft oświadczeń dostawcy tooa użytkownika podróży
5.  Przekazywanie hello tooan zasad usługi Azure AD B2C dzierżawy i przetestować go

## <a name="create-a-microsoft-account-application"></a>Tworzenie aplikacji konta Microsoft
toouse konta Microsoft, funkcję dostawcy tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji konta Microsoft i dostarczyć hello prawo parametrów. Musisz mieć konto Microsoft. Jeśli nie masz, odwiedź stronę [https://www.live.com/](https://www.live.com/).

1.  Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) i zaloguj się przy użyciu poświadczeń konta Microsoft.
2.  Kliknij przycisk **Dodaj aplikację**.

    ![Microsoft konta — Dodawanie aplikacji](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  Podaj **nazwa** dla aplikacji, **adres e-mail kontaktu**, usuń zaznaczenie pola wyboru **nas pomocy Rozpoczynanie pracy** i kliknij przycisk **Utwórz**.

    ![Konto Microsoft - rejestrowania aplikacji](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  Skopiuj wartość hello **identyfikator aplikacji**. Należy go tooconfigure konto Microsoft jako dostawca tożsamości w dzierżawie.

    ![Konto Microsoft - kopiowania hello wartość identyfikatora aplikacji](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  Polecenie **Dodaj platformy**

    ![Microsoft konta — Dodawanie platformy](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  Z listy platformy hello wybierz **Web**.

    ![Konto Microsoft — z listy platformy hello wybierz sieci Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  Wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **identyfikator URI przekierowania** pola. Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).

    ![Konto Microsoft — zestaw adresów URL przekierowania.](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  Polecenie **wygenerować nowe hasło** w obszarze hello **klucze tajne aplikacji** sekcji. Skopiuj nowe hasło hello wyświetlany na ekranie. Należy go tooconfigure konto Microsoft jako dostawca tożsamości w dzierżawie. To hasło jest ważne poświadczenie zabezpieczeń.

    ![Microsoft konta — wygenerować nowe hasło](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Konto Microsoft - kopiowania hello nowe hasło](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  Witaj opcję **Obsługa zestaw Live SDK** w obszarze hello **zaawansowane opcje** sekcji. Kliknij pozycję **Zapisz**.

    ![Konto Microsoft — Obsługa zestaw Live SDK](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a>Dodaj hello Microsoft konta aplikacji klucza tooAzure AD B2C
Federacja z kontami Microsoft wymaga klucza tajnego klienta tootrust konta Microsoft Azure AD B2C w imieniu aplikacji hello. Należy toostore Twojego secert aplikacji konta Microsoft, w dzierżawie usługi Azure AD B2C:   

1.  Przejdź do dzierżawy usługi Azure AD B2C tooyour i wybierz **ustawieniami B2C** > **Framework obsługi tożsamości**
2.  Wybierz **zasad kluczy** klawiszy hello tooview dostępnych w dzierżawie.
3.  Kliknij przycisk **+ Dodaj**.
4.  Aby uzyskać **opcje**, użyj **ręcznego**.
5.  Aby uzyskać **nazwa**, użyj `MSASecret`.  
    Prefiks Hello `B2C_1A_` mogą być dodawane automatycznie.
6.  W hello **klucz tajny** wprowadź klucz tajny aplikacji firmy Microsoft z https://apps.dev.microsoft.com
7.  Aby uzyskać **użycie klucza**, użyj **podpisu**.
8.  Kliknij przycisk **Utwórz**
9.  Upewnij się, że utworzono klucz hello `B2C_1A_MSASecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Dodawanie dostawcy oświadczeń w zasadach rozszerzenia
Jeśli chcesz toosign użytkowników przy użyciu Account firmy Microsoft, należy toodefine Account Microsoft jako dostawcy oświadczeń. Innymi słowy należy toospecify punktu końcowego, który komunikuje się usługi Azure AD B2C. punkt końcowy Hello zawiera zestaw oświadczeń, które są używane przez usługi Azure AD B2C tooverify, który został uwierzytelniony określonego użytkownika.

Zdefiniuj Account Microsoft jako dostawcy oświadczeń, dodając `<ClaimsProvider>` węzeł rozszerzenia pliku zasad:

1.  Otwórz plik zasad rozszerzenia hello (TrustFrameworkExtensions.xml) z katalogu roboczego. Jeśli potrzebujesz edytora XML [spróbuj Visual Studio Code](https://code.visualstudio.com/download), lekkie edytora i platform.
2.  Znajdź hello `<ClaimsProviders>` sekcji
3.  Dodaj następujący fragment kodu XML w obszarze hello `ClaimsProviders` elementu:

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  Zastąp `client_id` wartości identyfikatora klienta aplikacji Account firmy Microsoft

5.  Zapisz plik hello.

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Zarejestruj hello Account Microsoft oświadczeń dostawcy tooSign się lub logowanie przebieg użytkownika

W tym momencie hello dostawcy tożsamości nie został skonfigurowany, ale nie jest dostępna w żadnym hello konta-konta/logowania ekranów. Teraz należy użytkownika tooyour dostawcy tożsamości Account Microsoft hello tooadd `SignUpOrSignIn` podróży użytkownika. toomake ją, utworzymy duplikatem istniejącej przebieg użytkownika szablonu.  Następnie dodaj dostawcy tożsamości Account Microsoft hello:

> [!NOTE]
>
>Jeśli został wcześniej skopiowany hello `<UserJourneys>` elementu z pliku podstawowego pliku rozszerzenia zasad toohello `TrustFrameworkExtensions.xml`, toothis sekcję można pominąć.

1.  Otwórz plik podstawowy hello zasad (na przykład TrustFrameworkBase.xml).
2.  Znajdź hello `<UserJourneys>` element kopiowania hello całej zawartości i `<UserJourneys>` węzła.
3.  Otwórz plik rozszerzenia hello (na przykład TrustFrameworkExtensions.xml) i Znajdź hello `<UserJourneys>` elementu. Jeśli hello element nie istnieje, dodaj je.
4.  Wklej zawartość całego hello `<UserJournesy>` węzła, który został skopiowany jako element podrzędny hello `<UserJourneys>` elementu.

### <a name="display-hello-button"></a>Przycisk hello wyświetlania
Witaj `<ClaimsProviderSelections>` element definiuje listę hello opcje wyboru dostawcy oświadczeń i ich kolejność.  `<ClaimsProviderSelection>`element jest przycisku dostawcy tożsamości analogiczne tooan na stronie konta-konta/logowania. Jeśli dodasz `<ClaimsProviderSelection>` elementu dla konta Microsoft, nowy przycisk zostaną wyświetlone po wyładowuje użytkownika na stronie powitania. tooadd tego elementu:

1.  Znajdź hello `<UserJourney>` węzła, który zawiera `Id="SignUpOrSignIn"` w podróży użytkownika hello, które zostały skopiowane.
2.  Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`
3.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Akcja tooan przycisku hello łącza
Teraz, gdy masz przycisku w miejscu, należy toolink go tooan akcji. Akcja Hello jest dla usługi Azure AD B2C toocommunicate z tooreceive Account Microsoft w tym przypadku tokenu. Link akcji tooan przycisk hello przez łączenie hello techniczne profilu dla dostawcy oświadczeń Account Microsoft:

1.  Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.
2.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * Upewnij się, hello `Id` ma takie same wartości jak hello `TargetClaimsExchangeId` w powyższej sekcji hello
>   * Upewnij się, `TechnicalProfileReferenceId` ustawiono Identyfikatora profilu techniczne toohello utworzonego wcześniej (MSA-OIDC).

## <a name="upload-hello-policy-tooyour-tenant"></a>Przekaż hello zasad tooyour dzierżawy
1.  W hello [portalu Azure](https://portal.azure.com), przejdź do hello [kontekstu dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)i otwórz hello **usługi Azure AD B2C** bloku.
2.  Wybierz **Framework obsługi tożsamości**.
3.  Otwórz hello **wszystkie zasady** bloku.
4.  Wybierz **przekazywać zasady**.
5.  Sprawdź **zastąpić hello zasady, jeśli istnieje** pole.
6.  **Przekaż** TrustFrameworkExtensions.xml i upewnij się, że nie wystąpi niepowodzenie weryfikacji hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Testowanie zasad niestandardowych hello przy użyciu Uruchom teraz

1.  Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.
> [!NOTE]
>
>**Uruchom teraz** wymaga co najmniej jedną aplikację toobe preregistered hello dzierżawcy. toolearn tooregister aplikacji, zobacz temat hello Azure AD B2C [wprowadzenie](active-directory-b2c-get-started.md) artykułu lub hello [Rejestracja aplikacji](active-directory-b2c-app-registration.md) artykułu.
2.  Otwórz **B2C_1A_signup_signin**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany. Wybierz **Uruchom teraz**.
3.  Powinno być możliwe toosign za pomocą konta Microsoft.

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a>[Opcjonalnie] Zarejestruj hello Account Microsoft oświadczeń dostawcy tooProfile Edycja użytkownika podróży
Możesz dostawcy tożsamości Account Microsoft hello tooadd również użytkownika tooyour `ProfileEdit` podróży użytkownika. toomake ją, powtórz firma Microsoft hello ostatnie dwa kroki:

### <a name="display-hello-button"></a>Przycisk hello wyświetlania
1.  Otwórz plik rozszerzenia hello zasad (na przykład TrustFrameworkExtensions.xml).
2.  Znajdź hello `<UserJourney>` węzła, który zawiera `Id="ProfileEdit"` w podróży użytkownika hello, które zostały skopiowane.
3.  Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`
4.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Akcja tooan przycisku hello łącza
1.  Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.
2.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Testowanie zasad niestandardowych edycji profilu hello przy użyciu Uruchom teraz
1.  Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.
2.  Otwórz **B2C_1A_ProfileEdit**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany. Wybierz **Uruchom teraz**.
3.  Powinno być możliwe toosign za pomocą konta Microsoft.

## <a name="download-hello-complete-policy-files"></a>Pobierz pliki zasad pełną hello
Opcjonalnie: Zaleca się tworzenie scenariusz przy użyciu własnych niestandardowych zasad plików po zakończeniu hello wprowadzenie zasady niestandardowe przeprowadzenie zamiast te przykładowe pliki.  [Przykładowe pliki zasad dla odwołania](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
