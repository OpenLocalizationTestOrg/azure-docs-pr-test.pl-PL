---
title: "Kodowanie elementu zawartości przy użyciu standardu Media Encoder Standard z portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki kodowania zasobów przy użyciu standardu Media Encoder Standard z portalu Azure."
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
ms.openlocfilehash: a299245e285c4caa68988b184799cd6f4d13e080
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-the-azure-portal"></a>Kodowanie elementu zawartości przy użyciu standardu Media Encoder Standard z portalu Azure
> [!NOTE]
> Do ukończenia tego samouczka jest potrzebne konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Podczas pracy w usłudze Azure Media Services jednym z najbardziej typowych scenariuszy jest zapewnianie klientom przesyłania strumieniowego z adaptacyjną szybkością transmisji bitów. Usługa Media Services obsługuje następujące technologie przesyłania strumieniowego z adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming i MPEG DASH. Aby przygotować pliki wideo do przesyłania strumieniowego z adaptacyjną szybkością transmisji bitów, należy zakodować źródłowy plik wideo do plików o różnej szybkości transmisji bitów. Do kodowania plików wideo należy używać kodera **Media Encoder Standard**.  

Usługa Media Services udostępnia również funkcję dynamicznego tworzenia pakietów, która pozwala dostarczać MP4s Twojego wielokrotnej szybkości transmisji bitów w formatach przesyłania strumieniowego: MPEG DASH, HLS, Smooth Streaming, bez konieczności ponownego tworzenia pakietów w tych formatach. Dzięki funkcji dynamicznego tworzenia pakietów wystarczy przechowywać i opłacać pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź na podstawie żądań klienta.

Aby korzystać z dynamicznego tworzenia pakietów, wykonaj kodowanie pliku źródłowego do zestawu plików MP4 o różnej szybkości transmisji bitów (kroki kodowania przedstawiono w dalszej części tej sekcji).

Aby skalować przetwarzania nośnika, zobacz [to](media-services-portal-scale-media-processing.md) tematu.

## <a name="encode-with-the-azure-portal"></a>Kodowanie przy użyciu portalu Azure
W tej sekcji opisano kroki, które należy wykonać w celu zakodowania zawartości przy użyciu standardu Media Encoder Standard.

1. W witrynie [Azure Portal](https://portal.azure.com/) wybierz swoje konto usługi Azure Media Services.
2. W oknie **Ustawienia** wybierz opcję **Elementy zawartości**.  
3. W oknie **Elementy zawartości** wybierz element zawartości, który chcesz kodować.
4. Kliknij przycisk **Koduj**.
5. W oknie **Kodowanie elementu zawartości** wybierz procesor „Media Encoder Standard” oraz ustawienie wstępne. Aby uzyskać informacje o ustawieniach wstępnych, zobacz [Automatyczne generowanie drabiny szybkości transmisji bitów](media-services-autogen-bitrate-ladder-with-mes.md) i [Ustawienia wstępne zadań usługi MES](media-services-mes-presets-overview.md). Jeśli zamierzasz kontrolować, które ustawienie wstępne jest używane, pamiętaj, aby wybrać ustawienie wstępne, które jest najbardziej odpowiednie dla danego wejściowego pliku wideo. Na przykład: jeśli wejściowy plik wideo ma rozdzielczość 1920 x 1080 pikseli, można użyć ustawienia wstępnego „Wielokrotna szybkość transmisji bitów H264 1080p”. Jeśli wideo jest w niskiej rozdzielczości (640 x 360), nie używaj ustawienia wstępnego „Wielokrotna szybkość transmisji bitów H264 1080p”.
   
   Aby ułatwić zarządzanie istnieje możliwość edytowania nazwy wyjściowego elementu zawartości oraz nazwy zadania.
   
   ![Kodowanie elementów zawartości](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. Kliknij przycisk **Utwórz**.

## <a name="next-step"></a>Następny krok
Można monitorować postępu zadania kodowania w portalu Azure, zgodnie z opisem w [to](media-services-portal-check-job-progress.md) artykułu.  

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

