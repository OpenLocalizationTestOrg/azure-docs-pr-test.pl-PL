---
title: aaaHow toocrop wideo z Media Encoder Standard - Azure | Dokumentacja firmy Microsoft
description: "W tym artykule przedstawiono sposób toocrop wideo przy użyciu Media Encoder Standard."
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
ms.openlocfilehash: 2b4ac3d96228b93c890a38c57c4913988de1e8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="e337b-103">Przycinanie wideo za pomocą usługi Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="e337b-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="e337b-104">Możesz użyć toocrop Media Encoder Standard (rynkowej) wejściowego pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="e337b-104">You can use Media Encoder Standard (MES) toocrop your input video.</span></span> <span data-ttu-id="e337b-105">Przycinanie jest proces hello wybierając prostokątne okna w ramce wideo hello i kodowanie tylko hello pikseli w danym przedziale.</span><span class="sxs-lookup"><span data-stu-id="e337b-105">Cropping is hello process of selecting a rectangular window within hello video frame, and encoding just hello pixels within that window.</span></span> <span data-ttu-id="e337b-106">powitania po diagram ułatwia ilustrują hello procesu.</span><span class="sxs-lookup"><span data-stu-id="e337b-106">hello following diagram helps illustrate hello process.</span></span>

![Przytnij wideo](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="e337b-108">Załóżmy, że masz wideo ma rozdzielczość 1920 x 1080 pikseli (współczynnik proporcji 16:9), ale ma czarne paski (słupka pola) na powitania lewy i prawy, tak aby tylko okna 4:3 lub 1440 x 1080 pikseli zawiera aktywne wideo jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="e337b-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at hello left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="e337b-109">Można użyć toocrop rynkowej lub Edytuj limit hello czarne paski i kodowanie hello 1440 x 1080 regionu.</span><span class="sxs-lookup"><span data-stu-id="e337b-109">You can use MES toocrop or edit out hello black bars, and encode hello 1440x1080 region.</span></span>

<span data-ttu-id="e337b-110">Przycinanie w rynkowej jest przetwarzania wstępnego etap, więc hello parametry przycinania w ustawienie wstępne kodowania hello stosuje się toohello oryginalnego wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="e337b-110">Cropping in MES is a pre-processing stage, so hello cropping parameters in hello encoding preset apply toohello original input video.</span></span> <span data-ttu-id="e337b-111">Kodowanie jest dalszym etapie i hello szerokość i wysokość ustawienia mają zastosowanie toohello *wstępnie przetworzonych* wideo, a nie toohello oryginalnego wideo.</span><span class="sxs-lookup"><span data-stu-id="e337b-111">Encoding is a subsequent stage, and hello width/height settings apply toohello *pre-processed* video, and not toohello original video.</span></span> <span data-ttu-id="e337b-112">Podczas projektowania ustawienia potrzebne następujące hello toodo: () wybierz parametry przycięcia hello oparte na powitania oryginalnego wejściowy plik wideo i (b) wybierz Twoje kodowania ustawienia oparte na powitania przycięte wideo.</span><span class="sxs-lookup"><span data-stu-id="e337b-112">When designing your preset you need toodo hello following: (a) select hello crop parameters based on hello original input video, and (b) select your encode settings based on hello cropped video.</span></span> <span data-ttu-id="e337b-113">Jeśli nie są zgodne z kodowania toohello ustawienia przycięte wideo, nie będą dane wyjściowe hello, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="e337b-113">If you do not match your encode settings toohello cropped video, hello output will not be as you expect.</span></span>

<span data-ttu-id="e337b-114">Witaj [następujące](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) temacie pokazano, jak toocreate zadania kodowania z rynkowej i jak toospecify niestandardowego ustawienia wstępnego dla hello kodowania zadań.</span><span class="sxs-lookup"><span data-stu-id="e337b-114">hello [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how toocreate an encoding job with MES and how toospecify a custom preset for hello encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="e337b-115">Tworzenie animacji niestandardowej</span><span class="sxs-lookup"><span data-stu-id="e337b-115">Creating a custom preset</span></span>
<span data-ttu-id="e337b-116">W przykładzie hello na diagramie hello:</span><span class="sxs-lookup"><span data-stu-id="e337b-116">In hello example shown in hello diagram:</span></span>

1. <span data-ttu-id="e337b-117">Oryginalne dane wejściowe są 1920 x 1080 pikseli</span><span class="sxs-lookup"><span data-stu-id="e337b-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="e337b-118">Musi on toobe przycięte dane wyjściowe tooan 1440 x 1080 pikseli, który skupia się w ramce wejściowych hello</span><span class="sxs-lookup"><span data-stu-id="e337b-118">It needs toobe cropped tooan output of 1440x1080, which is centered in hello input frame</span></span>
3. <span data-ttu-id="e337b-119">Oznacza to Przesunięcie X (1920 — 1440) / 2 = 240 i Y przesunięcia o wartości zero</span><span class="sxs-lookup"><span data-stu-id="e337b-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="e337b-120">Hello szerokość i wysokość prostokąta przycięcia hello otrzymują 1440 1080, odpowiednio i</span><span class="sxs-lookup"><span data-stu-id="e337b-120">hello Width and Height of hello Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="e337b-121">W hello kodowania etapie hello pytanie, jest tooproduce trzy warstwy, są odpowiednio rozdzielczości 1440 x 1080 pikseli, 960 x 720 i 480 x 360</span><span class="sxs-lookup"><span data-stu-id="e337b-121">In hello encode stage, hello ask is tooproduce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="e337b-122">Ustawienie wstępne JSON</span><span class="sxs-lookup"><span data-stu-id="e337b-122">JSON preset</span></span>
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="e337b-123">Ograniczenia dotyczące przycinanie</span><span class="sxs-lookup"><span data-stu-id="e337b-123">Restrictions on cropping</span></span>
<span data-ttu-id="e337b-124">Przycinanie funkcji Hello oznacza toobe ręcznego.</span><span class="sxs-lookup"><span data-stu-id="e337b-124">hello cropping feature is meant toobe manual.</span></span> <span data-ttu-id="e337b-125">Będzie potrzebny tooload dane wejściowe wideo do odpowiedniego narzędzia edycji umożliwiające zaznacz ramki zainteresowań, umieść hello kursora toodetermine przesunięć hello przycinanie prostokąta, toodetermine hello ustawienie wstępne kodowania, które dostosowana pod kątem tego konkretnego wideo, itp. Ta funkcja nie jest przeznaczona tooenable np: automatyczne wykrywanie i usuwanie granic czarny letterbox/pillarbox w wejściowego pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="e337b-125">You would need tooload your input video into a suitable editing tool that lets you select frames of interest, position hello cursor toodetermine offsets for hello cropping rectangle, toodetermine hello encoding preset that is tuned for that particular video, etc. This feature is not meant tooenable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="e337b-126">Przycinanie funkcji toohello obowiązują następujące ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="e337b-126">Following constraints apply toohello cropping feature.</span></span> <span data-ttu-id="e337b-127">Jeśli te nie są spełnione, hello kodowania zadań może się nie powieść lub wygenerować nieoczekiwane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="e337b-127">If these are not met, hello encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="e337b-128">Witaj współrzędne i rozmiar prostokąta przycięcia hello mają toofit w hello wejściowy plik wideo</span><span class="sxs-lookup"><span data-stu-id="e337b-128">hello co-ordinates and size of hello Crop rectangle have toofit within hello input video</span></span>
2. <span data-ttu-id="e337b-129">Jak wspomniano powyżej, hello szerokość i wysokość w hello kodowania ustawień ma toohello toocorrespond przycięte wideo</span><span class="sxs-lookup"><span data-stu-id="e337b-129">As mentioned above, hello Width & Height in hello encode settings have toocorrespond toohello cropped video</span></span>
3. <span data-ttu-id="e337b-130">Przycinanie stosuje toovideos przechwycone w trybie krajobraz (tj. nie dotyczy toovideos pamięci zarejestrowane z smartphone przechowywanych w pionie lub w trybie portret)</span><span class="sxs-lookup"><span data-stu-id="e337b-130">Cropping applies toovideos captured in landscape mode (i.e. not applicable toovideos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="e337b-131">Działa najlepiej z obiektem wideo przechwycone kwadratowy pikseli</span><span class="sxs-lookup"><span data-stu-id="e337b-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="e337b-132">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="e337b-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="e337b-133">Następny krok</span><span class="sxs-lookup"><span data-stu-id="e337b-133">Next step</span></span>
<span data-ttu-id="e337b-134">Zobacz usługi Azure Media Services learning toohelp ścieżek, które Dowiedz się więcej o funkcje oferowane przez usługi AMS.</span><span class="sxs-lookup"><span data-stu-id="e337b-134">See Azure Media Services learning paths toohelp you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
