---
title: "aplikacje jednej strony aaaSecure przy użyciu niejawnego przepływu v2.0 hello Azure AD | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji sieci web przy użyciu usługi Azure AD w wersji 2.0 implementacji przepływu niejawnego powitania dla aplikacji jednej strony."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 3605931f-dc24-4910-bb50-5375defec6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 2cdce4eee88be4af54966d15204b79fa4992a58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Protokoły - źródła przy użyciu niejawnego przepływu hello w wersji 2.0
Z punktem końcowym v2.0 hello należy zalogować się użytkowników do aplikacji jednej strony z konta osobiste oraz pracy/służbowego firmy Microsoft.  Jednej strony i inne aplikacje JavaScript Uruchom głównie w przypadku krój przeglądarki kilka interesujące będzie wymagał kiedy pochodzi tooauthentication:

* właściwości zabezpieczeń Hello te aplikacje są znacznie różni się od tradycyjnych serwera aplikacji sieci web.
* Wiele serwerów autoryzacji & dostawców tożsamości nie obsługują żądania CORS.
* Przekierowania przeglądarki całą stronę od aplikacji hello stają się szczególnie inwazyjne toohello środowisko użytkownika.

W przypadku tych aplikacji (wziąć pod uwagę: AngularJS, Ember.js, React.js, itp.) usługi Azure AD obsługuje hello przepływ udzielania niejawne OAuth 2.0.  przepływu niejawnego Hello jest opisana w hello [OAuth 2.0 specyfikacji](http://tools.ietf.org/html/rfc6749#section-4.2).  Podstawowy korzyści jest możliwość tokenów tooget aplikacji hello z usługi Azure AD bez wykonywania wymiany poświadczeń serwera wewnętrznej bazy danych.  Dzięki temu toosign aplikacji hello w hello użytkownika, zachowania sesji i uzyskać tokeny tooother interfejsów API sieci web w kodu JavaScript powitania klienta.  Istnieje kilka tootake zagadnienia dotyczące zabezpieczeń ważne pod uwagę podczas przy użyciu niejawnego przepływu hello — w szczególności około [klienta](http://tools.ietf.org/html/rfc6749#section-10.3) i [personifikacji użytkownika](http://tools.ietf.org/html/rfc6749#section-10.3).

Jeśli chcesz toouse hello niejawnego przepływu i aplikacji usługi Azure AD tooadd uwierzytelniania tooyour JavaScript, zalecane jest użycie nasza Biblioteka JavaScript typu open source [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js).  Istnieje kilka samouczki AngularJS [tutaj](active-directory-appmodel-v2-overview.md#getting-started) toohelp rozpocząć pracę.  

Jednak jeśli chcesz toouse biblioteki w wiadomości protokołu aplikacji i wysyłania jednej strony samodzielnie, wykonaj hello ogólne kroki.

> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.  toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

## Diagram protokołu
Hello całego niejawne logowania przepływu wygląda następująco — każdy hello kroki zostały szczegółowo opisane w poniższej.

![OpenId Connect ścieżek](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## Wysyłanie żądania logowania hello
znak tooinitially hello użytkownika w aplikacji, możesz wysłać [OpenID Connect](active-directory-v2-protocols-oidc.md) żądania autoryzacji i get `id_token` z punktu końcowego v2.0 hello:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&response_mode=fragment
&state=12345
&nonce=678910
```

> [!TIP]
> Kliknij łącze hello poniżej tooexecute tego żądania. Po zalogowaniu, przeglądarka powinno nastąpić przekierowanie zbyt`https://localhost/myapp/` z `id_token` na pasku adresu hello.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token+token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/Authorize...</a>
> 
> 

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Witaj `{tenant}` wartość w ścieżce hello hello żądania mogą być używane toocontrol, który można zalogować się do aplikacji hello.  Witaj dozwolone wartości to `common`, `organizations`, `consumers`i dzierżawców identyfikatorów.  Aby uzyskać więcej szczegółów, zobacz [protokołu podstawy](active-directory-v2-protocols.md#endpoints). |
| client_id |Wymagane |Identyfikator aplikacji tego portalu rejestracji hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) przypisany do aplikacji. |
| response_type |Wymagane |Musi zawierać `id_token` OpenID Connect logowaniu.  Mogą również obejmować hello response_type `token`. Przy użyciu `token` tutaj umożliwi Twojej tooreceive app token dostępu bezpośrednio z hello punktu końcowego autoryzacji bez konieczności toomake drugi toohello żądania autoryzacji punktu końcowego.  Jeśli używasz hello `token` response_type, hello `scope` parametr może zawierać wskazująca, których token hello tooissue zasobów dla zakresu. |
| redirect_uri |Zalecane |Witaj redirect_uri aplikacji, w którym można wysłanych i odebranych przez aplikację odpowiedzi uwierzytelniania.  Dokładnie musi odpowiadać jedną redirect_uris hello, który został zarejestrowany w portalu hello, z wyjątkiem musi być zakodowane w adresie url. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów.  Dla protokołu OpenID Connect, musi on zawierać zakres hello `openid`, co przekłada się uprawnienie "Logowanie się w" toohello w zgody hello interfejsu użytkownika.  Opcjonalnie można również tooinclude hello `email` lub `profile` [zakresy](active-directory-v2-scopes.md) do uzyskania danych użytkownika tooadditional dostępu.  Można również użyć innych zakresów w tym żądaniu żądanych zasobów toovarious zgody. |
| response_mode |Zalecane |Określa metodę hello, który ma być używane toosend hello wynikowy tooyour tyłu tokenu aplikacji.  Powinien być `fragment` dla przepływu niejawnego hello. |
| state |Zalecane |Wartość zawarte w żądaniu hello, zwracana w hello odpowiedzi tokenu.  Można go ciągiem zawartość, która ma.  Losowo generowany unikatową wartość jest zazwyczaj używana w przypadku [zapobieganie fałszerstwie żądania międzywitrynowego](http://tools.ietf.org/html/rfc6749#section-10.12).  Stan Hello jest również używane tooencode informacji na temat stanu hello użytkownika w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takie jak strona hello lub widok, które były na. |
| Identyfikator jednorazowy |Wymagane |Wartość zawarte w żądaniu hello, generowane przez hello aplikacji, która zostanie uwzględniona w żądaniu wynikowy hello jako oświadczenia.  Aplikacja Hello następnie sprawdzić, czy ataki powtórzeń tokenów toomitigate wartość.  wartość Hello jest zwykle losowego, unikatowy ciąg, który może być używane tooidentify hello pochodzenia hello żądania. |
| wiersz |Opcjonalne |Wskazuje typ hello interakcji z użytkownikiem, który jest wymagany.  Witaj prawidłowe są tylko wartości w tym momencie "login", "none", "wyrazić zgodę".  `prompt=login`zostanie życie hello tooenter użytkownika poświadczeń w tym żądaniu Negacja jednokrotnego na.  `prompt=none`jest hello przeciwną - zapewnić nie zobaczy tego użytkownika hello jakiejkolwiek monitu interakcyjnego.  Jeśli nie można ukończyć żądania hello dyskretnie za pośrednictwem jednokrotnego, punktu końcowego v2.0 hello zwróci błąd.  `prompt=consent`wyzwalacz hello OAuth zgody okna dialogowego po hello użytkownik loguje, prosząc hello użytkownika toogrant uprawnienia toohello aplikacji. |
| login_hint |Opcjonalne |Można używane wypełnienia toopre hello nazwy użytkownika/poczta e-mail adres pola hello zalogować się Strona hello użytkownika, jeśli znasz swoją nazwę użytkownika wcześniejsze.  Aplikacje często użyje tego parametru podczas ponowne uwierzytelnianie hello username już o wyodrębnione z poprzednich logowanie przy użyciu hello `preferred_username` oświadczeń. |
| domain_hint |Opcjonalne |Może być jednym z `consumers` lub `organizations`.  Jeśli uwzględniona, pominie proces odnajdywania opartych na poczcie e-mail hello użytkownik przechodzi przez na stronie logowania v2.0 hello wiodące tooa wymaga nieco więcej usprawnić środowisko użytkownika.  Aplikacje często użyje tego parametru podczas ponownego uwierzytelniania, wyodrębniając hello `tid` oświadczeń z hello żądaniu.  Jeśli hello `tid` oświadczeń, wartość jest `9188040d-6c67-4c5b-b112-36a304b66dad`, należy użyć `domain_hint=consumers`.  W przeciwnym razie użyj `domain_hint=organizations`. |

W tym momencie hello użytkownik będzie zadawane tooenter ich poświadczeń i uwierzytelniania hello ukończone.  Witaj punktu końcowego v2.0 zapewni hello użytkownik zgodził uprawnienia toohello wskazane hello `scope` parametr zapytania.  Jeśli hello użytkownik zgodził nie tooany tych uprawnień, jego poprosi tooconsent użytkownika hello toohello wymagane uprawnienia.  Szczegóły [uprawnień, zgody i aplikacje wielodostępne znajdują się w tym miejscu](active-directory-v2-scopes.md).

Po hello użytkownik jest uwierzytelniany i udziela zgody, punktu końcowego v2.0 hello zwróci aplikacji tooyour odpowiedzi w momencie hello wskazanych `redirect_uri`, przy użyciu metody hello określonej w hello `response_mode` parametru.

#### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie przy użyciu `response_mode=fragment` i `response_type=id_token+token` wygląda podobnie do następujących hello, podziały wiersza dla czytelności:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope=https%3a%2f%2fgraph.microsoft.com%2fmail.read 
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
```

| Parametr | Opis |
| --- | --- |
| ' access_token ' |Jeśli uwzględniona `response_type` obejmuje `token`. token dostępu Hello hello aplikacji żądanie, w tym przypadku dla hello Microsoft Graph.  token dostępu Hello nie powinna być zdekodować lub inaczej sprawdzić, może być traktowana jako ciąg z ogólnym opisem. |
| token_type |Jeśli uwzględniona `response_type` obejmuje `token`.  Zawsze będzie `Bearer`. |
| expires_in |Jeśli uwzględniona `response_type` obejmuje `token`.  Wskazuje hello liczbę sekund, przez które hello token jest prawidłowy na potrzeby buforowania. |
| Zakres |Jeśli uwzględniona `response_type` obejmuje `token`.  Wskazuje zakresy hello, dla których hello ' access_token ' będzie poprawna. |
| żądaniu |Witaj żądaniu, który hello żądanej aplikacji. Można użyć hello żądaniu tooverify hello tożsamości użytkownika i rozpocząć sesję użytkownika hello.  Więcej informacji na temat id_tokens i ich zawartość znajduje się w hello [odwołania do tokenu punktu końcowego v2.0](active-directory-v2-tokens.md). |
| state |Jeśli parametr Stan jest uwzględniony w żądaniu hello, hello tej samej wartości powinny być wyświetlane w hello odpowiedzi. Aplikacja Hello sprawdzić, czy wartości stanu hello hello żądań i odpowiedzi są identyczne. |

#### Odpowiedzi na błąd
Odpowiedzi na błędy mogą być również wysyłane toohello `redirect_uri` dzięki aplikacji hello można je odpowiednią obsługę:

```
GET https://localhost/myapp/#
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu mogą być używane tooclassify typów błędów występujących, która może być używana tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |

## Sprawdź poprawność żądaniu hello
Tylko odbieranie żądaniu nie jest wystarczające użytkownika hello tooauthenticate; musi sprawdzić poprawności podpisu żądaniu hello i sprawdź hello oświadczenia w tokenie hello na wymagania dotyczące Twojej aplikacji.  korzysta z punktu końcowego v2.0 Hello [tokenów sieci Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) i publicznego klucza szyfrowania tokenów toosign i sprawdź, czy są prawidłowe.

Możesz wybrać toovalidate hello `id_token` w kodzie klienta, ale toosend hello jest typowym rozwiązaniem `id_token` tooa serwera wewnętrznej bazy danych i sprawdzania poprawności hello istnieje.  Po upewnieniu się hello podpis żądaniu hello, istnieje kilka oświadczenia będą wymagane tooverify.  Zobacz hello [odwołania do tokenu v2.0](active-directory-v2-tokens.md) uzyskać więcej informacji, łącznie z [sprawdzania poprawności tokenów](active-directory-v2-tokens.md#validating-tokens) i [ważne informacje dotyczące podpisywania klucza przerzucania](active-directory-v2-tokens.md#validating-tokens).  Firma Microsoft zaleca korzystające z biblioteki do analizowania i weryfikowania tokenów — Brak co najmniej jeden dostępny dla większości języków i platform.
<!--TODO: Improve hello information on this-->

Możesz również toovalidate dodatkowe oświadczeń w zależności od danego scenariusza.  Niektóre typowe operacje sprawdzania poprawności obejmują:

* Zapewnienie organizacja użytkownika powitania po zarejestrowaniu aplikacji hello.
* Zapewnienie hello użytkownika ma właściwe autoryzacji/uprawnienia
* Zapewnienie siły uwierzytelniania wystąpił, takich jak uwierzytelnianie wieloskładnikowe.

Aby uzyskać więcej informacji na oświadczeniach hello w żądaniu, zobacz hello [odwołania do tokenu punktu końcowego v2.0](active-directory-v2-tokens.md).

Po zweryfikowaniu całkowicie żądaniu hello, możesz rozpocząć sesję użytkownika hello i użyć oświadczeń hello w hello żądaniu tooobtain informacje o użytkowniku hello w aplikacji.  Te informacje można służyć do wyświetlania rekordów, autoryzacje itp.

## Pobieranie tokenów dostępu
Teraz, kiedy się zalogowano użytkownika hello aplikacji jednej strony, możesz też uzyskać tokenów dostępu do sieci web wywoływania interfejsów API zabezpieczone przez usługę Azure AD, takie jak hello [Microsoft Graph](https://graph.microsoft.io).  Nawet jeśli otrzymany tokenu przy użyciu hello `token` response_type, można użyć tej metody tooacquire tokenów tooadditional zasobów bez konieczności tooredirect hello użytkownika toosign ponownie.

W normalnym przepływie OpenID Connect/OAuth hello, można to zrobić poprzez v2.0 toohello żądania `/token` punktu końcowego.  Jednak punktu końcowego v2.0 hello nie nie żądań CORPS pomocy technicznej, co AJAX wywołuje tooget i tokenów odświeżania jest poza hello pytanie.  Zamiast tego można użyć przepływu niejawnego hello w tooget ukryte iframe nowe tokeny dla innych interfejsów API sieci web: 

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment
&state=12345&nonce=678910
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
```

> [!TIP]
> Spróbuj wykonać kopiowanie i wklejanie hello poniżej żądania do karty przeglądarki! (Nie zapomnij tooreplace hello `domain_hint` i hello `login_hint` wartości z hello Popraw wartości dla użytkownika)
> 
> 

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910&prompt=none&domain_hint={{consumers-or-organizations}}&login_hint={{your-username}}
```

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Witaj `{tenant}` wartość w ścieżce hello hello żądania mogą być używane toocontrol, który można zalogować się do aplikacji hello.  Witaj dozwolone wartości to `common`, `organizations`, `consumers`i dzierżawców identyfikatorów.  Aby uzyskać więcej szczegółów, zobacz [protokołu podstawy](active-directory-v2-protocols.md#endpoints). |
| client_id |Wymagane |Identyfikator aplikacji tego portalu rejestracji hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) przypisany do aplikacji. |
| response_type |Wymagane |Musi zawierać `id_token` OpenID Connect logowaniu.  Może również obejmować innych response_types, takich jak `code`. |
| redirect_uri |Zalecane |Witaj redirect_uri aplikacji, w którym można wysłanych i odebranych przez aplikację odpowiedzi uwierzytelniania.  Dokładnie musi odpowiadać jedną redirect_uris hello, który został zarejestrowany w portalu hello, z wyjątkiem musi być zakodowane w adresie url. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów.  Uzyskiwania tokenów, Uwzględnij wszystkie [zakresy](active-directory-v2-scopes.md) wymagają dla zasobu hello zainteresowań. |
| response_mode |Zalecane |Określa metodę hello, który ma być używane toosend hello wynikowy tooyour tyłu tokenu aplikacji.  Może być jednym z `query`, `form_post`, lub `fragment`. |
| state |Zalecane |Wartość zawarte w żądaniu hello, zwracana w hello odpowiedzi tokenu.  Można go ciągiem zawartość, która ma.  Losowo generowany unikatową wartość jest zwykle używany zapobiegania fałszerstwie żądania międzywitrynowego.  Stan Hello jest również używane tooencode informacji na temat stanu hello użytkownika w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takie jak strona hello lub widok, które były na. |
| Identyfikator jednorazowy |Wymagane |Wartość zawarte w żądaniu hello, generowane przez hello aplikacji, która zostanie uwzględniona w żądaniu wynikowy hello jako oświadczenia.  Aplikacja Hello następnie sprawdzić, czy ataki powtórzeń tokenów toomitigate wartość.  wartość Hello jest zwykle losowego, unikatowy ciąg, który może być używane tooidentify hello pochodzenia hello żądania. |
| wiersz |Wymagane |Aby odświeżyć & uzyskiwania tokenów w ukrytym iframe, należy użyć `prompt=none` tooensure, który hello iframe nie zostać zawieszone na stronę logowania w wersji 2.0 hello i zwraca natychmiast. |
| login_hint |Wymagane |Odświeżanie i uzyskiwania tokenów w ukrytym iframe, musi zawierać nazwy użytkownika hello hello użytkownika w tym warunku w kolejności toodistinguish między wiele sesji, która hello użytkownika może znajdować się w danym punkcie w czasie. Można wyodrębnić hello username z poprzednich logowanie przy użyciu hello `preferred_username` oświadczeń. |
| domain_hint |Wymagane |Może być jednym z `consumers` lub `organizations`.  Odświeżanie i uzyskiwania tokenów w ukrytym iframe, musi zawierać hello domain_hint w żądaniu hello.  Należy wyodrębnić hello `tid` oświadczeń w żądaniu hello z poprzednich toodetermine logowania które toouse wartość.  Jeśli hello `tid` oświadczeń, wartość jest `9188040d-6c67-4c5b-b112-36a304b66dad`, należy użyć `domain_hint=consumers`.  W przeciwnym razie użyj `domain_hint=organizations`. |

Dziękujemy toohello `prompt=none` , tego żądania zostanie albo powiedzie się albo natychmiast zakończyć się niepowodzeniem i zwracać tooyour aplikacji.  Odpowiedź oznaczająca Powodzenie będą wysyłane tooyour aplikacji na wskazanych hello `redirect_uri`, przy użyciu metody hello określonej w hello `response_mode` parametru.

#### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie przy użyciu `response_mode=fragment` wygląda jak:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read
```

| Parametr | Opis |
| --- | --- |
| ' access_token ' |Witaj token, aplikacja hello żądanie. |
| token_type |Zawsze będzie `Bearer`. |
| state |Jeśli parametr Stan jest uwzględniony w żądaniu hello, hello tej samej wartości powinny być wyświetlane w hello odpowiedzi. Aplikacja Hello sprawdzić, czy wartości stanu hello hello żądań i odpowiedzi są identyczne. |
| expires_in |Jak długo hello token dostępu jest nieprawidłowy (w sekundach). |
| Zakres |nadaje się do zakresów Hello hello tokenu dostępu. |

#### Odpowiedzi na błąd
Odpowiedzi na błędy mogą być również wysyłane toohello `redirect_uri` dzięki aplikacji hello można je odpowiednią obsługę.  W przypadku hello `prompt=none`, będzie oczekiwany błąd:

```
GET https://localhost/myapp/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu mogą być używane tooclassify typów błędów występujących, która może być używana tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |

Jeśli ten błąd jest wyświetlany w żądaniu iframe hello, hello użytkownika interakcyjnie zalogować ponownie tooretrieve nowy token.  Można wybrać toohandle tego przypadku w dowolnie wybrany sposób sens dla aplikacji.

## Odświeżanie tokenów
Zarówno `id_token`s i `access_token`s wygaśnie po krótkim czasie, więc aplikacji muszą być przygotowane toorefresh tokeny są okresowo.  toorefresh albo typ tokenu, można wykonywać hello jednym żądaniu ukryte iframe powyższego przy użyciu hello `prompt=none` parametru zachowanie toocontrol usługi Azure AD.  Jeśli chcesz, aby tooreceive nowy `id_token`, toouse się, że można `response_type=id_token` i `scope=openid`, a także `nonce` parametru.

## Wyślij żądanie logowania
Witaj OpenIdConnect `end_session_endpoint` umożliwia żądania toohello v2.0 punktu końcowego tooend sesji i wyczyść pliki cookie użytkownika ustawione przez punktu końcowego v2.0 hello toosend Twojej aplikacji.  toofully zalogować użytkownika poza aplikacją sieci web, aplikacji należy zakończyć sesję użytkownika hello (zwykle przez wyczyszczenie pamięci podręcznej tokenu lub usunięcie plików cookie) i przekierowanie przeglądarki hello:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/logout?post_logout_redirect_uri=https://localhost/myapp/
```

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Witaj `{tenant}` wartość w ścieżce hello hello żądania mogą być używane toocontrol, który można zalogować się do aplikacji hello.  Witaj dozwolone wartości to `common`, `organizations`, `consumers`i dzierżawców identyfikatorów.  Aby uzyskać więcej szczegółów, zobacz [protokołu podstawy](active-directory-v2-protocols.md#endpoints). |
| post_logout_redirect_uri | Zalecane | adres URL Hello hello użytkownika powinien być zwracany zakończeniu tooafter wylogowania. Ta wartość musi pasować hello przekierowania aplikacji hello zarejestrowane identyfikatory URI. Jeśli nie zostanie uwzględniony, hello zostanie wyświetlony komunikat ogólny przez hello punktu końcowego v2.0. |
