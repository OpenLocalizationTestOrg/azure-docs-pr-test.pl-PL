---
title: "Ustawienie aaaH264 pojedynczej szybkości transmisji bitów 4K Media Encoder Standard - Azure | Dokumentacja firmy Microsoft"
description: "Witaj temat zawiera omówienie hello ** pojedynczej szybkości transmisji bitów H264 4 K ** ustawienie wstępne zadań."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 8e437aea-8193-49a0-9ff2-4fd391c80972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 3a88207ba89baaefddfea631aa5d4c1c74194c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-4k"></a><span data-ttu-id="2bbee-103">H264 Pojedynczej szybkości transmisji bitów 4K</span><span class="sxs-lookup"><span data-stu-id="2bbee-103">H264 Single Bitrate 4K</span></span>
<span data-ttu-id="2bbee-104">`Media Encoder Standard`definiuje zestaw kodowania ustawienia używanego podczas tworzenia zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="2bbee-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="2bbee-105">Można użyć `preset name` toospecify do formatu, który chcesz tooencode Twojego pliku multimedialnego.</span><span class="sxs-lookup"><span data-stu-id="2bbee-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="2bbee-106">Lub można utworzyć własny JSON lub ustawienia opartych na języku XML (przy użyciu kodowania UTF-8 lub UTF-16.</span><span class="sxs-lookup"><span data-stu-id="2bbee-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="2bbee-107">Następnie możesz przejdzie hello toohello wstępnie ustawiony niestandardowy koder.</span><span class="sxs-lookup"><span data-stu-id="2bbee-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="2bbee-108">Lista hello hello wszystkie ustawienia wstępnego nazw obsługiwanych przez to `Media Encoder Standard` kodera, zobacz [ustawień wstępnych zadań dla standardu Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2bbee-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="2bbee-109">W tym temacie przedstawiono hello `H264 Single Bitrate 4K` ustawienia wstępnego w formacie XML i JSON.</span><span class="sxs-lookup"><span data-stu-id="2bbee-109">This topic shows hello `H264 Single Bitrate 4K` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="2bbee-110">Ten plik wstępnie zdefiniowane i tworzy jednej MP4 o szybkości transmisji bitów 18000 KB/s i stereo AAC audio.</span><span class="sxs-lookup"><span data-stu-id="2bbee-110">This preset produces a single MP4 file with a bitrate of 18000 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="2bbee-111">Aby uzyskać szczegółowe informacje o profilu szybkości transmisji bitów próbkowania szybkości, itp. tego ustawień, sprawdź hello XML lub JSON określonych poniżej.</span><span class="sxs-lookup"><span data-stu-id="2bbee-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="2bbee-112">Dla wyjaśnienia, jaki każdego elementu w tych oznacza, że ustawienia i hello prawidłowe wartości dla każdego elementu, zobacz hello [Media Encoder Standard schematu](media-services-mes-schema.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="2bbee-112">For explanations of what each element in these presets means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="2bbee-113">Należy pobrać hello Premium zastrzeżone koduje typu jednostki z 4K.</span><span class="sxs-lookup"><span data-stu-id="2bbee-113">You should get hello Premium reserved unit type with 4K encodes.</span></span> <span data-ttu-id="2bbee-114">Aby uzyskać więcej informacji, zobacz [jak tooScale kodowanie](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span><span class="sxs-lookup"><span data-stu-id="2bbee-114">For more information, see [How tooScale Encoding](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span></span>  
  
 <span data-ttu-id="2bbee-115">XML</span><span class="sxs-lookup"><span data-stu-id="2bbee-115">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>18000</Bitrate>  
          <Width>3840</Width>  
          <Height>2160</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>18000</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
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
```  
  
 <span data-ttu-id="2bbee-116">JSON</span><span class="sxs-lookup"><span data-stu-id="2bbee-116">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 18000,  
          "MaxBitrate": 18000,  
          "BufferWindow": "00:00:05",  
          "Width": 3840,  
          "Height": 2160,  
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
```
