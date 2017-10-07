---
title: "Filtry aaaCreating przy użyciu interfejsu API REST Azure Media Services | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano, jak toocreate filtry, aby klient mógł ich użyć toostream określonych sekcji strumienia. Usługi Media Services tworzy dynamiczne manifestów tooachieve selektywnego strumienia."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: d0b5af3b193b35f22ac70887963c2f0a06b60bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="2b63c-104">Tworzenia filtrów z usługi Azure Media Services interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="2b63c-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b63c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2b63c-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="2b63c-106">REST</span><span class="sxs-lookup"><span data-stu-id="2b63c-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="2b63c-107">Począwszy od wersji 2.11, Media Services umożliwia filtry toodefine trwałych.</span><span class="sxs-lookup"><span data-stu-id="2b63c-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="2b63c-108">Te filtry są reguły po stronie serwera, zezwalające klientom toochoose toodo np.: odtwarzanie tylko części klipu wideo (a nie odtwarzane hello całego wideo), lub określ tylko podzestaw audio i wideo wersji obsługi (przez klienta urządzenia zamiast wersji hello wszystkich skojarzonych z hello zasobów).</span><span class="sxs-lookup"><span data-stu-id="2b63c-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="2b63c-109">Filtrowania elementów zawartości zostaną zarchiwizowane za pośrednictwem **dynamiczne manifestu**, które są tworzone w chwili toostream żądania klienta wideo oparte na określonej filtry.</span><span class="sxs-lookup"><span data-stu-id="2b63c-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="2b63c-110">Bardziej szczegółowe informacje pokrewne toofilters i dynamiczne manifestu, zobacz [dynamicznie manifesty omówienie](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2b63c-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="2b63c-111">W tym temacie przedstawiono sposób toouse toocreate interfejsów API REST, aktualizować i usuwać filtrów.</span><span class="sxs-lookup"><span data-stu-id="2b63c-111">This topic shows how toouse REST APIs toocreate, update, and delete filters.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="2b63c-112">Typy używane filtry toocreate</span><span class="sxs-lookup"><span data-stu-id="2b63c-112">Types used toocreate filters</span></span>
<span data-ttu-id="2b63c-113">Witaj następujące typy są używane podczas tworzenia filtrów:</span><span class="sxs-lookup"><span data-stu-id="2b63c-113">hello following types are used when creating filters:</span></span>  

* [<span data-ttu-id="2b63c-114">Filtr</span><span class="sxs-lookup"><span data-stu-id="2b63c-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="2b63c-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="2b63c-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="2b63c-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="2b63c-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="2b63c-117">FilterTrackSelect i FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="2b63c-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="2b63c-118">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b63c-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="2b63c-119">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="2b63c-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="2b63c-120">Połączenie usług tooMedia</span><span class="sxs-lookup"><span data-stu-id="2b63c-120">Connect tooMedia Services</span></span>

<span data-ttu-id="2b63c-121">Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="2b63c-121">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="2b63c-122">Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="2b63c-122">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="2b63c-123">Należy wykonać kolejne wywołania toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="2b63c-123">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="2b63c-124">Tworzenie filtrów</span><span class="sxs-lookup"><span data-stu-id="2b63c-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="2b63c-125">Utwórz filtry globalne</span><span class="sxs-lookup"><span data-stu-id="2b63c-125">Create global Filters</span></span>
<span data-ttu-id="2b63c-126">toocreate filtr globalny Użyj hello następujące żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="2b63c-126">toocreate a global Filter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="2b63c-127">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="2b63c-127">HTTP Request</span></span>
<span data-ttu-id="2b63c-128">Nagłówki żądania</span><span class="sxs-lookup"><span data-stu-id="2b63c-128">Request Headers</span></span>

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

<span data-ttu-id="2b63c-129">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2b63c-129">Request body</span></span> 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a><span data-ttu-id="2b63c-130">Odpowiedź HTTP</span><span class="sxs-lookup"><span data-stu-id="2b63c-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="2b63c-131">Utwórz AssetFilters lokalnego</span><span class="sxs-lookup"><span data-stu-id="2b63c-131">Create local AssetFilters</span></span>
<span data-ttu-id="2b63c-132">toocreate AssetFilter lokalnego, należy użyć hello następujące żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="2b63c-132">toocreate a local AssetFilter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="2b63c-133">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="2b63c-133">HTTP Request</span></span>
<span data-ttu-id="2b63c-134">Nagłówki żądania</span><span class="sxs-lookup"><span data-stu-id="2b63c-134">Request Headers</span></span>

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

<span data-ttu-id="2b63c-135">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="2b63c-135">Request body</span></span> 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a><span data-ttu-id="2b63c-136">Odpowiedź HTTP</span><span class="sxs-lookup"><span data-stu-id="2b63c-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="2b63c-137">Lista filtrów</span><span class="sxs-lookup"><span data-stu-id="2b63c-137">List filters</span></span>
### <a name="get-all-global-filters-in-hello-ams-account"></a><span data-ttu-id="2b63c-138">Pobierz wszystkie globalne **filtru**s na koncie hello AMS</span><span class="sxs-lookup"><span data-stu-id="2b63c-138">Get all global **Filter**s in hello AMS account</span></span>
<span data-ttu-id="2b63c-139">filtry toolist Użyj hello następujące żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="2b63c-139">toolist filters, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="2b63c-140">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="2b63c-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="2b63c-141">Pobierz **AssetFilter**s skojarzony z zasobem</span><span class="sxs-lookup"><span data-stu-id="2b63c-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="2b63c-142">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="2b63c-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="2b63c-143">Pobierz **AssetFilter** na podstawie jego identyfikatora</span><span class="sxs-lookup"><span data-stu-id="2b63c-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="2b63c-144">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="2b63c-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="2b63c-145">Filtry aktualizacji</span><span class="sxs-lookup"><span data-stu-id="2b63c-145">Update filters</span></span>
<span data-ttu-id="2b63c-146">Użyj poprawka tooupdate PUT lub scalania filtr o nowej wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="2b63c-146">Use PATCH, PUT or MERGE tooupdate a filter with new property values.</span></span>  <span data-ttu-id="2b63c-147">Aby uzyskać więcej informacji o tych operacjach, zobacz [poprawki, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b63c-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="2b63c-148">Po zaktualizowaniu filtru może potrwać too2 minut do przesyłania strumieniowego punktu końcowego toorefresh hello reguły.</span><span class="sxs-lookup"><span data-stu-id="2b63c-148">If you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="2b63c-149">Jeśli zawartość hello zostało obsłużone przy użyciu tego filtru (i w pamięci podręcznej serwerów proxy i sieci CDN pamięci podręcznych), aktualizacja tego filtru może powodować błędy player.</span><span class="sxs-lookup"><span data-stu-id="2b63c-149">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="2b63c-150">Jest zalecane tooclear hello w pamięci podręcznej po zaktualizowaniu hello filtru.</span><span class="sxs-lookup"><span data-stu-id="2b63c-150">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="2b63c-151">Jeśli ta opcja nie jest możliwe, należy rozważyć użycie inny filtr.</span><span class="sxs-lookup"><span data-stu-id="2b63c-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="2b63c-152">Filtry globalne aktualizacji</span><span class="sxs-lookup"><span data-stu-id="2b63c-152">Update global Filters</span></span>
<span data-ttu-id="2b63c-153">tooupdate filtr globalny hello Użyj następującego żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="2b63c-153">tooupdate a global filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="2b63c-154">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="2b63c-154">HTTP Request</span></span>
<span data-ttu-id="2b63c-155">Nagłówki żądania:</span><span class="sxs-lookup"><span data-stu-id="2b63c-155">Request headers:</span></span> 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

<span data-ttu-id="2b63c-156">Treść żądania:</span><span class="sxs-lookup"><span data-stu-id="2b63c-156">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a><span data-ttu-id="2b63c-157">Aktualizacja lokalnych AssetFilters</span><span class="sxs-lookup"><span data-stu-id="2b63c-157">Update local AssetFilters</span></span>
<span data-ttu-id="2b63c-158">tooupdate filtr lokalne powitania Użyj następującego żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="2b63c-158">tooupdate a local filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="2b63c-159">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="2b63c-159">HTTP Request</span></span>
<span data-ttu-id="2b63c-160">Nagłówki żądania:</span><span class="sxs-lookup"><span data-stu-id="2b63c-160">Request headers:</span></span> 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

<span data-ttu-id="2b63c-161">Treść żądania:</span><span class="sxs-lookup"><span data-stu-id="2b63c-161">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a><span data-ttu-id="2b63c-162">Usuwanie filtrów</span><span class="sxs-lookup"><span data-stu-id="2b63c-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="2b63c-163">Usuń filtry globalne</span><span class="sxs-lookup"><span data-stu-id="2b63c-163">Delete global Filters</span></span>
<span data-ttu-id="2b63c-164">toodelete filtr globalny Użyj hello następujące żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="2b63c-164">toodelete a global Filter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="2b63c-165">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="2b63c-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="2b63c-166">Usuń lokalne AssetFilters</span><span class="sxs-lookup"><span data-stu-id="2b63c-166">Delete local AssetFilters</span></span>
<span data-ttu-id="2b63c-167">toodelete AssetFilter lokalnego, należy użyć hello następujące żądania HTTP:</span><span class="sxs-lookup"><span data-stu-id="2b63c-167">toodelete a local AssetFilter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="2b63c-168">Żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="2b63c-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="2b63c-169">Tworzenie adresów URL, które należy używać filtrów przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="2b63c-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="2b63c-170">Aby uzyskać informacje dotyczące toopublish i dostarczyć zasobów, zobacz temat [tooCustomers dostarczanie zawartości omówienie](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2b63c-170">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="2b63c-171">Witaj następujące przykłady przedstawiają sposób tooadd filtry tooyour adresów URL przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="2b63c-171">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="2b63c-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="2b63c-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="2b63c-173">**Apple HTTP Live przesyłania strumieniowego V4 (HLS)**</span><span class="sxs-lookup"><span data-stu-id="2b63c-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="2b63c-174">**Apple HTTP Live przesyłania strumieniowego V3 (HLS)**</span><span class="sxs-lookup"><span data-stu-id="2b63c-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="2b63c-175">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="2b63c-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="2b63c-176">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="2b63c-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2b63c-177">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="2b63c-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="2b63c-178">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2b63c-178">See Also</span></span>
[<span data-ttu-id="2b63c-179">Omówienie dynamicznej manifestów</span><span class="sxs-lookup"><span data-stu-id="2b63c-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

