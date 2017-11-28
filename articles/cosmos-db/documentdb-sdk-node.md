---
title: "aaaAzure rozwiązania Cosmos interfejsu API środowiska Node.js DB, zestaw SDK i zasoby | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o hello interfejsu API środowiska Node.js i zestawu SDK, w tym daty wydania, daty wycofania i zmiany między poszczególnymi wersjami hello Azure rozwiązania Cosmos DB Node.js SDK."
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
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="44af2-103">Zestaw SDK platformy Azure rozwiązania Cosmos DB Node.js: Informacje o wersji i zasoby</span><span class="sxs-lookup"><span data-stu-id="44af2-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="44af2-104">.NET</span><span class="sxs-lookup"><span data-stu-id="44af2-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="44af2-105">Źródła danych zmian .NET</span><span class="sxs-lookup"><span data-stu-id="44af2-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="44af2-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="44af2-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="44af2-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="44af2-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="44af2-108">Java</span><span class="sxs-lookup"><span data-stu-id="44af2-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="44af2-109">Python</span><span class="sxs-lookup"><span data-stu-id="44af2-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="44af2-110">REST</span><span class="sxs-lookup"><span data-stu-id="44af2-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="44af2-111">Dostawca zasobów REST</span><span class="sxs-lookup"><span data-stu-id="44af2-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="44af2-112">SQL</span><span class="sxs-lookup"><span data-stu-id="44af2-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="44af2-113">**Pobierz zestaw SDK**</span><span class="sxs-lookup"><span data-stu-id="44af2-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="44af2-114">NPM</span><span class="sxs-lookup"><span data-stu-id="44af2-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="44af2-115">**Dokumentacja interfejsu API**</span><span class="sxs-lookup"><span data-stu-id="44af2-115">**API documentation**</span></span></td><td>[<span data-ttu-id="44af2-116">Dokumentacji interfejsu API środowiska node.js</span><span class="sxs-lookup"><span data-stu-id="44af2-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="44af2-117">**Instrukcje dotyczące instalacji zestawu SDK**</span><span class="sxs-lookup"><span data-stu-id="44af2-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="44af2-118">Instrukcje dotyczące instalacji</span><span class="sxs-lookup"><span data-stu-id="44af2-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="44af2-119">**Współtworzenia tooSDK**</span><span class="sxs-lookup"><span data-stu-id="44af2-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="44af2-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="44af2-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="44af2-121">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="44af2-121">**Samples**</span></span></td><td>[<span data-ttu-id="44af2-122">Przykłady kodu node.js</span><span class="sxs-lookup"><span data-stu-id="44af2-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="44af2-123">**Samouczek z wprowadzeniem**</span><span class="sxs-lookup"><span data-stu-id="44af2-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="44af2-124">Rozpoczynanie pracy z hello Node.js SDK</span><span class="sxs-lookup"><span data-stu-id="44af2-124">Get started with hello Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="44af2-125">**Samouczek aplikacji sieci Web**</span><span class="sxs-lookup"><span data-stu-id="44af2-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="44af2-126">Tworzenie aplikacji sieci web Node.js za pomocą bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="44af2-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="44af2-127">**Bieżący obsługiwanych platform**</span><span class="sxs-lookup"><span data-stu-id="44af2-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="44af2-128">6.x node.js</span><span class="sxs-lookup"><span data-stu-id="44af2-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="44af2-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="44af2-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="44af2-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="44af2-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="44af2-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="44af2-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="44af2-132">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="44af2-132">Release notes</span></span>

### <span data-ttu-id="44af2-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="44af2-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="44af2-134">Dokumentacja programu npm stałej.</span><span class="sxs-lookup"><span data-stu-id="44af2-134">npm documentation fixed.</span></span>

### <span data-ttu-id="44af2-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="44af2-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="44af2-136">Stała usterki executeStoredProcedure, w którym dokumenty ma specjalne znaków Unicode (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="44af2-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="44af2-137">Stałe usterki w obsłudze dokumenty zawierające znaki Unicode w hello klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="44af2-137">Fixed a bug in handling documents with Unicode characters in hello partition key.</span></span>
* <span data-ttu-id="44af2-138">Stały obsługę tworzenia kolekcji hello nazwa nośnika.</span><span class="sxs-lookup"><span data-stu-id="44af2-138">Fixed support for creating collections with hello name media.</span></span> <span data-ttu-id="44af2-139">Problem Github #114.</span><span class="sxs-lookup"><span data-stu-id="44af2-139">Github issue #114.</span></span>
* <span data-ttu-id="44af2-140">Stałe obsługę token autoryzacji uprawnień.</span><span class="sxs-lookup"><span data-stu-id="44af2-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="44af2-141">Problem Github #178.</span><span class="sxs-lookup"><span data-stu-id="44af2-141">Github issue #178.</span></span>

### <span data-ttu-id="44af2-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="44af2-143">Dodano nową obsługę [poziomu spójności](consistency-levels.md) o nazwie ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="44af2-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="44af2-144">Dodano obsługę UriFactory.</span><span class="sxs-lookup"><span data-stu-id="44af2-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="44af2-145">Stałe błędów obsługę standardu Unicode.</span><span class="sxs-lookup"><span data-stu-id="44af2-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="44af2-146">Problem GitHub #171.</span><span class="sxs-lookup"><span data-stu-id="44af2-146">GitHub issue #171.</span></span>

### <span data-ttu-id="44af2-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="44af2-148">Obsługa hello dodanych zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.).</span><span class="sxs-lookup"><span data-stu-id="44af2-148">Added hello support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="44af2-149">Opcja hello dodany do kontrolowania stopień równoległości dla wielu partycji zapytań.</span><span class="sxs-lookup"><span data-stu-id="44af2-149">Added hello option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="44af2-150">Opcja dodano hello wyłączenie protokołu SSL weryfikacji podczas uruchamiania emulatora DB rozwiązania Cosmos Azure.</span><span class="sxs-lookup"><span data-stu-id="44af2-150">Added hello option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="44af2-151">Obniżony minimalnej przepustowości w kolekcji partycjonowanych z RU/s 10,100 too2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="44af2-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="44af2-152">Stałe hello kontynuacji tokenu usterki dla kolekcji jednej partycji.</span><span class="sxs-lookup"><span data-stu-id="44af2-152">Fixed hello continuation token bug for single partition collection.</span></span> <span data-ttu-id="44af2-153">Problem Github #107.</span><span class="sxs-lookup"><span data-stu-id="44af2-153">Github issue #107.</span></span>
* <span data-ttu-id="44af2-154">Błąd executeStoredProcedure hello stałej w obsługi 0 jako pojedynczy parametr.</span><span class="sxs-lookup"><span data-stu-id="44af2-154">Fixed hello executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="44af2-155">Problem Github #155.</span><span class="sxs-lookup"><span data-stu-id="44af2-155">Github issue #155.</span></span>

### <span data-ttu-id="44af2-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="44af2-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="44af2-157">Stałe agenta użytkownika nagłówka tooinclude hello zestawu SDK w wersji.</span><span class="sxs-lookup"><span data-stu-id="44af2-157">Fixed user-agent header tooinclude hello SDK version.</span></span>
* <span data-ttu-id="44af2-158">Oczyszczanie kodu pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="44af2-158">Minor code cleanup.</span></span>

### <span data-ttu-id="44af2-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="44af2-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="44af2-160">Wyłączanie weryfikacji SSL, używając hello SDK tootarget hello emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="44af2-160">Disabling SSL verification when using hello SDK tootarget hello emulator(hostname=localhost).</span></span>
* <span data-ttu-id="44af2-161">Dodano obsługę Włączanie rejestrowania skryptu podczas wykonywania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="44af2-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="44af2-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="44af2-163">Dodano obsługę dla wielu partycji zapytania równoległe.</span><span class="sxs-lookup"><span data-stu-id="44af2-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="44af2-164">Dodano obsługę TOP/ORDER BY zapytania dla kolekcji partycjonowanych.</span><span class="sxs-lookup"><span data-stu-id="44af2-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="44af2-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="44af2-166">Obsługa zasad dodano ponownych prób dla żądań z ograniczeniem przepustowości.</span><span class="sxs-lookup"><span data-stu-id="44af2-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="44af2-167">(Ograniczeniem przepustowości żądania odbierania żądania szybkość zbyt duży wyjątek, kod błędu 429.) Domyślnie bazy danych Azure rozwiązania Cosmos ponowi próbę dziewięciokrotnie dla każdego żądania po napotkaniu błędu kodu 429 ramach czasu retryAfter hello hello nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="44af2-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="44af2-168">Czas interwału ponawiania stałym teraz można ustawić jako część hello RetryOptions właściwości w obiekcie ConnectionPolicy hello Jeśli czas retryAfter hello tooignore zwrócony przez serwer między kolejnymi próbami hello.</span><span class="sxs-lookup"><span data-stu-id="44af2-168">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="44af2-169">Azure DB rozwiązania Cosmos teraz czeka na maksymalnie 30 sekund na każde żądanie jest ograniczane (niezależnie od liczby ponownych prób) i zwracającej odpowiedź hello 429 kod błędu.</span><span class="sxs-lookup"><span data-stu-id="44af2-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="44af2-170">Teraz zostać zastąpiona w taki sposób, w hello RetryOptions właściwości w obiekcie ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="44af2-170">This time can also be overridden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="44af2-171">Rozwiązania cosmos DB teraz zwraca x-ms ograniczania liczby ponownych prób i x-ms-throttle-retry-wait-time-ms hello i liczba skumulowany czas hello żądania oczekiwano między kolejnymi próbami hello ponów próbę hello nagłówków odpowiedzi w ograniczania hello toodenote każdego żądania.</span><span class="sxs-lookup"><span data-stu-id="44af2-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cumulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="44af2-172">Dodano Hello klasy RetryOptions udostępnianie właściwości RetryOptions hello na powitania ConnectionPolicy klasy, które mogą być używane toooverride niektóre hello domyślne opcje ponawiania.</span><span class="sxs-lookup"><span data-stu-id="44af2-172">hello RetryOptions class was added, exposing hello RetryOptions property on hello ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <span data-ttu-id="44af2-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="44af2-174">Hello dodano obsługę konta w przypadku bazy danych.</span><span class="sxs-lookup"><span data-stu-id="44af2-174">Added hello support for multi-region database accounts.</span></span>

### <span data-ttu-id="44af2-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="44af2-176">Witaj dodano obsługę funkcji tooLive(TTL) czasu dla dokumentów.</span><span class="sxs-lookup"><span data-stu-id="44af2-176">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <span data-ttu-id="44af2-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="44af2-178">Zaimplementowane [kolekcje partycjonowane](partition-data.md) i [poziomy wydajności zdefiniowanych przez użytkownika](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="44af2-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="44af2-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="44af2-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="44af2-180">Stałe usterki RangePartitionResolver.resolveForRead gdzie nie został zwrócił łącza powodu tooa concat nieprawidłowych wyników.</span><span class="sxs-lookup"><span data-stu-id="44af2-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due tooa bad concat of results.</span></span>

### <span data-ttu-id="44af2-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="44af2-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="44af2-182">Stałe hashParitionResolver resolveForRead(): gdy nie podany klucz partycji została Zgłaszanie wyjątku, zamiast zwracać listę wszystkich zarejestrowanych łączy.</span><span class="sxs-lookup"><span data-stu-id="44af2-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="44af2-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="44af2-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="44af2-184">Rozwiązuje problem [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -agenta w wersji dedykowanej HTTPS: unikać modyfikacji hello globalne agenta do celów bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="44af2-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying hello global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="44af2-185">Użyj dedykowanych agenta dla wszystkich żądań hello lib.</span><span class="sxs-lookup"><span data-stu-id="44af2-185">Use a dedicated agent for all of hello lib’s requests.</span></span>

### <span data-ttu-id="44af2-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="44af2-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="44af2-187">Rozwiązuje problem [#81](https://github.com/Azure/azure-documentdb-node/issues/81) — poprawnie obsłużyć myślniki identyfikatory nośników.</span><span class="sxs-lookup"><span data-stu-id="44af2-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="44af2-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="44af2-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="44af2-189">Rozwiązuje problem [#95](https://github.com/Azure/azure-documentdb-node/issues/95) -odbiornika EventEmitter wyciek ostrzeżenie.</span><span class="sxs-lookup"><span data-stu-id="44af2-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="44af2-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="44af2-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="44af2-191">Rozwiązuje problem [#92](https://github.com/Azure/azure-documentdb-node/issues/90) — Zmień nazwę folderu toohash wyznaczania wartości skrótu dla systemów z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="44af2-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash toohash for case-sensitive systems.</span></span>

### <span data-ttu-id="44af2-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="44af2-193">Implementowanie obsługi dzielenia na fragmenty przez dodanie skrótów & zakres rozpoznawania nazw partycji.</span><span class="sxs-lookup"><span data-stu-id="44af2-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="44af2-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="44af2-195">Implementuje Upsert.</span><span class="sxs-lookup"><span data-stu-id="44af2-195">Implement Upsert.</span></span> <span data-ttu-id="44af2-196">Nowych metod upsertXXX na documentClient.</span><span class="sxs-lookup"><span data-stu-id="44af2-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="44af2-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="44af2-198">Numery wersji pominięto toobring wyrównania z innych zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="44af2-198">Skipped toobring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="44af2-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="44af2-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="44af2-200">Q podziału niesie obietnice otoki toonew repozytorium.</span><span class="sxs-lookup"><span data-stu-id="44af2-200">Split Q promises wrapper toonew repository.</span></span>
* <span data-ttu-id="44af2-201">Plik toopackage aktualizacji rejestru npm.</span><span class="sxs-lookup"><span data-stu-id="44af2-201">Update toopackage file for npm registry.</span></span>

### <span data-ttu-id="44af2-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="44af2-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="44af2-203">Implementuje identyfikator oparte na routingu.</span><span class="sxs-lookup"><span data-stu-id="44af2-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="44af2-204">Rozwiązuje problem [#49](https://github.com/Azure/azure-documentdb-node/issues/49) -bieżącej właściwości powoduje konflikt z obiekt current() metody.</span><span class="sxs-lookup"><span data-stu-id="44af2-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="44af2-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="44af2-206">Dodano obsługę dla indeksu dane geograficzne.</span><span class="sxs-lookup"><span data-stu-id="44af2-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="44af2-207">Weryfikuje właściwość identyfikatora dla wszystkich zasobów.</span><span class="sxs-lookup"><span data-stu-id="44af2-207">Validates id property for all resources.</span></span> <span data-ttu-id="44af2-208">Identyfikatory zasobów nie może zawierać?, /, # &#47; &#47; znaków ani kończyć spacją.</span><span class="sxs-lookup"><span data-stu-id="44af2-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="44af2-209">Dodaje nowy tooResourceResponse "postępu przekształcania indeksu" nagłówka.</span><span class="sxs-lookup"><span data-stu-id="44af2-209">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <span data-ttu-id="44af2-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="44af2-211">Implementuje zasady indeksowania V2.</span><span class="sxs-lookup"><span data-stu-id="44af2-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="44af2-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="44af2-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="44af2-213">Problem [#40](https://github.com/Azure/azure-documentdb-node/issues/40) — zaimplementowana eslint grunt konfiguracje podstawowe hello i promise zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="44af2-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in hello core and promise SDK.</span></span>

### <span data-ttu-id="44af2-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="44af2-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="44af2-215">Problem [#45](https://github.com/Azure/azure-documentdb-node/issues/45) -otoki ze zobowiązania nie zawiera nagłówka z powodu błędu.</span><span class="sxs-lookup"><span data-stu-id="44af2-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="44af2-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="44af2-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="44af2-217">Możliwości implementowane tooquery konflikty, dodając readConflicts, readConflictAsync i queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="44af2-217">Implemented ability tooquery for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="44af2-218">Zaktualizowana dokumentacja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="44af2-218">Updated API documentation.</span></span>
* <span data-ttu-id="44af2-219">Problem [#41](https://github.com/Azure/azure-documentdb-node/issues/41) — błąd client.createDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="44af2-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="44af2-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="44af2-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="44af2-221">GA SDK.</span><span class="sxs-lookup"><span data-stu-id="44af2-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="44af2-222">Wersja & daty wycofania</span><span class="sxs-lookup"><span data-stu-id="44af2-222">Release & Retirement Dates</span></span>
<span data-ttu-id="44af2-223">Firma Microsoft udostępnia powiadomienia co najmniej **12 miesięcy** klienta z wyprzedzeniem wycofanie SDK w kolejności toosmooth hello przejścia tooa nowszej/nieobsługiwaną wersję.</span><span class="sxs-lookup"><span data-stu-id="44af2-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="44af2-224">Nowe funkcje i funkcjonalność i optymalizację, które są dodawane tylko toohello bieżącego zestawu SDK, w związku zaleca się tego należy zawsze uaktualnienia toohello najnowszego zestawu SDK w wersji możliwie jak najszybciej.</span><span class="sxs-lookup"><span data-stu-id="44af2-224">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommended that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="44af2-225">Każde żądanie tooCosmos bazy danych przy użyciu wycofane zestawu SDK jest odrzucane przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="44af2-225">Any request tooCosmos DB using a retired SDK is be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="44af2-226">Wersja</span><span class="sxs-lookup"><span data-stu-id="44af2-226">Version</span></span> | <span data-ttu-id="44af2-227">Data wydania</span><span class="sxs-lookup"><span data-stu-id="44af2-227">Release Date</span></span> | <span data-ttu-id="44af2-228">Dacie wycofania</span><span class="sxs-lookup"><span data-stu-id="44af2-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="44af2-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="44af2-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="44af2-230">10 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="44af2-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="44af2-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="44af2-232">10 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="44af2-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="44af2-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="44af2-234">10 maja 2017</span><span class="sxs-lookup"><span data-stu-id="44af2-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="44af2-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="44af2-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="44af2-236">16 marca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="44af2-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="44af2-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="44af2-238">27 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="44af2-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="44af2-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="44af2-240">22 grudnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="44af2-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="44af2-242">03 października 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="44af2-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="44af2-244">07 lipca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="44af2-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="44af2-246">14 czerwca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="44af2-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="44af2-248">26 kwietnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="44af2-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="44af2-250">29 marca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="44af2-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="44af2-252">08 marca 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="44af2-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="44af2-254">02 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="44af2-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="44af2-256">01 lutego 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="44af2-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="44af2-258">26 stycznia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="44af2-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="44af2-260">22 stycznia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="44af2-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="44af2-262">4 stycznia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="44af2-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="44af2-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="44af2-264">31 grudnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="44af2-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="44af2-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="44af2-266">06 października 2015</span><span class="sxs-lookup"><span data-stu-id="44af2-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="44af2-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="44af2-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="44af2-268">06 października 2015</span><span class="sxs-lookup"><span data-stu-id="44af2-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="44af2-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="44af2-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="44af2-270">10 września 2015</span><span class="sxs-lookup"><span data-stu-id="44af2-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="44af2-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="44af2-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="44af2-272">15 sierpnia 2015</span><span class="sxs-lookup"><span data-stu-id="44af2-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="44af2-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="44af2-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="44af2-274">05 sierpnia 2015</span><span class="sxs-lookup"><span data-stu-id="44af2-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="44af2-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="44af2-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="44af2-276">09 lipca 2015 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="44af2-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="44af2-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="44af2-278">04 czerwiec 2015 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="44af2-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="44af2-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="44af2-280">23 maja 2015 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="44af2-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="44af2-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="44af2-282">15 maja 2015 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="44af2-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="44af2-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="44af2-284">08 kwietnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="44af2-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="44af2-285">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="44af2-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="44af2-286">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="44af2-286">See also</span></span>
<span data-ttu-id="44af2-287">toolearn więcej informacji na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi.</span><span class="sxs-lookup"><span data-stu-id="44af2-287">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

