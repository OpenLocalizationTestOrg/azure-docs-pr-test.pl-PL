---
title: "pliki aaaUpload do konta usługi Azure Media Services z Azure StorSimple | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera krótkie omówienie usługi Azure StorSimple Data Manager. Artykuł Hello zawiera również linki tootutorials, który przedstawia sposób tooextract danych z StorSimple i przekaż go jako tooan zasobów konta usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a>Przekazywanie plików na konto usługi Azure Media Services z rozwiązania Azure StorSimple

Ten artykuł zawiera krótkie omówienie usługi Azure StorSimple Data Manager. Artykuł Hello zawiera również linki tootutorials, który przedstawia sposób tooextract danych z StorSimple i przekazać te dane jako tooan zasobów konta usługi Azure Media Services (AMS).

> 
> [!NOTE]
> Usługa Azure StorSimple Data Manager jest obecnie dostępna w prywatnej wersji zapoznawczej. 
> 

## <a name="overview"></a>Omówienie

Za pomocą usługi Media Services można przekazać pliki cyfrowe do elementu zawartości. Witaj zasobów może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżek i napisów plików (i hello metadane dotyczące tych plików.) Po przekazaniu plików hello zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.

[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) używa magazynu w chmurze jako rozszerzenie hello lokalnego rozwiązania i automatycznie warstwy danych przez Magazyn lokalne powitania i magazynu w chmurze. urządzenie StorSimple Hello dedupes i kompresuje dane przed wysłaniem toohello chmury, dzięki czemu bardzo wydajny wysyłania dużych plików toohello chmury. Witaj [Menedżer StorSimple danych](../storsimple/storsimple-data-manager-overview.md) usługi udostępnia interfejsy API, Włącz możesz tooextract danych z StorSimple i prezentować jako zasoby AMS.

## <a name="get-started"></a>Rozpoczęcie pracy

1. [Utwórz konto usługi Media Services](media-services-portal-create-account.md) do którego będzie tootransfer hello zasoby.
2. Załóż Data Manager w wersji zapoznawczej, zgodnie z opisem w hello [Menedżer StorSimple danych](../storsimple/storsimple-data-manager-overview.md) artykułu.
3. Utwórz konto usługi StorSimple Data Manager.
4. Utwórz zadanie przekształcania danych, które po uruchomieniu wyodrębnia dane z urządzenia StorSimple i przekazuje je na konto usługi AMS jako elementy zawartości. 

    Po uruchomieniu zadania hello systemem kolejki magazynu jest tworzony. Jest ona wypełniana przy użyciu komunikatów dotyczących przekształconych obiektów blob, gdy będą gotowe. Nazwa Hello tej kolejki jest hello taka sama jak nazwa hello hello definicji zadania. Można użyć tej kolejki toodetermine po zawartości jest gotowe i wywołać z żądaną toorun operacji usługi Media Services. Na przykład można użyć tej kolejki tootrigger funkcji platformy Azure, która ma hello niezbędne usługi Media Services kodu w nim.

## <a name="see-also"></a>Zobacz też

[Użyj hello .net SDK tootrigger zadania w hello Data Manager](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Następne kroki

Teraz możesz zakodować przekazane elementy zawartości. Więcej informacji znajduje się na stronie [Kodowanie elementów zawartości](media-services-portal-encode.md).
