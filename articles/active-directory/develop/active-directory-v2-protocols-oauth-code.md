---
title: "Przepływu kodu autoryzacji OAuth v2.0 usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji sieci web przy użyciu usługi Azure AD implementacji protokołu uwierzytelniania OAuth 2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: ae1d7d86-7098-468c-aa32-20df0a10ee3d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: b64413e9cc916837dc779b92117f90293c4f1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# Protokoły v2.0 - przepływu kodu autoryzacji OAuth 2.0
Udzielania kodu autoryzacji protokołu OAuth 2.0 służy w aplikacjach, które są zainstalowane na urządzeniu w celu uzyskania dostępu do chronionych zasobów, takich jak interfejsów API sieci web.  Przy użyciu app model v2.0 w implementacji protokołu OAuth 2.0, można dodać Zaloguj się i interfejsu API dostępu do aplikacji mobilnych i klasycznych.  Ten przewodnik jest niezależny od języka i opisuje sposób wysyłania i odbierania wiadomości HTTP bez przy użyciu dowolnej z naszych bibliotekach open source.

> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez punktu końcowego v2.0.  Aby ustalić, czy należy używać punktu końcowego v2.0, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

Przepływu kodu autoryzacji protokołu OAuth 2.0 jest opisany w w [sekcji 4.1 specyfikacji protokołu OAuth 2.0](http://tools.ietf.org/html/rfc6749).  Służy do wykonywania uwierzytelniania i autoryzacji w większości typów aplikacji, w tym [sieci web apps](active-directory-v2-flows.md#web-apps) i [natywnie zainstalowane aplikacje](active-directory-v2-flows.md#mobile-and-native-apps).  Umożliwia aplikacji można bezpiecznie uzyskać access_tokens, której można uzyskać dostęp do zasobów, które są chronione przy użyciu punktu końcowego v2.0.  

## Diagram protokołu
Na wysokim poziomie przepływ cały proces uwierzytelniania dla aplikacji native/mobile wygląda nieco następująco:

![Przepływu kodu autoryzacji OAuth](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## Kod autoryzacji żądania
Przepływu kodu autoryzacji rozpoczyna się od klienta kierowanie użytkownikowi `/authorize` punktu końcowego.  W tym żądaniu klient wskazuje uprawnień wymaganych do uzyskania dostępu przez użytkownika:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345
```

> [!TIP]
> Kliknij poniższe łącze, aby wykonać tego żądania. Po zalogowaniu, przeglądarka powinno nastąpić przekierowanie do `https://localhost/myapp/` z `code` na pasku adresu.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |`{tenant}` Wartość w ścieżce żądania może być używana w celu kontrolowania, kto może zalogować się do aplikacji.  Dozwolone wartości `common`, `organizations`, `consumers`i dzierżawców identyfikatorów.  Aby uzyskać więcej szczegółów, zobacz [protokołu podstawy](active-directory-v2-protocols.md#endpoints). |
| client_id |Wymagane |Identyfikator aplikacji który portalu rejestracji ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) przypisany do aplikacji. |
| response_type |Wymagane |Musi zawierać `code` dla przepływu kodu autoryzacji. |
| redirect_uri |Zalecane |Redirect_uri aplikacji, w którym można wysłanych i odebranych przez aplikację odpowiedzi uwierzytelniania.  Go musi dokładnie pasować redirect_uris, który został zarejestrowany w portalu, z wyjątkiem musi być zakodowane w adresie url.  W przypadku aplikacji natywnej & przenośnych powinny używać wartość domyślną `https://login.microsoftonline.com/common/oauth2/nativeclient`. |
| Zakres |Wymagane |Rozdzieloną spacjami listę [zakresy](active-directory-v2-scopes.md) oznaczający użytkownika o zgodę. |
| response_mode |Zalecane |Określa metodę, które mają być używane do wysyłania wynikowy token wstecz do aplikacji.  Może być `query` lub `form_post`. |
| state |Zalecane |Wartość zawarte w żądaniu zwracana w odpowiedzi tokenu.  Można go ciągiem zawartość, która ma.  Losowo generowany unikatową wartość jest zazwyczaj używana w przypadku [zapobieganie fałszerstwie żądania międzywitrynowego](http://tools.ietf.org/html/rfc6749#section-10.12).  Stan służy także do kodowania informacje o stanie użytkownika w aplikacji przed wystąpieniem żądania uwierzytelniania, takich jak strony lub widok, które były na. |
| wiersz |Opcjonalne |Wskazuje typ interakcji z użytkownikiem, który jest wymagany.  W tej chwili jedynymi prawidłowymi wartościami są "login", "none", "wyrazić zgodę".  `prompt=login`Spowoduje to wymuszenie użytkownika o wprowadzenie poświadczeń w tym żądaniu Negacja jednokrotnego.  `prompt=none`jest to odwrotność wzorca - zapewni, że użytkownik nie zobaczy jakiejkolwiek monitu interakcyjnego.  Jeśli żądanie nie można ukończyć w trybie dyskretnym za pośrednictwem jednokrotnego, punktu końcowego v2.0 spowoduje zwrócenie błędu.  `prompt=consent`wyzwoli okna dialogowego zgoda OAuth, po użytkownik się zaloguje, użytkownikowi uprawnienia do aplikacji. |
| login_hint |Opcjonalne |Można wstępnie wypełnić pole adresu e-mail/nazwa użytkownika konta na stronie dla użytkownika, jeśli znasz swoją nazwę użytkownika wcześniejsze.  Aplikacje często użyje tego parametru podczas ponownego uwierzytelniania już o wyodrębnić nazwy użytkownika z poprzedniej logowania przy użyciu `preferred_username` oświadczeń. |
| domain_hint |Opcjonalne |Może być jednym z `consumers` lub `organizations`.  Jeśli uwzględniona, pominie proces odnajdowania opartych na poczcie e-mail tego użytkownika odbywa się przez na stronie rejestracji v2.0, co może prowadzić do wymaga nieco więcej udoskonalone środowisko użytkownika.  Aplikacje często użyje tego parametru podczas ponownego uwierzytelniania, wyodrębniając `tid` z poprzednich logowanie.  Jeśli `tid` oświadczeń, wartość jest `9188040d-6c67-4c5b-b112-36a304b66dad`, należy użyć `domain_hint=consumers`.  W przeciwnym razie użyj `domain_hint=organizations`. |

W tym momencie użytkownik jest proszony o wprowadzenie poświadczeń i wykonania uwierzytelnienia.  Punktu końcowego v2.0 będzie również upewnij się, że użytkownik zgodził się na uprawnienia wskazanych w `scope` parametr zapytania.  Jeśli użytkownik zgodził się nie do dowolnego z tych uprawnień, poprosi użytkownika o zgodę na wymagane uprawnienia.  Szczegóły [uprawnień, zgody i aplikacje wielodostępne znajdują się w tym miejscu](active-directory-v2-scopes.md).

Po przyznaje zgody i uwierzytelnia użytkownika, punktu końcowego v2.0 zwróci odpowiedzi do aplikacji na wskazany `redirect_uri`, za pomocą metody określonej w `response_mode` parametru.

#### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie przy użyciu `response_mode=query` wygląda jak:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| Parametr | Opis |
| --- | --- |
| Kod |Authorization_code, żądany przez aplikację. Aplikację można użyć kodu autoryzacji do żądania tokenu dostępu dla zasobu docelowego.  Authorization_codes są bardzo krótko, zwykle wygaśnie po około 10 minut. |
| state |Jeśli parametr Stan jest uwzględniony w żądaniu, tę samą wartość powinna być widoczna w odpowiedzi. Aplikacja powinna Sprawdź, czy wartości stan żądania i odpowiedzi są identyczne. |

#### Odpowiedzi na błąd
Odpowiedzi na błędy mogą być również wysyłane do `redirect_uri` dzięki aplikacji można je odpowiednią obsługę:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu, który może służyć do klasyfikowania typy błędów występujących i może służyć do reagowania na błędy. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera Określ przyczynę błędu uwierzytelniania. |

#### Kody błędów dla błędów punktu końcowego autoryzacji
W poniższej tabeli opisano różne kody błędów, które mogą być zwracane w `error` parametr odpowiedzi na błąd.

| Kod błędu: | Opis | Akcja klienta |
| --- | --- | --- |
| invalid_request |Błąd protokołu, takie jak brak wymaganego parametru. |Usuń i ponownie prześlij żądanie. To rozwinięcie błąd jest zwykle przechwycono podczas testowania początkowej. |
| unauthorized_client |Aplikacja kliencka nie jest dozwolone przy kod autoryzacji żądania. |Dzieje się tak zazwyczaj, gdy aplikacja kliencka nie jest zarejestrowany w usłudze Azure AD lub nie została dodana do dzierżawy usługi Azure AD przez użytkownika. Aplikację można monitować użytkownika z instrukcji dotyczących instalowania aplikacji i dodanie go do usługi Azure AD. |
| ACCESS_DENIED |Odmowa zgody właściciel zasobu |Aplikacja kliencka powiadamiać użytkownika, którego nie można kontynuować, chyba że użytkownik zgadza. |
| unsupported_response_type |Serwer autoryzacji w żądaniu nie obsługuje typ odpowiedzi. |Usuń i ponownie prześlij żądanie. To rozwinięcie błąd jest zwykle przechwycono podczas testowania początkowej. |
| server_error |Serwer napotkał nieoczekiwany błąd. |Ponów żądanie. Te błędy może wynikać z tymczasowego warunków. Aplikacja kliencka może wyjaśnić użytkownikowi, że jego odpowiedzi jest opóźniony ze względu na tymczasowy błąd. |
| temporarily_unavailable |Serwer jest tymczasowo zbyt zajęty, aby obsłużyć żądania. |Ponów żądanie. Aplikacja kliencka może wyjaśnić użytkownikowi, że jego odpowiedzi jest opóźniony ze względu na tymczasowy warunek. |
| invalid_resource |Zasób docelowy jest nieprawidłowy, ponieważ nie istnieje, nie można znaleźć usługi Azure AD lub nie została poprawnie skonfigurowana. |Oznacza to, że zasób, jeśli istnieje, nie został skonfigurowany w dzierżawie. Aplikację można monitować użytkownika z instrukcji dotyczących instalowania aplikacji i dodanie go do usługi Azure AD. |

## Żądanie tokenu dostępu
Teraz, gdy zostały nabyte authorization_code i mieć odpowiednie uprawnienia udzielone przez użytkownika, można wykorzystać `code` dla `access_token` do żądanego zasobu, wysyłając `POST` żądanie `/token` punktu końcowego:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

> [!TIP]
> Spróbuj wykonywania tego żądania w Postman! (Pamiętaj zastąpić `code`) [ ![uruchamiane w Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |`{tenant}` Wartość w ścieżce żądania może być używana w celu kontrolowania, kto może zalogować się do aplikacji.  Dozwolone wartości `common`, `organizations`, `consumers`i dzierżawców identyfikatorów.  Aby uzyskać więcej szczegółów, zobacz [protokołu podstawy](active-directory-v2-protocols.md#endpoints). |
| client_id |Wymagane |Identyfikator aplikacji który portalu rejestracji ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) przypisany do aplikacji. |
| Typ grant_type |Wymagane |Musi być `authorization_code` dla przepływu kodu autoryzacji. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów.  Zakresy, w tym etap musi być równoważna lub podzbiór zakresów żądany podczas pierwszego etap.  Jeśli zakresy określone w tym żądaniu obejmują wiele zasobów serwerów, punktu końcowego v2.0 zwróci token dla zasobu określonego w pierwszym zakresie.  Bardziej szczegółowy opis zakresów, można znaleźć w temacie [uprawnień, zgody i zakresy](active-directory-v2-scopes.md). |
| Kod |Wymagane |Authorization_code, uzyskanego w pierwszego etap przepływu. |
| redirect_uri |Wymagane |Tym samym wartość redirect_uri został użyty do uzyskania authorization_code. |
| client_secret |wymagane dla aplikacji sieci web |Klucz tajny aplikacji utworzonej w portalu rejestracji aplikacji dla aplikacji.  Nie należy można użyć w natywnej aplikacji, ponieważ client_secrets nie może być niezawodnie przechowywanych na urządzeniach.  Jest wymagane dla aplikacji sieci web i interfejsów API, które mogą bezpiecznie przechowywać client_secret po stronie serwera sieci web. |

#### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie tokenu będą wyglądać jak:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parametr | Opis |
| --- | --- |
| ' access_token ' |Żądany dostęp token. Aplikacja może używać tego tokenu do uwierzytelniania zabezpieczonych zasobów, takich jak interfejsu API sieci web. |
| token_type |Wskazuje wartość typ tokenu. Elementów nośnych są jedynym typem, który obsługuje usługę Azure AD |
| expires_in |Jak długo token dostępu jest nieprawidłowy (w sekundach). |
| Zakres |Zakresy ' access_token ' jest nieprawidłowa dla. |
| refresh_token |Token odświeżania OAuth 2.0. Aplikacja może używać tego tokenu uzyskać tokeny dodatkowe dostępu po wygaśnięciu tokenu dostępu bieżącego.  Refresh_tokens są długotrwałe i pozwala zachować dostęp do zasobów przez dłuższy czas.  Aby uzyskać więcej szczegółów, zobacz [odwołania do tokenu v2.0](active-directory-v2-tokens.md). |
| żądaniu |Niepodpisane JSON Web Token (JWT). Aplikacji base64Url może zdekodować segmentów tego tokenu do żądania informacji dotyczących użytkownika, który jest zalogowany. Można je wyświetlić i pamięci podręcznej wartości aplikacji, ale nie należy polegać na nich autoryzacji lub granic zabezpieczeń.  Aby uzyskać więcej informacji na temat id_tokens zobacz [odwołania do tokenu punktu końcowego v2.0](active-directory-v2-tokens.md). |

#### Odpowiedzi na błąd
Błąd odpowiedzi będą wyglądać jak:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: The provided value for the input parameter 'scope' is not valid. The scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu, który może służyć do klasyfikowania typy błędów występujących i może służyć do reagowania na błędy. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera Określ przyczynę błędu uwierzytelniania. |
| error_codes |Listę kodów błędu STS, które mogą pomóc w diagnostyce. |
| sygnatura czasowa |Czas, w którym wystąpił błąd. |
| trace_id |Unikatowy identyfikator dla żądania, które mogą pomóc w diagnostyce. |
| correlation_id |Unikatowy identyfikator dla żądania, które mogą pomóc w diagnostyce między składnikami. |

#### Kody błędów dla punktu końcowego tokena błędów
| Kod błędu: | Opis | Akcja klienta |
| --- | --- | --- |
| invalid_request |Błąd protokołu, takie jak brak wymaganego parametru. |Usuń i ponownie prześlij żądanie |
| invalid_grant |Kod autoryzacji jest nieprawidłowa lub wygasła. |Ponów żądanie nowej `/authorize` punktu końcowego |
| unauthorized_client |Uwierzytelniany klient nie ma uprawnień do używania tego typu przydziału autoryzacji. |Dzieje się tak zazwyczaj, gdy aplikacja kliencka nie jest zarejestrowany w usłudze Azure AD lub nie została dodana do dzierżawy usługi Azure AD przez użytkownika. Aplikację można monitować użytkownika z instrukcji dotyczących instalowania aplikacji i dodanie go do usługi Azure AD. |
| invalid_client |Uwierzytelnianie klienta nie powiodło się. |Poświadczenia klienta są nieprawidłowe. Aby rozwiązać problem, administrator aplikacji aktualizuje poświadczenia. |
| unsupported_grant_type |Serwer autoryzacji nie obsługuje typ przydziału autoryzacji. |Zmień typ grant w żądaniu. Tego typu błędu powinien wystąpić tylko podczas programowania i być wykryte podczas testowania początkowej. |
| invalid_resource |Zasób docelowy jest nieprawidłowy, ponieważ nie istnieje, nie można znaleźć usługi Azure AD lub nie została poprawnie skonfigurowana. |Oznacza to, że zasób, jeśli istnieje, nie został skonfigurowany w dzierżawie. Aplikację można monitować użytkownika z instrukcji dotyczących instalowania aplikacji i dodanie go do usługi Azure AD. |
| interaction_required |Żądanie wymaga interakcji z użytkownikiem. Na przykład krok dodatkowego uwierzytelniania jest wymagany. |Ponów próbę żądania z tego samego zasobu. |
| temporarily_unavailable |Serwer jest tymczasowo zbyt zajęty, aby obsłużyć żądania. |Ponów żądanie. Aplikacja kliencka może wyjaśnić użytkownikowi, że jego odpowiedzi jest opóźniony ze względu na tymczasowy warunek. |

## Użyj tokenu dostępu
Teraz, zostały pomyślnie uzyskano `access_token`, użyć tokenu w żądaniach wysyłanych do interfejsów API sieci Web w tym `Authorization` nagłówka:

> [!TIP]
> Wykonanie tego żądania w Postman! (Zastąp `Authorization` nagłówek pierwszego) [ ![uruchamiane w Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## Odśwież token dostępu
Access_tokens są krótkie żyła i należy je odświeżyć, po wygaśnięciu, aby kontynuować, uzyskiwanie dostępu do zasobów.  Możesz to zrobić poprzez przesłanie innego `POST` żądanie `/token` punktu końcowego, ale tym razem zapewniające `refresh_token` zamiast `code`:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for web apps
```

> [!TIP]
> Spróbuj wykonywania tego żądania w Postman! (Pamiętaj zastąpić `refresh_token`) [ ![uruchamiane w Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |`{tenant}` Wartość w ścieżce żądania może być używana w celu kontrolowania, kto może zalogować się do aplikacji.  Dozwolone wartości `common`, `organizations`, `consumers`i dzierżawców identyfikatorów.  Aby uzyskać więcej szczegółów, zobacz [protokołu podstawy](active-directory-v2-protocols.md#endpoints). |
| client_id |Wymagane |Identyfikator aplikacji który portalu rejestracji ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) przypisany do aplikacji. |
| Typ grant_type |Wymagane |Musi być `refresh_token` dla ten etap przepływu kodu autoryzacji. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów.  Zakresy, w tym etap musi być równoważna lub podzbiór zakresów w oryginalnym etap żądania authorization_code.  Jeśli zakresy określone w tym żądaniu obejmują wiele zasobów serwerów, punktu końcowego v2.0 zwróci token dla zasobu określonego w pierwszym zakresie.  Bardziej szczegółowy opis zakresów, można znaleźć w temacie [uprawnień, zgody i zakresy](active-directory-v2-scopes.md). |
| refresh_token |Wymagane |Refresh_token, uzyskanego w drugi etap przepływu. |
| redirect_uri |Wymagane |Tym samym wartość redirect_uri został użyty do uzyskania authorization_code. |
| client_secret |wymagane dla aplikacji sieci web |Klucz tajny aplikacji utworzonej w portalu rejestracji aplikacji dla aplikacji.  Nie należy można użyć w natywnej aplikacji, ponieważ client_secrets nie może być niezawodnie przechowywanych na urządzeniach.  Jest wymagane dla aplikacji sieci web i interfejsów API, które mogą bezpiecznie przechowywać client_secret po stronie serwera sieci web. |

#### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie tokenu będą wyglądać jak:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Parametr | Opis |
| --- | --- |
| ' access_token ' |Żądany dostęp token. Aplikacja może używać tego tokenu do uwierzytelniania zabezpieczonych zasobów, takich jak interfejsu API sieci web. |
| token_type |Wskazuje wartość typ tokenu. Elementów nośnych są jedynym typem, który obsługuje usługę Azure AD |
| expires_in |Jak długo token dostępu jest nieprawidłowy (w sekundach). |
| Zakres |Zakresy ' access_token ' jest nieprawidłowa dla. |
| refresh_token |Nowy token odświeżania OAuth 2.0. Z tym tokenem nowo pobranych odświeżania, aby upewnić się, że tokenów odświeżania ważność tak długo, jak to możliwe, należy zastąpić stary token odświeżania. |
| żądaniu |Niepodpisane JSON Web Token (JWT). Aplikacji base64Url może zdekodować segmentów tego tokenu do żądania informacji dotyczących użytkownika, który jest zalogowany. Można je wyświetlić i pamięci podręcznej wartości aplikacji, ale nie należy polegać na nich autoryzacji lub granic zabezpieczeń.  Aby uzyskać więcej informacji na temat id_tokens zobacz [odwołania do tokenu punktu końcowego v2.0](active-directory-v2-tokens.md). |

#### Odpowiedzi na błąd
```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: The provided value for the input parameter 'scope' is not valid. The scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu, który może służyć do klasyfikowania typy błędów występujących i może służyć do reagowania na błędy. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera Określ przyczynę błędu uwierzytelniania. |
| error_codes |Listę kodów błędu STS, które mogą pomóc w diagnostyce. |
| sygnatura czasowa |Czas, w którym wystąpił błąd. |
| trace_id |Unikatowy identyfikator dla żądania, które mogą pomóc w diagnostyce. |
| correlation_id |Unikatowy identyfikator dla żądania, które mogą pomóc w diagnostyce między składnikami. |

Opis akcji zalecane klienta i kody błędów, zobacz [kody błędów dla błędów punktu końcowego tokena](#error-codes-for-token-endpoint-errors).

