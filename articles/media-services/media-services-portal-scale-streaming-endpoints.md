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
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="5a6e7-103">Skalowanie punktów końcowych przesyłania strumieniowego przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5a6e7-103">Scale streaming endpoints with the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="5a6e7-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5a6e7-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="5a6e7-105">Do ukończenia tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="5a6e7-106">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a6e7-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="5a6e7-107">Punkty końcowe przesyłania strumieniowego **Premium** są odpowiednie w przypadku zaawansowanych obciążeń, ponieważ zapewniają dedykowaną i skalowalną pojemność przepustowości.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="5a6e7-108">Klienci, którzy mają punkt końcowy przesyłania strumieniowego **Premium**, domyślnie uzyskują jedną jednostkę przesyłania strumieniowego (SU, streaming unit).</span><span class="sxs-lookup"><span data-stu-id="5a6e7-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="5a6e7-109">Punkt końcowy przesyłania strumieniowego można skalować poprzez dodawanie jednostek SU.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-109">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="5a6e7-110">Każdy jednostka SU zwiększa pojemność przepustowości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-110">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="5a6e7-111">Aby uzyskać więcej informacji na temat przesyłania strumieniowego i typy punktów końcowych usługi CDN konfiguracji, zobacz [omówienie punktu końcowego przesyłania strumieniowego](media-services-portal-manage-streaming-endpoints.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-111">For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="5a6e7-112">W tym temacie przedstawiono sposób skalowania punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-112">This topic shows how to scale a streaming endpoint.</span></span>

<span data-ttu-id="5a6e7-113">Aby dowiedzieć się więcej o cenach, zobacz artykuł [Szczegółowe informacje o cenach usługi Media Services](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="5a6e7-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="5a6e7-114">Skalowanie punktów końcowych przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="5a6e7-114">Scale streaming endpoints</span></span>

<span data-ttu-id="5a6e7-115">Aby zmienić liczbę jednostek przesyłania strumieniowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5a6e7-115">To change the number of streaming units, do the following:</span></span>

1. <span data-ttu-id="5a6e7-116">W witrynie [Azure Portal](https://portal.azure.com/) wybierz swoje konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="5a6e7-117">W **ustawienia** wybierz **punkty końcowe przesyłania strumieniowego**.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-117">In the **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="5a6e7-118">Polecenie punktu końcowego przesyłania strumieniowego, który ma być skalowana.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-118">Click on the streaming endpoint that you want to scale.</span></span> 

    [!NOTE] <span data-ttu-id="5a6e7-119">Można skalować tylko **Premium** punkty końcowe przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="5a6e7-120">Poruszając suwakiem, możesz określić liczbę jednostek przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-120">Move the slider to specify the number of streaming units.</span></span>

    ![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="5a6e7-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5a6e7-122">Next steps</span></span>
<span data-ttu-id="5a6e7-123">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="5a6e7-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5a6e7-124">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="5a6e7-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

