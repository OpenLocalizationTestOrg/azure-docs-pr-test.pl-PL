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
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a><span data-ttu-id="b60a8-103">Kodowanie elementu zawartości przy użyciu standardu Media Encoder Standard z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b60a8-103">Encode an asset using Media Encoder Standard with hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="b60a8-104">toocomplete tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b60a8-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="b60a8-105">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b60a8-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="b60a8-106">Podczas pracy w usłudze Azure Media Services jednym z hello najbardziej typowych scenariuszy jest dostarczanie przesyłania strumieniowego klientów tooyour adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="b60a8-106">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="b60a8-107">Usługa Media Services obsługuje hello następujące technologie przesyłania strumieniowego adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="b60a8-107">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="b60a8-108">tooprepare pliki wideo do przesyłania strumieniowego o adaptacyjnej szybkości bitowej, należy tooencode źródła wideo do plików o różnych szybkościach transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="b60a8-108">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="b60a8-109">Należy używać hello **Media Encoder Standard** tooencode koder wideo.</span><span class="sxs-lookup"><span data-stu-id="b60a8-109">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="b60a8-110">Media Services udostępnia również funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver Twojego MP4s wielokrotnej szybkości transmisji bitów w następujących formatów przesyłania strumieniowego hello: MPEG DASH, HLS, Smooth Streaming, bez konieczności toore pakietów w tych formatach.</span><span class="sxs-lookup"><span data-stu-id="b60a8-110">Media Services also provides dynamic packaging which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toore-package into these streaming formats.</span></span> <span data-ttu-id="b60a8-111">Dzięki funkcji dynamicznego tworzenia pakietów wystarczy toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services skompiluje oraz udostępni właściwą odpowiedź hello na podstawie żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="b60a8-111">With dynamic packaging you only need toostore and pay for hello files in single storage format and Media Services will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="b60a8-112">tootake korzyści z dynamicznego tworzenia pakietów, należy tooencode pliku źródłowego do zestawu plików MP4 wielokrotnej szybkości transmisji bitów (kroki kodowania hello przedstawiono w dalszej części tej sekcji).</span><span class="sxs-lookup"><span data-stu-id="b60a8-112">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="b60a8-113">media tooscale przetwarzania, zobacz [to](media-services-portal-scale-media-processing.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="b60a8-113">tooscale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-hello-azure-portal"></a><span data-ttu-id="b60a8-114">Kodowanie z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b60a8-114">Encode with hello Azure portal</span></span>
<span data-ttu-id="b60a8-115">W tej sekcji opisano kroki hello może zająć tooencode zawartości przy użyciu standardu Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="b60a8-115">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="b60a8-116">W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="b60a8-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="b60a8-117">W hello **ustawienia** wybierz **zasoby**.</span><span class="sxs-lookup"><span data-stu-id="b60a8-117">In hello **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="b60a8-118">W hello **zasoby** okna, wybierz hello zasobów chcesz tooencode.</span><span class="sxs-lookup"><span data-stu-id="b60a8-118">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
4. <span data-ttu-id="b60a8-119">Naciśnij klawisz hello **Koduj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b60a8-119">Press hello **Encode** button.</span></span>
5. <span data-ttu-id="b60a8-120">W hello **kodowanie elementu zawartości** okna, hello wybierz procesor "Media Encoder Standard" oraz ustawienie wstępne.</span><span class="sxs-lookup"><span data-stu-id="b60a8-120">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="b60a8-121">Aby uzyskać informacje o ustawieniach wstępnych, zobacz [Automatyczne generowanie drabiny szybkości transmisji bitów](media-services-autogen-bitrate-ladder-with-mes.md) i [Ustawienia wstępne zadań usługi MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b60a8-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="b60a8-122">Jeśli planujesz toocontrol które kodowania ustawienia wstępnego pamiętać to: koniecznie tooselect hello ustawienia wstępnego najbardziej odpowiednie dla wejściowego pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="b60a8-122">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="b60a8-123">Na przykład, jeśli znasz wejściowy plik wideo ma rozdzielczość 1920 x 1080 pikseli, następnie można hello "H264 szybkość transmisji bitów 1080p" wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="b60a8-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="b60a8-124">Jeśli wideo jest w niskiej rozdzielczości (640 x 360), nie używaj ustawienia wstępnego „Wielokrotna szybkość transmisji bitów H264 1080p”.</span><span class="sxs-lookup"><span data-stu-id="b60a8-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="b60a8-125">Aby ułatwić zarządzanie istnieje możliwość edytowania hello nazwę zawartości wyjściowej hello i nazwę hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="b60a8-125">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Kodowanie elementów zawartości](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="b60a8-127">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b60a8-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="b60a8-128">Następny krok</span><span class="sxs-lookup"><span data-stu-id="b60a8-128">Next step</span></span>
<span data-ttu-id="b60a8-129">Można monitorować postępu zadania kodowania z hello portalu Azure, zgodnie z opisem w [to](media-services-portal-check-job-progress.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b60a8-129">You can monitor encoding job progress with hello Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="b60a8-130">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="b60a8-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b60a8-131">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="b60a8-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

