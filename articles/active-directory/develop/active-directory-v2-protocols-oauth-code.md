---
title: "przepływu kodu autoryzacji OAuth 2.0 aaaAzure AD | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji sieci web przy użyciu usługi Azure AD implementacji protokołu uwierzytelniania hello OAuth 2.0."
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
ms.openlocfilehash: dee58f2f5c627fef35cae279349728c3c7bf9421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Protokoły v2.0 - przepływu kodu autoryzacji OAuth 2.0
udzielania kodu autoryzacji Hello OAuth 2.0 służy w aplikacjach, które są zainstalowane na urządzeniu toogain dostępu tooprotected zasoby, takie jak interfejsów API sieci web.  Przy użyciu hello app model v2.0 w implementacji protokołu OAuth 2.0, można dodać Zaloguj się i aplikacji mobilnych i klasycznych tooyour dostęp do interfejsu API.  Ten przewodnik jest niezależny od języka i opisano sposób toosend i odbieranie wiadomości HTTP bez przy użyciu dowolnej z naszych bibliotekach open source.

> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.  toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

Witaj przepływu kodu autoryzacji protokołu OAuth 2.0 jest opisany w w [sekcji 4.1 specyfikacji hello OAuth 2.0](http://tools.ietf.org/html/rfc6749).  Jest używana tooperform uwierzytelnianie i autoryzację w hello większość typów aplikacji, w tym [sieci web apps](active-directory-v2-flows.md#web-apps) i [natywnie zainstalowane aplikacje](active-directory-v2-flows.md#mobile-and-native-apps).  Umożliwia aplikacji toosecurely uzyskać access_tokens, które mogą być używane tooaccess zasobów, które są chronione przy użyciu punktu końcowego v2.0 hello.  

## Diagram protokołu
Na wysokim poziomie hello przepływ cały proces uwierzytelniania dla aplikacji native/mobile wygląda nieco następująco:

![Przepływu kodu autoryzacji OAuth](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## Kod autoryzacji żądania
przepływu kodu autoryzacji Hello rozpoczyna się od klienta hello kierowanie hello użytkownika toohello `/authorize` punktu końcowego.  W tym żądaniu powitania klienta wskazuje uprawnienia hello musi tooacquire hello użytkownika:

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
> Kliknij łącze hello poniżej tooexecute tego żądania. Po zalogowaniu, przeglądarka powinno nastąpić przekierowanie zbyt`https://localhost/myapp/` z `code` na pasku adresu hello.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Witaj `{tenant}` wartość w ścieżce hello hello żądania mogą być używane toocontrol, który można zalogować się do aplikacji hello.  Witaj dozwolone wartości to `common`, `organizations`, `consumers`i dzierżawców identyfikatorów.  Aby uzyskać więcej szczegółów, zobacz [protokołu podstawy](active-directory-v2-protocols.md#endpoints). |
| client_id |Wymagane |Identyfikator aplikacji tego portalu rejestracji hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) przypisany do aplikacji. |
| response_type |Wymagane |Musi zawierać `code` dla przepływu kodu autoryzacji hello. |
| redirect_uri |Zalecane |Witaj redirect_uri aplikacji, w którym można wysłanych i odebranych przez aplikację odpowiedzi uwierzytelniania.  Dokładnie musi odpowiadać jedną redirect_uris hello, który został zarejestrowany w portalu hello, z wyjątkiem musi być zakodowane w adresie url.  Dla aplikacji natywnych i przenośnych, należy używać wartość domyślną hello `https://login.microsoftonline.com/common/oauth2/nativeclient`. |
| Zakres |Wymagane |Rozdzieloną spacjami listę [zakresy](active-directory-v2-scopes.md) , które mają hello tooconsent użytkownika do. |
| response_mode |Zalecane |Określa metodę hello, który ma być używane toosend hello wynikowy tooyour tyłu tokenu aplikacji.  Może być `query` lub `form_post`. |
| state |Zalecane |Wartość zawarte w żądaniu hello, zwracana w hello odpowiedzi tokenu.  Można go ciągiem zawartość, która ma.  Losowo generowany unikatową wartość jest zazwyczaj używana w przypadku [zapobieganie fałszerstwie żądania międzywitrynowego](http://tools.ietf.org/html/rfc6749#section-10.12).  Stan Hello jest również używane tooencode informacji na temat stanu hello użytkownika w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takie jak strona hello lub widok, które były na. |
| wiersz |Opcjonalne |Wskazuje typ hello interakcji z użytkownikiem, który jest wymagany.  Witaj prawidłowe są tylko wartości w tym momencie "login", "none", "wyrazić zgodę".  `prompt=login`zostanie życie hello tooenter użytkownika poświadczeń w tym żądaniu Negacja jednokrotnego na.  `prompt=none`jest hello przeciwną - zapewnić nie zobaczy tego użytkownika hello jakiejkolwiek monitu interakcyjnego.  Jeśli nie można ukończyć żądania hello dyskretnie za pośrednictwem jednokrotnego, punktu końcowego v2.0 hello zwróci błąd.  `prompt=consent`wyzwalacz hello OAuth zgody okna dialogowego po hello użytkownik loguje, prosząc hello użytkownika toogrant uprawnienia toohello aplikacji. |
| login_hint |Opcjonalne |Można używane wypełnienia toopre hello nazwy użytkownika/poczta e-mail adres pola hello zalogować się Strona hello użytkownika, jeśli znasz swoją nazwę użytkownika wcześniejsze.  Aplikacje często użyje tego parametru podczas ponowne uwierzytelnianie hello username już o wyodrębnione z poprzednich logowanie przy użyciu hello `preferred_username` oświadczeń. |
| domain_hint |Opcjonalne |Może być jednym z `consumers` lub `organizations`.  Jeśli uwzględniona, pominie proces odnajdywania opartych na poczcie e-mail hello użytkownik przechodzi przez na stronie logowania v2.0 hello wiodące tooa wymaga nieco więcej usprawnić środowisko użytkownika.  Aplikacje często użyje tego parametru podczas ponownego uwierzytelniania, wyodrębniając hello `tid` z poprzednich logowanie.  Jeśli hello `tid` oświadczeń, wartość jest `9188040d-6c67-4c5b-b112-36a304b66dad`, należy użyć `domain_hint=consumers`.  W przeciwnym razie użyj `domain_hint=organizations`. |

W tym momencie hello użytkownik będzie zadawane tooenter ich poświadczeń i uwierzytelniania hello ukończone.  Witaj punktu końcowego v2.0 zapewni hello użytkownik zgodził uprawnienia toohello wskazane hello `scope` parametr zapytania.  Jeśli hello użytkownik zgodził nie tooany tych uprawnień, jego poprosi tooconsent użytkownika hello toohello wymagane uprawnienia.  Szczegóły [uprawnień, zgody i aplikacje wielodostępne znajdują się w tym miejscu](active-directory-v2-scopes.md).

Po hello użytkownik jest uwierzytelniany i udziela zgody, punktu końcowego v2.0 hello zwróci aplikacji tooyour odpowiedzi w momencie hello wskazanych `redirect_uri`, przy użyciu metody hello określonej w hello `response_mode` parametru.

#### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie przy użyciu `response_mode=query` wygląda jak:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| Parametr | Opis |
| --- | --- |
| Kod |Witaj authorization_code, który hello żądanej aplikacji. zasób docelowy hello aplikacji Hello można używać toorequest kod autoryzacji hello tokenu dostępu.  Authorization_codes są bardzo krótko, zwykle wygaśnie po około 10 minut. |
| state |Jeśli parametr Stan jest uwzględniony w żądaniu hello, hello tej samej wartości powinny być wyświetlane w hello odpowiedzi. Aplikacja Hello sprawdzić, czy wartości stanu hello hello żądań i odpowiedzi są identyczne. |

#### Odpowiedzi na błąd
Odpowiedzi na błędy mogą być również wysyłane toohello `redirect_uri` dzięki aplikacji hello można je odpowiednią obsługę:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu mogą być używane tooclassify typów błędów występujących, która może być używana tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |

#### Kody błędów dla błędów punktu końcowego autoryzacji
Witaj poniższej tabeli opisano hello różnych kody błędów, które mogą być zwracane w hello `error` parametru hello odpowiedzi na błąd.

| Kod błędu: | Opis | Akcja klienta |
| --- | --- | --- |
| invalid_request |Błąd protokołu, takie jak brak wymaganego parametru. |Usuń i ponownie prześlij żądanie hello. To rozwinięcie błąd jest zwykle przechwycono podczas testowania początkowej. |
| unauthorized_client |Witaj aplikację klienta nie jest dozwolone toorequest kod autoryzacji. |Zazwyczaj dzieje się tak, gdy aplikacja kliencka hello nie jest zarejestrowany w usłudze Azure AD lub dzierżawy usługi Azure AD toohello użytkownika nie została dodana. aplikacji Hello można monitować użytkownika hello z instrukcji dotyczących instalowania aplikacji hello i dodanie go tooAzure AD. |
| ACCESS_DENIED |Odmowa zgody właściciel zasobu |Aplikacja kliencka Hello powiadamiać hello użytkownika, którego nie można kontynuować, chyba że użytkownik hello zgadza. |
| unsupported_response_type |w żądaniu hello powitania serwera autoryzacji nie obsługuje hello typ odpowiedzi. |Usuń i ponownie prześlij żądanie hello. To rozwinięcie błąd jest zwykle przechwycono podczas testowania początkowej. |
| server_error |Witaj serwer napotkał nieoczekiwany błąd. |Ponów żądanie hello. Te błędy może wynikać z tymczasowego warunków. Aplikacja kliencka Hello może wyjaśnić toohello użytkownika czy odpowiedzi jest opóźniony ze względu na tymczasowy błąd. |
| temporarily_unavailable |Serwer Hello tymczasowo jest zbyt zajęty toohandle hello żądania. |Ponów żądanie hello. Aplikacja kliencka Hello może wyjaśnić toohello użytkownika czy odpowiedzi jest opóźniony ze względu na tymczasowy warunek. |
| invalid_resource |zasób docelowy Hello jest nieprawidłowy, ponieważ nie istnieje, nie można znaleźć usługi Azure AD lub nie została poprawnie skonfigurowana. |Oznacza to, że hello zasobu, jeśli istnieje, nie został skonfigurowany w dzierżawie powitalnych. aplikacji Hello można monitować użytkownika hello z instrukcji dotyczących instalowania aplikacji hello i dodanie go tooAzure AD. |

## Żądanie tokenu dostępu
Teraz, gdy zostały nabyte authorization_code i mieć odpowiednie uprawnienia udzielone przez użytkownika hello możesz zrealizować hello `code` dla `access_token` toohello żądanego zasobu, wysyłając `POST` żądania toohello `/token` punktu końcowego:

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
> Spróbuj wykonywania tego żądania w Postman! (Nie zapomnij tooreplace hello `code`) [ ![uruchamiane w Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Witaj `{tenant}` wartość w ścieżce hello hello żądania mogą być używane toocontrol, który można zalogować się do aplikacji hello.  Witaj dozwolone wartości to `common`, `organizations`, `consumers`i dzierżawców identyfikatorów.  Aby uzyskać więcej szczegółów, zobacz [protokołu podstawy](active-directory-v2-protocols.md#endpoints). |
| client_id |Wymagane |Identyfikator aplikacji tego portalu rejestracji hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) przypisany do aplikacji. |
| Typ grant_type |Wymagane |Musi być `authorization_code` dla przepływu kodu autoryzacji hello. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów.  zakresy Hello żądanie, w tym etap należy równoważne tooor podzbiór zakresów hello wystąpić w hello pierwszego etap.  Jeśli określony w żądaniu zakresy hello obejmują wiele zasobów serwerów, punktu końcowego v2.0 hello zwróci token dla zasobu hello określone w zakresie pierwszy hello.  Aby uzyskać bardziej szczegółowy opis zakresów można znaleźć za[uprawnień, zgody i zakresy](active-directory-v2-scopes.md). |
| Kod |Wymagane |Witaj authorization_code uzyskanego w hello pierwszego etap hello przepływu. |
| redirect_uri |Wymagane |Witaj tę samą wartość redirect_uri, która była używana tooacquire hello authorization_code. |
| client_secret |wymagane dla aplikacji sieci web |Witaj klucz tajny aplikacji utworzonej w portalu rejestracji aplikacji hello dla aplikacji.  Nie należy można użyć w natywnej aplikacji, ponieważ client_secrets nie może być niezawodnie przechowywanych na urządzeniach.  Jest wymagane dla aplikacji sieci web i interfejsów API, która ma hello możliwości toostore hello client_secret bezpiecznie na powitania po stronie serwera sieci web. |

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
| ' access_token ' |token dostępu do żądanego Hello. Aplikacja Hello można użyć tego toohello tokenu tooauthenticate zabezpieczonych zasobów, takich jak interfejsu API sieci web. |
| token_type |Wskazuje wartość tokenu typu hello. Witaj tylko typ, który obsługuje usługę Azure AD jest elementu nośnego |
| expires_in |Jak długo hello token dostępu jest nieprawidłowy (w sekundach). |
| Zakres |nadaje się do zakresów Hello hello ' access_token '. |
| refresh_token |Token odświeżania OAuth 2.0. Witaj aplikacji można użyć tego tokenu uzyskanie tokenów dostępu dodatkowe po wygaśnięciu hello bieżącego tokenu dostępu.  Refresh_tokens są długotrwałe i mogą być używane tooretain tooresources dostępu przez dłuższy czas.  Aby uzyskać więcej szczegółów można znaleźć toohello [odwołania do tokenu v2.0](active-directory-v2-tokens.md). |
| żądaniu |Niepodpisane JSON Web Token (JWT). base64Url może aplikacji Hello dekodowania hello segmenty tokenu toorequest informacje o hello użytkownik zalogowany. aplikacji Hello można buforować hello wartości i wyświetlić je, ale nie należy polegać na nich autoryzacji lub granic zabezpieczeń.  Aby uzyskać więcej informacji na temat id_tokens Zobacz hello [odwołania do tokenu punktu końcowego v2.0](active-directory-v2-tokens.md). |

#### Odpowiedzi na błąd
Błąd odpowiedzi będą wyglądać jak:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Ciąg kodu błędu mogą być używane tooclassify typów błędów występujących, która może być używana tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |
| error_codes |Listę kodów błędu STS, które mogą pomóc w diagnostyce. |
| sygnatura czasowa |czas Hello, w którym wystąpił błąd hello. |
| trace_id |Unikatowy identyfikator dla żądania hello, które mogą pomóc w diagnostyce. |
| correlation_id |Unikatowy identyfikator dla żądania hello, które mogą pomóc w diagnostyce między składnikami. |

#### Kody błędów dla punktu końcowego tokena błędów
| Kod błędu: | Opis | Akcja klienta |
| --- | --- | --- |
| invalid_request |Błąd protokołu, takie jak brak wymaganego parametru. |Usuń i ponownie prześlij żądanie hello |
| invalid_grant |Kod autoryzacji Hello jest nieprawidłowa lub wygasła. |Spróbuj nowe toohello żądania `/authorize` punktu końcowego |
| unauthorized_client |Witaj uwierzytelniany klient nie ma uprawnień toouse udzielić autoryzacji tego typu. |Zazwyczaj dzieje się tak, gdy aplikacja kliencka hello nie jest zarejestrowany w usłudze Azure AD lub dzierżawy usługi Azure AD toohello użytkownika nie została dodana. aplikacji Hello można monitować użytkownika hello z instrukcji dotyczących instalowania aplikacji hello i dodanie go tooAzure AD. |
| invalid_client |Uwierzytelnianie klienta nie powiodło się. |powitania klienta poświadczenia są nieprawidłowe. toofix, administrator aplikacji hello aktualizuje hello poświadczeń. |
| unsupported_grant_type |powitania serwera autoryzacji nie obsługuje typ przydziału hello autoryzacji. |Zmień hello przyznać typu w żądaniu hello. Tego typu błędu powinien wystąpić tylko podczas programowania i być wykryte podczas testowania początkowej. |
| invalid_resource |zasób docelowy Hello jest nieprawidłowy, ponieważ nie istnieje, nie można znaleźć usługi Azure AD lub nie została poprawnie skonfigurowana. |Oznacza to, że hello zasobu, jeśli istnieje, nie został skonfigurowany w dzierżawie powitalnych. aplikacji Hello można monitować użytkownika hello z instrukcji dotyczących instalowania aplikacji hello i dodanie go tooAzure AD. |
| interaction_required |Żądanie hello wymaga interakcji użytkownika. Na przykład krok dodatkowego uwierzytelniania jest wymagany. |Ponów żądanie hello z hello tego samego zasobu. |
| temporarily_unavailable |Serwer Hello tymczasowo jest zbyt zajęty toohandle hello żądania. |Ponów żądanie hello. Aplikacja kliencka Hello może wyjaśnić toohello użytkownika czy odpowiedzi jest opóźniony ze względu na tymczasowy warunek. |

## Użyj tokenu dostępu hello
Teraz, zostały pomyślnie uzyskano `access_token`, hello token w tooWeb żądań interfejsów API służy przez dołączenie go do hello `Authorization` nagłówka:

> [!TIP]
> Wykonanie tego żądania w Postman! (Zastąp hello `Authorization` nagłówek pierwszego) [ ![uruchamiane w Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## Odśwież hello token dostępu
Access_tokens są krótkie żyła i należy je odświeżyć, po wygasną toocontinue uzyskiwania dostępu do zasobów.  Możesz to zrobić poprzez przesłanie innego `POST` żądania toohello `/token` punktu końcowego, zapewniając hello teraz `refresh_token` zamiast hello `code`:

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
> Spróbuj wykonywania tego żądania w Postman! (Nie zapomnij tooreplace hello `refresh_token`) [ ![uruchamiane w Postman](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Witaj `{tenant}` wartość w ścieżce hello hello żądania mogą być używane toocontrol, który można zalogować się do aplikacji hello.  Witaj dozwolone wartości to `common`, `organizations`, `consumers`i dzierżawców identyfikatorów.  Aby uzyskać więcej szczegółów, zobacz [protokołu podstawy](active-directory-v2-protocols.md#endpoints). |
| client_id |Wymagane |Identyfikator aplikacji tego portalu rejestracji hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) przypisany do aplikacji. |
| Typ grant_type |Wymagane |Musi być `refresh_token` dla ten etap przepływu kodu autoryzacji hello. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów.  zakresy Hello żądanie, w tym etap należy równoważne tooor podzbiór zakresów hello wystąpić w hello oryginalnego authorization_code żądania etap.  Jeśli określony w żądaniu zakresy hello obejmują wiele zasobów serwerów, punktu końcowego v2.0 hello zwróci token dla zasobu hello określone w zakresie pierwszy hello.  Aby uzyskać bardziej szczegółowy opis zakresów można znaleźć za[uprawnień, zgody i zakresy](active-directory-v2-scopes.md). |
| refresh_token |Wymagane |Witaj refresh_token uzyskanego w drugi etap hello hello przepływu. |
| redirect_uri |Wymagane |Witaj tę samą wartość redirect_uri, która była używana tooacquire hello authorization_code. |
| client_secret |wymagane dla aplikacji sieci web |Witaj klucz tajny aplikacji utworzonej w portalu rejestracji aplikacji hello dla aplikacji.  Nie należy można użyć w natywnej aplikacji, ponieważ client_secrets nie może być niezawodnie przechowywanych na urządzeniach.  Jest wymagane dla aplikacji sieci web i interfejsów API, która ma hello możliwości toostore hello client_secret bezpiecznie na powitania po stronie serwera sieci web. |

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
| ' access_token ' |token dostępu do żądanego Hello. Aplikacja Hello można użyć tego toohello tokenu tooauthenticate zabezpieczonych zasobów, takich jak interfejsu API sieci web. |
| token_type |Wskazuje wartość tokenu typu hello. Witaj tylko typ, który obsługuje usługę Azure AD jest elementu nośnego |
| expires_in |Jak długo hello token dostępu jest nieprawidłowy (w sekundach). |
| Zakres |nadaje się do zakresów Hello hello ' access_token '. |
| refresh_token |Nowy token odświeżania OAuth 2.0. Należy zastąpić starego odświeżania hello tokenu z tym tooensure token odświeżania nowo pobranych tokenów odświeżania ważność tak długo, jak to możliwe. |
| żądaniu |Niepodpisane JSON Web Token (JWT). base64Url może aplikacji Hello dekodowania hello segmenty tokenu toorequest informacje o hello użytkownik zalogowany. aplikacji Hello można buforować hello wartości i wyświetlić je, ale nie należy polegać na nich autoryzacji lub granic zabezpieczeń.  Aby uzyskać więcej informacji na temat id_tokens Zobacz hello [odwołania do tokenu punktu końcowego v2.0](active-directory-v2-tokens.md). |

#### Odpowiedzi na błąd
```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Ciąg kodu błędu mogą być używane tooclassify typów błędów występujących, która może być używana tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |
| error_codes |Listę kodów błędu STS, które mogą pomóc w diagnostyce. |
| sygnatura czasowa |czas Hello, w którym wystąpił błąd hello. |
| trace_id |Unikatowy identyfikator dla żądania hello, które mogą pomóc w diagnostyce. |
| correlation_id |Unikatowy identyfikator dla żądania hello, które mogą pomóc w diagnostyce między składnikami. |

Opis i kody błędów hello hello zalecana Akcja klienta, zobacz [kody błędów dla błędów punktu końcowego tokena](#error-codes-for-token-endpoint-errors).

