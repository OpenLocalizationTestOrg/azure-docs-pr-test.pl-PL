---
title: "Omówienie i porównanie Azure na żądanie nośnika koderów | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie i porównanie Azure na żądanie koderów nośnika."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 538a6ab60168735c2626a93cdeedd8d4999a6efc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="db80d-103">Omówienie i porównanie Azure na żądanie nośnika koderów</span><span class="sxs-lookup"><span data-stu-id="db80d-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="db80d-104">Omówienie kodowania</span><span class="sxs-lookup"><span data-stu-id="db80d-104">Encoding overview</span></span>
<span data-ttu-id="db80d-105">Azure Media Services udostępnia wiele opcji kodowania nośnika w chmurze.</span><span class="sxs-lookup"><span data-stu-id="db80d-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span></span>

<span data-ttu-id="db80d-106">Podczas uruchamiania z programem Media Services, należy zrozumieć różnicę między formatami koderów-dekoderów i plików.</span><span class="sxs-lookup"><span data-stu-id="db80d-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span></span>
<span data-ttu-id="db80d-107">Kodery-dekodery to oprogramowanie, które implementuje algorytmy kompresji i dekompresji formatów plików są kontenery zawierających skompresowane wideo.</span><span class="sxs-lookup"><span data-stu-id="db80d-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span></span>

<span data-ttu-id="db80d-108">Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, co pozwala na dostarczanie zawartości o adaptacyjnej szybkości bitowej MP4 lub Smooth Streaming zakodowane w formatach transmisji strumieniowej obsługiwanych przez usługę Media Services (MPEG DASH, HLS, Smooth Streaming) bez konieczności ponownego tworzenia pakietów w tych formatach.</span><span class="sxs-lookup"><span data-stu-id="db80d-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="db80d-109">Po utworzeniu konta usługi AMS zostanie do niego dodany **domyślny** punkt końcowy przesyłania strumieniowego mający stan **Zatrzymany**.</span><span class="sxs-lookup"><span data-stu-id="db80d-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="db80d-110">Aby rozpocząć przesyłanie strumieniowe zawartości oraz korzystać z dynamicznego tworzenia pakietów i szyfrowania dynamicznego, punkt końcowy przesyłania strumieniowego, z którego chcesz strumieniowo przesyłać zawartość, musi mieć stan **Uruchomiony**.</span><span class="sxs-lookup"><span data-stu-id="db80d-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> <span data-ttu-id="db80d-111">Aby móc korzystać z [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md), należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="db80d-111">To take advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need to do the following:</span></span>
>
><span data-ttu-id="db80d-112">Ponadto kodowanie pliku źródłowego do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów (kroki kodowania przedstawiono w dalszej części tego samouczka).</span><span class="sxs-lookup"><span data-stu-id="db80d-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (the encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="db80d-113">Usługa Media Services obsługuje następujące na koderów żądanie, które zostały opisane w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="db80d-113">Media Services supports the following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="db80d-114">Usługa Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="db80d-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="db80d-115">Przepływ pracy usługi Media Encoder w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="db80d-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="db80d-116">W tym artykule zawiera krótki przegląd na żądanie koderów nośnika i łącza do artykułów, które zapewniają bardziej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="db80d-116">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span></span> <span data-ttu-id="db80d-117">Temat zawiera również porównania koderów.</span><span class="sxs-lookup"><span data-stu-id="db80d-117">The topic also provides comparison of the encoders.</span></span>

>[!NOTE]
><span data-ttu-id="db80d-118">Domyślnie wszystkie konta usługi Media Services może mieć aktywne zadania kodowania w czasie.</span><span class="sxs-lookup"><span data-stu-id="db80d-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="db80d-119">Istnieje możliwość rezerwowania jednostki kodowania, które umożliwiają wielu zadań kodowania uruchomione jednocześnie, po jednej dla każdego kodowania jednostka zarezerwowanego zakupu.</span><span class="sxs-lookup"><span data-stu-id="db80d-119">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="db80d-120">Aby uzyskać informacje, zobacz [skalowania jednostki kodowania](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="db80d-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="db80d-121">Usługa Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="db80d-121">Media Encoder Standard</span></span>
### <a name="how-to-use"></a><span data-ttu-id="db80d-122">Jak stosować</span><span class="sxs-lookup"><span data-stu-id="db80d-122">How to use</span></span>
[<span data-ttu-id="db80d-123">Sposób kodowania przy użyciu Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="db80d-123">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="db80d-124">Formaty</span><span class="sxs-lookup"><span data-stu-id="db80d-124">Formats</span></span>
[<span data-ttu-id="db80d-125">Koderów-dekoderów i formaty</span><span class="sxs-lookup"><span data-stu-id="db80d-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="db80d-126">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="db80d-126">Presets</span></span>
<span data-ttu-id="db80d-127">Media Encoder Standard została skonfigurowana przy użyciu jednego ustawień kodera opisane [tutaj](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="db80d-127">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="db80d-128">Wejście i wyjście metadanych</span><span class="sxs-lookup"><span data-stu-id="db80d-128">Input and output metadata</span></span>
<span data-ttu-id="db80d-129">Opisano metadanych wejściowych koderów [tutaj](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="db80d-129">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="db80d-130">Opisano metadanych dane wyjściowe koderów [tutaj](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="db80d-130">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="db80d-131">Generowanie miniatur</span><span class="sxs-lookup"><span data-stu-id="db80d-131">Generate thumbnails</span></span>
<span data-ttu-id="db80d-132">Aby uzyskać informacje, zobacz [sposób generowania miniatur przy użyciu standardu Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="db80d-132">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="db80d-133">TRIM wideo (wycinka)</span><span class="sxs-lookup"><span data-stu-id="db80d-133">Trim videos (clipping)</span></span>
<span data-ttu-id="db80d-134">Aby uzyskać informacje, zobacz [jak przyciąć wideo przy użyciu standardu Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="db80d-134">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="db80d-135">Utwórz nakładki</span><span class="sxs-lookup"><span data-stu-id="db80d-135">Create overlays</span></span>
<span data-ttu-id="db80d-136">Aby uzyskać informacje, zobacz [tworzenie nakładki przy użyciu standardu Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="db80d-136">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="db80d-137">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="db80d-137">See also</span></span>
[<span data-ttu-id="db80d-138">Blog usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="db80d-138">The Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="db80d-139">Przepływ pracy usługi Media Encoder w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="db80d-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="db80d-140">Omówienie</span><span class="sxs-lookup"><span data-stu-id="db80d-140">Overview</span></span>
[<span data-ttu-id="db80d-141">Wprowadzenie do kodowania w Azure Media Services w wersji Premium</span><span class="sxs-lookup"><span data-stu-id="db80d-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a><span data-ttu-id="db80d-142">Jak stosować</span><span class="sxs-lookup"><span data-stu-id="db80d-142">How to use</span></span>
<span data-ttu-id="db80d-143">Media Encoder Premium w przepływie pracy jest skonfigurowana przy użyciu złożonych przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="db80d-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="db80d-144">Pliki przepływu pracy może zostać utworzony i zaktualizować przy użyciu [projektanta przepływów pracy](media-services-workflow-designer.md) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="db80d-144">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="db80d-145">Jak używać kodowania w Azure Media Services w wersji Premium</span><span class="sxs-lookup"><span data-stu-id="db80d-145">How to Use Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="db80d-146">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="db80d-146">Known issues</span></span>
<span data-ttu-id="db80d-147">Jeśli wejściowy plik wideo nie zawiera kodowane się, dane wyjściowe zasobów będzie nadal zawierać pusty plik TTML.</span><span class="sxs-lookup"><span data-stu-id="db80d-147">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="db80d-148">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="db80d-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="db80d-149">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="db80d-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="db80d-150">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="db80d-150">Related articles</span></span>
* [<span data-ttu-id="db80d-151">Wykonywania zaawansowanych zadań kodowania dostosowując ustawienia standardu Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="db80d-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="db80d-152">Przydziały i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="db80d-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
