---
title: "Witaj aaaUnderstand OpenID Connect przepływu kodu uwierzytelniania w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooauthorize wiadomości toouse HTTP dostępu tooweb aplikacji i interfejsów API sieci web w dzierżawie przy użyciu usługi Azure Active Directory i OpenID Connect."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 29142f7e-d862-4076-9a1a-ecae5bcd9d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: fafd8ab906ee576c584fec2ef1e9de83ddb1f6e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Zezwolić aplikacji tooweb dostępu przy użyciu protokołu OpenID Connect i Azure Active Directory
[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) jest oparty na protokół OAuth 2.0 hello warstwy tożsamości proste. Definiuje OAuth 2.0 tooobtain mechanizmów i użyj **tokenów dostępu** tooaccess chronione zasoby, ale nie określają informacje o tożsamości tooprovide standardowych metod. OpenID Connect implementuje uwierzytelnianie jako rozszerzenie toohello procesu autoryzacji OAuth 2.0. Zawiera informacje na temat hello użytkownika końcowego w formie hello `id_token` która weryfikuje hello tożsamości użytkownika hello i profilu podstawowe informacje na temat hello użytkownika.

OpenID Connect Oto Nasze zalecenia, jeśli tworzysz aplikację sieci web jest hostowany na serwerze i dostępne za pośrednictwem przeglądarki.


[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)] 

## Przepływ uwierzytelniania przy użyciu protokołu OpenID Connect
Witaj najprostsze logowania przepływ zawiera następujące kroki hello — każdego z nich jest szczegółowo opisana poniżej.

![OpenId Connect przepływ uwierzytelniania](media/active-directory-protocols-openid-connect-code/active-directory-oauth-code-flow-web-app.png)

## Dokument metadanych OpenID Connect

OpenID Connect zawiera opis dokument metadanych zawiera większość informacji hello wymagane dla aplikacji tooperform logowania. Dotyczy to również informacje, takie jak hello toouse adresy URL i lokalizację hello hello usługi publiczne klucze podpisywania. Dokument metadanych OpenID Connect Hello można znaleźć w folderze:

```
https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration
```
metadane Hello jest proste dokumentu JavaScript Object Notation (JSON). Zobacz powitania po fragment, na przykład. Witaj zawartość fragment kodu w pełni opisanym w hello [OpenID Connect specyfikacji](https://openid.net).

```
{
    "authorization_endpoint": "https://login.microsoftonline.com/common/oauth2/authorize",
    "token_endpoint": "https://login.microsoftonline.com/common/oauth2/token",
    "token_endpoint_auth_methods_supported":
    [
        "client_secret_post",
        "private_key_jwt"
    ],
    "jwks_uri": "https://login.microsoftonline.com/common/discovery/keys"
    
    ...
}
```

## Wysyłanie żądania logowania hello
Gdy aplikacja sieci web musi tooauthenticate hello użytkownika, musi bezpośrednie hello użytkownika toohello `/authorize` punktu końcowego. To żądanie jest podobne pierwszego etap toohello hello [przepływu kodu autoryzacji OAuth 2.0](active-directory-protocols-oauth-code.md), z kilku ważnych różnice:

* Witaj żądanie musi zawierać zakres hello `openid` w hello `scope` parametru.
* Witaj `response_type` musi zawierać parametr `id_token`.
* Witaj żądanie musi zawierać hello `nonce` parametru.

Dlatego przykładowe żądanie będzie wyglądać następująco:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=7362CAEA-9CA5-4B43-9BA3-34D7C303EBA7
```

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Witaj `{tenant}` wartość w ścieżce hello hello żądania mogą być używane toocontrol, który można zalogować się do aplikacji hello.  Witaj dozwolone wartości to identyfikatory dzierżawy, na przykład `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` lub `contoso.onmicrosoft.com` lub `common` tokenów niezależny od dzierżawcy |
| client_id |Wymagane |Program Hello identyfikator aplikacji przypisany tooyour aplikacji został zarejestrowany z usługą Azure AD. To można znaleźć w portalu Azure hello. Kliknij przycisk **usługi Azure Active Directory**, kliknij przycisk **rejestracji aplikacji**, wybierz aplikację hello i zlokalizuj identyfikator aplikacji hello, na stronie aplikacji hello. |
| response_type |Wymagane |Musi zawierać `id_token` OpenID Connect logowaniu.  Może również obejmować innych response_types, takich jak `code`. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów.  Dla protokołu OpenID Connect, musi on zawierać zakres hello `openid`, co przekłada się uprawnienie "Logowanie się w" toohello w zgody hello interfejsu użytkownika.  Można również użyć innych zakresów w tym żądaniu żądanych zgody. |
| Identyfikator jednorazowy |Wymagane |Wartość zawarte w żądaniu hello, generowane przez hello app, do której jest uwzględniona w co hello `id_token` jako oświadczenia.  Aplikacja Hello następnie sprawdzić, czy ataki powtórzeń tokenów toomitigate wartość.  wartość Hello jest zwykle losowy unikatowy ciąg lub identyfikator GUID, które mogą być używane tooidentify hello pochodzenia hello żądania. |
| redirect_uri |Zalecane |Witaj redirect_uri aplikacji, w którym można wysłanych i odebranych przez aplikację odpowiedzi uwierzytelniania.  Dokładnie musi odpowiadać jedną redirect_uris hello, który został zarejestrowany w portalu hello, z wyjątkiem musi być zakodowane w adresie url. |
| response_mode |Zalecane |Określa metodę hello, który ma być używane toosend hello wynikowy authorization_code wstecz tooyour aplikacji.  Obsługiwane wartości to `form_post` dla *HTTP post formularza* lub `fragment` dla *fragmentu adresu URL*.  Dla aplikacji sieci web, zaleca się używanie `response_mode=form_post` tooensure hello najbardziej bezpieczny transfer tokenów tooyour aplikacji. |
| state |Zalecane |Wartość zawarte w żądaniu hello, który jest zwracany w odpowiedzi tokenu hello.  Można go ciągiem zawartość, która ma.  Losowo generowany unikatową wartość jest zazwyczaj używana w przypadku [zapobieganie fałszerstwie żądania międzywitrynowego](http://tools.ietf.org/html/rfc6749#section-10.12).  Stan Hello jest również używane tooencode informacji na temat stanu hello użytkownika w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takie jak strona hello lub widok, które były na. |
| wiersz |Opcjonalne |Wskazuje typ hello interakcji z użytkownikiem, który jest wymagany.  Obecnie hello tylko prawidłowe wartości to "login", "none", "wyrazić zgodę".  `prompt=login`Wymusza hello użytkownika tooenter swoje poświadczenia w tym żądaniu Negacja jednokrotnego.  `prompt=none`Witaj przeciwną — gwarantuje, że użytkownik hello nie zobaczy żadnych interakcyjnego prompt jakiejkolwiek.  Jeśli nie można ukończyć żądania hello dyskretnie za pośrednictwem jednokrotnego, punkt końcowy hello zwraca błąd.  `prompt=consent`wyzwala hello OAuth zgody okna dialogowego po hello użytkownik loguje, prosząc hello użytkownika toogrant uprawnienia toohello aplikacji. |
| login_hint |Opcjonalne |Może być pole adresu e-mail/nazwa użytkownika hello używane wypełnienia toopre hello strony logowania dla użytkownika hello, jeśli znasz swoją nazwę użytkownika wcześniejsze.  Aplikacje często tego parametru należy użyć podczas ponownego uwierzytelniania, już o wyodrębnić hello username z poprzednich logowanie przy użyciu hello `preferred_username` oświadczeń. |

W tym momencie użytkownik hello jest zadawane tooenter ich poświadczeń i uwierzytelniania hello ukończone.

### Przykładowa odpowiedź
Przykładowa odpowiedź, po uwierzytelnieniu użytkownika hello, może wyglądać następująco:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Parametr | Opis |
| --- | --- |
| żądaniu |Witaj `id_token` , aplikacja hello żądanie. Można użyć hello `id_token` tooverify hello tożsamości użytkownika i rozpocząć sesję przy użyciu hello użytkownika. |
| state |Wartość zawarte w żądaniu hello, który jest także zwracany w odpowiedzi tokenu hello. Losowo generowany unikatową wartość jest zazwyczaj używana w przypadku [zapobieganie fałszerstwie żądania międzywitrynowego](http://tools.ietf.org/html/rfc6749#section-10.12).  Stan Hello jest również używane tooencode informacji na temat stanu hello użytkownika w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takie jak strona hello lub widok, które były na. |

### Odpowiedzi na błąd
Odpowiedzi na błędy mogą być również wysyłane toohello `redirect_uri` dzięki aplikacji hello można je odpowiednią obsługę:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu mogą być używane tooclassify typów błędów występujących, która może być używana tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |

#### Kody błędów dla błędów punktu końcowego autoryzacji
Witaj poniższej tabeli opisano hello różnych kody błędów, które mogą być zwracane w hello `error` parametru hello odpowiedzi na błąd.

| Kod błędu: | Opis | Akcja klienta |
| --- | --- | --- |
| invalid_request |Błąd protokołu, takie jak brak wymaganego parametru. |Usuń i ponownie prześlij żądanie hello. Jest to błąd programowanie i zwykle zostanie przechwycony podczas testowania początkowej. |
| unauthorized_client |Witaj aplikację klienta nie jest dozwolone toorequest kod autoryzacji. |Zazwyczaj dzieje się tak, gdy aplikacja kliencka hello nie jest zarejestrowany w usłudze Azure AD lub dzierżawy usługi Azure AD toohello użytkownika nie została dodana. aplikacji Hello można monitować użytkownika hello z instrukcji dotyczących instalowania aplikacji hello i dodanie go tooAzure AD. |
| ACCESS_DENIED |Odmowa zgody właściciel zasobu |Aplikacja kliencka Hello powiadamiać hello użytkownika, którego nie można kontynuować, chyba że użytkownik hello zgadza. |
| unsupported_response_type |w żądaniu hello powitania serwera autoryzacji nie obsługuje hello typ odpowiedzi. |Usuń i ponownie prześlij żądanie hello. Jest to błąd programowanie i zwykle zostanie przechwycony podczas testowania początkowej. |
| server_error |Witaj serwer napotkał nieoczekiwany błąd. |Ponów żądanie hello. Te błędy może wynikać z tymczasowego warunków. Aplikacja kliencka Hello może wyjaśnić toohello użytkownika czy ze względu na tymczasowy błąd tooa jest opóźnione odpowiedzi. |
| temporarily_unavailable |Serwer Hello tymczasowo jest zbyt zajęty toohandle hello żądania. |Ponów żądanie hello. Aplikacja kliencka Hello może wyjaśnić toohello użytkownika czy ze względu na tymczasowy warunek tooa jest opóźnione odpowiedzi. |
| invalid_resource |zasób docelowy Hello jest nieprawidłowy, ponieważ nie istnieje, nie można znaleźć usługi Azure AD lub nie została poprawnie skonfigurowana. |Oznacza to, że hello zasobu, jeśli istnieje, nie został skonfigurowany w dzierżawie powitalnych. aplikacji Hello można monitować użytkownika hello z instrukcji dotyczących instalowania aplikacji hello i dodanie go tooAzure AD. |

## Sprawdź poprawność żądaniu hello
Tylko odbieranie `id_token` nie jest wystarczające użytkownika hello tooauthenticate; musi sprawdzić poprawności podpisu hello i sprawdź hello oświadczeń w hello `id_token` na wymagania dotyczące Twojej aplikacji. punkt końcowy usługi Azure AD Hello korzysta z tokenów sieci Web JSON (Jwt) i tokenów toosign kluczem publicznym i sprawdź, czy są prawidłowe.

Możesz wybrać toovalidate hello `id_token` w kodzie klienta, ale toosend hello jest typowym rozwiązaniem `id_token` tooa serwera wewnętrznej bazy danych i sprawdzania poprawności hello istnieje. Po upewnieniu się hello podpis hello `id_token`, istnieje kilka oświadczenia są wymagane tooverify.

Możesz również toovalidate dodatkowe oświadczeń w zależności od danego scenariusza. Niektóre typowe operacje sprawdzania poprawności obejmują:

* Zapewnienie organizacja użytkownika powitania po zarejestrowaniu aplikacji hello.
* Zapewnienie hello użytkownika ma właściwe autoryzacji/uprawnienia
* Zapewnienie siły uwierzytelniania wystąpił, takich jak uwierzytelnianie wieloskładnikowe.

Po zweryfikowaniu hello `id_token`, można rozpocząć sesji z hello użytkownika i używać hello oświadczeń w hello `id_token` tooobtain informacji na temat hello użytkownika w aplikacji. Te informacje można służyć do wyświetlania rekordów, autoryzacje itp. Aby uzyskać więcej informacji na temat hello typy tokenów i oświadczeń, przeczytaj [obsługiwany Token i typy oświadczeń](active-directory-token-and-claims.md).

## Wyślij żądanie wylogowania
Wtedy, gdy użytkownik hello toosign poza aplikacją hello, jest niewystarczająca tooclear plików cookie aplikacji lub inny sposób zakończenia sesji hello hello użytkownika.  Należy również przekierować hello użytkownika toohello `end_session_endpoint` do wylogowania.  Jeśli nie zostanie toodo tak, użytkownik hello będzie stanie tooreauthenticate tooyour aplikacji bez ponownego wprowadzania poświadczeń, ponieważ mają one nieprawidłowy jednej logowania jednokrotnego sesji z punktem końcowym usługi Azure AD hello.

Można przekierowywać po prostu toohello użytkownika hello `end_session_endpoint` dokument metadanych OpenID Connect hello na liście:

```
GET https://login.microsoftonline.com/common/oauth2/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F

```

| Parametr |  | Opis |
| --- | --- | --- |
| post_logout_redirect_uri |Zalecane |adres URL Hello hello użytkownika powinna być przekierowane tooafter wylogowania się pomyślnie.  Jeśli nie zostanie uwzględniony, użytkownik hello jest wyświetlany komunikat ogólny. |

## Wylogowanie jednokrotne
Podczas przekierowywania hello użytkownika toohello `end_session_endpoint`, sesji użytkownika hello z przeglądarki hello czyści usługi Azure AD. Jednak hello użytkownik może nadal musi być zarejestrowany w aplikacjach tooother, które używają usługi Azure AD do uwierzytelniania. tooenable toosign tych aplikacji hello użytkownika jednocześnie, usługi Azure AD wysyła HTTP GET żądania toohello zarejestrowany `LogoutUrl` wszystkich aplikacji hello hello użytkownik jest aktualnie zalogowany. Aplikacje musi odpowiadać toothis żądania przez wyczyszczenie wszelkich sesji, która identyfikuje użytkownika hello i zwracanie `200` odpowiedzi.  Jeśli chcesz toosupport funkcji logowania jednokrotnego, limit w aplikacji, musisz zaimplementować takie `LogoutUrl` w kodzie aplikacji.  Można ustawić hello `LogoutUrl` z hello portalu Azure:

1. Przejdź toohello [Azure Portal](https://portal.azure.com).
2. Wybierz usługi Active Directory, klikając na Twoim koncie w hello prawym górnym rogu strony hello.
3. W panelu nawigacyjnym po lewej stronie powitania wybrać **usługi Azure Active Directory**, a następnie wybierz **rejestracji aplikacji** i wybierz aplikację.
4. Polecenie **właściwości** i Znajdź hello **adresu URL wylogowania** pola tekstowego. 

## Token nabycia
Wiele aplikacji sieci web musi toonot tylko znak hello użytkownika w, ale także uzyskać dostęp do usługi sieci web w imieniu użytkownika, że w trybie OAuth. W tym scenariuszu łączy OpenID Connect do uwierzytelniania użytkowników podczas pobierania jednocześnie `authorization_code` które może być używane tooget `access_tokens` przy użyciu hello przepływu kodu autoryzacji OAuth.

## Pobieranie tokenów dostępu
tooacquire tokenów dostępu, należy żądania logowania hello toomodify z powyżej:

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application Id
&response_type=id_token+code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered Redirect Uri, url encoded
&response_mode=form_post                              // form_post', or 'fragment'
&scope=openid
&resource=https%3A%2F%2Fservice.contoso.com%2F                                     
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

W tym zakresy uprawnień w żądaniu hello i używając `response_type=code+id_token`, hello `authorize` punktu końcowego zapewnia hello użytkownik zgodził uprawnienia toohello wskazane hello `scope` parametr zapytania i zwracają kod autoryzacji aplikacji tooexchange dla tokenu dostępu.

### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie przy użyciu `response_mode=form_post` wygląda jak:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Parametr | Opis |
| --- | --- |
| żądaniu |Witaj `id_token` , aplikacja hello żądanie. Można użyć hello `id_token` tooverify hello tożsamości użytkownika i rozpocząć sesję przy użyciu hello użytkownika. |
| Kod |Witaj authorization_code, który hello żądanej aplikacji. zasób docelowy hello aplikacji Hello można używać toorequest kod autoryzacji hello tokenu dostępu. Authorization_codes są krótkie żyła i zwykle wygaśnie po około 10 minut. |
| state |Jeśli parametr Stan jest uwzględniony w żądaniu hello, hello tej samej wartości powinny być wyświetlane w hello odpowiedzi. Aplikacja Hello sprawdzić, czy wartości stanu hello hello żądań i odpowiedzi są identyczne. |

### Odpowiedzi na błąd
Odpowiedzi na błędy mogą być również wysyłane toohello `redirect_uri` dzięki aplikacji hello można je odpowiednią obsługę:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu mogą być używane tooclassify typów błędów występujących, która może być używana tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |

Opis hello możliwych kodów błędów i ich Akcja zalecana klienta, zobacz [kody błędów dla błędów punktu końcowego autoryzacji](#error-codes-for-authorization-endpoint-errors).

Po ich zaakceptujesz autoryzacji `code` i `id_token`, można zalogować użytkownika hello i uzyskać tokeny dostępu w ich imieniu.  Użytkownik hello toosign w, musisz zweryfikować hello `id_token` dokładnie tak jak opisano powyżej. tooget tokenów dostępu, możesz wykonać hello opisane w sekcji "Użyj toorequest kod autoryzacji hello token dostępu" hello z naszych [dokumentacji protokołu OAuth](active-directory-protocols-oauth-code.md).
