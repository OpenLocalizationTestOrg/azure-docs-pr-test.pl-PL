---
title: "aaaOverview i porównanie Azure na żądanie koderów nośnika | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="d05ac-103">Omówienie i porównanie Azure na żądanie nośnika koderów</span><span class="sxs-lookup"><span data-stu-id="d05ac-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="d05ac-104">Omówienie kodowania</span><span class="sxs-lookup"><span data-stu-id="d05ac-104">Encoding overview</span></span>
<span data-ttu-id="d05ac-105">Azure Media Services udostępnia wiele opcji hello kodowania nośnika w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="d05ac-105">Azure Media Services provides multiple options for hello encoding of media in hello cloud.</span></span>

<span data-ttu-id="d05ac-106">Podczas uruchamiania z programem Media Services, jest ważne toounderstand hello różnica między koderów-dekoderów i plik formatu.</span><span class="sxs-lookup"><span data-stu-id="d05ac-106">When starting out with Media Services, it is important toounderstand hello difference between codecs and file formats.</span></span>
<span data-ttu-id="d05ac-107">Kodery-dekodery hello oprogramowania, które implementuje algorytmy kompresji i dekompresji hello formatów plików są kontenery zawierających hello skompresowane wideo.</span><span class="sxs-lookup"><span data-stu-id="d05ac-107">Codecs are hello software that implements hello compression/decompression algorithms whereas file formats are containers that hold hello compressed video.</span></span>

<span data-ttu-id="d05ac-108">Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver Twojego o adaptacyjnej szybkości bitowej MP4 lub Smooth Streaming zakodowane zawartości w formatach transmisji strumieniowej obsługiwanych przez usługę Media Services (MPEG DASH, HLS, Smooth Streaming) bez konieczności toore pakietów w tych formatach transmisji strumieniowej.</span><span class="sxs-lookup"><span data-stu-id="d05ac-108">Media Services provides dynamic packaging which allows you toodeliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having toore-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="d05ac-109">Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu.</span><span class="sxs-lookup"><span data-stu-id="d05ac-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="d05ac-110">przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="d05ac-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> <span data-ttu-id="d05ac-111">Zaletą tootake [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md), należy toodo hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="d05ac-111">tootake advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need toodo hello following:</span></span>
>
><span data-ttu-id="d05ac-112">Ponadto kodowanie pliku źródłowego do zestawu plików MP4 lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów (kroki kodowania hello przedstawiono w dalszej części tego samouczka).</span><span class="sxs-lookup"><span data-stu-id="d05ac-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (hello encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="d05ac-113">Usługa Media Services obsługuje następujące hello na koderów żądanie, które zostały opisane w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="d05ac-113">Media Services supports hello following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="d05ac-114">Usługa Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="d05ac-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="d05ac-115">Przepływ pracy usługi Media Encoder w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="d05ac-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="d05ac-116">Ten artykuł zawiera krótki przegląd na żądanie koderów nośnika i zapewnia tooarticles łącza, które zapewniają bardziej szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d05ac-116">This article gives a brief overview of on demand media encoders and provides links tooarticles that give more detailed information.</span></span> <span data-ttu-id="d05ac-117">Witaj temat zawiera również porównania koderów hello.</span><span class="sxs-lookup"><span data-stu-id="d05ac-117">hello topic also provides comparison of hello encoders.</span></span>

>[!NOTE]
><span data-ttu-id="d05ac-118">Domyślnie wszystkie konta usługi Media Services może mieć aktywne zadania kodowania w czasie.</span><span class="sxs-lookup"><span data-stu-id="d05ac-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="d05ac-119">Jednostki kodowania, które pozwalają toohave może zarezerwować wielu zadań kodowania uruchomione jednocześnie, po jednej dla każdego kodowania jednostka zarezerwowanego zakupu.</span><span class="sxs-lookup"><span data-stu-id="d05ac-119">You can reserve encoding units that allow you toohave multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="d05ac-120">Aby uzyskać informacje, zobacz [skalowania jednostki kodowania](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d05ac-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="d05ac-121">Usługa Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="d05ac-121">Media Encoder Standard</span></span>
### <a name="how-toouse"></a><span data-ttu-id="d05ac-122">Jak toouse</span><span class="sxs-lookup"><span data-stu-id="d05ac-122">How toouse</span></span>
[<span data-ttu-id="d05ac-123">Jak tooencode przy użyciu Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="d05ac-123">How tooencode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="d05ac-124">Formaty</span><span class="sxs-lookup"><span data-stu-id="d05ac-124">Formats</span></span>
[<span data-ttu-id="d05ac-125">Koderów-dekoderów i formaty</span><span class="sxs-lookup"><span data-stu-id="d05ac-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="d05ac-126">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="d05ac-126">Presets</span></span>
<span data-ttu-id="d05ac-127">Media Encoder Standard została skonfigurowana przy użyciu jednego ustawień kodera hello opisane [tutaj](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d05ac-127">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="d05ac-128">Wejście i wyjście metadanych</span><span class="sxs-lookup"><span data-stu-id="d05ac-128">Input and output metadata</span></span>
<span data-ttu-id="d05ac-129">Hello metadanych wejściowych koderów opisano [tutaj](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d05ac-129">hello encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="d05ac-130">Hello koderów dane wyjściowe metadanych opisano [tutaj](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="d05ac-130">hello encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="d05ac-131">Generowanie miniatur</span><span class="sxs-lookup"><span data-stu-id="d05ac-131">Generate thumbnails</span></span>
<span data-ttu-id="d05ac-132">Aby uzyskać informacje, zobacz [jak miniatur toogenerate przy użyciu standardu Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="d05ac-132">For information, see [How toogenerate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="d05ac-133">TRIM wideo (wycinka)</span><span class="sxs-lookup"><span data-stu-id="d05ac-133">Trim videos (clipping)</span></span>
<span data-ttu-id="d05ac-134">Aby uzyskać informacje, zobacz [jak tootrim pliki wideo przy użyciu standardu Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="d05ac-134">For information, see [How tootrim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="d05ac-135">Utwórz nakładki</span><span class="sxs-lookup"><span data-stu-id="d05ac-135">Create overlays</span></span>
<span data-ttu-id="d05ac-136">Aby uzyskać informacje, zobacz [jak nakładki toocreate przy użyciu standardu Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="d05ac-136">For information, see [How toocreate overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="d05ac-137">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d05ac-137">See also</span></span>
[<span data-ttu-id="d05ac-138">blog usługi Media Services Hello</span><span class="sxs-lookup"><span data-stu-id="d05ac-138">hello Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="d05ac-139">Przepływ pracy usługi Media Encoder w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="d05ac-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="d05ac-140">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d05ac-140">Overview</span></span>
[<span data-ttu-id="d05ac-141">Wprowadzenie do kodowania w Azure Media Services w wersji Premium</span><span class="sxs-lookup"><span data-stu-id="d05ac-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a><span data-ttu-id="d05ac-142">Jak toouse</span><span class="sxs-lookup"><span data-stu-id="d05ac-142">How toouse</span></span>
<span data-ttu-id="d05ac-143">Media Encoder Premium w przepływie pracy jest skonfigurowana przy użyciu złożonych przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="d05ac-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="d05ac-144">Pliki przepływu pracy może zostać utworzony i zaktualizować przy użyciu hello [projektanta przepływów pracy](media-services-workflow-designer.md) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="d05ac-144">Workflow files could be created and updated using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="d05ac-145">Jak tooUse Premium kodowania w usłudze Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="d05ac-145">How tooUse Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="d05ac-146">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="d05ac-146">Known issues</span></span>
<span data-ttu-id="d05ac-147">Jeśli wejściowy plik wideo nie zawiera kodowane, hello wyjściowe zasobów nadal będzie zawierać pusty plik TTML.</span><span class="sxs-lookup"><span data-stu-id="d05ac-147">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="d05ac-148">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="d05ac-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d05ac-149">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="d05ac-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="d05ac-150">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="d05ac-150">Related articles</span></span>
* [<span data-ttu-id="d05ac-151">Wykonywania zaawansowanych zadań kodowania dostosowując ustawienia standardu Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="d05ac-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="d05ac-152">Przydziały i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="d05ac-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
