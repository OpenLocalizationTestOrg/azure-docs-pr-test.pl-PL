---
title: "Usługa Azure Active Directory B2C: Pobierania tokenu przy użyciu aplikacji systemu Android | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate aplikację systemu Android, który korzysta z tożsamości użytkowników usługi Azure Active Directory B2C toomanage AppAuth i uwierzytelnianie użytkowników."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a>Usługa Azure AD B2C: Zaloguj się przy użyciu aplikacji systemu Android

korzysta z platformą tożsamości Microsoft Hello Otwórz standardy, takie jak OAuth2 i OpenID Connect. Dzięki temu deweloperzy mogą tooleverage żadnej biblioteki życzą toointegrate z naszych usług. Deweloperzy tooaid przy użyciu platformy z innych bibliotek, możemy napisanych kilka wskazówki, takich jak ta toodemonstrate jeden sposób tooconfigure 3 bibliotek tooconnect toohello Microsoft tożsamość platformy firmy. Większość bibliotek, które implementują [specyfikację RFC6749 OAuth2 hello](https://tools.ietf.org/html/rfc6749) będą mogli tooconnect toohello pakietu Microsoft Identity platformy.

> [!WARNING]
> Firma Microsoft zapewnia poprawki dla 3rd strony biblioteki i nie przeprowadził Przegląd tych bibliotek. W tym przykładzie używa 3 biblioteki firmy o nazwie AppAuth, które zostały przetestowane zgodność w podstawowe scenariusze z hello Azure AD B2C. Problemy i żądania funkcji powinny być projekt open source ukierunkowanej toohello biblioteki. Zobacz [w tym artykule](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) Aby uzyskać więcej informacji.  
>
>

W przypadku nowych tooOAuth2 lub OpenID Connect znacznie to przykładowa konfiguracja może nie mieć wiele tooyou znaczeniu. Firma Microsoft zaleca, Obejrzyj krótkie [Omówienie protokołu hello mamy już opisanych tutaj](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Tworzenie katalogu usługi Azure AD B2C

Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę. Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów. Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.

## <a name="create-an-application"></a>Tworzenie aplikacji

Następnie należy toocreate aplikację w katalogu usługi B2C. Dzięki temu informacji usługi Azure AD, że wymaga ona toocommunicate bezpiecznie z aplikacją. toocreate aplikacji mobilnej, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md). Należy pamiętać o wykonaniu następujących czynności:

* Obejmują **Native Client** w aplikacji hello.
* Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji. Będzie on potrzebny później.
* Konfigurowanie klienta natywnego **identyfikator URI przekierowania** (np. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). On również będzie później potrzebny.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Tworzenie zasad

W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md). Ta aplikacja zawiera jeden obsługi tożsamości: połączone logowania i rejestrowania. Należy toocreate te zasady, zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Po utworzeniu hello zasad należy koniecznie:

* Wybierz hello **Nazwa wyświetlana** jako atrybut rejestracji w zasadach.
* Wybierz hello **Nazwa wyświetlana** i **obiektu o identyfikatorze** oświadczenia aplikacji we wszystkich zasadach. Można również wybrać inne oświadczenia.
* Kopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu. Powinien on mieć prefiks hello `b2c_1_`.  Nazwa zasad hello będą potrzebne później.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Po utworzeniu zasad, wszystko jest gotowe toobuild aplikacji.

## <a name="download-hello-sample-code"></a>Pobierz hello przykładowy kod

Firma Microsoft umieściła próbki pracy, który korzysta z usługi Azure AD B2C AppAuth [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Można pobrać kodu hello i uruchom go. Możesz szybko rozpocząć pracę z własną aplikację przy użyciu konfigurację usługi Azure AD B2C, wykonując następujące instrukcje hello hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).

przykład Hello jest modyfikacji próbki hello dostarczonych przez [AppAuth](https://openid.github.io/AppAuth-Android/). Odwiedź ich toolearn strony więcej informacji na temat AppAuth i ich funkcje.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modyfikowanie toouse Twojej aplikacji usługi Azure AD B2C z AppAuth

> [!NOTE]
> AppAuth obsługuje 16 interfejsu API systemu Android (Jellybean) lub nowszym. Firma Microsoft zaleca używanie 23 interfejsu API i powyżej.
>

### <a name="configuration"></a>Konfiguracja

Komunikację z usługą Azure AD B2C można skonfigurować albo odnajdywania hello określania identyfikatora URI lub podając zarówno punktu końcowego autoryzacji hello, jak i punktu końcowego tokena identyfikatorów URI. W obu przypadkach należy hello następujących informacji:

* Identyfikator dzierżawcy (np. contoso.onmicrosoft.com)
* Nazwa zasad (np. B2C\_1\_SignUpIn)

Jeśli wybierzesz tooautomatically odnajdywanie hello autoryzacji i tokena punktu końcowego identyfikatory URI, konieczne będą informacje toofetch z odnajdywania hello identyfikatora URI. Hello odnajdywania, zastępując hello dzierżawcy można wygenerować identyfikatora URI\_identyfikator i hello zasad\_nazwy w hello następującego adresu URL:

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

Można następnie uzyskać hello autoryzacji i tokena punktu końcowego identyfikatorów URI i utworzenia obiektu AuthorizationServiceConfiguration, uruchamiając następujące hello:

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

Zamiast używać odnajdywania tooobtain hello autoryzacji i tokena punktu końcowego identyfikatory URI, można również określić je jawnie przez zastąpienie hello dzierżawy\_identyfikator i hello zasad\_nazwą w hello URL poniżej:

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

Uruchom hello poniższy kod toocreate obiektu AuthorizationServiceConfiguration:

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a>Autoryzowanie

Po Konfigurowanie lub pobieranie konfiguracji usługi autoryzacji, można utworzyć żądania autoryzacji. Witaj toocreate żądania, konieczne będzie hello następujących informacji:

* Identyfikator klienta (np. 00000000-0000-0000-0000-000000000000)
* Identyfikator URI przekierowania z schematu niestandardowego (np. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)

Oba elementy powinny zostały zapisane, gdy użytkownik [rejestrowanie aplikacji](#create-an-application).

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

Zobacz toohello [przewodnik AppAuth](https://openid.github.io/AppAuth-Android/) w sposób toocomplete hello resztę procesu hello. Jeśli potrzebujesz tooquickly rozpocząć pracę z aplikacją pracy, zapoznaj się z [naszej próbki](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Wykonaj kroki hello hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter konfigurację usługi Azure AD B2C.

Jesteśmy zawsze toofeedback otwarte i sugestie! Jeśli masz trudności w tym temacie lub mają zalecenia dotyczące poprawy tej zawartości, prosimy o wyrażenie opinii u dołu hello hello strony. Funkcja żądań, dodaj ich zbyt[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

