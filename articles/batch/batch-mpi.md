---
title: "Użycie wielu wystąpień zadań w celu uruchamiania aplikacji MPI - partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie wykonywania aplikacji komunikat interfejsu (Passing Interface), za pomocą typu zadania wielu wystąpień w partii zadań Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77d12d6d48b22dfb3e7f09f273dffc11401bb15f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-multi-instance-tasks-to-run-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="02286-103">Użycie wielu wystąpień zadań w celu uruchamiania aplikacji komunikat interfejsu (Passing Interface) w partii</span><span class="sxs-lookup"><span data-stu-id="02286-103">Use multi-instance tasks to run Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="02286-104">Mająca wiele wystąpień zadań umożliwiają uruchomić zadanie partii zadań Azure jednocześnie na wielu węzłach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="02286-104">Multi-instance tasks allow you to run an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="02286-105">Te zadania umożliwiają wysokiej wydajności obliczeniowej scenariuszy, takich jak aplikacje interfejsu Message (Passing) w partii.</span><span class="sxs-lookup"><span data-stu-id="02286-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="02286-106">W tym artykule opisano sposób wykonania wielu wystąpień zadania przy użyciu [partiami platformy .NET] [ api_net] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="02286-106">In this article, you learn how to execute multi-instance tasks using the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="02286-107">Przykłady w tym artykule dotyczą partiami platformy .NET, MS-MPI i węzły obliczeniowe systemu Windows, wielu wystąpień zadań omówione w tym miejscu są stosowane do innych platform i technologii (Python i Intel MPI w węzłach Linux, na przykład).</span><span class="sxs-lookup"><span data-stu-id="02286-107">While the examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, the multi-instance task concepts discussed here are applicable to other platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="02286-108">Omówienie zadań wielu wystąpień</span><span class="sxs-lookup"><span data-stu-id="02286-108">Multi-instance task overview</span></span>
<span data-ttu-id="02286-109">W zadaniu wsadowym, każde zadanie jest zazwyczaj wykonywane na jednym węźle obliczeń — przesłać wielu zadań do zadania, a usługa partia zadań harmonogramy poszczególnych zadań do wykonania w węźle.</span><span class="sxs-lookup"><span data-stu-id="02286-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks to a job, and the Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="02286-110">Jednakże, konfigurując zadania **ustawień wielu wystąpieniach**, poinformuj partii, zamiast tego utworzyć jedno zadanie podstawowego i kilka podzadań, które następnie są wykonywane na wielu węzłach.</span><span class="sxs-lookup"><span data-stu-id="02286-110">However, by configuring a task's **multi-instance settings**, you tell Batch to instead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="02286-111">![Omówienie zadań wielu wystąpień][1]</span><span class="sxs-lookup"><span data-stu-id="02286-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="02286-112">Po przesłaniu zadania o wielu wystąpieniach ustawienia do zadania wsadowego wykonuje kilka kroków unikatowy do wielu wystąpień zadań:</span><span class="sxs-lookup"><span data-stu-id="02286-112">When you submit a task with multi-instance settings to a job, Batch performs several steps unique to multi-instance tasks:</span></span>

1. <span data-ttu-id="02286-113">Usługa partia zadań tworzy jeden **głównej** i kilka **podzadania** na podstawie ustawień wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="02286-113">The Batch service creates one **primary** and several **subtasks** based on the multi-instance settings.</span></span> <span data-ttu-id="02286-114">Łączna liczba zadań (podstawowym oraz wszystkie podzadania) jest zgodna z liczbą **wystąpień** (węzły obliczeniowe) określonym w ustawieniach wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="02286-114">The total number of tasks (primary plus all subtasks) matches the number of **instances** (compute nodes) you specify in the multi-instance settings.</span></span>
2. <span data-ttu-id="02286-115">Wsadowe wskazuje na jeden z węzłów obliczeniowych jako **wzorca**oraz ustalenia jego harmonogramu głównej zadań do wykonania na głównym.</span><span class="sxs-lookup"><span data-stu-id="02286-115">Batch designates one of the compute nodes as the **master**, and schedules the primary task to execute on the master.</span></span> <span data-ttu-id="02286-116">Planowana podzadania do wykonania na pozostałą część węzły obliczeniowe przydzielone do wielu wystąpień zadania, co podzadanie na węzeł.</span><span class="sxs-lookup"><span data-stu-id="02286-116">It schedules the subtasks to execute on the remainder of the compute nodes allocated to the multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="02286-117">Podstawową i wszystkie podzadania pobrać żadnej **wspólne pliki zasobów** określonymi w ustawieniach wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="02286-117">The primary and all subtasks download any **common resource files** you specify in the multi-instance settings.</span></span>
4. <span data-ttu-id="02286-118">Po wspólnych zasobów pliki zostały pobrane, podstawową i wykonywanie podzadania **polecenia koordynacji** określonymi w ustawieniach wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="02286-118">After the common resource files have been downloaded, the primary and subtasks execute the **coordination command** you specify in the multi-instance settings.</span></span> <span data-ttu-id="02286-119">Polecenie koordynacji zwykle służy do przygotowania węzły do wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="02286-119">The coordination command is typically used to prepare nodes for executing the task.</span></span> <span data-ttu-id="02286-120">Mogą to być uruchomienie usługi tła (takich jak [Microsoft MPI][msmpi_msdn]w `smpd.exe`) i sprawdzanie, czy węzły są gotowe do przetworzenia komunikatów między węzłami.</span><span class="sxs-lookup"><span data-stu-id="02286-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that the nodes are ready to process inter-node messages.</span></span>
5. <span data-ttu-id="02286-121">Podstawowe zadania wykonuje **polecenia aplikacji** w węźle głównym *po* pomyślnie wykonać polecenia koordynacji serwerem podstawowym, a wszystkie podzadania.</span><span class="sxs-lookup"><span data-stu-id="02286-121">The primary task executes the **application command** on the master node *after* the coordination command has been completed successfully by the primary and all subtasks.</span></span> <span data-ttu-id="02286-122">Polecenie aplikacji jest to samo zadanie wielu wystąpień wiersz polecenia i są wykonywane tylko przez podstawowe zadania.</span><span class="sxs-lookup"><span data-stu-id="02286-122">The application command is the command line of the multi-instance task itself, and is executed only by the primary task.</span></span> <span data-ttu-id="02286-123">W [MS-MPI][msmpi_msdn]— na podstawie rozwiązania, jest to, gdzie można wykonywać przy użyciu aplikacji obsługującej na MPI `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="02286-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="02286-124">Chociaż funkcjonalnie distinct, "zadanie wielu wystąpieniach" nie jest typu unikatowy zadań, takich jak [StartTask] [ net_starttask] lub [JobPreparationTask] [ net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="02286-124">Though it is functionally distinct, the "multi-instance task" is not a unique task type like the [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="02286-125">Zadanie wielu wystąpień jest po prostu standardowe zadania wsadowego ([CloudTask] [ net_task] w partiami platformy .NET) o wielu wystąpieniach ustawienia zostały skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="02286-125">The multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="02286-126">W tym artykule określane jako **wielu wystąpień zadań**.</span><span class="sxs-lookup"><span data-stu-id="02286-126">In this article, we refer to this as the **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="02286-127">Wymagania dotyczące zadań w wielu wystąpieniach</span><span class="sxs-lookup"><span data-stu-id="02286-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="02286-128">Mająca wiele wystąpień zadania wymagają z pulą **włączono komunikację między węzłami**oraz z **wykonywanie zadań jednoczesnych wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="02286-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="02286-129">Aby wyłączyć wykonywanie zadań jednoczesnych, ustaw [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) właściwości na wartość 1.</span><span class="sxs-lookup"><span data-stu-id="02286-129">To disable concurrent task execution, set the [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property to 1.</span></span>

<span data-ttu-id="02286-130">Następujący fragment kodu przedstawia sposób tworzenia puli dla wielu wystąpień zadań za pomocą biblioteki partiami platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="02286-130">This code snippet shows how to create a pool for multi-instance tasks using the Batch .NET library.</span></span>

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> <span data-ttu-id="02286-131">Jeśli zostanie podjęta próba uruchomienia zadania wielu wystąpień w puli, bez wyłączone komunikacji między węzłami lub z *maxTasksPerNode* wartość większą niż 1, nie jest zaplanowane zadanie — nieskończoność pozostaje w stanie "aktywny".</span><span class="sxs-lookup"><span data-stu-id="02286-131">If you try to run a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, the task is never scheduled--it remains indefinitely in the "active" state.</span></span> 
>
> <span data-ttu-id="02286-132">Mająca wiele wystąpień zadania mogą wykonywać tylko w przypadku węzłów w pulach utworzone po 14 grudnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="02286-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-to-install-mpi"></a><span data-ttu-id="02286-133">Należy zainstalować MPI StartTask</span><span class="sxs-lookup"><span data-stu-id="02286-133">Use a StartTask to install MPI</span></span>
<span data-ttu-id="02286-134">Do uruchamiania aplikacji MPI o wielu wystąpieniach zadania, należy najpierw zainstalować implementacja interfejsu MPI (MS-MPI lub MPI firmy Intel, na przykład) w węzłach obliczeniowych w puli.</span><span class="sxs-lookup"><span data-stu-id="02286-134">To run MPI applications with a multi-instance task, you first need to install an MPI implementation (MS-MPI or Intel MPI, for example) on the compute nodes in the pool.</span></span> <span data-ttu-id="02286-135">Jest to odpowiedni moment, aby użyć [StartTask][net_starttask], który wykonuje zawsze, gdy węzeł dołącza pulę lub ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="02286-135">This is a good time to use a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="02286-136">Następujący fragment kodu tworzy StartTask, który określa pakiet instalacyjny MS-MPI jako [pliku zasobu][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="02286-136">This code snippet creates a StartTask that specifies the MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="02286-137">Wiersz polecenia zadania uruchamiania jest wykonywany po pobraniu pliku zasobu do węzła.</span><span class="sxs-lookup"><span data-stu-id="02286-137">The start task's command line is executed after the resource file is downloaded to the node.</span></span> <span data-ttu-id="02286-138">W takim przypadku wiersza polecenia przeprowadza instalację nienadzorowaną MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="02286-138">In this case, the command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for the pool which we use for installing MS-MPI on
// the nodes as they join the pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit the fully configured pool to the Batch service to actually create
// the pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="02286-139">Zdalny bezpośredni dostęp do pamięci (RDMA)</span><span class="sxs-lookup"><span data-stu-id="02286-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="02286-140">Po wybraniu [z funkcją RDMA rozmiar](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) A9 dla węzłów obliczeniowych w puli partii, np. aplikacji MPI można korzystać z platformy Azure wysokiej wydajności i małych opóźnieniach zdalnego pamięci bezpośredniego dostępu (do pamięci RDMA) sieci.</span><span class="sxs-lookup"><span data-stu-id="02286-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for the compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="02286-141">Wyszukaj rozmiary określony jako "RDMA stanie" w następujących artykułach:</span><span class="sxs-lookup"><span data-stu-id="02286-141">Look for the sizes specified as "RDMA capable" in the following articles:</span></span>

* <span data-ttu-id="02286-142">**CloudServiceConfiguration** pule</span><span class="sxs-lookup"><span data-stu-id="02286-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="02286-143">[Rozmiary dla usług w chmurze](../cloud-services/cloud-services-sizes-specs.md) (tylko system Windows)</span><span class="sxs-lookup"><span data-stu-id="02286-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="02286-144">**VirtualMachineConfiguration** pule</span><span class="sxs-lookup"><span data-stu-id="02286-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="02286-145">[Rozmiary maszyn wirtualnych na platformie Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="02286-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="02286-146">[Rozmiary maszyn wirtualnych na platformie Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (system Windows)</span><span class="sxs-lookup"><span data-stu-id="02286-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="02286-147">Aby móc korzystać z funkcji RDMA [węzły obliczeniowe Linux](batch-linux-nodes.md), należy użyć **Intel MPI** w węzłach.</span><span class="sxs-lookup"><span data-stu-id="02286-147">To take advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on the nodes.</span></span> <span data-ttu-id="02286-148">Aby uzyskać więcej informacji na CloudServiceConfiguration i VirtualMachineConfiguration pule, zobacz sekcję puli [Przegląd funkcji partii](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="02286-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see the Pool section of the [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="02286-149">Utwórz zadanie wielu wystąpień z partiami platformy .NET</span><span class="sxs-lookup"><span data-stu-id="02286-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="02286-150">Teraz, kiedy możemy zostały objęte wymagań puli i instalacji pakietu MPI, Utwórzmy zadań wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="02286-150">Now that we've covered the pool requirements and MPI package installation, let's create the multi-instance task.</span></span> <span data-ttu-id="02286-151">W tym fragmencie, utworzymy standard [CloudTask][net_task], skonfiguruj jego [MultiInstanceSettings] [ net_multiinstance_prop] właściwości.</span><span class="sxs-lookup"><span data-stu-id="02286-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="02286-152">Jak wspomniano wcześniej, wielu wystąpieniach zadanie nie jest typem różne zadania, ale zadania wsadowego standardowego skonfigurowane przy użyciu ustawień wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="02286-152">As mentioned earlier, the multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create the multi-instance task. Its command line is the "application command"
// and will be executed *only* by the primary, and only after the primary and
// subtasks execute the CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure the task's MultiInstanceSettings. The CoordinationCommandLine will be executed by
// the primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit the task to the job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on the nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="02286-153">Podstawowe zadania i podzadania</span><span class="sxs-lookup"><span data-stu-id="02286-153">Primary task and subtasks</span></span>
<span data-ttu-id="02286-154">Podczas tworzenia ustawienia wielu wystąpień dla tego zadania można określić numer węzłów obliczeniowych, które są komponentu.</span><span class="sxs-lookup"><span data-stu-id="02286-154">When you create the multi-instance settings for a task, you specify the number of compute nodes that are to execute the task.</span></span> <span data-ttu-id="02286-155">Podczas przesyłania zadań do zadania, usługa partia zadań tworzy jeden **głównej** zadań i wystarczającą ilość **podzadania** razem spełniających liczba węzłów określona.</span><span class="sxs-lookup"><span data-stu-id="02286-155">When you submit the task to a job, the Batch service creates one **primary** task and enough **subtasks** that together match the number of nodes you specified.</span></span>

<span data-ttu-id="02286-156">Te zadania są przypisane identyfikator liczbą całkowitą z zakresu od 0 do *numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="02286-156">These tasks are assigned an integer id in the range of 0 to *numberOfInstances* - 1.</span></span> <span data-ttu-id="02286-157">Zadania o identyfikatorze 0 jest głównym zadaniem, a wszystkie inne identyfikatory są podzadania.</span><span class="sxs-lookup"><span data-stu-id="02286-157">The task with id 0 is the primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="02286-158">Na przykład jeśli tworzysz wiele wystąpień następujących ustawień zadania głównym zadaniem będzie mieć identyfikator 0 i podzadań znajdują się identyfikatory 1 do 9.</span><span class="sxs-lookup"><span data-stu-id="02286-158">For example, if you create the following multi-instance settings for a task, the primary task would have an id of 0, and the subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="02286-159">Węzła głównego</span><span class="sxs-lookup"><span data-stu-id="02286-159">Master node</span></span>
<span data-ttu-id="02286-160">Po przesłaniu zadania wielu wystąpień usługi partia zadań określa jeden z węzłów obliczeniowych jako węzeł "główny" oraz ustalenia jego harmonogramu głównej zadań do wykonania w węźle głównym.</span><span class="sxs-lookup"><span data-stu-id="02286-160">When you submit a multi-instance task, the Batch service designates one of the compute nodes as the "master" node, and schedules the primary task to execute on the master node.</span></span> <span data-ttu-id="02286-161">Do wykonania w pozostałych węzłach przydzielone do wielu wystąpień zadania zaplanowane podzadań.</span><span class="sxs-lookup"><span data-stu-id="02286-161">The subtasks are scheduled to execute on the remainder of the nodes allocated to the multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="02286-162">Polecenie koordynacji</span><span class="sxs-lookup"><span data-stu-id="02286-162">Coordination command</span></span>
<span data-ttu-id="02286-163">**Polecenia koordynacji** jest wykonywane przez serwer podstawowy i podzadania.</span><span class="sxs-lookup"><span data-stu-id="02286-163">The **coordination command** is executed by both the primary and subtasks.</span></span>

<span data-ttu-id="02286-164">Wywołanie polecenia koordynacji blokuje — partii nie wykonuj polecenia aplikacji, aż polecenie koordynacji zwrócił pomyślnie dla wszystkich zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="02286-164">The invocation of the coordination command is blocking--Batch does not execute the application command until the coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="02286-165">Polecenie koordynacji powinny w związku z tym uruchomić wszystkie wymagane tła usługi, sprawdź, czy są gotowe do użycia, a następnie zamknij.</span><span class="sxs-lookup"><span data-stu-id="02286-165">The coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="02286-166">Na przykład to polecenie koordynacji rozwiązania przy użyciu MS-MPI w wersji 7 uruchamia usługę SMPD w węźle kończy pracę:</span><span class="sxs-lookup"><span data-stu-id="02286-166">For example, this coordination command for a solution using MS-MPI version 7 starts the SMPD service on the node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="02286-167">Zwróć uwagę na użycie `start` w tym poleceniu koordynacji.</span><span class="sxs-lookup"><span data-stu-id="02286-167">Note the use of `start` in this coordination command.</span></span> <span data-ttu-id="02286-168">Jest to wymagane, ponieważ `smpd.exe` aplikacji nie może zwracać natychmiast po wykonaniu.</span><span class="sxs-lookup"><span data-stu-id="02286-168">This is required because the `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="02286-169">Bez użycia [start] [ cmd_start] polecenia, to polecenie koordynacji nie zwróci i w związku z tym uniemożliwiają uruchamianie polecenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02286-169">Without the use of the [start][cmd_start] command, this coordination command would not return, and would therefore block the application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="02286-170">Polecenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="02286-170">Application command</span></span>
<span data-ttu-id="02286-171">Po głównym zadaniem i wszystkie podzadania zostało ukończone, wykonując polecenie koordynacji, wiersz polecenia zadania wielu wystąpień jest wykonywana przez podstawowe zadania *tylko*.</span><span class="sxs-lookup"><span data-stu-id="02286-171">Once the primary task and all subtasks have finished executing the coordination command, the multi-instance task's command line is executed by the primary task *only*.</span></span> <span data-ttu-id="02286-172">Nazywamy to **polecenia aplikacji** odróżniający go od polecenia koordynacji.</span><span class="sxs-lookup"><span data-stu-id="02286-172">We call this the **application command** to distinguish it from the coordination command.</span></span>

<span data-ttu-id="02286-173">Dla aplikacji MS MPI, użyj polecenia aplikacji do wykonywania aplikacji z obsługą MPI z `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="02286-173">For MS-MPI applications, use the application command to execute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="02286-174">Na przykład poniżej przedstawiono polecenia aplikacji dotyczących rozwiązania przy użyciu MS-MPI w wersji 7:</span><span class="sxs-lookup"><span data-stu-id="02286-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="02286-175">Ponieważ MS MPI `mpiexec.exe` używa `CCP_NODES` zmiennej domyślnie (zobacz [zmiennych środowiskowych](#environment-variables)) powyżej wiersza polecenia aplikacji przykład wyklucza go.</span><span class="sxs-lookup"><span data-stu-id="02286-175">Because MS-MPI's `mpiexec.exe` uses the `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) the example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="02286-176">Zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="02286-176">Environment variables</span></span>
<span data-ttu-id="02286-177">Tworzy kilka partii [zmiennych środowiskowych] [ msdn_env_var] specyficzne dla zadania wielu wystąpień w węzłach obliczeniowych przydzielony do zadania wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="02286-177">Batch creates several [environment variables][msdn_env_var] specific to multi-instance tasks on the compute nodes allocated to a multi-instance task.</span></span> <span data-ttu-id="02286-178">Jak skrypty i programy, które są one wykonywane wiersze polecenia koordynacji i aplikacji może się odwoływać zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="02286-178">Your coordination and application command lines can reference these environment variables, as can the scripts and programs they execute.</span></span>

<span data-ttu-id="02286-179">Następujące zmienne środowiskowe są tworzone przez usługę partii do użycia przez wiele wystąpień zadania:</span><span class="sxs-lookup"><span data-stu-id="02286-179">The following environment variables are created by the Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="02286-180">Aby uzyskać szczegółowe informacje o tych i innych partii obliczeniowe węzła zmiennych środowiskowych, łącznie z ich zawartość i widoczność, zobacz [obliczeniowe zmiennych środowiskowych węzła][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="02286-180">For full details on these and the other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="02286-181">Przykładowy kod partii Linux MPI zawiera przykład sposobu niektóre zmienne środowiskowe użycia.</span><span class="sxs-lookup"><span data-stu-id="02286-181">The Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="02286-182">[Cmd koordynacji] [ coord_cmd_example] skryptu Bash pobiera typowych aplikacji i danych wejściowych plików z usługi Azure Storage, włącza udziału sieciowego systemu plików (NFS), w węźle głównym i konfiguruje innych węzłów przydzielony do zadania wielu wystąpień jako klienci systemu plików NFS.</span><span class="sxs-lookup"><span data-stu-id="02286-182">The [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on the master node, and configures the other nodes allocated to the multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="02286-183">Pliki zasobów</span><span class="sxs-lookup"><span data-stu-id="02286-183">Resource files</span></span>
<span data-ttu-id="02286-184">Istnieją dwa zestawy plików zasobów wziąć pod uwagę dla wielu wystąpień zadań: **wspólne pliki zasobów** który *wszystkie* zadania Pobierz (podstawowych i podzadania) i **pliki zasobów** określona dla wielu wystąpień zadań, które *tylko podstawowy* zadań pliki do pobrania.</span><span class="sxs-lookup"><span data-stu-id="02286-184">There are two sets of resource files to consider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and the **resource files** specified for the multi-instance task itself, which *only the primary* task downloads.</span></span>

<span data-ttu-id="02286-185">Można określić jedną lub więcej **wspólne pliki zasobów** w ustawieniach wielu wystąpień dla zadania.</span><span class="sxs-lookup"><span data-stu-id="02286-185">You can specify one or more **common resource files** in the multi-instance settings for a task.</span></span> <span data-ttu-id="02286-186">Te wspólne pliki zasobów są pobierane z [usługi Azure Storage](../storage/common/storage-introduction.md) w każdym węźle **zadań udostępnionego katalogu** serwerem podstawowym, a wszystkie podzadania.</span><span class="sxs-lookup"><span data-stu-id="02286-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by the primary and all subtasks.</span></span> <span data-ttu-id="02286-187">Udostępniony katalog zadania mogą korzystać z aplikacji i koordynacji wierszy polecenia, za pomocą `AZ_BATCH_TASK_SHARED_DIR` zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="02286-187">You can access the task shared directory from application and coordination command lines by using the `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="02286-188">`AZ_BATCH_TASK_SHARED_DIR` Jest identyczne w każdym węźle przydzielone do wielu wystąpień zadania, w związku z tym można udostępnić polecenie pojedynczego koordynację między serwerem podstawowym i wszystkie podzadania.</span><span class="sxs-lookup"><span data-stu-id="02286-188">The `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated to the multi-instance task, thus you can share a single coordination command between the primary and all subtasks.</span></span> <span data-ttu-id="02286-189">Partii nie "Udostępnij" katalog w znaczeniu dostępu zdalnego, ale można go użyć jako instalacji lub współużytkować punkt, jak wspomniano wcześniej w końcówką zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="02286-189">Batch does not "share" the directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in the tip on environment variables.</span></span>

<span data-ttu-id="02286-190">Pliki zasobów, które można określić dla samo zadanie wielu wystąpieniach są pobierane do katalogu roboczego zadania, `AZ_BATCH_TASK_WORKING_DIR`, domyślnie.</span><span class="sxs-lookup"><span data-stu-id="02286-190">Resource files that you specify for the multi-instance task itself are downloaded to the task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="02286-191">Jak wspomniano, w przeciwieństwie do plików wspólnych zasobów, głównym zadaniem pobiera pliki zasobów określony dla samo zadanie wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="02286-191">As mentioned, in contrast to common resource files, only the primary task downloads resource files specified for the  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02286-192">Należy zawsze używać zmiennych środowiskowych `AZ_BATCH_TASK_SHARED_DIR` i `AZ_BATCH_TASK_WORKING_DIR` do odwoływania się do tych katalogów w Twojej wiersze polecenia.</span><span class="sxs-lookup"><span data-stu-id="02286-192">Always use the environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` to refer to these directories in your command lines.</span></span> <span data-ttu-id="02286-193">Nie należy ręcznie utworzyć ścieżki.</span><span class="sxs-lookup"><span data-stu-id="02286-193">Do not attempt to construct the paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="02286-194">Cykl życia zadania</span><span class="sxs-lookup"><span data-stu-id="02286-194">Task lifetime</span></span>
<span data-ttu-id="02286-195">Okres istnienia głównym zadaniem kontroluje cykl życia zadania całego wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="02286-195">The lifetime of the primary task controls the lifetime of the entire multi-instance task.</span></span> <span data-ttu-id="02286-196">Gdy kończy się serwerem podstawowym, są zamykane wszystkie podzadania.</span><span class="sxs-lookup"><span data-stu-id="02286-196">When the primary exits, all of the subtasks are terminated.</span></span> <span data-ttu-id="02286-197">Kod zakończenia podstawowych jest kod zakończenia zadania, a w związku z tym służy do określania powodzenie lub niepowodzenie zadania dla celów ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="02286-197">The exit code of the primary is the exit code of the task, and is therefore used to determine the success or failure of the task for retry purposes.</span></span>

<span data-ttu-id="02286-198">W przypadku awarii dowolnego podzadań, został zakończony z kodem zwrotnym zera, na przykład cały wielu wystąpień niepowodzenia zadania.</span><span class="sxs-lookup"><span data-stu-id="02286-198">If any of the subtasks fail, exiting with a non-zero return code, for example, the entire multi-instance task fails.</span></span> <span data-ttu-id="02286-199">Zadanie wielu wystąpień jest następnie przerwane i ponowione do jego limit ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="02286-199">The multi-instance task is then terminated and retried, up to its retry limit.</span></span>

<span data-ttu-id="02286-200">Podczas usuwania zadania wielu wystąpień serwera podstawowego i wszystkie podzadania są również usuwane przez usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="02286-200">When you delete a multi-instance task, the primary and all subtasks are also deleted by the Batch service.</span></span> <span data-ttu-id="02286-201">Podzadanie wszystkie katalogi i pliki są usuwane z węzłów obliczeniowych, podobnie jak w przypadku zadania standardowego.</span><span class="sxs-lookup"><span data-stu-id="02286-201">All subtask directories and their files are deleted from the compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="02286-202">[TaskConstraints] [ net_taskconstraints] dla wielu wystąpień zadania, takie jak [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], i [RetentionTime] [ net_taskconstraint_retention] właściwości, są honorowane standardowe zadania, i mają zastosowanie do serwera podstawowego i wszystkie podzadania.</span><span class="sxs-lookup"><span data-stu-id="02286-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as the [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply to the primary and all subtasks.</span></span> <span data-ttu-id="02286-203">Jednak w przypadku zmiany [RetentionTime] [ net_taskconstraint_retention] właściwości po dodaniu zadań wielu wystąpień do zadania, ta zmiana jest stosowane tylko do głównej zadań.</span><span class="sxs-lookup"><span data-stu-id="02286-203">However, if you change the [RetentionTime][net_taskconstraint_retention] property after adding the multi-instance task to the job, this change is applied only to the primary task.</span></span> <span data-ttu-id="02286-204">Wszystkie podzadania nadal używać oryginalnej [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="02286-204">All of the subtasks continue to use the original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="02286-205">Listy ostatnich zadań węźle obliczeń odzwierciedla identyfikator podzadaniem ostatnie zadanie było częścią zadań wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="02286-205">A compute node's recent task list reflects the id of a subtask if the recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="02286-206">Uzyskaj informacje na temat podzadania</span><span class="sxs-lookup"><span data-stu-id="02286-206">Obtain information about subtasks</span></span>
<span data-ttu-id="02286-207">Aby uzyskać informacje na podzadania przy użyciu biblioteki partiami platformy .NET, należy wywołać [CloudTask.ListSubtasks] [ net_task_listsubtasks] metody.</span><span class="sxs-lookup"><span data-stu-id="02286-207">To obtain information on subtasks by using the Batch .NET library, call the [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="02286-208">Ta metoda zwraca informacje o wszystkich podzadań oraz informacje o węźle obliczeń, które wykonywane zadania.</span><span class="sxs-lookup"><span data-stu-id="02286-208">This method returns information on all subtasks, and information about the compute node that executed the tasks.</span></span> <span data-ttu-id="02286-209">Z tych informacji można określić katalogu głównego każdego podzadania, identyfikator puli, jego bieżący stan i kod zakończenia.</span><span class="sxs-lookup"><span data-stu-id="02286-209">From this information, you can determine each subtask's root directory, the pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="02286-210">Te informacje można użyć w połączeniu z [PoolOperations.GetNodeFile] [ poolops_getnodefile] metoda uzyskania podzadanie plików.</span><span class="sxs-lookup"><span data-stu-id="02286-210">You can use this information in combination with the [PoolOperations.GetNodeFile][poolops_getnodefile] method to obtain the subtask's files.</span></span> <span data-ttu-id="02286-211">Należy pamiętać, że ta metoda nie zwraca informacje o zadaniu głównej (identyfikator: 0).</span><span class="sxs-lookup"><span data-stu-id="02286-211">Note that this method does not return information for the primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="02286-212">O ile nie określono inaczej, metody partiami platformy .NET, które działają na wielu wystąpieniach [CloudTask] [ net_task] się zastosować *tylko* z podstawowym zadaniem.</span><span class="sxs-lookup"><span data-stu-id="02286-212">Unless otherwise stated, Batch .NET methods that operate on the multi-instance [CloudTask][net_task] itself apply *only* to the primary task.</span></span> <span data-ttu-id="02286-213">Na przykład podczas wywoływania [CloudTask.ListNodeFiles] [ net_task_listnodefiles] metody w wielu wystąpieniach zadania, zwracane są tylko pliki głównym zadaniem.</span><span class="sxs-lookup"><span data-stu-id="02286-213">For example, when you call the [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only the primary task's files are returned.</span></span>
>
>

<span data-ttu-id="02286-214">Poniższy fragment kodu przedstawia sposób uzyskiwania informacji podzadania, jak również zawartość pliku żądania w węzłach, na których są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="02286-214">The following code snippet shows how to obtain subtask information, as well as request file contents from the nodes on which they executed.</span></span>

```csharp
// Obtain the job and the multi-instance task from the Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain the list of subtasks for the task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over the subtasks and print their stdout and stderr
// output if the subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a><span data-ttu-id="02286-215">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="02286-215">Code sample</span></span>
<span data-ttu-id="02286-216">[MultiInstanceTasks] [ github_mpi] przykładowy kod w serwisie GitHub pokazano, jak używane do uruchamiania zadań wielowystąpieniowy [MS-MPI] [ msmpi_msdn] aplikację na Węzły obliczeniowe partii.</span><span class="sxs-lookup"><span data-stu-id="02286-216">The [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how to use a multi-instance task to run an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="02286-217">Postępuj zgodnie z instrukcjami [przygotowania](#preparation) i [wykonywania](#execution) do uruchomienia przykładu.</span><span class="sxs-lookup"><span data-stu-id="02286-217">Follow the steps in [Preparation](#preparation) and [Execution](#execution) to run the sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="02286-218">Przygotowanie</span><span class="sxs-lookup"><span data-stu-id="02286-218">Preparation</span></span>
1. <span data-ttu-id="02286-219">Postępuj zgodnie z instrukcjami dwóch pierwszych [jak skompilować i uruchomić prosty program MS-MPI][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="02286-219">Follow the first two steps in [How to compile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="02286-220">Spełnia on prerequesites dla następny krok.</span><span class="sxs-lookup"><span data-stu-id="02286-220">This satisfies the prerequesites for the following step.</span></span>
2. <span data-ttu-id="02286-221">Tworzenie *wersji* wersji [MPIHelloWorld] [ helloworld_proj] przykładowy program MPI.</span><span class="sxs-lookup"><span data-stu-id="02286-221">Build a *Release* version of the [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="02286-222">Jest to program, który zostanie uruchomione dla węzłów obliczeniowych w zadaniu wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="02286-222">This is the program that will be run on compute nodes by the multi-instance task.</span></span>
3. <span data-ttu-id="02286-223">Tworzenie pliku zip zawierającego `MPIHelloWorld.exe` (która będzie utworzony w kroku 2) i `MSMpiSetup.exe` (który został pobrany w kroku 1).</span><span class="sxs-lookup"><span data-stu-id="02286-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="02286-224">Ten plik zip będzie przekazać jako pakietu aplikacji w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="02286-224">You'll upload this zip file as an application package in the next step.</span></span>
4. <span data-ttu-id="02286-225">Użyj [portalu Azure] [ portal] do tworzenia instancji [aplikacji](batch-application-packages.md) o nazwie "MPIHelloWorld" i określ plik zip został utworzony w poprzednim kroku jako wersji "1.0" pakiet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02286-225">Use the [Azure portal][portal] to create a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify the zip file you created in the previous step as version "1.0" of the application package.</span></span> <span data-ttu-id="02286-226">Zobacz [przekazywanie aplikacji i zarządzanie nimi](batch-application-packages.md#upload-and-manage-applications) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="02286-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="02286-227">Tworzenie *wersji* wersji `MPIHelloWorld.exe` , dzięki czemu nie trzeba obejmują dodatkowe zależności (na przykład `msvcp140d.dll` lub `vcruntime140d.dll`) do pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02286-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have to include any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="02286-228">Wykonanie</span><span class="sxs-lookup"><span data-stu-id="02286-228">Execution</span></span>
1. <span data-ttu-id="02286-229">Pobierz [azure partii próbek] [ github_samples_zip] z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="02286-229">Download the [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="02286-230">Otwórz MultiInstanceTasks **rozwiązania** w programie Visual Studio 2015 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="02286-230">Open the MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="02286-231">`MultiInstanceTasks.sln` Plik rozwiązania znajduje się w:</span><span class="sxs-lookup"><span data-stu-id="02286-231">The `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="02286-232">Wprowadź poświadczenia konta wsadowego i magazynowania w `AccountSettings.settings` w **Microsoft.Azure.Batch.Samples.Common** projektu.</span><span class="sxs-lookup"><span data-stu-id="02286-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in the **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="02286-233">**Tworzenie i uruchamianie** rozwiązania MultiInstanceTasks wykonać MPI przykładową aplikację w węzłach obliczeń w puli partii.</span><span class="sxs-lookup"><span data-stu-id="02286-233">**Build and run** the MultiInstanceTasks solution to execute the MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="02286-234">*Opcjonalne*: Użyj [portalu Azure] [ portal] lub [Explorer partii] [ batch_explorer] do sprawdzenia puli próbki, zadań i zadań (" MultiInstanceSamplePool","MultiInstanceSampleJob","MultiInstanceSampleTask") przed usunięciem zasobów.</span><span class="sxs-lookup"><span data-stu-id="02286-234">*Optional*: Use the [Azure portal][portal] or the [Batch Explorer][batch_explorer] to examine the sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete the resources.</span></span>

> [!TIP]
> <span data-ttu-id="02286-235">Możesz pobrać [Visual Studio Community] [ visual_studio] bezpłatnie, jeśli nie masz programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="02286-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="02286-236">Dane wyjściowe z `MultiInstanceTasks.exe` jest podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="02286-236">Output from `MultiInstanceTasks.exe` is similar to the following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] to job [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks to complete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="02286-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02286-237">Next steps</span></span>
* <span data-ttu-id="02286-238">W tym artykule omówiono Microsoft HPC & Azure partii Team blog [MPI obsługę systemu Linux na partii zadań Azure][blog_mpi_linux]oraz informacje na temat używania [OpenFOAM] [ openfoam] z partii.</span><span class="sxs-lookup"><span data-stu-id="02286-238">The Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="02286-239">Można znaleźć przykłady kodu języka Python dla [przykład OpenFOAM w serwisie GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="02286-239">You can find Python code samples for the [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="02286-240">Dowiedz się, jak [tworzenia pul węzły obliczeniowe Linux](batch-linux-nodes.md) do użycia w rozwiązań MPI usługi partia zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="02286-240">Learn how to [create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Informacje o wielu wystąpieniach"
