---
title: "Użyj zależności zadań do uruchomienia zadania po zakończeniu innych zadań — partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Utwórz zadania, które są zależne od ukończenia innych zadań przetwarzania stylu MapReduce i podobnych danych big data obciążeń w partii zadań Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 465306d2de8d1dbe6ba1f0cd74be720b78a50de3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-task-dependencies-to-run-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="d9dda-103">Tworzenie zależności zadań do wykonywania zadań, które są zależne od innych zadań</span><span class="sxs-lookup"><span data-stu-id="d9dda-103">Create task dependencies to run tasks that depend on other tasks</span></span>

<span data-ttu-id="d9dda-104">Można określić zależności zadań do uruchomienia zadania lub zestawu zadań dopiero po zakończeniu zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d9dda-104">You can define task dependencies to run a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="d9dda-105">Sytuacje, w którym zależności zadań są przydatne obejmują:</span><span class="sxs-lookup"><span data-stu-id="d9dda-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="d9dda-106">Styl MapReduce obciążeń w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d9dda-106">MapReduce-style workloads in the cloud.</span></span>
* <span data-ttu-id="d9dda-107">Zadania, których zadania przetwarzania danych może zostać wyrażona jako ukierunkowanego wykresu acyklicznego (DAG).</span><span class="sxs-lookup"><span data-stu-id="d9dda-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="d9dda-108">Procesy renderowania wstępnego i renderowania po, gdzie każde zadanie należy wykonać przed rozpoczęciem następnego zadania.</span><span class="sxs-lookup"><span data-stu-id="d9dda-108">Pre-rendering and post-rendering processes, where each task must complete before the next task can begin.</span></span>
* <span data-ttu-id="d9dda-109">Inne zadanie w którym zadania podrzędne są zależne od dane wyjściowe zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d9dda-109">Any other job in which downstream tasks depend on the output of upstream tasks.</span></span>

<span data-ttu-id="d9dda-110">Zależności zadań wsadowych umożliwia tworzenie zadań, które są zaplanowane do uruchomienia na węzły obliczeniowe po zakończeniu jednego lub więcej zadań nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="d9dda-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after the completion of one or more parent tasks.</span></span> <span data-ttu-id="d9dda-111">Na przykład można utworzyć zadania, który renderuje każdej ramce 3D film z oddzielnych zadań równoległych.</span><span class="sxs-lookup"><span data-stu-id="d9dda-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="d9dda-112">Ostatni zadań — "merge zadanie"--scaleń renderowanych ramki do ukończenia filmu tylko wtedy, gdy wszystkie ramki zostały pomyślnie renderowane.</span><span class="sxs-lookup"><span data-stu-id="d9dda-112">The final task--the "merge task"--merges the rendered frames into the complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="d9dda-113">Domyślnie zadania zależne są zaplanowane do uruchomienia, dopiero po pomyślnym zakończeniu zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d9dda-113">By default, dependent tasks are scheduled for execution only after the parent task has completed successfully.</span></span> <span data-ttu-id="d9dda-114">Można określić akcję zależności, aby zastąpić domyślne zachowanie i uruchamianie zadań, gdy zadanie nadrzędne nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="d9dda-114">You can specify a dependency action to override the default behavior and run tasks when the parent task fails.</span></span> <span data-ttu-id="d9dda-115">Zobacz [akcje zależności](#dependency-actions) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d9dda-115">See the [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="d9dda-116">Można tworzyć zadania, które są zależne od innych zadań w relacji jeden do jednego lub jeden do wielu.</span><span class="sxs-lookup"><span data-stu-id="d9dda-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="d9dda-117">Można również utworzyć zależność zakresu, gdzie zadania zależy od zakończenia grupy zadań w określonym zakresie identyfikatorów zadań.</span><span class="sxs-lookup"><span data-stu-id="d9dda-117">You can also create a range dependency where a task depends on the completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="d9dda-118">Można połączyć te trzy podstawowe scenariusze do tworzenia relacji wiele do wielu.</span><span class="sxs-lookup"><span data-stu-id="d9dda-118">You can combine these three basic scenarios to create many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="d9dda-119">Zależności zadań z partiami platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d9dda-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="d9dda-120">W tym artykule omówiono sposób konfigurowania zależności zadań za pomocą [partiami platformy .NET] [ net_msdn] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="d9dda-120">In this article, we discuss how to configure task dependencies by using the [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="d9dda-121">Możemy najpierw przedstawia sposób do [włączyć zależności zadań](#enable-task-dependencies) na zadaniach, a następnie pokazują, jak [skonfigurować zadania z zależnościami](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="d9dda-121">We first show you how to [enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how to [configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="d9dda-122">Opisano również sposób określić akcję zależności do uruchomienia zadania zależne, jeśli element nadrzędny nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="d9dda-122">We also describe how to specify a dependency action to run dependent tasks if the parent fails.</span></span> <span data-ttu-id="d9dda-123">Ponadto omówiono [scenariusze zależności](#dependency-scenarios) obsługującego partii.</span><span class="sxs-lookup"><span data-stu-id="d9dda-123">Finally, we discuss the [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="d9dda-124">Włącz zależności zadań</span><span class="sxs-lookup"><span data-stu-id="d9dda-124">Enable task dependencies</span></span>
<span data-ttu-id="d9dda-125">Aby użyć zależności zadań w partii aplikacji, najpierw należy skonfigurować zadania do użycia zależności zadań.</span><span class="sxs-lookup"><span data-stu-id="d9dda-125">To use task dependencies in your Batch application, you must first configure the job to use task dependencies.</span></span> <span data-ttu-id="d9dda-126">W partiami platformy .NET, należy włączyć ją w Twojej [CloudJob] [ net_cloudjob] przez ustawienie jej [UsesTaskDependencies] [ net_usestaskdependencies] właściwości `true`:</span><span class="sxs-lookup"><span data-stu-id="d9dda-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property to `true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="d9dda-127">W poprzednim fragmencie kodu, "batchClient" jest wystąpieniem [BatchClient] [ net_batchclient] klasy.</span><span class="sxs-lookup"><span data-stu-id="d9dda-127">In the preceding code snippet, "batchClient" is an instance of the [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="d9dda-128">Utwórz zadania zależne</span><span class="sxs-lookup"><span data-stu-id="d9dda-128">Create dependent tasks</span></span>
<span data-ttu-id="d9dda-129">Aby utworzyć zadanie, które jest zależna od zakończenia jednego lub więcej zadań nadrzędnej, można określić, że zadanie "zależy od" innych zadań.</span><span class="sxs-lookup"><span data-stu-id="d9dda-129">To create a task that depends on the completion of one or more parent tasks, you can specify that the task "depends on" the other tasks.</span></span> <span data-ttu-id="d9dda-130">W partiami platformy .NET, należy skonfigurować [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] właściwości z wystąpieniem [TaskDependencies] [ net_taskdependencies] klasy:</span><span class="sxs-lookup"><span data-stu-id="d9dda-130">In Batch .NET, configure the [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of the [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="d9dda-131">Następujący fragment kodu tworzy zależnego zadania o identyfikatorze zadania "Kwiaty".</span><span class="sxs-lookup"><span data-stu-id="d9dda-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="d9dda-132">Zadanie "Kwiaty" zależy od zadania "Ustaniu" i "Sun".</span><span class="sxs-lookup"><span data-stu-id="d9dda-132">The "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="d9dda-133">Zadanie "kwiaty" zostanie zaplanowane do uruchomienia w węźle obliczeń tylko po zadań, które "Ustaniu" i "Sun" została ukończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="d9dda-133">Task "Flowers" will be scheduled to run on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="d9dda-134">Zadanie jest uznawany za zostanie ukończona pomyślnie, gdy jest on w **ukończone** stanu i jego **kod zakończenia** jest `0`.</span><span class="sxs-lookup"><span data-stu-id="d9dda-134">A task is considered to be completed successfully when it is in the **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="d9dda-135">W partiami platformy .NET, oznacza to [CloudTask][net_cloudtask].[ Stan] [ net_taskstate] wartość właściwości `Completed` i CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] wartość właściwości jest `0`.</span><span class="sxs-lookup"><span data-stu-id="d9dda-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and the CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="d9dda-136">Scenariusze zależności</span><span class="sxs-lookup"><span data-stu-id="d9dda-136">Dependency scenarios</span></span>
<span data-ttu-id="d9dda-137">Istnieją trzy scenariusze zależności podstawowe zadania, których można używać w partii zadań Azure: jeden do jednego, jeden do wielu, a zadania o identyfikatorze zakresu zależności.</span><span class="sxs-lookup"><span data-stu-id="d9dda-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="d9dda-138">Te można łączyć zapewnienie scenariusza czwarty wiele do wielu.</span><span class="sxs-lookup"><span data-stu-id="d9dda-138">These can be combined to provide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="d9dda-139">Scenariusz&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="d9dda-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="d9dda-140">Przykład</span><span class="sxs-lookup"><span data-stu-id="d9dda-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="d9dda-141">Jeden do jednego</span><span class="sxs-lookup"><span data-stu-id="d9dda-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="d9dda-142">*taskB* zależy od *taskA*</span><span class="sxs-lookup"><span data-stu-id="d9dda-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="d9dda-143">*taskB* nie będzie można zaplanować wykonywanie do momentu *taskA* zostało ukończone pomyślnie</span><span class="sxs-lookup"><span data-stu-id="d9dda-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="d9dda-144">![Diagram: jeden do jednego zadania zależności][1]</span><span class="sxs-lookup"><span data-stu-id="d9dda-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="d9dda-145">Jeden do wielu</span><span class="sxs-lookup"><span data-stu-id="d9dda-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="d9dda-146">*zadanieC* zależy od *zadaniaA* i *zadaniaB*</span><span class="sxs-lookup"><span data-stu-id="d9dda-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="d9dda-147">*taskC* nie zostanie zaplanowane do wykonania przed zakończeniem *taskA* i *taskB* zostały ukończone pomyślnie</span><span class="sxs-lookup"><span data-stu-id="d9dda-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="d9dda-148">![Diagram: jeden do wielu zadań zależności][2]</span><span class="sxs-lookup"><span data-stu-id="d9dda-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="d9dda-149">Zakres identyfikator zadania</span><span class="sxs-lookup"><span data-stu-id="d9dda-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="d9dda-150">*taskD* zależy od zakresu zadań</span><span class="sxs-lookup"><span data-stu-id="d9dda-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="d9dda-151">*taskD* nie będzie można zaplanowane do uruchomienia aż do zadań z identyfikatorami *1* za pośrednictwem *10* zostały ukończone pomyślnie</span><span class="sxs-lookup"><span data-stu-id="d9dda-151">*taskD* will not be scheduled for execution until the tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="d9dda-152">![Diagram: Zadanie identyfikator zakresu zależności][3]</span><span class="sxs-lookup"><span data-stu-id="d9dda-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="d9dda-153">Można utworzyć **wiele do wielu** relacje, np. gdy zadania C, D E i F każdego zależą od zadania, A i B. Jest to przydatne, na przykład w zrównoleglone przetwarzania wstępnego scenariuszach, w którym zadania podrzędne są zależne od danych wyjściowych wielu zadań nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d9dda-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on the output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="d9dda-154">W przykładach w tej sekcji zależne zadanie jest uruchamiane tylko wtedy, gdy pomyślnego wykonania zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d9dda-154">In the examples in this section, a dependent task runs only after the parent tasks complete successfully.</span></span> <span data-ttu-id="d9dda-155">To zachowanie jest domyślne zachowanie dla zadania zależne.</span><span class="sxs-lookup"><span data-stu-id="d9dda-155">This behavior is the default behavior for a dependent task.</span></span> <span data-ttu-id="d9dda-156">Po niepowodzeniu zadaniem nadrzędnym, określając akcji zależności, aby zastąpić zachowanie domyślne można uruchomić zadanie zależne.</span><span class="sxs-lookup"><span data-stu-id="d9dda-156">You can run a dependent task after a parent task fails by specifying a dependency action to override the default behavior.</span></span> <span data-ttu-id="d9dda-157">Zobacz [akcje zależności](#dependency-actions) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d9dda-157">See the [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="d9dda-158">Jeden do jednego</span><span class="sxs-lookup"><span data-stu-id="d9dda-158">One-to-one</span></span>
<span data-ttu-id="d9dda-159">W relacji jeden do jednego zadania zależy od pomyślne zakończenie zadania jednego zdarzenia nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d9dda-159">In a one-to-one relationship, a task depends on the successful completion of one parent task.</span></span> <span data-ttu-id="d9dda-160">Aby utworzyć zależność, podaj identyfikator pojedyncze zadanie [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] metody statycznej podczas wypełniania [DependsOn] [ net_dependson] właściwość [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="d9dda-160">To create the dependency, provide a single task ID to the [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="d9dda-161">Jeden do wielu</span><span class="sxs-lookup"><span data-stu-id="d9dda-161">One-to-many</span></span>
<span data-ttu-id="d9dda-162">W relacji jeden do wielu zadania zależy od ukończenia wielu zadań nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="d9dda-162">In a one-to-many relationship, a task depends on the completion of multiple parent tasks.</span></span> <span data-ttu-id="d9dda-163">Aby utworzyć zależność, przedstawiają kolekcję zadań identyfikatorów [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] metody statycznej podczas wypełniania [DependsOn] [ net_dependson] właściwość [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="d9dda-163">To create the dependency, provide a collection of task IDs to the [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a><span data-ttu-id="d9dda-164">Zakres identyfikator zadania</span><span class="sxs-lookup"><span data-stu-id="d9dda-164">Task ID range</span></span>
<span data-ttu-id="d9dda-165">Zależność od zakresu nadrzędnego zadania, zadania zależy od zakończenia zadania, których identyfikatory znajdują się w zakresie.</span><span class="sxs-lookup"><span data-stu-id="d9dda-165">In a dependency on a range of parent tasks, a task depends on the the completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="d9dda-166">Aby utworzyć zależność, podaj pierwszy i ostatni identyfikatorów zadań w zakresie do [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] metody statycznej podczas wypełniania [DependsOn] [ net_dependson] właściwość [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="d9dda-166">To create the dependency, provide the first and last task IDs in the range to the [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9dda-167">Jeśli używasz zakresy identyfikatorów zadań dla zależności, identyfikatorów zadań w zakresie *musi* być liczbami w postaci ciągu wartości będące liczbami całkowitymi.</span><span class="sxs-lookup"><span data-stu-id="d9dda-167">When you use task ID ranges for your dependencies, the task IDs in the range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="d9dda-168">Każde zadanie w zakresie muszą spełniać zależności, wykonując pomyślnie lub wykonując z błąd, który jest mapowany na akcję zależności ustawioną **Satisfy**.</span><span class="sxs-lookup"><span data-stu-id="d9dda-168">Every task in the range must satisfy the dependency, either by completing successfully or by completing with a failure that’s mapped to a dependency action set to **Satisfy**.</span></span> <span data-ttu-id="d9dda-169">Zobacz [akcje zależności](#dependency-actions) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d9dda-169">See the [Dependency actions](#dependency-actions) section for details.</span></span>
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // To use a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters to TaskIdRange,
    // but their ids (above) are string representations of the ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="d9dda-170">Akcje zależności</span><span class="sxs-lookup"><span data-stu-id="d9dda-170">Dependency actions</span></span>

<span data-ttu-id="d9dda-171">Domyślnie zadanie zależne lub zestawu zadań działa tylko po pomyślnym zakończeniu zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d9dda-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="d9dda-172">W niektórych scenariuszach może być uruchomienie zadania zależne, nawet jeśli zadaniem nadrzędnym nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="d9dda-172">In some scenarios, you may want to run dependent tasks even if the parent task fails.</span></span> <span data-ttu-id="d9dda-173">Domyślne zachowanie można zastąpić, określając akcji zależności.</span><span class="sxs-lookup"><span data-stu-id="d9dda-173">You can override the default behavior by specifying a dependency action.</span></span> <span data-ttu-id="d9dda-174">Akcja zależności Określa, czy zadanie zależne mogą być uruchamiane, oparte na powodzenie lub niepowodzenie zadaniem nadrzędnym.</span><span class="sxs-lookup"><span data-stu-id="d9dda-174">A dependency action specifies whether a dependent task is eligible to run, based on the success or failure of the parent task.</span></span> 

<span data-ttu-id="d9dda-175">Na przykład załóżmy, że zadanie zależne oczekuje na dane z ukończenia zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d9dda-175">For example, suppose that a dependent task is awaiting data from the completion of the upstream task.</span></span> <span data-ttu-id="d9dda-176">Jeśli poprzednie zadanie nie powiedzie się, zadanie zależne nadal można uruchomić przy użyciu starszych danych.</span><span class="sxs-lookup"><span data-stu-id="d9dda-176">If the upstream task fails, the dependent task may still be able to run using older data.</span></span> <span data-ttu-id="d9dda-177">W takim przypadku akcji zależności można określić, że zadanie zależne jest uprawniona do uruchamiania niezależnie od awarii zadaniem nadrzędnym.</span><span class="sxs-lookup"><span data-stu-id="d9dda-177">In this case, a dependency action can specify that the dependent task is eligible to run despite the failure of the parent task.</span></span>

<span data-ttu-id="d9dda-178">Akcja zależności jest oparta na warunku wyjścia dla zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d9dda-178">A dependency action is based on an exit condition for the parent task.</span></span> <span data-ttu-id="d9dda-179">Można określić akcję zależności dla żadnej z następujących warunków zakończenia; dla platformy .NET, zobacz [ExitConditions] [ net_exitconditions] klasy, aby uzyskać szczegółowe informacje:</span><span class="sxs-lookup"><span data-stu-id="d9dda-179">You can specify a dependency action for any of the following exit conditions; for .NET, see the [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="d9dda-180">Po wystąpieniu błędu przetwarzania wstępnego.</span><span class="sxs-lookup"><span data-stu-id="d9dda-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="d9dda-181">Po wystąpieniu błędu przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="d9dda-181">When a file upload error occurs.</span></span> <span data-ttu-id="d9dda-182">Jeśli zadanie kończy działanie z kodem zakończenia, która została określona za pomocą **exitCodes** lub **exitCodeRanges**, a następnie pierwszeństwo napotka błąd, akcji określonej przez kod zakończenia przekazywania pliku.</span><span class="sxs-lookup"><span data-stu-id="d9dda-182">If the task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, the action specified by the exit code takes precedence.</span></span>
- <span data-ttu-id="d9dda-183">Gdy zadanie kończy działanie z kodem zakończenia zdefiniowanych przez **ExitCodes** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d9dda-183">When the task exits with an exit code defined by the **ExitCodes** property.</span></span>
- <span data-ttu-id="d9dda-184">Gdy zadanie kończy działanie z kodem zakończenia, która wykracza poza zakres określony przez **ExitCodeRanges** właściwości.</span><span class="sxs-lookup"><span data-stu-id="d9dda-184">When the task exits with an exit code that falls within a range specified by the **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="d9dda-185">W przypadku domyślnej, jeśli zadanie kończy działanie z kodem zakończenia nie jest zdefiniowany przez **ExitCodes** lub **ExitCodeRanges**, lub jeśli zadanie kończy działanie z błędem przetwarzania wstępnego i **PreProcessingError** właściwość nie jest ustawiona, lub jeśli zadanie nie powiedzie się z plikiem błąd przekazywania i **FileUploadError** nie ustawiono właściwości.</span><span class="sxs-lookup"><span data-stu-id="d9dda-185">The default case, if the task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if the task exits with a pre-processing error and the **PreProcessingError** property is not set, or if the task fails with a file upload error and the **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="d9dda-186">Aby określić akcję zależności w programie .NET, należy ustawić [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] właściwości warunku exit.</span><span class="sxs-lookup"><span data-stu-id="d9dda-186">To specify a dependency action in .NET, set the [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for the exit condition.</span></span> <span data-ttu-id="d9dda-187">**DependencyAction** właściwość przyjmuje jeden z dwóch wartości:</span><span class="sxs-lookup"><span data-stu-id="d9dda-187">The **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="d9dda-188">Ustawienie **DependencyAction** właściwości **Satisfy** wskazuje, czy zadania zależne kwalifikują się do uruchomienia, jeśli zadaniem nadrzędnym kończy działanie z powodu określonego błędu.</span><span class="sxs-lookup"><span data-stu-id="d9dda-188">Setting the **DependencyAction** property to **Satisfy** indicates that dependent tasks are eligible to run if the parent task exits with a specified error.</span></span>
- <span data-ttu-id="d9dda-189">Ustawienie **DependencyAction** właściwości **bloku** wskazuje, czy zadania zależne nie będą kwalifikowały się do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="d9dda-189">Setting the **DependencyAction** property to **Block** indicates that dependent tasks are not eligible to run.</span></span>

<span data-ttu-id="d9dda-190">Ustawieniem domyślnym dla **DependencyAction** właściwość jest **Satisfy** dla kod zakończenia 0, a **bloku** dla wszystkich innych warunków zakończenia.</span><span class="sxs-lookup"><span data-stu-id="d9dda-190">The default setting for the **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="d9dda-191">Poniższy kod ustawia fragment **DependencyAction** właściwości dla zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="d9dda-191">The following code snippet sets the **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="d9dda-192">Jeśli zadaniem nadrzędnym kończy działanie z błędem przetwarzania wstępnego lub z kodami określonego błędu zależnego zadania jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="d9dda-192">If the parent task exits with a pre-processing error, or with the specified error codes, the dependent task is blocked.</span></span> <span data-ttu-id="d9dda-193">Jeśli zadaniem nadrzędnym kończy działanie z inny błąd inną niż zero, zadanie zależne nie kwalifikuje się do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="d9dda-193">If the parent task exits with any other non-zero error, the dependent task is eligible to run.</span></span>

```csharp
// Task A is the parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with the specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible to run 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible to run depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="d9dda-194">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="d9dda-194">Code sample</span></span>
<span data-ttu-id="d9dda-195">[TaskDependencies] [ github_taskdependencies] przykładowy projekt jest jednym z [przykłady kodu partii zadań Azure] [ github_samples] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="d9dda-195">The [TaskDependencies][github_taskdependencies] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="d9dda-196">Przedstawiono to rozwiązanie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="d9dda-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="d9dda-197">Jak włączyć zadania zależności w zadaniu</span><span class="sxs-lookup"><span data-stu-id="d9dda-197">How to enable task dependency on a job</span></span>
- <span data-ttu-id="d9dda-198">Tworzenie zadań, które są zależne od innych zadań</span><span class="sxs-lookup"><span data-stu-id="d9dda-198">How to create tasks that depend on other tasks</span></span>
- <span data-ttu-id="d9dda-199">Jak wykonać te zadania w puli węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="d9dda-199">How to execute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9dda-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9dda-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="d9dda-201">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="d9dda-201">Application deployment</span></span>
<span data-ttu-id="d9dda-202">[Pakietów aplikacji](batch-application-packages.md) funkcji partii zapewnia prosty sposób zarówno, jak wdrożyć i wersja aplikacji, które wykonania zadań na węzłach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="d9dda-202">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="d9dda-203">Instalowanie aplikacji i danych na potrzeby przemieszczania</span><span class="sxs-lookup"><span data-stu-id="d9dda-203">Installing applications and staging data</span></span>
<span data-ttu-id="d9dda-204">Zobacz [instalowania aplikacji i danych na partii przemieszczania węzły obliczeniowe] [ forum_post] na forum usługi partia zadań Azure Omówienie metody przygotowania węzły do uruchamiania zadań.</span><span class="sxs-lookup"><span data-stu-id="d9dda-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in the Azure Batch forum for an overview of methods for preparing your nodes to run tasks.</span></span> <span data-ttu-id="d9dda-205">Napisane przez jeden z członków zespołu partii zadań Azure, ten wpis jest dobrym Elementarz na różne sposoby, aby skopiować aplikacje, dane wejściowe zadania i inne pliki do węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="d9dda-205">Written by one of the Azure Batch team members, this post is a good primer on the different ways to copy applications, task input data, and other files to your compute nodes.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

<span data-ttu-id="d9dda-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: jeden do jednego zależności"</span><span class="sxs-lookup"><span data-stu-id="d9dda-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: one-to-one dependency"</span></span>
<span data-ttu-id="d9dda-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: jeden do wielu zależności"</span><span class="sxs-lookup"><span data-stu-id="d9dda-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: one-to-many dependency"</span></span>
<span data-ttu-id="d9dda-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: zadanie identyfikator zakresu zależności"</span><span class="sxs-lookup"><span data-stu-id="d9dda-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: task id range dependency"</span></span>
