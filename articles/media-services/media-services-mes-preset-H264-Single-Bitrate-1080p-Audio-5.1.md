---
title: "aaaH264 pojedynczej szybkości transmisji bitów 1080p Audio 5.1 | Dokumentacja firmy Microsoft"
description: "Witaj temat zawiera omówienie hello ** pojedynczej szybkości transmisji bitów H264 1080p Audio 5.1* * zadań ustawienie wstępne."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: b42238de-2a3c-4683-ae7f-7ce19ad5162e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 8ee5f34f4fd84c615ca8c5e7554e9ec832f54a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-1080p-audio-51"></a>H264 Audio 1080p pojedynczej szybkości transmisji bitów 5.1
`Media Encoder Standard`definiuje zestaw kodowania ustawienia używanego podczas tworzenia zadania kodowania. Można użyć `preset name` toospecify do formatu, który chcesz tooencode Twojego pliku multimedialnego. Lub można utworzyć własny JSON lub ustawienia opartych na języku XML (przy użyciu kodowania UTF-8 lub UTF-16. Następnie możesz przejdzie hello toohello wstępnie ustawiony niestandardowy koder. Lista hello hello wszystkie ustawienia wstępnego nazw obsługiwanych przez to `Media Encoder Standard` kodera, zobacz [ustawień wstępnych zadań dla standardu Media Encoder Standard](media-services-mes-presets-overview.md).  
  
 W tym temacie przedstawiono hello `H264 Single Bitrate 1080p Audio 5.1` ustawienia wstępnego w formacie XML i JSON.  
  
 To ustawienie wstępne tworzy pojedynczy plik MP4 o szybkości transmisji bitów 6750 KB/s i audio AAC 5.1. Aby uzyskać szczegółowe informacje o profilu szybkości transmisji bitów próbkowania szybkości, itp. tego ustawień, sprawdź hello XML lub JSON określonych poniżej. Wyjaśnienia dotyczące oznacza jakie każdy element i hello prawidłowe wartości dla każdego elementu, można znaleźć hello [Media Encoder Standard schematu](media-services-mes-schema.md).  
  
 XML  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>6750</Bitrate>  
          <Width>1920</Width>  
          <Height>1080</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>6750</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>6</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>384</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 JSON  
  
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
          "Bitrate": 6750,  
          "MaxBitrate": 6750,  
          "BufferWindow": "00:00:05",  
          "Width": 1920,  
          "Height": 1080,  
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
      "Channels": 6,  
      "SamplingRate": 48000,  
      "Bitrate": 384,  
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
