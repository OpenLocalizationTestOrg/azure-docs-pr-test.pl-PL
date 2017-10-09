---
title: "aaaPublish zawartości usługi Azure Media Services przy użyciu platformy .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate lokalizatora, która jest używana toobuild adresu URL przesyłania strumieniowego. Przykłady kodu są napisane w języku C# i używają hello SDK usługi Media Services dla platformy .NET."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: c53b1f83-4cb1-4b09-840f-9c145b7d6f8d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: c941cd93c252a96e66546cce2793bb426afac059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="8f64f-104">Publikowanie zawartości usługi Azure Media Services przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="8f64f-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f64f-105">REST</span><span class="sxs-lookup"><span data-stu-id="8f64f-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="8f64f-106">.NET</span><span class="sxs-lookup"><span data-stu-id="8f64f-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="8f64f-107">Portal</span><span class="sxs-lookup"><span data-stu-id="8f64f-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="8f64f-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8f64f-108">Overview</span></span>
<span data-ttu-id="8f64f-109">Można strumienia o adaptacyjnej szybkości bitowej MP4 ustawione przez utworzenie lokalizatora OnDemand przesyłania strumieniowego i tworzenia adresu URL przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="8f64f-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="8f64f-110">Witaj [kodowanie zasób](media-services-encode-asset.md) temacie pokazano, jak ustawić tooencode do adaptacyjnej szybkości bitowej MP4.</span><span class="sxs-lookup"><span data-stu-id="8f64f-110">hello [encoding an asset](media-services-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="8f64f-111">Jeśli zawartość jest zaszyfrowany, należy skonfigurować zasady dostarczania elementu zawartości (zgodnie z opisem w [to](media-services-dotnet-configure-asset-delivery-policy.md) tematu) przed utworzeniem lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="8f64f-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="8f64f-112">Można również użyć OnDemand przesyłania strumieniowego adresy URL toobuild lokalizatora tego punktu tooMP4 pliki, które można pobrać progresywnie.</span><span class="sxs-lookup"><span data-stu-id="8f64f-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="8f64f-113">W tym temacie przedstawiono sposób toocreate z zasobów i kompilacji Smooth, MPEG DASH i HLS adresów URL przesyłania strumieniowego przesyłania strumieniowego toopublish lokalizatora OnDemand.</span><span class="sxs-lookup"><span data-stu-id="8f64f-113">This topic shows how toocreate an OnDemand streaming locator toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="8f64f-114">Przedstawiono również gorących toobuild adresy URL pobierania progresywnego.</span><span class="sxs-lookup"><span data-stu-id="8f64f-114">It also shows hot toobuild progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="8f64f-115">Utwórz Lokalizator OnDemand przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="8f64f-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="8f64f-116">toocreate hello Lokalizator OnDemand przesyłania strumieniowego i uzyskiwanie adresów URL, należy hello toodo następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f64f-116">toocreate hello OnDemand streaming locator and get URLs, you need toodo hello following things:</span></span>

1. <span data-ttu-id="8f64f-117">Jeśli zawartość hello jest zaszyfrowany, należy zdefiniować zasadę dostępu.</span><span class="sxs-lookup"><span data-stu-id="8f64f-117">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="8f64f-118">Utwórz Lokalizator OnDemand przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="8f64f-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="8f64f-119">Jeśli planujesz toostream uzyskać hello przesyłania strumieniowego pliku manifestu (.ism) w hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="8f64f-119">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="8f64f-120">Jeśli planujesz pobierania tooprogressively uzyskać hello nazwy plików MP4 w hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="8f64f-120">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span>  
4. <span data-ttu-id="8f64f-121">Tworzenie pliku manifestu toohello adresy URL lub pliki MP4.</span><span class="sxs-lookup"><span data-stu-id="8f64f-121">Build URLs toohello manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="8f64f-122">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="8f64f-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="8f64f-123">Użyj hello sam identyfikator zasad, jeśli używasz zawsze hello sam dni / uprawnień dostępu.</span><span class="sxs-lookup"><span data-stu-id="8f64f-123">Use hello same policy ID if you are always using hello same days / access permissions.</span></span> <span data-ttu-id="8f64f-124">Na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (— przekazywanie zasady).</span><span class="sxs-lookup"><span data-stu-id="8f64f-124">For example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="8f64f-125">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="8f64f-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="8f64f-126">Użyj usługi Media Services zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8f64f-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="8f64f-127">Tworzenie adresy URL przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="8f64f-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL toomanifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL toomanifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL toomanifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="8f64f-128">wyniki Hello:</span><span class="sxs-lookup"><span data-stu-id="8f64f-128">hello outputs:</span></span>

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="8f64f-129">Można również strumienia zawartości za pośrednictwem połączenia SSL.</span><span class="sxs-lookup"><span data-stu-id="8f64f-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="8f64f-130">toodo tego podejścia, upewnij się, że uruchamiania adresy URL przesyłania strumieniowego z protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8f64f-130">toodo this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="8f64f-131">Obecnie usługa AMS nie obsługuje protokołu SSL z domen niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="8f64f-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="8f64f-132">Tworzenie adresy URL pobierania progresywnego</span><span class="sxs-lookup"><span data-stu-id="8f64f-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator toohello asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL toohello MP4 files. Use this tooprogressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="8f64f-133">wyniki Hello:</span><span class="sxs-lookup"><span data-stu-id="8f64f-133">hello outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="8f64f-134">Użyj rozszerzenia SDK .NET usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="8f64f-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="8f64f-135">Witaj następujący kod wywołuje metody rozszerzenia zestawu .NET SDK, które tworzenie lokalizatora i generowanie adresy URL MPEG-DASH, HLS i Smooth Streaming hello do adaptacyjnego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="8f64f-135">hello following code calls .NET SDK extensions methods that create a locator and generate hello Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get hello streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="8f64f-136">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="8f64f-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8f64f-137">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="8f64f-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="8f64f-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8f64f-138">Next steps</span></span>
* [<span data-ttu-id="8f64f-139">Pobieranie zasobów</span><span class="sxs-lookup"><span data-stu-id="8f64f-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="8f64f-140">Konfigurowanie zasad dostarczania elementów zawartości</span><span class="sxs-lookup"><span data-stu-id="8f64f-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

