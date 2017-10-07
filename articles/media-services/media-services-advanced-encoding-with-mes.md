---
title: "Zaawansowane aaaPerform kodowanie dostosowując ustawienia rynkowej | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooperform Zaawansowane kodowanie dostosowując Media Encoder Standard ustawienia zadania."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="9819f-103">Kodowanie zaawansowane dostosowując rynkowej ustawienia</span><span class="sxs-lookup"><span data-stu-id="9819f-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="9819f-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9819f-104">Overview</span></span>

<span data-ttu-id="9819f-105">W tym temacie przedstawiono, jak ustawienia toocustomize Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="9819f-105">This topic shows how toocustomize Media Encoder Standard presets.</span></span> <span data-ttu-id="9819f-106">Witaj [kodowanie przy użyciu predefiniowanych Media Encoder Standard](media-services-custom-mes-presets-with-dotnet.md) temacie pokazano, jak toocreate .NET toouse kodowania zadań i zadań, która wykonuje to zadanie.</span><span class="sxs-lookup"><span data-stu-id="9819f-106">hello [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how toouse .NET toocreate an encoding task and a job that executes this task.</span></span> <span data-ttu-id="9819f-107">Po dostosowaniu ustawienia domyślne, podaj hello predefiniowanych toohello kodowania zadań.</span><span class="sxs-lookup"><span data-stu-id="9819f-107">Once you customize a preset, supply hello custom presets toohello encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="9819f-108">Jeśli za pomocą wstępnie ustawionych XML, upewnij się, że toopreserve hello kolejność elementów, jak pokazano poniżej pokazano XML (na przykład KeyFrameInterval należy poprzedzać SceneChangeDetection).</span><span class="sxs-lookup"><span data-stu-id="9819f-108">If using an XML preset, make sure toopreserve hello order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="9819f-109">W tym temacie przedstawiono hello predefiniowanych wykonujących hello następujące zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="9819f-109">In this topic, hello custom presets that perform hello following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="9819f-110">Obsługa względnych rozmiarów</span><span class="sxs-lookup"><span data-stu-id="9819f-110">Support for relative sizes</span></span>

<span data-ttu-id="9819f-111">Podczas generowania miniatur, nie trzeba tooalways Określ dane wyjściowe szerokość i wysokość w pikselach.</span><span class="sxs-lookup"><span data-stu-id="9819f-111">When generating thumbnails, you do not need tooalways specify output width and height in pixels.</span></span> <span data-ttu-id="9819f-112">Możesz określić je w procentach, w zakresie hello [1%,..., 100%].</span><span class="sxs-lookup"><span data-stu-id="9819f-112">You can specify them in percentages, in hello range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="9819f-113">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="9819f-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="9819f-114">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="9819f-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="9819f-115"><a id="thumbnails"></a>Generowanie miniatur</span><span class="sxs-lookup"><span data-stu-id="9819f-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="9819f-116">W tej sekcji przedstawiono sposób toocustomize ustawienie wstępne, które generuje miniatur.</span><span class="sxs-lookup"><span data-stu-id="9819f-116">This section shows how toocustomize a preset that generates thumbnails.</span></span> <span data-ttu-id="9819f-117">Hello ustawienie wstępne określonych poniżej zawiera informacje dotyczące sposobu tooencode pliku również miniatur toogenerate potrzebne informacje.</span><span class="sxs-lookup"><span data-stu-id="9819f-117">hello preset defined below contains information on how you want tooencode your file as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="9819f-118">Może mieć jedną z ustawienia rynkowej hello udokumentowane [to](media-services-mes-presets-overview.md) sekcji, a następnie dodaj kod, który generuje miniatur.</span><span class="sxs-lookup"><span data-stu-id="9819f-118">You can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="9819f-119">Witaj **SceneChangeDetection** ustawienie w hello następujące wstępnie zdefiniowane można ustawić tylko tootrue jeśli są kodowanie wideo o pojedynczej szybkości transmisji bitów tooa.</span><span class="sxs-lookup"><span data-stu-id="9819f-119">hello **SceneChangeDetection** setting in hello following preset can only be set tootrue if you are encoding tooa single  bitrate video.</span></span> <span data-ttu-id="9819f-120">Jeśli są kodowanie tooa wielokrotnej szybkości transmisji bitów wideo i ustaw **SceneChangeDetection** tootrue, koder hello zwraca błąd.</span><span class="sxs-lookup"><span data-stu-id="9819f-120">If you are encoding tooa multi-bitrate video and set **SceneChangeDetection** tootrue, hello encoder returns an error.</span></span>  
>
>

<span data-ttu-id="9819f-121">Aby uzyskać informacje o schemacie, zobacz [to](media-services-mes-schema.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="9819f-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="9819f-122">Upewnij się, że hello tooreview [zagadnienia](#considerations) sekcji.</span><span class="sxs-lookup"><span data-stu-id="9819f-122">Make sure tooreview hello [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="9819f-123"><a id="json"></a>Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="9819f-123"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <span data-ttu-id="9819f-124"><a id="xml"></a>Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="9819f-124"><a id="xml"></a>XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a><span data-ttu-id="9819f-125">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="9819f-125">Considerations</span></span>

<span data-ttu-id="9819f-126">Zastosuj Hello następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="9819f-126">hello following considerations apply:</span></span>

* <span data-ttu-id="9819f-127">Hello użycie jawnego znacznika czasu rozpoczęcia/krok/zakresu przyjęto założenie, że źródło danych wejściowych w tym hello jest co najmniej 1 minutę.</span><span class="sxs-lookup"><span data-stu-id="9819f-127">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="9819f-128">Elementy BmpImage-jpg/Png mają Start, krok i należeć do zakresu atrybutów ciąg — mogą być interpretowane jako:</span><span class="sxs-lookup"><span data-stu-id="9819f-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="9819f-129">Numer ramki, jeśli są one — nieujemne liczby całkowite, na przykład "Start": "120"</span><span class="sxs-lookup"><span data-stu-id="9819f-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="9819f-130">Względną toosource czas trwania, jeśli wyrażony jako sufiks %, na przykład "Start": "15%", lub</span><span class="sxs-lookup"><span data-stu-id="9819f-130">Relative toosource duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="9819f-131">Sygnatura czasowa Jeśli wyrażonej w postaci hh: mm:...</span><span class="sxs-lookup"><span data-stu-id="9819f-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="9819f-132">Format, na przykład "Start": "00: 01:00"</span><span class="sxs-lookup"><span data-stu-id="9819f-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="9819f-133">Można mieszać i dopasowywać notacji jako użytkownik należy.</span><span class="sxs-lookup"><span data-stu-id="9819f-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="9819f-134">Ponadto Start obsługuje makra specjalnego: {najlepszych}, który próbuje hello toodetermine pierwszej ramki "interesujące" hello zawartości Uwaga: (krok i zakres są ignorowane w przypadku rozpoczęcia ustawiono zbyt {najlepsze})</span><span class="sxs-lookup"><span data-stu-id="9819f-134">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="9819f-135">Wartości domyślne: Start: {najlepsze}</span><span class="sxs-lookup"><span data-stu-id="9819f-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="9819f-136">Format danych wyjściowych musi toobe jawnie podany dla każdego format obrazu: BmpFormat-Jpg/Png.</span><span class="sxs-lookup"><span data-stu-id="9819f-136">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="9819f-137">Jeśli jest obecny, rynkowej odpowiada JpgVideo tooJpgFormat i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="9819f-137">When present, MES matches JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="9819f-138">OutputFormat wprowadza nowe określone makro koder-dekoder obrazów: {indeks}, która wymaga toobe obecne (jeden raz i tylko jeden raz) dla formatów wyjściowych obrazu.</span><span class="sxs-lookup"><span data-stu-id="9819f-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="9819f-139"><a id="trim_video"></a>Przycinanie wideo (wycinka)</span><span class="sxs-lookup"><span data-stu-id="9819f-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="9819f-140">Tej sekcji rozmów o modyfikowaniu kodera hello ustawienia tooclip lub trim wejściowy plik wideo hello gdzie wejściowy hello jest tak zwane mezzanine pliku lub plików na żądanie.</span><span class="sxs-lookup"><span data-stu-id="9819f-140">This section talks about modifying hello encoder presets tooclip or trim hello input video where hello input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="9819f-141">Witaj kodera można również tooclip używane lub trim zasób, przechwycone lub zarchiwizowane strumienia na żywo — hello tego są one dostępne w [ten blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="9819f-141">hello encoder can also be used tooclip or trim an asset, which is captured or archived from a live stream – hello details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="9819f-142">tootrim pliki wideo, można wykonać dowolne ustawienia rynkowej hello udokumentowane [to](media-services-mes-presets-overview.md) sekcji i zmodyfikuj hello **źródeł** elementu (jak pokazano poniżej).</span><span class="sxs-lookup"><span data-stu-id="9819f-142">tootrim your videos, you can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and modify hello **Sources** element (as shown below).</span></span> <span data-ttu-id="9819f-143">wartość StartTime Hello musi toomatch hello bezwzględną znacznikami czasu hello wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="9819f-143">hello value of StartTime needs toomatch hello absolute timestamps of hello input video.</span></span> <span data-ttu-id="9819f-144">Na przykład, jeśli hello pierwszej ramki hello wejściowy plik wideo ma sygnaturę 12:00:10.000, a następnie wartość StartTime powinna być co najmniej 12:00:10.000 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9819f-144">For example, if hello first frame of hello input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="9819f-145">W poniższym przykładzie hello przyjęto założenie, że hello wejściowego pliku wideo ma sygnaturę czasową początkowego o wartości zero.</span><span class="sxs-lookup"><span data-stu-id="9819f-145">In hello example below, we assume that hello input video has a starting timestamp of zero.</span></span> <span data-ttu-id="9819f-146">**Źródeł** należy umieścić na początku hello hello ustawienie wstępne.</span><span class="sxs-lookup"><span data-stu-id="9819f-146">**Sources** should be placed at hello beginning of hello preset.</span></span>

### <span data-ttu-id="9819f-147"><a id="json"></a>Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="9819f-147"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="9819f-148">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="9819f-148">XML preset</span></span>
<span data-ttu-id="9819f-149">tootrim pliki wideo, można wykonać dowolne ustawienia rynkowej hello udokumentowane [tutaj](media-services-mes-presets-overview.md) i zmodyfikuj hello **źródeł** elementu (jak pokazano poniżej).</span><span class="sxs-lookup"><span data-stu-id="9819f-149">tootrim your videos, you can take any of hello MES presets documented [here](media-services-mes-presets-overview.md) and modify hello **Sources** element (as shown below).</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="9819f-150"><a id="overlay"></a>Utwórz nakładki</span><span class="sxs-lookup"><span data-stu-id="9819f-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="9819f-151">Witaj Media Encoder Standard umożliwia toooverlay obrazu na istniejące wideo.</span><span class="sxs-lookup"><span data-stu-id="9819f-151">hello Media Encoder Standard allows you toooverlay an image onto an existing video.</span></span> <span data-ttu-id="9819f-152">Obecnie są obsługiwane następujące formaty hello: png, jpg, gif, bmp, a.</span><span class="sxs-lookup"><span data-stu-id="9819f-152">Currently, hello following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="9819f-153">Witaj ustawienie wstępne określonych poniżej jest podstawowy przykład nakładka wideo.</span><span class="sxs-lookup"><span data-stu-id="9819f-153">hello preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="9819f-154">Ponadto toodefining istniejących plików, masz również toolet Media Services wiedzieć, plik, który w zasobów hello jest hello nakładki obrazów i plik, który jest hello źródła wideo, na który chcesz toooverlay hello obrazu.</span><span class="sxs-lookup"><span data-stu-id="9819f-154">In addition toodefining a preset file, you also have toolet Media Services know which file in hello asset is hello overlay image and which file is hello source video onto which you want toooverlay hello image.</span></span> <span data-ttu-id="9819f-155">Witaj plik wideo ma toobe hello **głównej** pliku.</span><span class="sxs-lookup"><span data-stu-id="9819f-155">hello video file has toobe hello **primary** file.</span></span>

<span data-ttu-id="9819f-156">Jeśli używasz platformy .NET, Dodaj hello następujące dwie funkcje przykład .NET toohello zdefiniowane w [to](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tematu.</span><span class="sxs-lookup"><span data-stu-id="9819f-156">If you are using .NET, add hello following two functions toohello .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="9819f-157">Witaj **UploadMediaFilesFromFolder** funkcja przekazywania plików z folderu (na przykład BigBuckBunny.mp4 i Image001.png) i zestawy hello mp4 toobe hello podstawowy plik w hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="9819f-157">hello **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets hello mp4 file toobe hello primary file in hello asset.</span></span> <span data-ttu-id="9819f-158">Witaj **EncodeWithOverlay** funkcja używa hello niestandardowych predefiniowanych plik, który został przekazany tooit (na przykład hello ustawień tego następujące) toocreate hello zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="9819f-158">hello **EncodeWithOverlay** function uses hello custom preset file that was passed tooit (for example, hello preset that follows) toocreate hello encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="9819f-159">Bieżące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="9819f-159">Current limitations:</span></span>
>
> <span data-ttu-id="9819f-160">Ustawienie nieprzezroczystość nakładki Hello nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="9819f-160">hello overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="9819f-161">Źródłowy plik wideo, a plik obrazu nakładki hello ma toobe w hello elementu zawartości i hello zestawu toobe potrzeb plików wideo jako plik podstawowy hello w tym zasobów.</span><span class="sxs-lookup"><span data-stu-id="9819f-161">Your source video file and hello overlay image file have toobe in hello same asset, and hello video file needs toobe set as hello primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="9819f-162">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="9819f-162">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a><span data-ttu-id="9819f-163">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="9819f-163">XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <span data-ttu-id="9819f-164"><a id="silent_audio"></a>Wstawić dyskretnej ścieżki audio, gdy dane wejściowe nie zawierają żadnych audio</span><span class="sxs-lookup"><span data-stu-id="9819f-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="9819f-165">Domyślnie w przypadku wysłania koder toohello wejściowego, który zawiera tylko wideo i audio nie następnie zawartości wyjściowej hello zawiera pliki, które zawierają dane tylko wideo.</span><span class="sxs-lookup"><span data-stu-id="9819f-165">By default, if you send an input toohello encoder that contains only video, and no audio, then hello output asset contains files that contain only video data.</span></span> <span data-ttu-id="9819f-166">Niektóre odtwarzacze może nie być możliwe toohandle takich danych wyjściowych strumieni.</span><span class="sxs-lookup"><span data-stu-id="9819f-166">Some players may not be able toohandle such output streams.</span></span> <span data-ttu-id="9819f-167">W tym scenariuszu, można użyć tego ustawienia tooforce hello koder tooadd wyjściowego toohello dyskretnej ścieżki audio.</span><span class="sxs-lookup"><span data-stu-id="9819f-167">You can use this setting tooforce hello encoder tooadd a silent audio track toohello output in that scenario.</span></span>

<span data-ttu-id="9819f-168">tooforce hello koder tooproduce element zawartości zawierający dyskretnej ścieżki audio, gdy dane wejściowe nie zawierają żadnych audio, określ wartość "InsertSilenceIfNoAudio" hello.</span><span class="sxs-lookup"><span data-stu-id="9819f-168">tooforce hello encoder tooproduce an asset that contains a silent audio track when input has no audio, specify hello "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="9819f-169">Może mieć jedną z hello predefiniowane rynkowej udokumentowane w [to](media-services-mes-presets-overview.md) sekcji, a następnie wprowadź powitania po dokonaniu zmian:</span><span class="sxs-lookup"><span data-stu-id="9819f-169">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="9819f-170">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="9819f-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="9819f-171">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="9819f-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="9819f-172"><a id="deinterlacing"></a>Wyłączanie automatycznego usuwania przeplotu.</span><span class="sxs-lookup"><span data-stu-id="9819f-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="9819f-173">Klienci nie muszą toodo niczego, jeśli ich jak hello przeplotu toobe zawartość do naprzemiennych automatycznie.</span><span class="sxs-lookup"><span data-stu-id="9819f-173">Customers don’t need toodo anything if they like hello interlace contents toobe automatically de-interlaced.</span></span> <span data-ttu-id="9819f-174">Hello automatycznego usuwania przeplot znajduje się na powitania (ustawienie domyślne), który rynkowej hello automatyczne wykrywanie naprzemiennych ramek, a tylko cofnąć interlaces oznaczony jako naprzemiennych ramki.</span><span class="sxs-lookup"><span data-stu-id="9819f-174">When hello auto de-interlacing is on (default) hello MES does hello auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="9819f-175">Można wyłączyć hello automatycznego usuwania przeplotu.</span><span class="sxs-lookup"><span data-stu-id="9819f-175">You can turn hello auto de-interlacing off.</span></span> <span data-ttu-id="9819f-176">Ta opcja nie jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="9819f-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="9819f-177">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="9819f-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="9819f-178">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="9819f-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="9819f-179"><a id="audio_only"></a>Ustawienia tylko do audio</span><span class="sxs-lookup"><span data-stu-id="9819f-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="9819f-180">W tej sekcji przedstawiono dwie predefiniowane rynkowej tylko dźwięk: AAC Audio i AAC dobrej jakości Audio.</span><span class="sxs-lookup"><span data-stu-id="9819f-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="9819f-181">AAC Audio</span><span class="sxs-lookup"><span data-stu-id="9819f-181">AAC Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a><span data-ttu-id="9819f-182">AAC dobrej jakości Audio</span><span class="sxs-lookup"><span data-stu-id="9819f-182">AAC Good Quality Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="9819f-183"><a id="concatenate"></a>Łączenie dwóch lub więcej plików wideo</span><span class="sxs-lookup"><span data-stu-id="9819f-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="9819f-184">Witaj poniższy przykład pokazuje, jak można wygenerować wstępnie zdefiniowane tooconcatenate dwóch lub więcej plików wideo.</span><span class="sxs-lookup"><span data-stu-id="9819f-184">hello following example illustrates how you can generate a preset tooconcatenate two or more video files.</span></span> <span data-ttu-id="9819f-185">najbardziej typowym scenariuszem Hello jest tooadd nagłówka lub przyczepy toohello głównego wideo.</span><span class="sxs-lookup"><span data-stu-id="9819f-185">hello most common scenario is when you want tooadd a header or a trailer toohello main video.</span></span> <span data-ttu-id="9819f-186">Witaj przeznaczony jest używany, gdy pliki wideo hello edytowany razem udziału właściwości (rozdzielczości szybkość klatek, liczba ścieżki audio, itp.).</span><span class="sxs-lookup"><span data-stu-id="9819f-186">hello intended use is when hello video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="9819f-187">Należy zadbać nie toomix wideo różne szybkości odtwarzania, albo z różną liczbą ścieżki audio.</span><span class="sxs-lookup"><span data-stu-id="9819f-187">You should take care not toomix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="9819f-188">Witaj bieżący projekt funkcji łączenia hello oczekuje tego hello wejściowych klipy wideo są spójne pod względem rozdzielczości, szybkość klatek itp.</span><span class="sxs-lookup"><span data-stu-id="9819f-188">hello current design of hello concatenation feature expects that hello input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="9819f-189">Wymagania i uwagi</span><span class="sxs-lookup"><span data-stu-id="9819f-189">Requirements and considerations</span></span>

* <span data-ttu-id="9819f-190">Wejściowy wideo powinien mieć tylko jedną ścieżkę audio.</span><span class="sxs-lookup"><span data-stu-id="9819f-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="9819f-191">Wejściowy wideo powinien mieć hello tego samego szybkość klatek.</span><span class="sxs-lookup"><span data-stu-id="9819f-191">Input videos should all have hello same frame rate.</span></span>
* <span data-ttu-id="9819f-192">Należy przekazać pliki wideo do oddzielnych zasobów i ustawić hello wideo jako plik podstawowy hello w poszczególnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9819f-192">You must upload your videos into separate assets and set hello videos as hello primary file in each asset.</span></span>
* <span data-ttu-id="9819f-193">Należy czas trwania hello tooknow plików wideo.</span><span class="sxs-lookup"><span data-stu-id="9819f-193">You need tooknow hello duration of your videos.</span></span>
* <span data-ttu-id="9819f-194">Hello predefiniowanych poniższe przykłady przyjęto założenie, że wszystkie filmy wejściowych hello rozpocząć z sygnaturą czasową o wartości zero.</span><span class="sxs-lookup"><span data-stu-id="9819f-194">hello preset examples below assumes that all hello input videos start with a timestamp of zero.</span></span> <span data-ttu-id="9819f-195">Należy wartości StartTime hello toomodify Jeśli hello wideo ma inną sygnaturą czasową początkowego, tak jak zwykle hello przypadku archiwa na żywo.</span><span class="sxs-lookup"><span data-stu-id="9819f-195">You need toomodify hello StartTime values if hello videos have different starting timestamp, as is typically hello case with live archives.</span></span>
* <span data-ttu-id="9819f-196">Hello ustawienie wstępne JSON sprawia, że jawnego odwołania do wartości AssetID toohello hello zasobów wejściowych.</span><span class="sxs-lookup"><span data-stu-id="9819f-196">hello JSON preset makes explicit references toohello AssetID values of hello input assets.</span></span>
* <span data-ttu-id="9819f-197">Witaj przykładowy kod przyjęto założenie, że tego ustawienia wstępnego JSON powitalne został zapisany plik lokalny tooa, takie jak "C:\supportFiles\preset.json".</span><span class="sxs-lookup"><span data-stu-id="9819f-197">hello sample code assumes that hello JSON preset has been saved tooa local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="9819f-198">Zakłada się również, czy dwa zasoby zostały utworzone przez dwa pliki wideo i wiedzieć hello wynikowe IDśrodkaTrwałego wartości.</span><span class="sxs-lookup"><span data-stu-id="9819f-198">It also assumes that two assets have been created by uploading two video files, and that you know hello resultant AssetID values.</span></span>
* <span data-ttu-id="9819f-199">Witaj fragment kodu i JSON ustawienie wstępne przedstawiono przykład łączenia dwóch plików wideo.</span><span class="sxs-lookup"><span data-stu-id="9819f-199">hello code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="9819f-200">Można go rozszerzyć toomore niż dwa pliki wideo przez:</span><span class="sxs-lookup"><span data-stu-id="9819f-200">You can extend it toomore than two videos by:</span></span>

  1. <span data-ttu-id="9819f-201">Zadanie telefonicznej. InputAssets.Add() wielokrotnie tooadd więcej filmów w kolejności.</span><span class="sxs-lookup"><span data-stu-id="9819f-201">Calling task.InputAssets.Add() repeatedly tooadd more videos, in order.</span></span>
  2. <span data-ttu-id="9819f-202">Co odpowiadającego edytuje element toohello "Sources" hello JSON, dodając więcej wpisów w hello tej samej kolejności.</span><span class="sxs-lookup"><span data-stu-id="9819f-202">Making corresponding edits toohello "Sources" element in hello JSON, by adding more entries, in hello same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="9819f-203">Kodu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="9819f-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="9819f-204">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="9819f-204">JSON preset</span></span>

<span data-ttu-id="9819f-205">Zaktualizuj niestandardowe ustawienia wstępnego z identyfikatorami hello zasoby, które mają tooconcatenate i z segmentem odpowiedni czas hello każdego wideo.</span><span class="sxs-lookup"><span data-stu-id="9819f-205">Update your custom preset with ids of hello assets that you want tooconcatenate, and with hello appropriate time segment for each video.</span></span>

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="9819f-206"><a id="crop"></a>Przytnij wideo przy użyciu Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="9819f-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="9819f-207">Zobacz hello [Przycinanie wideo z Media Encoder Standard](media-services-crop-video.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="9819f-207">See hello [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="9819f-208"><a id="no_video"></a>Wstaw Ścieżka wideo, gdy dane wejściowe nie ma karty wideo</span><span class="sxs-lookup"><span data-stu-id="9819f-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="9819f-209">Domyślnie w przypadku wysłania koder toohello wejściowego, który zawiera tylko audio i wideo nie następnie zawartości wyjściowej hello zawiera pliki, które zawierają dane tylko audio.</span><span class="sxs-lookup"><span data-stu-id="9819f-209">By default, if you send an input toohello encoder that contains only audio, and no video, then hello output asset contains files that contain only audio data.</span></span> <span data-ttu-id="9819f-210">Niektóre odtwarzacze, łącznie z usługi Azure Media Player (zobacz [to](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) może nie być możliwe toohandle tych strumieni.</span><span class="sxs-lookup"><span data-stu-id="9819f-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able toohandle such streams.</span></span> <span data-ttu-id="9819f-211">Można użyć tego ustawienia tooforce hello koder tooadd wyjściowego toohello monochromatyczny Ścieżka wideo w tym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="9819f-211">You can use this setting tooforce hello encoder tooadd a monochrome video track toohello output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="9819f-212">Wymuszanie tooinsert kodera hello dane wyjściowe Ścieżka wideo zwiększa hello rozmiar hello output zasobów i tym samym hello kosztów ponoszonych na powitania kodowania zadań.</span><span class="sxs-lookup"><span data-stu-id="9819f-212">Forcing hello encoder tooinsert an output video track increases hello size of hello output Asset, and thereby hello cost incurred for hello encoding Task.</span></span> <span data-ttu-id="9819f-213">Należy uruchomić testy tooverify to zwiększenie wynikowe ma tylko niewielkie wpływ na Twoje opłaty miesięczne.</span><span class="sxs-lookup"><span data-stu-id="9819f-213">You should run tests tooverify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a><span data-ttu-id="9819f-214">Wstawianie wideo na wyłącznie hello najniższa szybkość transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="9819f-214">Inserting video at only hello lowest bitrate</span></span>

<span data-ttu-id="9819f-215">Załóżmy, że są przy użyciu wielu kodowania szybkości transmisji bitów ustawień, takich jak ["H264 szybkość transmisji bitów 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode całego wejściowych katalogu do przesyłania strumieniowego, który zawiera pliki wideo i audio — tylko do plików.</span><span class="sxs-lookup"><span data-stu-id="9819f-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="9819f-216">W tym scenariuszu po hello danych wejściowych nie ma karty wideo, może być tooinsert kodera hello tooforce wideo w skali odcieni szarości śledzenie na właśnie hello najniższa szybkość transmisji bitów, jako min. tooinserting wideo w każdym szybkości transmisji bitów danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="9819f-216">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at just hello lowest bitrate, as opposed tooinserting video at every output bitrate.</span></span> <span data-ttu-id="9819f-217">tooachieve, to należy toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flagi.</span><span class="sxs-lookup"><span data-stu-id="9819f-217">tooachieve this, you need toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="9819f-218">Może mieć jedną z hello predefiniowane rynkowej udokumentowane w [to](media-services-mes-presets-overview.md) sekcji, a następnie wprowadź powitania po dokonaniu zmian:</span><span class="sxs-lookup"><span data-stu-id="9819f-218">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="9819f-219">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="9819f-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="9819f-220">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="9819f-220">XML preset</span></span>

<span data-ttu-id="9819f-221">Za pomocą XML, używaj warunku = "InsertBlackIfNoVideoBottomLayerOnly" jako atrybutu toohello **H264Video** element i stan za = "InsertSilenceIfNoAudio" jako atrybutu**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="9819f-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="9819f-222">Wstawianie wideo na wszystkich danych wyjściowych szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="9819f-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="9819f-223">Załóżmy, że są przy użyciu wielu kodowania szybkości transmisji bitów ustawień, takich jak ["H264 szybkość transmisji bitów 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode całego wejściowych katalogu do przesyłania strumieniowego, który zawiera pliki wideo i audio — tylko do plików.</span><span class="sxs-lookup"><span data-stu-id="9819f-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="9819f-224">W tym scenariuszu po hello danych wejściowych nie ma karty wideo, może być tooinsert kodera hello tooforce monochromatyczny wideo śledzenia na wszystkich hello dane wyjściowe szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="9819f-224">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at all hello output bitrates.</span></span> <span data-ttu-id="9819f-225">Gwarantuje to, że dane wyjściowe są wszystkie jednorodnego z toonumber względem ścieżki wideo i audio ścieżki.</span><span class="sxs-lookup"><span data-stu-id="9819f-225">This ensures that your output Assets are all homogenous with respect toonumber of video tracks and audio tracks.</span></span> <span data-ttu-id="9819f-226">tooachieve, to należy hello toospecify flagi "InsertBlackIfNoVideo".</span><span class="sxs-lookup"><span data-stu-id="9819f-226">tooachieve this, you need toospecify hello "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="9819f-227">Może mieć jedną z hello predefiniowane rynkowej udokumentowane w [to](media-services-mes-presets-overview.md) sekcji, a następnie wprowadź powitania po dokonaniu zmian:</span><span class="sxs-lookup"><span data-stu-id="9819f-227">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="9819f-228">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="9819f-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="9819f-229">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="9819f-229">XML preset</span></span>

<span data-ttu-id="9819f-230">Za pomocą XML, używaj warunku = "InsertBlackIfNoVideo" jako atrybutu toohello **H264Video** element i stan za = "InsertSilenceIfNoAudio" jako atrybutu**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="9819f-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <span data-ttu-id="9819f-231"><a id="rotate_video"></a>Obróć wideo</span><span class="sxs-lookup"><span data-stu-id="9819f-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="9819f-232">Witaj [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) obsługuje obrotu kątami 0/90/180/270.</span><span class="sxs-lookup"><span data-stu-id="9819f-232">hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="9819f-233">Witaj domyślne zachowanie to "Auto", gdy próbuje toodetect hello obrotu metadane w pliku wideo przychodzących hello i kompensacji go.</span><span class="sxs-lookup"><span data-stu-id="9819f-233">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming video file and compensate for it.</span></span> <span data-ttu-id="9819f-234">Uwzględnij następujące elementy hello **źródeł** tooone element hello ustawień określonych w [to](media-services-mes-presets-overview.md) sekcji:</span><span class="sxs-lookup"><span data-stu-id="9819f-234">Include hello following **Sources** element tooone of hello presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="9819f-235">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="9819f-235">JSON preset</span></span>
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a><span data-ttu-id="9819f-236">Ustawienie wstępne XML</span><span class="sxs-lookup"><span data-stu-id="9819f-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="9819f-237">Zobacz też [to](media-services-mes-schema.md#PreserveResolutionAfterRotation) tematu, aby uzyskać więcej informacji na interpretowanie ustawienia szerokości i wysokości hello w hello kodera hello zdefiniowane, po wyzwoleniu kompensacji obrotu.</span><span class="sxs-lookup"><span data-stu-id="9819f-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how hello encoder interprets hello Width and Height settings in hello preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="9819f-238">Za pomocą hello wartość "0" tooindicate toohello koder tooignore obrotu metadanych, jeśli jest obecny w hello wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="9819f-238">You can use hello value "0" tooindicate toohello encoder tooignore rotation metadata, if present, in hello input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="9819f-239">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="9819f-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9819f-240">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="9819f-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="9819f-241">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9819f-241">See Also</span></span>
[<span data-ttu-id="9819f-242">Usługi multimediów kodowania — omówienie</span><span class="sxs-lookup"><span data-stu-id="9819f-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
