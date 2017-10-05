---
title: "H264 pojedynczej szybkości transmisji bitów 720p ustawienia standardu Media Encoder Standard - Azure | Dokumentacja firmy Microsoft"
description: "Temat zawiera omówienie ** ustawienie wstępne pojedynczej szybkości transmisji bitów H264 720 p ** zadań."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f66da66c-9f21-441d-8038-51e3094e9307
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 5ca683db654a5adda6e15e1761579c7e81438417
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="h264-single-bitrate-720p"></a><span data-ttu-id="4439e-103">H264 Pojedynczej szybkości transmisji bitów 720p</span><span class="sxs-lookup"><span data-stu-id="4439e-103">H264 Single Bitrate 720p</span></span>
<span data-ttu-id="4439e-104">`Media Encoder Standard`definiuje zestaw kodowania ustawienia używanego podczas tworzenia zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="4439e-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="4439e-105">Można użyć `preset name` do określenia do formatu, który chcesz kodować pliku nośnika.</span><span class="sxs-lookup"><span data-stu-id="4439e-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="4439e-106">Lub można utworzyć własny JSON lub ustawienia opartych na języku XML (przy użyciu kodowania UTF-8 lub UTF-16.</span><span class="sxs-lookup"><span data-stu-id="4439e-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="4439e-107">Następnie możesz przejdzie niestandardowe ustawienia do kodera.</span><span class="sxs-lookup"><span data-stu-id="4439e-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="4439e-108">Aby uzyskać listę wszystkich istniejących nazw obsługiwanych przez to `Media Encoder Standard` kodera, zobacz [ustawień wstępnych zadań dla standardu Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4439e-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="4439e-109">W tym temacie przedstawiono `H264 Single Bitrate 720p` ustawienia wstępnego w formacie XML i JSON.</span><span class="sxs-lookup"><span data-stu-id="4439e-109">This topic shows the `H264 Single Bitrate 720p` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="4439e-110">Ten plik wstępnie zdefiniowane i tworzy jednej MP4 o szybkości transmisji bitów 4500 KB/s i stereo AAC audio.</span><span class="sxs-lookup"><span data-stu-id="4439e-110">This preset produces a single MP4 file with a bitrate of 4500 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="4439e-111">Aby uzyskać szczegółowe informacje o profilu szybkości transmisji bitów próbkowania szybkości, itp. tego ustawień, sprawdzić XML lub JSON określonych poniżej.</span><span class="sxs-lookup"><span data-stu-id="4439e-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="4439e-112">Wyjaśnień jakie każdego elementu w sposób te ustawienia i prawidłowe wartości dla każdego elementu, zobacz [Media Encoder Standard schematu](media-services-mes-schema.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="4439e-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="4439e-113">XML</span><span class="sxs-lookup"><span data-stu-id="4439e-113">XML</span></span>  
  
```  
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
  
 <span data-ttu-id="4439e-114">JSON</span><span class="sxs-lookup"><span data-stu-id="4439e-114">JSON</span></span>  
  
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
          "Bitrate": 4500,  
          "MaxBitrate": 4500,  
          "BufferWindow": "00:00:05",  
          "Width": 1280,  
          "Height": 720,  
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
