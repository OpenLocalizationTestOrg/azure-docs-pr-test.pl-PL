---
title: "Usługa Azure Stream Analytics: Optymalizacja toouse Twojego zadania jednostki przesyłania strumieniowego wydajnie | Dokumentacja firmy Microsoft"
description: "Zapytanie najlepsze rozwiązania dotyczące skalowania i wydajności w usługi Azure Stream Analytics."
keywords: "Jednostka, wydajność zapytań"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a><span data-ttu-id="25ab5-104">Optymalizacja wydajnie toouse Twojego zadania jednostki przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="25ab5-104">Optimize your job toouse Streaming Units efficiently</span></span>

<span data-ttu-id="25ab5-105">Usługa Azure Stream Analytics agreguje wydajności hello "waga" uruchamiania zadania do jednostek przesyłania strumieniowego (SUs).</span><span class="sxs-lookup"><span data-stu-id="25ab5-105">Azure Stream Analytics aggregates hello performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="25ab5-106">Usługi SUs reprezentują hello zasobów obliczeniowych, które są wykorzystanych tooexecute zadania.</span><span class="sxs-lookup"><span data-stu-id="25ab5-106">SUs represent hello computing resources that are consumed tooexecute a job.</span></span> <span data-ttu-id="25ab5-107">Usługi SUs zapewniają sposób toodescribe hello względną przetwarzania zdarzeń pojemności oparte na mieszanych pomiarach Procesora, pamięci, Odczyt i zapis stawki.</span><span class="sxs-lookup"><span data-stu-id="25ab5-107">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="25ab5-108">Pozwala to wydajność można skupić się na powitania logikę kwerendy i usuwa z konieczności tooknow magazynu warstwy zagadnienia dotyczące wydajności, ręcznie przydzielić pamięci dla zadania, a przybliżona hello Procesora core-liczby potrzebnych toorun zadania w odpowiednim czasie.</span><span class="sxs-lookup"><span data-stu-id="25ab5-108">This capacity lets you focus on hello query logic and removes you from needing tooknow storage tier performance considerations, allocate memory for your job manually, and approximate hello CPU core-count needed toorun your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="25ab5-109">Ile SUs są wymagane w przypadku zadania?</span><span class="sxs-lookup"><span data-stu-id="25ab5-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="25ab5-110">Wybór hello liczba SUs wymagane dla określonego zadania zależy od konfiguracji partycji hello hello dane wejściowe i hello zapytania, który jest zdefiniowany w ramach zadania hello.</span><span class="sxs-lookup"><span data-stu-id="25ab5-110">Choosing hello number of required SUs for a particular job depends on hello partition configuration for hello inputs and hello query that's defined within hello job.</span></span> <span data-ttu-id="25ab5-111">Witaj **skali** bloku pozwala tooset hello prawo liczba SUs.</span><span class="sxs-lookup"><span data-stu-id="25ab5-111">hello **Scale** blade allows you tooset hello right number of SUs.</span></span> <span data-ttu-id="25ab5-112">Jest najlepszym rozwiązaniem tooallocate SUs więcej niż jest to potrzebne.</span><span class="sxs-lookup"><span data-stu-id="25ab5-112">It is a best practice tooallocate more SUs than needed.</span></span> <span data-ttu-id="25ab5-113">aparat przetwarzania Stream Analytics Hello optymalizuje opóźnienia i przepływności na powitania koszt przydzielania dodatkowych pamięci.</span><span class="sxs-lookup"><span data-stu-id="25ab5-113">hello Stream Analytics processing engine optimizes for latency and throughput at hello cost of allocating additional memory.</span></span>

<span data-ttu-id="25ab5-114">Ogólnie rzecz biorąc, najlepiej hello jest toostart z 6 SUs zapytań, które nie używają *PARTITION BY*.</span><span class="sxs-lookup"><span data-stu-id="25ab5-114">In general, hello best practice is toostart with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="25ab5-115">Następnie określ hello słodka miejscu przy użyciu metody prób i błędów, w którym można zmodyfikować hello liczba SUs po przekazać reprezentatywny ilości danych i sprawdź, czy hello SU % wykorzystania metryki.</span><span class="sxs-lookup"><span data-stu-id="25ab5-115">Then determine hello sweet spot by using a trial and error method in which you modify hello number of SUs after you pass representative amounts of data and examine hello SU %Utilization metric.</span></span>

<span data-ttu-id="25ab5-116">Usługa Azure Stream Analytics śledzi zdarzenia w oknie o nazwie hello "zmiany kolejności buforu" przed rozpoczęciem jakiegokolwiek przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="25ab5-116">Azure Stream Analytics keeps events in a window called hello “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="25ab5-117">Zdarzenia są sortowane w obrębie okna zmiany kolejności hello czasu, a kolejne operacje są wykonywane na powitania tymczasowo sortowane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="25ab5-117">Events are sorted within hello reorder window by time, and subsequent operations are performed on hello temporally sorted events.</span></span> <span data-ttu-id="25ab5-118">Ponowne porządkowanie zdarzenia według czasu zapewnia operatora hello ma dostęp do wszystkich zdarzeń hello w hello określone przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="25ab5-118">Reordering events by time ensures that hello operator has visibility into all hello events in hello stipulated timeframe.</span></span> <span data-ttu-id="25ab5-119">Ponadto pozwala on usłudze operator hello przetwarzania wymagane hello i utworzenie danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="25ab5-119">It also lets hello operator perform hello requisite processing and produce an output.</span></span> <span data-ttu-id="25ab5-120">Efektem ubocznym ten mechanizm jest, że przetwarzania jest opóźniony o hello zmiany kolejności przedział czasu hello.</span><span class="sxs-lookup"><span data-stu-id="25ab5-120">A side effect of this mechanism is that processing is delayed by hello duration of hello reorder window.</span></span> <span data-ttu-id="25ab5-121">zużycie pamięci Hello zadania hello, (co wpływa na zużycie SU) to funkcja hello rozmiaru tej zmiany kolejności okno i hello liczba zdarzeń w nim zawarte.</span><span class="sxs-lookup"><span data-stu-id="25ab5-121">hello memory footprint of hello job (which affects SU consumption) is a function of hello size of this reorder window and hello number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="25ab5-122">Po zmianie podczas uaktualniania zadania hello liczbę czytników przejściowej ostrzeżenia są zapisywane tooaudit dzienniki.</span><span class="sxs-lookup"><span data-stu-id="25ab5-122">When hello number of readers changes during job upgrades, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="25ab5-123">Zadania usługi analiza strumienia automatycznie odzyskać te przejściowych problemów.</span><span class="sxs-lookup"><span data-stu-id="25ab5-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="25ab5-124">Typowe przyczyny wysokiej pamięci wzrost wykorzystania SU dla uruchomionych zadań</span><span class="sxs-lookup"><span data-stu-id="25ab5-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="25ab5-125">Dużej kardynalności Grupuj według</span><span class="sxs-lookup"><span data-stu-id="25ab5-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="25ab5-126">Kardynalność Hello zdarzenia przychodzące nakazują użycie pamięci hello zadania.</span><span class="sxs-lookup"><span data-stu-id="25ab5-126">hello cardinality of incoming events dictates memory usage for hello job.</span></span>

<span data-ttu-id="25ab5-127">Na przykład w `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello numer skojarzony z **klastrowanych** jest Kardynalność hello hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="25ab5-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello number associated with **clustered** is hello cardinality of hello query.</span></span>

<span data-ttu-id="25ab5-128">toomitigate problemów, które są spowodowane dużej kardynalności skalowanie w poziomie zapytania hello zwiększając partycje przy użyciu **PARTITION BY**.</span><span class="sxs-lookup"><span data-stu-id="25ab5-128">toomitigate issues that are caused by high cardinality, scale out hello query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="25ab5-129">Witaj liczba *klastrowanych* jest hello Kardynalność GROUP BY w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="25ab5-129">hello number of *clustered* is hello cardinality of GROUP BY here.</span></span>

<span data-ttu-id="25ab5-130">Po zapytania hello jest podzielona na partycje, jego jest rozproszone na wielu węzłach.</span><span class="sxs-lookup"><span data-stu-id="25ab5-130">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="25ab5-131">W związku z tym hello zdarzenia wchodzących w każdym węźle ograniczono liczbę, co z kolei zmniejsza rozmiar hello hello zmiany kolejności buforu.</span><span class="sxs-lookup"><span data-stu-id="25ab5-131">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> <span data-ttu-id="25ab5-132">Należy również partycji partycji Centrum zdarzeń według identyfikatora partitionid.</span><span class="sxs-lookup"><span data-stu-id="25ab5-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="25ab5-133">Liczba wysokiej niedopasowane zdarzeń w celu utworzenia sprzężenia</span><span class="sxs-lookup"><span data-stu-id="25ab5-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="25ab5-134">Hello liczba zdarzeń niedopasowane sprzężenia wpływa na powitania użycie pamięci przez program hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="25ab5-134">hello number of unmatched events in a JOIN affects hello memory utilization of hello query.</span></span> <span data-ttu-id="25ab5-135">Na przykład wykonać kwerendę, która potrzebuje toofind hello liczba ad wyświetleń generujący kliknięć:</span><span class="sxs-lookup"><span data-stu-id="25ab5-135">For example, take a query that is looking toofind hello number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="25ab5-136">W tym scenariuszu jest możliwe, że podano wiele reklam i są generowane kilku kliknięć.</span><span class="sxs-lookup"><span data-stu-id="25ab5-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="25ab5-137">Takie wynik wymagają hello zadania tookeep wszystkie zdarzenia hello w hello przedział czasu.</span><span class="sxs-lookup"><span data-stu-id="25ab5-137">Such a result would require hello job tookeep all hello events within hello time window.</span></span> <span data-ttu-id="25ab5-138">Hello ilości pamięci używanej to okno toohello proporcjonalny szybkość rozmiaru i zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="25ab5-138">hello amount of memory consumed is proportional toohello window size and event rate.</span></span> 

<span data-ttu-id="25ab5-139">toomitigate takiej sytuacji skalowania w poziomie zapytania hello zwiększając partycje przy użyciu PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="25ab5-139">toomitigate this situation, scale out hello query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="25ab5-140">Po zapytania hello jest podzielona na partycje, jego jest rozproszone na wielu węzłach przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="25ab5-140">After hello query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="25ab5-141">W związku z tym hello zdarzenia wchodzących w każdym węźle ograniczono liczbę, co z kolei zmniejsza rozmiar hello hello zmiany kolejności buforu.</span><span class="sxs-lookup"><span data-stu-id="25ab5-141">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="25ab5-142">Duża liczba zdarzeń poza kolejnością</span><span class="sxs-lookup"><span data-stu-id="25ab5-142">Large number of out of order events</span></span> 

<span data-ttu-id="25ab5-143">Dużą liczbę zdarzenia poza kolejnością w przedziale czasu dużych powoduje, że rozmiar hello toobe "Zmień kolejność buforu" hello większy.</span><span class="sxs-lookup"><span data-stu-id="25ab5-143">A large number of out of order events within a large time window causes hello size of hello "reorder buffer" toobe larger.</span></span> <span data-ttu-id="25ab5-144">toomitigate takiej sytuacji zapytania hello skali, zwiększając partycje przy użyciu PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="25ab5-144">toomitigate this situation, scale hello query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="25ab5-145">Po zapytania hello jest podzielona na partycje, jego jest rozproszone na wielu węzłach.</span><span class="sxs-lookup"><span data-stu-id="25ab5-145">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="25ab5-146">W związku z tym hello zdarzenia wchodzących w każdym węźle ograniczono liczbę, co z kolei zmniejsza rozmiar hello hello zmiany kolejności buforu.</span><span class="sxs-lookup"><span data-stu-id="25ab5-146">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="25ab5-147">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="25ab5-147">Get help</span></span>
<span data-ttu-id="25ab5-148">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="25ab5-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="25ab5-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25ab5-149">Next steps</span></span>
* [<span data-ttu-id="25ab5-150">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="25ab5-150">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="25ab5-151">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="25ab5-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="25ab5-152">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="25ab5-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="25ab5-153">Dokumentacja języka zapytań usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="25ab5-153">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="25ab5-154">Odwołania API REST zarządzania usługi analiza strumienia Azure</span><span class="sxs-lookup"><span data-stu-id="25ab5-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
