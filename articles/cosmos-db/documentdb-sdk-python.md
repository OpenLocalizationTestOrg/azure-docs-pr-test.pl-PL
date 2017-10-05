---
title: "Python rozwiązania Cosmos Azure DB interfejsu API, zestaw SDK i zasoby | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o interfejsie API języka Python i zestawu SDK, w tym daty wydania, daty wycofania i zmiany wprowadzone od każdej wersji zestawu SDK Python platformy Azure rozwiązania Cosmos bazy danych."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70d2550f713ff0e9daed235eb8053589b8682633
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="385b3-103">Python rozwiązania Cosmos bazy danych Azure SDK: Informacje o wersji i zasoby</span><span class="sxs-lookup"><span data-stu-id="385b3-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="385b3-104">.NET</span><span class="sxs-lookup"><span data-stu-id="385b3-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="385b3-105">Źródła danych zmian .NET</span><span class="sxs-lookup"><span data-stu-id="385b3-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="385b3-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="385b3-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="385b3-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="385b3-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="385b3-108">Java</span><span class="sxs-lookup"><span data-stu-id="385b3-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="385b3-109">Python</span><span class="sxs-lookup"><span data-stu-id="385b3-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="385b3-110">REST</span><span class="sxs-lookup"><span data-stu-id="385b3-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="385b3-111">Dostawca zasobów REST</span><span class="sxs-lookup"><span data-stu-id="385b3-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="385b3-112">SQL</span><span class="sxs-lookup"><span data-stu-id="385b3-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="385b3-113">**Pobierz zestaw SDK**</span><span class="sxs-lookup"><span data-stu-id="385b3-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="385b3-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="385b3-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="385b3-115">**Dokumentacja interfejsu API**</span><span class="sxs-lookup"><span data-stu-id="385b3-115">**API documentation**</span></span></td><td>[<span data-ttu-id="385b3-116">Dokumentacji interfejsu API języka Python</span><span class="sxs-lookup"><span data-stu-id="385b3-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="385b3-117">**Instrukcje dotyczące instalacji zestawu SDK**</span><span class="sxs-lookup"><span data-stu-id="385b3-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="385b3-118">Instrukcje dotyczące instalacji zestawu SDK Python</span><span class="sxs-lookup"><span data-stu-id="385b3-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="385b3-119">**Przyczyniają się do zestawu SDK**</span><span class="sxs-lookup"><span data-stu-id="385b3-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="385b3-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="385b3-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="385b3-121">**Wprowadzenie**</span><span class="sxs-lookup"><span data-stu-id="385b3-121">**Get started**</span></span></td><td>[<span data-ttu-id="385b3-122">Rozpoczynanie pracy z zestawem SDK Python</span><span class="sxs-lookup"><span data-stu-id="385b3-122">Get started with the Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="385b3-123">**Bieżący obsługiwanych platform**</span><span class="sxs-lookup"><span data-stu-id="385b3-123">**Current supported platform**</span></span></td><td><span data-ttu-id="385b3-124">[Python 2.7](https://www.python.org/downloads/) i [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="385b3-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="385b3-125">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="385b3-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="385b3-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="385b3-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="385b3-127">Dodano obsługę nowego poziomu spójności o nazwie ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="385b3-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="385b3-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="385b3-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="385b3-129">Dodano obsługę zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.).</span><span class="sxs-lookup"><span data-stu-id="385b3-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="385b3-130">Dodano opcję wyłączenia weryfikacji protokołu SSL podczas uruchamiania emulatora DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="385b3-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="385b3-131">Usunięte ograniczenie zależnych żądań modułu należy dokładnie 2.10.0.</span><span class="sxs-lookup"><span data-stu-id="385b3-131">Removed the restriction of dependent requests module to be exactly 2.10.0.</span></span>
* <span data-ttu-id="385b3-132">Obniżony minimalnej przepustowości w kolekcji partycjonowanych z 10,100 RU/s do 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="385b3-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="385b3-133">Dodano obsługę Włączanie rejestrowania skryptu podczas wykonywania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="385b3-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="385b3-134">Wersja interfejsu API REST upadku do "2017-01-19' w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="385b3-134">REST API version bumped to '2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="385b3-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="385b3-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="385b3-136">Wprowadzone zmiany redakcyjne komentarzy do dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="385b3-136">Made editorial changes to documentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="385b3-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="385b3-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="385b3-138">Dodano obsługę języka Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="385b3-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="385b3-139">Dodano obsługę dla puli połączeń przy użyciu modułu żądania.</span><span class="sxs-lookup"><span data-stu-id="385b3-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="385b3-140">Dodano obsługę spójność sesji.</span><span class="sxs-lookup"><span data-stu-id="385b3-140">Added support for session consistency.</span></span>
* <span data-ttu-id="385b3-141">Dodano obsługę TOP/ORDERBY zapytania dla kolekcji partycjonowanych.</span><span class="sxs-lookup"><span data-stu-id="385b3-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="385b3-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="385b3-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="385b3-143">Obsługa zasad dodano ponownych prób dla żądań z ograniczeniem przepustowości.</span><span class="sxs-lookup"><span data-stu-id="385b3-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="385b3-144">(Ograniczeniem przepustowości żądania odbierania żądania szybkość zbyt duży wyjątek, kod błędu 429.) Domyślnie bazy danych Azure rozwiązania Cosmos ponowi próbę dziewięciokrotnie dla każdego żądania po napotkaniu błędu kodu 429 ramach czasu retryAfter nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="385b3-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="385b3-145">Czas interwału ponawiania stałym teraz można ustawić jako część właściwości RetryOptions w obiekcie ConnectionPolicy aby zignorować godzinę retryAfter zwrócony przez serwer między ponownymi próbami.</span><span class="sxs-lookup"><span data-stu-id="385b3-145">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="385b3-146">Azure DB rozwiązania Cosmos teraz czeka na maksymalnie 30 sekund dla każdego żądania jest ograniczane (niezależnie od liczby ponownych prób) i zwraca odpowiedź z kodem błędu 429.</span><span class="sxs-lookup"><span data-stu-id="385b3-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="385b3-147">Teraz można także przesłonięta we właściwości RetryOptions ConnectionPolicy obiektu.</span><span class="sxs-lookup"><span data-stu-id="385b3-147">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="385b3-148">Rozwiązania cosmos DB teraz zwraca x-ms ograniczania liczby ponownych prób i x-ms-throttle-retry-wait-time-ms nagłówków odpowiedzi każde żądanie do oznaczania przepustnicy ponów liczba i czas cummulative żądanie oczekiwało między ponownymi próbami.</span><span class="sxs-lookup"><span data-stu-id="385b3-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span></span>
* <span data-ttu-id="385b3-149">Usunąć klasę RetryPolicy i odpowiadających im właściwości (retry_policy) udostępniane w klasie document_client i zamiast tego wprowadzono klasy RetryOptions udostępnianie właściwości RetryOptions w klasie ConnectionPolicy, który może służyć do zastępowania niektórych domyślne opcje ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="385b3-149">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="385b3-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="385b3-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="385b3-151">Dodano obsługę konta w przypadku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="385b3-151">Added the support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="385b3-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="385b3-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="385b3-153">Dodano obsługę funkcji czas do Live(TTL) dokumentów.</span><span class="sxs-lookup"><span data-stu-id="385b3-153">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="385b3-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="385b3-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="385b3-155">Poprawki błędów związanych z serwera partycjonowania po stronie, aby zezwalać na znaki specjalne w ścieżce partitionkey.</span><span class="sxs-lookup"><span data-stu-id="385b3-155">Bug fixes related to server side partitioning to allow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="385b3-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="385b3-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="385b3-157">Zaimplementowane [kolekcje partycjonowane](partition-data.md) i [poziomy wydajności zdefiniowanych przez użytkownika](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="385b3-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="385b3-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="385b3-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="385b3-159">Dodaj skrót & zakres partycji rozwiązujący pomagające dzielenia na fragmenty aplikacji między wieloma partycjami.</span><span class="sxs-lookup"><span data-stu-id="385b3-159">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="385b3-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="385b3-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="385b3-161">Implementuje Upsert.</span><span class="sxs-lookup"><span data-stu-id="385b3-161">Implement Upsert.</span></span> <span data-ttu-id="385b3-162">Dodane w celu obsługi funkcji Upsert nowych metod UpsertXXX.</span><span class="sxs-lookup"><span data-stu-id="385b3-162">New UpsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="385b3-163">Na podstawie Identyfikatora wdrożenie routingu.</span><span class="sxs-lookup"><span data-stu-id="385b3-163">Implement ID Based Routing.</span></span> <span data-ttu-id="385b3-164">Brak zmian publicznego interfejsu API, wszystkie zmiany wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="385b3-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="385b3-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="385b3-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="385b3-166">Obsługuje dane geograficzne indeksu.</span><span class="sxs-lookup"><span data-stu-id="385b3-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="385b3-167">Weryfikuje właściwość identyfikatora dla wszystkich zasobów.</span><span class="sxs-lookup"><span data-stu-id="385b3-167">Validates id property for all resources.</span></span> <span data-ttu-id="385b3-168">Identyfikatory zasobów nie może zawierać?, /, #, \, znaków ani kończyć spacją.</span><span class="sxs-lookup"><span data-stu-id="385b3-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="385b3-169">Dodaje nowego nagłówka "indeksu przekształcania toku" do ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="385b3-169">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="385b3-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="385b3-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="385b3-171">Implementuje zasady indeksowania V2.</span><span class="sxs-lookup"><span data-stu-id="385b3-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="385b3-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="385b3-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="385b3-173">Obsługuje połączenia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="385b3-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="385b3-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="385b3-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="385b3-175">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="385b3-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="385b3-176">Wersja & wycofania dat</span><span class="sxs-lookup"><span data-stu-id="385b3-176">Release & retirement dates</span></span>
<span data-ttu-id="385b3-177">Firma Microsoft udostępni powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w celu złagodzenia przejścia do nowszej/nieobsługiwaną wersję.</span><span class="sxs-lookup"><span data-stu-id="385b3-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="385b3-178">Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko do bieżącego zestawu SDK, w związku jest zalecane, zawsze uaktualnienie SDK najnowszą tak szybko jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="385b3-178">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="385b3-179">Każde żądanie do rozwiązania Cosmos bazy danych przy użyciu wycofane zestawu SDK będą odrzucane przez usługę.</span><span class="sxs-lookup"><span data-stu-id="385b3-179">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="385b3-180">Wszystkie wersje zestawu SDK usługi DocumentDB platformy Azure dla języka Python poprzedzające wersję **1.0.0** zostaną wycofane w **29 lutego 2016**.</span><span class="sxs-lookup"><span data-stu-id="385b3-180">All versions of the Azure DocumentDB SDK for Python prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="385b3-181">Wersja</span><span class="sxs-lookup"><span data-stu-id="385b3-181">Version</span></span> | <span data-ttu-id="385b3-182">Data wydania</span><span class="sxs-lookup"><span data-stu-id="385b3-182">Release Date</span></span> | <span data-ttu-id="385b3-183">Dacie wycofania</span><span class="sxs-lookup"><span data-stu-id="385b3-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="385b3-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="385b3-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="385b3-185">10 maja 2017</span><span class="sxs-lookup"><span data-stu-id="385b3-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="385b3-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="385b3-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="385b3-187">01 maja 2017 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="385b3-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="385b3-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="385b3-189">30 października 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="385b3-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="385b3-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="385b3-191">29 wrześniu 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="385b3-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="385b3-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="385b3-193">07 lipca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="385b3-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="385b3-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="385b3-195">14 czerwca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="385b3-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="385b3-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="385b3-197">26 kwietnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="385b3-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="385b3-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="385b3-199">08 kwietnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="385b3-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="385b3-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="385b3-201">29 marca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="385b3-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="385b3-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="385b3-203">03 stycznia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="385b3-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="385b3-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="385b3-205">06 października 2015</span><span class="sxs-lookup"><span data-stu-id="385b3-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="385b3-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="385b3-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="385b3-207">06 października 2015</span><span class="sxs-lookup"><span data-stu-id="385b3-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="385b3-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="385b3-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="385b3-209">06 sierpień 2015</span><span class="sxs-lookup"><span data-stu-id="385b3-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="385b3-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="385b3-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="385b3-211">09 lipca 2015 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="385b3-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="385b3-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="385b3-213">25 maja 2015 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="385b3-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="385b3-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="385b3-215">07 kwietnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="385b3-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="385b3-216">0.9.4-prelease</span></span> |<span data-ttu-id="385b3-217">14 stycznia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-217">January 14, 2015</span></span> |<span data-ttu-id="385b3-218">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-218">February 29, 2016</span></span> |
| <span data-ttu-id="385b3-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="385b3-219">0.9.3-prelease</span></span> |<span data-ttu-id="385b3-220">09 grudnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-220">December 09, 2014</span></span> |<span data-ttu-id="385b3-221">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-221">February 29, 2016</span></span> |
| <span data-ttu-id="385b3-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="385b3-222">0.9.2-prelease</span></span> |<span data-ttu-id="385b3-223">25 listopada 2014 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-223">November 25, 2014</span></span> |<span data-ttu-id="385b3-224">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-224">February 29, 2016</span></span> |
| <span data-ttu-id="385b3-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="385b3-225">0.9.1-prelease</span></span> |<span data-ttu-id="385b3-226">23 września 2014 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-226">September 23, 2014</span></span> |<span data-ttu-id="385b3-227">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-227">February 29, 2016</span></span> |
| <span data-ttu-id="385b3-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="385b3-228">0.9.0-prelease</span></span> |<span data-ttu-id="385b3-229">21 sierpnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-229">August 21, 2014</span></span> |<span data-ttu-id="385b3-230">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="385b3-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="385b3-231">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="385b3-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="385b3-232">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="385b3-232">See also</span></span>
<span data-ttu-id="385b3-233">Aby dowiedzieć się więcej na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi.</span><span class="sxs-lookup"><span data-stu-id="385b3-233">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

