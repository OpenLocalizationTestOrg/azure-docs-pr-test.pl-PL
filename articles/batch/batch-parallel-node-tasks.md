---
title: "aaaRun zadań równoległych toouse zasoby obliczeniowe wydajnie - partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Zwiększenie wydajności i zredukowania kosztów przy użyciu mniejszej liczby węzłów obliczeniowych i uruchamianie równoczesnych zadań w każdym węźle w puli partii zadań Azure"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="d9d6b-103">Równoczesne uruchamianie zadań toomaximize użycia węzłów obliczeniowych partii</span><span class="sxs-lookup"><span data-stu-id="d9d6b-103">Run tasks concurrently toomaximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="d9d6b-104">Uruchamiając więcej niż jedno zadanie równocześnie w każdym węźle obliczeń w puli partii zadań Azure, można zmaksymalizować użycia zasobów na mniejszą liczbę węzłów w puli hello.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in hello pool.</span></span> <span data-ttu-id="d9d6b-105">W przypadku niektórych obciążeń może to spowodować krótszych czasów zadań i tańsze.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="d9d6b-106">Gdy niektóre scenariusze korzystania z dedykowanym wszystkie zasoby węzła tooa pojedyncze zadanie, kilku sytuacjach korzystać z stosowanie wielu zadań tooshare tych zasobów:</span><span class="sxs-lookup"><span data-stu-id="d9d6b-106">While some scenarios benefit from dedicating all of a node's resources tooa single task, several situations benefit from allowing multiple tasks tooshare those resources:</span></span>

* <span data-ttu-id="d9d6b-107">**Minimalizowanie transferu danych** podczas zadania są możliwe tooshare danych.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-107">**Minimizing data transfer** when tasks are able tooshare data.</span></span> <span data-ttu-id="d9d6b-108">W tym scenariuszu może znacznie zmniejszyć koszty transferu danych przez skopiowanie danych udostępnionych tooa mniejszej liczby węzłów i wykonywanie zadań równolegle na każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data tooa smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="d9d6b-109">Dotyczy to zwłaszcza, jeśli węzeł skopiowanych tooeach toobe danych hello muszą być przekazywane między regionów geograficznych.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-109">This especially applies if hello data toobe copied tooeach node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="d9d6b-110">**Maksymalizacja użycie pamięci** podczas zadania wymagają dużej ilości pamięci, ale tylko w krótkich okresach czasu i w czasie zmiennej podczas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="d9d6b-111">Można stosować mniej, ale większy, wyliczenia węzłów mających więcej pamięci tooefficiently obsługi tych wartości szczytowe.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-111">You can employ fewer, but larger, compute nodes with more memory tooefficiently handle such spikes.</span></span> <span data-ttu-id="d9d6b-112">Te węzły byłyby wielu zadań uruchomione równolegle w każdym węźle, ale każde zadanie będzie korzystać węzłów hello dużej ilości pamięci w różnym czasie.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of hello nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="d9d6b-113">**Zmniejszenia limity numer węzła** podczas komunikacji między węzłami jest wymagana w puli.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="d9d6b-114">Obecnie pule skonfigurowane do komunikacji między węzłami są ograniczone too50 węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-114">Currently, pools configured for inter-node communication are limited too50 compute nodes.</span></span> <span data-ttu-id="d9d6b-115">Jeśli każdy węzeł w takich puli jest tooexecute stanie zadania równolegle, większa liczba zadań mogą być wykonywane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-115">If each node in such a pool is able tooexecute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="d9d6b-116">**Replikowanie lokalnych klastra obliczeniowego**, takie jak kiedy najpierw przenieść tooAzure środowiska obliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment tooAzure.</span></span> <span data-ttu-id="d9d6b-117">Jeśli bieżącego rozwiązania lokalnego wykonuje wiele zadań na węzeł obliczeń, można zwiększyć maksymalną liczbę hello zadań węzła toomore ściśle duplikatów tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-117">If your current on-premises solution executes multiple tasks per compute node, you can increase hello maximum number of node tasks toomore closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="d9d6b-118">Przykładowy scenariusz</span><span class="sxs-lookup"><span data-stu-id="d9d6b-118">Example scenario</span></span>
<span data-ttu-id="d9d6b-119">Jako przykład tooillustrate hello zalet wykonywanie zadań równoległych, załóżmy, że aplikacja zadanie ma wymagania dotyczące procesora CPU i pamięci tak, aby [standardowe\_D1](../cloud-services/cloud-services-sizes-specs.md) węzły są wystarczające.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-119">As an example tooillustrate hello benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="d9d6b-120">Jednak w kolejności toofinish hello zadania w czasie hello wymagane 1000 te węzły są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-120">But, in order toofinish hello job in hello required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="d9d6b-121">Zamiast standardowego\_D1 węzły, które mają 1 rdzeń procesora CPU, można użyć [standardowe\_D14](../cloud-services/cloud-services-sizes-specs.md) węzłów, które ma 16 rdzeni i włącz wykonywanie zadań równoległych.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="d9d6b-122">W związku z tym *16 razy mniej węzłów* można użyć — zamiast 1000 węzłów tylko 63 będą wymagane.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="d9d6b-123">Ponadto jeśli pliki dużych aplikacji lub dane referencyjne są wymagane dla każdego węzła, czas trwania zadania i wydajności ponownie lepsza od hello dane są kopiowane tooonly 16 węzłów.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since hello data is copied tooonly 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="d9d6b-124">Włącz wykonywanie zadań równoległych</span><span class="sxs-lookup"><span data-stu-id="d9d6b-124">Enable parallel task execution</span></span>
<span data-ttu-id="d9d6b-125">Węzłami obliczeniowymi w celu wykonania zadań równoległych można skonfigurować na poziomie puli hello.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-125">You configure compute nodes for parallel task execution at hello pool level.</span></span> <span data-ttu-id="d9d6b-126">Z biblioteki .NET partii hello, ustaw hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] właściwość podczas tworzenia puli.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-126">With hello Batch .NET library, set hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="d9d6b-127">Jeśli używasz hello interfejsu API REST partii ustawić hello [maxTasksPerNode] [ rest_addpool] elementu w treści żądania hello podczas tworzenia puli.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-127">If you are using hello Batch REST API, set hello [maxTasksPerNode][rest_addpool] element in hello request body during pool creation.</span></span>

<span data-ttu-id="d9d6b-128">Partia zadań Azure umożliwia tooset maksymalną zadań na węzeł toofour razy (4 x) hello liczby rdzeni węzła.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-128">Azure Batch allows you tooset maximum tasks per node up toofour times (4x) hello number of node cores.</span></span> <span data-ttu-id="d9d6b-129">Na przykład jeśli hello pula jest skonfigurowana z węzłami rozmiar "Duże" (4 rdzenie), następnie `maxTasksPerNode` too16 może być ustawiony.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-129">For example, if hello pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set too16.</span></span> <span data-ttu-id="d9d6b-130">Aby uzyskać szczegółowe informacje na powitania liczba rdzeni dla każdego rozmiary węzła hello, zobacz [rozmiary dla usług w chmurze](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="d9d6b-130">For details on hello number of cores for each of hello node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="d9d6b-131">Aby uzyskać więcej informacji na ograniczenia usługi, zobacz [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="d9d6b-131">For more information on service limits, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="d9d6b-132">Można tootake się do konta hello `maxTasksPerNode` wartość utworzenia [formułą automatycznego skalowania] [ enable_autoscaling] dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-132">Be sure tootake into account hello `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="d9d6b-133">Na przykład formuła, której wynikiem `$RunningTasks` może mieć znaczący wpływ wzrost zadań na węzeł.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="d9d6b-134">Zobacz [automatycznie skali obliczeniowe węzłów w puli partii zadań Azure](batch-automatic-scaling.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="d9d6b-135">Podział zadań</span><span class="sxs-lookup"><span data-stu-id="d9d6b-135">Distribution of tasks</span></span>
<span data-ttu-id="d9d6b-136">W przypadku hello węzłów obliczeniowych w puli mogą jednocześnie wykonywać zadania, jest ważne toospecify sposób toobe zadania hello rozproszone na węzłach hello hello puli.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-136">When hello compute nodes in a pool can execute tasks concurrently, it's important toospecify how you want hello tasks toobe distributed across hello nodes in hello pool.</span></span>

<span data-ttu-id="d9d6b-137">Za pomocą hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] właściwości, można określić czy zadania powinien być przypisany równomiernie we wszystkich węzłach w puli hello ("rozpraszania").</span><span class="sxs-lookup"><span data-stu-id="d9d6b-137">By using hello [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in hello pool ("spreading").</span></span> <span data-ttu-id="d9d6b-138">Lub możesz określić, że jako wiele zadań, jak to możliwe należy przypisać węzła tooeach przed zadania są przydzielone tooanother węzła w puli hello ("pakowania").</span><span class="sxs-lookup"><span data-stu-id="d9d6b-138">Or you can specify that as many tasks as possible should be assigned tooeach node before tasks are assigned tooanother node in hello pool ("packing").</span></span>

<span data-ttu-id="d9d6b-139">Jako przykład sposobu ta funkcja jest przydatna, należy wziąć pod uwagę puli hello [standardowe\_D14](../cloud-services/cloud-services-sizes-specs.md) węzłów (w powyższym przykładzie hello), które skonfigurowano [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] wartość 16.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-139">As an example of how this feature is valuable, consider hello pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in hello example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="d9d6b-140">Jeśli hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] skonfigurowano [ComputeNodeFillType] [ fill_type] z *pakietu*, czy zmaksymalizować użycie wszystkich rdzeni 16 każdego węzła i umożliwia [puli Skalowanie automatyczne](batch-automatic-scaling.md) tooprune nieużywanych węzłów z puli hello (węzłów bez żadnych zadań przypisane).</span><span class="sxs-lookup"><span data-stu-id="d9d6b-140">If hello [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) tooprune unused nodes from hello pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="d9d6b-141">Ten sposób można zmniejszyć obciążenie zasobów i zapisuje pieniędzy.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="d9d6b-142">Przykład .NET partii</span><span class="sxs-lookup"><span data-stu-id="d9d6b-142">Batch .NET example</span></span>
<span data-ttu-id="d9d6b-143">To [partiami platformy .NET] [ api_net] interfejsu API fragment kodu przedstawia toocreate żądania puli, która zawiera cztery węzły dużych maksymalnie cztery zadania w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-143">This [Batch .NET][api_net] API code snippet shows a request toocreate a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="d9d6b-144">Określa zadanie planowania zasad, które spowoduje wypełnienie każdego węzła za węzeł tooanother zadania tooassigning wcześniejszych zadań w puli hello.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-144">It specifies a task scheduling policy that will fill each node with tasks prior tooassigning tasks tooanother node in hello pool.</span></span> <span data-ttu-id="d9d6b-145">Aby uzyskać więcej informacji o dodawaniu pule przy użyciu hello interfejs API .NET partii zobacz [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="d9d6b-145">For more information on adding pools by using hello Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a><span data-ttu-id="d9d6b-146">Przykład REST partii</span><span class="sxs-lookup"><span data-stu-id="d9d6b-146">Batch REST example</span></span>
<span data-ttu-id="d9d6b-147">To [REST partii] [ api_rest] interfejsu API fragment kodu przedstawia toocreate żądania puli, która zawiera dwa węzły dużych maksymalnie cztery zadania w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-147">This [Batch REST][api_rest] API snippet shows a request toocreate a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="d9d6b-148">Aby uzyskać więcej informacji o dodawaniu pule przy użyciu interfejsu API REST hello, zobacz [dodać konto puli tooan][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="d9d6b-148">For more information on adding pools by using hello REST API, see [Add a pool tooan account][rest_addpool].</span></span>

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> <span data-ttu-id="d9d6b-149">Można ustawić hello `maxTasksPerNode` elementu i [MaxTasksPerComputeNode] [ maxtasks_net] właściwość tylko w czasie tworzenia puli.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-149">You can set hello `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="d9d6b-150">Nie można zmodyfikować po puli został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="d9d6b-151">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="d9d6b-151">Code sample</span></span>
<span data-ttu-id="d9d6b-152">Witaj [ParallelNodeTasks] [ parallel_tasks_sample] projektu w witrynie GitHub przedstawiono użycie hello hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] właściwości.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-152">hello [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates hello use of hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="d9d6b-153">Witaj korzysta z tej aplikacji konsolowej C# [partiami platformy .NET] [ api_net] toocreate biblioteki puli z co najmniej jednym węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-153">This C# console application uses hello [Batch .NET][api_net] library toocreate a pool with one or more compute nodes.</span></span> <span data-ttu-id="d9d6b-154">Można skonfigurować wiele zadań jest wykonywana na tych węzłach toosimulate zmiennej obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-154">It executes a configurable number of tasks on those nodes toosimulate variable load.</span></span> <span data-ttu-id="d9d6b-155">Dane wyjściowe aplikacji hello Określa węzły, które wykonywane każdego zadania.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-155">Output from hello application specifies which nodes executed each task.</span></span> <span data-ttu-id="d9d6b-156">Aplikacja Hello także podsumowanie hello parametrów zadania i czas trwania.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-156">hello application also provides a summary of hello job parameters and duration.</span></span> <span data-ttu-id="d9d6b-157">Podsumowanie część hello dane wyjściowe dwa przebiegi różnych hello przykładowej aplikacji Hello pojawia się poniżej.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-157">hello summary portion of hello output from two different runs of hello sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="d9d6b-158">pierwszy wykonywanie hello przykładowej aplikacji Hello wskazuje, że z jednego węzła w puli hello i hello domyślne ustawienie jedno zadanie na węźle, czas trwania zadania hello jest ponad 30 minut.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-158">hello first execution of hello sample application shows that with a single node in hello pool and hello default setting of one task per node, hello job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="d9d6b-159">Witaj, drugi uruchomienie przedstawiono przykładowe hello znaczny spadek czas trwania zadania.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-159">hello second run of hello sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="d9d6b-160">Jest to spowodowane puli hello został skonfigurowany z czterech zadań na węzeł, dzięki czemu zadanie równoległe wykonywanie toocomplete hello zadania w niemal kwartału hello czasu.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-160">This is because hello pool was configured with four tasks per node, which allows for parallel task execution toocomplete hello job in nearly a quarter of hello time.</span></span>

> [!NOTE]
> <span data-ttu-id="d9d6b-161">czas trwania zadania Hello w powyższych podsumowania hello nie dołączaj czas utworzenia puli.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-161">hello job durations in hello summaries above do not include pool creation time.</span></span> <span data-ttu-id="d9d6b-162">Każdego z powyższych zadań hello został przesłany toopreviously utworzone pule którego węzły obliczeniowe były hello *bezczynny* stanu w czasie przesyłania.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-162">Each of hello jobs above was submitted toopreviously created pools whose compute nodes were in hello *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d9d6b-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9d6b-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="d9d6b-164">Mapa cieplna Explorer partii</span><span class="sxs-lookup"><span data-stu-id="d9d6b-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="d9d6b-165">Witaj [Eksploratora usługi partia zadań Azure][batch_explorer], jeden hello partii zadań Azure [przykładowe aplikacje][github_samples], zawiera *Mapa cieplna* funkcja, która umożliwia wizualizację wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-165">hello [Azure Batch Explorer][batch_explorer], one of hello Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="d9d6b-166">Jeśli w przypadku wykonywania hello [ParallelTasks] [ parallel_tasks_sample] przykładowej aplikacji, można użyć hello Mapa cieplna funkcji tooeasily wizualizacji hello wykonywanie zadań równoległych w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="d9d6b-166">When you're executing hello [ParallelTasks][parallel_tasks_sample] sample application, you can use hello Heat Map feature tooeasily visualize hello execution of parallel tasks on each node.</span></span>

![Mapa cieplna Explorer partii][1]

<span data-ttu-id="d9d6b-168">*Mapa cieplna Explorer partii przedstawiający puli czterech węzłów z każdego węzła aktualnie wykonywanych zadań cztery*</span><span class="sxs-lookup"><span data-stu-id="d9d6b-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
