---
title: "aaaWorking z zastosowaniem dat w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toowork z daty w usłudze Azure DB rozwiązania Cosmos."
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="c0c7e-103">Praca z daty w Azure rozwiązania Cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="c0c7e-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="c0c7e-104">Azure DB rozwiązania Cosmos zapewnia elastyczność schematu i rozbudowane indeksowanie za pomocą natywny [JSON](http://www.json.org) modelu danych.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="c0c7e-105">Wszystkie zasoby bazy danych rozwiązania Cosmos platformy Azure, w tym baz danych, kolekcji, dokumentów i procedury składowane są modelowane i przechowywane jako dokumenty JSON.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="c0c7e-106">Jako wymaganiem jest portable JSON (i bazy danych Azure rozwiązania Cosmos) obsługuje tylko niewielki zestaw typów podstawowych: ciąg, Number, Boolean, tablicy, obiektu i wartości Null.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="c0c7e-107">Jednak JSON jest elastyczny i umożliwia deweloperom i struktur toorepresent bardziej złożonych typów przy użyciu tych elementów podstawowych i tworzenia ich jako obiekty i tablice.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-107">However, JSON is flexible and allow developers and frameworks toorepresent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="c0c7e-108">Podstawowe typy toohello dodanie wiele aplikacji muszą hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) wpisz toorepresent daty i czasu.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-108">In addition toohello basic types, many applications need hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type toorepresent dates and timestamps.</span></span> <span data-ttu-id="c0c7e-109">W tym artykule opisano sposób deweloperzy można przechowywać, pobrać i dat w usłudze Azure DB rozwiązania Cosmos przy użyciu zestawu .NET SDK hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using hello .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="c0c7e-110">Przechowywanie dat i godzin</span><span class="sxs-lookup"><span data-stu-id="c0c7e-110">Storing DateTimes</span></span>
<span data-ttu-id="c0c7e-111">Domyślnie program hello [zestawu SDK usługi Azure rozwiązania Cosmos DB](documentdb-sdk-dotnet.md) serializuje wartości daty/godziny jako [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) ciągów.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-111">By default, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="c0c7e-112">Większość aplikacji można użyć hello domyślny ciąg reprezentujący dla daty i godziny dla hello z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="c0c7e-112">Most applications can use hello default string representation for DateTime for hello following reasons:</span></span>

* <span data-ttu-id="c0c7e-113">Można porównać ciągów i hello względne uporządkowanie hello wartości daty/godziny jest zachowywany, jeśli są one przekształcone toostrings.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-113">Strings can be compared, and hello relative ordering of hello DateTime values is preserved when they are transformed toostrings.</span></span> 
* <span data-ttu-id="c0c7e-114">Takie podejście nie wymaga żadnych niestandardowy kod lub atrybuty konwersji do formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="c0c7e-115">Hello dat jako przechowywane w formacie JSON są człowieka do odczytu.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-115">hello dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="c0c7e-116">Tej metody można korzystać z Azure rozwiązania Cosmos DB indeks wydajność szybkiego zapytań.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="c0c7e-117">Na przykład Witaj następujący fragment kodu magazynów `Order` obiektu zawierającego dwa właściwości daty i godziny — `ShipDate` i `OrderDate` jako dokument przy użyciu zestawu .NET SDK hello:</span><span class="sxs-lookup"><span data-stu-id="c0c7e-117">For example, hello following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using hello .NET SDK:</span></span>

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

<span data-ttu-id="c0c7e-118">Ten dokument jest przechowywany w usłudze Azure DB rozwiązania Cosmos w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c0c7e-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="c0c7e-119">Alternatywnie można przechowywać dat i godzin jako systemu Unix sygnatury czasowe, oznacza to, że jako liczba reprezentująca hello liczbę sekund czas od 1 stycznia 1970.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing hello number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="c0c7e-120">Sygnatura czasowa wewnętrzny Azure DB rozwiązania Cosmos (`_ts`) właściwość następuje tej metody.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="c0c7e-121">Można użyć hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) klasy tooserialize dat i godzin jako liczby.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-121">You can use hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class tooserialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="c0c7e-122">Indeksowanie zapytań zakres dat i godzin</span><span class="sxs-lookup"><span data-stu-id="c0c7e-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="c0c7e-123">Zakres zapytania są często używane z wartości daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="c0c7e-124">Na przykład jeśli konieczne toofind wszystkich zamówień tworzonych od wczoraj lub znaleźć zamówienia wydane hello ostatnich pięciu minut, należy tooperform zakresu zapytania.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-124">For example, if you need toofind all orders created since yesterday, or find all orders shipped in hello last five minutes, you need tooperform range queries.</span></span> <span data-ttu-id="c0c7e-125">tooexecute tych zapytań wydajnie, należy skonfigurować kolekcję dla zakresu indeksowania na ciągach.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-125">tooexecute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="c0c7e-126">Dowiedz się więcej na temat tooconfigure indeksowania zasady w [zasady indeksowania bazy danych Azure rozwiązania Cosmos](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c0c7e-126">You can learn more about how tooconfigure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="c0c7e-127">Wykonywanie zapytania dat i godzin w składniku LINQ</span><span class="sxs-lookup"><span data-stu-id="c0c7e-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="c0c7e-128">Witaj zestawu SDK .NET usługi DocumentDB obsługuje automatycznie zapytywanie o dane przechowywane w bazie danych rozwiązania Cosmos Azure za pomocą LINQ.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-128">hello DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="c0c7e-129">Na przykład hello poniższy fragment kodu przedstawia zapytania LINQ tego zamówienia filtry, które zostały wysłane w hello ostatnich trzech dni.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-129">For example, hello following snippet shows a LINQ query that filters orders that were shipped in hello last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="c0c7e-130">Dowiedz się więcej o DB rozwiązania Cosmos Azure SQL zapytań języka i hello dostawcy LINQ na [zapytań DB rozwiązania Cosmos](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="c0c7e-130">You can learn more about Azure Cosmos DB's SQL query language and hello LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="c0c7e-131">W tym artykule Analizujemy sposób toostore, indeksu i zapytania dat i godzin w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c0c7e-131">In this article, we looked at how toostore, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0c7e-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c0c7e-132">Next Steps</span></span>
* <span data-ttu-id="c0c7e-133">Pobierz i uruchom hello [przykłady w serwisie GitHub kodu](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="c0c7e-133">Download and run hello [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="c0c7e-134">Dowiedz się więcej o [zapytania interfejsu API usługi DocumentDB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="c0c7e-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="c0c7e-135">Dowiedz się więcej o [zasady indeksowania bazy danych Azure rozwiązania Cosmos](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="c0c7e-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
