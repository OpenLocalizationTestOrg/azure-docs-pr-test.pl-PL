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
# <a name="encode-an-asset-using-media-encoder-standard-with-the-azure-portal"></a><span data-ttu-id="24fa5-103">Kodowanie elementu zawartości przy użyciu standardu Media Encoder Standard z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="24fa5-103">Encode an asset using Media Encoder Standard with the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="24fa5-104">Do ukończenia tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="24fa5-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="24fa5-105">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24fa5-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="24fa5-106">Podczas pracy w usłudze Azure Media Services jednym z najbardziej typowych scenariuszy jest zapewnianie klientom przesyłania strumieniowego z adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="24fa5-106">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="24fa5-107">Usługa Media Services obsługuje następujące technologie przesyłania strumieniowego z adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming i MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="24fa5-107">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="24fa5-108">Aby przygotować pliki wideo do przesyłania strumieniowego z adaptacyjną szybkością transmisji bitów, należy zakodować źródłowy plik wideo do plików o różnej szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="24fa5-108">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="24fa5-109">Do kodowania plików wideo należy używać kodera **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="24fa5-109">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="24fa5-110">Usługa Media Services udostępnia również funkcję dynamicznego tworzenia pakietów, która pozwala dostarczać MP4s Twojego wielokrotnej szybkości transmisji bitów w formatach przesyłania strumieniowego: MPEG DASH, HLS, Smooth Streaming, bez konieczności ponownego tworzenia pakietów w tych formatach.</span><span class="sxs-lookup"><span data-stu-id="24fa5-110">Media Services also provides dynamic packaging which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to re-package into these streaming formats.</span></span> <span data-ttu-id="24fa5-111">Dzięki funkcji dynamicznego tworzenia pakietów wystarczy przechowywać i opłacać pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź na podstawie żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="24fa5-111">With dynamic packaging you only need to store and pay for the files in single storage format and Media Services will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="24fa5-112">Aby korzystać z dynamicznego tworzenia pakietów, wykonaj kodowanie pliku źródłowego do zestawu plików MP4 o różnej szybkości transmisji bitów (kroki kodowania przedstawiono w dalszej części tej sekcji).</span><span class="sxs-lookup"><span data-stu-id="24fa5-112">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="24fa5-113">Aby skalować przetwarzania nośnika, zobacz [to](media-services-portal-scale-media-processing.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="24fa5-113">To scale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-the-azure-portal"></a><span data-ttu-id="24fa5-114">Kodowanie przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="24fa5-114">Encode with the Azure portal</span></span>
<span data-ttu-id="24fa5-115">W tej sekcji opisano kroki, które należy wykonać w celu zakodowania zawartości przy użyciu standardu Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="24fa5-115">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="24fa5-116">W witrynie [Azure Portal](https://portal.azure.com/) wybierz swoje konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="24fa5-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="24fa5-117">W oknie **Ustawienia** wybierz opcję **Elementy zawartości**.</span><span class="sxs-lookup"><span data-stu-id="24fa5-117">In the **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="24fa5-118">W oknie **Elementy zawartości** wybierz element zawartości, który chcesz kodować.</span><span class="sxs-lookup"><span data-stu-id="24fa5-118">In the **Assets** window, select the asset that you would like to encode.</span></span>
4. <span data-ttu-id="24fa5-119">Kliknij przycisk **Koduj**.</span><span class="sxs-lookup"><span data-stu-id="24fa5-119">Press the **Encode** button.</span></span>
5. <span data-ttu-id="24fa5-120">W oknie **Kodowanie elementu zawartości** wybierz procesor „Media Encoder Standard” oraz ustawienie wstępne.</span><span class="sxs-lookup"><span data-stu-id="24fa5-120">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="24fa5-121">Aby uzyskać informacje o ustawieniach wstępnych, zobacz [Automatyczne generowanie drabiny szybkości transmisji bitów](media-services-autogen-bitrate-ladder-with-mes.md) i [Ustawienia wstępne zadań usługi MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24fa5-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="24fa5-122">Jeśli zamierzasz kontrolować, które ustawienie wstępne jest używane, pamiętaj, aby wybrać ustawienie wstępne, które jest najbardziej odpowiednie dla danego wejściowego pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="24fa5-122">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="24fa5-123">Na przykład: jeśli wejściowy plik wideo ma rozdzielczość 1920 x 1080 pikseli, można użyć ustawienia wstępnego „Wielokrotna szybkość transmisji bitów H264 1080p”.</span><span class="sxs-lookup"><span data-stu-id="24fa5-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="24fa5-124">Jeśli wideo jest w niskiej rozdzielczości (640 x 360), nie używaj ustawienia wstępnego „Wielokrotna szybkość transmisji bitów H264 1080p”.</span><span class="sxs-lookup"><span data-stu-id="24fa5-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="24fa5-125">Aby ułatwić zarządzanie istnieje możliwość edytowania nazwy wyjściowego elementu zawartości oraz nazwy zadania.</span><span class="sxs-lookup"><span data-stu-id="24fa5-125">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Kodowanie elementów zawartości](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="24fa5-127">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="24fa5-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="24fa5-128">Następny krok</span><span class="sxs-lookup"><span data-stu-id="24fa5-128">Next step</span></span>
<span data-ttu-id="24fa5-129">Można monitorować postępu zadania kodowania w portalu Azure, zgodnie z opisem w [to](media-services-portal-check-job-progress.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="24fa5-129">You can monitor encoding job progress with the Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="24fa5-130">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="24fa5-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="24fa5-131">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="24fa5-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

