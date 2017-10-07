---
title: "aaaSecure interfejsów API przy użyciu wstępnego uwierzytelniania certyfikatu klienta w usłudze API Management — zarządzanie interfejsami API Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosecure dostępu tooAPIs przy użyciu certyfikatów klienta"
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
ms.openlocfilehash: 6ff78bda3d429829da79d0dc4d652f19669cc919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="51e41-103">W jaki sposób toosecure interfejsów API przy użyciu klienta certyfikatów uwierzytelniania w zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="51e41-103">How toosecure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="51e41-104">Zarządzanie interfejsami API udostępnia hello możliwości toosecure dostępu tooAPIs (tj., klient tooAPI Management) przy użyciu certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="51e41-104">API Management provides hello capability toosecure access tooAPIs (i.e., client tooAPI Management) using client certificates.</span></span> <span data-ttu-id="51e41-105">Obecnie można sprawdzić hello odcisk palca certyfikatu klienta na żądaną wartość.</span><span class="sxs-lookup"><span data-stu-id="51e41-105">Currently, you can check hello thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="51e41-106">Możesz również sprawdzić się, że odcisk palca hello z istniejących certyfikatów przekazano tooAPI zarządzania.</span><span class="sxs-lookup"><span data-stu-id="51e41-106">You can also check hello thumbprint against existing certificates uploaded tooAPI Management.</span></span>  

<span data-ttu-id="51e41-107">Aby uzyskać informacje dotyczące zabezpieczania usługi zaplecza toohello dostępu do interfejsu API przy użyciu certyfikatów klienta (np. zarządzanie interfejsami API tooback-end), zobacz [jak za pomocą klienta usług zaplecza toosecure certyfikatu uwierzytelniania](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="51e41-107">For information about securing access toohello back-end service of an API using client certificates (i.e., API Management tooback-end), see [How toosecure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-hello-expiration-date"></a><span data-ttu-id="51e41-108">Sprawdzanie, czy data wygaśnięcia hello</span><span class="sxs-lookup"><span data-stu-id="51e41-108">Checking hello expiration date</span></span>

<span data-ttu-id="51e41-109">Poniżej zasad może być skonfigurowany toocheck Jeśli hello certyfikat wygasł:</span><span class="sxs-lookup"><span data-stu-id="51e41-109">Below policies can be configured toocheck if hello certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a><span data-ttu-id="51e41-110">Sprawdzanie, czy wystawca hello i podmiotu</span><span class="sxs-lookup"><span data-stu-id="51e41-110">Checking hello issuer and subject</span></span>

<span data-ttu-id="51e41-111">Poniżej zasad może być skonfigurowany toocheck hello wystawcy i podmiotu certyfikatu klienta:</span><span class="sxs-lookup"><span data-stu-id="51e41-111">Below policies can be configured toocheck hello issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a><span data-ttu-id="51e41-112">Sprawdzanie, czy hello odcisk palca</span><span class="sxs-lookup"><span data-stu-id="51e41-112">Checking hello thumbprint</span></span>

<span data-ttu-id="51e41-113">Poniżej zasad może być skonfigurowany toocheck hello odcisk palca certyfikatu klienta:</span><span class="sxs-lookup"><span data-stu-id="51e41-113">Below policies can be configured toocheck hello thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a><span data-ttu-id="51e41-114">Sprawdzanie odcisk palca przed certyfikatami, przekazać tooAPI zarządzania</span><span class="sxs-lookup"><span data-stu-id="51e41-114">Checking a thumbprint against certificates uploaded tooAPI Management</span></span>

<span data-ttu-id="51e41-115">Witaj poniższy przykład przedstawia sposób toocheck hello odcisk palca certyfikatu klienta przed certyfikatami, przekazać tooAPI zarządzania:</span><span class="sxs-lookup"><span data-stu-id="51e41-115">hello following example shows how toocheck hello thumbprint of a client certificate against certificates uploaded tooAPI Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="51e41-116">Następny krok</span><span class="sxs-lookup"><span data-stu-id="51e41-116">Next step</span></span>

*  [<span data-ttu-id="51e41-117">Jak za pomocą klienta usług zaplecza toosecure certyfikatu uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="51e41-117">How toosecure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="51e41-118">Jak tooupload certyfikatów</span><span class="sxs-lookup"><span data-stu-id="51e41-118">How tooupload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

