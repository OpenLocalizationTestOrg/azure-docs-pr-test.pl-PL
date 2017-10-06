---
title: "Po zakończeniu hello innych zadań — partii zadań Azure na podstawie aaaUse zadanie zależności toorun zadania | Dokumentacja firmy Microsoft"
description: "Utwórz zadania, które są zależne od ukończenia hello innych zadań przetwarzania stylu MapReduce i podobnych danych big data obciążeń w partii zadań Azure."
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
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="e4d75-103">Tworzenie zadań zależności toorun zadania, które są zależne od innych zadań</span><span class="sxs-lookup"><span data-stu-id="e4d75-103">Create task dependencies toorun tasks that depend on other tasks</span></span>

<span data-ttu-id="e4d75-104">Toorun zależności zadań można zdefiniować zadania lub zestawu zadań dopiero po zakończeniu zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="e4d75-104">You can define task dependencies toorun a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="e4d75-105">Sytuacje, w którym zależności zadań są przydatne obejmują:</span><span class="sxs-lookup"><span data-stu-id="e4d75-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="e4d75-106">Styl MapReduce obciążeń w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="e4d75-106">MapReduce-style workloads in hello cloud.</span></span>
* <span data-ttu-id="e4d75-107">Zadania, których zadania przetwarzania danych może zostać wyrażona jako ukierunkowanego wykresu acyklicznego (DAG).</span><span class="sxs-lookup"><span data-stu-id="e4d75-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="e4d75-108">Procesy renderowania wstępnego i renderowania po, gdzie każde zadanie należy wykonać przed rozpoczęciem powitalne następne zadanie.</span><span class="sxs-lookup"><span data-stu-id="e4d75-108">Pre-rendering and post-rendering processes, where each task must complete before hello next task can begin.</span></span>
* <span data-ttu-id="e4d75-109">Inne zadanie w którym zadania podrzędne są zależne od hello dane wyjściowe zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="e4d75-109">Any other job in which downstream tasks depend on hello output of upstream tasks.</span></span>

<span data-ttu-id="e4d75-110">Zależności zadań wsadowych umożliwia tworzenie zadań, które są zaplanowane do uruchomienia na węzły obliczeniowe po zakończeniu hello jednego lub więcej zadań nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="e4d75-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after hello completion of one or more parent tasks.</span></span> <span data-ttu-id="e4d75-111">Na przykład można utworzyć zadania, który renderuje każdej ramce 3D film z oddzielnych zadań równoległych.</span><span class="sxs-lookup"><span data-stu-id="e4d75-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="e4d75-112">ostatnim zadaniem Hello — Witaj "scalania zadania"--scaleń hello renderowane ramek na powitania tylko cały film po wszystkich ramki pomyślnie nadano.</span><span class="sxs-lookup"><span data-stu-id="e4d75-112">hello final task--hello "merge task"--merges hello rendered frames into hello complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="e4d75-113">Dopiero po pomyślnym zakończeniu zadania nadrzędnego hello zadania zależne są domyślnie zaplanowane do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="e4d75-113">By default, dependent tasks are scheduled for execution only after hello parent task has completed successfully.</span></span> <span data-ttu-id="e4d75-114">Można określić zachowanie domyślne hello toooverride akcji zależności i uruchamianie zadań, gdy zadanie nadrzędne hello nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="e4d75-114">You can specify a dependency action toooverride hello default behavior and run tasks when hello parent task fails.</span></span> <span data-ttu-id="e4d75-115">Zobacz hello [akcje zależności](#dependency-actions) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="e4d75-115">See hello [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="e4d75-116">Można tworzyć zadania, które są zależne od innych zadań w relacji jeden do jednego lub jeden do wielu.</span><span class="sxs-lookup"><span data-stu-id="e4d75-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="e4d75-117">Można również utworzyć zależność zakresu, gdzie zadania zależy od ukończenia hello grupy zadań w ramach określonego zakresu identyfikatorów zadań.</span><span class="sxs-lookup"><span data-stu-id="e4d75-117">You can also create a range dependency where a task depends on hello completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="e4d75-118">Można połączyć te trzy relacje wiele do wielu toocreate scenariuszy podstawowych.</span><span class="sxs-lookup"><span data-stu-id="e4d75-118">You can combine these three basic scenarios toocreate many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="e4d75-119">Zależności zadań z partiami platformy .NET</span><span class="sxs-lookup"><span data-stu-id="e4d75-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="e4d75-120">W tym artykule omówiono sposób hello tooconfigure zależności zadań za pomocą [partiami platformy .NET] [ net_msdn] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="e4d75-120">In this article, we discuss how tooconfigure task dependencies by using hello [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="e4d75-121">Firma Microsoft najpierw dowiesz się, jak za[włączyć współzależności](#enable-task-dependencies) na zadaniach i pokazują, jak za[skonfigurować zadania z zależnościami](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="e4d75-121">We first show you how too[enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how too[configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="e4d75-122">Również opisać jak toospecify zależności akcji toorun zadań zależnych Jeśli hello nadrzędnego nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="e4d75-122">We also describe how toospecify a dependency action toorun dependent tasks if hello parent fails.</span></span> <span data-ttu-id="e4d75-123">Ponadto omówiono hello [scenariusze zależności](#dependency-scenarios) obsługującego partii.</span><span class="sxs-lookup"><span data-stu-id="e4d75-123">Finally, we discuss hello [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="e4d75-124">Włącz zależności zadań</span><span class="sxs-lookup"><span data-stu-id="e4d75-124">Enable task dependencies</span></span>
<span data-ttu-id="e4d75-125">zależności zadań toouse w partii aplikacji, należy najpierw skonfigurować hello zadania toouse zadań zależności.</span><span class="sxs-lookup"><span data-stu-id="e4d75-125">toouse task dependencies in your Batch application, you must first configure hello job toouse task dependencies.</span></span> <span data-ttu-id="e4d75-126">W partiami platformy .NET, należy włączyć ją w Twojej [CloudJob] [ net_cloudjob] przez ustawienie jej [UsesTaskDependencies] [ net_usestaskdependencies] właściwości zbyt`true`:</span><span class="sxs-lookup"><span data-stu-id="e4d75-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property too`true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="e4d75-127">W hello poprzedzających fragment kodu, "batchClient" jest wystąpieniem hello [BatchClient] [ net_batchclient] klasy.</span><span class="sxs-lookup"><span data-stu-id="e4d75-127">In hello preceding code snippet, "batchClient" is an instance of hello [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="e4d75-128">Utwórz zadania zależne</span><span class="sxs-lookup"><span data-stu-id="e4d75-128">Create dependent tasks</span></span>
<span data-ttu-id="e4d75-129">toocreate zadanie, które jest zależna od zakończenia hello jednego lub więcej zadań nadrzędnej, można określić które hello zadania "zależy od" hello innych zadań.</span><span class="sxs-lookup"><span data-stu-id="e4d75-129">toocreate a task that depends on hello completion of one or more parent tasks, you can specify that hello task "depends on" hello other tasks.</span></span> <span data-ttu-id="e4d75-130">W partiami platformy .NET, należy skonfigurować hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] właściwości z wystąpieniem hello [TaskDependencies] [ net_taskdependencies] klasy:</span><span class="sxs-lookup"><span data-stu-id="e4d75-130">In Batch .NET, configure hello [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of hello [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="e4d75-131">Następujący fragment kodu tworzy zależnego zadania o identyfikatorze zadania "Kwiaty".</span><span class="sxs-lookup"><span data-stu-id="e4d75-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="e4d75-132">Witaj "Kwiaty" zadań zależy od zadania "Ustaniu" i "Sun".</span><span class="sxs-lookup"><span data-stu-id="e4d75-132">hello "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="e4d75-133">Zadanie "Kwiaty" będzie zaplanowane toorun w węźle obliczeń tylko po zadań, które "Ustaniu" i "Sun" została ukończona pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="e4d75-133">Task "Flowers" will be scheduled toorun on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="e4d75-134">Zadanie jest uznawany za toobe ukończona pomyślnie, gdy będzie hello **ukończone** stanu i jego **kod zakończenia** jest `0`.</span><span class="sxs-lookup"><span data-stu-id="e4d75-134">A task is considered toobe completed successfully when it is in hello **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="e4d75-135">W partiami platformy .NET, oznacza to [CloudTask][net_cloudtask].[ Stan] [ net_taskstate] wartość właściwości `Completed` i hello w CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] wartość właściwości jest `0`.</span><span class="sxs-lookup"><span data-stu-id="e4d75-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and hello CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="e4d75-136">Scenariusze zależności</span><span class="sxs-lookup"><span data-stu-id="e4d75-136">Dependency scenarios</span></span>
<span data-ttu-id="e4d75-137">Istnieją trzy scenariusze zależności podstawowe zadania, których można używać w partii zadań Azure: jeden do jednego, jeden do wielu, a zadania o identyfikatorze zakresu zależności.</span><span class="sxs-lookup"><span data-stu-id="e4d75-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="e4d75-138">Mogą to być połączone tooprovide czwarty scenariuszu wiele do wielu.</span><span class="sxs-lookup"><span data-stu-id="e4d75-138">These can be combined tooprovide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="e4d75-139">Scenariusz&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="e4d75-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="e4d75-140">Przykład</span><span class="sxs-lookup"><span data-stu-id="e4d75-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="e4d75-141">Jeden do jednego</span><span class="sxs-lookup"><span data-stu-id="e4d75-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="e4d75-142">*taskB* zależy od *taskA*</span><span class="sxs-lookup"><span data-stu-id="e4d75-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="e4d75-143">*taskB* nie będzie można zaplanować wykonywanie do momentu *taskA* zostało ukończone pomyślnie</span><span class="sxs-lookup"><span data-stu-id="e4d75-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="e4d75-144">![Diagram: jeden do jednego zadania zależności][1]</span><span class="sxs-lookup"><span data-stu-id="e4d75-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="e4d75-145">Jeden do wielu</span><span class="sxs-lookup"><span data-stu-id="e4d75-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="e4d75-146">*zadanieC* zależy od *zadaniaA* i *zadaniaB*</span><span class="sxs-lookup"><span data-stu-id="e4d75-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="e4d75-147">*taskC* nie zostanie zaplanowane do wykonania przed zakończeniem *taskA* i *taskB* zostały ukończone pomyślnie</span><span class="sxs-lookup"><span data-stu-id="e4d75-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="e4d75-148">![Diagram: jeden do wielu zadań zależności][2]</span><span class="sxs-lookup"><span data-stu-id="e4d75-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="e4d75-149">Zakres identyfikator zadania</span><span class="sxs-lookup"><span data-stu-id="e4d75-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="e4d75-150">*taskD* zależy od zakresu zadań</span><span class="sxs-lookup"><span data-stu-id="e4d75-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="e4d75-151">*taskD* nie zostanie zaplanowane wykonywanie do momentu hello zadania z identyfikatorami *1* za pośrednictwem *10* zostały ukończone pomyślnie</span><span class="sxs-lookup"><span data-stu-id="e4d75-151">*taskD* will not be scheduled for execution until hello tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="e4d75-152">![Diagram: Zadanie identyfikator zakresu zależności][3]</span><span class="sxs-lookup"><span data-stu-id="e4d75-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="e4d75-153">Można utworzyć **wiele do wielu** relacje, np. gdy zadania C, D E i F każdego zależą od zadania, A i B. Jest to przydatne, na przykład w zrównoleglone przetwarzania wstępnego scenariuszy, w którym zadania podrzędne są zależne od danych wyjściowych hello wielu zadań nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="e4d75-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on hello output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="e4d75-154">W przykładach hello w tej sekcji zależne zadanie jest uruchamiane tylko wtedy, gdy zadania nadrzędnego hello pomyślnie ukończona.</span><span class="sxs-lookup"><span data-stu-id="e4d75-154">In hello examples in this section, a dependent task runs only after hello parent tasks complete successfully.</span></span> <span data-ttu-id="e4d75-155">To zachowanie jest hello domyślne zachowanie dla zadania zależne.</span><span class="sxs-lookup"><span data-stu-id="e4d75-155">This behavior is hello default behavior for a dependent task.</span></span> <span data-ttu-id="e4d75-156">Możesz uruchomić zadanie zależne po niepowodzeniu zadaniem nadrzędnym, określając zachowanie domyślne hello toooverride akcji zależności.</span><span class="sxs-lookup"><span data-stu-id="e4d75-156">You can run a dependent task after a parent task fails by specifying a dependency action toooverride hello default behavior.</span></span> <span data-ttu-id="e4d75-157">Zobacz hello [akcje zależności](#dependency-actions) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="e4d75-157">See hello [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="e4d75-158">Jeden do jednego</span><span class="sxs-lookup"><span data-stu-id="e4d75-158">One-to-one</span></span>
<span data-ttu-id="e4d75-159">W relacji jeden do jednego zadania zależy od hello pomyślne zakończenie zadania jednego zdarzenia nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="e4d75-159">In a one-to-one relationship, a task depends on hello successful completion of one parent task.</span></span> <span data-ttu-id="e4d75-160">toocreate hello zależności, podaj toohello identyfikator pojedyncze zadanie [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] metody statycznej podczas wypełniania hello [DependsOn] [ net_dependson] właściwość [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="e4d75-160">toocreate hello dependency, provide a single task ID toohello [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="e4d75-161">Jeden do wielu</span><span class="sxs-lookup"><span data-stu-id="e4d75-161">One-to-many</span></span>
<span data-ttu-id="e4d75-162">W relacji jeden do wielu zadania zależy od ukończenia hello wielu zadań nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="e4d75-162">In a one-to-many relationship, a task depends on hello completion of multiple parent tasks.</span></span> <span data-ttu-id="e4d75-163">toocreate hello zależności, przedstawiają kolekcję zadań identyfikatorów toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] metody statycznej podczas wypełniania hello [DependsOn] [ net_dependson] właściwość [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="e4d75-163">toocreate hello dependency, provide a collection of task IDs toohello [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

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

### <a name="task-id-range"></a><span data-ttu-id="e4d75-164">Zakres identyfikator zadania</span><span class="sxs-lookup"><span data-stu-id="e4d75-164">Task ID range</span></span>
<span data-ttu-id="e4d75-165">W zależności w zakresie nadrzędnej zadania zadania zależy od hello hello zakończenia zadania, których identyfikatory znajdują się w zakresie.</span><span class="sxs-lookup"><span data-stu-id="e4d75-165">In a dependency on a range of parent tasks, a task depends on hello hello completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="e4d75-166">zależności hello toocreate, najpierw Podaj hello i ostatnio identyfikatorów zadań w hello zakresu toohello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] metody statycznej podczas wypełniania hello [DependsOn] [ net_dependson] właściwość [CloudTask] [net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="e4d75-166">toocreate hello dependency, provide hello first and last task IDs in hello range toohello [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4d75-167">Gdy używasz zakresy identyfikatorów zadań dla zależności hello identyfikatorów zadań w zakresie hello *musi* być liczbami w postaci ciągu wartości będące liczbami całkowitymi.</span><span class="sxs-lookup"><span data-stu-id="e4d75-167">When you use task ID ranges for your dependencies, hello task IDs in hello range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="e4d75-168">Każde zadanie w zakresie hello muszą spełniać zależności hello pomyślne zakończenie działania albo wykonując z błąd, który jest akcja zależności zamapowanych tooa ustawić także**Satisfy**.</span><span class="sxs-lookup"><span data-stu-id="e4d75-168">Every task in hello range must satisfy hello dependency, either by completing successfully or by completing with a failure that’s mapped tooa dependency action set too**Satisfy**.</span></span> <span data-ttu-id="e4d75-169">Zobacz hello [akcje zależności](#dependency-actions) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="e4d75-169">See hello [Dependency actions](#dependency-actions) section for details.</span></span>
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
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="e4d75-170">Akcje zależności</span><span class="sxs-lookup"><span data-stu-id="e4d75-170">Dependency actions</span></span>

<span data-ttu-id="e4d75-171">Domyślnie zadanie zależne lub zestawu zadań działa tylko po pomyślnym zakończeniu zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="e4d75-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="e4d75-172">W niektórych scenariuszach może być toorun zadania zależne, nawet w przypadku awarii hello zadaniem nadrzędnym.</span><span class="sxs-lookup"><span data-stu-id="e4d75-172">In some scenarios, you may want toorun dependent tasks even if hello parent task fails.</span></span> <span data-ttu-id="e4d75-173">Hello domyślne zachowanie można przesłonić, określając akcji zależności.</span><span class="sxs-lookup"><span data-stu-id="e4d75-173">You can override hello default behavior by specifying a dependency action.</span></span> <span data-ttu-id="e4d75-174">Akcja zależności Określa, czy zadanie zależne kwalifikujących się toorun, oparte na powitania powodzenie lub niepowodzenie hello zadaniem nadrzędnym.</span><span class="sxs-lookup"><span data-stu-id="e4d75-174">A dependency action specifies whether a dependent task is eligible toorun, based on hello success or failure of hello parent task.</span></span> 

<span data-ttu-id="e4d75-175">Na przykład załóżmy, że zadanie zależne oczekuje na dane z hello ukończenia zadania nadrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="e4d75-175">For example, suppose that a dependent task is awaiting data from hello completion of hello upstream task.</span></span> <span data-ttu-id="e4d75-176">Zadanie nadrzędne hello nie powiedzie się, zadania zależne hello może nadal być stanie toorun przy użyciu starszych danych.</span><span class="sxs-lookup"><span data-stu-id="e4d75-176">If hello upstream task fails, hello dependent task may still be able toorun using older data.</span></span> <span data-ttu-id="e4d75-177">W takim przypadku akcji zależności można określić zadania zależne hello jest toorun kwalifikujących się niezależnie od awarii hello hello zadaniem nadrzędnym.</span><span class="sxs-lookup"><span data-stu-id="e4d75-177">In this case, a dependency action can specify that hello dependent task is eligible toorun despite hello failure of hello parent task.</span></span>

<span data-ttu-id="e4d75-178">Akcja zależności jest oparta na warunku wyjścia dla zadania nadrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="e4d75-178">A dependency action is based on an exit condition for hello parent task.</span></span> <span data-ttu-id="e4d75-179">Można określić akcję zależności dla każdego hello następujących warunków zakończenia. dla platformy .NET, zobacz hello [ExitConditions] [ net_exitconditions] klasy, aby uzyskać szczegółowe informacje:</span><span class="sxs-lookup"><span data-stu-id="e4d75-179">You can specify a dependency action for any of hello following exit conditions; for .NET, see hello [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="e4d75-180">Po wystąpieniu błędu przetwarzania wstępnego.</span><span class="sxs-lookup"><span data-stu-id="e4d75-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="e4d75-181">Po wystąpieniu błędu przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="e4d75-181">When a file upload error occurs.</span></span> <span data-ttu-id="e4d75-182">Jeśli zadanie hello kończy działanie z kodem zakończenia, która została określona za pomocą **exitCodes** lub **exitCodeRanges**, a następnie napotka błąd podczas przekazywania pliku, hello akcji określonej przez hello zakończenia kod ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="e4d75-182">If hello task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, hello action specified by hello exit code takes precedence.</span></span>
- <span data-ttu-id="e4d75-183">Gdy zadanie hello kończy działanie z kodem zakończenia zdefiniowanych przez hello **ExitCodes** właściwości.</span><span class="sxs-lookup"><span data-stu-id="e4d75-183">When hello task exits with an exit code defined by hello **ExitCodes** property.</span></span>
- <span data-ttu-id="e4d75-184">Gdy zadanie hello kończy działanie z kodem zakończenia, która wykracza poza zakres określony przez hello **ExitCodeRanges** właściwości.</span><span class="sxs-lookup"><span data-stu-id="e4d75-184">When hello task exits with an exit code that falls within a range specified by hello **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="e4d75-185">Witaj domyślne działanie case, jeśli zadanie hello kończy działanie z kodem zakończenia nie jest zdefiniowany przez **ExitCodes** lub **ExitCodeRanges**, lub czy istnieje hello zadań przetwarzania wstępnego błąd i hello **PreProcessingError**  nie ustawiono właściwości lub jeśli hello zadań kończy się niepowodzeniem z plikiem przekazywanie błędów i hello **FileUploadError** nie ustawiono właściwości.</span><span class="sxs-lookup"><span data-stu-id="e4d75-185">hello default case, if hello task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if hello task exits with a pre-processing error and hello **PreProcessingError** property is not set, or if hello task fails with a file upload error and hello **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="e4d75-186">toospecify akcją zależności w programie .NET, zestaw hello [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] właściwości warunku exit hello.</span><span class="sxs-lookup"><span data-stu-id="e4d75-186">toospecify a dependency action in .NET, set hello [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for hello exit condition.</span></span> <span data-ttu-id="e4d75-187">Witaj **DependencyAction** właściwość przyjmuje jeden z dwóch wartości:</span><span class="sxs-lookup"><span data-stu-id="e4d75-187">hello **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="e4d75-188">Ustawienie hello **DependencyAction** właściwości zbyt**Satisfy** wskazuje, że zadania zależne są toorun kwalifikujących się, jeśli zadaniem nadrzędnym hello kończy działanie z powodu określonego błędu.</span><span class="sxs-lookup"><span data-stu-id="e4d75-188">Setting hello **DependencyAction** property too**Satisfy** indicates that dependent tasks are eligible toorun if hello parent task exits with a specified error.</span></span>
- <span data-ttu-id="e4d75-189">Ustawienie hello **DependencyAction** właściwości zbyt**bloku** wskazuje, że zadania zależne nie są toorun kwalifikujących się.</span><span class="sxs-lookup"><span data-stu-id="e4d75-189">Setting hello **DependencyAction** property too**Block** indicates that dependent tasks are not eligible toorun.</span></span>

<span data-ttu-id="e4d75-190">Domyślnym ustawieniem hello Hello **DependencyAction** właściwość jest **Satisfy** dla kod zakończenia 0, i **bloku** dla wszystkich innych warunków zakończenia.</span><span class="sxs-lookup"><span data-stu-id="e4d75-190">hello default setting for hello **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="e4d75-191">Witaj poniższy fragment kodu ustawia hello **DependencyAction** właściwości dla zadania nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="e4d75-191">hello following code snippet sets hello **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="e4d75-192">Jeśli zadaniem nadrzędnym hello kończy działanie z błędem przetwarzania wstępnego lub z hello hello zależnych kody błędów określona, zadanie zostanie zablokowany.</span><span class="sxs-lookup"><span data-stu-id="e4d75-192">If hello parent task exits with a pre-processing error, or with hello specified error codes, hello dependent task is blocked.</span></span> <span data-ttu-id="e4d75-193">Jeśli zadaniem nadrzędnym hello kończy działanie z inny błąd zera, zadania zależne hello jest toorun kwalifikujących się.</span><span class="sxs-lookup"><span data-stu-id="e4d75-193">If hello parent task exits with any other non-zero error, hello dependent task is eligible toorun.</span></span>

```csharp
// Task A is hello parent task.
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
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="e4d75-194">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="e4d75-194">Code sample</span></span>
<span data-ttu-id="e4d75-195">Witaj [TaskDependencies] [ github_taskdependencies] przykładowy projekt jest jednym z hello [przykłady kodu partii zadań Azure] [ github_samples] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="e4d75-195">hello [TaskDependencies][github_taskdependencies] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="e4d75-196">Przedstawiono to rozwiązanie Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e4d75-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="e4d75-197">Jak tooenable zadań zależności w zadaniu</span><span class="sxs-lookup"><span data-stu-id="e4d75-197">How tooenable task dependency on a job</span></span>
- <span data-ttu-id="e4d75-198">Jak toocreate zadań, które są zależne od innych zadań</span><span class="sxs-lookup"><span data-stu-id="e4d75-198">How toocreate tasks that depend on other tasks</span></span>
- <span data-ttu-id="e4d75-199">Jak tooexecute tych zadań w puli węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="e4d75-199">How tooexecute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4d75-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4d75-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="e4d75-201">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e4d75-201">Application deployment</span></span>
<span data-ttu-id="e4d75-202">Witaj [pakietów aplikacji](batch-application-packages.md) funkcja partii zapewnia łatwy sposób wdrożyć tooboth i wersji aplikacji hello, wykonywanych zadań na węzłach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="e4d75-202">hello [application packages](batch-application-packages.md) feature of Batch provides an easy way tooboth deploy and version hello applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="e4d75-203">Instalowanie aplikacji i danych na potrzeby przemieszczania</span><span class="sxs-lookup"><span data-stu-id="e4d75-203">Installing applications and staging data</span></span>
<span data-ttu-id="e4d75-204">Zobacz [instalowania aplikacji i danych na partii przemieszczania węzły obliczeniowe] [ forum_post] forum partii zadań Azure hello Omówienie metody przygotowania węzły toorun zadania.</span><span class="sxs-lookup"><span data-stu-id="e4d75-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in hello Azure Batch forum for an overview of methods for preparing your nodes toorun tasks.</span></span> <span data-ttu-id="e4d75-205">Zapisane przez jeden z członków zespołu partii zadań Azure hello, ten wpis jest dobrym Elementarz na powitania różne sposoby toocopy aplikacje, dane wejściowe zadania i inne pliki tooyour obliczeniowe węzłów.</span><span class="sxs-lookup"><span data-stu-id="e4d75-205">Written by one of hello Azure Batch team members, this post is a good primer on hello different ways toocopy applications, task input data, and other files tooyour compute nodes.</span></span>

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

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: jeden do jednego zależności"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: jeden do wielu zależności"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: zadanie identyfikator zakresu zależności"
