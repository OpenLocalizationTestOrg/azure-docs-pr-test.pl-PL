---
title: "AAA jak tooget wystąpienia procesor multimediów przy użyciu REST | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate tooencode składnika procesora nośnika przekonwertowania formatu, szyfrowania lub odszyfrowywania zawartości nośnika dla usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a>Jak tooget wystąpienia procesor multimediów
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Omówienie
W usłudze Media Services, który procesor multimediów jest składnikiem, który obsługuje przetwarzania specyficznego dla zadania, takie jak kodowanie format konwersji, szyfrowania lub odszyfrowywania zawartości nośnika. Zazwyczaj tworzenie procesor multimediów, tworząc tooencode zadań, szyfrowanie lub przekonwertować format hello zawartości nośnika.

## <a name="azure-media-processors"></a>Procesory multimediów Azure 

Witaj kolejny temat zawiera listę procesory multimediów:

* [Kodowanie procesory multimediów](scenarios-and-availability.md#encoding-media-processors)
* [Procesory multimediów usługi analiza](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
>Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP. Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).

## <a name="connect-toomedia-services"></a>Połączenie usług tooMedia

Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów. Należy wykonać kolejne wywołania toohello nowy identyfikator URI.

## <a name="get-a-media-processor"></a>Pobierz procesor multimediów

Po wywołaniu REST Hello pokazuje, jak tooget procesor multimediów wystąpienia według nazwy (w tym przypadku **Media Encoder Standard**). 

Żądanie:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

Odpowiedź:

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Następne kroki
Teraz, gdy wiesz, jak tooget wystąpienie procesora nośnika, przejdź toohello [jak tooEncode zasób](media-services-rest-get-started.md) tematu, w której opisano, jak toouse hello Media Encoder Standard tooencode zasób.

