---
title: "aaaScheduler uwierzytelniania połączeń wychodzących"
description: "Uwierzytelnianie połączeń wychodzących harmonogramu"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="1a242-103">Uwierzytelnianie połączeń wychodzących harmonogramu</span><span class="sxs-lookup"><span data-stu-id="1a242-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="1a242-104">Harmonogram zadań może być konieczne toocall limit tooservices, która wymaga uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1a242-104">Scheduler jobs may need toocall out tooservices that require authentication.</span></span> <span data-ttu-id="1a242-105">W ten sposób usługa o nazwie może określić, jeśli zadanie harmonogramu hello dostęp do jej zasobów.</span><span class="sxs-lookup"><span data-stu-id="1a242-105">This way, a called service can determine if hello Scheduler job can access its resources.</span></span> <span data-ttu-id="1a242-106">Niektóre z tych usług obejmują innych usług platformy Azure, witryny Salesforce.com, Facebook i bezpieczne niestandardowych witryn sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1a242-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="1a242-107">Dodawanie i usuwanie uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1a242-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="1a242-108">Dodawanie uwierzytelniania tooa harmonogramu zadania jest proste — dodawanie elementu podrzędnego JSON `authentication` toohello `request` elementu podczas tworzenia lub aktualizowania zadania.</span><span class="sxs-lookup"><span data-stu-id="1a242-108">Adding authentication tooa Scheduler job is simple – add a JSON child element `authentication` toohello `request` element when creating or updating a job.</span></span> <span data-ttu-id="1a242-109">Klucze tajne przekazano usługa Harmonogram toohello żądania PUT, PATCH lub POST — jako część hello `authentication` obiektu — nigdy nie są zwracane w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1a242-109">Secrets passed toohello Scheduler service in a PUT, PATCH, or POST request – as part of hello `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="1a242-110">W odpowiedzi na tajnych informacji ustawiono toonull lub może mieć publicznych token, który reprezentuje jednostkę hello uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="1a242-110">In responses, secret information is set toonull or may have a public token that represents hello authenticated entity.</span></span>

<span data-ttu-id="1a242-111">Uwierzytelnianie tooremove PUT lub poprawka zadania hello jawnie, ustawienie hello `authentication` obiekt toonull.</span><span class="sxs-lookup"><span data-stu-id="1a242-111">tooremove authentication, PUT or PATCH hello job explicitly, setting hello `authentication` object toonull.</span></span> <span data-ttu-id="1a242-112">Nie będą widzieć żadnych właściwości uwierzytelniania w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1a242-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="1a242-113">Obecnie hello obsługiwane tylko typy uwierzytelniania są hello `ClientCertificate` model (przy użyciu certyfikatów klienta SSL/TLS hello), hello `Basic` modelu (dla uwierzytelniania podstawowego) i hello `ActiveDirectoryOAuth` (dla OAuth usługi Active Directory uwierzytelnianie).</span><span class="sxs-lookup"><span data-stu-id="1a242-113">Currently, hello only supported authentication types are hello `ClientCertificate` model (for using hello SSL/TLS client certificates), hello `Basic` model (for Basic authentication), and hello `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="1a242-114">Treść żądania uwierzytelniania ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="1a242-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="1a242-115">Podczas dodawania uwierzytelnianie przy użyciu hello `ClientCertificate` modelu, określ następujące dodatkowe elementy w treści żądania hello hello.</span><span class="sxs-lookup"><span data-stu-id="1a242-115">When adding authentication using hello `ClientCertificate` model, specify hello following additional elements in hello request body.</span></span>  

| <span data-ttu-id="1a242-116">Element</span><span class="sxs-lookup"><span data-stu-id="1a242-116">Element</span></span> | <span data-ttu-id="1a242-117">Opis</span><span class="sxs-lookup"><span data-stu-id="1a242-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1a242-118">*uwierzytelnianie (element nadrzędny)*</span><span class="sxs-lookup"><span data-stu-id="1a242-118">*authentication (parent element)*</span></span> |<span data-ttu-id="1a242-119">Obiekt uwierzytelniania za pomocą certyfikatu klienta SSL.</span><span class="sxs-lookup"><span data-stu-id="1a242-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="1a242-120">*Typ*</span><span class="sxs-lookup"><span data-stu-id="1a242-120">*type*</span></span> |<span data-ttu-id="1a242-121">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1a242-121">Required.</span></span> <span data-ttu-id="1a242-122">Typ uwierzytelniania. W przypadku certyfikatów SSL klienta hello wartość musi być `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="1a242-122">Type of authentication.For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="1a242-123">*PFX*</span><span class="sxs-lookup"><span data-stu-id="1a242-123">*pfx*</span></span> |<span data-ttu-id="1a242-124">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1a242-124">Required.</span></span> <span data-ttu-id="1a242-125">Algorytmem Base64 zawartość pliku PFX hello.</span><span class="sxs-lookup"><span data-stu-id="1a242-125">Base64-encoded contents of hello PFX file.</span></span> |
| <span data-ttu-id="1a242-126">*hasło*</span><span class="sxs-lookup"><span data-stu-id="1a242-126">*password*</span></span> |<span data-ttu-id="1a242-127">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1a242-127">Required.</span></span> <span data-ttu-id="1a242-128">Plik PFX hello tooaccess hasła.</span><span class="sxs-lookup"><span data-stu-id="1a242-128">Password tooaccess hello PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="1a242-129">Treść odpowiedzi ClientCertificate uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1a242-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="1a242-130">Po wysłaniu żądania z użyciem informacji uwierzytelniania hello odpowiedzi zawiera następujące elementy związane z uwierzytelnianiem hello.</span><span class="sxs-lookup"><span data-stu-id="1a242-130">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="1a242-131">Element</span><span class="sxs-lookup"><span data-stu-id="1a242-131">Element</span></span> | <span data-ttu-id="1a242-132">Opis</span><span class="sxs-lookup"><span data-stu-id="1a242-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1a242-133">*uwierzytelnianie (element nadrzędny)*</span><span class="sxs-lookup"><span data-stu-id="1a242-133">*authentication (parent element)*</span></span> |<span data-ttu-id="1a242-134">Obiekt uwierzytelniania za pomocą certyfikatu klienta SSL.</span><span class="sxs-lookup"><span data-stu-id="1a242-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="1a242-135">*Typ*</span><span class="sxs-lookup"><span data-stu-id="1a242-135">*type*</span></span> |<span data-ttu-id="1a242-136">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1a242-136">Type of authentication.</span></span> <span data-ttu-id="1a242-137">Dla certyfikatów klienta SSL, wartość hello jest `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="1a242-137">For SSL client certificates, hello value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="1a242-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="1a242-138">*certificateThumbprint*</span></span> |<span data-ttu-id="1a242-139">Witaj odcisk palca certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="1a242-139">hello thumbprint of hello certificate.</span></span> |
| <span data-ttu-id="1a242-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="1a242-140">*certificateSubjectName*</span></span> |<span data-ttu-id="1a242-141">Witaj podmiotu nazwa wyróżniająca hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1a242-141">hello subject distinguished name of hello certificate.</span></span> |
| <span data-ttu-id="1a242-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="1a242-142">*certificateExpiration*</span></span> |<span data-ttu-id="1a242-143">Data wygaśnięcia Hello hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1a242-143">hello expiration date of hello certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="1a242-144">Przykładowe żądanie REST ClientCertificate uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1a242-144">Sample REST Request for ClientCertificate Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="1a242-145">Przykładowa odpowiedź REST ClientCertificate uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1a242-145">Sample REST Response for ClientCertificate Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="1a242-146">Treść żądania dla uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="1a242-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="1a242-147">Podczas dodawania uwierzytelnianie przy użyciu hello `Basic` modelu, określ następujące dodatkowe elementy w treści żądania hello hello.</span><span class="sxs-lookup"><span data-stu-id="1a242-147">When adding authentication using hello `Basic` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="1a242-148">Element</span><span class="sxs-lookup"><span data-stu-id="1a242-148">Element</span></span> | <span data-ttu-id="1a242-149">Opis</span><span class="sxs-lookup"><span data-stu-id="1a242-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1a242-150">*uwierzytelnianie (element nadrzędny)*</span><span class="sxs-lookup"><span data-stu-id="1a242-150">*authentication (parent element)*</span></span> |<span data-ttu-id="1a242-151">Obiekt uwierzytelniania dla uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="1a242-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="1a242-152">*Typ*</span><span class="sxs-lookup"><span data-stu-id="1a242-152">*type*</span></span> |<span data-ttu-id="1a242-153">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1a242-153">Required.</span></span> <span data-ttu-id="1a242-154">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1a242-154">Type of authentication.</span></span> <span data-ttu-id="1a242-155">W przypadku uwierzytelniania podstawowego hello wartość musi być `Basic`.</span><span class="sxs-lookup"><span data-stu-id="1a242-155">For Basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="1a242-156">*Nazwa użytkownika*</span><span class="sxs-lookup"><span data-stu-id="1a242-156">*username*</span></span> |<span data-ttu-id="1a242-157">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1a242-157">Required.</span></span> <span data-ttu-id="1a242-158">Tooauthenticate nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1a242-158">Username tooauthenticate.</span></span> |
| <span data-ttu-id="1a242-159">*hasło*</span><span class="sxs-lookup"><span data-stu-id="1a242-159">*password*</span></span> |<span data-ttu-id="1a242-160">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1a242-160">Required.</span></span> <span data-ttu-id="1a242-161">Tooauthenticate hasła.</span><span class="sxs-lookup"><span data-stu-id="1a242-161">Password tooauthenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="1a242-162">Treść odpowiedzi dla uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="1a242-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="1a242-163">Po wysłaniu żądania z użyciem informacji uwierzytelniania hello odpowiedzi zawiera następujące elementy związane z uwierzytelnianiem hello.</span><span class="sxs-lookup"><span data-stu-id="1a242-163">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="1a242-164">Element</span><span class="sxs-lookup"><span data-stu-id="1a242-164">Element</span></span> | <span data-ttu-id="1a242-165">Opis</span><span class="sxs-lookup"><span data-stu-id="1a242-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1a242-166">*uwierzytelnianie (element nadrzędny)*</span><span class="sxs-lookup"><span data-stu-id="1a242-166">*authentication (parent element)*</span></span> |<span data-ttu-id="1a242-167">Obiekt uwierzytelniania dla uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="1a242-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="1a242-168">*Typ*</span><span class="sxs-lookup"><span data-stu-id="1a242-168">*type*</span></span> |<span data-ttu-id="1a242-169">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1a242-169">Type of authentication.</span></span> <span data-ttu-id="1a242-170">W przypadku uwierzytelniania podstawowego jest wartość hello `Basic`.</span><span class="sxs-lookup"><span data-stu-id="1a242-170">For Basic authentication, hello value is `Basic`.</span></span> |
| <span data-ttu-id="1a242-171">*Nazwa użytkownika*</span><span class="sxs-lookup"><span data-stu-id="1a242-171">*username*</span></span> |<span data-ttu-id="1a242-172">Witaj uwierzytelnić nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1a242-172">hello authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="1a242-173">Przykładowe żądanie REST dla uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="1a242-173">Sample REST Request for Basic Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="1a242-174">Przykładowa odpowiedź REST dla uwierzytelniania podstawowego</span><span class="sxs-lookup"><span data-stu-id="1a242-174">Sample REST Response for Basic Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1a242-175">Treść żądania uwierzytelniania ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="1a242-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="1a242-176">Podczas dodawania uwierzytelnianie przy użyciu hello `ActiveDirectoryOAuth` modelu, określ następujące dodatkowe elementy w treści żądania hello hello.</span><span class="sxs-lookup"><span data-stu-id="1a242-176">When adding authentication using hello `ActiveDirectoryOAuth` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="1a242-177">Element</span><span class="sxs-lookup"><span data-stu-id="1a242-177">Element</span></span> | <span data-ttu-id="1a242-178">Opis</span><span class="sxs-lookup"><span data-stu-id="1a242-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1a242-179">*uwierzytelnianie (element nadrzędny)*</span><span class="sxs-lookup"><span data-stu-id="1a242-179">*authentication (parent element)*</span></span> |<span data-ttu-id="1a242-180">Obiekt uwierzytelniania dla uwierzytelniania ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="1a242-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="1a242-181">*Typ*</span><span class="sxs-lookup"><span data-stu-id="1a242-181">*type*</span></span> |<span data-ttu-id="1a242-182">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1a242-182">Required.</span></span> <span data-ttu-id="1a242-183">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1a242-183">Type of authentication.</span></span> <span data-ttu-id="1a242-184">W przypadku uwierzytelniania ActiveDirectoryOAuth hello wartość musi być `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="1a242-184">For ActiveDirectoryOAuth authentication, hello value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="1a242-185">*dzierżawy*</span><span class="sxs-lookup"><span data-stu-id="1a242-185">*tenant*</span></span> |<span data-ttu-id="1a242-186">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1a242-186">Required.</span></span> <span data-ttu-id="1a242-187">Identyfikator dzierżawy Hello dzierżawy hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a242-187">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="1a242-188">*grupy odbiorców*</span><span class="sxs-lookup"><span data-stu-id="1a242-188">*audience*</span></span> |<span data-ttu-id="1a242-189">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1a242-189">Required.</span></span> <span data-ttu-id="1a242-190">Ta opcja jest ustawiona toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="1a242-190">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="1a242-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="1a242-191">*clientId*</span></span> |<span data-ttu-id="1a242-192">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1a242-192">Required.</span></span> <span data-ttu-id="1a242-193">Podaj identyfikator klienta hello hello aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a242-193">Provide hello client identifier for hello Azure AD application.</span></span> |
| <span data-ttu-id="1a242-194">*klucz tajny*</span><span class="sxs-lookup"><span data-stu-id="1a242-194">*secret*</span></span> |<span data-ttu-id="1a242-195">Wymagany.</span><span class="sxs-lookup"><span data-stu-id="1a242-195">Required.</span></span> <span data-ttu-id="1a242-196">Klucz tajny klienta hello, który żąda hello token.</span><span class="sxs-lookup"><span data-stu-id="1a242-196">Secret of hello client that is requesting hello token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="1a242-197">Określanie identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="1a242-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="1a242-198">Uzyskać identyfikator dzierżawy hello dzierżawy hello Azure AD, uruchamiając `Get-AzureAccount` w programie Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a242-198">You can find hello tenant identifier for hello Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1a242-199">Treść odpowiedzi uwierzytelniania ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="1a242-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="1a242-200">Po wysłaniu żądania z użyciem informacji uwierzytelniania hello odpowiedzi zawiera następujące elementy związane z uwierzytelnianiem hello.</span><span class="sxs-lookup"><span data-stu-id="1a242-200">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="1a242-201">Element</span><span class="sxs-lookup"><span data-stu-id="1a242-201">Element</span></span> | <span data-ttu-id="1a242-202">Opis</span><span class="sxs-lookup"><span data-stu-id="1a242-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1a242-203">*uwierzytelnianie (element nadrzędny)*</span><span class="sxs-lookup"><span data-stu-id="1a242-203">*authentication (parent element)*</span></span> |<span data-ttu-id="1a242-204">Obiekt uwierzytelniania dla uwierzytelniania ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="1a242-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="1a242-205">*Typ*</span><span class="sxs-lookup"><span data-stu-id="1a242-205">*type*</span></span> |<span data-ttu-id="1a242-206">Typ uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1a242-206">Type of authentication.</span></span> <span data-ttu-id="1a242-207">W przypadku uwierzytelniania ActiveDirectoryOAuth wartość hello jest `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="1a242-207">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="1a242-208">*dzierżawy*</span><span class="sxs-lookup"><span data-stu-id="1a242-208">*tenant*</span></span> |<span data-ttu-id="1a242-209">Identyfikator dzierżawy Hello dzierżawy hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a242-209">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="1a242-210">*grupy odbiorców*</span><span class="sxs-lookup"><span data-stu-id="1a242-210">*audience*</span></span> |<span data-ttu-id="1a242-211">Ta opcja jest ustawiona toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="1a242-211">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="1a242-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="1a242-212">*clientId*</span></span> |<span data-ttu-id="1a242-213">Witaj identyfikator klienta aplikacji hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a242-213">hello client identifier for hello Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1a242-214">Przykładowe żądanie REST ActiveDirectoryOAuth uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1a242-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="1a242-215">Przykładowa odpowiedź REST ActiveDirectoryOAuth uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1a242-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a><span data-ttu-id="1a242-216">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1a242-216">See Also</span></span>
 [<span data-ttu-id="1a242-217">Co to jest Scheduler?</span><span class="sxs-lookup"><span data-stu-id="1a242-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="1a242-218">Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek</span><span class="sxs-lookup"><span data-stu-id="1a242-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="1a242-219">Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1a242-219">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="1a242-220">Plany i rozliczenia w usłudze Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="1a242-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="1a242-221">Dokumentacja interfejsu API REST usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="1a242-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="1a242-222">Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="1a242-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="1a242-223">Wysoka dostępność i niezawodność usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="1a242-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="1a242-224">Limity, wartości domyślne i kody błędów usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="1a242-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

