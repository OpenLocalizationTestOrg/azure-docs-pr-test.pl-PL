---
title: "aaaCertificate poświadczeń w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono hello rejestracji i stosowania certyfikatu poświadczeń dla uwierzytelniania aplikacji"
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 3508803112ac06268d553db86ab74812aa53e455
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-credentials-for-application-authentication"></a>Certyfikat poświadczeń do uwierzytelniania aplikacji

Usługa Azure Active Directory umożliwia toouse aplikacji własne poświadczenia dla uwierzytelniania, na przykład w hello przepływ udzielania poświadczeń klienta OAuth w 2.0 i hello imieniu-przepływ "w".
Jeden formularz poświadczeniami, które mogą być używane jest potwierdzenie Token(JWT) sieci Web JSON, podpisanego przy użyciu certyfikatu, który jest właścicielem aplikacji hello.

## <a name="format-of-hello-assertion"></a>Format hello potwierdzenia
Potwierdzenie hello toocompute, prawdopodobnie potrzebna będzie toouse jedną hello wiele [JSON Web Token](https://jwt.io/) bibliotek w dowolnie wybranym języku hello. informacje o Hello przez hello token są:

#### <a name="header"></a>Nagłówek

| Parametr |  Uwagi |
| --- | --- | --- |
| `alg` | Powinien być **RS256** |
| `typ` | Powinien być **JWT** |
| `x5t` | Powinien być odcisk palca certyfikatu X.509 SHA-1 hello |

#### <a name="claims-payload"></a>Oświadczenia (ładunku)

| Parametr |  Uwagi |
| --- | --- | --- |
| `aud` | Grupy odbiorców: Powinien być  **https://login.microsoftonline.com/*tenant_Id*  /oauth2/token ** |
| `exp` | Data wygaśnięcia: hello daty wygaśnięcia tokenu hello. czas Hello jest reprezentowany jako hello liczba sekund od 1 stycznia 1970 (1970-01-01T0:0:0Z) UTC do momentu wygaśnięcia hello hello czas ważności tokenu.|
| `iss` | Wystawca: powinien być client_id hello (identyfikator aplikacji hello usługi klienta) |
| `jti` | Identyfikator GUID: hello identyfikator JWT |
| `nbf` | Nie wcześniej niż: hello data przed hello, których nie można użyć tokenu. czas Hello jest reprezentowany jako hello liczba sekund od 1 stycznia 1970 (1970-01-01T0:0:0Z) UTC, dopóki hello czasu hello token został wystawiony. |
| `sub` | Podmiot: jak w przypadku `iss`, powinny być client_id hello (identyfikator aplikacji hello usługi klienta) |

#### <a name="signature"></a>Podpis
Podpis Hello jest obliczana stosowania hello certyfikatu zgodnie z opisem w hello [specyfikacji RFC7519 tokenu Web JSON](https://tools.ietf.org/html/rfc7519)

### <a name="example-of-a-decoded-jwt-assertion"></a>Przykład dekodowane potwierdzenia JWT
```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

### <a name="example-of-an-encoded-jwt-assertion"></a>Przykład zakodowanego potwierdzenia JWT
po ciągu Hello jest przykładem zakodowanego potwierdzenia. Zwróć uwagę, można zauważyć trzy części oddzielone kropkami (.).
Pierwsza sekcja Hello koduje hello nagłówka, drugi ładunek hello hello i hello jest ostatni hello podpisem obliczonym przy certyfikaty powitania od zawartości hello hello pierwsze dwie sekcje.
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a>Zarejestruj certyfikat z usługą Azure AD
tooassociate hello certyfikat poświadczeń z powitania klienta aplikacji w usłudze Azure AD, należy w manifeście aplikacji hello tooedit.
Posiadanie wstrzymywania certyfikatu, należy toocompute:
- `$base64Thumbprint`, które hello kodowanie base64 certyfikatu hello wyznaczania wartości skrótu
- `$base64Value`, które hello kodowanie base64 hello dane pierwotne certyfikatu

należy również tooprovide klucz hello tooidentify identyfikatora GUID w manifeście aplikacji hello (`$keyId`)

Manifest aplikacji hello Otwórz hello rejestracji aplikacji platformy Azure dla aplikacji klienckiej hello i Zastąp hello *keyCredentials* właściwości z informacjami certyfikatu przy użyciu hello następującego schematu:
```
"keyCredentials": [
    {
        "customKeyIdentifier": "$base64Thumbprint",
        "keyId": "$keyid",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value":  "$base64Value"
    }
]
```

Zapisz hello toohello edycji w manifeście aplikacji i przekazać tooAzure AD. Właściwość keyCredentials Hello jest wielokrotne wartości, więc może przekazać wiele certyfikatów bardziej zaawansowane funkcje zarządzania kluczami.
