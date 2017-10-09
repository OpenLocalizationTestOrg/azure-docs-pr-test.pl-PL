---
title: "przetwarzanie przy użyciu nośnika aaaScale hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki hello nośnika skalowania przetwarzania przy użyciu hello portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a>Typ jednostki zmiany hello zastrzeżone
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portal](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Omówienie

Konto usługi Media Services jest skojarzony z zarezerwowanych typu jednostki, który określa szybkość hello przetwarzania zadania przetwarzania multimediów. Można wybrać między hello następujące typy jednostek zarezerwowanych: **S1**, **S2**, lub **S3**. Na przykład hello tego samego zadania kodowania działa szybciej, gdy używasz hello **S2** jednostka zarezerwowanego typ porównania toohello **S1** typu.

Ponadto toospecifying hello zastrzeżone typ jednostki, można określić tooprovision Twojego konta z **jednostki zarezerwowanego** (RUs). Liczba Hello elastycznie RUs określa hello liczbę zadań nośnika, które mogą być jednocześnie przetwarzane w ramach danego konta.

>[!NOTE]
>Jednostki zarezerwowane przekształcają wszystkie operacje przetwarzania multimediów do postaci równoległej, uwzględniając zadania Indeksowania za pomocą usługi Azure Media Indexer. Jednak w przeciwieństwie do kodowania zadania indeksowania nie są przetwarzane szybciej przy użyciu szybszych jednostek zarezerwowanych.

> [!IMPORTANT]
> Upewnij się, że hello tooreview [omówienie](media-services-scale-media-processing-overview.md) tooget tematu więcej informacji na temat skalowania przetwarzania tematu nośnika.
> 
> 

## <a name="scale-media-processing"></a>Skalowanie przetwarzania multimediów
toochange hello zastrzeżone jednostki typu i hello liczbę jednostek zarezerwowanego hello następujące:

1. W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.
2. W hello **ustawienia** wybierz **jednostki zarezerwowane multimediów**.
   
    toochange hello liczba zarezerwowanych jednostek hello wybranego typu jednostka zarezerwowanego, użyj hello **jednostki obsługiwanej nośnika** suwaka.
   
    Witaj toochange **typ jednostki zarezerwowane**, naciśnij klawisz S1, S2 lub S3.
   
    ![Strona procesorów](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. Naciśnij klawisz hello ZAPISAĆ toosave przycisk zmiany.
   
    nowe jednostki zarezerwowanego Hello są przydzielane po naciśnięciu ZAPISZ.

## <a name="next-steps"></a>Następne kroki
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

