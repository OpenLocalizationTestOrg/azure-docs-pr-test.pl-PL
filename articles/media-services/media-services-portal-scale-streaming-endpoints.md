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
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="acd34-103">Skalowanie punktów końcowych przesyłania strumieniowego z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="acd34-103">Scale streaming endpoints with hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="acd34-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="acd34-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="acd34-105">toocomplete tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="acd34-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="acd34-106">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="acd34-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="acd34-107">Punkty końcowe przesyłania strumieniowego **Premium** są odpowiednie w przypadku zaawansowanych obciążeń, ponieważ zapewniają dedykowaną i skalowalną pojemność przepustowości.</span><span class="sxs-lookup"><span data-stu-id="acd34-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="acd34-108">Klienci, którzy mają punkt końcowy przesyłania strumieniowego **Premium**, domyślnie uzyskują jedną jednostkę przesyłania strumieniowego (SU, streaming unit).</span><span class="sxs-lookup"><span data-stu-id="acd34-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="acd34-109">Witaj punktu końcowego przesyłania strumieniowego można skalować, dodając SUs.</span><span class="sxs-lookup"><span data-stu-id="acd34-109">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="acd34-110">Każdy SU udostępnia dodatkowe ograniczenie użycia przepustowości pojemności toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="acd34-110">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="acd34-111">Aby uzyskać więcej informacji na temat przesyłania strumieniowego i typy punktów końcowych usługi CDN konfiguracji, zobacz hello [omówienie punktu końcowego przesyłania strumieniowego](media-services-portal-manage-streaming-endpoints.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="acd34-111">For more information about streaming endpoint types and CDN configuration, see hello [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="acd34-112">W tym temacie przedstawiono sposób tooscale punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="acd34-112">This topic shows how tooscale a streaming endpoint.</span></span>

<span data-ttu-id="acd34-113">Aby dowiedzieć się więcej o cenach, zobacz artykuł [Szczegółowe informacje o cenach usługi Media Services](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="acd34-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="acd34-114">Skalowanie punktów końcowych przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="acd34-114">Scale streaming endpoints</span></span>

<span data-ttu-id="acd34-115">toochange hello liczbę jednostek przesyłania strumieniowego, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="acd34-115">toochange hello number of streaming units, do hello following:</span></span>

1. <span data-ttu-id="acd34-116">W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="acd34-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="acd34-117">W hello **ustawienia** wybierz **punkty końcowe przesyłania strumieniowego**.</span><span class="sxs-lookup"><span data-stu-id="acd34-117">In hello **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="acd34-118">Kliknij punkt końcowy przesyłania strumieniowego hello, które mają tooscale.</span><span class="sxs-lookup"><span data-stu-id="acd34-118">Click on hello streaming endpoint that you want tooscale.</span></span> 

    [!NOTE] <span data-ttu-id="acd34-119">Można skalować tylko **Premium** punkty końcowe przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="acd34-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="acd34-120">Przenieś hello suwaka toospecify hello liczbę jednostek przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="acd34-120">Move hello slider toospecify hello number of streaming units.</span></span>

    ![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="acd34-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="acd34-122">Next steps</span></span>
<span data-ttu-id="acd34-123">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="acd34-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="acd34-124">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="acd34-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

