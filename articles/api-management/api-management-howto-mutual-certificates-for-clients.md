---
title: "Zabezpieczenie interfejsów API przy użyciu klienta uwierzytelniania certyfikatów w usłudze API Management — zarządzanie interfejsami API Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak bezpieczny dostęp do interfejsów API przy użyciu certyfikatów klienta"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: d3d51d0575a6d2dacced931601d48eb1e51a4051
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="65e8a-103">Jak zabezpieczyć interfejsy API za pomocą klienta uwierzytelniania certyfikatów w usłudze API Management</span><span class="sxs-lookup"><span data-stu-id="65e8a-103">How to secure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="65e8a-104">Zarządzanie interfejsami API oferuje możliwość bezpiecznego dostępu do interfejsów API (np. od klienta do usługi API Management) przy użyciu certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="65e8a-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span></span> <span data-ttu-id="65e8a-105">Obecnie można sprawdzić odcisk palca certyfikatu klienta na żądaną wartość.</span><span class="sxs-lookup"><span data-stu-id="65e8a-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="65e8a-106">Można również sprawdzić odcisk palca z istniejących certyfikatów przekazanych do interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="65e8a-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span></span>  

<span data-ttu-id="65e8a-107">Aby uzyskać informacji na temat zabezpieczania dostępu do usługi zaplecza interfejsu API przy użyciu certyfikatów klienta (np. interfejsu API Management do wewnętrznej), zobacz [zabezpieczania usług zaplecza za pomocą klienta uwierzytelnianie certyfikatu](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="65e8a-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-the-expiration-date"></a><span data-ttu-id="65e8a-108">Sprawdzanie daty wygaśnięcia</span><span class="sxs-lookup"><span data-stu-id="65e8a-108">Checking the expiration date</span></span>

<span data-ttu-id="65e8a-109">Aby sprawdzić, czy certyfikat wygasł można skonfigurować poniżej zasad:</span><span class="sxs-lookup"><span data-stu-id="65e8a-109">Below policies can be configured to check if the certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-issuer-and-subject"></a><span data-ttu-id="65e8a-110">Sprawdzanie wystawcy i podmiotu</span><span class="sxs-lookup"><span data-stu-id="65e8a-110">Checking the issuer and subject</span></span>

<span data-ttu-id="65e8a-111">Poniżej zasad można skonfigurować w celu sprawdzenia wystawcy i podmiotu certyfikatu klienta:</span><span class="sxs-lookup"><span data-stu-id="65e8a-111">Below policies can be configured to check the issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-thumbprint"></a><span data-ttu-id="65e8a-112">Sprawdzanie odcisk palca</span><span class="sxs-lookup"><span data-stu-id="65e8a-112">Checking the thumbprint</span></span>

<span data-ttu-id="65e8a-113">Poniżej zasad można skonfigurować w celu Sprawdź odcisk palca certyfikatu klienta:</span><span class="sxs-lookup"><span data-stu-id="65e8a-113">Below policies can be configured to check the thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-to-api-management"></a><span data-ttu-id="65e8a-114">Sprawdzanie odcisk palca przed certyfikatami, przekazany do interfejsu API zarządzania</span><span class="sxs-lookup"><span data-stu-id="65e8a-114">Checking a thumbprint against certificates uploaded to API Management</span></span>

<span data-ttu-id="65e8a-115">Poniższy przykład przedstawia sposób Sprawdź odcisk palca certyfikatu klienta przed przekazany do interfejsu API zarządzania certyfikatami:</span><span class="sxs-lookup"><span data-stu-id="65e8a-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="65e8a-116">Następny krok</span><span class="sxs-lookup"><span data-stu-id="65e8a-116">Next step</span></span>

*  [<span data-ttu-id="65e8a-117">Jak zabezpieczyć za pomocą klienta usług zaplecza uwierzytelnianie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="65e8a-117">How to secure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="65e8a-118">Jak przekazywać certyfikatów</span><span class="sxs-lookup"><span data-stu-id="65e8a-118">How to upload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

