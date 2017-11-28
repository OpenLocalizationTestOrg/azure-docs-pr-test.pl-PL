---
title: "aaaMedia przepływu pracy Premium kodera koderów-dekoderów i formaty | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie koderów-dekoderów i formaty Media Encoder Premium przepływu pracy formatów"
services: media-services
documentationcenter: 
author: juliako
manager: erik43
editor: 
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: e781384ca8f08926f00c83b6710fd413ce2a3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="e6e5a-103">Koderów-dekoderów i formaty Media Encoder Premium w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="e6e5a-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="e6e5a-104">Odpowiedzi na pytania koder premium poczty e-mail mepd z witryny Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="e6e5a-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="e6e5a-105">Procesor multimediów Media Encoder Premium w przepływie pracy omówione w tym temacie nie jest dostępna w Chinach.</span><span class="sxs-lookup"><span data-stu-id="e6e5a-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="e6e5a-106">Ten dokument zawiera listę formatów plików wejściowych i wyjściowych i koderów-dekoderów obsługiwanych przez wersję publicznej wersji zapoznawczej hello hello **Media Encoder Premium w przepływie pracy** kodera.</span><span class="sxs-lookup"><span data-stu-id="e6e5a-106">This document contains a list of input and output file formats and codecs that are supported by hello public preview version of hello **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="e6e5a-107">Koderów-dekoderów i formatów danych wejściowych Worflow Premium kodera multimediów</span><span class="sxs-lookup"><span data-stu-id="e6e5a-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="e6e5a-108">Koderów-dekoderów i formatów wyjściowych Worflow Premium kodera multimediów</span><span class="sxs-lookup"><span data-stu-id="e6e5a-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="e6e5a-109">**Przepływ pracy Premium kodera multimediów** obsługuje kodowane opisanego w [to](#closed_captioning) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e6e5a-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="e6e5a-110"><a id="input_formats"></a>Media Encoder Premium w przepływie pracy wprowadź koderów-dekoderów i formaty</span><span class="sxs-lookup"><span data-stu-id="e6e5a-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="e6e5a-111">powitania po sekcji list hello koderów-dekoderów i plik formatów obsługiwanych przez ten procesor multimediów jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="e6e5a-111">hello following section lists hello codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="e6e5a-112">Kontener/formatów wejściowych</span><span class="sxs-lookup"><span data-stu-id="e6e5a-112">Input Container/File Formats</span></span>
* <span data-ttu-id="e6e5a-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="e6e5a-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="e6e5a-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="e6e5a-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="e6e5a-115">GXF</span><span class="sxs-lookup"><span data-stu-id="e6e5a-115">GXF</span></span>
* <span data-ttu-id="e6e5a-116">Strumienie transportu MPEG-2</span><span class="sxs-lookup"><span data-stu-id="e6e5a-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="e6e5a-117">Strumienie programu MPEG-2</span><span class="sxs-lookup"><span data-stu-id="e6e5a-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="e6e5a-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="e6e5a-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="e6e5a-119">ASF Media systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e6e5a-119">Windows Media/ASF</span></span>
* <span data-ttu-id="e6e5a-120">AVI (nieskompresowanych 8-bitową/10 bity)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="e6e5a-121">Dane wejściowe kodery-dekodery wideo</span><span class="sxs-lookup"><span data-stu-id="e6e5a-121">Input Video Codecs</span></span>
* <span data-ttu-id="e6e5a-122">AVC 8-bitowych/10-bitowy, się too4:2:2, w tym AVCIntra</span><span class="sxs-lookup"><span data-stu-id="e6e5a-122">AVC 8-bit/10-bit, up too4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="e6e5a-123">Avid DNxHD (w MXF)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="e6e5a-124">DVCPro/DVCProHD (w MXF)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="e6e5a-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="e6e5a-125">JPEG2000</span></span>
* <span data-ttu-id="e6e5a-126">MPEG-2 (too422 profilu i wysoki poziom; tym wariantów, takich jak XDCAM, XDCAM HD, XDCAM IMX, CableLabs® i D10)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-126">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="e6e5a-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="e6e5a-127">MPEG-1</span></span>
* <span data-ttu-id="e6e5a-128">Windows Media wideo/VC-1</span><span class="sxs-lookup"><span data-stu-id="e6e5a-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="e6e5a-129">Dane wejściowe Audio koderów-dekoderów</span><span class="sxs-lookup"><span data-stu-id="e6e5a-129">Input Audio Codecs</span></span>
* <span data-ttu-id="e6e5a-130">AES (SMPTE 331 M i 302 M, AES3 2003)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="e6e5a-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="e6e5a-131">Dolby® E</span></span>
* <span data-ttu-id="e6e5a-132">Dolby® cyfrowy (AC3)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="e6e5a-133">AAC (AAC-LC, AAC HE i AAC-HEv2; zapasowej too5.1)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="e6e5a-134">MPEG warstwy 2</span><span class="sxs-lookup"><span data-stu-id="e6e5a-134">MPEG Layer 2</span></span>
* <span data-ttu-id="e6e5a-135">Mp3 (MPEG-1 Audio warstwy 3)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="e6e5a-136">Program Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="e6e5a-136">Windows Media Audio</span></span>
* <span data-ttu-id="e6e5a-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="e6e5a-137">WAV/PCM</span></span>

## <span data-ttu-id="e6e5a-138"><a id="output_format"></a>Koderów-dekoderów i formatów wyjściowych Media Encoder Premium przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="e6e5a-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="e6e5a-139">Witaj poniższej sekcji przedstawiono formatów koderów-dekoderów i plik hello, które są obsługiwane jako dane wyjściowe z tego nośnika procesora.</span><span class="sxs-lookup"><span data-stu-id="e6e5a-139">hello following section lists hello codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="e6e5a-140">Kontener i plik formatów</span><span class="sxs-lookup"><span data-stu-id="e6e5a-140">Output Container/File Formats</span></span>
* <span data-ttu-id="e6e5a-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="e6e5a-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="e6e5a-142">MXF (OP1a, XDCAM i AS02)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="e6e5a-143">DPP (w tym AS11)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-143">DPP (including AS11)</span></span>
* <span data-ttu-id="e6e5a-144">GXF</span><span class="sxs-lookup"><span data-stu-id="e6e5a-144">GXF</span></span>
* <span data-ttu-id="e6e5a-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="e6e5a-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="e6e5a-146">ASF Media systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e6e5a-146">Windows Media/ASF</span></span>
* <span data-ttu-id="e6e5a-147">AVI (nieskompresowanych 8-bitową/10 bity)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="e6e5a-148">Płynnego przesyłania strumieniowego Format pliku (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="e6e5a-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="e6e5a-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="e6e5a-150">Dane wyjściowe kodery-dekodery wideo</span><span class="sxs-lookup"><span data-stu-id="e6e5a-150">Output Video Codecs</span></span>
* <span data-ttu-id="e6e5a-151">AVC (H.264; 8-bitową w górę tooHigh profilu, poziom 5.2; HD bardzo 4K; Wewnątrz AVC)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-151">AVC (H.264; 8-bit; up tooHigh Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="e6e5a-152">Avid DNxHD (w MXF)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="e6e5a-153">DVCPro/DVCProHD (w MXF)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="e6e5a-154">MPEG-2 (too422 profilu i wysoki poziom; tym wariantów, takich jak XDCAM, XDCAM HD, XDCAM IMX, CableLabs® i D10)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-154">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="e6e5a-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="e6e5a-155">MPEG-1</span></span>
* <span data-ttu-id="e6e5a-156">Windows Media wideo/VC-1</span><span class="sxs-lookup"><span data-stu-id="e6e5a-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="e6e5a-157">Tworzenie miniatur JPEG</span><span class="sxs-lookup"><span data-stu-id="e6e5a-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="e6e5a-158">Dane wyjściowe Audio koderów-dekoderów</span><span class="sxs-lookup"><span data-stu-id="e6e5a-158">Output Audio Codecs</span></span>
* <span data-ttu-id="e6e5a-159">AES (SMPTE 331 M i 302 M, AES3 2003)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="e6e5a-160">Dolby® cyfrowy (AC3)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="e6e5a-161">Dolby® Digital Plus (E-AC3) się too7.1</span><span class="sxs-lookup"><span data-stu-id="e6e5a-161">Dolby® Digital Plus (E-AC3) up too7.1</span></span>
* <span data-ttu-id="e6e5a-162">AAC (AAC-LC, AAC HE i AAC-HEv2; zapasowej too5.1)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="e6e5a-163">MPEG warstwy 2</span><span class="sxs-lookup"><span data-stu-id="e6e5a-163">MPEG Layer 2</span></span>
* <span data-ttu-id="e6e5a-164">Mp3 (MPEG-1 Audio warstwy 3)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="e6e5a-165">Program Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="e6e5a-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="e6e5a-166">Jeśli kodowanie tooDolby® cyfrowy (AC3), dane wyjściowe hello można zapisywać tylko do pliku ISO MP4.</span><span class="sxs-lookup"><span data-stu-id="e6e5a-166">If you encode tooDolby® Digital (AC3), hello output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="e6e5a-167"><a id="closed_captioning"></a>Obsługa kodowane</span><span class="sxs-lookup"><span data-stu-id="e6e5a-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="e6e5a-168">Na pozyskiwania, **Media Encoder Premium w przepływie pracy** obsługuje:</span><span class="sxs-lookup"><span data-stu-id="e6e5a-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="e6e5a-169">Pliki SCC</span><span class="sxs-lookup"><span data-stu-id="e6e5a-169">SCC files</span></span>
2. <span data-ttu-id="e6e5a-170">Pliki SMPTE TT</span><span class="sxs-lookup"><span data-stu-id="e6e5a-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="e6e5a-171">CEA-608/CEA-708 — jako dane użytkownika (SEI wiadomości H.264 podstawowe strumieni, ATSC/53, SCTE20) lub przekazane jako dodatkowe dane w plikach MXF/GXF</span><span class="sxs-lookup"><span data-stu-id="e6e5a-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="e6e5a-172">Pliki napisów STL</span><span class="sxs-lookup"><span data-stu-id="e6e5a-172">STL subtitle files</span></span>

<span data-ttu-id="e6e5a-173">W danych wyjściowych dostępne są następujące opcje hello:</span><span class="sxs-lookup"><span data-stu-id="e6e5a-173">On output, hello following options are available:</span></span>

1. <span data-ttu-id="e6e5a-174">CEA 608 tooCEA 708 tłumaczenia</span><span class="sxs-lookup"><span data-stu-id="e6e5a-174">CEA-608 tooCEA-708 translation</span></span>
2. <span data-ttu-id="e6e5a-175">Przekazuj CEA-608/CEA-708 (osadzone w wiadomości SEI strumieniami H.264 lub przekazane jako dodatkowe dane w plikach MXF)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="e6e5a-176">SCC</span><span class="sxs-lookup"><span data-stu-id="e6e5a-176">SCC</span></span>
4. <span data-ttu-id="e6e5a-177">Tekst upłynął SMPTE (ze źródła CEA 608 na SMPTE RP2052; w tym tworzenia pliku DFXP)</span><span class="sxs-lookup"><span data-stu-id="e6e5a-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="e6e5a-178">Podtytuł SRT pliku</span><span class="sxs-lookup"><span data-stu-id="e6e5a-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="e6e5a-179">DVB podtytuł strumieni</span><span class="sxs-lookup"><span data-stu-id="e6e5a-179">DVB subtitle streams</span></span>

<span data-ttu-id="e6e5a-180">Uwaga: nie wszystkie hello powyżej formatów wyjściowych są obsługiwane w celu dostarczania za pośrednictwem przesyłania strumieniowego w usłudze Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="e6e5a-180">Note: not all of hello above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="e6e5a-181">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="e6e5a-181">Known issues</span></span>
<span data-ttu-id="e6e5a-182">Jeśli wejściowy plik wideo nie zawiera kodowane, hello wyjściowe zasobów nadal będzie zawierać pusty plik TTML.</span><span class="sxs-lookup"><span data-stu-id="e6e5a-182">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="e6e5a-183">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="e6e5a-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e6e5a-184">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="e6e5a-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

