---
title: "typy aaaApp dla punktu końcowego v2.0 usługi Azure Active Directory hello | Dokumentacja firmy Microsoft"
description: "typy Hello aplikacji i scenariusze obsługiwane przez punktu końcowego v2.0 usługi Azure Active Directory hello."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a>Typy aplikacji dla punktu końcowego v2.0 usługi Azure Active Directory hello
Witaj punktu końcowego v2.0 usługi Azure Active Directory (Azure AD) obsługuje uwierzytelnianie dla różnych architektur nowoczesnych aplikacji, wszystkie z nich oparte na standardowych protokołach [OAuth 2.0 lub OpenID Connect](active-directory-v2-protocols.md). W tym artykule opisano hello typy aplikacji, które można tworzyć przy użyciu usługi Azure AD w wersji 2.0, niezależnie od tego, czy z preferowanego języka lub platformy. Witaj w tym artykule jest zaprojektowana toohelp zrozumienie ogólnych scenariuszy przed [rozpocząć pracę z kodem hello](active-directory-appmodel-v2-overview.md#getting-started).

> [!NOTE]
> punktu końcowego v2.0 Hello nie obsługuje wszystkich scenariuszy Azure Active Directory i funkcji. toodetermine, czy należy używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="hello-basics"></a>podstawy Hello
Należy zarejestrować każdej aplikacji, który używa punktu końcowego v2.0 hello w hello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com). proces rejestracji aplikacji Hello zbiera i przypisuje te wartości dla aplikacji:

* **Identyfikator aplikacji** który unikatowo identyfikuje aplikację
* A **identyfikator URI przekierowania** służy toodirect odpowiedzi wstecz tooyour aplikacji
* Kilka wartości specyficzne dla scenariusza

Aby uzyskać szczegółowe informacje, Dowiedz się, jak za[rejestracji aplikacji](active-directory-v2-app-registration.md).

Po zarejestrowaniu aplikacji hello aplikacji hello komunikuje się z usługą Azure AD, wysyłając punktu końcowego v2.0 toohello usługi Azure AD żądań. Udostępniamy open source struktury i biblioteki, w których szczegóły hello te żądania obsługi. Masz również logikę uwierzytelniania hello hello opcja tooimplement samodzielnie przez utworzenie żądań toothese punktów końcowych:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a>Aplikacje sieci Web
W przypadku aplikacji sieci web (.NET, PHP, Java, Ruby, Python, węzeł) które hello użytkownik uzyskuje dostęp do za pośrednictwem przeglądarki, można użyć [OpenID Connect](active-directory-v2-protocols.md) dla logowania użytkownika. W OpenID Connect aplikacji sieci web hello odbiera token Identyfikatora. Identyfikator tokenu jest token zabezpieczający, weryfikuje tożsamość hello użytkownika, który zawiera informacje o użytkowniku hello w postaci hello oświadczeń:

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Informacje na temat wszystkich typów hello tokeny i oświadczenia, które są dostępne tooan aplikacji w hello [v2.0 tokeny odwołanie](active-directory-v2-tokens.md).

W aplikacji serwera sieci web przepływ uwierzytelniania logowania hello obejmuje następujące ogólne kroki:

![Przepływ uwierzytelniania aplikacji sieci Web](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

Upewnij się tożsamości użytkownika hello, sprawdzając poprawność hello identyfikator tokenu z publicznego klucza podpisywania otrzymanego z punktu końcowego v2.0 hello. Plik cookie sesji jest ustawiona, które mogą być używane tooidentify hello użytkownika na następnej stronie żądania.

toosee tym scenariuszem w praktyce, wypróbuj jedną z hello kodu logowania dla aplikacji sieci web przykłady w naszym v2.0 [wprowadzenie](active-directory-appmodel-v2-overview.md#getting-started) sekcji.

Ponadto toosimple logowania, aplikacja serwera sieci web może być konieczne tooaccess innej usługi sieci web, takich jak interfejsu API REST. W takim przypadku aplikacji serwera sieci web hello uczestniczy w scalonej przepływ protokołu OpenID Connect i OAuth 2.0, za pomocą hello [przepływu kodu autoryzacji protokołu OAuth 2.0](active-directory-v2-protocols.md). Aby uzyskać więcej informacji na temat tego scenariusza, przeczytaj o [wprowadzenie do korzystania z aplikacji sieci web i interfejsów API sieci Web](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).

## <a name="web-apis"></a>Interfejsy API sieci Web
Można użyć hello v2.0 punktu końcowego toosecure usług sieci web, takich jak interfejsu API sieci Web RESTful aplikacji. Zamiast tokeny Identyfikatora i pliki cookie z sesji, interfejs API sieci Web używa toosecure tokenów dostępu protokołu OAuth 2.0, danych i tooauthenticate żądań przychodzących. Witaj wywołujący interfejs API sieci Web dołącza token dostępu w nagłówku autoryzacji hello żądania HTTP, jak to:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Hello interfejsu API sieci Web używa hello dostępu tokenu tooverify hello elementu wywołującego interfejs API tożsamości i tooextract informacji o wywołującego hello z oświadczeń zakodowanych w tokenie dostępu hello. toolearn o hello typy tokenów i oświadczeń, które są dostępne tooan aplikacji, zobacz hello [v2.0 tokeny odwołanie](active-directory-v2-tokens.md).

Interfejs API sieci Web można umożliwić użytkownikom hello zasilania tooopt w lub zrezygnować z określonych funkcji lub danych, nazywane również udostępnianie uprawnienia [zakresy](active-directory-v2-scopes.md). Wywołanie aplikacji tooacquire uprawnienia tooa zakresu hello użytkownik musi wyrazić zgodę zakresu toohello podczas przepływu. punktu końcowego v2.0 Hello pyta użytkownika hello o uprawnienia, a następnie rejestruje uprawnienia w wszystkie tokeny dostępu tego hello, którą otrzymuje interfejsu API sieci Web. Witaj interfejsu API sieci Web weryfikuje tokeny dostępu hello odbierze przy każdym wywołaniu i sprawdza autoryzacji.

Interfejs API sieci Web może odbierać tokeny dostępu z niektórych typów aplikacji, w tym aplikacji serwera sieci web, pulpitu i aplikacji mobilnych, aplikacji jednej strony, demonów po stronie serwera i nawet innych interfejsów API sieci Web. ogólny przepływ Hello interfejsu API sieci Web wygląda następująco:

![Przepływ uwierzytelniania interfejsu API sieci Web](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

toolearn jak przykłady toosecure interfejs API sieci Web przy użyciu tokenów dostępu protokołu OAuth2, wyewidencjonowanie hello kodu interfejsu API sieci Web w naszym [wprowadzenie](active-directory-appmodel-v2-overview.md#getting-started) sekcji.

W wielu przypadkach interfejsów API sieci web muszą toomake żądań wychodzących za tooother sieci web API zabezpieczonej przez usługi Azure Active Directory.  toodo tak, interfejsów API sieci web można korzystać z usługi Azure AD **w imieniu z** przepływu, dzięki czemu tooexchange interfejsu API sieci web hello przychodzący token dostępu dla innego toobe token dostępu używany w żądań wychodzących.  Witaj punktu końcowego v2.0 w imieniu przepływu jest opisany w [szczegółowo opisano w tym miejscu](active-directory-v2-protocols-oauth-on-behalf-of.md).

## <a name="mobile-and-native-apps"></a>Aplikacje mobilne i natywne
Aplikacje zainstalowane urządzenie, takie jak aplikacji mobilnych i klasycznych, często muszą tooaccess usług zaplecza lub interfejsów API sieci Web, które przechowują dane i funkcji w imieniu użytkownika. Tych aplikacji można dodać usługi tooback-end logowania i autoryzacji za pomocą hello [przepływu kodu autoryzacji protokołu OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

W tym przepływie aplikacja hello odbiera kod autoryzacji z punktu końcowego v2.0 powitania po zalogowaniu użytkownika hello. reprezentuje kod autoryzacji Hello hello usług zaplecza aplikacji uprawnienia toocall imieniu hello, użytkownik jest zalogowany. Aplikacja Hello może wymieniać kod autoryzacji hello w tle hello token dostępu protokołu OAuth 2.0 i token odświeżania. aplikacji Hello można używa tooWeb tooauthenticate tokenu dostępu hello interfejsów API w żądaniach HTTP i hello odświeżanie tokenu tooget nowe tokeny dostępu po wygaśnięciu starsze tokenów dostępu.

![Przepływ uwierzytelniania aplikacji natywnej](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a>Aplikacje jednej strony (JavaScript)
Wiele nowoczesnych aplikacji ma jednostronicowej aplikacji fronton głównie napisany w języku JavaScript. Często są zapisywane przez przy użyciu platformy takie jak AngularJS, Ember.js lub Durandal.js. punktu końcowego v2.0 Hello Azure AD obsługuje te aplikacje przy użyciu hello [niejawnego przepływu OAuth 2.0](active-directory-v2-protocols-implicit.md).

W tym przepływie aplikacja hello odbiera tokeny bezpośrednio z hello v2.0 punktu końcowego, bez żadnych wymiany serwera serwera autoryzacji. Wszystkie logika uwierzytelniania i sesji obsługi ma umieścić w całości powitania klienta JavaScript, bez dodatkowej strony przekierowania.

![Przepływ uwierzytelniania niejawne](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

toosee tym scenariuszem w praktyce, wypróbuj jedną z próbek kodu jednostronicowej aplikacji hello w naszym [wprowadzenie](active-directory-appmodel-v2-overview.md#getting-started) sekcji.

## <a name="daemons-and-server-side-apps"></a>Demony i aplikacji po stronie serwera
Aplikacje, które mają procesy długotrwałe lub niewymagające interakcji z użytkownikiem muszą również sposób którą tooaccess zabezpieczone zasoby, takie jak interfejsów API sieci Web. Te aplikacje mogą uwierzytelniać i uzyskiwać tokeny przy użyciu tożsamości aplikacji hello zamiast tożsamość o przepływ poświadczeń klienta OAuth 2.0 hello delegowane przez użytkownika.

W tym przepływie aplikacja hello współpracuje bezpośrednio z hello `/token` punkty końcowe tooobtain punktu końcowego:

![Demon przebieg uwierzytelniania w aplikacji](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

toobuild aplikacji demon, zobacz dokumentację poświadczeń klienta hello w naszym [wprowadzenie](active-directory-appmodel-v2-overview.md#getting-started) sekcji lub spróbuj [.NET Przykładowa aplikacja](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
