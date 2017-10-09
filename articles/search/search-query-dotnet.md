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
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a>Tworzenie zapytań względem indeksu usługi Azure Search przy użyciu zestawu .NET SDK hello
> [!div class="op_single_selector"]
> * [Omówienie](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

W tym artykule opisano, jak hello tooquery indeksu przy użyciu [zestawu .NET SDK usługi Azure Search](https://aka.ms/search-sdk).

Przed rozpoczęciem pracy z tym przewodnikiem należy [utworzyć indeks usługi Azure Search](search-what-is-an-index.md) i [wypełnić go danymi](search-what-is-data-import.md).

> [!NOTE]
> Cały przykładowy kod przedstawiony w tym artykule został napisany w języku C#. Można znaleźć hello pełny kod źródłowy [w serwisie GitHub](http://aka.ms/search-dotnet-howto). Możesz przeczytać temat hello [zestawu .NET SDK usługi Azure Search](search-howto-dotnet-sdk.md) do bardziej szczegółowych przechodzenia przez hello próbki kodu.

## <a name="identify-your-azure-search-services-query-api-key"></a>Identyfikowanie klucza api-key zapytania usługi Azure Search
Po utworzeniu indeksu usługi Azure Search, użytkownik jest już prawie gotowe tooissue zapytań przy użyciu hello zestawu .NET SDK. Najpierw należy tooobtain jedną hello zapytania api Key który został wygenerowany dla aprowizowanej usługi wyszukiwania hello. Hello zestawu .NET SDK wyśle ten klucz interfejsu api w usłudze tooyour każdego żądania. Mając prawidłowy klucz ustanawia relację zaufania, na podstawie danego żądania między aplikacji hello wysyłanie żądania hello a usługą hello, która je obsługuje.

1. toofind klucze interfejsu api usługi możesz zalogować się toohello [portalu Azure](https://portal.azure.com/)
2. Przejdź do bloku usługi Azure Search tooyour
3. Kliknij ikonę "Klucze" hello

Usługa będzie dysponować *kluczami administratora* i *kluczami zapytań*.

* Podstawowego i pomocniczego *kluczy administratora* przyznać pełne prawa tooall operacje, w tym hello możliwości toomanage hello usługi, tworzenia i usuwania indeksów, indeksatorów i źródeł danych. Dostępne są dwa klucze, tak, aby można było kontynuować klucza pomocniczego hello toouse, jeśli zdecydujesz, klucz podstawowy hello tooregenerate i na odwrót.
* Twoje *klucze zapytań* przyznać dostęp tylko do odczytu tooindexes i dokumentów i są zwykle rozproszonej tooclient aplikacji, które wysyłają żądania wyszukiwania.

Dla celów hello tworzenia zapytań względem indeksu można użyć jednego z dowolnego klucza zapytania. Kluczy administratora może także służyć do kwerendy, ale należy używać klucza zapytania w kodzie aplikacji, ponieważ wynika to lepiej hello [zasadą najniższych uprawnień](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Utwórz wystąpienie hello klasy SearchIndexClient
tooissue zapytania z hello zestawu .NET SDK usługi Azure Search, konieczne będzie toocreate wystąpienia hello `SearchIndexClient` klasy. Ta klasa ma kilka konstruktorów. Witaj, co ma przyjmuje Twojej nazwy usługi wyszukiwania, nazwę indeksu i `SearchCredentials` jako parametry. `SearchCredentials` opakowuje klucz interfejsu API.

Witaj poniższy kod tworzy nową `SearchIndexClient` dla indeksu "hotels" hello (utworzone w [utworzyć indeks usługi Azure Search przy użyciu zestawu .NET SDK hello](search-create-index-dotnet.md)) przy użyciu wartości dla nazwy usługi wyszukiwania hello i klucz interfejsu api, które są przechowywane w pliku konfiguracyjnym aplikacji hello plik (`appsettings.json` w przypadku hello hello [Przykładowa aplikacja](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

`SearchIndexClient` ma właściwość `Documents`. Ta właściwość zapewnia wszystkie hello metody potrzebne tooquery indeksów usługi Azure Search.

## <a name="query-your-index"></a>Tworzenie zapytań względem indeksu
Wyszukiwanie za pomocą zestawu .NET SDK hello jest tak proste, jak wywołanie hello `Documents.Search` metody w Twojej `SearchIndexClient`. Ta metoda przyjmuje kilka parametrów, łącznie z tekstem wyszukiwania hello, wraz z `SearchParameters` obiektów, które mogą być używane toofurther Aktualizuj hello zapytania.

#### <a name="types-of-queries"></a>Typy zapytań
Witaj dwie główne [typy zapytań](search-query-overview.md#types-of-queries) będą używane są `search` i `filter`. Zapytanie `search` umożliwia wyszukanie jednego lub większej liczby terminów we wszystkich polach *z możliwością wyszukiwania* w indeksie. Zapytanie `filter` ocenia wyrażenie logiczne w odniesieniu do wszystkich pól *z możliwością filtrowania* w indeksie.

Zarówno wyszukiwań i filtrów są wykonywane przy użyciu hello `Documents.Search` metody. Zapytania wyszukiwania mogą być przekazywane w hello `searchText` parametru, gdy wyrażenie filtru mogą być przekazywane w hello `Filter` właściwości hello `SearchParameters` klasy. toofilter bez wyszukiwania, po prostu Przekaż `"*"` dla hello `searchText` parametru. toosearch bez filtrowania, pozostaw hello `Filter` nieustawioną właściwość lub nie są przekazywane w `SearchParameters` wystąpieniu.

#### <a name="example-queries"></a>Przykładowe zapytania
powitania po przykładowy kod przedstawia na kilka różnych sposobów hello tooquery "hotels" indeks jest zdefiniowany w [utworzyć indeks usługi Azure Search przy użyciu zestawu .NET SDK hello](search-create-index-dotnet.md#DefineIndex). Należy zauważyć, że dokumenty hello zwrócone wyniki wyszukiwania hello wystąpień hello `Hotel` klasy, która została zdefiniowana w [Import danych za pomocą usługi Azure Search hello zestawu .NET SDK](search-import-data-dotnet.md#HotelClass). Witaj przykładowy kod sprawia, że użycie `WriteDocuments` metody toooutput hello wyszukiwania wyniki toohello konsoli. Ta metoda została opisana w następnej sekcji hello.

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

## <a name="handle-search-results"></a>Obsługa wyników wyszukiwania
Witaj `Documents.Search` metoda zwraca `DocumentSearchResult` obiekt, który zawiera hello wyniki zapytania hello. przykład Witaj w poprzedniej sekcji hello używane metody o nazwie `WriteDocuments` toooutput hello wyszukiwania wyniki toohello konsoli:

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

Poniżej przedstawiono wyniki hello wyglądać jak hello zapytań w poprzedniej sekcji hello, przyjmuje hello indeksu "hotels" został wypełniony hello przykładowe dane w [Import danych za pomocą usługi Azure Search hello zestawu .NET SDK](search-import-data-dotnet.md):

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

Witaj powyższym przykładowym kodzie użyto wyniki wyszukiwania toooutput hello w konsoli. Należy również toodisplay wyniki wyszukiwania w swojej aplikacji. Zobacz [tego przykładu w serwisie GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) przykład sposobu wyniki wyszukiwania toorender w aplikacji sieci web opartych na platformie ASP.NET MVC.

