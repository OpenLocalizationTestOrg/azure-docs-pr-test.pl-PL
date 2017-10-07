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
# <a name="how-tooget-a-media-processor-instance"></a><span data-ttu-id="0de1f-103">Jak tooget wystąpienia procesor multimediów</span><span class="sxs-lookup"><span data-stu-id="0de1f-103">How tooget a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0de1f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0de1f-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="0de1f-105">REST</span><span class="sxs-lookup"><span data-stu-id="0de1f-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="0de1f-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0de1f-106">Overview</span></span>
<span data-ttu-id="0de1f-107">W usłudze Media Services, który procesor multimediów jest składnikiem, który obsługuje przetwarzania specyficznego dla zadania, takie jak kodowanie format konwersji, szyfrowania lub odszyfrowywania zawartości nośnika.</span><span class="sxs-lookup"><span data-stu-id="0de1f-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="0de1f-108">Zazwyczaj tworzenie procesor multimediów, tworząc tooencode zadań, szyfrowanie lub przekonwertować format hello zawartości nośnika.</span><span class="sxs-lookup"><span data-stu-id="0de1f-108">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="0de1f-109">Procesory multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="0de1f-109">Azure media processors</span></span> 

<span data-ttu-id="0de1f-110">Witaj kolejny temat zawiera listę procesory multimediów:</span><span class="sxs-lookup"><span data-stu-id="0de1f-110">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="0de1f-111">Kodowanie procesory multimediów</span><span class="sxs-lookup"><span data-stu-id="0de1f-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="0de1f-112">Procesory multimediów usługi analiza</span><span class="sxs-lookup"><span data-stu-id="0de1f-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="0de1f-113">Podczas uzyskiwania dostępu do obiektów w usłudze Media Services, należy ustawić określonych pól nagłówka i wartości w Twoich żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="0de1f-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="0de1f-114">Aby uzyskać więcej informacji, zobacz [ustawień dla rozwoju interfejsu API REST usługi Media](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0de1f-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="0de1f-115">Połączenie usług tooMedia</span><span class="sxs-lookup"><span data-stu-id="0de1f-115">Connect tooMedia Services</span></span>

<span data-ttu-id="0de1f-116">Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0de1f-116">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="0de1f-117">Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="0de1f-117">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="0de1f-118">Należy wykonać kolejne wywołania toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="0de1f-118">You must make subsequent calls toohello new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="0de1f-119">Pobierz procesor multimediów</span><span class="sxs-lookup"><span data-stu-id="0de1f-119">Get a media processor</span></span>

<span data-ttu-id="0de1f-120">Po wywołaniu REST Hello pokazuje, jak tooget procesor multimediów wystąpienia według nazwy (w tym przypadku **Media Encoder Standard**).</span><span class="sxs-lookup"><span data-stu-id="0de1f-120">hello following REST call shows how tooget a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="0de1f-121">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="0de1f-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="0de1f-122">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="0de1f-122">Response:</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="0de1f-123">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="0de1f-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0de1f-124">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="0de1f-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0de1f-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0de1f-125">Next Steps</span></span>
<span data-ttu-id="0de1f-126">Teraz, gdy wiesz, jak tooget wystąpienie procesora nośnika, przejdź toohello [jak tooEncode zasób](media-services-rest-get-started.md) tematu, w której opisano, jak toouse hello Media Encoder Standard tooencode zasób.</span><span class="sxs-lookup"><span data-stu-id="0de1f-126">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-rest-get-started.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

