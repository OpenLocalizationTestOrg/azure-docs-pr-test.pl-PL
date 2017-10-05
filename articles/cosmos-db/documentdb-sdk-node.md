---
title: "Zasoby, zestaw SDK & rozwiązania Cosmos Azure DB interfejsu API środowiska Node.js | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o interfejsu API środowiska Node.js i tym daty wydania, daty wycofania i zmiany wprowadzone od każdej wersji zestawu SDK platformy Azure rozwiązania Cosmos DB Node.js SDK."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4376a5c07b5f00311ce0fe3c0056efdf79c273f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="5e5af-103">Zestaw SDK platformy Azure rozwiązania Cosmos DB Node.js: Informacje o wersji i zasoby</span><span class="sxs-lookup"><span data-stu-id="5e5af-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e5af-104">.NET</span><span class="sxs-lookup"><span data-stu-id="5e5af-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="5e5af-105">Źródła danych zmian .NET</span><span class="sxs-lookup"><span data-stu-id="5e5af-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="5e5af-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="5e5af-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="5e5af-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="5e5af-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="5e5af-108">Java</span><span class="sxs-lookup"><span data-stu-id="5e5af-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="5e5af-109">Python</span><span class="sxs-lookup"><span data-stu-id="5e5af-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="5e5af-110">REST</span><span class="sxs-lookup"><span data-stu-id="5e5af-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="5e5af-111">Dostawca zasobów REST</span><span class="sxs-lookup"><span data-stu-id="5e5af-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="5e5af-112">SQL</span><span class="sxs-lookup"><span data-stu-id="5e5af-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="5e5af-113">**Pobierz zestaw SDK**</span><span class="sxs-lookup"><span data-stu-id="5e5af-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="5e5af-114">NPM</span><span class="sxs-lookup"><span data-stu-id="5e5af-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="5e5af-115">**Dokumentacja interfejsu API**</span><span class="sxs-lookup"><span data-stu-id="5e5af-115">**API documentation**</span></span></td><td>[<span data-ttu-id="5e5af-116">Dokumentacji interfejsu API środowiska node.js</span><span class="sxs-lookup"><span data-stu-id="5e5af-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="5e5af-117">**Instrukcje dotyczące instalacji zestawu SDK**</span><span class="sxs-lookup"><span data-stu-id="5e5af-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="5e5af-118">Instrukcje dotyczące instalacji</span><span class="sxs-lookup"><span data-stu-id="5e5af-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="5e5af-119">**Przyczyniają się do zestawu SDK**</span><span class="sxs-lookup"><span data-stu-id="5e5af-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="5e5af-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="5e5af-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="5e5af-121">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="5e5af-121">**Samples**</span></span></td><td>[<span data-ttu-id="5e5af-122">Przykłady kodu node.js</span><span class="sxs-lookup"><span data-stu-id="5e5af-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="5e5af-123">**Samouczek z wprowadzeniem**</span><span class="sxs-lookup"><span data-stu-id="5e5af-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="5e5af-124">Wprowadzenie do zestawu Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="5e5af-124">Get started with the Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="5e5af-125">**Samouczek aplikacji sieci Web**</span><span class="sxs-lookup"><span data-stu-id="5e5af-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="5e5af-126">Tworzenie aplikacji sieci web Node.js za pomocą bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="5e5af-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="5e5af-127">**Bieżący obsługiwanych platform**</span><span class="sxs-lookup"><span data-stu-id="5e5af-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="5e5af-128">6.x node.js</span><span class="sxs-lookup"><span data-stu-id="5e5af-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="5e5af-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="5e5af-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="5e5af-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="5e5af-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="5e5af-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="5e5af-132">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="5e5af-132">Release notes</span></span>

### <span data-ttu-id="5e5af-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="5e5af-134">Dokumentacja programu npm stałej.</span><span class="sxs-lookup"><span data-stu-id="5e5af-134">npm documentation fixed.</span></span>

### <span data-ttu-id="5e5af-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="5e5af-136">Stała usterki executeStoredProcedure, w którym dokumenty ma specjalne znaków Unicode (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="5e5af-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="5e5af-137">Stałe usterki w obsłudze dokumenty zawierające znaki Unicode w kluczu partycji.</span><span class="sxs-lookup"><span data-stu-id="5e5af-137">Fixed a bug in handling documents with Unicode characters in the partition key.</span></span>
* <span data-ttu-id="5e5af-138">Stały obsługę tworzenia kolekcji z nośnika nazwy.</span><span class="sxs-lookup"><span data-stu-id="5e5af-138">Fixed support for creating collections with the name media.</span></span> <span data-ttu-id="5e5af-139">Problem Github #114.</span><span class="sxs-lookup"><span data-stu-id="5e5af-139">Github issue #114.</span></span>
* <span data-ttu-id="5e5af-140">Stałe obsługę token autoryzacji uprawnień.</span><span class="sxs-lookup"><span data-stu-id="5e5af-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="5e5af-141">Problem Github #178.</span><span class="sxs-lookup"><span data-stu-id="5e5af-141">Github issue #178.</span></span>

### <span data-ttu-id="5e5af-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="5e5af-143">Dodano nową obsługę [poziomu spójności](consistency-levels.md) o nazwie ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="5e5af-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="5e5af-144">Dodano obsługę UriFactory.</span><span class="sxs-lookup"><span data-stu-id="5e5af-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="5e5af-145">Stałe błędów obsługę standardu Unicode.</span><span class="sxs-lookup"><span data-stu-id="5e5af-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="5e5af-146">Problem GitHub #171.</span><span class="sxs-lookup"><span data-stu-id="5e5af-146">GitHub issue #171.</span></span>

### <span data-ttu-id="5e5af-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="5e5af-148">Dodano obsługę zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.).</span><span class="sxs-lookup"><span data-stu-id="5e5af-148">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="5e5af-149">Dodano opcja kontrolowania stopień równoległości dla wielu partycji zapytań.</span><span class="sxs-lookup"><span data-stu-id="5e5af-149">Added the option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="5e5af-150">Dodano opcję wyłączenie protokołu SSL weryfikacji podczas uruchamiania emulatora DB rozwiązania Cosmos Azure.</span><span class="sxs-lookup"><span data-stu-id="5e5af-150">Added the option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="5e5af-151">Obniżony minimalnej przepustowości w kolekcji partycjonowanych z 10,100 RU/s do 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="5e5af-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="5e5af-152">Stałe błędów token kontynuacji dla kolekcji jednej partycji.</span><span class="sxs-lookup"><span data-stu-id="5e5af-152">Fixed the continuation token bug for single partition collection.</span></span> <span data-ttu-id="5e5af-153">Problem Github #107.</span><span class="sxs-lookup"><span data-stu-id="5e5af-153">Github issue #107.</span></span>
* <span data-ttu-id="5e5af-154">Stałe błędów executeStoredProcedure obsługi 0 jako pojedynczy parametr w.</span><span class="sxs-lookup"><span data-stu-id="5e5af-154">Fixed the executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="5e5af-155">Problem Github #155.</span><span class="sxs-lookup"><span data-stu-id="5e5af-155">Github issue #155.</span></span>

### <span data-ttu-id="5e5af-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="5e5af-157">Stałe agenta użytkownika nagłówek do uwzględnienia wersja zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="5e5af-157">Fixed user-agent header to include the SDK version.</span></span>
* <span data-ttu-id="5e5af-158">Oczyszczanie kodu pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="5e5af-158">Minor code cleanup.</span></span>

### <span data-ttu-id="5e5af-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="5e5af-160">Wyłączanie weryfikacji protokołu SSL podczas korzystania z zestawu SDK pod kątem emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="5e5af-160">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span></span>
* <span data-ttu-id="5e5af-161">Dodano obsługę Włączanie rejestrowania skryptu podczas wykonywania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="5e5af-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="5e5af-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="5e5af-163">Dodano obsługę dla wielu partycji zapytania równoległe.</span><span class="sxs-lookup"><span data-stu-id="5e5af-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="5e5af-164">Dodano obsługę TOP/ORDER BY zapytania dla kolekcji partycjonowanych.</span><span class="sxs-lookup"><span data-stu-id="5e5af-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="5e5af-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="5e5af-166">Obsługa zasad dodano ponownych prób dla żądań z ograniczeniem przepustowości.</span><span class="sxs-lookup"><span data-stu-id="5e5af-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="5e5af-167">(Ograniczeniem przepustowości żądania odbierania żądania szybkość zbyt duży wyjątek, kod błędu 429.) Domyślnie bazy danych Azure rozwiązania Cosmos ponowi próbę dziewięciokrotnie dla każdego żądania po napotkaniu błędu kodu 429 ramach czasu retryAfter nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5e5af-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="5e5af-168">Czas interwału ponawiania stałym teraz można ustawić jako część właściwości RetryOptions w obiekcie ConnectionPolicy aby zignorować godzinę retryAfter zwrócony przez serwer między ponownymi próbami.</span><span class="sxs-lookup"><span data-stu-id="5e5af-168">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="5e5af-169">Azure DB rozwiązania Cosmos teraz czeka na maksymalnie 30 sekund dla każdego żądania jest ograniczane (niezależnie od liczby ponownych prób) i zwraca odpowiedź z kodem błędu 429.</span><span class="sxs-lookup"><span data-stu-id="5e5af-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="5e5af-170">Teraz również może zostać przesłonięta we właściwości RetryOptions ConnectionPolicy obiektu.</span><span class="sxs-lookup"><span data-stu-id="5e5af-170">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="5e5af-171">Rozwiązania cosmos DB teraz zwraca x-ms ograniczania liczby ponownych prób i x-ms-throttle-retry-wait-time-ms nagłówków odpowiedzi każde żądanie do oznaczania przepustnicy ponów liczby i skumulowany czas żądanie oczekiwało między ponownymi próbami.</span><span class="sxs-lookup"><span data-stu-id="5e5af-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span></span>
* <span data-ttu-id="5e5af-172">Klasa RetryOptions został dodany, udostępnianie właściwości RetryOptions klasy ConnectionPolicy, który może służyć do zastępowania niektórych domyślne opcje ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="5e5af-172">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <span data-ttu-id="5e5af-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="5e5af-174">Dodano obsługę konta w przypadku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5e5af-174">Added the support for multi-region database accounts.</span></span>

### <span data-ttu-id="5e5af-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="5e5af-176">Dodano obsługę funkcji czas do Live(TTL) dokumentów.</span><span class="sxs-lookup"><span data-stu-id="5e5af-176">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <span data-ttu-id="5e5af-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="5e5af-178">Zaimplementowane [kolekcje partycjonowane](partition-data.md) i [poziomy wydajności zdefiniowanych przez użytkownika](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="5e5af-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="5e5af-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="5e5af-180">Usunięte usterki RangePartitionResolver.resolveForRead gdzie nie został zwrócił łącza z powodu nieprawidłowych concat wyników.</span><span class="sxs-lookup"><span data-stu-id="5e5af-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span></span>

### <span data-ttu-id="5e5af-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="5e5af-182">Stałe hashParitionResolver resolveForRead(): gdy nie podany klucz partycji została Zgłaszanie wyjątku, zamiast zwracać listę wszystkich zarejestrowanych łączy.</span><span class="sxs-lookup"><span data-stu-id="5e5af-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="5e5af-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="5e5af-184">Rozwiązuje problem [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -agenta w wersji dedykowanej HTTPS: unikać modyfikacji globalne agenta do celów bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5e5af-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="5e5af-185">Użyj dedykowanych agenta dla wszystkich żądań lib.</span><span class="sxs-lookup"><span data-stu-id="5e5af-185">Use a dedicated agent for all of the lib’s requests.</span></span>

### <span data-ttu-id="5e5af-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="5e5af-187">Rozwiązuje problem [#81](https://github.com/Azure/azure-documentdb-node/issues/81) — poprawnie obsłużyć myślniki identyfikatory nośników.</span><span class="sxs-lookup"><span data-stu-id="5e5af-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="5e5af-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="5e5af-189">Rozwiązuje problem [#95](https://github.com/Azure/azure-documentdb-node/issues/95) -odbiornika EventEmitter wyciek ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="5e5af-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="5e5af-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="5e5af-191">Rozwiązuje problem [#92](https://github.com/Azure/azure-documentdb-node/issues/90) — Zmień nazwę folderu skrót do wyznaczania wartości skrótu dla systemów z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="5e5af-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case-sensitive systems.</span></span>

### <span data-ttu-id="5e5af-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="5e5af-193">Implementowanie obsługi dzielenia na fragmenty przez dodanie skrótów & zakres rozpoznawania nazw partycji.</span><span class="sxs-lookup"><span data-stu-id="5e5af-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="5e5af-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="5e5af-195">Implementuje Upsert.</span><span class="sxs-lookup"><span data-stu-id="5e5af-195">Implement Upsert.</span></span> <span data-ttu-id="5e5af-196">Nowych metod upsertXXX na documentClient.</span><span class="sxs-lookup"><span data-stu-id="5e5af-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="5e5af-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="5e5af-198">Pominięto przenieść numery wersji wyrównania z innych zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="5e5af-198">Skipped to bring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="5e5af-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="5e5af-200">Q podziału niesie obietnice otok dla nowego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="5e5af-200">Split Q promises wrapper to new repository.</span></span>
* <span data-ttu-id="5e5af-201">Zaktualizuj do pliku pakietu do rejestru npm.</span><span class="sxs-lookup"><span data-stu-id="5e5af-201">Update to package file for npm registry.</span></span>

### <span data-ttu-id="5e5af-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="5e5af-203">Implementuje identyfikator oparte na routingu.</span><span class="sxs-lookup"><span data-stu-id="5e5af-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="5e5af-204">Rozwiązuje problem [#49](https://github.com/Azure/azure-documentdb-node/issues/49) -bieżącej właściwości powoduje konflikt z obiekt current() metody.</span><span class="sxs-lookup"><span data-stu-id="5e5af-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="5e5af-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="5e5af-206">Dodano obsługę dla indeksu dane geograficzne.</span><span class="sxs-lookup"><span data-stu-id="5e5af-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="5e5af-207">Weryfikuje właściwość identyfikatora dla wszystkich zasobów.</span><span class="sxs-lookup"><span data-stu-id="5e5af-207">Validates id property for all resources.</span></span> <span data-ttu-id="5e5af-208">Identyfikatory zasobów nie może zawierać?, /, # &#47; &#47; znaków ani kończyć spacją.</span><span class="sxs-lookup"><span data-stu-id="5e5af-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="5e5af-209">Dodaje nowego nagłówka "indeksu przekształcania toku" do ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="5e5af-209">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <span data-ttu-id="5e5af-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="5e5af-211">Implementuje zasady indeksowania V2.</span><span class="sxs-lookup"><span data-stu-id="5e5af-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="5e5af-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="5e5af-213">Problem [#40](https://github.com/Azure/azure-documentdb-node/issues/40) — zaimplementowana eslint grunt konfiguracje podstawowe i promise zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="5e5af-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span></span>

### <span data-ttu-id="5e5af-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="5e5af-215">Problem [#45](https://github.com/Azure/azure-documentdb-node/issues/45) -otoki ze zobowiązania nie zawiera nagłówka z powodu błędu.</span><span class="sxs-lookup"><span data-stu-id="5e5af-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="5e5af-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="5e5af-217">Zaimplementowany możliwość wykonywania kwerend konflikty, dodając readConflicts, readConflictAsync i queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="5e5af-217">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="5e5af-218">Zaktualizowana dokumentacja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5e5af-218">Updated API documentation.</span></span>
* <span data-ttu-id="5e5af-219">Problem [#41](https://github.com/Azure/azure-documentdb-node/issues/41) — błąd client.createDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="5e5af-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="5e5af-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="5e5af-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="5e5af-221">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="5e5af-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="5e5af-222">Wersja & daty wycofania</span><span class="sxs-lookup"><span data-stu-id="5e5af-222">Release & Retirement Dates</span></span>
<span data-ttu-id="5e5af-223">Firma Microsoft udostępnia powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w celu złagodzenia przejścia do nowszej/nieobsługiwaną wersję.</span><span class="sxs-lookup"><span data-stu-id="5e5af-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="5e5af-224">Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko do bieżącego zestawu SDK, w związku jest zalecane, zawsze Uaktualnij zestaw SDK najnowszą tak szybko jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="5e5af-224">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="5e5af-225">Każde żądanie przy użyciu rozwiązania Cosmos DB wycofane zestawu SDK jest odrzucane przez usługę.</span><span class="sxs-lookup"><span data-stu-id="5e5af-225">Any request to Cosmos DB using a retired SDK is be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="5e5af-226">Wersja</span><span class="sxs-lookup"><span data-stu-id="5e5af-226">Version</span></span> | <span data-ttu-id="5e5af-227">Data wydania</span><span class="sxs-lookup"><span data-stu-id="5e5af-227">Release Date</span></span> | <span data-ttu-id="5e5af-228">Dacie wycofania</span><span class="sxs-lookup"><span data-stu-id="5e5af-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="5e5af-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="5e5af-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="5e5af-230">10 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="5e5af-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="5e5af-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="5e5af-232">10 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="5e5af-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="5e5af-234">10 maja 2017</span><span class="sxs-lookup"><span data-stu-id="5e5af-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="5e5af-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="5e5af-236">16 marca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="5e5af-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="5e5af-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="5e5af-238">27 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="5e5af-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="5e5af-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="5e5af-240">22 grudnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="5e5af-242">03 października 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="5e5af-244">07 lipca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="5e5af-246">14 czerwca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="5e5af-248">26 kwietnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="5e5af-250">29 marca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="5e5af-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="5e5af-252">08 marca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="5e5af-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="5e5af-254">02 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="5e5af-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="5e5af-256">01 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="5e5af-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="5e5af-258">26 stycznia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="5e5af-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="5e5af-260">22 stycznia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="5e5af-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="5e5af-262">4 stycznia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="5e5af-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="5e5af-264">31 grudnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="5e5af-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="5e5af-266">06 października 2015</span><span class="sxs-lookup"><span data-stu-id="5e5af-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="5e5af-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="5e5af-268">06 października 2015</span><span class="sxs-lookup"><span data-stu-id="5e5af-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="5e5af-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="5e5af-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="5e5af-270">10 września 2015</span><span class="sxs-lookup"><span data-stu-id="5e5af-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="5e5af-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="5e5af-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="5e5af-272">15 sierpnia 2015</span><span class="sxs-lookup"><span data-stu-id="5e5af-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="5e5af-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="5e5af-274">05 sierpnia 2015</span><span class="sxs-lookup"><span data-stu-id="5e5af-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="5e5af-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="5e5af-276">09 lipca 2015 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="5e5af-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="5e5af-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="5e5af-278">04 czerwiec 2015 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="5e5af-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="5e5af-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="5e5af-280">23 maja 2015 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="5e5af-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="5e5af-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="5e5af-282">15 maja 2015 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="5e5af-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="5e5af-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="5e5af-284">08 kwietnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="5e5af-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="5e5af-285">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="5e5af-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="5e5af-286">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5e5af-286">See also</span></span>
<span data-ttu-id="5e5af-287">Aby dowiedzieć się więcej na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi.</span><span class="sxs-lookup"><span data-stu-id="5e5af-287">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

