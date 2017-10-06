---
title: "aaaAzure rozwiązania Cosmos DB .NET Core API zestawu SDK i zasoby | Dokumentacja firmy Microsoft"
description: "Dowiedz się wszystkiego o hello zestawu SDK, w tym daty wydania, daty wycofania i zmiany między poszczególnymi wersjami hello Azure rozwiązania Cosmos DB .NET Core SDK i interfejs API .NET Core."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="3ebcf-103">Azure rozwiązania Cosmos DB .NET Core SDK: Informacje o wersji i zasoby</span><span class="sxs-lookup"><span data-stu-id="3ebcf-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ebcf-104">.NET</span><span class="sxs-lookup"><span data-stu-id="3ebcf-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="3ebcf-105">Źródła danych zmian .NET</span><span class="sxs-lookup"><span data-stu-id="3ebcf-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="3ebcf-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3ebcf-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="3ebcf-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="3ebcf-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="3ebcf-108">Java</span><span class="sxs-lookup"><span data-stu-id="3ebcf-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="3ebcf-109">Python</span><span class="sxs-lookup"><span data-stu-id="3ebcf-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="3ebcf-110">REST</span><span class="sxs-lookup"><span data-stu-id="3ebcf-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="3ebcf-111">Dostawca zasobów REST</span><span class="sxs-lookup"><span data-stu-id="3ebcf-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="3ebcf-112">SQL</span><span class="sxs-lookup"><span data-stu-id="3ebcf-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="3ebcf-113">**Pobierz zestaw SDK**</span><span class="sxs-lookup"><span data-stu-id="3ebcf-113">**SDK download**</span></span></td><td>[<span data-ttu-id="3ebcf-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="3ebcf-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="3ebcf-115">**Dokumentacja interfejsu API**</span><span class="sxs-lookup"><span data-stu-id="3ebcf-115">**API documentation**</span></span></td><td>[<span data-ttu-id="3ebcf-116">Dokumentacji interfejsu API platformy .NET</span><span class="sxs-lookup"><span data-stu-id="3ebcf-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="3ebcf-117">**Przykłady**</span><span class="sxs-lookup"><span data-stu-id="3ebcf-117">**Samples**</span></span></td><td>[<span data-ttu-id="3ebcf-118">Przykłady kodu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="3ebcf-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="3ebcf-119">**Wprowadzenie**</span><span class="sxs-lookup"><span data-stu-id="3ebcf-119">**Get started**</span></span></td><td>[<span data-ttu-id="3ebcf-120">Rozpoczynanie pracy z hello Azure rozwiązania Cosmos DB .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="3ebcf-120">Get started with hello Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="3ebcf-121">**Samouczek aplikacji sieci Web**</span><span class="sxs-lookup"><span data-stu-id="3ebcf-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="3ebcf-122">Tworzenie aplikacji sieci Web z bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="3ebcf-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="3ebcf-123">**Bieżąca platforma obsługiwane**</span><span class="sxs-lookup"><span data-stu-id="3ebcf-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="3ebcf-124">.NET standard 1.6 i .NET Standard w wersji 1.5</span><span class="sxs-lookup"><span data-stu-id="3ebcf-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="3ebcf-125">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="3ebcf-125">Release Notes</span></span>

<span data-ttu-id="3ebcf-126">Hello Azure rozwiązania Cosmos DB .NET Core SDK ma parzystość funkcji z najnowszej wersji hello hello [zestawu .NET SDK usługi Azure rozwiązania Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3ebcf-126">hello Azure Cosmos DB .NET Core SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="3ebcf-127">Hello Azure rozwiązania Cosmos DB .NET Core SDK nie jest jeszcze zgodne z aplikacjami systemu Windows platformy Uniwersalnej.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-127">hello Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="3ebcf-128">Jeśli interesuje Cię hello .NET Core SDK, który obsługuje aplikacje platformy uniwersalnej systemu Windows, Wyślij wiadomość e-mail zbyt[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3ebcf-128">If you are interested in hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="3ebcf-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="3ebcf-130">Dodano obsługę PartitionKeyRangeId jako FeedOption do określania zakresu zapytania — wartość klucza zakresu określonej partycji tooa wyników.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results tooa specific partition key range value.</span></span> 
* <span data-ttu-id="3ebcf-131">Dodano obsługę StartTime jako toostart ChangeFeedOption, wyszukiwanie hello zmiany po upływie tego czasu.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-131">Added support for StartTime as a ChangeFeedOption toostart looking for hello changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="3ebcf-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="3ebcf-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="3ebcf-133">Rozwiązano problem w hello JsonSerializable klasy, która może spowodować wyjątek przepełnienia stosu.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-133">Fixed an issue in hello JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="3ebcf-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="3ebcf-135">Dodano obsługę służący do określania niestandardowej klasy JsonSerializerSettings podczas tworzenia wystąpienia [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="3ebcf-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="3ebcf-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="3ebcf-137">Obsługa platformy .NET Standard w wersji 1.5 wśród hello docelowych platform.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-137">Supporting .NET Standard 1.5 as one of hello target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="3ebcf-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="3ebcf-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="3ebcf-139">Rozwiązano problem dotyczący x64 maszyny, które nie obsługują instrukcji SSE4 i throw sehexception — podczas uruchamiania zapytań bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="3ebcf-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="3ebcf-141">Dodano obsługę nowego poziomu spójności o nazwie ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="3ebcf-142">Dodano obsługę metryki zapytania dla poszczególnych partycji.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="3ebcf-143">Dodano obsługę ograniczenie rozmiaru hello hello token kontynuacji dla zapytań.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-143">Added support for limiting hello size of hello continuation token for queries.</span></span>
*   <span data-ttu-id="3ebcf-144">Dodano obsługę dokładniejsze śledzenie niepomyślnych żądań.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="3ebcf-145">Niektóre ulepszenia wydajności w hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-145">Made some performance improvements in hello SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="3ebcf-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="3ebcf-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="3ebcf-147">Rozwiązano problem, który ignorowany podana w FeedOptions zapytania agregujące wartość PartitionKey hello.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-147">Fixed an issue that ignored hello PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="3ebcf-148">Rozwiązano problem w przezroczysty obsługi zarządzania partycji podczas pośredniej przesyłane między partycji Order By wykonywania zapytania.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="3ebcf-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="3ebcf-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="3ebcf-150">Rozwiązano problem, który spowodował zakleszczenie w niektórych async hello interfejsów API, gdy jest używany w kontekście programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-150">Fixed an issue which caused deadlocks in some of hello async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="3ebcf-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="3ebcf-152">Poprawki toomake SDK więcej tooautomatic odporność trybu failover, w niektórych warunkach.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-152">Fixes toomake SDK more resilient tooautomatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="3ebcf-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="3ebcf-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="3ebcf-154">Rozwiązać problemu, który czasami powoduje to klasa WebException: nie można rozpoznać nazwy zdalnej hello.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-154">Fix for an issue that occasionally causes a WebException: hello remote name could not be resolved.</span></span>
* <span data-ttu-id="3ebcf-155">Hello dodano obsługę bezpośrednio odczytywania typu dokumentu, dodając nowy interfejs API tooReadDocumentAsync przeciążenia.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-155">Added hello support for directly reading a typed document by adding new overloads tooReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="3ebcf-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="3ebcf-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="3ebcf-157">Dodano obsługę LINQ zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.).</span><span class="sxs-lookup"><span data-stu-id="3ebcf-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="3ebcf-158">Napraw problemu przeciek pamięci dla obiektu ConnectionPolicy hello spowodowane hello korzystanie z obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-158">Fix for a memory leak issue for hello ConnectionPolicy object caused by hello use of event handler.</span></span>
* <span data-ttu-id="3ebcf-159">Poprawkę dla problemu polegającego UpsertAttachmentAsync został nie działa, kiedy użyto ETag.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="3ebcf-160">Napraw problemu polegającego krzyżowego partycji zapytania według kontynuacji nie opracowanego podczas sortowania pola ciągu.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="3ebcf-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="3ebcf-162">Dodano obsługę zapytań agregacji (COUNT, MIN, MAX, SUM i Śr.).</span><span class="sxs-lookup"><span data-stu-id="3ebcf-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="3ebcf-163">Zobacz [Obsługa agregacji](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="3ebcf-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="3ebcf-164">Obniżony minimalnej przepustowości w kolekcji partycjonowanych z RU/s 10,100 too2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="3ebcf-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="3ebcf-166">Hello Azure rozwiązania Cosmos DB .NET Core SDK umożliwia toobuild szybkie, międzyplatformowa [platformy ASP.NET Core](https://www.asp.net/core) i [.NET Core](https://www.microsoft.com/net/core#windows) toorun aplikacji systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-166">hello Azure Cosmos DB .NET Core SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span> <span data-ttu-id="3ebcf-167">Witaj najnowszej wersji hello Azure rozwiązania Cosmos DB .NET Core SDK jest w pełni [Xamarin](https://www.xamarin.com) zgodny i aplikacje używane toobuild, przeznaczonych dla systemu iOS, Android i Mono (Linux).</span><span class="sxs-lookup"><span data-stu-id="3ebcf-167">hello latest release of hello Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used toobuild applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="3ebcf-168"><a name="0.1.0-preview"/>0.1.0-Preview</span><span class="sxs-lookup"><span data-stu-id="3ebcf-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="3ebcf-169">Hello Azure rozwiązania Cosmos DB .NET Core Podgląd SDK umożliwia toobuild szybkie, międzyplatformowa [platformy ASP.NET Core](https://www.asp.net/core) i [.NET Core](https://www.microsoft.com/net/core#windows) toorun aplikacji systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-169">hello Azure Cosmos DB .NET Core Preview SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="3ebcf-170">Hello Azure rozwiązania Cosmos DB .NET Core Podgląd SDK ma parzystość funkcji z najnowszej wersji hello hello [zestawu .NET SDK usługi Azure rozwiązania Cosmos DB](documentdb-sdk-dotnet.md) i obsługuje następujące hello:</span><span class="sxs-lookup"><span data-stu-id="3ebcf-170">hello Azure Cosmos DB .NET Core Preview SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports hello following:</span></span>
* <span data-ttu-id="3ebcf-171">Wszystkie [tryby połączeń](performance-tips.md#networking): tryb bramy, bezpośrednie TCP i bezpośredniego HTTPs.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="3ebcf-172">Wszystkie [poziomy spójności](consistency-levels.md): silne, sesji nieaktualności ograniczone i Eventual.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="3ebcf-173">[Kolekcje partycjonowane](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="3ebcf-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="3ebcf-174">[W przypadku bazy danych konta i replikacja geograficzna](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="3ebcf-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="3ebcf-175">Jeśli masz pytania pokrewne toothis SDK post zbyt[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), lub plik problemu w hello [repozytorium github](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="3ebcf-175">If you have questions related toothis SDK, post too[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in hello [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="3ebcf-176">Wersja & daty wycofania</span><span class="sxs-lookup"><span data-stu-id="3ebcf-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="3ebcf-177">Wersja</span><span class="sxs-lookup"><span data-stu-id="3ebcf-177">Version</span></span> | <span data-ttu-id="3ebcf-178">Data wydania</span><span class="sxs-lookup"><span data-stu-id="3ebcf-178">Release Date</span></span> | <span data-ttu-id="3ebcf-179">Dacie wycofania</span><span class="sxs-lookup"><span data-stu-id="3ebcf-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="3ebcf-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="3ebcf-181">10 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="3ebcf-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="3ebcf-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="3ebcf-183">07 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="3ebcf-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="3ebcf-185">02 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="3ebcf-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="3ebcf-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="3ebcf-187">12 czerwca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="3ebcf-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="3ebcf-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="3ebcf-189">23 maja 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="3ebcf-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="3ebcf-191">10 maja 2017</span><span class="sxs-lookup"><span data-stu-id="3ebcf-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="3ebcf-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="3ebcf-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="3ebcf-193">19 kwietnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="3ebcf-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="3ebcf-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="3ebcf-195">29 marca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="3ebcf-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="3ebcf-197">25 marca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="3ebcf-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="3ebcf-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="3ebcf-199">20 marca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="3ebcf-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="3ebcf-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="3ebcf-201">14 marca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="3ebcf-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="3ebcf-203">16 lutego 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="3ebcf-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3ebcf-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="3ebcf-205">21 grudnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="3ebcf-206">0.1.0-Preview</span><span class="sxs-lookup"><span data-stu-id="3ebcf-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="3ebcf-207">15 listopada 2016 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-207">November 15, 2016</span></span> |<span data-ttu-id="3ebcf-208">31 grudnia 2016 r.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="3ebcf-209">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3ebcf-209">See Also</span></span>
<span data-ttu-id="3ebcf-210">toolearn więcej informacji na temat rozwiązania Cosmos bazy danych, zobacz [bazy danych programu Microsoft Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) stronę usługi.</span><span class="sxs-lookup"><span data-stu-id="3ebcf-210">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

