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
# <a name="publish-azure-media-services-content-using-net"></a>Publikowanie zawartości usługi Azure Media Services przy użyciu platformy .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-deliver-streaming-content.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [Portal](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a>Omówienie
Można strumienia o adaptacyjnej szybkości bitowej MP4 ustawione przez utworzenie lokalizatora OnDemand przesyłania strumieniowego i tworzenia adresu URL przesyłania strumieniowego. Witaj [kodowanie zasób](media-services-encode-asset.md) temacie pokazano, jak ustawić tooencode do adaptacyjnej szybkości bitowej MP4. 

> [!NOTE]
> Jeśli zawartość jest zaszyfrowany, należy skonfigurować zasady dostarczania elementu zawartości (zgodnie z opisem w [to](media-services-dotnet-configure-asset-delivery-policy.md) tematu) przed utworzeniem lokalizatora. 
> 
> 

Można również użyć OnDemand przesyłania strumieniowego adresy URL toobuild lokalizatora tego punktu tooMP4 pliki, które można pobrać progresywnie.  

W tym temacie przedstawiono sposób toocreate z zasobów i kompilacji Smooth, MPEG DASH i HLS adresów URL przesyłania strumieniowego przesyłania strumieniowego toopublish lokalizatora OnDemand. Przedstawiono również gorących toobuild adresy URL pobierania progresywnego. 

## <a name="create-an-ondemand-streaming-locator"></a>Utwórz Lokalizator OnDemand przesyłania strumieniowego
toocreate hello Lokalizator OnDemand przesyłania strumieniowego i uzyskiwanie adresów URL, należy hello toodo następujące czynności:

1. Jeśli zawartość hello jest zaszyfrowany, należy zdefiniować zasadę dostępu.
2. Utwórz Lokalizator OnDemand przesyłania strumieniowego.
3. Jeśli planujesz toostream uzyskać hello przesyłania strumieniowego pliku manifestu (.ism) w hello zasobów. 
   
   Jeśli planujesz pobierania tooprogressively uzyskać hello nazwy plików MP4 w hello zasobów.  
4. Tworzenie pliku manifestu toohello adresy URL lub pliki MP4. 


>[!NOTE]
>Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy). Użyj hello sam identyfikator zasad, jeśli używasz zawsze hello sam dni / uprawnień dostępu. Na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (— przekazywanie zasady). Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.

### <a name="use-media-services-net-sdk"></a>Użyj usługi Media Services zestawu .NET SDK
Tworzenie adresy URL przesyłania strumieniowego 

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

wyniki Hello:

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> Można również strumienia zawartości za pośrednictwem połączenia SSL. toodo tego podejścia, upewnij się, że uruchamiania adresy URL przesyłania strumieniowego z protokołu HTTPS. Obecnie usługa AMS nie obsługuje protokołu SSL z domen niestandardowych.
> 
> 

Tworzenie adresy URL pobierania progresywnego 

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

wyniki Hello:

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a>Użyj rozszerzenia SDK .NET usługi Media Services
Witaj następujący kod wywołuje metody rozszerzenia zestawu .NET SDK, które tworzenie lokalizatora i generowanie adresy URL MPEG-DASH, HLS i Smooth Streaming hello do adaptacyjnego przesyłania strumieniowego.

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


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Następne kroki
* [Pobieranie zasobów](media-services-deliver-asset-download.md)
* [Konfigurowanie zasad dostarczania elementów zawartości](media-services-dotnet-configure-asset-delivery-policy.md)

