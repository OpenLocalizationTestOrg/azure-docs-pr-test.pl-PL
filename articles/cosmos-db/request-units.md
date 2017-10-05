---
title: "Jednostek żądania & Szacowanie przepływności - DB rozwiązania Cosmos Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu zrozumieć, określ i oszacować wymagania dotyczące jednostki żądania w usłudze Azure DB rozwiązania Cosmos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 7a4efc0fb9b3855b9dbbe445768ceb2a9940d0b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="c8f19-103">Żądanie jednostki w Azure rozwiązania Cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="c8f19-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="c8f19-104">Teraz dostępne: Azure DB rozwiązania Cosmos [Kalkulator jednostki żądania](https://www.documentdb.com/capacityplanner).</span><span class="sxs-lookup"><span data-stu-id="c8f19-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="c8f19-105">Dowiedz się więcej w [Szacowanie przepustowość sieci musi](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="c8f19-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Kalkulator przepływności][5]

## <a name="introduction"></a><span data-ttu-id="c8f19-107">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="c8f19-107">Introduction</span></span>
<span data-ttu-id="c8f19-108">[Azure DB rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) jest globalnie rozproszone wielu modelu bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c8f19-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="c8f19-109">Z bazy danych rozwiązania Cosmos platformy Azure nie trzeba wynajmować maszyn wirtualnych, wdrażania oprogramowania lub monitora bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c8f19-109">With Azure Cosmos DB, you don't have to rent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="c8f19-110">Azure DB rozwiązania Cosmos jest obsługiwane i stale monitorowane przez górny pracownicy firmy Microsoft do dostarczania światowej klasy ochrony dostępności, wydajności i danych.</span><span class="sxs-lookup"><span data-stu-id="c8f19-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers to deliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="c8f19-111">Są dostępne dane przy użyciu interfejsów API wybranych jako [SQL usługi DocumentDB](documentdb-sql-query.md) (dokument) bazy danych MongoDB (dokument), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (klucz wartość) i [Gremlin](https://tinkerpop.apache.org/gremlin.html) (wykres) znajdują się w obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="c8f19-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="c8f19-112">Waluta Azure DB rozwiązania Cosmos jest jednostka żądań (RU).</span><span class="sxs-lookup"><span data-stu-id="c8f19-112">The currency of Azure Cosmos DB is the Request Unit (RU).</span></span> <span data-ttu-id="c8f19-113">Z RUs nie należy do zarezerwowania możliwości odczytu/zapisu lub udostępnić Procesora, pamięci i IOPS.</span><span class="sxs-lookup"><span data-stu-id="c8f19-113">With RUs, you do not need to reserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="c8f19-114">Azure DB rozwiązania Cosmos obsługuje kilka interfejsów API z różnych operacji — od prostych odczytuje i zapisuje wykres złożonych zapytań.</span><span class="sxs-lookup"><span data-stu-id="c8f19-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes to complex graph queries.</span></span> <span data-ttu-id="c8f19-115">Ponieważ nie wszystkie żądania są takie same, są przypisane znormalizowane ilość **jednostek żądania** na podstawie ilości obliczeń wymaganych do obsłużenia żądania.</span><span class="sxs-lookup"><span data-stu-id="c8f19-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on the amount of computation required to serve the request.</span></span> <span data-ttu-id="c8f19-116">Liczba jednostek żądania dla operacji jest deterministyczna, a można śledzić liczbę jednostek żądania używane przez żadnych operacji w usłudze Azure DB rozwiązania Cosmos za pośrednictwem nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="c8f19-116">The number of request units for an operation is deterministic, and you can track the number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="c8f19-117">Zapewnienie przewidywalnej wydajności, należy zarezerwować przepływności w jednostkach 100 RU/sekundę.</span><span class="sxs-lookup"><span data-stu-id="c8f19-117">To provide predictable performance, you need to reserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="c8f19-118">Po przeczytaniu tego artykułu, będziesz mieć możliwość odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="c8f19-118">After reading this article, you'll be able to answer the following questions:</span></span>  

* <span data-ttu-id="c8f19-119">Co to są jednostek żądania i żądania opłat?</span><span class="sxs-lookup"><span data-stu-id="c8f19-119">What are request units and request charges?</span></span>
* <span data-ttu-id="c8f19-120">Jak określić żądanie pojemność jednostki dla kolekcji?</span><span class="sxs-lookup"><span data-stu-id="c8f19-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="c8f19-121">Jak oszacować musi jednostki żądania Moja aplikacja</span><span class="sxs-lookup"><span data-stu-id="c8f19-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="c8f19-122">Co się stanie, jeśli I przekracza pojemność jednostki żądania dla kolekcji?</span><span class="sxs-lookup"><span data-stu-id="c8f19-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="c8f19-123">Bazy danych Azure rozwiązania Cosmos jest wiele modeli bazy danych, to należy pamiętać, że odnoszą się do kolekcji/dokumentu do dokumentu interfejsu API, wykres/węzła Graph API i tabeli na jednostkę tabeli interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c8f19-123">As Azure Cosmos DB is a multi-model database, it is important to note that we will refer to a collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="c8f19-124">Przepływność tego dokumentu, firma Microsoft będzie generalize koncepcji element/kontenera.</span><span class="sxs-lookup"><span data-stu-id="c8f19-124">Throughput this document we will generalize to the concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="c8f19-125">Jednostek żądania i żądania opłat</span><span class="sxs-lookup"><span data-stu-id="c8f19-125">Request units and request charges</span></span>
<span data-ttu-id="c8f19-126">Azure DB rozwiązania Cosmos zapewnia szybkie, przewidywalną wydajność przez *rezerwowania* zasobów do zaspokojenia musi przepływność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8f19-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources to satisfy your application's throughput needs.</span></span>  <span data-ttu-id="c8f19-127">Ponieważ aplikacja obciążenia i dostęp do zmiany wzorce wraz z upływem czasu, bazy danych Azure rozwiązania Cosmos umożliwia łatwe zwiększyć lub zmniejszyć ilość zarezerwowaną przepływnością dostępne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8f19-127">Because application load and access patterns change over time, Azure Cosmos DB allows you to easily increase or decrease the amount of reserved throughput available to your application.</span></span>

<span data-ttu-id="c8f19-128">Z bazy danych Azure rozwiązania Cosmos zarezerwowaną przepływnością jest określane w przeliczeniu na jednostki żądania przetwarzania na sekundę.</span><span class="sxs-lookup"><span data-stu-id="c8f19-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="c8f19-129">Można potraktować jednostki żądania jako walutę przepływności, zgodnie z którymi możesz *zarezerwować* ilość gwarantowane żądania jednostki dostępne dla aplikacji na podstawie sekundowym.</span><span class="sxs-lookup"><span data-stu-id="c8f19-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available to your application on per second basis.</span></span>  <span data-ttu-id="c8f19-130">Każdej operacji w usłudze Azure DB rozwiązania Cosmos — zapisywanie dokumentu, wykonywania zapytania, aktualizowanie dokumentu — korzysta z Procesora, pamięci i IOPS.</span><span class="sxs-lookup"><span data-stu-id="c8f19-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="c8f19-131">Oznacza to, że każda operacja wiąże się z *żądań bezpłatnie*, który jest wyrażona w *jednostek żądania*.</span><span class="sxs-lookup"><span data-stu-id="c8f19-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="c8f19-132">Opis czynników, które będzie mieć wpływ na koszty jednostki żądania, oraz wymagania dotyczące przepływności aplikacji, umożliwia uruchamianie aplikacji jako koszt skutecznie, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="c8f19-132">Understanding the factors which impact request unit charges, along with your application's throughput requirements, enables you to run your application as cost effectively as possible.</span></span> <span data-ttu-id="c8f19-133">Eksplorator zapytań jest również cudowne narzędzie do testowania podstawowej zapytania.</span><span class="sxs-lookup"><span data-stu-id="c8f19-133">The query explorer is also a wonderful tool to test the core of a query.</span></span>

<span data-ttu-id="c8f19-134">Zalecamy rozpoczęcie pracy od obejrzenia poniższego klipu wideo, w którym Aravind Ramachandran wyjaśniono jednostek żądania i przewidywalną wydajność bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c8f19-134">We recommend getting started by watching the following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="c8f19-135">Określanie pojemność jednostki żądania w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="c8f19-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="c8f19-136">Przy uruchamianiu nową kolekcję, tabeli lub wykres, określ liczbę jednostek żądań na sekundę (RU na sekundę) mają zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="c8f19-136">When starting a new collection, table or graph, you specify the number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="c8f19-137">Na podstawie udostępnionej przepływności, bazy danych rozwiązania Cosmos Azure przydziela fizycznej partycji do obsługi kolekcji i podziałów/rebalances danych na partycji jako ich przyrostu.</span><span class="sxs-lookup"><span data-stu-id="c8f19-137">Based on the provisioned throughput, Azure Cosmos DB allocates physical partitions to host your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="c8f19-138">Azure DB rozwiązania Cosmos wymaga klucza partycji, należy określić, gdy kolekcja jest inicjowana z 2500 jednostek żądania lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c8f19-138">Azure Cosmos DB requires a partition key to be specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="c8f19-139">Klucz partycji jest wymagany również skalować przepływność kolekcji poza 2500 jednostki żądania w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c8f19-139">A partition key is also required to scale your collection's throughput beyond 2,500 request units in the future.</span></span> <span data-ttu-id="c8f19-140">W związku z tym zdecydowanie zaleca się konfigurowanie [klucza partycji](partition-data.md) podczas tworzenia kontenera niezależnie od programu początkowej przepływności.</span><span class="sxs-lookup"><span data-stu-id="c8f19-140">Therefore, it is highly recommended to configure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="c8f19-141">Ponieważ danych może być konieczne można podzielić na wiele partycji, jest konieczne pobranie klucza partycji, który ma dużej kardynalności (od 100 do milionów unikatowe wartości), dzięki czemu żądania i kolekcji/tabeli/graph mogą być skalowane jednolicie Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c8f19-141">Since your data might have to be split across multiple partitions, it is necessary to pick a partition key that has a high cardinality (100 to millions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="c8f19-142">Klucz partycji to logiczne granic, a nie jeden fizyczny.</span><span class="sxs-lookup"><span data-stu-id="c8f19-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="c8f19-143">W związku z tym nie należy ograniczyć liczbę wartości klucza partycji distinct.</span><span class="sxs-lookup"><span data-stu-id="c8f19-143">Therefore, you do not need to limit the number of distinct partition key values.</span></span> <span data-ttu-id="c8f19-144">W rzeczywistości jest lepiej użyć więcej różne wartości klucza partycji niż mniej, jako bazy danych rozwiązania Cosmos Azure ma więcej opcje równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c8f19-144">It is in fact better to have more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="c8f19-145">Oto fragment kodu dotyczący tworzenia kolekcji z 3000 jednostek żądania na drugi przy użyciu zestawu .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="c8f19-145">Here is a code snippet for creating a collection with 3,000 request units per second using the .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="c8f19-146">Azure DB rozwiązania Cosmos działa modelu rezerwacji przepływności.</span><span class="sxs-lookup"><span data-stu-id="c8f19-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="c8f19-147">Oznacza to, że są rozliczane ilości przepływności *zastrzeżone*, niezależnie od tego, jaka część tego przepływności jest aktywnie *używane*.</span><span class="sxs-lookup"><span data-stu-id="c8f19-147">That is, you are billed for the amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="c8f19-148">Aplikacją na obciążenia, danych i użycia zmiany wzorce, można łatwo skalowania ilość zastrzeżone RUs za pomocą zestawów SDK lub przy użyciu [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c8f19-148">As your application's load, data, and usage patterns change you can easily scale up and down the amount of reserved RUs through SDKs or using the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="c8f19-149">Każda kolekcja/tabeli/wykresu są mapowane na `Offer` zasobów w usłudze Azure DB rozwiązania Cosmos mającej metadane dotyczące udostępnionej przepływności.</span><span class="sxs-lookup"><span data-stu-id="c8f19-149">Each collection/table/graph are mapped to an `Offer` resource in Azure Cosmos DB, which has metadata about the provisioned throughput.</span></span> <span data-ttu-id="c8f19-150">Możesz zmienić przydzielone przepływności wyszukiwania odpowiadający jej zasób oferta dla kontenera, a następnie zaktualizowaniem go przy użyciu nowej wartości przepływności.</span><span class="sxs-lookup"><span data-stu-id="c8f19-150">You can change the allocated throughput by looking up the corresponding offer resource for a container, then updating it with the new throughput value.</span></span> <span data-ttu-id="c8f19-151">Oto fragment kodu do zmiany przepływność kolekcji do 5000 jednostek żądania na drugi przy użyciu zestawu .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="c8f19-151">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second using the .NET SDK:</span></span>

```csharp
// Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set the throughput to 5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="c8f19-152">Jeśli zmienisz przepływność jest bez zakłócania dostępności z kontenera.</span><span class="sxs-lookup"><span data-stu-id="c8f19-152">There is no impact to the availability of your container when you change the throughput.</span></span> <span data-ttu-id="c8f19-153">Zazwyczaj nowe zarezerwowaną przepływnością obowiązuje w ciągu kilku sekund na stosowanie nowych przepływności.</span><span class="sxs-lookup"><span data-stu-id="c8f19-153">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="c8f19-154">Zagadnienia dotyczące jednostki żądania</span><span class="sxs-lookup"><span data-stu-id="c8f19-154">Request unit considerations</span></span>
<span data-ttu-id="c8f19-155">Szacowanie liczby jednostek żądania do zarezerwowania dla Twojej bazy danych Azure rozwiązania Cosmos kontenera, należy wziąć pod uwagę następujące zmienne:</span><span class="sxs-lookup"><span data-stu-id="c8f19-155">When estimating the number of request units to reserve for your Azure Cosmos DB container, it is important to take the following variables into consideration:</span></span>

* <span data-ttu-id="c8f19-156">**Rozmiar elementu**.</span><span class="sxs-lookup"><span data-stu-id="c8f19-156">**Item size**.</span></span> <span data-ttu-id="c8f19-157">Jak rozmiarze jednostki używane do odczytu lub zapisu danych zwiększa.</span><span class="sxs-lookup"><span data-stu-id="c8f19-157">As size increases the units consumed to read or write the data will also increase.</span></span>
* <span data-ttu-id="c8f19-158">**Liczba właściwości elementu**.</span><span class="sxs-lookup"><span data-stu-id="c8f19-158">**Item property count**.</span></span> <span data-ttu-id="c8f19-159">Przyjmuje indeksowania domyślne wszystkich właściwości, jednostki używane do zapisywania dokumentu/węzła/ntity zwiększa się wraz ze wzrostem liczby właściwości.</span><span class="sxs-lookup"><span data-stu-id="c8f19-159">Assuming default indexing of all properties, the units consumed to write a document/node/ntity will increase as the property count increases.</span></span>
* <span data-ttu-id="c8f19-160">**Spójność danych**.</span><span class="sxs-lookup"><span data-stu-id="c8f19-160">**Data consistency**.</span></span> <span data-ttu-id="c8f19-161">Gdy za pomocą poziomów spójności danych silne lub ograniczonych nieaktualności, dodatkowych jednostek zostaną użyte do odczytu elementów.</span><span class="sxs-lookup"><span data-stu-id="c8f19-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed to read items.</span></span>
* <span data-ttu-id="c8f19-162">**Właściwości indeksowanych**.</span><span class="sxs-lookup"><span data-stu-id="c8f19-162">**Indexed properties**.</span></span> <span data-ttu-id="c8f19-163">Zasady indeksu na każdego kontenera określa właściwości, które są indeksowane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="c8f19-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="c8f19-164">Można ograniczyć zużycie jednostki Twoje żądanie, przez ograniczenie liczby właściwości indeksowanych lub włączenie indeksowanie z opóźnieniem.</span><span class="sxs-lookup"><span data-stu-id="c8f19-164">You can reduce your request unit consumption by limiting the number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="c8f19-165">**Indeksowanie dokumentów**.</span><span class="sxs-lookup"><span data-stu-id="c8f19-165">**Document indexing**.</span></span> <span data-ttu-id="c8f19-166">Domyślnie każdy element jest automatycznie indeksowane będą korzystać mniejszej liczby jednostek żądania, jeśli wybierzesz nie może zindeksować niektórych elementów.</span><span class="sxs-lookup"><span data-stu-id="c8f19-166">By default each item is automatically indexed, you will consume fewer request units if you choose not to index some of your items.</span></span>
* <span data-ttu-id="c8f19-167">**Zapytanie wzorce**.</span><span class="sxs-lookup"><span data-stu-id="c8f19-167">**Query patterns**.</span></span> <span data-ttu-id="c8f19-168">Złożoność kwerendy wpływa na liczbę jednostek żądania są używane dla operacji.</span><span class="sxs-lookup"><span data-stu-id="c8f19-168">The complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="c8f19-169">Liczba predykatów, rodzaj predykaty, projekcje liczbę funkcji UDF i rozmiaru zestawu danych źródła wszystkich wpływ kosztów operacji zapytania.</span><span class="sxs-lookup"><span data-stu-id="c8f19-169">The number of predicates, nature of the predicates, projections, number of UDFs, and the size of the source data set all influence the cost of query operations.</span></span>
* <span data-ttu-id="c8f19-170">**Użycie skryptu**.</span><span class="sxs-lookup"><span data-stu-id="c8f19-170">**Script usage**.</span></span>  <span data-ttu-id="c8f19-171">Podobnie jak w przypadku zapytań, procedury składowane i wyzwalaczy wykorzystywać jednostki żądania, zależnie od stopnia złożoności wykonywania operacji.</span><span class="sxs-lookup"><span data-stu-id="c8f19-171">As with queries, stored procedures and triggers consume request units based on the complexity of the operations being performed.</span></span> <span data-ttu-id="c8f19-172">Podczas opracowywania aplikacji, sprawdź, czy nagłówek opłat żądania, aby lepiej zrozumieć, jak każdej operacji zajmuje pojemność jednostki żądania.</span><span class="sxs-lookup"><span data-stu-id="c8f19-172">As you develop your application, inspect the request charge header to better understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="c8f19-173">Planowania potrzeb w zakresie przepustowości</span><span class="sxs-lookup"><span data-stu-id="c8f19-173">Estimating throughput needs</span></span>
<span data-ttu-id="c8f19-174">Jednostka żądania jest znormalizowane miara kosztu przetwarzania żądania.</span><span class="sxs-lookup"><span data-stu-id="c8f19-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="c8f19-175">Jednostka pojedyncze żądanie reprezentuje możliwości przetwarzania wymagane do odczytu (za pośrednictwem łączy własnych lub identyfikator) pojedynczego 1KB elementu składające się z 10 unikatowe wartości (z wyjątkiem właściwości systemu).</span><span class="sxs-lookup"><span data-stu-id="c8f19-175">A single request unit represents the processing capacity required to read (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="c8f19-176">Żądanie utworzenia (Wstaw), Zamień lub Usuń ten sam element będą korzystać z dodatkowych zadań przetwarzania przez usługę i tym samym więcej jednostek żądania.</span><span class="sxs-lookup"><span data-stu-id="c8f19-176">A request to create (insert), replace or delete the same item will consume more processing from the service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="c8f19-177">Linia bazowa jednostka żądania 1 do 1KB elementu odpowiada proste GET przez łącze własne lub identyfikator elementu.</span><span class="sxs-lookup"><span data-stu-id="c8f19-177">The baseline of 1 request unit for a 1KB item corresponds to a simple GET by self link or id of the item.</span></span>
> 
> 

<span data-ttu-id="c8f19-178">Na przykład, w tym miejscu jest tabelę, która zawiera liczbę jednostek żądania udzielenia na trzy rozmiary innego elementu (1KB, 4KB do 64KB) i na dwa różne poziomy wydajności (odczyty 500 na sekundę 100 zapisy na sekundę i 500 odczyty/sekundę + 500 zapisy na sekundę).</span><span class="sxs-lookup"><span data-stu-id="c8f19-178">For example, here's a table that shows how many request units to provision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="c8f19-179">Spójność danych skonfigurowano na sesji, a zasady indeksowania został ustawiony na None.</span><span class="sxs-lookup"><span data-stu-id="c8f19-179">The data consistency was configured at Session, and the indexing policy was set to None.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="c8f19-180"><strong>Rozmiar elementu</strong></span><span class="sxs-lookup"><span data-stu-id="c8f19-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-181"><strong>Odczyty/sekundę</strong></span><span class="sxs-lookup"><span data-stu-id="c8f19-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-182"><strong>Zapisy na sekundę</strong></span><span class="sxs-lookup"><span data-stu-id="c8f19-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-183"><strong>Jednostki żądania</strong></span><span class="sxs-lookup"><span data-stu-id="c8f19-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c8f19-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="c8f19-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-185">500</span><span class="sxs-lookup"><span data-stu-id="c8f19-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-186">100</span><span class="sxs-lookup"><span data-stu-id="c8f19-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-187">(500 * 1) + (100 * 5) = 1 000 RU/s</span><span class="sxs-lookup"><span data-stu-id="c8f19-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c8f19-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="c8f19-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-189">500</span><span class="sxs-lookup"><span data-stu-id="c8f19-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-190">500</span><span class="sxs-lookup"><span data-stu-id="c8f19-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-191">(500 * 1) + (500 * 5) = 3 000 RU/s</span><span class="sxs-lookup"><span data-stu-id="c8f19-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c8f19-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="c8f19-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-193">500</span><span class="sxs-lookup"><span data-stu-id="c8f19-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-194">100</span><span class="sxs-lookup"><span data-stu-id="c8f19-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-195">(500 * 1,3) + (100 * 7) = 1,350 RU/s</span><span class="sxs-lookup"><span data-stu-id="c8f19-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c8f19-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="c8f19-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-197">500</span><span class="sxs-lookup"><span data-stu-id="c8f19-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-198">500</span><span class="sxs-lookup"><span data-stu-id="c8f19-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-199">(500 * 1,3) + (500 * 7) = 4,150 RU/s</span><span class="sxs-lookup"><span data-stu-id="c8f19-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c8f19-200">64 KB</span><span class="sxs-lookup"><span data-stu-id="c8f19-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-201">500</span><span class="sxs-lookup"><span data-stu-id="c8f19-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-202">100</span><span class="sxs-lookup"><span data-stu-id="c8f19-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span><span class="sxs-lookup"><span data-stu-id="c8f19-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c8f19-204">64 KB</span><span class="sxs-lookup"><span data-stu-id="c8f19-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-205">500</span><span class="sxs-lookup"><span data-stu-id="c8f19-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-206">500</span><span class="sxs-lookup"><span data-stu-id="c8f19-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c8f19-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="c8f19-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-the-request-unit-calculator"></a><span data-ttu-id="c8f19-208">Użycie kalkulatora jednostki żądania</span><span class="sxs-lookup"><span data-stu-id="c8f19-208">Use the request unit calculator</span></span>
<span data-ttu-id="c8f19-209">Aby ułatwić klientom poprawnie dostroić ich ocen przepływności, jest opartego na sieci web [Kalkulator jednostki żądania](https://www.documentdb.com/capacityplanner) aby oszacować wymagania dotyczące jednostki żądania dla operacji typowych, w tym:</span><span class="sxs-lookup"><span data-stu-id="c8f19-209">To help customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) to help estimate the request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="c8f19-210">Element tworzy (zapisy)</span><span class="sxs-lookup"><span data-stu-id="c8f19-210">Item creates (writes)</span></span>
* <span data-ttu-id="c8f19-211">Odczytuje element</span><span class="sxs-lookup"><span data-stu-id="c8f19-211">Item reads</span></span>
* <span data-ttu-id="c8f19-212">Usuwa element</span><span class="sxs-lookup"><span data-stu-id="c8f19-212">Item deletes</span></span>
* <span data-ttu-id="c8f19-213">Element aktualizacji</span><span class="sxs-lookup"><span data-stu-id="c8f19-213">Item updates</span></span>

<span data-ttu-id="c8f19-214">Narzędzie obejmuje również obsługę Szacowanie oparte na elementach próbki, podane wymagania dotyczące przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="c8f19-214">The tool also includes support for estimating data storage needs based on the sample items you provide.</span></span>

<span data-ttu-id="c8f19-215">Za pomocą narzędzia jest prosty:</span><span class="sxs-lookup"><span data-stu-id="c8f19-215">Using the tool is simple:</span></span>

1. <span data-ttu-id="c8f19-216">Należy przekazać co najmniej jeden element reprezentatywny.</span><span class="sxs-lookup"><span data-stu-id="c8f19-216">Upload one or more representative items.</span></span>
   
    ![Przekaż elementów do Kalkulatora jednostki żądania][2]
2. <span data-ttu-id="c8f19-218">Aby oszacować wymagania dotyczące magazynu danych, wprowadź całkowitą liczbę elementów, które chcesz przechowywać.</span><span class="sxs-lookup"><span data-stu-id="c8f19-218">To estimate data storage requirements, enter the total number of items you expect to store.</span></span>
3. <span data-ttu-id="c8f19-219">Wprowadź liczbę elementów, które tworzenia, odczytu, aktualizacji i usuwania działań, które wymagają (na podstawie na sekundę).</span><span class="sxs-lookup"><span data-stu-id="c8f19-219">Enter the number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="c8f19-220">Aby oszacować opłat jednostki żądania operacji aktualizowania elementu, Przekaż kopię elementu próbki z kroku 1 zawiera pole typowe aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="c8f19-220">To estimate the request unit charges of item update operations, upload a copy of the sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="c8f19-221">Na przykład aktualizacji elementu zmodyfikowania zwykle dwie właściwości o nazwie lastLogin i userVisits, następnie po prostu skopiuj element przykładowych, zaktualizuj wartości dla tych dwóch właściwości i przekaż skopiowany element.</span><span class="sxs-lookup"><span data-stu-id="c8f19-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy the sample item, update the values for those two properties, and upload the copied item.</span></span>
   
    ![Wprowadź wymagania dotyczące przepływności w Kalkulator jednostki żądania][3]
4. <span data-ttu-id="c8f19-223">Kliknij przycisk Oblicz i przejrzeć wyniki.</span><span class="sxs-lookup"><span data-stu-id="c8f19-223">Click calculate and examine the results.</span></span>
   
    ![Wyniki Kalkulator jednostki żądania][4]

> [!NOTE]
> <span data-ttu-id="c8f19-225">Jeśli masz typów elementów, które różnią się znacznie pod względem rozmiaru i liczby właściwości indeksowanych, Przekaż przykładowe każdego *typu* z typowych elementu do narzędzia i obliczyć wyniki.</span><span class="sxs-lookup"><span data-stu-id="c8f19-225">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then upload a sample of each *type* of typical item to the tool and then calculate the results.</span></span>
> 
> 

### <a name="use-the-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="c8f19-226">Użyj nagłówka odpowiedzi opłat żądania bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="c8f19-226">Use the Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="c8f19-227">Każdy odpowiedź z usługi Azure DB rozwiązania Cosmos zawiera niestandardowy nagłówek (`x-ms-request-charge`) zawiera jednostki żądania używane dla żądania.</span><span class="sxs-lookup"><span data-stu-id="c8f19-227">Every response from the Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains the request units consumed for the request.</span></span> <span data-ttu-id="c8f19-228">Ten nagłówek jest również dostępny za pośrednictwem Azure DB rozwiązania Cosmos z zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="c8f19-228">This header is also accessible through the Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="c8f19-229">W zestawie SDK .NET RequestCharge jest właściwością obiektu ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="c8f19-229">In the .NET SDK, RequestCharge is a property of the ResourceResponse object.</span></span>  <span data-ttu-id="c8f19-230">Dla zapytań Eksploratora zapytań bazy danych Azure rozwiązania Cosmos w portalu Azure informacje żądania opłaty dotyczące wykonywane zapytania.</span><span class="sxs-lookup"><span data-stu-id="c8f19-230">For queries, the Azure Cosmos DB Query Explorer in the Azure portal provides request charge information for executed queries.</span></span>

![Badanie RU opłat w Eksploratorze zapytania][1]

<span data-ttu-id="c8f19-232">Pamiętając o tym jednej metody w oszacowania zarezerwowaną przepływnością wymagane przez aplikację jest rejestrowanie skojarzone z systemem typowymi operacjami względem elementu reprezentatywny używanych przez aplikację, a następnie Szacowanie opłata jednostki żądania Liczba operacji przewidujesz wykonywania każdej sekundy.</span><span class="sxs-lookup"><span data-stu-id="c8f19-232">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="c8f19-233">Pamiętaj mierzyć i obejmują typowe zapytania i również użycie skryptu bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c8f19-233">Be sure to measure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="c8f19-234">Jeśli masz typów elementów, które różnią się znacznie pod względem rozmiaru i liczby właściwości indeksowanych rejestrowania opłata jednostki żądanie dotyczy operacji związanych z każdym *typu* typowe elementu.</span><span class="sxs-lookup"><span data-stu-id="c8f19-234">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="c8f19-235">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c8f19-235">For example:</span></span>

1. <span data-ttu-id="c8f19-236">Zarejestruj opłata jednostki żądania tworzenia (Wstawianie) typowe elementu.</span><span class="sxs-lookup"><span data-stu-id="c8f19-236">Record the request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="c8f19-237">Rekord opłata jednostki żądanie odczytu typowe elementu.</span><span class="sxs-lookup"><span data-stu-id="c8f19-237">Record the request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="c8f19-238">Rekord opłata jednostki żądania aktualizowania typowych elementu.</span><span class="sxs-lookup"><span data-stu-id="c8f19-238">Record the request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="c8f19-239">Rekord opłata jednostki żądania elementu typowe, typowe zapytań.</span><span class="sxs-lookup"><span data-stu-id="c8f19-239">Record the request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="c8f19-240">Zarejestruj opłata jednostki żądania żadnych niestandardowych skryptów (procedury składowane, wyzwalacze, funkcje zdefiniowane przez użytkownika) wykorzystywana przez aplikację</span><span class="sxs-lookup"><span data-stu-id="c8f19-240">Record the request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by the application</span></span>
6. <span data-ttu-id="c8f19-241">Oblicz jednostki żądania wymagane podane szacowaną liczbę operacji, które planujesz do uruchomienia w ciągu sekundy.</span><span class="sxs-lookup"><span data-stu-id="c8f19-241">Calculate the required request units given the estimated number of operations you anticipate to run each second.</span></span>

### <span data-ttu-id="c8f19-242"><a id="GetLastRequestStatistics"></a>Za pomocą interfejsu API dla bazy danych MongoDB w GetLastRequestStatistics polecenia</span><span class="sxs-lookup"><span data-stu-id="c8f19-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="c8f19-243">Interfejs API bazy danych mongodb obsługuje polecenia niestandardowych, *getLastRequestStatistics*, pobierania opłat żądania dla określonej operacji.</span><span class="sxs-lookup"><span data-stu-id="c8f19-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving the request charge for specified operations.</span></span>

<span data-ttu-id="c8f19-244">Na przykład w powłokę Mongo, należy wykonać chcesz zweryfikować opłata żądania dla operacji.</span><span class="sxs-lookup"><span data-stu-id="c8f19-244">For example, in the Mongo Shell, execute the operation you want to verify the request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="c8f19-245">Następnie wykonaj polecenie *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="c8f19-245">Next, execute the command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="c8f19-246">Pamiętając o tym jednej metody w oszacowania zarezerwowaną przepływnością wymagane przez aplikację jest rejestrowanie skojarzone z systemem typowymi operacjami względem elementu reprezentatywny używanych przez aplikację, a następnie Szacowanie opłata jednostki żądania Liczba operacji przewidujesz wykonywania każdej sekundy.</span><span class="sxs-lookup"><span data-stu-id="c8f19-246">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="c8f19-247">Jeśli masz typów elementów, które różnią się znacznie pod względem rozmiaru i liczby właściwości indeksowanych rejestrowania opłata jednostki żądanie dotyczy operacji związanych z każdym *typu* typowe elementu.</span><span class="sxs-lookup"><span data-stu-id="c8f19-247">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="c8f19-248">Za pomocą interfejsu API dla bazy danych MongoDB w portalu metryki</span><span class="sxs-lookup"><span data-stu-id="c8f19-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="c8f19-249">Najprostszym sposobem, aby uzyskać dobrą szacowania żądania opłat jednostki do interfejsu API jest korzystanie z bazy danych MongoDB [portalu Azure](https://portal.azure.com) metryki.</span><span class="sxs-lookup"><span data-stu-id="c8f19-249">The simplest way to get a good estimation of request unit charges for your API for MongoDB database is to use the [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="c8f19-250">Z *liczba żądań* i *opłat żądania* wykresy, możesz uzyskać oszacowanie liczbę jednostek żądania, każdy zajmuje operacji i liczbę jednostek żądania zużywają względem siebie.</span><span class="sxs-lookup"><span data-stu-id="c8f19-250">With the *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative to one another.</span></span>

![Interfejs API dla metryki portalu bazy danych MongoDB][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="c8f19-252">W przykładzie szacowania jednostki żądania</span><span class="sxs-lookup"><span data-stu-id="c8f19-252">A request unit estimation example</span></span>
<span data-ttu-id="c8f19-253">Należy wziąć pod uwagę następujące dokumentu ~ 1KB:</span><span class="sxs-lookup"><span data-stu-id="c8f19-253">Consider the following ~1KB document:</span></span>

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="c8f19-254">Dokumenty są zminimalizowany w usłudze Azure DB rozwiązania Cosmos, więc system obliczeniowe rozmiar dokumentu powyżej jest nieco mniej niż 1 KB.</span><span class="sxs-lookup"><span data-stu-id="c8f19-254">Documents are minified in Azure Cosmos DB, so the system calculated size of the document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="c8f19-255">W poniższej tabeli przedstawiono przybliżone żądania jednostki związanych z typowymi operacjami na tym elemencie (opłata jednostki żądania przybliżonej przy założeniu, że poziomu spójności konta jest ustawiona na "Sesja" i że wszystkie elementy są automatycznie indeksowane):</span><span class="sxs-lookup"><span data-stu-id="c8f19-255">The following table shows approximate request unit charges for typical operations on this item (the approximate request unit charge assumes that the account consistency level is set to “Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="c8f19-256">Operacja</span><span class="sxs-lookup"><span data-stu-id="c8f19-256">Operation</span></span> | <span data-ttu-id="c8f19-257">Opłata jednostki żądania</span><span class="sxs-lookup"><span data-stu-id="c8f19-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="c8f19-258">Utwórz element</span><span class="sxs-lookup"><span data-stu-id="c8f19-258">Create item</span></span> |<span data-ttu-id="c8f19-259">~ 15 RU</span><span class="sxs-lookup"><span data-stu-id="c8f19-259">~15 RU</span></span> |
| <span data-ttu-id="c8f19-260">Odczytu elementu</span><span class="sxs-lookup"><span data-stu-id="c8f19-260">Read item</span></span> |<span data-ttu-id="c8f19-261">~ 1 RU</span><span class="sxs-lookup"><span data-stu-id="c8f19-261">~1 RU</span></span> |
| <span data-ttu-id="c8f19-262">Element zapytania według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="c8f19-262">Query item by id</span></span> |<span data-ttu-id="c8f19-263">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="c8f19-263">~2.5 RU</span></span> |

<span data-ttu-id="c8f19-264">Ponadto w poniższej tabeli zamieszczono przybliżonej żądania jednostki opłat za typowe zapytania używane w aplikacji:</span><span class="sxs-lookup"><span data-stu-id="c8f19-264">Additionally, this table shows approximate request unit charges for typical queries used in the application:</span></span>

| <span data-ttu-id="c8f19-265">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="c8f19-265">Query</span></span> | <span data-ttu-id="c8f19-266">Opłata jednostki żądania</span><span class="sxs-lookup"><span data-stu-id="c8f19-266">Request Unit Charge</span></span> | <span data-ttu-id="c8f19-267">Liczba zwróconych elementów</span><span class="sxs-lookup"><span data-stu-id="c8f19-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8f19-268">Wybierz żywności według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="c8f19-268">Select food by id</span></span> |<span data-ttu-id="c8f19-269">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="c8f19-269">~2.5 RU</span></span> |<span data-ttu-id="c8f19-270">1</span><span class="sxs-lookup"><span data-stu-id="c8f19-270">1</span></span> |
| <span data-ttu-id="c8f19-271">Wybierz żywności według producenta</span><span class="sxs-lookup"><span data-stu-id="c8f19-271">Select foods by manufacturer</span></span> |<span data-ttu-id="c8f19-272">~ 7 RU</span><span class="sxs-lookup"><span data-stu-id="c8f19-272">~7 RU</span></span> |<span data-ttu-id="c8f19-273">7</span><span class="sxs-lookup"><span data-stu-id="c8f19-273">7</span></span> |
| <span data-ttu-id="c8f19-274">Wybierz grupy żywności i kolejność według wagi</span><span class="sxs-lookup"><span data-stu-id="c8f19-274">Select by food group and order by weight</span></span> |<span data-ttu-id="c8f19-275">~ 70 RU</span><span class="sxs-lookup"><span data-stu-id="c8f19-275">~70 RU</span></span> |<span data-ttu-id="c8f19-276">100</span><span class="sxs-lookup"><span data-stu-id="c8f19-276">100</span></span> |
| <span data-ttu-id="c8f19-277">Zaznacz górny żywności 10 w grupie żywności</span><span class="sxs-lookup"><span data-stu-id="c8f19-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="c8f19-278">~ 10 RU</span><span class="sxs-lookup"><span data-stu-id="c8f19-278">~10 RU</span></span> |<span data-ttu-id="c8f19-279">10</span><span class="sxs-lookup"><span data-stu-id="c8f19-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="c8f19-280">Opłat RU się różnić w zależności od liczby elementów zwróconych.</span><span class="sxs-lookup"><span data-stu-id="c8f19-280">RU charges vary based on the number of items returned.</span></span>
> 
> 

<span data-ttu-id="c8f19-281">Dzięki tym informacjom możemy oszacować wymagania RU dla tej aplikacji liczby operacji i zapytań Oczekujemy na sekundę:</span><span class="sxs-lookup"><span data-stu-id="c8f19-281">With this information, we can estimate the RU requirements for this application given the number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="c8f19-282">Operacja/zapytania</span><span class="sxs-lookup"><span data-stu-id="c8f19-282">Operation/Query</span></span> | <span data-ttu-id="c8f19-283">Szacowaną liczbę na sekundę</span><span class="sxs-lookup"><span data-stu-id="c8f19-283">Estimated number per second</span></span> | <span data-ttu-id="c8f19-284">Wymagane RUs</span><span class="sxs-lookup"><span data-stu-id="c8f19-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c8f19-285">Utwórz element</span><span class="sxs-lookup"><span data-stu-id="c8f19-285">Create item</span></span> |<span data-ttu-id="c8f19-286">10</span><span class="sxs-lookup"><span data-stu-id="c8f19-286">10</span></span> |<span data-ttu-id="c8f19-287">150</span><span class="sxs-lookup"><span data-stu-id="c8f19-287">150</span></span> |
| <span data-ttu-id="c8f19-288">Odczytu elementu</span><span class="sxs-lookup"><span data-stu-id="c8f19-288">Read item</span></span> |<span data-ttu-id="c8f19-289">100</span><span class="sxs-lookup"><span data-stu-id="c8f19-289">100</span></span> |<span data-ttu-id="c8f19-290">100</span><span class="sxs-lookup"><span data-stu-id="c8f19-290">100</span></span> |
| <span data-ttu-id="c8f19-291">Wybierz żywności według producenta</span><span class="sxs-lookup"><span data-stu-id="c8f19-291">Select foods by manufacturer</span></span> |<span data-ttu-id="c8f19-292">25</span><span class="sxs-lookup"><span data-stu-id="c8f19-292">25</span></span> |<span data-ttu-id="c8f19-293">175</span><span class="sxs-lookup"><span data-stu-id="c8f19-293">175</span></span> |
| <span data-ttu-id="c8f19-294">Wybierz grupy żywności</span><span class="sxs-lookup"><span data-stu-id="c8f19-294">Select by food group</span></span> |<span data-ttu-id="c8f19-295">10</span><span class="sxs-lookup"><span data-stu-id="c8f19-295">10</span></span> |<span data-ttu-id="c8f19-296">700</span><span class="sxs-lookup"><span data-stu-id="c8f19-296">700</span></span> |
| <span data-ttu-id="c8f19-297">Wybierz 10 pierwszych</span><span class="sxs-lookup"><span data-stu-id="c8f19-297">Select top 10</span></span> |<span data-ttu-id="c8f19-298">15</span><span class="sxs-lookup"><span data-stu-id="c8f19-298">15</span></span> |<span data-ttu-id="c8f19-299">Łącznie 150</span><span class="sxs-lookup"><span data-stu-id="c8f19-299">150 Total</span></span> |

<span data-ttu-id="c8f19-300">W takim przypadku oczekujemy wymaganie średniej przepływności 1,275 RU/s.</span><span class="sxs-lookup"><span data-stu-id="c8f19-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="c8f19-301">Zaokrąglenie do najbliższej 100, firma Microsoft może udostępnić 1300 RU/s dla kolekcji tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8f19-301">Rounding up to the nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="c8f19-302"><a id="RequestRateTooLarge"></a>Przekraczanie limitów zarezerwowaną przepływnością w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="c8f19-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="c8f19-303">Odwołaj, że zużycie jednostka żądania jest oceniana jako szybkość na sekundę, jeśli budżetu jest pusta.</span><span class="sxs-lookup"><span data-stu-id="c8f19-303">Recall that request unit consumption is evaluated as a rate per second if the budget is empty.</span></span> <span data-ttu-id="c8f19-304">Dla aplikacji, które przekroczyć współczynnika jednostki żądania elastycznie kontenera żądań do tej kolekcji zostanie ograniczony, dopóki częstotliwość spadnie poniżej poziomu zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="c8f19-304">For applications that exceed the provisioned request unit rate for a container, requests to that collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="c8f19-305">W przypadku przepustnicy serwer będzie preemptively zakończyć żądania z RequestRateTooLargeException (kod stanu HTTP 429) i powrócić nagłówka x-ms ponawiania — po ms wskazująca czas (w milisekundach), które użytkownik musi czekać przed ponowną próbą wykonania żądanie.</span><span class="sxs-lookup"><span data-stu-id="c8f19-305">When a throttle occurs, the server will preemptively end the request with RequestRateTooLargeException (HTTP status code 429) and return the x-ms-retry-after-ms header indicating the amount of time, in milliseconds, that the user must wait before reattempting the request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="c8f19-306">Jeśli używasz zestawu SDK klienta usługi .NET i LINQ zapytania, a następnie w większości przypadków, nie trzeba uwzględniać tego wyjątku, zgodnie z bieżącą wersją programu .NET SDK klienta niejawnie przechwytuje tej odpowiedzi szanuje określony serwer ponownych prób po nagłówka i ponawia żądanie.</span><span class="sxs-lookup"><span data-stu-id="c8f19-306">If you are using the .NET Client SDK and LINQ queries, then most of the time you never have to deal with this exception, as the current version of the .NET Client SDK implicitly catches this response, respects the server-specified retry-after header, and retries the request.</span></span> <span data-ttu-id="c8f19-307">Następna ponowna próba powiedzie się, chyba że Twoje konto jest uzyskiwany jednocześnie przez wielu klientów.</span><span class="sxs-lookup"><span data-stu-id="c8f19-307">Unless your account is being accessed concurrently by multiple clients, the next retry will succeed.</span></span>

<span data-ttu-id="c8f19-308">Jeśli masz więcej niż jednego klienta zbiorczo operacyjnego powyżej liczby żądań domyślne zachowanie ponownych prób nie mogą być niewystarczające, a klient zgłosi DocumentClientException z kodem stanu 429 do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8f19-308">If you have more than one client cumulatively operating above the request rate, the default retry behavior may not suffice, and the client will throw a DocumentClientException with status code 429 to the application.</span></span> <span data-ttu-id="c8f19-309">W przypadkach, takich jak ta można rozważyć Obsługa zachowanie ponownych prób i logikę w aplikacji Błąd procedury obsługi lub zwiększenie zarezerwowaną przepływnością kontenera.</span><span class="sxs-lookup"><span data-stu-id="c8f19-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing the reserved throughput for the container.</span></span>

## <span data-ttu-id="c8f19-310"><a id="RequestRateTooLargeAPIforMongoDB"></a>Przekraczanie limitów zarezerwowaną przepływnością w interfejsie API, bazy danych mongodb</span><span class="sxs-lookup"><span data-stu-id="c8f19-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="c8f19-311">Aplikacje, które przekraczają żądania elastycznie jednostki dla kolekcji będzie ograniczony, dopóki częstotliwość spadnie poniżej poziomu zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="c8f19-311">Applications that exceed the provisioned request units for a collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="c8f19-312">W przypadku przepustnicy wewnętrznej bazy danych preemptively zakończy się żądanie z *16500* kod błędu: - *zbyt wiele żądań*.</span><span class="sxs-lookup"><span data-stu-id="c8f19-312">When a throttle occurs, the backend will preemptively end the request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="c8f19-313">Domyślnie interfejsu API dla bazy danych MongoDB automatycznie ponowi próbę maksymalnie 10 razy przed zwróceniem *zbyt wiele żądań* kod błędu.</span><span class="sxs-lookup"><span data-stu-id="c8f19-313">By default, API for MongoDB will automatically retry up to 10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="c8f19-314">W przypadku otrzymania wiele *zbyt wiele żądań* kody błędów, można rozważyć albo dodanie zachowanie ponownych prób w aplikacji Błąd procedury obsługi lub [zwiększenie zarezerwowaną przepływnością dla kolekcji](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="c8f19-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing the reserved throughput for the collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8f19-315">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c8f19-315">Next steps</span></span>
<span data-ttu-id="c8f19-316">Aby dowiedzieć się więcej na temat zarezerwowaną przepływnością z bazami danych bazy danych Azure rozwiązania Cosmos, zapoznaj się z tymi zasobami:</span><span class="sxs-lookup"><span data-stu-id="c8f19-316">To learn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="c8f19-317">Cennik platformy Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="c8f19-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="c8f19-318">Partycjonowanie danych w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="c8f19-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="c8f19-319">Aby dowiedzieć się więcej na temat bazy danych rozwiązania Cosmos Azure, zobacz Azure DB rozwiązania Cosmos [dokumentacji](https://azure.microsoft.com/documentation/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="c8f19-319">To learn more about Azure Cosmos DB, see the Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="c8f19-320">Aby rozpocząć testowanie z bazy danych Azure rozwiązania Cosmos wydajności i skalowania, zobacz [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="c8f19-320">To get started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
