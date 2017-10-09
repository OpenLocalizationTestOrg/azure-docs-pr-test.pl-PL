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
# <a name="crop-videos-with-media-encoder-standard"></a>Przycinanie wideo za pomocą usługi Media Encoder Standard
Możesz użyć toocrop Media Encoder Standard (rynkowej) wejściowego pliku wideo. Przycinanie jest proces hello wybierając prostokątne okna w ramce wideo hello i kodowanie tylko hello pikseli w danym przedziale. powitania po diagram ułatwia ilustrują hello procesu.

![Przytnij wideo](./media/media-services-crop-video/media-services-crop-video01.png)

Załóżmy, że masz wideo ma rozdzielczość 1920 x 1080 pikseli (współczynnik proporcji 16:9), ale ma czarne paski (słupka pola) na powitania lewy i prawy, tak aby tylko okna 4:3 lub 1440 x 1080 pikseli zawiera aktywne wideo jako dane wejściowe. Można użyć toocrop rynkowej lub Edytuj limit hello czarne paski i kodowanie hello 1440 x 1080 regionu.

Przycinanie w rynkowej jest przetwarzania wstępnego etap, więc hello parametry przycinania w ustawienie wstępne kodowania hello stosuje się toohello oryginalnego wejściowy plik wideo. Kodowanie jest dalszym etapie i hello szerokość i wysokość ustawienia mają zastosowanie toohello *wstępnie przetworzonych* wideo, a nie toohello oryginalnego wideo. Podczas projektowania ustawienia potrzebne następujące hello toodo: () wybierz parametry przycięcia hello oparte na powitania oryginalnego wejściowy plik wideo i (b) wybierz Twoje kodowania ustawienia oparte na powitania przycięte wideo. Jeśli nie są zgodne z kodowania toohello ustawienia przycięte wideo, nie będą dane wyjściowe hello, zgodnie z oczekiwaniami.

Witaj [następujące](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) temacie pokazano, jak toocreate zadania kodowania z rynkowej i jak toospecify niestandardowego ustawienia wstępnego dla hello kodowania zadań. 

## <a name="creating-a-custom-preset"></a>Tworzenie animacji niestandardowej
W przykładzie hello na diagramie hello:

1. Oryginalne dane wejściowe są 1920 x 1080 pikseli
2. Musi on toobe przycięte dane wyjściowe tooan 1440 x 1080 pikseli, który skupia się w ramce wejściowych hello
3. Oznacza to Przesunięcie X (1920 — 1440) / 2 = 240 i Y przesunięcia o wartości zero
4. Hello szerokość i wysokość prostokąta przycięcia hello otrzymują 1440 1080, odpowiednio i
5. W hello kodowania etapie hello pytanie, jest tooproduce trzy warstwy, są odpowiednio rozdzielczości 1440 x 1080 pikseli, 960 x 720 i 480 x 360

### <a name="json-preset"></a>Ustawienie wstępne JSON
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


## <a name="restrictions-on-cropping"></a>Ograniczenia dotyczące przycinanie
Przycinanie funkcji Hello oznacza toobe ręcznego. Będzie potrzebny tooload dane wejściowe wideo do odpowiedniego narzędzia edycji umożliwiające zaznacz ramki zainteresowań, umieść hello kursora toodetermine przesunięć hello przycinanie prostokąta, toodetermine hello ustawienie wstępne kodowania, które dostosowana pod kątem tego konkretnego wideo, itp. Ta funkcja nie jest przeznaczona tooenable np: automatyczne wykrywanie i usuwanie granic czarny letterbox/pillarbox w wejściowego pliku wideo.

Przycinanie funkcji toohello obowiązują następujące ograniczenia. Jeśli te nie są spełnione, hello kodowania zadań może się nie powieść lub wygenerować nieoczekiwane dane wyjściowe.

1. Witaj współrzędne i rozmiar prostokąta przycięcia hello mają toofit w hello wejściowy plik wideo
2. Jak wspomniano powyżej, hello szerokość i wysokość w hello kodowania ustawień ma toohello toocorrespond przycięte wideo
3. Przycinanie stosuje toovideos przechwycone w trybie krajobraz (tj. nie dotyczy toovideos pamięci zarejestrowane z smartphone przechowywanych w pionie lub w trybie portret)
4. Działa najlepiej z obiektem wideo przechwycone kwadratowy pikseli

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Następny krok
Zobacz usługi Azure Media Services learning toohelp ścieżek, które Dowiedz się więcej o funkcje oferowane przez usługi AMS.  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
