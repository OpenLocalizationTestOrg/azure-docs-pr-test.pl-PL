---
title: "Uruchom zadania równolegle efektywnie - korzystać z zasobów obliczeniowych partii zadań Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6903552d907a1ddb21d3b678e2d224b4b5e35b77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-concurrently-to-maximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="686f5-103">Węzły obliczeniowe uruchamiania zadań jednocześnie, aby zapewnić maksymalne użycie usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="686f5-103">Run tasks concurrently to maximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="686f5-104">Uruchamiając więcej niż jedno zadanie równocześnie w każdym węźle obliczeń w puli partii zadań Azure, można zmaksymalizować użycia zasobów na mniejszą liczbę węzłów w puli.</span><span class="sxs-lookup"><span data-stu-id="686f5-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in the pool.</span></span> <span data-ttu-id="686f5-105">W przypadku niektórych obciążeń może to spowodować krótszych czasów zadań i tańsze.</span><span class="sxs-lookup"><span data-stu-id="686f5-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="686f5-106">Gdy niektóre scenariusze korzystania z dedykowanym wszystkie zasoby węzła do danego zadania, kilku sytuacjach korzystać z wielu zadań udostępnić te zasoby umożliwiające:</span><span class="sxs-lookup"><span data-stu-id="686f5-106">While some scenarios benefit from dedicating all of a node's resources to a single task, several situations benefit from allowing multiple tasks to share those resources:</span></span>

* <span data-ttu-id="686f5-107">**Minimalizowanie transferu danych** podczas zadania będą mogli udostępniać dane.</span><span class="sxs-lookup"><span data-stu-id="686f5-107">**Minimizing data transfer** when tasks are able to share data.</span></span> <span data-ttu-id="686f5-108">W tym scenariuszu można zdecydowanie zmniejszyć koszty transferu danych przez skopiowanie danych udostępnionych do mniejszej liczby węzłów i wykonywanie zadań równolegle na każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="686f5-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data to a smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="686f5-109">Dotyczy to zwłaszcza, jeśli dane do skopiowania na każdym węźle muszą być przekazywane między regionów geograficznych.</span><span class="sxs-lookup"><span data-stu-id="686f5-109">This especially applies if the data to be copied to each node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="686f5-110">**Maksymalizacja użycie pamięci** podczas zadania wymagają dużej ilości pamięci, ale tylko w krótkich okresach czasu i w czasie zmiennej podczas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="686f5-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="686f5-111">Można wdrożyć węzły obliczeniowe mniej, ale są większe, więcej pamięci do efektywnej obsługi tych wartości szczytowe.</span><span class="sxs-lookup"><span data-stu-id="686f5-111">You can employ fewer, but larger, compute nodes with more memory to efficiently handle such spikes.</span></span> <span data-ttu-id="686f5-112">Te węzły byłyby wielu zadań uruchomione równolegle w każdym węźle, ale każde zadanie będzie korzystać z tych węzłów dużej ilości pamięci w różnym czasie.</span><span class="sxs-lookup"><span data-stu-id="686f5-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of the nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="686f5-113">**Zmniejszenia limity numer węzła** podczas komunikacji między węzłami jest wymagana w puli.</span><span class="sxs-lookup"><span data-stu-id="686f5-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="686f5-114">Obecnie skonfigurowane do komunikacji między węzłami pule są ograniczone do 50 węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="686f5-114">Currently, pools configured for inter-node communication are limited to 50 compute nodes.</span></span> <span data-ttu-id="686f5-115">Jeśli każdy węzeł w takich puli jest w stanie wykonywać zadania równolegle, większa liczba zadań mogą być wykonywane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="686f5-115">If each node in such a pool is able to execute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="686f5-116">**Replikowanie lokalnych klastra obliczeniowego**, takie jak kiedy należy najpierw przenieść środowiska obliczeniowe na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="686f5-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment to Azure.</span></span> <span data-ttu-id="686f5-117">Jeśli lokalne rozwiązanie wykonuje wiele zadań na węzeł obliczeń, można zwiększyć maksymalną liczbę zadań węzła dokładniejsze dublowanego tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="686f5-117">If your current on-premises solution executes multiple tasks per compute node, you can increase the maximum number of node tasks to more closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="686f5-118">Przykładowy scenariusz</span><span class="sxs-lookup"><span data-stu-id="686f5-118">Example scenario</span></span>
<span data-ttu-id="686f5-119">Na przykład ilustrujący zalet wykonywanie zadań równoległych Załóżmy, że czy aplikacji zadanie ma wymagania dotyczące procesora CPU i pamięci tak, aby [standardowe\_D1](../cloud-services/cloud-services-sizes-specs.md) węzły są wystarczające.</span><span class="sxs-lookup"><span data-stu-id="686f5-119">As an example to illustrate the benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="686f5-120">Jednak, aby zakończyć zadanie w wymaganym czasie, 1000 te węzły są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="686f5-120">But, in order to finish the job in the required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="686f5-121">Zamiast standardowego\_D1 węzły, które mają 1 rdzeń procesora CPU, można użyć [standardowe\_D14](../cloud-services/cloud-services-sizes-specs.md) węzłów, które ma 16 rdzeni i włącz wykonywanie zadań równoległych.</span><span class="sxs-lookup"><span data-stu-id="686f5-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="686f5-122">W związku z tym *16 razy mniej węzłów* można użyć — zamiast 1000 węzłów tylko 63 będą wymagane.</span><span class="sxs-lookup"><span data-stu-id="686f5-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="686f5-123">Ponadto jeśli pliki dużych aplikacji lub dane referencyjne są wymagane dla każdego węzła, czas trwania zadania i wydajności ponownie zwiększona, ponieważ dane są kopiowane do węzłów tylko 16.</span><span class="sxs-lookup"><span data-stu-id="686f5-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since the data is copied to only 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="686f5-124">Włącz wykonywanie zadań równoległych</span><span class="sxs-lookup"><span data-stu-id="686f5-124">Enable parallel task execution</span></span>
<span data-ttu-id="686f5-125">Węzłami obliczeniowymi w celu wykonania zadań równoległych można skonfigurować na poziomie puli.</span><span class="sxs-lookup"><span data-stu-id="686f5-125">You configure compute nodes for parallel task execution at the pool level.</span></span> <span data-ttu-id="686f5-126">Z biblioteki partiami platformy .NET, należy ustawić [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] właściwość podczas tworzenia puli.</span><span class="sxs-lookup"><span data-stu-id="686f5-126">With the Batch .NET library, set the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="686f5-127">Jeśli korzystasz z interfejsu API REST partii, ustaw [maxTasksPerNode] [ rest_addpool] elementu w treści żądania podczas tworzenia puli.</span><span class="sxs-lookup"><span data-stu-id="686f5-127">If you are using the Batch REST API, set the [maxTasksPerNode][rest_addpool] element in the request body during pool creation.</span></span>

<span data-ttu-id="686f5-128">Partia zadań Azure umożliwia określenie maksymalnej zadań na węzeł maksymalnie cztery razy (4 x) liczba rdzeni węzła.</span><span class="sxs-lookup"><span data-stu-id="686f5-128">Azure Batch allows you to set maximum tasks per node up to four times (4x) the number of node cores.</span></span> <span data-ttu-id="686f5-129">Na przykład, jeśli pula jest skonfigurowana z węzłami z rozmiar "Duże" (4 rdzenie), następnie `maxTasksPerNode` ustawioną 16.</span><span class="sxs-lookup"><span data-stu-id="686f5-129">For example, if the pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set to 16.</span></span> <span data-ttu-id="686f5-130">Szczegółowe informacje dotyczące liczby rdzeni dla każdego węzła rozmiarów, zobacz [rozmiary dla usług w chmurze](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="686f5-130">For details on the number of cores for each of the node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="686f5-131">Aby uzyskać więcej informacji na ograniczenia usługi, zobacz [przydziały i limity dla usługi partia zadań Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="686f5-131">For more information on service limits, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="686f5-132">Należy wziąć pod uwagę `maxTasksPerNode` wartość utworzenia [formułą automatycznego skalowania] [ enable_autoscaling] dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="686f5-132">Be sure to take into account the `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="686f5-133">Na przykład formuła, której wynikiem `$RunningTasks` może mieć znaczący wpływ wzrost zadań na węzeł.</span><span class="sxs-lookup"><span data-stu-id="686f5-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="686f5-134">Zobacz [automatycznie skali obliczeniowe węzłów w puli partii zadań Azure](batch-automatic-scaling.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="686f5-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="686f5-135">Podział zadań</span><span class="sxs-lookup"><span data-stu-id="686f5-135">Distribution of tasks</span></span>
<span data-ttu-id="686f5-136">Węzły obliczeń w puli mogą jednocześnie wykonywać zadania, należy określić sposób zadań, które mają być dystrybuowane między węzłami w puli.</span><span class="sxs-lookup"><span data-stu-id="686f5-136">When the compute nodes in a pool can execute tasks concurrently, it's important to specify how you want the tasks to be distributed across the nodes in the pool.</span></span>

<span data-ttu-id="686f5-137">Za pomocą [CloudPool.TaskSchedulingPolicy] [ task_schedule] właściwości, można określić czy zadania powinien być przypisany równomiernie we wszystkich węzłach w puli ("rozpraszania").</span><span class="sxs-lookup"><span data-stu-id="686f5-137">By using the [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in the pool ("spreading").</span></span> <span data-ttu-id="686f5-138">Lub możesz określić, że jako liczbę zadań powinny zostać przypisane do każdego węzła przed zadania są przypisane do innego węzła w puli ("pakowania").</span><span class="sxs-lookup"><span data-stu-id="686f5-138">Or you can specify that as many tasks as possible should be assigned to each node before tasks are assigned to another node in the pool ("packing").</span></span>

<span data-ttu-id="686f5-139">Jako przykład sposobu ta funkcja jest przydatna, należy wziąć pod uwagę puli [standardowe\_D14](../cloud-services/cloud-services-sizes-specs.md) (w powyższym przykładzie) węzły, które są skonfigurowane przy użyciu [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] wartość 16.</span><span class="sxs-lookup"><span data-stu-id="686f5-139">As an example of how this feature is valuable, consider the pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in the example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="686f5-140">Jeśli [CloudPool.TaskSchedulingPolicy] [ task_schedule] skonfigurowano [ComputeNodeFillType] [ fill_type] z *pakietu*, czy zmaksymalizować użycie wszystkich rdzeni 16 każdego węzła i umożliwia [puli Skalowanie automatyczne](batch-automatic-scaling.md) Aby oczyścić nieużywane węzłów z puli (węzłów bez żadnych zadań przypisane).</span><span class="sxs-lookup"><span data-stu-id="686f5-140">If the [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) to prune unused nodes from the pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="686f5-141">Ten sposób można zmniejszyć obciążenie zasobów i zapisuje pieniędzy.</span><span class="sxs-lookup"><span data-stu-id="686f5-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="686f5-142">Przykład .NET partii</span><span class="sxs-lookup"><span data-stu-id="686f5-142">Batch .NET example</span></span>
<span data-ttu-id="686f5-143">To [partiami platformy .NET] [ api_net] interfejsu API fragment kodu przedstawia żądanie, aby utworzyć pulę zawierającą czterech węzłów dużych maksymalnie cztery zadania w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="686f5-143">This [Batch .NET][api_net] API code snippet shows a request to create a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="686f5-144">Określa zadanie planowania zasad, który zostanie wypełniony każdego węzła zadania przed przypisywanie zadań do innego węzła w puli.</span><span class="sxs-lookup"><span data-stu-id="686f5-144">It specifies a task scheduling policy that will fill each node with tasks prior to assigning tasks to another node in the pool.</span></span> <span data-ttu-id="686f5-145">Aby uzyskać więcej informacji o dodawaniu pule przy użyciu interfejsu API programu .NET partii, zobacz [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="686f5-145">For more information on adding pools by using the Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="686f5-146">Przykład REST partii</span><span class="sxs-lookup"><span data-stu-id="686f5-146">Batch REST example</span></span>
<span data-ttu-id="686f5-147">To [REST partii] [ api_rest] interfejsu API fragment kodu przedstawia żądanie, aby utworzyć pulę, która zawiera dwa węzły dużych maksymalnie cztery zadania w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="686f5-147">This [Batch REST][api_rest] API snippet shows a request to create a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="686f5-148">Aby uzyskać więcej informacji o dodawaniu pule przy użyciu interfejsu API REST, zobacz [Dodaj pulę, aby konto][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="686f5-148">For more information on adding pools by using the REST API, see [Add a pool to an account][rest_addpool].</span></span>

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
> <span data-ttu-id="686f5-149">Można ustawić `maxTasksPerNode` elementu i [MaxTasksPerComputeNode] [ maxtasks_net] właściwość tylko w czasie tworzenia puli.</span><span class="sxs-lookup"><span data-stu-id="686f5-149">You can set the `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="686f5-150">Nie można zmodyfikować po puli został już utworzony.</span><span class="sxs-lookup"><span data-stu-id="686f5-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="686f5-151">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="686f5-151">Code sample</span></span>
<span data-ttu-id="686f5-152">[ParallelNodeTasks] [ parallel_tasks_sample] projektu w witrynie GitHub ilustruje użycie [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] właściwości.</span><span class="sxs-lookup"><span data-stu-id="686f5-152">The [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates the use of the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="686f5-153">Korzysta z tej aplikacji konsolowej C# [partiami platformy .NET] [ api_net] biblioteki, aby utworzyć pulę z co najmniej jednym węźle obliczeń.</span><span class="sxs-lookup"><span data-stu-id="686f5-153">This C# console application uses the [Batch .NET][api_net] library to create a pool with one or more compute nodes.</span></span> <span data-ttu-id="686f5-154">Można skonfigurować wiele zadań jest wykonywana na tych węzłach, aby symulować zmiennej obciążenia.</span><span class="sxs-lookup"><span data-stu-id="686f5-154">It executes a configurable number of tasks on those nodes to simulate variable load.</span></span> <span data-ttu-id="686f5-155">Dane wyjściowe aplikacji Określa węzły, które wykonywane każdego zadania.</span><span class="sxs-lookup"><span data-stu-id="686f5-155">Output from the application specifies which nodes executed each task.</span></span> <span data-ttu-id="686f5-156">Aplikacja jest także podsumowanie parametrów zadania i czas trwania.</span><span class="sxs-lookup"><span data-stu-id="686f5-156">The application also provides a summary of the job parameters and duration.</span></span> <span data-ttu-id="686f5-157">Podsumowanie część dane wyjściowe z dwóch różnych uruchomień przykładowej aplikacji pojawia się poniżej.</span><span class="sxs-lookup"><span data-stu-id="686f5-157">The summary portion of the output from two different runs of the sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="686f5-158">Pierwszy wykonywanie przykładowej aplikacji wskazuje, że z jednego węzła w puli i ustawieniem domyślnym jednego zadania w każdym węźle, czas trwania zadania jest ponad 30 minut.</span><span class="sxs-lookup"><span data-stu-id="686f5-158">The first execution of the sample application shows that with a single node in the pool and the default setting of one task per node, the job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="686f5-159">Drugi uruchomienie przedstawiono przykładowe znaczny spadek czas trwania zadania.</span><span class="sxs-lookup"><span data-stu-id="686f5-159">The second run of the sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="686f5-160">Jest to spowodowane puli został skonfigurowany z czterech zadań na węzeł, który pozwala na ukończenie zadania w niemal kwartału czasu wykonywania zadań równoległych.</span><span class="sxs-lookup"><span data-stu-id="686f5-160">This is because the pool was configured with four tasks per node, which allows for parallel task execution to complete the job in nearly a quarter of the time.</span></span>

> [!NOTE]
> <span data-ttu-id="686f5-161">Czas trwania zadania w powyższym podsumowania nie dołączaj czas utworzenia puli.</span><span class="sxs-lookup"><span data-stu-id="686f5-161">The job durations in the summaries above do not include pool creation time.</span></span> <span data-ttu-id="686f5-162">Każdy z powyższych zadania zostało przesłane do utworzonej wcześniej pule, którego węzły obliczeniowe były w *bezczynny* stanu w czasie przesyłania.</span><span class="sxs-lookup"><span data-stu-id="686f5-162">Each of the jobs above was submitted to previously created pools whose compute nodes were in the *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="686f5-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="686f5-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="686f5-164">Mapa cieplna Explorer partii</span><span class="sxs-lookup"><span data-stu-id="686f5-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="686f5-165">[Eksploratora usługi partia zadań Azure][batch_explorer], jeden z partii zadań Azure [przykładowe aplikacje][github_samples], zawiera *Mapa cieplna* funkcja, która umożliwia wizualizację wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="686f5-165">The [Azure Batch Explorer][batch_explorer], one of the Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="686f5-166">Jeśli w przypadku wykonywania [ParallelTasks] [ parallel_tasks_sample] przykładowej aplikacji, można użyć funkcji Mapa cieplna można łatwo przedstawić wizualnie wykonywanie zadań równoległych w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="686f5-166">When you're executing the [ParallelTasks][parallel_tasks_sample] sample application, you can use the Heat Map feature to easily visualize the execution of parallel tasks on each node.</span></span>

![Mapa cieplna Explorer partii][1]

<span data-ttu-id="686f5-168">*Mapa cieplna Explorer partii przedstawiający puli czterech węzłów z każdego węzła aktualnie wykonywanych zadań cztery*</span><span class="sxs-lookup"><span data-stu-id="686f5-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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
