---
title: "aaaUse usługi Azure AD w wersji 2.0 tooaccess zabezpieczenia zasobów bez interakcji z użytkownikiem | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji sieci web przy użyciu usługi Azure AD hello implementacji protokołu uwierzytelniania hello OAuth 2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9b7cfbd7-f89f-4e33-aff2-414edd584b07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 0003ec836d633a5466c48033adedac1108f27203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Przepływ usługi Azure Active Directory w wersji 2.0 i hello OAuth 2.0 poświadczeń klienta
Można użyć hello [przyznania poświadczeń klienta OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.4), nazywane czasem *bokami dwa OAuth*, tooaccess zasobów hostowanych w sieci web przy użyciu tożsamości hello aplikacji. Ten typ grant często służy do interakcji do serwera, które muszą zostać uruchomione w tle hello, bez natychmiastowego interakcji z użytkownikiem. Aplikacje tego typu są często określonego tooas *demony* lub *kont usługi*.

> [!NOTE]
> punktu końcowego v2.0 Hello nie obsługuje wszystkich scenariuszy Azure Active Directory i funkcji. toodetermine, czy należy używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
>
>

W bardziej typowego hello *bokami trzech OAuth*, aplikacja kliencka jest tooaccess uprawnienia nadanego zasobu w imieniu określonego użytkownika. delegowane uprawnienia Hello z hello aplikacji toohello użytkowników, zazwyczaj podczas hello [zgody](active-directory-v2-scopes.md) procesu. Jednak hello przepływu poświadczeń klienta, uprawnienia są przyznawane bezpośrednio toohello samej aplikacji. Gdy aplikacja hello Wyświetla zasobów token tooa, zasobów hello wymusza hello aplikacja ma tooperform autoryzacji działanie, czy użytkownik hello nie ma autoryzacji.

## Diagram protokołu
Przepływ poświadczeń klienta całego Hello wygląda podobnie toohello diagram dalej. Opisano każdy hello kroki opisane w dalszej części tego artykułu.

![Przepływ poświadczeń klienta](../../media/active-directory-v2-flows/convergence_scenarios_client_creds.png)

## Uzyskiwanie bezpośredniego autoryzacji
Zwykle aplikacja odbiera tooaccess bezpośredniego autoryzacji zasobu w jeden z dwóch sposobów: przez listy kontroli dostępu (ACL) na powitania zasobów, albo przez przypisanie uprawnień aplikacji w usłudze Azure Active Directory (Azure AD). Te dwie metody są hello najczęściej w usłudze Azure AD i firma Microsoft zaleca klientów i wykonać przepływ poświadczeń klienta hello zasobów. Zasób można wybrać tooauthorize swoich klientów w inny sposób, jednak. Każdy serwer zasobów można wybrać metodę hello, która ma sens hello większości jej stosowania.

### Listy kontroli dostępu
Dostawca zasobów może wymuszać wyboru autoryzacji na podstawie listy identyfikatorów aplikacji wie i nieograniczony dostęp do określonego poziomu. Gdy zasobów hello otrzymała token od punktu końcowego v2.0 hello, można zdekodować hello token i wyodrębniania powitania klienta identyfikator aplikacji hello `appid` i `iss` oświadczeń. Następnie porównuje aplikacji hello względem listy kontroli dostępu, który przechowuje. Witaj szczegółowości listy kontroli dostępu i — metoda może się znacznie różnić między zasobami.

Typowe przypadek użycia jest toouse toorun ACL testów dla aplikacji sieci web lub interfejs API sieci Web. Witaj interfejsu API sieci Web może udzielić tylko podzbioru pełnych uprawnień tooa określonego klienta. testy na trasie toorun na powitania interfejsu API, Utwórz klienta testu, który uzyskuje tokeny od punktu końcowego v2.0 hello, a następnie wysyła je toohello interfejsu API. Witaj interfejsu API, a następnie hello sprawdza listy ACL dla hello testu identyfikator aplikacji klienta dla pełnego dostępu do całej funkcji toohello interfejsu API. Jeśli używasz tego rodzaju listy ACL, należy toovalidate nie tylko hello obiektu wywołującego `appid` wartość. Zweryfikować tego hello `iss` wartość tokenu hello jest zaufany.

Ten typ autoryzacji jest typowe dla demonów i kont usług, które wymagają tooaccess danych należących do użytkowników odbiorców, którzy mają osobistego konta Microsoft. Dla danych należących do organizacji firma Microsoft zaleca uzyskanie autoryzacji niezbędne hello za pośrednictwem uprawnienia aplikacji.

### Uprawnienia aplikacji
Zamiast przy użyciu list kontroli dostępu, możesz użyć interfejsów API tooexpose zestaw uprawnień aplikacji. Aplikacji uprawnienia aplikacji tooan przez administratora organizacji, a właścicielem może być używane tylko tooaccess danych organizacji i jej pracowników. Na przykład program Microsoft Graph udostępnia kilka następujących hello toodo uprawnienia aplikacji:

* Odczytuj pocztę we wszystkich skrzynkach pocztowych
* Odczytuj i zapisuj wiadomości e-mail we wszystkich skrzynkach pocztowych
* Wysyłaj wiadomości e-mail jako dowolny użytkownik
* Odczyt danych katalogu

Aby uzyskać więcej informacji na temat uprawnień aplikacji przejdź zbyt[Microsoft Graph](https://graph.microsoft.io).

uprawnienia aplikacji toouse w Twojej aplikacji hello czynności, które omówiono w kolejnych sekcjach hello.

#### Żądanie uprawnienia hello w portalu rejestracji aplikacji hello
1. Przejdź tooyour aplikacji hello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub [Utwórz aplikację](active-directory-v2-app-registration.md), jeśli nie jest jeszcze. Będziesz potrzebować toouse co najmniej jeden klucz tajny aplikacji podczas tworzenia aplikacji.
2. Zlokalizuj hello **bezpośrednie uprawnienia aplikacji** sekcji, a następnie dodaj hello uprawnienia, które wymaga aplikacji.
3. **Zapisz** hello rejestracji aplikacji.

#### Zalecane: Znak hello użytkownika w aplikacji tooyour
Zazwyczaj podczas tworzenia aplikacji, która używa uprawnienia aplikacji hello aplikacja wymaga strony lub widok, w którym hello admin zatwierdzi uprawnienia aplikacji hello. Ta strona może być częścią aplikacji hello logowania przepływu, część ustawień aplikacji hello, lub może być dedykowany "Połącz" przepływu. W wielu przypadkach warto dla tooshow aplikacji hello to "Połącz" Wyświetl tylko wtedy, gdy użytkownik jest zalogowany za pomocą służbowego konta Microsoft.

Jeśli zarejestrujesz hello użytkownika w aplikacji tooyour można zidentyfikować hello organizacji użytkownika hello toowhich należy przed skontaktowaniem się tooapprove użytkownika hello uprawnienia aplikacji hello. Chociaż nie niezbędne, ułatwia tworzenie bardziej intuicyjne środowisko dla użytkowników. toosign hello użytkownika w wykonaj naszych [samouczki protocol w wersji 2.0](active-directory-v2-protocols.md).

#### Żądanie uprawnienia powitania od administratora katalogu
Jeśli wszystko jest gotowe toorequest uprawnień z administratorem organizacji hello, można przekierowywać hello użytkownika toohello v2.0 *punktu końcowego zgody administratora*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello following request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Parametr | Warunek | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Dzierżawca katalogu Hello ma toorequest zgody. Może to być w formacie przyjaznej nazwy lub identyfikatora GUID. Jeśli nie wiadomo, które użytkownik hello dzierżawy należy tooand ma toolet ich Zaloguj się przy użyciu dowolnej dzierżawy, użyj `common`. |
| client_id |Wymagane |hello tego IDENTYFIKATORA aplikacji Hello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) przypisane tooyour aplikacji. |
| redirect_uri |Wymagane |Witaj przekierowania URI miejscu hello toobe odpowiedzi wysłanych toohandle Twojej aplikacji. Go musi dokładnie odpowiadać jeden hello przekierowania URI, który został zarejestrowany w portalu hello z tą różnicą, że musi być zakodowane w adresie URL, i może mieć segmenty ścieżki dodatkowe. |
| state |Zalecane |Wartość, która znajduje się w żądaniu hello, który jest także zwracany w odpowiedzi tokenu hello. Można go ciąg ma zawartość. Stan Hello jest używany tooencode informacji na temat stanu hello użytkownika w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takich jak strony hello lub widoku, które znajdowały się w. |

W tym momencie usługi Azure AD wymusza, czy administrator dzierżawy może zalogować się toocomplete hello żądania. Hello administrator zapyta tooapprove hello wszystkie uprawnienia bezpośredniego aplikacji, które żądanej aplikacji w portalu rejestracji aplikacji hello.

##### Odpowiedź oznaczająca Powodzenie
Jeśli Witaj, Administratorze zatwierdza hello uprawnienia dla aplikacji, odpowiedź oznaczająca Powodzenie hello wygląda następująco:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Parametr | Opis |
| --- | --- | --- |
| Dzierżawy |Hello katalogu dzierżawy, którym przyznano uprawnienia aplikacji hello, który żądał, w formacie GUID. |
| state |Wartość, która znajduje się w żądaniu hello, który jest także zwracany w odpowiedzi tokenu hello. Można go ciąg ma zawartość. Stan Hello jest używany tooencode informacji na temat stanu hello użytkownika w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takich jak strony hello lub widoku, które znajdowały się w. |
| admin_consent |Ustaw zbyt**true**. |

##### Odpowiedzi na błąd
Witaj, Administratorze nie zatwierdzenia hello uprawnienia dla aplikacji, hello nie powiodła się odpowiedzi wygląda następująco:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Parametr | Opis |
| --- | --- | --- |
| error |Ciąg kodu błędu, których można używać typów tooclassify błędów i której można użyć tooreact tooerrors. |
| error_description |Komunikat o błędzie, który ułatwia identyfikowanie hello główną przyczynę błędu. |

Po otrzymaniu pomyślnej odpowiedzi z inicjowania obsługi administracyjnej punktu końcowego aplikacji hello, aplikację zyskały hello bezpośredniego stosowania uprawnienia, które go żądanie. Teraz można żądać tokenu hello zasobu, który ma.

## Uzyskaj token
Po zostały nabyte hello niezbędne autoryzacji dla aplikacji, kontynuuj pobieranie tokenów dostępu do interfejsów API. tooget tokenu przy użyciu przyznania poświadczeń klienta hello, Wyślij toohello żądania POST `/token` punktu końcowego v2.0:

### Najpierw przypadek: żądanie tokenu dostępu z wspólny klucz tajny

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials
```

```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials' 'https://login.microsoftonline.com/common/oauth2/v2.0/token'
```

| Parametr | Warunek | Opis |
| --- | --- | --- |
| client_id |Wymagane |hello tego IDENTYFIKATORA aplikacji Hello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) przypisane tooyour aplikacji. |
| Zakres |Wymagane |wartość Hello przekazana do hello `scope` parametr w tym żądaniu powinien być hello zasobów identyfikator aplikacji identyfikator URI zasobu hello ma, umieszczone z hello `.default` sufiks. Na przykład program Microsoft Graph hello wartość hello jest `https://graph.microsoft.com/.default`. Ta wartość informuje punktu końcowego v2.0 hello, czy wszystkie hello bezpośredniego stosowania uprawnień, które zostały skonfigurowane dla aplikacji, jego powinien wystawiać token dla hello skojarzone z żądanego zasobu hello toouse. |
| client_secret |Wymagane |klucz tajny aplikacji, generowany dla aplikacji w portalu rejestracji aplikacji hello Hello. |
| Typ grant_type |Wymagane |Musi być `client_credentials`. |

### W drugim przypadku: żądanie tokenu dostępu przy użyciu certyfikatu

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

| Parametr | Warunek | Opis |
| --- | --- | --- |
| client_id |Wymagane |hello tego IDENTYFIKATORA aplikacji Hello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) przypisane tooyour aplikacji. |
| Zakres |Wymagane |wartość Hello przekazana do hello `scope` parametr w tym żądaniu powinien być hello zasobów identyfikator aplikacji identyfikator URI zasobu hello ma, umieszczone z hello `.default` sufiks. Na przykład program Microsoft Graph hello wartość hello jest `https://graph.microsoft.com/.default`. Ta wartość informuje punktu końcowego v2.0 hello, czy wszystkie hello bezpośredniego stosowania uprawnień, które zostały skonfigurowane dla aplikacji, jego powinien wystawiać token dla hello skojarzone z żądanego zasobu hello toouse. |
| client_assertion_type |Wymagane |Witaj, wartość musi być`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Wymagane | Potwierdzeniem (JSON Web Token) czy potrzebujesz toocreate oraz znak hello certyfikatu można zarejestrowany jako poświadczeń dla aplikacji. Przeczytaj informacje o [certyfikatu poświadczeń](active-directory-certificate-credentials.md) toolearn jak tooregister Twojego certyfikatu i hello format hello potwierdzenia.|
| Typ grant_type |Wymagane |Musi być `client_credentials`. |

Należy zauważyć, że parametry hello są prawie hello takie same jak przypadku hello hello żądania przez Wspólny klucz tajny z tą różnicą, że parametr client_secret hello zostało zastąpione przez dwa parametry: client_assertion_type i client_assertion.

### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie wygląda następująco:

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

| Parametr | Opis |
| --- | --- |
| ' access_token ' |token dostępu do żądanego Hello. Aplikacja Hello można użyć tego toohello tokenu tooauthenticate zabezpieczonych zasobów, takich jak tooa interfejsu API sieci Web. |
| token_type |Wskazuje wartość tokenu typu hello. Witaj tylko typ, który obsługuje usługę Azure AD `bearer`. |
| expires_in |Jak długo hello token dostępu jest nieprawidłowy (w sekundach). |

### Odpowiedzi na błąd
Odpowiedzi na błąd wygląda następująco:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/.default is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Ciąg kodu błędu, który można używać typów tooclassify o błędach i tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić identyfikację hello głównej przyczyny błędu uwierzytelniania. |
| error_codes |Lista specyficzne dla usługi STS kody błędów, które mogą ułatwić rozwiązanie diagnostyki. |
| sygnatura czasowa |czas Hello, w którym wystąpił błąd hello. |
| trace_id |Unikatowy identyfikator dla żądania hello, które mogą ułatwić rozwiązanie diagnostyki. |
| correlation_id |Unikatowy identyfikator dla żądania hello, które mogą pomóc w diagnostyce między składnikami. |

## Użyj tokenu
Teraz, gdy zostały nabyte token, należy użyć hello token toomake żądania toohello zasobu. Po wygaśnięciu tokenu hello Powtórz hello żądania toohello `/token` tooacquire punktu końcowego tokenu dostępu świeże.

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

```
// Pro tip: Try hello following command! (Replace hello token with your own.)
```

```
curl -X GET -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q" 'https://graph.microsoft.com/v1.0/me/messages'
```

## Przykład kodu
toosee przykład aplikacji czy implementuje hello przyznania poświadczeń klienta przy użyciu hello punktu końcowego zgody administratora, zobacz nasze [przykładowy kod demon v2.0](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
