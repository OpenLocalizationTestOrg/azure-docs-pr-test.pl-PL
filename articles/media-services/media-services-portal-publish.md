---
title: "AAA\"publikowania zawartości za pomocą hello portalu Azure | Dokumentacja firmy Microsoft\""
description: "Ten samouczek przedstawia kroki hello publikowania zawartości przy użyciu hello portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a><span data-ttu-id="93d69-103">Publikowanie zawartości z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="93d69-103">Publish content with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="93d69-104">Portal</span><span class="sxs-lookup"><span data-stu-id="93d69-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="93d69-105">.NET</span><span class="sxs-lookup"><span data-stu-id="93d69-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="93d69-106">REST</span><span class="sxs-lookup"><span data-stu-id="93d69-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="93d69-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="93d69-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="93d69-108">toocomplete tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="93d69-108">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="93d69-109">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93d69-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="93d69-110">tooprovide użytkownika przy użyciu adresu URL, który może być używane toostream lub pobierania zawartości, należy najpierw należy zbyt "Publikuj" zawartości, tworząc Lokalizator.</span><span class="sxs-lookup"><span data-stu-id="93d69-110">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="93d69-111">Lokalizatory zapewniają toofiles dostępu do zawartych w hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="93d69-111">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="93d69-112">Usługa Media Services obsługuje dwa typy lokalizatorów:</span><span class="sxs-lookup"><span data-stu-id="93d69-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="93d69-113">Przesyłanie strumieniowe lokalizatory (OnDemandOrigin) używane do adaptacyjnego przesyłania strumieniowego (na przykład toostream MPEG DASH, HLS lub Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="93d69-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="93d69-114">toocreate Lokalizator przesyłania strumieniowego zawartości musi zawierać plik .ism.</span><span class="sxs-lookup"><span data-stu-id="93d69-114">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="93d69-115">Progresywne lokalizatory (SAS) używane do dostarczania plików wideo przy użyciu pobierania progresywnego.</span><span class="sxs-lookup"><span data-stu-id="93d69-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="93d69-116">Adresu URL przesyłania strumieniowego ma hello zgodny z formatem i może być używany tooplay Smooth Streaming zasoby.</span><span class="sxs-lookup"><span data-stu-id="93d69-116">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="93d69-117">Dołącz toobuild jako HLS URL, przesyłania strumieniowego (format = m3u8-aapl) toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="93d69-117">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="93d69-118">Dołącz toobuild jako MPEG DASH URL, przesyłania strumieniowego (format = mpd-time-csf) toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="93d69-118">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="93d69-119">Adres URL SAS ma hello zgodny z formatem.</span><span class="sxs-lookup"><span data-stu-id="93d69-119">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="93d69-120">Aby uzyskać więcej informacji, zobacz [dostarczanie zawartości omówienie](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93d69-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="93d69-121">Jeśli używasz hello portalu toocreate lokalizatorów przed marcem 2015 r., zostały utworzone lokalizatory z dwuletnim okresem ważności.</span><span class="sxs-lookup"><span data-stu-id="93d69-121">If you used hello portal toocreate locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="93d69-122">tooupdate Data wygaśnięcia na lokalizatorze użyj [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) lub [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="93d69-122">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="93d69-123">Należy pamiętać, że po zaktualizowaniu hello daty wygaśnięcia lokalizatora SAS następuje zmiana adresu URL hello.</span><span class="sxs-lookup"><span data-stu-id="93d69-123">Note that when you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="93d69-124">toouse hello portalu toopublish zasobów</span><span class="sxs-lookup"><span data-stu-id="93d69-124">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="93d69-125">toouse hello portalu toopublish zasobów hello następujące:</span><span class="sxs-lookup"><span data-stu-id="93d69-125">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="93d69-126">W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="93d69-126">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="93d69-127">Wybierz kolejno pozycje **Ustawienia** > **Elementy zawartości**.</span><span class="sxs-lookup"><span data-stu-id="93d69-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="93d69-128">Wybierz hello zasobów, które mają toopublish.</span><span class="sxs-lookup"><span data-stu-id="93d69-128">Select hello asset that you want toopublish.</span></span>
4. <span data-ttu-id="93d69-129">Kliknij przycisk hello **publikowania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="93d69-129">Click hello **Publish** button.</span></span>
5. <span data-ttu-id="93d69-130">Wybierz typ lokalizatora hello.</span><span class="sxs-lookup"><span data-stu-id="93d69-130">Select hello locator type.</span></span>
6. <span data-ttu-id="93d69-131">Kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="93d69-131">Press **Add**.</span></span>
   
    ![Publikowanie](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="93d69-133">adres URL Hello zostanie dodany toohello listę **publikowane adresy URL**.</span><span class="sxs-lookup"><span data-stu-id="93d69-133">hello URL will be added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="93d69-134">Odtwarzanie zawartości z portalu hello</span><span class="sxs-lookup"><span data-stu-id="93d69-134">Play content from hello portal</span></span>
<span data-ttu-id="93d69-135">Witaj Azure portal udostępnia odtwarzacz zawartości możesz za pomocą tootest wideo.</span><span class="sxs-lookup"><span data-stu-id="93d69-135">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="93d69-136">Kliknij żądany hello wideo, a następnie kliknij przycisk hello **odtwarzanie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="93d69-136">Click hello desired video and then click hello **Play** button.</span></span>

![Publikowanie](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="93d69-138">Zagadnienia do rozważenia:</span><span class="sxs-lookup"><span data-stu-id="93d69-138">Some considerations apply:</span></span>

* <span data-ttu-id="93d69-139">Upewnij się, że hello wideo został opublikowany.</span><span class="sxs-lookup"><span data-stu-id="93d69-139">Make sure hello video has been published.</span></span>
* <span data-ttu-id="93d69-140">To **Media player** odtwarza z domyślnego hello punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="93d69-140">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="93d69-141">Jeśli chcesz, aby tooplay z innych niż domyślne przesyłania strumieniowego punktu końcowego, kliknij adres URL hello toocopy i użyć innego odtwarzacza.</span><span class="sxs-lookup"><span data-stu-id="93d69-141">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="93d69-142">(np. [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)).</span><span class="sxs-lookup"><span data-stu-id="93d69-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="93d69-143">Witaj, z którego są przesyłania strumieniowego punktu końcowego przesyłania strumieniowego musi być uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="93d69-143">hello streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="93d69-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="93d69-144">Next steps</span></span>
<span data-ttu-id="93d69-145">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="93d69-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="93d69-146">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="93d69-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

