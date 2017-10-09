---
title: "Przepływu kodu autoryzacji — usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toobuild web apps za pomocą protokołu uwierzytelniania usługi Azure AD B2C i OpenID Connect."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6bf9d37310bd45b39bda346441413556f9fd4fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a>Azure Active Directory B2C: Przepływu kodu autoryzacji protokołu OAuth 2.0
W aplikacji zainstalowanych na urządzeniu toogain dostępu tooprotected zasoby, takie jak interfejsów API sieci web służy udzielania kodu autoryzacji hello OAuth 2.0. Przy użyciu hello Azure Active Directory B2C (Azure AD B2C) stosowania OAuth 2.0, można dodać rejestrację, logowanie i Zarządzanie tożsamościami, inne zadania tooyour aplikacji mobilnych i klasycznych. W tym artykule jest niezależny od języka. W artykule hello opisano sposób toosend i odbieranie wiadomości HTTP bez korzystania z żadnych bibliotek open source.

<!-- TODO: Need link toolibraries -->

Witaj przepływu kodu autoryzacji protokołu OAuth 2.0 jest opisany w [sekcji 4.1 specyfikacji hello OAuth 2.0](http://tools.ietf.org/html/rfc6749). Służy do uwierzytelniania i autoryzacji w większości typów aplikacji, w tym [sieci web apps](active-directory-b2c-apps.md#web-apps) i [natywnie zainstalowane aplikacje](active-directory-b2c-apps.md#mobile-and-native-apps). Można użyć hello OAuth 2.0 uzyskać toosecurely przepływu kodu autoryzacji *tokenów dostępu* dla aplikacji, które mogą być używane tooaccess zasoby, które są zabezpieczone przez [serwera autoryzacji](active-directory-b2c-reference-protocols.md#the-basics).

Ten artykuł skupia się na powitania **klientów publicznych** przepływu kodu autoryzacji protokołu OAuth 2.0. Publiczny klient jest w dowolnej aplikacji klienta, która nie może być zaufane toosecurely zachowanie spójności hello tajnego hasła. Obejmuje to aplikacje mobilne, aplikacje komputerowe i zasadniczo dowolnej aplikacji, która jest uruchamiana na urządzeniu i musi tooget tokenów dostępu. 

> [!NOTE]
> tooadd tożsamości zarządzania tooa aplikacji sieci web przy użyciu usługi Azure AD B2C, użyj [OpenID Connect](active-directory-b2c-reference-oidc.md) zamiast protokołu OAuth 2.0.

Usługa Azure AD B2C rozszerza standardowej hello przepływu OAuth 2.0 toodo więcej niż prostego uwierzytelniania i autoryzacji. Podaj hello [parametru zasad](active-directory-b2c-reference-policies.md). Wbudowane zasady, możesz zastosować OAuth 2.0 użytkownika tooadd napotyka tooyour aplikacji, takich jak konta, logowania i zarządzania profilami. W tym artykule zostanie przedstawiony zostanie sposób tooimplement OAuth 2.0 i zasady toouse każdego z tych napotka w natywnej aplikacji. Możemy również przedstawiają sposób jest tooget tokenów dostępu do uzyskiwania dostępu do interfejsów API sieci web.

W żądaniach HTTP przykład hello w tym artykule, korzystamy z naszych katalog usługi Azure AD B2C przykładu **fabrikamb2c.onmicrosoft.com**. Możemy również użyć naszych przykładowej aplikacji i zasad. Można spróbować żądań hello samodzielnie przy użyciu tych wartości, lub należy je zastąpić własne wartości.
Dowiedz się, jak za[uzyskać własnego katalogu usługi Azure AD B2C, aplikacji i zasad](#use-your-own-azure-ad-b2c-directory).

## <a name="1-get-an-authorization-code"></a>1. Pobierz kod autoryzacji
przepływu kodu autoryzacji Hello rozpoczyna się od klienta hello kierowanie hello użytkownika toohello `/authorize` punktu końcowego. Jest to hello interakcyjne część przepływu hello, gdzie hello użytkownik wykona akcję. W tym żądaniu powitania klienta wskazuje w hello `scope` uprawnienia hello parametru musi tooacquire hello użytkownika. W hello `p` parametr wskazuje hello tooexecute zasad. Witaj następujące trzy przykłady można podać (podziałów wierszy dla czytelności) każdego użyć różnych zasad.

### <a name="use-a-sign-in-policy"></a>Użyj zasad logowania
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Użyj zasad rejestracji
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Użyj zasad edycji profilu
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| Parametr | Wymagana? | Opis |
| --- | --- | --- |
| client_id |Wymagane |Identyfikator aplikacji Hello przypisany tooyour aplikacji w hello [portalu Azure](https://portal.azure.com). |
| response_type |Wymagane |Typ odpowiedzi Hello, który musi zawierać `code` dla przepływu kodu autoryzacji hello. |
| redirect_uri |Wymagane |Identyfikator URI aplikacji, w którym wysyłanych i odbieranych przez aplikację uwierzytelniania odpowiedzi przekierowania Hello. Go musi dokładnie odpowiadać jeden hello przekierowania URI, który został zarejestrowany w portalu hello z tą różnicą, że musi być zakodowane w adresie URL. |
| Zakres |Wymagane |Rozdzieloną spacjami listę zakresów. Wartość pojedynczy zakres wskazuje tooAzure usługi Active Directory (Azure AD) zarówno hello uprawnień, które są żądane. Za pomocą Identyfikatora jak zakres hello wskazuje, że Twoja aplikacja powinna tokenu dostępu, który można użyć w odniesieniu do własnych usług lub web API, reprezentowany przez klienta hello hello tego samego identyfikatora klienta.  Witaj `offline_access` zakresu wskazuje, że aplikacja wymaga token odświeżania dla tooresources długotrwałe dostępu. Można też użyć hello `openid` toorequest zakres Identyfikatora tokenu z usługi Azure AD B2C. |
| response_mode |Zalecane |Metoda Hello czy użyć toosend hello wynikowy autoryzacji kodu wstecz tooyour aplikacji. Można ją `query`, `form_post`, lub `fragment`. |
| state |Zalecane |Wartość zawarte w żądaniu hello, który jest zwracany w odpowiedzi tokenu hello. Można go ciągu zawartości, które mają toouse. Zwykle jest używana wartość losowo generowany unikatowy, okno fałszerstwie żądania międzywitrynowego tooprevent. Stan Hello także jest używane tooencode informacji na temat stanu hello użytkownika w aplikacji hello, przed wystąpieniem hello żądanie uwierzytelnienia. Na przykład użytkownika hello strony hello na lub hello zasad, które było wykonywane. |
| P |Wymagane |zasady Hello, która jest wykonywana. Jego hello nazwę zasad, który jest tworzony w katalogu usługi Azure AD B2C. wartość Nazwa zasad Hello powinny rozpoczynać się od **b2c\_1\_**. toolearn więcej informacji na temat zasad, zobacz [wbudowane zasady usługi Azure AD B2C](active-directory-b2c-reference-policies.md). |
| wiersz |Optional (Opcjonalność) |Typ Hello interakcji z użytkownikiem, który jest wymagany. Obecnie jest jedyną poprawną wartością hello `login`, która wymusza hello tooenter użytkownika poświadczeń dla tego żądania. Logowanie jednokrotne nie zacznie obowiązywać. |

W tym momencie hello użytkownik jest proszony toocomplete hello zasad przepływu pracy. Może to obejmować użytkownika hello wprowadzić swoją nazwę użytkownika i hasło, zalogować się społecznościowych tożsamości, podczas tworzenia katalogu hello lub dowolnej liczby kroków. Akcje użytkownika zależą od tego, jak zdefiniowano hello zasad.

Po zakończeniu zasad hello hello użytkownika usługi Azure AD zwraca aplikacji tooyour odpowiedzi, w wartości hello używane dla `redirect_uri`. Używa metody hello określonej w hello `response_mode` parametru. odpowiedź Hello jest hello dokładnie tego samego dla każdego hello akcji scenariusze użytkowników, niezależnie od zasady hello, które zostało wykonane.

Odpowiedź oznaczająca Powodzenie, która używa `response_mode=query` wygląda podobnie do następującej:

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // hello authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // hello value provided in hello request
```

| Parametr | Opis |
| --- | --- |
| Kod |Kod autoryzacji Hello hello żądanej aplikacji. Aplikacja Hello służy toorequest kod autoryzacji hello tokenu dostępu dla zasobu docelowego. Kody autoryzacji są bardzo krótkim okresie. Zazwyczaj wygasną po około 10 minut. |
| state |Zobacz pełny opis hello w tabeli hello w powyższej sekcji hello. Jeśli `state` parametru jest częścią żądania hello hello tę samą wartość powinna być widoczna w odpowiedzi hello. Witaj aplikacji należy sprawdzić, że hello `state` wartości hello żądań i odpowiedzi są identyczne. |

Odpowiedzi na błędy również mogą być wysyłane identyfikator URI przekierowania toohello tak, aby hello aplikacji można je odpowiednią obsługę:

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu, który można używać typów hello tooclassify występujące błędy. Można też użyć tooerrors tooreact ciąg hello. |
| error_description |Komunikat o błędzie, który ułatwia identyfikowanie hello głównej przyczyny błędu uwierzytelniania. |
| state |Zobacz pełny opis hello w hello powyższej tabeli. Jeśli `state` parametru jest częścią żądania hello hello tę samą wartość powinna być widoczna w odpowiedzi hello. Witaj aplikacji należy sprawdzić, że hello `state` wartości hello żądań i odpowiedzi są identyczne. |

## <a name="2-get-a-token"></a>2. Uzyskaj token
Teraz, gdy zostały nabyte kod autoryzacji, możesz zrealizować hello `code` dla tokenu toohello zasobów, które wysyłając toohello żądania POST `/token` punktu końcowego. W usłudze Azure AD B2C hello tylko tych zasobów, jakiej może żądać tokenu dla jest własnych aplikacji zaplecza interfejsu API sieci web. Konwencja Hello, która jest używana dla żądania tokenu tooyourself jest toouse identyfikator klienta aplikacji jako zakres hello:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| Parametr | Wymagana? | Opis |
| --- | --- | --- |
| P |Wymagane |Witaj zasad, które były używane tooacquire hello autoryzacji kodu. Nie można użyć różnych zasad w tym żądaniu. Uwaga dodanie tego parametru toohello *ciągu zapytania*, a nie w hello treść wpisu. |
| client_id |Wymagane |Identyfikator aplikacji Hello przypisany tooyour aplikacji w hello [portalu Azure](https://portal.azure.com). |
| Typ grant_type |Wymagane |Typ Hello grant. Witaj przepływu kodu autoryzacji, musi być typu przydziału hello `authorization_code`. |
| Zakres |Zalecane |Rozdzieloną spacjami listę zakresów. Wartość pojedynczy zakres wskazuje tooAzure AD zarówno hello uprawnienia, które są żądane. Za pomocą Identyfikatora jak zakres hello wskazuje, że Twoja aplikacja powinna tokenu dostępu, który można użyć w odniesieniu do własnych usług lub web API, reprezentowany przez klienta hello hello tego samego identyfikatora klienta.  Witaj `offline_access` zakresu wskazuje, że aplikacja wymaga token odświeżania dla tooresources długotrwałe dostępu.  Można też użyć hello `openid` toorequest zakres Identyfikatora tokenu z usługi Azure AD B2C. |
| Kod |Wymagane |Kod autoryzacji Hello uzyskanego w hello pierwszego etap hello przepływu. |
| redirect_uri |Wymagane |Identyfikator URI aplikacji hello gdzie otrzymany kod autoryzacji hello przekierowania Hello. |

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
| token_type |wartość tokenu typu Hello. Hello tylko typ, czy obsługa usługi Azure AD jest elementu nośnego. |
| ' access_token ' |Witaj podpisany JSON Web Token (JWT) żądanych. |
| Zakres |zakresy Hello hello token jest prawidłowy dla. Możesz również używaj tokenów toocache zakresów do późniejszego użycia. |
| expires_in |Hello długość czasu, przez który hello token jest prawidłowy (w sekundach). |
| refresh_token |Token odświeżania OAuth 2.0. Aplikacja Hello można użyć tego tokenu tooacquire dodatkowe tokeny, po wygaśnięciu tokenu bieżącego hello. Tokeny odświeżania są długotrwałe. Można używać tooresources dostępu tooretain ich przez dłuższy czas. Aby uzyskać więcej informacji, zobacz hello [odwołania do tokenu usługi Azure AD B2C](active-directory-b2c-reference-tokens.md). |

Odpowiedzi na błędy wyglądać następująco:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu, który można używać typów hello tooclassify występujące błędy. Można też użyć tooerrors tooreact ciąg hello. |
| error_description |Komunikat o błędzie, który ułatwia identyfikowanie hello głównej przyczyny błędu uwierzytelniania. |

## <a name="3-use-hello-token"></a>3. Użyj tokenu hello
Teraz, zostały pomyślnie uzyskano tokenu dostępu, można hello token w żądań tooyour zaplecza interfejsów API sieci web przez dołączenie go do hello `Authorization` nagłówka:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-hello-token"></a>4. Odśwież hello tokenu
Tokeny dostępu i identyfikator tokeny są krótkim okresie. Po wygasną, należy je odświeżyć toocontinue tooaccess zasobów. toodo to, przesłać innego toohello żądania POST `/token` punktu końcowego. Teraz, podaj hello `refresh_token` zamiast hello `code`:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| Parametr | Wymagana? | Opis |
| --- | --- | --- |
| P |Wymagane |Hello zasady, które zostało tooacquire używane hello oryginalnego token odświeżania. Nie można użyć różnych zasad w tym żądaniu. Uwaga dodanie tego parametru toohello *ciągu zapytania*, a nie w hello treść wpisu. |
| client_id |Zalecane |Identyfikator aplikacji Hello przypisany tooyour aplikacji w hello [portalu Azure](https://portal.azure.com). |
| Typ grant_type |Wymagane |Typ Hello grant. Ten etap przepływu kodu autoryzacji hello musi być typu przydziału hello `refresh_token`. |
| Zakres |Zalecane |Rozdzieloną spacjami listę zakresów. Wartość pojedynczy zakres wskazuje tooAzure AD zarówno hello uprawnienia, które są żądane. Za pomocą Identyfikatora jak zakres hello wskazuje, że Twoja aplikacja powinna tokenu dostępu, który można użyć w odniesieniu do własnych usług lub web API, reprezentowany przez klienta hello hello tego samego identyfikatora klienta.  Witaj `offline_access` zakresu wskazuje, że aplikacja będzie potrzebny token odświeżania tooresources długotrwałe dostępu.  Można też użyć hello `openid` toorequest zakres Identyfikatora tokenu z usługi Azure AD B2C. |
| redirect_uri |Optional (Opcjonalność) |Identyfikator URI aplikacji hello gdzie otrzymany kod autoryzacji hello przekierowania Hello. |
| refresh_token |Wymagane |Witaj oryginalnego token odświeżania uzyskanego w drugi etap hello hello przepływu. |

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
| token_type |wartość tokenu typu Hello. Hello tylko typ, czy obsługa usługi Azure AD jest elementu nośnego. |
| ' access_token ' |Hello podpisany token JWT, którego zażądano. |
| Zakres |zakresy Hello hello token jest prawidłowy dla. Możesz również używaj tokenów toocache zakresy hello do późniejszego użycia. |
| expires_in |Hello długość czasu, przez który hello token jest prawidłowy (w sekundach). |
| refresh_token |Token odświeżania OAuth 2.0. Aplikacja Hello można użyć tego tokenu tooacquire dodatkowe tokeny, po wygaśnięciu tokenu bieżącego hello. Odśwież tokeny są to długotrwałe i mogą być używane tooretain tooresources dostępu przez dłuższy czas. Aby uzyskać więcej informacji, zobacz hello [odwołania do tokenu usługi Azure AD B2C](active-directory-b2c-reference-tokens.md). |

Odpowiedzi na błędy wyglądać następująco:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu, który można używać typów tooclassify występujące błędy. Można też użyć tooerrors tooreact ciąg hello. |
| error_description |Komunikat o błędzie, który ułatwia identyfikowanie hello głównej przyczyny błędu uwierzytelniania. |

## <a name="use-your-own-azure-ad-b2c-directory"></a>Użyj katalogu usługi Azure AD B2C
tootry te żądania samodzielnie pełną hello następujące kroki. Zastąp hello przykładowe wartości, używane w tym artykule i własne wartości.

1. [Utwórz katalog usługi Azure AD B2C](active-directory-b2c-get-started.md). Użyj nazwy hello katalogu w żądaniach hello.
2. [Tworzenie aplikacji](active-directory-b2c-app-registration.md) tooobtain identyfikator aplikacji i identyfikator URI przekierowania. Uwzględnij klienta natywnego w aplikacji.
3. [Tworzenie zasad](active-directory-b2c-reference-policies.md) tooobtain nazwy zasad.

