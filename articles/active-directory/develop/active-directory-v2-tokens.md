---
title: "aaaAzure usługi Active Directory w wersji 2.0 tokeny odwołania | Dokumentacja firmy Microsoft"
description: "Witaj typy tokenów i oświadczeń emitowane przez hello punktu końcowego v2.0 usługi Azure AD"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: dc58c282-9684-4b38-b151-f3e079f034fd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 29eb5c3402aeae302ee7c6234488520495f85904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-v20-tokens-reference"></a>Azure Active Directory w wersji 2.0 tokeny odwołania
Witaj punktu końcowego v2.0 usługi Azure Active Directory (Azure AD) emituje kilka typów tokenów zabezpieczających w każdym [przepływ uwierzytelniania](active-directory-v2-flows.md). To odwołanie opisano hello format, właściwości zabezpieczeń i zawartości każdego typu tokenu.

> [!NOTE]
> punktu końcowego v2.0 Hello nie obsługuje wszystkich scenariuszy Azure Active Directory i funkcji. toodetermine, czy należy używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
>
>

## <a name="types-of-tokens"></a>Typy tokenów
Witaj punktu końcowego v2.0 obsługuje hello [protokół OAuth 2.0](active-directory-v2-protocols.md), który korzysta z tokenów dostępu i tokenów odświeżania. punktu końcowego v2.0 Hello obsługuje również uwierzytelniania i logowania za pomocą [OpenID Connect](active-directory-v2-protocols.md). OpenID Connect wprowadza trzeci typ tokenu, hello Identyfikatora tokenu. Każdy z tych tokenów jest reprezentowany jako *elementu nośnego* tokenu.

Token elementu nośnego jest token zabezpieczający lekkie, że przyznaje hello tooa dostępu do elementu nośnego chronionych zasobów. elementu nośnego Hello jest każda strona, która może ona powodować hello tokenu. Mimo że strona musi przeprowadzić uwierzytelnianie tokenu elementu nośnego hello tooreceive usługi Azure AD, jeśli kroki nie są brane toosecure hello tokenu podczas transmisji i przechowywania, można przechwycony i używane przez niezamierzone strony. Niektóre tokeny zabezpieczające ma wbudowany mechanizm strony tooprevent nieautoryzowany używana, ale tokenów elementu nośnego nie. Musi być transportowane tokenów elementu nośnego bezpiecznego kanału, takie jak zabezpieczeń warstwy transportu (HTTPS). Jeśli token elementu nośnego, są przesyłane bez zabezpieczeń tego typu, strony złośliwych można użyć tokenu "man-in--middle ataku" hello tooacquire i użyć jej do nieautoryzowanego dostępu tooa chronionych zasobów. Witaj te same zasady zabezpieczeń mają zastosowanie po zapisaniu lub buforowanie tokenów elementu nośnego do późniejszego użycia. Zawsze upewnij się, że aplikacji bezpiecznego przesyła i przechowuje tokenów elementu nośnego. Aby uzyskać więcej uwagi dotyczące zabezpieczeń tokenów elementu nośnego, zobacz [RFC 6750 sekcji 5](http://tools.ietf.org/html/rfc6750).

Wiele hello tokenów wystawionych przez punktu końcowego v2.0 hello są zaimplementowane jako tokenów sieci Web JSON (Jwt). Token JWT jest informacji tootransfer sposób compact, bezpieczne dla adresu URL, między dwiema stronami. Witaj w token JWT nosi nazwę *oświadczeń*. To potwierdzenie informacji na temat elementów nośnych hello i podmiotu hello tokenu. oświadczenia Hello w token JWT są obiektów JavaScript Object Notation (JSON), które są zakodowane i serializację do transmisji. Ponieważ hello Jwt wystawione przez punktu końcowego v2.0 hello jest podpisany, ale nie są szyfrowane, możesz łatwo sprawdzić zawartość hello token JWT na potrzeby debugowania. Aby uzyskać więcej informacji na temat tokenów Jwt, zobacz hello [specyfikacji JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

### <a name="id-tokens"></a>Tokeny Identyfikatora
Identyfikator tokenu jest formą logowania w tokenie zabezpieczającym aplikacja odbiera podczas uwierzytelniania przy użyciu [OpenID Connect](active-directory-v2-protocols.md). Identyfikator tokeny są reprezentowane jako [Jwt](#types-of-tokens), i zawierają roszczenia, w której można toosign hello użytkownika w aplikacji tooyour. Można użyć hello oświadczenia w tokenie identyfikator na różne sposoby. Zazwyczaj Administratorzy korzystają informacji o identyfikatorze tokenów toodisplay konta lub toomake decyzje dotyczące kontroli dostępu w aplikacji. punktu końcowego v2.0 Hello wystawia tylko jednego typu Identyfikatora tokenu, który ma spójny zestaw oświadczeń, niezależnie od typu hello użytkownika, który jest zalogowany. Hello format i zawartość tokeny Identyfikatora są hello takie same, osobistych użytkowników kont Microsoft i konta firmowego lub szkolnego.

Tokeny Identyfikatora są obecnie podpisany, ale nie jest zaszyfrowany. Gdy aplikacja odbiera token Identyfikatora, należy [sprawdzanie poprawności podpisu hello](#validating-tokens) tooprove hello autentyczności tokenu i zweryfikować kilka oświadczenia w hello token tooprove jego ważności. Witaj oświadczeń zweryfikowany przez aplikację różny w zależności od wymagań scenariusza, ale aplikacji należy wykonać niektóre [typowych operacji sprawdzania poprawności oświadczeń](#validating-tokens) w każdym scenariuszu.

Firma Microsoft daje hello wszystkich szczegółów dotyczących oświadczenia w tokenach identyfikator w hello następujących sekcji, oprócz tooa przykładowy identyfikator token. Należy pamiętać, że oświadczenia w tokenach identyfikator nie są zwracane w określonej kolejności. Ponadto oświadczeń nowy mogą zostać wprowadzone do tokeny Identyfikatora, w dowolnym momencie. Aplikacji nie powinna Przerwij, gdy wprowadzono nowych oświadczeń. Hello następujące listy zawiera hello oświadczenia, które aplikacji obecnie można niezawodnie zinterpretować. Więcej informacji można znaleźć w hello [OpenID Connect specyfikacji](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-id-token"></a>Przykładowy identyfikator token
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiI2NzMxZGU3Ni0xNGE2LTQ5YWUtOTdiYy02ZWJhNjkxNDM5MWUiLCJpc3MiOiJodHRwczovL2xvZ2luLm1pY3Jvc29mdG9ubGluZS5jb20vYjk0MTk4MTgtMDlhZi00OWMyLWIwYzMtNjUzYWRjMWYzNzZlL3YyLjAiLCJpYXQiOjE0NTIyODUzMzEsIm5iZiI6MTQ1MjI4NTMzMSwiZXhwIjoxNDUyMjg5MjMxLCJuYW1lIjoiQmFiZSBSdXRoIiwibm9uY2UiOiIxMjM0NSIsIm9pZCI6ImExZGJkZGU4LWU0ZjktNDU3MS1hZDkzLTMwNTllMzc1MGQyMyIsInByZWZlcnJlZF91c2VybmFtZSI6InRoZWdyZWF0YmFtYmlub0BueXkub25taWNyb3NvZnQuY29tIiwic3ViIjoiTUY0Zi1nZ1dNRWppMTJLeW5KVU5RWnBoYVVUdkxjUXVnNWpkRjJubDAxUSIsInRpZCI6ImI5NDE5ODE4LTA5YWYtNDljMi1iMGMzLTY1M2FkYzFmMzc2ZSIsInZlciI6IjIuMCJ9.p_rYdrtJ1oCmgDBggNHB9O38KTnLCMGbMDODdirdmZbmJcTHiZDdtTc-hguu3krhbtOsoYM2HJeZM3Wsbp_YcfSKDY--X_NobMNsxbT7bqZHxDnA2jTMyrmt5v2EKUnEeVtSiJXyO3JWUq9R0dO-m4o9_8jGP6zHtR62zLaotTBYHmgeKpZgTFB9WtUq8DVdyMn_HSvQEfz-LWqckbcTwM_9RNKoGRVk38KChVJo4z5LkksYRarDo8QgQ7xEKmYmPvRr_I7gvM2bmlZQds2OeqWLB1NSNbFZqyFOCgYn3bAQ-nEQSKwBaA36jYGPOVG2r2Qv1uKcpSOxzxaQybzYpQ
```

> [!TIP]
> Praktyki, tooinspect hello oświadczenia w tokenie identyfikator próbki hello, Wklej hello przykładowy identyfikator tokenu do [calebb.net](http://calebb.net/).
>
>

#### <a name="claims-in-id-tokens"></a>Oświadczenia w tokenach identyfikator
| Nazwa | Claim | Przykładowa wartość | Opis |
| --- | --- | --- | --- |
| grupy odbiorców |`aud` |`6731de76-14a6-49ae-97bc-6eba6914391e` |Identyfikuje hello przeznaczone odbiorcy tokenu hello. W tokenach identyfikator odbiorców hello jest identyfikator aplikacji aplikacji, przypisany tooyour aplikacji w portalu rejestracji aplikacji Microsoft hello. Aplikację należy sprawdzić tę wartość i Odrzuć hello token, jeśli wartość hello jest niezgodna. |
| Wystawcy |`iss` |`https://login.microsoftonline.com/b9419818-09af-49c2-b0c3-653adc1f376e/v2.0 ` |Identyfikuje hello usługi tokenu zabezpieczającego (STS) tworzy i zwraca hello token i hello dzierżawy usługi Azure AD, w których hello uwierzytelnienia użytkownika. Aplikację należy zweryfikować Witaj wystawca oświadczeń tooensure, który hello tokenu pochodzi z punktu końcowego v2.0 hello. On również należy używać części identyfikatora GUID hello hello toorestrict hello zestawu oświadczeń dzierżawcami, które można zarejestrować się w aplikacji toohello. Witaj identyfikator GUID, który wskazuje użytkownika hello jest użytkownik konsumentów firmy Microsoft, konto jest `9188040d-6c67-4c5b-b112-36a304b66dad`. |
| wystawiony w |`iat` |`1452285331` |czas Hello, w których hello token został wystawiony, czas epoki. |
| czas wygaśnięcia |`exp` |`1452289231` |czas Hello, w których hello token staje się nieprawidłowy, reprezentowane w czasie epoki. Aplikację należy użyć tego oświadczenia tooverify hello ważności hello okres ważności tokenu. |
| nie wcześniej niż |`nbf` |`1452285331` |czas Hello, w których hello token staje się nieprawidłowy, reprezentowane w czasie epoki. Jest zwykle hello sam jako czas wystawiania hello. Aplikację należy użyć tego oświadczenia tooverify hello ważności hello okres ważności tokenu. |
| Wersja |`ver` |`2.0` |Wersja Hello hello identyfikator tokenu, zgodnie z definicją w usłudze Azure AD. Dla punktu końcowego v2.0 hello, wartość hello jest `2.0`. |
| Identyfikator dzierżawy |`tid` |`b9419818-09af-49c2-b0c3-653adc1f376e` |Identyfikator GUID, który reprezentuje dzierżawy hello Azure AD, która hello użytkownika jest. Dla kont służbowych hello identyfikator GUID jest hello niezmienne dzierżawy, której należy dany identyfikator organizacji hello hello użytkownika. W przypadku konta osobiste, wartość hello jest `9188040d-6c67-4c5b-b112-36a304b66dad`. Witaj `profile` zakres jest wymagany w celu tooreceive tego oświadczenia. |
| Kod skrótu |`c_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Skrót kodu Hello wchodzi w tokeny Identyfikatora tylko wtedy, gdy token identyfikator hello jest wystawiony z kodu autoryzacji protokołu OAuth 2.0. Może być używane toovalidate hello autentyczności kod autoryzacji. Aby uzyskać szczegółowe informacje o wykonywaniu tej weryfikacji, zobacz hello [OpenID Connect specyfikacji](http://openid.net/specs/openid-connect-core-1_0.html). |
| Skrót token dostępu |`at_hash` |`SGCPtt01wxwfgnYZy2VJtQ` |Skrót tokenu dostępu Hello znajduje się w identyfikatorze tokenów tylko wtedy, gdy token Identyfikatora hello jest wydane token dostępu protokołu OAuth 2.0. Może być używane toovalidate hello autentyczności tokenu dostępu. Aby uzyskać szczegółowe informacje o wykonywaniu tej weryfikacji, zobacz hello [OpenID Connect specyfikacji](http://openid.net/specs/openid-connect-core-1_0.html). |
| Identyfikator jednorazowy |`nonce` |`12345` |Identyfikator jednorazowy Hello jest strategii łagodzenia ataków powtórzeń tokenów. Aplikację można określić identyfikatora jednorazowego w żądaniu autoryzacji przy użyciu hello `nonce` parametr zapytania. wartość Hello podane w żądaniu hello jest emitowany hello identyfikator tokenu `nonce` oświadczenia, nie mają być modyfikowane. Aplikację można zweryfikować wartości hello względem hello określone w żądaniu hello, co umożliwia skojarzenie aplikacji hello sesji z określonym tokenem identyfikator. Aplikację należy wykonać tej weryfikacji podczas hello identyfikator sprawdzenia poprawności tokenu procesu. |
| name |`name` |`Babe Ruth` |oświadczenia nazwy Hello zawiera wartość zrozumiałą dla użytkownika, która identyfikuje podmiotu hello hello tokenu. wartość Hello nie jest gwarantowana toobe unikatowe, jest modyfikowalna, i jest zaprojektowany toobe używana tylko do wyświetlania. Witaj `profile` zakres jest wymagany w celu tooreceive tego oświadczenia. |
| Adres e-mail |`email` |`thegreatbambino@nyy.onmicrosoft.com` |Witaj podstawowego adresu e-mail skojarzonego z hello konta użytkownika, jeśli taka istnieje. Jego wartość jest modyfikowalna i może ulec zmianie. Witaj `email` zakres jest wymagany w celu tooreceive tego oświadczenia. |
| Preferowany nazwy użytkownika |`preferred_username` |`thegreatbambino@nyy.onmicrosoft.com` |Witaj głównej nazwy użytkownika, która reprezentuje użytkownika hello w hello punktu końcowego v2.0. Może to być adres e-mail, numer telefonu lub ogólny nazwy użytkownika bez określonego formatu. Jego wartość jest modyfikowalna i może ulec zmianie. Witaj `profile` zakres jest wymagany w celu tooreceive tego oświadczenia. |
| Temat |`sub` |`MF4f-ggWMEji12KynJUNQZphaUTvLcQug5jdF2nl01Q` | główna Hello, o którym hello token deklaracji rozkazujących informacje, takie jak hello użytkownika aplikacji. Ta wartość jest niezmienne i nie można ponownie przypisać lub ponownie. Sprawdzanie autoryzacji używany tooperform może być bezpiecznie, takie jak podczas hello token jest używany tooaccess zasobu i może być używany jako klucz w tabelach bazy danych. Ponieważ podmiotu hello jest zawsze znajdujących się w tokeny hello problemów z usługą Azure AD, zaleca się korzystanie z tej wartości w systemie autoryzacji ogólnego przeznaczenia. podmiot Hello jest jednak parowania identyfikator — to identyfikator unikatowy tooa określonej aplikacji.  W związku z tym jeśli jeden użytkownik zaloguje się do dwóch różnych aplikacji przy użyciu dwóch identyfikatorów innego klienta, tych aplikacji zostanie wyświetlony dwóch różnych wartości oświadczenia podmiotu hello.  To może lub nie może być wskazane w zależności od wymagań architektury i ochrony prywatności. |
| Identyfikator obiektu: |`oid` |`a1dbdde8-e4f9-4571-ad93-3059e3750d23` | Witaj niezmienne identyfikator obiektu w hello Microsoft tożsamości systemu, w tym przypadku konta użytkownika.  Sprawdzanie autoryzacji używany tooperform może być również bezpiecznie i jako klucz w tabelach bazy danych. Ten identyfikator unikatowo identyfikuje hello użytkownika w aplikacjach — Witaj dwóch różnych aplikacji logowanie hello otrzymają tego samego użytkownika, takie same wartości w hello `oid` oświadczeń.  Oznacza to, że mogą być używane podczas wykonywania kwerend tooMicrosoft usług online services, takich jak hello Microsoft Graph.  Witaj Microsoft Graph, którą będzie zwracać ten identyfikator jako hello `id` właściwości dla danego konta użytkownika.  Ponieważ hello `oid` zezwala na wiele aplikacji użytkowników toocorrelate hello `profile` zakres jest wymagany w celu tooreceive tego oświadczenia. Należy pamiętać, że jeden użytkownik istnieje w wielu dzierżawców, hello użytkownika będzie zawierać identyfikator inny obiekt, w każdej dzierżawy — są traktowane jako różne konta, mimo że hello zalogowaniu użytkownika do wszystkich kont z hello tych samych poświadczeń. |

### <a name="access-tokens"></a>Tokeny dostępu
Obecnie wystawiony przez punktu końcowego v2.0 hello tokenów dostępu mogą być używane tylko przez program Microsoft Services. Aplikacje nie powinny potrzebne tooperform weryfikacji ani kontroli tokenów dostępu hello obecnie obsługiwane scenariusze. Tokeny dostępu można traktować jako całkowicie przezroczystości. Są one tylko ciągi, że aplikację można przekazać tooMicrosoft żądań HTTP.

W hello niemal przyszłych, v2.0 hello punktu końcowego wprowadzi hello możliwości dla tokenów dostępu tooreceive aplikacji z innych klientów. W tym czasie program hello informacje w tym temacie zostaną zaktualizowane z hello informacje potrzebne do Twojej aplikacji tooperform dostępu tokenu weryfikacji i inne podobne zadania.

W przypadku żądania tokenu dostępu z punktu końcowego v2.0 hello, punktu końcowego v2.0 hello również zwraca metadane dotyczące hello tokenu dostępu dla użytkownika toouse aplikacji. Informacje te obejmują hello czas wygaśnięcia tokenu dostępu hello i zakresy hello, dla których jest prawidłowy. Twoja aplikacja korzysta z tego tooperform inteligentne buforowanie metadanych tokenów dostępu bez tokenu dostępu Otwórz hello tooparse sam.

### <a name="refresh-tokens"></a>Tokenów odświeżania
Tokenów odświeżania są tokenów w przepływu OAuth 2.0 dostęp do aplikacji za pomocą tooget nowe tokeny zabezpieczające. Aplikację można użyć odświeżania tokenów tooachieve długoterminowej dostępu tooresources w imieniu użytkownika bez konieczności interakcji z użytkownikiem hello.

Tokeny odświeżania są wielu zasobów. Token odświeżania otrzymał podczas żądania tokenu dla jednego zasobu można wykorzystać dla zasobu dwóch zupełnie różnych tooa tokenów dostępu.

tooreceive odświeżania w odpowiedzi tokenu, należy zażądać aplikacji i otrzymać hello `offline_acesss` zakresu. więcej informacji na temat hello toolearn `offline_access` zakres, zobacz hello [zgody i zakresy](active-directory-v2-scopes.md) artykułu.

Tokenów odświeżania są i zawsze będą, całkowicie nieprzezroczyste tooyour aplikacji. One są wystawiane przez punktu końcowego v2.0 usługi Azure AD hello i można tylko inspekcji, a interpretowane przez hello punktu końcowego v2.0. Są one długotrwałe, ale nie powinien być zapisywany aplikacji tooexpect, który ka¿dy okres będzie trwać token odświeżania. Tokeny odświeżania nieważne można w dowolnym momencie z różnych przyczyn. Witaj tooattempt tooredeem jest sposób tooknow Twojej aplikacji, jeśli token odświeżania jest prawidłowy tylko jego dokonując punktu końcowego v2.0 toohello żądania tokenu.

Gdy zrealizować token odświeżania, aby uzyskać nowy token dostępu (i jeśli przyznano aplikacji hello `offline_access` zakresu), zostanie wyświetlony nowy token odświeżania w hello odpowiedzi tokenu. Zapisz hello nowo wystawiony odświeżanie tokenu, tooreplace hello jedną, którego użyto w żądaniu hello. Gwarantuje to, że tokenów odświeżania ważność tak długo, jak to możliwe.

## <a name="validating-tokens"></a>Sprawdzanie poprawności tokenów
Obecnie hello tylko sprawdzenia poprawności tokenu aplikacji konieczne tooperform jest sprawdzanie poprawności tokenów identyfikator. toovalidate token Identyfikatora aplikacji należy zweryfikować zarówno hello token identyfikator podpisu i hello oświadczeń z hello identyfikator tokenu.

<!-- TODO: Link -->
Firma Microsoft udostępnia bibliotek i przykładów kodu, które pokazują, jak tooeasily obsługuje tokenu weryfikacji. W kolejnych sekcjach hello przedstawione hello podstawowy proces. Kilka bibliotek open source innych firm również są dostępne do weryfikacji tokenu JWT. Ma co najmniej jedną bibliotekę opcji dla prawie wszystkich platform i języków.

### <a name="validate-hello-signature"></a>Sprawdzanie poprawności podpisu hello
Token JWT zawiera trzy segmentów, które są oddzielone hello `.` znaków. pierwszy segment Hello jest nazywany hello *nagłówka*, drugi segment hello jest hello *treści*, i segmentu trzeciego hello jest hello *podpisu*. segment podpisu Hello może być używane toovalidate hello autentyczności hello identyfikator tokenu, dzięki czemu mogą być zaufane przez aplikację.

Tokeny Identyfikatora zalogowano się za pomocą standardowych szyfrowanie asymetryczne algorytmy, takie jak RSA 256. Witaj nagłówka hello identyfikator tokenu ma informacji na temat klucza hello i toosign hello token używany metody szyfrowania. Na przykład:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "kid": "MnC_VZcATfM5pOYiJHMba9goEKY"
}
```

Witaj `alg` oświadczeń wskazuje hello algorytmu, który był używany toosign hello token. Witaj `kid` oświadczeń wskazuje hello klucza publicznego, który był używany toosign hello token.

W dowolnym momencie punktu końcowego v2.0 hello może podpisać identyfikator tokenu przy użyciu jednej z określonych par kluczy publicznych i prywatnych. punktu końcowego v2.0 Hello okresowo obraca hello możliwe zestawu kluczy, więc aplikacja powinna być zapisana toohandle powoduje automatyczną zmianę tych kluczy. Toocheck uzasadnione częstotliwości aktualizacji toohello kluczy publicznych używane przez punktu końcowego v2.0 hello jest co 24 godziny.

Można uzyskać hello podpisywania klucza danych toovalidate hello podpisu za pomocą hello OpenID Connect dokument metadanych w lokalizacji:

```
https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration
```

> [!TIP]
> Spróbuj użyć adresu URL hello w przeglądarce!
>
>

Ten dokument metadanych jest obiekt JSON, który ma kilka części przydatne informacje, takie jak lokalizacja hello hello różne punkty końcowe wymagane do uwierzytelniania OpenID Connect.  zawiera również dokumentu Hello *jwks_uri*, co daje hello lokalizacji hello zestawu kluczy publicznych używane toosign tokenów. dokument JSON Hello znajdujący się w hello jwks_uri ma wszystkie hello informacje o kluczu publicznym, który jest aktualnie używany. Aplikację można użyć hello `kid` oświadczeń w hello JWT nagłówka tooselect, którego klucz publiczny w tym dokumencie został użyty toosign tokenu. Następnie wykonuje sprawdzanie poprawności podpisu za pomocą hello prawidłowy klucz publiczny i algorytm wskazanych hello.

Sprawdzaniu poprawności podpisu jest poza zakresem hello tego dokumentu. Wiele open source biblioteki są dostępne toohelp zostanie o tym.

### <a name="validate-hello-claims"></a>Sprawdź poprawność hello oświadczeń
Gdy aplikacja odbiera token identyfikator podczas logowania użytkownika, jego również wykonywać kilka kontroli względem hello oświadczeń hello identyfikator tokenu. Te obejmują, ale nie są ograniczone do:

* **grupy odbiorców** oświadczeń tooverify, który hello token Identyfikatora zostało przeznaczone toobe podane tooyour aplikacji
* **nie wcześniej niż** i **czas wygaśnięcia** oświadczeń, tooverify, który hello identyfikator token nie wygasł.
* **Wystawca** oświadczeń tooverify, który hello token został wystawiony tooyour aplikacji przez hello punktu końcowego v2.0
* **Identyfikator jednorazowy**, jako token powtarzania ograniczenie ataków

Aby uzyskać pełną listę operacji sprawdzania poprawności oświadczenia, które należy wykonać w aplikacji, zobacz hello [OpenID Connect specyfikacji](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).

Szczegóły hello oczekiwanych wartości tych oświadczeń są objęte hello [tokeny Identyfikatora](# ID tokens) sekcji.

## <a name="token-lifetimes"></a>Okresy istnienia tokenu
Udostępniamy hello następującego tokenu okresy istnienia tylko charakter informacyjny. Hello informacje mogą pomóc podczas opracowywania i debugowania aplikacji. Aplikacje nie powinny być napisane tooexpect żadnego z tych stała tooremain okresy istnienia. Token może okresy istnienia i zmieni się w dowolnym momencie.

| Token | Cykl życia | Opis |
| --- | --- | --- |
| Identyfikator tokeny (konta firmowego lub szkolnego) |1 godzina |Tokeny Identyfikatora zwykle są prawidłowe dla 1 godzina. Aplikacja sieci web można użyć tego samego toomaintain okres istnienia własnej sesji z hello użytkownika (zalecane), lub wybrać okres istnienia sesji innej. Jeśli Twoja aplikacja powinna tooget nowy token identyfikator, musi toomake nowe logowanie żądania punktu końcowego autoryzacji toohello w wersji 2.0. Jeśli użytkownik hello ma prawidłową sesję z punktem końcowym v2.0 hello, hello użytkownika nie może być wymagane tooenter ponownie swoje poświadczenia. |
| Identyfikator tokeny (konta osobiste) |24 godziny |Identyfikator tokeny dla kont osobistych zwykle są ważne przez 24 godziny. Aplikacja sieci web można użyć tego samego toomaintain okres istnienia własnej sesji z hello użytkownika (zalecane), lub wybrać okres istnienia sesji innej. Jeśli Twoja aplikacja powinna tooget nowy token identyfikator, musi toomake nowe logowanie żądania punktu końcowego autoryzacji toohello w wersji 2.0. Jeśli użytkownik hello ma prawidłową sesję z punktem końcowym v2.0 hello, hello użytkownika nie może być wymagane tooenter ponownie swoje poświadczenia. |
| Tokeny dostępu (konta firmowego lub szkolnego) |1 godzina |Wskazane jako część tokenu metadanych hello odpowiedzi tokenu. |
| Tokeny dostępu (konta osobiste) |1 godzina |Wskazane jako część tokenu metadanych hello odpowiedzi tokenu. Tokenów dostępu, które są wydawane w imieniu kont osobistych można skonfigurować dla różnych okres istnienia, ale jest typowy 1 godzina. |
| Odśwież tokeny (konta firmowego lub szkolnego) |Zapasowej too14 dni |Token odświeżania pojedynczego jest prawidłowa dla maksymalnie 14 dni. Jednak token odświeżania hello mogą być nieprawidłowe w dowolnym momencie z różnych powodów, dlatego aplikacji powinno być kontynuowane toouse tootry token odświeżania, dopóki nie jest on lub dopóki aplikacja zastępuje go nowy token odświeżania. Token odświeżania również staje się nieprawidłowy, jeśli został 90 dni od momentu hello użytkownik wprowadził swoje poświadczenia. |
| Odśwież tokeny (konta osobiste) |Zapasowej too1 roku |Token odświeżania pojedynczego jest prawidłowa dla maksymalnie 1 rok. Jednak w dowolnym momencie z różnych powodów token odświeżania hello mogą być nieprawidłowe, więc aplikacji powinno być kontynuowane tootry toouse token odświeżania, dopóki zakończy się niepowodzeniem. |
| Kodach autoryzacji (konta firmowego lub szkolnego) |10 minut |Kodach autoryzacji są celowo krótkim okresie i powinny być natychmiast zrealizowane tokenów dostępu i tokenów odświeżania, po odebraniu hello tokenów. |
| Kodach autoryzacji (konta osobiste) |5 minut |Kodach autoryzacji są celowo krótkim okresie i powinny być natychmiast zrealizowane tokenów dostępu i tokenów odświeżania, po odebraniu hello tokenów. Kodach autoryzacji, które są wydawane w imieniu kont osobistych jest przeznaczony do jednorazowego użytku. |
