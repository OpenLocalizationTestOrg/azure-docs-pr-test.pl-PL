---
title: "Azure DB rozwiązania Cosmos: Java usługi DocumentDB interfejsu API zestawu SDK i zasoby | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o hello interfejsu API języka Java i zestawu SDK, w tym daty wydania, daty wycofania i zmiany między poszczególnymi wersjami hello zestawu SDK Java usługi DocumentDB Azure rozwiązania Cosmos bazy danych."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="9db1c-103">Azure DB rozwiązania Cosmos: Zestawu SDK Java usługi DocumentDB informacje o wersji i zasoby</span><span class="sxs-lookup"><span data-stu-id="9db1c-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9db1c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="9db1c-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="9db1c-105">Źródła danych zmian .NET</span><span class="sxs-lookup"><span data-stu-id="9db1c-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="9db1c-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="9db1c-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="9db1c-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="9db1c-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="9db1c-108">Java</span><span class="sxs-lookup"><span data-stu-id="9db1c-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="9db1c-109">Python</span><span class="sxs-lookup"><span data-stu-id="9db1c-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="9db1c-110">REST</span><span class="sxs-lookup"><span data-stu-id="9db1c-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="9db1c-111">Dostawca zasobów REST</span><span class="sxs-lookup"><span data-stu-id="9db1c-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="9db1c-112">SQL</span><span class="sxs-lookup"><span data-stu-id="9db1c-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="9db1c-113">**Pobierz zestaw SDK**</span><span class="sxs-lookup"><span data-stu-id="9db1c-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="9db1c-114">Maven</span><span class="sxs-lookup"><span data-stu-id="9db1c-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="9db1c-115">**Dokumentacja interfejsu API**</span><span class="sxs-lookup"><span data-stu-id="9db1c-115">**API documentation**</span></span></td><td>[<span data-ttu-id="9db1c-116">Dokumentacji interfejsu API języka Java</span><span class="sxs-lookup"><span data-stu-id="9db1c-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="9db1c-117">**Współtworzenia tooSDK**</span><span class="sxs-lookup"><span data-stu-id="9db1c-117">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="9db1c-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="9db1c-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="9db1c-119">**Wprowadzenie**</span><span class="sxs-lookup"><span data-stu-id="9db1c-119">**Get started**</span></span></td><td>[<span data-ttu-id="9db1c-120">Rozpoczynanie pracy z hello zestawu Java SDK</span><span class="sxs-lookup"><span data-stu-id="9db1c-120">Get started with hello Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="9db1c-121">**Samouczek aplikacji sieci Web**</span><span class="sxs-lookup"><span data-stu-id="9db1c-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="9db1c-122">Tworzenie aplikacji sieci Web z bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="9db1c-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="9db1c-123">**Bieżącego środowiska uruchomieniowego obsługiwane**</span><span class="sxs-lookup"><span data-stu-id="9db1c-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="9db1c-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="9db1c-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="9db1c-125">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="9db1c-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="9db1c-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="9db1c-127">Dzieli toorequest krytycznych poprawek przetwarzania podczas partycji.</span><span class="sxs-lookup"><span data-stu-id="9db1c-127">Critical bug fixes toorequest processing during partition splits.</span></span>
* <span data-ttu-id="9db1c-128">Rozwiązano problem z hello silne i BoundedStaleness poziomy spójności.</span><span class="sxs-lookup"><span data-stu-id="9db1c-128">Fixed an issue with hello Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="9db1c-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="9db1c-130">Dodano obsługę nowego poziomu spójności o nazwie ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="9db1c-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="9db1c-131">Stałe błędów w kolekcji sesji w trybie odczytu.</span><span class="sxs-lookup"><span data-stu-id="9db1c-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="9db1c-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="9db1c-133">Włączona obsługa kolekcji partycjonowanych jako niskie jako 2500 RU/s i skalować z przyrostem 100 RU/s.</span><span class="sxs-lookup"><span data-stu-id="9db1c-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="9db1c-134">Rozwiązane usterki w hello natywny zestaw, co może spowodować wyjątek NullRef niektórych kwerend.</span><span class="sxs-lookup"><span data-stu-id="9db1c-134">Fixed a bug in hello native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="9db1c-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="9db1c-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="9db1c-136">Stała usterki w hello zapytań aparatu konfiguracji, które mogą powodować wyjątki dla zapytań w trybie bramy.</span><span class="sxs-lookup"><span data-stu-id="9db1c-136">Fixed a bug in hello query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="9db1c-137">Stałe kilka błędów w kontenerze hello sesji, która może spowodować wyjątek "Nie można odnaleźć zasobu właściciela" żądań natychmiast po utworzeniu kolekcji.</span><span class="sxs-lookup"><span data-stu-id="9db1c-137">Fixed a few bugs in hello session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="9db1c-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="9db1c-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="9db1c-139">Dodano obsługę zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.).</span><span class="sxs-lookup"><span data-stu-id="9db1c-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="9db1c-140">Zobacz [Obsługa agregacji](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="9db1c-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="9db1c-141">Dodano obsługę zmiany źródła danych.</span><span class="sxs-lookup"><span data-stu-id="9db1c-141">Added support for change feed.</span></span>
* <span data-ttu-id="9db1c-142">Dodano obsługę za pośrednictwem RequestOptions.setPopulateQuotaInfo, informacje o limicie przydziału kolekcji.</span><span class="sxs-lookup"><span data-stu-id="9db1c-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="9db1c-143">Dodano obsługę rejestrowania skryptu procedury składowanej za pośrednictwem RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="9db1c-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="9db1c-144">Stałe usterki, gdzie mogą wykraczać zapytania w trybie DirectHttps, gdy wystąpią błędy ograniczania.</span><span class="sxs-lookup"><span data-stu-id="9db1c-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="9db1c-145">Rozwiązane usterki w tryb spójność sesji.</span><span class="sxs-lookup"><span data-stu-id="9db1c-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="9db1c-146">Stałe błędów, które mogą spowodować NullReferenceException element HttpContext po wysoki współczynnik żądań.</span><span class="sxs-lookup"><span data-stu-id="9db1c-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="9db1c-147">Lepsza wydajność DirectHttps tryb.</span><span class="sxs-lookup"><span data-stu-id="9db1c-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="9db1c-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="9db1c-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="9db1c-149">Dodano proste klienta oparte na wystąpienie obsługi serwera proxy z interfejsem API ConnectionPolicy.setProxy().</span><span class="sxs-lookup"><span data-stu-id="9db1c-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="9db1c-150">Dodano DocumentClient.close() API tooproperly zamknięcia DocumentClient wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="9db1c-150">Added DocumentClient.close() API tooproperly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="9db1c-151">Wydajność ulepszone zapytań w trybie bezpośrednie połączenie między przez pochodny planu zapytania hello hello natywny zestaw zamiast hello bramy.</span><span class="sxs-lookup"><span data-stu-id="9db1c-151">Improved query performance in direct connectivity mode by deriving hello query plan from hello native assembly instead of hello Gateway.</span></span>
* <span data-ttu-id="9db1c-152">Ustaw FAIL_ON_UNKNOWN_PROPERTIES = false, dzięki czemu użytkownicy nie muszą toodefine JsonIgnoreProperties w ich typu POJO.</span><span class="sxs-lookup"><span data-stu-id="9db1c-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need toodefine JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="9db1c-153">Rejestrowanie refaktoryzowane toouse SLF4J.</span><span class="sxs-lookup"><span data-stu-id="9db1c-153">Refactored logging toouse SLF4J.</span></span>
* <span data-ttu-id="9db1c-154">Stała kilka innych błędów spójności czytnika.</span><span class="sxs-lookup"><span data-stu-id="9db1c-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="9db1c-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="9db1c-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="9db1c-156">Rozwiązane usterki w hello przecieki połączenia tooprevent zarządzania połączenia w trybie bezpośredniego połączenia.</span><span class="sxs-lookup"><span data-stu-id="9db1c-156">Fixed a bug in hello connection management tooprevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="9db1c-157">Stała usterki hello zapytania TOP, w którym może zgłosić wyjątek NullReferenece.</span><span class="sxs-lookup"><span data-stu-id="9db1c-157">Fixed a bug in hello TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="9db1c-158">Lepszą wydajność dzięki zmniejszeniu liczby hello wywołania sieci dla hello wewnętrznych pamięci podręcznych.</span><span class="sxs-lookup"><span data-stu-id="9db1c-158">Improved performance by reducing hello number of network call for hello internal caches.</span></span>
* <span data-ttu-id="9db1c-159">Kod stanu dodany, ActivityID i identyfikator URI żądania w DocumentClientException w celu ułatwienia rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="9db1c-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="9db1c-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="9db1c-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="9db1c-161">Rozwiązano problem z zarządzaniem połączeniami hello stabilności.</span><span class="sxs-lookup"><span data-stu-id="9db1c-161">Fixed an issue in hello connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="9db1c-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="9db1c-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="9db1c-163">Dodano obsługę BoundedStaleness poziomu spójności.</span><span class="sxs-lookup"><span data-stu-id="9db1c-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="9db1c-164">Dodano obsługę bezpośrednie połączenie między dla operacji CRUD dla kolekcji partycjonowanych.</span><span class="sxs-lookup"><span data-stu-id="9db1c-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="9db1c-165">Stałe błędów badania bazy danych z programu SQL.</span><span class="sxs-lookup"><span data-stu-id="9db1c-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="9db1c-166">Rozwiązane usterki w pamięci podręcznej sesji hello gdzie może być niepoprawna tokenu sesji.</span><span class="sxs-lookup"><span data-stu-id="9db1c-166">Fixed a bug in hello session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="9db1c-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="9db1c-168">Dodano obsługę dla wielu partycji zapytania równoległe.</span><span class="sxs-lookup"><span data-stu-id="9db1c-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="9db1c-169">Dodano obsługę TOP/ORDER BY zapytania dla kolekcji partycjonowanych.</span><span class="sxs-lookup"><span data-stu-id="9db1c-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="9db1c-170">Dodano obsługę wysoki poziom spójności.</span><span class="sxs-lookup"><span data-stu-id="9db1c-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="9db1c-171">Dodano obsługę żądań na podstawie nazwy przy użyciu bezpośrednie połączenie między.</span><span class="sxs-lookup"><span data-stu-id="9db1c-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="9db1c-172">Stałe toomake ActivityId pozostaną niezmienione we wszystkich ponownych prób wykonania żądania.</span><span class="sxs-lookup"><span data-stu-id="9db1c-172">Fixed toomake ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="9db1c-173">Stałe błędów związane z pamięci podręcznej toohello sesji podczas odtwarzania Kolekcja o hello tej samej nazwy.</span><span class="sxs-lookup"><span data-stu-id="9db1c-173">Fixed a bug related toohello session cache when recreating a collection with hello same name.</span></span>
* <span data-ttu-id="9db1c-174">Dodano wielokąta i typy danych LineString podczas określania kolekcji indeksowania zasad dla zapytań przestrzennych grodzenia.</span><span class="sxs-lookup"><span data-stu-id="9db1c-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="9db1c-175">Rozwiązane problemy z dokumentem Java dla języka Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="9db1c-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="9db1c-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="9db1c-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="9db1c-177">Rozwiązane usterki w PartitionKeyDefinitionMap toocache kolekcje z jedną partycją i nie dokonywać dodatkowe pobrać partycji żądania klucza.</span><span class="sxs-lookup"><span data-stu-id="9db1c-177">Fixed a bug in PartitionKeyDefinitionMap toocache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="9db1c-178">Stała ponowna próba toonot usterki, gdy została podana wartość klucza partycji niepoprawne.</span><span class="sxs-lookup"><span data-stu-id="9db1c-178">Fixed a bug toonot retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="9db1c-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="9db1c-180">Hello dodano obsługę konta w przypadku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9db1c-180">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="9db1c-181">Dodano obsługę automatycznego próbowania na ograniczeniem przepustowości żądania za pomocą opcji toocustomize hello max ponowienia i maksymalna czas oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="9db1c-181">Added support for automatic retry on throttled requests with options toocustomize hello max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="9db1c-182">Zobacz RetryOptions i ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="9db1c-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="9db1c-183">Przestarzałe IPartitionResolver na podstawie niestandardowych kodów partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="9db1c-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="9db1c-184">Użyj kolekcji partycjonowanych wyżej magazynu i przepustowości.</span><span class="sxs-lookup"><span data-stu-id="9db1c-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="9db1c-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="9db1c-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="9db1c-186">Obsługa zasad ponawiania dodano ograniczania.</span><span class="sxs-lookup"><span data-stu-id="9db1c-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="9db1c-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="9db1c-188">Czas toolive (TTL) Obsługa dokumentów.</span><span class="sxs-lookup"><span data-stu-id="9db1c-188">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="9db1c-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="9db1c-190">Zaimplementowane [kolekcje partycjonowane](partition-data.md) i [poziomy wydajności zdefiniowanych przez użytkownika](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="9db1c-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="9db1c-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="9db1c-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="9db1c-192">Rozwiązane usterki w wartości skrótu toogenerate HashPartitionResolver w toobe little endian zgodne z innych zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="9db1c-192">Fixed a bug in HashPartitionResolver toogenerate hash values in little-endian toobe consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="9db1c-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="9db1c-194">Dodaj skrót & zakres tooassist rozpoznawania nazw partycji z aplikacjami dzielenia na fragmenty między wieloma partycjami.</span><span class="sxs-lookup"><span data-stu-id="9db1c-194">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="9db1c-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="9db1c-196">Implementuje Upsert.</span><span class="sxs-lookup"><span data-stu-id="9db1c-196">Implement Upsert.</span></span> <span data-ttu-id="9db1c-197">Nowych metod upsertXXX dodać toosupport Upsert funkcji.</span><span class="sxs-lookup"><span data-stu-id="9db1c-197">New upsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="9db1c-198">Na podstawie Identyfikatora wdrożenie routingu.</span><span class="sxs-lookup"><span data-stu-id="9db1c-198">Implement ID Based Routing.</span></span> <span data-ttu-id="9db1c-199">Brak zmian publicznego interfejsu API, wszystkie zmiany wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="9db1c-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="9db1c-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="9db1c-201">Numer wersji toobring wyrównania z innych zestawów SDK pominięte zlecenia</span><span class="sxs-lookup"><span data-stu-id="9db1c-201">Release skipped toobring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="9db1c-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="9db1c-203">Obsługuje dane geograficzne indeksu</span><span class="sxs-lookup"><span data-stu-id="9db1c-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="9db1c-204">Weryfikuje właściwość identyfikatora dla wszystkich zasobów.</span><span class="sxs-lookup"><span data-stu-id="9db1c-204">Validates id property for all resources.</span></span> <span data-ttu-id="9db1c-205">Identyfikatory zasobów nie może zawierać?, /, #, \, znaków ani kończyć spacją.</span><span class="sxs-lookup"><span data-stu-id="9db1c-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="9db1c-206">Dodaje nowy tooResourceResponse "postępu przekształcania indeksu" nagłówka.</span><span class="sxs-lookup"><span data-stu-id="9db1c-206">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="9db1c-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="9db1c-208">Implementuje zasady indeksowania V2</span><span class="sxs-lookup"><span data-stu-id="9db1c-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="9db1c-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="9db1c-210">GA SDK</span><span class="sxs-lookup"><span data-stu-id="9db1c-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="9db1c-211">Wersja & daty wycofania</span><span class="sxs-lookup"><span data-stu-id="9db1c-211">Release & Retirement Dates</span></span>
<span data-ttu-id="9db1c-212">Firma Microsoft udostępni powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w kolejności toosmooth hello przejścia tooa nowszej/nieobsługiwaną wersję.</span><span class="sxs-lookup"><span data-stu-id="9db1c-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="9db1c-213">Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko bieżącego toohello SDK, jak jest możliwie jak najszybciej zaleca tego należy zawsze uaktualnienia toohello najnowsze wersja zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="9db1c-213">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="9db1c-214">Wszystkie żądania tooCosmos bazy danych przy użyciu wycofane zestawu SDK będą odrzucane przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="9db1c-214">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="9db1c-215">Wszystkie wersje hello zestawu SDK usługi DocumentDB dla poprzedniego tooversion Java **1.0.0** zostaną wycofane w **29 lutego 2016**.</span><span class="sxs-lookup"><span data-stu-id="9db1c-215">All versions of hello DocumentDB SDK for Java prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="9db1c-216">Wersja</span><span class="sxs-lookup"><span data-stu-id="9db1c-216">Version</span></span> | <span data-ttu-id="9db1c-217">Data wydania</span><span class="sxs-lookup"><span data-stu-id="9db1c-217">Release Date</span></span> | <span data-ttu-id="9db1c-218">Dacie wycofania</span><span class="sxs-lookup"><span data-stu-id="9db1c-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="9db1c-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="9db1c-220">11 lipca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="9db1c-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="9db1c-222">10 maja 2017</span><span class="sxs-lookup"><span data-stu-id="9db1c-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="9db1c-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="9db1c-224">11 marca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="9db1c-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="9db1c-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="9db1c-226">21 lutego 2017 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="9db1c-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="9db1c-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="9db1c-228">31 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="9db1c-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="9db1c-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="9db1c-230">24 listopada 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="9db1c-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="9db1c-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="9db1c-232">30 października 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="9db1c-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="9db1c-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="9db1c-234">28 października 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="9db1c-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="9db1c-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="9db1c-236">26 października 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="9db1c-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="9db1c-238">03 października 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="9db1c-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="9db1c-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="9db1c-240">30 czerwca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="9db1c-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="9db1c-242">14 czerwca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="9db1c-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="9db1c-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="9db1c-244">30 kwietnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="9db1c-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="9db1c-246">27 kwietnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="9db1c-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="9db1c-248">29 marca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="9db1c-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="9db1c-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="9db1c-250">31 grudnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="9db1c-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="9db1c-252">04 grudnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="9db1c-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="9db1c-254">05 października 2015</span><span class="sxs-lookup"><span data-stu-id="9db1c-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="9db1c-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="9db1c-256">05 października 2015</span><span class="sxs-lookup"><span data-stu-id="9db1c-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="9db1c-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="9db1c-258">05 sierpnia 2015</span><span class="sxs-lookup"><span data-stu-id="9db1c-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="9db1c-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="9db1c-260">09 lipca 2015 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="9db1c-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="9db1c-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="9db1c-262">12 maja 2015 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="9db1c-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9db1c-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="9db1c-264">07 kwietnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="9db1c-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="9db1c-265">0.9.5-prelease</span></span> |<span data-ttu-id="9db1c-266">09 marca 2015 roku.</span><span class="sxs-lookup"><span data-stu-id="9db1c-266">Mar 09, 2015</span></span> |<span data-ttu-id="9db1c-267">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-267">February 29, 2016</span></span> |
| <span data-ttu-id="9db1c-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="9db1c-268">0.9.4-prelease</span></span> |<span data-ttu-id="9db1c-269">17 lutego 2015</span><span class="sxs-lookup"><span data-stu-id="9db1c-269">February 17, 2015</span></span> |<span data-ttu-id="9db1c-270">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-270">February 29, 2016</span></span> |
| <span data-ttu-id="9db1c-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="9db1c-271">0.9.3-prelease</span></span> |<span data-ttu-id="9db1c-272">13 stycznia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-272">January 13, 2015</span></span> |<span data-ttu-id="9db1c-273">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-273">February 29, 2016</span></span> |
| <span data-ttu-id="9db1c-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="9db1c-274">0.9.2-prelease</span></span> |<span data-ttu-id="9db1c-275">19 grudnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-275">December 19, 2014</span></span> |<span data-ttu-id="9db1c-276">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-276">February 29, 2016</span></span> |
| <span data-ttu-id="9db1c-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="9db1c-277">0.9.1-prelease</span></span> |<span data-ttu-id="9db1c-278">19 grudnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-278">December 19, 2014</span></span> |<span data-ttu-id="9db1c-279">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-279">February 29, 2016</span></span> |
| <span data-ttu-id="9db1c-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="9db1c-280">0.9.0-prelease</span></span> |<span data-ttu-id="9db1c-281">10 grudnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-281">December 10, 2014</span></span> |<span data-ttu-id="9db1c-282">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="9db1c-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="9db1c-283">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="9db1c-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="9db1c-284">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9db1c-284">See Also</span></span>
<span data-ttu-id="9db1c-285">toolearn więcej informacji na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi.</span><span class="sxs-lookup"><span data-stu-id="9db1c-285">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

