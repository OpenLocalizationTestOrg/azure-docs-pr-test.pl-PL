---
title: "Usługa Azure Active Directory B2C: Dodawanie dostawcy usługi Azure AD za pomocą niestandardowych zasad | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o zasadach niestandardowych usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a>Usługa Azure Active Directory B2C: Zaloguj się przy użyciu konta usługi Azure AD

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

W tym artykule opisano sposób tooenable logowania użytkowników z określonych organizacji usługi Azure Active Directory (Azure AD) przy użyciu hello [niestandardowych zasad](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Wymagania wstępne

Zakończenie hello etapami hello [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) artykułu.

Kroki te obejmują:

1. Tworzenie usługi Azure Active Directory B2C dzierżawy (Azure AD B2C).
2. Tworzenie aplikacji usługi Azure AD B2C.
3. Rejestrowanie dwie aplikacje aparat zasad.
4. Konfigurowanie kluczy.
5. Konfigurowanie hello początkowego pakietu.

## <a name="create-an-azure-ad-app"></a>Utwórz aplikację usługi Azure AD

tooenable logowania użytkowników z określonej usługi Azure AD w organizacji, należy tooregister aplikacji w ramach dzierżawy hello Azure AD w organizacji.

>[!NOTE]
> Używamy "contoso.com" dla dzierżawcy hello organizacyjnego usługi Azure AD i "fabrikamb2c.onmicrosoft.com" jako dzierżawy hello Azure AD B2C w hello, postępując zgodnie z instrukcjami.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
1. Na górnym pasku hello wybierz konto. Z hello **katalogu** wybierz dzierżawy hello Azure AD w organizacji, w którym ma tooregister aplikacji (contoso.com).
1. Wybierz **więcej usług** w okienku po lewej stronie powitania i wyszukaj "Rejestracji aplikacji".
1. Wybierz **nowej rejestracji aplikacji**.
1. Wprowadź nazwę dla aplikacji (na przykład `Azure AD B2C App`).
1. Wybierz **aplikacji sieci Web / interfejs API** hello typu aplikacja.
1. Dla **adres URL logowania**, wprowadź hello następującego adresu URL, gdzie `yourtenant` zastępuje nazwę hello dzierżawy usługi Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. Zapisz identyfikator hello aplikacji.
1. Wybierz nowo utworzony hello aplikacji.
1. W obszarze hello **ustawienia** bloku, wybierz opcję **klucze**.
1. Utwórz nowy klucz i zapisz go. W krokach hello w następnej sekcji hello będą używać go.

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a>Dodawanie klucza tooAzure hello Azure AD AD B2C

Należy klucz aplikacji contoso.com hello toostore w dzierżawie usługi Azure AD B2C. toodo to:
1. Przejdź do dzierżawy usługi Azure AD B2C tooyour i wybierz **ustawieniami B2C** > **Framework obsługi tożsamości** > **zasad kluczy**.
1. Wybierz **+ Dodaj**.
1. Wybierz lub wprowadź następujące opcje:
   * Wybierz **ręcznego**.
   * Aby uzyskać **nazwa**, wybierz nazwę, która odpowiada nazwa dzierżawy usługi Azure AD (na przykład `ContosoAppSecret`).  Prefiks Hello `B2C_1A_` zostanie automatycznie dodana nazwę toohello klucza.
   * Wklej klucz aplikacji hello **klucz tajny** pole.
   * Wybierz **podpisu**.
1. Wybierz pozycję **Utwórz**.
1. Upewnij się, że utworzono klucz hello `B2C_1A_ContosoAppSecret`.


## <a name="add-a-claims-provider-in-your-base-policy"></a>Dodawanie dostawcy oświadczeń w zasadach podstawowej

Jeśli chcesz toosign użytkowników za pomocą usługi Azure AD, należy toodefine usługi Azure AD jako dostawcy oświadczeń. Innymi słowy należy toospecify punktu końcowego usługi Azure AD B2C będzie komunikować się z. punkt końcowy Hello zapewni zestaw oświadczeń, które są używane przez usługi Azure AD B2C tooverify, który został uwierzytelniony określonego użytkownika. 

Można zdefiniować usługi Azure AD jako dostawcy oświadczeń, dodając toohello usługi Azure AD `<ClaimsProvider>` węzeł w hello rozszerzenia pliku zasad:

1. Otwórz plik rozszerzenia hello (TrustFrameworkExtensions.xml) z katalogu roboczego.
1. Znajdź hello `<ClaimsProviders>` sekcji. Jeśli nie istnieje, dodaj ją w obszarze węzła głównego hello.
1. Dodaj nową `<ClaimsProvider>` węzła w następujący sposób:

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
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

1. W obszarze hello `<ClaimsProvider>` węzła, wartość hello aktualizacji `<Domain>` tooa unikatową wartość, które mogą być używane toodistinguish go od innych dostawców tożsamości.
1. W obszarze hello `<ClaimsProvider>` węzła, wartość hello aktualizacji `<DisplayName>` tooa przyjazną nazwę hello dostawcy oświadczeń. Ta wartość nie jest obecnie używana.

### <a name="update-hello-technical-profile"></a>Aktualizuj profil techniczne hello

tooget tokenu z punktu końcowego usługi Azure AD hello należy protokołów hello toodefine usługi Azure AD B2C należy używać toocommunicate z usługą Azure AD. Jest to realizowane wewnątrz hello `<TechnicalProfile>` elementu `<ClaimsProvider>`.
1. Aktualizacja Identyfikatora hello hello `<TechnicalProfile>` węzła. Ten identyfikator jest używane toorefer toothis techniczne profil z innymi częściami hello zasad.
1. Zaktualizuj wartość hello `<DisplayName>`. Ta wartość będzie wyświetlana na powitania przycisk Zarejestruj się na ekranie logowania.
1. Zaktualizuj wartość hello `<Description>`.
1. Protokołu OpenID Connect hello używa usługi Azure AD, dlatego upewnij się, ta wartość hello dla `<Protocol>` jest `"OpenIdConnect"`.

Należy tooupdate hello `<Metadata>` sekcji w pliku XML hello określonego tooearlier tooreflect hello konfigurację ustawień dla konkretnej dzierżawy usługi Azure AD. W pliku XML hello zaktualizuj wartości metadanych hello w następujący sposób:

1. Ustaw `<Item Key="METADATA">` za`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, gdzie `yourAzureADtenant` jest nazwa dzierżawy usługi Azure AD (contoso.com).
1. Otwórz toohello Twojego przeglądarki, a następnie przejść `METADATA` adres URL, które zostało zaktualizowane.
1. W przeglądarce hello wyszukiwania dla obiektu "Wystawca" hello i skopiuj jej wartość. Powinien wyglądać podobnie jak poniżej hello: `https://sts.windows.net/{tenantId}/`.
1. Wklej wartość hello `<Item Key="ProviderName">` hello pliku XML.
1. Ustaw `<Item Key="client_id">` toohello identyfikator aplikacji hello rejestracji aplikacji.
1. Ustaw `<Item Key="IdTokenAudience">` toohello identyfikator aplikacji hello rejestracji aplikacji.
1. Upewnij się, że `<Item Key="response_types">` ustawiono zbyt`id_token`.
1. Upewnij się, że `<Item Key="UsePolicyInRedirectUri">` ustawiono zbyt`false`.

Należy również hasło hello Azure AD toolink zarejestrowanych w Twojej usługi Azure AD B2C toohello dzierżawy usługi Azure AD `<ClaimsProvider>` informacji:

* W hello `<CryptographicKeys>` sekcji hello poprzedzających pliku XML, zaktualizuj wartość hello `StorageReferenceId` toohello Identyfikator odwołania hello klucz tajny, który zdefiniowano (na przykład `ContosoAppSecret`).

### <a name="upload-hello-extension-file-for-verification"></a>Przekaż plik rozszerzenia hello do weryfikacji

Chwili skonfigurowano zasad, aby usługi Azure AD B2C znała jak toocommunicate z katalogiem Azure AD. Spróbuj przekazać plik rozszerzenia hello z Twojej tooconfirm tylko zasady czy problemów nie ma do tej pory. toodo tak:

1. Otwórz hello **wszystkie zasady** bloku w dzierżawie usługi Azure AD B2C.
1. Sprawdź hello **zastąpić hello zasady, jeśli istnieje** pole.
1. Przekaż plik rozszerzenia hello (TrustFrameworkExtensions.xml) i upewnij się, że nie wystąpi niepowodzenie weryfikacji hello.

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a>Zarejestruj hello Azure AD oświadczeń dostawcy tooa użytkownika podróży

Teraz należy tooadd tooone dostawcy tożsamości usługi Azure AD hello podróży z użytkownika. W tym momencie hello dostawcy tożsamości nie został skonfigurowany, ale nie jest dostępna w żadnym hello konta-konta/logowania ekranów. toomake dostępne, firma Microsoft utworzy duplikatem istniejącej przebieg użytkownika szablonu i następnie zmodyfikować go, aby miała ona również dostawcy tożsamości hello Azure AD:

1. Otwórz plik podstawowy hello zasad (na przykład TrustFrameworkBase.xml).
1. Znajdź hello `<UserJourneys>` hello elementu i skopiuj cały `<UserJourney>` węzła, który zawiera `Id="SignUpOrSignIn"`.
1. Otwórz plik rozszerzenia hello (na przykład TrustFrameworkExtensions.xml) i Znajdź hello `<UserJourneys>` elementu. Jeśli hello element nie istnieje, dodaj je.
1. Wklej hello cały `<UserJourney>` węzła, który został skopiowany jako element podrzędny hello `<UserJourneys>` elementu.
1. Zmień nazwę Identyfikatora hello hello nowego użytkownika podróży (na przykład zmienić nazwę jako `SignUpOrSignUsingContoso`).

### <a name="display-hello-button"></a>Wyświetl hello "button"

Witaj `<ClaimsProviderSelection>` element jest przycisk dostawcy tożsamości analogiczne tooan na ekranie konta-konta/logowania. Jeśli dodasz `<ClaimsProviderSelection>` elementu dla usługi Azure AD, nowy przycisk zostaną wyświetlone po wyładowuje użytkownika na stronie powitania. tooadd tego elementu:

1. Znajdź hello `<OrchestrationStep>` węzła, który zawiera `Order="1"` w podróży użytkownika hello, który został właśnie utworzony.
1. Dodaj następujące hello:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. Ustaw `TargetClaimsExchangeId` tooan odpowiednią wartość. Zaleca się następujące hello sam Konwencji jako inne:  *\[ClaimProviderName\]Exchange*.

### <a name="link-hello-button-tooan-action"></a>Akcja tooan przycisku hello łącza

Teraz, gdy masz przycisku w miejscu, należy toolink go tooan akcji. Akcja Hello jest dla usługi Azure AD B2C toocommunicate z usługi Azure AD tooreceive w takim przypadku tokenu. Łącze hello tooan Akcja przycisku przez łączenie hello techniczne profilu dla dostawcy oświadczeń usługi Azure AD:

1. Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.
1. Dodaj następujące hello:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. Aktualizacja `Id` toohello samą wartość jak `TargetClaimsExchangeId` w powyższej sekcji hello.
1. Aktualizacja `TechnicalProfileReferenceId` toohello identyfikator hello techniczne profilu utworzonego wcześniej (ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Przekaż hello zaktualizowane rozszerzenie pliku

Po zakończeniu modyfikowania hello rozszerzenia pliku. Zapisz go. Następnie przekaż plik hello i upewnij się, że wszystkie operacje sprawdzania poprawności powiodło się.

### <a name="update-hello-rp-file"></a>Zaktualizuj plik RP hello

Teraz należy tooupdate hello jednostki uzależnionej strony (RP) pliku, który inicjuje przebieg użytkownika hello, który został właśnie utworzony:

1. Utwórz kopię SignUpOrSignIn.xml w katalogu roboczym i zmień jego nazwę (na przykład, zmień jego nazwę tooSignUpOrSignInWithAAD.xml).
1. Nowy plik i aktualizacji hello hello Otwórz `PolicyId` atrybutu dla `<TrustFrameworkPolicy>` unikatowe wartości (na przykład SignUpOrSignInWithAAD). <br> To będzie nazwa hello zasad (na przykład B2C\_1A\_SignUpOrSignInWithAAD).
1. Modyfikowanie hello `ReferenceId` atrybutu w `<DefaultUserJourney>` toomatch identyfikator hello hello nowy przebieg użytkownika utworzony (SignUpOrSignUsingContoso).
1. Zapisz zmiany i przekaż plik hello.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Testowanie hello niestandardowych zasad, które przekazanym właśnie otwierając jego bloku i klikając pozycję **Uruchom teraz**. toodiagnose problemów, przeczytaj o [Rozwiązywanie problemów z](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Następne kroki

Wyrazić swoją opinię za[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
