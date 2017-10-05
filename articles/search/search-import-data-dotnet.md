---
title: "Przekazywanie danych (usługa Azure Search na platformie .NET) | Microsoft Docs"
description: "Dowiedz się, jak przekazywać dane do indeksu w usłudze Azure Search przy użyciu zestawu .NET SDK."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: bdd952869143c6ca6374bb9264db5bcba1f32b50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-net-sdk"></a><span data-ttu-id="deba9-103">Przekazywanie danych do usługi Azure Search przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="deba9-103">Upload data to Azure Search using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="deba9-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="deba9-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="deba9-105">.NET</span><span class="sxs-lookup"><span data-stu-id="deba9-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="deba9-106">REST</span><span class="sxs-lookup"><span data-stu-id="deba9-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="deba9-107">W tym artykule opisano, jak używać [zestawu .NET SDK usługi Azure Search](https://aka.ms/search-sdk) w celu importowania danych do indeksu usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="deba9-107">This article will show you how to use the [Azure Search .NET SDK](https://aka.ms/search-sdk) to import data into an Azure Search index.</span></span>

<span data-ttu-id="deba9-108">Przed rozpoczęciem pracy z tym przewodnikiem powinien zostać [utworzony indeks usługi Azure Search](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="deba9-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="deba9-109">W tym artykule przyjęto również, że już wcześniej utworzono obiekt `SearchServiceClient`, jak pokazano w artykule [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient) (Tworzenie indeksu usługi Azure Search przy użyciu zestawu .NET SDK).</span><span class="sxs-lookup"><span data-stu-id="deba9-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="deba9-110">Cały przykładowy kod przedstawiony w tym artykule został napisany w języku C#.</span><span class="sxs-lookup"><span data-stu-id="deba9-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="deba9-111">Pełny kod źródłowy można znaleźć [w usłudze GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="deba9-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="deba9-112">Można również poczytać o [zestawie SDK platformy .NET dla usługi Azure Search](search-howto-dotnet-sdk.md), aby uzyskać bardziej szczegółowe omówienie przykładowego kodu.</span><span class="sxs-lookup"><span data-stu-id="deba9-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

<span data-ttu-id="deba9-113">Aby wypchnąć dokumenty do indeksu przy użyciu zestawu .NET SDK, konieczne jest wykonanie następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="deba9-113">In order to push documents into your index using the .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="deba9-114">Utworzenie obiektu `SearchIndexClient`, aby połączyć się z indeksem wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="deba9-114">Create a `SearchIndexClient` object to connect to your search index.</span></span>
2. <span data-ttu-id="deba9-115">Utworzenie obiektu `IndexBatch` zawierającego dokumenty przeznaczone do dodania, modyfikacji lub usunięcia.</span><span class="sxs-lookup"><span data-stu-id="deba9-115">Create an `IndexBatch` containing the documents to be added, modified, or deleted.</span></span>
3. <span data-ttu-id="deba9-116">Wywołanie metody `Documents.Index` klasy `SearchIndexClient`, aby wysłać obiekt `IndexBatch` do indeksu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="deba9-116">Call the `Documents.Index` method of your `SearchIndexClient` to send the `IndexBatch` to your search index.</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="deba9-117">Tworzenie wystąpienia klasy SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="deba9-117">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="deba9-118">Aby zaimportować dane do indeksu, używając zestawu .NET SDK usługi Azure Search, konieczne jest utworzenie wystąpienia klasy `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="deba9-118">To import data into your index using the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="deba9-119">Takie wystąpienie można utworzyć samodzielnie, ale, jeśli masz już wystąpienie klasy `SearchServiceClient`, łatwiej jest wywołać jej metodę `Indexes.GetClient`.</span><span class="sxs-lookup"><span data-stu-id="deba9-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance to call its `Indexes.GetClient` method.</span></span> <span data-ttu-id="deba9-120">W poniższym przykładzie przedstawiono, jak można uzyskać klasę `SearchIndexClient` dla indeksu o nazwie „hotels” z klasy `SearchServiceClient` o nazwie `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="deba9-120">For example, here is how you would obtain a `SearchIndexClient` for the index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="deba9-121">W typowej aplikacji wyszukującej wypełnianie indeksu i zarządzanie nim jest obsługiwane przez inny składnik niż zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="deba9-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="deba9-122">`Indexes.GetClient` jest wygodną metodą wypełniania indeksu, ponieważ nie wymaga dostarczenia kolejnej klasy `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="deba9-122">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="deba9-123">Dzieje się tak dzięki przekazaniu klucza administratora, który został użyty w celu utworzenia klasy `SearchServiceClient` do nowej klasy `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="deba9-123">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="deba9-124">Jednak w tej części aplikacji, która wykonuje zapytania, zaleca się utworzenie klasy `SearchIndexClient` bezpośrednio, dzięki czemu można przekazać klucz zapytania zamiast klucza administratora.</span><span class="sxs-lookup"><span data-stu-id="deba9-124">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="deba9-125">Jest to zgodne z [zasadą najniższych uprawnień](https://en.wikipedia.org/wiki/Principle_of_least_privilege) i pomoże zapewnić większe bezpieczeństwo aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deba9-125">This is consistent with the [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help to make your application more secure.</span></span> <span data-ttu-id="deba9-126">Więcej informacji o kluczach administratora i kluczach zapytań można znaleźć w [dokumentacji interfejsu API REST usługi Azure Search](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="deba9-126">You can find out more about admin keys and query keys in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="deba9-127">`SearchIndexClient` ma właściwość `Documents`.</span><span class="sxs-lookup"><span data-stu-id="deba9-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="deba9-128">Ta właściwość zapewnia wszystkie metody, które są potrzebne, aby dodawać, modyfikować i usuwać dokumenty w indeksie oraz wykonywać zapytania o nie.</span><span class="sxs-lookup"><span data-stu-id="deba9-128">This property provides all the methods you need to add, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="deba9-129">Wybieranie akcji indeksowania do użycia</span><span class="sxs-lookup"><span data-stu-id="deba9-129">Decide which indexing action to use</span></span>
<span data-ttu-id="deba9-130">Aby zaimportować dane przy użyciu zestawu .NET SDK, należy spakować dane do obiektu `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="deba9-130">To import data using the .NET SDK, you will need to package up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="deba9-131">Obiekt `IndexBatch` hermetyzuje kolekcję obiektów `IndexAction`, z których każdy zawiera dokument i właściwość, które informują usługę Azure Search, jaką akcję wykonać na tym dokumencie (przekazać, scalić, usunąć itp.).</span><span class="sxs-lookup"><span data-stu-id="deba9-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action to perform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="deba9-132">W zależności od tego, którą z poniższych akcji wybierzesz, tylko określone pola muszą być uwzględnione w danym dokumencie:</span><span class="sxs-lookup"><span data-stu-id="deba9-132">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="deba9-133">Akcja</span><span class="sxs-lookup"><span data-stu-id="deba9-133">Action</span></span> | <span data-ttu-id="deba9-134">Opis</span><span class="sxs-lookup"><span data-stu-id="deba9-134">Description</span></span> | <span data-ttu-id="deba9-135">Wymagane pola dla każdego dokumentu</span><span class="sxs-lookup"><span data-stu-id="deba9-135">Necessary fields for each document</span></span> | <span data-ttu-id="deba9-136">Uwagi</span><span class="sxs-lookup"><span data-stu-id="deba9-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="deba9-137">Akcja `Upload` jest podobna do akcji „upsert”, co oznacza, że dokument zostanie wstawiony, jeśli jest nowy, albo zaktualizowany/zastąpiony, jeśli już istnieje.</span><span class="sxs-lookup"><span data-stu-id="deba9-137">An `Upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="deba9-138">pole klucza oraz inne pola, które chcesz zdefiniować</span><span class="sxs-lookup"><span data-stu-id="deba9-138">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="deba9-139">Podczas aktualizowania/zastępowania istniejącego dokumentu każde pole, które nie jest określone w żądaniu, zostanie ustawione na wartość `null`.</span><span class="sxs-lookup"><span data-stu-id="deba9-139">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="deba9-140">Dzieje się tak nawet wtedy, gdy pole było wcześniej ustawione na wartość inną niż null.</span><span class="sxs-lookup"><span data-stu-id="deba9-140">This occurs even when the field was previously set to a non-null value.</span></span> |
| `Merge` |<span data-ttu-id="deba9-141">Aktualizuje istniejący dokument o określone pola.</span><span class="sxs-lookup"><span data-stu-id="deba9-141">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="deba9-142">Jeśli dokument nie istnieje w indeksie, scalanie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="deba9-142">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="deba9-143">pole klucza oraz inne pola, które chcesz zdefiniować</span><span class="sxs-lookup"><span data-stu-id="deba9-143">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="deba9-144">Wszystkie pola, które określisz w żądaniu scalania, zastąpią istniejące pola w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="deba9-144">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="deba9-145">Obejmuje to również pola typu `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="deba9-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="deba9-146">Jeśli na przykład dokument zawiera pole `tags` o wartości `["budget"]` i wykonywane jest scalanie z wartością `["economy", "pool"]` dla pola `tags`, końcowa wartość pola `tags` będzie równa `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="deba9-146">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="deba9-147">Nie będzie to `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="deba9-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="deba9-148">Ta akcja działa jak akcja `Merge`, jeśli dokument o danym kluczu już istnieje w indeksie.</span><span class="sxs-lookup"><span data-stu-id="deba9-148">This action behaves like `Merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="deba9-149">Jeśli dokument nie istnieje, działa jak akcja `Upload` dla nowego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="deba9-149">If the document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="deba9-150">pole klucza oraz inne pola, które chcesz zdefiniować</span><span class="sxs-lookup"><span data-stu-id="deba9-150">key, plus any other fields you wish to define</span></span> |- |
| `Delete` |<span data-ttu-id="deba9-151">Usuwa określony dokument z indeksu.</span><span class="sxs-lookup"><span data-stu-id="deba9-151">Removes the specified document from the index.</span></span> |<span data-ttu-id="deba9-152">tylko pole klucza</span><span class="sxs-lookup"><span data-stu-id="deba9-152">key only</span></span> |<span data-ttu-id="deba9-153">Wszystkie pola, które określisz oprócz pola klucza, zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="deba9-153">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="deba9-154">Jeśli chcesz usunąć pojedyncze pole z dokumentu, zamiast tej akcji użyj akcji `Merge` i po prostu jawnie ustaw dla pola wartość null.</span><span class="sxs-lookup"><span data-stu-id="deba9-154">If you want to remove an individual field from a document, use `Merge` instead and simply set the field explicitly to null.</span></span> |

<span data-ttu-id="deba9-155">Akcję do użycia możesz określić za pomocą różnych metod statycznych klas `IndexBatch` i `IndexAction`. Pokazano to w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="deba9-155">You can specify what action you want to use with the various static methods of the `IndexBatch` and `IndexAction` classes, as shown in the next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="deba9-156">Konstruowanie obiektu IndexBatch</span><span class="sxs-lookup"><span data-stu-id="deba9-156">Construct your IndexBatch</span></span>
<span data-ttu-id="deba9-157">Teraz, kiedy już wiesz, które akcje wykonać na dokumentach, możesz przystąpić do konstruowania obiektu `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="deba9-157">Now that you know which actions to perform on your documents, you are ready to construct the `IndexBatch`.</span></span> <span data-ttu-id="deba9-158">Poniższy przykład przedstawia sposób tworzenia partii z kilkoma różnymi akcjami.</span><span class="sxs-lookup"><span data-stu-id="deba9-158">The example below shows how to create a batch with a few different actions.</span></span> <span data-ttu-id="deba9-159">Zauważ, że przedstawiony przykład używa niestandardowej klasy o nazwie `Hotel`, która jest mapowana na dokument w indeksie „hotels”.</span><span class="sxs-lookup"><span data-stu-id="deba9-159">Note that our example uses a custom class called `Hotel` that maps to a document in the "hotels" index.</span></span>

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "1",
                BaseRate = 199.0,
                Description = "Best hotel in town",
                DescriptionFr = "Meilleur hôtel en ville",
                HotelName = "Fancy Stay",
                Category = "Luxury",
                Tags = new[] { "pool", "view", "wifi", "concierge" },
                ParkingIncluded = false,
                SmokingAllowed = false,
                LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero),
                Rating = 5,
                Location = GeographyPoint.Create(47.678581, -122.131577)
            }),
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "2",
                BaseRate = 79.99,
                Description = "Cheapest hotel in town",
                DescriptionFr = "Hôtel le moins cher en ville",
                HotelName = "Roach Motel",
                Category = "Budget",
                Tags = new[] { "motel", "budget" },
                ParkingIncluded = true,
                SmokingAllowed = true,
                LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
                Rating = 1,
                Location = GeographyPoint.Create(49.678581, -122.131577)
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close to town hall and the river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="deba9-160">W tym przypadku użyto akcji wyszukiwania `Upload`, `MergeOrUpload` i `Delete` określonych przez metody wywołane względem klasy `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="deba9-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by the methods called on the `IndexAction` class.</span></span>

<span data-ttu-id="deba9-161">Załóżmy, że przedstawiony w przykładzie indeks „hotels” jest już wypełniony różnymi dokumentami.</span><span class="sxs-lookup"><span data-stu-id="deba9-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="deba9-162">Zwróć uwagę na to, że w przypadku akcji `MergeOrUpload` nie było konieczne określenie wszystkich możliwych pól dokumentu. Klucz dokumentu (`HotelId`) został określony tylko w przypadku akcji `Delete`.</span><span class="sxs-lookup"><span data-stu-id="deba9-162">Note how we did not have to specify all the possible document fields when using `MergeOrUpload` and how we only specified the document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="deba9-163">Zauważ również, że pojedyncze żądanie indeksowania może zawierać maksymalnie 1000 dokumentów.</span><span class="sxs-lookup"><span data-stu-id="deba9-163">Also, note that you can only include up to 1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="deba9-164">W tym przykładzie stosujemy różne akcje do różnych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="deba9-164">In this example, we are applying different actions to different documents.</span></span> <span data-ttu-id="deba9-165">Jeśli chcesz wykonać te same akcje dla wszystkich dokumentów w partii, zamiast wywoływać metodę `IndexBatch.New`, możesz użyć innej metody statycznej klasy `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="deba9-165">If you wanted to perform the same actions across all documents in the batch, instead of calling `IndexBatch.New`, you could use the other static methods of `IndexBatch`.</span></span> <span data-ttu-id="deba9-166">Na przykład możesz utworzyć partie przez wywołanie metody `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` lub `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="deba9-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="deba9-167">Te metody przyjmują kolekcję dokumentów (w tym przykładzie obiekty typu `Hotel`) zamiast obiektów `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="deba9-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-to-the-index"></a><span data-ttu-id="deba9-168">Importowanie danych do indeksu</span><span class="sxs-lookup"><span data-stu-id="deba9-168">Import data to the index</span></span>
<span data-ttu-id="deba9-169">Po zainicjowaniu obiektu `IndexBatch` możesz go wysłać do indeksu przez wywołanie metody `Documents.Index` względem obiektu `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="deba9-169">Now that you have an initialized `IndexBatch` object, you can send it to the index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="deba9-170">Poniższy przykład pokazuje, jak wywołać metodę `Index` oraz inne dodatkowe kroki, które należy wykonać:</span><span class="sxs-lookup"><span data-stu-id="deba9-170">The following example shows how to call `Index`, as well as some extra steps you will need to perform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of the documents in
    // the batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log the failed document keys and continue.
    Console.WriteLine(
        "Failed to index some of the documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents to be indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="deba9-171">Zwróć uwagę na blok `try`/`catch` otaczający wywołanie metody `Index`.</span><span class="sxs-lookup"><span data-stu-id="deba9-171">Note the `try`/`catch` surrounding the call to the `Index` method.</span></span> <span data-ttu-id="deba9-172">Blok catch obsługuje ważny przypadek błędu indeksowania.</span><span class="sxs-lookup"><span data-stu-id="deba9-172">The catch block handles an important error case for indexing.</span></span> <span data-ttu-id="deba9-173">Jeśli usługa Azure Search nie może zindeksować niektórych dokumentów w partii, metoda `Documents.Index` zgłasza wyjątek `IndexBatchException`.</span><span class="sxs-lookup"><span data-stu-id="deba9-173">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="deba9-174">Może to nastąpić, jeśli indeksujesz dokumenty w czasie, gdy usługa jest mocno obciążona.</span><span class="sxs-lookup"><span data-stu-id="deba9-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="deba9-175">**Zdecydowanie zalecamy jawną obsługę tego przypadku w kodzie.**</span><span class="sxs-lookup"><span data-stu-id="deba9-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="deba9-176">Możesz opóźnić, a następnie ponowić indeksowanie dokumentów, których przetwarzanie zakończyło się niepowodzeniem, lub możesz zarejestrować błąd i kontynuować, tak jak w prezentowanym przykładzie. Możesz też wykonać inną akcję w zależności od wymagań spójności danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deba9-176">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="deba9-177">Na końcu powyższego przykładu umieszczono dwusekundowe opóźnienie.</span><span class="sxs-lookup"><span data-stu-id="deba9-177">Finally, the code in the example above delays for two seconds.</span></span> <span data-ttu-id="deba9-178">Indeksowanie w usłudze Azure Search jest asynchroniczne, więc przykładowa aplikacja musi czekać przez krótki czas, aby upewnić się, że dokumenty można wyszukiwać.</span><span class="sxs-lookup"><span data-stu-id="deba9-178">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="deba9-179">Tego typu opóźnienia są zazwyczaj konieczne tylko w przypadku pokazów, testów i przykładowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deba9-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="deba9-180">Jak zestaw .NET SDK obsługuje dokumenty</span><span class="sxs-lookup"><span data-stu-id="deba9-180">How the .NET SDK handles documents</span></span>
<span data-ttu-id="deba9-181">Możesz się zastanawiać, jak zestaw .NET SDK usługi Azure Search jest w stanie przekazać wystąpienia klasy zdefiniowanej przez użytkownika, np. `Hotel`, do indeksu.</span><span class="sxs-lookup"><span data-stu-id="deba9-181">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="deba9-182">Aby odpowiedzieć na to pytanie, przyjrzyjmy się klasie `Hotel`, która jest mapowana na schemat indeksu zdefiniowany w artykule [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex) (Tworzenie indeksu usługi Azure Search przy użyciu zestawu .NET SDK):</span><span class="sxs-lookup"><span data-stu-id="deba9-182">To help answer that question, let's look at the `Hotel` class, which maps to the index schema defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }

    // ToString() method omitted for brevity...
}
```

<span data-ttu-id="deba9-183">Przede wszystkim należy zauważyć, że każda właściwość publiczna klasy `Hotel` odpowiada polu w definicji indeksu, ale z jedną istotną różnicą: nazwa każdego pola rozpoczyna się małą literą (camelCase), podczas gdy nazwa każdej właściwości publicznej klasy `Hotel` rozpoczyna się wielką literą (PascalCase).</span><span class="sxs-lookup"><span data-stu-id="deba9-183">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="deba9-184">Jest to częsty przypadek w aplikacjach platformy .NET, które tworzą powiązania danych, gdzie schemat docelowy jest poza kontrolą dewelopera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="deba9-184">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="deba9-185">Zamiast naruszać zasady nazewnictwa platformy .NET przez używanie notacji camelCase dla nazw właściwości, za pomocą atrybutu `[SerializePropertyNamesAsCamelCase]` można określić, że zestaw SDK ma mapować nazwy właściwości na notację camelCase automatycznie.</span><span class="sxs-lookup"><span data-stu-id="deba9-185">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="deba9-186">Zestaw .NET SDK usługi Azure Search korzysta z biblioteki [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) w celu serializacji i deserializacji niestandardowych obiektów modelu do i z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="deba9-186">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="deba9-187">W razie potrzeby możesz dostosować serializację.</span><span class="sxs-lookup"><span data-stu-id="deba9-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="deba9-188">Więcej szczegółowych informacji znajdziesz w sekcji [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet) (Serializacja niestandardowa przy użyciu programu JSON.NET).</span><span class="sxs-lookup"><span data-stu-id="deba9-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="deba9-189">Jako przykład może posłużyć użycie atrybutu `[JsonProperty]` dla właściwości `DescriptionFr` w powyższym kodzie przykładowym.</span><span class="sxs-lookup"><span data-stu-id="deba9-189">One example of this is the use of the `[JsonProperty]` attribute on the `DescriptionFr` property in the sample code above.</span></span>
> 
> 

<span data-ttu-id="deba9-190">Drugą ważną kwestią dotyczącą klasy `Hotel` są typy danych właściwości publicznych.</span><span class="sxs-lookup"><span data-stu-id="deba9-190">The second important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="deba9-191">Typy .NET tych właściwości są mapowane na odpowiadające im typy pól w definicji indeksu.</span><span class="sxs-lookup"><span data-stu-id="deba9-191">The .NET types of these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="deba9-192">Na przykład właściwość ciągu `Category` jest mapowana na pole `category` mające typ `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="deba9-192">For example, the `Category` string property maps to the `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="deba9-193">Podobne mapowania typów występują między typami `bool?` i `DataType.Boolean`, `DateTimeOffset?` i `DataType.DateTimeOffset` itd.</span><span class="sxs-lookup"><span data-stu-id="deba9-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="deba9-194">Dokładne zasady mapowania typów znajdują się w dokumentacji metody `Documents.Get` w [dokumentacji zestawu .NET SDK usługi Azure Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="deba9-194">The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="deba9-195">Ta możliwość używania własnych klas jako dokumentów działa w obu kierunkach. Możesz również pobrać wyniki wyszukiwania i za pomocą zestawu SDK dokonać ich automatycznej deserializacji do wybranego przez Ciebie typu, jak pokazano w [kolejnym artykule](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="deba9-195">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as shown in the [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="deba9-196">Zestaw .NET SDK usługi Azure Search obsługuje również dynamiczne typowanie dokumentów za pomocą klasy `Document`, która stanowi mapowanie klucz/wartość nazw pól na wartości pól.</span><span class="sxs-lookup"><span data-stu-id="deba9-196">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="deba9-197">Jest to przydatne, jeśli nie znasz schematu indeksu w czasie projektowania lub jeśli powiązanie z określonymi klasami modelu jest niedogodne.</span><span class="sxs-lookup"><span data-stu-id="deba9-197">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="deba9-198">Wszystkie metody w zestawie SDK, które obsługują dokumenty, mają przeciążenia działające z klasą `Document`, a także przeciążenia o silnych typach przyjmujące parametr typu ogólnego.</span><span class="sxs-lookup"><span data-stu-id="deba9-198">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="deba9-199">Tylko te ostatnie są używane w przykładowym kodzie w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="deba9-199">Only the latter are used in the sample code in this article.</span></span>
> 
> 

<span data-ttu-id="deba9-200">**Dlaczego należy używać typów danych dopuszczających wartość null**</span><span class="sxs-lookup"><span data-stu-id="deba9-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="deba9-201">Jeśli projektujesz własne klasy modeli na potrzeby mapowania na indeks usługi Azure Search, zalecamy deklarowanie właściwości typów wartości, takich jak `bool` i `int`, aby dopuszczały możliwość użycia wartości null (na przykład `bool?` zamiast `bool`).</span><span class="sxs-lookup"><span data-stu-id="deba9-201">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="deba9-202">W przypadku użycia właściwości niedopuszczającej wartości null musisz **zagwarantować**, że żaden dokument w indeksie nie zawiera wartości null w odpowiednim polu.</span><span class="sxs-lookup"><span data-stu-id="deba9-202">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="deba9-203">Ani zestaw SDK, ani usługa Azure Search nie pomoże Ci tego wymusić.</span><span class="sxs-lookup"><span data-stu-id="deba9-203">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="deba9-204">Nie jest to czysto hipotetyczny problem: wyobraź sobie scenariusz, w którym dodajesz nowe pole do istniejącego indeksu typu `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="deba9-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="deba9-205">Po zaktualizowaniu definicji indeksu wszystkie dokumenty będą miały wartość null dla tego nowego pola (ponieważ wszystkie typy w usłudze Azure Search dopuszczają wartość null).</span><span class="sxs-lookup"><span data-stu-id="deba9-205">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="deba9-206">Jeśli następnie dla tego pola użyjesz klasy modelu z właściwością `int` niedopuszczającą wartości null, podczas próby pobrania dokumentów otrzymasz wyjątek `JsonSerializationException` podobny do poniższego:</span><span class="sxs-lookup"><span data-stu-id="deba9-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="deba9-207">Z tego powodu najlepszym i zalecanym rozwiązaniem jest używanie w klasach modeli typów dopuszczających wartość null.</span><span class="sxs-lookup"><span data-stu-id="deba9-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="deba9-208">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="deba9-208">Next steps</span></span>
<span data-ttu-id="deba9-209">Po wypełnieniu indeksu usługi Azure Search możesz rozpocząć wykonywanie zapytań w celu wyszukania dokumentów.</span><span class="sxs-lookup"><span data-stu-id="deba9-209">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="deba9-210">Aby uzyskać szczegóły, zobacz [Query Your Azure Search Index](search-query-overview.md) (Tworzenie zapytań względem indeksu usługi Azure Search).</span><span class="sxs-lookup"><span data-stu-id="deba9-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

