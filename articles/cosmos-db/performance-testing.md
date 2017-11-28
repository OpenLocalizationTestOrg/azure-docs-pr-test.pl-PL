---
title: "aaaAzure DB rozwiązania Cosmos skali i testowania wydajności | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skalować tooperform i testowania wydajności z bazy danych Azure rozwiązania Cosmos"
keywords: "Testowanie wydajności"
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="ee2bc-104">Wydajność i skalę testowania z bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="ee2bc-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="ee2bc-105">Skala testowanie wydajności i jest klucza krok w rozwoju aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="ee2bc-106">Dla wielu aplikacji hello warstwy bazy danych ma znaczący wpływ na hello ogólną wydajność i skalowalność i w związku z tym składnikiem krytycznym wydajności testuje.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-106">For many applications, hello database tier has a significant impact on hello overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="ee2bc-107">[Azure DB rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) jest dedykowanym elastycznego skalowania przewidywalną wydajność i w związku z tym stanowi doskonałe dopasowanie dla aplikacji, które wymagają warstwy wysokiej wydajności bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="ee2bc-108">W tym artykule jest odwołaniem dla deweloperów wykonania testów wydajności dla obciążeń DB rozwiązania Cosmos lub obliczenia DB rozwiązania Cosmos w scenariuszach wysokiej wydajności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="ee2bc-109">Skupiono się głównie na testowania wydajności izolowanego hello bazy danych, ale zawiera również najlepsze rozwiązania dotyczące aplikacji produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-109">It focuses primarily on isolated performance testing of hello database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="ee2bc-110">Po przeczytaniu tego artykułu, będą mogli tooanswer hello następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="ee2bc-110">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="ee2bc-111">Gdzie mogę znaleźć przykładowej aplikacji .NET klienta do testowania wydajności DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="ee2bc-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="ee2bc-112">Jak osiągnięcia wysokiej przepływności poziomy DB rozwiązania Cosmos z mojej aplikacji klienta?</span><span class="sxs-lookup"><span data-stu-id="ee2bc-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="ee2bc-113">tooget wprowadzenie kodu, Pobierz hello projektu z [próbka testowania wydajności bazy danych rozwiązania Cosmos Azure](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="ee2bc-113">tooget started with code, please download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="ee2bc-114">Celem tej aplikacji Hello jest toodemonstrate najlepsze rozwiązania dotyczące wyodrębniania lepszą wydajność poza DB rozwiązania Cosmos o niewielkiej liczby komputerów klienckich.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-114">hello goal of this application is toodemonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="ee2bc-115">Nie przeprowadzono toodemonstrate hello szczytu pojemności hello usługi, które można skalować nieograniczony.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-115">This was not made toodemonstrate hello peak capacity of hello service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="ee2bc-116">Jeśli szukasz tooimprove opcje konfiguracji po stronie klienta DB rozwiązania Cosmos wydajności, zobacz [porady dotyczące wydajności bazy danych Azure rozwiązania Cosmos](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="ee2bc-116">If you're looking for client-side configuration options tooimprove Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-hello-performance-testing-application"></a><span data-ttu-id="ee2bc-117">Uruchom testowanie aplikacji hello wydajności</span><span class="sxs-lookup"><span data-stu-id="ee2bc-117">Run hello performance testing application</span></span>
<span data-ttu-id="ee2bc-118">Witaj najszybszy sposób tooget uruchomiona jest toocompile i wykonywania hello .NET przykładowa poniżej, zgodnie z opisem w poniższych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-118">hello quickest way tooget started is toocompile and run hello .NET sample below, as described in hello steps below.</span></span> <span data-ttu-id="ee2bc-119">Można również przejrzeć kod źródłowy hello i wdrożenia podobnych konfiguracji tooyour klienta własnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-119">You can also review hello source code and implement similar configurations tooyour own client applications.</span></span>

<span data-ttu-id="ee2bc-120">**Krok 1:** pobierania hello projektu z [próbka testowania wydajności bazy danych rozwiązania Cosmos Azure](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), lub repozytorium GitHub hello rozwidlenia.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-120">**Step 1:** Download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork hello GitHub repository.</span></span>

<span data-ttu-id="ee2bc-121">**Krok 2:** zmodyfikować ustawienia hello EndpointUrl i AuthorizationKey, CollectionThroughput DocumentTemplate (opcjonalnie) w pliku App.config.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-121">**Step 2:** Modify hello settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="ee2bc-122">Przed zainicjowaniem obsługi administracyjnej kolekcje z wysokiej przepływności, zobacz toohello [stronie cennika](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate koszty hello na kolekcję.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-122">Before provisioning collections with high throughput, please refer toohello [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello costs per collection.</span></span> <span data-ttu-id="ee2bc-123">Azure DB rozwiązania Cosmos rachunków pamięci masowej i przepływność niezależnie co godzinę, więc można zmniejszyć koszty przez usunięcie lub zmniejszenie przepływności hello kolekcji bazy danych rozwiązania Cosmos Azure po zakończeniu testowania.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering hello throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="ee2bc-124">**Krok 3:** skompilować i uruchomić z wiersza polecenia hello hello aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-124">**Step 3:** Compile and run hello console app from hello command line.</span></span> <span data-ttu-id="ee2bc-125">Powinny pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="ee2bc-125">You should see output like hello following:</span></span>

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


<span data-ttu-id="ee2bc-126">**Krok 4 (Jeśli to konieczne):** hello przepływności zgłoszone (RU/s) z narzędzia hello powinna być hello tego samego lub wyższego niż hello udostępnionej przepływności hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-126">**Step 4 (if necessary):** hello throughput reported (RU/s) from hello tool should be hello same or higher than hello provisioned throughput of hello collection.</span></span> <span data-ttu-id="ee2bc-127">Jeśli nie, zwiększa hello DegreeOfParallelism w małych odstępach mogą pomóc w osiągnięciu limitu hello.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-127">If not, increasing hello DegreeOfParallelism in small increments may help you reach hello limit.</span></span> <span data-ttu-id="ee2bc-128">Jeśli płaskowyżach przepływności hello z aplikacji klienta, uruchamianie wielu wystąpień aplikacji hello na hello takie same lub różnych maszyn mogą pomóc w osiągnięciu limitu hello udostępniane między hello różnymi wystąpieniami.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-128">If hello throughput from your client app plateaus, launching multiple instances of hello app on hello same or different machines will help you reach hello provisioned limit across hello different instances.</span></span> <span data-ttu-id="ee2bc-129">Jeśli potrzebujesz pomocy w ramach tego kroku, napisz wiadomość e-mail tooaskcosmosdb@microsoft.com lub pliku biletu pomocy technicznej z hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee2bc-129">If you need help with this step, please, write an email tooaskcosmosdb@microsoft.com or file a support ticket from hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="ee2bc-130">Po uruchomieniu aplikacji hello, możesz spróbować innego [zasady indeksowania](indexing-policies.md) i [poziomy spójności](consistency-levels.md) toounderstand ich wpływ na przepustowości i opóźnień.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-130">Once you have hello app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) toounderstand their impact on throughput and latency.</span></span> <span data-ttu-id="ee2bc-131">Można również przejrzeć kod źródłowy hello i implementować podobnych konfiguracji tooyour własnych testów lub aplikacje produkcyjne.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-131">You can also review hello source code and implement similar configurations tooyour own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee2bc-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ee2bc-132">Next steps</span></span>
<span data-ttu-id="ee2bc-133">W tym artykule analizujemy sposobu wykonywania wydajności i skalowania testowanie za pomocą rozwiązania Cosmos bazy danych przy użyciu aplikacji konsoli .NET.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="ee2bc-134">Aby uzyskać dodatkowe informacje na temat pracy z bazy danych Azure rozwiązania Cosmos, zapoznaj się z łącza toohello poniżej.</span><span class="sxs-lookup"><span data-stu-id="ee2bc-134">Please refer toohello links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="ee2bc-135">Testowanie próbki Azure wydajności bazy danych rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="ee2bc-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="ee2bc-136">Tooimprove opcje konfiguracji klienta wydajności bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="ee2bc-136">Client configuration options tooimprove Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="ee2bc-137">Partycjonowanie po stronie serwera w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="ee2bc-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


