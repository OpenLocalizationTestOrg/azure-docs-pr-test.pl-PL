---
title: "aaaEncode zasobów przy użyciu standardu Media Encoder Standard z hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki hello kodowanie zasobów przy użyciu standardu Media Encoder Standard z hello portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a>Kodowanie elementu zawartości przy użyciu standardu Media Encoder Standard z hello portalu Azure
> [!NOTE]
> toocomplete tego samouczka jest potrzebne konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Podczas pracy w usłudze Azure Media Services jednym z hello najbardziej typowych scenariuszy jest dostarczanie przesyłania strumieniowego klientów tooyour adaptacyjną szybkością transmisji bitów. Usługa Media Services obsługuje hello następujące technologie przesyłania strumieniowego adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare pliki wideo do przesyłania strumieniowego o adaptacyjnej szybkości bitowej, należy tooencode źródła wideo do plików o różnych szybkościach transmisji bitów. Należy używać hello **Media Encoder Standard** tooencode koder wideo.  

Media Services udostępnia również funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver Twojego MP4s wielokrotnej szybkości transmisji bitów w następujących formatów przesyłania strumieniowego hello: MPEG DASH, HLS, Smooth Streaming, bez konieczności toore pakietów w tych formatach. Dzięki funkcji dynamicznego tworzenia pakietów wystarczy toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź hello na podstawie żądań klienta.

tootake korzyści z dynamicznego tworzenia pakietów, należy tooencode pliku źródłowego do zestawu plików MP4 wielokrotnej szybkości transmisji bitów (kroki kodowania hello przedstawiono w dalszej części tej sekcji).

media tooscale przetwarzania, zobacz [to](media-services-portal-scale-media-processing.md) tematu.

## <a name="encode-with-hello-azure-portal"></a>Kodowanie z hello portalu Azure
W tej sekcji opisano kroki hello może zająć tooencode zawartości przy użyciu standardu Media Encoder Standard.

1. W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.
2. W hello **ustawienia** wybierz **zasoby**.  
3. W hello **zasoby** okna, wybierz hello zasobów chcesz tooencode.
4. Naciśnij klawisz hello **Koduj** przycisku.
5. W hello **kodowanie elementu zawartości** okna, hello wybierz procesor "Media Encoder Standard" oraz ustawienie wstępne. Aby uzyskać informacje o ustawieniach wstępnych, zobacz [Automatyczne generowanie drabiny szybkości transmisji bitów](media-services-autogen-bitrate-ladder-with-mes.md) i [Ustawienia wstępne zadań usługi MES](media-services-mes-presets-overview.md). Jeśli planujesz toocontrol które kodowania ustawienia wstępnego pamiętać to: koniecznie tooselect hello ustawienia wstępnego najbardziej odpowiednie dla wejściowego pliku wideo. Na przykład, jeśli znasz wejściowy plik wideo ma rozdzielczość 1920 x 1080 pikseli, następnie można hello "H264 szybkość transmisji bitów 1080p" wstępnie zdefiniowane. Jeśli wideo jest w niskiej rozdzielczości (640 x 360), nie używaj ustawienia wstępnego „Wielokrotna szybkość transmisji bitów H264 1080p”.
   
   Aby ułatwić zarządzanie istnieje możliwość edytowania hello nazwę zawartości wyjściowej hello i nazwę hello hello zadania.
   
   ![Kodowanie elementów zawartości](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. Kliknij przycisk **Utwórz**.

## <a name="next-step"></a>Następny krok
Można monitorować postępu zadania kodowania z hello portalu Azure, zgodnie z opisem w [to](media-services-portal-check-job-progress.md) artykułu.  

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

