---
title: "Praca z zmiany źródła pomocy technicznej w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Obsługa kanału informacyjnego zmiany bazy danych Azure rozwiązania Cosmos umożliwia śledzenie zmian w dokumentach i wykonywać oparty na zdarzeniach przetwarzania, takich jak wyzwalaczy i aktualizowanie systemów pamięci podręcznych i analiza."
keywords: "Zmiana źródła danych"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="2c6fa-104">Praca z zmiany źródła pomocy technicznej w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="2c6fa-104">Working with the change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="2c6fa-105">[Azure DB rozwiązania Cosmos](../cosmos-db/introduction.md) jest szybkie i elastyczne globalnie replikowane usługi bazy danych, która służy do przechowywania duże ilości danych transakcyjnych i działa z przewidywalną jednocyfrowej milisekundy opóźnienia dla operacji odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="2c6fa-106">Dzięki temu odpowiednie IoT gry detaliczna, i operacyjne rejestrowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="2c6fa-107">Typowe wzorzec projektowania w tych aplikacjach jest śledzić zmiany wprowadzone w danych bazy danych Azure rozwiązania Cosmos i zaktualizować zmaterializowanych widoków, wykonywać analizy w czasie rzeczywistym, archiwizowanie danych do magazynu chłodni i powiadomienia wyzwalane na określone zdarzenia na podstawie tych zmian.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-107">A common design pattern in these applications is to track changes made to Azure Cosmos DB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="2c6fa-108">**Zmiany źródła pomocy technicznej** w usłudze Azure DB rozwiązania Cosmos umożliwia tworzenie wydajnych i skalowalne rozwiązania dla każdego z tych wzorców.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-108">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="2c6fa-109">W przypadku zmiany źródła pomocy technicznej bazy danych Azure rozwiązania Cosmos zapewnia posortowaną listę dokumentów w kolekcji usługi Azure DB rozwiązania Cosmos w kolejności, w którym zostały zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in the order in which they were modified.</span></span> <span data-ttu-id="2c6fa-110">To źródło może służyć do nasłuchiwania zmian danych w kolekcji i wykonywać akcje, takie jak:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span></span>

* <span data-ttu-id="2c6fa-111">Wyzwala wywołanie interfejsu API, gdy dokument zostanie wstawiony lub zmodyfikowany</span><span class="sxs-lookup"><span data-stu-id="2c6fa-111">Trigger a call to an API when a document is inserted or modified</span></span>
* <span data-ttu-id="2c6fa-112">Podczas przetwarzania strumienia w czasie rzeczywistym () aktualizacji</span><span class="sxs-lookup"><span data-stu-id="2c6fa-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="2c6fa-113">Synchronizowanie danych z pamięci podręcznej, aparat wyszukiwania lub magazynu danych</span><span class="sxs-lookup"><span data-stu-id="2c6fa-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="2c6fa-114">Zmiany w usłudze Azure DB rozwiązania Cosmos są zachowywane mogą być przetwarzane asynchronicznie i dystrybuowana do co najmniej jeden konsumentów w celu równoległego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="2c6fa-115">Przyjrzyjmy się interfejsy API do zmiany źródła danych i jak ich używać do tworzenia skalowalnych aplikacji w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-115">Let's look at the APIs for change feed and how you can use them to build scalable real-time applications.</span></span> <span data-ttu-id="2c6fa-116">W tym artykule przedstawiono sposób pracy z bazy danych Azure rozwiązania Cosmos zmiany źródła danych i interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-116">This article shows how to work with Azure Cosmos DB change feed and the DocumentDB API.</span></span> 

![Przy użyciu bazy danych Azure rozwiązania Cosmos zmiany źródła danych do analizy w czasie rzeczywistym zasilania i scenariuszach obliczeniowych o sterowane zdarzeniami](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="2c6fa-118">Zmiana źródła danych obsługi jest tworzony tylko dla interfejsu API usługi DocumentDB w tej chwili; Interfejs API programu Graph i interfejsu API tabeli nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-118">Change feed support is only provided for the DocumentDB API at this time; the Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="2c6fa-119">Przypadki użycia i scenariusze</span><span class="sxs-lookup"><span data-stu-id="2c6fa-119">Use cases and scenarios</span></span>
<span data-ttu-id="2c6fa-120">Zmiana źródła umożliwia wydajne przetwarzania dużych zestawów danych z dużą liczbę operacji zapisu i oferuje alternatywę do badania cały zestaw danych do identyfikacji, co się zmieniło.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span></span> <span data-ttu-id="2c6fa-121">Na przykład można efektywnie wykonywać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-121">For example, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="2c6fa-122">Aktualizacji pamięci podręcznej, indeksu wyszukiwania lub magazynu danych z danych przechowywanych w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="2c6fa-123">Implementuje warstw i archiwizowania danych na poziomie aplikacji, czyli przechowywać "gorących danych" w usłudze Azure DB rozwiązania Cosmos i przedawniają "zimnych danych", aby [magazyn obiektów Blob Azure](../storage/common/storage-introduction.md) lub [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="2c6fa-124">Implementowanie analizach wsadowych na danych przy użyciu [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="2c6fa-125">Implementowanie [potoki lambda na platformie Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="2c6fa-126">Azure DB rozwiązania Cosmos zapewnia rozwiązanie skalowalne bazy danych, które można obsługiwać wprowadzanie i zapytań oraz implementował architektury lambda z niskim całkowitego kosztu posiadania.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="2c6fa-127">Wykonywać zero czas przestoju migracji na inne konto bazy danych Azure rozwiązania Cosmos z różnych schemat partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-127">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="2c6fa-128">**Potoki lambda z bazy danych rozwiązania Cosmos Azure wprowadzanie i zapytania:**</span><span class="sxs-lookup"><span data-stu-id="2c6fa-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Potok lambda wprowadzanie i zapytań na podstawie Azure DB rozwiązania Cosmos](./media/change-feed/lambda.png)

<span data-ttu-id="2c6fa-130">Użyj bazy danych Azure rozwiązania Cosmos do pobierania i przechowywania danych o zdarzeniach z urządzeń, czujników, infrastruktury i aplikacji, a przetwarzanie tych zdarzeń w czasie rzeczywistym za pomocą [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), lub [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-130">You can use Azure Cosmos DB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="2c6fa-131">W ramach Twojej [niekorzystającą](http://azure.com/serverless) sieci web i aplikacji mobilnych można Śledź zdarzenia, takie jak zmiany do klienta profilu, preferencje lub lokalizacji do wyzwalania określonych akcji, takich jak wysyłanie powiadomień wypychanych do urządzeń przy użyciu [ Środowisko Azure Functions](../azure-functions/functions-bindings-documentdb.md) lub [usługi aplikacji](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="2c6fa-132">Jeśli używasz bazy danych Azure rozwiązania Cosmos do tworzenia gier, można wykonywać następujące czynności, na przykład używanie zmiany źródła danych do zaimplementowania w czasie rzeczywistym tablice wyników oparte na wyniki z gry ukończone.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-132">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="2c6fa-133">Jak działa zmiany źródła danych w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="2c6fa-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="2c6fa-134">Azure DB rozwiązania Cosmos pozwala przyrostowo odczytać aktualizacje wprowadzone w kolekcji usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-134">Azure Cosmos DB provides the ability to incrementally read updates made to an Azure Cosmos DB collection.</span></span> <span data-ttu-id="2c6fa-135">To źródło zmiany ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-135">This change feed has the following properties:</span></span>

* <span data-ttu-id="2c6fa-136">Zmiany są trwałe w usłudze Azure DB rozwiązania Cosmos i mogą być przetwarzane asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="2c6fa-137">Zmiany do dokumentów w kolekcji są dostępne natychmiast w zmiany źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-137">Changes to documents within a collection are available immediately in the change feed.</span></span>
* <span data-ttu-id="2c6fa-138">Każdej zmiany do dokumentu zostanie wyświetlone tylko raz w przypadku zmiany źródła danych, a klienci zarządzania ich logiki tworzenie punktów kontrolnych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-138">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="2c6fa-139">Biblioteka źródła procesora zmianami zapewnia automatyczne tworzenie punktów kontrolnych i "co najmniej raz" semantyki.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-139">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="2c6fa-140">Tylko najnowsze zmiany w danym dokumencie znajduje się w dzienniku zmian.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-140">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="2c6fa-141">Pośrednie zmiany mogą nie być dostępne.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="2c6fa-142">Zmiana źródła danych jest sortowana numer modyfikacji w każdej wartości klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-142">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="2c6fa-143">Brak nie gwarantuje kolejności między wartości klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="2c6fa-144">Zmiany mogą być synchronizowane z dowolnego punktu w czasie, oznacza to, że istnieje nie okres przechowywania danych, dla której zmiany są dostępne.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="2c6fa-145">Zmiany są dostępne w fragmentów zakresami kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="2c6fa-146">Ta funkcja umożliwia zmiany w dużych kolekcjach do przetworzenia równolegle przez wielu użytkowników/serwerów.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-146">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="2c6fa-147">Aplikacje mogą żądać wiele źródeł zmiany równocześnie w tej samej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-147">Applications can request for multiple change feeds simultaneously on the same collection.</span></span>

<span data-ttu-id="2c6fa-148">Azure DB rozwiązania Cosmos zmiany źródła jest domyślnie włączona dla wszystkich kont.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="2c6fa-149">Można użyć programu [udostępnionej przepływności](request-units.md) w Twoim regionie zapisu lub w dowolnej [odczytu region](distribute-data-globally.md) odczytywać zmian źródła danych, podobnie jak inne operacje z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="2c6fa-150">Zmiana źródła strumieniowego obejmuje wstawienia i operacje aktualizacji do dokumentów w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-150">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="2c6fa-151">Można przechwycić usuwa przez ustawienie w dokumentach zamiast usuwa flagę "soft-delete".</span><span class="sxs-lookup"><span data-stu-id="2c6fa-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="2c6fa-152">Alternatywnie, można ustawić okresu wygaśnięcia skończoną dla dokumentów za pomocą [możliwości TTL](time-to-live.md), na przykład, 24 godzin i użyj wartości tej właściwości, aby przechwycić usuwa.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-152">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="2c6fa-153">W tym rozwiązaniu ma przetwarzać zmiany w określonym czasie krótszy niż okres ważności TTL.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-153">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span> <span data-ttu-id="2c6fa-154">Zmiany źródła danych jest dostępne dla każdego zakresu klucza partycji w obrębie kolekcji dokumentów i w związku z tym mogą być rozproszone na co najmniej jeden konsumentów w celu równoległego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-154">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Przetwarzanie rozproszone zmiany bazy danych Azure rozwiązania Cosmos źródła danych](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="2c6fa-156">Istnieje kilka opcji w sposobu implementacji zmiany źródła danych w kodzie klienta.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="2c6fa-157">W kolejnych sekcjach natychmiast opisano sposób wdrażania zmian źródła danych przy użyciu interfejsu API REST Azure rozwiązania Cosmos bazy danych i zestawy SDK usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-157">The sections that immediately follow describe how to implement the change feed using the Azure Cosmos DB REST API and the DocumentDB SDKs.</span></span> <span data-ttu-id="2c6fa-158">Jednak dla aplikacji .NET, firma Microsoft zaleca używanie nowego [zmiany źródła danych biblioteki procesora](#change-feed-processor) do przetwarzania zdarzeń z zmiany źródła upraszcza odczytu zmiany na partycje i umożliwia wiele wątków pracy w równoległe.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-158">However, for .NET applications, we recommend using the new [Change feed processor library](#change-feed-processor) for processing events from the change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="2c6fa-159"><a id="rest-apis"></a>Praca z interfejsu API REST i zestawów SDK usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="2c6fa-159"><a id="rest-apis"></a>Working with the REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="2c6fa-160">Azure DB rozwiązania Cosmos zapewnia elastyczne kontenery magazynu i przepustowości o nazwie **kolekcji**.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="2c6fa-161">Przy użyciu logicznie pogrupowane danych w kolekcjach [kluczy partycji](partition-data.md) na skalowalność i wydajność.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="2c6fa-162">Azure DB rozwiązania Cosmos udostępnia różne interfejsy API do uzyskiwania dostępu do tych danych, tym wyszukiwanie według Identyfikatora (odczyt/Get), kwerendy i odczytu źródła danych (skanowania).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="2c6fa-163">Zmiana źródła danych można uzyskać za wypełnianie dwa nowe nagłówki żądania do usługi DocumentDB `ReadDocumentFeed` interfejsu API i mogą być przetwarzane równolegle w zakresach kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-163">The change feed can be obtained by populating two new request headers to the DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="2c6fa-164">ReadDocumentFeed interfejsu API</span><span class="sxs-lookup"><span data-stu-id="2c6fa-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="2c6fa-165">Spójrzmy krótki opis działania ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="2c6fa-166">Obsługuje bazę danych systemu Azure rozwiązania Cosmos czytania źródła dokumentów w kolekcji za pomocą `ReadDocumentFeed` interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-166">Azure Cosmos DB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span></span> <span data-ttu-id="2c6fa-167">Na przykład następujące żądania zwraca stronę dokumenty wewnątrz `serverlogs` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-167">For example, the following request returns a page of documents inside the `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="2c6fa-168">Wyniki mogą być ograniczone za pomocą `x-ms-max-item-count` nagłówka i odczytuje można wznowić, stosując Prześlij żądanie z `x-ms-continuation` nagłówka zwracane w poprzedniej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-168">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span></span> <span data-ttu-id="2c6fa-169">Gdy wykonywane z jednego klienta, `ReadDocumentFeed` iteruje wyników na partycje pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="2c6fa-170">**Seryjne odczytu dokumentu źródła danych**</span><span class="sxs-lookup"><span data-stu-id="2c6fa-170">**Serial read document feed**</span></span>

<span data-ttu-id="2c6fa-171">Można również pobierać źródła dokumentów przy użyciu jednego z obsługiwanych [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-171">You can also retrieve the feed of documents using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="2c6fa-172">Na przykład poniższy fragment kodu przedstawia sposób użycia [metody ReadDocumentFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) w .NET.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-172">For example, the following snippet shows how to use the [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="2c6fa-173">Rozproszonego wykonywania ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="2c6fa-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="2c6fa-174">Dla kolekcji, które zawierają terabajtów danych lub więcej lub pozyskiwania dużą liczbę aktualizacji serial wykonywanie odczytu źródła danych z maszyny jednego klienta może nie być praktyczne.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="2c6fa-175">Aby zapewnić obsługę tych scenariuszy danych big data, bazy danych rozwiązania Cosmos Azure udostępnia interfejsy API do dystrybucji `ReadDocumentFeed` wywołania niewidocznie przez wielu klientów czytników klientów.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-175">In order to support these big data scenarios, Azure Cosmos DB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="2c6fa-176">**Źródło dokumentu odczytu rozproszonych**</span><span class="sxs-lookup"><span data-stu-id="2c6fa-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="2c6fa-177">Aby zapewnić skalowalne, przetwarzanie zmiany przyrostowe bazy danych Azure rozwiązania Cosmos obsługuje skalowalnego w poziomie model zmian źródła danych na podstawie zakresów kluczy partycji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-177">To provide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for the change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="2c6fa-178">Można uzyskać listę partycji zakresami kluczy do wykonywania kolekcji `ReadPartitionKeyRanges` wywołania.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="2c6fa-179">Dla każdego zakresu klucza partycji można wykonywać `ReadDocumentFeed` odczytać dokumenty z kluczami partycji w ramach tego zakresu.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-179">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="2c6fa-180">Pobieranie zakresów klucza partycji dla kolekcji</span><span class="sxs-lookup"><span data-stu-id="2c6fa-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="2c6fa-181">Zakresy klucza partycji można pobrać przez zażądanie `pkranges` zasobów w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-181">You can retrieve the partition key ranges by requesting the `pkranges` resource within a collection.</span></span> <span data-ttu-id="2c6fa-182">Na przykład następujące żądania pobiera listę zakresy klucza partycji dla `serverlogs` kolekcji:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-182">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="2c6fa-183">To żądanie zwraca następującą odpowiedź zawierający metadane o zakresach klucza partycji:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-183">This request returns the following response containing metadata about the partition key ranges:</span></span>

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


<span data-ttu-id="2c6fa-184">**Właściwości zakresu klucza partycji**: każdego zakresem kluczy partycji zawiera właściwości metadanych w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-184">**Partition key range properties**: Each partition key range includes the metadata properties in the following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="2c6fa-185">Nazwa nagłówka</span><span class="sxs-lookup"><span data-stu-id="2c6fa-185">Header name</span></span></th>
        <th><span data-ttu-id="2c6fa-186">Opis</span><span class="sxs-lookup"><span data-stu-id="2c6fa-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-187">id</span><span class="sxs-lookup"><span data-stu-id="2c6fa-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="2c6fa-188">Identyfikator zakresu klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-188">The ID for the partition key range.</span></span> <span data-ttu-id="2c6fa-189">To jest stabilna i unikatowy identyfikator w ramach każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="2c6fa-190">Może posłużyć w poniższym wywołaniu odczytać zmiany zakresem kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-190">Must be used in the following call to read changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="2c6fa-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="2c6fa-192">Wartość skrótu klucza partycji maksymalną zakresem kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-192">The maximum partition key hash value for the partition key range.</span></span> <span data-ttu-id="2c6fa-193">Do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="2c6fa-194">minInclusive</span></span></td>
        <td><span data-ttu-id="2c6fa-195">Wartość skrótu klucza partycji minimalna zakresem kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-195">The minimum partition key hash value for the partition key range.</span></span> <span data-ttu-id="2c6fa-196">Do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="2c6fa-197">Można to zrobić przy użyciu jednego z obsługiwanych [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-197">You can do this using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="2c6fa-198">Na przykład poniższy fragment kodu przedstawia sposób pobrać zakresami kluczy partycji w .NET przy użyciu [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) metody.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-198">For example, the following snippet shows how to retrieve partition key ranges in .NET using the [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

<span data-ttu-id="2c6fa-199">Azure DB rozwiązania Cosmos obsługuje pobierania dokumentów na zakresem kluczy partycji przez ustawienie opcjonalne `x-ms-documentdb-partitionkeyrangeid` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="2c6fa-200">Wykonywanie przyrostowych ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="2c6fa-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="2c6fa-201">ReadDocumentFeed obsługuje następujące scenariusze/zadania przetwarzania przyrostowe zmiany w kolekcjach bazy danych rozwiązania Cosmos Azure:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-201">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="2c6fa-202">Odczytywać wszystkie zmiany do dokumentów od początku, czyli tworzenia kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-202">Read all changes to documents from the beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="2c6fa-203">Przeczytaj wszystkie zmiany do przyszłych aktualizacji do dokumentów z bieżącej godziny lub wszelkie zmiany od czasu określonego przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-203">Read all changes to future updates to documents from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="2c6fa-204">Odczytywać wszystkie zmiany do dokumentów logicznej wersji kolekcji (ETag).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-204">Read all changes to documents from a logical version of the collection (ETag).</span></span> <span data-ttu-id="2c6fa-205">Punkt kontrolny można użytkowników oparte na zwrócony element ETag z przyrostowych żądań odczytu źródła.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-205">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="2c6fa-206">Wstawia obejmują zmiany i aktualizacje do dokumentów.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-206">The changes include inserts and updates to documents.</span></span> <span data-ttu-id="2c6fa-207">Aby przechwycić usuwa, należy użyć właściwości "usuwania nietrwałego" w dokumencie, lub użyj [wbudowanych właściwości TTL](time-to-live.md) sygnalizują Oczekujące usunięcie zmian źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-207">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](time-to-live.md) to signal a pending deletion in the change feed.</span></span>

<span data-ttu-id="2c6fa-208">W poniższej tabeli wymieniono [żądania](/rest/api/documentdb/common-documentdb-rest-request-headers.md) i [nagłówki odpowiedzi](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed operacji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-208">The following table lists the [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="2c6fa-209">**Nagłówki żądań dla przyrostowych ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="2c6fa-210">Nazwa nagłówka</span><span class="sxs-lookup"><span data-stu-id="2c6fa-210">Header name</span></span></th>
        <th><span data-ttu-id="2c6fa-211">Opis</span><span class="sxs-lookup"><span data-stu-id="2c6fa-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-212">WIADOMOŚCI BŁYSKAWICZNYCH A</span><span class="sxs-lookup"><span data-stu-id="2c6fa-212">A-IM</span></span></td>
        <td><span data-ttu-id="2c6fa-213">Musi być ustawiona na "Przyrostowe źródła strumieniowego" lub w przeciwnym razie pominięcia</span><span class="sxs-lookup"><span data-stu-id="2c6fa-213">Must be set to "Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="2c6fa-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="2c6fa-215">Brak nagłówka: zwraca wszystkie zmiany od początku (kolekcja tworzenia)</span><span class="sxs-lookup"><span data-stu-id="2c6fa-215">No header: returns all changes from the beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="2c6fa-216">"*": zwraca wszystkie nowe zmiany danych w kolekcji</span><span class="sxs-lookup"><span data-stu-id="2c6fa-216">"*": returns all new changes to data within the collection</span></span></p>           
            <p><span data-ttu-id="2c6fa-217">&lt;Element etag&gt;: Jeśli zestaw kolekcji ETag, zwraca wszystkie zmiany wprowadzone od momentu ten znacznik logiczne</span><span class="sxs-lookup"><span data-stu-id="2c6fa-217">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="2c6fa-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="2c6fa-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="2c6fa-219">Format czasu RFC 1123; ignorowane, jeśli If-None-Match został określony.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="2c6fa-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="2c6fa-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="2c6fa-221">Identyfikator zakresem kluczy partycji do odczytywania danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-221">The partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="2c6fa-222">**Nagłówki odpowiedzi dla przyrostowych ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="2c6fa-223">Nazwa nagłówka</span><span class="sxs-lookup"><span data-stu-id="2c6fa-223">Header name</span></span></th>
        <th><span data-ttu-id="2c6fa-224">Opis</span><span class="sxs-lookup"><span data-stu-id="2c6fa-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-225">Element etag</span><span class="sxs-lookup"><span data-stu-id="2c6fa-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="2c6fa-226">Numer sekwencyjny logiczne (LSN) ostatniego dokumentu zwrócił w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-226">The logical sequence number (LSN) of last document returned in the response.</span></span></p>
            <p><span data-ttu-id="2c6fa-227">Przy ponownym przesłaniem tej wartości w If-None-Match można wznawiać ReadDocumentFeed przyrostowe.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="2c6fa-228">Poniżej przedstawiono przykładowe żądanie, aby zwrócić wszystkie zmiany przyrostowe w kolekcji z logiczną wersji/ETag `28535` i zakresem kluczy partycji = `16`:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-228">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span></span>

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="2c6fa-229">Zmiany są uporządkowane według czasu w każdym wartość klucza partycji w zakresie klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-229">Changes are ordered by time within each partition key value within the partition key range.</span></span> <span data-ttu-id="2c6fa-230">Brak nie gwarantuje kolejności między wartości klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="2c6fa-231">Jeśli istnieje więcej wyników niż można zmieścić w jednej strony, można uzyskać następnej strony wyników Prześlij żądanie z `If-None-Match` nagłówek o wartości równej `etag` z poprzedniej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-231">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span></span> <span data-ttu-id="2c6fa-232">Jeśli wiele dokumentów zostały wstawione lub zaktualizowane transakcyjnie, w ramach procedury składowanej lub wyzwalacza, ich zostaną wszystkie zwrócone w ramach tej samej stronie odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="2c6fa-233">Z zmian w źródle danych może spowodować, że więcej elementów zwróconych na stronie, niż określa `x-ms-max-item-count` w przypadku wielu dokumentów wstawiane lub aktualizowane w ramach procedur składowanych lub wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="2c6fa-234">Podczas korzystania z zestawu .NET SDK (1.17.0), ustaw dla pola `StartTime` w `ChangeFeedOptions` do zwrócenia bezpośrednio dokumenty zmienione od czasu `StartTime` podczas wywoływania metody `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-234">When using the .NET SDK (1.17.0), set the field `StartTime` in `ChangeFeedOptions` to directly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="2c6fa-235">Określając `If-Modified-Since` przy użyciu interfejsu API REST, żądanie będzie zwracać nie dokumentów samodzielnie, ale raczej token kontynuacji lub `etag` nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-235">By specifying `If-Modified-Since` using the REST API, your request will return not the documents themselves, but rather the continuation token or `etag` in the response header.</span></span> <span data-ttu-id="2c6fa-236">Aby zwrócić określonego czasu token kontynuacji zmodyfikowane dokumenty `etag` następnie musi być używany w następnym żądaniu z `If-None-Match` do zwrócenia rzeczywistego dokumentów.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-236">To return the documents modified the specified time, the continuation token `etag` must then be used in the next request with `If-None-Match` to return the actual documents.</span></span> 

<span data-ttu-id="2c6fa-237">Zestaw .NET SDK zawiera [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) i [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) klasy pomocy do zmiany wprowadzone do kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-237">The .NET SDK provides the [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes to access changes made to a collection.</span></span> <span data-ttu-id="2c6fa-238">Poniższy fragment kodu przedstawia sposób pobrać wszystkie zmiany od początku przy użyciu zestawu .NET SDK z jednego klienta.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-238">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span></span>

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
<span data-ttu-id="2c6fa-239">I poniższy fragment kodu przedstawia sposób przetwarzaniem zmian w w czasie rzeczywistym z bazy danych rozwiązania Cosmos Azure za pomocą zmiany źródła pomocy technicznej i poprzedniego funkcji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-239">And the following snippet shows how to process changes in real-time with Azure Cosmos DB by using the change feed support and the preceding function.</span></span> <span data-ttu-id="2c6fa-240">Pierwsze wywołanie zwraca wszystkie dokumenty w kolekcji, natomiast drugi tylko dwa dokumenty utworzone utworzonych od czasu ostatniego punktu kontrolnego.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-240">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span></span>

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="2c6fa-241">Można również filtrować zmiany źródła danych przy użyciu logiki po stronie klienta można selektywnie przetworzyć zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-241">You can also filter the change feed using client side logic to selectively process events.</span></span> <span data-ttu-id="2c6fa-242">Na przykład poniżej przedstawiono fragment kodu, który używa po stronie klienta LINQ do przetwarzania zdarzeń zmiany temperatury tylko z czujników urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-242">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="2c6fa-243"><a id="change-feed-processor"></a>Zmiana źródła procesora biblioteki</span><span class="sxs-lookup"><span data-stu-id="2c6fa-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="2c6fa-244">Inną opcją jest użycie [biblioteki Azure rozwiązania Cosmos DB zmienić źródła procesora](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), który pomoże Ci łatwo rozpowszechniaj przetwarzania ze źródła danych w wielu klientów zmiany zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-244">Another option is to use the [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="2c6fa-245">Biblioteka jest doskonały dla tworzenia zmiany źródła czytników na platformie .NET.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-245">The library is great for building change feed readers on the .NET platform.</span></span> <span data-ttu-id="2c6fa-246">Niektóre przepływy pracy, które może uprościć przy użyciu biblioteki zmiany procesora źródła danych za pośrednictwem metody zawarte w innych zestawów SDK DB rozwiązania Cosmos obejmują:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-246">Some workflows that would be simplified by using the Change Feed Processor library over the methods included in the other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="2c6fa-247">Ściągania aktualizacji z zmiany źródła danych, gdy dane są przechowywane w wielu partycji</span><span class="sxs-lookup"><span data-stu-id="2c6fa-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="2c6fa-248">Przenoszenie lub replikowanie danych z jednej kolekcji do innego</span><span class="sxs-lookup"><span data-stu-id="2c6fa-248">Moving or replicating data from one collection to another</span></span>
* <span data-ttu-id="2c6fa-249">Równoległe wykonywanie akcji wyzwalane przez aktualizacje do danych i zmiany źródła danych</span><span class="sxs-lookup"><span data-stu-id="2c6fa-249">Parallel execution of actions triggered by updates to data and change feed</span></span> 

<span data-ttu-id="2c6fa-250">Za pomocą interfejsów API w zestawy SDK rozwiązania Cosmos zawiera dokładne dostęp do zmiany źródła aktualizacji w każdej partycji, natomiast za pomocą biblioteki zmienić źródła procesora upraszcza odczytu zmiany na partycje i wiele wątków działające równolegle.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-250">While using the APIs in the Cosmos SDKs provides precise access to change feed updates in each partition, using the Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="2c6fa-251">Zamiast ręcznego odczytywać zmian z każdego kontenera i zapisywać token kontynuacji dla każdej partycji procesor źródła danych zmian automatycznie zarządza odczytu zmiany na partycje przy użyciu mechanizmu dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-251">Instead of manually reading changes from each container and saving a continuation token for each partition, the Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="2c6fa-252">Biblioteka jest dostępna jako pakietu NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) i z kodu źródłowego jako Github [próbki](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-252">The library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="2c6fa-253">Opis zmiany procesora źródła danych biblioteki</span><span class="sxs-lookup"><span data-stu-id="2c6fa-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="2c6fa-254">Istnieją cztery główne składniki wdrażania procesora źródła danych zmian: monitorowanych kolekcję, Kolekcja dzierżawy hosta procesora i konsumentów.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-254">There are four main components of implementing the Change Feed Processor: the monitored collection, the lease collection, the processor host, and the consumers.</span></span> 

<span data-ttu-id="2c6fa-255">**Kolekcja monitorowanych:** monitorowanych kolekcja jest danych, z którego jest generowany zmiany źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-255">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span></span> <span data-ttu-id="2c6fa-256">Żadnych instrukcji INSERT i zmiany w kolekcji monitorowane są uwzględniane w źródle danych zmiany kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-256">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span></span> 

<span data-ttu-id="2c6fa-257">**Kolekcja dzierżawy:** współrzędne kolekcji dzierżawy przetwarzania zmian źródła danych w wielu pracowników.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-257">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="2c6fa-258">Oddzielne kolekcji jest używany do przechowywania dzierżaw z jednej dzierżawy dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-258">A separate collection is used to store the leases with one lease per partition.</span></span> <span data-ttu-id="2c6fa-259">Jest korzystne w przypadku przechowywania tej kolekcji dzierżawy na inne konto o regionowi zapisu na którym jest uruchomiona procesora źródła danych zmian.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-259">It is advantageous to store this lease collection on a different account with the write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="2c6fa-260">Obiekt dzierżawy zawiera następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-260">A lease object contains the following attributes:</span></span> 
* <span data-ttu-id="2c6fa-261">Właściciel: Określa hosta, który jest właścicielem dzierżawy</span><span class="sxs-lookup"><span data-stu-id="2c6fa-261">Owner: Specifies the host that owns the lease</span></span>
* <span data-ttu-id="2c6fa-262">Kontynuacja: Określa położenie (token kontynuacji) w przypadku zmiany dla określonej partycji</span><span class="sxs-lookup"><span data-stu-id="2c6fa-262">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span></span>
* <span data-ttu-id="2c6fa-263">Znacznik czasu: Czas ostatniego dzierżawy został zaktualizowany; Sygnatura czasowa może służyć do sprawdzenia, czy dzierżawy jest uznawany za wygasły</span><span class="sxs-lookup"><span data-stu-id="2c6fa-263">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span></span> 

<span data-ttu-id="2c6fa-264">**Host procesora:** każdy host Określa, ile partycje do przetworzenia na podstawie liczby wystąpień hostów mają aktywne dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-264">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="2c6fa-265">Po uruchomieniu hosta, uzyskuje dzierżawy w celu zrównoważenia obciążenia na wszystkich hostach.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-265">When a host starts up, it acquires leases to balance the workload across all hosts.</span></span> <span data-ttu-id="2c6fa-266">Hosta okresowo odnowieniu dzierżawy, więc pozostaną aktywne dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="2c6fa-267">Punkty kontrolne hosta ostatniego token kontynuacji do dzierżawy dla każdego do odczytu.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-267">A host checkpoints the last continuation token to its lease for each read.</span></span> <span data-ttu-id="2c6fa-268">Do zapewnienia bezpieczeństwa współbieżności, host sprawdza ETag dla każdej aktualizacji dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-268">To ensure concurrency safety, a host checks the ETag for each lease update.</span></span> <span data-ttu-id="2c6fa-269">Obsługiwane są także inne strategie punktu kontrolnego.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="2c6fa-270">Podczas zamykania systemu host zwalnia wszystkie dzierżawy, ale przechowuje informacje kontynuacji, aby go ponownie później odczytu z przechowywanych punktu kontrolnego.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-270">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span></span> 

<span data-ttu-id="2c6fa-271">W tym momencie liczba hostów nie może być większa niż liczba partycji (dzierżawy).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-271">At this time the number of hosts cannot be greater than the number of partitions (leases).</span></span>

<span data-ttu-id="2c6fa-272">**Konsumenci:** użytkowników lub pracowników, są wątki przetwarzania zmian źródła danych inicjowane przez każdego hosta.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-272">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span></span> <span data-ttu-id="2c6fa-273">Każdy host procesora może mieć wielu klientów.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="2c6fa-274">Każdy odbiorca odczytuje zmiany źródła danych z partycji, który jest przypisany do powiadamia jej hosta zmian i ważność dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-274">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="2c6fa-275">Aby jeszcze lepiej zrozumieć, jak te cztery elementy procesora źródła danych zmian współdziałać ze sobą, Przyjrzyjmy się przykład na poniższym diagramie.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-275">To further understand how these four elements of Change Feed Processor work together, let's look at an example in the following diagram.</span></span> <span data-ttu-id="2c6fa-276">Kolekcja monitorowanych przechowuje dokumenty i używa "Miasto" jako klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-276">The monitored collection stores documents and uses the "city" as the partition key.</span></span> <span data-ttu-id="2c6fa-277">Widzimy niebieski partycji i tak dalej zawiera dokumenty z polem "Miasto" od "A-E".</span><span class="sxs-lookup"><span data-stu-id="2c6fa-277">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span></span> <span data-ttu-id="2c6fa-278">Istnieją dwa hosty, każda z dwóch konsumentów odczytu z cztery partycje równolegle.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-278">There are two hosts, each with two consumers reading from the four partitions in parallel.</span></span> <span data-ttu-id="2c6fa-279">Strzałki oznaczają konsumentów czytania z określonego punktu w przypadku zmiany źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-279">The arrows show the consumers reading from a specific spot in the change feed.</span></span> <span data-ttu-id="2c6fa-280">W pierwszej partycji niebieski ciemniejszego reprezentuje nieprzeczytana zmiany podczas koloru niebieskiego reprezentuje już odczytu zmiany w przypadku zmiany źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-280">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span></span> <span data-ttu-id="2c6fa-281">Hosty używają kolekcji dzierżawy do przechowywania wartości "kontynuacji", aby śledzić bieżącą pozycję odczytu dla każdego konsumenta.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-281">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span></span> 

![Przy użyciu zmian bazy danych Azure rozwiązania Cosmos źródła danych hosta procesora](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="2c6fa-283">Przy użyciu zmian źródła danych biblioteki procesora</span><span class="sxs-lookup"><span data-stu-id="2c6fa-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="2c6fa-284">Poniższej sekcji opisano sposób korzystania z biblioteki procesora źródła danych zmian w kontekście replikacji zmian z kolekcji źródłowej do docelowej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-284">The following section explains how to use the Change Feed Processor library in the context of replicating changes from a source collection to a destination collection.</span></span> <span data-ttu-id="2c6fa-285">W tym miejscu kolekcji źródłowej jest kolekcją monitorowanych w procesorze źródła danych zmian.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-285">Here, the source collection is the monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="2c6fa-286">**Zainstaluj i zawierać pakiet NuGet procesora źródła danych zmian**</span><span class="sxs-lookup"><span data-stu-id="2c6fa-286">**Install and include the Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="2c6fa-287">Przed zainstalowaniem pakietu NuGet procesora zmiany źródła danych należy najpierw zainstalować:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="2c6fa-288">Microsoft.Azure.DocumentDB, wersja 1.13.1 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="2c6fa-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="2c6fa-289">Newtonsoft.Json, wersja 9.0.1 lub powyżej instalacji `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` i dołączyć go jako odwołanie.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="2c6fa-290">**Utwórz kolekcję monitorowanych, dzierżawy i docelowego**</span><span class="sxs-lookup"><span data-stu-id="2c6fa-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="2c6fa-291">Aby można było używać biblioteki procesora zmiany źródła danych, kolekcji dzierżawy musi zostać utworzona przed uruchomieniem hostami procesora.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-291">In order to use the Change Feed Processor Library, the lease collection needs to be created before running the processor host(s).</span></span> <span data-ttu-id="2c6fa-292">Zaleca się ponownie, przechowywania kolekcji dzierżawy na inne konto, za pomocą zapisu obszaru bliżej na którym jest uruchomiona procesora źródła danych zmian.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-292">Again, we recommend storing a lease collection on a different account with a write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="2c6fa-293">W tym przykładzie przepływu danych należy utworzyć przed uruchomieniem hosta procesora źródła danych zmiany kolekcji docelowej.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-293">In this data movement example, we need to create the destination collection before running the Change Feed Processor host.</span></span> <span data-ttu-id="2c6fa-294">W przykładowym kodzie nazywamy metoda pomocnika umożliwiająca tworzenie monitorowanych, dzierżawy, i kolekcji docelowej, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-294">In the sample code we call a helper method to create the monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="2c6fa-295">Tworzenie kolekcji ma cenę, jak są rezerwacji przepustowości dla aplikacji do komunikowania się z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-295">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="2c6fa-296">Aby uzyskać więcej informacji, odwiedź stronę [stronie dotyczącej cen](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="2c6fa-296">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="2c6fa-297">*Tworzenie hosta procesora*</span><span class="sxs-lookup"><span data-stu-id="2c6fa-297">*Creating a processor host*</span></span>

<span data-ttu-id="2c6fa-298">`ChangeFeedProcessorHost` Klasa udostępnia środowisko wątkowo, wieloprocesowe, bezpieczne środowisko uruchomieniowe dla implementacji procesora zdarzeń, które umożliwia także tworzenie punktów kontrolnych i zarządzanie dzierżawą partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-298">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="2c6fa-299">Aby użyć `ChangeFeedProcessorHost` klasy, można zaimplementować `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-299">To use the `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="2c6fa-300">Ten interfejs zawiera trzy metody:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-300">This interface contains three methods:</span></span>

* <span data-ttu-id="2c6fa-301">`OpenAsync`: Ta funkcja jest wywoływana po otwarciu źródła obserwator zmiany.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="2c6fa-302">Można go zmodyfikować, aby wykonywać konkretną akcję po otwarciu konsumenta/obserwatora.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-302">It can be modified to perform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="2c6fa-303">`CloseAsync`: Ta funkcja jest wywoływana, gdy zmiana źródła obserwator jest zakończony.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="2c6fa-304">Można go zmodyfikować, aby wykonywać konkretną akcję po zamknięciu konsumenta/obserwatora.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-304">It can be modified to perform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="2c6fa-305">`ProcessChangesAsync`: Ta funkcja jest wywoływana, gdy nowe zmiany w dokumencie są dostępne na zmiany źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="2c6fa-306">Można go zmodyfikować, aby wykonywać konkretną akcję po każdej zmiany źródła aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-306">It can be modified to perform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="2c6fa-307">W naszym przykładzie mamy implementować interfejs `IChangeFeedObserver` za pośrednictwem `DocumentFeedObserver` klasy.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-307">In our example, we implement the interface `IChangeFeedObserver` through the `DocumentFeedObserver` class.</span></span> <span data-ttu-id="2c6fa-308">W tym miejscu `ProcessChangesAsync` funkcji upserts (aktualizacje), za pomocą zmian źródła danych w kolekcji docelowej.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-308">Here, the `ProcessChangesAsync` function upserts (updates) a document from change feed into the destination collection.</span></span> <span data-ttu-id="2c6fa-309">W tym przykładzie jest przydatna do przenoszenia danych z jednej kolekcji do innego, aby zmienić wartość klucza partycji zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-309">This example is useful for moving data from one collection to another in order to change the partition key of a data set.</span></span> 

<span data-ttu-id="2c6fa-310">*Uruchomiona hosta procesora*</span><span class="sxs-lookup"><span data-stu-id="2c6fa-310">*Running the Processor Host*</span></span>

<span data-ttu-id="2c6fa-311">Przed rozpoczęciem przetwarzania zdarzeń, zmień obie opcje źródła i zmień opcje hosta źródła strumieniowego można dostosować.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="2c6fa-312">Określonych pól, które można dostosowywać podsumowano w poniższych tabelach.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-312">The specific fields that can be customized are summarized in the following tables.</span></span> 

<span data-ttu-id="2c6fa-313">**Zmień opcje źródła**:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="2c6fa-314">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="2c6fa-314">Property Name</span></span></th>
        <th><span data-ttu-id="2c6fa-315">Opis</span><span class="sxs-lookup"><span data-stu-id="2c6fa-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="2c6fa-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="2c6fa-317">Pobiera lub ustawia maksymalną liczbę elementów, które mają być zwracane w operacji wyliczenia w usłudze Azure DB rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-317">Gets or sets the maximum number of items to be returned in the enumeration operation in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="2c6fa-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="2c6fa-319">Pobiera lub ustawia identyfikator zakresem kluczy partycji dla bieżącego żądania w usłudze Azure DB rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-319">Gets or sets the partition key range id for the current request in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="2c6fa-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="2c6fa-321">Pobiera lub ustawia token kontynuacji żądania w usłudze Azure DB rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-321">Gets or sets the request continuation token in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="2c6fa-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="2c6fa-322">SessionToken</span></span></td>
        <td><span data-ttu-id="2c6fa-323">Pobiera lub ustawia tokenu sesji do użycia z spójność sesji w usłudze Azure DB rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-323">Gets or sets the session token for use with session consistency in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="2c6fa-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="2c6fa-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="2c6fa-325">Pobiera lub ustawia, czy zmiany źródła danych w usłudze Azure DB rozwiązania Cosmos bazy danych powinna zaczynać się od początku (true) lub od bieżącego (false).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-325">Gets or sets whether change feed in the Azure Cosmos DB database service should start from the beginning (true) or from current (false).</span></span> <span data-ttu-id="2c6fa-326">Domyślnie rozpoczyna się od bieżącego (false).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="2c6fa-327">**Zmień opcje hosta źródła**:</span><span class="sxs-lookup"><span data-stu-id="2c6fa-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="2c6fa-328">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="2c6fa-328">Property Name</span></span></th>
        <th><span data-ttu-id="2c6fa-329">Typ</span><span class="sxs-lookup"><span data-stu-id="2c6fa-329">Type</span></span></th>
        <th><span data-ttu-id="2c6fa-330">Opis</span><span class="sxs-lookup"><span data-stu-id="2c6fa-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="2c6fa-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="2c6fa-332">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="2c6fa-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="2c6fa-333">Interwał wszystkie dzierżawy dla aktualnie utrzymywane przez wystąpienie ChangeFeedEventHost partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-333">The interval for all leases for partitions currently held by the ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="2c6fa-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="2c6fa-335">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="2c6fa-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="2c6fa-336">Odstęp czasu, aby rozpocząć wyłączyć zadanie do obliczenia, czy partycje są rozmieszczone równomiernie wystąpień znane hosta.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-336">The interval to kick off a task to compute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="2c6fa-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="2c6fa-338">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="2c6fa-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="2c6fa-339">Interwał, dla którego podjęto dzierżawy na dzierżawę reprezentujący partycji.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-339">The interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="2c6fa-340">Jeśli dzierżawa nie zostanie odnowiony w tym przedziale czasu, wygasł i własność partycji są przenoszone do innego wystąpienia ChangeFeedEventHost.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-340">If the lease is not renewed within this interval, it is expired and ownership of the partition moves to another ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="2c6fa-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="2c6fa-342">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="2c6fa-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="2c6fa-343">Opóźnienie między sondowania partycji dla nowych zmian na zmiany źródła, gdy wszyscy bieżący zostały opróżnione.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-343">The delay between polling a partition for new changes on the feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="2c6fa-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="2c6fa-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="2c6fa-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="2c6fa-346">Częstotliwość dzierżawy punktu kontrolnego.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-346">The frequency to checkpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="2c6fa-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="2c6fa-348">int</span><span class="sxs-lookup"><span data-stu-id="2c6fa-348">Int</span></span></td>
        <td><span data-ttu-id="2c6fa-349">Liczba partycji minimalną dla hosta.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-349">The minimum partition count for the host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="2c6fa-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="2c6fa-351">int</span><span class="sxs-lookup"><span data-stu-id="2c6fa-351">Int</span></span></td>
        <td><span data-ttu-id="2c6fa-352">Maksymalna liczba partycji, który może obsługiwać hosta.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-352">The maximum number of partitions the host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2c6fa-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="2c6fa-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="2c6fa-354">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2c6fa-354">Bool</span></span></td>
        <td><span data-ttu-id="2c6fa-355">Czy na początku hosta należy usunąć wszystkie istniejące dzierżawy i host ma się rozpoczynać od zera.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-355">Whether on the start of the host all existing leases should be deleted and the host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="2c6fa-356">Aby rozpocząć przetwarzanie zdarzeń, Utwórz wystąpienie `ChangeFeedProcessorHost`, podając odpowiednie parametry dla kolekcji bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-356">To start event processing, instantiate `ChangeFeedProcessorHost`, providing the appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="2c6fa-357">Następnie wywołaj metodę `RegisterObserverAsync` zarejestrować Twoje `IChangeFeedObserver` implementacji (DocumentFeedObserver w tym przykładzie) ze środowiskiem uruchomieniowym.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-357">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with the runtime.</span></span> <span data-ttu-id="2c6fa-358">W tym momencie host podejmie próbę uzyskania dzierżawy na każdym zakresem kluczy partycji w kolekcji bazy danych rozwiązania Cosmos Azure za pomocą "zachłannego" algorytmu.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-358">At this point, the host attempts to acquire a lease on every partition key range in the Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="2c6fa-359">Te dzierżawy trwać przez dany przedział czasu, a następnie muszą być odnowione.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="2c6fa-360">Jak nowe węzły wystąpień procesów roboczych, w tym przypadku przejdzie w tryb online, one rezerwacje dzierżawy i wraz z upływem czasu ładowania Przenosi między węzłami jako każdy host próbuje uzyskać więcej dzierżaw.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time the load shifts between nodes as each host attempts to acquire more leases.</span></span> 

<span data-ttu-id="2c6fa-361">W przykładowym kodzie używamy klasę fabryki (DocumentFeedObserverFactory.cs) do utworzenia obserwatora i `RegistObserverFactoryAsync` zarejestrować obserwatora.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-361">In the sample code, we use a factory class (DocumentFeedObserverFactory.cs) to create an observer and the `RegistObserverFactoryAsync` to register the observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="2c6fa-362">W miarę upływu czasu zostaje ustalona równowaga.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="2c6fa-363">Ta dynamiczna funkcja umożliwia Procesora na podstawie automatycznego skalowania ma zostać zastosowany do konsumentów do skalowania w górę i w dół.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-363">This dynamic capability enables CPU-based auto-scaling to be applied to consumers for both scale-up and scale-down.</span></span> <span data-ttu-id="2c6fa-364">Jeśli zmiany są dostępne w usłudze Azure DB rozwiązania Cosmos szybkością szybciej, niż odbiorcy mogą przetworzyć, zwiększenie użycia procesora CPU przez odbiorców może służyć do powodują automatyczne skalowanie liczby wystąpień procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="2c6fa-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c6fa-365">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2c6fa-365">Next steps</span></span>
* <span data-ttu-id="2c6fa-366">Spróbuj [Azure rozwiązania Cosmos DB zmiany źródła przykłady kodu w witrynie GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="2c6fa-366">Try the [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="2c6fa-367">Rozpoczynanie pracy kodowanie dzięki funkcjom [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md) lub [interfejsu API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="2c6fa-367">Get started coding with the [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
