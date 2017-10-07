---
title: "Procesor nośnika przy użyciu tooCreate aaaHow hello Azure Media Services SDK dla platformy .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate tooencode składnika procesora nośnika przekonwertowania formatu, szyfrowania lub odszyfrowywania zawartości nośnika dla usługi Azure Media Services. Przykłady kodu są napisane w języku C# i używają hello SDK usługi Media Services dla platformy .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="effc5-104">Porady: uzyskiwanie wystąpienia procesora nośnika</span><span class="sxs-lookup"><span data-stu-id="effc5-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="effc5-105">.NET</span><span class="sxs-lookup"><span data-stu-id="effc5-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="effc5-106">REST</span><span class="sxs-lookup"><span data-stu-id="effc5-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="effc5-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="effc5-107">Overview</span></span>
<span data-ttu-id="effc5-108">W usłudze Media Services, który procesor multimediów jest składnikiem, który obsługuje przetwarzania specyficznego dla zadania, takie jak kodowanie format konwersji, szyfrowania lub odszyfrowywania zawartości nośnika.</span><span class="sxs-lookup"><span data-stu-id="effc5-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="effc5-109">Zazwyczaj tworzenie procesor multimediów, tworząc tooencode zadań, szyfrowanie lub przekonwertować format hello zawartości nośnika.</span><span class="sxs-lookup"><span data-stu-id="effc5-109">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="effc5-110">Procesory multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="effc5-110">Azure media processors</span></span> 

<span data-ttu-id="effc5-111">Witaj kolejny temat zawiera listę procesory multimediów:</span><span class="sxs-lookup"><span data-stu-id="effc5-111">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="effc5-112">Kodowanie procesory multimediów</span><span class="sxs-lookup"><span data-stu-id="effc5-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="effc5-113">Procesory multimediów usługi analiza</span><span class="sxs-lookup"><span data-stu-id="effc5-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="effc5-114">Pobierz procesor multimediów</span><span class="sxs-lookup"><span data-stu-id="effc5-114">Get Media Processor</span></span>

<span data-ttu-id="effc5-115">Witaj po — metoda, pokazuje sposób tooget wystąpienia procesora nośnika.</span><span class="sxs-lookup"><span data-stu-id="effc5-115">hello following method shows how tooget a media processor instance.</span></span> <span data-ttu-id="effc5-116">Hello przykład kodu zakłada użycie hello zmiennej poziom modułu o nazwie **_kontekstu** tooreference kontekstu serwera hello zgodnie z opisem w sekcji hello [porady: połączenie programowe usługi tooMedia](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="effc5-116">hello code example assumes hello use of a module-level variable named **_context** tooreference hello server context as described in hello section [How to: Connect tooMedia Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="effc5-117">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="effc5-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="effc5-118">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="effc5-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="effc5-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="effc5-119">Next Steps</span></span>
<span data-ttu-id="effc5-120">Teraz, gdy wiesz, jak tooget wystąpienie procesora nośnika, przejdź toohello [jak tooEncode zasób](media-services-dotnet-encode-with-media-encoder-standard.md) tematu, w której opisano, jak toouse hello Media Encoder Standard tooencode zasób.</span><span class="sxs-lookup"><span data-stu-id="effc5-120">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

