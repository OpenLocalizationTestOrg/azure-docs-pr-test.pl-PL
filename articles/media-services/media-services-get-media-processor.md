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
# <a name="how-to-get-a-media-processor-instance"></a>Porady: uzyskiwanie wystąpienia procesora nośnika
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

## <a name="get-media-processor"></a>Pobierz procesor multimediów

Witaj po — metoda, pokazuje sposób tooget wystąpienia procesora nośnika. Hello przykład kodu zakłada użycie hello zmiennej poziom modułu o nazwie **_kontekstu** tooreference kontekstu serwera hello zgodnie z opisem w sekcji hello [porady: połączenie programowe usługi tooMedia](media-services-use-aad-auth-to-access-ams-api.md).

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Następne kroki
Teraz, gdy wiesz, jak tooget wystąpienie procesora nośnika, przejdź toohello [jak tooEncode zasób](media-services-dotnet-encode-with-media-encoder-standard.md) tematu, w której opisano, jak toouse hello Media Encoder Standard tooencode zasób.

