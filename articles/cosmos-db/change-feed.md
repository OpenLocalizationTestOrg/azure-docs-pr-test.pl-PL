---
title: "aaaWorking hello zmiana źródła pomocy technicznej w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Bazy danych use Azure rozwiązania Cosmos zmiana źródła pomocy technicznej tootrack zmiany w dokumentach i wykonywać oparty na zdarzeniach przetwarzania, takich jak wyzwalaczy i aktualizowanie systemów pamięci podręcznych i analiza."
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
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="446f0-104">Praca z obsługą hello zmiany kanału informacyjnego w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="446f0-104">Working with hello change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="446f0-105">[Azure DB rozwiązania Cosmos](../cosmos-db/introduction.md) jest szybkie i elastyczne globalnie replikowane usługi bazy danych, która służy do przechowywania duże ilości danych transakcyjnych i działa z przewidywalną jednocyfrowej milisekundy opóźnienia dla operacji odczytu i zapisu.</span><span class="sxs-lookup"><span data-stu-id="446f0-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="446f0-106">Dzięki temu odpowiednie IoT gry detaliczna, i operacyjne rejestrowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="446f0-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="446f0-107">Typowe wzorzec projektowania w tych aplikacjach jest tootrack zmiany wykonane danych tooAzure rozwiązania Cosmos bazy danych i zaktualizuj zmaterializowanych widoków, wykonywanie analiz w czasie rzeczywistym, toocold danych archiwizowanie i powiadomienia wyzwalane na określone zdarzenia na podstawie tych zmian.</span><span class="sxs-lookup"><span data-stu-id="446f0-107">A common design pattern in these applications is tootrack changes made tooAzure Cosmos DB data, and update materialized views, perform real-time analytics, archive data toocold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="446f0-108">Witaj **zmiany źródła pomocy technicznej** w usłudze Azure DB rozwiązania Cosmos pozwala toobuild wydajne i skalowalne rozwiązania dla każdego z tych wzorców.</span><span class="sxs-lookup"><span data-stu-id="446f0-108">hello **change feed support** in Azure Cosmos DB enables you toobuild efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="446f0-109">W przypadku zmiany źródła pomocy technicznej bazy danych rozwiązania Cosmos Azure udostępnia posortowaną listę dokumentów w kolekcji bazy danych Azure rozwiązania Cosmos w kolejności hello, w którym zostały zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="446f0-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in hello order in which they were modified.</span></span> <span data-ttu-id="446f0-110">To źródło można toolisten używane dla toodata zmiany w kolekcji hello i wykonywać akcje, takie jak:</span><span class="sxs-lookup"><span data-stu-id="446f0-110">This feed can be used toolisten for modifications toodata within hello collection and perform actions such as:</span></span>

* <span data-ttu-id="446f0-111">Wyzwalanie tooan wywołania interfejsu API, gdy dokument zostanie wstawiony lub zmodyfikowany</span><span class="sxs-lookup"><span data-stu-id="446f0-111">Trigger a call tooan API when a document is inserted or modified</span></span>
* <span data-ttu-id="446f0-112">Podczas przetwarzania strumienia w czasie rzeczywistym () aktualizacji</span><span class="sxs-lookup"><span data-stu-id="446f0-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="446f0-113">Synchronizowanie danych z pamięci podręcznej, aparat wyszukiwania lub magazynu danych</span><span class="sxs-lookup"><span data-stu-id="446f0-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="446f0-114">Zmiany w usłudze Azure DB rozwiązania Cosmos są zachowywane mogą być przetwarzane asynchronicznie i dystrybuowana do co najmniej jeden konsumentów w celu równoległego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="446f0-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="446f0-115">Przyjrzyjmy się hello interfejsów API dla źródła danych zmian i używania ich toobuild skalowalnych aplikacji w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="446f0-115">Let's look at hello APIs for change feed and how you can use them toobuild scalable real-time applications.</span></span> <span data-ttu-id="446f0-116">W tym artykule opisano, jak toowork z bazy danych Azure rozwiązania Cosmos zmienić źródła danych i hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="446f0-116">This article shows how toowork with Azure Cosmos DB change feed and hello DocumentDB API.</span></span> 

![Przy użyciu bazy danych Azure rozwiązania Cosmos zmiany źródła danych, analiz w czasie rzeczywistym toopower i scenariuszach obliczeniowych o sterowane zdarzeniami](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="446f0-118">Zmiana źródła danych obsługi jest tworzony tylko dla hello interfejsu API usługi DocumentDB w tej chwili; Hello interfejsu API programu Graph i interfejsu API tabeli nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="446f0-118">Change feed support is only provided for hello DocumentDB API at this time; hello Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="446f0-119">Przypadki użycia i scenariusze</span><span class="sxs-lookup"><span data-stu-id="446f0-119">Use cases and scenarios</span></span>
<span data-ttu-id="446f0-120">Zmiana źródła umożliwia wydajne przetwarzania dużych zestawów danych z dużą liczbę operacji zapisu i oferuje alternatywne tooquerying tooidentify cały zestaw danych, co się zmieniło.</span><span class="sxs-lookup"><span data-stu-id="446f0-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative tooquerying entire datasets tooidentify what has changed.</span></span> <span data-ttu-id="446f0-121">Na przykład można wykonywać hello wydajnie następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="446f0-121">For example, you can perform hello following tasks efficiently:</span></span>

* <span data-ttu-id="446f0-122">Aktualizacji pamięci podręcznej, indeksu wyszukiwania lub magazynu danych z danych przechowywanych w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="446f0-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="446f0-123">Implementuje warstw i archiwizowania danych na poziomie aplikacji, oznacza to, przechowywać "gorących danych" w usłudze Azure DB rozwiązania Cosmos i przedawniają "zimnych danych" zbyt[magazyn obiektów Blob Azure](../storage/common/storage-introduction.md) lub [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="446f0-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" too[Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="446f0-124">Implementowanie analizach wsadowych na danych przy użyciu [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="446f0-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="446f0-125">Implementowanie [potoki lambda na platformie Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="446f0-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="446f0-126">Azure DB rozwiązania Cosmos zapewnia rozwiązanie skalowalne bazy danych, które można obsługiwać wprowadzanie i zapytań oraz implementował architektury lambda z niskim całkowitego kosztu posiadania.</span><span class="sxs-lookup"><span data-stu-id="446f0-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="446f0-127">Wykonaj zero tooanother czas przestoju migracji konta bazy danych Azure rozwiązania Cosmos z różnych schemat partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="446f0-127">Perform zero down-time migrations tooanother Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="446f0-128">**Potoki lambda z bazy danych rozwiązania Cosmos Azure wprowadzanie i zapytania:**</span><span class="sxs-lookup"><span data-stu-id="446f0-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Potok lambda wprowadzanie i zapytań na podstawie Azure DB rozwiązania Cosmos](./media/change-feed/lambda.png)

<span data-ttu-id="446f0-130">Użyj bazy danych Azure rozwiązania Cosmos tooreceive i przechowywania danych o zdarzeniach z urządzeń, czujników, infrastruktury i aplikacji oraz przetwarzania tych zdarzeń w czasie rzeczywistym za pomocą [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), lub [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="446f0-130">You can use Azure Cosmos DB tooreceive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="446f0-131">W ramach Twojej [niekorzystającą](http://azure.com/serverless) sieci web i aplikacji mobilnych, można Śledź zdarzenia, takie jak zmiany tooyour klienta tootrigger profilu, preferencje lub lokalizacji pewne akcje, takie jak wysyłanie powiadomień tootheir urządzeń przy użyciu wypychania[Usługę azure Functions](../azure-functions/functions-bindings-documentdb.md) lub [usługi aplikacji](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="446f0-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes tooyour customer's profile, preferences, or location tootrigger certain actions like sending push notifications tootheir devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="446f0-132">Jeśli używasz bazy danych Azure rozwiązania Cosmos toobuild gier, na przykład można używać zmiany tooimplement źródła strumieniowego w czasie rzeczywistym tablice wyników oparte na wyniki z gry ukończone.</span><span class="sxs-lookup"><span data-stu-id="446f0-132">If you're using Azure Cosmos DB toobuild a game, you can, for example, use change feed tooimplement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="446f0-133">Jak działa zmiany źródła danych w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="446f0-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="446f0-134">Azure DB rozwiązania Cosmos zawiera hello tooincrementally możliwości odczytu tooan aktualizacji bazy danych Azure rozwiązania Cosmos kolekcji.</span><span class="sxs-lookup"><span data-stu-id="446f0-134">Azure Cosmos DB provides hello ability tooincrementally read updates made tooan Azure Cosmos DB collection.</span></span> <span data-ttu-id="446f0-135">To źródło zmiany ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="446f0-135">This change feed has hello following properties:</span></span>

* <span data-ttu-id="446f0-136">Zmiany są trwałe w usłudze Azure DB rozwiązania Cosmos i mogą być przetwarzane asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="446f0-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="446f0-137">Toodocuments zmiany w kolekcji są dostępne natychmiast w hello zmian w źródle strumieniowym.</span><span class="sxs-lookup"><span data-stu-id="446f0-137">Changes toodocuments within a collection are available immediately in hello change feed.</span></span>
* <span data-ttu-id="446f0-138">Każdy dokument tooa zmiany pojawią się dokładnie raz hello zmiany źródła i klienci zarządzania ich logiki tworzenie punktów kontrolnych.</span><span class="sxs-lookup"><span data-stu-id="446f0-138">Each change tooa document appears exactly once in hello change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="446f0-139">Biblioteka źródła procesora zmianami Hello zapewnia automatyczne tworzenie punktów kontrolnych i "co najmniej raz" semantyki.</span><span class="sxs-lookup"><span data-stu-id="446f0-139">hello change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="446f0-140">Tylko hello ostatniej zmiany w danym dokumencie znajduje się w dzienniku zmian hello.</span><span class="sxs-lookup"><span data-stu-id="446f0-140">Only hello most recent change for a given document is included in hello change log.</span></span> <span data-ttu-id="446f0-141">Pośrednie zmiany mogą nie być dostępne.</span><span class="sxs-lookup"><span data-stu-id="446f0-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="446f0-142">źródła danych zmian Hello jest sortowana numer modyfikacji w każdej wartości klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-142">hello change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="446f0-143">Brak nie gwarantuje kolejności między wartości klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="446f0-144">Zmiany mogą być synchronizowane z dowolnego punktu w czasie, oznacza to, że istnieje nie okres przechowywania danych, dla której zmiany są dostępne.</span><span class="sxs-lookup"><span data-stu-id="446f0-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="446f0-145">Zmiany są dostępne w fragmentów zakresami kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="446f0-146">Ta funkcja umożliwia zmiany w dużych kolekcjach toobe przetwarzane równolegle przez wielu użytkowników/serwerów.</span><span class="sxs-lookup"><span data-stu-id="446f0-146">This capability allows changes from large collections toobe processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="446f0-147">Aplikacje można żądanie zmiany wielu źródeł jednocześnie na powitania sam kolekcji.</span><span class="sxs-lookup"><span data-stu-id="446f0-147">Applications can request for multiple change feeds simultaneously on hello same collection.</span></span>

<span data-ttu-id="446f0-148">Azure DB rozwiązania Cosmos zmiany źródła jest domyślnie włączona dla wszystkich kont.</span><span class="sxs-lookup"><span data-stu-id="446f0-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="446f0-149">Można użyć programu [udostępnionej przepływności](request-units.md) w Twoim regionie zapisu lub w dowolnej [odczytu region](distribute-data-globally.md) tooread z hello zmienić źródła danych, podobnie jak inne operacje z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="446f0-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) tooread from hello change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="446f0-150">źródła danych zmian Hello obejmuje wstawienia i operacje aktualizacji toodocuments w kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="446f0-150">hello change feed includes inserts and update operations made toodocuments within hello collection.</span></span> <span data-ttu-id="446f0-151">Można przechwycić usuwa przez ustawienie w dokumentach zamiast usuwa flagę "soft-delete".</span><span class="sxs-lookup"><span data-stu-id="446f0-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="446f0-152">Alternatywnie, można ustawić okresu wygaśnięcia skończoną dla dokumentów za pomocą hello [możliwości TTL](time-to-live.md), na przykład, 24 godzin i użycie hello wartość tej właściwości usuwa toocapture.</span><span class="sxs-lookup"><span data-stu-id="446f0-152">Alternatively, you can set a finite expiration period for your documents via hello [TTL capability](time-to-live.md), for example, 24 hours and use hello value of that property toocapture deletes.</span></span> <span data-ttu-id="446f0-153">W tym rozwiązaniu masz tooprocess zmiany w określonym czasie krótszy niż okres ważności TTL hello.</span><span class="sxs-lookup"><span data-stu-id="446f0-153">With this solution, you have tooprocess changes within a shorter time interval than hello TTL expiration period.</span></span> <span data-ttu-id="446f0-154">źródła danych zmian Hello jest dostępna dla każdego zakresu klucza partycji w obrębie kolekcji dokumentów hello i w związku z tym mogą być rozproszone na co najmniej jeden konsumentów w celu równoległego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="446f0-154">hello change feed is available for each partition key range within hello document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Przetwarzanie rozproszone zmiany bazy danych Azure rozwiązania Cosmos źródła danych](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="446f0-156">Istnieje kilka opcji w sposobu implementacji zmiany źródła danych w kodzie klienta.</span><span class="sxs-lookup"><span data-stu-id="446f0-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="446f0-157">Witaj sekcje, które natychmiast wykonaj opisano sposób tooimplement hello zmiany źródła danych przy użyciu interfejsu API REST Azure rozwiązania Cosmos DB hello i hello zestawów SDK usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="446f0-157">hello sections that immediately follow describe how tooimplement hello change feed using hello Azure Cosmos DB REST API and hello DocumentDB SDKs.</span></span> <span data-ttu-id="446f0-158">Jednak dla aplikacji .NET, firma Microsoft zaleca używanie hello nowe [zmiany źródła danych biblioteki procesora](#change-feed-processor) przetwarzanie zdarzeń z hello zmian źródła danych, upraszcza odczytu zmiany na partycje i umożliwia wiele wątków Praca równoległe.</span><span class="sxs-lookup"><span data-stu-id="446f0-158">However, for .NET applications, we recommend using hello new [Change feed processor library](#change-feed-processor) for processing events from hello change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="446f0-159"><a id="rest-apis"></a>Praca z hello interfejsu API REST i zestawy SDK usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="446f0-159"><a id="rest-apis"></a>Working with hello REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="446f0-160">Azure DB rozwiązania Cosmos zapewnia elastyczne kontenery magazynu i przepustowości o nazwie **kolekcji**.</span><span class="sxs-lookup"><span data-stu-id="446f0-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="446f0-161">Przy użyciu logicznie pogrupowane danych w kolekcjach [kluczy partycji](partition-data.md) na skalowalność i wydajność.</span><span class="sxs-lookup"><span data-stu-id="446f0-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="446f0-162">Azure DB rozwiązania Cosmos udostępnia różne interfejsy API do uzyskiwania dostępu do tych danych, tym wyszukiwanie według Identyfikatora (odczyt/Get), kwerendy i odczytu źródła danych (skanowania).</span><span class="sxs-lookup"><span data-stu-id="446f0-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="446f0-163">Witaj zmiany źródła danych można uzyskać za wypełnianie dwa nowe toohello nagłówki żądania usługi DocumentDB `ReadDocumentFeed` interfejsu API i mogą być przetwarzane równolegle w zakresach kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-163">hello change feed can be obtained by populating two new request headers toohello DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="446f0-164">ReadDocumentFeed interfejsu API</span><span class="sxs-lookup"><span data-stu-id="446f0-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="446f0-165">Spójrzmy krótki opis działania ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="446f0-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="446f0-166">Obsługuje bazę danych systemu Azure rozwiązania Cosmos czytania źródła dokumentów w kolekcji za pomocą hello `ReadDocumentFeed` interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="446f0-166">Azure Cosmos DB supports reading a feed of documents within a collection via hello `ReadDocumentFeed` API.</span></span> <span data-ttu-id="446f0-167">Na przykład hello następujące żądania zwraca stronę dokumenty wewnątrz hello `serverlogs` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="446f0-167">For example, hello following request returns a page of documents inside hello `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="446f0-168">Wyniki mogą być ograniczone za pomocą hello `x-ms-max-item-count` nagłówka i odczytuje można wznowić, stosując Prześlij żądanie hello `x-ms-continuation` nagłówka zwracane w hello poprzedniej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="446f0-168">Results can be limited by using hello `x-ms-max-item-count` header, and reads can be resumed by resubmitting hello request with a `x-ms-continuation` header returned in hello previous response.</span></span> <span data-ttu-id="446f0-169">Gdy wykonywane z jednego klienta, `ReadDocumentFeed` iteruje wyników na partycje pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="446f0-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="446f0-170">**Seryjne odczytu dokumentu źródła danych**</span><span class="sxs-lookup"><span data-stu-id="446f0-170">**Serial read document feed**</span></span>

<span data-ttu-id="446f0-171">Można również pobierać kanału informacyjnego hello dokumentów przy użyciu jednego z obsługiwanych hello [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="446f0-171">You can also retrieve hello feed of documents using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="446f0-172">Na przykład powitania po fragment kodu przedstawia sposób toouse hello [metody ReadDocumentFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) w .NET.</span><span class="sxs-lookup"><span data-stu-id="446f0-172">For example, hello following snippet shows how toouse hello [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="446f0-173">Rozproszonego wykonywania ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="446f0-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="446f0-174">Dla kolekcji, które zawierają terabajtów danych lub więcej lub pozyskiwania dużą liczbę aktualizacji serial wykonywanie odczytu źródła danych z maszyny jednego klienta może nie być praktyczne.</span><span class="sxs-lookup"><span data-stu-id="446f0-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="446f0-175">W kolejności toosupport tych scenariuszy danych big data rozwiązania Cosmos Azure DB udostępnia interfejsy API toodistribute `ReadDocumentFeed` wywołania niewidocznie przez wielu klientów czytników klientów.</span><span class="sxs-lookup"><span data-stu-id="446f0-175">In order toosupport these big data scenarios, Azure Cosmos DB provides APIs toodistribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="446f0-176">**Źródło dokumentu odczytu rozproszonych**</span><span class="sxs-lookup"><span data-stu-id="446f0-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="446f0-177">skalowalne przetwarzania tooprovide zmiany przyrostowe rozwiązania Cosmos Azure DB obsługuje model skalowalnego w poziomie dla hello zmiany źródła danych na podstawie zakresów kluczy partycji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="446f0-177">tooprovide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for hello change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="446f0-178">Można uzyskać listę partycji zakresami kluczy do wykonywania kolekcji `ReadPartitionKeyRanges` wywołania.</span><span class="sxs-lookup"><span data-stu-id="446f0-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="446f0-179">Dla każdego zakresu klucza partycji można wykonywać `ReadDocumentFeed` tooread dokumentów za pomocą kluczy partycji w ramach tego zakresu.</span><span class="sxs-lookup"><span data-stu-id="446f0-179">For each partition key range, you can perform a `ReadDocumentFeed` tooread documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="446f0-180">Pobieranie zakresów klucza partycji dla kolekcji</span><span class="sxs-lookup"><span data-stu-id="446f0-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="446f0-181">Możesz pobrać zakresami kluczy partycji hello żądania hello `pkranges` zasobów w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="446f0-181">You can retrieve hello partition key ranges by requesting hello `pkranges` resource within a collection.</span></span> <span data-ttu-id="446f0-182">Na przykład hello następujące żądania pobiera listę hello zakresy klucza partycji dla hello `serverlogs` kolekcji:</span><span class="sxs-lookup"><span data-stu-id="446f0-182">For example hello following request retrieves hello list of partition key ranges for hello `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="446f0-183">To żądanie zwraca powitania po odpowiedzi zawierający metadane o zakresach klucza partycji hello:</span><span class="sxs-lookup"><span data-stu-id="446f0-183">This request returns hello following response containing metadata about hello partition key ranges:</span></span>

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


<span data-ttu-id="446f0-184">**Właściwości zakresu klucza partycji**: każdego zakresem kluczy partycji zawiera właściwości metadanych hello w hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="446f0-184">**Partition key range properties**: Each partition key range includes hello metadata properties in hello following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="446f0-185">Nazwa nagłówka</span><span class="sxs-lookup"><span data-stu-id="446f0-185">Header name</span></span></th>
        <th><span data-ttu-id="446f0-186">Opis</span><span class="sxs-lookup"><span data-stu-id="446f0-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-187">id</span><span class="sxs-lookup"><span data-stu-id="446f0-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="446f0-188">Identyfikator Hello hello zakresem kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-188">hello ID for hello partition key range.</span></span> <span data-ttu-id="446f0-189">To jest stabilna i unikatowy identyfikator w ramach każdej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="446f0-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="446f0-190">Musi być używane w hello następujące zmiany tooread wywołanie przez zakresem kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-190">Must be used in hello following call tooread changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="446f0-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="446f0-192">Hello wartość skrótu klucza partycji maksymalną hello zakresem kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-192">hello maximum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="446f0-193">Do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="446f0-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="446f0-194">minInclusive</span></span></td>
        <td><span data-ttu-id="446f0-195">Hello wartość skrótu klucza partycji minimalna hello zakresem kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-195">hello minimum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="446f0-196">Do użytku wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="446f0-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="446f0-197">Można to zrobić przy użyciu jednego z obsługiwanych hello [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="446f0-197">You can do this using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="446f0-198">Na przykład hello poniższy fragment kodu przedstawia sposób tooretrieve klucza partycji z zakresów w .NET przy użyciu hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) metody.</span><span class="sxs-lookup"><span data-stu-id="446f0-198">For example, hello following snippet shows how tooretrieve partition key ranges in .NET using hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="446f0-199">Azure DB rozwiązania Cosmos obsługuje pobierania dokumentów na zakresem kluczy partycji przez ustawienie opcjonalne hello `x-ms-documentdb-partitionkeyrangeid` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="446f0-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting hello optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="446f0-200">Wykonywanie przyrostowych ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="446f0-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="446f0-201">ReadDocumentFeed obsługuje następujące scenariusze/zadań przetwarzania przyrostowe zmiany w kolekcjach bazy danych Azure rozwiązania Cosmos hello:</span><span class="sxs-lookup"><span data-stu-id="446f0-201">ReadDocumentFeed supports hello following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="446f0-202">Odczyt wszystkich zmienia toodocuments od początku hello, czyli tworzenia kolekcji.</span><span class="sxs-lookup"><span data-stu-id="446f0-202">Read all changes toodocuments from hello beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="446f0-203">Odczyt wszystkich zmienia toodocuments aktualizacje toofuture bieżący czas lub wszelkie zmiany od czasu określonego przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="446f0-203">Read all changes toofuture updates toodocuments from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="446f0-204">Odczyt wszystkich zmienia toodocuments logicznej wersji hello kolekcji (ETag).</span><span class="sxs-lookup"><span data-stu-id="446f0-204">Read all changes toodocuments from a logical version of hello collection (ETag).</span></span> <span data-ttu-id="446f0-205">Możesz punktu kontrolnego przez użytkowników oparte na powitania zwrócony element ETag z przyrostowych żądań odczytu źródła.</span><span class="sxs-lookup"><span data-stu-id="446f0-205">You can checkpoint your consumers based on hello returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="446f0-206">Witaj zmiany obejmują toodocuments INSERT i Update.</span><span class="sxs-lookup"><span data-stu-id="446f0-206">hello changes include inserts and updates toodocuments.</span></span> <span data-ttu-id="446f0-207">Usuwa toocapture, należy użyć właściwości "usuwania nietrwałego" w dokumencie lub użyć hello [wbudowanych właściwości TTL](time-to-live.md) toosignal Oczekujące usunięcie w hello zmienić źródła danych.</span><span class="sxs-lookup"><span data-stu-id="446f0-207">toocapture deletes, you must use a "soft delete" property within your documents, or use hello [built-in TTL property](time-to-live.md) toosignal a pending deletion in hello change feed.</span></span>

<span data-ttu-id="446f0-208">Witaj następujących hello list tabeli [żądania](/rest/api/documentdb/common-documentdb-rest-request-headers.md) i [nagłówki odpowiedzi](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed operacji.</span><span class="sxs-lookup"><span data-stu-id="446f0-208">hello following table lists hello [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="446f0-209">**Nagłówki żądań dla przyrostowych ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="446f0-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="446f0-210">Nazwa nagłówka</span><span class="sxs-lookup"><span data-stu-id="446f0-210">Header name</span></span></th>
        <th><span data-ttu-id="446f0-211">Opis</span><span class="sxs-lookup"><span data-stu-id="446f0-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-212">WIADOMOŚCI BŁYSKAWICZNYCH A</span><span class="sxs-lookup"><span data-stu-id="446f0-212">A-IM</span></span></td>
        <td><span data-ttu-id="446f0-213">Musi być ustawiona zbyt "Przyrostowe źródła danych", lub pominięta, w przeciwnym razie</span><span class="sxs-lookup"><span data-stu-id="446f0-213">Must be set too"Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="446f0-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="446f0-215">Brak nagłówka: zwraca wszystkie zmiany z powitania od (kolekcja tworzenia)</span><span class="sxs-lookup"><span data-stu-id="446f0-215">No header: returns all changes from hello beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="446f0-216">"*": zwraca wszystkie nowe toodata zmiany w kolekcji hello</span><span class="sxs-lookup"><span data-stu-id="446f0-216">"*": returns all new changes toodata within hello collection</span></span></p>         
            <p><span data-ttu-id="446f0-217">&lt;Element etag&gt;: Jeśli ustawić kolekcji tooa ETag, zwraca wszystkie zmiany wprowadzone od momentu ten znacznik logiczne</span><span class="sxs-lookup"><span data-stu-id="446f0-217">&lt;etag&gt;: If set tooa collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="446f0-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="446f0-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="446f0-219">Format czasu RFC 1123; ignorowane, jeśli If-None-Match został określony.</span><span class="sxs-lookup"><span data-stu-id="446f0-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="446f0-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="446f0-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="446f0-221">Witaj identyfikator zakresem kluczy partycji do odczytywania danych.</span><span class="sxs-lookup"><span data-stu-id="446f0-221">hello partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="446f0-222">**Nagłówki odpowiedzi dla przyrostowych ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="446f0-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="446f0-223">Nazwa nagłówka</span><span class="sxs-lookup"><span data-stu-id="446f0-223">Header name</span></span></th>
        <th><span data-ttu-id="446f0-224">Opis</span><span class="sxs-lookup"><span data-stu-id="446f0-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-225">Element etag</span><span class="sxs-lookup"><span data-stu-id="446f0-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="446f0-226">numer sekwencyjny logicznej Hello (LSN) ostatniego dokumentu zwracany w odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="446f0-226">hello logical sequence number (LSN) of last document returned in hello response.</span></span></p>
            <p><span data-ttu-id="446f0-227">Przy ponownym przesłaniem tej wartości w If-None-Match można wznawiać ReadDocumentFeed przyrostowe.</span><span class="sxs-lookup"><span data-stu-id="446f0-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="446f0-228">Poniżej przedstawiono przykładowe żądanie tooreturn wszystkie przyrostowe zmiany w kolekcji z wersji logicznej hello/ETag `28535` i zakresem kluczy partycji = `16`:</span><span class="sxs-lookup"><span data-stu-id="446f0-228">Here's a sample request tooreturn all incremental changes in collection from hello logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="446f0-229">Zmiany są uporządkowane według czasu w każdej wartości klucza partycji w hello zakresem kluczy partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-229">Changes are ordered by time within each partition key value within hello partition key range.</span></span> <span data-ttu-id="446f0-230">Brak nie gwarantuje kolejności między wartości klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="446f0-231">W przypadku więcej wyników niż można zmieścić w jednej stronie można uzyskać hello następnej strony wyników Prześlij żądanie hello hello `If-None-Match` nagłówek o wartość równa toohello `etag` z hello poprzedniej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="446f0-231">If there are more results than can fit in a single page, you can read hello next page of results by resubmitting hello request with hello `If-None-Match` header with value equal toohello `etag` from hello previous response.</span></span> <span data-ttu-id="446f0-232">Wiele dokumentów zostały wstawione lub zaktualizowane transakcyjnie, w ramach procedury składowanej lub wyzwalacza, ich zostaną wszystkie zwrócone w hello sama strona odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="446f0-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within hello same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="446f0-233">Z zmian w źródle danych może spowodować, że więcej elementów zwróconych na stronie, niż określa `x-ms-max-item-count` w przypadku hello wielu dokumentów wstawiane lub aktualizowane w ramach procedur składowanych lub wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="446f0-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in hello case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="446f0-234">Korzystając z hello zestawu .NET SDK (1.17.0), ustaw pole hello `StartTime` w `ChangeFeedOptions` dokumenty toodirectly zwracany zmienione od czasu `StartTime` podczas wywoływania metody `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="446f0-234">When using hello .NET SDK (1.17.0), set hello field `StartTime` in `ChangeFeedOptions` toodirectly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="446f0-235">Określając `If-Modified-Since` przy użyciu interfejsu API REST hello, żądanie będzie zwracać nie hello dokumentów samodzielnie, ale raczej token kontynuacji hello lub `etag` hello nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="446f0-235">By specifying `If-Modified-Since` using hello REST API, your request will return not hello documents themselves, but rather hello continuation token or `etag` in hello response header.</span></span> <span data-ttu-id="446f0-236">dokumenty hello tooreturn zmodyfikowane hello określony czas, token kontynuacji hello `etag` musi być następnie używane w następnym żądaniu hello z `If-None-Match` tooreturn hello rzeczywiste dokumentów.</span><span class="sxs-lookup"><span data-stu-id="446f0-236">tooreturn hello documents modified hello specified time, hello continuation token `etag` must then be used in hello next request with `If-None-Match` tooreturn hello actual documents.</span></span> 

<span data-ttu-id="446f0-237">Witaj zestawu .NET SDK udostępnia hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) i [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) tooaccess zmiany kolekcji tooa klas pomocy.</span><span class="sxs-lookup"><span data-stu-id="446f0-237">hello .NET SDK provides hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes tooaccess changes made tooa collection.</span></span> <span data-ttu-id="446f0-238">Hello poniższy fragment kodu przedstawia sposób tooretrieve wszystkie zmiany od początku hello przy użyciu hello zestawu .NET SDK z jednego klienta.</span><span class="sxs-lookup"><span data-stu-id="446f0-238">hello following snippet shows how tooretrieve all changes from hello beginning using hello .NET SDK from a single client.</span></span>

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
<span data-ttu-id="446f0-239">I hello poniższy fragment kodu przedstawia sposób tooprocess zmienia się w czasie rzeczywistym z bazy danych rozwiązania Cosmos Azure przy użyciu hello zmiany źródła pomocy technicznej i hello poprzedzających funkcji.</span><span class="sxs-lookup"><span data-stu-id="446f0-239">And hello following snippet shows how tooprocess changes in real-time with Azure Cosmos DB by using hello change feed support and hello preceding function.</span></span> <span data-ttu-id="446f0-240">pierwsze wywołanie Hello zwraca wszystkie dokumenty hello w kolekcji hello, natomiast hello drugi tylko hello dwa dokumenty utworzone utworzonych od czasu ostatniego punktu kontrolnego hello.</span><span class="sxs-lookup"><span data-stu-id="446f0-240">hello first call returns all hello documents in hello collection, and hello second only returns hello two documents created that were created since hello last checkpoint.</span></span>

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="446f0-241">Można również filtrować hello zmiany źródła przy użyciu zdarzeń procesu tooselectively logiki po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="446f0-241">You can also filter hello change feed using client side logic tooselectively process events.</span></span> <span data-ttu-id="446f0-242">Na przykład poniżej przedstawiono fragment kodu, który używa tooprocess LINQ po stronie klienta, tylko zdarzenia zmian temperatury z czujników urządzenia.</span><span class="sxs-lookup"><span data-stu-id="446f0-242">For example, here's a snippet that uses client side LINQ tooprocess only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="446f0-243"><a id="change-feed-processor"></a>Zmiana źródła procesora biblioteki</span><span class="sxs-lookup"><span data-stu-id="446f0-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="446f0-244">Innym rozwiązaniem jest toouse hello [biblioteki Azure rozwiązania Cosmos DB zmienić źródła procesora](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), który pomoże Ci łatwo rozpowszechniaj przetwarzania ze źródła danych w wielu klientów zmiany zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="446f0-244">Another option is toouse hello [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="446f0-245">Biblioteka Hello stanowi doskonałe rozwiązanie do tworzenia zmiany na platformie .NET hello źródła danych czytników.</span><span class="sxs-lookup"><span data-stu-id="446f0-245">hello library is great for building change feed readers on hello .NET platform.</span></span> <span data-ttu-id="446f0-246">Niektóre przepływy pracy, które może uprościć przy użyciu biblioteki procesora źródła danych zmian hello za pośrednictwem metody hello zawarte w hello innych zestawów SDK DB rozwiązania Cosmos obejmują:</span><span class="sxs-lookup"><span data-stu-id="446f0-246">Some workflows that would be simplified by using hello Change Feed Processor library over hello methods included in hello other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="446f0-247">Ściągania aktualizacji z zmiany źródła danych, gdy dane są przechowywane w wielu partycji</span><span class="sxs-lookup"><span data-stu-id="446f0-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="446f0-248">Przenoszenie lub replikowanie danych z jednej kolekcji tooanother</span><span class="sxs-lookup"><span data-stu-id="446f0-248">Moving or replicating data from one collection tooanother</span></span>
* <span data-ttu-id="446f0-249">Równoległe wykonywanie akcji wyzwalane przez toodata aktualizacji i zmian źródła danych</span><span class="sxs-lookup"><span data-stu-id="446f0-249">Parallel execution of actions triggered by updates toodata and change feed</span></span> 

<span data-ttu-id="446f0-250">Przy użyciu hello interfejsów API w hello rozwiązania Cosmos zestawów SDK zawiera toochange dokładne dostępu podawania aktualizacje w każdej partycji, natomiast przy użyciu biblioteki procesora źródła danych zmian hello upraszcza odczytu zmiany na partycje i wiele wątków działające równolegle.</span><span class="sxs-lookup"><span data-stu-id="446f0-250">While using hello APIs in hello Cosmos SDKs provides precise access toochange feed updates in each partition, using hello Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="446f0-251">Zamiast ręcznego odczytywać zmian z każdego kontenera i zapisywać token kontynuacji dla każdej partycji hello procesora źródła danych zmian automatycznie zarządza odczytu zmiany na partycje przy użyciu mechanizmu dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="446f0-251">Instead of manually reading changes from each container and saving a continuation token for each partition, hello Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="446f0-252">Biblioteka Hello jest dostępna jako pakietu NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) i z kodu źródłowego jako Github [próbki](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="446f0-252">hello library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="446f0-253">Opis zmiany procesora źródła danych biblioteki</span><span class="sxs-lookup"><span data-stu-id="446f0-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="446f0-254">Istnieją cztery główne składniki wdrażania hello zmiany źródła procesora: hello monitorowane kolekcji, kolekcji dzierżawy hello hello procesora hosta i hello konsumentów.</span><span class="sxs-lookup"><span data-stu-id="446f0-254">There are four main components of implementing hello Change Feed Processor: hello monitored collection, hello lease collection, hello processor host, and hello consumers.</span></span> 

<span data-ttu-id="446f0-255">**Kolekcja monitorowanych:** kolekcja hello monitorowane jest hello danych, z których hello jest generowany zmiany źródła danych.</span><span class="sxs-lookup"><span data-stu-id="446f0-255">**Monitored Collection:** hello monitored collection is hello data from which hello change feed is generated.</span></span> <span data-ttu-id="446f0-256">Kolekcji toohello monitorowane wstawienia i zmiany zostaną odzwierciedlone w źródło danych zmiany hello hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="446f0-256">Any inserts and changes toohello monitored collection are reflected in hello change feed of hello collection.</span></span> 

<span data-ttu-id="446f0-257">**Kolekcja dzierżawy:** hello współrzędne kolekcji dzierżawy przetwarzania zmian hello źródła danych w wielu pracowników.</span><span class="sxs-lookup"><span data-stu-id="446f0-257">**Lease Collection:** hello lease collection coordinates processing hello change feed across multiple workers.</span></span> <span data-ttu-id="446f0-258">Oddzielne kolekcja jest używana toostore hello dzierżawy jednej dzierżawy dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-258">A separate collection is used toostore hello leases with one lease per partition.</span></span> <span data-ttu-id="446f0-259">Jest korzystne toostore tej kolekcji dzierżawy na inne konto o hello zapisu region bliżej toowhere powitalne procesor źródła danych zmian jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="446f0-259">It is advantageous toostore this lease collection on a different account with hello write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="446f0-260">Obiekt dzierżawy zawiera hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="446f0-260">A lease object contains hello following attributes:</span></span> 
* <span data-ttu-id="446f0-261">Właściciel: Określa hello hosta, który jest właścicielem hello dzierżawy</span><span class="sxs-lookup"><span data-stu-id="446f0-261">Owner: Specifies hello host that owns hello lease</span></span>
* <span data-ttu-id="446f0-262">Kontynuacja: Określa położenie hello (token kontynuacji) w przypadku zmiany powitania dla określonej partycji</span><span class="sxs-lookup"><span data-stu-id="446f0-262">Continuation: Specifies hello position (continuation token) in hello change feed for a particular partition</span></span>
* <span data-ttu-id="446f0-263">Znacznik czasu: Czas ostatniego dzierżawy został zaktualizowany; Sygnatura czasowa Hello można toocheck używane dzierżawy hello jest uznawany za wygasły</span><span class="sxs-lookup"><span data-stu-id="446f0-263">Timestamp: Last time lease was updated; hello timestamp can be used toocheck whether hello lease is considered expired</span></span> 

<span data-ttu-id="446f0-264">**Host procesora:** każdy host Określa, ile tooprocess partycji na podstawie liczby wystąpień hostów mają aktywne dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="446f0-264">**Processor Host:** Each host determines how many partitions tooprocess based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="446f0-265">Po uruchomieniu hosta, uzyskuje dzierżawy toobalance hello obciążenia na wszystkich hostach.</span><span class="sxs-lookup"><span data-stu-id="446f0-265">When a host starts up, it acquires leases toobalance hello workload across all hosts.</span></span> <span data-ttu-id="446f0-266">Hosta okresowo odnowieniu dzierżawy, więc pozostaną aktywne dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="446f0-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="446f0-267">Host punkty kontrolne hello ostatniego kontynuacji tokenu tooits dzierżawy przy każdym odczycie.</span><span class="sxs-lookup"><span data-stu-id="446f0-267">A host checkpoints hello last continuation token tooits lease for each read.</span></span> <span data-ttu-id="446f0-268">tooensure współbieżności bezpieczeństwa, host sprawdza hello ETag dla każdej aktualizacji dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="446f0-268">tooensure concurrency safety, a host checks hello ETag for each lease update.</span></span> <span data-ttu-id="446f0-269">Obsługiwane są także inne strategie punktu kontrolnego.</span><span class="sxs-lookup"><span data-stu-id="446f0-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="446f0-270">Podczas zamykania systemu host zwalnia wszystkie dzierżawy, ale zachowuje hello kontynuacji informacji, aby go ponownie odczytu z punktu kontrolnego przechowywanych hello później.</span><span class="sxs-lookup"><span data-stu-id="446f0-270">Upon shutdown, a host releases all leases but keeps hello continuation information, so it can resume reading from hello stored checkpoint later.</span></span> 

<span data-ttu-id="446f0-271">W tym momencie hello liczby hostów nie może być większa niż liczba hello partycji (dzierżawy).</span><span class="sxs-lookup"><span data-stu-id="446f0-271">At this time hello number of hosts cannot be greater than hello number of partitions (leases).</span></span>

<span data-ttu-id="446f0-272">**Konsumenci:** użytkowników lub pracowników, są wątków, które przeprowadzić hello zmiany źródła przetwarzania inicjowane przez każdego hosta.</span><span class="sxs-lookup"><span data-stu-id="446f0-272">**Consumers:** Consumers, or workers, are threads that perform hello change feed processing initiated by each host.</span></span> <span data-ttu-id="446f0-273">Każdy host procesora może mieć wielu klientów.</span><span class="sxs-lookup"><span data-stu-id="446f0-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="446f0-274">Każdy odbiorca odczytuje hello zmiany źródła z hello partycji jest przypisany tooand powiadamia jej hosta zmian i ważność dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="446f0-274">Each consumer reads hello change feed from hello partition it is assigned tooand notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="446f0-275">toofurther zrozumieć, jak te cztery elementy procesora źródła danych zmian ze sobą współdziałać, Przyjrzyjmy się przykładem w powitania po diagramu.</span><span class="sxs-lookup"><span data-stu-id="446f0-275">toofurther understand how these four elements of Change Feed Processor work together, let's look at an example in hello following diagram.</span></span> <span data-ttu-id="446f0-276">Hello monitorowane kolekcji dokumentów magazynów i używa Miasto"hello" jako klucza partycji hello.</span><span class="sxs-lookup"><span data-stu-id="446f0-276">hello monitored collection stores documents and uses hello "city" as hello partition key.</span></span> <span data-ttu-id="446f0-277">Widzimy hello niebieski partycji i tak dalej zawiera dokumentów za pomocą pola "Miasto" hello "A-E".</span><span class="sxs-lookup"><span data-stu-id="446f0-277">We see that hello blue partition contains documents with hello "city" field from "A-E" and so on.</span></span> <span data-ttu-id="446f0-278">Istnieją dwa hosty, każda z dwóch konsumentów odczytu z partycji hello czterech równolegle.</span><span class="sxs-lookup"><span data-stu-id="446f0-278">There are two hosts, each with two consumers reading from hello four partitions in parallel.</span></span> <span data-ttu-id="446f0-279">Witaj strzałki oznaczają konsumentów hello czytania z określonego punktu w hello zmienić źródła danych.</span><span class="sxs-lookup"><span data-stu-id="446f0-279">hello arrows show hello consumers reading from a specific spot in hello change feed.</span></span> <span data-ttu-id="446f0-280">W pierwszej partycji hello blue ciemniejszego hello reprezentuje nieprzeczytana zmiany podczas hello koloru niebieskiego reprezentuje hello już odczytywać zmian na powitania zmiany źródła.</span><span class="sxs-lookup"><span data-stu-id="446f0-280">In hello first partition, hello darker blue represents unread changes while hello light blue represents hello already read changes on hello change feed.</span></span> <span data-ttu-id="446f0-281">hosty Hello używają hello dzierżawy kolekcji toostore track tookeep wartość "kontynuacji" hello bieżącego odczytywania położenia w przypadku każdego konsumenta.</span><span class="sxs-lookup"><span data-stu-id="446f0-281">hello hosts use hello lease collection toostore a "continuation" value tookeep track of hello current reading position for each consumer.</span></span> 

![Przy użyciu hello Azure DB rozwiązania Cosmos zmiany źródła danych hosta procesora](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="446f0-283">Przy użyciu zmian źródła danych biblioteki procesora</span><span class="sxs-lookup"><span data-stu-id="446f0-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="446f0-284">powitania po sekcji wyjaśniono, jak toouse hello biblioteki procesora źródła danych zmian w kontekście hello replikację zmian z kolekcji docelowej tooa kolekcji źródłowej.</span><span class="sxs-lookup"><span data-stu-id="446f0-284">hello following section explains how toouse hello Change Feed Processor library in hello context of replicating changes from a source collection tooa destination collection.</span></span> <span data-ttu-id="446f0-285">W tym miejscu hello kolekcji źródłowej jest kolekcją hello monitorowane w procesorze źródła danych zmian.</span><span class="sxs-lookup"><span data-stu-id="446f0-285">Here, hello source collection is hello monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="446f0-286">**Zainstaluj i zawierać pakiet NuGet procesora źródła danych zmian hello**</span><span class="sxs-lookup"><span data-stu-id="446f0-286">**Install and include hello Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="446f0-287">Przed zainstalowaniem pakietu NuGet procesora zmiany źródła danych należy najpierw zainstalować:</span><span class="sxs-lookup"><span data-stu-id="446f0-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="446f0-288">Microsoft.Azure.DocumentDB, wersja 1.13.1 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="446f0-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="446f0-289">Newtonsoft.Json, wersja 9.0.1 lub powyżej instalacji `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` i dołączyć go jako odwołanie.</span><span class="sxs-lookup"><span data-stu-id="446f0-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="446f0-290">**Utwórz kolekcję monitorowanych, dzierżawy i docelowego**</span><span class="sxs-lookup"><span data-stu-id="446f0-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="446f0-291">W kolejności toouse hello biblioteki procesora źródła danych zmian hello dzierżawy kolekcji musi mieć toobe utworzyć przed uruchomieniem hello procesora hostami.</span><span class="sxs-lookup"><span data-stu-id="446f0-291">In order toouse hello Change Feed Processor Library, hello lease collection needs toobe created before running hello processor host(s).</span></span> <span data-ttu-id="446f0-292">Zaleca się ponownie, przechowywania kolekcji dzierżawy na inne konto z zapisu region bliżej toowhere hello się, że procesor źródła danych zmian jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="446f0-292">Again, we recommend storing a lease collection on a different account with a write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="446f0-293">W tym przykładzie przepływu danych potrzebujemy kolekcji docelowej hello toocreate przed uruchomieniem hello zmiany źródła procesora hosta.</span><span class="sxs-lookup"><span data-stu-id="446f0-293">In this data movement example, we need toocreate hello destination collection before running hello Change Feed Processor host.</span></span> <span data-ttu-id="446f0-294">W hello przykładowy kod nazywamy hello toocreate metody pomocnika monitorowane, dzierżawy i kolekcji docelowej, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="446f0-294">In hello sample code we call a helper method toocreate hello monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="446f0-295">Tworzenie kolekcji ma cenę, jak są rezerwacji przepustowości dla toocommunicate aplikacji hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="446f0-295">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="446f0-296">Aby uzyskać więcej informacji, odwiedź stronę hello [stronie dotyczącej cen](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="446f0-296">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="446f0-297">*Tworzenie hosta procesora*</span><span class="sxs-lookup"><span data-stu-id="446f0-297">*Creating a processor host*</span></span>

<span data-ttu-id="446f0-298">Witaj `ChangeFeedProcessorHost` klasa udostępnia środowisko wątkowo, wieloprocesowe, bezpieczne środowisko uruchomieniowe dla implementacji procesora zdarzeń, które umożliwia także tworzenie punktów kontrolnych i zarządzanie dzierżawą partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-298">hello `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="446f0-299">Witaj toouse `ChangeFeedProcessorHost` klasy, można zaimplementować `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="446f0-299">toouse hello `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="446f0-300">Ten interfejs zawiera trzy metody:</span><span class="sxs-lookup"><span data-stu-id="446f0-300">This interface contains three methods:</span></span>

* <span data-ttu-id="446f0-301">`OpenAsync`: Ta funkcja jest wywoływana po otwarciu źródła obserwator zmiany.</span><span class="sxs-lookup"><span data-stu-id="446f0-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="446f0-302">Po otwarciu konsumenta/obserwatora może być zmodyfikowany tooperform określonej akcji.</span><span class="sxs-lookup"><span data-stu-id="446f0-302">It can be modified tooperform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="446f0-303">`CloseAsync`: Ta funkcja jest wywoływana, gdy zmiana źródła obserwator jest zakończony.</span><span class="sxs-lookup"><span data-stu-id="446f0-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="446f0-304">Po zamknięciu konsumenta/obserwatora może być zmodyfikowany tooperform określonej akcji.</span><span class="sxs-lookup"><span data-stu-id="446f0-304">It can be modified tooperform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="446f0-305">`ProcessChangesAsync`: Ta funkcja jest wywoływana, gdy nowe zmiany w dokumencie są dostępne na zmiany źródła danych.</span><span class="sxs-lookup"><span data-stu-id="446f0-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="446f0-306">Może być zmodyfikowany tooperform określonej akcji po każdej aktualizacji zmiany źródła danych.</span><span class="sxs-lookup"><span data-stu-id="446f0-306">It can be modified tooperform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="446f0-307">W naszym przykładzie mamy implementować interfejs hello `IChangeFeedObserver` za pośrednictwem hello `DocumentFeedObserver` klasy.</span><span class="sxs-lookup"><span data-stu-id="446f0-307">In our example, we implement hello interface `IChangeFeedObserver` through hello `DocumentFeedObserver` class.</span></span> <span data-ttu-id="446f0-308">W tym miejscu hello `ProcessChangesAsync` funkcji upserts (aktualizacje) do kolekcji docelowej hello strumieniowe źródło dokumentu z zmiany.</span><span class="sxs-lookup"><span data-stu-id="446f0-308">Here, hello `ProcessChangesAsync` function upserts (updates) a document from change feed into hello destination collection.</span></span> <span data-ttu-id="446f0-309">W tym przykładzie jest przydatna do przenoszenia danych z tooanother jednej kolekcji w kolejności toochange hello klucz partycji zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="446f0-309">This example is useful for moving data from one collection tooanother in order toochange hello partition key of a data set.</span></span> 

<span data-ttu-id="446f0-310">*Uruchomiona hello hosta procesora*</span><span class="sxs-lookup"><span data-stu-id="446f0-310">*Running hello Processor Host*</span></span>

<span data-ttu-id="446f0-311">Przed rozpoczęciem przetwarzania zdarzeń, zmień obie opcje źródła i zmień opcje hosta źródła strumieniowego można dostosować.</span><span class="sxs-lookup"><span data-stu-id="446f0-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="446f0-312">Witaj określonych pól, które można dostosowywać przedstawiono hello następujące tabele.</span><span class="sxs-lookup"><span data-stu-id="446f0-312">hello specific fields that can be customized are summarized in hello following tables.</span></span> 

<span data-ttu-id="446f0-313">**Zmień opcje źródła**:</span><span class="sxs-lookup"><span data-stu-id="446f0-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="446f0-314">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="446f0-314">Property Name</span></span></th>
        <th><span data-ttu-id="446f0-315">Opis</span><span class="sxs-lookup"><span data-stu-id="446f0-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="446f0-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="446f0-317">Pobiera lub ustawia maksymalną liczbę elementów toobe zwracane w operacji wyliczania hello w hello Azure DB rozwiązania Cosmos bazy danych usługi hello.</span><span class="sxs-lookup"><span data-stu-id="446f0-317">Gets or sets hello maximum number of items toobe returned in hello enumeration operation in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="446f0-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="446f0-319">Pobiera lub ustawia identyfikator zakresem kluczy partycji powitania dla bieżącego żądania hello hello Azure DB rozwiązania Cosmos bazy danych usługi.</span><span class="sxs-lookup"><span data-stu-id="446f0-319">Gets or sets hello partition key range id for hello current request in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="446f0-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="446f0-321">Pobiera lub ustawia token kontynuacji żądania hello hello Azure DB rozwiązania Cosmos bazy danych usługi.</span><span class="sxs-lookup"><span data-stu-id="446f0-321">Gets or sets hello request continuation token in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="446f0-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="446f0-322">SessionToken</span></span></td>
        <td><span data-ttu-id="446f0-323">Pobiera lub ustawia hello tokenu sesji do użycia z spójność sesji w hello Azure DB rozwiązania Cosmos usługi bazy danych.</span><span class="sxs-lookup"><span data-stu-id="446f0-323">Gets or sets hello session token for use with session consistency in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="446f0-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="446f0-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="446f0-325">Pobiera lub ustawia, czy zmiany źródła danych w usłudze baza danych bazy danych Azure rozwiązania Cosmos hello powinna zaczynać się z powitania od (true) lub bieżący (false).</span><span class="sxs-lookup"><span data-stu-id="446f0-325">Gets or sets whether change feed in hello Azure Cosmos DB database service should start from hello beginning (true) or from current (false).</span></span> <span data-ttu-id="446f0-326">Domyślnie rozpoczyna się od bieżącego (false).</span><span class="sxs-lookup"><span data-stu-id="446f0-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="446f0-327">**Zmień opcje hosta źródła**:</span><span class="sxs-lookup"><span data-stu-id="446f0-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="446f0-328">Nazwa właściwości</span><span class="sxs-lookup"><span data-stu-id="446f0-328">Property Name</span></span></th>
        <th><span data-ttu-id="446f0-329">Typ</span><span class="sxs-lookup"><span data-stu-id="446f0-329">Type</span></span></th>
        <th><span data-ttu-id="446f0-330">Opis</span><span class="sxs-lookup"><span data-stu-id="446f0-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="446f0-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="446f0-332">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="446f0-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="446f0-333">Interwał powitania dla wszystkich dzierżaw dla aktualnie utrzymywane przez wystąpienie ChangeFeedEventHost hello partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-333">hello interval for all leases for partitions currently held by hello ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="446f0-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="446f0-335">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="446f0-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="446f0-336">Witaj tookick interwał poza toocompute zadań czy partycje są równomiernie rozłożone wystąpień znane hosta.</span><span class="sxs-lookup"><span data-stu-id="446f0-336">hello interval tookick off a task toocompute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="446f0-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="446f0-338">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="446f0-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="446f0-339">Interwał powitania, dla których hello dzierżawy jest wykonywana na dzierżawę reprezentujący partycji.</span><span class="sxs-lookup"><span data-stu-id="446f0-339">hello interval for which hello lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="446f0-340">Jeśli w tym przedziale czasu nie odnowieniu dzierżawy hello, wygasł i własność partycji hello przenosi tooanother ChangeFeedEventHost wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="446f0-340">If hello lease is not renewed within this interval, it is expired and ownership of hello partition moves tooanother ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="446f0-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="446f0-342">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="446f0-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="446f0-343">Witaj opóźnienia między sondowania partycji dla nowych zmian na powitania źródła danych, po opróżnione są wszystkie bieżące zmiany.</span><span class="sxs-lookup"><span data-stu-id="446f0-343">hello delay between polling a partition for new changes on hello feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="446f0-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="446f0-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="446f0-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="446f0-346">Witaj częstotliwość toocheckpoint dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="446f0-346">hello frequency toocheckpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="446f0-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="446f0-348">int</span><span class="sxs-lookup"><span data-stu-id="446f0-348">Int</span></span></td>
        <td><span data-ttu-id="446f0-349">Liczba partycji minimalna Hello hello hosta.</span><span class="sxs-lookup"><span data-stu-id="446f0-349">hello minimum partition count for hello host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="446f0-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="446f0-351">int</span><span class="sxs-lookup"><span data-stu-id="446f0-351">Int</span></span></td>
        <td><span data-ttu-id="446f0-352">Hello maksymalną liczbę partycji hello hostów mogą zostać użyte.</span><span class="sxs-lookup"><span data-stu-id="446f0-352">hello maximum number of partitions hello host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="446f0-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="446f0-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="446f0-354">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="446f0-354">Bool</span></span></td>
        <td><span data-ttu-id="446f0-355">Czy na powitania Uruchom hosta hello wszystkie istniejące dzierżawy, powinien zostać usunięty, a hello host należy rozpocząć od początku.</span><span class="sxs-lookup"><span data-stu-id="446f0-355">Whether on hello start of hello host all existing leases should be deleted and hello host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="446f0-356">przetwarzanie zdarzeń toostart wystąpienia `ChangeFeedProcessorHost`, podając odpowiednie parametry hello kolekcji bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="446f0-356">toostart event processing, instantiate `ChangeFeedProcessorHost`, providing hello appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="446f0-357">Następnie wywołaj metodę `RegisterObserverAsync` tooregister Twojego `IChangeFeedObserver` implementacji (DocumentFeedObserver w tym przykładzie) ze środowiskiem uruchomieniowym hello.</span><span class="sxs-lookup"><span data-stu-id="446f0-357">Then, call `RegisterObserverAsync` tooregister your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with hello runtime.</span></span> <span data-ttu-id="446f0-358">W tym momencie hello host prób tooacquire dzierżawy na każdym zakresem kluczy partycji w kolekcji bazy danych Azure rozwiązania Cosmos hello za pomocą "zachłannego" algorytmu.</span><span class="sxs-lookup"><span data-stu-id="446f0-358">At this point, hello host attempts tooacquire a lease on every partition key range in hello Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="446f0-359">Te dzierżawy trwać przez dany przedział czasu, a następnie muszą być odnowione.</span><span class="sxs-lookup"><span data-stu-id="446f0-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="446f0-360">Jak nowe węzły wystąpień procesów roboczych, w tym przypadku przejdzie w tryb online, ich rezerwacje dzierżawy i w czasie ładowania hello przewiduje między węzłami jako każdy host próby tooacquire więcej dzierżaw.</span><span class="sxs-lookup"><span data-stu-id="446f0-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time hello load shifts between nodes as each host attempts tooacquire more leases.</span></span> 

<span data-ttu-id="446f0-361">W przykładowym kodzie hello używamy toocreate klasy (DocumentFeedObserverFactory.cs) fabryki obserwatora i hello `RegistObserverFactoryAsync` tooregister hello obserwatora.</span><span class="sxs-lookup"><span data-stu-id="446f0-361">In hello sample code, we use a factory class (DocumentFeedObserverFactory.cs) toocreate an observer and hello `RegistObserverFactoryAsync` tooregister hello observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="446f0-362">W miarę upływu czasu zostaje ustalona równowaga.</span><span class="sxs-lookup"><span data-stu-id="446f0-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="446f0-363">Ta dynamiczna funkcja umożliwia dla systemów z procesorem CPU automatyczne skalowanie tooconsumers toobe stosowane do skalowania w górę i w dół.</span><span class="sxs-lookup"><span data-stu-id="446f0-363">This dynamic capability enables CPU-based auto-scaling toobe applied tooconsumers for both scale-up and scale-down.</span></span> <span data-ttu-id="446f0-364">Jeśli zmiany są dostępne w usłudze Azure DB rozwiązania Cosmos szybkością szybciej, niż odbiorcy mogą przetworzyć, hello zwiększenie użycia procesora CPU przez odbiorców może być używane toocause automatyczne skalowanie liczby wystąpień procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="446f0-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, hello CPU increase on consumers can be used toocause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="446f0-365">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="446f0-365">Next steps</span></span>
* <span data-ttu-id="446f0-366">Spróbuj hello [Azure rozwiązania Cosmos DB zmiany źródła przykłady kodu w witrynie GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="446f0-366">Try hello [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="446f0-367">Rozpoczynanie pracy kodowania z hello [zestawów SDK DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet.md) lub hello [interfejsu API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="446f0-367">Get started coding with hello [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
