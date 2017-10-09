---
title: "aaaSynonyms Podgląd samouczek w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Dodaj hello synonimy Podgląd funkcji tooan indeksu w usłudze Azure Search."
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="173d3-103">Samouczek dotyczący synonimów (wersja zapoznawcza) języka C# dla usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="173d3-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="173d3-104">Synonimy rozwiń węzeł kwerendy przez dopasowanie na warunkach uznawane za semantycznie równoważne toohello termin wejściowego.</span><span class="sxs-lookup"><span data-stu-id="173d3-104">Synonyms expand a query by matching on terms considered semantically equivalent toohello input term.</span></span> <span data-ttu-id="173d3-105">Na przykład może być "samochód" toomatch dokumenty zawierające warunki hello "samochodów" lub "nośnika".</span><span class="sxs-lookup"><span data-stu-id="173d3-105">For example, you might want "car" toomatch documents containing hello terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="173d3-106">W usłudze Azure Search synonimy są definiowane w *mapie synonimów* za pośrednictwem *reguł mapowania*, które kojarzą równoważne wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="173d3-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="173d3-107">Można tworzyć wiele map synonim, zamieścić je jako indeks tooany dostępnych zasobów całej usługi i odwoływanie które jeden toouse na poziomie pola hello.</span><span class="sxs-lookup"><span data-stu-id="173d3-107">You can create multiple synonym maps, post them as a service-wide resource available tooany index, and then reference which one toouse at hello field level.</span></span> <span data-ttu-id="173d3-108">Podczas przeszukiwania Ponadto toosearching indeksu usługi Azure Search pojawia się wyszukiwania w mapie synonim został określony dla pól używanych w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="173d3-108">At query time, in addition toosearching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="173d3-109">synonimy Hello funkcja jest aktualnie Podgląd i obsługiwana w tylko hello najnowszej wersji zapoznawczej interfejsu API i wersje zestawu SDK (interfejs api-version = 2016-09-01-Preview, wersji zestawu SDK 4.x-preview).</span><span class="sxs-lookup"><span data-stu-id="173d3-109">hello synonyms feature is currently in preview and only supported in hello latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="173d3-110">Obecnie witryna Azure Portal nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="173d3-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="173d3-111">Interfejsy API w wersji zapoznawczej nie są objęte umową SLA, a funkcje wersji zapoznawczej mogą ulec zmianie, dlatego nie zaleca się ich używania w aplikacjach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="173d3-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="173d3-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="173d3-112">Prerequisites</span></span>

<span data-ttu-id="173d3-113">Samouczek wymagania obejmują następujące hello:</span><span class="sxs-lookup"><span data-stu-id="173d3-113">Tutorial requirements include hello following:</span></span>

* [<span data-ttu-id="173d3-114">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="173d3-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="173d3-115">Usługa Azure Search</span><span class="sxs-lookup"><span data-stu-id="173d3-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="173d3-116">Wersja zapoznawcza biblioteki Microsoft.Azure.Search .NET</span><span class="sxs-lookup"><span data-stu-id="173d3-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="173d3-117">W jaki sposób toouse Azure wyszukiwanie od aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="173d3-117">How toouse Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="173d3-118">Omówienie</span><span class="sxs-lookup"><span data-stu-id="173d3-118">Overview</span></span>

<span data-ttu-id="173d3-119">Przed i po zapytania pokazują, wartość hello synonimów.</span><span class="sxs-lookup"><span data-stu-id="173d3-119">Before-and-after queries demonstrate hello value of synonyms.</span></span> <span data-ttu-id="173d3-120">W tym samouczku używamy przykładowej aplikacji, która wykonuje zapytania i zwraca wyniki w przykładowym indeksie.</span><span class="sxs-lookup"><span data-stu-id="173d3-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="173d3-121">Witaj przykładowej aplikacji tworzy małych indeks o nazwie "hotels" wypełniane przy użyciu dwa dokumenty.</span><span class="sxs-lookup"><span data-stu-id="173d3-121">hello sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="173d3-122">Aplikacja Hello wykonuje zapytania wyszukiwania korzystania z warunków i wyrażeń, które nie są wyświetlane w indeksie hello, funkcje hello synonimy, następnie problemów Witaj ponownie wyszukiwania tego samego.</span><span class="sxs-lookup"><span data-stu-id="173d3-122">hello application executes search queries using terms and phrases that do not appear in hello index, enables hello synonyms feature, then issues hello same searches again.</span></span> <span data-ttu-id="173d3-123">Poniższy kod Hello pokazuje hello ogólny przepływ.</span><span class="sxs-lookup"><span data-stu-id="173d3-123">hello code below demonstrates hello overall flow.</span></span>

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="173d3-124">Witaj toocreate kroki i wypełnić Indeks przykładów hello opisano szczegółowo w [jak toouse Azure wyszukiwanie od aplikacji .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="173d3-124">hello steps toocreate and populate hello sample index are explained in [How toouse Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="173d3-125">Zapytania „przed”</span><span class="sxs-lookup"><span data-stu-id="173d3-125">"Before" queries</span></span>

<span data-ttu-id="173d3-126">W indeksie `RunQueriesWithNonExistentTermsInIndex` wykonujemy zapytania wyszukiwania z użyciem wyrażeń „five star”, „internet” oraz „economy AND hotel”.</span><span class="sxs-lookup"><span data-stu-id="173d3-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="173d3-127">Ani dwa dokumenty indeksowanego hello zawierają postanowienia hello, tak aby uzyskujemy hello następujące dane wyjściowe z hello `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="173d3-127">Neither of hello two indexed documents contain hello terms, so we get hello following output from hello first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="173d3-128">Włączanie synonimów</span><span class="sxs-lookup"><span data-stu-id="173d3-128">Enable synonyms</span></span>

<span data-ttu-id="173d3-129">Włączenie synonimów to dwuetapowy proces.</span><span class="sxs-lookup"><span data-stu-id="173d3-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="173d3-130">Firma Microsoft najpierw zdefiniować i przekaż synonim reguły, a następnie skonfiguruj toouse pola je.</span><span class="sxs-lookup"><span data-stu-id="173d3-130">We first define and upload synonym rules and then configure fields toouse them.</span></span> <span data-ttu-id="173d3-131">proces Hello jest opisane w temacie `UploadSynonyms` i `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="173d3-131">hello process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="173d3-132">Dodaj usługę wyszukiwania tooyour synonim mapy.</span><span class="sxs-lookup"><span data-stu-id="173d3-132">Add a synonym map tooyour search service.</span></span> <span data-ttu-id="173d3-133">W `UploadSynonyms`, możemy zdefiniować cztery reguły w naszym mapy synonim "desc synonymmap" i usługa toohello przekazywania.</span><span class="sxs-lookup"><span data-stu-id="173d3-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload toohello service.</span></span>
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
<span data-ttu-id="173d3-134">Mapa synonim musi być zgodna standard typu open source toohello `solr` format.</span><span class="sxs-lookup"><span data-stu-id="173d3-134">A synonym map must conform toohello open source standard `solr` format.</span></span> <span data-ttu-id="173d3-135">Hello format zostało wyjaśnione w dokumencie [synonimy w usłudze Azure Search](search-synonyms.md) sekcji hello `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="173d3-135">hello format is explained in [Synonyms in Azure Search](search-synonyms.md) under hello section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="173d3-136">W definicji indeksu hello, należy skonfigurować pola z możliwością przeszukiwania toouse hello synonim mapy.</span><span class="sxs-lookup"><span data-stu-id="173d3-136">Configure searchable fields toouse hello synonym map in hello index definition.</span></span> <span data-ttu-id="173d3-137">W `EnableSynonymsInHotelsIndex`, włączysz synonimy na dwa pola `category` i `tags` przez ustawienie hello `synonymMaps` toohello nazwę właściwości hello nowo przekazać synonim mapy.</span><span class="sxs-lookup"><span data-stu-id="173d3-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting hello `synonymMaps` property toohello name of hello newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="173d3-138">Podczas dodawania mapy synonimów ponowne kompilowanie indeksu nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="173d3-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="173d3-139">Można dodać usługę tooyour mapy synonim, a następnie zmiana istniejących definicji pola w dowolnej nowej mapy synonim indeksu toouse hello.</span><span class="sxs-lookup"><span data-stu-id="173d3-139">You can add a synonym map tooyour service, and then amend existing field definitions in any index toouse hello new synonym map.</span></span> <span data-ttu-id="173d3-140">dodanie nowych atrybutów Hello nie ma wpływu na dostępność indeksu.</span><span class="sxs-lookup"><span data-stu-id="173d3-140">hello addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="173d3-141">Witaj, którego dotyczy to również w wyłączenie synonimy dla pola.</span><span class="sxs-lookup"><span data-stu-id="173d3-141">hello same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="173d3-142">Można ustawić po prostu hello `synonymMaps` właściwości tooan pustej listy.</span><span class="sxs-lookup"><span data-stu-id="173d3-142">You can simply set hello `synonymMaps` property tooan empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="173d3-143">Zapytania „po”</span><span class="sxs-lookup"><span data-stu-id="173d3-143">"After" queries</span></span>

<span data-ttu-id="173d3-144">Po przekazaniu mapy synonim hello i indeks hello jest zaktualizowane toouse hello synonim mapy, drugi hello `RunQueriesWithNonExistentTermsInIndex` hello następujących danych wyjściowych wywołania:</span><span class="sxs-lookup"><span data-stu-id="173d3-144">After hello synonym map is uploaded and hello index is updated toouse hello synonym map, hello second `RunQueriesWithNonExistentTermsInIndex` call outputs hello following:</span></span>

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="173d3-145">Hello pierwszego zapytania znajduje hello dokumentu z reguły hello `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="173d3-145">hello first query finds hello document from hello rule `five star=>luxury`.</span></span> <span data-ttu-id="173d3-146">Rozszerza Hello drugiego zapytania hello wyszukiwanie przy użyciu `internet,wifi` i hello innej przy użyciu zarówno `hotel, motel` i `economy,inexpensive=>budget` w znajdowaniu dokumentów hello one zgodne.</span><span class="sxs-lookup"><span data-stu-id="173d3-146">hello second query expands hello search using `internet,wifi` and hello third using both `hotel, motel` and `economy,inexpensive=>budget` in finding hello documents they matched.</span></span>

<span data-ttu-id="173d3-147">Dodawanie synonimy całkowicie zmienia hello wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="173d3-147">Adding synonyms completely changes hello search experience.</span></span> <span data-ttu-id="173d3-148">W tym samouczku hello oryginalnego zapytania nie tooreturn znaczących wyników, nawet jeśli były odpowiednie hello dokumenty w indeksie.</span><span class="sxs-lookup"><span data-stu-id="173d3-148">In this tutorial, hello original queries failed tooreturn meaningful results even though hello documents in our index were relevant.</span></span> <span data-ttu-id="173d3-149">Przez włączenie synonimy, możemy rozwiń tooinclude indeksu wspólną użyć warunki, bez zmian danych toounderlying hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="173d3-149">By enabling synonyms, we can expand an index tooinclude terms in common use, with no changes toounderlying data in hello index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="173d3-150">Kod źródłowy przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="173d3-150">Sample application source code</span></span>
<span data-ttu-id="173d3-151">Można znaleźć hello pełny kod źródłowy hello przykładowej aplikacji używane w tym krokach związanych z na [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="173d3-151">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="173d3-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="173d3-152">Next steps</span></span>

* <span data-ttu-id="173d3-153">Przegląd [jak synonimy toouse w usłudze Azure Search](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="173d3-153">Review [How toouse synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="173d3-154">Zapoznaj się z [Dokumentacją interfejsu API REST synonimów](https://aka.ms/rgm6rq)</span><span class="sxs-lookup"><span data-stu-id="173d3-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="173d3-155">Przeglądaj hello odwołań dla hello [zestawu .NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) i [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="173d3-155">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
