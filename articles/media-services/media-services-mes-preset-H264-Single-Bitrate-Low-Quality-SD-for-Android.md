---
title: "aaaH264 pojedynczy SD jakości małej szybkości transmisji bitów dla systemu Android | Dokumentacja firmy Microsoft"
description: "Witaj temat zawiera omówienie hello ** H264 pojedynczego szybkości transmisji bitów niska jakość SD dla systemu Android ** ustawienia wstępnego zadania."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 67d3446d-e3b8-419f-bbf8-e5149c108531
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: dc9c4e1bf65ea5f678ec1fc990c4cd353329c352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-low-quality-sd-for-android"></a>H264 SD jakości jednej małej szybkości transmisji bitów dla systemu Android
`Media Encoder Standard`definiuje zestaw kodowania ustawienia używanego podczas tworzenia zadania kodowania. Można użyć `preset name` toospecify do formatu, który chcesz tooencode Twojego pliku multimedialnego. Lub można utworzyć własny JSON lub ustawienia opartych na języku XML (przy użyciu kodowania UTF-8 lub UTF-16. Następnie możesz przejdzie hello toohello wstępnie ustawiony niestandardowy koder. Lista hello hello wszystkie ustawienia wstępnego nazw obsługiwanych przez to `Media Encoder Standard` kodera, zobacz [ustawień wstępnych zadań dla standardu Media Encoder Standard](media-services-mes-presets-overview.md).  
  
 W tym temacie przedstawiono hello `H264 Single Bitrate Low Quality SD for Android` ustawienia wstępnego w formacie XML i JSON.  
  
 Ten plik wstępnie zdefiniowane i tworzy jednej MP4 o szybkości transmisji bitów w 56 Kb/s i stereo AAC audio. Aby uzyskać szczegółowe informacje o profilu szybkości transmisji bitów próbkowania szybkości, itp. tego ustawień, sprawdź hello XML lub JSON określonych poniżej. Dla wyjaśnienia, jaki każdego elementu w tych oznacza, że ustawienia i hello prawidłowe wartości dla każdego elementu, zobacz hello [Media Encoder Standard schematu](media-services-mes-schema.md) tematu.  
  
 XML  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:05</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>56</Bitrate>  
          <Width>176</Width>  
          <Height>144</Height>  
          <FrameRate>12/1</FrameRate>  
          <Profile>Baseline</Profile>  
          <Level>2</Level>  
          <BFrames>0</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>false</AdaptiveBFrame>  
          <EntropyMode>Cavlc</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>56</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>HEAACV2</Profile>  
      <Channels>2</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>24</Bitrate>  
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
      "KeyFrameInterval": "00:00:05",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Baseline",  
          "Level": "2",  
          "Bitrate": 56,  
          "MaxBitrate": 56,  
          "BufferWindow": "00:00:05",  
          "Width": 176,  
          "Height": 144,  
          "ReferenceFrames": 3,  
          "EntropyMode": "Cavlc",  
          "Type": "H264Layer",  
          "FrameRate": "12/1"  
        }  
      ],  
      "Type": "H264Video"  
    },  
    {  
      "Profile": "HEAACV2",  
      "Channels": 2,  
      "SamplingRate": 48000,  
      "Bitrate": 24,  
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
