---
title: "Usługa Azure Active Directory B2C: Jednostronicowej aplikacji przy użyciu niejawnego przepływu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aplikacje jednej strony toobuild bezpośrednio przy użyciu protokołu OAuth 2.0 niejawnego przepływu z usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: a45cc74c-a37e-453f-b08b-af75855e0792
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: parakhj
ms.openlocfilehash: 5e52abc18fe545f0f6d1745cdb2ea42c5b2698cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-single-page-app-sign-in-by-using-oauth-20-implicit-flow"></a>Usługa Azure AD B2C: Jednostronicowej aplikacji logowania przy użyciu niejawnego przepływu OAuth 2.0

> [!NOTE]
> Ta funkcja jest dostępna w wersji zapoznawczej.
> 

Wiele nowoczesnych aplikacji ma jednostronicowej aplikacji fronton głównie napisany w języku JavaScript. Często aplikacji hello jest zapisywany przy użyciu framework, takich jak AngularJS, Ember.js lub Durandal. Aplikacje jednej strony i innych aplikacji JavaScript, które można uruchamiać głównie w przeglądarce ma pewne dodatkowe problemy dotyczące uwierzytelniania:

* właściwości zabezpieczeń Hello te aplikacje są znacznie różni się od tradycyjnych na serwerze sieci web aplikacji.
* Wiele serwerów autoryzacji i dostawców tożsamości nie obsługują współużytkowanie zasobów między źródłami (CORS) żądania udostępniania.
* Przekierowania całej strony przeglądarki w kierunku od aplikacji hello może być znacznie inwazyjne toohello środowisko użytkownika.

toosupport tych aplikacji, usługi Azure Active Directory B2C (Azure AD B2C) używa przepływu niejawnego hello OAuth 2.0. Przepływ niejawne Przyznaj autoryzacji OAuth 2.0 Hello jest opisany w [sekcji 4.2 specyfikacji hello OAuth 2.0](http://tools.ietf.org/html/rfc6749). W niejawnego przepływu aplikacji hello odbiera tokeny bezpośrednio z hello punktu końcowego, bez żadnych do serwera exchange autoryzacji usługi Azure Active Directory (Azure AD). Wszystkie logika uwierzytelniania i sesji obsługi ma umieścić w całości powitania klienta JavaScript, bez dodatkowa strona przekierowania.

Usługa Azure AD B2C rozszerza hello standardowego protokołu OAuth 2.0 przepływu niejawnego toomore niż prostego uwierzytelniania i autoryzacji. Usługa Azure AD B2C wprowadza hello [parametru zasad](active-directory-b2c-reference-policies.md). Z parametrem zasad hello, można użyć protokołu OAuth 2.0 użytkownika tooadd napotyka tooyour aplikacji, takich jak konta, logowania i zarządzania profilami. W tym artykule zostanie przedstawiony zostanie sposób toouse hello niejawnego przepływu i usługi Azure AD tooimplement każdej funkcji aplikacji jednej strony. toohelp rozpocząć, zapoznaj się naszego [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi) i [programu Microsoft .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi) próbek.

W żądaniach HTTP przykład hello w tym artykule, korzystamy z naszych katalog usługi Azure AD B2C przykładu **fabrikamb2c.onmicrosoft.com**. Możemy również użyć własnej przykładowej aplikacji i zasad. Można spróbować żądań hello samodzielnie przy użyciu tych wartości, lub należy je zastąpić własne wartości.
Dowiedz się, jak za[uzyskać własnego katalogu usługi Azure AD B2C, aplikacji i zasad](#use-your-own-b2c-tenant).


## <a name="protocol-diagram"></a>Diagram protokołu

Witaj logowania przepływu niejawnego wygląda powitania po rysunku. Każdy krok jest szczegółowo opisane w dalszej części artykułu hello.

![OpenID Connect ścieżek](../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## <a name="send-authentication-requests"></a>Wysyłanie żądania uwierzytelniania
W przypadku aplikacji sieci web musi tooauthenticate hello użytkowników i wykonywanie zasad, kieruje go toohello użytkownika hello `/authorize` punktu końcowego. Jest hello interakcyjne część przepływu hello, gdzie hello użytkownik wykona akcję w zależności od zasad hello. Użytkownik Hello pobiera identyfikator tokenu z punktu końcowego usługi Azure AD hello.

W tym żądaniu powitania klienta wskazuje w hello `scope` uprawnienia hello parametru musi tooacquire hello użytkownika. W hello `p` parametr wskazuje hello tooexecute zasad. Witaj następujące trzy przykłady można podać (podziałów wierszy dla czytelności) każdego użyć różnych zasad. tooget działania dla działania każdego żądania, spróbuj wklejanie hello żądania do przeglądarki i jego uruchomieniem.

### <a name="use-a-sign-in-policy"></a>Użyj zasad logowania
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Użyj zasad rejestracji
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Użyj zasad edycji profilu
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Parametr | Wymagana? | Opis |
| --- | --- | --- |
| client_id |Wymagane |Identyfikator aplikacji Hello przypisany tooyour aplikacji w hello [portalu Azure](https://portal.azure.com). |
| response_type |Wymagane |Musi zawierać `id_token` OpenID Connect logowaniu. On również obejmować opcję Typ odpowiedzi hello `token`. Jeśli używasz `token`, aplikacja może bezpośrednio odbierać token dostępu z hello autoryzacji punktu końcowego, bez wprowadzania drugi toohello żądania punktu końcowego autoryzacji.  Jeśli używasz hello `token` typ odpowiedzi, hello `scope` parametr musi zawierać zakres, który wskazuje, które token hello tooissue zasobów dla. |
| redirect_uri |Zalecane |Identyfikator URI aplikacji, gdzie można wysyłanych i odbieranych przez aplikację uwierzytelniania odpowiedzi przekierowania Hello. Go musi dokładnie odpowiadać jeden hello przekierowania URI, który został zarejestrowany w portalu hello z tą różnicą, że musi być zakodowane w adresie URL. |
| response_mode |Zalecane |Określa hello metody toouse toosend hello wynikowy tooyour tyłu tokenu aplikacji.  Niejawne przepływów, użyj `fragment`. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów. Wartość pojedynczy zakres wskazuje tooAzure AD zarówno hello uprawnienia, które są żądane. Witaj `openid` toosign uprawnienia, w danych użytkownika i get hello o hello użytkownika w postaci hello tokenów identyfikator wskazuje zakres. (Będzie omawianiu to bardziej dalszej części artykułu hello.) Witaj `offline_access` zakres jest opcjonalne dla aplikacji sieci web. Wskazuje on, że Twoja aplikacja powinna token odświeżania dla tooresources długotrwałe dostępu. |
| state |Zalecane |Wartość zawarte w żądaniu hello, który jest także zwracany w odpowiedzi tokenu hello. Można go ciągu zawartości, które mają toouse. Zwykle jest używana wartość losowo generowany, unikatowy, okno fałszerstwie żądania międzywitrynowego tooprevent. Witaj stan jest również używane tooencode informacji o stanie użytkownika hello w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takich jak strony hello znajdowały się w. |
| Identyfikator jednorazowy |Wymagane |Wartość zawarte w żądaniu hello (wygenerowany przez aplikację hello), który znajduje się w hello identyfikator tokenu jako oświadczenia. Aplikacja Hello następnie sprawdzić, czy ataki powtórzeń tokenów toomitigate wartość. Zazwyczaj wartość hello jest losowe, unikatowy ciąg, który może być używane tooidentify hello pochodzenia hello żądania. |
| P |Wymagane |Witaj tooexecute zasad. Jego hello nazwę zasad, która jest tworzona w dzierżawie usługi Azure AD B2C. wartość Nazwa zasad Hello powinny rozpoczynać się od **b2c\_1\_**. Aby uzyskać więcej informacji, zobacz [wbudowane zasady usługi Azure AD B2C](active-directory-b2c-reference-policies.md). |
| wiersz |Optional (Opcjonalność) |Typ Hello interakcji użytkownika, która jest wymagana. Obecnie jest jedyną poprawną wartością hello `login`. Wymusza hello użytkownika tooenter swoje poświadczenia dla tego żądania. Logowanie jednokrotne nie zacznie obowiązywać. |

W tym momencie hello użytkownik jest proszony toocomplete hello zasad przepływu pracy. Może to obejmować użytkownika hello wprowadzić swoją nazwę użytkownika i hasło, zalogować się społecznościowych tożsamości, podczas tworzenia katalogu hello lub dowolnej liczby kroków. Akcje użytkownika zależą od tego, jak zdefiniowano hello zasad.

Po zakończeniu zasad hello hello użytkownika usługi Azure AD zwraca aplikacji tooyour odpowiedzi, w wartości hello używane dla `redirect_uri`. Używa metody hello określonej w hello `response_mode` parametru. odpowiedź Hello jest hello dokładnie tego samego dla każdego hello akcji scenariusze użytkowników, niezależnie od zasady hello, które zostało wykonane.

### <a name="successful-response"></a>Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie, która używa `response_mode=fragment` i `response_type=id_token+token` wygląda podobnie do następujących hello, podziały wiersza dla czytelności:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
```

| Parametr | Opis |
| --- | --- |
| ' access_token ' |token dostępu Hello hello żądanej aplikacji.  Nie można zdekodować lub w przeciwnym razie sprawdził Hello tokenu dostępu. Może być traktowana jako ciąg z ogólnym opisem. |
| token_type |wartość tokenu typu Hello. Hello tylko typ, czy obsługa usługi Azure AD jest elementu nośnego. |
| expires_in |Hello długość czasu, przez który hello token dostępu jest nieprawidłowy (w sekundach). |
| Zakres |zakresy Hello hello token jest prawidłowy dla. Możesz również używaj tokenów toocache zakresów do późniejszego użycia. |
| żądaniu |Witaj identyfikator token, aplikacja hello żądanie. Można użyć hello identyfikator tokenu tooverify hello tożsamości użytkownika i rozpocząć sesję użytkownika hello. Aby uzyskać więcej informacji o identyfikatorze tokeny i ich zawartość, zobacz hello [odwołania do tokenu usługi Azure AD B2C](active-directory-b2c-reference-tokens.md). |
| state |Jeśli `state` parametru jest częścią żądania hello hello tę samą wartość powinna być widoczna w odpowiedzi hello. Witaj aplikacji należy sprawdzić, że hello `state` wartości hello żądań i odpowiedzi są identyczne. |

### <a name="error-response"></a>Odpowiedzi na błąd
Odpowiedzi na błędy również mogą być wysyłane identyfikator URI przekierowania toohello tak, aby hello aplikacji można je odpowiednią obsługę:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parametr | Opis |
| --- | --- |
| error |Błąd kodu ciąg używany tooclassify typy występujące błędy. Również można użyć hello błąd kodu do obsługi błędów. |
| error_description |Komunikat o błędzie, który ułatwia identyfikowanie hello głównej przyczyny błędu uwierzytelniania. |
| state |Zobacz pełny opis hello w hello powyższej tabeli. Jeśli `state` parametru jest częścią żądania hello hello tę samą wartość powinna być widoczna w odpowiedzi hello. Witaj aplikacji należy sprawdzić, że hello `state` wartości hello żądań i odpowiedzi są identyczne.|

## <a name="validate-hello-id-token"></a>Sprawdź poprawność hello identyfikator tokenu
Odbieranie token identyfikator nie jest wystarczająco dużo tooauthenticate hello użytkownikiem. Musisz zweryfikować podpisu tokenu identyfikator hello i sprawdzić hello oświadczenia w tokenie hello na wymagania dotyczące Twojej aplikacji. Używa usługi Azure AD B2C [tokenów sieci Web JSON (Jwt)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) i publicznego klucza szyfrowania tokenów toosign i sprawdź, czy są prawidłowe.

Wiele open source biblioteki są dostępne sprawdzania poprawności tokenów Jwt, w zależności od języka hello wolisz toouse. Należy wziąć pod uwagę eksploracji dostępnych bibliotek open source, a nie implementacji logiki weryfikacji. Korzystając z informacji hello w toohelp tego artykułu dowiesz się, jak korzystać z tooproperly tych bibliotek.

Usługa Azure AD B2C ma punkt końcowy metadanych OpenID Connect. Aplikacja może używać hello punktu końcowego toofetch informacji o usłudze Azure AD B2C w czasie wykonywania. Informacje te obejmują punkty końcowe, zawartość tokenu i klucze podpisywania tokenu. Brak dokument metadanych JSON dla każdej zasady w dzierżawie usługi Azure AD B2C. Na przykład dokument metadanych hello hello b2c_1_sign_in zasad w dzierżawie fabrikamb2c.onmicrosoft.com hello jest w następującej lokalizacji:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Jedna z właściwości hello tego dokumentu konfiguracji jest hello `jwks_uri`. wartość Hello hello, które będą takie same zasady:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`

toodetermine zasady, które zostało używane toosign token identyfikator (i gdzie toofetch hello metadanych z), są dostępne dwie opcje. Najpierw hello zasad nazwa jest uwzględniona w hello `acr` oświadczeń w `id_token`. Informacje, jak tooparse hello oświadczeń z tokenu identyfikator, zobacz hello [odwołania do tokenu usługi Azure AD B2C](active-directory-b2c-reference-tokens.md). Drugą opcją jest zasad hello tooencode hello wartości hello `state` parametru w przypadku wysyłania żądania hello. Następnie dekodowania hello `state` toodetermine parametru zasady, które zostało użyte. Każda metoda jest prawidłowa.

Po zostały nabyte hello dokument metadanych z punktu końcowego metadanych hello OpenID Connect, należy użyć hello RSA 256 kluczy publicznych (znajdujące się w tym punkcie końcowym) toovalidate hello podpisu hello Identyfikatora tokenu. Może istnieć wiele kluczy wymienione w tym punkcie końcowym w dowolnym momencie, identyfikowanych przez `kid`. Nagłówek Hello `id_token` zawiera także `kid` oświadczeń. Oznacza to, które z tych kluczy została toosign używane hello identyfikator tokenu. Aby uzyskać więcej informacji, łącznie z zapoznawanie [sprawdzanie poprawności tokenów](active-directory-b2c-reference-tokens.md#token-validation), zobacz hello [odwołania do tokenu usługi Azure AD B2C](active-directory-b2c-reference-tokens.md).
<!--TODO: Improve hello information on this-->

Po weryfikacji podpisu hello hello identyfikator tokenu oświadczeń kilka Żądaj weryfikacji. Na przykład:

* Sprawdź poprawność hello `nonce` tooprevent ataków powtórzeń tokenów oświadczeń. Jego wartość powinna być określona w hello żądania logowania.
* Sprawdź poprawność hello `aud` oświadczeń tooensure, który hello identyfikator token został wystawiony dla aplikacji. Jego wartość powinna być identyfikator aplikacji hello aplikacji.
* Sprawdź poprawność hello `iat` i `exp` oświadczeń tooensure, który hello identyfikator token nie wygasł.

Kilka więcej operacji sprawdzania poprawności, które należy wykonać opisano szczegółowo w hello [OpenID Connect podstawowych specyfikacji](http://openid.net/specs/openid-connect-core-1_0.html). Można także toovalidate dodatkowe roszczenia, w zależności od danego scenariusza. Niektóre typowe operacje sprawdzania poprawności obejmują:

* Zapewnienie tego użytkownika hello lub organizacji po zarejestrowaniu aplikacji hello.
* Zapewnienie hello użytkownik ma odpowiednią autoryzacją i uprawnienia.
* Zapewnienie, że niektóre siły uwierzytelniania wystąpił, takie jak przy użyciu usługi Azure Multi-Factor Authentication.

Aby uzyskać więcej informacji na temat hello oświadczenia w tokenie identyfikator Zobacz hello [odwołania do tokenu usługi Azure AD B2C](active-directory-b2c-reference-tokens.md).

Po całkowicie poprawności hello identyfikator tokenu można rozpocząć sesji hello użytkownika. W aplikacji należy użyć oświadczeń hello hello identyfikator tokenu tooobtain informacje o hello użytkownika. Te informacje może służyć do wyświetlania, rekordy, autoryzacji i tak dalej.

## <a name="get-access-tokens"></a>Pobieranie tokenów dostępu
Jedyną operacją hello toodo potrzeb aplikacji sieci web jest wykonanie zasad, można pominąć hello kolejnych sekcjach kilku. informacje Hello w hello następujące sekcje są stosowane tylko aplikacje tooweb wymagające toomake uwierzytelnione wywołania tooa — interfejs API sieci web, a które są chronione przez usługę Azure AD B2C.

Teraz, gdy zostały podpisane hello użytkownika w aplikacji jednej strony tooyour, można uzyskać tokenów dostępu do sieci web wywoływania interfejsów API, które są zabezpieczone przez usługę Azure AD. Nawet jeśli już uzyskały tokenu przy użyciu hello `token` typ odpowiedzi można użyć tej metody tooacquire tokeny Aby uzyskać dodatkowe zasoby bez ponownie przekierowywanie hello toosign użytkownika w.

W typowej sieci web przepływu aplikacji, można to zrobić poprzez toohello żądania `/token` punktu końcowego.  Jednak hello punktu końcowego nie nie żądań CORPS pomocy technicznej, co AJAX wywołuje tooget i tokenów odświeżania nie jest opcją. Zamiast tego można użyć niejawnego przepływu hello w ukrytym HTML iframe element tooget nowe tokeny dla innych interfejsów API sieci web. Oto przykład podziałami wierszy dla czytelności:

```

https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
&response_mode=fragment
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
&p=b2c_1_sign_in
```

| Parametr | Wymagana? | Opis |
| --- | --- | --- |
| client_id |Wymagane |Identyfikator aplikacji Hello przypisany tooyour aplikacji w hello [portalu Azure](https://portal.azure.com). |
| response_type |Wymagane |Musi zawierać `id_token` OpenID Connect logowaniu.  Może również zawierać typ odpowiedzi hello `token`. Jeśli używasz `token` , aplikacja natychmiast może odbierać token dostępu z hello autoryzacji punktu końcowego, bez wprowadzania drugi toohello żądania punktu końcowego autoryzacji. Jeśli używasz hello `token` typ odpowiedzi, hello `scope` parametr musi zawierać zakres, który wskazuje, które token hello tooissue zasobów dla. |
| redirect_uri |Zalecane |Identyfikator URI aplikacji, gdzie można wysyłanych i odbieranych przez aplikację uwierzytelniania odpowiedzi przekierowania Hello. Go musi dokładnie odpowiadać jeden hello przekierowania URI zarejestrowany w portalu hello z tą różnicą, że musi być zakodowane w adresie URL. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów.  W przypadku uzyskiwania tokenów, zawiera wszystkie zakresy wymagające zasobu hello przeznaczone. |
| response_mode |Zalecane |Określa metodę hello, która jest używana toosend hello wynikowy tooyour tyłu tokenu aplikacji.  Może być `query`, `form_post`, lub `fragment`. |
| state |Zalecane |Wartość zawarte w żądaniu hello, który jest zwracany w odpowiedzi tokenu hello.  Można go ciągu zawartości, które mają toouse.  Zwykle jest używana wartość losowo generowany, unikatowy, okno fałszerstwie żądania międzywitrynowego tooprevent.  Stan Hello także jest używane tooencode informacji na temat stanu hello użytkownika w aplikacji hello, przed wystąpieniem hello żądanie uwierzytelnienia. Na przykład użytkownika hello hello stronę lub widok został na. |
| Identyfikator jednorazowy |Wymagane |Wartość zawarte w żądaniu hello, generowane przez aplikacji hello, który znajduje się w hello identyfikator tokenu jako oświadczenia.  Aplikacja Hello następnie sprawdzić, czy ataki powtórzeń tokenów toomitigate wartość. Zazwyczaj wartość hello jest losowe, unikatowy ciąg identyfikujący hello pochodzenia hello żądania. |
| wiersz |Wymagane |Użyj toorefresh i get tokenów w ukrytym iframe, `prompt=none` tooensure, który hello iframe nie zostać zablokowane na powitania strony logowania, a następnie zwraca natychmiast. |
| login_hint |Wymagane |toorefresh i get tokenów w ukrytym iframe, obejmują username hello hello użytkownika, w tym toodistinguish wskazówka między wiele sesji, który hello użytkownika może być w danym momencie. Można wyodrębnić hello username z wcześniejszych logowanie przy użyciu hello `preferred_username` oświadczeń. |
| domain_hint |Wymagane |Może być `consumers` lub `organizations`.  Odświeżanie i uzyskiwania tokenów w ukrytym iframe, musi zawierać hello `domain_hint` wartość w żądaniu hello.  Wyodrębnij hello `tid` oświadczeń z tokenu identyfikator hello wcześniej logowania toodetermine które toouse wartość.  Jeśli hello `tid` oświadczeń, wartość jest `9188040d-6c67-4c5b-b112-36a304b66dad`, użyj `domain_hint=consumers`.  W przeciwnym razie użyj `domain_hint=organizations`. |

Przez ustawienie hello `prompt=none` parametru tego żądania albo zakończy się pomyślnie lub natychmiast kończy się niepowodzeniem i zwraca tooyour aplikacji.  Odpowiedź oznaczająca Powodzenie wysłaniu tooyour aplikacji na wskazanych hello przekierowania URI, za pomocą metody hello określonej w hello `response_mode` parametru.

### <a name="successful-response"></a>Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie przy użyciu `response_mode=fragment` wygląda podobnie do następującej:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
```

| Parametr | Opis |
| --- | --- |
| ' access_token ' |Witaj token, aplikacja hello żądanie. |
| token_type |Typ tokenu Hello jest zawsze elementu nośnego. |
| state |Jeśli `state` parametru jest częścią żądania hello hello tę samą wartość powinna być widoczna w odpowiedzi hello. Witaj aplikacji należy sprawdzić, że hello `state` wartości hello żądań i odpowiedzi są identyczne. |
| expires_in |Jak długo hello token dostępu jest nieprawidłowy (w sekundach). |
| Zakres |nadaje się do zakresów Hello hello tokenu dostępu. |

### <a name="error-response"></a>Odpowiedzi na błąd
Odpowiedzi na błędy również mogą być wysyłane identyfikator URI przekierowania toohello tak, aby hello aplikacji można je odpowiednią obsługę.  Aby uzyskać `prompt=none`, oczekiwany błąd wygląda następująco:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu, które mogą być używane tooclassify typów błędów występujących. Można też użyć tooerrors tooreact ciąg hello. |
| error_description |Komunikat o błędzie, który ułatwia identyfikowanie hello głównej przyczyny błędu uwierzytelniania. |

Jeśli ten błąd jest wyświetlany w żądaniu iframe hello, hello użytkownika interakcyjnie zalogować ponownie tooretrieve nowy token. Problem można rozwiązać w taki sposób, który ma sens dla aplikacji.

## <a name="refresh-tokens"></a>Tokenów odświeżania
Tokeny Identyfikatora i tokenów dostępu wygasają po krótkim czasie. Aplikację należy przygotować toorefresh te tokeny okresowo.  wykonania dowolnego typu tokenu, toorefresh hello jednym żądaniu ukryte iframe zostały użyte podczas wcześniejszego przykładu, za pomocą hello `prompt=none` parametru kroki toocontrol usługi Azure AD.  tooreceive nowy `id_token` wartość, należy się toouse `response_type=id_token` i `scope=openid`, a `nonce` parametru.

## <a name="send-a-sign-out-request"></a>Wyślij żądanie wylogowania
Użytkownik hello toosign poza aplikacją hello, należy przekierować hello użytkownika tooAzure AD toosign limit. Jeśli nie zrobisz, hello użytkownika może być możliwe tooreauthenticate tooyour aplikacji bez konieczności ponownego wprowadzania poświadczeń. Jest tak, ponieważ mają one nieprawidłowy jednej logowania jednokrotnego sesji z usługą Azure AD.

Można przekierowywać po prostu hello użytkownika toohello `end_session_endpoint` oznacza to wymienione w hello samego dokumentu metadanych OpenID Connect opisanego w [weryfikacji hello identyfikator tokenu](#validate-the-id-token). Na przykład:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Parametr | Wymagana? | Opis |
| --- | --- | --- |
| P |Wymagane |Witaj zasad toouse toosign hello użytkownika z aplikacji. |
| post_logout_redirect_uri |Zalecane |Witaj adres URL tego użytkownika hello powinien być przekierowanego tooafter pomyślnie wylogowania. Jeśli nie zostanie włączony, usługi Azure AD B2C wyświetla komunikat ogólny toohello użytkownika. |

> [!NOTE]
> Kierowanie hello użytkownika toohello `end_session_endpoint` czyści niektóre użytkownika hello pojedynczego logowania jednokrotnego stanu z usługi Azure AD B2C. Jednak nie go podpisać hello użytkownika z sesji dostawcy tożsamości społecznościowych hello użytkownika. Jeśli hello użytkownik wybiera hello dostawcy sam identyfikację podczas kolejnych logowanie, hello użytkownika jest ponownie uwierzytelnić bez wprowadzania poświadczeń. Jeśli użytkownik chce toosign poza aplikacji usługi Azure AD B2C, go nie musi oznaczać, że chcą toocompletely Wyloguj swojego konta usługi Facebook, na przykład. Jednak dla kont lokalnych hello sesja zostanie zakończona poprawnie.
> 
> 

## <a name="use-your-own-azure-ad-b2c-tenant"></a>Użyj dzierżawy usługi Azure AD B2C
tootry żądań użytkownika, je ukończyć powitalnych następujące trzy kroki. Zastąp hello przykładowe wartości używanej w tym artykule i własne wartości:

1. [Tworzenie dzierżawy usługi Azure AD B2C](active-directory-b2c-get-started.md). Użyj nazwy hello dzierżawy w żądaniach hello.
2. [Tworzenie aplikacji](active-directory-b2c-app-registration.md) tooobtain identyfikator aplikacji i `redirect_uri` wartość. Uwzględnij aplikację sieci web lub interfejsu API sieci web w aplikacji. Opcjonalnie możesz utworzyć klucz tajny aplikacji.
3. [Tworzenie zasad](active-directory-b2c-reference-policies.md) tooobtain nazwy zasad.

## <a name="samples"></a>Przykłady

* [Tworzenie aplikacji jednej strony przy użyciu środowiska Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi)
* [Tworzenie aplikacji jednej strony przy użyciu programu .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi)

