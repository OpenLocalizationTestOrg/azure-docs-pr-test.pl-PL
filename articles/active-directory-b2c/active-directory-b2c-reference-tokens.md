---
title: "Usługa Azure Active Directory B2C: Token odwołania | Dokumentacja firmy Microsoft"
description: "Witaj typy tokenów wystawionych w usłudze Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/17/2017
ms.author: dastrock
ms.openlocfilehash: 776bc88cc0308875ac6e576f19ac9edf50319d08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-token-reference"></a>Usługi Azure AD B2C: Odwołanie Token
Usługa Azure Active Directory B2C (Azure AD B2C) emituje kilka typów tokenów zabezpieczających w czasie przetwarzania każdego [przepływ uwierzytelniania](active-directory-b2c-apps.md). W tym dokumencie opisano hello format, właściwości zabezpieczeń i zawartości każdego typu tokenu.

## <a name="types-of-tokens"></a>Typy tokenów
Usługa Azure AD B2C obsługuje hello [protokół OAuth 2.0](active-directory-b2c-reference-protocols.md), korzystające z obu tokenów dostępu i tokenów odświeżania. Obsługuje ona również uwierzytelniania i logowania za pomocą [OpenID Connect](active-directory-b2c-reference-protocols.md), który został wprowadzony trzeci typ tokenu: token Identyfikatora hello. Każdy z tych tokenów jest reprezentowany jako tokenu elementu nośnego.

Token elementu nośnego jest token zabezpieczający lekkie, że przyznaje hello tooa dostępu "bearer" chronionych zasobów. elementu nośnego Hello jest każda strona, która może ona powodować hello tokenu. Usługi Azure AD muszą najpierw zostać uwierzytelnione strona przed może odbierać tokenu elementu nośnego. Jednak jeśli hello wymagane kroki nie są brane toosecure hello token w transmisji i przechowywania, może być przechwycony i używane przez niezamierzone strony. Niektóre tokeny zabezpieczające mają wbudowany mechanizm nieupoważnione uniemożliwia korzystania z nich, ale tokenów elementu nośnego nie mają ten mechanizm. Muszą one być transportowane w bezpiecznego kanału, takie jak zabezpieczeń warstwy transportu (HTTPS).

Jeśli token elementu nośnego, są przesyłane poza bezpiecznego kanału, strony złośliwych można używa tokenu hello tooacquire ataku man-in--middle i jego toogain nieautoryzowany dostęp tooa chronionych zasobów. Witaj, te same zasady zabezpieczeń mają zastosowanie, gdy tokenów elementu nośnego, są przechowywane lub w pamięci podręcznej do późniejszego użycia. Zawsze upewnij się, że aplikacja przesyła i przechowuje tokenów elementu nośnego w bezpieczny sposób.

Uwagi dodatkowe zabezpieczenia na tokenów elementu nośnego można znaleźć [RFC 6750 sekcji 5](http://tools.ietf.org/html/rfc6750).

Wiele z usługi Azure AD B2C wystawia tokeny hello są zaimplementowane jako tokenów sieci web JSON (Jwt). Token JWT jest compact, adres URL bezpiecznego sposób przekazywania informacji między dwiema stronami. Jwt zawierają informacje znane jako oświadczenia. Są potwierdzeniami informacji na temat elementów nośnych hello i podmiotu hello hello tokenu. oświadczenia Hello w Jwt są obiektami JSON, które kodowania i serializację do transmisji. Ponieważ hello Jwt wystawione przez usługi Azure AD B2C podpisany, ale nie są szyfrowane, możesz łatwo sprawdzić zawartość hello JWT toodebug go. Dostępnych jest kilka narzędzi który można to zrobić, w tym [calebb.net](http://calebb.net). Aby uzyskać więcej informacji na temat tokenów Jwt, można znaleźć zbyt[specyfikacje JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Tokeny Identyfikatora
Identyfikator tokenu jest formą token zabezpieczający, który odbiera aplikacji z usługi Azure AD B2C hello `authorize` i `token` punktów końcowych. Identyfikator tokeny są reprezentowane jako [Jwt](#types-of-tokens), i zawierają roszczenia, w której można tooidentify użytkowników w aplikacji. Gdy tokeny Identyfikatora drogą kupna z hello `authorize` punktu końcowego, są często używane toosign w aplikacjach tooweb użytkowników. Gdy tokeny Identyfikatora drogą kupna z hello `token` punktu końcowego, mogą być wysyłane w żądaniach HTTP podczas komunikacji między dwa składniki hello sama aplikacja lub usługa. Można użyć hello oświadczenia w tokenie identyfikator, zgodnie z własnymi potrzebami. Są często używane toodisplay konta informacje lub toomake decyzje dotyczące kontroli dostępu w aplikacji.  

Zalogowano tokeny Identyfikatora, ale obecnie nie są zaszyfrowane. Gdy aplikację lub interfejsu API odbiera token Identyfikatora, należy [sprawdzanie poprawności podpisu hello](#token-validation) tooprove, który hello tokenu jest autentyczny. Aplikację lub interfejsu API należy zweryfikować kilka oświadczeń w hello tooprove tokenu jest nieprawidłowy. W zależności od wymagań scenariusza hello, może się różnić oświadczeń hello zweryfikowany przez aplikację, ale aplikacji należy wykonać niektóre [typowych operacji sprawdzania poprawności oświadczeń](#token-validation) w każdym scenariuszu.

#### <a name="sample-id-token"></a>Przykładowy identyfikator token
```
// Line breaks for display purposes only

eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6IklkVG9rZW5TaWduaW5nS2V5Q29udGFpbmVyIn0.
eyJleHAiOjE0NDIzNjAwMzQsIm5iZiI6MTQ0MjM1NjQzNCwidmVyIjoiMS4wIiwiaXNzIjoiaHR0cHM6Ly9s
b2dpbi5taWNyb3NvZnRvbmxpbmUuY29tLzc3NTUyN2ZmLTlhMzctNDMwNy04YjNkLWNjMzExZjU4ZDkyNS92
Mi4wLyIsImFjciI6ImIyY18xX3NpZ25faW5fc3RvY2siLCJzdWIiOiJOb3Qgc3VwcG9ydGVkIGN1cnJlbnRs
eS4gVXNlIG9pZCBjbGFpbS4iLCJhdWQiOiI5MGMwZmU2My1iY2YyLTQ0ZDUtOGZiNy1iOGJiYzBiMjlkYzYi
LCJpYXQiOjE0NDIzNTY0MzQsImF1dGhfdGltZSI6MTQ0MjM1NjQzNCwiaWRwIjoiZmFjZWJvb2suY29tIn0.
h-uiKcrT882pSKUtWCpj-_3b3vPs3bOWsESAhPMrL-iIIacKc6_uZrWxaWvIYkLra5czBcGKWrYwrAC8ZvQe
DJWZ50WXQrZYODEW1OUwzaD_I1f1HE0c2uvaWdGXBpDEVdsD3ExKaFlKGjFR2V7F-fPThkVDdKmkUDQX3bVc
yyj2V2nlCQ9jd7aGnokTPfLfpOjuIrTsAdPcGpe5hfSEuwYDmqOJjGs9Jp1f-eSNEiCDQOaTBSvr479L5ptP
XWeQZyX2SypN05Rjr05bjZh3j70ZUimiocfJzjibeoDCaQTz907yAg91WYuFOrQxb-5BaUoR7K-O7vxr2M-_
CQhoFA

```

### <a name="access-tokens"></a>Tokeny dostępu
Token dostępu jest również formularza token zabezpieczający, który odbiera aplikacji z usługi Azure AD B2C hello `authorize` i `token` punktów końcowych. Tokeny dostępu są także przedstawione jako [Jwt](#types-of-tokens), i zawierają oświadczeń służy hello tooidentify przyznane uprawnienia tooyour interfejsów API. Tokeny dostępu są podpisane, ale obecnie nie są zaszyfrowane. Tokeny dostępu powinien być serwery dostępu do używanych tooprovide tooAPIs i zasobów. Dowiedz się więcej o tym, jak za[używaj tokenów dostępu](active-directory-b2c-access-tokens.md). 

Interfejs API odebrania tokenu dostępu, należy [sprawdzanie poprawności podpisu hello](#token-validation) tooprove, który hello tokenu jest autentyczny. Interfejs API należy zweryfikować kilka oświadczeń w hello tooprove tokenu jest nieprawidłowy. W zależności od wymagań scenariusza hello, może się różnić oświadczeń hello zweryfikowany przez aplikację, ale aplikacji należy wykonać niektóre [typowych operacji sprawdzania poprawności oświadczeń](#token-validation) w każdym scenariuszu.

### <a name="claims-in-id-and-access-tokens"></a>Oświadczenia w tokenach dostępu i identyfikator
Gdy używasz usługi Azure AD B2C, masz precyzyjną kontrolę nad zawartością hello z tokenów. Można skonfigurować [zasady](active-directory-b2c-reference-policies.md) toosend niektóre zestawy danych użytkownika w oświadczenia, które wymaga aplikacji dla operacji. Oświadczenia te mogą obejmować właściwości standardowych, takich jak hello użytkownika `displayName` i `emailAddress`. Mogą również obejmować [atrybuty użytkownika niestandardowego](active-directory-b2c-reference-custom-attr.md) zdefiniowanej w katalogu usługi B2C. Każdy identyfikator i dostęp do tokenu, który pojawi się zawiera zestaw oświadczeń związanych z zabezpieczeniami. Aplikacje można użyć tych oświadczeń toosecurely uwierzytelniania użytkowników i żądań.

Należy pamiętać, że hello oświadczenia w tokenach identyfikator nie są zwracane w określonej kolejności. Ponadto oświadczeń nowy może zostać wprowadzony w tokeny Identyfikatora, w dowolnym momencie. Aplikacji nie powinna zostać podzielona na miarę wprowadzania nowych oświadczeń. Poniżej przedstawiono hello oświadczeń oczekiwać tooexist w tokenach dostępu i identyfikator wystawione przez usługi Azure AD B2C. Wszelkie dodatkowe oświadczenia są określone przez zasady. Praktyki, spróbuj sprawdzania hello oświadczenia w tokenie identyfikator próbki hello przez wklejenie go do [calebb.net](http://calebb.net). Dalsze szczegóły można znaleźć w hello [OpenID Connect specyfikacji](http://openid.net/specs/openid-connect-core-1_0.html).

| Nazwa | Claim | Przykładowa wartość | Opis |
| --- | --- | --- | --- |
| Grupy odbiorców |`aud` |`90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6` |Oświadczenie odbiorców identyfikację hello przeznaczone odbiorcy tokenu hello. Dla usługi Azure AD B2C odbiorców hello jest identyfikator aplikacji dla danej aplikacji, co przypisane tooyour aplikacji w portalu rejestracji aplikacji hello. Aplikację należy sprawdzić tę wartość i odrzucić hello token, jeśli nie jest zgodny. |
| Wystawcy |`iss` |`https://login.microsoftonline.com/775527ff-9a37-4307-8b3d-cc311f58d925/v2.0/` |To oświadczenie identyfikuje hello usługi tokenu zabezpieczającego (STS) tworzy i zwraca hello token. Identyfikuje hello katalog usługi Azure AD, w których hello uwierzytelnienia użytkownika. Aplikację należy zweryfikować Witaj wystawca oświadczeń tooensure, który hello tokenu pochodzi z punktu końcowego v2.0 usługi Azure Active Directory hello. |
| wystawiony w |`iat` |`1438535543` |Oświadczenie to hello czasu, w których hello token został wystawiony, czas epoki. |
| czas wygaśnięcia |`exp` |`1438539443` |Witaj oświadczeń czas wygaśnięcia jest hello czasu, w których hello token staje się nieprawidłowy, w czasie epoki. Aplikację należy użyć tego oświadczenia tooverify hello ważności hello okres ważności tokenu. |
| nie wcześniej niż |`nbf` |`1438535543` |Oświadczenie to hello godzina, w którym hello token prawidłową, w czasie epoki. To jest zwykle hello sam jak hello czasu hello token został wystawiony. Aplikację należy użyć tego oświadczenia tooverify hello ważności hello okres ważności tokenu. |
| Wersja |`ver` |`1.0` |To jest wersja hello hello identyfikator tokenu, zgodnie z definicją w usłudze Azure AD. |
| Kod skrótu |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Skrót kodu jest uwzględnione w tokenie identyfikator, tylko wtedy, gdy hello token jest wystawiony wraz z kodu autoryzacji protokołu OAuth 2.0. Skrót kodu mogą być używane toovalidate hello autentyczności kod autoryzacji. Aby uzyskać więcej informacji na temat tooperform tej weryfikacji, zobacz hello [OpenID Connect specyfikacji](http://openid.net/specs/openid-connect-core-1_0.html).  |
| Skrót token dostępu |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Skrót token dostępu jest uwzględnione w tokenie identyfikator, tylko wtedy, gdy hello token jest wystawiony wraz z tokenu dostępu protokołu OAuth 2.0. Skrót tokenu dostępu mogą być używane toovalidate hello autentyczności tokenu dostępu. Aby uzyskać więcej informacji na temat tooperform tej weryfikacji, zobacz hello [specyfikacji OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html)  |
| Identyfikator jednorazowy |`nonce` |`12345` |Identyfikator jednorazowy jest strategia używana toomitigate powtórzeń tokenów ataków. Aplikację można określić identyfikatora jednorazowego w żądaniu autoryzacji przy użyciu hello `nonce` parametr zapytania. wartość Hello podane w żądaniu hello będzie obliczanie nie mają być modyfikowane w hello `nonce` oświadczeń tylko identyfikator tokenu. Dzięki temu wartość aplikacji hello tooverify względem hello określone w żądaniu hello, co umożliwia skojarzenie aplikacji hello sesji z danego tokenu identyfikator. Aplikację należy wykonać tej weryfikacji podczas hello identyfikator sprawdzenia poprawności tokenu procesu. |
| Temat |`sub` |`884408e1-2918-4cz0-b12d-3aa027d7563b` |Jest to główna hello o którym hello token deklaracji rozkazujących informacje, takie jak hello użytkownika aplikacji. Ta wartość jest niezmienne i nie można ponownie przypisać lub ponownie. Sprawdzanie autoryzacji używany tooperform może być bezpiecznie, np. gdy hello token jest używane tooaccess zasobu. Domyślnie oświadczeń podmiotu hello jest wypełniane przy użyciu Identyfikatora obiektu hello hello użytkownika w katalogu hello. toolearn więcej, zobacz [usługi Azure Active Directory B2C: tokenu sesji i konfiguracji rejestracji jednokrotnej](active-directory-b2c-token-session-sso.md). |
| Klasy kontekstu uwierzytelniania |`acr` |Nie dotyczy |Nie używane obecnie, z wyjątkiem w przypadku hello starsze zasad. toolearn więcej, zobacz [usługi Azure Active Directory B2C: tokenu sesji i konfiguracji rejestracji jednokrotnej](active-directory-b2c-token-session-sso.md). |
| Framework zasady zaufania |`tfp` |`b2c_1_sign_in` |Jest to nazwa hello hello zasad, który był używany tooacquire hello Identyfikatora tokenu. |
| Czas uwierzytelniania |`auth_time` |`1438535543` |Oświadczenie to czas hello jaką ostatniego poświadczenia wprowadzonego użytkownika, reprezentowane w czasie epoki. |

### <a name="refresh-tokens"></a>Tokenów odświeżania
Odśwież tokeny to tokeny zabezpieczające aplikacji może użyć tooacquire nowe tokeny Identyfikatora i dostęp do tokenów w przepływu OAuth 2.0. Udostępniają one aplikacji z długoterminowej tooresources dostępu w imieniu użytkowników bez konieczności interakcji z tymi użytkownikami.

tooreceive token odświeżania w odpowiedzi tokenu aplikacji należy zażądać hello `offline_acesss` zakresu. więcej informacji na temat hello toolearn `offline_access` zakres, zapoznaj się toohello [odwołanie do usługi Azure AD B2C protokołu](active-directory-b2c-reference-protocols.md).

Tokenów odświeżania są i będą zawsze miały, całkowicie nieprzezroczyste tooyour aplikacji. Są wystawiane przez usługę Azure AD i mogą być kontrolowane i interpretowane tylko przez usługę Azure AD. Są one długotrwałe, ale aplikacja nie powinien być zapisywany z hello oczekiwanie, że trwa token odświeżania w określonym okresie czasu. Tokeny odświeżania nieważne można w dowolnym momencie z różnych przyczyn. Witaj tooattempt tooredeem jest sposób tooknow Twojej aplikacji, jeśli token odświeżania jest prawidłowy tylko go poprzez tooAzure żądania tokenu usługi AD.

Gdy zrealizować token odświeżania, aby uzyskać nowy token (i jeśli aplikacja ma przyznane hello `offline_access` zakresu), zostanie wyświetlony nowy token odświeżania w hello odpowiedzi tokenu. Należy zapisać hello nowo wystawiony token odświeżania. Należy go zastąpić token odświeżania hello wcześniej używane w żądaniu hello. Pozwala to zagwarantować, że tokenów odświeżania ważność tak długo, jak to możliwe.

## <a name="token-validation"></a>Token weryfikacji.
toovalidate tokenu aplikacji należy sprawdzić zarówno hello podpis, jak i oświadczenia hello tokenu.

Wiele bibliotek typu open source dostępnych sprawdzania poprawności tokenów Jwt, w zależności od preferowany język. Zaleca się, że można eksplorować te opcje, a nie implementacji logiki weryfikacji. Witaj informacje w tym przewodniku może pomóc Dowiedz się, jak korzystać z tooproperly tych bibliotek.

### <a name="validate-hello-signature"></a>Sprawdzanie poprawności podpisu hello
Token JWT zawiera trzy segmenty oddzielone hello `.` znaków. pierwszy segment Hello jest hello *nagłówka*, hello jest drugi hello *treści*, i hello jest trzeci hello *podpisu*. segment podpisu Hello może być używane toovalidate hello autentyczności hello token, dzięki czemu mogą być zaufane przez aplikację.

Azure AD B2C tokeny są podpisane za pomocą standardowych szyfrowanie asymetryczne algorytmy, takie jak RSA 256. Nagłówek Hello hello tokenu zawiera informacje na temat klucza hello i toosign hello token używany metody szyfrowania:

```
{
        "typ": "JWT",
        "alg": "RS256",
        "kid": "GvnPApfWMdLRi8PDmisFn7bprKg"
}
```

Witaj `alg` oświadczeń wskazuje hello algorytmu, który był używany toosign hello token. Witaj `kid` oświadczeń wskazuje hello określonego klucz publiczny, który był używany toosign hello token.

W dowolnym momencie usługi Azure AD można zarejestrować tokenu przy użyciu dowolny zestaw par kluczy publicznych i prywatnych. Usługi Azure AD obraca hello zestaw możliwych kluczy okresowo, więc aplikacja powinna być zapisana toohandle powoduje automatyczną zmianę tych kluczy. Toocheck uzasadnione częstotliwości aktualizacji toohello kluczy publicznych używane przez usługę Azure AD jest co 24 godziny.

Usługa Azure AD B2C ma punkt końcowy metadanych OpenID Connect. Umożliwia to aplikacjom toofetch informacji na temat usługi Azure AD B2C w czasie wykonywania. Informacje te obejmują punkty końcowe, zawartość tokenu i klucze podpisywania tokenu. Katalogu usługi B2C zawiera dokument metadanych JSON dla każdej zasady. Na przykład dokument metadanych hello hello `b2c_1_sign_in` zasad w `fabrikamb2c.onmicrosoft.com` znajduje się pod adresem:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in
```

`fabrikamb2c.onmicrosoft.com`jest katalog hello B2C używany tooauthenticate hello użytkownika, i `b2c_1_sign_in` jest tooacquire hello token używany hello zasad. toodetermine zasady, których został użyty toosign token (i gdzie toogo toofetch hello metadanych), są dostępne dwie opcje. Najpierw hello zasad nazwa jest uwzględniona w hello `acr` oświadczenia w tokenie hello. Można analizować oświadczeń poza hello treści hello JWT przez base-64 dekodowania hello treści i deserializacji hello JSON ciąg tego wyników. Witaj `acr` oświadczeń będzie nazwa hello hello zasad, który był używany tooissue hello token.  Drugą opcją jest zasad hello tooencode hello wartości hello `state` parametru, gdy Żądanie hello, a następnie zdekodować toodetermine zasady, które zostało użyte. Każda metoda jest prawidłowa.

Dokument metadanych Hello jest obiekt JSON, który zawiera przydatne w kilku informacji. Obejmują one lokalizację hello hello punkty końcowe wymagane tooperform uwierzytelniania OpenID Connect. Obejmuje to też `jwks_uri`, co daje hello lokalizacji hello zestawu kluczy publicznych, które są używane toosign tokenów. Tutaj podano tej lokalizacji, ale dynamicznie jest najlepszym miejscem hello toofetch za pomocą hello dokument metadanych i analizowania limit `jwks_uri`:

```
https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in
```

dokument JSON Hello znajdujący się pod tym adresem URL zawiera wszystkie hello informacje o kluczu publicznym używany w danym momencie. Aplikację można użyć hello `kid` oświadczeń w hello JWT nagłówka tooselect hello klucza publicznego w dokumencie JSON hello, która jest używana toosign określonej tokenu. Następnie można przeprowadzić sprawdzania poprawności podpisu za pomocą hello prawidłowy klucz publiczny i algorytm wskazanych hello.

Opis sposobu sprawdzania poprawności podpisu tooperform jest hello poza zakres tego dokumentu. Wiele biblioteki typu open source są dostępne toohelp o to, jeśli będzie potrzebny.

### <a name="validate-hello-claims"></a>Sprawdź poprawność hello oświadczeń
Gdy aplikację lub interfejsu API odbiera token Identyfikatora, go również wykonywać kilka kontroli względem hello oświadczenia w tokenie identyfikator hello. Te obejmują, ale nie są ograniczone do:

* Witaj **odbiorców** oświadczeń: zweryfikuje hello identyfikator tokenu zostało przeznaczone toobe podane tooyour aplikacji.
* Witaj **nie wcześniej niż** i **czas wygaśnięcia** oświadczenia: Sprawdź te hello identyfikator token nie wygasł.
* Witaj **wystawcy** oświadczeń: zweryfikuje hello token został wystawiony tooyour aplikacji przez usługę Azure AD.
* Witaj **identyfikator jednorazowy**: jest strategię ograniczenie ataków powtórzeń tokenów.

Pełna lista aplikacji należy wykonać sprawdzanie poprawności, znajduje się w sekcji toohello [OpenID Connect specyfikacji](https://openid.net). Szczegóły hello oczekiwanych wartości tych oświadczeń znajdują się w poprzednim hello [token sekcji](#types-of-tokens).  

## <a name="token-lifetimes"></a>Okresy istnienia tokenu
następujące okresy istnienia tokenu Hello są udostępniane toofurther wiedzy użytkownika. One może pomóc podczas opracowywania i debugowania aplikacji. Należy pamiętać, że aplikacje nie powinny być napisane tooexpect żadnego z tych stała tooremain okresy istnienia. Mogą i ulegnie zmianie. Dowiedz się więcej o hello [dostosowywania okresy istnienia tokenu](active-directory-b2c-token-session-sso.md) w usłudze Azure AD B2C.

| Token | Cykl życia | Opis |
| --- | --- | --- |
| Tokeny Identyfikatora |Jedna godzina |Identyfikator tokeny są zwykle prawidłowe godziny. Aplikacja sieci web można używać tego okresu istnienia toomaintain własnej sesji z użytkownikami (zalecane). Możesz również istnienia innej sesji. Jeśli Twoja aplikacja powinna tooget nowy token identyfikator, po prostu musi toomake nowe tooAzure żądania logowania usługi AD. Jeśli użytkownik ma prawidłowy sesję z usługą Azure AD, użytkownik może nie być tooenter wymaganych poświadczeń ponownie. |
| Tokenów odświeżania |Zapasowej too14 dni |Token odświeżania pojedynczego jest prawidłowa dla maksymalnie 14 dni. Jednak token odświeżania może być nieprawidłowy, w dowolnej chwili z kilku powodów. Dopiero po niepowodzeniu żądania hello lub aplikacja zastępuje token odświeżania hello nowej aplikacji powinno być kontynuowane toouse tootry token odświeżania. Token odświeżania również może być nieprawidłowy, jeśli upłynie 90 dni od czasu ostatniego wprowadzone poświadczenia użytkownika hello. |
| Kodach autoryzacji |Pięć minut |Kody autoryzacji są celowo krótkim okresie. One powinny być zrealizowane natychmiast tokenów dostępu, tokeny Identyfikatora lub tokenów odświeżania po odebraniu. |

