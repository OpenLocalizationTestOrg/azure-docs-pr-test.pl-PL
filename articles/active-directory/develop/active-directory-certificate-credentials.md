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
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="0565a-103">Certyfikat poświadczeń do uwierzytelniania aplikacji</span><span class="sxs-lookup"><span data-stu-id="0565a-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="0565a-104">Usługa Azure Active Directory umożliwia toouse aplikacji własne poświadczenia dla uwierzytelniania, na przykład w hello przepływ udzielania poświadczeń klienta OAuth w 2.0 i hello imieniu-przepływ "w".</span><span class="sxs-lookup"><span data-stu-id="0565a-104">Azure Active Directory allows an application toouse its own credentials for authentication, for example, in hello OAuth 2.0 Client Credentials Grant flow and hello On-Behalf-Of flow.</span></span>
<span data-ttu-id="0565a-105">Jeden formularz poświadczeniami, które mogą być używane jest potwierdzenie Token(JWT) sieci Web JSON, podpisanego przy użyciu certyfikatu, który jest właścicielem aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0565a-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that hello application owns.</span></span>

## <a name="format-of-hello-assertion"></a><span data-ttu-id="0565a-106">Format hello potwierdzenia</span><span class="sxs-lookup"><span data-stu-id="0565a-106">Format of hello assertion</span></span>
<span data-ttu-id="0565a-107">Potwierdzenie hello toocompute, prawdopodobnie potrzebna będzie toouse jedną hello wiele [JSON Web Token](https://jwt.io/) bibliotek w dowolnie wybranym języku hello.</span><span class="sxs-lookup"><span data-stu-id="0565a-107">toocompute hello assertion, you probably want toouse one of hello many [JSON Web Token](https://jwt.io/) libraries in hello language of your choice.</span></span> <span data-ttu-id="0565a-108">informacje o Hello przez hello token są:</span><span class="sxs-lookup"><span data-stu-id="0565a-108">hello information carried by hello token is:</span></span>

#### <a name="header"></a><span data-ttu-id="0565a-109">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="0565a-109">Header</span></span>

| <span data-ttu-id="0565a-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="0565a-110">Parameter</span></span> |  <span data-ttu-id="0565a-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="0565a-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="0565a-112">Powinien być **RS256**</span><span class="sxs-lookup"><span data-stu-id="0565a-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="0565a-113">Powinien być **JWT**</span><span class="sxs-lookup"><span data-stu-id="0565a-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="0565a-114">Powinien być odcisk palca certyfikatu X.509 SHA-1 hello</span><span class="sxs-lookup"><span data-stu-id="0565a-114">Should be hello X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="0565a-115">Oświadczenia (ładunku)</span><span class="sxs-lookup"><span data-stu-id="0565a-115">Claims (Payload)</span></span>

| <span data-ttu-id="0565a-116">Parametr</span><span class="sxs-lookup"><span data-stu-id="0565a-116">Parameter</span></span> |  <span data-ttu-id="0565a-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="0565a-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="0565a-118">Grupy odbiorców: Powinien być  **https://login.microsoftonline.com/*tenant_Id*  /oauth2/token **</span><span class="sxs-lookup"><span data-stu-id="0565a-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="0565a-119">Data wygaśnięcia: hello daty wygaśnięcia tokenu hello.</span><span class="sxs-lookup"><span data-stu-id="0565a-119">Expiration date: hello date when hello token expires.</span></span> <span data-ttu-id="0565a-120">czas Hello jest reprezentowany jako hello liczba sekund od 1 stycznia 1970 (1970-01-01T0:0:0Z) UTC do momentu wygaśnięcia hello hello czas ważności tokenu.</span><span class="sxs-lookup"><span data-stu-id="0565a-120">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token validity expires.</span></span>|
| `iss` | <span data-ttu-id="0565a-121">Wystawca: powinien być client_id hello (identyfikator aplikacji hello usługi klienta)</span><span class="sxs-lookup"><span data-stu-id="0565a-121">Issuer: should be hello client_id (Application Id of hello client service)</span></span> |
| `jti` | <span data-ttu-id="0565a-122">Identyfikator GUID: hello identyfikator JWT</span><span class="sxs-lookup"><span data-stu-id="0565a-122">GUID: hello JWT ID</span></span> |
| `nbf` | <span data-ttu-id="0565a-123">Nie wcześniej niż: hello data przed hello, których nie można użyć tokenu.</span><span class="sxs-lookup"><span data-stu-id="0565a-123">Not Before: hello date before which hello token cannot be used.</span></span> <span data-ttu-id="0565a-124">czas Hello jest reprezentowany jako hello liczba sekund od 1 stycznia 1970 (1970-01-01T0:0:0Z) UTC, dopóki hello czasu hello token został wystawiony.</span><span class="sxs-lookup"><span data-stu-id="0565a-124">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token was issued.</span></span> |
| `sub` | <span data-ttu-id="0565a-125">Podmiot: jak w przypadku `iss`, powinny być client_id hello (identyfikator aplikacji hello usługi klienta)</span><span class="sxs-lookup"><span data-stu-id="0565a-125">Subject: As for `iss`, should be hello client_id (Application Id of hello client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="0565a-126">Podpis</span><span class="sxs-lookup"><span data-stu-id="0565a-126">Signature</span></span>
<span data-ttu-id="0565a-127">Podpis Hello jest obliczana stosowania hello certyfikatu zgodnie z opisem w hello [specyfikacji RFC7519 tokenu Web JSON](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="0565a-127">hello signature is computed applying hello certificate as described in hello [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="0565a-128">Przykład dekodowane potwierdzenia JWT</span><span class="sxs-lookup"><span data-stu-id="0565a-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="0565a-129">Przykład zakodowanego potwierdzenia JWT</span><span class="sxs-lookup"><span data-stu-id="0565a-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="0565a-130">po ciągu Hello jest przykładem zakodowanego potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="0565a-130">hello following string is an example of encoded assertion.</span></span> <span data-ttu-id="0565a-131">Zwróć uwagę, można zauważyć trzy części oddzielone kropkami (.).</span><span class="sxs-lookup"><span data-stu-id="0565a-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="0565a-132">Pierwsza sekcja Hello koduje hello nagłówka, drugi ładunek hello hello i hello jest ostatni hello podpisem obliczonym przy certyfikaty powitania od zawartości hello hello pierwsze dwie sekcje.</span><span class="sxs-lookup"><span data-stu-id="0565a-132">hello first section encodes hello header, hello second hello payload, and hello last is hello signature computed with hello certificates from hello content of hello first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="0565a-133">Zarejestruj certyfikat z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="0565a-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="0565a-134">tooassociate hello certyfikat poświadczeń z powitania klienta aplikacji w usłudze Azure AD, należy w manifeście aplikacji hello tooedit.</span><span class="sxs-lookup"><span data-stu-id="0565a-134">tooassociate hello certificate credential with hello client application in Azure AD, you need tooedit hello application manifest.</span></span>
<span data-ttu-id="0565a-135">Posiadanie wstrzymywania certyfikatu, należy toocompute:</span><span class="sxs-lookup"><span data-stu-id="0565a-135">Having hold of a certificate, you need toocompute:</span></span>
- <span data-ttu-id="0565a-136">`$base64Thumbprint`, które hello kodowanie base64 certyfikatu hello wyznaczania wartości skrótu</span><span class="sxs-lookup"><span data-stu-id="0565a-136">`$base64Thumbprint`, which is hello base64 encoding of hello certificate Hash</span></span>
- <span data-ttu-id="0565a-137">`$base64Value`, które hello kodowanie base64 hello dane pierwotne certyfikatu</span><span class="sxs-lookup"><span data-stu-id="0565a-137">`$base64Value`, which is hello base64 encoding of hello certificate raw data</span></span>

<span data-ttu-id="0565a-138">należy również tooprovide klucz hello tooidentify identyfikatora GUID w manifeście aplikacji hello (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="0565a-138">you also need tooprovide a GUID tooidentify hello key in hello application manifest (`$keyId`)</span></span>

<span data-ttu-id="0565a-139">Manifest aplikacji hello Otwórz hello rejestracji aplikacji platformy Azure dla aplikacji klienckiej hello i Zastąp hello *keyCredentials* właściwości z informacjami certyfikatu przy użyciu hello następującego schematu:</span><span class="sxs-lookup"><span data-stu-id="0565a-139">In hello Azure app registration for hello client application, open hello application manifest, and replace hello *keyCredentials* property with your new certificate information using hello following schema:</span></span>
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

<span data-ttu-id="0565a-140">Zapisz hello toohello edycji w manifeście aplikacji i przekazać tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="0565a-140">Save hello edits toohello application manifest, and upload tooAzure AD.</span></span> <span data-ttu-id="0565a-141">Właściwość keyCredentials Hello jest wielokrotne wartości, więc może przekazać wiele certyfikatów bardziej zaawansowane funkcje zarządzania kluczami.</span><span class="sxs-lookup"><span data-stu-id="0565a-141">hello keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
