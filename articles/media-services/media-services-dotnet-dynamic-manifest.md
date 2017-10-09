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
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>Tworzenie filtrów za pomocą zestawu .NET SDK usługi Azure Media Services
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

Począwszy od wersji 2.11, Media Services umożliwia filtry toodefine trwałych. Te filtry są reguły po stronie serwera, zezwalające klientom toochoose toodo np.: odtwarzanie tylko części klipu wideo (a nie odtwarzane hello całego wideo), lub określ tylko podzestaw audio i wideo wersji obsługi (przez klienta urządzenia zamiast wersji hello wszystkich skojarzonych z hello zasobów). Ta filtrowania zasobów odbywa się za pośrednictwem **dynamiczne manifestu**, które są tworzone w chwili toostream żądania klienta wideo oparte na określonej filtry.

Bardziej szczegółowe informacje pokrewne toofilters i dynamiczne manifestu, zobacz [dynamicznie manifesty omówienie](media-services-dynamic-manifest-overview.md).

W tym temacie przedstawiono sposób toouse toocreate .NET SDK usługi Media Services, aktualizować i usuwać filtrów. 

Należy zwrócić uwagę, jeśli zaktualizujesz filtru może potrwać too2 minut do przesyłania strumieniowego punktu końcowego toorefresh hello reguły. Jeśli zawartość hello zostało obsłużone przy użyciu tego filtru (i w pamięci podręcznej serwerów proxy i sieci CDN pamięci podręcznych), aktualizacja tego filtru może powodować błędy player. Jest zalecane tooclear hello w pamięci podręcznej po zaktualizowaniu hello filtru. Jeśli ta opcja nie jest możliwe, należy rozważyć użycie inny filtr. 

## <a name="types-used-toocreate-filters"></a>Typy używane filtry toocreate
Witaj następujące typy są używane podczas tworzenia filtrów: 

* **IStreamingFilter**.  Ten typ jest oparty na powitania po interfejsu API REST [filtru](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**. Ten typ jest oparty na powitania po interfejsu API REST [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**. Ten typ jest oparty na powitania po interfejsu API REST [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** i **IFilterTrackPropertyCondition**. Te typy są oparte na powitania po interfejsów API REST [FilterTrackSelect i FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>Filtry globalne tworzenia/aktualizacji/odczytu/usuwania
Witaj poniższy kod przedstawia sposób toouse .NET toocreate, aktualizacji, do odczytu i usuwania filtrów zasobów.

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


## <a name="createupdatereaddelete-asset-filters"></a>Filtry tworzenia/aktualizacji/odczytu/usuwania zasobów
Witaj poniższy kod przedstawia sposób toouse .NET toocreate, aktualizacji, do odczytu i usuwania filtrów zasobów.

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




## <a name="build-streaming-urls-that-use-filters"></a>Tworzenie adresów URL, które należy używać filtrów przesyłania strumieniowego
Aby uzyskać informacje dotyczące toopublish i dostarczyć zasobów, zobacz temat [tooCustomers dostarczanie zawartości omówienie](media-services-deliver-content-overview.md).

Witaj następujące przykłady przedstawiają sposób tooadd filtry tooyour adresów URL przesyłania strumieniowego.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live przesyłania strumieniowego V4 (HLS)**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live przesyłania strumieniowego V3 (HLS)**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Smooth Streaming**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Omówienie dynamicznej manifestów](media-services-dynamic-manifest-overview.md)

