---
title: "Jak sprawdzić postęp zadania przy użyciu interfejsu API REST | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak śledzić postęp zadania."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a1a1f956-c035-448a-af9c-5ac15fcce9dd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: fea4383e81f3ca21955252cf1d573f1b347b5a38
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-check-job-progress"></a><span data-ttu-id="d9bd7-103">Porady: sprawdzanie postępu zadania</span><span class="sxs-lookup"><span data-stu-id="d9bd7-103">How to: check job progress</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9bd7-104">Portal</span><span class="sxs-lookup"><span data-stu-id="d9bd7-104">Portal</span></span>](media-services-portal-check-job-progress.md)
> * [<span data-ttu-id="d9bd7-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d9bd7-105">.NET</span></span>](media-services-check-job-progress.md)
> * [<span data-ttu-id="d9bd7-106">REST</span><span class="sxs-lookup"><span data-stu-id="d9bd7-106">REST</span></span>](media-services-rest-check-job-progress.md)
> 
> 

<span data-ttu-id="d9bd7-107">Po uruchomieniu zadania często wymagają sposób, aby śledzić postęp zadania.</span><span class="sxs-lookup"><span data-stu-id="d9bd7-107">When you run jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="d9bd7-108">Stan zadania można znaleźć przy użyciu właściwości stanu zadania.</span><span class="sxs-lookup"><span data-stu-id="d9bd7-108">You can find out the Job status by using the Job's State property.</span></span> <span data-ttu-id="d9bd7-109">Aby uzyskać więcej informacji na temat właściwości stanu zobacz [właściwości jednostki zadania](https://docs.microsoft.com/rest/api/media/operations/job#job_entity_properties).</span><span class="sxs-lookup"><span data-stu-id="d9bd7-109">For more information on the State property, see [Job Entity Properties](https://docs.microsoft.com/rest/api/media/operations/job#job_entity_properties).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="d9bd7-110">Łączenie się z usługą Media Services</span><span class="sxs-lookup"><span data-stu-id="d9bd7-110">Connect to Media Services</span></span>

<span data-ttu-id="d9bd7-111">Aby uzyskać informacje na temat nawiązywania połączenia z interfejsu API usług AMS, zobacz [dostępu Azure Media Services API przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d9bd7-111">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d9bd7-112">Po pomyślnym połączeniu się https://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="d9bd7-112">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d9bd7-113">Upewnij się kolejne wywołania nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="d9bd7-113">You must make subsequent calls to the new URI.</span></span>

## <a name="check-job-progress"></a><span data-ttu-id="d9bd7-114">Sprawdzanie postępu zadania</span><span class="sxs-lookup"><span data-stu-id="d9bd7-114">Check job progress</span></span>

<span data-ttu-id="d9bd7-115">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="d9bd7-115">Request:</span></span>

    GET https://media.windows.net/api/Jobs()?$filter=Id%20eq%20'nb%3Ajid%3AUUID%3Af3c43f94-327f-2347-90bb-3bf79f8559f1'&$top=1 HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423640758&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=z5yFIG%2bk8Z2G2aXABqM60P9smHNKD7P4BfSxXanwKFc%3d
    x-ms-version: 2.11
    Host: media.windows.net



<span data-ttu-id="d9bd7-116">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="d9bd7-116">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 450
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d9b83c57-e26c-4d10-a20b-2be634c4b6a8
    request-id: 91d2be35-20ed-4e1c-a147-e82cd000c193
    x-ms-request-id: 91d2be35-20ed-4e1c-a147-e82cd000c193
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains

    {"odata.metadata":"https://media.windows.net/api/$metadata#Jobs","value":[{"Id":"nb:jid:UUID:f3c43f94-327f-2347-90bb-3bf79f8559f1","Name":"Encoding BigBuckBunny into to H264 Adaptive Bitrate MP4 Set 720p","Created":"2015-02-11T01:46:08.897","LastModified":"2015-02-11T01:46:08.897","EndTime":null,"Priority":0,"RunningDuration":0.0,"StartTime":"2015-02-11T01:46:16.58","State":2,"TemplateId":null,"JobNotificationSubscriptions":[]}]} 


## <a name="media-services-learning-paths"></a><span data-ttu-id="d9bd7-117">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="d9bd7-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d9bd7-118">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="d9bd7-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d9bd7-119">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d9bd7-119">See also</span></span>

[<span data-ttu-id="d9bd7-120">Przegląd interfejsu API REST operacji usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="d9bd7-120">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)
