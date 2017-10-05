---
title: "Jak utworzyć procesor multimediów przy użyciu zestawu SDK usługi Azure Media Services dla platformy .NET | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia nośnika składnika procesora do kodowania, przekonwertować format, szyfrowania lub odszyfrowywania zawartości nośnika dla usługi Azure Media Services. Przykłady kodu są napisane w języku C# i używają SDK usługi Media Services dla platformy .NET."
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
ms.openlocfilehash: c2cbe41b71afa8acc184f9d7f4cfe94686de783e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="7ef45-104">Porady: uzyskiwanie wystąpienia procesora nośnika</span><span class="sxs-lookup"><span data-stu-id="7ef45-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ef45-105">.NET</span><span class="sxs-lookup"><span data-stu-id="7ef45-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="7ef45-106">REST</span><span class="sxs-lookup"><span data-stu-id="7ef45-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="7ef45-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7ef45-107">Overview</span></span>
<span data-ttu-id="7ef45-108">W usłudze Media Services, który procesor multimediów jest składnikiem, który obsługuje przetwarzania specyficznego dla zadania, takie jak kodowanie format konwersji, szyfrowania lub odszyfrowywania zawartości nośnika.</span><span class="sxs-lookup"><span data-stu-id="7ef45-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="7ef45-109">Podczas tworzenia zadania kodowania, szyfrowania lub przekonwertować format zawartości multimedialnej zwykle utworzyć procesor multimediów.</span><span class="sxs-lookup"><span data-stu-id="7ef45-109">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="7ef45-110">Procesory multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="7ef45-110">Azure media processors</span></span> 

<span data-ttu-id="7ef45-111">Poniższy temat zawiera listę procesory multimediów:</span><span class="sxs-lookup"><span data-stu-id="7ef45-111">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="7ef45-112">Kodowanie procesory multimediów</span><span class="sxs-lookup"><span data-stu-id="7ef45-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="7ef45-113">Procesory multimediów usługi analiza</span><span class="sxs-lookup"><span data-stu-id="7ef45-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="7ef45-114">Pobierz procesor multimediów</span><span class="sxs-lookup"><span data-stu-id="7ef45-114">Get Media Processor</span></span>

<span data-ttu-id="7ef45-115">Następująca metoda pokazano, jak pobrać wystąpienia procesora nośnika.</span><span class="sxs-lookup"><span data-stu-id="7ef45-115">The following method shows how to get a media processor instance.</span></span> <span data-ttu-id="7ef45-116">Przykład kodu zakłada użycie zmiennej poziom modułu o nazwie **_kontekstu** do odwołania z kontekstem serwera, zgodnie z opisem w sekcji [porady: nawiązać Media Services programowo](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="7ef45-116">The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="7ef45-117">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="7ef45-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7ef45-118">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="7ef45-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="7ef45-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ef45-119">Next Steps</span></span>
<span data-ttu-id="7ef45-120">Teraz, gdy wiesz, jak uzyskać wystąpienia procesora nośnika, przejdź do [jak kodowanie elementu zawartości](media-services-dotnet-encode-with-media-encoder-standard.md) tematu, w której opisano, jak na potrzeby Media Encoder Standard kodowanie elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="7ef45-120">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

