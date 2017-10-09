---
title: "Filtry aaaCreating przy użyciu zestawu .NET SDK usługi Azure Media Services"
description: "W tym temacie opisano, jak toocreate filtry, aby klient mógł ich użyć toostream określonych sekcji strumienia. Usługi Media Services tworzy dynamiczne manifestów tooachieve selektywnego strumienia."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 16d9497d48ab1d3f841dd97efb0f66016a2435c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="a68a1-104">Tworzenie filtrów za pomocą zestawu .NET SDK usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="a68a1-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a68a1-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a68a1-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="a68a1-106">REST</span><span class="sxs-lookup"><span data-stu-id="a68a1-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="a68a1-107">Począwszy od wersji 2.11, Media Services umożliwia filtry toodefine trwałych.</span><span class="sxs-lookup"><span data-stu-id="a68a1-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="a68a1-108">Te filtry są reguły po stronie serwera, zezwalające klientom toochoose toodo np.: odtwarzanie tylko części klipu wideo (a nie odtwarzane hello całego wideo), lub określ tylko podzestaw audio i wideo wersji obsługi (przez klienta urządzenia zamiast wersji hello wszystkich skojarzonych z hello zasobów).</span><span class="sxs-lookup"><span data-stu-id="a68a1-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="a68a1-109">Ta filtrowania zasobów odbywa się za pośrednictwem **dynamiczne manifestu**, które są tworzone w chwili toostream żądania klienta wideo oparte na określonej filtry.</span><span class="sxs-lookup"><span data-stu-id="a68a1-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="a68a1-110">Bardziej szczegółowe informacje pokrewne toofilters i dynamiczne manifestu, zobacz [dynamicznie manifesty omówienie](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a68a1-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="a68a1-111">W tym temacie przedstawiono sposób toouse toocreate .NET SDK usługi Media Services, aktualizować i usuwać filtrów.</span><span class="sxs-lookup"><span data-stu-id="a68a1-111">This topic shows how toouse Media Services .NET SDK toocreate, update, and delete filters.</span></span> 

<span data-ttu-id="a68a1-112">Należy zwrócić uwagę, jeśli zaktualizujesz filtru może potrwać too2 minut do przesyłania strumieniowego punktu końcowego toorefresh hello reguły.</span><span class="sxs-lookup"><span data-stu-id="a68a1-112">Note if you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="a68a1-113">Jeśli zawartość hello zostało obsłużone przy użyciu tego filtru (i w pamięci podręcznej serwerów proxy i sieci CDN pamięci podręcznych), aktualizacja tego filtru może powodować błędy player.</span><span class="sxs-lookup"><span data-stu-id="a68a1-113">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="a68a1-114">Jest zalecane tooclear hello w pamięci podręcznej po zaktualizowaniu hello filtru.</span><span class="sxs-lookup"><span data-stu-id="a68a1-114">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="a68a1-115">Jeśli ta opcja nie jest możliwe, należy rozważyć użycie inny filtr.</span><span class="sxs-lookup"><span data-stu-id="a68a1-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="a68a1-116">Typy używane filtry toocreate</span><span class="sxs-lookup"><span data-stu-id="a68a1-116">Types used toocreate filters</span></span>
<span data-ttu-id="a68a1-117">Witaj następujące typy są używane podczas tworzenia filtrów:</span><span class="sxs-lookup"><span data-stu-id="a68a1-117">hello following types are used when creating filters:</span></span> 

* <span data-ttu-id="a68a1-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="a68a1-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="a68a1-119">Ten typ jest oparty na powitania po interfejsu API REST [filtru](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="a68a1-119">This type is based on hello following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="a68a1-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="a68a1-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="a68a1-121">Ten typ jest oparty na powitania po interfejsu API REST [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="a68a1-121">This type is based on hello following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="a68a1-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="a68a1-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="a68a1-123">Ten typ jest oparty na powitania po interfejsu API REST [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="a68a1-123">This type is based on hello following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="a68a1-124">**FilterTrackSelectStatement** i **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="a68a1-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="a68a1-125">Te typy są oparte na powitania po interfejsów API REST [FilterTrackSelect i FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="a68a1-125">These types are based on hello following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="a68a1-126">Filtry globalne tworzenia/aktualizacji/odczytu/usuwania</span><span class="sxs-lookup"><span data-stu-id="a68a1-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="a68a1-127">Witaj poniższy kod przedstawia sposób toouse .NET toocreate, aktualizacji, do odczytu i usuwania filtrów zasobów.</span><span class="sxs-lookup"><span data-stu-id="a68a1-127">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="a68a1-128">Filtry tworzenia/aktualizacji/odczytu/usuwania zasobów</span><span class="sxs-lookup"><span data-stu-id="a68a1-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="a68a1-129">Witaj poniższy kod przedstawia sposób toouse .NET toocreate, aktualizacji, do odczytu i usuwania filtrów zasobów.</span><span class="sxs-lookup"><span data-stu-id="a68a1-129">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="a68a1-130">Tworzenie adresów URL, które należy używać filtrów przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="a68a1-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="a68a1-131">Aby uzyskać informacje dotyczące toopublish i dostarczyć zasobów, zobacz temat [tooCustomers dostarczanie zawartości omówienie](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a68a1-131">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="a68a1-132">Witaj następujące przykłady przedstawiają sposób tooadd filtry tooyour adresów URL przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="a68a1-132">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="a68a1-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="a68a1-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="a68a1-134">**Apple HTTP Live przesyłania strumieniowego V4 (HLS)**</span><span class="sxs-lookup"><span data-stu-id="a68a1-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="a68a1-135">**Apple HTTP Live przesyłania strumieniowego V3 (HLS)**</span><span class="sxs-lookup"><span data-stu-id="a68a1-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="a68a1-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="a68a1-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="a68a1-137">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="a68a1-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a68a1-138">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="a68a1-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a68a1-139">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a68a1-139">See Also</span></span>
[<span data-ttu-id="a68a1-140">Omówienie dynamicznej manifestów</span><span class="sxs-lookup"><span data-stu-id="a68a1-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

