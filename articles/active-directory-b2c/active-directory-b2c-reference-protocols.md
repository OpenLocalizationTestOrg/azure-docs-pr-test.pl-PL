---
title: "Usługi Azure Active Directory B2C: Protokoły uwierzytelniania | Dokumentacja firmy Microsoft"
description: "Jak aplikacje toobuild bezpośrednio za pomocą hello protokołów, które są obsługiwane przez usługę Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5e407d0a-73a2-4d74-ac81-3aa6c31ddcee
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8fa4cbebe711841d410b3ae43b78f893c06d9b63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Usługi Azure AD B2C: Protokoły uwierzytelniania
Usługa Azure Active Directory B2C (Azure AD B2C) zapewnia tożsamości jako usługa dla aplikacji dzięki obsłudze dwóch standardowych protokołach branżowych: OpenID Connect i OAuth 2.0. Usługa Hello jest zgodny ze standardami, ale dwóch implementacjami tych protokołów mogą mieć niewielkie różnice. 

informacje Hello w tym przewodniku są przydatne, jeśli wpisz swój kod bezpośrednio wysyłając i obsługi żądań HTTP, a nie za pomocą biblioteki typu open source. Zalecamy przeczytanie tej strony, przed Poznaj hello szczegóły każdego określonego protokołu. Ale jeśli już znasz usługi Azure AD B2C, można przejść bezpośrednio za[hello podręczniki protokołu](#protocols).

<!-- TODO: Need link toolibraries above -->

## podstawy Hello
Każda aplikacja, która używa usługi Azure AD B2C musi toobe zarejestrowanych w katalogu usługi B2C w hello [portalu Azure](https://portal.azure.com). proces rejestracji aplikacji Hello zbiera i przypisuje kilka wartości tooyour aplikacji:

* **Identyfikator aplikacji** który w sposób unikatowy identyfikuje aplikację.
* A **identyfikator URI przekierowania** lub **pakietu identyfikator** które może być używane toodirect odpowiedzi wstecz tooyour aplikacji.
* Kilka innych wartości specyficzne dla scenariusza. Aby uzyskać więcej informacji, Dowiedz się [jak tooregister aplikacji](active-directory-b2c-app-registration.md).

Po zarejestrowaniu aplikacji komunikacji z usługą Azure Active Directory (Azure AD), wysyłając żądania punktu końcowego z toohello:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

W prawie wszystkie przepływy OAuth i OpenID Connect cztery strony są zaangażowane w programie exchange hello:

![Role uwierzytelniania OAuth 2.0](./media/active-directory-b2c-reference-protocols/protocols_roles.png)

* Witaj **serwera autoryzacji** jest punkt końcowy hello Azure AD. Obsługuje bezpiecznego dostępu i toouser cokolwiek powiązane informacje. Obsługuje ona również hello relacje zaufania między stronami hello w strumieniu. Jest odpowiedzialny za weryfikowania tożsamości użytkownika hello, udzielanie i odwoływanie dostępu tooresources i wystawiania tokenów. Jest nazywana hello dostawcy tożsamości.

* Witaj **właściciel zasobu** jest zazwyczaj hello użytkownika końcowego. Jest stroną hello, który jest właścicielem danych hello, i ma hello zasilania tooallow stron trzecich tooaccess tych danych lub zasobu.

* Witaj **klienta OAuth** jest aplikacji. Jest identyfikowany przez jego identyfikator aplikacji. Zazwyczaj jest strona hello użytkownikom końcowym interakcję z. Z serwera autoryzacji hello są również żądań tokenów. właściciel zasobu Hello należy przyznać powitania klienta uprawnienia tooaccess hello zasobów.

* Witaj **serwer zasobów** jest, w którym znajduje się hello zasobów lub danych. Zaufany autoryzacji hello toosecurely serwera uwierzytelniania i autoryzacji powitania klienta OAuth. Używa tooensure tokenów, który dostęp do zasobów tooa można udzielić dostępu do elementu nośnego.

## Zasady
Można przypuszczać, że zasady usługi Azure AD B2C są hello najważniejszych funkcji usługi hello. Usługa Azure AD B2C rozszerza hello standardowych protokołów OAuth 2.0 i OpenID Connect dzięki zastosowaniu zasad. Umożliwiają one tooperform usługi Azure AD B2C znacznie więcej niż prostego uwierzytelniania i autoryzacji. 

Zasady pełni opisano funkcje tożsamości użytkownika, w tym rejestrację, logowanie i profilu edycji. Zasady można zdefiniować w administracyjnej interfejsu użytkownika. Mogą one wykonywane za pomocą parametru zapytania specjalne w żądania uwierzytelniania HTTP. 

Zasady nie są standardowe funkcje OAuth 2.0 i OpenID Connect, dlatego należy podjąć toounderstand czasu hello je. Aby uzyskać więcej informacji, zobacz hello [przewodniku zasad usługi Azure AD B2C](active-directory-b2c-reference-policies.md).

## Tokeny
Implementacja Hello Azure AD B2C OAuth 2.0 i OpenID Connect sprawia, że zwiększone użycie tokenów elementu nośnego, łącznie z tokenów elementu nośnego, które są reprezentowane jako tokenów sieci web JSON (Jwt). Token elementu nośnego jest token zabezpieczający lekkie, że przyznaje hello tooa dostępu "bearer" chronionych zasobów.

elementu nośnego Hello jest każda strona, która może ona powodować hello tokenu. Usługi Azure AD muszą najpierw zostać uwierzytelnione strona przed może odbierać tokenu elementu nośnego. Jednak jeśli hello wymagane kroki nie są brane toosecure hello token w transmisji i przechowywania, może być przechwycony i używane przez niezamierzone strony.

Niektóre tokeny zabezpieczające mają wbudowane mechanizmy, które uniemożliwić ich użycie nieupoważnione, ale tokenów elementu nośnego nie mają ten mechanizm. Muszą one być transportowane w bezpiecznego kanału, takie jak zabezpieczeń warstwy transportu (HTTPS). 

Jeśli token elementu nośnego, są przesyłane poza bezpiecznego kanału, strony złośliwych można używa tokenu hello tooacquire ataku man-in--middle i jego toogain nieautoryzowany dostęp tooa chronionych zasobów. Witaj, te same zasady zabezpieczeń mają zastosowanie, gdy tokenów elementu nośnego, są przechowywane lub w pamięci podręcznej do późniejszego użycia. Zawsze upewnij się, że aplikacja przesyła i przechowuje tokenów elementu nośnego w bezpieczny sposób.

Dla elementu nośnego dodatkowe zagadnienia dotyczące tokenu zabezpieczeń, zobacz [RFC 6750 sekcji 5](http://tools.ietf.org/html/rfc6750).

Więcej informacji na temat różnych typów tokenów, które są używane w usłudze Azure AD B2C hello są dostępne w [hello odwołania do tokenu usługi Azure AD](active-directory-b2c-reference-tokens.md).

## Protokoły
Jeśli wszystko jest gotowe tooreview przedstawiono przykładowe żądanie, można uruchomić z jednej z następujących samouczków hello. Każdy odpowiada tooa uwierzytelniania konkretnego scenariusza. Jeśli potrzebujesz pomocy przy ustaleniu, które przebieg jest odpowiednie dla Ciebie, zapoznaj się [hello typy aplikacji, można tworzyć za pomocą usługi Azure AD B2C](active-directory-b2c-apps.md).

* [Tworzenie aplikacji mobilnych i natywnego przy użyciu protokołu OAuth 2.0](active-directory-b2c-reference-oauth-code.md)
* [Tworzenie aplikacji sieci web przy użyciu protokołu OpenID Connect](active-directory-b2c-reference-oidc.md)
* [Tworzenie aplikacji jednej strony przy użyciu niejawnego przepływu OAuth 2.0 hello](active-directory-b2c-reference-spa.md)

