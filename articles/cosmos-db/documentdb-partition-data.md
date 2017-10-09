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
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a><span data-ttu-id="0c2e9-103">Podział na partycje w usłudze Azure DB rozwiązania Cosmos przy użyciu hello interfejsu API usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0c2e9-103">Partitioning in Azure Cosmos DB using hello DocumentDB API</span></span>

<span data-ttu-id="0c2e9-104">[Bazy danych programu Microsoft Azure rozwiązania Cosmos](../cosmos-db/introduction.md) jest toohelp zaprojektowanej globalna baza danych rozproszone i wiele modeli, można osiągnąć szybkie, przewidywalną wydajność i skalę bezproblemowo wraz z aplikacji jako ich przyrostu.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="0c2e9-105">Ten artykuł zawiera omówienie sposobu toowork z partycjonowania kontenerów DB rozwiązania Cosmos z hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-105">This article provides an overview of how toowork with partitioning of Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="0c2e9-106">Zobacz [partycjonowania i skalowanie w poziomie](../cosmos-db/partition-data.md) omówienie pojęć i najlepsze rozwiązania dotyczące partycjonowania z jakiegokolwiek interfejsu API Azure rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="0c2e9-107">tooget pracę z kodem, Pobierz hello projekt z [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="0c2e9-107">tooget started with code, download hello project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="0c2e9-108">Po przeczytaniu tego artykułu, będą mogli tooanswer hello następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="0c2e9-108">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="0c2e9-109">Jak działa partycjonowania w usłudze Azure DB rozwiązania Cosmos?</span><span class="sxs-lookup"><span data-stu-id="0c2e9-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="0c2e9-110">Jak skonfigurować partycje w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="0c2e9-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="0c2e9-111">Co to są klucze partycji, i jak pobranie hello klucza partycji prawo do mojej aplikacji?</span><span class="sxs-lookup"><span data-stu-id="0c2e9-111">What are partition keys, and how do I pick hello right partition key for my application?</span></span>

<span data-ttu-id="0c2e9-112">tooget pracę z kodem, Pobierz hello projekt z [Azure rozwiązania Cosmos DB wydajności testowania sterownik Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="0c2e9-112">tooget started with code, download hello project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="0c2e9-113">Klucze partycji</span><span class="sxs-lookup"><span data-stu-id="0c2e9-113">Partition keys</span></span>

<span data-ttu-id="0c2e9-114">Należy określić w hello interfejsu API usługi DocumentDB, hello definicji klucza partycji w formie hello ścieżce JSON.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-114">In hello DocumentDB API, you specify hello partition key definition in hello form of a JSON path.</span></span> <span data-ttu-id="0c2e9-115">Witaj poniższej tabeli przedstawiono przykłady partycji kluczowe definicje i wartości hello tooeach.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-115">hello following table shows examples of partition key definitions and hello values corresponding tooeach.</span></span> <span data-ttu-id="0c2e9-116">Klucz partycji Hello jest określony jako ścieżkę, np. `/department` reprezentuje hello działu właściwości.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-116">hello partition key is specified as a path, e.g. `/department` represents hello property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="0c2e9-117"><strong>Klucz partycji</strong></span><span class="sxs-lookup"><span data-stu-id="0c2e9-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="0c2e9-118"><strong>Opis</strong></span><span class="sxs-lookup"><span data-stu-id="0c2e9-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="0c2e9-119">/Department</span><span class="sxs-lookup"><span data-stu-id="0c2e9-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="0c2e9-120">Odpowiada wartości toohello doc.department dokumentu w przypadku elementu hello.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-120">Corresponds toohello value of doc.department where doc is hello item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="0c2e9-121">/ właściwości/Nazwa</span><span class="sxs-lookup"><span data-stu-id="0c2e9-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="0c2e9-122">Odpowiada wartości toohello doc.properties.name dokumentu w przypadku elementu hello (właściwość zagnieżdżonych).</span><span class="sxs-lookup"><span data-stu-id="0c2e9-122">Corresponds toohello value of doc.properties.name where doc is hello item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="0c2e9-123">/ Identyfikator</span><span class="sxs-lookup"><span data-stu-id="0c2e9-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="0c2e9-124">Odpowiada wartości toohello doc.id (identyfikator i partycji klucza są takie same hello właściwości).</span><span class="sxs-lookup"><span data-stu-id="0c2e9-124">Corresponds toohello value of doc.id (id and partition key are hello same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="0c2e9-125">/ "dział name"</span><span class="sxs-lookup"><span data-stu-id="0c2e9-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="0c2e9-126">Odpowiada wartości toohello doc ["Nazwa działu"], gdzie dokumentu jest hello elementu.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-126">Corresponds toohello value of doc["department name"] where doc is hello item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="0c2e9-127">Składnia Hello klucza partycji jest podobne specyfikacji ścieżki toohello indeksowania ścieżki zasad z hello klucza różnicą, że ścieżka hello odpowiada właściwości toohello zamiast wartości hello, tj. w nie ma żadnych symbol wieloznaczny zakończenia hello.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-127">hello syntax for partition key is similar toohello path specification for indexing policy paths with hello key difference that hello path corresponds toohello property instead of hello value, i.e. there is no wild card at hello end.</span></span> <span data-ttu-id="0c2e9-128">Na przykład należy określić/dział /?</span><span class="sxs-lookup"><span data-stu-id="0c2e9-128">For example, you would specify /department/?</span></span> <span data-ttu-id="0c2e9-129">Witaj tooindex wartości w obszarze działu, ale określ /department jako definicji klucza partycji hello.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-129">tooindex hello values under department, but specify /department as hello partition key definition.</span></span> <span data-ttu-id="0c2e9-130">Klucz partycji Hello jest niejawnie indeksowane i nie można wykluczyć z indeksowania, używając zastąpień zasad indeksowania.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-130">hello partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="0c2e9-131">Oto jak hello wydajność aplikacji ma wpływ na wybór hello klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-131">Let's look at how hello choice of partition key impacts hello performance of your application.</span></span>

## <a name="working-with-hello-azure-cosmos-db-sdks"></a><span data-ttu-id="0c2e9-132">Praca z hello Azure rozwiązania Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="0c2e9-132">Working with hello Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="0c2e9-133">Azure DB rozwiązania Cosmos dodano obsługę automatycznego partycjonowania z [interfejsu API REST wersji 2015-12-16](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="0c2e9-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="0c2e9-134">W kolejności kontenery toocreate podzielona na partycje, należy pobrać zestaw SDK w wersji 1.6.0 lub nowszej w jednym z hello obsługiwane zestawu SDK platformy (.NET, Node.js, Java, Python, bazy danych MongoDB).</span><span class="sxs-lookup"><span data-stu-id="0c2e9-134">In order toocreate partitioned containers, you must download SDK versions 1.6.0 or newer in one of hello supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="0c2e9-135">Tworzenie kontenerów</span><span class="sxs-lookup"><span data-stu-id="0c2e9-135">Creating containers</span></span>
<span data-ttu-id="0c2e9-136">Witaj poniższy przykład przedstawia toocreate fragment kodu .NET dane telemetryczne kontenera toostore urządzenie 20 000 jednostek żądań na sekundę, przepływności.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-136">hello following sample shows a .NET snippet toocreate a container toostore device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="0c2e9-137">Witaj SDK ustawia wartość OfferThroughput hello (który z kolei ustawia hello `x-ms-offer-throughput` nagłówek żądania w hello interfejsu API REST).</span><span class="sxs-lookup"><span data-stu-id="0c2e9-137">hello SDK sets hello OfferThroughput value (which in turn sets hello `x-ms-offer-throughput` request header in hello REST API).</span></span> <span data-ttu-id="0c2e9-138">W tym miejscu możemy ustawić hello `/deviceId` jako klucza partycji hello.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-138">Here we set hello `/deviceId` as hello partition key.</span></span> <span data-ttu-id="0c2e9-139">Wybór Hello klucza partycji są zapisywane wraz z resztą hello hello metadanych kontenera, takie jak nazwa i zasady indeksowania.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-139">hello choice of partition key is saved along with hello rest of hello container metadata like name and indexing policy.</span></span>

<span data-ttu-id="0c2e9-140">Dla tego przykładu, wybraniu `deviceId` ponieważ wiemy, że () od dużej liczby urządzeń, zapisy mogą być rozproszone na partycje równomiernie i pozwalając nam tooscale hello bazy danych tooingest duże ilości danych i (b) wiele żądań hello, takich jak Pobieranie najnowszych odczytu hello urządzenia są deviceId pojedynczego tooa zakresie i mogą być pobierane z jednej partycji.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us tooscale hello database tooingest massive volumes of data and (b) many of hello requests like fetching hello latest reading for a device are scoped tooa single deviceId and can be retrieved from a single partition.</span></span>

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

<span data-ttu-id="0c2e9-141">Ta metoda powoduje tooCosmos DB wywołania interfejsu API REST i usługi hello Obsługa będzie inicjowana liczba partycji na podstawie przepływności żądanego hello.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-141">This method makes a REST API call tooCosmos DB, and hello service will provision a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="0c2e9-142">W razie rozwoju potrzeb wydajność można zmienić przepływności hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-142">You can change hello throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="0c2e9-143">Odczytywanie i zapisywanie elementów</span><span class="sxs-lookup"><span data-stu-id="0c2e9-143">Reading and writing items</span></span>
<span data-ttu-id="0c2e9-144">Teraz Dodajmy danych w bazie danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="0c2e9-145">W tym miejscu jest klasą próbki zawierającego odczytu urządzenia i tooinsert tooCreateDocumentAsync wywołania nowe urządzenie odczytu do kontenera.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-145">Here's a sample class containing a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a container.</span></span> <span data-ttu-id="0c2e9-146">To jest przykład wykorzystaniu hello interfejsu API usługi DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="0c2e9-146">This is an example leveraging hello DocumentDB API:</span></span>

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

<span data-ttu-id="0c2e9-147">Umożliwia odczytu elementu hello przez identyfikator i klucz partycji, zaktualizować go, a następnie jako ostatni krok, usuń go przez klucz partycji i identyfikator. Należy pamiętać, że odczyty hello zawierają wartość PartitionKey (odpowiedniego toohello `x-ms-documentdb-partitionkey` nagłówek żądania w hello interfejsu API REST).</span><span class="sxs-lookup"><span data-stu-id="0c2e9-147">Let's read hello item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="0c2e9-148">Wykonywanie zapytania kontenery podzielonym na partycje</span><span class="sxs-lookup"><span data-stu-id="0c2e9-148">Querying partitioned containers</span></span>
<span data-ttu-id="0c2e9-149">Automatycznie kwerendy danych w kontenerach podzielonym na partycje, DB rozwiązania Cosmos trasy hello partycji toohello zapytań odpowiadającą wartości klucza partycji toohello określony w filtrze hello (jeśli istnieją).</span><span class="sxs-lookup"><span data-stu-id="0c2e9-149">When you query data in partitioned containers, Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="0c2e9-150">Na przykład to zapytanie jest kierowany toojust hello partycji zawierającego hello klucza partycji "XMS 0001".</span><span class="sxs-lookup"><span data-stu-id="0c2e9-150">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="0c2e9-151">Witaj następujące zapytanie nie ma filtr klucza partycji hello (DeviceId) i jest rozwiniętym tooall partycji, którym jest wykonywany przed hello partycjonowania indeksu.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-151">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="0c2e9-152">Należy pamiętać, że program toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` w hello interfejsu API REST) toohave hello SDK tooexecute zapytania na partycje.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-152">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="0c2e9-153">Obsługuje rozwiązania cosmos DB [funkcje agregujące](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` i `AVG` over podzielona na partycje przy użyciu programu SQL z zestawów SDK 1.12.0 i powyżej uruchomienia kontenerów.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="0c2e9-154">Zapytania musi zawierać pojedynczy operatora agregacji i musi zawierać jedną wartość w hello projekcji.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-154">Queries must include a single aggregate operator, and must include a single value in hello projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="0c2e9-155">Równoległego wykonywania zapytań</span><span class="sxs-lookup"><span data-stu-id="0c2e9-155">Parallel query execution</span></span>
<span data-ttu-id="0c2e9-156">Witaj zestawów SDK DB rozwiązania Cosmos 1.9.0 i powyżej Obsługa opcje wykonywania zapytania równoległe, umożliwiających tooperform małe opóźnienia zapytanie względem kolekcji partycjonowanych, nawet wtedy, gdy potrzebna jest tootouch dużą liczbę partycji.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-156">hello Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="0c2e9-157">Na przykład hello następującego zapytania jest skonfigurowany toorun równolegle na partycje.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-157">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="0c2e9-158">Możesz zarządzać równoległego wykonywania zapytań przez dostrajanie hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="0c2e9-158">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="0c2e9-159">Przez ustawienie `MaxDegreeOfParallelism`, można kontrolować hello stopień równoległości, tj. Data hello maksymalną liczbę kontenera sieci równoczesnych połączeń toohello partycji.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-159">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello container's partitions.</span></span> <span data-ttu-id="0c2e9-160">Jeśli ustawisz to zbyt-1, hello stopień równoległości jest zarządzana przez hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-160">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="0c2e9-161">Jeśli hello `MaxDegreeOfParallelism` nie jest określony lub ustaw too0, która jest wartością domyślną hello, będzie jednej sieci połączenia toohello kontenera na partycje.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-161">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello container's partitions.</span></span>
* <span data-ttu-id="0c2e9-162">Przez ustawienie `MaxBufferedItemCount`, można kompromis wykorzystanie pamięci zapytania opóźnienia i po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="0c2e9-163">Jeśli ten parametr lub ustaw tę wartość za 1 hello liczbę elementów buforowane podczas równoległego wykonywania zapytań jest zarządzana przez hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-163">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="0c2e9-164">Podane hello niezmienionym hello kolekcji, równoległe zapytania zostanie zwracają wyniki w hello kolejność takie same jak wykonanie szeregowego.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-164">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="0c2e9-165">Podczas wykonywania kwerendy między partycji zawierającej, sortowanie (ORDER BY i/lub góry), problemy z zestawu SDK platformy Azure rozwiązania Cosmos DB hello hello zapytania równolegle na partycje i scaleń częściowo sortowane wyniki w tooproduce po stronie klienta hello globalnie uporządkowanych wyników.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello Azure Cosmos DB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="0c2e9-166">Wykonywanie procedury składowane</span><span class="sxs-lookup"><span data-stu-id="0c2e9-166">Executing stored procedures</span></span>
<span data-ttu-id="0c2e9-167">Można również wykonywać transakcje atomic względem dokumentów za pomocą hello tego samego Identyfikatora urządzenia, np. Jeśli jest utrzymanie agreguje lub hello najnowszy stan urządzeń w jeden element.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-167">You can also execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="0c2e9-168">W następnej sekcji hello przyjrzymy się jak kontenery toopartitioned mogą być przenoszone z kontenerów jednej partycji.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-168">In hello next section, we look at how you can move toopartitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c2e9-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0c2e9-169">Next steps</span></span>
<span data-ttu-id="0c2e9-170">W tym artykule podaliśmy omówienie sposobu toowork z partycjonowania kontenerów bazy danych Azure rozwiązania Cosmos z hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-170">In this article, we provided an overview of how toowork with partitioning of Azure Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="0c2e9-171">Zobacz też [partycjonowania i skalowanie w poziomie](../cosmos-db/partition-data.md) omówienie pojęć i najlepsze rozwiązania dotyczące partycjonowania z jakiegokolwiek interfejsu API Azure rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="0c2e9-172">Należy przeprowadzić testowanie z bazy danych Azure rozwiązania Cosmos wydajności i skalowania.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="0c2e9-173">Zobacz [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md) przykładowe.</span><span class="sxs-lookup"><span data-stu-id="0c2e9-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="0c2e9-174">Rozpoczynanie pracy kodowania z hello [zestawów SDK](documentdb-sdk-dotnet.md) lub hello [interfejsu API REST](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="0c2e9-174">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="0c2e9-175">Dowiedz się więcej o [udostępnionej przepływności w usłudze Azure DB rozwiązania Cosmos](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="0c2e9-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

