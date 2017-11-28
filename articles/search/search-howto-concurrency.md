---
title: "toomanage aaaHow równoczesnych zapisuje tooresources w usłudze Azure Search"
description: "Użyć optymistycznej współbieżności tooavoid pośredniej lotniczego kolizji w aktualizacji lub usuwania indeksów wyszukiwania tooAzure, indeksatorów i źródeł danych."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a><span data-ttu-id="0e1dd-103">Jak toomanage współbieżność w usłudze Azure Search</span><span class="sxs-lookup"><span data-stu-id="0e1dd-103">How toomanage concurrency in Azure Search</span></span>

<span data-ttu-id="0e1dd-104">Zarządzanie zasobami usługi Azure Search, takich jak indeksy i źródeł danych, jest ważne tooupdate zasobów bezpiecznie, szczególnie w przypadku, gdy zasoby są dostępne jednocześnie różnych składników aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-104">When managing Azure Search resources such as indexes and data sources, it's important tooupdate resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="0e1dd-105">Po dwóch klientów jednocześnie aktualizować zasobu bez koordynacji, wyścigu są możliwe.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="0e1dd-106">tooprevent oferty, usługa Azure Search *modelu optymistycznej współbieżności*.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-106">tooprevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="0e1dd-107">Na zasób nie ma żadnych blokad.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-107">There are no locks on a resource.</span></span> <span data-ttu-id="0e1dd-108">Zamiast tego jest tag ETag dla spowoduje zastąpienie wszystkich zasobów, który określa wersję zasobu hello, dzięki czemu można sformułować żądań, które uniknąć przypadkowego.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-108">Instead, there is an ETag for every resource that identifies hello resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="0e1dd-109">Kod koncepcyjny w [przykładowe rozwiązanie C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) wyjaśniono sposób działania sterowania współbieżnością w usłudze Azure Search.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="0e1dd-110">Kod Hello tworzy warunki, które wywołują formant współbieżności.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-110">hello code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="0e1dd-111">Odczytywanie hello [poniższy fragment kodu](#samplecode) jest prawdopodobnie wystarczający dla deweloperów większości, ale toorun ma on, nazwa usługi hello tooadd appsettings.json edycji i klucz interfejsu api administratora.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-111">Reading hello [code fragment below](#samplecode) is probably sufficient for most developers, but if you want toorun it, edit appsettings.json tooadd hello service name and an admin api-key.</span></span> <span data-ttu-id="0e1dd-112">Podany adres URL usługi `http://myservice.search.windows.net`, nazwa usługi hello jest `myservice`.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-112">Given a service URL of `http://myservice.search.windows.net`, hello service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="0e1dd-113">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="0e1dd-113">How it works</span></span>

<span data-ttu-id="0e1dd-114">Oznacza, że współbieżności jest implementowane za pomocą dostępu warunek sprawdza w wywołaniach interfejsu API zapisywania tooindexes, indeksatorów i źródeł danych oraz synonymMap zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-114">Optimistic concurrency is implemented through access condition checks in API calls writing tooindexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="0e1dd-115">Wszystkie zasoby mają [ *tag jednostki (ETag)* ](https://en.wikipedia.org/wiki/HTTP_ETag) udostępniająca informacje o wersji obiektu.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="0e1dd-116">Sprawdzając hello ETag najpierw, można uniknąć równoczesnych aktualizacji w typowym przepływie pracy (get, zmodyfikuj lokalnie, zaktualizować) przez zapewnienie im dopasowań ETag hello zasób lokalną kopię.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-116">By checking hello ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring hello resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="0e1dd-117">Witaj interfejsu API REST używa [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) na powitania nagłówek żądania.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-117">hello REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello request header.</span></span>
+ <span data-ttu-id="0e1dd-118">Witaj zestawu .NET SDK ustawia hello ETag za pośrednictwem obiektu accessCondition, ustawienie hello [If-Match | Nagłówek If-Match — Brak](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-118">hello .NET SDK sets hello ETag through an accessCondition object, setting hello [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello resource.</span></span> <span data-ttu-id="0e1dd-119">Dowolny obiekt dziedziczących [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) ma obiekt accessCondition.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="0e1dd-120">Za każdym razem, gdy zasób, powoduje automatyczną zmianę jego ETag.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="0e1dd-121">Po zaimplementowaniu zarządzania współbieżności wszystkich wykonywanych obciążające warunku wstępnego na żądanie aktualizacji hello wymagającego zasób zdalny hello toohave hello tego samego ETag jako hello kopię zasobu hello zmodyfikowane na powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-121">When you implement concurrency management, all you're doing is putting a precondition on hello update request that requires hello remote resource toohave hello same ETag as hello copy of hello resource that you modified on hello client.</span></span> <span data-ttu-id="0e1dd-122">Zmiana procesów współbieżnych zasób zdalny hello już hello ETag będzie niezgodna z warunkiem wstępnym hello i HTTP 412 niepowodzenie hello żądania.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-122">If a concurrent process has changed hello remote resource already, hello ETag will not match hello precondition and hello request will fail with HTTP 412.</span></span> <span data-ttu-id="0e1dd-123">Jeśli używasz hello zestawu .NET SDK to manifesty jako `CloudException` gdzie hello `IsAccessConditionFailed()` rozszerzenia metoda zwraca wartość true.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-123">If you're using hello .NET SDK, this manifests as a `CloudException` where hello `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="0e1dd-124">Istnieje tylko jeden mechanizm współbieżności.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="0e1dd-125">Jest on używany zawsze niezależnie od tego, które interfejs API jest używany dla aktualizacji zasobów.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="0e1dd-126">Przypadki użycia i przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="0e1dd-126">Use cases and sample code</span></span>

<span data-ttu-id="0e1dd-127">Witaj następującego kodu przedstawiono accessCondition sprawdza, czy operacje aktualizacji klucza:</span><span class="sxs-lookup"><span data-stu-id="0e1dd-127">hello following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="0e1dd-128">W przypadku hello zasób nie istnieje już w trybie aktualizacji</span><span class="sxs-lookup"><span data-stu-id="0e1dd-128">Fail an update if hello resource no longer exists</span></span>
+ <span data-ttu-id="0e1dd-129">W przypadku zmiany wersji zasobów hello w trybie aktualizacji</span><span class="sxs-lookup"><span data-stu-id="0e1dd-129">Fail an update if hello resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="0e1dd-130">Przykładowy kod z [DotNetETagsExplainer programu](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="0e1dd-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a><span data-ttu-id="0e1dd-131">Wzorzec projektowy</span><span class="sxs-lookup"><span data-stu-id="0e1dd-131">Design pattern</span></span>

<span data-ttu-id="0e1dd-132">Wzorzec projektowania implementacji optymistycznej współbieżności powinna zawierać pętli ponowi próbę sprawdzania warunku hello dostępu test na powitania warunki dostępu, i opcjonalnie pobiera zaktualizowanego zasobu przed podjęciem próby wykonania toore-hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-132">A design pattern for implementing optimistic concurrency should include a loop that retries hello access condition check, a test for hello access condition, and optionally retrieves an updated resource before attempting toore-apply hello changes.</span></span> 

<span data-ttu-id="0e1dd-133">Następujący fragment kodu przedstawia dodanie hello indeksu tooan synonymMap, który już istnieje.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-133">This code snippet illustrates hello addition of a synonymMap tooan index that already exists.</span></span> <span data-ttu-id="0e1dd-134">Ten kod jest z hello [samouczek synonim (wersja zapoznawcza) C# dla usługi Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="0e1dd-134">This code is from hello [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="0e1dd-135">fragment Hello pobiera indeks hello "hotels", sprawdza wersję obiektu hello w przypadku operacji aktualizacji, zgłasza wyjątek, jeśli warunek hello ulegnie awarii, a następnie ponowne próby hello operacji (w górę toothree razy), zaczynając od pobierania o indeksu z powitania serwera tooget hello najnowsza wersja Wersja.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-135">hello snippet gets hello "hotels" index, checks hello object version on an update operation, throws an exception if hello condition fails, and then retries hello operation (up toothree times), starting with index retrieval from hello server tooget hello latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a><span data-ttu-id="0e1dd-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0e1dd-136">Next steps</span></span>

<span data-ttu-id="0e1dd-137">Przejrzyj hello [próbki synonimy C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) więcej kontekstu w sposób toosafely zaktualizować istniejący indeks.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-137">Review hello [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how toosafely update an existing index.</span></span>

<span data-ttu-id="0e1dd-138">Spróbuj zmodyfikować jedną z następujących hello przykłady tooinclude elementy etag lub AccessCondition obiektów.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-138">Try modifying either of hello following samples tooinclude ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="0e1dd-139">Przykładowy interfejs API REST w usłudze Github</span><span class="sxs-lookup"><span data-stu-id="0e1dd-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="0e1dd-140">[Przykład zestawu SDK .NET w witrynie Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="0e1dd-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="0e1dd-141">To rozwiązanie zawiera projekt "DotNetEtagsExplainer" hello, zawierający hello kod przedstawiony w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="0e1dd-141">This solution includes hello "DotNetEtagsExplainer" project containing hello code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="0e1dd-142">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="0e1dd-142">See also</span></span>

  <span data-ttu-id="0e1dd-143">[Typowe nagłówki żądań i odpowiedzi HTTP](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span><span class="sxs-lookup"><span data-stu-id="0e1dd-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="0e1dd-144">[Kody stanu HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [indeksu operacji (interfejsu API REST)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span><span class="sxs-lookup"><span data-stu-id="0e1dd-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>