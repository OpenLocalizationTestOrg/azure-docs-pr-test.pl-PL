---
title: "aaaRequest jednostki i planowania przepływności - DB rozwiązania Cosmos Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie toounderstand, określ i oszacować wymagania dotyczące jednostki żądania w usłudze Azure DB rozwiązania Cosmos."
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
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="1980c-103">Żądanie jednostki w Azure rozwiązania Cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="1980c-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="1980c-104">Teraz dostępne: Azure DB rozwiązania Cosmos [Kalkulator jednostki żądania](https://www.documentdb.com/capacityplanner).</span><span class="sxs-lookup"><span data-stu-id="1980c-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="1980c-105">Dowiedz się więcej w [Szacowanie przepustowość sieci musi](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="1980c-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Kalkulator przepływności][5]

## <a name="introduction"></a><span data-ttu-id="1980c-107">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="1980c-107">Introduction</span></span>
<span data-ttu-id="1980c-108">[Azure DB rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) jest globalnie rozproszone wielu modelu bazy danych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1980c-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="1980c-109">Z bazy danych rozwiązania Cosmos platformy Azure nie toorent z maszyn wirtualnych, wdrażania oprogramowania lub monitora bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1980c-109">With Azure Cosmos DB, you don't have toorent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="1980c-110">Azure DB rozwiązania Cosmos jest obsługiwane i stale monitorowane przez program Microsoft inżynierów najwyższego toodeliver światowej klasy dostępności, wydajności i danych ochrony.</span><span class="sxs-lookup"><span data-stu-id="1980c-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers toodeliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="1980c-111">Są dostępne dane przy użyciu interfejsów API wybranych jako [SQL usługi DocumentDB](documentdb-sql-query.md) (dokument) bazy danych MongoDB (dokument), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (klucz wartość) i [Gremlin](https://tinkerpop.apache.org/gremlin.html) (wykres) znajdują się w obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="1980c-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="1980c-112">Waluta Hello Azure DB rozwiązania Cosmos jest hello jednostek żądań (RU).</span><span class="sxs-lookup"><span data-stu-id="1980c-112">hello currency of Azure Cosmos DB is hello Request Unit (RU).</span></span> <span data-ttu-id="1980c-113">RUs nie wymaga możliwości odczytu/zapisu tooreserve lub udostępnić Procesora, pamięci i IOPS.</span><span class="sxs-lookup"><span data-stu-id="1980c-113">With RUs, you do not need tooreserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="1980c-114">Azure DB rozwiązania Cosmos obsługuje kilka interfejsów API z różnych operacji — od prostych odczytuje i zapisuje toocomplex zapytania wykresu.</span><span class="sxs-lookup"><span data-stu-id="1980c-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes toocomplex graph queries.</span></span> <span data-ttu-id="1980c-115">Ponieważ nie wszystkie żądania są takie same, są przypisane znormalizowane ilość **jednostek żądania** na podstawie kwoty hello obliczenia wymagane tooserve hello żądania.</span><span class="sxs-lookup"><span data-stu-id="1980c-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on hello amount of computation required tooserve hello request.</span></span> <span data-ttu-id="1980c-116">Liczba Hello jednostek żądania dla operacji jest deterministyczna, a można śledzić hello liczby jednostek żądania używane przez żadnych operacji w usłudze Azure DB rozwiązania Cosmos za pośrednictwem nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1980c-116">hello number of request units for an operation is deterministic, and you can track hello number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="1980c-117">tooprovide przewidywalną wydajność, należy tooreserve przepływności w jednostkach 100 RU/sekundę.</span><span class="sxs-lookup"><span data-stu-id="1980c-117">tooprovide predictable performance, you need tooreserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="1980c-118">Po przeczytaniu tego artykułu, będziesz w stanie tooanswer hello następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="1980c-118">After reading this article, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="1980c-119">Co to są jednostek żądania i żądania opłat?</span><span class="sxs-lookup"><span data-stu-id="1980c-119">What are request units and request charges?</span></span>
* <span data-ttu-id="1980c-120">Jak określić żądanie pojemność jednostki dla kolekcji?</span><span class="sxs-lookup"><span data-stu-id="1980c-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="1980c-121">Jak oszacować musi jednostki żądania Moja aplikacja</span><span class="sxs-lookup"><span data-stu-id="1980c-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="1980c-122">Co się stanie, jeśli I przekracza pojemność jednostki żądania dla kolekcji?</span><span class="sxs-lookup"><span data-stu-id="1980c-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="1980c-123">Bazy danych Azure rozwiązania Cosmos jest wiele modeli bazy danych, jest ważne toonote, że dokument interfejsu API, wykres/węzła Graph API i tabeli na jednostkę tabeli interfejsu API odnoszą się tooa kolekcji lub dokumentu.</span><span class="sxs-lookup"><span data-stu-id="1980c-123">As Azure Cosmos DB is a multi-model database, it is important toonote that we will refer tooa collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="1980c-124">Przepływność tego dokumentu, firma Microsoft będzie generalize pojęcia toohello kontenera/elementu.</span><span class="sxs-lookup"><span data-stu-id="1980c-124">Throughput this document we will generalize toohello concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="1980c-125">Jednostek żądania i żądania opłat</span><span class="sxs-lookup"><span data-stu-id="1980c-125">Request units and request charges</span></span>
<span data-ttu-id="1980c-126">Azure DB rozwiązania Cosmos zapewnia szybkie, przewidywalną wydajność przez *rezerwowania* musi przepływność aplikacji toosatisfy zasobów.</span><span class="sxs-lookup"><span data-stu-id="1980c-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources toosatisfy your application's throughput needs.</span></span>  <span data-ttu-id="1980c-127">Ponieważ aplikacji obciążenia oraz dostęp wzorce zmian w czasie, bazy danych Azure rozwiązania Cosmos pozwala zwiększyć tooeasily lub zmniejszyć ilość hello zarezerwowaną przepływnością tooyour dostępnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1980c-127">Because application load and access patterns change over time, Azure Cosmos DB allows you tooeasily increase or decrease hello amount of reserved throughput available tooyour application.</span></span>

<span data-ttu-id="1980c-128">Z bazy danych Azure rozwiązania Cosmos zarezerwowaną przepływnością jest określane w przeliczeniu na jednostki żądania przetwarzania na sekundę.</span><span class="sxs-lookup"><span data-stu-id="1980c-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="1980c-129">Można potraktować jednostki żądania jako walutę przepływności, zgodnie z którymi możesz *zarezerwować* ilość gwarantowane jednostki żądania tooyour dostępnych aplikacji na podstawie sekundowym.</span><span class="sxs-lookup"><span data-stu-id="1980c-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available tooyour application on per second basis.</span></span>  <span data-ttu-id="1980c-130">Każdej operacji w usłudze Azure DB rozwiązania Cosmos — zapisywanie dokumentu, wykonywania zapytania, aktualizowanie dokumentu — korzysta z Procesora, pamięci i IOPS.</span><span class="sxs-lookup"><span data-stu-id="1980c-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="1980c-131">Oznacza to, że każda operacja wiąże się z *żądań bezpłatnie*, który jest wyrażona w *jednostek żądania*.</span><span class="sxs-lookup"><span data-stu-id="1980c-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="1980c-132">Opis czynników hello, to wpływ na koszty jednostki żądania, oraz wymagania dotyczące przepływności aplikacji, umożliwia toorun możesz aplikacji jako koszt skutecznie, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="1980c-132">Understanding hello factors which impact request unit charges, along with your application's throughput requirements, enables you toorun your application as cost effectively as possible.</span></span> <span data-ttu-id="1980c-133">Eksplorator zapytań Hello jest również podstawowa cudowne narzędzie tootest hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="1980c-133">hello query explorer is also a wonderful tool tootest hello core of a query.</span></span>

<span data-ttu-id="1980c-134">Zalecamy rozpoczęcie pracy od obejrzenia powitania po wideo, w którym Aravind Ramachandran wyjaśniono jednostek żądania i przewidywalną wydajność bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="1980c-134">We recommend getting started by watching hello following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="1980c-135">Określanie pojemność jednostki żądania w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="1980c-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="1980c-136">Przy uruchamianiu nową kolekcję, tabeli lub wykres, określ numer hello jednostek żądań na sekundę (RU na sekundę) mają zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="1980c-136">When starting a new collection, table or graph, you specify hello number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="1980c-137">Oparte na powitania udostępnionej przepływności, bazy danych rozwiązania Cosmos Azure przydziela toohost partycji fizycznej kolekcji i podziałów/rebalances danych na partycji jako ich przyrostu.</span><span class="sxs-lookup"><span data-stu-id="1980c-137">Based on hello provisioned throughput, Azure Cosmos DB allocates physical partitions toohost your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="1980c-138">Azure DB rozwiązania Cosmos wymaga toobe klucza partycji określone, gdy kolekcja jest inicjowana z 2500 jednostek żądania lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1980c-138">Azure Cosmos DB requires a partition key toobe specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="1980c-139">Klucz partycji jest również wymagany tooscale przepływność kolekcji poza 2500 jednostki żądania w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="1980c-139">A partition key is also required tooscale your collection's throughput beyond 2,500 request units in hello future.</span></span> <span data-ttu-id="1980c-140">W związku z tym zdecydowanie zaleca się tooconfigure [klucza partycji](partition-data.md) podczas tworzenia kontenera niezależnie od programu początkowej przepływności.</span><span class="sxs-lookup"><span data-stu-id="1980c-140">Therefore, it is highly recommended tooconfigure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="1980c-141">Ponieważ dane mogą mieć toobe podzielić na wiele partycji, jest konieczne toopick klucza partycji, który ma dużej kardynalności (100 toomillions unikatowe wartości), dzięki czemu żądania i kolekcji/tabeli/graph mogą być skalowane jednolicie Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="1980c-141">Since your data might have toobe split across multiple partitions, it is necessary toopick a partition key that has a high cardinality (100 toomillions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="1980c-142">Klucz partycji to logiczne granic, a nie jeden fizyczny.</span><span class="sxs-lookup"><span data-stu-id="1980c-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="1980c-143">W związku z tym nie trzeba toolimit hello liczba wartości kluczy partycji distinct.</span><span class="sxs-lookup"><span data-stu-id="1980c-143">Therefore, you do not need toolimit hello number of distinct partition key values.</span></span> <span data-ttu-id="1980c-144">W rzeczywistości jest znacznie lepszą toohave partycji wartości klucza niż mniej, jako bazy danych rozwiązania Cosmos Azure ma więcej opcje równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="1980c-144">It is in fact better toohave more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="1980c-145">Oto fragment kodu dotyczący tworzenia kolekcji z 3000 żądania jednostek na drugi przy użyciu hello zestawu .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="1980c-145">Here is a code snippet for creating a collection with 3,000 request units per second using hello .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="1980c-146">Azure DB rozwiązania Cosmos działa modelu rezerwacji przepływności.</span><span class="sxs-lookup"><span data-stu-id="1980c-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="1980c-147">Oznacza to, że są rozliczane hello ilość przepustowości *zastrzeżone*, niezależnie od tego, jaka część tego przepływności jest aktywnie *używane*.</span><span class="sxs-lookup"><span data-stu-id="1980c-147">That is, you are billed for hello amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="1980c-148">Jako aplikacji obciążenia, danych i stosowania wzorców zmiany możesz łatwo skalować w górę i w dół hello ilość zastrzeżone RUs za pomocą zestawów SDK lub przy użyciu hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1980c-148">As your application's load, data, and usage patterns change you can easily scale up and down hello amount of reserved RUs through SDKs or using hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="1980c-149">Każda kolekcja/tabeli/wykresu są mapowane tooan `Offer` zasobów w usłudze Azure DB rozwiązania Cosmos mającej metadane dotyczące hello udostępnionej przepływności.</span><span class="sxs-lookup"><span data-stu-id="1980c-149">Each collection/table/graph are mapped tooan `Offer` resource in Azure Cosmos DB, which has metadata about hello provisioned throughput.</span></span> <span data-ttu-id="1980c-150">Możesz zmienić przepływności hello przydzielone wyszukiwania hello odpowiadający jej zasób oferta dla kontenera, a następnie Uaktualnianie hello nową wartość przepływności.</span><span class="sxs-lookup"><span data-stu-id="1980c-150">You can change hello allocated throughput by looking up hello corresponding offer resource for a container, then updating it with hello new throughput value.</span></span> <span data-ttu-id="1980c-151">Oto fragment kodu do zmiany hello przepływność too5 kolekcji, 000 jednostek żądań na drugi przy użyciu hello zestawu .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="1980c-151">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second using hello .NET SDK:</span></span>

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="1980c-152">Jeśli zmienisz przepływności hello jest wpływ dostępności toohello Twojego kontenera.</span><span class="sxs-lookup"><span data-stu-id="1980c-152">There is no impact toohello availability of your container when you change hello throughput.</span></span> <span data-ttu-id="1980c-153">Zazwyczaj nowe zarezerwowaną przepływnością hello obowiązuje w ciągu kilku sekund na aplikacji hello przepływności nowe.</span><span class="sxs-lookup"><span data-stu-id="1980c-153">Typically hello new reserved throughput is effective within seconds on application of hello new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="1980c-154">Zagadnienia dotyczące jednostki żądania</span><span class="sxs-lookup"><span data-stu-id="1980c-154">Request unit considerations</span></span>
<span data-ttu-id="1980c-155">Podczas oceny hello liczba tooreserve jednostki żądania dla Twojej bazy danych Azure rozwiązania Cosmos kontenera, jest ważne tootake hello następujące zmienne pod uwagę:</span><span class="sxs-lookup"><span data-stu-id="1980c-155">When estimating hello number of request units tooreserve for your Azure Cosmos DB container, it is important tootake hello following variables into consideration:</span></span>

* <span data-ttu-id="1980c-156">**Rozmiar elementu**.</span><span class="sxs-lookup"><span data-stu-id="1980c-156">**Item size**.</span></span> <span data-ttu-id="1980c-157">Rozmiar zwiększa tooread jednostki używane hello lub zwiększa zapis hello danych.</span><span class="sxs-lookup"><span data-stu-id="1980c-157">As size increases hello units consumed tooread or write hello data will also increase.</span></span>
* <span data-ttu-id="1980c-158">**Liczba właściwości elementu**.</span><span class="sxs-lookup"><span data-stu-id="1980c-158">**Item property count**.</span></span> <span data-ttu-id="1980c-159">Zakładając, że domyślna indeksowania wszystkich właściwości, hello toowrite zużywanych jednostek, które dokumentu/węzła/ntity zwiększa się wraz ze wzrostem liczby właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="1980c-159">Assuming default indexing of all properties, hello units consumed toowrite a document/node/ntity will increase as hello property count increases.</span></span>
* <span data-ttu-id="1980c-160">**Spójność danych**.</span><span class="sxs-lookup"><span data-stu-id="1980c-160">**Data consistency**.</span></span> <span data-ttu-id="1980c-161">Po za pomocą poziomów spójności danych silne lub ograniczonych nieaktualności, dodatkowych jednostek będzie wykorzystanych tooread elementów.</span><span class="sxs-lookup"><span data-stu-id="1980c-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed tooread items.</span></span>
* <span data-ttu-id="1980c-162">**Właściwości indeksowanych**.</span><span class="sxs-lookup"><span data-stu-id="1980c-162">**Indexed properties**.</span></span> <span data-ttu-id="1980c-163">Zasady indeksu na każdego kontenera określa właściwości, które są indeksowane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="1980c-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="1980c-164">Można ograniczyć zużycie jednostki Twoje żądanie, przez ograniczanie liczby hello właściwości indeksowanych lub włączenie indeksowanie z opóźnieniem.</span><span class="sxs-lookup"><span data-stu-id="1980c-164">You can reduce your request unit consumption by limiting hello number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="1980c-165">**Indeksowanie dokumentów**.</span><span class="sxs-lookup"><span data-stu-id="1980c-165">**Document indexing**.</span></span> <span data-ttu-id="1980c-166">Domyślnie każdy element jest indeksowany automatycznie będą korzystać mniejszej liczby jednostek żądania, jeśli wybierzesz nie tooindex niektórych elementów.</span><span class="sxs-lookup"><span data-stu-id="1980c-166">By default each item is automatically indexed, you will consume fewer request units if you choose not tooindex some of your items.</span></span>
* <span data-ttu-id="1980c-167">**Zapytanie wzorce**.</span><span class="sxs-lookup"><span data-stu-id="1980c-167">**Query patterns**.</span></span> <span data-ttu-id="1980c-168">złożoność Hello zapytania ma wpływ na liczbę jednostek żądania są używane dla operacji.</span><span class="sxs-lookup"><span data-stu-id="1980c-168">hello complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="1980c-169">Hello liczba predykatów, rodzaj predykaty hello, projekcje, liczba funkcji UDF i hello rozmiaru zestawu danych źródła hello wszystkie wpływ koszt hello zapytania operacji.</span><span class="sxs-lookup"><span data-stu-id="1980c-169">hello number of predicates, nature of hello predicates, projections, number of UDFs, and hello size of hello source data set all influence hello cost of query operations.</span></span>
* <span data-ttu-id="1980c-170">**Użycie skryptu**.</span><span class="sxs-lookup"><span data-stu-id="1980c-170">**Script usage**.</span></span>  <span data-ttu-id="1980c-171">Podobnie jak w przypadku zapytań, procedury składowane i wyzwalaczy wykorzystywać oparte na powitania złożoność operacjom hello jednostki żądania.</span><span class="sxs-lookup"><span data-stu-id="1980c-171">As with queries, stored procedures and triggers consume request units based on hello complexity of hello operations being performed.</span></span> <span data-ttu-id="1980c-172">Podczas opracowywania aplikacji hello żądań bezpłatnie sprawdzić toobetter nagłówka zrozumieć, jak każdej operacji zajmuje pojemność jednostki żądania.</span><span class="sxs-lookup"><span data-stu-id="1980c-172">As you develop your application, inspect hello request charge header toobetter understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="1980c-173">Planowania potrzeb w zakresie przepustowości</span><span class="sxs-lookup"><span data-stu-id="1980c-173">Estimating throughput needs</span></span>
<span data-ttu-id="1980c-174">Jednostka żądania jest znormalizowane miara kosztu przetwarzania żądania.</span><span class="sxs-lookup"><span data-stu-id="1980c-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="1980c-175">Jednostka pojedyncze żądanie reprezentuje tooread wymaganą wydajność przetwarzania hello (za pośrednictwem łączy własnych lub identyfikator) pojedynczego 1KB elementu składające się z 10 unikatowe wartości (z wyjątkiem właściwości systemu).</span><span class="sxs-lookup"><span data-stu-id="1980c-175">A single request unit represents hello processing capacity required tooread (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="1980c-176">Żądanie toocreate (Wstaw), Zamień lub usuń hello sam element zajmie więcej przetwarzania z usługi hello i tym samym więcej jednostek żądania.</span><span class="sxs-lookup"><span data-stu-id="1980c-176">A request toocreate (insert), replace or delete hello same item will consume more processing from hello service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="1980c-177">linii bazowej Hello jednostki 1 żądanie dla 1KB elementu odpowiada tooa proste UZYSKAĆ łącze własne lub identyfikator elementu hello.</span><span class="sxs-lookup"><span data-stu-id="1980c-177">hello baseline of 1 request unit for a 1KB item corresponds tooa simple GET by self link or id of hello item.</span></span>
> 
> 

<span data-ttu-id="1980c-178">Na przykład, w tym miejscu jest tabelę, która pokazuje, ile żądań tooprovision jednostki na trzy rozmiary innego elementu (1KB, 4KB do 64KB) i na dwa różne poziomy wydajności (odczyty 500 na sekundę 100 zapisy na sekundę i 500 odczyty/sekundę + 500 zapisy na sekundę).</span><span class="sxs-lookup"><span data-stu-id="1980c-178">For example, here's a table that shows how many request units tooprovision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="1980c-179">spójność danych Hello został skonfigurowany na sesji i hello indeksowania zasad ustawiono tooNone.</span><span class="sxs-lookup"><span data-stu-id="1980c-179">hello data consistency was configured at Session, and hello indexing policy was set tooNone.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="1980c-180"><strong>Rozmiar elementu</strong></span><span class="sxs-lookup"><span data-stu-id="1980c-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-181"><strong>Odczyty/sekundę</strong></span><span class="sxs-lookup"><span data-stu-id="1980c-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-182"><strong>Zapisy na sekundę</strong></span><span class="sxs-lookup"><span data-stu-id="1980c-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-183"><strong>Jednostki żądania</strong></span><span class="sxs-lookup"><span data-stu-id="1980c-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="1980c-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="1980c-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-185">500</span><span class="sxs-lookup"><span data-stu-id="1980c-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-186">100</span><span class="sxs-lookup"><span data-stu-id="1980c-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-187">(500 * 1) + (100 * 5) = 1 000 RU/s</span><span class="sxs-lookup"><span data-stu-id="1980c-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="1980c-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="1980c-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-189">500</span><span class="sxs-lookup"><span data-stu-id="1980c-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-190">500</span><span class="sxs-lookup"><span data-stu-id="1980c-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-191">(500 * 1) + (500 * 5) = 3 000 RU/s</span><span class="sxs-lookup"><span data-stu-id="1980c-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="1980c-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="1980c-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-193">500</span><span class="sxs-lookup"><span data-stu-id="1980c-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-194">100</span><span class="sxs-lookup"><span data-stu-id="1980c-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-195">(500 * 1,3) + (100 * 7) = 1,350 RU/s</span><span class="sxs-lookup"><span data-stu-id="1980c-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="1980c-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="1980c-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-197">500</span><span class="sxs-lookup"><span data-stu-id="1980c-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-198">500</span><span class="sxs-lookup"><span data-stu-id="1980c-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-199">(500 * 1,3) + (500 * 7) = 4,150 RU/s</span><span class="sxs-lookup"><span data-stu-id="1980c-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="1980c-200">64 KB</span><span class="sxs-lookup"><span data-stu-id="1980c-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-201">500</span><span class="sxs-lookup"><span data-stu-id="1980c-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-202">100</span><span class="sxs-lookup"><span data-stu-id="1980c-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span><span class="sxs-lookup"><span data-stu-id="1980c-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="1980c-204">64 KB</span><span class="sxs-lookup"><span data-stu-id="1980c-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-205">500</span><span class="sxs-lookup"><span data-stu-id="1980c-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-206">500</span><span class="sxs-lookup"><span data-stu-id="1980c-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="1980c-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span><span class="sxs-lookup"><span data-stu-id="1980c-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a><span data-ttu-id="1980c-208">Użycie kalkulatora jednostki żądania hello</span><span class="sxs-lookup"><span data-stu-id="1980c-208">Use hello request unit calculator</span></span>
<span data-ttu-id="1980c-209">Klienci toohelp poprawnie dostroić ich ocen przepływności, jest opartego na sieci web [Kalkulator jednostki żądania](https://www.documentdb.com/capacityplanner) wymagań hello szacowania toohelp jednostki żądania dla operacji typowych, w tym:</span><span class="sxs-lookup"><span data-stu-id="1980c-209">toohelp customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) toohelp estimate hello request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="1980c-210">Element tworzy (zapisy)</span><span class="sxs-lookup"><span data-stu-id="1980c-210">Item creates (writes)</span></span>
* <span data-ttu-id="1980c-211">Odczytuje element</span><span class="sxs-lookup"><span data-stu-id="1980c-211">Item reads</span></span>
* <span data-ttu-id="1980c-212">Usuwa element</span><span class="sxs-lookup"><span data-stu-id="1980c-212">Item deletes</span></span>
* <span data-ttu-id="1980c-213">Element aktualizacji</span><span class="sxs-lookup"><span data-stu-id="1980c-213">Item updates</span></span>

<span data-ttu-id="1980c-214">Narzędzie Hello obejmuje również obsługę Szacowanie oparte na powitania przykładowych elementów podane wymagania dotyczące przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="1980c-214">hello tool also includes support for estimating data storage needs based on hello sample items you provide.</span></span>

<span data-ttu-id="1980c-215">Za pomocą narzędzia hello jest prosty:</span><span class="sxs-lookup"><span data-stu-id="1980c-215">Using hello tool is simple:</span></span>

1. <span data-ttu-id="1980c-216">Należy przekazać co najmniej jeden element reprezentatywny.</span><span class="sxs-lookup"><span data-stu-id="1980c-216">Upload one or more representative items.</span></span>
   
    ![Przekaż Kalkulator jednostki żądania toohello elementów][2]
2. <span data-ttu-id="1980c-218">wymagania dotyczące magazynu danych tooestimate, wprowadź hello łączna liczba elementów spodziewasz się toostore.</span><span class="sxs-lookup"><span data-stu-id="1980c-218">tooestimate data storage requirements, enter hello total number of items you expect toostore.</span></span>
3. <span data-ttu-id="1980c-219">Wprowadź hello liczba elementów tworzenia, odczytu, aktualizacji i usuwania działań, które wymagają (na podstawie na sekundę).</span><span class="sxs-lookup"><span data-stu-id="1980c-219">Enter hello number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="1980c-220">opłaty za jednostki żądania hello tooestimate elementu operacji aktualizacji, Przekaż kopię hello próbka z kroku 1 zawiera pole typowe aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="1980c-220">tooestimate hello request unit charges of item update operations, upload a copy of hello sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="1980c-221">Na przykład jeśli element aktualizacje zwykle zmodyfikować dwie właściwości o nazwie lastLogin i userVisits, a następnie po prostu skopiuj element przykładowych hello, zaktualizuj hello wartości tych dwóch właściwości i przekaż hello skopiowany element.</span><span class="sxs-lookup"><span data-stu-id="1980c-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy hello sample item, update hello values for those two properties, and upload hello copied item.</span></span>
   
    ![Wprowadź wymagania dotyczące przepływności w Kalkulator jednostki żądania hello][3]
4. <span data-ttu-id="1980c-223">Kliknij przycisk Oblicz i wyniki hello sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="1980c-223">Click calculate and examine hello results.</span></span>
   
    ![Wyniki Kalkulator jednostki żądania][4]

> [!NOTE]
> <span data-ttu-id="1980c-225">Jeśli masz typów elementów, które różnią się znacznie pod względem rozmiaru i hello liczbę właściwości indeksowanych, Przekaż przykładowe każdego *typu* z toohello elementu typowe narzędzia, a następnie obliczyć hello wyników.</span><span class="sxs-lookup"><span data-stu-id="1980c-225">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then upload a sample of each *type* of typical item toohello tool and then calculate hello results.</span></span>
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="1980c-226">Użyj nagłówka odpowiedzi opłat hello Azure DB rozwiązania Cosmos żądania</span><span class="sxs-lookup"><span data-stu-id="1980c-226">Use hello Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="1980c-227">Każdy odpowiedź z hello Azure DB rozwiązania Cosmos usługi zawiera niestandardowy nagłówek (`x-ms-request-charge`) zawiera jednostki żądania hello używane dla hello żądania.</span><span class="sxs-lookup"><span data-stu-id="1980c-227">Every response from hello Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains hello request units consumed for hello request.</span></span> <span data-ttu-id="1980c-228">Ten nagłówek jest również dostępny za pośrednictwem hello Azure rozwiązania Cosmos DB SDK.</span><span class="sxs-lookup"><span data-stu-id="1980c-228">This header is also accessible through hello Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="1980c-229">W hello zestawu .NET SDK RequestCharge jest właściwością obiektu ResourceResponse hello.</span><span class="sxs-lookup"><span data-stu-id="1980c-229">In hello .NET SDK, RequestCharge is a property of hello ResourceResponse object.</span></span>  <span data-ttu-id="1980c-230">Dla zapytań hello Eksploratora zapytań DB rozwiązania Cosmos Azure w portalu Azure hello informacje żądania opłaty dotyczące wykonywane zapytania.</span><span class="sxs-lookup"><span data-stu-id="1980c-230">For queries, hello Azure Cosmos DB Query Explorer in hello Azure portal provides request charge information for executed queries.</span></span>

![Badanie RU opłat w hello Eksploratora zapytań][1]

<span data-ttu-id="1980c-232">Pamiętając o tym, jedną z metod szacowania hello ilość zarezerwowaną przepływnością wymagane przez aplikację jest toorecord hello żądania jednostki opłat związanych z prowadzeniem typowymi operacjami względem elementu reprezentatywny używanych przez aplikację, a następnie Szacowanie hello liczba operacji przewidywania wykonywania każdej sekundy.</span><span class="sxs-lookup"><span data-stu-id="1980c-232">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="1980c-233">Można się toomeasure i obejmują typowe zapytania i również użycie skryptu bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="1980c-233">Be sure toomeasure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="1980c-234">Jeśli masz typów elementów, które różnią się znacznie pod względem rozmiaru i hello liczbę właściwości indeksowanych rejestrowania hello odpowiednich operacji żądania jednostki opłat związanych z każdym *typu* typowe elementu.</span><span class="sxs-lookup"><span data-stu-id="1980c-234">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="1980c-235">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1980c-235">For example:</span></span>

1. <span data-ttu-id="1980c-236">Zarejestruj hello żądania jednostkę opłatą tworzenia (Wstawianie) typowe elementu.</span><span class="sxs-lookup"><span data-stu-id="1980c-236">Record hello request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="1980c-237">Opłata jednostki żądania rekordów hello odczytywania typowe elementu.</span><span class="sxs-lookup"><span data-stu-id="1980c-237">Record hello request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="1980c-238">Opłata jednostki żądania rekordów hello aktualizowania typowych elementu.</span><span class="sxs-lookup"><span data-stu-id="1980c-238">Record hello request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="1980c-239">Opłata jednostki żądania hello rekordów zapytań typowe, wspólnego elementu.</span><span class="sxs-lookup"><span data-stu-id="1980c-239">Record hello request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="1980c-240">Witaj rekordów żądania jednostki opłat skrypty niestandardowe (procedury składowane, wyzwalacze, funkcje zdefiniowane przez użytkownika) wykorzystywane przez aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="1980c-240">Record hello request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by hello application</span></span>
6. <span data-ttu-id="1980c-241">Oblicz hello żądania wymaganych jednostek podanych hello szacowana liczba operacji przewidujesz toorun każdej sekundy.</span><span class="sxs-lookup"><span data-stu-id="1980c-241">Calculate hello required request units given hello estimated number of operations you anticipate toorun each second.</span></span>

### <span data-ttu-id="1980c-242"><a id="GetLastRequestStatistics"></a>Za pomocą interfejsu API dla bazy danych MongoDB w GetLastRequestStatistics polecenia</span><span class="sxs-lookup"><span data-stu-id="1980c-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="1980c-243">Interfejs API bazy danych mongodb obsługuje polecenia niestandardowych, *getLastRequestStatistics*, pobierania hello opłat żądania dla określonej operacji.</span><span class="sxs-lookup"><span data-stu-id="1980c-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving hello request charge for specified operations.</span></span>

<span data-ttu-id="1980c-244">Na przykład w hello powłokę Mongo, wykonaj operację hello, którą chcesz tooverify hello żądania opłata za.</span><span class="sxs-lookup"><span data-stu-id="1980c-244">For example, in hello Mongo Shell, execute hello operation you want tooverify hello request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="1980c-245">Następnie wykonaj polecenie hello *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="1980c-245">Next, execute hello command *getLastRequestStatistics*.</span></span>
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

<span data-ttu-id="1980c-246">Pamiętając o tym, jedną z metod szacowania hello ilość zarezerwowaną przepływnością wymagane przez aplikację jest toorecord hello żądania jednostki opłat związanych z prowadzeniem typowymi operacjami względem elementu reprezentatywny używanych przez aplikację, a następnie Szacowanie hello liczba operacji przewidywania wykonywania każdej sekundy.</span><span class="sxs-lookup"><span data-stu-id="1980c-246">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="1980c-247">Jeśli masz typów elementów, które różnią się znacznie pod względem rozmiaru i hello liczbę właściwości indeksowanych rejestrowania hello odpowiednich operacji żądania jednostki opłat związanych z każdym *typu* typowe elementu.</span><span class="sxs-lookup"><span data-stu-id="1980c-247">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="1980c-248">Za pomocą interfejsu API dla bazy danych MongoDB w portalu metryki</span><span class="sxs-lookup"><span data-stu-id="1980c-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="1980c-249">Witaj najprostszym tooget sposób dobrej szacowania jednostki żądania opłaty do interfejsu API dla bazy danych MongoDB jest toouse hello [portalu Azure](https://portal.azure.com) metryki.</span><span class="sxs-lookup"><span data-stu-id="1980c-249">hello simplest way tooget a good estimation of request unit charges for your API for MongoDB database is toouse hello [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="1980c-250">Z hello *liczba żądań* i *opłat żądania* wykresy, można uzyskać oszacowanie liczbę jednostek żądania każdej operacji jest wykorzystywanie i liczbę jednostek żądania zużywają tooone względną innej.</span><span class="sxs-lookup"><span data-stu-id="1980c-250">With hello *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative tooone another.</span></span>

![Interfejs API dla metryki portalu bazy danych MongoDB][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="1980c-252">W przykładzie szacowania jednostki żądania</span><span class="sxs-lookup"><span data-stu-id="1980c-252">A request unit estimation example</span></span>
<span data-ttu-id="1980c-253">Należy wziąć pod uwagę powitania po ~ 1KB dokumentu:</span><span class="sxs-lookup"><span data-stu-id="1980c-253">Consider hello following ~1KB document:</span></span>

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
> <span data-ttu-id="1980c-254">Dokumenty są zminimalizowany w usłudze Azure DB rozwiązania Cosmos, więc hello system obliczeniowe rozmiar dokumentu hello powyżej jest nieco mniej niż 1 KB.</span><span class="sxs-lookup"><span data-stu-id="1980c-254">Documents are minified in Azure Cosmos DB, so hello system calculated size of hello document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="1980c-255">Witaj poniższej tabeli przedstawiono przybliżone żądania jednostki związanych z typowymi operacjami na tym elemencie (opłat jednostki żądania przybliżonej hello zakłada poziomu spójności konta hello ustawiono zbyt "Sesja" i że wszystkie elementy są automatycznie indeksowane):</span><span class="sxs-lookup"><span data-stu-id="1980c-255">hello following table shows approximate request unit charges for typical operations on this item (hello approximate request unit charge assumes that hello account consistency level is set too“Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="1980c-256">Operacja</span><span class="sxs-lookup"><span data-stu-id="1980c-256">Operation</span></span> | <span data-ttu-id="1980c-257">Opłata jednostki żądania</span><span class="sxs-lookup"><span data-stu-id="1980c-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="1980c-258">Utwórz element</span><span class="sxs-lookup"><span data-stu-id="1980c-258">Create item</span></span> |<span data-ttu-id="1980c-259">~ 15 RU</span><span class="sxs-lookup"><span data-stu-id="1980c-259">~15 RU</span></span> |
| <span data-ttu-id="1980c-260">Odczytu elementu</span><span class="sxs-lookup"><span data-stu-id="1980c-260">Read item</span></span> |<span data-ttu-id="1980c-261">~ 1 RU</span><span class="sxs-lookup"><span data-stu-id="1980c-261">~1 RU</span></span> |
| <span data-ttu-id="1980c-262">Element zapytania według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="1980c-262">Query item by id</span></span> |<span data-ttu-id="1980c-263">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="1980c-263">~2.5 RU</span></span> |

<span data-ttu-id="1980c-264">Ponadto w poniższej tabeli zamieszczono przybliżonej żądania jednostki opłat za typowe zapytania używane w aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="1980c-264">Additionally, this table shows approximate request unit charges for typical queries used in hello application:</span></span>

| <span data-ttu-id="1980c-265">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="1980c-265">Query</span></span> | <span data-ttu-id="1980c-266">Opłata jednostki żądania</span><span class="sxs-lookup"><span data-stu-id="1980c-266">Request Unit Charge</span></span> | <span data-ttu-id="1980c-267">Liczba zwróconych elementów</span><span class="sxs-lookup"><span data-stu-id="1980c-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1980c-268">Wybierz żywności według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="1980c-268">Select food by id</span></span> |<span data-ttu-id="1980c-269">~2.5 RU</span><span class="sxs-lookup"><span data-stu-id="1980c-269">~2.5 RU</span></span> |<span data-ttu-id="1980c-270">1</span><span class="sxs-lookup"><span data-stu-id="1980c-270">1</span></span> |
| <span data-ttu-id="1980c-271">Wybierz żywności według producenta</span><span class="sxs-lookup"><span data-stu-id="1980c-271">Select foods by manufacturer</span></span> |<span data-ttu-id="1980c-272">~ 7 RU</span><span class="sxs-lookup"><span data-stu-id="1980c-272">~7 RU</span></span> |<span data-ttu-id="1980c-273">7</span><span class="sxs-lookup"><span data-stu-id="1980c-273">7</span></span> |
| <span data-ttu-id="1980c-274">Wybierz grupy żywności i kolejność według wagi</span><span class="sxs-lookup"><span data-stu-id="1980c-274">Select by food group and order by weight</span></span> |<span data-ttu-id="1980c-275">~ 70 RU</span><span class="sxs-lookup"><span data-stu-id="1980c-275">~70 RU</span></span> |<span data-ttu-id="1980c-276">100</span><span class="sxs-lookup"><span data-stu-id="1980c-276">100</span></span> |
| <span data-ttu-id="1980c-277">Zaznacz górny żywności 10 w grupie żywności</span><span class="sxs-lookup"><span data-stu-id="1980c-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="1980c-278">~ 10 RU</span><span class="sxs-lookup"><span data-stu-id="1980c-278">~10 RU</span></span> |<span data-ttu-id="1980c-279">10</span><span class="sxs-lookup"><span data-stu-id="1980c-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="1980c-280">Opłaty RU różnić w zależności od hello liczbę zwracanych elementów.</span><span class="sxs-lookup"><span data-stu-id="1980c-280">RU charges vary based on hello number of items returned.</span></span>
> 
> 

<span data-ttu-id="1980c-281">Dzięki tym informacjom możemy oszacować hello RU wymagania dla tej aplikacji, podanych hello liczby operacji i zapytań Oczekujemy na sekundę:</span><span class="sxs-lookup"><span data-stu-id="1980c-281">With this information, we can estimate hello RU requirements for this application given hello number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="1980c-282">Operacja/zapytania</span><span class="sxs-lookup"><span data-stu-id="1980c-282">Operation/Query</span></span> | <span data-ttu-id="1980c-283">Szacowaną liczbę na sekundę</span><span class="sxs-lookup"><span data-stu-id="1980c-283">Estimated number per second</span></span> | <span data-ttu-id="1980c-284">Wymagane RUs</span><span class="sxs-lookup"><span data-stu-id="1980c-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1980c-285">Utwórz element</span><span class="sxs-lookup"><span data-stu-id="1980c-285">Create item</span></span> |<span data-ttu-id="1980c-286">10</span><span class="sxs-lookup"><span data-stu-id="1980c-286">10</span></span> |<span data-ttu-id="1980c-287">150</span><span class="sxs-lookup"><span data-stu-id="1980c-287">150</span></span> |
| <span data-ttu-id="1980c-288">Odczytu elementu</span><span class="sxs-lookup"><span data-stu-id="1980c-288">Read item</span></span> |<span data-ttu-id="1980c-289">100</span><span class="sxs-lookup"><span data-stu-id="1980c-289">100</span></span> |<span data-ttu-id="1980c-290">100</span><span class="sxs-lookup"><span data-stu-id="1980c-290">100</span></span> |
| <span data-ttu-id="1980c-291">Wybierz żywności według producenta</span><span class="sxs-lookup"><span data-stu-id="1980c-291">Select foods by manufacturer</span></span> |<span data-ttu-id="1980c-292">25</span><span class="sxs-lookup"><span data-stu-id="1980c-292">25</span></span> |<span data-ttu-id="1980c-293">175</span><span class="sxs-lookup"><span data-stu-id="1980c-293">175</span></span> |
| <span data-ttu-id="1980c-294">Wybierz grupy żywności</span><span class="sxs-lookup"><span data-stu-id="1980c-294">Select by food group</span></span> |<span data-ttu-id="1980c-295">10</span><span class="sxs-lookup"><span data-stu-id="1980c-295">10</span></span> |<span data-ttu-id="1980c-296">700</span><span class="sxs-lookup"><span data-stu-id="1980c-296">700</span></span> |
| <span data-ttu-id="1980c-297">Wybierz 10 pierwszych</span><span class="sxs-lookup"><span data-stu-id="1980c-297">Select top 10</span></span> |<span data-ttu-id="1980c-298">15</span><span class="sxs-lookup"><span data-stu-id="1980c-298">15</span></span> |<span data-ttu-id="1980c-299">Łącznie 150</span><span class="sxs-lookup"><span data-stu-id="1980c-299">150 Total</span></span> |

<span data-ttu-id="1980c-300">W takim przypadku oczekujemy wymaganie średniej przepływności 1,275 RU/s.</span><span class="sxs-lookup"><span data-stu-id="1980c-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="1980c-301">Zaokrąglania toohello najbliższej 100, firma Microsoft może udostępnić 1300 RU/s dla kolekcji tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1980c-301">Rounding up toohello nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="1980c-302"><a id="RequestRateTooLarge"></a>Przekraczanie limitów zarezerwowaną przepływnością w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="1980c-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="1980c-303">Odwołaj, że zużycie jednostka żądania jest oceniana jako szybkość na sekundę, jeśli budżetu hello jest pusta.</span><span class="sxs-lookup"><span data-stu-id="1980c-303">Recall that request unit consumption is evaluated as a rate per second if hello budget is empty.</span></span> <span data-ttu-id="1980c-304">Dla aplikacji, które przekraczają hello elastycznie jednostki częstość kontenera, żądania kolekcji toothat będzie ograniczony, dopóki hello spada poniżej poziomu hello zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="1980c-304">For applications that exceed hello provisioned request unit rate for a container, requests toothat collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="1980c-305">W przypadku przepustnicy powitania serwera preemptively zakończy się Żądanie hello RequestRateTooLargeException (kod stanu HTTP 429) i zwracany hello nagłówka x-ms ponawiania — po ms wskazujący, że hello ilość czasu, w milisekundach hello użytkownik musi zaczekać na Interwał ponawiania hello żądanie.</span><span class="sxs-lookup"><span data-stu-id="1980c-305">When a throttle occurs, hello server will preemptively end hello request with RequestRateTooLargeException (HTTP status code 429) and return hello x-ms-retry-after-ms header indicating hello amount of time, in milliseconds, that hello user must wait before reattempting hello request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="1980c-306">Jeśli używasz hello zestawu SDK klienta usługi .NET i LINQ zapytania, a następnie w większości przypadków hello nigdy nie masz toodeal z tym wyjątkiem, zgodnie z bieżącą wersję hello hello zestawu SDK klienta .NET niejawnie przechwytuje tej odpowiedzi względem hello określony serwer ponownych prób po nagłówka i Żądanie hello ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="1980c-306">If you are using hello .NET Client SDK and LINQ queries, then most of hello time you never have toodeal with this exception, as hello current version of hello .NET Client SDK implicitly catches this response, respects hello server-specified retry-after header, and retries hello request.</span></span> <span data-ttu-id="1980c-307">Hello Następna ponowna próba powiedzie się, chyba że Twoje konto jest uzyskiwany jednocześnie przez wielu klientów.</span><span class="sxs-lookup"><span data-stu-id="1980c-307">Unless your account is being accessed concurrently by multiple clients, hello next retry will succeed.</span></span>

<span data-ttu-id="1980c-308">Jeśli masz więcej niż jednego klienta zbiorczo operacyjnego powyżej liczby żądań hello, hello domyślne zachowanie ponawiania mogą być niewystarczające i powitania klienta zgłosi DocumentClientException z aplikacją toohello 429 kodu stanu.</span><span class="sxs-lookup"><span data-stu-id="1980c-308">If you have more than one client cumulatively operating above hello request rate, hello default retry behavior may not suffice, and hello client will throw a DocumentClientException with status code 429 toohello application.</span></span> <span data-ttu-id="1980c-309">W przypadkach, takich jak ta można rozważyć Obsługa zachowanie ponownych prób i logikę w aplikacji Błąd procedury obsługi lub zwiększenie hello zarezerwowaną przepływnością hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="1980c-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing hello reserved throughput for hello container.</span></span>

## <span data-ttu-id="1980c-310"><a id="RequestRateTooLargeAPIforMongoDB"></a>Przekraczanie limitów zarezerwowaną przepływnością w interfejsie API, bazy danych mongodb</span><span class="sxs-lookup"><span data-stu-id="1980c-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="1980c-311">Aplikacje, które przekraczają hello elastycznie jednostek żądania dla kolekcji będzie ograniczony, dopóki hello spada poniżej poziomu hello zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="1980c-311">Applications that exceed hello provisioned request units for a collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="1980c-312">W przypadku przepustnicy zaplecza hello preemptively zakończy się hello żądania z *16500* kod błędu: - *zbyt wiele żądań*.</span><span class="sxs-lookup"><span data-stu-id="1980c-312">When a throttle occurs, hello backend will preemptively end hello request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="1980c-313">Domyślnie interfejsu API dla bazy danych MongoDB automatycznie ponowi próbę zapasowej razy too10 przed zwróceniem *zbyt wiele żądań* kod błędu.</span><span class="sxs-lookup"><span data-stu-id="1980c-313">By default, API for MongoDB will automatically retry up too10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="1980c-314">W przypadku otrzymania wiele *zbyt wiele żądań* kody błędów, można rozważyć albo dodanie zachowanie ponownych prób w aplikacji Błąd procedury obsługi lub [zwiększenie hello zarezerwowaną przepływnością dla kolekcji hello](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="1980c-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing hello reserved throughput for hello collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1980c-315">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1980c-315">Next steps</span></span>
<span data-ttu-id="1980c-316">toolearn więcej informacji na temat zarezerwowaną przepływnością z bazami danych bazy danych Azure rozwiązania Cosmos, zapoznaj się z tymi zasobami:</span><span class="sxs-lookup"><span data-stu-id="1980c-316">toolearn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="1980c-317">Cennik platformy Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="1980c-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="1980c-318">Partycjonowanie danych w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="1980c-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="1980c-319">toolearn więcej informacji na temat bazy danych rozwiązania Cosmos platformy Azure, zobacz hello Azure DB rozwiązania Cosmos [dokumentacji](https://azure.microsoft.com/documentation/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="1980c-319">toolearn more about Azure Cosmos DB, see hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="1980c-320">Zobacz tooget wprowadzenie testowanie Azure DB rozwiązania Cosmos, wydajności i skalowania [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="1980c-320">tooget started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
