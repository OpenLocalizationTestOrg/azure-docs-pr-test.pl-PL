---
title: "aaaAzure rozwiązania Cosmos DB Python interfejsu API zestawu SDK i zasoby | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o hello interfejsu API języka Python i zestawu SDK, w tym daty wydania, daty wycofania i zmiany między poszczególnymi wersjami hello Azure rozwiązania Cosmos DB Python SDK."
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
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="e4a39-103">Python rozwiązania Cosmos bazy danych Azure SDK: Informacje o wersji i zasoby</span><span class="sxs-lookup"><span data-stu-id="e4a39-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4a39-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e4a39-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="e4a39-105">Źródła danych zmian .NET</span><span class="sxs-lookup"><span data-stu-id="e4a39-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="e4a39-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="e4a39-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="e4a39-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="e4a39-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="e4a39-108">Java</span><span class="sxs-lookup"><span data-stu-id="e4a39-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="e4a39-109">Python</span><span class="sxs-lookup"><span data-stu-id="e4a39-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="e4a39-110">REST</span><span class="sxs-lookup"><span data-stu-id="e4a39-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="e4a39-111">Dostawca zasobów REST</span><span class="sxs-lookup"><span data-stu-id="e4a39-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="e4a39-112">SQL</span><span class="sxs-lookup"><span data-stu-id="e4a39-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="e4a39-113">**Pobierz zestaw SDK**</span><span class="sxs-lookup"><span data-stu-id="e4a39-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="e4a39-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="e4a39-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="e4a39-115">**Dokumentacja interfejsu API**</span><span class="sxs-lookup"><span data-stu-id="e4a39-115">**API documentation**</span></span></td><td>[<span data-ttu-id="e4a39-116">Dokumentacji interfejsu API języka Python</span><span class="sxs-lookup"><span data-stu-id="e4a39-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="e4a39-117">**Instrukcje dotyczące instalacji zestawu SDK**</span><span class="sxs-lookup"><span data-stu-id="e4a39-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="e4a39-118">Instrukcje dotyczące instalacji zestawu SDK Python</span><span class="sxs-lookup"><span data-stu-id="e4a39-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="e4a39-119">**Współtworzenia tooSDK**</span><span class="sxs-lookup"><span data-stu-id="e4a39-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="e4a39-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="e4a39-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="e4a39-121">**Wprowadzenie**</span><span class="sxs-lookup"><span data-stu-id="e4a39-121">**Get started**</span></span></td><td>[<span data-ttu-id="e4a39-122">Rozpoczynanie pracy z hello zestaw SDK Python</span><span class="sxs-lookup"><span data-stu-id="e4a39-122">Get started with hello Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="e4a39-123">**Bieżący obsługiwanych platform**</span><span class="sxs-lookup"><span data-stu-id="e4a39-123">**Current supported platform**</span></span></td><td><span data-ttu-id="e4a39-124">[Python 2.7](https://www.python.org/downloads/) i [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="e4a39-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="e4a39-125">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="e4a39-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="e4a39-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="e4a39-127">Dodano obsługę nowego poziomu spójności o nazwie ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="e4a39-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="e4a39-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="e4a39-129">Dodano obsługę zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.).</span><span class="sxs-lookup"><span data-stu-id="e4a39-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="e4a39-130">Dodano opcję wyłączenia weryfikacji protokołu SSL podczas uruchamiania emulatora DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e4a39-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="e4a39-131">Usunąć ograniczenia hello zależnych żądań modułu toobe dokładnie 2.10.0.</span><span class="sxs-lookup"><span data-stu-id="e4a39-131">Removed hello restriction of dependent requests module toobe exactly 2.10.0.</span></span>
* <span data-ttu-id="e4a39-132">Obniżony minimalnej przepustowości w kolekcji partycjonowanych z RU/s 10,100 too2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="e4a39-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="e4a39-133">Dodano obsługę Włączanie rejestrowania skryptu podczas wykonywania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="e4a39-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="e4a39-134">Wersja interfejsu API REST za upadku "2017-01-19' w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="e4a39-134">REST API version bumped too'2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="e4a39-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="e4a39-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="e4a39-136">Wprowadzone zmiany redakcyjne toodocumentation komentarze.</span><span class="sxs-lookup"><span data-stu-id="e4a39-136">Made editorial changes toodocumentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="e4a39-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="e4a39-138">Dodano obsługę języka Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="e4a39-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="e4a39-139">Dodano obsługę dla puli połączeń przy użyciu modułu żądania.</span><span class="sxs-lookup"><span data-stu-id="e4a39-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="e4a39-140">Dodano obsługę spójność sesji.</span><span class="sxs-lookup"><span data-stu-id="e4a39-140">Added support for session consistency.</span></span>
* <span data-ttu-id="e4a39-141">Dodano obsługę TOP/ORDERBY zapytania dla kolekcji partycjonowanych.</span><span class="sxs-lookup"><span data-stu-id="e4a39-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="e4a39-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="e4a39-143">Obsługa zasad dodano ponownych prób dla żądań z ograniczeniem przepustowości.</span><span class="sxs-lookup"><span data-stu-id="e4a39-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="e4a39-144">(Ograniczeniem przepustowości żądania odbierania żądania szybkość zbyt duży wyjątek, kod błędu 429.) Domyślnie bazy danych Azure rozwiązania Cosmos ponowi próbę dziewięciokrotnie dla każdego żądania po napotkaniu błędu kodu 429 ramach czasu retryAfter hello hello nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e4a39-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="e4a39-145">Czas interwału ponawiania stałym teraz można ustawić jako część hello RetryOptions właściwości w obiekcie ConnectionPolicy hello Jeśli czas retryAfter hello tooignore zwrócony przez serwer między kolejnymi próbami hello.</span><span class="sxs-lookup"><span data-stu-id="e4a39-145">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="e4a39-146">Azure DB rozwiązania Cosmos teraz czeka na maksymalnie 30 sekund na każde żądanie jest ograniczane (niezależnie od liczby ponownych prób) i zwracającej odpowiedź hello 429 kod błędu.</span><span class="sxs-lookup"><span data-stu-id="e4a39-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="e4a39-147">Teraz również może zostać zastąpiona w hello RetryOptions właściwości w obiekcie ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="e4a39-147">This time can also be overriden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="e4a39-148">Rozwiązania cosmos DB teraz zwraca x-ms ograniczania liczby ponownych prób i x-ms-throttle-retry-wait-time-ms hello nagłówków odpowiedzi w każdego żądania toodenote hello ograniczania hello i liczba cummulative godzina ponowienia hello żądania oczekiwano między kolejnymi próbami hello.</span><span class="sxs-lookup"><span data-stu-id="e4a39-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cummulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="e4a39-149">Klasa RetryPolicy hello usunięte i odpowiadających im właściwości hello (retry_policy) widoczne w klasie document_client hello i zamiast tego wprowadzono klasy RetryOptions udostępnianie właściwości RetryOptions hello ConnectionPolicy klasy, które mogą być używane toooverride Opcje niektóre domyślne hello ponawiania.</span><span class="sxs-lookup"><span data-stu-id="e4a39-149">Removed hello RetryPolicy class and hello corresponding property (retry_policy) exposed on hello document_client class and instead introduced a RetryOptions class exposing hello RetryOptions property on ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="e4a39-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="e4a39-151">Hello dodano obsługę konta w przypadku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e4a39-151">Added hello support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="e4a39-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="e4a39-153">Witaj dodano obsługę funkcji tooLive(TTL) czasu dla dokumentów.</span><span class="sxs-lookup"><span data-stu-id="e4a39-153">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="e4a39-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="e4a39-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="e4a39-155">Poprawki błędów związanych z tooserver po stronie tooallow znaki specjalne w ścieżce partitionkey partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="e4a39-155">Bug fixes related tooserver side partitioning tooallow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="e4a39-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="e4a39-157">Zaimplementowane [kolekcje partycjonowane](partition-data.md) i [poziomy wydajności zdefiniowanych przez użytkownika](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="e4a39-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="e4a39-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="e4a39-159">Dodaj skrót & zakres tooassist rozpoznawania nazw partycji z aplikacjami dzielenia na fragmenty między wieloma partycjami.</span><span class="sxs-lookup"><span data-stu-id="e4a39-159">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="e4a39-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="e4a39-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="e4a39-161">Implementuje Upsert.</span><span class="sxs-lookup"><span data-stu-id="e4a39-161">Implement Upsert.</span></span> <span data-ttu-id="e4a39-162">Nowych metod UpsertXXX dodać toosupport Upsert funkcji.</span><span class="sxs-lookup"><span data-stu-id="e4a39-162">New UpsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="e4a39-163">Na podstawie Identyfikatora wdrożenie routingu.</span><span class="sxs-lookup"><span data-stu-id="e4a39-163">Implement ID Based Routing.</span></span> <span data-ttu-id="e4a39-164">Brak zmian publicznego interfejsu API, wszystkie zmiany wewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="e4a39-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="e4a39-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="e4a39-166">Obsługuje dane geograficzne indeksu.</span><span class="sxs-lookup"><span data-stu-id="e4a39-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="e4a39-167">Weryfikuje właściwość identyfikatora dla wszystkich zasobów.</span><span class="sxs-lookup"><span data-stu-id="e4a39-167">Validates id property for all resources.</span></span> <span data-ttu-id="e4a39-168">Identyfikatory zasobów nie może zawierać?, /, #, \, znaków ani kończyć spacją.</span><span class="sxs-lookup"><span data-stu-id="e4a39-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="e4a39-169">Dodaje nowy tooResourceResponse "postępu przekształcania indeksu" nagłówka.</span><span class="sxs-lookup"><span data-stu-id="e4a39-169">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="e4a39-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="e4a39-171">Implementuje zasady indeksowania V2.</span><span class="sxs-lookup"><span data-stu-id="e4a39-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="e4a39-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="e4a39-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="e4a39-173">Obsługuje połączenia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="e4a39-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="e4a39-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="e4a39-175">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="e4a39-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="e4a39-176">Wersja & wycofania dat</span><span class="sxs-lookup"><span data-stu-id="e4a39-176">Release & retirement dates</span></span>
<span data-ttu-id="e4a39-177">Firma Microsoft udostępni powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w kolejności toosmooth hello przejścia tooa nowszej/nieobsługiwaną wersję.</span><span class="sxs-lookup"><span data-stu-id="e4a39-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="e4a39-178">Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko bieżącego toohello SDK, jak jest możliwie jak najszybciej zaleca tego należy zawsze uaktualnienia toohello najnowsze wersja zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="e4a39-178">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="e4a39-179">Wszystkie żądania tooCosmos bazy danych przy użyciu wycofane zestawu SDK będą odrzucane przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="e4a39-179">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="e4a39-180">Wszystkie wersje hello zestawu SDK usługi Azure DocumentDB do poprzedniego tooversion Python **1.0.0** zostaną wycofane w **29 lutego 2016**.</span><span class="sxs-lookup"><span data-stu-id="e4a39-180">All versions of hello Azure DocumentDB SDK for Python prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="e4a39-181">Wersja</span><span class="sxs-lookup"><span data-stu-id="e4a39-181">Version</span></span> | <span data-ttu-id="e4a39-182">Data wydania</span><span class="sxs-lookup"><span data-stu-id="e4a39-182">Release Date</span></span> | <span data-ttu-id="e4a39-183">Dacie wycofania</span><span class="sxs-lookup"><span data-stu-id="e4a39-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="e4a39-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="e4a39-185">10 maja 2017</span><span class="sxs-lookup"><span data-stu-id="e4a39-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="e4a39-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="e4a39-187">01 maja 2017 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="e4a39-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="e4a39-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="e4a39-189">30 października 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="e4a39-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="e4a39-191">29 wrześniu 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="e4a39-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="e4a39-193">07 lipca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="e4a39-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="e4a39-195">14 czerwca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="e4a39-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="e4a39-197">26 kwietnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="e4a39-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="e4a39-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="e4a39-199">08 kwietnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="e4a39-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="e4a39-201">29 marca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="e4a39-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="e4a39-203">03 stycznia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="e4a39-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="e4a39-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="e4a39-205">06 października 2015</span><span class="sxs-lookup"><span data-stu-id="e4a39-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="e4a39-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="e4a39-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="e4a39-207">06 października 2015</span><span class="sxs-lookup"><span data-stu-id="e4a39-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="e4a39-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="e4a39-209">06 sierpień 2015</span><span class="sxs-lookup"><span data-stu-id="e4a39-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="e4a39-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="e4a39-211">09 lipca 2015 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="e4a39-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="e4a39-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="e4a39-213">25 maja 2015 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="e4a39-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e4a39-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="e4a39-215">07 kwietnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="e4a39-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="e4a39-216">0.9.4-prelease</span></span> |<span data-ttu-id="e4a39-217">14 stycznia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-217">January 14, 2015</span></span> |<span data-ttu-id="e4a39-218">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-218">February 29, 2016</span></span> |
| <span data-ttu-id="e4a39-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="e4a39-219">0.9.3-prelease</span></span> |<span data-ttu-id="e4a39-220">09 grudnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-220">December 09, 2014</span></span> |<span data-ttu-id="e4a39-221">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-221">February 29, 2016</span></span> |
| <span data-ttu-id="e4a39-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="e4a39-222">0.9.2-prelease</span></span> |<span data-ttu-id="e4a39-223">25 listopada 2014 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-223">November 25, 2014</span></span> |<span data-ttu-id="e4a39-224">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-224">February 29, 2016</span></span> |
| <span data-ttu-id="e4a39-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="e4a39-225">0.9.1-prelease</span></span> |<span data-ttu-id="e4a39-226">23 września 2014 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-226">September 23, 2014</span></span> |<span data-ttu-id="e4a39-227">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-227">February 29, 2016</span></span> |
| <span data-ttu-id="e4a39-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="e4a39-228">0.9.0-prelease</span></span> |<span data-ttu-id="e4a39-229">21 sierpnia 2014 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-229">August 21, 2014</span></span> |<span data-ttu-id="e4a39-230">29 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="e4a39-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="e4a39-231">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="e4a39-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="e4a39-232">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e4a39-232">See also</span></span>
<span data-ttu-id="e4a39-233">toolearn więcej informacji na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi.</span><span class="sxs-lookup"><span data-stu-id="e4a39-233">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

