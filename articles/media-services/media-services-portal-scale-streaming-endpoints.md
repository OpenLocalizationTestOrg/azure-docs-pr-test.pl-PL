---
title: "punkty końcowe z portalu Azure hello przesyłania strumieniowego aaaScale | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki hello skalowanie punktów końcowych przesyłania strumieniowego z hello portalu Azure."
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
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a>Skalowanie punktów końcowych przesyłania strumieniowego z hello portalu Azure
## <a name="overview"></a>Omówienie

> [!NOTE]
> toocomplete tego samouczka jest potrzebne konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Punkty końcowe przesyłania strumieniowego **Premium** są odpowiednie w przypadku zaawansowanych obciążeń, ponieważ zapewniają dedykowaną i skalowalną pojemność przepustowości. Klienci, którzy mają punkt końcowy przesyłania strumieniowego **Premium**, domyślnie uzyskują jedną jednostkę przesyłania strumieniowego (SU, streaming unit). Witaj punktu końcowego przesyłania strumieniowego można skalować, dodając SUs. Każdy SU udostępnia dodatkowe ograniczenie użycia przepustowości pojemności toohello aplikacji. Aby uzyskać więcej informacji na temat przesyłania strumieniowego i typy punktów końcowych usługi CDN konfiguracji, zobacz hello [omówienie punktu końcowego przesyłania strumieniowego](media-services-portal-manage-streaming-endpoints.md) tematu.
 
W tym temacie przedstawiono sposób tooscale punktu końcowego przesyłania strumieniowego.

Aby dowiedzieć się więcej o cenach, zobacz artykuł [Szczegółowe informacje o cenach usługi Media Services](http://go.microsoft.com/fwlink/?LinkId=275107).

## <a name="scale-streaming-endpoints"></a>Skalowanie punktów końcowych przesyłania strumieniowego

toochange hello liczbę jednostek przesyłania strumieniowego, hello następujące:

1. W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.
2. W hello **ustawienia** wybierz **punkty końcowe przesyłania strumieniowego**.
3. Kliknij punkt końcowy przesyłania strumieniowego hello, które mają tooscale. 

    [!NOTE] Można skalować tylko **Premium** punkty końcowe przesyłania strumieniowego.

4. Przenieś hello suwaka toospecify hello liczbę jednostek przesyłania strumieniowego.

    ![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a>Następne kroki
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

