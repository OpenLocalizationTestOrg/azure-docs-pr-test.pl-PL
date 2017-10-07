---
title: "Sieci Web logowania z OpenID Connect - usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji sieci web przy użyciu usługi Azure Active Directory hello implementacji protokołu uwierzytelniania OpenID Connect hello"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 21d420c8-3c10-4319-b681-adf2e89e7ede
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 89e9cfa28e4e5c34304aea355cca2dd0c4b42abc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-web-sign-in-with-openid-connect"></a>Usługa Azure Active Directory B2C: Sieci Web logowania z OpenID Connect
OpenID Connect to protokół uwierzytelniania, rozszerzający OAuth 2.0, które mogą być używane toosecurely logowania użytkowników w aplikacjach tooweb. Przy użyciu wdrażania protokołu OpenID Connect (Azure AD B2C) hello Azure Active Directory B2C, można zewnętrzny rejestrację, logowanie i wykonywania innych zarządzania tożsamościami w tooAzure aplikacji sieci web usługi Active Directory (Azure AD). W tym przewodniku przedstawiono sposób toodo tak w sposób niezależny od języka. Opisuje sposób toosend i odbieranie wiadomości HTTP bez przy użyciu dowolnej z naszych bibliotekach open source.

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) rozszerza hello OAuth 2.0 *autoryzacji* protokół do użycia jako *uwierzytelniania* protokołu. Dzięki temu można tooperform logowania jednokrotnego przy użyciu uwierzytelniania OAuth. Wprowadza ona pojęcia hello *token Identyfikatora*, który jest token zabezpieczający, który umożliwia powitania klienta tooverify hello tożsamości użytkownika hello i uzyskać profilu podstawowe informacje o użytkowniku hello.

Ponieważ rozszerza on OAuth 2.0, umożliwia również uzyskanie toosecurely aplikacji *tokenów dostępu*. Można użyć access_tokens tooaccess zasoby, które są zabezpieczone przez [serwera autoryzacji](active-directory-b2c-reference-protocols.md#the-basics). Zalecamy OpenID Connect, jeśli tworzysz aplikację sieci web jest hostowany na serwerze i dostępne za pośrednictwem przeglądarki. Jeśli chcesz tooadd tożsamości zarządzania tooyour aplikacji mobilnych lub komputerowych, za pomocą usługi Azure AD B2C, należy użyć [OAuth 2.0](active-directory-b2c-reference-oauth-code.md) zamiast OpenID Connect.

Usługa Azure AD B2C rozszerza hello standardowe OpenID Connect toodo protokołu więcej niż prostego uwierzytelniania i autoryzacji. Podaj hello [parametru zasady](active-directory-b2c-reference-policies.md), umożliwiający toouse OpenID Connect tooadd wrażenia użytkowników — takich jak konta, logowania i zarządzania profilami--tooyour aplikacji. W tym miejscu zostanie przedstawiony zostanie sposób tooimplement OpenID Connect i zasady toouse wykonywania każdego z nich w aplikacji sieci web. Również pokażemy ci jak jest tooget tokenów dostępu do uzyskiwania dostępu do interfejsów API sieci web.

Witaj przykład HTTP żądania w następnej sekcji hello przy użyciu katalogu B2C naszej próbki, fabrikamb2c.onmicrosoft.com, jak również naszych przykładowej aplikacji https://aadb2cplayground.azurewebsites.net i zasad. Można go dowolnie tootry limit hello żądań samodzielnie przy użyciu tych wartości, lub można je zastąpić własnymi.
Dowiedz się, jak za[uzyskać własne dzierżawy B2C, aplikacji i zasad](#use-your-own-b2c-directory).

## <a name="send-authentication-requests"></a>Wysyłanie żądania uwierzytelniania
W przypadku aplikacji sieci web musi tooauthenticate hello użytkowników i wykonywanie zasad, można kierować hello użytkownika toohello `/authorize` punktu końcowego. Jest hello interakcyjne część przepływu hello, gdzie hello użytkownik wykona akcję w zależności od zasad hello.

W tym żądaniu powitania klienta wskazuje uprawnienia hello, że wymaga ona tooacquire od użytkownika hello w hello `scope` parametr i hello tooexecute zasad w hello `p` parametru. Trzy przedstawione przykłady w hello następujące sekcje (podziałami wierszy dla czytelności), każdy przy użyciu różnych zasad. tooget działania dla działania każdego żądania, spróbuj wklejanie hello żądania do przeglądarki i jego uruchomieniem.

#### <a name="use-a-sign-in-policy"></a>Użyj zasad logowania
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

#### <a name="use-a-sign-up-policy"></a>Użyj zasad rejestracji
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

#### <a name="use-an-edit-profile-policy"></a>Użyj zasad edycji profilu
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parametr | Wymagana? | Opis |
| --- | --- | --- |
| client_id |Wymagane |Witaj aplikacji IDENTYFIKATORA tego hello [portalu Azure](https://portal.azure.com/) przypisane tooyour aplikacji. |
| response_type |Wymagane |Typ odpowiedzi Hello, który musi zawierać token Identyfikatora dla OpenID Connect. Jeśli aplikacja sieci web musi również tokenów do wywoływania interfejsu API sieci web, możesz użyć `code+id_token`, jak firma Microsoft zostało wykonane w tym miejscu. |
| redirect_uri |Zalecane |Witaj `redirect_uri` parametru aplikacji, w którym można wysłanych i odebranych przez aplikację odpowiedzi uwierzytelniania. Musi dokładnie odpowiadać jeden hello `redirect_uri` parametrów, które zarejestrowano w portalu hello z tą różnicą, że musi być zakodowane w adresie URL. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów. Wartość pojedynczy zakres wskazuje tooAzure AD zarówno uprawnienia, które są żądane. Witaj `openid` toosign uprawnienia, w danych użytkownika i get hello o hello użytkownika w postaci hello tokenów identyfikator (więcej toocome na tym w dalszej części artykułu hello) wskazuje zakres. Witaj `offline_access` zakres jest opcjonalne dla aplikacji sieci web. Wskazuje, że aplikacja, należy *token odświeżania* dla tooresources długotrwałe dostępu. |
| response_mode |Zalecane |Metoda Hello powinny być używane toosend hello wynikowy autoryzacji kodu wstecz tooyour aplikacji. Może być albo `query`, `form_post`, lub `fragment`.  Witaj `form_post` najlepiej zalecany jest tryb odpowiedzi. |
| state |Zalecane |Wartość zawarte w żądaniu hello, który jest także zwracany w odpowiedzi tokenu hello. Można go ciąg ma zawartość. Losowo generowany unikatową wartość jest zwykle używany zapobiegania fałszerstwie żądania międzywitrynowego. Stan Hello jest również używane tooencode informacji na temat stanu hello użytkownika w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takie jak strona hello, w której znajdowały się w. |
| Identyfikator jednorazowy |Wymagane |Wartość zawarte w żądaniu hello (wygenerowany przez aplikację hello), która zostanie uwzględniona w hello identyfikator tokenu jako oświadczenia. Aplikacja Hello następnie sprawdzić, czy ataki powtórzeń tokenów toomitigate wartość. wartość Hello jest zwykle losowego unikatowy ciąg, które mogą być używane tooidentify hello pochodzenia hello żądania. |
| P |Wymagane |zasady Hello, która zostanie wykonana. To nazwa hello zasady, która jest tworzona w dzierżawie usługi B2C. wartość Nazwa zasad Hello powinny rozpoczynać się od `b2c\_1\_`. Dowiedz się więcej o zasadach i hello [rozszerzona platforma zasad](active-directory-b2c-reference-policies.md). |
| wiersz |Optional (Opcjonalność) |Typ Hello interakcji z użytkownikiem, który jest wymagany. Witaj jedyną prawidłową wartością w tej chwili jest `login`, która wymusza hello tooenter użytkownika poświadczeń dla tego żądania. Logowanie jednokrotne nie zacznie obowiązywać. |

W tym momencie hello użytkownik jest proszony toocomplete hello zasad przepływu pracy. Może to obejmować użytkownika hello wprowadzić swoją nazwę użytkownika i hasło, zalogować się społecznościowych tożsamości, podczas tworzenia katalogu hello lub dowolną liczbę kroków w zależności od tego, jak zdefiniowano hello zasad.

Po zakończeniu zasad hello hello użytkownika usługi Azure AD zwraca aplikacji tooyour odpowiedzi w momencie hello wskazanych `redirect_uri` parametr przy użyciu metody hello, który określono w hello `response_mode` parametru. odpowiedź Hello jest hello sam dla każdej hello poprzedzających przypadków, niezależnie od zasady hello, która jest wykonywana.

Odpowiedź oznaczająca Powodzenie przy użyciu `response_mode=fragment` powinien wyglądać tak:

```
GET https://aadb2cplayground.azurewebsites.net/#
id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parametr | Opis |
| --- | --- |
| żądaniu |Witaj identyfikator token, aplikacja hello żądanie. Można użyć hello identyfikator tokenu tooverify hello tożsamości użytkownika i rozpocząć sesję użytkownika hello. Więcej informacji na temat identyfikator tokeny i ich zawartość są objęte hello [odwołania do tokenu usługi Azure AD B2C](active-directory-b2c-reference-tokens.md). |
| Kod |Witaj autoryzacji kodu, aplikacja hello wymagane, jeśli używasz `response_type=code+id_token`. Aplikacja Hello służy toorequest kod autoryzacji hello tokenu dostępu dla zasobu docelowego. Kody autoryzacji są bardzo krótkim okresie. Zazwyczaj wygasną po około 10 minut. |
| state |Jeśli `state` parametru jest częścią żądania hello hello tę samą wartość powinna być widoczna w odpowiedzi hello. Witaj aplikacji należy sprawdzić, że hello `state` wartości hello żądań i odpowiedzi są identyczne. |

Odpowiedzi na błędy mogą być również wysyłane toohello `redirect_uri` parametr tak, aplikacja hello można je odpowiednią obsługę:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kod błędu, które mogą być używane tooclassify typy błędów, które występować i które może być używane tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |
| state |Zobacz pełny opis hello w pierwszej tabeli hello w tej sekcji. Jeśli `state` parametru jest częścią żądania hello hello tę samą wartość powinna być widoczna w odpowiedzi hello. Witaj aplikacji należy sprawdzić, że hello `state` wartości hello żądań i odpowiedzi są identyczne. |

## <a name="validate-hello-id-token"></a>Sprawdź poprawność hello identyfikator tokenu
Tylko odbieranie token identyfikator nie jest wystarczająco dużo tooauthenticate hello użytkownikiem. Musisz zweryfikować podpisu tokenu identyfikator hello i sprawdzić hello oświadczenia w tokenie hello na wymagania dotyczące Twojej aplikacji. Używa usługi Azure AD B2C [tokenów sieci Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) i publicznego klucza szyfrowania tokenów toosign i sprawdź, czy są prawidłowe.

Istnieje wiele bibliotekach open source dostępnych sprawdzania poprawności tokenów Jwt, w zależności od języka preferencji. Firma Microsoft zaleca eksploracji te opcje, a nie implementacji logiki weryfikacji. tutaj informacje Hello będzie przydatna w ustaleniem, jak korzystać z tooproperly tych bibliotek.

Usługa Azure AD B2C ma OpenID Connect punktu końcowego metadanych, dzięki czemu aplikacja toofetch informacji o usłudze Azure AD B2C w czasie wykonywania. Informacje te obejmują punkty końcowe, zawartość tokenu i klucze podpisywania tokenu. Brak dokument metadanych JSON dla każdej zasady w dzierżawie usługi B2C. Na przykład dokument metadanych hello hello `b2c_1_sign_in` zasad w `fabrikamb2c.onmicrosoft.com` znajduje się pod adresem:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Jedna z właściwości hello tego dokumentu konfiguracji jest `jwks_uri`, którego wartość hello będą takie same zasady:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`.

toodetermine zasady, które zostało użyte w podpisywania tokenu identyfikator (i z których toofetch hello metadanych) są dostępne dwie opcje. Najpierw hello zasad nazwa jest uwzględniona w hello `acr` oświadczenia w tokenie identyfikator hello. Aby informacji na temat sposobu tooparse hello oświadczeń z tokenu identyfikator, zobacz hello [odwołania do tokenu usługi Azure AD B2C](active-directory-b2c-reference-tokens.md). Drugą opcją jest zasad hello tooencode hello wartości hello `state` parametru, gdy Żądanie hello, a następnie zdekodować toodetermine zasady, które zostało użyte. Każda metoda jest prawidłowa.

Po zostały nabyte hello dokument metadanych z punktu końcowego metadanych hello OpenID Connect, możesz użyć hello RSA 256 kluczy publicznych (które znajdują się w tym punkcie końcowym) toovalidate podpisu hello hello Identyfikatora tokenu. Może istnieć wiele kluczy wymienione w tym punkcie końcowym w dowolny punkt w czasie, identyfikowanych przez `kid` oświadczeń. Witaj nagłówek hello identyfikator tokenu zawiera także `kid` oświadczeń, co wskazuje, które z tych kluczy została toosign używane hello identyfikator tokenu. Aby uzyskać więcej informacji, zobacz hello [odwołania do tokenu usługi Azure AD B2C](active-directory-b2c-reference-tokens.md) (hello sekcji na [sprawdzanie poprawności tokenów](active-directory-b2c-reference-tokens.md#token-validation), w szczególności).
<!--TODO: Improve hello information on this-->

Po upewnieniu się hello podpisu tokenu identyfikator hello, istnieje kilka oświadczenia należy tooverify. Na wystąpienie:

* Należy sprawdzić, czy hello `nonce` tooprevent ataków powtórzeń tokenów oświadczeń. Jego wartość powinna być określona w hello żądania logowania.
* Należy sprawdzić, czy hello `aud` oświadczeń tooensure, który hello identyfikator token został wystawiony dla aplikacji. Jego wartość powinna być identyfikator aplikacji hello aplikacji.
* Należy sprawdzić, czy hello `iat` i `exp` oświadczeń tooensure, który hello identyfikator token nie wygasł.

Istnieje kilka więcej operacji sprawdzania poprawności, które należy wykonać. Te ustawienia zostały opisane szczegółowo w hello [OpenID Connect podstawowych specyfikacji](http://openid.net/specs/openid-connect-core-1_0.html).  Można także toovalidate dodatkowe roszczenia, w zależności od danego scenariusza. Niektóre typowe operacje sprawdzania poprawności obejmują:

* Zapewnienie, że który hello użytkownika/organizacji po zarejestrowaniu aplikacji hello.
* Zapewnienie hello użytkownika ma właściwe autoryzacji/uprawnienia.
* Zapewnienie, że niektóre siły uwierzytelniania wystąpił, takich jak uwierzytelnianie wieloskładnikowe Azure.

Aby uzyskać więcej informacji na powitania oświadczenia w tokenie identyfikator, zobacz hello [odwołania do tokenu usługi Azure AD B2C](active-directory-b2c-reference-tokens.md).

Po zweryfikowaniu hello identyfikator tokenu, można rozpocząć sesji hello użytkownika. Witaj oświadczeń w hello identyfikator tokenu tooobtain informacje o użytkowniku hello służy w aplikacji. Zastosowania te informacje obejmują ekranu, rekordów i autoryzacji.

## <a name="get-a-token"></a>Uzyskaj token
Jeśli potrzebujesz tooonly aplikacji sieci web wykonania zasady, można pominąć hello kolejnych sekcjach kilku. Sekcje te są stosowane tooweb tylko aplikacje, które muszą toomake uwierzytelnione wywołania tooa — interfejs API sieci web, a także są chronione przez usługę Azure AD B2C.

Możesz zrealizować kod autoryzacji hello uzyskanego (przy użyciu `response_type=code+id_token`) dla tokenu toohello żądanego zasobu, wysyłając `POST` żądania toohello `/token` punktu końcowego. Witaj tylko tych zasobów, jakiej może żądać tokenu dla jest obecnie własnych aplikacji zaplecza interfejsu API sieci web. Konwencja powitania dla żądania tokenu tooyourself jest toouse identyfikator klienta aplikacji jako zakres hello:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>

```

| Parametr | Wymagana? | Opis |
| --- | --- | --- |
| P |Wymagane |Witaj zasad, które były używane tooacquire hello autoryzacji kodu. Nie można użyć różnych zasad w tym żądaniu. Uwaga dodano ten ciąg zapytania toohello parametru, a nie toohello `POST` treści. |
| client_id |Wymagane |Witaj aplikacji IDENTYFIKATORA tego hello [portalu Azure](https://portal.azure.com/) przypisane tooyour aplikacji. |
| Typ grant_type |Wymagane |Witaj typu grant, który musi być `authorization_code` dla przepływu kodu autoryzacji hello. |
| Zakres |Zalecane |Rozdzieloną spacjami listę zakresów. Wartość pojedynczy zakres wskazuje tooAzure AD zarówno uprawnienia, które są żądane. Witaj `openid` zakresu wskazuje toosign uprawnienia, w danych użytkownika i get hello o hello użytkownika w postaci hello parametrów w żądaniu. Może być używane tooget tokenów tooyour własnych aplikacji zaplecza interfejsu API sieci web, która jest reprezentowana przez hello tego samego Identyfikatora aplikacji jako powitania klienta. Witaj `offline_access` zakresu wskazuje, że aplikacja będzie potrzebny token odświeżania tooresources długotrwałe dostępu. |
| Kod |Wymagane |Kod autoryzacji Hello uzyskanego w hello pierwszego etap hello przepływu. |
| redirect_uri |Wymagane |Witaj `redirect_uri` parametru aplikacji hello którym odebrano hello kod autoryzacji. |
| client_secret |Wymagane |klucz tajny aplikacji Hello generowany w hello [portalu Azure](https://portal.azure.com/). Ten klucz tajny aplikacji jest ważny artefaktu. Użytkownik powinien Zapisz w bezpiecznej lokalizacji na serwerze. Należy również Obróć ten klucz tajny klienta w regularnych odstępach czasu. |

Odpowiedź oznaczająca Powodzenie tokenu wygląda następująco:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parametr | Opis |
| --- | --- |
| not_before |czas Hello, w których hello token jest uznawany za ważny w czasie epoki. |
| token_type |wartość tokenu typu Hello. Witaj tylko typ, który obsługuje usługę Azure AD `Bearer`. |
| ' access_token ' |Witaj podpisany token JWT, którego zażądano. |
| Zakres |zakresy Hello, dla których hello token jest prawidłowy. Mogą być one używane do buforowania tokeny na potrzeby późniejszego użycia. |
| expires_in |Hello długość czasu, przez który hello token dostępu jest nieprawidłowy (w sekundach). |
| refresh_token |Token odświeżania OAuth 2.0. Aplikacja Hello można użyć tego tokenu tooacquire dodatkowe tokeny, po wygaśnięciu tokenu bieżącego hello. Odśwież tokeny są to długotrwałe i mogą być używane tooretain tooresources dostępu przez dłuższy czas. Aby uzyskać więcej informacji, zobacz toohello [odwołania do tokenu usługi B2C](active-directory-b2c-reference-tokens.md). Uwaga musi użycie zakresu hello `offline_access` w hello autoryzacji i tokena żądań w kolejności tooreceive token odświeżania. |

Błąd odpowiedzi następującą postać:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kod błędu, które mogą być używane tooclassify typy błędów, które występować i które może być używane tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |

## <a name="use-hello-token"></a>Użyj tokenu hello
Teraz, zostały pomyślnie uzyskano tokenu dostępu, można hello token w żądań tooyour zaplecza interfejsów API sieci web przez dołączenie go do hello `Authorization` nagłówka:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="refresh-hello-token"></a>Odśwież hello tokenu
Identyfikator tokeny są krótkim okresie. Należy odświeżyć je po wygasną toocontinue jest w stanie tooaccess zasobów. Możesz to zrobić poprzez przesłanie innego `POST` żądania toohello `/token` punktu końcowego. Teraz, podaj hello `refresh_token` parametru zamiast hello `code` parametru:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=openid offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>
```

| Parametr | Wymagane | Opis |
| --- | --- | --- |
| P |Wymagane |Hello zasady, które zostało tooacquire używane hello oryginalnego token odświeżania. Nie można użyć różnych zasad w tym żądaniu. Należy pamiętać, dodano ten ciąg zapytania toohello parametru, a nie toohello treść wpisu. |
| client_id |Wymagane |Witaj aplikacji IDENTYFIKATORA tego hello [portalu Azure](https://portal.azure.com/) przypisane tooyour aplikacji. |
| Typ grant_type |Wymagane |Typ Hello grant, który musi być token odświeżania dla tego etap przepływu kodu autoryzacji hello. |
| Zakres |Zalecane |Rozdzieloną spacjami listę zakresów. Wartość pojedynczy zakres wskazuje tooAzure AD zarówno uprawnienia, które są żądane. Witaj `openid` toosign uprawnienia, w danych użytkownika i get hello o hello użytkownika w postaci hello tokenów identyfikator wskazuje zakres. Może być używane tooget tokenów tooyour własnych aplikacji zaplecza interfejsu API sieci web, która jest reprezentowana przez hello tego samego Identyfikatora aplikacji jako powitania klienta. Witaj `offline_access` zakresu wskazuje, że aplikacja będzie potrzebny token odświeżania tooresources długotrwałe dostępu. |
| redirect_uri |Zalecane |Witaj `redirect_uri` parametru aplikacji hello którym odebrano hello kod autoryzacji. |
| refresh_token |Wymagane |Witaj oryginalnego token odświeżania uzyskanego w drugi etap hello hello przepływu. Uwaga musi użycie zakresu hello `offline_access` w hello autoryzacji i tokena żądań w kolejności tooreceive token odświeżania. |
| client_secret |Wymagane |klucz tajny aplikacji Hello generowany w hello [portalu Azure](https://portal.azure.com/). Ten klucz tajny aplikacji jest ważny artefaktu. Użytkownik powinien Zapisz w bezpiecznej lokalizacji na serwerze. Należy również Obróć ten klucz tajny klienta w regularnych odstępach czasu. |

Odpowiedź oznaczająca Powodzenie tokenu wygląda następująco:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Parametr | Opis |
| --- | --- |
| not_before |czas Hello, w których hello token jest uznawany za ważny w czasie epoki. |
| token_type |wartość tokenu typu Hello. Witaj tylko typ, który obsługuje usługę Azure AD `Bearer`. |
| ' access_token ' |Witaj podpisany token JWT, którego zażądano. |
| Zakres |zakres Hello hello token jest prawidłowy, które mogą służyć do buforowania tokeny na potrzeby późniejszego użycia. |
| expires_in |Hello długość czasu, przez który hello token dostępu jest nieprawidłowy (w sekundach). |
| refresh_token |Token odświeżania OAuth 2.0. Aplikacja Hello można użyć tego tokenu tooacquire dodatkowe tokeny, po wygaśnięciu tokenu bieżącego hello.  Odśwież tokeny są to długotrwałe i mogą być używane tooretain tooresources dostępu przez dłuższy czas. Aby uzyskać więcej szczegółów można znaleźć toohello [odwołania do tokenu usługi B2C](active-directory-b2c-reference-tokens.md). |

Błąd odpowiedzi następującą postać:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kod błędu, które mogą być używane tooclassify typy błędów, które występować i które może być używane tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |

## <a name="send-a-sign-out-request"></a>Wyślij żądanie wylogowania
Użytkownika hello toosign poza aplikacją hello, należy jest za mało tooclear plików cookie aplikacji lub inny sposób zakończenia sesji hello hello użytkownika. Należy również przekierować hello użytkownika tooAzure AD toosign wychodzących. Jeśli tak nie toodo, hello użytkownika może być stanie tooreauthenticate tooyour aplikacji bez konieczności ponownego wprowadzania poświadczeń. Jest tak, ponieważ mają one nieprawidłowy jednej logowania jednokrotnego sesji z usługą Azure AD.

Można przekierowywać po prostu toohello użytkownika hello `end_session` punktu końcowego, który znajduje się w dokumencie metadanych OpenID Connect hello opisem we wcześniejszej części hello sekcji "Sprawdzanie poprawności hello identyfikator tokenu":

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Parametr | Wymagana? | Opis |
| --- | --- | --- |
| P |Wymagane |zasady Hello mają toouse toosign hello użytkownika z aplikacji. |
| post_logout_redirect_uri |Zalecane |Witaj adres URL tego użytkownika hello powinien być przekierowanego tooafter pomyślnie wylogowania. Jeśli nie zostanie włączony, usługi Azure AD B2C pokazuje hello użytkownika zostanie wyświetlony komunikat ogólny. |

> [!NOTE]
> Mimo że kierowanie hello użytkownika toohello `end_session` punktu końcowego spowoduje wyczyszczenie niektóre użytkownika hello pojedynczego logowania jednokrotnego stanu z usługi Azure AD B2C, nie podpisze użytkownika hello poza swoją sesję dostawca tożsamości społecznościowych. Po wybraniu opcji użytkownika hello hello tego samego IDP podczas kolejnych logowanie, one będzie można ponownie uwierzytelnić, bez konieczności wprowadzania poświadczeń. Jeśli użytkownik chce toosign poza aplikacji B2C, go nie musi oznaczać że toosign poza swojego konta w serwisie Facebook. Jednak w przypadku hello kont lokalnych, hello sesja zostanie zakończona poprawnie.
> 
> 

## <a name="use-your-own-b2c-tenant"></a>Użyj dzierżawy usługi B2C
Jeśli chcesz tootry te żądania dla siebie, należy najpierw wykonać następujące trzy kroki, a następnie zastąp hello przykładowe wartości opisanych wcześniej własnymi:

1. [Tworzenie dzierżawy B2C](active-directory-b2c-get-started.md)i użyj hello nazwy dzierżawy w żądaniach hello.
2. [Tworzenie aplikacji](active-directory-b2c-app-registration.md) tooobtain identyfikator aplikacji. Dołącz aplikacji sieci web aplikacji/składnika web API. Opcjonalnie: Utwórz klucz tajny aplikacji.
3. [Tworzenie zasad](active-directory-b2c-reference-policies.md) tooobtain nazwy zasad.

