---
title: "często zadawane pytania dotyczące usługi Media Services aaaAzure | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania (FAQ)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="64b38-103">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="64b38-103">Frequently asked questions</span></span>

<span data-ttu-id="64b38-104">W tym artykule opisano często zadawane pytania zgłoszone przez społeczność użytkowników programu hello Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="64b38-104">This article addresses frequently asked questions raised by hello Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="64b38-105">Często zadawane pytania ogólne AMS</span><span class="sxs-lookup"><span data-stu-id="64b38-105">General AMS FAQs</span></span>
<span data-ttu-id="64b38-106">Pytanie: jak można skalować, indeksowania?</span><span class="sxs-lookup"><span data-stu-id="64b38-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="64b38-107">A: jednostki zarezerwowane hello są hello tego samego kodowanie i zadania indeksowania.</span><span class="sxs-lookup"><span data-stu-id="64b38-107">A: hello reserved units are hello same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="64b38-108">Postępuj zgodnie z instrukcjami wyświetlanymi [jak tooScale kodowanie jednostki zarezerwowanego](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64b38-108">Follow instructions on [How tooScale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="64b38-109">**Uwaga** czy wydajność indeksatora nie ma wpływu na typ jednostki zarezerwowane.</span><span class="sxs-lookup"><span data-stu-id="64b38-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="64b38-110">Pytanie: I przekazany, zakodowany i publikowane wideo.</span><span class="sxs-lookup"><span data-stu-id="64b38-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="64b38-111">Jakie byłyby hello Przyczyna hello wideo nie jest odtwarzany podczas toostream go?</span><span class="sxs-lookup"><span data-stu-id="64b38-111">What would be hello reason hello video does not play when I try toostream it?</span></span>

<span data-ttu-id="64b38-112">Odpowiedź: jeden hello najczęściej powodów, dla których jest hello, z którym próbujesz tooplayback w hello punktu końcowego przesyłania strumieniowego nie ma **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="64b38-112">A: One of hello most common reasons is you do not have hello streaming endpoint from which you are trying tooplayback in hello **Running** state.</span></span>  

<span data-ttu-id="64b38-113">Pytanie: czy można składania na strumień na żywo?</span><span class="sxs-lookup"><span data-stu-id="64b38-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="64b38-114">A: składania na strumienie na żywo aktualnie nie jest oferowany usługi Azure Media Services, więc musisz toopre-tworzą na komputerze.</span><span class="sxs-lookup"><span data-stu-id="64b38-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need toopre-compose on your computer.</span></span>

<span data-ttu-id="64b38-115">Pytanie: czy za pomocą usługi Azure CDN transmisji strumieniowej na żywo?</span><span class="sxs-lookup"><span data-stu-id="64b38-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="64b38-116">Odpowiedź: Media Services obsługuje integrację z usługą Azure CDN (Aby uzyskać więcej informacji, zobacz [jak punkty końcowe przesyłania strumieniowego tooManage w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="64b38-116">A: Media Services supports integration with Azure CDN (for more information, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="64b38-117">Możesz użyć Live streaming sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="64b38-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="64b38-118">Azure Media Services udostępnia Smooth Streaming, HLS i MPEG-DASH danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="64b38-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="64b38-119">Wszystkie te formaty do przesyłania danych za pomocą protokołu HTTP i uzyskać korzyści buforowania HTTP.</span><span class="sxs-lookup"><span data-stu-id="64b38-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="64b38-120">Na żywo, przesyłania strumieniowego audio/wideo dane jest podzielony toofragments i to poszczególne fragmenty pobrać buforowane w sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="64b38-120">In live streaming actual video/audio data is divided toofragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="64b38-121">Tylko dane potrzeb toobe odświeżyć jest hello manifestu danych.</span><span class="sxs-lookup"><span data-stu-id="64b38-121">Only data needs toobe refreshed is hello manifest data.</span></span> <span data-ttu-id="64b38-122">CDN okresowo odświeża dane manifestu.</span><span class="sxs-lookup"><span data-stu-id="64b38-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="64b38-123">Pytanie: jest usługa Azure Media services obsługuje przechowywania obrazów?</span><span class="sxs-lookup"><span data-stu-id="64b38-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="64b38-124">Odpowiedź: Jeśli chcesz tylko toostore JPEG lub PNG obrazów, należy przechowywać w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="64b38-124">A: If you are just looking toostore JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="64b38-125">Nie ma żadnych tooputting korzyści, które je w usługach nośnika konta, dopóki nie ma tookeep ich skojarzony z wideo lub Audio zasoby.</span><span class="sxs-lookup"><span data-stu-id="64b38-125">There is no benefit tooputting them in your Media Services account unless you want tookeep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="64b38-126">Lub może zajść potrzeba toouse hello obrazów jako nakładki na powitania koder wideo. Media Encoder Standard obsługuje nakładanie obrazów na górze wideo i to, co wyświetlane JPEG lub PNG jako obsługiwane formaty wejściowych.</span><span class="sxs-lookup"><span data-stu-id="64b38-126">Or if you might have a need toouse hello images as overlays in hello video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="64b38-127">Aby uzyskać więcej informacji, zobacz [tworzenie nakładki](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="64b38-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="64b38-128">Pytanie: jak kopiowanie zasobów z jednego tooanother konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="64b38-128">Q: How can I copy assets from one Media Services account tooanother.</span></span>

<span data-ttu-id="64b38-129">A: Użyj toocopy zasoby z jednej tooanother konta usługi Media Services przy użyciu platformy .NET, [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) — metoda rozszerzenia dostępne w hello [rozszerzenia SDK .NET usługi Azure Media Services](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repozytorium.</span><span class="sxs-lookup"><span data-stu-id="64b38-129">A: toocopy assets from one Media Services account tooanother using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="64b38-130">Aby uzyskać więcej informacji, zobacz [to](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum wątku.</span><span class="sxs-lookup"><span data-stu-id="64b38-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="64b38-131">Pytanie: jakie są hello obsługiwane znaki nazewnictwa plików podczas pracy z AMS?</span><span class="sxs-lookup"><span data-stu-id="64b38-131">Q: What are hello supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="64b38-132">A: Media Services używa wartości hello hello właściwość IAssetFile.Name podczas kompilowania adresów URL dla hello przesyłania strumieniowego zawartości (na przykład http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Z tego powodu kodowania procent jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="64b38-132">A: Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="64b38-133">Hello wartość hello **nazwa** właściwość nie może mieć jedną z następujących przyczyn hello [procent kodowanie zarezerwowanych znaków](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? [] % #".</span><span class="sxs-lookup"><span data-stu-id="64b38-133">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="64b38-134">Ponadto może istnieć tylko jeden "."</span><span class="sxs-lookup"><span data-stu-id="64b38-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="64b38-135">dla hello rozszerzenia nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="64b38-135">for hello file name extension.</span></span>

<span data-ttu-id="64b38-136">Pytanie: jak przy użyciu tooconnect REST?</span><span class="sxs-lookup"><span data-stu-id="64b38-136">Q: How tooconnect using REST?</span></span>

<span data-ttu-id="64b38-137">Odp.: Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="64b38-137">A: For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="64b38-138">Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="64b38-138">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="64b38-139">Należy wykonać kolejne wywołania toohello nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="64b38-139">You must make subsequent calls toohello new URI.</span></span> 

<span data-ttu-id="64b38-140">Pytanie: jak obrócić wideo podczas hello kodowanie procesu.</span><span class="sxs-lookup"><span data-stu-id="64b38-140">Q: How can I rotate a video during hello encoding process.</span></span>

<span data-ttu-id="64b38-141">A: Witaj [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) obsługuje obrotu kątami 90/180/270.</span><span class="sxs-lookup"><span data-stu-id="64b38-141">A: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="64b38-142">Witaj domyślne zachowanie to "Auto", gdy próbuje toodetect hello obrotu metadane w pliku MP4/MOV przychodzących hello i kompensacji go.</span><span class="sxs-lookup"><span data-stu-id="64b38-142">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="64b38-143">Uwzględnij następujące elementy hello **źródeł** tooone element hello json ustawień zdefiniowanych [tutaj](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="64b38-143">Include hello following **Sources** element tooone of hello json presets defined [here](media-services-mes-presets-overview.md):</span></span>

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a><span data-ttu-id="64b38-144">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="64b38-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="64b38-145">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="64b38-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
