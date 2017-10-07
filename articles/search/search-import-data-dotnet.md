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
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a>Przekazywanie danych tooAzure wyszukiwania przy użyciu hello zestawu .NET SDK
> [!div class="op_single_selector"]
> * [Omówienie](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

W tym artykule opisano, jak toouse hello [zestawu .NET SDK usługi Azure Search](https://aka.ms/search-sdk) tooimport danych do indeksu usługi Azure Search.

Przed rozpoczęciem pracy z tym przewodnikiem powinien zostać [utworzony indeks usługi Azure Search](search-what-is-an-index.md). W tym artykule założono również, że utworzono już `SearchServiceClient` obiektów, jak pokazano w [utworzyć indeks usługi Azure Search przy użyciu zestawu .NET SDK hello](search-create-index-dotnet.md#CreateSearchServiceClient).

> [!NOTE]
> Cały przykładowy kod przedstawiony w tym artykule został napisany w języku C#. Można znaleźć hello pełny kod źródłowy [w serwisie GitHub](http://aka.ms/search-dotnet-howto). Możesz przeczytać temat hello [zestawu .NET SDK usługi Azure Search](search-howto-dotnet-sdk.md) do bardziej szczegółowych przechodzenia przez hello próbki kodu.

W kolejności toopush dokumenty do indeksu przy użyciu zestawu .NET SDK hello musisz:

1. Utwórz `SearchIndexClient` indeksu wyszukiwania tooyour tooconnect obiektu.
2. Utwórz `IndexBatch` hello toobe dokumenty zawierające dodane, modyfikacji lub usunięcia.
3. Wywołaj hello `Documents.Index` metody z `SearchIndexClient` toosend hello `IndexBatch` tooyour indeksu wyszukiwania.

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Utwórz wystąpienie hello klasy SearchIndexClient
dane tooimport do Twojego indeksu przy użyciu hello zestawu .NET SDK usługi Azure Search, konieczne będzie toocreate wystąpienia hello `SearchIndexClient` klasy. Możesz takie wystąpienie można utworzyć samodzielnie, ale można je łatwiej Jeśli masz już `SearchServiceClient` toocall wystąpienia jego `Indexes.GetClient` metody. Na przykład, Oto, jak można uzyskać `SearchIndexClient` hello indeksu o nazwie "hotels" z `SearchServiceClient` o nazwie `serviceClient`:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> W typowej aplikacji wyszukującej wypełnianie indeksu i zarządzanie nim jest obsługiwane przez inny składnik niż zapytania wyszukiwania. `Indexes.GetClient`jest wygodną metodą wypełniania indeksu, ponieważ wymaga dostarczenia kolejnej hello `SearchCredentials`. Robi to przez przekazanie klucza administratora hello tego możesz używane toocreate hello `SearchServiceClient` toohello nowe `SearchIndexClient`. Jednak w hello część aplikacji, która wykonuje zapytania jest lepsze hello toocreate `SearchIndexClient` bezpośrednio, aby można przekazać klucz zapytania zamiast klucza administratora. Jest to zgodne z hello [zasadą najniższych uprawnień](https://en.wikipedia.org/wiki/Principle_of_least_privilege) i pomoże toomake aplikacji bardziej bezpieczne. Można dowiedzieć się więcej o kluczach administratora i kluczach zapytań w hello [dokumentacji interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/).
> 
> 

`SearchIndexClient` ma właściwość `Documents`. Ta właściwość zapewnia wszystkie metody hello należy tooadd, modyfikować lub zbadać dokumenty w indeksie.

## <a name="decide-which-indexing-action-toouse"></a>Zdecyduj, które indeksowania toouse akcji
tooimport danych przy użyciu zestawu .NET SDK hello, konieczne będzie toopackage danych do `IndexBatch` obiektu. `IndexBatch` Hermetyzuje kolekcję `IndexAction` obiektów, z których każdy zawiera dokument i właściwość, która powoduje tooperform jakie działania usługi Azure Search w tym dokumencie (przekazywania, scalania, delete itd.). W zależności od tego, który hello poniższych akcji, którą wybierzesz tylko niektóre pola muszą być uwzględnione w danym dokumencie:

| Akcja | Opis | Wymagane pola dla każdego dokumentu | Uwagi |
| --- | --- | --- | --- |
| `Upload` |`Upload` Akcji jest podobne tooan "upsert", gdzie hello dokument zostanie wstawiony, jeśli jest nowy albo zaktualizowany/zastąpiony, jeśli istnieje. |pole klucza oraz inne pola mają toodefine |Podczas aktualizowania/zastępowania istniejącego dokumentu, wszystkie pola, które nie jest określony w żądaniu hello ma ustawione zbyt`null`. Dzieje się tak nawet wtedy, gdy hello pole było wcześniej ustawione tooa wartość inną niż null. |
| `Merge` |Aktualizacje istniejący dokument o hello określone pola. Jeśli hello dokument nie istnieje w indeksie hello, hello scalanie zakończy się niepowodzeniem. |pole klucza oraz inne pola mają toodefine |Wszystkie pola, które określisz w żądaniu scalania zastąpi istniejące pole hello w dokumencie hello. Obejmuje to również pola typu `DataType.Collection(DataType.String)`. Na przykład, jeśli hello dokument zawiera pole `tags` z wartością `["budget"]` i wykonywane jest scalanie z wartością `["economy", "pool"]` dla `tags`, końcowa wartość hello hello `tags` pole będzie `["economy", "pool"]`. Nie będzie to `["budget", "economy", "pool"]`. |
| `MergeOrUpload` |Ta akcja działa jak `Merge` Jeśli dokument o hello podany klucz już istnieje w indeksie hello. Jeśli dokument hello nie istnieje, działa jak akcja `Upload` dla nowego dokumentu. |pole klucza oraz inne pola mają toodefine |- |
| `Delete` |Usuwa określony dokument hello z hello indeksu. |tylko pole klucza |Wszystkie pola, które określisz oprócz pola klucza hello zostaną zignorowane. Tooremove pojedyncze pole z dokumentu, należy użyć `Merge` zamiast i po prostu jawnie ustaw pola hello toonull. |

Można określić, jakie działanie ma toouse z różnych metod statycznych hello hello `IndexBatch` i `IndexAction` klasy, jak pokazano w następnej sekcji hello.

## <a name="construct-your-indexbatch"></a>Konstruowanie obiektu IndexBatch
Teraz, znając tooperform akcje, które z dokumentami są gotowe tooconstruct hello `IndexBatch`. Witaj przykład poniżej przedstawiono sposób toocreate partii z kilkoma różnymi akcjami. Należy pamiętać, że przedstawiony przykład używa niestandardowej klasy o nazwie `Hotel` mapujący tooa dokument w indeksie "hotels" hello.

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

W tym przypadku użyto `Upload`, `MergeOrUpload`, i `Delete` jako akcje wyszukiwania określonych hello metody wywołane względem hello `IndexAction` klasy.

Załóżmy, że przedstawiony w przykładzie indeks „hotels” jest już wypełniony różnymi dokumentami. Należy zwrócić uwagę, jak firma Microsoft nie miał toospecify wszystkich hello możliwych pól dokumentu przy użyciu `MergeOrUpload` tylko określony klucz dokumentu hello (`HotelId`) przy użyciu `Delete`.

Ponadto należy pamiętać, że może zawierać tylko dokumentów too1000 pojedyncze żądanie indeksowania.

> [!NOTE]
> W tym przykładzie stosujemy różne akcje toodifferent dokumentów. Jeśli potrzebujesz tooperform hello same akcje dla wszystkich dokumentów w partii hello, zamiast wywoływać metodę `IndexBatch.New`, można użyć innych metod statycznych hello `IndexBatch`. Na przykład możesz utworzyć partie przez wywołanie metody `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` lub `IndexBatch.Delete`. Te metody przyjmują kolekcję dokumentów (w tym przykładzie obiekty typu `Hotel`) zamiast obiektów `IndexAction`.
> 
> 

## <a name="import-data-toohello-index"></a>Importowanie danych toohello indeksu
Są już zainicjowane `IndexBatch` obiektu, możesz go wysłać toohello indeksu przez wywołanie metody `Documents.Index` na Twojej `SearchIndexClient` obiektu. powitania po przykładzie pokazano, jak toocall `Index`oraz inne dodatkowe kroki, konieczne będzie tooperform:

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

Uwaga hello `try` / `catch` otaczającego hello wywołania toohello `Index` metody. Witaj blok catch obsługuje ważny przypadek błędu indeksowania. Jeśli usługi Azure Search nie powiedzie się tooindex niektóre hello dokumentów w partii hello `IndexBatchException` jest generowany przez `Documents.Index`. Może to nastąpić, jeśli indeksujesz dokumenty w czasie, gdy usługa jest mocno obciążona. **Zdecydowanie zalecamy jawną obsługę tego przypadku w kodzie.** Można opóźnić, a następnie ponów próbę indeksowania hello dokumentów, których nie powiodła się lub zaloguj się i kontynuować jak w prezentowanym przykładzie hello, lub możesz też wykonać inną akcję w zależności od wymagań spójności danych aplikacji.

Na koniec hello kod w przykładzie hello powyżej umieszczono dwusekundowe opóźnienie. Indeksowanie odbywa się asynchronicznie w usłudze Azure Search tak hello Przykładowa aplikacja musi toowait tooensure krótki czas, że hello dokumenty można wyszukiwać. Tego typu opóźnienia są zazwyczaj konieczne tylko w przypadku pokazów, testów i przykładowych aplikacji.

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a>Jak hello zestawu .NET SDK obsługuje dokumenty
Możesz się zastanawiać, jak hello zestawu .NET SDK usługi Azure Search jest tooupload stanie wystąpienia klasy zdefiniowanej przez użytkownika, jak `Hotel` toohello indeksu. toohelp odpowiedzi na to pytanie, Przyjrzyjmy się hello `Hotel` klasy, która mapuje toohello schemat indeksu zdefiniowany w [utworzyć indeks usługi Azure Search przy użyciu zestawu .NET SDK hello](search-create-index-dotnet.md#DefineIndex):

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

Witaj po pierwsze toonotice jest to, że każda właściwość publiczna klasy `Hotel` odpowiada tooa pola w definicji indeksu hello, ale z jedną istotną różnicą: hello nazwę każdego pola rozpoczyna się małą literą (camelcase"), podczas hello nazwę każdego publicznego Właściwość `Hotel` rozpoczyna się wielką literą ("Pascal litery"). To typowy scenariusz w aplikacjach .NET, które tworzą powiązania danych, gdzie schemat docelowy hello jest poza hello kontroli Deweloper aplikacji hello. Zamiast tooviolate hello zasady nazewnictwa platformy .NET dokonując camelcase nazwy właściwości, można ustalić hello SDK toomap hello właściwość nazwy toocamel przypadku automatycznie z hello `[SerializePropertyNamesAsCamelCase]` atrybutu.

> [!NOTE]
> Witaj zestawu .NET SDK usługi Azure Search korzysta hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize biblioteki i deserializacji tooand obiekty z modelu niestandardowych z formatu JSON. W razie potrzeby możesz dostosować serializację. Więcej szczegółowych informacji znajdziesz w sekcji [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet) (Serializacja niestandardowa przy użyciu programu JSON.NET). Przykładem tego jest użycie hello hello `[JsonProperty]` atrybutu na powitania `DescriptionFr` właściwości w powyższym kodzie przykładowym hello.
> 
> 

Witaj drugą ważną kwestią dotyczącą hello `Hotel` hello typy danych właściwości publicznych hello są klasy. Hello typy .NET tych właściwości mapy typy pól równoważne tootheir w definicji indeksu hello. Na przykład Witaj `Category` toohello mapy właściwości ciągu `category` pola, które jest typu `DataType.String`. Podobne mapowania typów występują między typami `bool?` i `DataType.Boolean`, `DateTimeOffset?` i `DataType.DateTimeOffset` itd. dokładne zasady mapowania typu hello Hello są udokumentowane hello `Documents.Get` metoda hello [odwołanie do zestawu .NET SDK usługi Azure Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).

Ta toouse możliwości własnych klas jako dokumentów działa w obu kierunkach; Można również pobrać wyniki wyszukiwania i hello zestawu SDK dokonać ich automatycznej deserializacji typu tooa wybranych przez użytkownika, jak pokazano w hello [kolejnym artykule](search-query-dotnet.md).

> [!NOTE]
> Witaj zestawu .NET SDK usługi Azure Search obsługuje również dynamiczne typowanie dokumentów za pomocą hello `Document` klasy, która jest mapowanie klucz/wartość, wartości toofield nazw pól. Jest to przydatne w scenariuszach, jeśli nie znasz schematu indeksu hello w czasie projektowania lub gdy byłoby niewygodne toobind toospecific modelu klasy. Wszystkie metody hello w hello zestawu SDK, które obsługują dokumenty mają przeciążenia działające z hello `Document` klasy, a także przeciążenia o silnych typach, które przyjmują parametr typu ogólnego. Tylko hello te ostatnie są używane w hello przykładowy kod w tym artykule.
> 
> 

**Dlaczego należy używać typów danych dopuszczających wartość null**

Podczas projektowania indeksu własne modelu klasy toomap tooan usługi Azure Search, zalecamy deklarowanie właściwości typów wartości, takich jak `bool` i `int` toobe wartości null (na przykład `bool?` zamiast `bool`). Użycie wartości null właściwość masz zbyt**zagwarantować** że żaden dokument w indeksie nie zawiera wartości null dla odpowiednich pól hello. Hello zestawu SDK ani hello usługi Azure Search nie pomoże tooenforce należy to.

To nie jest to czysto hipotetyczny problem: Wyobraź sobie scenariusz, w którym dodajesz nowe pole tooan istniejącego indeksu typu `DataType.Int32`. Po zaktualizowaniu definicji indeksu hello, wszystkie dokumenty będą miały wartość null dla tego nowego pola (ponieważ wszystkie typy dopuszczają wartości null w usłudze Azure Search). Jeśli następnie użyjesz klasy modelu z niedopuszczającą `int` właściwości dla tego pola, otrzymasz `JsonSerializationException` podobny podczas próby tooretrieve dokumentów:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Z tego powodu najlepszym i zalecanym rozwiązaniem jest używanie w klasach modeli typów dopuszczających wartość null.

## <a name="next-steps"></a>Następne kroki
Po wypełnieniu indeksu usługi Azure Search, będzie gotowy toostart wystawiania toosearch zapytań dla dokumentów. Aby uzyskać szczegóły, zobacz [Query Your Azure Search Index](search-query-overview.md) (Tworzenie zapytań względem indeksu usługi Azure Search).

