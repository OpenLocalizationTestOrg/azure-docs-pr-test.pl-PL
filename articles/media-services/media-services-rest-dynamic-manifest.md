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
# <a name="creating-filters-with-azure-media-services-rest-api"></a>Tworzenia filtrów z usługi Azure Media Services interfejsu API REST
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

Począwszy od wersji 2.11, Media Services umożliwia filtry toodefine trwałych. Te filtry są reguły po stronie serwera, zezwalające klientom toochoose toodo np.: odtwarzanie tylko części klipu wideo (a nie odtwarzane hello całego wideo), lub określ tylko podzestaw audio i wideo wersji obsługi (przez klienta urządzenia zamiast wersji hello wszystkich skojarzonych z hello zasobów). Filtrowania elementów zawartości zostaną zarchiwizowane za pośrednictwem **dynamiczne manifestu**, które są tworzone w chwili toostream żądania klienta wideo oparte na określonej filtry.

Bardziej szczegółowe informacje pokrewne toofilters i dynamiczne manifestu, zobacz [dynamicznie manifesty omówienie](media-services-dynamic-manifest-overview.md).

W tym temacie przedstawiono sposób toouse toocreate interfejsów API REST, aktualizować i usuwać filtrów. 

## <a name="types-used-toocreate-filters"></a>Typy używane filtry toocreate
Witaj następujące typy są używane podczas tworzenia filtrów:  

* [Filtr](https://docs.microsoft.com/rest/api/media/operations/filter)
* [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [FilterTrackSelect i FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

>Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP. Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Połączenie usług tooMedia

Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów. Należy wykonać kolejne wywołania toohello nowy identyfikator URI.

## <a name="create-filters"></a>Tworzenie filtrów
### <a name="create-global-filters"></a>Utwórz filtry globalne
toocreate filtr globalny Użyj hello następujące żądania HTTP:  

#### <a name="http-request"></a>Żądania HTTP
Nagłówki żądania

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

Treść żądania 

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




#### <a name="http-response"></a>Odpowiedź HTTP
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a>Utwórz AssetFilters lokalnego
toocreate AssetFilter lokalnego, należy użyć hello następujące żądania HTTP:  

#### <a name="http-request"></a>Żądania HTTP
Nagłówki żądania

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

Treść żądania 

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

#### <a name="http-response"></a>Odpowiedź HTTP
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a>Lista filtrów
### <a name="get-all-global-filters-in-hello-ams-account"></a>Pobierz wszystkie globalne **filtru**s na koncie hello AMS
filtry toolist Użyj hello następujące żądania HTTP: 

#### <a name="http-request"></a>Żądania HTTP
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a>Pobierz **AssetFilter**s skojarzony z zasobem
#### <a name="http-request"></a>Żądania HTTP
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a>Pobierz **AssetFilter** na podstawie jego identyfikatora
#### <a name="http-request"></a>Żądania HTTP
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a>Filtry aktualizacji
Użyj poprawka tooupdate PUT lub scalania filtr o nowej wartości właściwości.  Aby uzyskać więcej informacji o tych operacjach, zobacz [poprawki, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).

Po zaktualizowaniu filtru może potrwać too2 minut do przesyłania strumieniowego punktu końcowego toorefresh hello reguły. Jeśli zawartość hello zostało obsłużone przy użyciu tego filtru (i w pamięci podręcznej serwerów proxy i sieci CDN pamięci podręcznych), aktualizacja tego filtru może powodować błędy player. Jest zalecane tooclear hello w pamięci podręcznej po zaktualizowaniu hello filtru. Jeśli ta opcja nie jest możliwe, należy rozważyć użycie inny filtr.  

### <a name="update-global-filters"></a>Filtry globalne aktualizacji
tooupdate filtr globalny hello Użyj następującego żądania HTTP: 

#### <a name="http-request"></a>Żądania HTTP
Nagłówki żądania: 

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

Treść żądania: 

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

### <a name="update-local-assetfilters"></a>Aktualizacja lokalnych AssetFilters
tooupdate filtr lokalne powitania Użyj następującego żądania HTTP: 

#### <a name="http-request"></a>Żądania HTTP
Nagłówki żądania: 

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

Treść żądania: 

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


## <a name="delete-filters"></a>Usuwanie filtrów
### <a name="delete-global-filters"></a>Usuń filtry globalne
toodelete filtr globalny Użyj hello następujące żądania HTTP:

#### <a name="http-request"></a>Żądania HTTP
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a>Usuń lokalne AssetFilters
toodelete AssetFilter lokalnego, należy użyć hello następujące żądania HTTP:

#### <a name="http-request"></a>Żądania HTTP
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a>Tworzenie adresów URL, które należy używać filtrów przesyłania strumieniowego
Aby uzyskać informacje dotyczące toopublish i dostarczyć zasobów, zobacz temat [tooCustomers dostarczanie zawartości omówienie](media-services-deliver-content-overview.md).

Witaj następujące przykłady przedstawiają sposób tooadd filtry tooyour adresów URL przesyłania strumieniowego.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live przesyłania strumieniowego V4 (HLS)**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live przesyłania strumieniowego V3 (HLS)**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Smooth Streaming**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Omówienie dynamicznej manifestów](media-services-dynamic-manifest-overview.md)

