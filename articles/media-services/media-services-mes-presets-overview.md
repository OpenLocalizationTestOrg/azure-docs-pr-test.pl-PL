---
title: Ustawienia aaaTask rynkowej (Media Encoder Standard) | Dokumentacja firmy Microsoft
description: "Omówienie ustawień domyślnych zadań dla rynkowej (Media Encoder Standard) i zapewnia tematu Hello."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f243ed1c-ac9c-4300-a5f7-f092cf9853b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 56e098d6d8c8f84031421ec59f087f20370ba111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a>Ustawienia zadania rynkowej (Media Encoder Standard)

**Media Encoder Standard** definiuje zestaw kodowanie ustawienia, można użyć podczas tworzenia zadania kodowania. Zalecane jest hello toouse "Adaptacyjne przesyłanie strumieniowe" ustawień wstępnych. Jeśli chcesz tooencode wideo do przesyłania strumieniowego z usługi Media Services. Po określeniu to wstępnie zdefiniowane, zostanie Media Encoder Standard [automatycznego generowania drabinę szybkości transmisji bitów](media-services-autogen-bitrate-ladder-with-mes.md). 

Jednak toocustomize predefiniowanych funkcji kodowania, należy należy wykonać jedną z hello kodowanie ustawienia zdefiniowane w tej sekcji jako szablon dla danej konfiguracji niestandardowej. Dla wyjaśnienia, jaki każdego elementu w tych oznacza, że ustawienia i hello prawidłowe wartości dla każdego elementu, zobacz hello [Media Encoder Standard schematu](media-services-mes-schema.md) tematu.  
  
> [!NOTE]
>  Korzystając z ustawienia domyślne dla koduje 4k, należy pobrać hello `S3` zastrzeżone typu jednostki. Aby uzyskać więcej informacji, zobacz [jak tooScale kodowanie](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).  
  
Podczas pracy z Media Encoder Standard, obracanie jest domyślnie włączona. Jeśli wideo został zarejestrowany na smartfonie lub inne urządzenie przenośne w trybie portret predefiniowane domyślnie obracanie tooLandscape tryb uprzedniego tooencoding (w przeciwieństwie do, podczas pracy z usługi Azure Media Encoder, gdzie obrotu wideo jest ręczne operacji, a następnie zgodnie z opisem w [to](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) blogu w obszarze "Wideo obrotu").  
  
Dostępne ustawienia:  
  
 [Wiele transmisji bitów H264 1080p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 8, od 6000 KB/s too400 KB/s i audio AAC 5.1.  
  
 [Wiele transmisji bitów H264 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 8, od 6000 KB/s too400 KB/s i stereo AAC audio.  
  
 [H264 szybkość transmisji bitów 16 x 9 dla systemu iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 8, od 8500 KB/s too200 KB/s i stereo AAC audio.  
  
 [Wiele transmisji bitów H264 16 x 9 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 5, od 1900 KB/s too400 KB/s i audio AAC 5.1.  
  
 [Wiele transmisji bitów H264 16 x 9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 5, od 1900 KB/s too400 KB/s i stereo AAC audio.  
  
 [Wiele transmisji bitów H264 4K Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 12, od 20000 KB/s too1000 KB/s i audio AAC 5.1.  
  
 [Wiele transmisji bitów H264 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 12, od 20000 KB/s too1000 KB/s i stereo AAC audio.  
  
 [H264 szybkość transmisji bitów 4 x 3 dla systemu iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 8, od 8500 KB/s too200 KB/s i stereo AAC audio.  
  
 [Wiele transmisji bitów H264 4 x 3 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 5, od 1600 KB/s too400 KB/s i audio AAC 5.1.  
  
 [Wiele transmisji bitów H264 4 x 3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 5, od 1600 KB/s too400 KB/s i stereo AAC audio.  
  
 [Wiele transmisji bitów H264 720p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 6, od 3400 KB/s too400 KB/s i audio AAC 5.1.  
  
 [Wiele transmisji bitów H264 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) powoduje utworzenie zestawu plików MP4 wyrównane GOP 6, od 3400 KB/s too400 KB/s i stereo AAC audio.  
  
 [Pojedynczej szybkości transmisji bitów H264 1080p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) tworzy pojedynczy plik MP4 o szybkości transmisji bitów 6750 KB/s i audio AAC 5.1.  
  
 [Pojedynczy transmisji bitów H264 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) tworzy pojedynczy plik MP4 o szybkości transmisji bitów 6750 KB/s i stereo AAC audio.  
  
 [H264 pojedynczej szybkości transmisji bitów 4K Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) tworzy pojedynczy plik MP4 o szybkości transmisji bitów 18000 KB/s i audio AAC 5.1.  
  
 [H264 pojedynczej szybkości transmisji bitów 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) tworzy pojedynczy plik MP4 o szybkości transmisji bitów 18000 KB/s i stereo AAC audio.  
  
 [H264 pojedynczej szybkości transmisji bitów 4 x 3 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) tworzy pojedynczy plik MP4 o szybkości transmisji bitów 1800 KB/s i audio AAC 5.1.  
  
 [SD H264 pojedynczej szybkości transmisji bitów 4 x 3](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) tworzy pojedynczy plik MP4 o szybkości transmisji bitów 1800 KB/s i stereo AAC audio.  
  
 [H264 pojedynczej szybkości transmisji bitów 16 x 9 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) tworzy pojedynczy plik MP4 o szybkości transmisji bitów 2200 KB/s i audio AAC 5.1.  
  
 [SD H264 pojedynczej szybkości transmisji bitów 16 x 9](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) tworzy pojedynczy plik MP4 o szybkości transmisji bitów 2200 KB/s i stereo AAC audio.  
  
 [Pojedynczej szybkości transmisji bitów H264 720p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) tworzy pojedynczy plik MP4 o szybkości transmisji bitów 4500 KB/s i audio AAC 5.1.  
  
 [H264 pojedynczej szybkości transmisji bitów 720p dla systemu Android](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) pojedynczego pliku MP4 o szybkości transmisji bitów 2000 KB/s i stereo AAC powoduje ustawienie wstępne.  
  
 [H264 pojedynczej szybkości transmisji bitów 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) tworzy pojedynczy plik MP4 o szybkości transmisji bitów 4500 KB/s i stereo AAC audio.  
  
 [H264 pojedynczego szybkości transmisji bitów wysokiej jakości SD dla systemu Android](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) powoduje utworzenie pojedynczego pliku MP4 o szybkości 500 KB/s i stereo AAC audio...  
  
 [H264 pojedynczego szybkości transmisji bitów niska jakość SD dla systemu Android](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) tworzy pojedynczy plik MP4 o szybkości transmisji bitów w 56 Kb/s i stereo AAC audio.  
  
 Aby uzyskać więcej informacji zobacz pokrewne tooMedia koderów usług, [kodowanie na żądanie za pomocą usługi Azure Media Services](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).
