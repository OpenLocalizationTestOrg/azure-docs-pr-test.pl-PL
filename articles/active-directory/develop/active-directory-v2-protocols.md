---
title: "aaaLearn o hello autoryzacji protokołów obsługiwanych przez usługę Azure AD w wersji 2.0 | Dokumentacja firmy Microsoft"
description: "Obsługiwane przez punktu końcowego v2.0 usługi Azure AD hello tooprotocols przewodnik."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5fb4fa1b-8fc4-438e-b3b0-258d8c145f22
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f90511b1880ff223f725c1f79df9f79bddccc7bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# w wersji 2.0 protokołów - OAuth 2.0 & OpenID Connect
punktu końcowego v2.0 Hello można używać usługi Azure AD identity jako — usługa z branży standardowe protokoły OpenID Connect i OAuth 2.0.  Gdy usługa hello jest zgodny ze standardami, może to mieć niewielkie różnice między dwoma implementacjami tych protokołów.  tutaj informacje Hello będzie przydatna, jeśli wybierzesz toowrite kodu bezpośrednio wysyłając & obsługiwanie żądań HTTP lub użyj 3rd strona Otwórz źródło biblioteki, a nie przy użyciu jednej z naszych biblioteki typu open source.
<!-- TODO: Need link toolibraries above -->

> [!NOTE]
> Nie wszystkie usługi Azure Active Directory scenariuszy i funkcji obsługiwanych przez hello punktu końcowego v2.0.  toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
>
>

## Witaj podstawy
W niemal wszystkich przepływów OAuth i OpenID Connect obejmuje cztery strony hello programu exchange:

![Role uwierzytelniania OAuth 2.0](../../media/active-directory-v2-flows/protocols_roles.png)

* Witaj **serwera autoryzacji** jest hello punktu końcowego v2.0.  Jest on odpowiedzialny za zapewnienie tożsamości użytkownika hello, udzielanie i odwoływanie dostępu tooresources i wystawiania tokenów.  Jest także znana jako dostawca tożsamości hello — niczego bezpieczną obsługę toodo hello użytkownika informacje, ich dostęp i hello relacje zaufania między stronami w strumieniu.
* Witaj **właściciel zasobu** jest zazwyczaj hello przez użytkownika końcowego.  Jest to strona hello, który jest właścicielem danych hello i ma hello power tooallow innej strony tooaccess danych lub zasobu.
* Witaj **klienta OAuth** jest aplikację identyfikowaną na podstawie jego identyfikatora aplikacji.  Zazwyczaj jest stroną hello użytkownika końcowego hello współdziała z, czy tokeny żąda od serwera autoryzacji hello.  powitania klienta musi mieć przyznane się, że uprawnienia tooaccess hello zasobów hello właściciela zasobów.
* Witaj **serwer zasobów** jest, w którym znajduje się hello zasobów lub danych.  Relacje zaufania powitania serwera autoryzacji toosecurely uwierzytelniania i autoryzacji powitania klienta OAuth i używa elementu nośnego tooensure access_tokens, że dostęp do zasobów tooa może zostać przydzielony.

## Rejestracja aplikacji
Każda aplikacja, która korzysta z punktu końcowego v2.0 hello należy toobe zarejestrowany pod [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) przed mogą współdziałać, za pomocą uwierzytelniania OAuth lub OpenID Connect.  proces rejestracji aplikacji Hello będzie zbierać & przypisać kilka wartości tooyour aplikacji:

* **Identyfikator aplikacji** który unikatowo identyfikuje aplikację
* A **identyfikator URI przekierowania** lub **identyfikator pakietu** które może być używane toodirect odpowiedzi wstecz tooyour aplikacji
* Kilka innych wartości specyficzne dla scenariusza.

Aby uzyskać więcej informacji, Dowiedz się, jak za[rejestracji aplikacji](active-directory-v2-app-registration.md).

## Punkty końcowe
Po zarejestrowaniu aplikacji hello komunikuje się z usługą Azure AD, wysyłając punktu końcowego v2.0 toohello żądań:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Gdzie hello `{tenant}` można wykonać jedną z czterech różnych wartości:

| Wartość | Opis |
| --- | --- |
| `common` |Umożliwia użytkownikom z osobistego konta Microsoft i pracy/służbowego konta z toosign usługi Azure Active Directory do aplikacji hello. |
| `organizations` |Umożliwia tylko użytkownicy z kontami pracy/służbowych z usługą Azure Active Directory toosign do aplikacji hello. |
| `consumers` |Umożliwia tylko użytkownicy z osobistego toosign kont (MSA) firmy Microsoft do aplikacji hello. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` lub `contoso.onmicrosoft.com` |Umożliwia tylko użytkownicy z kontami pracy/służbowych z konkretnym toosign dzierżawy usługi Azure Active Directory do aplikacji hello.  Nazwa domeny przyjazną hello hello dzierżawy usługi Azure AD, albo identyfikator guid dzierżawy hello może służyć. |

Aby uzyskać więcej informacji na temat toointeract z tymi punktami końcowymi, wybierz poniżej typ danej aplikacji.

## Tokeny
Implementacja v2.0 Hello OAuth 2.0 i OpenID Connect należy zwiększone użycie tokenów elementu nośnego, łącznie z tokenów elementu nośnego reprezentowane jako tokenów Jwt. Token elementu nośnego jest token zabezpieczający lekkie, że przyznaje hello tooa dostępu "bearer" chronionych zasobów. W tym sensie "bearer" hello jest każda strona, która może ona powodować hello tokenu. Jeśli strona muszą najpierw zostać uwierzytelnione z tokenu elementu nośnego hello tooreceive usługi Azure AD, czy hello wymagane kroki nie są brane toosecure hello token w transmisji i przechowywania, można przechwycony i używane przez firmę niezamierzone. Chociaż w niektórych tokeny zabezpieczające wbudowany mechanizm uniemożliwia ich użycie przez osoby nieupoważnione, tokenów elementu nośnego nie mają ten mechanizm i musi być transportowane bezpiecznego kanału, takie jak zabezpieczeń warstwy transportu (HTTPS). Jeśli token elementu nośnego jest przesyłany w hello Wyczyść, środkowej atak powitania man-in mogą być używane przez token hello tooacquire strony złośliwych i użyć jej do zasobu tooa chronione nieautoryzowanego dostępu. Witaj te same zasady zabezpieczeń mają zastosowanie po zapisaniu lub buforowanie tokenów elementu nośnego do późniejszego użycia. Zawsze upewnij się, że aplikacja przesyła i przechowuje tokenów elementu nośnego w bezpieczny sposób. Aby uzyskać więcej zagadnienia dotyczące zabezpieczeń na tokenów elementu nośnego, zobacz [RFC 6750 sekcji 5](http://tools.ietf.org/html/rfc6750).

Dalsze szczegóły o różnych typach tokenów używanych w punktu końcowego v2.0 hello jest dostępna w [hello tokenu odwołania do punktu końcowego v2.0](active-directory-v2-tokens.md).

## Protokoły
Jeśli wszystko jest gotowe toosee żądań przedstawiono przykładowe Rozpoczynanie pracy z jednym hello poniżej samouczki.  Każda z nich odpowiada tooa uwierzytelniania konkretnego scenariusza.  Jeśli potrzebujesz pomocy przy ustaleniu, czyli hello prawo przepływu można wyewidencjonować [hello typy aplikacji, można tworzyć za pomocą hello v2.0](active-directory-v2-flows.md).

* [Tworzenie przenośnych i aplikacji natywnej z protokołem OAuth 2.0](active-directory-v2-protocols-oauth-code.md)
* [Tworzenie sieci Web aplikacje z Open ID Connect](active-directory-v2-protocols-oidc.md)
* [Twórz aplikacje jednej strony w hello niejawnego przepływu OAuth 2.0](active-directory-v2-protocols-implicit.md)
* [Kompiluj demonów lub procesy po stronie serwera z hello przepływu poświadczeń klienta OAuth 2.0](active-directory-v2-protocols-oauth-client-creds.md)
* [Uzyskiwanie tokenów w składniku Web API z hello OAuth 2.0 w imieniu On przepływu](active-directory-v2-protocols-oauth-on-behalf-of.md)
