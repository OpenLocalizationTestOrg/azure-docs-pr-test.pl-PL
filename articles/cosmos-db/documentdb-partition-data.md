---
title: "aaaPartitioning i skalowania w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o sposobie partycjonowania działania w usłudze Azure DB rozwiązania Cosmos, jak tooconfigure partycjonowania i kluczy partycji i jak toopick hello prawo partycji klucz dla aplikacji."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30621d2ba0b89efb72005680d5f3a73998347514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a>Podział na partycje w usłudze Azure DB rozwiązania Cosmos przy użyciu hello interfejsu API usługi DocumentDB

[Bazy danych programu Microsoft Azure rozwiązania Cosmos](../cosmos-db/introduction.md) jest toohelp zaprojektowanej globalna baza danych rozproszone i wiele modeli, można osiągnąć szybkie, przewidywalną wydajność i skalę bezproblemowo wraz z aplikacji jako ich przyrostu. 

Ten artykuł zawiera omówienie sposobu toowork z partycjonowania kontenerów DB rozwiązania Cosmos z hello interfejsu API usługi DocumentDB. Zobacz [partycjonowania i skalowanie w poziomie](../cosmos-db/partition-data.md) omówienie pojęć i najlepsze rozwiązania dotyczące partycjonowania z jakiegokolwiek interfejsu API Azure rozwiązania Cosmos bazy danych. 

tooget pracę z kodem, Pobierz hello projekt z [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

Po przeczytaniu tego artykułu, będą mogli tooanswer hello następujące pytania:   

* Jak działa partycjonowania w usłudze Azure DB rozwiązania Cosmos?
* Jak skonfigurować partycje w usłudze Azure DB rozwiązania Cosmos
* Co to są klucze partycji, i jak pobranie hello klucza partycji prawo do mojej aplikacji?

tooget pracę z kodem, Pobierz hello projekt z [Azure rozwiązania Cosmos DB wydajności testowania sterownik Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a>Klucze partycji

Należy określić w hello interfejsu API usługi DocumentDB, hello definicji klucza partycji w formie hello ścieżce JSON. Witaj poniższej tabeli przedstawiono przykłady partycji kluczowe definicje i wartości hello tooeach. Klucz partycji Hello jest określony jako ścieżkę, np. `/department` reprezentuje hello działu właściwości. 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Klucz partycji</strong></p></td>
            <td valign="top"><p><strong>Opis</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>/Department</p></td>
            <td valign="top"><p>Odpowiada wartości toohello doc.department dokumentu w przypadku elementu hello.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/ właściwości/Nazwa</p></td>
            <td valign="top"><p>Odpowiada wartości toohello doc.properties.name dokumentu w przypadku elementu hello (właściwość zagnieżdżonych).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/ Identyfikator</p></td>
            <td valign="top"><p>Odpowiada wartości toohello doc.id (identyfikator i partycji klucza są takie same hello właściwości).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/ "dział name"</p></td>
            <td valign="top"><p>Odpowiada wartości toohello doc ["Nazwa działu"], gdzie dokumentu jest hello elementu.</p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> Składnia Hello klucza partycji jest podobne specyfikacji ścieżki toohello indeksowania ścieżki zasad z hello klucza różnicą, że ścieżka hello odpowiada właściwości toohello zamiast wartości hello, tj. w nie ma żadnych symbol wieloznaczny zakończenia hello. Na przykład należy określić/dział /? Witaj tooindex wartości w obszarze działu, ale określ /department jako definicji klucza partycji hello. Klucz partycji Hello jest niejawnie indeksowane i nie można wykluczyć z indeksowania, używając zastąpień zasad indeksowania.
> 
> 

Oto jak hello wydajność aplikacji ma wpływ na wybór hello klucza partycji.

## <a name="working-with-hello-azure-cosmos-db-sdks"></a>Praca z hello Azure rozwiązania Cosmos DB SDK
Azure DB rozwiązania Cosmos dodano obsługę automatycznego partycjonowania z [interfejsu API REST wersji 2015-12-16](/rest/api/documentdb/). W kolejności kontenery toocreate podzielona na partycje, należy pobrać zestaw SDK w wersji 1.6.0 lub nowszej w jednym z hello obsługiwane zestawu SDK platformy (.NET, Node.js, Java, Python, bazy danych MongoDB). 

### <a name="creating-containers"></a>Tworzenie kontenerów
Witaj poniższy przykład przedstawia toocreate fragment kodu .NET dane telemetryczne kontenera toostore urządzenie 20 000 jednostek żądań na sekundę, przepływności. Witaj SDK ustawia wartość OfferThroughput hello (który z kolei ustawia hello `x-ms-offer-throughput` nagłówek żądania w hello interfejsu API REST). W tym miejscu możemy ustawić hello `/deviceId` jako klucza partycji hello. Wybór Hello klucza partycji są zapisywane wraz z resztą hello hello metadanych kontenera, takie jak nazwa i zasady indeksowania.

Dla tego przykładu, wybraniu `deviceId` ponieważ wiemy, że () od dużej liczby urządzeń, zapisy mogą być rozproszone na partycje równomiernie i pozwalając nam tooscale hello bazy danych tooingest duże ilości danych i (b) wiele żądań hello, takich jak Pobieranie najnowszych odczytu hello urządzenia są deviceId pojedynczego tooa zakresie i mogą być pobierane z jednej partycji.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here hello property deviceId will be used as hello partition key too
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

Ta metoda powoduje tooCosmos DB wywołania interfejsu API REST i usługi hello Obsługa będzie inicjowana liczba partycji na podstawie przepływności żądanego hello. W razie rozwoju potrzeb wydajność można zmienić przepływności hello kontenera. 

### <a name="reading-and-writing-items"></a>Odczytywanie i zapisywanie elementów
Teraz Dodajmy danych w bazie danych rozwiązania Cosmos. W tym miejscu jest klasą próbki zawierającego odczytu urządzenia i tooinsert tooCreateDocumentAsync wywołania nowe urządzenie odczytu do kontenera. To jest przykład wykorzystaniu hello interfejsu API usługi DocumentDB:

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```

Umożliwia odczytu elementu hello przez identyfikator i klucz partycji, zaktualizować go, a następnie jako ostatni krok, usuń go przez klucz partycji i identyfikator. Należy pamiętać, że odczyty hello zawierają wartość PartitionKey (odpowiedniego toohello `x-ms-documentdb-partitionkey` nagłówek żądania w hello interfejsu API REST).

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-containers"></a>Wykonywanie zapytania kontenery podzielonym na partycje
Automatycznie kwerendy danych w kontenerach podzielonym na partycje, DB rozwiązania Cosmos trasy hello partycji toohello zapytań odpowiadającą wartości klucza partycji toohello określony w filtrze hello (jeśli istnieją). Na przykład to zapytanie jest kierowany toojust hello partycji zawierającego hello klucza partycji "XMS 0001".

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Witaj następujące zapytanie nie ma filtr klucza partycji hello (DeviceId) i jest rozwiniętym tooall partycji, którym jest wykonywany przed hello partycjonowania indeksu. Należy pamiętać, że program toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` w hello interfejsu API REST) toohave hello SDK tooexecute zapytania na partycje.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

Obsługuje rozwiązania cosmos DB [funkcje agregujące](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` i `AVG` over podzielona na partycje przy użyciu programu SQL z zestawów SDK 1.12.0 i powyżej uruchomienia kontenerów. Zapytania musi zawierać pojedynczy operatora agregacji i musi zawierać jedną wartość w hello projekcji.

### <a name="parallel-query-execution"></a>Równoległego wykonywania zapytań
Witaj zestawów SDK DB rozwiązania Cosmos 1.9.0 i powyżej Obsługa opcje wykonywania zapytania równoległe, umożliwiających tooperform małe opóźnienia zapytanie względem kolekcji partycjonowanych, nawet wtedy, gdy potrzebna jest tootouch dużą liczbę partycji. Na przykład hello następującego zapytania jest skonfigurowany toorun równolegle na partycje.

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Możesz zarządzać równoległego wykonywania zapytań przez dostrajanie hello następujące parametry:

* Przez ustawienie `MaxDegreeOfParallelism`, można kontrolować hello stopień równoległości, tj. Data hello maksymalną liczbę kontenera sieci równoczesnych połączeń toohello partycji. Jeśli ustawisz to zbyt-1, hello stopień równoległości jest zarządzana przez hello zestawu SDK. Jeśli hello `MaxDegreeOfParallelism` nie jest określony lub ustaw too0, która jest wartością domyślną hello, będzie jednej sieci połączenia toohello kontenera na partycje.
* Przez ustawienie `MaxBufferedItemCount`, można kompromis wykorzystanie pamięci zapytania opóźnienia i po stronie klienta. Jeśli ten parametr lub ustaw tę wartość za 1 hello liczbę elementów buforowane podczas równoległego wykonywania zapytań jest zarządzana przez hello zestawu SDK.

Podane hello niezmienionym hello kolekcji, równoległe zapytania zostanie zwracają wyniki w hello kolejność takie same jak wykonanie szeregowego. Podczas wykonywania kwerendy między partycji zawierającej, sortowanie (ORDER BY i/lub góry), problemy z zestawu SDK platformy Azure rozwiązania Cosmos DB hello hello zapytania równolegle na partycje i scaleń częściowo sortowane wyniki w tooproduce po stronie klienta hello globalnie uporządkowanych wyników.

### <a name="executing-stored-procedures"></a>Wykonywanie procedury składowane
Można również wykonywać transakcje atomic względem dokumentów za pomocą hello tego samego Identyfikatora urządzenia, np. Jeśli jest utrzymanie agreguje lub hello najnowszy stan urządzeń w jeden element. 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
W następnej sekcji hello przyjrzymy się jak kontenery toopartitioned mogą być przenoszone z kontenerów jednej partycji.

## <a name="next-steps"></a>Następne kroki
W tym artykule podaliśmy omówienie sposobu toowork z partycjonowania kontenerów bazy danych Azure rozwiązania Cosmos z hello interfejsu API usługi DocumentDB. Zobacz też [partycjonowania i skalowanie w poziomie](../cosmos-db/partition-data.md) omówienie pojęć i najlepsze rozwiązania dotyczące partycjonowania z jakiegokolwiek interfejsu API Azure rozwiązania Cosmos bazy danych. 

* Należy przeprowadzić testowanie z bazy danych Azure rozwiązania Cosmos wydajności i skalowania. Zobacz [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md) przykładowe.
* Rozpoczynanie pracy kodowania z hello [zestawów SDK](documentdb-sdk-dotnet.md) lub hello [interfejsu API REST](/rest/api/documentdb/)
* Dowiedz się więcej o [udostępnionej przepływności w usłudze Azure DB rozwiązania Cosmos](request-units.md)

