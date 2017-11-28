---
title: "Uwierzytelnianie tooservice usługi aaaAzure AD przy użyciu OAuth2.0 specyfikacji w imieniu — z projektu | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse HTTP wiadomości tooimplement tooservice uwierzytelnianie usługi przy użyciu hello OAuth2.0 imieniu-przepływ \"w\"."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 09f6f318-e88b-4024-9ee1-e7f09fb19a82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 55b7fcfe6c0223bddedd8d8fa2defcb5769b43c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Wywołuje tooservice usługi przy użyciu tożsamości użytkownika delegowanego w imieniu-przepływ "w" hello
Witaj przepływu OAuth 2.0 On-Behalf-Of służy hello przypadek użycia gdzie aplikacja wywołuje usługi/składnika web API, który z kolei musi toocall innej usługi/interfejs API sieci web. pomysł Hello jest toopropagate hello delegowane uprawnienia za pomocą hello łańcucha żądań i tożsamości użytkowników. Dla hello warstwy środkowej toomake uwierzytelnić żądania toohello podrzędne usługi musi on toosecure token dostępu z usługi Azure Active Directory (Azure AD), w imieniu użytkownika hello.

## W imieniu — z diagram przepływu
Załóżmy, że hello użytkownik został uwierzytelniony w aplikacji przy użyciu hello [kodu autoryzacji protokołu OAuth 2.0 przyznać przepływu](active-directory-protocols-oauth-code.md). W tym momencie aplikacji hello ma token dostępu (token A) z oświadczeń użytkownika hello i zgody tooaccess hello warstwy środkowej interfejsu API sieci web (A interfejsu API). Teraz A interfejsu API musi toomake żądania uwierzytelnionego toohello podrzędne interfejsu API sieci web (interfejs API B).

Hello czynności, które wykonują stanowią hello imieniu-przepływ "w" i opisano szczegółowo za pomocą hello powitania po diagramu.

![OAuth2.0 imieniu-przepływ "w"](media/active-directory-protocols-oauth-on-behalf-of/active-directory-protocols-oauth-on-behalf-of-flow.png)


1. Aplikacja kliencka Hello sprawia, że tooAPI żądania A z hello tokenu A.
2. Interfejs API A uwierzytelnia punkt końcowy wystawiania tokenu usługi Azure AD toohello i żądania tokenu tooaccess B. interfejsu API
3. punkt końcowy wystawiania tokenu usługi Azure AD Hello weryfikuje poświadczenia A interfejsu API z tokenów w przypadku i problemy hello tokenu dostępu dla interfejsu API B (token B).
4. Hello token B znajduje się w nagłówku autoryzacji hello hello żądania tooAPI B.
5. Dane hello zabezpieczonych zasobów jest zwracane przez interfejs API B.

## Rejestrowanie aplikacji hello i usługi w usłudze Azure AD
Zarejestruj zarówno hello aplikacji klienckiej i usługi warstwy środkowej hello w usłudze Azure AD.
### Zarejestruj usługę warstwy środkowej hello
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku hello, kliknij na Twoim koncie, a w obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, którym chcesz tooregister aplikacji.
3. Polecenie **więcej usług** w hello nawigacji po lewej stronie i wybierz polecenie **usługi Azure Active Directory**.
4. Polecenie **rejestracji aplikacji** i wybierz polecenie **nowej rejestracji aplikacji**.
5. Wprowadź przyjazną nazwę dla aplikacji hello i wybierz typ aplikacji hello. Na podstawie typu aplikacji hello zestaw hello adres URL logowania lub podstawowy adres URL przekierowania adresu URL toohello. Polecenie **Utwórz** toocreate hello aplikacji.
6. Podczas jeszcze hello portalu Azure, wybierz aplikację, a następnie kliknij przycisk na **ustawienia**. Z menu Ustawienia hello, wybierz **klucze** i Dodaj klucz — wybierz czas trwania klucza roku 1 lub 2 lata. Po zapisaniu tej strony, wartość klucza hello będą wyświetlane, skopiuj i Zapisz wartość hello w bezpiecznym miejscu — tego klucza nowsze tooconfigure hello ustawienia aplikacji będą potrzebne w implementacji — wartość tego klucza nie będą wyświetlane ponownie ani pobieranie według dowolnej inny sposób, dlatego należy rekordu go jak najszybciej nie jest widoczny hello portalu Azure.

### Zarejestruj powitania klienta aplikacji
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku hello, kliknij na Twoim koncie, a w obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, którym chcesz tooregister aplikacji.
3. Polecenie **więcej usług** w hello nawigacji po lewej stronie i wybierz polecenie **usługi Azure Active Directory**.
4. Polecenie **rejestracji aplikacji** i wybierz polecenie **nowej rejestracji aplikacji**.
5. Wprowadź przyjazną nazwę dla aplikacji hello i wybierz typ aplikacji hello. Na podstawie typu aplikacji hello zestaw hello adres URL logowania lub podstawowy adres URL przekierowania adresu URL toohello. Polecenie **Utwórz** toocreate hello aplikacji.
6. Konfigurowania uprawnień dla aplikacji - w menu Ustawienia hello, wybierz hello **wymagane uprawnienia** kliknij na **Dodaj**, następnie **wybierz interfejs API**i hello typu Nazwa usługi warstwy środkowej hello w polu tekstowym hello. Następnie kliknij **wybierz uprawnienia** i wybierz pozycję "dostępu *nazwa usługi*".

### Skonfiguruj aplikacje klienckie znane
W tym scenariuszu usługa warstwy środkowej hello ma nie interakcji tooobtain hello użytkownik użytkownika zgody podrzędne interfejsu API tooaccess hello. W związku z tym hello toohello dostępu toogrant opcji podrzędne interfejsu API musi zostać przedstawione góry w ramach kroku zgody hello podczas uwierzytelniania.
tooachieve, wykonaj czynności hello tooexplicitly bind powitania klienta rejestracji aplikacji w usłudze Azure AD z rejestracją hello hello średniego poziomu usługi, która scala zgody hello wymagane przez powitania klienta i warstwy środkowej w jednym oknie dialogowym.
1. Przejdź toohello rejestracji usługi warstwy środkowej, a następnie kliknij polecenie **manifestu** tooopen hello manifestu edytora.
2. W manifeście hello zlokalizować hello `knownClientApplications` tablicy właściwości, a następnie dodaj hello identyfikator klienta aplikacji klienckiej hello jako elementu.
3. Zapisz hello manifest klikając hello przycisk zapisywania.

## Żądanie tokenu dostępu usługi tooservice
toorequest tokenu dostępu, dzięki hello następujące parametry punktu końcowego HTTP POST toohello specyficznego dla dzierżawy usługi Azure AD.

```
https://login.microsoftonline.com/<tenant>/oauth2/token
```
Istnieją dwa przypadki, w zależności od tego, czy aplikacja kliencka hello wybierze toobe zabezpieczone przez Wspólny klucz tajny lub certyfikatu.

### Najpierw przypadek: żądanie tokenu dostępu z wspólny klucz tajny
Korzystając z wspólny klucz tajny, żądania tokenu dostępu do usługi zawiera hello następujące parametry:

| Parametr |  | Opis |
| --- | --- | --- |
| Typ grant_type |Wymagane | Typ Hello hello żądania tokenu. Dla żądania przy użyciu token JWT, hello wartość musi być **urn: ietf:params:oauth:grant — typ: jwt-elementu nośnego**. |
| Potwierdzenia |Wymagane | wartość Hello hello token użyty w żądaniu hello. |
| client_id |Wymagane | Witaj identyfikator aplikacji przypisany toohello wywoływania usługi podczas rejestracji w usłudze Azure AD. Kliknij toofind hello identyfikator aplikacji w portalu zarządzania Azure, hello **usługi Active Directory**, kliknij przycisk hello katalog, a następnie kliknij nazwę aplikacji hello. |
| client_secret |Wymagane | klucz Hello zarejestrowanym hello wywoływania usługi w usłudze Azure AD. Ta wartość powinna zauważyć w czasie hello rejestracji. |
| Zasobów |Wymagane | Witaj identyfikator URI aplikacji hello odbieranie usługi (zabezpieczonych zasobów). Kliknij toofind hello identyfikator URI aplikacji w portalu zarządzania Azure, hello **usługi Active Directory**, kliknij przycisk hello katalogu, kliknij nazwę aplikacji hello, kliknij przycisk **wszystkie ustawienia** , a następnie kliknij przycisk **właściwości** . |
| requested_token_use |Wymagane | Określa sposób przetwarzania żądań hello. W imieniu-przepływ "w" hello, musi być wartością hello **on_behalf_of**. |
| Zakres |Wymagane | Lista zakresów dla żądania tokenu hello rozdzielonych spacją. Dla protokołu OpenID Connect, hello zakresu **openid** musi być określona.|

#### Przykład
Hello następujące POST protokołu HTTP żądania tokenu dostępu dla sieci web https://graph.windows.net hello interfejsu API. Witaj `client_id` identyfikuje hello usługa, która żąda hello tokenu dostępu.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_secret=0Y1W%2BY3yYb3d9N8vSjvm8WrGzVZaAaHbHHcGbcgG%2BoI%3D
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

### W drugim przypadku: żądanie tokenu dostępu przy użyciu certyfikatu
Żądanie tokenu dostępu do usługi przy użyciu certyfikatu zawiera hello następujące parametry:

| Parametr |  | Opis |
| --- | --- | --- |
| Typ grant_type |Wymagane | Typ Hello hello żądania tokenu. Dla żądania przy użyciu token JWT, hello wartość musi być **urn: ietf:params:oauth:grant — typ: jwt-elementu nośnego**. |
| Potwierdzenia |Wymagane | wartość Hello hello token użyty w żądaniu hello. |
| client_id |Wymagane | Witaj identyfikator aplikacji przypisany toohello wywoływania usługi podczas rejestracji w usłudze Azure AD. Kliknij toofind hello identyfikator aplikacji w portalu zarządzania Azure, hello **usługi Active Directory**, kliknij przycisk hello katalog, a następnie kliknij nazwę aplikacji hello. |
| client_assertion_type |Wymagane |Witaj, wartość musi być`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |Wymagane | Potwierdzeniem (JSON Web Token) czy potrzebujesz toocreate oraz znak hello certyfikatu można zarejestrowany jako poświadczeń dla aplikacji.  Przeczytaj informacje o [certyfikatu poświadczeń](active-directory-certificate-credentials.md) toolearn jak tooregister Twojego certyfikatu i hello format hello potwierdzenia.|
| Zasobów |Wymagane | Witaj identyfikator URI aplikacji hello odbieranie usługi (zabezpieczonych zasobów). Kliknij toofind hello identyfikator URI aplikacji w portalu zarządzania Azure, hello **usługi Active Directory**, kliknij przycisk hello katalogu, kliknij nazwę aplikacji hello, kliknij przycisk **wszystkie ustawienia** , a następnie kliknij przycisk **właściwości** . |
| requested_token_use |Wymagane | Określa sposób przetwarzania żądań hello. W imieniu-przepływ "w" hello, musi być wartością hello **on_behalf_of**. |
| Zakres |Wymagane | Lista zakresów dla żądania tokenu hello rozdzielonych spacją. Dla protokołu OpenID Connect, hello zakresu **openid** musi być określona.|

Należy zauważyć, że parametry hello są prawie hello takie same jak przypadku hello hello żądania przez Wspólny klucz tajny z tą różnicą, że parametr client_secret hello zostało zastąpione przez dwa parametry: client_assertion_type i client_assertion.

#### Przykład
powitania po POST protokołu HTTP żądania tokenu dostępu dla hello https://graph.windows.net interfejsu API sieci web przy użyciu certyfikatu. Witaj `client_id` identyfikuje hello usługa, która żąda hello tokenu dostępu.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

## Usługa odpowiedzi tokenu dostępu tooservice
Odpowiedź sukcesu jest odpowiedź JSON OAuth 2.0 z hello następujące parametry.

| Parametr | Opis |
| --- | --- |
| token_type |Wskazuje wartość tokenu typu hello. Witaj tylko typ, który obsługuje usługę Azure AD **elementu nośnego**. Aby uzyskać więcej informacji na temat tokenów elementu nośnego, zobacz hello [OAuth 2.0 autoryzacji Framework: użycie tokenu elementu nośnego (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| Zakres |zakres Hello udzielono hello tokenu dostępu. |
| expires_in |Długość Hello tokenu dostępu hello czasu jest prawidłowy (w sekundach). |
| expires_on |Witaj czas wygaśnięcia tokenu dostępu hello. Data Hello jest reprezentowany jako hello liczbę sekund z rokiem 1970-01-01T0:0:0Z UTC czasu wygaśnięcia hello. Ta wartość jest używane toodetermine hello okres istnienia pamięci podręcznej tokenów. |
| Zasobów |Witaj identyfikator URI aplikacji hello odbieranie usługi (zabezpieczonych zasobów). |
| ' access_token ' |token dostępu do żądanego Hello. Witaj wywoływania usługi można użyć tej usługi odbierania toohello tooauthenticate tokenu. |
| żądaniu |Witaj token żądanym identyfikatorem. Hello wywoływania usługi można użyć tego tooverify hello tożsamości użytkownika i rozpocząć sesję użytkownika hello. |
| refresh_token |token odświeżania Hello hello żądanego tokenu dostępu. Hello wywoływania usługi można użyć z tym token toorequest inny token dostępu po wygaśnięciu tokenu dostępu bieżącego hello. |

### Przykład odpowiedź sukcesu
Witaj poniższy przykład przedstawia żądania tooa odpowiedź sukcesu token dostępu dla hello interfejsu API sieci web https://graph.windows.net.

```
{
    "token_type":"Bearer",
    "scope":"User.Read",
    "expires_in":"43482",
    "ext_expires_in":"302683",
    "expires_on":"1493466951",
    "not_before":"1493423168",
    "resource":"https://graph.windows.net",
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ",
    "refresh_token":"AQABAAAAAABnfiG-mA6NTae7CdWW7QfdjKGu9-t1scy_TDEmLi4eLQMjJGt_nAoVu6A4oSu1KsRiz8XyQIPKQxSGfbf2FoSK-hm2K8TYzbJuswYusQpJaHUQnSqEvdaCeFuqXHBv84wjFhuanzF9dQZB_Ng5za9xKlUENrNtlq9XuLNVKzxEyeUM7JyxzdY7JiEphWImwgOYf6II316d0Z6-H3oYsFezf4Xsjz-MOBYEov0P64UaB5nJMvDyApV-NWpgklLASfNoSPGb67Bc02aFRZrm4kLk-xTl6eKE6hSo0XU2z2t70stFJDxvNQobnvNHrAmBaHWPAcC3FGwFnBOojpZB2tzG1gLEbmdROVDp8kHEYAwnRK947Py12fJNKExUdN0njmXrKxNZ_fEM33LHW1Tf4kMX_GvNmbWHtBnIyG0w5emb-b54ef5AwV5_tGUeivTCCysgucEc-S7G8Cz0xNJ_BOiM_4bAv9iFmrm9STkltpz0-Tftg8WKmaJiC0xXj6uTf4ZkX79mJJIuuM7XP4ARIcLpkktyg2Iym9jcZqymRkGH2Rm9sxBwC4eeZXM7M5a7TJ-5CqOdfuE3sBPq40RdEWMFLcrAzFvP0VDR8NKHIrPR1AcUruat9DETmTNJukdlJN3O41nWdZOVoJM-uKN3uz2wQ2Ld1z0Mb9_6YfMox9KTJNzRzcL52r4V_y3kB6ekaOZ9wQ3HxGBQ4zFt-2U0mSszIAA",
    "id_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IvIiwiaWF0IjoxNDkzNDIzMTY4LCJuYmYiOjE0OTM0MjMxNjgsImV4cCI6MTQ5MzQ2Njk1MSwiYW1yIjpbInB3ZCJdLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXRpIjoieEN3ZnpoYS1QMFdKUU9MeENHZ0tBQSIsInZlciI6IjEuMCJ9."
}
```

### Przykład odpowiedzi błędu
Odpowiedzi na błąd jest zwracany przez punkt końcowy tokenu usługi Azure AD podczas próby tooacquire token dostępu hello podrzędne interfejsu API, gdy zasady dostępu warunkowego, takich jak uwierzytelnianie wieloskładnikowe, ustaw w niej ma hello podrzędne interfejsu API. Usługa warstwy środkowej Hello powinien powierzchni aplikacji klienta toohello błąd tak, aby aplikacja kliencka hello zapewniają zasady dostępu warunkowego hello toosatisfy interakcji użytkownika hello.

```
{
    "error":"interaction_required",
    "error_description":"AADSTS50079: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must enroll in multi-factor authentication tooaccess 'bf8d80f9-9098-4972-b203-500f535113b1'.\r\nTrace ID: b72a68c3-0926-4b8e-bc35-3150069c2800\r\nCorrelation ID: 73d656cf-54b1-4eb2-b429-26d8165a52d7\r\nTimestamp: 2017-05-01 22:43:20Z",
    "error_codes":[50079],
    "timestamp":"2017-05-01 22:43:20Z",
    "trace_id":"b72a68c3-0926-4b8e-bc35-3150069c2800",
    "correlation_id":"73d656cf-54b1-4eb2-b429-26d8165a52d7",
    "claims":"{\"access_token\":{\"polids\":{\"essential\":true,\"values\":[\"9ab03e19-ed42-4168-b6b7-7001fb3e933a\"]}}}"
}
```

## Użyj hello tooaccess tokenu dostępu hello zabezpieczonych zasobów
Teraz usługi warstwy środkowej hello używać downstream toohello żądania tokenu toomake nabytych przez niego powyżej uwierzytelniony hello interfejs API, sieci web przez ustawienie token hello w hello `Authorization` nagłówka.

### Przykład
```
GET /me?api-version=2013-11-08 HTTP/1.1
Host: graph.windows.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ
```

## Następne kroki
Dowiedz się więcej o protokół OAuth 2.0 hello i inny sposób tooperform usługi tooservice uwierzytelniania przy użyciu poświadczeń klienta.
* [Usługa tooservice uwierzytelniania przy użyciu przyznania poświadczeń klienta OAuth 2.0 w usłudze Azure AD](active-directory-protocols-oauth-service-to-service.md)
* [OAuth 2.0 w usłudze Azure AD](active-directory-protocols-oauth-code.md)
