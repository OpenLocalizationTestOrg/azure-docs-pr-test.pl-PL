---
title: "Schemat wejściowych metadanych usługi Media Services aaaAzure | Dokumentacja firmy Microsoft"
description: "Witaj temat zawiera omówienie usługi Azure Media Services wejściowych metadanych schematu."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a><span data-ttu-id="839b1-103">Dane wejściowe metadanych</span><span class="sxs-lookup"><span data-stu-id="839b1-103">Input Metadata</span></span>
<span data-ttu-id="839b1-104">Zadania kodowania jest skojarzony z zasób wejściowy (lub zasoby) na którym chcesz tooperform niektóre zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="839b1-104">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span>  <span data-ttu-id="839b1-105">Po zakończeniu zadania jest generowany zawartości wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="839b1-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="839b1-106">zawartości wyjściowej Hello zawiera wideo, audio, miniatur manifestu, zawartości wyjściowej hello itp. zawiera także plik o metadane dotyczące zasobu wejściowego hello.</span><span class="sxs-lookup"><span data-stu-id="839b1-106">hello output asset contains video, audio, thumbnails, manifest, etc. hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="839b1-107">Witaj nazwę pliku XML metadanych hello ma hello następującego formatu: &lt;asset_id&gt;_metadata.xml (na przykład 41114ad3-eb5e - 4c d 57 8 92-5354e2b7d4a4_metadata.xml), gdzie &lt;asset_id&gt; jest hello IDśrodkaTrwałego wartość hello zasobów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="839b1-107">hello name of hello metadata XML file has hello following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is hello AssetId value of hello input asset.</span></span>  

<span data-ttu-id="839b1-108">Jeśli chcesz tooexamine hello metadanych plików, można utworzyć **SAS** lokalizator i pobierania hello komputera lokalnego tooyour pliku.</span><span class="sxs-lookup"><span data-stu-id="839b1-108">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="839b1-109">Przykład można znaleźć na temat toocreate lokalizatora SAS i pobranie pliku [przy użyciu rozszerzeń zestawu SDK .NET usługi Media hello](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="839b1-109">You can find an example on how toocreate a SAS locator and download a file  [Using hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="839b1-110">W tym temacie omówiono hello elementów i typy hello schematu XML na które metada wejściowych hello (&lt;asset_id&gt;_metadata.xml) opiera się.</span><span class="sxs-lookup"><span data-stu-id="839b1-110">This topic discusses hello elements and types of hello XML schema on which hello input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="839b1-111">Informacje o hello zawierający metadane dotyczące zawartości wyjściowej hello, zobacz [metadanych dane wyjściowe](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="839b1-111">For information about hello file that contains metadata about hello output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="839b1-112">Można znaleźć hello [kodu schematu](media-services-input-metadata-schema.md#code) [przykład XML](media-services-input-metadata-schema.md#xml) na powitania na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="839b1-112">You can find hello [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at hello end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="839b1-113"><a name="AssetFiles"></a>Element AssetFiles (element główny)</span><span class="sxs-lookup"><span data-stu-id="839b1-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="839b1-114">Zawiera kolekcję [elementu AssetFile](media-services-input-metadata-schema.md#AssetFile)s hello zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="839b1-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for hello encoding job.</span></span>  

<span data-ttu-id="839b1-115">Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="839b1-115">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="839b1-116">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-116">Name</span></span> | <span data-ttu-id="839b1-117">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="839b1-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="839b1-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="839b1-119">minOccurs = maxOccurs "1" = "unbounded"</span><span class="sxs-lookup"><span data-stu-id="839b1-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="839b1-120">Element podrzędny pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="839b1-120">A single child element.</span></span> <span data-ttu-id="839b1-121">Aby uzyskać więcej informacji, zobacz [AssetFile elementu](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="839b1-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="839b1-122"><a name="AssetFile"></a>AssetFile element</span><span class="sxs-lookup"><span data-stu-id="839b1-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="839b1-123">Zawiera atrybuty i elementy, które opisują pliku zasobów.</span><span class="sxs-lookup"><span data-stu-id="839b1-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="839b1-124">Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="839b1-124">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="839b1-125">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="839b1-125">Attributes</span></span>
| <span data-ttu-id="839b1-126">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-126">Name</span></span> | <span data-ttu-id="839b1-127">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-127">Type</span></span> | <span data-ttu-id="839b1-128">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-129">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="839b1-129">**Name**</span></span><br /><br /> <span data-ttu-id="839b1-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-130">Required</span></span> |<span data-ttu-id="839b1-131">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-131">**xs:string**</span></span> |<span data-ttu-id="839b1-132">Nazwa pliku zasobów.</span><span class="sxs-lookup"><span data-stu-id="839b1-132">Asset file name.</span></span> |
| <span data-ttu-id="839b1-133">**Rozmiar**</span><span class="sxs-lookup"><span data-stu-id="839b1-133">**Size**</span></span><br /><br /> <span data-ttu-id="839b1-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-134">Required</span></span> |<span data-ttu-id="839b1-135">**xs:Long**</span><span class="sxs-lookup"><span data-stu-id="839b1-135">**xs:long**</span></span> |<span data-ttu-id="839b1-136">Rozmiar pliku zasobów hello w bajtach.</span><span class="sxs-lookup"><span data-stu-id="839b1-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="839b1-137">**Czas trwania**</span><span class="sxs-lookup"><span data-stu-id="839b1-137">**Duration**</span></span><br /><br /> <span data-ttu-id="839b1-138">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-138">Required</span></span> |<span data-ttu-id="839b1-139">**DURATION**</span><span class="sxs-lookup"><span data-stu-id="839b1-139">**xs:duration**</span></span> |<span data-ttu-id="839b1-140">Czas trwania wstecz odtwarzania zawartości.</span><span class="sxs-lookup"><span data-stu-id="839b1-140">Content play back duration.</span></span> <span data-ttu-id="839b1-141">Przykład: Czas trwania = "PT25M37.757S".</span><span class="sxs-lookup"><span data-stu-id="839b1-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="839b1-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="839b1-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="839b1-143">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-143">Required</span></span> |<span data-ttu-id="839b1-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-144">**xs:int**</span></span> |<span data-ttu-id="839b1-145">Liczba strumieni w pliku trwałego hello.</span><span class="sxs-lookup"><span data-stu-id="839b1-145">Number of streams in hello asset file.</span></span> |
| <span data-ttu-id="839b1-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="839b1-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="839b1-147">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-147">Required</span></span> |<span data-ttu-id="839b1-148">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-148">**xs:string**</span></span> |<span data-ttu-id="839b1-149">Format nazwy.</span><span class="sxs-lookup"><span data-stu-id="839b1-149">Format names.</span></span> |
| <span data-ttu-id="839b1-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="839b1-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="839b1-151">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-151">Required</span></span> |<span data-ttu-id="839b1-152">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-152">**xs:string**</span></span> |<span data-ttu-id="839b1-153">Pełne nazwy formatu.</span><span class="sxs-lookup"><span data-stu-id="839b1-153">Format verbose names.</span></span> |
| <span data-ttu-id="839b1-154">**Czas rozpoczęcia**</span><span class="sxs-lookup"><span data-stu-id="839b1-154">**StartTime**</span></span> |<span data-ttu-id="839b1-155">**DURATION**</span><span class="sxs-lookup"><span data-stu-id="839b1-155">**xs:duration**</span></span> |<span data-ttu-id="839b1-156">Godzina rozpoczęcia zawartości.</span><span class="sxs-lookup"><span data-stu-id="839b1-156">Content start time.</span></span> <span data-ttu-id="839b1-157">Przykład: Wartość StartTime = "PT2.669S".</span><span class="sxs-lookup"><span data-stu-id="839b1-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="839b1-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="839b1-158">**OverallBitRate**</span></span> |<span data-ttu-id="839b1-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-159">**xs:int**</span></span> |<span data-ttu-id="839b1-160">Średnia szybkość transmisji bitów pliku zasobów hello w KB/s.</span><span class="sxs-lookup"><span data-stu-id="839b1-160">Average bitrate of hello asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="839b1-161">Witaj następujące 4 elementy podrzędne muszą być umieszczone w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="839b1-161">hello following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="839b1-162">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="839b1-162">Child elements</span></span>
| <span data-ttu-id="839b1-163">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-163">Name</span></span> | <span data-ttu-id="839b1-164">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-164">Type</span></span> | <span data-ttu-id="839b1-165">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-166">**Programy**</span><span class="sxs-lookup"><span data-stu-id="839b1-166">**Programs**</span></span><br /><br /> <span data-ttu-id="839b1-167">minOccurs = "0"</span><span class="sxs-lookup"><span data-stu-id="839b1-167">minOccurs="0"</span></span> | |<span data-ttu-id="839b1-168">Kolekcja wszystkich [element programy](media-services-input-metadata-schema.md#Programs) gdy plik zasobów hello jest w formacie MPEG-TS.</span><span class="sxs-lookup"><span data-stu-id="839b1-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when hello asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="839b1-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="839b1-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="839b1-170">minOccurs = "0"</span><span class="sxs-lookup"><span data-stu-id="839b1-170">minOccurs="0"</span></span> | |<span data-ttu-id="839b1-171">Każdy plik zasobów fizycznych może zawierać zero lub więcej ścieżek wideo przeplatana do formatu odpowiedniego kontenera.</span><span class="sxs-lookup"><span data-stu-id="839b1-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="839b1-172">Ten element zawiera zbiór wszystkich [elementu VideoTracks](media-services-input-metadata-schema.md#VideoTracks) będących częścią hello pliku zasobów.</span><span class="sxs-lookup"><span data-stu-id="839b1-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="839b1-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="839b1-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="839b1-174">minOccurs = "0"</span><span class="sxs-lookup"><span data-stu-id="839b1-174">minOccurs="0"</span></span> | |<span data-ttu-id="839b1-175">Każdy plik zasobów fizycznych może zawierać zero lub więcej ścieżek audio przeplatana do formatu odpowiedniego kontenera.</span><span class="sxs-lookup"><span data-stu-id="839b1-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="839b1-176">Ten element zawiera zbiór wszystkich [elementu AudioTracks](media-services-input-metadata-schema.md#AudioTracks) będących częścią hello pliku zasobów.</span><span class="sxs-lookup"><span data-stu-id="839b1-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="839b1-177">**Metadane**</span><span class="sxs-lookup"><span data-stu-id="839b1-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="839b1-178">minOccurs = maxOccurs "0" = "unbounded"</span><span class="sxs-lookup"><span data-stu-id="839b1-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="839b1-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="839b1-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="839b1-180">Reprezentowane jako ciągi key\value metadanych pliku zasobów.</span><span class="sxs-lookup"><span data-stu-id="839b1-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="839b1-181">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="839b1-181">For example:</span></span><br /><br /> <span data-ttu-id="839b1-182">**&lt;Metadane klucz = wartość "język" = "eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="839b1-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="839b1-183"><a name="TrackType"></a>TrackType</span><span class="sxs-lookup"><span data-stu-id="839b1-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="839b1-184">Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="839b1-184">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="839b1-185">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="839b1-185">Attributes</span></span>
| <span data-ttu-id="839b1-186">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-186">Name</span></span> | <span data-ttu-id="839b1-187">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-187">Type</span></span> | <span data-ttu-id="839b1-188">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-189">**Identyfikator**</span><span class="sxs-lookup"><span data-stu-id="839b1-189">**Id**</span></span><br /><br /> <span data-ttu-id="839b1-190">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-190">Required</span></span> |<span data-ttu-id="839b1-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-191">**xs:int**</span></span> |<span data-ttu-id="839b1-192">Liczony od zera indeks tej ścieżki audio i wideo.</span><span class="sxs-lookup"><span data-stu-id="839b1-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="839b1-193">Nie jest tym hello TrackID w pliku MP4.</span><span class="sxs-lookup"><span data-stu-id="839b1-193">This is not necessarily that hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="839b1-194">**Koder-dekoder**</span><span class="sxs-lookup"><span data-stu-id="839b1-194">**Codec**</span></span> |<span data-ttu-id="839b1-195">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-195">**xs:string**</span></span> |<span data-ttu-id="839b1-196">Parametry kodera-dekodera wideo Śledź.</span><span class="sxs-lookup"><span data-stu-id="839b1-196">Video track codec string.</span></span> |
| <span data-ttu-id="839b1-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="839b1-197">**CodecLongName**</span></span> |<span data-ttu-id="839b1-198">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-198">**xs:string**</span></span> |<span data-ttu-id="839b1-199">Śledź audio i wideo koder-dekoder długa nazwa.</span><span class="sxs-lookup"><span data-stu-id="839b1-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="839b1-200">**Podstawy czasu**</span><span class="sxs-lookup"><span data-stu-id="839b1-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="839b1-201">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-201">Required</span></span> |<span data-ttu-id="839b1-202">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-202">**xs:string**</span></span> |<span data-ttu-id="839b1-203">Podstawa czasu.</span><span class="sxs-lookup"><span data-stu-id="839b1-203">Time base.</span></span> <span data-ttu-id="839b1-204">Przykład: Podstawy czasu = "1/48000"</span><span class="sxs-lookup"><span data-stu-id="839b1-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="839b1-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="839b1-205">**NumberOfFrames**</span></span> |<span data-ttu-id="839b1-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-206">**xs:int**</span></span> |<span data-ttu-id="839b1-207">Liczba ramek (istnieje dla ścieżki wideo).</span><span class="sxs-lookup"><span data-stu-id="839b1-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="839b1-208">**Czas rozpoczęcia**</span><span class="sxs-lookup"><span data-stu-id="839b1-208">**StartTime**</span></span> |<span data-ttu-id="839b1-209">**DURATION**</span><span class="sxs-lookup"><span data-stu-id="839b1-209">**xs:duration**</span></span> |<span data-ttu-id="839b1-210">Godzina rozpoczęcia śledzenia.</span><span class="sxs-lookup"><span data-stu-id="839b1-210">Track start time.</span></span> <span data-ttu-id="839b1-211">Przykład: Wartość StartTime = "PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="839b1-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="839b1-212">**Czas trwania**</span><span class="sxs-lookup"><span data-stu-id="839b1-212">**Duration**</span></span> |<span data-ttu-id="839b1-213">**DURATION**</span><span class="sxs-lookup"><span data-stu-id="839b1-213">**xs:duration**</span></span> |<span data-ttu-id="839b1-214">Śledzenie czasu trwania.</span><span class="sxs-lookup"><span data-stu-id="839b1-214">Track duration.</span></span> <span data-ttu-id="839b1-215">Przykład: Czas trwania = "PTSampleFormat M37.757S".</span><span class="sxs-lookup"><span data-stu-id="839b1-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="839b1-216">powitania po 2 elementy podrzędne muszą być umieszczone w sekwencji.</span><span class="sxs-lookup"><span data-stu-id="839b1-216">hello following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="839b1-217">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="839b1-217">Child elements</span></span>
| <span data-ttu-id="839b1-218">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-218">Name</span></span> | <span data-ttu-id="839b1-219">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-219">Type</span></span> | <span data-ttu-id="839b1-220">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-221">**Dyspozycji**</span><span class="sxs-lookup"><span data-stu-id="839b1-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="839b1-222">minOccurs = maxOccurs "0" = "1"</span><span class="sxs-lookup"><span data-stu-id="839b1-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="839b1-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="839b1-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="839b1-224">Zawiera informacje o prezentacji (na przykład czy określonej ścieżki audio jest dla osób niedowidzących).</span><span class="sxs-lookup"><span data-stu-id="839b1-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="839b1-225">**Metadane**</span><span class="sxs-lookup"><span data-stu-id="839b1-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="839b1-226">minOccurs = maxOccurs "0" = "unbounded"</span><span class="sxs-lookup"><span data-stu-id="839b1-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="839b1-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="839b1-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="839b1-228">Ciągi ogólnego klucza i wartości, które mogą być używane toohold różne informacje.</span><span class="sxs-lookup"><span data-stu-id="839b1-228">Generic key/value strings that can be used toohold a variety of information.</span></span> <span data-ttu-id="839b1-229">Na przykład klucz = "język", a wartość = "eng".</span><span class="sxs-lookup"><span data-stu-id="839b1-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="839b1-230"><a name="AudioTrackType"></a>AudioTrackType (dziedziczy TrackType)</span><span class="sxs-lookup"><span data-stu-id="839b1-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="839b1-231">**AudioTrackType** jest typem złożonym globalny, który dziedziczy z [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="839b1-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="839b1-232">Typ Hello reprezentuje określonej ścieżki audio w pliku trwałego hello.</span><span class="sxs-lookup"><span data-stu-id="839b1-232">hello type represents a specific audio track in hello asset file.</span></span>  

 <span data-ttu-id="839b1-233">Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="839b1-233">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="839b1-234">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="839b1-234">Attributes</span></span>
| <span data-ttu-id="839b1-235">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-235">Name</span></span> | <span data-ttu-id="839b1-236">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-236">Type</span></span> | <span data-ttu-id="839b1-237">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="839b1-238">**SampleFormat**</span></span> |<span data-ttu-id="839b1-239">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-239">**xs:string**</span></span> |<span data-ttu-id="839b1-240">Przykładowy format.</span><span class="sxs-lookup"><span data-stu-id="839b1-240">Sample format.</span></span> |
| <span data-ttu-id="839b1-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="839b1-241">**ChannelLayout**</span></span> |<span data-ttu-id="839b1-242">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-242">**xs:string**</span></span> |<span data-ttu-id="839b1-243">Układ kanału.</span><span class="sxs-lookup"><span data-stu-id="839b1-243">Channel layout.</span></span> |
| <span data-ttu-id="839b1-244">**Kanały**</span><span class="sxs-lookup"><span data-stu-id="839b1-244">**Channels**</span></span><br /><br /> <span data-ttu-id="839b1-245">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-245">Required</span></span> |<span data-ttu-id="839b1-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-246">**xs:int**</span></span> |<span data-ttu-id="839b1-247">Liczba (0 lub więcej) audio kanałów.</span><span class="sxs-lookup"><span data-stu-id="839b1-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="839b1-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="839b1-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="839b1-249">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-249">Required</span></span> |<span data-ttu-id="839b1-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-250">**xs:int**</span></span> |<span data-ttu-id="839b1-251">Częstotliwość próbkowania audio w próbek na sekundę lub Hz.</span><span class="sxs-lookup"><span data-stu-id="839b1-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="839b1-252">**Szybkość transmisji bitów**</span><span class="sxs-lookup"><span data-stu-id="839b1-252">**Bitrate**</span></span> |<span data-ttu-id="839b1-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-253">**xs:int**</span></span> |<span data-ttu-id="839b1-254">Średnia audio szybkość transmisji bitów w bitów na sekundę, obliczoną z hello pliku zasobów.</span><span class="sxs-lookup"><span data-stu-id="839b1-254">Average audio bit rate in bits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="839b1-255">Tylko hello podstawowe strumienia ładunku jest liczony i koszty pakietów hello jest niedostępna w tej liczby.</span><span class="sxs-lookup"><span data-stu-id="839b1-255">Only hello elementary stream payload is counted, and hello packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="839b1-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="839b1-256">**BitsPerSample**</span></span> |<span data-ttu-id="839b1-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-257">**xs:int**</span></span> |<span data-ttu-id="839b1-258">Wpisz bitów na próbkę hello wFormatTag formatu.</span><span class="sxs-lookup"><span data-stu-id="839b1-258">Bits per sample for hello wFormatTag format type.</span></span> |

## <span data-ttu-id="839b1-259"><a name="VideoTrackType"></a>VideoTrackType (dziedziczy TrackType)</span><span class="sxs-lookup"><span data-stu-id="839b1-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="839b1-260">**VideoTrackType** jest typem złożonym globalny, który dziedziczy z [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="839b1-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="839b1-261">Typ Hello reprezentuje określonej ścieżki wideo w pliku trwałego hello.</span><span class="sxs-lookup"><span data-stu-id="839b1-261">hello type represents a specific video track in hello asset file.</span></span>  

<span data-ttu-id="839b1-262">Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="839b1-262">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="839b1-263">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="839b1-263">Attributes</span></span>
| <span data-ttu-id="839b1-264">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-264">Name</span></span> | <span data-ttu-id="839b1-265">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-265">Type</span></span> | <span data-ttu-id="839b1-266">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="839b1-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="839b1-268">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-268">Required</span></span> |<span data-ttu-id="839b1-269">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-269">**xs:string**</span></span> |<span data-ttu-id="839b1-270">Kodera-dekodera wideo FourCC kodu.</span><span class="sxs-lookup"><span data-stu-id="839b1-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="839b1-271">**Profil**</span><span class="sxs-lookup"><span data-stu-id="839b1-271">**Profile**</span></span> |<span data-ttu-id="839b1-272">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-272">**xs:string**</span></span> |<span data-ttu-id="839b1-273">Ścieżka wideo profil.</span><span class="sxs-lookup"><span data-stu-id="839b1-273">Video track's profile.</span></span> |
| <span data-ttu-id="839b1-274">**Poziom**</span><span class="sxs-lookup"><span data-stu-id="839b1-274">**Level**</span></span> |<span data-ttu-id="839b1-275">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-275">**xs:string**</span></span> |<span data-ttu-id="839b1-276">Poziom śledzenia wideo.</span><span class="sxs-lookup"><span data-stu-id="839b1-276">Video track's level.</span></span> |
| <span data-ttu-id="839b1-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="839b1-277">**PixelFormat**</span></span> |<span data-ttu-id="839b1-278">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-278">**xs:string**</span></span> |<span data-ttu-id="839b1-279">Ścieżka wideo format piksela.</span><span class="sxs-lookup"><span data-stu-id="839b1-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="839b1-280">**Szerokość**</span><span class="sxs-lookup"><span data-stu-id="839b1-280">**Width**</span></span><br /><br /> <span data-ttu-id="839b1-281">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-281">Required</span></span> |<span data-ttu-id="839b1-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-282">**xs:int**</span></span> |<span data-ttu-id="839b1-283">Zakodowany szerokości wideo w pikselach.</span><span class="sxs-lookup"><span data-stu-id="839b1-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="839b1-284">**Wysokość**</span><span class="sxs-lookup"><span data-stu-id="839b1-284">**Height**</span></span><br /><br /> <span data-ttu-id="839b1-285">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-285">Required</span></span> |<span data-ttu-id="839b1-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-286">**xs:int**</span></span> |<span data-ttu-id="839b1-287">Zakodowany wideo wysokość w pikselach.</span><span class="sxs-lookup"><span data-stu-id="839b1-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="839b1-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="839b1-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="839b1-289">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-289">Required</span></span> |<span data-ttu-id="839b1-290">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="839b1-290">**xs:double**</span></span> |<span data-ttu-id="839b1-291">Licznik współczynnik proporcji wideo.</span><span class="sxs-lookup"><span data-stu-id="839b1-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="839b1-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="839b1-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="839b1-293">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-293">Required</span></span> |<span data-ttu-id="839b1-294">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="839b1-294">**xs:double**</span></span> |<span data-ttu-id="839b1-295">Denominator współczynnik proporcji wideo.</span><span class="sxs-lookup"><span data-stu-id="839b1-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="839b1-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="839b1-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="839b1-297">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-297">Required</span></span> |<span data-ttu-id="839b1-298">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="839b1-298">**xs:double**</span></span> |<span data-ttu-id="839b1-299">Przykładowe wideo licznik współczynnik proporcji.</span><span class="sxs-lookup"><span data-stu-id="839b1-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="839b1-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="839b1-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="839b1-301">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="839b1-301">**xs:double**</span></span> |<span data-ttu-id="839b1-302">Przykładowe wideo licznik współczynnik proporcji.</span><span class="sxs-lookup"><span data-stu-id="839b1-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="839b1-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="839b1-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="839b1-304">**xs:Double**</span><span class="sxs-lookup"><span data-stu-id="839b1-304">**xs:double**</span></span> |<span data-ttu-id="839b1-305">Denominator współczynnik proporcji próbki wideo.</span><span class="sxs-lookup"><span data-stu-id="839b1-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="839b1-306">**Szybkość klatek**</span><span class="sxs-lookup"><span data-stu-id="839b1-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="839b1-307">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-307">Required</span></span> |<span data-ttu-id="839b1-308">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="839b1-308">**xs:decimal**</span></span> |<span data-ttu-id="839b1-309">Mierzy szybkość odtwarzania wideo w formacie .3f.</span><span class="sxs-lookup"><span data-stu-id="839b1-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="839b1-310">**Szybkość transmisji bitów**</span><span class="sxs-lookup"><span data-stu-id="839b1-310">**Bitrate**</span></span> |<span data-ttu-id="839b1-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-311">**xs:int**</span></span> |<span data-ttu-id="839b1-312">Średnia wideo szybkość transmisji bitów w kilobitów na sekundę, obliczoną z hello pliku zasobów.</span><span class="sxs-lookup"><span data-stu-id="839b1-312">Average video bit rate in kilobits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="839b1-313">Tylko hello podstawowe strumienia ładunku jest liczony i koszty pakietów hello nie jest dołączony.</span><span class="sxs-lookup"><span data-stu-id="839b1-313">Only hello elementary stream payload is counted, and hello packaging overhead is not included.</span></span> |
| <span data-ttu-id="839b1-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="839b1-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="839b1-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-315">**xs:int**</span></span> |<span data-ttu-id="839b1-316">Maksymalna liczba GOP średnia szybkość transmisji bitów dla tej ścieżki wideo, w kilobitów na sekundę.</span><span class="sxs-lookup"><span data-stu-id="839b1-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="839b1-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="839b1-317">**HasBFrames**</span></span> |<span data-ttu-id="839b1-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-318">**xs:int**</span></span> |<span data-ttu-id="839b1-319">Ścieżka wideo liczbę ramek B.</span><span class="sxs-lookup"><span data-stu-id="839b1-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="839b1-320"><a name="MetadataType"></a>MetadataType</span><span class="sxs-lookup"><span data-stu-id="839b1-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="839b1-321">**MetadataType** jest typem złożonym globalne informacje metadanych z pliku zasobów jako ciągi klucza i wartości.</span><span class="sxs-lookup"><span data-stu-id="839b1-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="839b1-322">Na przykład klucz = "język", a wartość = "eng".</span><span class="sxs-lookup"><span data-stu-id="839b1-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="839b1-323">Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="839b1-323">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="839b1-324">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="839b1-324">Attributes</span></span>
| <span data-ttu-id="839b1-325">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-325">Name</span></span> | <span data-ttu-id="839b1-326">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-326">Type</span></span> | <span data-ttu-id="839b1-327">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-328">**klucz**</span><span class="sxs-lookup"><span data-stu-id="839b1-328">**key**</span></span><br /><br /> <span data-ttu-id="839b1-329">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-329">Required</span></span> |<span data-ttu-id="839b1-330">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-330">**xs:string**</span></span> |<span data-ttu-id="839b1-331">klucz Hello hello pary klucz wartość.</span><span class="sxs-lookup"><span data-stu-id="839b1-331">hello key in hello key/value pair.</span></span> |
| <span data-ttu-id="839b1-332">**wartość**</span><span class="sxs-lookup"><span data-stu-id="839b1-332">**value**</span></span><br /><br /> <span data-ttu-id="839b1-333">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-333">Required</span></span> |<span data-ttu-id="839b1-334">**xs:String**</span><span class="sxs-lookup"><span data-stu-id="839b1-334">**xs:string**</span></span> |<span data-ttu-id="839b1-335">wartość Hello hello pary klucza/wartości.</span><span class="sxs-lookup"><span data-stu-id="839b1-335">hello value in hello key/value pair.</span></span> |

## <span data-ttu-id="839b1-336"><a name="ProgramType"></a>ProgramType</span><span class="sxs-lookup"><span data-stu-id="839b1-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="839b1-337">**ProgramType** jest typem złożonym globalnego zawiera opis programu.</span><span class="sxs-lookup"><span data-stu-id="839b1-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="839b1-338">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="839b1-338">Attributes</span></span>
| <span data-ttu-id="839b1-339">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-339">Name</span></span> | <span data-ttu-id="839b1-340">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-340">Type</span></span> | <span data-ttu-id="839b1-341">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="839b1-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="839b1-343">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-343">Required</span></span> |<span data-ttu-id="839b1-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-344">**xs:int**</span></span> |<span data-ttu-id="839b1-345">Identyfikator programu</span><span class="sxs-lookup"><span data-stu-id="839b1-345">Program Id</span></span> |
| <span data-ttu-id="839b1-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="839b1-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="839b1-347">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-347">Required</span></span> |<span data-ttu-id="839b1-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-348">**xs:int**</span></span> |<span data-ttu-id="839b1-349">Liczba programów.</span><span class="sxs-lookup"><span data-stu-id="839b1-349">Number of programs.</span></span> |
| <span data-ttu-id="839b1-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="839b1-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="839b1-351">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-351">Required</span></span> |<span data-ttu-id="839b1-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-352">**xs:int**</span></span> |<span data-ttu-id="839b1-353">Program mapy tabele (PMTs) zawierają informacje o programach.</span><span class="sxs-lookup"><span data-stu-id="839b1-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="839b1-354">Aby uzyskać więcej informacji, zobacz [rata](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="839b1-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="839b1-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="839b1-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="839b1-356">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-356">Required</span></span> |<span data-ttu-id="839b1-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-357">**xs:int**</span></span> |<span data-ttu-id="839b1-358">Używany przez dekodera.</span><span class="sxs-lookup"><span data-stu-id="839b1-358">Used by decoder.</span></span> <span data-ttu-id="839b1-359">Aby uzyskać więcej informacji, zobacz [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span><span class="sxs-lookup"><span data-stu-id="839b1-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="839b1-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="839b1-360">**StartPTS**</span></span> |<span data-ttu-id="839b1-361">**xs: długa**</span><span class="sxs-lookup"><span data-stu-id="839b1-361">**xs: long**</span></span> |<span data-ttu-id="839b1-362">Sygnatura czasowa rozpoczęcia prezentacji.</span><span class="sxs-lookup"><span data-stu-id="839b1-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="839b1-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="839b1-363">**EndPTS**</span></span> |<span data-ttu-id="839b1-364">**xs: długa**</span><span class="sxs-lookup"><span data-stu-id="839b1-364">**xs: long**</span></span> |<span data-ttu-id="839b1-365">Końcowa sygnatura czasowa prezentacji.</span><span class="sxs-lookup"><span data-stu-id="839b1-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="839b1-366"><a name="StreamDispositionType"></a>StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="839b1-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="839b1-367">**StreamDispositionType** jest typem złożonym globalne opisuje hello strumienia.</span><span class="sxs-lookup"><span data-stu-id="839b1-367">**StreamDispositionType** is a global complex type that describes hello stream.</span></span>  

<span data-ttu-id="839b1-368">Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="839b1-368">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="839b1-369">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="839b1-369">Attributes</span></span>
| <span data-ttu-id="839b1-370">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-370">Name</span></span> | <span data-ttu-id="839b1-371">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-371">Type</span></span> | <span data-ttu-id="839b1-372">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-373">**Domyślne**</span><span class="sxs-lookup"><span data-stu-id="839b1-373">**Default**</span></span><br /><br /> <span data-ttu-id="839b1-374">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-374">Required</span></span> |<span data-ttu-id="839b1-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-375">**xs:int**</span></span> |<span data-ttu-id="839b1-376">Ustawienie tego atrybutu tooindicate too1, to hello domyślne prezentacji.</span><span class="sxs-lookup"><span data-stu-id="839b1-376">Set this attribute too1 tooindicate this is hello default presentation.</span></span> |
| <span data-ttu-id="839b1-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="839b1-377">**Dub**</span></span><br /><br /> <span data-ttu-id="839b1-378">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-378">Required</span></span> |<span data-ttu-id="839b1-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-379">**xs:int**</span></span> |<span data-ttu-id="839b1-380">Ustaw ten atrybut too1 tooindicate jest hello dubbingu prezentacji.</span><span class="sxs-lookup"><span data-stu-id="839b1-380">Set this attribute too1 tooindicate this is hello dubbed presentation.</span></span> |
| <span data-ttu-id="839b1-381">**Oryginał**</span><span class="sxs-lookup"><span data-stu-id="839b1-381">**Original**</span></span><br /><br /> <span data-ttu-id="839b1-382">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-382">Required</span></span> |<span data-ttu-id="839b1-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-383">**xs:int**</span></span> |<span data-ttu-id="839b1-384">Ustaw ten atrybut tooindicate too1, jest to hello oryginalnej prezentacji.</span><span class="sxs-lookup"><span data-stu-id="839b1-384">Set this attribute too1 tooindicate this is hello original presentation.</span></span> |
| <span data-ttu-id="839b1-385">**Komentarz**</span><span class="sxs-lookup"><span data-stu-id="839b1-385">**Comment**</span></span><br /><br /> <span data-ttu-id="839b1-386">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-386">Required</span></span> |<span data-ttu-id="839b1-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-387">**xs:int**</span></span> |<span data-ttu-id="839b1-388">Ustaw ten atrybut too1 tooindicate Śledź zawiera komentarz.</span><span class="sxs-lookup"><span data-stu-id="839b1-388">Set this attribute too1 tooindicate this track contains commentary.</span></span> |
| <span data-ttu-id="839b1-389">**Tekst**</span><span class="sxs-lookup"><span data-stu-id="839b1-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="839b1-390">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-390">Required</span></span> |<span data-ttu-id="839b1-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-391">**xs:int**</span></span> |<span data-ttu-id="839b1-392">Ustaw ten atrybut too1 tooindicate Śledź zawiera tekst.</span><span class="sxs-lookup"><span data-stu-id="839b1-392">Set this attribute too1 tooindicate this track contains lyrics.</span></span> |
| <span data-ttu-id="839b1-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="839b1-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="839b1-394">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-394">Required</span></span> |<span data-ttu-id="839b1-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-395">**xs:int**</span></span> |<span data-ttu-id="839b1-396">Ustaw tooindicate too1 ten atrybut reprezentuje hello Śledź karaoke (muzyką w tle, nie vocals).</span><span class="sxs-lookup"><span data-stu-id="839b1-396">Set this attribute too1 tooindicate this represents hello karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="839b1-397">**Wymuszone**</span><span class="sxs-lookup"><span data-stu-id="839b1-397">**Forced**</span></span><br /><br /> <span data-ttu-id="839b1-398">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-398">Required</span></span> |<span data-ttu-id="839b1-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-399">**xs:int**</span></span> |<span data-ttu-id="839b1-400">Ustawienie tego atrybutu tooindicate too1, to hello wymuszone prezentacji.</span><span class="sxs-lookup"><span data-stu-id="839b1-400">Set this attribute too1 tooindicate this is hello forced presentation.</span></span> |
| <span data-ttu-id="839b1-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="839b1-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="839b1-402">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-402">Required</span></span> |<span data-ttu-id="839b1-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-403">**xs:int**</span></span> |<span data-ttu-id="839b1-404">Ustaw tooindicate too1 ten atrybut, którego hello niesłyszący tej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="839b1-404">Set this attribute too1 tooindicate this track is for hello hearing impaired.</span></span> |
| <span data-ttu-id="839b1-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="839b1-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="839b1-406">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-406">Required</span></span> |<span data-ttu-id="839b1-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-407">**xs:int**</span></span> |<span data-ttu-id="839b1-408">Ustaw ten atrybut tooindicate too1, Śledź ten jest przeznaczony dla osób niedowidzących hello.</span><span class="sxs-lookup"><span data-stu-id="839b1-408">Set this attribute too1 tooindicate this track is for hello visually impaired.</span></span> |
| <span data-ttu-id="839b1-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="839b1-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="839b1-410">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-410">Required</span></span> |<span data-ttu-id="839b1-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-411">**xs:int**</span></span> |<span data-ttu-id="839b1-412">Ustaw tooindicate too1 tego atrybutu, ta ścieżka ma efekty czyste.</span><span class="sxs-lookup"><span data-stu-id="839b1-412">Set this attribute too1 tooindicate this track has clean effects.</span></span> |
| <span data-ttu-id="839b1-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="839b1-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="839b1-414">Wymagane</span><span class="sxs-lookup"><span data-stu-id="839b1-414">Required</span></span> |<span data-ttu-id="839b1-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="839b1-415">**xs:int**</span></span> |<span data-ttu-id="839b1-416">Ustawienie tego atrybutu tooindicate too1, ta ścieżka ma obrazów.</span><span class="sxs-lookup"><span data-stu-id="839b1-416">Set this attribute too1 tooindicate this track has pictures.</span></span> |

## <span data-ttu-id="839b1-417"><a name="Programs"></a>Element programy</span><span class="sxs-lookup"><span data-stu-id="839b1-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="839b1-418">Element otoki zawierający wiele **Program** elementów.</span><span class="sxs-lookup"><span data-stu-id="839b1-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="839b1-419">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="839b1-419">Child elements</span></span>
| <span data-ttu-id="839b1-420">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-420">Name</span></span> | <span data-ttu-id="839b1-421">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-421">Type</span></span> | <span data-ttu-id="839b1-422">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-423">**Program**</span><span class="sxs-lookup"><span data-stu-id="839b1-423">**Program**</span></span><br /><br /> <span data-ttu-id="839b1-424">minOccurs = maxOccurs "0" = "unbounded"</span><span class="sxs-lookup"><span data-stu-id="839b1-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="839b1-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="839b1-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="839b1-426">Dla plików zasobów, które są w formacie MPEG-TS zawiera informacje dotyczące programów w pliku trwałego hello.</span><span class="sxs-lookup"><span data-stu-id="839b1-426">For asset files that are in MPEG-TS format, contains information about programs in hello asset file.</span></span> |

## <span data-ttu-id="839b1-427"><a name="VideoTracks"></a>VideoTracks element</span><span class="sxs-lookup"><span data-stu-id="839b1-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="839b1-428">Element otoki zawierający wiele **VideoTrack** elementów.</span><span class="sxs-lookup"><span data-stu-id="839b1-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="839b1-429">Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="839b1-429">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="839b1-430">Elementy podrzędne</span><span class="sxs-lookup"><span data-stu-id="839b1-430">Child elements</span></span>
| <span data-ttu-id="839b1-431">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-431">Name</span></span> | <span data-ttu-id="839b1-432">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-432">Type</span></span> | <span data-ttu-id="839b1-433">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="839b1-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="839b1-435">minOccurs = maxOccurs "0" = "unbounded"</span><span class="sxs-lookup"><span data-stu-id="839b1-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="839b1-436">VideoTrackType (dziedziczy TrackType)</span><span class="sxs-lookup"><span data-stu-id="839b1-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="839b1-437">Zawiera informacje dotyczące ścieżki wideo w pliku trwałego hello.</span><span class="sxs-lookup"><span data-stu-id="839b1-437">Contains information about video tracks in hello asset file.</span></span> |

## <span data-ttu-id="839b1-438"><a name="AudioTracks"></a>AudioTracks element</span><span class="sxs-lookup"><span data-stu-id="839b1-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="839b1-439">Element otoki zawierający wiele **AudioTrack** elementów.</span><span class="sxs-lookup"><span data-stu-id="839b1-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="839b1-440">Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="839b1-440">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="839b1-441">Elementy</span><span class="sxs-lookup"><span data-stu-id="839b1-441">elements</span></span>
| <span data-ttu-id="839b1-442">Nazwa</span><span class="sxs-lookup"><span data-stu-id="839b1-442">Name</span></span> | <span data-ttu-id="839b1-443">Typ</span><span class="sxs-lookup"><span data-stu-id="839b1-443">Type</span></span> | <span data-ttu-id="839b1-444">Opis</span><span class="sxs-lookup"><span data-stu-id="839b1-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="839b1-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="839b1-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="839b1-446">minOccurs = maxOccurs "0" = "unbounded"</span><span class="sxs-lookup"><span data-stu-id="839b1-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="839b1-447">AudioTrackType (dziedziczy TrackType)</span><span class="sxs-lookup"><span data-stu-id="839b1-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="839b1-448">Zawiera informacje dotyczące ścieżki audio w pliku trwałego hello.</span><span class="sxs-lookup"><span data-stu-id="839b1-448">Contains information about audio tracks in hello asset file.</span></span> |

## <span data-ttu-id="839b1-449"><a name="code"></a>Kod schematu</span><span class="sxs-lookup"><span data-stu-id="839b1-449"><a name="code"></a> Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <span data-ttu-id="839b1-450"><a name="xml"></a>Przykład pliku XML</span><span class="sxs-lookup"><span data-stu-id="839b1-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="839b1-451">Hello poniżej znajduje się przykład pliku metadanych hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="839b1-451">hello following is an example of hello Input metadata file.</span></span>  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="839b1-452">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="839b1-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="839b1-453">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="839b1-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

