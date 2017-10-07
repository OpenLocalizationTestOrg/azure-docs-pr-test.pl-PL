---
title: "Uzyskiwanie tokenu przy użyciu aplikacji systemu iOS — usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate aplikację systemu iOS, która korzysta z tożsamości użytkowników usługi Azure Active Directory B2C toomanage AppAuth i uwierzytelnianie użytkowników."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>Usługa Azure AD B2C: Zaloguj się przy użyciu aplikacji systemu iOS

korzysta z platformą tożsamości Microsoft Hello Otwórz standardy, takie jak OAuth2 i OpenID Connect. Przy użyciu standardowego protokołu zapewniającego Otwórz oferuje większy wybór developer, wybierając toointegrate biblioteki z naszych usług. Przygotowaliśmy tego przewodnika oraz innym osobom podoba Ci się tooaid deweloperom pisanie aplikacje łączące toohello platformy pakietu Microsoft Identity. Większość bibliotek, które implementują [specyfikację RFC6749 OAuth2 hello](https://tools.ietf.org/html/rfc6749) są możliwe tooconnect toohello pakietu Microsoft Identity platformy.

> [!WARNING]
> Firma Microsoft zapewnia poprawki dla bibliotek innych firm, a nie przeprowadził Przegląd tych bibliotek. Ten przykład jest przy użyciu biblioteki innej firmy o nazwie AppAuth, które zostały przetestowane zgodność w podstawowe scenariusze z hello Azure AD B2C. Problemy i żądania funkcji powinny być projekt open source ukierunkowanej toohello biblioteki. Więcej informacji znajduje się w [tym artykule](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).
>
>

Jeśli nowy tooOAuth2 lub OpenID Connect znacznie to przykładowa konfiguracja może nie mieć znacznie tooyou znaczeniu. Firma Microsoft zaleca, Obejrzyj krótkie [Omówienie protokołu hello mamy już opisanych tutaj](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Tworzenie katalogu usługi Azure AD B2C
Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę. Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i inne. Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.

## <a name="create-an-application"></a>Tworzenie aplikacji
Następnie należy toocreate aplikację w katalogu usługi B2C. rejestracji aplikacji Hello zawiera informacje usługi Azure AD, że wymaga ona toocommunicate bezpiecznie z aplikacją. toocreate aplikacji mobilnej, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md). Należy pamiętać o wykonaniu następujących czynności:

* Obejmują **Native client** w aplikacji hello.
* Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji. Ten identyfikator GUID jest potrzebny później.
* Konfigurowanie **identyfikator URI przekierowania** z schematu niestandardowego (na przykład com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Ten identyfikator URI potrzebne później.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Tworzenie zasad
W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md). Ta aplikacja zawiera jeden obsługi tożsamości: połączone logowania i rejestrowania. Utwórz te zasady, zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Po utworzeniu hello zasad należy koniecznie:

* W obszarze **atrybuty rejestracji**, wybierz atrybut hello **Nazwa wyświetlana**.  Możesz wybrać także inne atrybuty.
* W obszarze **oświadczenia aplikacji**, wybierz oświadczeń hello **Nazwa wyświetlana** i **Identyfikatora obiektu użytkownika**. Możesz wybrać także inne oświadczenia.
* Kopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu. Nazwę zasad jest prefiksem `b2c_1_` podczas zapisywania hello zasad.  Nazwa zasad hello potrzebne później.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Po utworzeniu zasad, wszystko jest gotowe toobuild aplikacji.

## <a name="download-hello-sample-code"></a>Pobierz hello przykładowy kod
Firma Microsoft umieściła próbki pracy, który korzysta z usługi Azure AD B2C AppAuth [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Można pobrać kodu hello i uruchom go. toouse dzierżawy własne usługi Azure AD B2C, wykonaj te instrukcje hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).

W tym przykładzie został utworzony przez instrukcjami README hello przez hello [iOS AppAuth projektu w witrynie GitHub](https://github.com/openid/AppAuth-iOS). Aby uzyskać więcej informacji na temat działania przykładowe hello i biblioteki hello odwołanie hello README AppAuth w witrynie GitHub.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modyfikowanie toouse Twojej aplikacji usługi Azure AD B2C z AppAuth

> [!NOTE]
> AppAuth obsługuje system iOS 7 lub nowszym.  Jednak toosupport logowania społecznościowych Google, SFSafariViewController jest potrzebna, które wymaga systemu iOS 9 lub nowszą.
>

### <a name="configuration"></a>Konfiguracja

Komunikację można skonfigurować z usługi Azure AD B2C, określając zarówno punktu końcowego autoryzacji hello, jak i punktu końcowego tokena identyfikatorów URI.  toogenerate tych identyfikatorów należy hello następujących informacji:
* Identyfikator dzierżawcy (np. contoso.onmicrosoft.com)
* Nazwa zasady (na przykład B2C\_1\_SignUpIn)

Witaj punktu końcowego tokena identyfikatora URI może zostać wygenerowany przez zastąpienie hello dzierżawy\_identyfikator i hello zasad\_nazwy w hello następującego adresu URL:

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

Witaj zastępując można wygenerować identyfikatora URI punktu końcowego autoryzacji hello dzierżawy\_identyfikator i hello zasad\_nazwy w hello następującego adresu URL:

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

Uruchom hello poniższy kod toocreate obiektu AuthorizationServiceConfiguration:

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a>Autoryzowanie

Po Konfigurowanie lub pobieranie konfiguracji usługi autoryzacji, można utworzyć żądania autoryzacji. Witaj toocreate żądania, należy hello następujących informacji:  
* Identyfikator klienta (na przykład 00000000-0000-0000-0000-000000000000)
* Identyfikator URI przekierowania z schematu niestandardowego (na przykład com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)

Oba elementy powinny zostały zapisane, gdy użytkownik [rejestrowanie aplikacji](#create-an-application).

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

tooset się Twojej aplikacji toohandle hello przekierowania toohello URI ze schematem niestandardowych hello, tooupdate hello listy programów"URL" potrzebne w Twojej Info.pList:
* Otwórz Info.pList.
* Umieść kursor nad wiersza, takie jak "Kod typu systemu operacyjnego pakietu", a następnie kliknij przycisk hello \+ symbolu.
* Zmień nazwę hello nowego wiersza "adres URL typy".
* Kliknij przycisk toohello Strzałka hello "Adres URL typy" tooopen hello drzewa w lewo.
* Kliknij przycisk hello Strzałka toohello lewej "Elementu 0" tooopen hello drzewa.
* Zmień nazwę pierwszego elementu poniżej schematy 0 too'URL elementów.
* Kliknij przycisk toohello Strzałka hello "Schematy adresów URL" tooopen hello drzewa w lewo.
* W kolumnie "Wartość" hello, jest puste pole toohello po lewej "Elementu 0" poniżej "Schematy adresów URL".  Ustawienie aplikacji hello wartość tooyour unikatowy schematu.  wartość Hello musi odpowiadać używany w redirectURL, podczas tworzenia obiektu OIDAuthorizationRequest hello schemat hello.  W naszym przykładzie użyliśmy hello schemat "com.onmicrosoft.fabrikamb2c.exampleapp".

Zobacz toohello [przewodnik AppAuth](https://openid.github.io/AppAuth-iOS/) w sposób toocomplete hello resztę procesu hello. Jeśli potrzebujesz tooquickly rozpocząć pracę z aplikacją pracy, zapoznaj się z [naszej próbki](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Wykonaj kroki hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter konfigurację usługi Azure AD B2C.

Jesteśmy zawsze toofeedback otwarte i sugestie! Jeśli masz trudności w tym temacie lub mają zalecenia dotyczące poprawy tej zawartości, prosimy o wyrażenie opinii u dołu hello hello strony. Funkcja żądań, dodaj ich zbyt[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
