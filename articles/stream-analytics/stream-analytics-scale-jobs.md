---
title: "Przepływność tooincrease zadania usługi analiza strumienia aaaScale | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zadania usługi analiza strumienia tooscale Konfigurowanie partycji wejściowych, dostrajanie hello definicji zapytania i ustawiając zadania jednostki przesyłania strumieniowego."
keywords: "przesyłanie strumieniowe, danych przesyłania strumieniowego przetwarzania danych, dostroić analityka"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a><span data-ttu-id="45138-104">Skalowanie usługi Azure Stream Analytics zadania tooincrease strumienia przetwarzania danych przepływności</span><span class="sxs-lookup"><span data-stu-id="45138-104">Scale Azure Stream Analytics jobs tooincrease stream data processing throughput</span></span>
<span data-ttu-id="45138-105">W tym artykule opisano, jak tootune Stream Analytics zapytania tooincrease przepływność dla zadań przesyłania strumieniowego usługi Analytics.</span><span class="sxs-lookup"><span data-stu-id="45138-105">This article shows you how tootune a Stream Analytics query tooincrease throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="45138-106">Dowiedz się, jak tooscale analiza strumienia zadania przez skonfigurowanie wejściowych partycji, dostrajania analytics hello zapytania definicji i obliczanie i ustawiania zadania *jednostki przesyłania strumieniowego* (SUs).</span><span class="sxs-lookup"><span data-stu-id="45138-106">You learn how tooscale Stream Analytics jobs by configuring input partitions, tuning hello analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a><span data-ttu-id="45138-107">Co to są hello części zadanie usługi Stream Analytics?</span><span class="sxs-lookup"><span data-stu-id="45138-107">What are hello parts of a Stream Analytics job?</span></span>
<span data-ttu-id="45138-108">Definicji zadania Stream Analytics zawiera dane wejściowe, zapytań i danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="45138-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="45138-109">Dane wejściowe są, gdzie hello zadania odczytuje hello strumień danych.</span><span class="sxs-lookup"><span data-stu-id="45138-109">Inputs are where hello job reads hello data stream from.</span></span> <span data-ttu-id="45138-110">Hello zapytania jest strumienia danych wejściowych hello tootransform używane, a dane wyjściowe hello jest gdzie zadanie hello wysyła hello wyniki zadania do.</span><span class="sxs-lookup"><span data-stu-id="45138-110">hello query is used tootransform hello data input stream, and hello output is where hello job sends hello job results to.</span></span>  

<span data-ttu-id="45138-111">Zadanie wymaga co najmniej jedno źródło danych wejściowych do strumieniowego przesyłania danych.</span><span class="sxs-lookup"><span data-stu-id="45138-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="45138-112">Witaj źródło wejścia strumienia danych mogą być przechowywane w Centrum zdarzeń platformy Azure lub w magazynie obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="45138-112">hello data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="45138-113">Aby uzyskać więcej informacji, zobacz [tooAzure wprowadzenie Stream Analytics](stream-analytics-introduction.md) i [rozpocząć korzystanie z usługi Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="45138-113">For more information, see [Introduction tooAzure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="45138-114">Partycje w centra zdarzeń i magazynu systemu Azure</span><span class="sxs-lookup"><span data-stu-id="45138-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="45138-115">Skalowanie zadania Stream Analytics korzysta z partycji w hello wejściowych lub wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="45138-115">Scaling a Stream Analytics job takes advantage of partitions in hello input or output.</span></span> <span data-ttu-id="45138-116">Partycjonowanie umożliwia dzielenia danych na podzestawy oparte na kluczu partycji.</span><span class="sxs-lookup"><span data-stu-id="45138-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="45138-117">Proces, który używa danych hello (na przykład zadanie analizy przesyłania strumieniowego) może wykorzystywać i zapisać różnych partycji równolegle, co zwiększa przepustowość.</span><span class="sxs-lookup"><span data-stu-id="45138-117">A process that consumes hello data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="45138-118">Podczas pracy z analizy przesyłania strumieniowego, możesz korzystać z partycjonowania usługi event hubs i w magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="45138-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="45138-119">Aby uzyskać więcej informacji o partycjach zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="45138-119">For more information about partitions, see hello following articles:</span></span>

* [<span data-ttu-id="45138-120">Omówienie funkcji usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="45138-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="45138-121">Partycjonowanie danych</span><span class="sxs-lookup"><span data-stu-id="45138-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="45138-122">Jednostki przesyłania strumieniowego (SUs)</span><span class="sxs-lookup"><span data-stu-id="45138-122">Streaming units (SUs)</span></span>
<span data-ttu-id="45138-123">Przesyłanie strumieniowe jednostki (SUs) reprezentuje hello zasobów i przetwarzania danych zasilania, które są wymagane w kolejności tooexecute zadanie usługi analiza strumienia Azure.</span><span class="sxs-lookup"><span data-stu-id="45138-123">Streaming units (SUs) represent hello resources and computing power that are required in order tooexecute an Azure Stream Analytics job.</span></span> <span data-ttu-id="45138-124">Usługi SUs zapewniają sposób toodescribe hello względną przetwarzania zdarzeń pojemności oparte na mieszanych pomiarach Procesora, pamięci, Odczyt i zapis stawki.</span><span class="sxs-lookup"><span data-stu-id="45138-124">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="45138-125">Każdy SU odpowiada tooroughly 1 MB/s przepustowości.</span><span class="sxs-lookup"><span data-stu-id="45138-125">Each SU corresponds tooroughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="45138-126">Wybranie liczby SUs są wymagane dla określonego zadania zależy od hello konfiguracji partycji dla danych wejściowych hello kwerendy hello zdefiniowanej dla hello zadania.</span><span class="sxs-lookup"><span data-stu-id="45138-126">Choosing how many SUs are required for a particular job depends on hello partition configuration for hello inputs and on hello query defined for hello job.</span></span> <span data-ttu-id="45138-127">Możesz wybrać zapasowej przydziału tooyour w SUs dla zadania.</span><span class="sxs-lookup"><span data-stu-id="45138-127">You can select up tooyour quota in SUs for a job.</span></span> <span data-ttu-id="45138-128">Domyślnie każdej subskrypcji platformy Azure ma przydziału zapasowej SUs too50 dla wszystkich zadań analizy hello w określonym regionie.</span><span class="sxs-lookup"><span data-stu-id="45138-128">By default, each Azure subscription has a quota of up too50 SUs for all hello analytics jobs in a specific region.</span></span> <span data-ttu-id="45138-129">tooincrease SUs dla subskrypcji przekracza ten limit przydziału, skontaktuj się z [Microsoft Support](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="45138-129">tooincrease SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="45138-130">Prawidłowe wartości SUs na zadanie to 1, 3, 6 oraz w przyrostach 6.</span><span class="sxs-lookup"><span data-stu-id="45138-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="45138-131">Embarrassingly równoległych zadań</span><span class="sxs-lookup"><span data-stu-id="45138-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="45138-132">*Embarrassingly równoległych* zadania jest scenariusz najbardziej skalowalny hello mamy w Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="45138-132">An *embarrassingly parallel* job is hello most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="45138-133">Łączy jedną partycję hello wejściowych tooone wystąpienia partycji tooone kwerendy hello hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="45138-133">It connects one partition of hello input tooone instance of hello query tooone partition of hello output.</span></span> <span data-ttu-id="45138-134">Równoległość ten ma hello następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="45138-134">This parallelism has hello following requirements:</span></span>

1. <span data-ttu-id="45138-135">Logika zapytania jest zależna od hello klucza przetwarzanych przez hello sam kwerendy wystąpienia, należy upewnić się, że zdarzenia hello Przejdź toohello tej samej partycji dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="45138-135">If your query logic depends on hello same key being processed by hello same query instance, you must make sure that hello events go toohello same partition of your input.</span></span> <span data-ttu-id="45138-136">Usługi event hubs, oznacza to, że hello zdarzeń danych muszą mieć hello **PartitionKey** zestawu wartości.</span><span class="sxs-lookup"><span data-stu-id="45138-136">For event hubs, this means that hello event data must have hello **PartitionKey** value set.</span></span> <span data-ttu-id="45138-137">Alternatywnie można użyć nadawców podzielonym na partycje.</span><span class="sxs-lookup"><span data-stu-id="45138-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="45138-138">W przypadku magazynu obiektów blob, oznacza to, że hello zdarzenia są wysyłane toohello tego samego folderu partycji.</span><span class="sxs-lookup"><span data-stu-id="45138-138">For blob storage, this means that hello events are sent toohello same partition folder.</span></span> <span data-ttu-id="45138-139">Logiki kwerendy nie wymaga hello klucza toobe przetworzone przez hello sam kwerendy wystąpienia, możesz zignorować to wymaganie.</span><span class="sxs-lookup"><span data-stu-id="45138-139">If your query logic does not require hello same key toobe processed by hello same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="45138-140">Przykładem tego logiki może być prostego zapytania wybierz projekt filtru.</span><span class="sxs-lookup"><span data-stu-id="45138-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="45138-141">Po danych hello jest rozmieszczona na powitania strony wejściowej, to należy się upewnić, że zapytanie jest podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="45138-141">Once hello data is laid out on hello input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="45138-142">Wymaga to toouse **Partition By** wszystkie kroki hello w.</span><span class="sxs-lookup"><span data-stu-id="45138-142">This requires you toouse **Partition By** in all hello steps.</span></span> <span data-ttu-id="45138-143">Wiele kroków są dozwolone, ale wszystkie muszą partycjonowanego hello tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="45138-143">Multiple steps are allowed, but they all must be partitioned by hello same key.</span></span> <span data-ttu-id="45138-144">Obecnie hello klucz partycjonowania musi ustawić także**PartitionId** aby toobe zadania hello pełni równoległych.</span><span class="sxs-lookup"><span data-stu-id="45138-144">Currently, hello partitioning key must be set too**PartitionId** in order for hello job toobe fully parallel.</span></span>  

3. <span data-ttu-id="45138-145">Obecnie tylko centra zdarzeń i magazynu obiektów blob obsługują partycjonowanej danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="45138-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="45138-146">W przypadku danych wyjściowych Centrum zdarzeń, należy skonfigurować toobe klucza partycji hello **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="45138-146">For event hub output, you must configure hello partition key toobe **PartitionId**.</span></span> <span data-ttu-id="45138-147">Dla danych wyjściowych z magazynu obiektów blob nie masz toodo żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="45138-147">For blob storage output, you don't have toodo anything.</span></span>  

4. <span data-ttu-id="45138-148">Hello liczby partycji wejściowy musi być równa hello liczby partycji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="45138-148">hello number of input partitions must equal hello number of output partitions.</span></span> <span data-ttu-id="45138-149">Dane wyjściowe z magazynu obiektów blob nie obsługuje obecnie partycji.</span><span class="sxs-lookup"><span data-stu-id="45138-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="45138-150">Ale nie szkodzi, ponieważ dziedziczy on hello schemat nadrzędny zapytania hello partycji.</span><span class="sxs-lookup"><span data-stu-id="45138-150">But that's okay, because it inherits hello partitioning scheme of hello upstream query.</span></span> <span data-ttu-id="45138-151">Poniżej przedstawiono przykładowe wartości partycji, umożliwiających pełni równoległe zadania:</span><span class="sxs-lookup"><span data-stu-id="45138-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="45138-152">8 partycje wejściowych Centrum zdarzeń i Centrum zdarzeń 8 output partycji</span><span class="sxs-lookup"><span data-stu-id="45138-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="45138-153">8 partycje wejściowych Centrum zdarzeń i danych wyjściowych z magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="45138-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="45138-154">8 partycje wejściowych magazynu obiektów blob i dane wyjściowe z magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="45138-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="45138-155">8 obiektu blob magazynu wejściowego partycji i 8 partycje danych wyjściowych Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="45138-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="45138-156">Witaj poniższych sekcjach omówiono niektóre przykładowe scenariusze, które są embarrassingly równoległe.</span><span class="sxs-lookup"><span data-stu-id="45138-156">hello following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="45138-157">Prostego zapytania</span><span class="sxs-lookup"><span data-stu-id="45138-157">Simple query</span></span>

* <span data-ttu-id="45138-158">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="45138-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="45138-159">Dane wyjściowe: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="45138-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="45138-160">Zapytanie:</span><span class="sxs-lookup"><span data-stu-id="45138-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="45138-161">To zapytanie jest proste filtru.</span><span class="sxs-lookup"><span data-stu-id="45138-161">This query is a simple filter.</span></span> <span data-ttu-id="45138-162">W związku z tym nie należy tooworry o partycjonowaniu hello danych wejściowych, który jest wysyłany toohello Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="45138-162">Therefore, we don't need tooworry about partitioning hello input that is being sent toohello event hub.</span></span> <span data-ttu-id="45138-163">Zwróć uwagę, zawiera zapytania hello **partycji przez PartitionId**, więc jego spełnia wymagania #2 z wcześniej.</span><span class="sxs-lookup"><span data-stu-id="45138-163">Notice that hello query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="45138-164">Dla danych wyjściowych hello, potrzebujemy danych wyjściowych Centrum zdarzeń hello tooconfigure hello zadania toohave hello partycjonowania klucza zestawu, zbyt**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="45138-164">For hello output, we need tooconfigure hello event hub output in hello job toohave hello parition key set too**PartitionId**.</span></span> <span data-ttu-id="45138-165">Jeden ostatni test jest toomake się, że hello liczby partycji wejściowy jest równy toohello liczby partycji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="45138-165">One last check is toomake sure that hello number of input partitions is equal toohello number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="45138-166">Zapytanie z kluczem grupowania</span><span class="sxs-lookup"><span data-stu-id="45138-166">Query with a grouping key</span></span>

* <span data-ttu-id="45138-167">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="45138-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="45138-168">Danych wyjściowych: Magazyn obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="45138-168">Output: Blob storage</span></span>

<span data-ttu-id="45138-169">Zapytanie:</span><span class="sxs-lookup"><span data-stu-id="45138-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="45138-170">Ta kwerenda zawiera klucz grupowania.</span><span class="sxs-lookup"><span data-stu-id="45138-170">This query has a grouping key.</span></span> <span data-ttu-id="45138-171">Witaj w związku z tym samym toobe klucza potrzeb przetworzonych przez program hello takie same zapytanie wystąpienia, co oznacza, że zdarzenia musi być wysyłane toohello Centrum zdarzeń w sposób podzielonym na partycje.</span><span class="sxs-lookup"><span data-stu-id="45138-171">Therefore, hello same key needs toobe processed by hello same query instance, which means that events must be sent toohello event hub in a partitioned manner.</span></span> <span data-ttu-id="45138-172">Ale klucz, do którego należy używać?</span><span class="sxs-lookup"><span data-stu-id="45138-172">But which key should be used?</span></span> <span data-ttu-id="45138-173">**PartitionId** to pojęcie logiczne zadania.</span><span class="sxs-lookup"><span data-stu-id="45138-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="45138-174">klucz Hello faktycznie Szanujemy jest **TollBoothId**, więc hello **PartitionKey** musi mieć wartość dane zdarzeń hello **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="45138-174">hello key we actually care about is **TollBoothId**, so hello **PartitionKey** value of hello event data should be **TollBoothId**.</span></span> <span data-ttu-id="45138-175">Firma Microsoft to zrobić w zapytaniu hello przez ustawienie **Partition By** za**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="45138-175">We do this in hello query by setting **Partition By** too**PartitionId**.</span></span> <span data-ttu-id="45138-176">Ponieważ dane wyjściowe hello jest magazyn obiektów blob, nie musisz tooworry o konfigurowaniu wartość klucza partycji, zgodnie z harmonogramem wymaganie #4.</span><span class="sxs-lookup"><span data-stu-id="45138-176">Since hello output is blob storage, we don't need tooworry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="45138-177">Zapytanie wieloetapowych kluczem grupowania</span><span class="sxs-lookup"><span data-stu-id="45138-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="45138-178">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="45138-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="45138-179">Dane wyjściowe: Wystąpienie koncentratora zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="45138-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="45138-180">Zapytanie:</span><span class="sxs-lookup"><span data-stu-id="45138-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="45138-181">Ta kwerenda zawiera klucz grupowania, więc hello tego samego toobe klucza potrzeb przetworzonych przez program hello tego samego wystąpienia zapytania.</span><span class="sxs-lookup"><span data-stu-id="45138-181">This query has a grouping key, so hello same key needs toobe processed by hello same query instance.</span></span> <span data-ttu-id="45138-182">Możemy użyć tej samej strategii jak w poprzednim przykładzie hello hello.</span><span class="sxs-lookup"><span data-stu-id="45138-182">We can use hello same strategy as in hello previous example.</span></span> <span data-ttu-id="45138-183">W takim przypadku hello zapytania ma wiele kroków.</span><span class="sxs-lookup"><span data-stu-id="45138-183">In this case, hello query has multiple steps.</span></span> <span data-ttu-id="45138-184">Ma każdego kroku **partycji przez PartitionId**?</span><span class="sxs-lookup"><span data-stu-id="45138-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="45138-185">Tak więc zapytania hello spełnia wymagania #3.</span><span class="sxs-lookup"><span data-stu-id="45138-185">Yes, so hello query fulfills requirement #3.</span></span> <span data-ttu-id="45138-186">Dla danych wyjściowych hello, potrzebujemy klucza partycji hello tooset, zbyt**PartitionId**, zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="45138-186">For hello output, we need tooset hello partition key too**PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="45138-187">Można zobaczyć, czy ma ona hello tej samej liczby partycji jako dane wejściowe hello.</span><span class="sxs-lookup"><span data-stu-id="45138-187">We can also see that it has hello same number of partitions as hello input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="45138-188">Przykładowe scenariusze, które są *nie* embarrassingly równoległych</span><span class="sxs-lookup"><span data-stu-id="45138-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="45138-189">W poprzedniej sekcji hello możemy pokazano kilka scenariuszy embarrassingly równoległych.</span><span class="sxs-lookup"><span data-stu-id="45138-189">In hello previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="45138-190">W tej sekcji omówiono scenariusze, które nie spełniają wszystkie hello wymagania toobe embarrassingly równoległych.</span><span class="sxs-lookup"><span data-stu-id="45138-190">In this section, we discuss scenarios that don't meet all hello requirements toobe embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="45138-191">Liczba partycji niezgodne</span><span class="sxs-lookup"><span data-stu-id="45138-191">Mismatched partition count</span></span>
* <span data-ttu-id="45138-192">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="45138-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="45138-193">Dane wyjściowe: Centrum zdarzeń z partycjami 32</span><span class="sxs-lookup"><span data-stu-id="45138-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="45138-194">W takim przypadku nie ma znaczenia, jakie zapytanie hello jest.</span><span class="sxs-lookup"><span data-stu-id="45138-194">In this case, it doesn't matter what hello query is.</span></span> <span data-ttu-id="45138-195">Jeśli liczba partycji wejściowych hello nie odpowiada liczba partycji hello danych wyjściowych, topologii hello nie jest embarrassingly równoległych.</span><span class="sxs-lookup"><span data-stu-id="45138-195">If hello input partition count doesn't match hello output partition count, hello topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="45138-196">Nie używa usługi event hubs lub magazynu obiektów blob jako dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="45138-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="45138-197">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="45138-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="45138-198">Dane wyjściowe: usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="45138-198">Output: PowerBI</span></span>

<span data-ttu-id="45138-199">Wyjście usługi Power BI aktualnie nie obsługuje partycjonowanie.</span><span class="sxs-lookup"><span data-stu-id="45138-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="45138-200">Dlatego w tym scenariuszu nie jest embarrassingly równoległych.</span><span class="sxs-lookup"><span data-stu-id="45138-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="45138-201">Zapytanie wieloetapowych o różnych wartościach Partition By</span><span class="sxs-lookup"><span data-stu-id="45138-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="45138-202">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="45138-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="45138-203">Dane wyjściowe: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="45138-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="45138-204">Zapytanie:</span><span class="sxs-lookup"><span data-stu-id="45138-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="45138-205">Jak widać, drugi etap hello używa **TollBoothId** jako hello klucz partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="45138-205">As you can see, hello second step uses **TollBoothId** as hello partitioning key.</span></span> <span data-ttu-id="45138-206">Ten krok jest hello sam nie jako pierwsze hello i dlatego wymaga nam toodo losowa.</span><span class="sxs-lookup"><span data-stu-id="45138-206">This step is not hello same as hello first step, and it therefore requires us toodo a shuffle.</span></span> 

<span data-ttu-id="45138-207">Witaj poprzednich przykładach niektóre zadania usługi analiza strumienia, które są zbyt (lub nie) embarrassingly równoległych topologii.</span><span class="sxs-lookup"><span data-stu-id="45138-207">hello preceding examples show some Stream Analytics jobs that conform too(or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="45138-208">Jeśli są one zgodne, mają możliwość hello maksymalną skalę.</span><span class="sxs-lookup"><span data-stu-id="45138-208">If they do conform, they have hello potential for maximum scale.</span></span> <span data-ttu-id="45138-209">Aktualizacje dla zadania, które nie pasują do jednego z tych profilów skalowania wskazówki będą dostępne w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="45138-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="45138-210">Na razie użyj hello ogólne wskazówki w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="45138-210">For now, use hello general guidance in hello following sections.</span></span>

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a><span data-ttu-id="45138-211">Oblicz maksymalną liczbę jednostek przesyłania strumieniowego hello zadania</span><span class="sxs-lookup"><span data-stu-id="45138-211">Calculate hello maximum streaming units of a job</span></span>
<span data-ttu-id="45138-212">Hello całkowita liczba jednostek przesyłania strumieniowego, które mogą być używane przez zadanie usługi Stream Analytics zależy od hello liczbę kroków w zapytaniu hello zdefiniowane dla zadania hello i hello liczby partycji dla każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="45138-212">hello total number of streaming units that can be used by a Stream Analytics job depends on hello number of steps in hello query defined for hello job and hello number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="45138-213">Kroki w kwerendzie</span><span class="sxs-lookup"><span data-stu-id="45138-213">Steps in a query</span></span>
<span data-ttu-id="45138-214">Kwerenda może mieć jeden lub wiele kroków.</span><span class="sxs-lookup"><span data-stu-id="45138-214">A query can have one or many steps.</span></span> <span data-ttu-id="45138-215">Każdy krok jest zdefiniowane przez hello podzapytania **WITH** — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="45138-215">Each step is a subquery defined by hello **WITH** keyword.</span></span> <span data-ttu-id="45138-216">Hello kwerendę, która znajduje się poza hello **WITH** — słowo kluczowe (tylko w jednej kwerendzie) również jest traktowane jako krok, takich jak hello **wybierz** instrukcji w hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="45138-216">hello query that is outside hello **WITH** keyword (one query only) is also counted as a step, such as hello **SELECT** statement in hello following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="45138-217">Ta kwerenda zawiera dwa kroki.</span><span class="sxs-lookup"><span data-stu-id="45138-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="45138-218">To zapytanie jest omówiona bardziej szczegółowo w dalszej części artykułu hello.</span><span class="sxs-lookup"><span data-stu-id="45138-218">This query is discussed in more detail later in hello article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="45138-219">Krok partycji</span><span class="sxs-lookup"><span data-stu-id="45138-219">Partition a step</span></span>
<span data-ttu-id="45138-220">Partycjonowanie krok wymaga hello następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="45138-220">Partitioning a step requires hello following conditions:</span></span>

* <span data-ttu-id="45138-221">musi być dzielony na partycje Hello źródło danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="45138-221">hello input source must be partitioned.</span></span> 
* <span data-ttu-id="45138-222">Witaj **wybierz** instrukcji kwerendy hello musi odczytywać partycjonowanej źródło danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="45138-222">hello **SELECT** statement of hello query must read from a partitioned input source.</span></span>
* <span data-ttu-id="45138-223">Zapytanie Hello w ramach kroku hello musi mieć hello **Partition By** — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="45138-223">hello query within hello step must have hello **Partition By** keyword.</span></span>

<span data-ttu-id="45138-224">Gdy zapytanie jest podzielona na partycje, zdarzenia wejściowe hello są przetwarzane i zagregowane w oddzielnej partycji grupy, a dane wyjściowe zdarzenia są generowane dla poszczególnych grup hello.</span><span class="sxs-lookup"><span data-stu-id="45138-224">When a query is partitioned, hello input events are processed and aggregated in separate partition groups, and outputs events are generated for each of hello groups.</span></span> <span data-ttu-id="45138-225">Jeśli chcesz połączonych Agregacja należy utworzyć drugi tooaggregate niepartycjonowany kroku.</span><span class="sxs-lookup"><span data-stu-id="45138-225">If you want a combined aggregate, you must create a second non-partitioned step tooaggregate.</span></span>

### <a name="calculate-hello-max-streaming-units-for-a-job"></a><span data-ttu-id="45138-226">Oblicz max hello jednostki zadania przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="45138-226">Calculate hello max streaming units for a job</span></span>
<span data-ttu-id="45138-227">Wszystkie kroki niepartycjonowany razem można skalować toosix jednostki (SUs) dla zadania usługi analiza strumienia przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="45138-227">All non-partitioned steps together can scale up toosix streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="45138-228">musi być dzielony na partycje SUs tooadd, krok.</span><span class="sxs-lookup"><span data-stu-id="45138-228">tooadd SUs, a step must be partitioned.</span></span> <span data-ttu-id="45138-229">Każda partycja może mieć sześć SUs.</span><span class="sxs-lookup"><span data-stu-id="45138-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="45138-230">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="45138-230">Query</span></span></th><th><span data-ttu-id="45138-231">Maksymalna liczba SUs hello zadania</span><span class="sxs-lookup"><span data-stu-id="45138-231">Max SUs for hello job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="45138-232">Zapytanie Hello zawiera jeden krok.</span><span class="sxs-lookup"><span data-stu-id="45138-232">hello query contains one step.</span></span></li>
<li><span data-ttu-id="45138-233">Witaj krok nie jest podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="45138-233">hello step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="45138-234">6</span><span class="sxs-lookup"><span data-stu-id="45138-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="45138-235">strumień danych wejściowych Hello jest podzielona na partycje przez 3.</span><span class="sxs-lookup"><span data-stu-id="45138-235">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="45138-236">Zapytanie Hello zawiera jeden krok.</span><span class="sxs-lookup"><span data-stu-id="45138-236">hello query contains one step.</span></span></li>
<li><span data-ttu-id="45138-237">krok Hello jest podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="45138-237">hello step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="45138-238">18</span><span class="sxs-lookup"><span data-stu-id="45138-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="45138-239">Zapytanie Hello zawiera dwa kroki.</span><span class="sxs-lookup"><span data-stu-id="45138-239">hello query contains two steps.</span></span></li>
<li><span data-ttu-id="45138-240">Żadne czynności hello jest podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="45138-240">Neither of hello steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="45138-241">6</span><span class="sxs-lookup"><span data-stu-id="45138-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="45138-242">strumień danych wejściowych Hello jest podzielona na partycje przez 3.</span><span class="sxs-lookup"><span data-stu-id="45138-242">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="45138-243">Zapytanie Hello zawiera dwa kroki.</span><span class="sxs-lookup"><span data-stu-id="45138-243">hello query contains two steps.</span></span> <span data-ttu-id="45138-244">wejściowych kroku Hello jest podzielona na partycje, a drugi etap hello nie.</span><span class="sxs-lookup"><span data-stu-id="45138-244">hello input step is partitioned and hello second step is not.</span></span></li>
<li><span data-ttu-id="45138-245">Witaj <strong>wybierz</strong> instrukcji odczytuje z danych wejściowych hello podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="45138-245">hello <strong>SELECT</strong> statement reads from hello partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="45138-246">24 (18 partycjonowanej kroki) + 6 niepartycjonowany czynności</span><span class="sxs-lookup"><span data-stu-id="45138-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="45138-247">Przykłady skalowania</span><span class="sxs-lookup"><span data-stu-id="45138-247">Examples of scaling</span></span>

<span data-ttu-id="45138-248">Witaj następujące zapytanie oblicza hello liczba samochodów w ramach pośrednictwa stacji przez, który ma trzy tollbooths okna trzy minuty.</span><span class="sxs-lookup"><span data-stu-id="45138-248">hello following query calculates hello number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="45138-249">To zapytanie może być skalowana w górę toosix SUs.</span><span class="sxs-lookup"><span data-stu-id="45138-249">This query can be scaled up toosix SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="45138-250">toouse więcej SUs dla hello zapytania, zarówno hello strumienia danych wejściowych i musi być dzielony na partycje hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="45138-250">toouse more SUs for hello query, both hello input data stream and hello query must be partitioned.</span></span> <span data-ttu-id="45138-251">Ponieważ partycja strumienia danych hello jest ustawiona too3, hello następujące zmodyfikowanej zapytanie umożliwia skalowanie too18 SUs:</span><span class="sxs-lookup"><span data-stu-id="45138-251">Since hello data stream partition is set too3, hello following modified query can be scaled up too18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="45138-252">Zapytanie jest podzielona na partycje, zdarzenia wejściowe hello są przetwarzane i zagregowane w oddzielnej partycji grup.</span><span class="sxs-lookup"><span data-stu-id="45138-252">When a query is partitioned, hello input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="45138-253">Dane wyjściowe zdarzenia są także generowane dla poszczególnych grup hello.</span><span class="sxs-lookup"><span data-stu-id="45138-253">Output events are also generated for each of hello groups.</span></span> <span data-ttu-id="45138-254">Partycjonowanie może powodować pewne nieoczekiwane wyniki hello **GROUP BY** pole nie jest kluczem partycji hello w strumieniu danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="45138-254">Partitioning can cause some unexpected results when hello **GROUP BY** field is not hello partition key in hello input data stream.</span></span> <span data-ttu-id="45138-255">Na przykład Witaj **TollBoothId** pole w hello poprzednie zapytanie nie jest klucz partycji hello **Input1**.</span><span class="sxs-lookup"><span data-stu-id="45138-255">For example, hello **TollBoothId** field in hello previous query is not hello partition key of **Input1**.</span></span> <span data-ttu-id="45138-256">wynik Hello jest hello, że dane z budki #1 mogą rozprzestrzeniać się, w wielu partycji.</span><span class="sxs-lookup"><span data-stu-id="45138-256">hello result is that hello data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="45138-257">Każdy z hello **Input1** partycje będą przetwarzane oddzielnie przez Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="45138-257">Each of hello **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="45138-258">W związku z tym wiele rekordów liczby hello samochodu hello tego samego budki w powitalne okno wirowania tego samego zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="45138-258">As a result, multiple records of hello car count for hello same tollbooth in hello same Tumbling window will be created.</span></span> <span data-ttu-id="45138-259">Jeśli nie można zmienić klucza partycji wejściowych hello, można naprawić ten problem, dodając krok-partition, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="45138-259">If hello input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in hello following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="45138-260">To zapytanie może być skalowana too24 SUs.</span><span class="sxs-lookup"><span data-stu-id="45138-260">This query can be scaled too24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="45138-261">Jeśli są Sprzęganie dwóch strumieni, upewnij się, że strumienie hello są podzielone na partycje według klucza partycji hello kolumny hello użycie toocreate hello sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="45138-261">If you are joining two streams, make sure that hello streams are partitioned by hello partition key of hello column that you use toocreate hello joins.</span></span> <span data-ttu-id="45138-262">Upewnij się, że masz hello również tej samej liczby partycji w obu strumieni.</span><span class="sxs-lookup"><span data-stu-id="45138-262">Also make sure that you have hello same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="45138-263">Konfigurowanie usługi Stream Analytics jednostki przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="45138-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="45138-264">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="45138-264">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="45138-265">Hello listy zasobów Znajdź zadanie usługi Stream Analytics hello mają tooscale, a następnie otwórz go.</span><span class="sxs-lookup"><span data-stu-id="45138-265">In hello list of resources, find hello Stream Analytics job that you want tooscale and then open it.</span></span>
3. <span data-ttu-id="45138-266">W hello zadania bloku, w obszarze **Konfiguruj**, kliknij przycisk **skali**.</span><span class="sxs-lookup"><span data-stu-id="45138-266">In hello job blade, under **Configure**, click **Scale**.</span></span>

    ![Konfiguracja zadania usługi analiza strumienia portalu Azure][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="45138-268">Użyj hello suwaka tooset hello SUs hello zadania.</span><span class="sxs-lookup"><span data-stu-id="45138-268">Use hello slider tooset hello SUs for hello job.</span></span> <span data-ttu-id="45138-269">Zwróć uwagę, czy ustawienia SU toospecific ograniczone.</span><span class="sxs-lookup"><span data-stu-id="45138-269">Notice that you are limited toospecific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="45138-270">Monitor wydajności zadania</span><span class="sxs-lookup"><span data-stu-id="45138-270">Monitor job performance</span></span>
<span data-ttu-id="45138-271">Witaj portalu Azure można śledzić przepływności hello zadania:</span><span class="sxs-lookup"><span data-stu-id="45138-271">Using hello Azure portal, you can track hello throughput of a job:</span></span>

![Azure Stream Analytics monitorowanie zadań][img.stream.analytics.monitor.job]

<span data-ttu-id="45138-273">Oblicz przepływności hello oczekiwano hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="45138-273">Calculate hello expected throughput of hello workload.</span></span> <span data-ttu-id="45138-274">Przepływności hello jest mniejsza niż oczekiwano, dostroić hello wejściowych partycji, dostroić hello zapytania i dodać SUs tooyour zadania.</span><span class="sxs-lookup"><span data-stu-id="45138-274">If hello throughput is less than expected, tune hello input partition, tune hello query, and add SUs tooyour job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a><span data-ttu-id="45138-275">Wizualizuj Stream Analytics przepustowość na dużą skalę: hello Pi malina scenariusza</span><span class="sxs-lookup"><span data-stu-id="45138-275">Visualize Stream Analytics throughput at scale: hello Raspberry Pi scenario</span></span>
<span data-ttu-id="45138-276">toohelp zrozumieć, jak skalować zadania usługi analiza strumienia, wykonane eksperyment na podstawie danych wprowadzonych z urządzenia malina Pi.</span><span class="sxs-lookup"><span data-stu-id="45138-276">toohelp you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="45138-277">Tego eksperymentu poinformować nas, zobacz hello wpływu na przepustowość wiele jednostek przesyłania strumieniowego i partycje.</span><span class="sxs-lookup"><span data-stu-id="45138-277">This experiment let us see hello effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="45138-278">W tym scenariuszu urządzenie hello wysyła czujnik danych (klienci) tooan zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="45138-278">In this scenario, hello device sends sensor data (clients) tooan event hub.</span></span> <span data-ttu-id="45138-279">Przesyłanie strumieniowe Analytics przetwarza dane hello i wysyła alert ani w statystyce jako Centrum zdarzeń tooanother danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="45138-279">Streaming Analytics processes hello data and sends an alert or statistics as an output tooanother event hub.</span></span> 

<span data-ttu-id="45138-280">powitania klienta wysyła dane czujników w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="45138-280">hello client sends sensor data in JSON format.</span></span> <span data-ttu-id="45138-281">Witaj danych wyjściowych jest również w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="45138-281">hello data output is also in JSON format.</span></span> <span data-ttu-id="45138-282">dane Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="45138-282">hello data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="45138-283">Hello następującego zapytania jest używana toosend alert po wyłączeniu światło:</span><span class="sxs-lookup"><span data-stu-id="45138-283">hello following query is used toosend an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="45138-284">Miara przepływności</span><span class="sxs-lookup"><span data-stu-id="45138-284">Measure throughput</span></span>

<span data-ttu-id="45138-285">W tym kontekście przepływność wynosi hello ilość danych wejściowych przetworzone przez usługę Stream Analytics w stałej ilości czasu.</span><span class="sxs-lookup"><span data-stu-id="45138-285">In this context, throughput is hello amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="45138-286">(Firma Microsoft mierzy przez 10 minut.) dane wejściowe tooachieve hello najlepsze przetwarzania przepływności hello, zarówno dane hello strumienia danych wejściowych i zapytania hello zostały podzielone na partycje.</span><span class="sxs-lookup"><span data-stu-id="45138-286">(We measured for 10 minutes.) tooachieve hello best processing throughput for hello input data, both hello data stream input and hello query were  partitioned.</span></span> <span data-ttu-id="45138-287">Jest dostępna **COUNT()** w toomeasure zapytania hello przetworzono ile zdarzenia wejściowe.</span><span class="sxs-lookup"><span data-stu-id="45138-287">We included **COUNT()** in hello query toomeasure how many input events were processed.</span></span> <span data-ttu-id="45138-288">czy zadania hello toomake nie oczekiwał po prostu dla zdarzenia wejściowe toocome, każdej partycji Centrum zdarzeń wejściowych hello są załadowane z około 300 MB danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="45138-288">toomake sure hello job was not simply waiting for input events toocome, each partition of hello input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="45138-289">Witaj poniższej tabeli przedstawiono wyniki hello, którą widzieliśmy, gdy firma Microsoft zwiększyć hello liczbę jednostek przesyłania strumieniowego i odpowiadająca mu partycja hello liczby w usługi event hubs.</span><span class="sxs-lookup"><span data-stu-id="45138-289">hello following table shows hello results we saw when we increased hello number of streaming units and hello corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="45138-290">Partycje wejściowych</span><span class="sxs-lookup"><span data-stu-id="45138-290">Input Partitions</span></span></th><th><span data-ttu-id="45138-291">Partycje danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="45138-291">Output Partitions</span></span></th><th><span data-ttu-id="45138-292">Jednostki przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="45138-292">Streaming Units</span></span></th><th><span data-ttu-id="45138-293">Długoterminowa przepustowość</span><span class="sxs-lookup"><span data-stu-id="45138-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="45138-294">12</span><span class="sxs-lookup"><span data-stu-id="45138-294">12</span></span></td>
<td><span data-ttu-id="45138-295">12</span><span class="sxs-lookup"><span data-stu-id="45138-295">12</span></span></td>
<td><span data-ttu-id="45138-296">6</span><span class="sxs-lookup"><span data-stu-id="45138-296">6</span></span></td>
<td><span data-ttu-id="45138-297">4.06 MB/s</span><span class="sxs-lookup"><span data-stu-id="45138-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="45138-298">12</span><span class="sxs-lookup"><span data-stu-id="45138-298">12</span></span></td>
<td><span data-ttu-id="45138-299">12</span><span class="sxs-lookup"><span data-stu-id="45138-299">12</span></span></td>
<td><span data-ttu-id="45138-300">12</span><span class="sxs-lookup"><span data-stu-id="45138-300">12</span></span></td>
<td><span data-ttu-id="45138-301">8.06 MB/s</span><span class="sxs-lookup"><span data-stu-id="45138-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="45138-302">48</span><span class="sxs-lookup"><span data-stu-id="45138-302">48</span></span></td>
<td><span data-ttu-id="45138-303">48</span><span class="sxs-lookup"><span data-stu-id="45138-303">48</span></span></td>
<td><span data-ttu-id="45138-304">48</span><span class="sxs-lookup"><span data-stu-id="45138-304">48</span></span></td>
<td><span data-ttu-id="45138-305">38.32 MB/s</span><span class="sxs-lookup"><span data-stu-id="45138-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="45138-306">192</span><span class="sxs-lookup"><span data-stu-id="45138-306">192</span></span></td>
<td><span data-ttu-id="45138-307">192</span><span class="sxs-lookup"><span data-stu-id="45138-307">192</span></span></td>
<td><span data-ttu-id="45138-308">192</span><span class="sxs-lookup"><span data-stu-id="45138-308">192</span></span></td>
<td><span data-ttu-id="45138-309">172.67 MB/s</span><span class="sxs-lookup"><span data-stu-id="45138-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="45138-310">480</span><span class="sxs-lookup"><span data-stu-id="45138-310">480</span></span></td>
<td><span data-ttu-id="45138-311">480</span><span class="sxs-lookup"><span data-stu-id="45138-311">480</span></span></td>
<td><span data-ttu-id="45138-312">480</span><span class="sxs-lookup"><span data-stu-id="45138-312">480</span></span></td>
<td><span data-ttu-id="45138-313">454.27 MB/s</span><span class="sxs-lookup"><span data-stu-id="45138-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="45138-314">720</span><span class="sxs-lookup"><span data-stu-id="45138-314">720</span></span></td>
<td><span data-ttu-id="45138-315">720</span><span class="sxs-lookup"><span data-stu-id="45138-315">720</span></span></td>
<td><span data-ttu-id="45138-316">720</span><span class="sxs-lookup"><span data-stu-id="45138-316">720</span></span></td>
<td><span data-ttu-id="45138-317">609.69 MB/s</span><span class="sxs-lookup"><span data-stu-id="45138-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="45138-318">I hello Wykres ukazuje wizualizacji hello relacji między usługami SUs i przepływności.</span><span class="sxs-lookup"><span data-stu-id="45138-318">And hello following graph shows a visualization of hello relationship between SUs and throughput.</span></span>

![img.stream.Analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="45138-320">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="45138-320">Get help</span></span>
<span data-ttu-id="45138-321">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="45138-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="45138-322">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="45138-322">Next steps</span></span>
* [<span data-ttu-id="45138-323">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="45138-323">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="45138-324">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="45138-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="45138-325">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="45138-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="45138-326">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="45138-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

