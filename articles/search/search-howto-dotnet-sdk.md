---
title: "toouse aaaHow usługi Azure Search z aplikacji .NET | Dokumentacja firmy Microsoft"
description: "W jaki sposób toouse Azure wyszukiwanie od aplikacji .NET"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a>W jaki sposób toouse Azure wyszukiwanie od aplikacji .NET
W tym artykule jest tooget wskazówki można do pracy z hello [zestawu .NET SDK usługi Azure Search](https://aka.ms/search-sdk). Można użyć tooimplement zestawu .NET SDK hello wzbogaconej wyszukiwania doświadczenie w aplikacji przy użyciu usługi Azure Search.

## <a name="whats-in-hello-azure-search-sdk"></a>Nowości w hello wyszukiwanie Azure SDK
Witaj zestaw SDK składa się z biblioteki klienta, `Microsoft.Azure.Search`. Go umożliwia toomanage można z indeksów, źródła danych i indeksatorów, oraz przekazywanie i zarządzania dokumentami i wykonywać zapytania, bez konieczności toodeal ze szczegółami hello HTTP i JSON.

Biblioteka klienta Hello definiuje klas takich jak `Index`, `Field`, i `Document`, jak również operacji, takich jak `Indexes.Create` i `Documents.Search` na powitania `SearchServiceClient` i `SearchIndexClient` klasy. Te klasy są podzielone na następujące obszary nazw hello:

* [Microsoft.Azure.Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [Microsoft.Azure.Search.Models](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

Bieżąca wersja hello zestawu .NET SDK usługi Azure Search Hello teraz jest ogólnie dostępna. Jeśli chcesz opinii tooprovide nam tooincorporate hello następnej wersji, można znaleźć na naszych [strony](https://feedback.azure.com/forums/263029-azure-search/).

Witaj zestawu .NET SDK obsługuje wersję `2016-09-01` z hello [interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/). Ta wersja zawiera teraz obsługę niestandardowych analizatory i obiektów Blob platformy Azure i tabel Azure indeksatorze obsługi. Funkcji, które są w wersji zapoznawczej *nie* są częścią tej wersji, takie jak Obsługa indeksowania JSON i woluminów CSV, [Podgląd](search-api-2015-02-28-preview.md) i dostępne za pośrednictwem hello starsze [2.0 — wersja zapoznawcza hello zestawu .NET SDK ](https://aka.ms/search-sdk-preview).

Zestaw SDK nie obsługuje [operacji zarządzania](https://docs.microsoft.com/rest/api/searchmanagement/) takich jak tworzenie i skalowanie usługi wyszukiwania i zarządzanie nimi klucze interfejsu API. Jeśli potrzebujesz toomanage wyszukiwania zasobów z poziomu aplikacji .NET, można użyć hello [zestawu SDK usługi Azure Search .NET zarządzania](https://aka.ms/search-mgmt-sdk).

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a>Uaktualnianie toohello najnowszą wersję hello zestawu SDK
Jeśli już używasz starszej wersji hello zestawu .NET SDK usługi Azure Search i chcesz tooupgrade toohello ogólnie dostępna wersja nowego, [w tym artykule](search-dotnet-sdk-migration.md) wyjaśniono sposób.

## <a name="requirements-for-hello-sdk"></a>Wymagania dotyczące hello zestawu SDK
1. Visual Studio 2017 r.
2. Własne usługi Azure Search. W kolejności toouse hello zestawu SDK konieczne będzie hello nazwę usługi i co najmniej jeden klucz interfejsu API. [Tworzenie usługi w portalu hello](search-create-service-portal.md) pomoże Ci tych kroków.
3. Pobierz hello zestawu .NET SDK usługi Azure Search [pakietu NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) za pomocą "Manage NuGet Packages" programu Visual Studio. Po prostu wyszukać nazwę pakietu hello `Microsoft.Azure.Search` na NuGet.org.

Witaj zestawu .NET SDK usługi Azure Search obsługuje aplikacji hello .NET Framework 4.6 i .NET Core.

## <a name="core-scenarios"></a>Podstawowe scenariusze
Istnieje kilka czynności, będziesz potrzebować toodo w aplikacji wyszukiwania. W tym samouczku omówione zostaną następujące czynności te podstawowe scenariusze:

* Tworzenie indeksu
* Podczas wypełniania indeksu hello z dokumentami
* Wyszukiwanie dokumentów za pomocą wyszukiwania pełnotekstowego oraz filtry

Hello przykładowy kod, który następuje ilustruje każdą z tych. Możesz wstawki kodu hello wolnego toouse w swojej aplikacji.

### <a name="overview"></a>Omówienie
Witaj przykładowej aplikacji, firma Microsoft będzie można badać tworzy nowy indeks o nazwie "hotels" wypełnia kilku dokumentów, a następnie wykonuje kilka zapytań wyszukiwania. Oto główne programu hello, przedstawiający hello ogólny przepływ:

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> Można znaleźć hello pełny kod źródłowy hello przykładowej aplikacji używane w tym krokach związanych z na [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).
> 
>

Zostanie omówiony ten krok po kroku. Najpierw musimy toocreate nowy `SearchServiceClient`. Ten obiekt umożliwia toomanage indeksów. W kolejności tooconstruct jedną należy tooprovide nazwę usługi Azure Search, a także klucz interfejsu API administratora. Te informacje można wprowadzić w hello `appsettings.json` pliku hello [Przykładowa aplikacja](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> Jeśli podasz nieprawidłowy klucz (na przykład klucz zapytania gdzie klucz administratora nie jest wymagana) hello `SearchServiceClient` zgłosi `CloudException` z hello błąd komunikat "Zabronione" hello po raz pierwszy należy wywołać metody operacji, takich jak `Indexes.Create`. W takim przypadku tooyou dokładnie sprawdzić naszych klucz interfejsu API.
> 
> 

Witaj następnych kilku wierszy wywołania metody toocreate indeksu o nazwie "hotels", usuwając go najpierw, jeśli już istnieje. Firma Microsoft przeprowadzi tych metod nieco później.

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

Następnie hello indeks musi toobe wypełnione. toodo, firma Microsoft będzie `SearchIndexClient`. Istnieją dwa sposoby tooobtain, jedną: tworząc go lub poprzez wywołanie `Indexes.GetClient` na powitania `SearchServiceClient`. Używamy hello drugie dla wygody.

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> W typowej aplikacji wyszukującej wypełnianie indeksu i zarządzanie nim jest obsługiwane przez inny składnik niż zapytania wyszukiwania. `Indexes.GetClient`jest wygodną metodą wypełniania indeksu, ponieważ wymaga dostarczenia kolejnej hello `SearchCredentials`. Robi to przez przekazanie klucza administratora hello tego możesz używane toocreate hello `SearchServiceClient` toohello nowe `SearchIndexClient`. Jednak w hello część aplikacji, która wykonuje zapytania jest lepsze hello toocreate `SearchIndexClient` bezpośrednio, aby można przekazać klucz zapytania zamiast klucza administratora. To jest zgodna z zasadą najniższych uprawnień hello i pomoże toomake aplikacji bardziej bezpieczne. Można dowiedzieć się więcej o kluczach administratora i kluczach zapytań [tutaj](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).
> 
> 

Teraz, gdy mamy `SearchIndexClient`, firma Microsoft może wypełnić hello indeksu. Jest to realizowane przy użyciu innej metody, które firma Microsoft przeprowadzi później.

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

Na koniec możemy wykonać kilka zapytań wyszukiwania i wyświetlić wyniki hello. Teraz możemy użyć innego `SearchIndexClient`:

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

Firma Microsoft podejmie bliższe spojrzenie na powitania `RunQueries` metody później. Poniżej przedstawiono nowe hello kodu toocreate hello `SearchIndexClient`:

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

Teraz firma Microsoft używa klucza zapytania, ponieważ nie potrzebujemy indeksu toohello dostęp do zapisu. Te informacje można wprowadzić w hello `appsettings.json` pliku hello [Przykładowa aplikacja](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

Po uruchomieniu tej aplikacji z prawidłową nazwę usługi i klucze interfejsu API hello dane wyjściowe powinny wyglądać następująco:

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
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
    
    Complete.  Press any key tooend application...

Witaj pełny kod źródłowy aplikacji hello znajduje się na końcu hello w tym artykule.

Następnie będzie trwać bliższe spojrzenie na każdej z metod hello wywoływane przez `Main`.

### <a name="creating-an-index"></a>Tworzenie indeksu
Po utworzeniu `SearchServiceClient`, co dalej hello `Main` jest jest delete hello indeksu "hotels", jeśli już istnieje. Który odbywa się przez hello następujące metody:

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

Ta metoda używa hello podane `SearchServiceClient` toocheck Jeśli indeks hello istnieje, a jeśli tak, usuń go.

> [!NOTE]
> Witaj przykładowy kod w tym artykule używa metod synchronicznych hello hello zestawu .NET SDK usługi Azure Search dla uproszczenia. Firma Microsoft zaleca używanie metod asynchronicznych hello w tookeep własne aplikacje ich skalowalne i szybko reagowały. Na przykład w hello metody powyżej, które można użyć `ExistsAsync` i `DeleteAsync` zamiast `Exists` i `Delete`.
> 
> 

Następnie `Main` powoduje utworzenie nowego indeksu "hotels" przez wywołanie tej metody:

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

Ta metoda tworzy nowy `Index` obiektu z listy `Field` obiektów, które definiuje schemat hello hello nowego indeksu. Każde pole ma nazwę, typ danych i kilka atrybutów, które określają zachowanie wyszukiwania. Witaj `FieldBuilder` klasy używa toocreate odbicia listę `Field` obiektów dla indeksu hello, sprawdzając hello publicznej właściwości i atrybutów hello podane `Hotel` klasa modelu. Przeniesiemy bliższe spojrzenie na powitania `Hotel` klasy później.

> [!NOTE]
> Zawsze można utworzyć listy hello `Field` obiektów bezpośrednio zamiast `FieldBuilder` w razie potrzeby. Na przykład możesz nie chcieć toouse klasę modelu lub może być konieczne toouse istniejącej klasy modelu użytkownik chce toomodify przez dodanie atrybutów.
>
> 

Ponadto toofields, można również dodać oceniania profile, sugestorów lub CORS toohello opcji indeksu (te zostaną pominięte próbki hello w celu jego skrócenia). Więcej informacji na temat hello indeksu obiekt i jego elementów składowych można znaleźć w hello [odwołania do zestawu SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), jak również w hello [dokumentacji interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/).

### <a name="populating-hello-index"></a>Podczas wypełniania indeksu hello
następnym krokiem Hello w `Main` toopopulate hello nowo utworzony indeks. Można to zrobić w hello następujące metody:

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
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
        },
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
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

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
}
```

Ta metoda ma cztery części. Witaj najpierw tworzy tablicę `Hotel` obiektów, które będzie służyć jako dane wejściowe tooupload toohello indeksu. Te dane są stałe dla uproszczenia. W aplikacji danych prawdopodobnie będzie pochodził z zewnętrznego źródła danych takie jak bazy danych SQL.

druga część Hello tworzy `IndexBatch` zawierających hello dokumenty. Określ operację hello ma tooapply toohello partii w czasie hello należy utworzyć ją, w tym przypadku przez wywołanie metody `IndexBatch.Upload`. Hello partii jest następnie przekazane toohello usługi Azure Search index przez hello `Documents.Index` metody.

> [!NOTE]
> W tym przykładzie mamy tylko przekazywania dokumentów. Jeśli potrzebujesz toomerge zmian do istniejących dokumentów lub usuwanie dokumentów, możesz utworzyć partie przez wywołanie metody `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, lub `IndexBatch.Delete` zamiast tego. Możesz łączyć różnych operacji w pojedynczej partii przez wywołanie metody `IndexBatch.New`, który przyjmuje Kolekcja `IndexAction` obiektów, z których każdy określa, że usługi Azure Search tooperform określonej operacji w dokumencie. Można utworzyć każdego `IndexAction` z działaniem wywołując hello odpowiedniej metody, takie jak `IndexAction.Merge`, `IndexAction.Upload`i tak dalej.
> 
> 

Witaj trzeci część tej metody jest blok catch obsługuje ważny przypadek błędu indeksowania. Jeśli usługi Azure Search nie powiedzie się tooindex niektóre hello dokumentów w partii hello `IndexBatchException` jest generowany przez `Documents.Index`. Może to nastąpić, jeśli indeksujesz dokumenty w czasie, gdy usługa jest mocno obciążona. **Zdecydowanie zalecamy jawną obsługę tego przypadku w kodzie.** Można opóźnić, a następnie ponów próbę indeksowania hello dokumentów, których nie powiodła się lub zaloguj się i kontynuować jak w prezentowanym przykładzie hello, lub możesz też wykonać inną akcję w zależności od wymagań spójności danych aplikacji.

> [!NOTE]
> Można użyć hello `FindFailedActionsToRetry` tooconstruct metody, zawierający nowe partii hello tylko akcje, których nie powiodła się w poprzednie wywołanie za`Index`. Metoda Hello jest udokumentowany [tutaj](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) i uzyskać informacje dotyczące sposobu używania go tooproperly [w witrynie StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).
>
>

Na koniec hello `UploadDocuments` umieszczono dwusekundowe opóźnienie metody. Indeksowanie odbywa się asynchronicznie w usłudze Azure Search tak hello Przykładowa aplikacja musi toowait tooensure krótki czas, że hello dokumenty można wyszukiwać. Tego typu opóźnienia są zazwyczaj konieczne tylko w przypadku pokazów, testów i przykładowych aplikacji.

#### <a name="how-hello-net-sdk-handles-documents"></a>Jak hello zestawu .NET SDK obsługuje dokumenty
Możesz się zastanawiać, jak hello zestawu .NET SDK usługi Azure Search jest tooupload stanie wystąpienia klasy zdefiniowanej przez użytkownika, jak `Hotel` toohello indeksu. toohelp odpowiedzi na to pytanie, Przyjrzyjmy się hello `Hotel` klasy:

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

Witaj po pierwsze toonotice jest to, że każda właściwość publiczna klasy `Hotel` odpowiada tooa pola w definicji indeksu hello, ale z jedną istotną różnicą: hello nazwę każdego pola rozpoczyna się małą literą (camelcase"), podczas hello nazwę każdego publicznego Właściwość `Hotel` rozpoczyna się wielką literą ("Pascal litery"). To typowy scenariusz w aplikacjach .NET, które tworzą powiązania danych, gdzie schemat docelowy hello jest poza hello kontroli Deweloper aplikacji hello. Zamiast tooviolate hello zasady nazewnictwa platformy .NET dokonując camelcase nazwy właściwości, można ustalić hello SDK toomap hello właściwość nazwy toocamel przypadku automatycznie z hello `[SerializePropertyNamesAsCamelCase]` atrybutu.

> [!NOTE]
> Witaj zestawu .NET SDK usługi Azure Search korzysta hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize biblioteki i deserializacji tooand obiekty z modelu niestandardowych z formatu JSON. W razie potrzeby możesz dostosować serializację. Aby uzyskać więcej informacji, zobacz [niestandardowe serializacji z struktury JSON.NET](#JsonDotNet).
> 
> 

Hello drugi element toonotice to hello atrybutów, takich jak `IsFilterable`, `IsSearchable`, `Key`, i `Analyzer` który dekoracji każda właściwość publiczna. Te atrybuty bezpośrednio mapy toohello [odpowiednie atrybuty indeksu usługi Azure Search hello](https://docs.microsoft.com/rest/api/searchservice/create-index#request). Witaj `FieldBuilder` klasy używa tych definicji pola tooconstruct hello indeksu.

Witaj trzeci ważną kwestią dotyczącą hello `Hotel` hello typy danych właściwości publicznych hello są klasy. Hello typy .NET tych właściwości mapy typy pól równoważne tootheir w definicji indeksu hello. Na przykład Witaj `Category` toohello mapy właściwości ciągu `category` pola, które jest typu `Edm.String`. Istnieją podobne mapowania typów między `bool?` i `Edm.Boolean`, `DateTimeOffset?` i `Edm.DateTimeOffset`, itp. hello dokładne zasady mapowania typu hello są udokumentowane hello `Documents.Get` metoda hello [zestawu .NET SDK usługi Azure Search Odwołanie](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_). Witaj `FieldBuilder` klasy zajmuje się to mapowanie dla Ciebie, ale nadal może być przydatne toounderstand w razie potrzeby tootroubleshoot problemy serializacji.

Ta toouse możliwości własnych klas jako dokumentów działa w obu kierunkach; Można również pobrać wyniki wyszukiwania i hello zestawu SDK dokonać ich automatycznej deserializacji typu tooa wybranych przez użytkownika, jak zostanie wyświetlone w następnej sekcji hello.

> [!NOTE]
> Witaj zestawu .NET SDK usługi Azure Search obsługuje również dynamiczne typowanie dokumentów za pomocą hello `Document` klasy, która jest mapowanie klucz/wartość, wartości toofield nazw pól. Jest to przydatne w scenariuszach, jeśli nie znasz schematu indeksu hello w czasie projektowania lub gdy byłoby niewygodne toobind toospecific modelu klasy. Wszystkie metody hello w hello zestawu SDK, które obsługują dokumenty mają przeciążenia działające z hello `Document` klasy, a także przeciążenia o silnych typach, które przyjmują parametr typu ogólnego. Tylko hello te ostatnie są używane w hello przykładowy kod w tym samouczku. Witaj `Document` klasa dziedziczy `Dictionary<string, object>`. Inne szczegółowe informacje można znaleźć [tutaj](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).
> 
> 

**Dlaczego należy używać typów danych dopuszczających wartość null**

Podczas projektowania indeksu własne modelu klasy toomap tooan usługi Azure Search, zalecamy deklarowanie właściwości typów wartości, takich jak `bool` i `int` toobe wartości null (na przykład `bool?` zamiast `bool`). Użycie wartości null właściwość masz zbyt**zagwarantować** że żaden dokument w indeksie nie zawiera wartości null dla odpowiednich pól hello. Hello zestawu SDK ani hello usługi Azure Search nie pomoże tooenforce należy to.

To nie jest to czysto hipotetyczny problem: Wyobraź sobie scenariusz, w którym dodajesz nowe pole tooan istniejącego indeksu typu `Edm.Int32`. Po zaktualizowaniu definicji indeksu hello, wszystkie dokumenty będą miały wartość null dla tego nowego pola (ponieważ wszystkie typy dopuszczają wartości null w usłudze Azure Search). Jeśli następnie użyjesz klasy modelu z niedopuszczającą `int` właściwości dla tego pola, otrzymasz `JsonSerializationException` podobny podczas próby tooretrieve dokumentów:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Z tego powodu najlepszym i zalecanym rozwiązaniem jest używanie w klasach modeli typów dopuszczających wartość null.

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a>Niestandardowej serializacji z struktury JSON.NET
Witaj SDK używa struktury JSON.NET do serializacji i deserializacji dokumentów. Można dostosować serializacji i deserializacji w razie potrzeby, definiując własne `JsonConverter` lub `IContractResolver` (zobacz hello [dokumentacji struktury JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) więcej szczegółów). Może to być przydatne, jeśli chcesz tooadapt istniejącej klasy modelu z aplikacji do użycia z usługi Azure Search i innych bardziej zaawansowanych scenariuszy. Na przykład za pomocą niestandardowej serializacji można:

* Uwzględnić lub wykluczyć pewne właściwości klasy modelu są przechowywane jako pól dokumentu.
* Mapowania nazw właściwości w kodzie i nazw pól w indeksie.
* Tworzenie atrybutów niestandardowych, które mogą być używane do mapowania pól toodocument właściwości.

Można znaleźć przykłady stosowania niestandardowej serializacji w hello testów jednostkowych dla hello Azure Search .NET SDK w serwisie GitHub. Dobry punkt wyjścia jest [ten folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models). Zawiera klasy, które są używane przez hello niestandardowej serializacji testy.

### <a name="searching-for-documents-in-hello-index"></a>Wyszukiwanie dokumentów w indeksie hello
Ostatnim krokiem hello Przykładowa aplikacja Hello jest toosearch dla niektórych dokumentów w indeksie hello. następujące metody Hello robi to:

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
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
}
```

Każdy czasu wykonywania zapytania, najpierw ta metoda tworzy nowy `SearchParameters` obiektu. Jest to dodatkowe opcje używane toospecify hello zapytania, takie jak sortowanie, filtrowanie, stronicowania i tworzenie aspektów. W przypadku tej metody, firma Microsoft jest ustawienie hello `Filter`, `Select`, `OrderBy`, i `Top` właściwości dla różnych zapytań. Wszystkie hello `SearchParameters` właściwości są udokumentowane [tutaj](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).

Witaj, następnym krokiem jest tooactually wykonać hello zapytania wyszukiwania. Jest to realizowane przy użyciu hello `Documents.Search` metody. Dla każdego zapytania hello wyszukiwania tekstu toouse przekazywana jako ciąg (lub `"*"` , jeśli nie ma żadnego tekstu wyszukiwania), oraz hello wyszukiwania parametry utworzony wcześniej. Również określić `Hotel` jako parametr typu hello `Documents.Search`, który informuje hello SDK toodeserialize dokumentów w wynikach wyszukiwania hello w obiektach typu `Hotel`.

> [!NOTE]
> Można znaleźć więcej informacji na temat składni wyrażeń zapytania wyszukiwania hello [tutaj](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).
> 
> 

Na koniec po każdym zapytaniem tej metody iteruje wszystkie dopasowania hello w wynikach wyszukiwania hello, drukowanie każdego dokumentu toohello konsoli:

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

Z kolei wytłumaczone bliższe spojrzenie na każdym hello zapytań. Oto hello kodu tooexecute hello pierwszego zapytania:

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

W takim przypadku możemy Cię szukające hoteli, zgodne hello word "budget" i chcemy tooget ponownie tylko hello hoteli nazwy, określony przez hello `Select` parametru. Poniżej przedstawiono wyniki hello:

    Name: Roach Motel

Następnie możemy mają hotels hello toofind co noc szybkość wynosi mniej niż 150 USD i zwracać tylko identyfikator hoteli hello i opis:

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

To zapytanie używa OData `$filter` wyrażenie `baseRate lt 150`, toofilter hello dokumenty w indeksie hello. Można dowiedzieć się więcej o składni OData, który obsługuje usługę Azure Search hello [tutaj](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).

Poniżej przedstawiono wyniki hello hello zapytania:

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

Następnie chcemy toofind hello top dwóch hotels został ostatnio renovated, które zawierają nazwę hoteli hello i odnawianie Data. Oto kod hello: 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

W takim przypadku ponownie używamy OData składni toospecify hello `OrderBy` parametr jako `lastRenovationDate desc`. Możemy również ustawić `Top` too2 tooensure tylko uzyskujemy hello dwa dokumenty. Jak wcześniej, możemy ustawić `Select` toospecify pola, które ma zostać zwrócony.

Poniżej przedstawiono wyniki hello:

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Wreszcie chcemy mieć toofind wszystkie hotele, zgodne hello słowo "motel":

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

A Oto hello wyników, które obejmują wszystkie pola, ponieważ nie określono firma Microsoft hello `Select` właściwości:

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

Ten krok jest wykonywany hello samouczek, ale nie zatrzymuje tutaj. **Następne kroki** przedstawiono dodatkowe zasoby, aby uzyskać więcej informacji na temat usługi Azure Search.

## <a name="next-steps"></a>Następne kroki
* Przeglądaj hello odwołań dla hello [zestawu .NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) i [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/).
* Pogłębić swoją wiedzę za pośrednictwem [wideo i inne przykłady i samouczki](search-video-demo-tutorial-list.md).
* Przegląd [konwencje nazewnictwa](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello reguły nazewnictwa różnych obiektów.
* Przegląd [obsługiwane typy danych](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) w usłudze Azure Search.
