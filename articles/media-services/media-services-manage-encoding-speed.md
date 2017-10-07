---
title: "szybkość Zarządzaj aaa i współbieżność kodowania usłudze Azure Media Services | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera krótkie omówienie sposobu zarządzania szybkość i współbieżność kodowania zadań/zadań z usługi Azure Media Services."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>Zarządzanie szybkość i współbieżności z kodowaniem

Ten artykuł zawiera krótkie omówienie sposobu zarządzania szybkość i współbieżność zadań/zadania kodowania.

## <a name="overview"></a>Omówienie

W usłudze Media Services **typ jednostki zarezerwowane** określa szybkość hello przetwarzania zadania przetwarzania multimediów. Można wybrać między hello następujące typy jednostek zarezerwowanych: **S1**, **S2**, lub **S3**. Na przykład hello tego samego zadania kodowania działa szybciej, gdy używasz hello **S2** jednostka zarezerwowanego typ porównania toohello **S1** typu. Witaj [skalowania jednostki kodowania](media-services-scale-media-processing-overview.md) tematu zawiera tabelę, która ułatwia podjęcie decyzji, wybierając między różnych szybkościach kodowania.

Ponadto toospecifying hello zastrzeżone typ jednostki, można określić tooprovision Twojego konta z **jednostki zarezerwowanego**. Liczba Hello elastycznie jednostki zarezerwowanego określa hello liczbę zadań nośnika, które mogą być jednocześnie przetwarzane w ramach danego konta. Na przykład jeśli konto ma pięć jednostki zarezerwowanego, następnie nośnika pięć zadań będą uruchomione jednocześnie tak długo, jak istnieją toobe zadania przetwarzania. Witaj pozostałych zadań będzie czekać w kolejce hello i zostanie pobrana uzyskać przetwarzania sekwencyjnie, po zakończeniu uruchomione zadanie. Jeśli konto nie ma żadnych jednostek zarezerwowanego zainicjowano obsługę administracyjną, następnie zadania będą pobierane po kolei. W takim przypadku hello czas oczekiwania między jeden Kończenie zadań i hello uruchomienie kolejnej będzie zależeć od hello dostępność zasobów w systemie hello.

Aby uzyskać szczegółowe informacje i przykłady przedstawiające tooscale jednostki kodowania, zobacz temat [to](media-services-scale-media-processing-overview.md) tematu.

## <a name="next-step"></a>Następny krok

[Kodowania jednostki skalowania](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

