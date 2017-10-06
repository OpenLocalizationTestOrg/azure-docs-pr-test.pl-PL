---
title: "aaaLearn o inny token hello i typy obsługiwane przez usługę Azure AD | Dokumentacja firmy Microsoft"
description: "Przewodnik dla opis i ocena oświadczeń hello hello SAML 2.0 i tokenów sieci Web JSON (JWT) tokeny wystawione przez usługi Azure Active Directory (AAD)"
documentationcenter: na
author: dstrockis
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 166aa18e-1746-4c5e-b382-68338af921e2
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: c512894476613e94d86a994c32a8459d6cf00fbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-token-reference"></a>Odwołania do usługi Azure AD tokenu
Azure Active Directory (Azure AD) emituje kilka typów tokenów zabezpieczających hello przetwarzania każdego przepływu uwierzytelniania. W tym dokumencie opisano hello format, właściwości zabezpieczeń i zawartości każdego typu tokenu.

## <a name="types-of-tokens"></a>Typy tokenów
Usługi Azure AD obsługuje hello [protokół OAuth 2.0](active-directory-protocols-oauth-code.md), który wykorzystuje access_tokens i refresh_tokens.  Obsługuje ona również uwierzytelniania i logowania za pomocą [OpenID Connect](active-directory-protocols-openid-connect-code.md), które wprowadza trzeci typ tokenu, hello żądaniu.  Każdy z tych tokenów jest reprezentowany jako "bearer token".

Token elementu nośnego jest token zabezpieczający lekkie, że przyznaje hello tooa dostępu "bearer" chronionych zasobów. W tym sensie "bearer" hello jest każda strona, która może ona powodować hello tokenu. Chociaż uwierzytelniania za pomocą usługi Azure AD jest wymagany w kolejności tooreceive tokenu elementu nośnego, należy przedsięwziąć toosecure hello tokenu, tooprevent przechwytywaniu niezamierzone strony. Ponieważ tokenów elementu nośnego nie ma strony tooprevent nieautoryzowany wbudowany mechanizm, ich użycie, musi być transportowane w bezpiecznego kanału, takie jak zabezpieczeń warstwy transportu (HTTPS). Jeśli token elementu nośnego jest przesyłany w hello Wyczyść, środkowej atak powitania man-in można tooacquire używane hello token i uzyskania nieautoryzowanego dostępu tooa chronionych zasobów. Witaj te same zasady zabezpieczeń mają zastosowanie po zapisaniu lub buforowanie tokenów elementu nośnego do późniejszego użycia. Zawsze upewnij się, że aplikacja przesyła i przechowuje tokenów elementu nośnego w bezpieczny sposób. Aby uzyskać więcej zagadnienia dotyczące zabezpieczeń na tokenów elementu nośnego, zobacz [RFC 6750 sekcji 5](http://tools.ietf.org/html/rfc6750).

Wiele tokenów hello wystawiony przez usługę Azure AD są zaimplementowane jako tokenów sieci Web JSON lub tokenów Jwt.  Token JWT jest compact, adres URL bezpiecznego sposób przekazywania informacji między dwiema stronami.  Hello informacje zawarte w Jwt są określane jako "oświadczenia", lub potwierdzenia informacji o elementu nośnego hello i temat hello tokenu.  oświadczenia Hello w Jwt są obiektów JSON, kodowania i serializację do transmisji.  Ponieważ hello Jwt wystawione przez usługę Azure AD jest podpisany, ale nie są szyfrowane, możesz łatwo sprawdzić zawartość hello token JWT na potrzeby debugowania.  Istnieje kilka narzędzi w ten sposób, takich jak [jwt.calebb.net](http://jwt.calebb.net). Aby uzyskać więcej informacji dotyczących tokenów Jwt, może się odwoływać toohello [specyfikacji JWT](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html).

## <a name="idtokens"></a>Id_tokens
Id_tokens są w formie tokenów zabezpieczających logowania aplikacji otrzymuje podczas uwierzytelniania przy użyciu [OpenID Connect](active-directory-protocols-openid-connect-code.md).  Są one reprezentowane jako [Jwt](#types-of-tokens)i może zawierać oświadczenia, które służy do podpisywania hello użytkownika w aplikacji.  Można użyć oświadczeń hello w żądaniu, zgodnie z własnymi potrzebami — zwykle są używane do wyświetlania informacji o koncie lub podejmowania decyzji dotyczących kontroli dostępu w aplikacji.

Id_tokens jest podpisany, ale nie są szyfrowane w tej chwili.  Gdy aplikacja odbiera żądaniu, musi ona [sprawdzanie poprawności podpisu hello](#validating-tokens) tooprove hello autentyczności tokenu i zweryfikować kilka oświadczenia w hello token tooprove jego ważności.  Witaj oświadczeń zweryfikowany przez aplikację się różnić w zależności od wymagań scenariusza, ale w przypadku niektórych [typowych operacji sprawdzania poprawności oświadczeń](#validating-tokens) który aplikacji należy wykonać w każdym scenariuszu.

Zobacz powitania po sekcji informacji o id_tokens oświadczeń, a także żądaniu próbki.  Należy pamiętać, że oświadczenia hello w id_tokens nie są zwracane w określonej kolejności.  Ponadto nowych oświadczeń może być wprowadzane do id_tokens w dowolnym momencie w czasie — aplikacji nie powinna zostać podzielona na miarę wprowadzania nowych oświadczeń.  Witaj Poniższa lista zawiera hello oświadczenia, które aplikacji można niezawodnie interpretacji w czasie hello pisania tego dokumentu.  Jeśli to konieczne, nawet więcej szczegółów można znaleźć w hello [OpenID Connect specyfikacji](http://openid.net/specs/openid-connect-core-1_0.html).

#### <a name="sample-idtoken"></a>Przykładowe żądaniu
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ.
```

> [!TIP]
> Praktyki, spróbuj sprawdzania oświadczeń hello w żądaniu próbki hello przez wklejenie go do [calebb.net](http://jwt.calebb.net).
> 
> 

#### <a name="claims-in-idtokens"></a>Oświadczenia w id_tokens
> [!div class="mx-codeBreakAll"]
| Token JWT oświadczeń | Nazwa | Opis |
| --- | --- | --- |
| `appid` |Identyfikator aplikacji |Identyfikuje aplikacji hello, która używa tokenu tooaccess hello zasobu. Aplikacja Hello może działać jako sam lub w imieniu użytkownika. Identyfikator aplikacji Hello zazwyczaj reprezentuje obiekt aplikacji, ale może także reprezentować obiekt główny usługi w usłudze Azure AD. <br><br> **Przykładowa wartość JWT**: <br> `"appid":"15CB020F-3984-482A-864D-1D92265E8268"` |
| `aud` |Grupy odbiorców |Witaj przeznaczony odbiorcy tokenu hello. Aplikacja Hello, która odbiera hello token należy sprawdzić, czy wartość odbiorców hello jest poprawny i odrzucić wszystkie tokeny przeznaczona dla różnych użytkowników. <br><br> **Przykładowa wartość SAML**: <br> `<AudienceRestriction>`<br>`<Audience>`<br>`https://contoso.com`<br>`</Audience>`<br>`</AudienceRestriction>` <br><br> **Przykładowa wartość JWT**: <br> `"aud":"https://contoso.com"` |
| `appidacr` |Application Authentication Context Class Reference |Wskazuje, jak została uwierzytelniona powitania klienta. Dla publicznych klienta hello wartość to 0. Jeśli identyfikator klienta i klucz tajny klienta są używane, hello wartość to 1. <br><br> **Przykładowa wartość JWT**: <br> `"appidacr": "0"` |
| `acr` |Authentication Context Class Reference |Wskazuje, jak został uwierzytelniony podmiot hello, jako klient min. toohello hello Application Authentication Context Class Reference oświadczenia. Wartość "0" oznacza, że uwierzytelnianie użytkownika końcowego hello nie spełnia wymagań hello z normą ISO/IEC 29115. <br><br> **Przykładowa wartość JWT**: <br> `"acr": "0"` |
| Błyskawiczne uwierzytelniania |Rejestruje hello daty i godziny po przeprowadzeniu uwierzytelnienia. <br><br> **Przykładowa wartość SAML**: <br> `<AuthnStatement AuthnInstant="2011-12-29T05:35:22.000Z">` | |
| `amr` |Metoda uwierzytelniania |Określa, jak został uwierzytelniony podmiot hello hello tokenu. <br><br> **Przykładowa wartość SAML**: <br> `<AuthnContextClassRef>`<br>`http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod/password`<br>`</AuthnContextClassRef>` <br><br> **Przykładowa wartość JWT**:`“amr”: ["pwd"]` |
| `given_name` |Imię |Udostępnia hello najpierw lub "podany" Nazwa użytkownika, powitalne, zgodnie z ustaleniami obiektu użytkownika hello Azure AD. <br><br> **Przykładowa wartość SAML**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname”>`<br>`<AttributeValue>Frank<AttributeValue>` <br><br> **Przykładowa wartość JWT**: <br> `"given_name": "Frank"` |
| `groups` |Grupy |Zawiera identyfikatory obiektu, które reprezentują członkostwa w grupach hello podmiotu. Te wartości są unikatowe (patrz obiektu o identyfikatorze) i bezpiecznie umożliwia zarządzanie dostępem, takie jak wymuszanie autoryzacji tooaccess zasobu. Hello grup objętych oświadczenia grupy hello są konfigurowane na poszczególnych aplikacji, za pośrednictwem właściwości "groupMembershipClaims" hello manifest aplikacji hello. Wartość null powoduje wyłączenie wszystkich grup, wartość "SecurityGroup" będzie zawierać tylko członkostwa grupy zabezpieczeń usługi Active Directory, a wartość "All" będzie zawierać grup zabezpieczeń i listami dystrybucyjnymi usługi Office 365. <br><br> **Przykładowa wartość SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">`<br>`<AttributeValue>07dd8a60-bf6d-4e17-8844-230b77145381</AttributeValue>` <br><br> **Przykładowa wartość JWT**: <br> `“groups”: ["0e129f5b-6b0a-4944-982d-f776045632af", … ]` |
| `idp` |Dostawca tożsamości |Rejestruje hello dostawcy tożsamości, który uwierzytelniony podmiot hello hello tokenu. Ta wartość jest wartością toohello identyczne Witaj wystawca oświadczeń, chyba że konto użytkownika hello jest w innej dzierżawie niż Witaj Wystawca. <br><br> **Przykładowa wartość SAML**: <br> `<Attribute Name=” http://schemas.microsoft.com/identity/claims/identityprovider”>`<br>`<AttributeValue>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/<AttributeValue>` <br><br> **Przykładowa wartość JWT**: <br> `"idp":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `iat` |IssuedAt |Przechowuje hello czasu, w którym hello token został wystawiony. Jest często używane toomeasure świeżości tokenu. <br><br> **Przykładowa wartość SAML**: <br> `<Assertion ID="_d5ec7a9b-8d8f-4b44-8c94-9812612142be" IssueInstant="2014-01-06T20:20:23.085Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">` <br><br> **Przykładowa wartość JWT**: <br> `"iat": 1390234181` |
| `iss` |Wystawcy |Identyfikuje hello usługi tokenu zabezpieczającego (STS) tworzy i zwraca hello token. W tokenach hello, które zwraca usługi Azure AD Witaj wystawca jest sts.windows.net. Hello identyfikator GUID w wartości oświadczenia wystawcy hello jest identyfikator dzierżawcy hello hello katalogu Azure AD. Identyfikator dzierżawy Hello jest identyfikatorem niezmienne i niezawodne hello katalogu. <br><br> **Przykładowa wartość SAML**: <br> `<Issuer>https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/</Issuer>` <br><br> **Przykładowa wartość JWT**: <br>  `"iss":”https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/”` |
| `family_name` |Nazwisko |Umożliwia hello nazwisko, nazwisko lub nazwisko użytkownika hello, zgodnie z definicją w obiekcie użytkownika usługi Azure AD hello. <br><br> **Przykładowa wartość SAML**: <br> `<Attribute Name=” http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname”>`<br>`<AttributeValue>Miller<AttributeValue>` <br><br> **Przykładowa wartość JWT**: <br> `"family_name": "Miller"` |
| `unique_name` |Nazwa |Udostępnia człowieka wartość do odczytu, która identyfikuje podmiotu hello hello tokenu. Ta wartość nie jest gwarantowana toobe unikatowa w ramach dzierżawcy i jest zaprojektowana toobe używana tylko do wyświetlania. <br><br> **Przykładowa wartość SAML**: <br> `<Attribute Name=”http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name”>`<br>`<AttributeValue>frankm@contoso.com<AttributeValue>` <br><br> **Przykładowa wartość JWT**: <br> `"unique_name": "frankm@contoso.com"` |
| `oid` |Identyfikator obiektu: |Zawiera unikatowy identyfikator obiektu w usłudze Azure AD. Ta wartość jest niezmienne i nie można ponownie przypisać lub ponownie. Użyj tooidentify identyfikator obiektu hello obiektu w tooAzure zapytań AD. <br><br> **Przykładowa wartość SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">`<br>`<AttributeValue>528b2ac2-aa9c-45e1-88d4-959b53bc7dd0<AttributeValue>` <br><br> **Przykładowa wartość JWT**: <br> `"oid":"528b2ac2-aa9c-45e1-88d4-959b53bc7dd0"` |
| `roles` |Role |Reprezentuje wszystkie role aplikacji hello temat zostały przyznane bezpośrednio i pośrednio przez przynależność do grupy i mogą być używane tooenforce opartej na rolach kontrola dostępu. Role aplikacji są zdefiniowane na podstawie poszczególnych aplikacji, za pomocą hello `appRoles` właściwości hello w manifeście aplikacji. Witaj `value` właściwości każdej roli aplikacji jest hello wartość, która jest wyświetlana w hello ról oświadczeń. <br><br> **Przykładowa wartość SAML**: <br> `<Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/role">`<br>`<AttributeValue>Admin</AttributeValue>` <br><br> **Przykładowa wartość JWT**: <br> `“roles”: ["Admin", … ]` |
| `scp` |Zakres |Wskazuje hello personifikacji uprawnienia nadanego toohello aplikacji klienckiej. Witaj domyślne uprawnienia `user_impersonation`. Właściciel Hello hello zabezpieczonych zasobów można zarejestrować dodatkowych wartości w usłudze Azure AD. <br><br> **Przykładowa wartość JWT**: <br> `"scp": "user_impersonation"` |
| `sub` |Temat |Identyfikuje hello podmiot zabezpieczeń, o których hello token deklaracji rozkazujących informacje, takie jak hello użytkownik aplikacji. Ta wartość jest niezmienne i nie może zostać przypisany lub używane ponownie, więc może być używane tooperform sprawdzeń autoryzacji bezpiecznie. Ponieważ podmiotu hello zawsze znajduje się w hello tokeny hello Azure AD problemów, firma Microsoft zaleca korzystanie z tej wartości w systemie autoryzacji ogólnego przeznaczenia. <br> `SubjectConfirmation`nie jest oświadczenie. Opisuje sposób hello przedmiotem hello token jest weryfikowany. `Bearer`Wskazuje, że tego podmiotu hello potwierdza zapoznały hello tokenu. <br><br> **Przykładowa wartość SAML**: <br> `<Subject>`<br>`<NameID>S40rgb3XjhFTv6EQTETkEzcgVmToHKRkZUIsJlmLdVc</NameID>`<br>`<SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />`<br>`</Subject>` <br><br> **Przykładowa wartość JWT**: <br> `"sub":"92d0312b-26b9-4887-a338-7b00fb3c5eab"` |
| `tid` |Identyfikator dzierżawy |Identyfikator niezmienne, jednorazowego, który identyfikuje hello katalogu dzierżawy, który wystawił hello tokenu. Zasobów katalogu specyficznego dla dzierżawy tooaccess tej wartości można użyć w aplikacji wielodostępnej. Na przykład można tej dzierżawy hello tooidentify wartość w toohello wywołania interfejsu API programu Graph. <br><br> **Przykładowa wartość SAML**: <br> `<Attribute Name=”http://schemas.microsoft.com/identity/claims/tenantid”>`<br>`<AttributeValue>cbb1a5ac-f33b-45fa-9bf5-f37db0fed422<AttributeValue>` <br><br> **Przykładowa wartość JWT**: <br> `"tid":"cbb1a5ac-f33b-45fa-9bf5-f37db0fed422"` |
| `nbf`, `exp` |Okres istnienia tokenu |Definiuje hello interwał czasu, w którym token jest prawidłowy. Usługa Hello, która weryfikuje hello token powinien Sprawdź, czy tego hello bieżąca data jest w hello okres istnienia tokenu, else należy odrzucić hello token. Witaj usługi może wzrosnąć dla minut toofive poza hello okres istnienia tokenu zakresu tooaccount różnice w zegarze ("czas zegara") między usługami Azure AD i usługi hello. <br><br> **Przykładowa wartość SAML**: <br> `<Conditions`<br>`NotBefore="2013-03-18T21:32:51.261Z"`<br>`NotOnOrAfter="2013-03-18T22:32:51.261Z"`<br>`>` <br><br> **Przykładowa wartość JWT**: <br> `"nbf":1363289634, "exp":1363293234` |
| `upn` |Główna nazwa użytkownika |Magazyny hello nazwa użytkownika hello podmiotu zabezpieczeń.<br><br> **Przykładowa wartość JWT**: <br> `"upn": frankm@contoso.com` |
| `ver` |Wersja |Przechowuje numer wersji hello hello tokenu. <br><br> **Przykładowa wartość JWT**: <br> `"ver": "1.0"` |

## <a name="access-tokens"></a>Tokeny dostępu
Po pomyślnym uwierzytelnieniu usługi Azure AD zwraca token dostępu, które mogą być używane tooaccess chronionych zasobów. token dostępu Hello jest base 64 zakodowane tokenu Web JSON (JWT) i jego zawartość można sprawdzić, uruchamiając go przy użyciu dekodera.

Jeśli aplikacja tylko *używa* tooAPIs dostępu tooget tokeny dostępu, można i powinien są traktowane tokenów dostępu jako całkowicie nieprzezroczyste — są tylko ciągi, które aplikacji można przekazać tooresources żądania HTTP.

W przypadku żądania tokenu dostępu, usługi Azure AD zwraca także niektóre metadane dotyczące hello token dostępu do aplikacji przez.  Informacje te obejmują hello czas wygaśnięcia tokenu dostępu hello i zakresy hello, dla których jest prawidłowy.  Dzięki temu można inteligentne buforowanie tokenów dostępu bez konieczności tooparse Otwórz tokenu dostępu hello sam tooperform Twojej aplikacji.

Jeśli aplikacja jest chroniony za pomocą usługi Azure AD, która oczekuje tokenów dostępu w żądaniach HTTP interfejsu API, następnie należy wykonać sprawdzanie poprawności i kontroli hello tokenów, który pojawi się. Aplikację należy przeprowadzić weryfikacji tokenu dostępu hello przed jego użyciem tooaccess zasobów. Aby uzyskać więcej informacji dotyczących sprawdzania poprawności, zobacz [sprawdzania poprawności tokenów](#validating-tokens).  
Aby uzyskać więcej informacji na toodo to z platformą .NET, zobacz temat [chronić interfejsu API sieci Web za pomocą tokenów elementu nośnego z usługi Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

## <a name="refresh-tokens"></a>Tokenów odświeżania

Odśwież tokeny to tokeny zabezpieczające, których może używać aplikacja tooacquire dostęp do nowych tokenów w przepływu OAuth 2.0.  Umożliwia Twojej aplikacji tooachieve długoterminowej dostępu tooresources w imieniu użytkownika bez konieczności interakcji przez użytkownika hello.

Tokeny odświeżania są wielu zasobów.  To toosay otrzymania token odświeżania podczas żądania tokenu dla jednego zasobu można wykorzystać dla dwóch zupełnie różnych zasobów tooa tokeny dostępu. toodo hello tego zestawu `resource` parametru w toohello żądania hello docelowe zasobów.

Tokeny odświeżania są całkowicie nieprzezroczyste tooyour aplikacji. Są one długotrwałe, ale nie powinien być zapisywany aplikacji tooexpect, który ka¿dy okres będzie trwać token odświeżania.  Tokeny odświeżania nieważne można w dowolnej chwili z różnych przyczyn.  Witaj tooattempt tooredeem jest sposób tooknow Twojej aplikacji, jeśli token odświeżania jest prawidłowy tylko go przez punkt końcowy tokenów tooAzure AD żądania tokenu.

Gdy zrealizować token odświeżania, aby uzyskać nowy token dostępu, otrzymasz nowy token odświeżania w hello odpowiedzi tokenu.  Należy zapisać hello nowo wystawiony token odświeżania, zastępując hello jedną używanego w żądaniu hello.  Gwarantuje to, że tokenów odświeżania ważność tak długo, jak to możliwe.

## <a name="validating-tokens"></a>Sprawdzanie poprawności tokenów

W kolejności toovalidate żądaniu lub jako ' access_token ' aplikacji należy zweryfikować oświadczenia podpisu i hello token zarówno hello. W kolejności toovalidate tokenów dostępu aplikacji należy zweryfikować hello wystawcy, hello odbiorców i hello podpisywania tokenów. Te czynności toobe weryfikowana pod kątem wartości hello w dokumencie odnajdywania hello OpenID. Na przykład hello dzierżawy niezależnie od wersji dokumentu hello znajduje się w [https://login.microsoftonline.com/common/.well-known/openid-configuration](https://login.microsoftonline.com/common/.well-known/openid-configuration). Azure AD oprogramowanie pośredniczące ma wbudowane funkcje sprawdzania poprawności tokenów dostępu i można przeglądać naszych [przykłady](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-code-samples) toofind jeden w dowolnie wybranym języku hello. Aby uzyskać więcej informacji dotyczących sposobu tooexplicitly sprawdzania poprawności tokenu JWT, zobacz hello [ręczne próbki sprawdzania poprawności tokenu JWT](https://github.com/Azure-Samples/active-directory-dotnet-webapi-manual-jwt-validation).  

Firma Microsoft udostępnia bibliotek i przykładów kodu, które pokazują, jak tooeasily obsługuje sprawdzanie poprawności tokenu — hello poniżej informacje po prostu jest dostępna dla tych, którzy chcą hello toounderstand podstawowy proces.  Dostępne są również kilka innych firm bibliotek typu open source dla weryfikacji JWT — Brak co najmniej jedną opcję dla prawie wszystkich platform i tam języka. Aby uzyskać więcej informacji na temat biblioteki uwierzytelniania usługi Azure AD i przykładów kodu, zobacz [biblioteki uwierzytelniania usługi Azure AD](active-directory-authentication-libraries.md).

#### <a name="validating-hello-signature"></a>Sprawdzanie poprawności podpisu hello

Token JWT zawiera trzy segmentów, które są oddzielone hello `.` znaków.  pierwszy segment Hello jest nazywany hello **nagłówka**, hello drugi jako hello **treści**i hello innej jako hello **podpisu**.  segment podpisu Hello może być używane toovalidate hello autentyczności hello token, dzięki czemu mogą być zaufane przez aplikację.

Tokenów wystawionych przez usługę Azure AD są podpisane za pomocą branżowy standard szyfrowanie asymetryczne algorytmy, takie jak RSA 256. Nagłówek Hello hello JWT zawiera informacje o kluczu hello i toosign hello token używany metody szyfrowania:

```
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "kriMPdmBvx68skT8-mPAB3BseeA"
}
```

Witaj `alg` oświadczeń wskazuje hello algorytmu, który został token hello toosign używane podczas hello `x5t` oświadczeń wskazuje hello określonego klucz publiczny, który był używany toosign hello token.

Na dowolnym etapie w czasie usługi Azure AD mogą zarejestrować żądaniu przy użyciu jednego z określone pary kluczy publiczno prywatnych. Usługi Azure AD obraca hello zestaw możliwych kluczy w regularnych odstępach czasu, więc aplikacja powinna być zapisana toohandle powoduje automatyczną zmianę tych kluczy.  Toocheck uzasadnione częstotliwości aktualizacji toohello kluczy publicznych używane przez usługę Azure AD jest co 24 godziny.

Można uzyskać hello podpisywania podpisu hello toovalidate niezbędne dane klucza przy użyciu hello OpenID Connect dokument metadanych w lokalizacji:

```
https://login.microsoftonline.com/common/.well-known/openid-configuration
```

> [!TIP]
> Sprawdź ten adres URL w przeglądarce!
> 
> 

Ten dokument metadanych jest obiekt JSON zawierający kilku przydatne informacje, takie jak lokalizacja hello hello różne punkty końcowe wymagane do wykonywania uwierzytelniania OpenID Connect.  

Zawiera także `jwks_uri`, co daje hello lokalizacji hello zestawu kluczy publicznych używane toosign tokenów.  dokument JSON Hello znajdujący się w hello `jwks_uri` zawiera wszystkie hello informacje o kluczu publicznym używany w tej chwili określonego czasu.  Aplikację można użyć hello `kid` oświadczeń w hello JWT nagłówka tooselect, którego klucz publiczny w tym dokumencie został użyty toosign określonej tokenu.  Następnie można przeprowadzić przy użyciu hello prawidłowy klucz publiczny i algorytm wskazanych hello Walidacja podpisu.

Zostanie wykonana Walidacja podpisu hello poza zakres tego dokumentu — Brak dostępnych wiele bibliotek typu open source za pomoc, możesz to zrobić w razie potrzeby.

#### <a name="validating-hello-claims"></a>Sprawdzanie poprawności hello oświadczeń

Gdy aplikacja odbiera token (żądaniu podczas logowania użytkownika lub token dostępu jako tokenu elementu nośnego w żądaniu hello HTTP) on również wykonywać kilka kontroli względem hello oświadczenia w tokenie hello.  Te obejmują, ale nie są ograniczone do:

* Witaj **odbiorców** oświadczeń - tooverify, który hello token został zamierzonego toobe podane tooyour aplikacji.
* Witaj **nie wcześniej niż** i **czas wygaśnięcia** oświadczeń - tooverify, który hello token nie wygasł.
* Witaj **wystawcy** oświadczeń - tooverify, który hello tokenu aplikacji tooyour rzeczywiście został wystawiony przez usługę Azure AD.
* Witaj **identyfikator jednorazowy** -toomitigate atak powtórzeń tokenów.
* i więcej...

Pełną listę operacji sprawdzania poprawności oświadczenia aplikacji należy wykonać tokeny Identyfikatora, można znaleźć w temacie toohello [OpenID Connect specyfikacji](http://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation). Szczegóły hello oczekiwanych wartości tych oświadczeń znajdują się w poprzednim hello [sekcji żądaniu](#id-tokens) sekcji.

## <a name="sample-tokens"></a>Tokeny próbki

Ta sekcja Wyświetla przykłady tokeny SAML i JWT, które zwraca usługi Azure AD. Te przykłady umożliwiają sprawdzanie oświadczenia hello w kontekście.

### <a name="saml-token"></a>SAML Token

To jest przykład typowego tokenu SAML.

    <?xml version="1.0" encoding="UTF-8"?>
    <t:RequestSecurityTokenResponse xmlns:t="http://schemas.xmlsoap.org/ws/2005/02/trust">
      <t:Lifetime>
        <wsu:Created xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T05:15:47.060Z</wsu:Created>
        <wsu:Expires xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">2014-12-24T06:15:47.060Z</wsu:Expires>
      </t:Lifetime>
      <wsp:AppliesTo xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy">
        <EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
          <Address>https://contoso.onmicrosoft.com/MyWebApp</Address>
        </EndpointReference>
      </wsp:AppliesTo>
      <t:RequestedSecurityToken>
        <Assertion xmlns="urn:oasis:names:tc:SAML:2.0:assertion" ID="_3ef08993-846b-41de-99df-b7f3ff77671b" IssueInstant="2014-12-24T05:20:47.060Z" Version="2.0">
          <Issuer>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</Issuer>
          <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
            <ds:SignedInfo>
              <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
              <ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256" />
              <ds:Reference URI="#_3ef08993-846b-41de-99df-b7f3ff77671b">
                <ds:Transforms>
                  <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
                  <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
                </ds:Transforms>
                <ds:DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256" />
                <ds:DigestValue>cV1J580U1pD24hEyGuAxrbtgROVyghCqI32UkER/nDY=</ds:DigestValue>
              </ds:Reference>
            </ds:SignedInfo>
            <ds:SignatureValue>j+zPf6mti8Rq4Kyw2NU2nnu0pbJU1z5bR/zDaKaO7FCTdmjUzAvIVfF8pspVR6CbzcYM3HOAmLhuWmBkAAk6qQUBmKsw+XlmF/pB/ivJFdgZSLrtlBs1P/WBV3t04x6fRW4FcIDzh8KhctzJZfS5wGCfYw95er7WJxJi0nU41d7j5HRDidBoXgP755jQu2ZER7wOYZr6ff+ha+/Aj3UMw+8ZtC+WCJC3yyENHDAnp2RfgdElJal68enn668fk8pBDjKDGzbNBO6qBgFPaBT65YvE/tkEmrUxdWkmUKv3y7JWzUYNMD9oUlut93UTyTAIGOs5fvP9ZfK2vNeMVJW7Xg==</ds:SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <X509Data>
                <X509Certificate>MIIDPjCCAabcAwIBAgIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTQwMTAxMDcwMDAwWhcNMTYwMTAxMDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAkSCWg6q9iYxvJE2NIhSyOiKvqoWCO2GFipgH0sTSAs5FalHQosk9ZNTztX0ywS/AHsBeQPqYygfYVJL6/EgzVuwRk5txr9e3n1uml94fLyq/AXbwo9yAduf4dCHTP8CWR1dnDR+Qnz/4PYlWVEuuHHONOw/blbfdMjhY+C/BYM2E3pRxbohBb3x//CfueV7ddz2LYiH3wjz0QS/7kjPiNCsXcNyKQEOTkbHFi3mu0u13SQwNddhcynd/GTgWN8A+6SN1r4hzpjFKFLbZnBt77ACSiYx+IHK4Mp+NaVEi5wQtSsjQtI++XsokxRDqYLwus1I1SihgbV/STTg5enufuwIDAQABo2IwYDBeBgNVHQEEVzBVgBDLebM6bK3BjWGqIBrBNFeNoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQsRiM0jheFZhKk49YD0SK1TAJBgUrDgMCHQUAA4IBAQCJ4JApryF77EKC4zF5bUaBLQHQ1PNtA1uMDbdNVGKCmSp8M65b8h0NwlIjGGGy/unK8P6jWFdm5IlZ0YPTOgzcRZguXDPj7ajyvlVEQ2K2ICvTYiRQqrOhEhZMSSZsTKXFVwNfW6ADDkN3bvVOVbtpty+nBY5UqnI7xbcoHLZ4wYD251uj5+lo13YLnsVrmQ16NCBYq2nQFNPuNJw6t3XUbwBHXpF46aLT1/eGf/7Xx6iy8yPJX4DyrpFTutDz882RWofGEO5t4Cw+zZg70dJ/hH/ODYRMorfXEW+8uKmXMKmX2wyxMKvfiPbTy5LmAU8Jvjs2tLg4rOBcXWLAIarZ</X509Certificate>
              </X509Data>
            </KeyInfo>
          </ds:Signature>
          <Subject>
            <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">m_H3naDei2LNxUmEcWd0BZlNi_jVET1pMLR6iQSuYmo</NameID>
            <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
          </Subject>
          <Conditions NotBefore="2014-12-24T05:15:47.060Z" NotOnOrAfter="2014-12-24T06:15:47.060Z">
            <AudienceRestriction>
              <Audience>https://contoso.onmicrosoft.com/MyWebApp</Audience>
            </AudienceRestriction>
          </Conditions>
          <AttributeStatement>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
              <AttributeValue>a1addde8-e4f9-4571-ad93-3059e3750d23</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/tenantid">
              <AttributeValue>b9411234-09af-49c2-b0c3-653adc1f376e</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
              <AttributeValue>sample.admin@contoso.onmicrosoft.com</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname">
              <AttributeValue>Admin</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname">
              <AttributeValue>Sample</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/ws/2008/06/identity/claims/groups">
              <AttributeValue>5581e43f-6096-41d4-8ffa-04e560bab39d</AttributeValue>
              <AttributeValue>07dd8a89-bf6d-4e81-8844-230b77145381</AttributeValue>
              <AttributeValue>0e129f4g-6b0a-4944-982d-f776000632af</AttributeValue>
              <AttributeValue>3ee07328-52ef-4739-a89b-109708c22fb5</AttributeValue>
              <AttributeValue>329k14b3-1851-4b94-947f-9a4dacb595f4</AttributeValue>
              <AttributeValue>6e32c650-9b0a-4491-b429-6c60d2ca9a42</AttributeValue>
              <AttributeValue>f3a169a7-9a58-4e8f-9d47-b70029v07424</AttributeValue>
              <AttributeValue>8e2c86b2-b1ad-476d-9574-544d155aa6ff</AttributeValue>
              <AttributeValue>1bf80264-ff24-4866-b22c-6212e5b9a847</AttributeValue>
              <AttributeValue>4075f9c3-072d-4c32-b542-03e6bc678f3e</AttributeValue>
              <AttributeValue>76f80527-f2cd-46f4-8c52-8jvd8bc749b1</AttributeValue>
              <AttributeValue>0ba31460-44d0-42b5-b90c-47b3fcc48e35</AttributeValue>
              <AttributeValue>edd41703-8652-4948-94a7-2d917bba7667</AttributeValue>
            </Attribute>
            <Attribute Name="http://schemas.microsoft.com/identity/claims/identityprovider">
              <AttributeValue>https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/</AttributeValue>
            </Attribute>
          </AttributeStatement>
          <AuthnStatement AuthnInstant="2014-12-23T18:51:11.000Z">
            <AuthnContext>
              <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
            </AuthnContext>
          </AuthnStatement>
        </Assertion>
      </t:RequestedSecurityToken>
      <t:RequestedAttachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedAttachedReference>
      <t:RequestedUnattachedReference>
        <SecurityTokenReference xmlns="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd" xmlns:d3p1="http://docs.oasis-open.org/wss/oasis-wss-wssecurity-secext-1.1.xsd" d3p1:TokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0">
          <KeyIdentifier ValueType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLID">_3ef08993-846b-41de-99df-b7f3ff77671b</KeyIdentifier>
        </SecurityTokenReference>
      </t:RequestedUnattachedReference>
      <t:TokenType>http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV2.0</t:TokenType>
      <t:RequestType>http://schemas.xmlsoap.org/ws/2005/02/trust/Issue</t:RequestType>
      <t:KeyType>http://schemas.xmlsoap.org/ws/2005/05/identity/NoProofKey</t:KeyType>
    </t:RequestSecurityTokenResponse>

### <a name="jwt-token---user-impersonation"></a>Token JWT - personifikacji użytkownika
To jest przykładowy typowe tokenu web JSON (JWT) używane w grant przepływu kodu autoryzacji.
W tooclaims dodanie hello token zawiera numeru wersji w **ver** i **appidacr**, hello uwierzytelniania kontekstu odwołania do klasy, który wskazuje, jak została uwierzytelniona powitania klienta. Dla publicznych klienta hello wartość to 0. Jeśli użyto Identyfikatora klienta lub klucz tajny klienta hello wartość to 1.

    {
     typ: "JWT",
     alg: "RS256",
     x5t: "kriMPdmBvx68skT8-mPAB3BseeA"
    }.
    {
     aud: "https://contoso.onmicrosoft.com/scratchservice",
     iss: "https://sts.windows.net/b9411234-09af-49c2-b0c3-653adc1f376e/",
     iat: 1416968588,
     nbf: 1416968588,
     exp: 1416972488,
     ver: "1.0",
     tid: "b9411234-09af-49c2-b0c3-653adc1f376e",
     amr: [
      "pwd"
     ],
     roles: [
      "Admin"
     ],
     oid: "6526e123-0ff9-4fec-ae64-a8d5a77cf287",
     upn: "sample.user@contoso.onmicrosoft.com",
     unique_name: "sample.user@contoso.onmicrosoft.com",
     sub: "yf8C5e_VRkR1egGxJSDt5_olDFay6L5ilBA81hZhQEI",
     family_name: "User",
     given_name: "Sample",
     groups: [
      "0e129f6b-6b0a-4944-982d-f776000632af",
      "323b13b3-1851-4b94-947f-9a4dacb595f4",
      "6e32c250-9b0a-4491-b429-6c60d2ca9a42",
      "f3a161a7-9a58-4e8f-9d47-b70022a07424",
      "8d4c81b2-b1ad-476d-9574-544d155aa6ff",
      "1bf80164-ff24-4866-b19c-6212e5b9a847",
      "76f80127-f2cd-46f4-8c52-8edd8bc749b1",
      "0ba27160-44d0-42b5-b90c-47b3fcc48e35"
     ],
     appid: "b075ddef-0efa-123b-997b-de1337c29185",
     appidacr: "1",
     scp: "user_impersonation",
     acr: "1"
    }.

## <a name="related-content"></a>Zawartość pokrewna
* Zobacz hello Azure AD Graph [operacji zasad](https://msdn.microsoft.com/library/azure/ad/graph/api/policy-operations) i hello [jednostki zasady](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#policy-entity), toolearn więcej informacji na temat zarządzania zasadami okres istnienia tokenu przy użyciu hello interfejsu API usługi Azure AD Graph.
* Aby uzyskać więcej informacji i przykłady dotyczące zarządzania zasadami za pomocą poleceń cmdlet programu PowerShell, zawierająca próbek, zobacz [można skonfigurować tokenu okresy istnienia w usłudze Azure AD](../active-directory-configurable-token-lifetimes.md). 
