---
title: "AAA \"przekazywanie danych (.NET — usługi Azure Search) | Dokumentacja firmy Microsoft\""
description: "Dowiedz się, jak tooupload indeks tooan danych za pomocą usługi Azure Search hello zestawu .NET SDK."
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
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a><span data-ttu-id="251d8-103">Przekazywanie danych tooAzure wyszukiwania przy użyciu hello zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="251d8-103">Upload data tooAzure Search using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="251d8-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="251d8-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="251d8-105">.NET</span><span class="sxs-lookup"><span data-stu-id="251d8-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="251d8-106">REST</span><span class="sxs-lookup"><span data-stu-id="251d8-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="251d8-107">W tym artykule opisano, jak toouse hello [zestawu .NET SDK usługi Azure Search](https://aka.ms/search-sdk) tooimport danych do indeksu usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="251d8-107">This article will show you how toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="251d8-108">Przed rozpoczęciem pracy z tym przewodnikiem powinien zostać [utworzony indeks usługi Azure Search](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="251d8-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="251d8-109">W tym artykule założono również, że utworzono już `SearchServiceClient` obiektów, jak pokazano w [utworzyć indeks usługi Azure Search przy użyciu zestawu .NET SDK hello](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="251d8-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="251d8-110">Cały przykładowy kod przedstawiony w tym artykule został napisany w języku C#.</span><span class="sxs-lookup"><span data-stu-id="251d8-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="251d8-111">Można znaleźć hello pełny kod źródłowy [w serwisie GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="251d8-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="251d8-112">Możesz przeczytać temat hello [zestawu .NET SDK usługi Azure Search](search-howto-dotnet-sdk.md) do bardziej szczegółowych przechodzenia przez hello próbki kodu.</span><span class="sxs-lookup"><span data-stu-id="251d8-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

<span data-ttu-id="251d8-113">W kolejności toopush dokumenty do indeksu przy użyciu zestawu .NET SDK hello musisz:</span><span class="sxs-lookup"><span data-stu-id="251d8-113">In order toopush documents into your index using hello .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="251d8-114">Utwórz `SearchIndexClient` indeksu wyszukiwania tooyour tooconnect obiektu.</span><span class="sxs-lookup"><span data-stu-id="251d8-114">Create a `SearchIndexClient` object tooconnect tooyour search index.</span></span>
2. <span data-ttu-id="251d8-115">Utwórz `IndexBatch` hello toobe dokumenty zawierające dodane, modyfikacji lub usunięcia.</span><span class="sxs-lookup"><span data-stu-id="251d8-115">Create an `IndexBatch` containing hello documents toobe added, modified, or deleted.</span></span>
3. <span data-ttu-id="251d8-116">Wywołaj hello `Documents.Index` metody z `SearchIndexClient` toosend hello `IndexBatch` tooyour indeksu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="251d8-116">Call hello `Documents.Index` method of your `SearchIndexClient` toosend hello `IndexBatch` tooyour search index.</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="251d8-117">Utwórz wystąpienie hello klasy SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="251d8-117">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="251d8-118">dane tooimport do Twojego indeksu przy użyciu hello zestawu .NET SDK usługi Azure Search, konieczne będzie toocreate wystąpienia hello `SearchIndexClient` klasy.</span><span class="sxs-lookup"><span data-stu-id="251d8-118">tooimport data into your index using hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="251d8-119">Możesz takie wystąpienie można utworzyć samodzielnie, ale można je łatwiej Jeśli masz już `SearchServiceClient` toocall wystąpienia jego `Indexes.GetClient` metody.</span><span class="sxs-lookup"><span data-stu-id="251d8-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance toocall its `Indexes.GetClient` method.</span></span> <span data-ttu-id="251d8-120">Na przykład, Oto, jak można uzyskać `SearchIndexClient` hello indeksu o nazwie "hotels" z `SearchServiceClient` o nazwie `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="251d8-120">For example, here is how you would obtain a `SearchIndexClient` for hello index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="251d8-121">W typowej aplikacji wyszukującej wypełnianie indeksu i zarządzanie nim jest obsługiwane przez inny składnik niż zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="251d8-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="251d8-122">`Indexes.GetClient`jest wygodną metodą wypełniania indeksu, ponieważ wymaga dostarczenia kolejnej hello `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="251d8-122">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="251d8-123">Robi to przez przekazanie klucza administratora hello tego możesz używane toocreate hello `SearchServiceClient` toohello nowe `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="251d8-123">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="251d8-124">Jednak w hello część aplikacji, która wykonuje zapytania jest lepsze hello toocreate `SearchIndexClient` bezpośrednio, aby można przekazać klucz zapytania zamiast klucza administratora.</span><span class="sxs-lookup"><span data-stu-id="251d8-124">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="251d8-125">Jest to zgodne z hello [zasadą najniższych uprawnień](https://en.wikipedia.org/wiki/Principle_of_least_privilege) i pomoże toomake aplikacji bardziej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="251d8-125">This is consistent with hello [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help toomake your application more secure.</span></span> <span data-ttu-id="251d8-126">Można dowiedzieć się więcej o kluczach administratora i kluczach zapytań w hello [dokumentacji interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="251d8-126">You can find out more about admin keys and query keys in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="251d8-127">`SearchIndexClient` ma właściwość `Documents`.</span><span class="sxs-lookup"><span data-stu-id="251d8-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="251d8-128">Ta właściwość zapewnia wszystkie metody hello należy tooadd, modyfikować lub zbadać dokumenty w indeksie.</span><span class="sxs-lookup"><span data-stu-id="251d8-128">This property provides all hello methods you need tooadd, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="251d8-129">Zdecyduj, które indeksowania toouse akcji</span><span class="sxs-lookup"><span data-stu-id="251d8-129">Decide which indexing action toouse</span></span>
<span data-ttu-id="251d8-130">tooimport danych przy użyciu zestawu .NET SDK hello, konieczne będzie toopackage danych do `IndexBatch` obiektu.</span><span class="sxs-lookup"><span data-stu-id="251d8-130">tooimport data using hello .NET SDK, you will need toopackage up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="251d8-131">`IndexBatch` Hermetyzuje kolekcję `IndexAction` obiektów, z których każdy zawiera dokument i właściwość, która powoduje tooperform jakie działania usługi Azure Search w tym dokumencie (przekazywania, scalania, delete itd.).</span><span class="sxs-lookup"><span data-stu-id="251d8-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action tooperform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="251d8-132">W zależności od tego, który hello poniższych akcji, którą wybierzesz tylko niektóre pola muszą być uwzględnione w danym dokumencie:</span><span class="sxs-lookup"><span data-stu-id="251d8-132">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="251d8-133">Akcja</span><span class="sxs-lookup"><span data-stu-id="251d8-133">Action</span></span> | <span data-ttu-id="251d8-134">Opis</span><span class="sxs-lookup"><span data-stu-id="251d8-134">Description</span></span> | <span data-ttu-id="251d8-135">Wymagane pola dla każdego dokumentu</span><span class="sxs-lookup"><span data-stu-id="251d8-135">Necessary fields for each document</span></span> | <span data-ttu-id="251d8-136">Uwagi</span><span class="sxs-lookup"><span data-stu-id="251d8-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="251d8-137">`Upload` Akcji jest podobne tooan "upsert", gdzie hello dokument zostanie wstawiony, jeśli jest nowy albo zaktualizowany/zastąpiony, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="251d8-137">An `Upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="251d8-138">pole klucza oraz inne pola mają toodefine</span><span class="sxs-lookup"><span data-stu-id="251d8-138">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="251d8-139">Podczas aktualizowania/zastępowania istniejącego dokumentu, wszystkie pola, które nie jest określony w żądaniu hello ma ustawione zbyt`null`.</span><span class="sxs-lookup"><span data-stu-id="251d8-139">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="251d8-140">Dzieje się tak nawet wtedy, gdy hello pole było wcześniej ustawione tooa wartość inną niż null.</span><span class="sxs-lookup"><span data-stu-id="251d8-140">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `Merge` |<span data-ttu-id="251d8-141">Aktualizacje istniejący dokument o hello określone pola.</span><span class="sxs-lookup"><span data-stu-id="251d8-141">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="251d8-142">Jeśli hello dokument nie istnieje w indeksie hello, hello scalanie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="251d8-142">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="251d8-143">pole klucza oraz inne pola mają toodefine</span><span class="sxs-lookup"><span data-stu-id="251d8-143">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="251d8-144">Wszystkie pola, które określisz w żądaniu scalania zastąpi istniejące pole hello w dokumencie hello.</span><span class="sxs-lookup"><span data-stu-id="251d8-144">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="251d8-145">Obejmuje to również pola typu `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="251d8-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="251d8-146">Na przykład, jeśli hello dokument zawiera pole `tags` z wartością `["budget"]` i wykonywane jest scalanie z wartością `["economy", "pool"]` dla `tags`, końcowa wartość hello hello `tags` pole będzie `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="251d8-146">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="251d8-147">Nie będzie to `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="251d8-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="251d8-148">Ta akcja działa jak `Merge` Jeśli dokument o hello podany klucz już istnieje w indeksie hello.</span><span class="sxs-lookup"><span data-stu-id="251d8-148">This action behaves like `Merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="251d8-149">Jeśli dokument hello nie istnieje, działa jak akcja `Upload` dla nowego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="251d8-149">If hello document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="251d8-150">pole klucza oraz inne pola mają toodefine</span><span class="sxs-lookup"><span data-stu-id="251d8-150">key, plus any other fields you wish toodefine</span></span> |- |
| `Delete` |<span data-ttu-id="251d8-151">Usuwa określony dokument hello z hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="251d8-151">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="251d8-152">tylko pole klucza</span><span class="sxs-lookup"><span data-stu-id="251d8-152">key only</span></span> |<span data-ttu-id="251d8-153">Wszystkie pola, które określisz oprócz pola klucza hello zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="251d8-153">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="251d8-154">Tooremove pojedyncze pole z dokumentu, należy użyć `Merge` zamiast i po prostu jawnie ustaw pola hello toonull.</span><span class="sxs-lookup"><span data-stu-id="251d8-154">If you want tooremove an individual field from a document, use `Merge` instead and simply set hello field explicitly toonull.</span></span> |

<span data-ttu-id="251d8-155">Można określić, jakie działanie ma toouse z różnych metod statycznych hello hello `IndexBatch` i `IndexAction` klasy, jak pokazano w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="251d8-155">You can specify what action you want toouse with hello various static methods of hello `IndexBatch` and `IndexAction` classes, as shown in hello next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="251d8-156">Konstruowanie obiektu IndexBatch</span><span class="sxs-lookup"><span data-stu-id="251d8-156">Construct your IndexBatch</span></span>
<span data-ttu-id="251d8-157">Teraz, znając tooperform akcje, które z dokumentami są gotowe tooconstruct hello `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="251d8-157">Now that you know which actions tooperform on your documents, you are ready tooconstruct hello `IndexBatch`.</span></span> <span data-ttu-id="251d8-158">Witaj przykład poniżej przedstawiono sposób toocreate partii z kilkoma różnymi akcjami.</span><span class="sxs-lookup"><span data-stu-id="251d8-158">hello example below shows how toocreate a batch with a few different actions.</span></span> <span data-ttu-id="251d8-159">Należy pamiętać, że przedstawiony przykład używa niestandardowej klasy o nazwie `Hotel` mapujący tooa dokument w indeksie "hotels" hello.</span><span class="sxs-lookup"><span data-stu-id="251d8-159">Note that our example uses a custom class called `Hotel` that maps tooa document in hello "hotels" index.</span></span>

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
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="251d8-160">W tym przypadku użyto `Upload`, `MergeOrUpload`, i `Delete` jako akcje wyszukiwania określonych hello metody wywołane względem hello `IndexAction` klasy.</span><span class="sxs-lookup"><span data-stu-id="251d8-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by hello methods called on hello `IndexAction` class.</span></span>

<span data-ttu-id="251d8-161">Załóżmy, że przedstawiony w przykładzie indeks „hotels” jest już wypełniony różnymi dokumentami.</span><span class="sxs-lookup"><span data-stu-id="251d8-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="251d8-162">Należy zwrócić uwagę, jak firma Microsoft nie miał toospecify wszystkich hello możliwych pól dokumentu przy użyciu `MergeOrUpload` tylko określony klucz dokumentu hello (`HotelId`) przy użyciu `Delete`.</span><span class="sxs-lookup"><span data-stu-id="251d8-162">Note how we did not have toospecify all hello possible document fields when using `MergeOrUpload` and how we only specified hello document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="251d8-163">Ponadto należy pamiętać, że może zawierać tylko dokumentów too1000 pojedyncze żądanie indeksowania.</span><span class="sxs-lookup"><span data-stu-id="251d8-163">Also, note that you can only include up too1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="251d8-164">W tym przykładzie stosujemy różne akcje toodifferent dokumentów.</span><span class="sxs-lookup"><span data-stu-id="251d8-164">In this example, we are applying different actions toodifferent documents.</span></span> <span data-ttu-id="251d8-165">Jeśli potrzebujesz tooperform hello same akcje dla wszystkich dokumentów w partii hello, zamiast wywoływać metodę `IndexBatch.New`, można użyć innych metod statycznych hello `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="251d8-165">If you wanted tooperform hello same actions across all documents in hello batch, instead of calling `IndexBatch.New`, you could use hello other static methods of `IndexBatch`.</span></span> <span data-ttu-id="251d8-166">Na przykład możesz utworzyć partie przez wywołanie metody `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` lub `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="251d8-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="251d8-167">Te metody przyjmują kolekcję dokumentów (w tym przykładzie obiekty typu `Hotel`) zamiast obiektów `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="251d8-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-toohello-index"></a><span data-ttu-id="251d8-168">Importowanie danych toohello indeksu</span><span class="sxs-lookup"><span data-stu-id="251d8-168">Import data toohello index</span></span>
<span data-ttu-id="251d8-169">Są już zainicjowane `IndexBatch` obiektu, możesz go wysłać toohello indeksu przez wywołanie metody `Documents.Index` na Twojej `SearchIndexClient` obiektu.</span><span class="sxs-lookup"><span data-stu-id="251d8-169">Now that you have an initialized `IndexBatch` object, you can send it toohello index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="251d8-170">powitania po przykładzie pokazano, jak toocall `Index`oraz inne dodatkowe kroki, konieczne będzie tooperform:</span><span class="sxs-lookup"><span data-stu-id="251d8-170">hello following example shows how toocall `Index`, as well as some extra steps you will need tooperform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
    // hello batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log hello failed document keys and continue.
    Console.WriteLine(
        "Failed tooindex some of hello documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents toobe indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="251d8-171">Uwaga hello `try` / `catch` otaczającego hello wywołania toohello `Index` metody.</span><span class="sxs-lookup"><span data-stu-id="251d8-171">Note hello `try`/`catch` surrounding hello call toohello `Index` method.</span></span> <span data-ttu-id="251d8-172">Witaj blok catch obsługuje ważny przypadek błędu indeksowania.</span><span class="sxs-lookup"><span data-stu-id="251d8-172">hello catch block handles an important error case for indexing.</span></span> <span data-ttu-id="251d8-173">Jeśli usługi Azure Search nie powiedzie się tooindex niektóre hello dokumentów w partii hello `IndexBatchException` jest generowany przez `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="251d8-173">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="251d8-174">Może to nastąpić, jeśli indeksujesz dokumenty w czasie, gdy usługa jest mocno obciążona.</span><span class="sxs-lookup"><span data-stu-id="251d8-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="251d8-175">**Zdecydowanie zalecamy jawną obsługę tego przypadku w kodzie.**</span><span class="sxs-lookup"><span data-stu-id="251d8-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="251d8-176">Można opóźnić, a następnie ponów próbę indeksowania hello dokumentów, których nie powiodła się lub zaloguj się i kontynuować jak w prezentowanym przykładzie hello, lub możesz też wykonać inną akcję w zależności od wymagań spójności danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="251d8-176">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="251d8-177">Na koniec hello kod w przykładzie hello powyżej umieszczono dwusekundowe opóźnienie.</span><span class="sxs-lookup"><span data-stu-id="251d8-177">Finally, hello code in hello example above delays for two seconds.</span></span> <span data-ttu-id="251d8-178">Indeksowanie odbywa się asynchronicznie w usłudze Azure Search tak hello Przykładowa aplikacja musi toowait tooensure krótki czas, że hello dokumenty można wyszukiwać.</span><span class="sxs-lookup"><span data-stu-id="251d8-178">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="251d8-179">Tego typu opóźnienia są zazwyczaj konieczne tylko w przypadku pokazów, testów i przykładowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="251d8-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="251d8-180">Jak hello zestawu .NET SDK obsługuje dokumenty</span><span class="sxs-lookup"><span data-stu-id="251d8-180">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="251d8-181">Możesz się zastanawiać, jak hello zestawu .NET SDK usługi Azure Search jest tooupload stanie wystąpienia klasy zdefiniowanej przez użytkownika, jak `Hotel` toohello indeksu.</span><span class="sxs-lookup"><span data-stu-id="251d8-181">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="251d8-182">toohelp odpowiedzi na to pytanie, Przyjrzyjmy się hello `Hotel` klasy, która mapuje toohello schemat indeksu zdefiniowany w [utworzyć indeks usługi Azure Search przy użyciu zestawu .NET SDK hello](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="251d8-182">toohelp answer that question, let's look at hello `Hotel` class, which maps toohello index schema defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

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

<span data-ttu-id="251d8-183">Witaj po pierwsze toonotice jest to, że każda właściwość publiczna klasy `Hotel` odpowiada tooa pola w definicji indeksu hello, ale z jedną istotną różnicą: hello nazwę każdego pola rozpoczyna się małą literą (camelcase"), podczas hello nazwę każdego publicznego Właściwość `Hotel` rozpoczyna się wielką literą ("Pascal litery").</span><span class="sxs-lookup"><span data-stu-id="251d8-183">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="251d8-184">To typowy scenariusz w aplikacjach .NET, które tworzą powiązania danych, gdzie schemat docelowy hello jest poza hello kontroli Deweloper aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="251d8-184">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="251d8-185">Zamiast tooviolate hello zasady nazewnictwa platformy .NET dokonując camelcase nazwy właściwości, można ustalić hello SDK toomap hello właściwość nazwy toocamel przypadku automatycznie z hello `[SerializePropertyNamesAsCamelCase]` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="251d8-185">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="251d8-186">Witaj zestawu .NET SDK usługi Azure Search korzysta hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize biblioteki i deserializacji tooand obiekty z modelu niestandardowych z formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="251d8-186">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="251d8-187">W razie potrzeby możesz dostosować serializację.</span><span class="sxs-lookup"><span data-stu-id="251d8-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="251d8-188">Więcej szczegółowych informacji znajdziesz w sekcji [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet) (Serializacja niestandardowa przy użyciu programu JSON.NET).</span><span class="sxs-lookup"><span data-stu-id="251d8-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="251d8-189">Przykładem tego jest użycie hello hello `[JsonProperty]` atrybutu na powitania `DescriptionFr` właściwości w powyższym kodzie przykładowym hello.</span><span class="sxs-lookup"><span data-stu-id="251d8-189">One example of this is hello use of hello `[JsonProperty]` attribute on hello `DescriptionFr` property in hello sample code above.</span></span>
> 
> 

<span data-ttu-id="251d8-190">Witaj drugą ważną kwestią dotyczącą hello `Hotel` hello typy danych właściwości publicznych hello są klasy.</span><span class="sxs-lookup"><span data-stu-id="251d8-190">hello second important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="251d8-191">Hello typy .NET tych właściwości mapy typy pól równoważne tootheir w definicji indeksu hello.</span><span class="sxs-lookup"><span data-stu-id="251d8-191">hello .NET types of these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="251d8-192">Na przykład Witaj `Category` toohello mapy właściwości ciągu `category` pola, które jest typu `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="251d8-192">For example, hello `Category` string property maps toohello `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="251d8-193">Podobne mapowania typów występują między typami `bool?` i `DataType.Boolean`, `DateTimeOffset?` i `DataType.DateTimeOffset` itd.</span><span class="sxs-lookup"><span data-stu-id="251d8-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="251d8-194">dokładne zasady mapowania typu hello Hello są udokumentowane hello `Documents.Get` metoda hello [odwołanie do zestawu .NET SDK usługi Azure Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="251d8-194">hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="251d8-195">Ta toouse możliwości własnych klas jako dokumentów działa w obu kierunkach; Można również pobrać wyniki wyszukiwania i hello zestawu SDK dokonać ich automatycznej deserializacji typu tooa wybranych przez użytkownika, jak pokazano w hello [kolejnym artykule](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="251d8-195">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as shown in hello [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="251d8-196">Witaj zestawu .NET SDK usługi Azure Search obsługuje również dynamiczne typowanie dokumentów za pomocą hello `Document` klasy, która jest mapowanie klucz/wartość, wartości toofield nazw pól.</span><span class="sxs-lookup"><span data-stu-id="251d8-196">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="251d8-197">Jest to przydatne w scenariuszach, jeśli nie znasz schematu indeksu hello w czasie projektowania lub gdy byłoby niewygodne toobind toospecific modelu klasy.</span><span class="sxs-lookup"><span data-stu-id="251d8-197">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="251d8-198">Wszystkie metody hello w hello zestawu SDK, które obsługują dokumenty mają przeciążenia działające z hello `Document` klasy, a także przeciążenia o silnych typach, które przyjmują parametr typu ogólnego.</span><span class="sxs-lookup"><span data-stu-id="251d8-198">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="251d8-199">Tylko hello te ostatnie są używane w hello przykładowy kod w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="251d8-199">Only hello latter are used in hello sample code in this article.</span></span>
> 
> 

<span data-ttu-id="251d8-200">**Dlaczego należy używać typów danych dopuszczających wartość null**</span><span class="sxs-lookup"><span data-stu-id="251d8-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="251d8-201">Podczas projektowania indeksu własne modelu klasy toomap tooan usługi Azure Search, zalecamy deklarowanie właściwości typów wartości, takich jak `bool` i `int` toobe wartości null (na przykład `bool?` zamiast `bool`).</span><span class="sxs-lookup"><span data-stu-id="251d8-201">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="251d8-202">Użycie wartości null właściwość masz zbyt**zagwarantować** że żaden dokument w indeksie nie zawiera wartości null dla odpowiednich pól hello.</span><span class="sxs-lookup"><span data-stu-id="251d8-202">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="251d8-203">Hello zestawu SDK ani hello usługi Azure Search nie pomoże tooenforce należy to.</span><span class="sxs-lookup"><span data-stu-id="251d8-203">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="251d8-204">To nie jest to czysto hipotetyczny problem: Wyobraź sobie scenariusz, w którym dodajesz nowe pole tooan istniejącego indeksu typu `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="251d8-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="251d8-205">Po zaktualizowaniu definicji indeksu hello, wszystkie dokumenty będą miały wartość null dla tego nowego pola (ponieważ wszystkie typy dopuszczają wartości null w usłudze Azure Search).</span><span class="sxs-lookup"><span data-stu-id="251d8-205">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="251d8-206">Jeśli następnie użyjesz klasy modelu z niedopuszczającą `int` właściwości dla tego pola, otrzymasz `JsonSerializationException` podobny podczas próby tooretrieve dokumentów:</span><span class="sxs-lookup"><span data-stu-id="251d8-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="251d8-207">Z tego powodu najlepszym i zalecanym rozwiązaniem jest używanie w klasach modeli typów dopuszczających wartość null.</span><span class="sxs-lookup"><span data-stu-id="251d8-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="251d8-208">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="251d8-208">Next steps</span></span>
<span data-ttu-id="251d8-209">Po wypełnieniu indeksu usługi Azure Search, będzie gotowy toostart wystawiania toosearch zapytań dla dokumentów.</span><span class="sxs-lookup"><span data-stu-id="251d8-209">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="251d8-210">Aby uzyskać szczegóły, zobacz [Query Your Azure Search Index](search-query-overview.md) (Tworzenie zapytań względem indeksu usługi Azure Search).</span><span class="sxs-lookup"><span data-stu-id="251d8-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

