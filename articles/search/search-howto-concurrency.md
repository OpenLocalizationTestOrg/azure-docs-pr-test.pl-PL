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
# <a name="how-toomanage-concurrency-in-azure-search"></a>Jak toomanage współbieżność w usłudze Azure Search

Zarządzanie zasobami usługi Azure Search, takich jak indeksy i źródeł danych, jest ważne tooupdate zasobów bezpiecznie, szczególnie w przypadku, gdy zasoby są dostępne jednocześnie różnych składników aplikacji. Po dwóch klientów jednocześnie aktualizować zasobu bez koordynacji, wyścigu są możliwe. tooprevent oferty, usługa Azure Search *modelu optymistycznej współbieżności*. Na zasób nie ma żadnych blokad. Zamiast tego jest tag ETag dla spowoduje zastąpienie wszystkich zasobów, który określa wersję zasobu hello, dzięki czemu można sformułować żądań, które uniknąć przypadkowego.

> [!Tip]
> Kod koncepcyjny w [przykładowe rozwiązanie C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) wyjaśniono sposób działania sterowania współbieżnością w usłudze Azure Search. Kod Hello tworzy warunki, które wywołują formant współbieżności. Odczytywanie hello [poniższy fragment kodu](#samplecode) jest prawdopodobnie wystarczający dla deweloperów większości, ale toorun ma on, nazwa usługi hello tooadd appsettings.json edycji i klucz interfejsu api administratora. Podany adres URL usługi `http://myservice.search.windows.net`, nazwa usługi hello jest `myservice`.

## <a name="how-it-works"></a>Jak to działa

Oznacza, że współbieżności jest implementowane za pomocą dostępu warunek sprawdza w wywołaniach interfejsu API zapisywania tooindexes, indeksatorów i źródeł danych oraz synonymMap zasobów. 

Wszystkie zasoby mają [ *tag jednostki (ETag)* ](https://en.wikipedia.org/wiki/HTTP_ETag) udostępniająca informacje o wersji obiektu. Sprawdzając hello ETag najpierw, można uniknąć równoczesnych aktualizacji w typowym przepływie pracy (get, zmodyfikuj lokalnie, zaktualizować) przez zapewnienie im dopasowań ETag hello zasób lokalną kopię. 

+ Witaj interfejsu API REST używa [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) na powitania nagłówek żądania.
+ Witaj zestawu .NET SDK ustawia hello ETag za pośrednictwem obiektu accessCondition, ustawienie hello [If-Match | Nagłówek If-Match — Brak](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) hello zasobu. Dowolny obiekt dziedziczących [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) ma obiekt accessCondition.

Za każdym razem, gdy zasób, powoduje automatyczną zmianę jego ETag. Po zaimplementowaniu zarządzania współbieżności wszystkich wykonywanych obciążające warunku wstępnego na żądanie aktualizacji hello wymagającego zasób zdalny hello toohave hello tego samego ETag jako hello kopię zasobu hello zmodyfikowane na powitania klienta. Zmiana procesów współbieżnych zasób zdalny hello już hello ETag będzie niezgodna z warunkiem wstępnym hello i HTTP 412 niepowodzenie hello żądania. Jeśli używasz hello zestawu .NET SDK to manifesty jako `CloudException` gdzie hello `IsAccessConditionFailed()` rozszerzenia metoda zwraca wartość true.

> [!Note]
> Istnieje tylko jeden mechanizm współbieżności. Jest on używany zawsze niezależnie od tego, które interfejs API jest używany dla aktualizacji zasobów. 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a>Przypadki użycia i przykładowy kod

Witaj następującego kodu przedstawiono accessCondition sprawdza, czy operacje aktualizacji klucza:

+ W przypadku hello zasób nie istnieje już w trybie aktualizacji
+ W przypadku zmiany wersji zasobów hello w trybie aktualizacji

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a>Przykładowy kod z [DotNetETagsExplainer programu](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)

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

## <a name="design-pattern"></a>Wzorzec projektowy

Wzorzec projektowania implementacji optymistycznej współbieżności powinna zawierać pętli ponowi próbę sprawdzania warunku hello dostępu test na powitania warunki dostępu, i opcjonalnie pobiera zaktualizowanego zasobu przed podjęciem próby wykonania toore-hello zmiany. 

Następujący fragment kodu przedstawia dodanie hello indeksu tooan synonymMap, który już istnieje. Ten kod jest z hello [samouczek synonim (wersja zapoznawcza) C# dla usługi Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk). 

fragment Hello pobiera indeks hello "hotels", sprawdza wersję obiektu hello w przypadku operacji aktualizacji, zgłasza wyjątek, jeśli warunek hello ulegnie awarii, a następnie ponowne próby hello operacji (w górę toothree razy), zaczynając od pobierania o indeksu z powitania serwera tooget hello najnowsza wersja Wersja.

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


## <a name="next-steps"></a>Następne kroki

Przejrzyj hello [próbki synonimy C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) więcej kontekstu w sposób toosafely zaktualizować istniejący indeks.

Spróbuj zmodyfikować jedną z następujących hello przykłady tooinclude elementy etag lub AccessCondition obiektów.

+ [Przykładowy interfejs API REST w usłudze Github](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ [Przykład zestawu SDK .NET w witrynie Github](https://github.com/Azure-Samples/search-dotnet-getting-started). To rozwiązanie zawiera projekt "DotNetEtagsExplainer" hello, zawierający hello kod przedstawiony w tym artykule.

## <a name="see-also"></a>Zobacz też

  [Typowe nagłówki żądań i odpowiedzi HTTP](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)    
  [Kody stanu HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [indeksu operacji (interfejsu API REST)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)