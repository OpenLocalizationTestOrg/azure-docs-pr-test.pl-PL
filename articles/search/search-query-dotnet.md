---
title: "AAA \"Tworzenie zapytań względem indeksu (interfejs API .NET — usługi Azure Search) | Dokumentacja firmy Microsoft\""
description: "Konstruowanie zapytania wyszukiwania w usłudze Azure search i Użyj wyszukiwania parametrów toofilter i sortowanie wyników wyszukiwania."
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a><span data-ttu-id="2e1c5-103">Tworzenie zapytań względem indeksu usługi Azure Search przy użyciu zestawu .NET SDK hello</span><span class="sxs-lookup"><span data-stu-id="2e1c5-103">Query your Azure Search index using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e1c5-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2e1c5-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="2e1c5-105">Portal</span><span class="sxs-lookup"><span data-stu-id="2e1c5-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="2e1c5-106">.NET</span><span class="sxs-lookup"><span data-stu-id="2e1c5-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="2e1c5-107">REST</span><span class="sxs-lookup"><span data-stu-id="2e1c5-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="2e1c5-108">W tym artykule opisano, jak hello tooquery indeksu przy użyciu [zestawu .NET SDK usługi Azure Search](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="2e1c5-108">This article will show you how tooquery an index using hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="2e1c5-109">Przed rozpoczęciem pracy z tym przewodnikiem należy [utworzyć indeks usługi Azure Search](search-what-is-an-index.md) i [wypełnić go danymi](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="2e1c5-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2e1c5-110">Cały przykładowy kod przedstawiony w tym artykule został napisany w języku C#.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="2e1c5-111">Można znaleźć hello pełny kod źródłowy [w serwisie GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="2e1c5-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="2e1c5-112">Możesz przeczytać temat hello [zestawu .NET SDK usługi Azure Search](search-howto-dotnet-sdk.md) do bardziej szczegółowych przechodzenia przez hello próbki kodu.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="2e1c5-113">Identyfikowanie klucza api-key zapytania usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="2e1c5-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="2e1c5-114">Po utworzeniu indeksu usługi Azure Search, użytkownik jest już prawie gotowe tooissue zapytań przy użyciu hello zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-114">Now that you have created an Azure Search index, you are almost ready tooissue queries using hello .NET SDK.</span></span> <span data-ttu-id="2e1c5-115">Najpierw należy tooobtain jedną hello zapytania api Key który został wygenerowany dla aprowizowanej usługi wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-115">First, you will need tooobtain one of hello query api-keys that was generated for hello search service you provisioned.</span></span> <span data-ttu-id="2e1c5-116">Hello zestawu .NET SDK wyśle ten klucz interfejsu api w usłudze tooyour każdego żądania.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-116">hello .NET SDK will send this api-key on every request tooyour service.</span></span> <span data-ttu-id="2e1c5-117">Mając prawidłowy klucz ustanawia relację zaufania, na podstawie danego żądania między aplikacji hello wysyłanie żądania hello a usługą hello, która je obsługuje.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-117">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="2e1c5-118">toofind klucze interfejsu api usługi możesz zalogować się toohello [portalu Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="2e1c5-118">toofind your service's api-keys you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="2e1c5-119">Przejdź do bloku usługi Azure Search tooyour</span><span class="sxs-lookup"><span data-stu-id="2e1c5-119">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="2e1c5-120">Kliknij ikonę "Klucze" hello</span><span class="sxs-lookup"><span data-stu-id="2e1c5-120">Click on hello "Keys" icon</span></span>

<span data-ttu-id="2e1c5-121">Usługa będzie dysponować *kluczami administratora* i *kluczami zapytań*.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="2e1c5-122">Podstawowego i pomocniczego *kluczy administratora* przyznać pełne prawa tooall operacje, w tym hello możliwości toomanage hello usługi, tworzenia i usuwania indeksów, indeksatorów i źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-122">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="2e1c5-123">Dostępne są dwa klucze, tak, aby można było kontynuować klucza pomocniczego hello toouse, jeśli zdecydujesz, klucz podstawowy hello tooregenerate i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-123">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="2e1c5-124">Twoje *klucze zapytań* przyznać dostęp tylko do odczytu tooindexes i dokumentów i są zwykle rozproszonej tooclient aplikacji, które wysyłają żądania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-124">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="2e1c5-125">Dla celów hello tworzenia zapytań względem indeksu można użyć jednego z dowolnego klucza zapytania.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-125">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="2e1c5-126">Kluczy administratora może także służyć do kwerendy, ale należy używać klucza zapytania w kodzie aplikacji, ponieważ wynika to lepiej hello [zasadą najniższych uprawnień](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="2e1c5-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="2e1c5-127">Utwórz wystąpienie hello klasy SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="2e1c5-127">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="2e1c5-128">tooissue zapytania z hello zestawu .NET SDK usługi Azure Search, konieczne będzie toocreate wystąpienia hello `SearchIndexClient` klasy.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-128">tooissue queries with hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="2e1c5-129">Ta klasa ma kilka konstruktorów.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-129">This class has several constructors.</span></span> <span data-ttu-id="2e1c5-130">Witaj, co ma przyjmuje Twojej nazwy usługi wyszukiwania, nazwę indeksu i `SearchCredentials` jako parametry.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-130">hello one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="2e1c5-131">`SearchCredentials` opakowuje klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="2e1c5-132">Witaj poniższy kod tworzy nową `SearchIndexClient` dla indeksu "hotels" hello (utworzone w [utworzyć indeks usługi Azure Search przy użyciu zestawu .NET SDK hello](search-create-index-dotnet.md)) przy użyciu wartości dla nazwy usługi wyszukiwania hello i klucz interfejsu api, które są przechowywane w pliku konfiguracyjnym aplikacji hello plik (`appsettings.json` w przypadku hello hello [Przykładowa aplikacja](http://aka.ms/search-dotnet-howto)):</span><span class="sxs-lookup"><span data-stu-id="2e1c5-132">hello code below creates a new `SearchIndexClient` for hello "hotels" index (created in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md)) using values for hello search service name and api-key that are stored in hello application's config file (`appsettings.json` in hello case of hello [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="2e1c5-133">`SearchIndexClient` ma właściwość `Documents`.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="2e1c5-134">Ta właściwość zapewnia wszystkie hello metody potrzebne tooquery indeksów usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-134">This property provides all hello methods you need tooquery Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="2e1c5-135">Tworzenie zapytań względem indeksu</span><span class="sxs-lookup"><span data-stu-id="2e1c5-135">Query your index</span></span>
<span data-ttu-id="2e1c5-136">Wyszukiwanie za pomocą zestawu .NET SDK hello jest tak proste, jak wywołanie hello `Documents.Search` metody w Twojej `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-136">Searching with hello .NET SDK is as simple as calling hello `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="2e1c5-137">Ta metoda przyjmuje kilka parametrów, łącznie z tekstem wyszukiwania hello, wraz z `SearchParameters` obiektów, które mogą być używane toofurther Aktualizuj hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-137">This method takes a few parameters, including hello search text, along with a `SearchParameters` object that can be used toofurther refine hello query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="2e1c5-138">Typy zapytań</span><span class="sxs-lookup"><span data-stu-id="2e1c5-138">Types of Queries</span></span>
<span data-ttu-id="2e1c5-139">Witaj dwie główne [typy zapytań](search-query-overview.md#types-of-queries) będą używane są `search` i `filter`.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-139">hello two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="2e1c5-140">Zapytanie `search` umożliwia wyszukanie jednego lub większej liczby terminów we wszystkich polach *z możliwością wyszukiwania* w indeksie.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="2e1c5-141">Zapytanie `filter` ocenia wyrażenie logiczne w odniesieniu do wszystkich pól *z możliwością filtrowania* w indeksie.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="2e1c5-142">Zarówno wyszukiwań i filtrów są wykonywane przy użyciu hello `Documents.Search` metody.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-142">Both searches and filters are performed using hello `Documents.Search` method.</span></span> <span data-ttu-id="2e1c5-143">Zapytania wyszukiwania mogą być przekazywane w hello `searchText` parametru, gdy wyrażenie filtru mogą być przekazywane w hello `Filter` właściwości hello `SearchParameters` klasy.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-143">A search query can be passed in hello `searchText` parameter, while a filter expression can be passed in hello `Filter` property of hello `SearchParameters` class.</span></span> <span data-ttu-id="2e1c5-144">toofilter bez wyszukiwania, po prostu Przekaż `"*"` dla hello `searchText` parametru.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-144">toofilter without searching, just pass `"*"` for hello `searchText` parameter.</span></span> <span data-ttu-id="2e1c5-145">toosearch bez filtrowania, pozostaw hello `Filter` nieustawioną właściwość lub nie są przekazywane w `SearchParameters` wystąpieniu.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-145">toosearch without filtering, just leave hello `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="2e1c5-146">Przykładowe zapytania</span><span class="sxs-lookup"><span data-stu-id="2e1c5-146">Example Queries</span></span>
<span data-ttu-id="2e1c5-147">powitania po przykładowy kod przedstawia na kilka różnych sposobów hello tooquery "hotels" indeks jest zdefiniowany w [utworzyć indeks usługi Azure Search przy użyciu zestawu .NET SDK hello](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="2e1c5-147">hello following sample code shows a few different ways tooquery hello "hotels" index defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="2e1c5-148">Należy zauważyć, że dokumenty hello zwrócone wyniki wyszukiwania hello wystąpień hello `Hotel` klasy, która została zdefiniowana w [Import danych za pomocą usługi Azure Search hello zestawu .NET SDK](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="2e1c5-148">Note that hello documents returned with hello search results are instances of hello `Hotel` class, which was defined in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="2e1c5-149">Witaj przykładowy kod sprawia, że użycie `WriteDocuments` metody toooutput hello wyszukiwania wyniki toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-149">hello sample code makes use of a `WriteDocuments` method toooutput hello search results toohello console.</span></span> <span data-ttu-id="2e1c5-150">Ta metoda została opisana w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-150">This method is described in hello next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
Console.WriteLine("and return hello hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take hello top two results, and show only hotelName and ");
Console.WriteLine("lastRenovationDate:\n");

parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="2e1c5-151">Obsługa wyników wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="2e1c5-151">Handle search results</span></span>
<span data-ttu-id="2e1c5-152">Witaj `Documents.Search` metoda zwraca `DocumentSearchResult` obiekt, który zawiera hello wyniki zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-152">hello `Documents.Search` method returns a `DocumentSearchResult` object that contains hello results of hello query.</span></span> <span data-ttu-id="2e1c5-153">przykład Witaj w poprzedniej sekcji hello używane metody o nazwie `WriteDocuments` toooutput hello wyszukiwania wyniki toohello konsoli:</span><span class="sxs-lookup"><span data-stu-id="2e1c5-153">hello example in hello previous section used a method called `WriteDocuments` toooutput hello search results toohello console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="2e1c5-154">Poniżej przedstawiono wyniki hello wyglądać jak hello zapytań w poprzedniej sekcji hello, przyjmuje hello indeksu "hotels" został wypełniony hello przykładowe dane w [Import danych za pomocą usługi Azure Search hello zestawu .NET SDK](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="2e1c5-154">Here is what hello results look like for hello queries in hello previous section, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search hello entire index for hello term 'budget' and return only hello hotelName field:

Name: Roach Motel

Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close tootown hall and hello river

Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search hello entire index for hello term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="2e1c5-155">Witaj powyższym przykładowym kodzie użyto wyniki wyszukiwania toooutput hello w konsoli.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-155">hello sample code above uses hello console toooutput search results.</span></span> <span data-ttu-id="2e1c5-156">Należy również toodisplay wyniki wyszukiwania w swojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-156">You will likewise need toodisplay search results in your own application.</span></span> <span data-ttu-id="2e1c5-157">Zobacz [tego przykładu w serwisie GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) przykład sposobu wyniki wyszukiwania toorender w aplikacji sieci web opartych na platformie ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="2e1c5-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how toorender search results in an ASP.NET MVC-based web application.</span></span>

