---
title: "Certyfikat poświadczeń w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono rejestracji i stosowania certyfikatu poświadczeń dla uwierzytelniania aplikacji"
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
ms.openlocfilehash: 08bb5140bb35bbd120aaa506afeab8ad247f81e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="d7ba7-103">Certyfikat poświadczeń do uwierzytelniania aplikacji</span><span class="sxs-lookup"><span data-stu-id="d7ba7-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="d7ba7-104">Usługi Azure Active Directory umożliwia aplikacji korzystanie własne poświadczenia dla uwierzytelniania, na przykład przepływ udzielania poświadczeń klienta OAuth w 2.0 i przepływu w imieniu-z.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-104">Azure Active Directory allows an application to use its own credentials for authentication, for example, in the OAuth 2.0 Client Credentials Grant flow and the On-Behalf-Of flow.</span></span>
<span data-ttu-id="d7ba7-105">Jeden formularz poświadczeniami, które mogą być używane jest potwierdzenie Token(JWT) sieci Web JSON, podpisanego przy użyciu certyfikatu, który jest właścicielem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that the application owns.</span></span>

## <a name="format-of-the-assertion"></a><span data-ttu-id="d7ba7-106">Format potwierdzenia</span><span class="sxs-lookup"><span data-stu-id="d7ba7-106">Format of the assertion</span></span>
<span data-ttu-id="d7ba7-107">Do obliczenia potwierdzenia, prawdopodobnie chcesz skorzystać z jednej z wielu [JSON Web Token](https://jwt.io/) bibliotek w wybranym języku.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-107">To compute the assertion, you probably want to use one of the many [JSON Web Token](https://jwt.io/) libraries in the language of your choice.</span></span> <span data-ttu-id="d7ba7-108">Informacje przez token jest:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-108">The information carried by the token is:</span></span>

#### <a name="header"></a><span data-ttu-id="d7ba7-109">Nagłówek</span><span class="sxs-lookup"><span data-stu-id="d7ba7-109">Header</span></span>

| <span data-ttu-id="d7ba7-110">Parametr</span><span class="sxs-lookup"><span data-stu-id="d7ba7-110">Parameter</span></span> |  <span data-ttu-id="d7ba7-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d7ba7-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="d7ba7-112">Powinien być **RS256**</span><span class="sxs-lookup"><span data-stu-id="d7ba7-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="d7ba7-113">Powinien być **JWT**</span><span class="sxs-lookup"><span data-stu-id="d7ba7-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="d7ba7-114">Powinien być odcisk palca certyfikatu X.509 SHA-1.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-114">Should be the X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="d7ba7-115">Oświadczenia (ładunku)</span><span class="sxs-lookup"><span data-stu-id="d7ba7-115">Claims (Payload)</span></span>

| <span data-ttu-id="d7ba7-116">Parametr</span><span class="sxs-lookup"><span data-stu-id="d7ba7-116">Parameter</span></span> |  <span data-ttu-id="d7ba7-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d7ba7-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="d7ba7-118">Grupy odbiorców: Powinien być  **https://login.microsoftonline.com/*tenant_Id*  /oauth2/token **</span><span class="sxs-lookup"><span data-stu-id="d7ba7-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="d7ba7-119">Data wygaśnięcia: Data wygaśnięcia tokenu.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-119">Expiration date: the date when the token expires.</span></span> <span data-ttu-id="d7ba7-120">Czas jest reprezentowany jako liczba sekund od 1 stycznia 1970 (1970-01-01T0:0:0Z) UTC czasu wygaśnięcia ważności tokenu.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-120">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.</span></span>|
| `iss` | <span data-ttu-id="d7ba7-121">Wystawca: powinien być client_id (identyfikator aplikacji usługi klienta)</span><span class="sxs-lookup"><span data-stu-id="d7ba7-121">Issuer: should be the client_id (Application Id of the client service)</span></span> |
| `jti` | <span data-ttu-id="d7ba7-122">Identyfikator GUID: identyfikator JWT</span><span class="sxs-lookup"><span data-stu-id="d7ba7-122">GUID: the JWT ID</span></span> |
| `nbf` | <span data-ttu-id="d7ba7-123">Nie wcześniej niż: Data przed którym nie można użyć tokenu.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-123">Not Before: the date before which the token cannot be used.</span></span> <span data-ttu-id="d7ba7-124">Czas jest reprezentowany jako liczba sekund od 1 stycznia 1970 (1970-01-01T0:0:0Z) UTC czasu token został wystawiony.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-124">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.</span></span> |
| `sub` | <span data-ttu-id="d7ba7-125">Podmiot: jak w przypadku `iss`, powinny być client_id (identyfikator aplikacji usługi klienta)</span><span class="sxs-lookup"><span data-stu-id="d7ba7-125">Subject: As for `iss`, should be the client_id (Application Id of the client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="d7ba7-126">Podpis</span><span class="sxs-lookup"><span data-stu-id="d7ba7-126">Signature</span></span>
<span data-ttu-id="d7ba7-127">Podpis jest obliczana stosowania certyfikatu zgodnie z opisem w [specyfikacji RFC7519 tokenu Web JSON](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="d7ba7-127">The signature is computed applying the certificate as described in the [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="d7ba7-128">Przykład dekodowane potwierdzenia JWT</span><span class="sxs-lookup"><span data-stu-id="d7ba7-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="d7ba7-129">Przykład zakodowanego potwierdzenia JWT</span><span class="sxs-lookup"><span data-stu-id="d7ba7-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="d7ba7-130">Następujący ciąg jest przykładem zakodowanego potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-130">The following string is an example of encoded assertion.</span></span> <span data-ttu-id="d7ba7-131">Zwróć uwagę, można zauważyć trzy części oddzielone kropkami (.).</span><span class="sxs-lookup"><span data-stu-id="d7ba7-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="d7ba7-132">Pierwsza sekcja koduje nagłówka, drugi ładunku oraz za ostatni jest z podpisem obliczonym z certyfikatami od zawartości najpierw dwie sekcje.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-132">The first section encodes the header, the second the payload, and the last is the signature computed with the certificates from the content of the first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="d7ba7-133">Zarejestruj certyfikat z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7ba7-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="d7ba7-134">Aby skojarzyć poświadczenia certyfikatu z aplikacji klienckiej w usłudze Azure AD, należy edytować manifest aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-134">To associate the certificate credential with the client application in Azure AD, you need to edit the application manifest.</span></span>
<span data-ttu-id="d7ba7-135">O wstrzymywania certyfikatu, należy obliczyć:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-135">Having hold of a certificate, you need to compute:</span></span>
- <span data-ttu-id="d7ba7-136">`$base64Thumbprint`, która jest base64 kodowanie skrót certyfikatu</span><span class="sxs-lookup"><span data-stu-id="d7ba7-136">`$base64Thumbprint`, which is the base64 encoding of the certificate Hash</span></span>
- <span data-ttu-id="d7ba7-137">`$base64Value`, która jest base64 kodowanie dane pierwotne certyfikatu</span><span class="sxs-lookup"><span data-stu-id="d7ba7-137">`$base64Value`, which is the base64 encoding of the certificate raw data</span></span>

<span data-ttu-id="d7ba7-138">należy również podać identyfikator GUID, aby zidentyfikować klucza w manifeście aplikacji (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="d7ba7-138">you also need to provide a GUID to identify the key in the application manifest (`$keyId`)</span></span>

<span data-ttu-id="d7ba7-139">W aplikacji Azure rejestracji aplikacji klienckiej, otwórz plik manifestu aplikacji i Zastąp *keyCredentials* właściwości z informacjami certyfikatu przy użyciu następującego schematu:</span><span class="sxs-lookup"><span data-stu-id="d7ba7-139">In the Azure app registration for the client application, open the application manifest, and replace the *keyCredentials* property with your new certificate information using the following schema:</span></span>
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

<span data-ttu-id="d7ba7-140">Zapisać zmiany w manifeście aplikacji, a następnie przekazać do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-140">Save the edits to the application manifest, and upload to Azure AD.</span></span> <span data-ttu-id="d7ba7-141">Właściwość keyCredentials jest wielowartościowe, więc może przekazać wiele certyfikatów bardziej zaawansowane funkcje zarządzania kluczami.</span><span class="sxs-lookup"><span data-stu-id="d7ba7-141">The keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
