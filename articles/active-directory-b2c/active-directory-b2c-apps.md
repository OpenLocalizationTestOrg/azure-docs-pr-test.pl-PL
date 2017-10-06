---
title: aaaAzure AD B2C | Dokumentacja firmy Microsoft
description: "Witaj typów aplikacji, które można tworzyć w hello Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a>Usługa Azure Active Directory B2C: typy aplikacji
Usługa Azure Active Directory (Azure AD) B2C obsługuje uwierzytelnianie w wielu nowoczesnych architekturach aplikacji. Wszystkie z nich są oparte na standardowych protokołach branżowych hello [OAuth 2.0](active-directory-b2c-reference-protocols.md) lub [OpenID Connect](active-directory-b2c-reference-protocols.md). W tym dokumencie krótko opisano hello typy aplikacji, które można tworzyć, niezależnie od języka hello lub platformy preferowane. Ułatwia on także zrozumienie ogólnych scenariuszy hello przed [rozpocząć tworzenie aplikacji](active-directory-b2c-overview.md#get-started).

## <a name="hello-basics"></a>podstawy Hello
Każda aplikacja, która używa usługi Azure AD B2C musi być zarejestrowana w Twojej [katalogu B2C](active-directory-b2c-get-started.md) za pośrednictwem hello [Azure Portal](https://portal.azure.com/). proces rejestracji aplikacji Hello zbiera i przypisuje kilka wartości tooyour aplikacji:

* **Identyfikator aplikacji** który w sposób unikatowy identyfikuje aplikację.
* A **identyfikator URI przekierowania** które może być używane toodirect odpowiedzi wstecz tooyour aplikacji.
* Dowolne inne wartości właściwe dla scenariusza. Aby uzyskać więcej informacji, Dowiedz się, jak za[rejestracji aplikacji](active-directory-b2c-app-registration.md).

Po zarejestrowaniu aplikacji hello komunikacji z usługą Azure AD, wysyłając punktu końcowego v2.0 toohello usługi Azure AD żądań:

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

Każde żądanie wysłania tooAzure AD B2C Określa **zasad**. Zasady regulują hello zachowanie usługi Azure AD. Umożliwia także te punkty końcowe toocreate dużym stopniu dostosowywane zestawu funkcji środowiska użytkownika. Wspólne zasady obejmują rejestrację, logowanie i edycję profilu. Jeśli nie masz doświadczenia z zasadami, należy przeczytać temat hello Azure AD B2C [rozszerzona platforma zasad](active-directory-b2c-reference-policies.md) przed kontynuowaniem.

Witaj interakcja wszystkich aplikacji z punktem końcowym v2.0 następujące podobnego wzorca wysokiego poziomu:

1. Aplikacja Hello przekierowuje hello użytkownika toohello v2.0 punktu końcowego tooexecute [zasad](active-directory-b2c-reference-policies.md).
2. Użytkownik Hello kończy hello zasad zgodnie z toohello definicji zasad.
3. Aplikacja Hello odbiera określonego rodzaju token zabezpieczający z punktu końcowego v2.0 hello.
4. Aplikacja Hello używa hello zabezpieczeń tokenu tooaccess chronionych informacji lub chronionego zasobu.
5. Witaj, serwer zasobów weryfikuje hello zabezpieczeń tokenu tooverify, który może być przyznany dostęp.
6. Aplikacja Hello okresowo odświeża token zabezpieczający hello.

<!-- TODO: Need a page for libraries toolink too-->
Te kroki mogą się nieznacznie różnić na powitania typu aplikacji, które tworzysz. Biblioteki typu open source można adres hello szczegóły.

## <a name="web-apps"></a>Aplikacje sieci Web
W przypadku aplikacji sieci Web (w tym .NET, PHP, Java, Ruby, Python i Node.js), które są hostowane na serwerze i dostępne za pośrednictwem przeglądarki, usługa Azure AD B2C obsługuje protokół [OpenID Connect](active-directory-b2c-reference-protocols.md) w odniesieniu wszystkich funkcji środowiska użytkownika. Obejmuje to logowanie, rejestrację i zarządzanie profilami. W implementacji hello Azure AD B2C OpenID Connect aplikacji sieci web inicjuje te funkcje środowiska użytkownika przez wystawienie tooAzure żądań uwierzytelniania usługi AD. wynik żądania hello Hello jest `id_token`. Ten token zabezpieczający reprezentuje tożsamość użytkownika hello. Zawiera także informacje o użytkowniku hello w postaci hello oświadczeń:

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

Dowiedz się więcej o typach tokenów i oświadczeń aplikacji tooan dostępne w hello hello [odwołania do tokenu usługi B2C](active-directory-b2c-reference-tokens.md).

W aplikacji sieci Web każde wykonanie [zasad](active-directory-b2c-reference-policies.md) obejmuje następujące ogólne kroki:

![Obraz ścieżek aplikacji sieci Web](./media/active-directory-b2c-apps/webapp.png)

Sprawdzanie poprawności hello `id_token` przy użyciu publicznego klucza podpisywania otrzymanego z usługi Azure AD jest wystarczające tożsamości użytkownika hello hello tooverify. Powoduje ono również ustawienie pliku cookie sesji, które mogą być używane tooidentify hello użytkownika na następnej stronie żądania.

toosee tym scenariuszem w praktyce, wypróbuj jedną z hello przykłady kodu logowania aplikacji sieci web w naszym [sekcji wprowadzenie](active-directory-b2c-overview.md#get-started).

W dodatku toofacilitating prostego logowania aplikacja serwera sieci web może być również konieczne tooaccess usługi sieci web zaplecza. W takim przypadku hello aplikacji sieci web może wykonać nieco inny [przepływ protokołu OpenID Connect](active-directory-b2c-reference-oidc.md) i uzyskać tokeny przy użyciu kodów autoryzacji i tokenów odświeżania. Ten scenariusz jest opisany w następujących hello [interfejsów API sieci Web sekcji](#web-apis).

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a>Interfejsy API sieci Web
Można użyć usług sieci web toosecure usługi Azure AD B2C, takich jak RESTful aplikacji interfejsu API sieci web. Interfejsy API sieci Web można używać toosecure OAuth 2.0 ich danych uwierzytelniający przychodzących żądań HTTP przy użyciu tokenów. Witaj wywołujący interfejs API sieci web dołącza token w nagłówku autoryzacji hello żądania HTTP:

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

Hello interfejsu API sieci web może następnie używać hello tokenu tooverify hello interfejsu API wywołującego tożsamości i tooextract informacji o wywołującego hello z oświadczeń zakodowanych w tokenie hello. Dowiedz się więcej o typach tokenów i oświadczeń aplikacji tooan dostępne w hello hello [odwołania do tokenu usługi Azure AD B2C](active-directory-b2c-reference-tokens.md).

> [!NOTE]
> Usługa Azure AD B2C obsługuje obecnie tylko interfejsy API sieci Web, do których dostęp uzyskują ich własne dobrze znane aplikacje klienckie. Na przykład pełna aplikacja może obejmować aplikację systemu iOS, aplikację systemu Android i interfejs API sieci Web zaplecza. Taka architektura jest w pełni obsługiwana. Zezwalanie klientowi partnera, np. innej aplikacji systemu iOS tooaccess hello tej samej sieci web interfejsu API nie jest obecnie obsługiwane. Wszystkie składniki hello pełnej aplikacji muszą współdzielić jeden identyfikator aplikacji.
>
>

Interfejs API sieci Web może odbierać tokeny od wielu typów klientów, m.in. aplikacji sieci Web, aplikacji klasycznych i aplikacji, aplikacji jednej strony, demonów po stronie serwera oraz innych interfejsów API sieci Web. Oto przykład pełnego przepływu aplikacji sieci web, która wywołuje interfejs API sieci web hello:

![Obraz ścieżek interfejsu API sieci Web aplikacji sieci Web](./media/active-directory-b2c-apps/webapi.png)

toolearn więcej informacji o kodach autoryzacji, tokenach odświeżania i kroki hello dla uzyskiwania tokenów, przeczytaj o hello [protokołu OAuth 2.0](active-directory-b2c-reference-oauth-code.md).

toolearn jak toosecure interfejs API sieci web przy użyciu usługi Azure AD B2C, wyewidencjonowanie hello sieci web samouczki interfejsu API w naszym [sekcji wprowadzenie](active-directory-b2c-overview.md#get-started).

## <a name="mobile-and-native-apps"></a>Aplikacje mobilne i natywne
Aplikacje, które są zainstalowane na urządzeniach, takich jak aplikacji mobilnych i klasycznych, często muszą tooaccess usług zaplecza lub interfejsów API sieci web w imieniu użytkowników. Możesz dodać aplikacje natywne tooyour środowiska zarządzania dostosowane tożsamości i bezpiecznie wywoływać usługi zaplecza przy użyciu usługi Azure AD B2C i hello [przepływu kodu autoryzacji protokołu OAuth 2.0](active-directory-b2c-reference-oauth-code.md).  

W tym przepływie aplikacja hello wykonuje [zasady](active-directory-b2c-reference-policies.md) i odbiera `authorization_code` z usługi Azure AD po hello użytkownik kończy hello zasad. Witaj `authorization_code` reprezentuje hello usług zaplecza aplikacji uprawnienia toocall imieniu hello użytkownika, który jest aktualnie zalogowany. Aplikacja Hello może następnie wymienić hello `authorization_code` w tle hello `id_token` i `refresh_token`.  Aplikacja Hello można używać hello `id_token` tooauthenticate tooa zaplecza interfejsu API sieci web w żądaniach HTTP. Można również użyć hello `refresh_token` tooget nowy `id_token` gdy wygaśnie stary.

> [!NOTE]
> Azure AD B2C obsługuje obecnie tylko tokeny, które są używane tooaccess usługę sieci web zaplecza w aplikacji. Na przykład pełna aplikacja może obejmować aplikację systemu iOS, aplikację systemu Android i interfejs API sieci Web zaplecza. Taka architektura jest w pełni obsługiwana. Stosowanie interfejsu API sieci web partnera z tooaccess aplikacji systemu iOS przy użyciu tokenów dostępu protokołu OAuth 2.0 nie jest obecnie obsługiwane. Wszystkie składniki hello pełnej aplikacji muszą współdzielić jeden identyfikator aplikacji.
>
>

![Obraz ścieżek aplikacji natywnej](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a>Bieżące ograniczenia
Usługa Azure AD B2C nie obsługuje obecnie hello następujące typy aplikacji, ale znajdują się na plan hello. 

### <a name="daemonsserver-side-apps"></a>Demony/aplikacje po stronie serwera
Aplikacje, które zawierają procesy długotrwałe lub niewymagające obecności użytkownika hello muszą również sposób którą tooaccess zabezpieczonych zasobów, takich jak interfejsów API sieci web. Te aplikacje mogą uwierzytelniać i uzyskiwać tokeny przy użyciu tożsamości aplikacji hello (zamiast delegowanej tożsamości użytkownika) i przy użyciu przepływu poświadczeń klienta hello OAuth 2.0.

Ten przepływ nie jest obecnie obsługiwany w usłudze Azure AD B2C. Te aplikacje mogą uzyskiwać tokeny tylko po wystąpieniu interaktywnego przepływu użytkownika.

### <a name="web-api-chains-on-behalf-of-flow"></a>Łańcuchy interfejsu API sieci Web (przepływ „w imieniu”)
Wiele architektur obejmują składnika web API, który wymaga toocall inny podrzędny interfejs API sieci web, gdy oba interfejsy są zabezpieczane przez usługi Azure AD B2C. Ten scenariusz jest często spotykany w klientach natywnych, którzy mają zaplecza interfejsu API sieci Web. Następnie następuje wywołanie usługi online firmy Microsoft, takich jak hello interfejsu API usługi Azure AD Graph.

Ten scenariusz łańcuchowa interfejsu API sieci web mogą być obsługiwane przez przy użyciu przyznania poświadczeń elementu nośnego OAuth 2.0 JWT hello, znanej także jako hello imieniu-przepływ "w".  Jednak hello imieniu-przepływ "w" nie jest obecnie zaimplementowana w hello Azure AD B2C.
