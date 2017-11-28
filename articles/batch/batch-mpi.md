---
title: "mająca wiele wystąpień aaaUse zadań toorun MPI aplikacje — partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak typ tooexecute komunikat interfejsu (Passing Interface) aplikacji za pomocą zadania o wielu wystąpieniach hello w partii zadań Azure."
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
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="0db9b-103">Korzystać z wielu wystąpień zadania toorun komunikat interfejsu (Passing Interface) aplikacji w trybie wsadowym</span><span class="sxs-lookup"><span data-stu-id="0db9b-103">Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="0db9b-104">Mająca wiele wystąpień zadań pozwalają toorun zadań partii zadań Azure na wielu węzłach obliczeniowych jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="0db9b-104">Multi-instance tasks allow you toorun an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="0db9b-105">Te zadania umożliwiają wysokiej wydajności obliczeniowej scenariuszy, takich jak aplikacje interfejsu Message (Passing) w partii.</span><span class="sxs-lookup"><span data-stu-id="0db9b-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="0db9b-106">W tym artykule dowiesz się, jak hello tooexecute wielu wystąpień zadania przy użyciu [partiami platformy .NET] [ api_net] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="0db9b-106">In this article, you learn how tooexecute multi-instance tasks using hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="0db9b-107">Przykłady hello w tym artykule dotyczą partiami platformy .NET, MS-MPI i węzły obliczeniowe systemu Windows, hello wielu wystąpień zadań omówione w tym miejscu są tooother odpowiednich platform i technologii (Python i Intel MPI w węzłach Linux, na przykład).</span><span class="sxs-lookup"><span data-stu-id="0db9b-107">While hello examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, hello multi-instance task concepts discussed here are applicable tooother platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="0db9b-108">Omówienie zadań wielu wystąpień</span><span class="sxs-lookup"><span data-stu-id="0db9b-108">Multi-instance task overview</span></span>
<span data-ttu-id="0db9b-109">W zadaniu wsadowym, każde zadanie jest zazwyczaj wykonywane na jednym węźle obliczeń — przesyłania zadania tooa wielu zadań, a hello usługa partia zadań harmonogramy poszczególnych zadań do wykonania w węźle.</span><span class="sxs-lookup"><span data-stu-id="0db9b-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks tooa job, and hello Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="0db9b-110">Jednakże, konfigurując zadania **ustawień wielu wystąpień**, poinformuj partii tooinstead utworzyć jedno zadanie podstawowego i kilka podzadań, które następnie są wykonywane na wielu węzłach.</span><span class="sxs-lookup"><span data-stu-id="0db9b-110">However, by configuring a task's **multi-instance settings**, you tell Batch tooinstead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="0db9b-111">![Omówienie zadań wielu wystąpień][1]</span><span class="sxs-lookup"><span data-stu-id="0db9b-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="0db9b-112">Po przesłaniu zadania o wielu wystąpieniach ustawienia tooa zadania wsadowego wykonuje kilka zadań unikatową toomulti kroki:</span><span class="sxs-lookup"><span data-stu-id="0db9b-112">When you submit a task with multi-instance settings tooa job, Batch performs several steps unique toomulti-instance tasks:</span></span>

1. <span data-ttu-id="0db9b-113">Tworzy Hello usługa partia zadań **głównej** i kilka **podzadania** na podstawie ustawień wielu wystąpieniach hello.</span><span class="sxs-lookup"><span data-stu-id="0db9b-113">hello Batch service creates one **primary** and several **subtasks** based on hello multi-instance settings.</span></span> <span data-ttu-id="0db9b-114">Hello łączna liczba zadań (podstawowym oraz wszystkie podzadania) jest zgodna liczbą hello **wystąpień** (węzły obliczeniowe) określonym w ustawieniach wielu wystąpieniach hello.</span><span class="sxs-lookup"><span data-stu-id="0db9b-114">hello total number of tasks (primary plus all subtasks) matches hello number of **instances** (compute nodes) you specify in hello multi-instance settings.</span></span>
2. <span data-ttu-id="0db9b-115">Partii określa jeden hello węzły obliczeniowe jako hello **wzorca**, i harmonogramy hello tooexecute głównym zadaniem hello wzorca.</span><span class="sxs-lookup"><span data-stu-id="0db9b-115">Batch designates one of hello compute nodes as hello **master**, and schedules hello primary task tooexecute on hello master.</span></span> <span data-ttu-id="0db9b-116">Planowana tooexecute podzadania hello na powitania pozostałej części hello obliczeń węzłów przydzielone toohello wielu wystąpień zadań, podzadanie jednej na każdy węzeł.</span><span class="sxs-lookup"><span data-stu-id="0db9b-116">It schedules hello subtasks tooexecute on hello remainder of hello compute nodes allocated toohello multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="0db9b-117">Hello głównej i wszystkich podzadań pobrać żadnej **wspólne pliki zasobów** określonymi w ustawieniach wielu wystąpieniach hello.</span><span class="sxs-lookup"><span data-stu-id="0db9b-117">hello primary and all subtasks download any **common resource files** you specify in hello multi-instance settings.</span></span>
4. <span data-ttu-id="0db9b-118">Po pobraniu hello wspólne pliki zasobów hello podstawowego i podzadania wykonania hello **polecenia koordynacji** określonymi w ustawieniach wielu wystąpieniach hello.</span><span class="sxs-lookup"><span data-stu-id="0db9b-118">After hello common resource files have been downloaded, hello primary and subtasks execute hello **coordination command** you specify in hello multi-instance settings.</span></span> <span data-ttu-id="0db9b-119">polecenie koordynacji Hello jest węzły tooprepare zwykle używane do wykonywania zadań hello.</span><span class="sxs-lookup"><span data-stu-id="0db9b-119">hello coordination command is typically used tooprepare nodes for executing hello task.</span></span> <span data-ttu-id="0db9b-120">Mogą to być uruchomienie usługi tła (takich jak [Microsoft MPI][msmpi_msdn]w `smpd.exe`) i sprawdzanie, czy węzły hello są gotowe tooprocess wiadomości między węzłami.</span><span class="sxs-lookup"><span data-stu-id="0db9b-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that hello nodes are ready tooprocess inter-node messages.</span></span>
5. <span data-ttu-id="0db9b-121">głównym zadaniem Hello wykonuje hello **polecenia aplikacji** w węźle głównym hello *po* pomyślnie wykonać polecenia koordynacji hello hello głównej i wszystkich podzadań.</span><span class="sxs-lookup"><span data-stu-id="0db9b-121">hello primary task executes hello **application command** on hello master node *after* hello coordination command has been completed successfully by hello primary and all subtasks.</span></span> <span data-ttu-id="0db9b-122">polecenie aplikacji Hello jest wiersz polecenia hello samo zadanie wielu wystąpieniach hello i jest wykonywane tylko przez hello głównym zadaniem.</span><span class="sxs-lookup"><span data-stu-id="0db9b-122">hello application command is hello command line of hello multi-instance task itself, and is executed only by hello primary task.</span></span> <span data-ttu-id="0db9b-123">W [MS-MPI][msmpi_msdn]— na podstawie rozwiązania, jest to, gdzie można wykonywać przy użyciu aplikacji obsługującej na MPI `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="0db9b-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="0db9b-124">Chociaż funkcjonalnie distinct, hello "wielu wystąpień zadania" nie jest typem unikatowy zadań takich jak hello [StartTask] [ net_starttask] lub [JobPreparationTask] [ net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="0db9b-124">Though it is functionally distinct, hello "multi-instance task" is not a unique task type like hello [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="0db9b-125">zadanie wielu wystąpieniach Hello jest po prostu standardowe zadania wsadowego ([CloudTask] [ net_task] w partiami platformy .NET) o wielu wystąpieniach ustawienia zostały skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="0db9b-125">hello multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="0db9b-126">W tym artykule określane toothis jako hello **wielu wystąpień zadań**.</span><span class="sxs-lookup"><span data-stu-id="0db9b-126">In this article, we refer toothis as hello **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="0db9b-127">Wymagania dotyczące zadań w wielu wystąpieniach</span><span class="sxs-lookup"><span data-stu-id="0db9b-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="0db9b-128">Mająca wiele wystąpień zadania wymagają z pulą **włączono komunikację między węzłami**oraz z **wykonywanie zadań jednoczesnych wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="0db9b-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="0db9b-129">wykonywanie zadań jednoczesnych toodisable, zestaw hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 właściwości.</span><span class="sxs-lookup"><span data-stu-id="0db9b-129">toodisable concurrent task execution, set hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property too1.</span></span>

<span data-ttu-id="0db9b-130">Następujący fragment kodu przedstawia sposób toocreate pulę dla wielu wystąpień zadań za pomocą hello biblioteki partiami platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="0db9b-130">This code snippet shows how toocreate a pool for multi-instance tasks using hello Batch .NET library.</span></span>

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
> <span data-ttu-id="0db9b-131">Jeśli spróbujesz toorun wyłączone zadania wielu wystąpień w puli z komunikacją między węzłami lub z *maxTasksPerNode* wartość większą niż 1, nie jest zaplanowane zadanie hello — zawsze pozostaje w stanie "active" hello.</span><span class="sxs-lookup"><span data-stu-id="0db9b-131">If you try toorun a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, hello task is never scheduled--it remains indefinitely in hello "active" state.</span></span> 
>
> <span data-ttu-id="0db9b-132">Mająca wiele wystąpień zadania mogą wykonywać tylko w przypadku węzłów w pulach utworzone po 14 grudnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="0db9b-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a><span data-ttu-id="0db9b-133">Użyj tooinstall StartTask MPI</span><span class="sxs-lookup"><span data-stu-id="0db9b-133">Use a StartTask tooinstall MPI</span></span>
<span data-ttu-id="0db9b-134">aplikacje MPI toorun o wielu wystąpieniach zadania, należy najpierw tooinstall implementacja MPI (MS-MPI lub MPI firmy Intel, na przykład) węzły obliczeniowe hello hello puli.</span><span class="sxs-lookup"><span data-stu-id="0db9b-134">toorun MPI applications with a multi-instance task, you first need tooinstall an MPI implementation (MS-MPI or Intel MPI, for example) on hello compute nodes in hello pool.</span></span> <span data-ttu-id="0db9b-135">Jest to toouse odpowiedni moment [StartTask][net_starttask], który wykonuje zawsze, gdy węzeł dołącza pulę lub ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="0db9b-135">This is a good time toouse a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="0db9b-136">Następujący fragment kodu tworzy StartTask, który określa pakiet instalacyjny hello MS-MPI jako [pliku zasobu][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="0db9b-136">This code snippet creates a StartTask that specifies hello MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="0db9b-137">Wiersz polecenia zadania uruchamiania Hello jest wykonywana po pliku zasobu hello jest węzłem toohello pobrany.</span><span class="sxs-lookup"><span data-stu-id="0db9b-137">hello start task's command line is executed after hello resource file is downloaded toohello node.</span></span> <span data-ttu-id="0db9b-138">W takim przypadku wiersza polecenia hello przeprowadza instalację nienadzorowaną MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="0db9b-138">In this case, hello command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="0db9b-139">Zdalny bezpośredni dostęp do pamięci (RDMA)</span><span class="sxs-lookup"><span data-stu-id="0db9b-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="0db9b-140">Po wybraniu [z funkcją RDMA rozmiar](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) takich jak A9 dla hello obliczeniowy węzłów w puli partii, aplikacja MPI można korzystać z platformy Azure wysokiej wydajności i małych opóźnieniach zdalnego pamięci bezpośredniego dostępu (do pamięci RDMA) sieci.</span><span class="sxs-lookup"><span data-stu-id="0db9b-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for hello compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="0db9b-141">Wyszukaj rozmiary hello określony jako "RDMA stanie" w hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="0db9b-141">Look for hello sizes specified as "RDMA capable" in hello following articles:</span></span>

* <span data-ttu-id="0db9b-142">**CloudServiceConfiguration** pule</span><span class="sxs-lookup"><span data-stu-id="0db9b-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="0db9b-143">[Rozmiary dla usług w chmurze](../cloud-services/cloud-services-sizes-specs.md) (tylko system Windows)</span><span class="sxs-lookup"><span data-stu-id="0db9b-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="0db9b-144">**VirtualMachineConfiguration** pule</span><span class="sxs-lookup"><span data-stu-id="0db9b-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="0db9b-145">[Rozmiary maszyn wirtualnych na platformie Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="0db9b-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="0db9b-146">[Rozmiary maszyn wirtualnych na platformie Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (system Windows)</span><span class="sxs-lookup"><span data-stu-id="0db9b-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="0db9b-147">Zaletą tootake RDMA na [węzły obliczeniowe Linux](batch-linux-nodes.md), należy użyć **Intel MPI** w węzłach hello.</span><span class="sxs-lookup"><span data-stu-id="0db9b-147">tootake advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on hello nodes.</span></span> <span data-ttu-id="0db9b-148">Aby uzyskać więcej informacji na CloudServiceConfiguration i VirtualMachineConfiguration pule, zobacz hello puli części hello [Przegląd funkcji partii](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="0db9b-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see hello Pool section of hello [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="0db9b-149">Utwórz zadanie wielu wystąpień z partiami platformy .NET</span><span class="sxs-lookup"><span data-stu-id="0db9b-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="0db9b-150">Teraz, kiedy możemy zostały objęte hello puli wymagania i instalacji pakietu MPI, Utwórzmy hello wielu wystąpień zadań.</span><span class="sxs-lookup"><span data-stu-id="0db9b-150">Now that we've covered hello pool requirements and MPI package installation, let's create hello multi-instance task.</span></span> <span data-ttu-id="0db9b-151">W tym fragmencie, utworzymy standard [CloudTask][net_task], skonfiguruj jego [MultiInstanceSettings] [ net_multiinstance_prop] właściwości.</span><span class="sxs-lookup"><span data-stu-id="0db9b-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="0db9b-152">Jak wspomniano wcześniej, hello wielu wystąpień zadań nie jest typem różne zadania, ale zadania wsadowego standardowego skonfigurowane przy użyciu ustawień wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="0db9b-152">As mentioned earlier, hello multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="0db9b-153">Podstawowe zadania i podzadania</span><span class="sxs-lookup"><span data-stu-id="0db9b-153">Primary task and subtasks</span></span>
<span data-ttu-id="0db9b-154">Podczas tworzenia hello ustawień wielu wystąpień dla tego zadania można określić numer hello węzłów obliczeniowych, które są tooexecute hello zadań.</span><span class="sxs-lookup"><span data-stu-id="0db9b-154">When you create hello multi-instance settings for a task, you specify hello number of compute nodes that are tooexecute hello task.</span></span> <span data-ttu-id="0db9b-155">Po przesłaniu zadania tooa zadań hello hello usługa partia zadań tworzy jeden **głównej** zadań i wystarczającą ilość **podzadania** razem spełniających hello liczba węzłów, można określić.</span><span class="sxs-lookup"><span data-stu-id="0db9b-155">When you submit hello task tooa job, hello Batch service creates one **primary** task and enough **subtasks** that together match hello number of nodes you specified.</span></span>

<span data-ttu-id="0db9b-156">Te zadania są przypisane liczbą całkowitą identyfikator hello zakresu od 0 za*numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="0db9b-156">These tasks are assigned an integer id in hello range of 0 too*numberOfInstances* - 1.</span></span> <span data-ttu-id="0db9b-157">Witaj zadania o identyfikatorze 0 jest głównym zadaniem hello i wszystkich innych identyfikatorów podzadania.</span><span class="sxs-lookup"><span data-stu-id="0db9b-157">hello task with id 0 is hello primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="0db9b-158">Na przykład jeśli tworzysz hello następujące ustawienia wielu wystąpień zadania hello głównym zadaniem będzie mieć identyfikator 0 i podzadania hello znajdują się identyfikatory 1 do 9.</span><span class="sxs-lookup"><span data-stu-id="0db9b-158">For example, if you create hello following multi-instance settings for a task, hello primary task would have an id of 0, and hello subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="0db9b-159">Węzła głównego</span><span class="sxs-lookup"><span data-stu-id="0db9b-159">Master node</span></span>
<span data-ttu-id="0db9b-160">Po przesłaniu zadania wielu wystąpień hello usługa partia zadań oznacza jedną hello węzły obliczeniowe jako węzeł "główny" hello, a harmonogramy hello tooexecute głównym zadaniem w węźle głównym hello.</span><span class="sxs-lookup"><span data-stu-id="0db9b-160">When you submit a multi-instance task, hello Batch service designates one of hello compute nodes as hello "master" node, and schedules hello primary task tooexecute on hello master node.</span></span> <span data-ttu-id="0db9b-161">podzadania Hello są zaplanowane tooexecute na powitania pozostałej części węzłów hello przydzielone toohello wielu wystąpień zadań.</span><span class="sxs-lookup"><span data-stu-id="0db9b-161">hello subtasks are scheduled tooexecute on hello remainder of hello nodes allocated toohello multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="0db9b-162">Polecenie koordynacji</span><span class="sxs-lookup"><span data-stu-id="0db9b-162">Coordination command</span></span>
<span data-ttu-id="0db9b-163">Witaj **polecenia koordynacji** jest wykonywana przez zarówno hello podstawowego, jak i podzadania.</span><span class="sxs-lookup"><span data-stu-id="0db9b-163">hello **coordination command** is executed by both hello primary and subtasks.</span></span>

<span data-ttu-id="0db9b-164">blokuje Hello wywołania polecenia koordynacji hello — partii nie wykonuj polecenia aplikacji hello aż polecenie koordynacji hello zwrócił pomyślnie dla wszystkich zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="0db9b-164">hello invocation of hello coordination command is blocking--Batch does not execute hello application command until hello coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="0db9b-165">polecenie koordynacji Hello powinny w związku z tym uruchomić wszystkie wymagane tła usługi, sprawdź, czy są gotowe do użycia, a następnie zamknij.</span><span class="sxs-lookup"><span data-stu-id="0db9b-165">hello coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="0db9b-166">Na przykład to polecenie koordynacji rozwiązania przy użyciu MS-MPI w wersji 7 uruchamia usługę SMPD hello w węźle hello, a następnie zamyka:</span><span class="sxs-lookup"><span data-stu-id="0db9b-166">For example, this coordination command for a solution using MS-MPI version 7 starts hello SMPD service on hello node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="0db9b-167">Należy zwrócić uwagę użycie hello `start` w tym poleceniu koordynacji.</span><span class="sxs-lookup"><span data-stu-id="0db9b-167">Note hello use of `start` in this coordination command.</span></span> <span data-ttu-id="0db9b-168">Jest to wymagane, ponieważ hello `smpd.exe` aplikacji nie może zwracać natychmiast po wykonaniu.</span><span class="sxs-lookup"><span data-stu-id="0db9b-168">This is required because hello `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="0db9b-169">Bez użycia hello hello [start] [ cmd_start] polecenia, to polecenie koordynacji nie zwróci i w związku z tym uniemożliwiają polecenia aplikacji hello uruchamianie.</span><span class="sxs-lookup"><span data-stu-id="0db9b-169">Without hello use of hello [start][cmd_start] command, this coordination command would not return, and would therefore block hello application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="0db9b-170">Polecenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0db9b-170">Application command</span></span>
<span data-ttu-id="0db9b-171">Po hello głównym zadaniem i wszystkie podzadania zostało ukończone, wykonując polecenie koordynacji hello, hello wielu wystąpień zadania wiersza polecenia jest wykonywana przez hello głównym zadaniem *tylko*.</span><span class="sxs-lookup"><span data-stu-id="0db9b-171">Once hello primary task and all subtasks have finished executing hello coordination command, hello multi-instance task's command line is executed by hello primary task *only*.</span></span> <span data-ttu-id="0db9b-172">Nazywamy to hello **polecenia aplikacji** toodistinguish z hello koordynacji polecenia.</span><span class="sxs-lookup"><span data-stu-id="0db9b-172">We call this hello **application command** toodistinguish it from hello coordination command.</span></span>

<span data-ttu-id="0db9b-173">W przypadku aplikacji MS MPI Użyj hello tooexecute polecenia aplikacji do aplikacji z obsługą MPI z `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="0db9b-173">For MS-MPI applications, use hello application command tooexecute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="0db9b-174">Na przykład poniżej przedstawiono polecenia aplikacji dotyczących rozwiązania przy użyciu MS-MPI w wersji 7:</span><span class="sxs-lookup"><span data-stu-id="0db9b-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="0db9b-175">Ponieważ MS MPI `mpiexec.exe` hello używa `CCP_NODES` zmiennej domyślnie (zobacz [zmiennych środowiskowych](#environment-variables)) przykład Witaj wykluczająca powyżej wiersza polecenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0db9b-175">Because MS-MPI's `mpiexec.exe` uses hello `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) hello example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="0db9b-176">Zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="0db9b-176">Environment variables</span></span>
<span data-ttu-id="0db9b-177">Tworzy kilka partii [zmiennych środowiskowych] [ msdn_env_var] zadania określonego wystąpienia toomulti na powitania obliczeniowe węzłów przydzielone tooa wielu wystąpień zadań.</span><span class="sxs-lookup"><span data-stu-id="0db9b-177">Batch creates several [environment variables][msdn_env_var] specific toomulti-instance tasks on hello compute nodes allocated tooa multi-instance task.</span></span> <span data-ttu-id="0db9b-178">Jak można hello skryptów i programów, które są one wykonywane wiersze polecenia koordynacji i aplikacji może się odwoływać zmienne środowiskowe.</span><span class="sxs-lookup"><span data-stu-id="0db9b-178">Your coordination and application command lines can reference these environment variables, as can hello scripts and programs they execute.</span></span>

<span data-ttu-id="0db9b-179">Witaj następujące zmienne środowiskowe są tworzone przez hello usługa partia zadań do użycia przez wiele wystąpień zadania:</span><span class="sxs-lookup"><span data-stu-id="0db9b-179">hello following environment variables are created by hello Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="0db9b-180">Aby uzyskać szczegółowe informacje o tych i hello Zobacz partii obliczeń węzła zmiennych środowiskowych, łącznie z ich zawartość i widoczność, [obliczeniowe zmiennych środowiskowych węzła][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="0db9b-180">For full details on these and hello other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="0db9b-181">Przykładowy kod partii Linux MPI Hello zawiera przykład sposobu niektóre zmienne środowiskowe użycia.</span><span class="sxs-lookup"><span data-stu-id="0db9b-181">hello Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="0db9b-182">Witaj [cmd koordynacji] [ coord_cmd_example] Bash skryptu pobiera typowych aplikacji i plików wejściowych z usługi Azure Storage, włącza udziału sieciowego systemu plików (NFS), w węźle głównym hello i konfiguruje hello innych węzłów przydzielony toohello wielu wystąpień zadań jako klienci systemu plików NFS.</span><span class="sxs-lookup"><span data-stu-id="0db9b-182">hello [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on hello master node, and configures hello other nodes allocated toohello multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="0db9b-183">Pliki zasobów</span><span class="sxs-lookup"><span data-stu-id="0db9b-183">Resource files</span></span>
<span data-ttu-id="0db9b-184">Istnieją dwa zestawy tooconsider plików zasobów dla zadań w wielu wystąpieniach: **wspólne pliki zasobów** który *wszystkie* zadania Pobierz (podstawowych i podzadania) i hello **pliki zasobów** określona dla hello wielu wystąpień zadań, które *tylko hello głównej* zadań pliki do pobrania.</span><span class="sxs-lookup"><span data-stu-id="0db9b-184">There are two sets of resource files tooconsider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and hello **resource files** specified for hello multi-instance task itself, which *only hello primary* task downloads.</span></span>

<span data-ttu-id="0db9b-185">Można określić jedną lub więcej **wspólne pliki zasobów** w ustawieniach wielu wystąpieniach hello zadania.</span><span class="sxs-lookup"><span data-stu-id="0db9b-185">You can specify one or more **common resource files** in hello multi-instance settings for a task.</span></span> <span data-ttu-id="0db9b-186">Te wspólne pliki zasobów są pobierane z [usługi Azure Storage](../storage/common/storage-introduction.md) w każdym węźle **zadań udostępnionego katalogu** hello głównej i wszystkich podzadań.</span><span class="sxs-lookup"><span data-stu-id="0db9b-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by hello primary and all subtasks.</span></span> <span data-ttu-id="0db9b-187">Witaj zadań udostępnionego katalogu mogą korzystać z aplikacji i koordynacji wierszy polecenia, za pomocą hello `AZ_BATCH_TASK_SHARED_DIR` zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="0db9b-187">You can access hello task shared directory from application and coordination command lines by using hello `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="0db9b-188">Witaj `AZ_BATCH_TASK_SHARED_DIR` jest taka sama w każdego węzła przydzielone toohello wielu wystąpień zadania, w związku z tym można udostępnić polecenie pojedynczego koordynacji między hello głównej i wszystkich podzadań.</span><span class="sxs-lookup"><span data-stu-id="0db9b-188">hello `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated toohello multi-instance task, thus you can share a single coordination command between hello primary and all subtasks.</span></span> <span data-ttu-id="0db9b-189">Partii nie "Udostępnij" hello katalog w znaczeniu dostępu zdalnego, ale można go użyć jako instalacji lub współużytkować punkt, jak wspomniano wcześniej w etykietce hello w zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="0db9b-189">Batch does not "share" hello directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in hello tip on environment variables.</span></span>

<span data-ttu-id="0db9b-190">Pliki zasobów, które określisz hello samo zadanie wielu wystąpieniach to katalog roboczy pobrany toohello zadań, `AZ_BATCH_TASK_WORKING_DIR`, domyślnie.</span><span class="sxs-lookup"><span data-stu-id="0db9b-190">Resource files that you specify for hello multi-instance task itself are downloaded toohello task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="0db9b-191">Jak wspomniano, z kolei toocommon pliki zasobów, tylko hello głównym zadaniem pobiera określone dla samo zadanie wielu wystąpieniach hello pliki zasobów.</span><span class="sxs-lookup"><span data-stu-id="0db9b-191">As mentioned, in contrast toocommon resource files, only hello primary task downloads resource files specified for hello  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0db9b-192">Zawsze używać zmiennych środowiskowych hello `AZ_BATCH_TASK_SHARED_DIR` i `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese katalogów w Twojej wiersze polecenia.</span><span class="sxs-lookup"><span data-stu-id="0db9b-192">Always use hello environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese directories in your command lines.</span></span> <span data-ttu-id="0db9b-193">Nie należy podejmować ścieżek hello tooconstruct ręcznie.</span><span class="sxs-lookup"><span data-stu-id="0db9b-193">Do not attempt tooconstruct hello paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="0db9b-194">Cykl życia zadania</span><span class="sxs-lookup"><span data-stu-id="0db9b-194">Task lifetime</span></span>
<span data-ttu-id="0db9b-195">okres istnienia Hello hello głównym zadaniem formanty hello okres istnienia hello całego wystąpienia wielu zadań.</span><span class="sxs-lookup"><span data-stu-id="0db9b-195">hello lifetime of hello primary task controls hello lifetime of hello entire multi-instance task.</span></span> <span data-ttu-id="0db9b-196">Gdy kończy hello podstawowy, wszystkie podzadania hello są zakończone.</span><span class="sxs-lookup"><span data-stu-id="0db9b-196">When hello primary exits, all of hello subtasks are terminated.</span></span> <span data-ttu-id="0db9b-197">Kod zakończenia Hello hello podstawowy jest kod zakończenia hello hello zadania i dlatego używane toodetermine hello powodzenie lub niepowodzenie zadań hello potrzeby ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="0db9b-197">hello exit code of hello primary is hello exit code of hello task, and is therefore used toodetermine hello success or failure of hello task for retry purposes.</span></span>

<span data-ttu-id="0db9b-198">W przypadku awarii dowolnego podzadania hello, został zakończony z kodem zwrotnym zera, na przykład hello całego wystąpienia wielu zadań kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="0db9b-198">If any of hello subtasks fail, exiting with a non-zero return code, for example, hello entire multi-instance task fails.</span></span> <span data-ttu-id="0db9b-199">zadanie wielu wystąpieniach Hello jest następnie zakończone i ponowione się tooits limit ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="0db9b-199">hello multi-instance task is then terminated and retried, up tooits retry limit.</span></span>

<span data-ttu-id="0db9b-200">Podczas usuwania zadania wielu wystąpieniach hello głównej i wszystkich podzadań są również usuwane przez hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="0db9b-200">When you delete a multi-instance task, hello primary and all subtasks are also deleted by hello Batch service.</span></span> <span data-ttu-id="0db9b-201">Podzadanie wszystkie katalogi i pliki są usuwane z węzłów obliczeniowych hello, podobnie jak w przypadku zadania standardowego.</span><span class="sxs-lookup"><span data-stu-id="0db9b-201">All subtask directories and their files are deleted from hello compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="0db9b-202">[TaskConstraints] [ net_taskconstraints] dla wielu wystąpień zadania, takie jak hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], i [RetentionTime] [ net_taskconstraint_retention] właściwości, są honorowane standardowe zadania, i Zastosuj toohello podstawowym i wszystkie podzadania.</span><span class="sxs-lookup"><span data-stu-id="0db9b-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply toohello primary and all subtasks.</span></span> <span data-ttu-id="0db9b-203">Jednak w przypadku zmiany hello [RetentionTime] [ net_taskconstraint_retention] właściwości po dodaniu hello wielu wystąpieniach toohello zadanie, ta zmiana jest stosowane tylko toohello głównym zadaniem.</span><span class="sxs-lookup"><span data-stu-id="0db9b-203">However, if you change hello [RetentionTime][net_taskconstraint_retention] property after adding hello multi-instance task toohello job, this change is applied only toohello primary task.</span></span> <span data-ttu-id="0db9b-204">Wszystkie podzadania hello kontynuować oryginalne hello toouse [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="0db9b-204">All of hello subtasks continue toouse hello original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="0db9b-205">Listy ostatnich zadań węźle obliczeń odzwierciedla hello identyfikator podzadaniem hello ostatnie zadanie było częścią zadań wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="0db9b-205">A compute node's recent task list reflects hello id of a subtask if hello recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="0db9b-206">Uzyskaj informacje na temat podzadania</span><span class="sxs-lookup"><span data-stu-id="0db9b-206">Obtain information about subtasks</span></span>
<span data-ttu-id="0db9b-207">informacje tooobtain podzadań przy użyciu biblioteki partiami platformy .NET hello, wywołanie hello [CloudTask.ListSubtasks] [ net_task_listsubtasks] metody.</span><span class="sxs-lookup"><span data-stu-id="0db9b-207">tooobtain information on subtasks by using hello Batch .NET library, call hello [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="0db9b-208">Ta metoda zwraca informacje o wszystkich zadań podrzędnych, a informacje o hello obliczeniowe węzła, który hello zadania wykonywane.</span><span class="sxs-lookup"><span data-stu-id="0db9b-208">This method returns information on all subtasks, and information about hello compute node that executed hello tasks.</span></span> <span data-ttu-id="0db9b-209">Z tych informacji można określić katalogu głównego każdego podzadania, identyfikator puli hello, jego bieżący stan i kod zakończenia.</span><span class="sxs-lookup"><span data-stu-id="0db9b-209">From this information, you can determine each subtask's root directory, hello pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="0db9b-210">Te informacje można użyć w połączeniu z hello [PoolOperations.GetNodeFile] [ poolops_getnodefile] podzadanie metody tooobtain hello plików.</span><span class="sxs-lookup"><span data-stu-id="0db9b-210">You can use this information in combination with hello [PoolOperations.GetNodeFile][poolops_getnodefile] method tooobtain hello subtask's files.</span></span> <span data-ttu-id="0db9b-211">Należy pamiętać, że ta metoda nie zwraca informacje o zadaniu głównej hello (identyfikator: 0).</span><span class="sxs-lookup"><span data-stu-id="0db9b-211">Note that this method does not return information for hello primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="0db9b-212">O ile nie określono inaczej, metody partiami platformy .NET, które pracują na hello wielu wystąpień [CloudTask] [ net_task] się zastosować *tylko* toohello głównym zadaniem.</span><span class="sxs-lookup"><span data-stu-id="0db9b-212">Unless otherwise stated, Batch .NET methods that operate on hello multi-instance [CloudTask][net_task] itself apply *only* toohello primary task.</span></span> <span data-ttu-id="0db9b-213">Na przykład, jeśli wywołasz hello [CloudTask.ListNodeFiles] [ net_task_listnodefiles] metody w wielu wystąpieniach zadania, zwracane są tylko pliki hello głównym zadaniem.</span><span class="sxs-lookup"><span data-stu-id="0db9b-213">For example, when you call hello [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only hello primary task's files are returned.</span></span>
>
>

<span data-ttu-id="0db9b-214">Witaj poniższy fragment kodu przedstawia sposób tooobtain podzadanie informacje, a także żądania zawartość pliku z węzłów hello, na których są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="0db9b-214">hello following code snippet shows how tooobtain subtask information, as well as request file contents from hello nodes on which they executed.</span></span>

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
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

## <a name="code-sample"></a><span data-ttu-id="0db9b-215">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="0db9b-215">Code sample</span></span>
<span data-ttu-id="0db9b-216">Witaj [MultiInstanceTasks] [ github_mpi] przykładowy kod w serwisie GitHub pokazano, jak toouse wielu wystąpień zadań toorun [MS-MPI] [ msmpi_msdn] Aplikacja w węzłach obliczeniowych partii.</span><span class="sxs-lookup"><span data-stu-id="0db9b-216">hello [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how toouse a multi-instance task toorun an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="0db9b-217">Wykonaj kroki hello w [przygotowania](#preparation) i [wykonywania](#execution) toorun hello próbki.</span><span class="sxs-lookup"><span data-stu-id="0db9b-217">Follow hello steps in [Preparation](#preparation) and [Execution](#execution) toorun hello sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="0db9b-218">Przygotowanie</span><span class="sxs-lookup"><span data-stu-id="0db9b-218">Preparation</span></span>
1. <span data-ttu-id="0db9b-219">Wykonaj kroki dwóch pierwszych hello w [jak toocompile i uruchomić proste program MS-MPI][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="0db9b-219">Follow hello first two steps in [How toocompile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="0db9b-220">To spełnia prerequesites hello na powitania po kroku.</span><span class="sxs-lookup"><span data-stu-id="0db9b-220">This satisfies hello prerequesites for hello following step.</span></span>
2. <span data-ttu-id="0db9b-221">Tworzenie *wersji* wersji hello [MPIHelloWorld] [ helloworld_proj] przykładowy program MPI.</span><span class="sxs-lookup"><span data-stu-id="0db9b-221">Build a *Release* version of hello [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="0db9b-222">To jest program hello, które będą uruchamiane w węzłach obliczeniowych hello wielu wystąpień zadań.</span><span class="sxs-lookup"><span data-stu-id="0db9b-222">This is hello program that will be run on compute nodes by hello multi-instance task.</span></span>
3. <span data-ttu-id="0db9b-223">Tworzenie pliku zip zawierającego `MPIHelloWorld.exe` (która będzie utworzony w kroku 2) i `MSMpiSetup.exe` (który został pobrany w kroku 1).</span><span class="sxs-lookup"><span data-stu-id="0db9b-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="0db9b-224">Ten plik zip będzie przekazać jako pakietu aplikacji w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="0db9b-224">You'll upload this zip file as an application package in hello next step.</span></span>
4. <span data-ttu-id="0db9b-225">Użyj hello [portalu Azure] [ portal] toocreate partii [aplikacji](batch-application-packages.md) o nazwie "MPIHelloWorld" i określ plik zip hello utworzony w poprzednim kroku hello jako wersji "1.0" pakiet aplikacji Hello.</span><span class="sxs-lookup"><span data-stu-id="0db9b-225">Use hello [Azure portal][portal] toocreate a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify hello zip file you created in hello previous step as version "1.0" of hello application package.</span></span> <span data-ttu-id="0db9b-226">Zobacz [przekazywanie aplikacji i zarządzanie nimi](batch-application-packages.md#upload-and-manage-applications) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="0db9b-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="0db9b-227">Tworzenie *wersji* wersji `MPIHelloWorld.exe` tak, aby tooinclude nie ma dodatkowe zależności (na przykład `msvcp140d.dll` lub `vcruntime140d.dll`) do pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0db9b-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have tooinclude any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="0db9b-228">Wykonanie</span><span class="sxs-lookup"><span data-stu-id="0db9b-228">Execution</span></span>
1. <span data-ttu-id="0db9b-229">Pobierz hello [azure partii próbek] [ github_samples_zip] z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="0db9b-229">Download hello [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="0db9b-230">Otwórz hello MultiInstanceTasks **rozwiązania** w programie Visual Studio 2015 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="0db9b-230">Open hello MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="0db9b-231">Witaj `MultiInstanceTasks.sln` plik rozwiązania znajduje się w:</span><span class="sxs-lookup"><span data-stu-id="0db9b-231">hello `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="0db9b-232">Wprowadź poświadczenia konta wsadowego i magazynowania w `AccountSettings.settings` w hello **Microsoft.Azure.Batch.Samples.Common** projektu.</span><span class="sxs-lookup"><span data-stu-id="0db9b-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in hello **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="0db9b-233">**Tworzenie i uruchamianie** hello MultiInstanceTasks rozwiązania tooexecute hello MPI aplikację przykładową na węzłach w puli partii obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="0db9b-233">**Build and run** hello MultiInstanceTasks solution tooexecute hello MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="0db9b-234">*Opcjonalne*: Użyj hello [portalu Azure] [ portal] lub hello [Explorer partii] [ batch_explorer] tooexamine hello próbki puli, zadania, i zadania ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask"), aby usunąć hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="0db9b-234">*Optional*: Use hello [Azure portal][portal] or hello [Batch Explorer][batch_explorer] tooexamine hello sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete hello resources.</span></span>

> [!TIP]
> <span data-ttu-id="0db9b-235">Możesz pobrać [Visual Studio Community] [ visual_studio] bezpłatnie, jeśli nie masz programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0db9b-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="0db9b-236">Dane wyjściowe z `MultiInstanceTasks.exe` podobne toohello następująco:</span><span class="sxs-lookup"><span data-stu-id="0db9b-236">Output from `MultiInstanceTasks.exe` is similar toohello following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

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

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="0db9b-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0db9b-237">Next steps</span></span>
* <span data-ttu-id="0db9b-238">w tym artykule omówiono Hello Microsoft HPC & Azure partii Team blog [MPI obsługę systemu Linux na partii zadań Azure][blog_mpi_linux]oraz informacje na temat używania [OpenFOAM] [ openfoam] z partii.</span><span class="sxs-lookup"><span data-stu-id="0db9b-238">hello Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="0db9b-239">Przykłady kodu dla języka Python można znaleźć hello [przykład OpenFOAM w serwisie GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="0db9b-239">You can find Python code samples for hello [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="0db9b-240">Dowiedz się, jak za[tworzenia pul węzły obliczeniowe Linux](batch-linux-nodes.md) do użycia w rozwiązań MPI usługi partia zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="0db9b-240">Learn how too[create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

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
