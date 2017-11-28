---
title: Jak przycinanie wideo z Media Encoder Standard - Azure | Dokumentacja firmy Microsoft
description: "W tym artykule przedstawiono sposób przycięcia wideo z Media Encoder Standard."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 7628f674-2005-4531-8b61-d7a4f53e46ba
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/09/2017
ms.author: anilmur;juliako;
ms.openlocfilehash: 60d0ce14a271fcbe698559da95ca011cb888b221
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="caf47-103">Przycinanie wideo za pomocą usługi Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="caf47-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="caf47-104">Aby przyciąć dane wejściowe wideo, można użyć Media Encoder Standard (rynkowej).</span><span class="sxs-lookup"><span data-stu-id="caf47-104">You can use Media Encoder Standard (MES) to crop your input video.</span></span> <span data-ttu-id="caf47-105">Przycinanie to proces wyboru prostokątne okna w ramce wideo i kodowanie tylko pikseli w danym przedziale.</span><span class="sxs-lookup"><span data-stu-id="caf47-105">Cropping is the process of selecting a rectangular window within the video frame, and encoding just the pixels within that window.</span></span> <span data-ttu-id="caf47-106">Poniższy diagram ułatwia zilustrowanie tego procesu.</span><span class="sxs-lookup"><span data-stu-id="caf47-106">The following diagram helps illustrate the process.</span></span>

![Przytnij wideo](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="caf47-108">Załóżmy, że masz jako dane wejściowe wideo ma rozdzielczość 1920 x 1080 pikseli (współczynnik proporcji 16:9), ale ma czarne paski (pola słupka) w lewo i w prawo, tak aby tylko okna 4:3 lub 1440 x 1080 pikseli zawiera aktywne wideo.</span><span class="sxs-lookup"><span data-stu-id="caf47-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at the left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="caf47-109">Użyj rynkowej Aby przyciąć lub edytować limit czarne paski i kodowanie region 1440 x 1080 pikseli.</span><span class="sxs-lookup"><span data-stu-id="caf47-109">You can use MES to crop or edit out the black bars, and encode the 1440x1080 region.</span></span>

<span data-ttu-id="caf47-110">Przycinanie w rynkowej jest przetwarzania wstępnego etap, więc przycinania parametry w ustawienie wstępne kodowania stosuje się do oryginalnej wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="caf47-110">Cropping in MES is a pre-processing stage, so the cropping parameters in the encoding preset apply to the original input video.</span></span> <span data-ttu-id="caf47-111">Kodowanie jest dalszym etapie i ustawienia szerokości i wysokości dotyczą *wstępnie przetworzonych* wideo, a nie do oryginalnego wideo.</span><span class="sxs-lookup"><span data-stu-id="caf47-111">Encoding is a subsequent stage, and the width/height settings apply to the *pre-processed* video, and not to the original video.</span></span> <span data-ttu-id="caf47-112">Podczas projektowania ustawienia należy wykonać następujące czynności: () wybierz parametrów przycięcia oparty na oryginalnym wejściowy plik wideo i (b) wybierz Twoje kodowania ustawienia oparte na przycięte wideo.</span><span class="sxs-lookup"><span data-stu-id="caf47-112">When designing your preset you need to do the following: (a) select the crop parameters based on the original input video, and (b) select your encode settings based on the cropped video.</span></span> <span data-ttu-id="caf47-113">Jeśli nie są zgodne z kodowania ustawienia przycięte wideo, nie będą dane wyjściowe, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="caf47-113">If you do not match your encode settings to the cropped video, the output will not be as you expect.</span></span>

<span data-ttu-id="caf47-114">[Następujące](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) temacie przedstawiono sposób tworzenia zadania kodowania rynkowej oraz sposób określania niestandardowej ustawienie wstępne kodowania zadania.</span><span class="sxs-lookup"><span data-stu-id="caf47-114">The [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how to create an encoding job with MES and how to specify a custom preset for the encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="caf47-115">Tworzenie animacji niestandardowej</span><span class="sxs-lookup"><span data-stu-id="caf47-115">Creating a custom preset</span></span>
<span data-ttu-id="caf47-116">W przykładzie przedstawionym w diagramie:</span><span class="sxs-lookup"><span data-stu-id="caf47-116">In the example shown in the diagram:</span></span>

1. <span data-ttu-id="caf47-117">Oryginalne dane wejściowe są 1920 x 1080 pikseli</span><span class="sxs-lookup"><span data-stu-id="caf47-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="caf47-118">Należy go przycięte do wyjścia 1440 x 1080 pikseli, który skupia się w ramce wejściowych</span><span class="sxs-lookup"><span data-stu-id="caf47-118">It needs to be cropped to an output of 1440x1080, which is centered in the input frame</span></span>
3. <span data-ttu-id="caf47-119">Oznacza to Przesunięcie X (1920 — 1440) / 2 = 240 i Y przesunięcia o wartości zero</span><span class="sxs-lookup"><span data-stu-id="caf47-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="caf47-120">Szerokość i wysokość prostokąta przycięcia są 1440 i 1080, w odpowiednio</span><span class="sxs-lookup"><span data-stu-id="caf47-120">The Width and Height of the Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="caf47-121">W fazie Koduj Zadaj jest przygotowanie trzy warstwy, są odpowiednio rozdzielczości 1440 x 1080 pikseli, 960 x 720 i 480 x 360</span><span class="sxs-lookup"><span data-stu-id="caf47-121">In the encode stage, the ask is to produce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="caf47-122">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="caf47-122">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "Crop": {
                "X": 240,
                "Y": 0,
                "Width": 1440,
                "Height": 1080
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
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1440,
              "Height": 1080,
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
              "Bitrate": 1250,
              "MaxBitrate": 1250,
              "BufferWindow": "00:00:05",
              "Width": 480,
              "Height": 360,
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="caf47-123">Ograniczenia dotyczące przycinanie</span><span class="sxs-lookup"><span data-stu-id="caf47-123">Restrictions on cropping</span></span>
<span data-ttu-id="caf47-124">Oznacza, że funkcja przycinania można ręcznie.</span><span class="sxs-lookup"><span data-stu-id="caf47-124">The cropping feature is meant to be manual.</span></span> <span data-ttu-id="caf47-125">Musisz załadować wejściowy plik wideo do odpowiedniej edycji narzędzie, które pozwala wybrać ramki zainteresowań, umieść kursor ustalenie przesunięć prostokąta kadrowania, aby określić ustawienie wstępne kodowania, które dostosowana pod kątem tego konkretnego wideo, itp. Ta funkcja nie jest przeznaczona do elementów, jak włączyć: automatyczne wykrywanie i usuwanie granic czarny letterbox/pillarbox w wejściowego pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="caf47-125">You would need to load your input video into a suitable editing tool that lets you select frames of interest, position the cursor to determine offsets for the cropping rectangle, to determine the encoding preset that is tuned for that particular video, etc. This feature is not meant to enable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="caf47-126">Następujące ograniczenia dotyczące funkcji przycinania.</span><span class="sxs-lookup"><span data-stu-id="caf47-126">Following constraints apply to the cropping feature.</span></span> <span data-ttu-id="caf47-127">Te nie są spełnione, kodowanie zadań mogą zakończyć się niepowodzeniem, czy wygenerować nieoczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="caf47-127">If these are not met, the encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="caf47-128">Współrzędne i Rozmiar przycięcia musi mieścić się w wejściowy plik wideo</span><span class="sxs-lookup"><span data-stu-id="caf47-128">The co-ordinates and size of the Crop rectangle have to fit within the input video</span></span>
2. <span data-ttu-id="caf47-129">Jak wspomniano powyżej, szerokość i wysokość w ustawieniach Koduj musi odpowiadać przycięte wideo</span><span class="sxs-lookup"><span data-stu-id="caf47-129">As mentioned above, the Width & Height in the encode settings have to correspond to the cropped video</span></span>
3. <span data-ttu-id="caf47-130">Przycinanie dotyczy wideo przechwycone w trybie krajobraz (tj. nie dotyczy filmy wideo z smartphone zapisywane przechowywanych w pionie lub w trybie portret)</span><span class="sxs-lookup"><span data-stu-id="caf47-130">Cropping applies to videos captured in landscape mode (i.e. not applicable to videos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="caf47-131">Działa najlepiej z obiektem wideo przechwycone kwadratowy pikseli</span><span class="sxs-lookup"><span data-stu-id="caf47-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="caf47-132">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="caf47-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="caf47-133">Następny krok</span><span class="sxs-lookup"><span data-stu-id="caf47-133">Next step</span></span>
<span data-ttu-id="caf47-134">Zobacz usługi Azure Media Services ścieżki szkoleniowe dotyczące Aby uzyskać więcej informacji o funkcje oferowane przez usługi AMS.</span><span class="sxs-lookup"><span data-stu-id="caf47-134">See Azure Media Services learning paths to help you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
