---
title: "Skalowanie zadania usługi analiza strumienia w celu zwiększenia przepływności | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skalować zadania usługi analiza strumienia Konfigurowanie partycji wejściowych, dostosowywanie definicji zapytania i ustawiając zadania jednostki przesyłania strumieniowego."
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
ms.openlocfilehash: ab894976c72ea3785d7f58e51b3dd64511e1e8e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="scale-azure-stream-analytics-jobs-to-increase-stream-data-processing-throughput"></a><span data-ttu-id="19a22-104">Skalowanie zadania usługi analiza strumienia Azure w celu zwiększenia przepływności przetwarzania danych strumienia</span><span class="sxs-lookup"><span data-stu-id="19a22-104">Scale Azure Stream Analytics jobs to increase stream data processing throughput</span></span>
<span data-ttu-id="19a22-105">W tym artykule przedstawiono sposób dostrajania Stream Analytics zapytanie w celu zwiększenia przepływności zadań przesyłania strumieniowego usługi Analytics.</span><span class="sxs-lookup"><span data-stu-id="19a22-105">This article shows you how to tune a Stream Analytics query to increase throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="19a22-106">Dowiesz się, jak skalowanie zadania usługi analiza strumienia przez konfigurowanie partycji wejściowych, dostosowywanie definicji zapytania analytics i obliczanie i ustawiania zadania *jednostki przesyłania strumieniowego* (SUs).</span><span class="sxs-lookup"><span data-stu-id="19a22-106">You learn how to scale Stream Analytics jobs by configuring input partitions, tuning the analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-the-parts-of-a-stream-analytics-job"></a><span data-ttu-id="19a22-107">Co to są elementy zadania Stream Analytics?</span><span class="sxs-lookup"><span data-stu-id="19a22-107">What are the parts of a Stream Analytics job?</span></span>
<span data-ttu-id="19a22-108">Definicji zadania Stream Analytics zawiera dane wejściowe, zapytań i danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="19a22-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="19a22-109">Dane wejściowe są, gdy zadanie odczytuje strumienia danych z.</span><span class="sxs-lookup"><span data-stu-id="19a22-109">Inputs are where the job reads the data stream from.</span></span> <span data-ttu-id="19a22-110">Zapytanie jest używany do transformacji strumienia danych wejściowych, a dane wyjściowe są, gdy zadanie wysyła wyników zadania do.</span><span class="sxs-lookup"><span data-stu-id="19a22-110">The query is used to transform the data input stream, and the output is where the job sends the job results to.</span></span>  

<span data-ttu-id="19a22-111">Zadanie wymaga co najmniej jedno źródło danych wejściowych do strumieniowego przesyłania danych.</span><span class="sxs-lookup"><span data-stu-id="19a22-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="19a22-112">Źródło dla wejścia strumienia danych mogą być przechowywane w Centrum zdarzeń platformy Azure lub w magazynie obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="19a22-112">The data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="19a22-113">Aby uzyskać więcej informacji, zobacz [wprowadzenie do usługi Azure Stream Analytics](stream-analytics-introduction.md) i [rozpocząć korzystanie z usługi Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="19a22-113">For more information, see [Introduction to Azure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="19a22-114">Partycje w centra zdarzeń i magazynu systemu Azure</span><span class="sxs-lookup"><span data-stu-id="19a22-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="19a22-115">Skalowanie zadania Stream Analytics korzysta z partycjami w danych wejściowych lub wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="19a22-115">Scaling a Stream Analytics job takes advantage of partitions in the input or output.</span></span> <span data-ttu-id="19a22-116">Partycjonowanie umożliwia dzielenia danych na podzestawy oparte na kluczu partycji.</span><span class="sxs-lookup"><span data-stu-id="19a22-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="19a22-117">Proces, który używa danych (na przykład zadanie analizy przesyłania strumieniowego) może wykorzystywać i zapisać różnych partycji równolegle, co zwiększa przepustowość.</span><span class="sxs-lookup"><span data-stu-id="19a22-117">A process that consumes the data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="19a22-118">Podczas pracy z analizy przesyłania strumieniowego, możesz korzystać z partycjonowania usługi event hubs i w magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="19a22-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="19a22-119">Aby uzyskać więcej informacji o partycjach zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="19a22-119">For more information about partitions, see the following articles:</span></span>

* [<span data-ttu-id="19a22-120">Omówienie funkcji usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="19a22-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="19a22-121">Partycjonowanie danych</span><span class="sxs-lookup"><span data-stu-id="19a22-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="19a22-122">Jednostki przesyłania strumieniowego (SUs)</span><span class="sxs-lookup"><span data-stu-id="19a22-122">Streaming units (SUs)</span></span>
<span data-ttu-id="19a22-123">Jednostki przesyłania strumieniowego (SUs) reprezentuje zasobów i mocy obliczeniowej, które są wymagane w celu wykonania zadanie usługi analiza strumienia Azure.</span><span class="sxs-lookup"><span data-stu-id="19a22-123">Streaming units (SUs) represent the resources and computing power that are required in order to execute an Azure Stream Analytics job.</span></span> <span data-ttu-id="19a22-124">Jednostki przesyłania strumieniowego to sposób opisywania względnych możliwości obliczeniowych dotyczących przetwarzania na podstawie mieszanego pomiaru wydajności procesora CPU, pamięci i operacji odczytu oraz zapisu.</span><span class="sxs-lookup"><span data-stu-id="19a22-124">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="19a22-125">Każdy SU odpowiada około 1 MB/s przepustowości.</span><span class="sxs-lookup"><span data-stu-id="19a22-125">Each SU corresponds to roughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="19a22-126">Wybranie liczby SUs są wymagane dla określonego zadania zależy od konfiguracji partycji dla danych wejściowych oraz zapytania zdefiniowanych dla tego zadania.</span><span class="sxs-lookup"><span data-stu-id="19a22-126">Choosing how many SUs are required for a particular job depends on the partition configuration for the inputs and on the query defined for the job.</span></span> <span data-ttu-id="19a22-127">Można wybrać do limitu przydziału w SUs dla zadania.</span><span class="sxs-lookup"><span data-stu-id="19a22-127">You can select up to your quota in SUs for a job.</span></span> <span data-ttu-id="19a22-128">Domyślnie każdej subskrypcji platformy Azure ma limit przydziału wynoszący maksymalnie 50 SUs dla wszystkich zadań analityka w określonym regionie.</span><span class="sxs-lookup"><span data-stu-id="19a22-128">By default, each Azure subscription has a quota of up to 50 SUs for all the analytics jobs in a specific region.</span></span> <span data-ttu-id="19a22-129">Aby zwiększyć SUs dla Twojej subskrypcji po przekroczeniu tego przydziału, skontaktuj się z [Microsoft Support](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="19a22-129">To increase SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="19a22-130">Prawidłowe wartości SUs na zadanie to 1, 3, 6 oraz w przyrostach 6.</span><span class="sxs-lookup"><span data-stu-id="19a22-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="19a22-131">Embarrassingly równoległych zadań</span><span class="sxs-lookup"><span data-stu-id="19a22-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="19a22-132">*Embarrassingly równoległych* zadanie jest najbardziej skalowalny scenariusza mamy w Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="19a22-132">An *embarrassingly parallel* job is the most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="19a22-133">Jedna partycja danych wejściowych do jednego wystąpienia zapytania łączy się jedną partycję w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="19a22-133">It connects one partition of the input to one instance of the query to one partition of the output.</span></span> <span data-ttu-id="19a22-134">Równoległość ten ma następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="19a22-134">This parallelism has the following requirements:</span></span>

1. <span data-ttu-id="19a22-135">Logika zapytania zależy od tego samego klucza przetwarzanych przez to samo wystąpienie zapytania, należy się upewnić, że zdarzenia przejdź do tej samej partycji dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="19a22-135">If your query logic depends on the same key being processed by the same query instance, you must make sure that the events go to the same partition of your input.</span></span> <span data-ttu-id="19a22-136">Usługi event hubs, oznacza to, że dane zdarzeń muszą mieć **PartitionKey** zestawu wartości.</span><span class="sxs-lookup"><span data-stu-id="19a22-136">For event hubs, this means that the event data must have the **PartitionKey** value set.</span></span> <span data-ttu-id="19a22-137">Alternatywnie można użyć nadawców podzielonym na partycje.</span><span class="sxs-lookup"><span data-stu-id="19a22-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="19a22-138">W przypadku magazynu obiektów blob oznacza to, że zdarzenia są wysyłane do tego samego folderu partycji.</span><span class="sxs-lookup"><span data-stu-id="19a22-138">For blob storage, this means that the events are sent to the same partition folder.</span></span> <span data-ttu-id="19a22-139">Jeśli logika zapytania nie wymaga tego samego klucza do przetworzenia przez to samo wystąpienie zapytania, możesz zignorować to wymaganie.</span><span class="sxs-lookup"><span data-stu-id="19a22-139">If your query logic does not require the same key to be processed by the same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="19a22-140">Przykładem tego logiki może być prostego zapytania wybierz projekt filtru.</span><span class="sxs-lookup"><span data-stu-id="19a22-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="19a22-141">Po danych jest rozmieszczona na stronie wprowadzania, to należy się upewnić, że zapytanie jest podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="19a22-141">Once the data is laid out on the input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="19a22-142">Wymaga to użycia **Partition By** wszystkich kroków.</span><span class="sxs-lookup"><span data-stu-id="19a22-142">This requires you to use **Partition By** in all the steps.</span></span> <span data-ttu-id="19a22-143">Wiele kroków są dozwolone, ale wszystkie muszą podzielone na partycje przy użyciu tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="19a22-143">Multiple steps are allowed, but they all must be partitioned by the same key.</span></span> <span data-ttu-id="19a22-144">Obecnie, podziału klucza musi być ustawiona na **PartitionId** aby pełni równoległe zadania.</span><span class="sxs-lookup"><span data-stu-id="19a22-144">Currently, the partitioning key must be set to **PartitionId** in order for the job to be fully parallel.</span></span>  

3. <span data-ttu-id="19a22-145">Obecnie tylko centra zdarzeń i magazynu obiektów blob obsługują partycjonowanej danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="19a22-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="19a22-146">W przypadku danych wyjściowych Centrum zdarzeń, należy skonfigurować klucz partycji, który ma być **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="19a22-146">For event hub output, you must configure the partition key to be **PartitionId**.</span></span> <span data-ttu-id="19a22-147">Dla danych wyjściowych z magazynu obiektów blob nie trzeba wykonywać żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="19a22-147">For blob storage output, you don't have to do anything.</span></span>  

4. <span data-ttu-id="19a22-148">Liczby partycji wejściowych musi być równa liczbie partycji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="19a22-148">The number of input partitions must equal the number of output partitions.</span></span> <span data-ttu-id="19a22-149">Dane wyjściowe z magazynu obiektów blob nie obsługuje obecnie partycji.</span><span class="sxs-lookup"><span data-stu-id="19a22-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="19a22-150">Ale nie szkodzi, ponieważ dziedziczy ona schemat partycjonowania nadrzędnego zapytania.</span><span class="sxs-lookup"><span data-stu-id="19a22-150">But that's okay, because it inherits the partitioning scheme of the upstream query.</span></span> <span data-ttu-id="19a22-151">Poniżej przedstawiono przykładowe wartości partycji, umożliwiających pełni równoległe zadania:</span><span class="sxs-lookup"><span data-stu-id="19a22-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="19a22-152">8 partycje wejściowych Centrum zdarzeń i Centrum zdarzeń 8 output partycji</span><span class="sxs-lookup"><span data-stu-id="19a22-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="19a22-153">8 partycje wejściowych Centrum zdarzeń i danych wyjściowych z magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="19a22-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="19a22-154">8 partycje wejściowych magazynu obiektów blob i dane wyjściowe z magazynu obiektów blob</span><span class="sxs-lookup"><span data-stu-id="19a22-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="19a22-155">8 obiektu blob magazynu wejściowego partycji i 8 partycje danych wyjściowych Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="19a22-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="19a22-156">W poniższych sekcjach omówiono niektóre przykładowe scenariusze, które są embarrassingly równoległe.</span><span class="sxs-lookup"><span data-stu-id="19a22-156">The following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="19a22-157">Prostego zapytania</span><span class="sxs-lookup"><span data-stu-id="19a22-157">Simple query</span></span>

* <span data-ttu-id="19a22-158">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="19a22-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="19a22-159">Dane wyjściowe: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="19a22-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="19a22-160">Zapytanie:</span><span class="sxs-lookup"><span data-stu-id="19a22-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="19a22-161">To zapytanie jest proste filtru.</span><span class="sxs-lookup"><span data-stu-id="19a22-161">This query is a simple filter.</span></span> <span data-ttu-id="19a22-162">W związku z tym firma Microsoft nie trzeba martwić partycjonowanie danych wejściowych, który jest wysyłany do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="19a22-162">Therefore, we don't need to worry about partitioning the input that is being sent to the event hub.</span></span> <span data-ttu-id="19a22-163">Należy zauważyć, że kwerenda zawiera **partycji przez PartitionId**, więc jego spełnia wymagania #2 z wcześniej.</span><span class="sxs-lookup"><span data-stu-id="19a22-163">Notice that the query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="19a22-164">Dla danych wyjściowych, należy skonfigurować zadania zawiera zestaw klucza partycjonowania do danych wyjściowych Centrum zdarzeń **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="19a22-164">For the output, we need to configure the event hub output in the job to have the parition key set to **PartitionId**.</span></span> <span data-ttu-id="19a22-165">Jeden ostatni test jest upewnij się, że liczba partycji wejściowy jest równa liczbie partycji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="19a22-165">One last check is to make sure that the number of input partitions is equal to the number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="19a22-166">Zapytanie z kluczem grupowania</span><span class="sxs-lookup"><span data-stu-id="19a22-166">Query with a grouping key</span></span>

* <span data-ttu-id="19a22-167">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="19a22-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="19a22-168">Danych wyjściowych: Magazyn obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="19a22-168">Output: Blob storage</span></span>

<span data-ttu-id="19a22-169">Zapytanie:</span><span class="sxs-lookup"><span data-stu-id="19a22-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="19a22-170">Ta kwerenda zawiera klucz grupowania.</span><span class="sxs-lookup"><span data-stu-id="19a22-170">This query has a grouping key.</span></span> <span data-ttu-id="19a22-171">W związku z tym samym kluczem musi być przetwarzane przez to samo wystąpienie kwerendy, co oznacza, że zdarzenia musi być wysyłane do Centrum zdarzeń w sposób podzielonym na partycje.</span><span class="sxs-lookup"><span data-stu-id="19a22-171">Therefore, the same key needs to be processed by the same query instance, which means that events must be sent to the event hub in a partitioned manner.</span></span> <span data-ttu-id="19a22-172">Ale klucz, do którego należy używać?</span><span class="sxs-lookup"><span data-stu-id="19a22-172">But which key should be used?</span></span> <span data-ttu-id="19a22-173">**PartitionId** to pojęcie logiczne zadania.</span><span class="sxs-lookup"><span data-stu-id="19a22-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="19a22-174">Klucz faktycznie Szanujemy jest **TollBoothId**, więc **PartitionKey** musi mieć wartość dane zdarzenia **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="19a22-174">The key we actually care about is **TollBoothId**, so the **PartitionKey** value of the event data should be **TollBoothId**.</span></span> <span data-ttu-id="19a22-175">Firma Microsoft to zrobić w zapytaniu przez ustawienie **Partition By** do **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="19a22-175">We do this in the query by setting **Partition By** to **PartitionId**.</span></span> <span data-ttu-id="19a22-176">Ponieważ dane wyjściowe magazynu obiektów blob, firma Microsoft nie trzeba martwić się o konfigurowaniu wartość klucza partycji, zgodnie z harmonogramem wymaganie #4.</span><span class="sxs-lookup"><span data-stu-id="19a22-176">Since the output is blob storage, we don't need to worry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="19a22-177">Zapytanie wieloetapowych kluczem grupowania</span><span class="sxs-lookup"><span data-stu-id="19a22-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="19a22-178">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="19a22-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="19a22-179">Dane wyjściowe: Wystąpienie koncentratora zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="19a22-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="19a22-180">Zapytanie:</span><span class="sxs-lookup"><span data-stu-id="19a22-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="19a22-181">Ta kwerenda zawiera klucz grupowania, więc ten sam klucz musi być przetwarzane przez to samo wystąpienie zapytania.</span><span class="sxs-lookup"><span data-stu-id="19a22-181">This query has a grouping key, so the same key needs to be processed by the same query instance.</span></span> <span data-ttu-id="19a22-182">Możemy użyć tej samej strategii co w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="19a22-182">We can use the same strategy as in the previous example.</span></span> <span data-ttu-id="19a22-183">W takim przypadku zapytanie ma wiele kroków.</span><span class="sxs-lookup"><span data-stu-id="19a22-183">In this case, the query has multiple steps.</span></span> <span data-ttu-id="19a22-184">Ma każdego kroku **partycji przez PartitionId**?</span><span class="sxs-lookup"><span data-stu-id="19a22-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="19a22-185">Tak, aby zapytanie spełnia wymagania #3.</span><span class="sxs-lookup"><span data-stu-id="19a22-185">Yes, so the query fulfills requirement #3.</span></span> <span data-ttu-id="19a22-186">Dla danych wyjściowych, należy ustawić klucz partycji **PartitionId**, zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="19a22-186">For the output, we need to set the partition key to **PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="19a22-187">Można zobaczyć, że ma taką samą liczbę partycji jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="19a22-187">We can also see that it has the same number of partitions as the input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="19a22-188">Przykładowe scenariusze, które są *nie* embarrassingly równoległych</span><span class="sxs-lookup"><span data-stu-id="19a22-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="19a22-189">W poprzedniej sekcji możemy pokazano kilka scenariuszy embarrassingly równoległych.</span><span class="sxs-lookup"><span data-stu-id="19a22-189">In the previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="19a22-190">W tej sekcji omówiono scenariusze, które nie spełniają wszystkie wymagania dotyczące być embarrassingly równoległe.</span><span class="sxs-lookup"><span data-stu-id="19a22-190">In this section, we discuss scenarios that don't meet all the requirements to be embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="19a22-191">Liczba partycji niezgodne</span><span class="sxs-lookup"><span data-stu-id="19a22-191">Mismatched partition count</span></span>
* <span data-ttu-id="19a22-192">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="19a22-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="19a22-193">Dane wyjściowe: Centrum zdarzeń z partycjami 32</span><span class="sxs-lookup"><span data-stu-id="19a22-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="19a22-194">W takim przypadku nie ma znaczenia, zapytanie jest.</span><span class="sxs-lookup"><span data-stu-id="19a22-194">In this case, it doesn't matter what the query is.</span></span> <span data-ttu-id="19a22-195">Jeśli liczba partycji wejściowych nie odpowiada liczba partycji danych wyjściowych, topologia nie jest embarrassingly równoległych.</span><span class="sxs-lookup"><span data-stu-id="19a22-195">If the input partition count doesn't match the output partition count, the topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="19a22-196">Nie używa usługi event hubs lub magazynu obiektów blob jako dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="19a22-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="19a22-197">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="19a22-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="19a22-198">Dane wyjściowe: usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="19a22-198">Output: PowerBI</span></span>

<span data-ttu-id="19a22-199">Wyjście usługi Power BI aktualnie nie obsługuje partycjonowanie.</span><span class="sxs-lookup"><span data-stu-id="19a22-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="19a22-200">Dlatego w tym scenariuszu nie jest embarrassingly równoległych.</span><span class="sxs-lookup"><span data-stu-id="19a22-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="19a22-201">Zapytanie wieloetapowych o różnych wartościach Partition By</span><span class="sxs-lookup"><span data-stu-id="19a22-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="19a22-202">Wejście: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="19a22-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="19a22-203">Dane wyjściowe: Centrum zdarzeń z partycjami 8</span><span class="sxs-lookup"><span data-stu-id="19a22-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="19a22-204">Zapytanie:</span><span class="sxs-lookup"><span data-stu-id="19a22-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="19a22-205">Jak widać, drugi etap używa **TollBoothId** jako klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="19a22-205">As you can see, the second step uses **TollBoothId** as the partitioning key.</span></span> <span data-ttu-id="19a22-206">Ten krok nie jest taka sama, co w pierwszym kroku i dlatego wymaga do zrobienia losowa.</span><span class="sxs-lookup"><span data-stu-id="19a22-206">This step is not the same as the first step, and it therefore requires us to do a shuffle.</span></span> 

<span data-ttu-id="19a22-207">W poprzednich przykładach pokazano, niektóre zadania Stream Analytics, które odpowiadają (lub nie) embarrassingly równoległych topologii.</span><span class="sxs-lookup"><span data-stu-id="19a22-207">The preceding examples show some Stream Analytics jobs that conform to (or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="19a22-208">Jeśli są one zgodne, mają one potencjalnie maksymalną skalę.</span><span class="sxs-lookup"><span data-stu-id="19a22-208">If they do conform, they have the potential for maximum scale.</span></span> <span data-ttu-id="19a22-209">Aktualizacje dla zadania, które nie pasują do jednego z tych profilów skalowania wskazówki będą dostępne w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="19a22-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="19a22-210">Na razie użyj ogólne wskazówki w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="19a22-210">For now, use the general guidance in the following sections.</span></span>

## <a name="calculate-the-maximum-streaming-units-of-a-job"></a><span data-ttu-id="19a22-211">Oblicz maksymalną jednostki zadania przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="19a22-211">Calculate the maximum streaming units of a job</span></span>
<span data-ttu-id="19a22-212">Całkowita liczba jednostek przesyłania strumieniowego, które mogą być używane przez zadanie usługi Stream Analytics zależy od liczby kroków w zapytaniu zdefiniowane dla zadania i liczby partycji dla każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="19a22-212">The total number of streaming units that can be used by a Stream Analytics job depends on the number of steps in the query defined for the job and the number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="19a22-213">Kroki w kwerendzie</span><span class="sxs-lookup"><span data-stu-id="19a22-213">Steps in a query</span></span>
<span data-ttu-id="19a22-214">Kwerenda może mieć jeden lub wiele kroków.</span><span class="sxs-lookup"><span data-stu-id="19a22-214">A query can have one or many steps.</span></span> <span data-ttu-id="19a22-215">Każdy krok jest zdefiniowane przez podzapytania **WITH** — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="19a22-215">Each step is a subquery defined by the **WITH** keyword.</span></span> <span data-ttu-id="19a22-216">Zapytanie, które znajduje się poza **WITH** — słowo kluczowe (tylko w jednej kwerendzie) również będzie traktowany jako krok, na przykład **wybierz** instrukcji w następującym zapytaniu:</span><span class="sxs-lookup"><span data-stu-id="19a22-216">The query that is outside the **WITH** keyword (one query only) is also counted as a step, such as the **SELECT** statement in the following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="19a22-217">Ta kwerenda zawiera dwa kroki.</span><span class="sxs-lookup"><span data-stu-id="19a22-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="19a22-218">To zapytanie jest omówiona bardziej szczegółowo w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="19a22-218">This query is discussed in more detail later in the article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="19a22-219">Krok partycji</span><span class="sxs-lookup"><span data-stu-id="19a22-219">Partition a step</span></span>
<span data-ttu-id="19a22-220">Partycjonowanie krok wymaga spełnienia następujących warunków:</span><span class="sxs-lookup"><span data-stu-id="19a22-220">Partitioning a step requires the following conditions:</span></span>

* <span data-ttu-id="19a22-221">Źródło danych wejściowych musi być partycjonowane.</span><span class="sxs-lookup"><span data-stu-id="19a22-221">The input source must be partitioned.</span></span> 
* <span data-ttu-id="19a22-222">**Wybierz** instrukcji zapytania musi odczytywać partycjonowanej źródło danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="19a22-222">The **SELECT** statement of the query must read from a partitioned input source.</span></span>
* <span data-ttu-id="19a22-223">Zapytanie w ramach kroku musi mieć **Partition By** — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="19a22-223">The query within the step must have the **Partition By** keyword.</span></span>

<span data-ttu-id="19a22-224">Jeśli zapytanie jest podzielona na partycje, zdarzenia wejściowe są przetwarzane i zagregowane w oddzielnej partycji grupy, a dane wyjściowe zdarzenia są generowane dla poszczególnych grup.</span><span class="sxs-lookup"><span data-stu-id="19a22-224">When a query is partitioned, the input events are processed and aggregated in separate partition groups, and outputs events are generated for each of the groups.</span></span> <span data-ttu-id="19a22-225">Jeśli chcesz połączonych agregacja, należy utworzyć drugi etap niepartycjonowany do zagregowania.</span><span class="sxs-lookup"><span data-stu-id="19a22-225">If you want a combined aggregate, you must create a second non-partitioned step to aggregate.</span></span>

### <a name="calculate-the-max-streaming-units-for-a-job"></a><span data-ttu-id="19a22-226">Obliczenia maksymalnej liczby jednostek w zadaniu przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="19a22-226">Calculate the max streaming units for a job</span></span>
<span data-ttu-id="19a22-227">Wszystkie kroki niepartycjonowany razem można skalować do sześciu jednostki przesyłania strumieniowego (SUs) dla zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="19a22-227">All non-partitioned steps together can scale up to six streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="19a22-228">Aby dodać SUs, musi być dzielony na partycje kroku.</span><span class="sxs-lookup"><span data-stu-id="19a22-228">To add SUs, a step must be partitioned.</span></span> <span data-ttu-id="19a22-229">Każda partycja może mieć sześć SUs.</span><span class="sxs-lookup"><span data-stu-id="19a22-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="19a22-230">Zapytanie</span><span class="sxs-lookup"><span data-stu-id="19a22-230">Query</span></span></th><th><span data-ttu-id="19a22-231">Maksymalna liczba SUs zadania</span><span class="sxs-lookup"><span data-stu-id="19a22-231">Max SUs for the job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="19a22-232">Zapytanie zawiera w jednym kroku.</span><span class="sxs-lookup"><span data-stu-id="19a22-232">The query contains one step.</span></span></li>
<li><span data-ttu-id="19a22-233">Krok nie jest podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="19a22-233">The step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="19a22-234">6</span><span class="sxs-lookup"><span data-stu-id="19a22-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="19a22-235">Strumień danych wejściowych jest podzielona na partycje przez 3.</span><span class="sxs-lookup"><span data-stu-id="19a22-235">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="19a22-236">Zapytanie zawiera w jednym kroku.</span><span class="sxs-lookup"><span data-stu-id="19a22-236">The query contains one step.</span></span></li>
<li><span data-ttu-id="19a22-237">Krok jest podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="19a22-237">The step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="19a22-238">18</span><span class="sxs-lookup"><span data-stu-id="19a22-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="19a22-239">Zapytanie zawiera dwa kroki.</span><span class="sxs-lookup"><span data-stu-id="19a22-239">The query contains two steps.</span></span></li>
<li><span data-ttu-id="19a22-240">Żadne kroki są podzielone na partycje.</span><span class="sxs-lookup"><span data-stu-id="19a22-240">Neither of the steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="19a22-241">6</span><span class="sxs-lookup"><span data-stu-id="19a22-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="19a22-242">Strumień danych wejściowych jest podzielona na partycje przez 3.</span><span class="sxs-lookup"><span data-stu-id="19a22-242">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="19a22-243">Zapytanie zawiera dwa kroki.</span><span class="sxs-lookup"><span data-stu-id="19a22-243">The query contains two steps.</span></span> <span data-ttu-id="19a22-244">Wejściowych kroku jest podzielona na partycje, a drugi etap nie.</span><span class="sxs-lookup"><span data-stu-id="19a22-244">The input step is partitioned and the second step is not.</span></span></li>
<li><span data-ttu-id="19a22-245"><strong>Wybierz</strong> instrukcji odczytuje z podzielonym na partycje danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="19a22-245">The <strong>SELECT</strong> statement reads from the partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="19a22-246">24 (18 partycjonowanej kroki) + 6 niepartycjonowany czynności</span><span class="sxs-lookup"><span data-stu-id="19a22-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="19a22-247">Przykłady skalowania</span><span class="sxs-lookup"><span data-stu-id="19a22-247">Examples of scaling</span></span>

<span data-ttu-id="19a22-248">Następujące zapytanie oblicza liczbę samochodów w ramach pośrednictwa stacji przez, który ma trzy tollbooths okna trzy minuty.</span><span class="sxs-lookup"><span data-stu-id="19a22-248">The following query calculates the number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="19a22-249">To zapytanie może być skalowana maksymalnie sześć SUs.</span><span class="sxs-lookup"><span data-stu-id="19a22-249">This query can be scaled up to six SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="19a22-250">Aby użyć więcej SUs dla zapytania, musi być podzielony zarówno strumienia danych wejściowych, jak i zapytania.</span><span class="sxs-lookup"><span data-stu-id="19a22-250">To use more SUs for the query, both the input data stream and the query must be partitioned.</span></span> <span data-ttu-id="19a22-251">Ponieważ partycji strumień danych jest ustawiona na 3, następujące zmodyfikowanej zapytania mogą być skalowane maksymalnie 18 SUs:</span><span class="sxs-lookup"><span data-stu-id="19a22-251">Since the data stream partition is set to 3, the following modified query can be scaled up to 18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="19a22-252">Zapytanie jest podzielona na partycje, zdarzenia wejściowe są przetwarzane i zagregowane w oddzielnej partycji grup.</span><span class="sxs-lookup"><span data-stu-id="19a22-252">When a query is partitioned, the input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="19a22-253">Dane wyjściowe zdarzenia są także generowane dla poszczególnych grup.</span><span class="sxs-lookup"><span data-stu-id="19a22-253">Output events are also generated for each of the groups.</span></span> <span data-ttu-id="19a22-254">Partycjonowanie może powodować pewne nieoczekiwane wyniki podczas **GROUP BY** pole nie jest częścią klucza partycji w strumieniu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="19a22-254">Partitioning can cause some unexpected results when the **GROUP BY** field is not the partition key in the input data stream.</span></span> <span data-ttu-id="19a22-255">Na przykład **TollBoothId** pole w poprzednich zapytań nie jest klucz partycji **Input1**.</span><span class="sxs-lookup"><span data-stu-id="19a22-255">For example, the **TollBoothId** field in the previous query is not the partition key of **Input1**.</span></span> <span data-ttu-id="19a22-256">Wynik jest, że dane z budki #1 może rozprzestrzeniać się w wielu partycji.</span><span class="sxs-lookup"><span data-stu-id="19a22-256">The result is that the data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="19a22-257">Każdy z **Input1** partycje będą przetwarzane oddzielnie przez Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="19a22-257">Each of the **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="19a22-258">W związku z tym wiele rekordów liczba samochodów dla tego samego budki w tym samym oknie wirowania zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="19a22-258">As a result, multiple records of the car count for the same tollbooth in the same Tumbling window will be created.</span></span> <span data-ttu-id="19a22-259">Jeśli nie można zmienić klucza partycji wejściowych, można naprawić ten problem, dodając krok z systemem innym niż partycji, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="19a22-259">If the input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in the following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="19a22-260">To zapytanie może być skalowana do 24 SUs.</span><span class="sxs-lookup"><span data-stu-id="19a22-260">This query can be scaled to 24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="19a22-261">Jeśli są Sprzęganie dwóch strumieni, upewnij się, że strumienie są dzielone przez klucz partycji kolumny, która służy do tworzenia sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="19a22-261">If you are joining two streams, make sure that the streams are partitioned by the partition key of the column that you use to create the joins.</span></span> <span data-ttu-id="19a22-262">Upewnij się również mieć taką samą liczbę partycji w obu strumieni.</span><span class="sxs-lookup"><span data-stu-id="19a22-262">Also make sure that you have the same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="19a22-263">Konfigurowanie usługi Stream Analytics jednostki przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="19a22-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="19a22-264">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19a22-264">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="19a22-265">Na liście zasobów można znaleźć zadania usługi analiza strumienia, który chcesz skalować, a następnie otwórz go.</span><span class="sxs-lookup"><span data-stu-id="19a22-265">In the list of resources, find the Stream Analytics job that you want to scale and then open it.</span></span>
3. <span data-ttu-id="19a22-266">W bloku zadania w obszarze **Konfiguruj**, kliknij przycisk **skali**.</span><span class="sxs-lookup"><span data-stu-id="19a22-266">In the job blade, under **Configure**, click **Scale**.</span></span>

    ![Konfiguracja zadania usługi analiza strumienia portalu Azure][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="19a22-268">Aby ustawić SUs zadania za pomocą suwaka.</span><span class="sxs-lookup"><span data-stu-id="19a22-268">Use the slider to set the SUs for the job.</span></span> <span data-ttu-id="19a22-269">Zwróć uwagę, że jest ograniczona do określonych ustawień SU.</span><span class="sxs-lookup"><span data-stu-id="19a22-269">Notice that you are limited to specific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="19a22-270">Monitor wydajności zadania</span><span class="sxs-lookup"><span data-stu-id="19a22-270">Monitor job performance</span></span>
<span data-ttu-id="19a22-271">Przy użyciu portalu Azure, można śledzić przepływności zadania:</span><span class="sxs-lookup"><span data-stu-id="19a22-271">Using the Azure portal, you can track the throughput of a job:</span></span>

![Azure Stream Analytics monitorowanie zadań][img.stream.analytics.monitor.job]

<span data-ttu-id="19a22-273">Oblicz przepływność oczekiwanego obciążenia.</span><span class="sxs-lookup"><span data-stu-id="19a22-273">Calculate the expected throughput of the workload.</span></span> <span data-ttu-id="19a22-274">Jeśli przepustowość jest mniejsza niż oczekiwano, dostroić wejściowych partycji, ulepszenia zapytania i dodać SUs do zadania.</span><span class="sxs-lookup"><span data-stu-id="19a22-274">If the throughput is less than expected, tune the input partition, tune the query, and add SUs to your job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-the-raspberry-pi-scenario"></a><span data-ttu-id="19a22-275">Wizualizuj Stream Analytics przepustowość na dużą skalę: w scenariuszu Pi malina</span><span class="sxs-lookup"><span data-stu-id="19a22-275">Visualize Stream Analytics throughput at scale: the Raspberry Pi scenario</span></span>
<span data-ttu-id="19a22-276">Aby ułatwić zrozumienie, jak skalować zadania usługi analiza strumienia, wykonane eksperyment na podstawie danych wprowadzonych z urządzenia malina Pi.</span><span class="sxs-lookup"><span data-stu-id="19a22-276">To help you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="19a22-277">Tego eksperymentu poinformować nas, zobacz wpływu na przepustowość wiele jednostek przesyłania strumieniowego i partycje.</span><span class="sxs-lookup"><span data-stu-id="19a22-277">This experiment let us see the effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="19a22-278">W tym scenariuszu urządzenie wysyła dane czujników (klienci) do Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="19a22-278">In this scenario, the device sends sensor data (clients) to an event hub.</span></span> <span data-ttu-id="19a22-279">Przesyłanie strumieniowe Analytics przetwarza dane i wysyła alert ani w statystyce jako dane wyjściowe do innego Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="19a22-279">Streaming Analytics processes the data and sends an alert or statistics as an output to another event hub.</span></span> 

<span data-ttu-id="19a22-280">Klient wysyła dane czujników w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="19a22-280">The client sends sensor data in JSON format.</span></span> <span data-ttu-id="19a22-281">Dane wyjściowe jest również w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="19a22-281">The data output is also in JSON format.</span></span> <span data-ttu-id="19a22-282">Dane wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="19a22-282">The data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="19a22-283">Następujące zapytanie służy do wysyłania alertu po wyłączeniu światło:</span><span class="sxs-lookup"><span data-stu-id="19a22-283">The following query is used to send an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="19a22-284">Miara przepływności</span><span class="sxs-lookup"><span data-stu-id="19a22-284">Measure throughput</span></span>

<span data-ttu-id="19a22-285">W tym kontekście przepływność wynosi ilość danych wejściowych przetworzone przez usługę Stream Analytics w stałej ilości czasu.</span><span class="sxs-lookup"><span data-stu-id="19a22-285">In this context, throughput is the amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="19a22-286">(Firma Microsoft mierzy przez 10 minut.) Aby uzyskać najlepsze przepływności przetwarzania danych wejściowych, zarówno wejściowego strumienia danych i zapytania zostały podzielone na partycje.</span><span class="sxs-lookup"><span data-stu-id="19a22-286">(We measured for 10 minutes.) To achieve the best processing throughput for the input data, both the data stream input and the query were  partitioned.</span></span> <span data-ttu-id="19a22-287">Jest dostępna **COUNT()** do mierzenia, ile zdarzenia wejściowe były przetwarzane w kwerendzie.</span><span class="sxs-lookup"><span data-stu-id="19a22-287">We included **COUNT()** in the query to measure how many input events were processed.</span></span> <span data-ttu-id="19a22-288">Aby upewnij się, że zadania nie oczekiwał po prostu dla zdarzenia wejściowe przejdzie, każdej partycji Centrum zdarzeń wejściowych został wstępnie ładowane z około 300 MB danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="19a22-288">To make sure the job was not simply waiting for input events to come, each partition of the input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="19a22-289">W poniższej tabeli przedstawiono wyniki, którą widzieliśmy, gdy firma Microsoft zwiększyć liczbę jednostek przesyłania strumieniowego i odpowiadająca mu partycja liczby w usłudze event hubs.</span><span class="sxs-lookup"><span data-stu-id="19a22-289">The following table shows the results we saw when we increased the number of streaming units and the corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="19a22-290">Partycje wejściowych</span><span class="sxs-lookup"><span data-stu-id="19a22-290">Input Partitions</span></span></th><th><span data-ttu-id="19a22-291">Partycje danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="19a22-291">Output Partitions</span></span></th><th><span data-ttu-id="19a22-292">Jednostki przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="19a22-292">Streaming Units</span></span></th><th><span data-ttu-id="19a22-293">Długoterminowa przepustowość</span><span class="sxs-lookup"><span data-stu-id="19a22-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="19a22-294">12</span><span class="sxs-lookup"><span data-stu-id="19a22-294">12</span></span></td>
<td><span data-ttu-id="19a22-295">12</span><span class="sxs-lookup"><span data-stu-id="19a22-295">12</span></span></td>
<td><span data-ttu-id="19a22-296">6</span><span class="sxs-lookup"><span data-stu-id="19a22-296">6</span></span></td>
<td><span data-ttu-id="19a22-297">4.06 MB/s</span><span class="sxs-lookup"><span data-stu-id="19a22-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="19a22-298">12</span><span class="sxs-lookup"><span data-stu-id="19a22-298">12</span></span></td>
<td><span data-ttu-id="19a22-299">12</span><span class="sxs-lookup"><span data-stu-id="19a22-299">12</span></span></td>
<td><span data-ttu-id="19a22-300">12</span><span class="sxs-lookup"><span data-stu-id="19a22-300">12</span></span></td>
<td><span data-ttu-id="19a22-301">8.06 MB/s</span><span class="sxs-lookup"><span data-stu-id="19a22-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="19a22-302">48</span><span class="sxs-lookup"><span data-stu-id="19a22-302">48</span></span></td>
<td><span data-ttu-id="19a22-303">48</span><span class="sxs-lookup"><span data-stu-id="19a22-303">48</span></span></td>
<td><span data-ttu-id="19a22-304">48</span><span class="sxs-lookup"><span data-stu-id="19a22-304">48</span></span></td>
<td><span data-ttu-id="19a22-305">38.32 MB/s</span><span class="sxs-lookup"><span data-stu-id="19a22-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="19a22-306">192</span><span class="sxs-lookup"><span data-stu-id="19a22-306">192</span></span></td>
<td><span data-ttu-id="19a22-307">192</span><span class="sxs-lookup"><span data-stu-id="19a22-307">192</span></span></td>
<td><span data-ttu-id="19a22-308">192</span><span class="sxs-lookup"><span data-stu-id="19a22-308">192</span></span></td>
<td><span data-ttu-id="19a22-309">172.67 MB/s</span><span class="sxs-lookup"><span data-stu-id="19a22-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="19a22-310">480</span><span class="sxs-lookup"><span data-stu-id="19a22-310">480</span></span></td>
<td><span data-ttu-id="19a22-311">480</span><span class="sxs-lookup"><span data-stu-id="19a22-311">480</span></span></td>
<td><span data-ttu-id="19a22-312">480</span><span class="sxs-lookup"><span data-stu-id="19a22-312">480</span></span></td>
<td><span data-ttu-id="19a22-313">454.27 MB/s</span><span class="sxs-lookup"><span data-stu-id="19a22-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="19a22-314">720</span><span class="sxs-lookup"><span data-stu-id="19a22-314">720</span></span></td>
<td><span data-ttu-id="19a22-315">720</span><span class="sxs-lookup"><span data-stu-id="19a22-315">720</span></span></td>
<td><span data-ttu-id="19a22-316">720</span><span class="sxs-lookup"><span data-stu-id="19a22-316">720</span></span></td>
<td><span data-ttu-id="19a22-317">609.69 MB/s</span><span class="sxs-lookup"><span data-stu-id="19a22-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="19a22-318">I Wykres ukazuje wizualizacji relacji między usługami SUs i przepływności.</span><span class="sxs-lookup"><span data-stu-id="19a22-318">And the following graph shows a visualization of the relationship between SUs and throughput.</span></span>

![img.stream.Analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="19a22-320">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="19a22-320">Get help</span></span>
<span data-ttu-id="19a22-321">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="19a22-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="19a22-322">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="19a22-322">Next steps</span></span>
* [<span data-ttu-id="19a22-323">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="19a22-323">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="19a22-324">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="19a22-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="19a22-325">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="19a22-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="19a22-326">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="19a22-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

