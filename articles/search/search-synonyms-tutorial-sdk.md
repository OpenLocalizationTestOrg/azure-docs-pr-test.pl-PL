---
title: "Samouczek dotyczący synonimów w wersji zapoznawczej w usłudze Azure Search | Microsoft Docs"
description: "Dodaj funkcję synonimów (wersja zapoznawcza) do indeksu w usłudze Azure Search."
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
ms.openlocfilehash: 014959ed471f796d2184f0f8ff10d15cdc8a2ec6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="d6c3e-103">Samouczek dotyczący synonimów (wersja zapoznawcza) języka C# dla usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="d6c3e-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="d6c3e-104">Synonimy rozszerzają zapytanie, dopasowując wyrażenia uznane za semantycznie równoważne z wyrażeniem wejściowym.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-104">Synonyms expand a query by matching on terms considered semantically equivalent to the input term.</span></span> <span data-ttu-id="d6c3e-105">Przykładowo można sprawić, aby wyraz „samochód” pasował do dokumentów zawierających wyrażenia „auto” lub „pojazd”.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-105">For example, you might want "car" to match documents containing the terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="d6c3e-106">W usłudze Azure Search synonimy są definiowane w *mapie synonimów* za pośrednictwem *reguł mapowania*, które kojarzą równoważne wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="d6c3e-107">Możesz utworzyć wiele map synonimów, opublikować je jako zasób obejmujący usługę dostępny dla dowolnych indeksów, a następnie określić, której z nich należy używać na poziomie pola.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-107">You can create multiple synonym maps, post them as a service-wide resource available to any index, and then reference which one to use at the field level.</span></span> <span data-ttu-id="d6c3e-108">W czasie realizacji zapytania, poza wyszukiwaniem indeksu, usługa Azure Search wyszukuje mapę synonimów, jeśli mapa została określona dla pól używanych w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-108">At query time, in addition to searching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="d6c3e-109">Funkcja synonimów jest obecnie dostępna w wersji zapoznawczej i jest obsługiwana tylko w najnowszych wersjach zapoznawczych interfejsu API i zestawów SDK (wersja interfejsu API: 2016-09-01-Preview, wersja zestawu SDK: 4.x-preview).</span><span class="sxs-lookup"><span data-stu-id="d6c3e-109">The synonyms feature is currently in preview and only supported in the latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="d6c3e-110">Obecnie witryna Azure Portal nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="d6c3e-111">Interfejsy API w wersji zapoznawczej nie są objęte umową SLA, a funkcje wersji zapoznawczej mogą ulec zmianie, dlatego nie zaleca się ich używania w aplikacjach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6c3e-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d6c3e-112">Prerequisites</span></span>

<span data-ttu-id="d6c3e-113">Wymagania samouczka obejmują poniższe elementy:</span><span class="sxs-lookup"><span data-stu-id="d6c3e-113">Tutorial requirements include the following:</span></span>

* [<span data-ttu-id="d6c3e-114">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d6c3e-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="d6c3e-115">Usługa Azure Search</span><span class="sxs-lookup"><span data-stu-id="d6c3e-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="d6c3e-116">Wersja zapoznawcza biblioteki Microsoft.Azure.Search .NET</span><span class="sxs-lookup"><span data-stu-id="d6c3e-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="d6c3e-117">Jak używać usługi Azure Search z poziomu aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="d6c3e-117">How to use Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="d6c3e-118">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d6c3e-118">Overview</span></span>

<span data-ttu-id="d6c3e-119">Zapytania „przed” i „po” demonstrują wartość synonimów.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-119">Before-and-after queries demonstrate the value of synonyms.</span></span> <span data-ttu-id="d6c3e-120">W tym samouczku używamy przykładowej aplikacji, która wykonuje zapytania i zwraca wyniki w przykładowym indeksie.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="d6c3e-121">Przykładowa aplikacja tworzy mały indeks o nazwie „hotels” uzupełniony dwoma dokumentami.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-121">The sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="d6c3e-122">Aplikacja wykonuje zapytania wyszukiwania przy użyciu wyrażeń i fraz, które nie pojawiają się w indeksie, włącza funkcję synonimów, a następnie ponownie wykonuje te same wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-122">The application executes search queries using terms and phrases that do not appear in the index, enables the synonyms feature, then issues the same searches again.</span></span> <span data-ttu-id="d6c3e-123">Poniższy kod demonstruje ogólny przepływ.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-123">The code below demonstrates the overall flow.</span></span>

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
      Thread.Sleep(10000); // Wait for the changes to propagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="d6c3e-124">Kroki związane z tworzeniem i uzupełnianiem przykładowego indeksu zostały wyjaśnione w temacie [Jak używać usługi Azure Search z poziomu aplikacji .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="d6c3e-124">The steps to create and populate the sample index are explained in [How to use Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="d6c3e-125">Zapytania „przed”</span><span class="sxs-lookup"><span data-stu-id="d6c3e-125">"Before" queries</span></span>

<span data-ttu-id="d6c3e-126">W indeksie `RunQueriesWithNonExistentTermsInIndex` wykonujemy zapytania wyszukiwania z użyciem wyrażeń „five star”, „internet” oraz „economy AND hotel”.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search the entire index for the phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="d6c3e-127">Żaden ze zindeksowanych dokumentów nie zawiera tych wyrażeń, więc z pierwszego indeksu `RunQueriesWithNonExistentTermsInIndex` uzyskujemy następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-127">Neither of the two indexed documents contain the terms, so we get the following output from the first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search the entire index for the phrase "five star":

no document matched

Search the entire index for the term 'internet':

no document matched

Search the entire index for the terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="d6c3e-128">Włączanie synonimów</span><span class="sxs-lookup"><span data-stu-id="d6c3e-128">Enable synonyms</span></span>

<span data-ttu-id="d6c3e-129">Włączenie synonimów to dwuetapowy proces.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="d6c3e-130">Najpierw definiujemy i przekazujemy reguły synonimów, a następnie konfigurujemy pola, aby ich używały.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-130">We first define and upload synonym rules and then configure fields to use them.</span></span> <span data-ttu-id="d6c3e-131">Proces jest opisany w `UploadSynonyms` i `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-131">The process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="d6c3e-132">Dodaj mapę synonimów do usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-132">Add a synonym map to your search service.</span></span> <span data-ttu-id="d6c3e-133">W `UploadSynonyms` definiujemy cztery reguły w mapie synonimów „desc-synonymmap” i przekazujemy je do usługi.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload to the service.</span></span>
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
<span data-ttu-id="d6c3e-134">Mapa synonimów musi być zgodna z formatem `solr` w standardzie open source.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-134">A synonym map must conform to the open source standard `solr` format.</span></span> <span data-ttu-id="d6c3e-135">Format został wyjaśniony w artykule [Synonimy w usłudze Azure Search](search-synonyms.md) w sekcji `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-135">The format is explained in [Synonyms in Azure Search](search-synonyms.md) under the section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="d6c3e-136">Skonfiguruj pola z możliwością wyszukiwania, aby używać mapy synonimów w definicji indeksu.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-136">Configure searchable fields to use the synonym map in the index definition.</span></span> <span data-ttu-id="d6c3e-137">W `EnableSynonymsInHotelsIndex` włączamy synonimy w dwóch polach, `category` i `tags`, ustawiając właściwość `synonymMaps` na nazwę nowo przekazanej mapy synonimów.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting the `synonymMaps` property to the name of the newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="d6c3e-138">Podczas dodawania mapy synonimów ponowne kompilowanie indeksu nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="d6c3e-139">Możesz dodać mapę synonimów do usługi, a następnie zmienić istniejące definicje pól w dowolnym indeksie, aby użyć nowej mapy synonimów.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-139">You can add a synonym map to your service, and then amend existing field definitions in any index to use the new synonym map.</span></span> <span data-ttu-id="d6c3e-140">Dodawanie nowych atrybutów nie ma wpływu na dostępność indeksu.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-140">The addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="d6c3e-141">To samo dotyczy wyłączania synonimów dla pola.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-141">The same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="d6c3e-142">Możesz po prostu ustawić właściwość `synonymMaps` na pustą listę.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-142">You can simply set the `synonymMaps` property to an empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="d6c3e-143">Zapytania „po”</span><span class="sxs-lookup"><span data-stu-id="d6c3e-143">"After" queries</span></span>

<span data-ttu-id="d6c3e-144">Po przekazaniu mapy synonimów i zaktualizowaniu indeksu do używania mapy synonimów drugie wywołanie `RunQueriesWithNonExistentTermsInIndex` zwraca następujące wyniki:</span><span class="sxs-lookup"><span data-stu-id="d6c3e-144">After the synonym map is uploaded and the index is updated to use the synonym map, the second `RunQueriesWithNonExistentTermsInIndex` call outputs the following:</span></span>

~~~
Search the entire index for the phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="d6c3e-145">Pierwsze zapytanie znajduje dokument na podstawie reguły `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-145">The first query finds the document from the rule `five star=>luxury`.</span></span> <span data-ttu-id="d6c3e-146">Drugie zapytanie rozszerza wyszukiwanie przy użyciu `internet,wifi`, a trzecie przy użyciu `hotel, motel` i `economy,inexpensive=>budget` w zakresie wyszukiwania dopasowanych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-146">The second query expands the search using `internet,wifi` and the third using both `hotel, motel` and `economy,inexpensive=>budget` in finding the documents they matched.</span></span>

<span data-ttu-id="d6c3e-147">Dodanie synonimów całkowicie zmienia funkcję wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-147">Adding synonyms completely changes the search experience.</span></span> <span data-ttu-id="d6c3e-148">W tym samouczku oryginalne zapytania nie zwróciły znaczących wyników, chociaż dokumenty w naszym indeksie były odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-148">In this tutorial, the original queries failed to return meaningful results even though the documents in our index were relevant.</span></span> <span data-ttu-id="d6c3e-149">Włączając synonimy, możemy rozszerzyć indeks, aby objął popularne wyrażenia, nie zmieniając danych źródłowych w indeksie.</span><span class="sxs-lookup"><span data-stu-id="d6c3e-149">By enabling synonyms, we can expand an index to include terms in common use, with no changes to underlying data in the index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="d6c3e-150">Kod źródłowy przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="d6c3e-150">Sample application source code</span></span>
<span data-ttu-id="d6c3e-151">Możesz znaleźć pełny kod źródłowy przykładowej aplikacji używanej w tym poradniku w portalu [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="d6c3e-151">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6c3e-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6c3e-152">Next steps</span></span>

* <span data-ttu-id="d6c3e-153">Zapoznaj się z tematem [Jak używać synonimów w usłudze Azure Search](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="d6c3e-153">Review [How to use synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="d6c3e-154">Zapoznaj się z [Dokumentacją interfejsu API REST synonimów](https://aka.ms/rgm6rq)</span><span class="sxs-lookup"><span data-stu-id="d6c3e-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="d6c3e-155">Przeglądaj odwołania do [zestawu SDK .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) oraz [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="d6c3e-155">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
