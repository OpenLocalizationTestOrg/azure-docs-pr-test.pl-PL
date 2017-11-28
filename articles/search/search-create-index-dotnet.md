---
title: "AAA \"Tworzenie indeksu (interfejs API .NET — usługi Azure Search) | Dokumentacja firmy Microsoft\""
description: "Tworzenie indeksu za pomocą zestawu .NET SDK usługi Azure Search hello kodu."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 3a851647-fc7b-4fb6-8506-6aaa519e77cd
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 7fa4030b8c3565bc02b1d6bb4426331657cf3a5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-net-sdk"></a>Tworzenie indeksu usługi Azure Search przy użyciu hello zestawu .NET SDK
> [!div class="op_single_selector"]
> * [Omówienie](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

W tym artykule przeprowadzi Cię przez proces tworzenia usługi Azure Search hello [indeksu](https://docs.microsoft.com/rest/api/searchservice/Create-Index) przy użyciu hello [zestawu .NET SDK usługi Azure Search](https://aka.ms/search-sdk).

Przed rozpoczęciem pracy z przewodnikiem oraz przed utworzeniem indeksu powinna zostać [utworzona usługa Azure Search](search-create-service-portal.md).

> [!NOTE]
> Cały przykładowy kod przedstawiony w tym artykule został napisany w języku C#. Można znaleźć hello pełny kod źródłowy [w serwisie GitHub](http://aka.ms/search-dotnet-howto). Możesz przeczytać temat hello [zestawu .NET SDK usługi Azure Search](search-howto-dotnet-sdk.md) do bardziej szczegółowych przechodzenia przez hello próbki kodu.


## <a name="identify-your-azure-search-services-admin-api-key"></a>Identyfikowanie klucza api-key administratora usługi Azure Search
Po aprowizowaniu usługi Azure Search, jesteś już prawie gotowe tooissue żądań względem punktu końcowego usługi za pomocą hello zestawu .NET SDK. Najpierw należy tooobtain jedną hello api Key administratora który został wygenerowany dla aprowizowanej usługi wyszukiwania hello. Hello zestawu .NET SDK wyśle ten klucz interfejsu api w usłudze tooyour każdego żądania. Mając prawidłowy klucz ustanawia relację zaufania, na podstawie danego żądania między aplikacji hello wysyłanie żądania hello a usługą hello, która je obsługuje.

1. toofind z usługą api Key, zaloguj się toohello [portalu Azure](https://portal.azure.com/)
2. Przejdź do bloku usługi Azure Search tooyour
3. Kliknij ikonę "Klucze" hello

Usługa będzie dysponować *kluczami administratora* i *kluczami zapytań*.

* Podstawowego i pomocniczego *kluczy administratora* przyznać pełne prawa tooall operacje, w tym hello możliwości toomanage hello usługi, tworzenia i usuwania indeksów, indeksatorów i źródeł danych. Dostępne są dwa klucze, tak, aby można było kontynuować klucza pomocniczego hello toouse, jeśli zdecydujesz, klucz podstawowy hello tooregenerate i na odwrót.
* Twoje *klucze zapytań* przyznać dostęp tylko do odczytu tooindexes i dokumentów i są zwykle rozproszonej tooclient aplikacji, które wysyłają żądania wyszukiwania.

Dla celów hello Tworzenie indeksu, możesz użyć dowolnej z podstawowego i pomocniczego klucza administratora.

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-hello-searchserviceclient-class"></a>Utwórz wystąpienie hello klasy SearchServiceClient
przy użyciu toostart hello zestawu .NET SDK usługi Azure Search, konieczne będzie toocreate wystąpienia hello `SearchServiceClient` klasy. Ta klasa ma kilka konstruktorów. Witaj, co ma przyjmuje nazwę usługi wyszukiwania i `SearchCredentials` jako parametry. `SearchCredentials` opakowuje klucz interfejsu API.

Witaj poniższy kod tworzy nową `SearchServiceClient` przy użyciu wartości dla nazwy usługi wyszukiwania hello i klucz interfejsu api, które są przechowywane w pliku konfiguracyjnym aplikacji hello (`appsettings.json` w przypadku hello hello [Przykładowa aplikacja](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

`SearchServiceClient` ma właściwość `Indexes`. Ta właściwość zapewnia wszystkie metody hello muszą toocreate, listy, aktualizacji lub usuwania indeksów usługi Azure Search.

> [!NOTE]
> Witaj `SearchServiceClient` klasa zarządza usługi wyszukiwania tooyour połączenia. W kolejności tooavoid otwarcia zbyt wielu połączeń, należy spróbować tooshare pojedyncze wystąpienie `SearchServiceClient` w miarę możliwości aplikacji. Metody są wątkowo tooenable rodzaju udostępnianie.
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a>Definiowanie indeksu usługi Azure Search
Toohello jednego wywołania `Indexes.Create` metody spowoduje utworzenie indeksu. Ta metoda przyjmuje jako parametr obiekt `Index`, który definiuje indeks usługi Azure Search. Należy toocreate `Index` i zainicjować go w następujący sposób:

1. Zestaw hello `Name` właściwości hello `Index` nazwa obiektu toohello Twojego indeksu.
2. Zestaw hello `Fields` właściwości hello `Index` obiektu tooan tablicę `Field` obiektów. Witaj Najprostszym sposobem toocreate Witaj `Field` obiektów jest przez wywołanie hello `FieldBuilder.BuildForType` jest metoda klasę modelu dla parametru typu hello. Klasa modelu ma właściwości, które mapują pola toohello Twojego indeksu. Dzięki temu dokumenty toobind Twojego tooinstances indeksu wyszukiwania klasy modelu.

> [!NOTE]
> Jeśli nie planujesz toouse klasę modelu, nadal można zdefiniować indeksu, tworząc `Field` obiekty bezpośrednio. Można podać nazwę hello hello pola toohello konstruktora, wraz z hello — typ danych (lub analizator w przypadku pól ciągów). Możesz również ustawić inne właściwości, takie jak `IsSearchable`, `IsFilterable` itp.
>
>

Należy pamiętać o Twojej wyszukiwania użytkownika oraz o potrzebach biznesowych na uwadze podczas projektowania indeksu jako każdego pola należy przypisać hello jest [odpowiednie właściwości](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Te właściwości kontrolują, które funkcje wyszukiwania (filtrowanie, tworzenie aspektów, sortowanie, wyszukiwanie pełnotekstowe itp.) mają zastosowanie toowhich pola. Dla każdej właściwości, nie zostanie jawnie ustawiona hello `Field` klasy domyślne toodisabling hello odpowiednia funkcja wyszukiwania, chyba że jawnie włączyć.

W naszym przykładzie indeksowi nadaliśmy nazwę „hotels”, a pola zdefiniowaliśmy przy użyciu klasy modelu. Każda właściwość klasy modelu hello ma atrybuty, które określają zachowania związane z wyszukiwania hello hello odpowiedni indeks pola. Klasa modelu Hello jest zdefiniowane w następujący sposób:

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
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
}
```

Starannie Wybraliśmy atrybuty powitania dla każdej właściwości w oparciu o jak naszym zdaniem będą używane w aplikacji. Na przykład jest prawdopodobne, że osoby szukające hoteli będzie interesować dopasowanie słów kluczowych na powitania `description` pola, dlatego włączyliśmy wyszukiwanie pełnotekstowe dla tego pola przez dodanie hello `IsSearchable` atrybutu toohello `Description` właściwości.

Należy pamiętać, że dokładnie jedno pole w indeksie typu `string` muszą być Witaj wyznaczone jako hello *klucza* przez dodanie hello `Key` atrybutu (zobacz `HotelId` w hello powyżej przykładzie).

Powyższa definicja indeksu Hello używa analizatora języka dla hello `description_fr` pola, ponieważ jest to zamierzone toostore tekstu w języku francuskim. Zobacz [tematu obsługi Language hello](https://docs.microsoft.com/rest/api/searchservice/Language-support) oraz hello odpowiadającego [wpis w blogu](https://azure.microsoft.com/blog/language-support-in-azure-search/) Aby uzyskać więcej informacji o analizatorach języka.

> [!NOTE]
> Domyślnie nazwa każdej właściwości w klasie modelu hello jest używana jako nazwa hello hello odpowiednie pola w indeksie hello. Toomap wszystkie nazwy pola przypadku toocamel nazwy właściwości, oznaczyć hello klasy hello `SerializePropertyNamesAsCamelCase` atrybutu. Jeśli chcesz toomap tooa inną nazwę, możesz użyć hello `JsonProperty` atrybutów, takich jak hello `DescriptionFr` właściwości powyżej. Witaj `JsonProperty` atrybutu mają pierwszeństwo przed hello `SerializePropertyNamesAsCamelCase` atrybutu.
> 
> 

Zdefiniowaliśmy już klasę modelu, dlatego z łatwością możemy utworzyć definicję indeksu:

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-hello-index"></a>Tworzenie indeksu hello
Teraz, gdy masz zainicjowane `Index` obiekt, utworzenie hello indeksu przez wywołanie metody `Indexes.Create` na Twojej `SearchServiceClient` obiektu:

```csharp
serviceClient.Indexes.Create(definition);
```

Na żądanie zakończy się powodzeniem hello metoda zwróci dane normalnie. W przypadku problemu z żądaniem hello, takiego jak nieprawidłowy parametr hello metoda zgłosi `CloudException`.

Gdy wszystko będzie gotowe z toodelete indeksu i chcesz ją, po prostu Wywołaj hello `Indexes.Delete` metody w Twojej `SearchServiceClient`. Na przykład jest to, jak usunąć indeksu "hotels" hello:

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> Witaj przykładowy kod w tym artykule używa metod synchronicznych hello hello zestawu .NET SDK usługi Azure Search dla uproszczenia. Firma Microsoft zaleca używanie metod asynchronicznych hello w tookeep własne aplikacje ich skalowalne i szybko reagowały. Na przykład w hello przykłady powyżej, które można użyć `CreateAsync` i `DeleteAsync` zamiast `Create` i `Delete`.
> 
> 

## <a name="next-steps"></a>Następne kroki
Po utworzeniu indeksu usługi Azure Search, wszystko będzie gotowe za[przekazać zawartość do indeksu hello](search-what-is-data-import.md) , aby rozpocząć wyszukiwanie danych.

