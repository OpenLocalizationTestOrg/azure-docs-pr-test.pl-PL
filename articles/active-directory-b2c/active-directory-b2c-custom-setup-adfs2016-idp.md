---
title: "Usługa Azure Active Directory B2C: Dodawanie usług AD FS jako dostawca tożsamości SAML za pomocą zasad niestandardowych"
description: "Tooarticle instrukcje dotyczące konfigurowania usług AD FS 2016 przy użyciu protokołu SAML i zasad niestandardowych"
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
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a>Usługa Azure Active Directory B2C: Dodawanie usług AD FS jako dostawca tożsamości SAML za pomocą zasad niestandardowych

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

W tym artykule opisano sposób tooenable logowania użytkowników z konta usług AD FS przy użyciu hello [niestandardowych zasad](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Wymagania wstępne

Zakończenie hello etapami hello [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) artykułu.

Kroki te obejmują:

1.  Tworzenie usług AD FS jednostki uzależnionej zaufania.
2.  Dodawanie tooAzure certyfikatu usług AD FS zaufania jednostki uzależnionej hello AD B2C.
3.  Dodawanie zasad tooa dostawcy oświadczeń.
4.  Konta usług AD FS w usłudze rejestrowania hello oświadczeń przebieg użytkownika tooa dostawcy.
5.  Przekazywanie hello tooan zasad usługi Azure AD B2C dzierżawy i przetestować go.

## <a name="toocreate-a-claims-aware-relying-party-trust"></a>toocreate oświadczeń zaufania jednostki uzależnionej

toouse usług AD FS jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate usług AD FS zaufania jednostki uzależnionej i dostarczyć hello prawo parametrów.

tooadd nowe uzależnionej zaufania przy użyciu przystawki Zarządzanie FS hello AD i ręcznie skonfigurować ustawienia hello wykonać hello następujące procedury na serwerze federacyjnym.

Członkostwo w grupie **Administratorzy**, lub równoważnej na komputerze lokalnym hello hello minimalne wymagane toocomplete tej procedury. Szczegółowe informacje o używaniu hello odpowiednich kont i członkostwa w grupach [grupy domyślne w domenie i lokalne](http://go.microsoft.com/fwlink/?LinkId=83477)

1.  W Menedżerze serwera kliknij **narzędzia**, a następnie wybierz **zarządzania usług AD FS**.

2.  Polecenie **Dodawanie zaufania jednostki uzależnionej**.
    ![Dodawanie zaufania jednostki uzależnionej](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)

3.  Na powitania **powitalnej** wybierz pozycję **oświadczeń pamiętać** i kliknij przycisk **Start**.
    ![Na stronie powitalnej hello wybierz oświadczeń pamiętać](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)
4.  Na powitania **wybierz źródło danych** kliknij przycisk **ręcznie wprowadź dane dotyczące jednostki uzależnionej hello**, a następnie kliknij przycisk **dalej**.
    ![Wprowadź dane dotyczące jednostki uzależnionej hello](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)

5.  Na powitania **Określanie nazwy wyświetlanej** wpisz nazwę w **Nazwa wyświetlana**w obszarze **uwagi** wpisz opis tego zaufania jednostki uzależnionej, a następnie kliknij przycisk **dalej** .
    ![Określ nazwę wyświetlaną i uwagi](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)
6.  Opcjonalny. Jeśli masz certyfikat szyfrowania tokenu opcjonalne następnie na powitania **Konfigurowanie certyfikatu** kliknij przycisk **Przeglądaj** toolocate plik certyfikatu, a następnie kliknij przycisk **dalej** .
    ![Konfigurowanie certyfikatu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)
7.  Na powitania **Konfigurowanie adresu URL** strona, wybierz hello **Włącz obsługę protokołu SAML 2.0 WebSSO hello** pole wyboru. W obszarze **URL usługi logowania jednokrotnego SAML 2.0 jednostki uzależnionej w strona**wpisz adres URL punktu końcowego usługi Security (Assertion Markup Language SAML) powitania dla tego zaufania jednostki uzależnionej, a następnie kliknij przycisk **dalej**.  Dla hello **URL usługi logowania jednokrotnego SAML 2.0 jednostki uzależnionej w strona**, Wklej hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`. Zamień na nazwę swojej dzierżawy (na przykład contosob2c.onmicrosoft.com) {dzierżawa} i {zasad} hello Zamień na nazwę zasady rozszerzenia (na przykład B2C_1A_TrustFrameworkExtensions).
    > [!IMPORTANT]
    >Nazwa zasady Hello jest hello jedną dziedziczący signup_or_signin zasady, w tym przypadku jest: `B2C_1A_TrustFrameworkExtensions`.
    >Na przykład można hello adresu URL: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.

    ![Jednostki uzależnionej adres URL strony logowania jednokrotnego SAML 2.0 usługi](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. Na powitania **skonfiguruj identyfikatory** Określ hello tego samego adresu URL jako hello poprzedniego kroku, kliknij przycisk **Dodaj** tooadd ich toohello listy, a następnie kliknij przycisk **dalej**.
    ![Jednostki uzależnionej identyfikatorów zaufania](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)
9.  Na powitania **wybierz zasady kontroli dostępu** wybierz zasady, a następnie kliknij przycisk **dalej**.
    ![Wybierz zasady kontroli dostępu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)
10.  Na powitania **gotowe tooAdd zaufania** , przejrzyj ustawienia hello, a następnie kliknij przycisk **dalej** toosave informacje o zaufaniu jednostki uzależnionej strony.
    ![Zapisz dane zaufania jednostki uzależnionej strony](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)
11.  Na powitania **Zakończ** kliknij przycisk **Zamknij**, ta czynność spowoduje automatyczne wyświetlenie hello **Edycja reguł oświadczeń** okno dialogowe.
    ![Edycja reguł oświadczeń](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)
12. Kliknij przycisk **Dodaj regułę**.  
      ![Dodaj nową regułę](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)
13.  W **szablonu reguły oświadczeń**, wybierz pozycję **Wyślij atrybuty LDAP jako oświadczeń**.
    ![Wybierz Wyślij atrybuty LDAP jako oświadczeń szablonu reguł](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)
14.  Podaj **nazwy reguły oświadczeń**. Dla hello **magazynu atrybutów** wybierz **usługi Active Directory wybierz** Dodaj powitania po oświadczeń, a następnie kliknij przycisk **Zakończ** i **OK**.
    ![Właściwości zestawu reguł](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)
15.  W Menedżerze serwera wybierz **zaufania jednostek uzależnionych** wybierz hello zaufania jednostki uzależnionej został utworzony i kliknij **właściwości**.
    ![Jednostki uzależnionej strony Edytuj właściwości](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)
16.  Witaj jednej jednostki uzależnionej strony zaufania (pokaz B2C) właściwości kliknij **podpisu** i kliknij polecenie **Dodaj**.  
    ![Podpis zestawu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)
17.  Dodaj certyfikat podpisu (bez klucza prywatnego plik .cert).  
    ![Dodaj certyfikat podpisu](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  W oknie Właściwości zaufania (pokaz B2C) jednostki uzależnionej strony powitania kliknij **zaawansowane** karcie i zmień hello **skrótu Secure hash algorithm** za**SHA-1**, kliknij przycisk **Ok**.  
    ![Wartość skrótu secure hash algorithm tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a>Dodaj hello usług AD FS konta aplikacji klucza tooAzure AD B2C
Federacja z kontami usług AD FS wymaga klucza tajnego klienta usług AD FS tootrust konta usługi Azure AD B2C w imieniu aplikacji hello. Należy toostore certyfikatu usług AD FS w dzierżawie usługi Azure AD B2C. 

1.  Przejdź do dzierżawy usługi Azure AD B2C tooyour i wybierz **ustawieniami B2C** > **Framework obsługi tożsamości**
2.  Wybierz **zasad kluczy** klawiszy hello tooview dostępnych w dzierżawie.
3.  Kliknij przycisk **+ Dodaj**.
4.  Aby uzyskać **opcje**, użyj **przekazać**.
5.  Aby uzyskać **nazwa**, użyj `ADFSSamlCert`.  
    Prefiks Hello `B2C_1A_` mogą być dodawane automatycznie.
6.  W hello przekazywania pliku ** wybierz plik .pfx certyfikatu z kluczem prywatnym. Uwaga: ten certyfikat (z kluczem prywatnym hello) powinna być hello, tej samej, który wystawił i używane dla usług AD FS hello jednostki uzależnionej.
![Przekazywanie klucza zasad](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)
7.  Kliknij przycisk **Utwórz**
8.  Upewnij się, że utworzono klucz hello `B2C_1A_ADFSSamlCert`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Dodawanie dostawcy oświadczeń w zasadach rozszerzenia
Jeśli chcesz toosign użytkowników przy użyciu konta usług AD FS, musisz mieć konto usług AD FS toodefine jako dostawcy oświadczeń. Innymi słowy należy toospecify punktu końcowego, który komunikuje się usługi Azure AD B2C. punkt końcowy Hello zawiera zestaw oświadczeń, które są używane przez usługi Azure AD B2C tooverify, który został uwierzytelniony określonego użytkownika.

Zdefiniuj usług AD FS jako dostawcy oświadczeń, dodając `<ClaimsProvider>` węzeł rozszerzenia pliku zasad:

1. Otwórz plik zasad rozszerzenia hello (TrustFrameworkExtensions.xml) z katalogu roboczego. Jeśli potrzebujesz edytora XML [spróbuj Visual Studio Code](https://code.visualstudio.com/download), lekkie edytora i platform.
2. Znajdź hello `<ClaimsProviders>` sekcji
3. Dodaj następujące fragment kodu XML w obszarze hello hello `ClaimsProviders` elementu i zastępowanie `identityProvider` o systemie DNS (dowolną wartość, która wskazuje domenę) i Zapisz plik hello. 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Zarejestruj hello usług AD FS konta oświadczeń dostawcy tooSign się lub zaloguj się w podróży użytkownika
W tym momencie hello dostawcy tożsamości nie został skonfigurowany.  Jednak nie jest dostępna w żadnym hello konta-konta/logowania ekranów. Teraz należy użytkownik tooyour dostawcy tożsamości konta tooadd hello usług AD FS `SignUpOrSignIn` podróży użytkownika. toomake ją, utworzymy duplikatem istniejącej przebieg użytkownika szablonu.  Następnie możemy zmodyfikować go, uwzględniając dostawcy tożsamości usługi AD FS hello:
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  Otwórz plik podstawowy hello zasad (na przykład TrustFrameworkBase.xml).
2.  Znajdź hello `<UserJourneys>` element kopiowania hello całej zawartości i `<UserJourneys>` węzła.
3.  Otwórz plik rozszerzenia hello (na przykład TrustFrameworkExtensions.xml) i Znajdź hello `<UserJourneys>` elementu. Jeśli hello element nie istnieje, dodaj je.
4.  Wklej zawartość całego hello `<UserJournesy>` węzła, który został skopiowany jako element podrzędny hello `<UserJourneys>` elementu.

### <a name="display-hello-button"></a>Przycisk hello wyświetlania
Witaj `<ClaimsProviderSelections>` element definiuje listę hello opcje wyboru dostawcy oświadczeń i ich kolejność.  `<ClaimsProviderSelection>`element jest przycisku dostawcy tożsamości analogiczne tooan na stronie konta-konta/logowania. Jeśli dodasz `<ClaimsProviderSelection>` elementu dla konta usług AD FS, nowy przycisk zostaną wyświetlone po wyładowuje użytkownika na stronie powitania. tooadd tego elementu:

1.  Znajdź hello `<UserJourney>` węzła, który zawiera `Id="SignUpOrSignIn"` w podróży użytkownika hello, które zostały skopiowane.
2.  Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`
3.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a>Akcja tooan przycisku hello łącza

Teraz, gdy masz przycisku w miejscu, należy toolink go tooan akcji. Akcja Hello jest dla usługi Azure AD B2C toocommunicate z tooreceive konta usług AD FS w takim przypadku tokenu. Łącze hello tooan Akcja przycisku przez łączenie hello techniczne profilu dla dostawcy oświadczeń konta usług AD FS:

1.  Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.
2.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * Upewnij się, hello `Id` ma takie same wartości jak hello `TargetClaimsExchangeId` w powyższej sekcji hello.
> * Upewnij się, `TechnicalProfileReferenceId` ustawiono profil techniczne toohello utworzony wcześniej (Contoso-SAML2).

## <a name="upload-hello-policy-tooyour-tenant"></a>Przekaż hello zasad tooyour dzierżawy
1.  W hello [portalu Azure](https://portal.azure.com), przejdź do hello [kontekstu dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)i otwórz hello **usługi Azure AD B2C** bloku.
2.  Wybierz **Framework obsługi tożsamości**.
3.  Otwórz hello **wszystkie zasady** bloku.
4.  Wybierz **przekazywać zasady**.
5.  Sprawdź **zastąpić hello zasady, jeśli istnieje** pole.
6.  **Przekaż** TrustFrameworkExtensions.xml i upewnij się, że nie wystąpi niepowodzenie weryfikacji hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Testowanie zasad niestandardowych hello przy użyciu Uruchom teraz
1.  Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.
2.  Otwórz **B2C_1A_signup_signin**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany. Wybierz **Uruchom teraz**.
3.  Powinno być możliwe toosign za pomocą konta usług AD FS.

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a>[Opcjonalnie] Zarejestruj przebieg użytkownika edycji tooProfile dostawcy oświadczeń hello usług AD FS konta
Możesz dostawcy tożsamości konta usług AD FS hello tooadd również użytkownika tooyour `ProfileEdit` podróży użytkownika. toomake ją, powtórz firma Microsoft hello ostatnie dwa kroki:

### <a name="display-hello-button"></a>Przycisk hello wyświetlania
1.  Otwórz plik rozszerzenia hello zasad (na przykład TrustFrameworkExtensions.xml).
2.  Znajdź hello `<UserJourney>` węzła, który zawiera `Id="ProfileEdit"` w podróży użytkownika hello, które zostały skopiowane.
3.  Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`
4.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Akcja tooan przycisku hello łącza
1.  Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.
2.  Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Testowanie zasad niestandardowych edycji profilu hello przy użyciu Uruchom teraz
1.  Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.
2.  Otwórz **B2C_1A_ProfileEdit**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany. Wybierz **Uruchom teraz**.
3.  Powinno być możliwe toosign za pomocą konta usług AD FS.

## <a name="download-hello-complete-policy-files"></a>Pobierz pliki zasad pełną hello
Opcjonalnie: Zaleca się kompilacji danego scenariusza przy użyciu własnych niestandardowych zasad plików po zakończeniu hello przeprowadzenie wprowadzenie zasady niestandardowe. [Pliki przykładowe zasady jedynie do celów referencyjnych](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
