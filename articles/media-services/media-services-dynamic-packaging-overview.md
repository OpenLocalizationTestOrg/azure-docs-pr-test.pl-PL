---
title: "Omówienie dynamicznego tworzenia pakietów usługi Media Services aaaAzure | Dokumentacja firmy Microsoft"
description: "Omówienie z dynamicznego tworzenia pakietów i Hello zapewnia tematu."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a>Dynamiczne tworzenie pakietów
## <a name="overview"></a>Omówienie
Microsoft Azure Media Services może być używane toodeliver wiele nośnika źródłowego formatów plików, formatów przesyłania strumieniowego multimediów i ochrony zawartości formatów tooa różne technologie klienta (na przykład iOS, XBOX, Silverlight, Windows 8). Ci klienci zrozumienie różnych protokołów, na przykład iOS wymaga formatu HTTP Live Streaming (HLS) w wersji 4 i Silverlight i Xbox wymagają Smooth Streaming. Jeśli istnieje zestaw o adaptacyjnej szybkości transmisji bitów (różnych szybkościach transmisji bitów) MP4 plików (ISO Base nośników 14496 12) lub zestawu plików funkcji Smooth Streaming adaptacyjną szybkością transmisji bitów, które mają tooclients tooserve, który MPEG DASH, HLS lub Smooth Streaming, należy skorzystać z nośnika Dynamiczne tworzenie pakietów usług.

Pakowania dynamicznego, wymagany jest toocreate element zawartości zawierający zestaw plików MP4 lub Smooth Streaming plików. Następnie na podstawie hello formatu określonego w manifeście hello lub fragmentu żądania, hello Streaming na żądanie serwera zapewni odbierania strumienia hello w protokole hello, wybrana. W związku z tym konieczne toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź hello na podstawie żądań klienta.

Witaj Poniższy diagram przedstawia hello tradycyjne kodowanie i statyczne pakowania przepływ pracy.

![Kodowanie statyczne](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

Witaj Poniższy diagram przedstawia przepływ pracy dynamicznego tworzenia pakietów hello.

![Kodowanie dynamiczne](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a>Typowy scenariusz
1. Przekaż plik wejściowy (nazywanego plikiem mezzanine). Na przykład, H.264, MP4 lub WMV (hello Lista obsługiwanych formatów, zobacz [obsługiwane formaty przez hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).
2. Kodowanie z mezzanine pliku tooH.264 MP4 o adaptacyjnej szybkości bitowej zestawów.
3. Publikowanie zawartości hello, który zawiera hello o adaptacyjnej szybkości bitowej MP4 ustawiony przez utworzenie hello lokalizatora na żądanie.
4. Skompiluj hello przesyłania strumieniowego tooaccess adresy URL i strumienia zawartości.

## <a name="preparing-assets-for-dynamic-streaming"></a>Przygotowanie zasobów do dynamicznego przesyłania strumieniowego
tooprepare zawartości do przesyłania strumieniowego można dynamicznie są dostępne dwie opcje:

1. [Przekaż plik główny](media-services-dotnet-upload-files.md).
2. [Użyj hello Media Encoder Standard koder tooproduce H.264 MP4 o adaptacyjnej szybkości bitowej zestawy](media-services-dotnet-encode-with-media-encoder-standard.md).
3. [Strumieniowo zawartość](media-services-deliver-content-overview.md).

## <a id="unsupported_formats"></a>Formatów, które nie są obsługiwane przez funkcję dynamicznego tworzenia pakietów
Witaj następujących formatów pliku źródłowego nie są obsługiwane przez funkcję dynamicznego tworzenia pakietów.

* Pliki mp4 cyfrowe Dolby.
* Pliki smooth cyfrowe Dolby.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

