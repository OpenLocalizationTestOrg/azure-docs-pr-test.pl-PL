---
title: "Praca z daty w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu pracy z daty w usłudze Azure DB rozwiązania Cosmos."
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
ms.openlocfilehash: b6a77e33eea24000037ffb31d7aae3cb1d345ce9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="9e898-103">Praca z daty w Azure rozwiązania Cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="9e898-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="9e898-104">Azure DB rozwiązania Cosmos zapewnia elastyczność schematu i rozbudowane indeksowanie za pomocą natywny [JSON](http://www.json.org) modelu danych.</span><span class="sxs-lookup"><span data-stu-id="9e898-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="9e898-105">Wszystkie zasoby bazy danych rozwiązania Cosmos platformy Azure, w tym baz danych, kolekcji, dokumentów i procedury składowane są modelowane i przechowywane jako dokumenty JSON.</span><span class="sxs-lookup"><span data-stu-id="9e898-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="9e898-106">Jako wymaganiem jest portable JSON (i bazy danych Azure rozwiązania Cosmos) obsługuje tylko niewielki zestaw typów podstawowych: ciąg, Number, Boolean, tablicy, obiektu i wartości Null.</span><span class="sxs-lookup"><span data-stu-id="9e898-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="9e898-107">Jednak JSON jest elastyczny i umożliwia deweloperom i platformy, do reprezentowania bardziej złożonych typów przy użyciu tych elementów podstawowych i tworzenia ich jako obiekty i tablice.</span><span class="sxs-lookup"><span data-stu-id="9e898-107">However, JSON is flexible and allow developers and frameworks to represent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="9e898-108">Oprócz podstawowych typów wiele aplikacji muszą [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) typu do reprezentowania daty i czasu.</span><span class="sxs-lookup"><span data-stu-id="9e898-108">In addition to the basic types, many applications need the [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type to represent dates and timestamps.</span></span> <span data-ttu-id="9e898-109">W tym artykule opisano sposób deweloperzy można przechowywać, pobieranie i zapytania dat w usłudze Azure DB rozwiązania Cosmos przy użyciu zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="9e898-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using the .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="9e898-110">Przechowywanie dat i godzin</span><span class="sxs-lookup"><span data-stu-id="9e898-110">Storing DateTimes</span></span>
<span data-ttu-id="9e898-111">Domyślnie [zestawu SDK usługi Azure rozwiązania Cosmos DB](documentdb-sdk-dotnet.md) serializuje wartości daty/godziny jako [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) ciągów.</span><span class="sxs-lookup"><span data-stu-id="9e898-111">By default, the [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="9e898-112">Większość aplikacji można użyć domyślnej reprezentacji ciągu dla typu DateTime z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="9e898-112">Most applications can use the default string representation for DateTime for the following reasons:</span></span>

* <span data-ttu-id="9e898-113">Można porównać ciągów i względne uporządkowanie wartości daty/godziny jest zachowywana, gdy są one przekształcone na ciągi.</span><span class="sxs-lookup"><span data-stu-id="9e898-113">Strings can be compared, and the relative ordering of the DateTime values is preserved when they are transformed to strings.</span></span> 
* <span data-ttu-id="9e898-114">Takie podejście nie wymaga żadnych niestandardowy kod lub atrybuty konwersji do formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="9e898-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="9e898-115">Dane przechowywane w formacie JSON są człowieka do odczytu.</span><span class="sxs-lookup"><span data-stu-id="9e898-115">The dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="9e898-116">Tej metody można korzystać z Azure rozwiązania Cosmos DB indeks wydajność szybkiego zapytań.</span><span class="sxs-lookup"><span data-stu-id="9e898-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="9e898-117">Na przykład poniższy fragment przechowuje `Order` obiektu zawierającego dwa właściwości daty i godziny — `ShipDate` i `OrderDate` jako dokument przy użyciu zestawu .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="9e898-117">For example, the following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using the .NET SDK:</span></span>

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

<span data-ttu-id="9e898-118">Ten dokument jest przechowywany w usłudze Azure DB rozwiązania Cosmos w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9e898-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="9e898-119">Alternatywnie można przechowywać dat i godzin jako systemu Unix sygnatury czasowe, czyli jako liczbę reprezentującą liczbę sekund czas od 1 stycznia 1970.</span><span class="sxs-lookup"><span data-stu-id="9e898-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing the number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="9e898-120">Sygnatura czasowa wewnętrzny Azure DB rozwiązania Cosmos (`_ts`) właściwość następuje tej metody.</span><span class="sxs-lookup"><span data-stu-id="9e898-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="9e898-121">Można użyć [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) klasy do serializacji dat i godzin jako liczby.</span><span class="sxs-lookup"><span data-stu-id="9e898-121">You can use the [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class to serialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="9e898-122">Indeksowanie zapytań zakres dat i godzin</span><span class="sxs-lookup"><span data-stu-id="9e898-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="9e898-123">Zakres zapytania są często używane z wartości daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="9e898-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="9e898-124">Na przykład jeśli należy znaleźć zamówienia utworzone od wczoraj lub znaleźć zamówienia wydane w ciągu ostatnich pięciu minut, należy wykonać kwerendy zakresu.</span><span class="sxs-lookup"><span data-stu-id="9e898-124">For example, if you need to find all orders created since yesterday, or find all orders shipped in the last five minutes, you need to perform range queries.</span></span> <span data-ttu-id="9e898-125">Do wykonania tych zapytań wydajnie, należy skonfigurować kolekcję dla zakresu indeksowania na ciągach.</span><span class="sxs-lookup"><span data-stu-id="9e898-125">To execute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="9e898-126">Dowiedz się więcej na temat sposobu konfigurowania zasad indeksowania w [zasady indeksowania bazy danych Azure rozwiązania Cosmos](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="9e898-126">You can learn more about how to configure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="9e898-127">Wykonywanie zapytania dat i godzin w składniku LINQ</span><span class="sxs-lookup"><span data-stu-id="9e898-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="9e898-128">Zestaw SDK .NET usługi DocumentDB obsługuje automatycznie zapytywanie o dane przechowywane w bazie danych rozwiązania Cosmos Azure za pomocą LINQ.</span><span class="sxs-lookup"><span data-stu-id="9e898-128">The DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="9e898-129">Na przykład poniższy fragment kodu przedstawia zapytania LINQ tego zamówienia filtry, które zostały wysłane w ciągu ostatnich trzech dni.</span><span class="sxs-lookup"><span data-stu-id="9e898-129">For example, the following snippet shows a LINQ query that filters orders that were shipped in the last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated to the following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="9e898-130">Dowiedz się więcej o język zapytań SQL Azure rozwiązania Cosmos DB i dostawcy LINQ w [zapytań DB rozwiązania Cosmos](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="9e898-130">You can learn more about Azure Cosmos DB's SQL query language and the LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="9e898-131">W tym artykule analizujemy przechowywania, indeksu i zapytania dat i godzin w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="9e898-131">In this article, we looked at how to store, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e898-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9e898-132">Next Steps</span></span>
* <span data-ttu-id="9e898-133">Pobierz i uruchom [przykłady w serwisie GitHub kodu](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="9e898-133">Download and run the [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="9e898-134">Dowiedz się więcej o [zapytania interfejsu API usługi DocumentDB](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="9e898-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="9e898-135">Dowiedz się więcej o [zasady indeksowania bazy danych Azure rozwiązania Cosmos](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="9e898-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
