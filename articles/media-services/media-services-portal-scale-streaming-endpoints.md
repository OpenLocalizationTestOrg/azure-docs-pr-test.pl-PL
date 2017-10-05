---
title: "Skala przesyłania strumieniowego punktów końcowych z portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki skalowanie punktów końcowych przesyłania strumieniowego przy użyciu portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 4bb891371e3fc802fa667688a88878db18e32422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a>Skalowanie punktów końcowych przesyłania strumieniowego przy użyciu witryny Azure Portal
## <a name="overview"></a>Omówienie

> [!NOTE]
> Do ukończenia tego samouczka jest potrzebne konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Punkty końcowe przesyłania strumieniowego **Premium** są odpowiednie w przypadku zaawansowanych obciążeń, ponieważ zapewniają dedykowaną i skalowalną pojemność przepustowości. Klienci, którzy mają punkt końcowy przesyłania strumieniowego **Premium**, domyślnie uzyskują jedną jednostkę przesyłania strumieniowego (SU, streaming unit). Punkt końcowy przesyłania strumieniowego można skalować poprzez dodawanie jednostek SU. Każdy jednostka SU zwiększa pojemność przepustowości aplikacji. Aby uzyskać więcej informacji na temat przesyłania strumieniowego i typy punktów końcowych usługi CDN konfiguracji, zobacz [omówienie punktu końcowego przesyłania strumieniowego](media-services-portal-manage-streaming-endpoints.md) tematu.
 
W tym temacie przedstawiono sposób skalowania punktu końcowego przesyłania strumieniowego.

Aby dowiedzieć się więcej o cenach, zobacz artykuł [Szczegółowe informacje o cenach usługi Media Services](http://go.microsoft.com/fwlink/?LinkId=275107).

## <a name="scale-streaming-endpoints"></a>Skalowanie punktów końcowych przesyłania strumieniowego

Aby zmienić liczbę jednostek przesyłania strumieniowego, wykonaj następujące czynności:

1. W witrynie [Azure Portal](https://portal.azure.com/) wybierz swoje konto usługi Azure Media Services.
2. W **ustawienia** wybierz **punkty końcowe przesyłania strumieniowego**.
3. Polecenie punktu końcowego przesyłania strumieniowego, który ma być skalowana. 

    [!NOTE] Można skalować tylko **Premium** punkty końcowe przesyłania strumieniowego.

4. Poruszając suwakiem, możesz określić liczbę jednostek przesyłania strumieniowego.

    ![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a>Następne kroki
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

