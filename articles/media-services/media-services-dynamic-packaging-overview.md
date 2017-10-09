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
# <a name="dynamic-packaging"></a><span data-ttu-id="acf0b-103">Dynamiczne tworzenie pakietów</span><span class="sxs-lookup"><span data-stu-id="acf0b-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="acf0b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="acf0b-104">Overview</span></span>
<span data-ttu-id="acf0b-105">Microsoft Azure Media Services może być używane toodeliver wiele nośnika źródłowego formatów plików, formatów przesyłania strumieniowego multimediów i ochrony zawartości formatów tooa różne technologie klienta (na przykład iOS, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="acf0b-105">Microsoft Azure Media Services can be used toodeliver many media source file formats, media streaming formats, and content protection formats tooa variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="acf0b-106">Ci klienci zrozumienie różnych protokołów, na przykład iOS wymaga formatu HTTP Live Streaming (HLS) w wersji 4 i Silverlight i Xbox wymagają Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="acf0b-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="acf0b-107">Jeśli istnieje zestaw o adaptacyjnej szybkości transmisji bitów (różnych szybkościach transmisji bitów) MP4 plików (ISO Base nośników 14496 12) lub zestawu plików funkcji Smooth Streaming adaptacyjną szybkością transmisji bitów, które mają tooclients tooserve, który MPEG DASH, HLS lub Smooth Streaming, należy skorzystać z nośnika Dynamiczne tworzenie pakietów usług.</span><span class="sxs-lookup"><span data-stu-id="acf0b-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want tooserve tooclients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="acf0b-108">Pakowania dynamicznego, wymagany jest toocreate element zawartości zawierający zestaw plików MP4 lub Smooth Streaming plików.</span><span class="sxs-lookup"><span data-stu-id="acf0b-108">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="acf0b-109">Następnie na podstawie hello formatu określonego w manifeście hello lub fragmentu żądania, hello Streaming na żądanie serwera zapewni odbierania strumienia hello w protokole hello, wybrana.</span><span class="sxs-lookup"><span data-stu-id="acf0b-109">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="acf0b-110">W związku z tym konieczne toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź hello na podstawie żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="acf0b-110">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="acf0b-111">Witaj Poniższy diagram przedstawia hello tradycyjne kodowanie i statyczne pakowania przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="acf0b-111">hello following diagram shows hello traditional encoding and static packaging workflow.</span></span>

![Kodowanie statyczne](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="acf0b-113">Witaj Poniższy diagram przedstawia przepływ pracy dynamicznego tworzenia pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="acf0b-113">hello following diagram shows hello dynamic packaging workflow.</span></span>

![Kodowanie dynamiczne](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="acf0b-115">Typowy scenariusz</span><span class="sxs-lookup"><span data-stu-id="acf0b-115">Common scenario</span></span>
1. <span data-ttu-id="acf0b-116">Przekaż plik wejściowy (nazywanego plikiem mezzanine).</span><span class="sxs-lookup"><span data-stu-id="acf0b-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="acf0b-117">Na przykład, H.264, MP4 lub WMV (hello Lista obsługiwanych formatów, zobacz [obsługiwane formaty przez hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span><span class="sxs-lookup"><span data-stu-id="acf0b-117">For example, H.264, MP4, or WMV (for hello list of supported formats see [Formats Supported by hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="acf0b-118">Kodowanie z mezzanine pliku tooH.264 MP4 o adaptacyjnej szybkości bitowej zestawów.</span><span class="sxs-lookup"><span data-stu-id="acf0b-118">Encode your mezzanine file tooH.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="acf0b-119">Publikowanie zawartości hello, który zawiera hello o adaptacyjnej szybkości bitowej MP4 ustawiony przez utworzenie hello lokalizatora na żądanie.</span><span class="sxs-lookup"><span data-stu-id="acf0b-119">Publish hello asset that contains hello adaptive bitrate MP4 set by creating hello On-Demand Locator.</span></span>
4. <span data-ttu-id="acf0b-120">Skompiluj hello przesyłania strumieniowego tooaccess adresy URL i strumienia zawartości.</span><span class="sxs-lookup"><span data-stu-id="acf0b-120">Build hello streaming URLs tooaccess and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="acf0b-121">Przygotowanie zasobów do dynamicznego przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="acf0b-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="acf0b-122">tooprepare zawartości do przesyłania strumieniowego można dynamicznie są dostępne dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="acf0b-122">tooprepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="acf0b-123">[Przekaż plik główny](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="acf0b-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="acf0b-124">[Użyj hello Media Encoder Standard koder tooproduce H.264 MP4 o adaptacyjnej szybkości bitowej zestawy](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="acf0b-124">[Use hello Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="acf0b-125">[Strumieniowo zawartość](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="acf0b-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="acf0b-126"><a id="unsupported_formats"></a>Formatów, które nie są obsługiwane przez funkcję dynamicznego tworzenia pakietów</span><span class="sxs-lookup"><span data-stu-id="acf0b-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="acf0b-127">Witaj następujących formatów pliku źródłowego nie są obsługiwane przez funkcję dynamicznego tworzenia pakietów.</span><span class="sxs-lookup"><span data-stu-id="acf0b-127">hello following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="acf0b-128">Pliki mp4 cyfrowe Dolby.</span><span class="sxs-lookup"><span data-stu-id="acf0b-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="acf0b-129">Pliki smooth cyfrowe Dolby.</span><span class="sxs-lookup"><span data-stu-id="acf0b-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="acf0b-130">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="acf0b-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="acf0b-131">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="acf0b-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

