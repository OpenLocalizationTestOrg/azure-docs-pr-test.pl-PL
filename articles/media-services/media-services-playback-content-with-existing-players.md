---
title: "Korzystanie z istniejących odtwarzaczy do odtwarzania zawartości - Azure | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera listę istniejących odtwarzacze czy służy do odtwarzania zawartości."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 48f373b013b1192c353352b801876d706d91dd28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="playing-your-content-with-existing-players"></a><span data-ttu-id="a8999-103">Odtwarzanie zawartości z istniejących graczy</span><span class="sxs-lookup"><span data-stu-id="a8999-103">Playing your content with existing players</span></span>
<span data-ttu-id="a8999-104">Usługa Azure Media Services obsługuje wiele popularnych formatach przesyłania strumieniowego, takie jak Smooth Streaming, HTTP transmisji strumieniowej na żywo i MPEG-Dash.</span><span class="sxs-lookup"><span data-stu-id="a8999-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span></span> <span data-ttu-id="a8999-105">W tym temacie punktów do istniejących odtwarzaczy, których można użyć do testowania strumienie.</span><span class="sxs-lookup"><span data-stu-id="a8999-105">This topic points you to existing players that you can use to test your streams.</span></span>

### <a name="the-azure-portal-media-services-content-player"></a><span data-ttu-id="a8999-106">Azure portalu odtwarzacz zawartości Media Services</span><span class="sxs-lookup"><span data-stu-id="a8999-106">The Azure portal Media Services content player</span></span>
<span data-ttu-id="a8999-107">**Azure** portal udostępnia odtwarzacz zawartości, który służy do testowania pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="a8999-107">The **Azure** portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="a8999-108">Kliknij wybrany film wideo (Upewnij się, że został on [opublikowane](media-services-portal-publish.md)) i kliknij przycisk **odtwarzanie** przycisk w dolnej części portalu.</span><span class="sxs-lookup"><span data-stu-id="a8999-108">Click on the desired video (make sure it was [published](media-services-portal-publish.md)) and click the **Play** button at the bottom of the portal.</span></span>

<span data-ttu-id="a8999-109">Zagadnienia do rozważenia:</span><span class="sxs-lookup"><span data-stu-id="a8999-109">Some considerations apply:</span></span>

* <span data-ttu-id="a8999-110">**Odtwarzacz zawartości MEDIA SERVICES** odtwarza z domyślnego punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="a8999-110">The **MEDIA SERVICES CONTENT PLAYER** plays from the default streaming endpoint.</span></span> <span data-ttu-id="a8999-111">Do odtwarzania z punktu końcowego przesyłania strumieniowego innego niż domyślny należy użyć innego odtwarzacza</span><span class="sxs-lookup"><span data-stu-id="a8999-111">If you want to play from a non-default streaming endpoint, use another player.</span></span> <span data-ttu-id="a8999-112">Na przykład [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="a8999-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a><span data-ttu-id="a8999-114">Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="a8999-114">Azure Media Player</span></span>
<span data-ttu-id="a8999-115">Użyj [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) do odtwarzania zawartości (Wyczyść lub protected) w jednym z następujących formatów:</span><span class="sxs-lookup"><span data-stu-id="a8999-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to playback your content (clear or protected) in any of the following formats:</span></span>

* <span data-ttu-id="a8999-116">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="a8999-116">Smooth Streaming</span></span>
* <span data-ttu-id="a8999-117">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="a8999-117">MPEG DASH</span></span>
* <span data-ttu-id="a8999-118">HLS</span><span class="sxs-lookup"><span data-stu-id="a8999-118">HLS</span></span>
* <span data-ttu-id="a8999-119">MP4 progresywnego</span><span class="sxs-lookup"><span data-stu-id="a8999-119">Progressive MP4</span></span>

### <a name="flash-player"></a><span data-ttu-id="a8999-120">Flash Player</span><span class="sxs-lookup"><span data-stu-id="a8999-120">Flash Player</span></span>
#### <a name="aes-encrypted-with-token"></a><span data-ttu-id="a8999-121">Szyfrowania AES z tokenem</span><span class="sxs-lookup"><span data-stu-id="a8999-121">AES-encrypted with Token</span></span>
[<span data-ttu-id="a8999-122">http://aestoken.azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="a8999-122">http://aestoken.azurewebsites.net</span></span>](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a><span data-ttu-id="a8999-123">Odtwarzaczy programu Silverlight</span><span class="sxs-lookup"><span data-stu-id="a8999-123">Silverlight Players</span></span>
#### <a name="monitoring"></a><span data-ttu-id="a8999-124">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="a8999-124">Monitoring</span></span>
[<span data-ttu-id="a8999-125">http://SMF.cloudapp.NET/healthmonitor</span><span class="sxs-lookup"><span data-stu-id="a8999-125">http://smf.cloudapp.net/healthmonitor</span></span>](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a><span data-ttu-id="a8999-126">PlayReady z tokenem</span><span class="sxs-lookup"><span data-stu-id="a8999-126">PlayReady with Token</span></span>
[<span data-ttu-id="a8999-127">http://sltoken.azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="a8999-127">http://sltoken.azurewebsites.net</span></span>](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a><span data-ttu-id="a8999-128">Odtwarzacze kreska</span><span class="sxs-lookup"><span data-stu-id="a8999-128">DASH Players</span></span>
[<span data-ttu-id="a8999-129">http://dashplayer.azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="a8999-129">http://dashplayer.azurewebsites.net</span></span>](http://dashplayer.azurewebsites.net)

[<span data-ttu-id="a8999-130">http://dashif.org</span><span class="sxs-lookup"><span data-stu-id="a8999-130">http://dashif.org</span></span>](http://dashif.org)

### <a name="other"></a><span data-ttu-id="a8999-131">Inne</span><span class="sxs-lookup"><span data-stu-id="a8999-131">Other</span></span>
<span data-ttu-id="a8999-132">W celu przetestowania adresów URL HLS, można również użyć:</span><span class="sxs-lookup"><span data-stu-id="a8999-132">To test HLS URLs you can also use:</span></span>

* <span data-ttu-id="a8999-133">**Safari** na urządzeniu z systemem iOS lub</span><span class="sxs-lookup"><span data-stu-id="a8999-133">**Safari** on an iOS device or</span></span>
* <span data-ttu-id="a8999-134">**Odtwarzacz HLS 3ivx** w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="a8999-134">**3ivx HLS Player** on Windows.</span></span>

## <a name="developing-video-players"></a><span data-ttu-id="a8999-135">Tworzenie odtwarzaczy wideo</span><span class="sxs-lookup"><span data-stu-id="a8999-135">Developing video players</span></span>
<span data-ttu-id="a8999-136">Aby uzyskać informacje dotyczące sposobu tworzenia własnych odtwarzaczy, zobacz [opracowywanie odtwarzaczy wideo](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="a8999-136">For information about how to develop your own players, see [Developing video players](media-services-develop-video-players.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a8999-137">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="a8999-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a8999-138">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="a8999-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
