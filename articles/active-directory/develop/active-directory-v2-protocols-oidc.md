---
title: "aaaAzure usługi Active Directory w wersji 2.0 i hello protokołu OpenID Connect | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji sieci web przy użyciu hello Azure AD w wersji 2.0 implementacji protokołu uwierzytelniania OpenID Connect hello."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a4875997-3aac-4e4c-b7fe-2b4b829151ce
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 277bb406dbb24ccefb09e4e4c928f0421755cf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory w wersji 2.0 i hello protokołu OpenID Connect
OpenID Connect to protokół uwierzytelniania, oparty na OAuth 2.0, w której można toosecurely logowania w aplikacji sieci web tooa użytkownika. Użycie końcowego v2.0 hello wdrażania protokołu OpenID Connect, możesz dodać logowania i interfejsu API dostępu tooyour aplikacji sieci web. W tym artykule zostanie przedstawiony zostanie sposób toodo tym niezależny od języka. Opisano sposób toosend i odbieranie wiadomości HTTP bez korzystania z żadnych bibliotek open source firmy Microsoft.

> [!NOTE]
> punktu końcowego v2.0 Hello nie obsługuje wszystkich scenariuszy Azure Active Directory i funkcji. toodetermine, czy należy używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) rozszerza hello OAuth 2.0 *autoryzacji* toouse protokołu jako *uwierzytelniania* protokołu, dzięki czemu można wykonywać z jednego logowania w trybie OAuth. OpenID Connect wprowadzono pojęcie hello *token Identyfikatora*, który jest tokenu zabezpieczającego, która umożliwia klientowi hello tooverify hello tożsamości użytkownika hello. token Identyfikatora Hello pobiera również profilu podstawowe informacje o użytkowniku hello. Ponieważ OpenID Connect rozszerza protokół OAuth 2.0, aplikacje mogą bezpiecznie uzyskiwać *tokenów dostępu*, które mogą być używane tooaccess zasoby, które są zabezpieczone przez [serwera autoryzacji](active-directory-v2-protocols.md#the-basics). Zaleca się, że używasz OpenID Connect, jeśli tworzysz [aplikacji sieci web](active-directory-v2-flows.md#web-apps) który jest hostowany na serwerze i dostępne za pośrednictwem przeglądarki.

## Diagram protokołu: logowania
Witaj najprostsze przepływu logowania ma hello kroki opisane w diagramie dalej hello. Opisano każdy krok szczegółowo w tym artykule.

![Protokołu OpenID Connect: logowania](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

## Pobierz hello OpenID Connect dokument metadanych
OpenID Connect zawiera opis dokument metadanych zawiera większość informacji hello wymagane dla aplikacji tooperform logowania. Dotyczy to również informacje, takie jak hello toouse adresy URL i lokalizację hello hello usługi publiczne klucze podpisywania. Dla punktu końcowego v2.0 hello to hello OpenID Connect metadanych dokument, który należy używać:

```
https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration
```

Witaj `{tenant}` można wykonać jedną z czterech wartości:

| Wartość | Opis |
| --- | --- |
| `common` |Użytkownicy z osobistego konta Microsoft i konto służbowe z usługi Azure Active Directory (Azure AD) można się zalogować w toohello aplikacji. |
| `organizations` |Tylko użytkownicy z pracy lub kont służbowych z usługi Azure AD można zarejestrować się w aplikacji toohello. |
| `consumers` |Tylko użytkownicy z osobistego konta Microsoft zalogować toohello aplikacji. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` lub `contoso.onmicrosoft.com` |Tylko użytkownicy przy użyciu konta służbowego z określonej usługi Azure AD dzierżawy może zalogować toohello aplikacji. Nazwa domeny przyjazną hello hello dzierżawy usługi Azure AD, albo identyfikator GUID dzierżawy hello może służyć. |

metadane Hello jest proste dokumentu JavaScript Object Notation (JSON). Zobacz powitania po fragment, na przykład. Witaj zawartość fragment kodu w pełni opisanym w hello [OpenID Connect specyfikacji](https://openid.net).

```
{
  "authorization_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/authorize",
  "token_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_post",
    "private_key_jwt"
  ],
  "jwks_uri": "https:\/\/login.microsoftonline.com\/common\/discovery\/v2.0\/keys",

  ...

}
```

Zazwyczaj będzie używać tego tooconfigure dokumentu metadanych biblioteki OpenID Connect lub zestawu SDK; Biblioteka Hello użyje toodo metadanych hello swojej pracy. Jednak jeśli nie używasz biblioteki OpenID Connect wstępnej kompilacji, można wykonać kroki hello w pozostałych hello tego artykułu tooperform logowania w aplikacji sieci web przy użyciu punktu końcowego v2.0 hello.

## Wysyłanie żądania logowania hello
Gdy aplikacja sieci web musi tooauthenticate hello użytkownika, można kierować hello użytkownika toohello `/authorize` punktu końcowego. To żądanie jest podobne pierwszego etap toohello hello [przepływu kodu autoryzacji protokołu OAuth 2.0](active-directory-v2-protocols-oauth-code.md), z tych istotne różnice:

* Witaj żądanie musi zawierać hello `openid` zakres hello `scope` parametru.
* Witaj `response_type` musi zawierać parametr `id_token`.
* Witaj żądanie musi zawierać hello `nonce` parametru.

Na przykład:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=678910
```

> [!TIP]
> Kliknij następujące łącze tooexecute hello tego żądania. Po zalogowaniu w przeglądarce będzie przekierowanego toohttps://localhost/myapp/, z tokenem identyfikator na pasku adresu hello. Należy pamiętać, że używa tego żądania `response_mode=query` (tylko w celach demonstracyjnych). Firma Microsoft zaleca użycie `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid&response_mode=query&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

| Parametr | Warunek | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Można użyć hello `{tenant}` wartość hello ścieżka hello toocontrol żądania, który mógł zalogować się w aplikacji toohello. Witaj dozwolone wartości to `common`, `organizations`, `consumers`i dzierżawców identyfikatorów. Aby uzyskać więcej informacji, zobacz [protokołu podstawy](active-directory-v2-protocols.md#endpoints). |
| client_id |Wymagane |hello tego IDENTYFIKATORA aplikacji Hello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) przypisane tooyour aplikacji. |
| response_type |Wymagane |Musi zawierać `id_token` OpenID Connect logowaniu. Może również zawierać inne `response_types` wartości, takich jak `code`. |
| redirect_uri |Zalecane |Identyfikator URI aplikacji, gdzie można wysyłanych i odbieranych przez aplikację uwierzytelniania odpowiedzi przekierowania Hello. Dokładnie musi odpowiadać jeden hello przekierowania URI został zarejestrowany w portalu hello z tą różnicą, że adres URL musi być zakodowany. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów. Dla protokołu OpenID Connect, musi on zawierać zakres hello `openid`, co przekłada się uprawnienie "Logowanie się w" toohello w zgody hello interfejsu użytkownika. Mogą również obejmować innych zakresach, w tym żądaniu żądanych zgody. |
| Identyfikator jednorazowy |Wymagane |Wartość zawarte w żądaniu hello, generowane przez hello aplikacji, która zostanie uwzględniona w wynikowej wartości żądaniu hello jako oświadczenia. Aplikacja Hello sprawdzić, czy ataki powtórzeń tokenów toomitigate wartość. wartość Hello jest zwykle losowego, unikatowy ciąg, który może być używane tooidentify hello pochodzenia hello żądania. |
| response_mode |Zalecane |Określa metodę hello, który ma być używane toosend hello wynikowy autoryzacji kodu wstecz tooyour aplikacji. Może być jednym z `query`, `form_post`, lub `fragment`. Dla aplikacji sieci web, zaleca się używanie `response_mode=form_post`, tooensure hello najbardziej bezpieczny transfer tokenów tooyour aplikacji. |
| state |Zalecane |Wartość zawarte w żądaniu hello, które również zostaną zwrócone w odpowiedzi tokenu hello. Można go ciągiem żadnej zawartości, który ma. Losowo generowany unikatowy używana jest wartość zwykle zbyt[zapobiec fałszerstwie żądania międzywitrynowego](http://tools.ietf.org/html/rfc6749#section-10.12). Stan Hello również jest używane tooencode informacji na temat stanu hello użytkownika w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takich jak użytkownika hello hello stronę lub widok został na. |
| wiersz |Optional (Opcjonalność) |Wskazuje typ hello interakcji z użytkownikiem, który jest wymagany. Witaj prawidłowe są tylko wartości w tej chwili `login`, `none`, i `consent`. Witaj `prompt=login` oświadczeń wymusza hello tooenter użytkownika poświadczeń na żądanie i Negacja rejestracji jednokrotnej. Witaj `prompt=none` oświadczenia jest przeciwny hello. To oświadczenie gwarantuje, że użytkownik hello nie zobaczy jakiejkolwiek monitu interakcyjnego. Jeśli nie można ukończyć żądania hello dyskretnie za pośrednictwem rejestracji jednokrotnej, punktu końcowego v2.0 hello zwraca błąd. Witaj `prompt=consent` oświadczeń wyzwalaczy hello OAuth zgody w oknie dialogowym po zalogowaniu użytkownika hello. Witaj w oknie dialogowym z pytaniem, hello użytkownika toogrant uprawnienia toohello aplikacji. |
| login_hint |Optional (Opcjonalność) |Ten parametr toopre wypełnienia hello nazwy użytkownika i wiadomości e-mail adres pole służy hello logowania strony hello użytkownika, jeśli znasz nazwę użytkownika hello wcześniejsze. Często aplikacje tego parametru należy użyć podczas ponownego uwierzytelniania po już wyodrębniania hello username z wcześniejszych logowanie przy użyciu hello `preferred_username` oświadczeń. |
| domain_hint |Optional (Opcjonalność) |Ta wartość może być `consumers` lub `organizations`. Jeśli uwzględniona, pomija hello procesu odnajdywania opartych na poczcie e-mail tego użytkownika hello przechodzi przez na powitania v2.0 strony logowania, wymaga nieco więcej udoskonalone środowisko użytkownika. Często aplikacje tego parametru należy użyć podczas ponownego uwierzytelniania wyodrębniając hello `tid` oświadczeń z hello Identyfikatora tokenu. Jeśli hello `tid` oświadczeń, wartość jest `9188040d-6c67-4c5b-b112-36a304b66dad`, użyj `domain_hint=consumers`. W przeciwnym razie użyj `domain_hint=organizations`. |

W tym momencie hello użytkownika jest tooenter zostanie wyświetlony monit o ich poświadczeń i uwierzytelniania hello ukończone. Witaj punktu końcowego v2.0 sprawdza hello użytkownik zgodził uprawnienia toohello wskazane hello `scope` parametr zapytania. Jeśli użytkownik hello nie zgodził tooany te uprawnienia, punktu końcowego v2.0 hello monituje hello użytkownika tooconsent toohello wymagane uprawnienia. Możesz przeczytać dodatkowe informacje [uprawnień, zgody i aplikacje wielodostępne](active-directory-v2-scopes.md).

Po hello użytkownik jest uwierzytelniany i udziela zgody, zwraca punktu końcowego v2.0 hello aplikacji tooyour odpowiedzi w momencie hello wskazany identyfikator URI przekierowania za pomocą metody hello określonej w hello `response_mode` parametru.

### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie, korzystając z `response_mode=form_post` wygląda podobnie do następującej:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Parametr | Opis |
| --- | --- |
| żądaniu |Witaj identyfikator token, aplikacja hello żądanie. Można użyć hello `id_token` tooverify parametru hello tożsamości użytkownika i rozpocząć sesję przy użyciu hello użytkownika. Aby uzyskać więcej informacji o identyfikatorze tokeny i ich zawartość, zobacz hello [punktu końcowego v2.0 tokeny odwołanie](active-directory-v2-tokens.md). |
| state |Jeśli `state` parametru jest częścią żądania hello hello tę samą wartość powinna być widoczna w odpowiedzi hello. Aplikacja Hello sprawdzić, czy wartości stanu hello hello żądań i odpowiedzi są identyczne. |

### Odpowiedzi na błąd
Odpowiedzi na błędy mogą również wysłane identyfikator URI przekierowania toohello tak, aby hello aplikacji można je obsłużyć. Odpowiedzi na błąd wygląda następująco:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu, który można używać typów tooclassify o błędach i tooreact tooerrors. |
| error_description |Komunikat o błędzie, który ułatwia identyfikowanie hello głównej przyczyny błędu uwierzytelniania. |

### Kody błędów dla błędów punktu końcowego autoryzacji
Witaj poniższej tabeli opisano kody błędów, które mogą być zwracane w hello `error` parametru hello odpowiedzi komunikat o błędzie:

| Kod błędu: | Opis | Akcja klienta |
| --- | --- | --- |
| invalid_request |Błąd protokołu, takie jak brak wymaganego parametru. |Usuń i ponownie prześlij żądanie hello. Jest to błąd programistyczny, zwykle przechwycone podczas testowania początkowej. |
| unauthorized_client |Aplikacja kliencka Hello nie można żądać kod autoryzacji. |Zazwyczaj dzieje się tak, gdy aplikacja kliencka hello nie jest zarejestrowany w usłudze Azure AD lub dzierżawy usługi Azure AD toohello użytkownika nie została dodana. Aplikacja Hello można hello Monituj o aplikacji hello tooinstall instrukcje, a następnie dodaj go tooAzure AD. |
| ACCESS_DENIED |właściciel zasobu Hello odmowa zgody. |Aplikacja kliencka Hello powiadamiać hello użytkownika, którego nie można kontynuować, chyba że użytkownik hello zgadza. |
| unsupported_response_type |w żądaniu hello powitania serwera autoryzacji nie obsługuje hello typ odpowiedzi. |Usuń i ponownie prześlij żądanie hello. Jest to błąd programistyczny, zwykle przechwycone podczas testowania początkowej. |
| server_error |Witaj serwer napotkał nieoczekiwany błąd. |Ponów żądanie hello. Te błędy może wynikać z tymczasowego warunków. Aplikacja kliencka Hello może wyjaśnić toohello użytkownika czy ze względu na tymczasowy błąd tooa jest opóźnione odpowiedzi. |
| temporarily_unavailable |Serwer Hello tymczasowo jest zbyt zajęty toohandle hello żądania. |Ponów żądanie hello. Aplikacja kliencka Hello może wyjaśnić toohello użytkownika czy ze względu na tymczasowy warunek tooa jest opóźnione odpowiedzi. |
| invalid_resource |zasób docelowy Hello jest nieprawidłowy, ponieważ nie istnieje, nie można znaleźć usługi Azure AD, lub nie jest poprawnie skonfigurowana. |Oznacza to, że hello zasobu, jeśli istnieje, nie został skonfigurowany w dzierżawie powitalnych. Aplikacja Hello można Monituj użytkownika hello instrukcje dotyczące instalowania aplikacji hello i dodanie go tooAzure AD. |

## Sprawdź poprawność hello identyfikator tokenu
Odbieranie token identyfikator nie jest wystarczające tooauthenticate hello użytkownika. Musisz również zweryfikować podpisu tokenu identyfikator hello i sprawdzić hello oświadczenia w tokenie hello na wymagania dotyczące Twojej aplikacji. korzysta z punktu końcowego v2.0 Hello [tokenów sieci Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) i publicznego klucza szyfrowania tokenów toosign i sprawdź, czy są prawidłowe.

Można wybrać toovalidate hello Identyfikatora tokenu w kodu klienta, ale popularną praktyką jest toosend hello identyfikator tokenu tooa wewnętrznego serwera i sprawdzania poprawności hello istnieje. Po upewnieniu się hello podpisu tokenu identyfikator hello, musisz tooverify kilka oświadczeń. Aby uzyskać więcej informacji, tym więcej o [sprawdzanie poprawności tokenów](active-directory-v2-tokens.md#validating-tokens) i [ważnych informacji na temat podpisywania Przerzucanie klucza](active-directory-v2-tokens.md#validating-tokens), zobacz hello [v2.0 tokeny odwołanie](active-directory-v2-tokens.md). Firma Microsoft zaleca używanie tooparse biblioteki i sprawdzania poprawności tokenów. Istnieje co najmniej jeden z tych bibliotek dostępne dla większości języków i platform.
<!--TODO: Improve hello information on this-->

Można również toovalidate dodatkowe roszczenia, w zależności od danego scenariusza. Niektóre typowe operacje sprawdzania poprawności obejmują:

* Upewnij się, że użytkownik hello lub organizacji po zarejestrowaniu aplikacji hello.
* Upewnij się, że użytkownik hello ma wymagane uprawnienia lub autoryzacji.
* Upewnij się, że niektóre siły uwierzytelniania wystąpił, takich jak uwierzytelnianie wieloskładnikowe.

Aby uzyskać więcej informacji na temat hello oświadczenia w tokenie identyfikator Zobacz hello [punktu końcowego v2.0 tokeny odwołanie](active-directory-v2-tokens.md).

Po całkowicie poprawności hello identyfikator tokenu można rozpocząć sesji hello użytkownika. Użyj hello oświadczeń w hello identyfikator tokenu tooget informacje o użytkowniku hello w aplikacji. Te informacje służy do wyświetlania, rekordy, autoryzacje i tak dalej.

## Wyślij żądanie wylogowania
Z aplikacji, należy toosign limit hello użytkownika nie jest wystarczające tooclear plików cookie aplikacji lub w przeciwnym razie kończenie sesji użytkownika hello. Należy również przekierować toosign toohello użytkownika hello punktu końcowego v2.0 wychodzących. Jeśli nie zrobisz, użytkownik hello ponownie uwierzytelnia tooyour aplikacji bez ponownego wprowadzania poświadczeń, ponieważ mają one nieprawidłowy jednej sesji logowania z punktem końcowym v2.0 hello.

Można przekierować hello użytkownika toohello `end_session_endpoint` dokument metadanych OpenID Connect hello na liście:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
```

| Parametr | Warunek | Opis |
| ----------------------- | ------------------------------- | ------------ |
| post_logout_redirect_uri | Zalecane | adres URL Hello hello użytkownika jest przekierowane tooafter pomyślnie wylogowywania. Jeśli nie dołączono parametru hello, hello użytkownika jest wyświetlany ogólny komunikat, który jest generowany przez hello punktu końcowego v2.0. Ten adres URL musi pasować hello przekierowania dla aplikacji w portalu rejestracji aplikacji hello zarejestrowane identyfikatory URI.  |

## Wylogowanie jednokrotne
Podczas przekierowywania hello użytkownika toohello `end_session_endpoint`, punktu końcowego v2.0 hello czyści hello sesja z hello przeglądarki. Jednak hello użytkownik nadal może być podpisana tooother aplikacji, które używają kont Microsoft do uwierzytelniania. tooenable te aplikacje toosign hello użytkownika wychodzących jednocześnie hello punktu końcowego v2.0 wysyła HTTP GET żądania toohello zarejestrowany `LogoutUrl` wszystkich aplikacji hello hello użytkownik jest aktualnie zalogowany. Aplikacje musi odpowiadać toothis żądania przez wyczyszczenie wszelkich sesji, która identyfikuje użytkownika hello i zwracanie `200` odpowiedzi.  Jeśli chcesz toosupport funkcji logowania jednokrotnego, limit w aplikacji, musisz zaimplementować takie `LogoutUrl` w kodzie aplikacji.  Można ustawić hello `LogoutUrl` z portalu rejestracji aplikacji hello.

## Diagram protokołu: Token nabycia
Wiele aplikacji sieci web należy toonot tylko znak hello użytkownika, ale także tooaccess usługi sieci web w imieniu użytkownika hello przy użyciu uwierzytelniania OAuth. W tym scenariuszu łączy OpenID Connect do uwierzytelniania użytkowników jednocześnie uzyskanie autoryzacji kod służy dostępu tooget tokeny używania przepływu kodu autoryzacji OAuth hello.

Witaj pełna OpenID Connect logowania i przepływu tokenu nabycia wygląda podobnie toohello diagram dalej. Opisano każdy krok szczegółowo w kolejnych sekcjach hello hello artykułu.

![Protokołu OpenID Connect: Token nabycia](../../media/active-directory-v2-flows/convergence_scenarios_webapp_webapi.png)

## Pobieranie tokenów dostępu
tooacquire tokenów dostępu, należy zmodyfikować hello żądania logowania:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application ID
&response_type=id_token%20code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered redirect URI, URL encoded
&response_mode=form_post                              // 'query', 'form_post', or 'fragment'
&scope=openid%20                                      // Include both 'openid' and scopes that your app needs  
offline_access%20                                         
https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

> [!TIP]
> Kliknij następujące łącze tooexecute hello tego żądania. Po zalogowaniu w przeglądarce jest przekierowane toohttps://localhost/myapp/, ID token i kod na pasku adresu hello. Należy pamiętać, że używa tego żądania `response_mode=query` (tylko w celach demonstracyjnych). Firma Microsoft zaleca użycie `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token%20code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

Włączając zakresy uprawnień w żądaniu hello i za pomocą `response_type=id_token code`, punktu końcowego v2.0 hello zapewnia hello użytkownik zgodził uprawnienia toohello wskazane hello `scope` parametr zapytania. Zwraca tooexchange autoryzacji kodu tooyour aplikacji dla tokenu dostępu.

### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie z za pomocą `response_mode=form_post` wygląda podobnie do następującej:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Parametr | Opis |
| --- | --- |
| żądaniu |Witaj identyfikator token, aplikacja hello żądanie. Można użyć hello identyfikator tokenu tooverify hello tożsamości użytkownika i rozpocząć sesję użytkownika hello. Szczegółowe informacje o identyfikatorze tokeny i ich zawartość znajdziesz w hello [punktu końcowego v2.0 tokeny odwołanie](active-directory-v2-tokens.md). |
| Kod |Kod autoryzacji Hello hello żądanej aplikacji. zasób docelowy hello aplikacji Hello można używać toorequest kod autoryzacji hello tokenu dostępu. Kod autoryzacji jest bardzo krótkim okresie. Zazwyczaj autoryzacji kod wygasa po upływie około 10 minut. |
| state |Jeśli parametr Stan jest uwzględniony w żądaniu hello, hello tej samej wartości powinny być wyświetlane w hello odpowiedzi. Aplikacja Hello sprawdzić, czy wartości stanu hello hello żądań i odpowiedzi są identyczne. |

### Odpowiedzi na błąd
Odpowiedzi na błędy mogą również wysłane identyfikator URI przekierowania toohello tak, aby hello aplikacji można je odpowiednią obsługę. Odpowiedzi na błąd wygląda następująco:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu, który można używać typów tooclassify o błędach i tooreact tooerrors. |
| error_description |Komunikat o błędzie, który ułatwia identyfikowanie hello głównej przyczyny błędu uwierzytelniania. |

Opis możliwych kodów błędów i zalecane klienta odpowiedzi, zobacz [kody błędów dla błędów punktu końcowego autoryzacji](#error-codes-for-authorization-endpoint-errors).

Jeśli masz kod autoryzacji i tokena identyfikator możesz zalogować użytkownika hello i uzyskać tokeny dostępu w ich imieniu. toosign hello użytkownika w, musisz zweryfikować hello identyfikator tokenu [dokładnie zgodnie z opisem](#validate-the-id-token). tokeny dostępu tooget, wykonaj kroki hello opisanego w naszym [dokumentacji protokołu OAuth](active-directory-v2-protocols-oauth-code.md#request-an-access-token).
