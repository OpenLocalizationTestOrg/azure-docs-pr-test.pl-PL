---
title: "Usługa Azure Active Directory B2C: Wprowadzenie do zasad niestandardowych | Dokumentacja firmy Microsoft"
description: "Jak tooget wprowadzenie do zasad niestandardowych usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a>Usługa Azure Active Directory B2C: Wprowadzenie do zasad niestandardowych

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Po wykonaniu kroków hello w tym artykule zasad niestandardowych będzie obsługiwać "konta lokalnego" rejestracji lub logowania za pomocą adresu e-mail i hasło. Zostanie również przygotować swoje środowisko do dodawania dostawcy tożsamości (takich jak Facebook lub Azure Active Directory). Firma Microsoft zachęca toocomplete te kroki przed przeczytaniem o innych zastosowań hello Azure Active Directory (Azure AD) B2C tożsamości środowiska Framework.

## <a name="prerequisites"></a>Wymagania wstępne

Przed kontynuowaniem upewnij się, że masz dzierżawę usługi Azure AD B2C, który jest kontenerem dla wszystkich użytkowników, aplikacji, zasad i. Jeśli nie masz już, należy za[tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md). Firma Microsoft zachęca wszystkich deweloperów hello toocomplete wskazówki dotyczące wbudowanych zasad usługi Azure AD B2C i konfigurowanie aplikacji przy użyciu wbudowanych zasad przed kontynuowaniem. Aplikacje będą działać z obydwu typach zasad po wprowadzeniu zmiany pośredniej toohello zasad nazwa tooinvoke hello zasady niestandardowe.

>[!NOTE]
>Edytowanie zasad niestandardowych tooaccess należy dzierżawy połączonego tooyour ważnej subskrypcji platformy Azure. Jeśli nie zostało to jeszcze [połączone z tooan dzierżawy usługi Azure AD B2C subskrypcji platformy Azure](active-directory-b2c-how-to-enable-billing.md) lub subskrypcji platformy Azure jest wyłączona, przycisk Framework obsługi tożsamości hello nie będzie dostępny.

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a>Dodaj podpisywania i szyfrowania dzierżawy tooyour B2C klucze do użytku przez zasady niestandardowe

1. Otwórz hello **Framework obsługi tożsamości** bloku w ustawieniach dzierżawy usługi Azure AD B2C.
2. Wybierz **zasad kluczy** klawiszy hello tooview dostępnych w dzierżawie.
3. Utwórz B2C_1A_TokenSigningKeyContainer, jeśli nie istnieje:<br>
    a. Wybierz pozycję **Dodaj**. <br>
    b. Wybierz **Generowanie**.<br>
    c. Aby uzyskać **nazwa**, użyj `TokenSigningKeyContainer`. <br> 
    Prefiks Hello `B2C_1A_` mogą być dodawane automatycznie.<br>
    d. Aby uzyskać **typ klucza**, użyj **RSA**.<br>
    e. Aby uzyskać **dat**, użyj wartości domyślnych hello. <br>
    f. Aby uzyskać **użycie klucza**, użyj **podpisu**.<br>
    g. Wybierz pozycję **Utwórz**.<br>
4. Utwórz B2C_1A_TokenEncryptionKeyContainer, jeśli nie istnieje:<br>
 a. Wybierz pozycję **Dodaj**.<br>
 b. Wybierz **Generowanie**.<br>
 c. Aby uzyskać **nazwa**, użyj `TokenEncryptionKeyContainer`. <br>
   Prefiks Hello `B2C_1A`_ mogą być dodawane automatycznie.<br>
 d. Aby uzyskać **typ klucza**, użyj **RSA**.<br>
 e. Aby uzyskać **dat**, użyj wartości domyślnych hello.<br>
 f. Aby uzyskać **użycie klucza**, użyj **szyfrowania**.<br>
 g. Wybierz pozycję **Utwórz**.<br>
5. Utwórz B2C_1A_FacebookSecret. <br>
Jeśli masz już klucz tajny aplikacji Facebook, dodaj go jako zasady tooyour klucza dzierżawy. W przeciwnym razie należy utworzyć hello klucza o wartości symbolu zastępczego, aby zasad przeszedł pomyślnie weryfikacji.<br>
 a. Wybierz pozycję **Dodaj**.<br>
 b. Aby uzyskać **opcje**, użyj **ręcznego**.<br>
 c. Aby uzyskać **nazwa**, użyj `FacebookSecret`. <br>
 Prefiks Hello `B2C_1A_` mogą być dodawane automatycznie.<br>
 d. W hello **klucz tajny** wprowadź FacebookSecret Twojego z developers.facebook.com lub `0` jako symbol zastępczy. *To nie jest identyfikatorem aplikacji usługi Facebook* <br>
 e. Aby uzyskać **użycie klucza**, użyj **podpisu**. <br>
 f. Wybierz **Utwórz** i potwierdzić tworzenie.

## <a name="register-identity-experience-framework-applications"></a>Rejestrowanie aplikacji w ramach obsługi tożsamości

Usługa Azure AD B2C wymaga tooregister dwóch dodatkowych aplikacji, które są używane przez hello aparat toosign się i zaloguj się użytkownicy.

>[!NOTE]
>Należy utworzyć dwie aplikacje tego włączyć logowanie przy użyciu kont lokalnych: IdentityExperienceFramework (aplikacji sieci web) i ProxyIdentityExperienceFramework (aplikacji natywnej) z delegowane uprawnienia na powitania IdentityExperienceFramework aplikacji. Konta lokalne istnieje tylko w dzierżawie. Użytkownicy konto z tooaccess kombinacja adresu i hasła unikatowego adresu e-mail zarejestrowany dzierżawy aplikacji.

### <a name="create-hello-identityexperienceframework-application"></a>Tworzenie aplikacji IdentityExperienceFramework hello

1. W hello [portalu Azure](https://portal.azure.com), przejdź do hello [kontekstu dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md).
2. Otwórz hello **usługi Azure Active Directory** bloku (nie hello **usługi Azure AD B2C** bloku). Może być konieczne tooselect **więcej usług** toofind go.
3. Wybierz **rejestracji aplikacji**.
4. Wybierz **nowej rejestracji aplikacji**.
   * Aby uzyskać **nazwa**, użyj `IdentityExperienceFramework`.
   * Aby uzyskać **typu aplikacji**, użyj **aplikacji/interfejs API sieci Web**.
   * Dla **adres URL logowania**, użyj `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, gdzie `yourtenant` oznacza nazwę domeny dzierżawy usługi Azure AD B2C.
5. Wybierz pozycję **Utwórz**.
6. Po utworzeniu, wybierz aplikację hello nowo utworzony **IdentityExperienceFramework**.<br>
   * Wybierz **właściwości**.<br>
   * Skopiuj identyfikator aplikacji hello i zapisz je.

### <a name="create-hello-proxyidentityexperienceframework-application"></a>Tworzenie aplikacji ProxyIdentityExperienceFramework hello

1. Wybierz **rejestracji aplikacji**.
1. Wybierz **nowej rejestracji aplikacji**.
   * Aby uzyskać **nazwa**, użyj `ProxyIdentityExperienceFramework`.
   * Dla **typu aplikacji**, użyj **natywnego**.
   * Dla **identyfikator URI przekierowania**, użyj `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, gdzie `yourtenant` jest dzierżawy usługi Azure AD B2C.
1. Wybierz pozycję **Utwórz**.
1. Po utworzeniu, wybierz aplikację hello **ProxyIdentityExperienceFramework**.<br>
   * Wybierz **właściwości**. <br>
   * Skopiuj identyfikator aplikacji hello i zapisz je.
1. Wybierz **wymagane uprawnienia**.
1. Wybierz pozycję **Dodaj**.
1. Wybierz **wybierz interfejs API**.
1. Wyszukaj nazwę hello IdentityExperienceFramework. Wybierz **IdentityExperienceFramework** w hello wyniki, a następnie kliknij przycisk **wybierz**.
1. Zaznacz pole wyboru hello obok zbyt**IdentityExperienceFramework dostępu**, a następnie kliknij przycisk **wybierz**.
1. Wybierz **gotowe**.
1. Wybierz **udzielanie uprawnień**, a następnie potwierdź wybierając **tak**.

## <a name="download-starter-pack-and-modify-policies"></a>Pobierz pakiet starter i modyfikowania zasad

Zasady niestandardowe są zestaw plików XML, które wymagają dzierżawy usługi Azure AD B2C tooyour toobe przekazany. Firma Microsoft udostępnia tooget pakiety startowe mimo to szybko. Każdy pakiet starter w hello następujące listy zawiera hello najmniejszą liczbę profilów technicznych i podróże użytkownika wymagane opisane scenariusze hello tooachieve:
 * LocalAccounts. Umożliwia użycie hello tylko kont lokalnych.
 * SocialAccounts. Umożliwia korzystanie hello tylko kont społecznościowych (lub federacyjnych).
 * **SocialAndLocalAccounts**. Przewodnik hello korzystamy z tego pliku.
 * SocialAndLocalAccountsWithMFA. Włącza się tu opcje społecznych, lokalne i uwierzytelniania wieloskładnikowego.

Każdy pakiet początkowy zawiera:

* Witaj [pliku podstawowego](active-directory-b2c-overview-custom.md#policy-files) hello zasad. Kilka zmian są wymagane toohello podstawowej.
* Witaj [plik rozszerzenia](active-directory-b2c-overview-custom.md#policy-files) hello zasad.  Ten plik jest, gdzie większość zmiany konfiguracji zostały wprowadzone.
* [Jednostki uzależnionej plików firm](active-directory-b2c-overview-custom.md#policy-files) są pliki specyficzne dla zadania o nazwie przez aplikację.

>[!NOTE]
>Jeśli w edytorze XML obsługuje sprawdzanie poprawności, sprawdź pliki hello względem schematu TrustFrameworkPolicy_0.3.0.0.xsd XML hello, który znajduje się w katalogu głównym hello hello początkowego pakietu. Sprawdzanie poprawności schematu XML identyfikuje błędy przed przesłaniem.

 Rozpocznijmy:

1. Pobierz active-directory-b2c-custom-policy-starterpack z usługi GitHub. [Pobierz plik zip hello](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) lub uruchom

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. Otwórz hello SocialAndLocalAccounts folder.  plik podstawowy Hello (TrustFrameworkBase.xml) w tym folderze zawartość wymagane dla kont lokalnych i społecznego/firmowej. zawartość społecznościowych Hello nie zakłóca hello kroki pobierania kont lokalnych w i uruchomiony.
3. Otwórz TrustFrameworkBase.xml. Jeśli potrzebujesz edytora XML [spróbuj Visual Studio Code](https://code.visualstudio.com/download), lekkie edytora i platform.
4. W katalogu głównym hello `TrustFrameworkPolicy` element, hello aktualizacji `TenantId` i `PublicPolicyUri` atrybuty, zastępując `yourtenant.onmicrosoft.com` hello nazwę domeny dzierżawy usługi Azure AD B2C:
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   >`PolicyId`to nazwa zasady hello widoczny w portalu hello i nazwa hello za pomocą którego ten plik zasad jest używany przez inne pliki zasad.

5. Zapisz plik hello.
6. Otwórz TrustFrameworkExtensions.xml. Zmiany hello tego samego dwóch zastępując `yourtenant.onmicrosoft.com` z dzierżawą usługi Azure AD B2C. Upewnij się, hello same zastąpienie w hello `<TenantId>` elementu dla wszystkich trzech zmian. Zapisz plik hello.
7. Otwórz SignUpOrSignIn.xml. Zmiany hello tego samego zastępując `yourtenant.onmicrosoft.com` z dzierżawą usługi Azure AD B2C w trzech miejscach. Zapisz plik hello.
8. Resetowania hasła hello otwarte i profilu edytowanie plików. Zmiany hello tego samego zastępując `yourtenant.onmicrosoft.com` z dzierżawą usługi Azure AD B2C w trzech miejscach w każdym pliku. Zapisywanie plików hello.

### <a name="add-hello-application-ids-tooyour-custom-policy"></a>Dodaj zasady niestandardowe tooyour identyfikatory aplikacji hello
Dodawanie pliku rozszerzeń toohello identyfikatory aplikacji hello (`TrustFrameworkExtensions.xml`):

1. W hello rozszerzenia plików (TrustFrameworkExtensions.xml), Znajdź hello element `<TechnicalProfile Id="login-NonInteractive">`.
2. Zastąp oba wystąpienia `IdentityExperienceFrameworkAppId` z Identyfikatorem aplikacji hello hello aplikacji Framework obsługi tożsamości, utworzony wcześniej. Oto przykład:

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. Zastąp oba wystąpienia `ProxyIdentityExperienceFrameworkAppId` z Identyfikatorem aplikacji hello hello Framework obsługi tożsamości serwera Proxy aplikacji, utworzony wcześniej.
4. Zapisz plik rozszerzenia.

## <a name="upload-hello-policies-tooyour-tenant"></a>Przekaż hello zasady tooyour dzierżawy

1. W hello [portalu Azure](https://portal.azure.com), przejdź do hello [kontekstu dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)i otwórz hello **usługi Azure AD B2C** bloku.
2. Wybierz **Framework obsługi tożsamości**.
3. Wybierz **przekazywać zasady**.

    >[!WARNING]
    >pliki zasad niestandardowych Hello, należy przekazać hello w następującej kolejności:

1. Przekaż TrustFrameworkBase.xml.
2. Przekaż TrustFrameworkExtensions.xml.
3. Przekaż SignUpOrSignin.xml.
4. Przekazywanie plików zasad.

Po przekazaniu pliku hello nazwę pliku zasad hello jest poprzedzony przez `B2C_1A_`.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Testowanie zasad niestandardowych hello przy użyciu Uruchom teraz

1. Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.

   >[!NOTE]
   >**Uruchom teraz** wymaga co najmniej jedną aplikację toobe preregistered hello dzierżawcy. Aplikacji musi być zarejestrowana w dzierżawie powitalnych B2C, przy użyciu hello **aplikacji** zaznaczenia menu w usłudze Azure AD B2C lub za pomocą tooinvoke Framework obsługi tożsamości hello zarówno wbudowanych i niestandardowych zasad. Wymagany jest tylko jedna rejestracja na aplikację.<br><br>
   toolearn tooregister aplikacji, zobacz temat hello Azure AD B2C [wprowadzenie](active-directory-b2c-get-started.md) artykułu lub hello [Rejestracja aplikacji](active-directory-b2c-app-registration.md) artykułu.  

2. Otwórz B2C_1A_signup_signin, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany. Wybierz **Uruchom teraz**.

3. Powinno być możliwe toosign przy użyciu adresu e-mail.

4. Zaloguj się przy użyciu hello, tego samego konta tooconfirm, czy masz hello prawidłowej konfiguracji.

>[!NOTE]
>Częstą przyczyną niepowodzenia logowania jest nieprawidłowo skonfigurowana aplikacji IdentityExperienceFramework.


## <a name="next-steps"></a>Następne kroki

### <a name="add-facebook-as-an-identity-provider"></a>Dodaj funkcję dostawcy tożsamości usługi Facebook
tooset się Facebook:
1. [Konfigurowanie aplikacji usługi Facebook w developers.facebook.com](active-directory-b2c-setup-fb-app.md).
2. [Dodaj dzierżawy tooyour tajny usługi Azure AD B2C aplikacji usługi Facebook hello](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).
3. W pliku zasad TrustFrameworkExtensions hello, zastąp wartość hello `client_id` identyfikator aplikacji Facebook hello:

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. Przekaż hello TrustFrameworkExtensions.xml zasad pliku tooyour dzierżawy.
5. Test przy użyciu **Uruchom teraz** lub za pomocą zasad hello bezpośrednio w zarejestrowany aplikacji.

### <a name="add-azure-active-directory-as-an-identity-provider"></a>Dodaj funkcję dostawcy tożsamości usługi Azure Active Directory
Hello pliku podstawowego użyty w tym przewodniku Rozpoczęto pobieranie zawiera niektóre hello zawartość, która należy do dodawania innych dostawców tożsamości. Aby uzyskać informacje na temat konfigurowania logowania, zobacz hello [usługi Azure Active Directory B2C: Zaloguj się przy użyciu konta usługi Azure AD](active-directory-b2c-setup-aad-custom.md) artykułu.

Omówienie zasad niestandardowych w usłudze Azure AD B2C, które używają hello Framework obsługi tożsamości, zobacz hello [usługi Azure Active Directory B2C: zasady niestandardowe](active-directory-b2c-overview-custom.md) artykułu. 
