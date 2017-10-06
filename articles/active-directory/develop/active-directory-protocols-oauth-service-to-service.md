---
title: "aaaAzure tooService usługi AD uwierzytelniania przy użyciu OAuth2.0 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooimplement wiadomości toouse HTTP usługi tooservice uwierzytelnianie przy użyciu przepływ przyznania poświadczeń hello OAuth2.0 klienta."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: a7f939d9-532d-4b6d-b6d3-95520207965d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f4bfd4ea8a7de1929c7dcf7ad65a156edff74f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Usługa tooservice wywołania przy użyciu poświadczeń klienta (wspólny klucz tajny lub certyfikatu)
usługi sieci web pozwala na powitania przepływu OAuth 2.0 klienta poświadczenia Grant (*poufne klienta*) toouse własne poświadczenia zamiast personifikacji użytkownika, tooauthenticate podczas wywoływania innego usługi sieci web. W tym scenariuszu klient hello jest zwykle usługi sieci web warstwy środkowej, usługa demona lub witryny sieci web. Wyższy poziom gwarancji usługi Azure AD umożliwia także hello wywoływania usługi toouse certyfikatu (zamiast wspólny klucz tajny) jako poświadczenie.

## Diagram przepływu przyznania poświadczeń klienta
Witaj poniższym diagramie wyjaśniono, jak powitania klienta poświadczenia umożliwiają działania przepływu w usłudze Azure Active Directory (Azure AD).

![Przepływ przyznania poświadczeń klienta OAuth2.0](media/active-directory-protocols-oauth-service-to-service/active-directory-protocols-oauth-client-credentials-grant-flow.jpg)

1. Aplikacja kliencka Hello uwierzytelnia punkt końcowy wystawiania tokenu usługi Azure AD toohello i żądania tokenu dostępu.
2. Hello Azure AD wydawania tokenów punktu końcowego problemów hello tokenu dostępu.
3. token dostępu Hello jest używane tooauthenticate toohello zabezpieczonych zasobów.
4. Dane z hello zabezpieczonych zasobów jest zwracana toohello aplikacji sieci web.

## Zarejestruj hello usług w usłudze Azure AD
Zarejestruj zarówno hello wywoływania usługi i hello odbieranie usługi w usłudze Azure Active Directory (Azure AD). Aby uzyskać szczegółowe instrukcje, zobacz [Integrowanie aplikacji z usługą Azure Active Directory](active-directory-integrating-applications.md).

## Żądanie tokenu dostępu
toorequest tokenu dostępu, użyj punktu końcowego HTTP POST toohello specyficznego dla dzierżawy usługi Azure AD.

```
https://login.microsoftonline.com/<tenant id>/oauth2/token
```

## Żądanie tokenu dostępu do usługi
Istnieją dwa przypadki, w zależności od tego, czy aplikacja kliencka hello wybierze toobe zabezpieczone przez Wspólny klucz tajny lub certyfikatu.

### Najpierw przypadek: żądanie tokenu dostępu z wspólny klucz tajny
Korzystając z wspólny klucz tajny, żądania tokenu dostępu do usługi zawiera hello następujące parametry:

| Parametr |  | Opis |
| --- | --- | --- |
| Typ grant_type |Wymagane |Określa Żądanie hello przyznać typu. W przepływie przyznania poświadczeń klienta, wartość hello musi być **client_credentials**. |
| client_id |Wymagane |Określa identyfikator klienta usługi Azure AD hello hello wywoływania usługi sieci web. wywoływanie identyfikator klienta aplikacji, w hello hello toofind [portalu Azure](https://portal.azure.com), kliknij przycisk **usługi Active Directory**, Przełącz katalogu, kliknij przycisk aplikacji hello. Hello client_id jest hello *identyfikator aplikacji* |
| client_secret |Wymagane |Wprowadź klucz, w zarejestrowany dla hello wywoływania usługi lub demon aplikacji sieci web w usłudze Azure AD. toocreate klucz w hello portalu Azure, kliknij przycisk **usługi Active Directory**przełącznika katalogu, kliknij aplikacji hello, kliknij przycisk **ustawienia**, kliknij przycisk **klucze**, i Dodaj klucz.|
| Zasobów |Wymagane |Wprowadź hello identyfikator URI aplikacji hello odbieranie usługi sieci web. Witaj toofind identyfikator URI aplikacji w hello portalu Azure, kliknij przycisk **usługi Active Directory**przełącznika katalogu, kliknij przycisk hello aplikacji usługi, a następnie kliknij **ustawienia** i **właściwości** |

#### Przykład
Witaj następujące POST protokołu HTTP żądania tokenu dostępu dla usługi sieci web https://service.contoso.com/ hello. Witaj `client_id` identyfikuje usługi sieci web hello żądań hello tokenu dostępu.

```
POST /contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fservice.contoso.com%2F
```

### W drugim przypadku: żądanie tokenu dostępu przy użyciu certyfikatu
Żądanie tokenu dostępu do usługi przy użyciu certyfikatu zawiera hello następujące parametry:

| Parametr |  | Opis |
| --- | --- | --- |
| Typ grant_type |Wymagane |Określa hello żądany typ odpowiedzi. W przepływie przyznania poświadczeń klienta, wartość hello musi być **client_credentials**. |
| client_id |Wymagane |Określa identyfikator klienta usługi Azure AD hello hello wywoływania usługi sieci web. wywoływanie identyfikator klienta aplikacji, w hello hello toofind [portalu Azure](https://portal.azure.com), kliknij przycisk **usługi Active Directory**, Przełącz katalogu, kliknij przycisk aplikacji hello. Hello client_id jest hello *identyfikator aplikacji* |
| client_assertion_type |Wymagane |Witaj, wartość musi być`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Wymagane | Potwierdzeniem (JSON Web Token) czy potrzebujesz toocreate oraz znak hello certyfikatu można zarejestrowany jako poświadczeń dla aplikacji. Przeczytaj informacje o [certyfikatu poświadczeń](active-directory-certificate-credentials.md) toolearn jak tooregister Twojego certyfikatu i hello format hello potwierdzenia.|
| Zasobów | Wymagane |Wprowadź hello identyfikator URI aplikacji hello odbieranie usługi sieci web. Witaj toofind identyfikator URI aplikacji w hello portalu Azure, kliknij przycisk **usługi Active Directory**kliknij katalog hello, kliknij przycisk aplikacji hello, a następnie kliknij przycisk **Konfiguruj**. |

Należy zauważyć, że parametry hello są prawie hello takie same jak przypadku hello hello żądania przez Wspólny klucz tajny z tą różnicą, że parametr client_secret hello zostało zastąpione przez dwa parametry: client_assertion_type i client_assertion.

#### Przykład
powitania po POST protokołu HTTP żądania tokenu dostępu dla usługi sieci web https://service.contoso.com/ hello przy użyciu certyfikatu. Witaj `client_id` identyfikuje usługi sieci web hello żądań hello tokenu dostępu.

```
POST /<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

resource=https%3A%2F%contoso.onmicrosoft.com%2Ffc7664b4-cdd6-43e1-9365-c2e1c4e1b3bf&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

### Odpowiedzi tokenu dostępu do usługi

Odpowiedź sukcesu zawiera odpowiedzi JSON OAuth 2.0 z hello następujące parametry:

| Parametr | Opis |
| --- | --- |
| ' access_token ' |token dostępu do żądanego Hello. Witaj wywoływania usługi sieci web można użyć tego toohello tokenu tooauthenticate odbieranie usługi sieci web. |
| token_type |Wskazuje wartość tokenu typu hello. Witaj tylko typ, który obsługuje usługę Azure AD **elementu nośnego**. Aby uzyskać więcej informacji na temat tokenów elementu nośnego, zobacz hello [OAuth 2.0 autoryzacji Framework: użycie tokenu elementu nośnego (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| expires_in |Jak długo hello token dostępu jest nieprawidłowy (w sekundach). |
| expires_on |Witaj czas wygaśnięcia tokenu dostępu hello. Data Hello jest reprezentowany jako hello liczbę sekund z rokiem 1970-01-01T0:0:0Z UTC czasu wygaśnięcia hello. Ta wartość jest używane toodetermine hello okres istnienia pamięci podręcznej tokenów. |
| not_before |czas Hello, z których hello nadaje się tokenu dostępu. Data Hello jest reprezentowany jako hello liczbę sekund z rokiem 1970-01-01T0:0:0Z UTC czasu ważności tokenu hello.|
| Zasobów |Witaj identyfikator URI aplikacji hello odbieranie usługi sieci web. |

#### Przykład odpowiedzi
Witaj poniższy przykład przedstawia Powodzenie odpowiedzi tooa żądanie usługi sieci web tooa tokenu dostępu.

```
{
"access_token":"eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0ODI2NywibmJmIjoxMzg4NDQ4MjY3LCJleHAiOjEzODg0NTIxNjcsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsInN1YiI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZS8iLCJhcHBpZCI6ImQxN2QxNWJjLWM1NzYtNDFlNS05MjdmLWRiNWYzMGRkNThmMSIsImFwcGlkYWNyIjoiMSJ9.aqtfJ7G37CpKV901Vm9sGiQhde0WMg6luYJR4wuNR2ffaQsVPPpKirM5rbc6o5CmW1OtmaAIdwDcL6i9ZT9ooIIicSRrjCYMYWHX08ip-tj-uWUihGztI02xKdWiycItpWiHxapQm0a8Ti1CWRjJghORC1B1-fah_yWx6Cjuf4QE8xJcu-ZHX0pVZNPX22PHYV5Km-vPTq2HtIqdboKyZy3Y4y3geOrRIFElZYoqjqSv5q9Jgtj5ERsNQIjefpyxW3EwPtFqMcDm4ebiAEpoEWRN4QYOMxnC9OUBeG9oLA0lTfmhgHLAtvJogJcYFzwngTsVo6HznsvPWy7UP3MINA",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://service.contoso.com/"
}
```

## Zobacz też
* [OAuth 2.0 w usłudze Azure AD](active-directory-protocols-oauth-code.md)
* [Przykład w języku C# hello wywołania tooservice usługi z wspólny klucz tajny](https://github.com/Azure-Samples/active-directory-dotnet-daemon) i [próbki w języku C# hello wywołania tooservice usługi przy użyciu certyfikatu](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential)
