---
title: "aaaCreate zadań tooprepare zadania i zakończenie zadania na węzłach obliczeniowych - partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Użyj poziom zadania przygotowanie zadania toominimize danych przenieść węzłów obliczeniowych partii tooAzure i zwolnij zadania oczyszczania węzła po zakończeniu zadania."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="9b467-103">Uruchom zadanie przygotowanie i wersji zadania w partii węzły obliczeniowe</span><span class="sxs-lookup"><span data-stu-id="9b467-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="9b467-104">Zadanie usługi partia zadań Azure często wymaga pewnej formy instalacji, przed jego zadania są wykonywane, a po zadania konserwacji, po zakończeniu jego zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="9b467-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="9b467-105">Może być konieczne toodownload typowych zadań danych wejściowych tooyour węzły obliczeniowe lub Przekaż tooAzure danych wyjściowych zadania magazynu po zakończeniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="9b467-105">You might need toodownload common task input data tooyour compute nodes, or upload task output data tooAzure Storage after hello job completes.</span></span> <span data-ttu-id="9b467-106">Można użyć **zadania przygotowanie** i **zadania wersji** zadań tooperform te operacje.</span><span class="sxs-lookup"><span data-stu-id="9b467-106">You can use **job preparation** and **job release** tasks tooperform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="9b467-107">Co to są zadanie przygotowanie i zwolnij zadania?</span><span class="sxs-lookup"><span data-stu-id="9b467-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="9b467-108">Przed uruchomieniem zadania, hello zadanie przygotowanie zadania działa na wszystkich toorun zaplanowane węzły obliczeniowe co najmniej jedno zadanie.</span><span class="sxs-lookup"><span data-stu-id="9b467-108">Before a job's tasks run, hello job preparation task runs on all compute nodes scheduled toorun at least one task.</span></span> <span data-ttu-id="9b467-109">Po zakończeniu zadania hello hello zadania Zwolnienie zadania działa na każdym węźle puli hello wykonywane co najmniej jedno zadanie.</span><span class="sxs-lookup"><span data-stu-id="9b467-109">Once hello job is completed, hello job release task runs on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="9b467-110">Podobnie jak w przypadku normalnych partii zadań, możesz określić toobe wiersza polecenia, wywoływana, gdy zadanie przygotowanie lub wersji zadanie zostanie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="9b467-110">As with normal Batch tasks, you can specify a command line toobe invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="9b467-111">Zadania przygotowania i wersji oferują znanych partii zadań funkcje, takie jak pobieranie pliku ([pliki zasobów][net_job_prep_resourcefiles]), z podwyższonym poziomem uprawnień wykonywania, zmienne środowiskowe niestandardowych wykonywania maksymalny czas trwania, liczbę ponownych prób i czas przechowywania pliku.</span><span class="sxs-lookup"><span data-stu-id="9b467-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="9b467-112">W następujące sekcje hello, dowiesz się, jak toouse hello [JobPreparationTask] [ net_job_prep] i [JobReleaseTask] [ net_job_release] w hello znaleziono klas [Partiami platformy .NET] [ api_net] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="9b467-112">In hello following sections, you'll learn how toouse hello [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in hello [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="9b467-113">Przygotowanie i wersji zadania są szczególnie przydatne w środowiskach "udostępniania puli", w którym puli węzłów obliczeniowych będzie się powtarzał między uruchomionych zadań i jest używany przez wiele zadań.</span><span class="sxs-lookup"><span data-stu-id="9b467-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a><span data-ttu-id="9b467-114">Gdy toouse zadania przygotowanie i zwolnić zadania</span><span class="sxs-lookup"><span data-stu-id="9b467-114">When toouse job preparation and release tasks</span></span>
<span data-ttu-id="9b467-115">Przygotowanie zadania i wersji zadania są dobrze dla hello następujące sytuacje:</span><span class="sxs-lookup"><span data-stu-id="9b467-115">Job preparation and job release tasks are a good fit for hello following situations:</span></span>

<span data-ttu-id="9b467-116">**Pobierz dane typowe zadania**</span><span class="sxs-lookup"><span data-stu-id="9b467-116">**Download common task data**</span></span>

<span data-ttu-id="9b467-117">Zadania wsadowe często wymagają ze wspólnego zestawu danych jako dane wejściowe dla hello zadania.</span><span class="sxs-lookup"><span data-stu-id="9b467-117">Batch jobs often require a common set of data as input for hello job's tasks.</span></span> <span data-ttu-id="9b467-118">Na przykład codziennie obliczenia analizy ryzyka, danych rynkowych jest określonych zadań jeszcze typowych zadań tooall w zadaniu hello.</span><span class="sxs-lookup"><span data-stu-id="9b467-118">For example, in daily risk analysis calculations, market data is job-specific, yet common tooall tasks in hello job.</span></span> <span data-ttu-id="9b467-119">Tych danych rynkowych, rozmiar, często kilku gigabajtów należy węzeł obliczeniowy tooeach pobrane tylko raz, aby wszystkie zadania w węźle hello może być używany.</span><span class="sxs-lookup"><span data-stu-id="9b467-119">This market data, often several gigabytes in size, should be downloaded tooeach compute node only once so that any task that runs on hello node can use it.</span></span> <span data-ttu-id="9b467-120">Użyj **zadanie przygotowanie zadania** toodownload tego węzła tooeach danych przed hello wykonanie zadania hello innych zadań.</span><span class="sxs-lookup"><span data-stu-id="9b467-120">Use a **job preparation task** toodownload this data tooeach node before hello execution of hello job's other tasks.</span></span>

<span data-ttu-id="9b467-121">**Usuń dane wyjściowe poleceń i zadań**</span><span class="sxs-lookup"><span data-stu-id="9b467-121">**Delete job and task output**</span></span>

<span data-ttu-id="9b467-122">W środowisku "udostępniania puli", gdzie węzły obliczeniowe puli nie są wycofany z eksploatacji między zadaniami, może być konieczne danych zadania toodelete między działa.</span><span class="sxs-lookup"><span data-stu-id="9b467-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need toodelete job data between runs.</span></span> <span data-ttu-id="9b467-123">Może być konieczne tooconserve miejsce na węzłach hello lub spełnia zasady zabezpieczeń w organizacji.</span><span class="sxs-lookup"><span data-stu-id="9b467-123">You might need tooconserve disk space on hello nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="9b467-124">Użyj **zadania Zwolnienie zadania** toodelete danych, które zostało pobrane przez zadanie przygotowanie zadania lub wygenerowanych podczas wykonanie zadania.</span><span class="sxs-lookup"><span data-stu-id="9b467-124">Use a **job release task** toodelete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="9b467-125">**Przechowywanie dziennika**</span><span class="sxs-lookup"><span data-stu-id="9b467-125">**Log retention**</span></span>

<span data-ttu-id="9b467-126">Możesz tookeep kopię plików dziennika, które generują zadań lub być może pliki zrzutu awaryjnego, które mogą być generowane przez aplikacje nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="9b467-126">You might want tookeep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="9b467-127">Użyj **zadania Zwolnienie zadania** w takich przypadkach toocompress i przekazać ten tooan danych [usługi Azure Storage] [ azure_storage] konta.</span><span class="sxs-lookup"><span data-stu-id="9b467-127">Use a **job release task** in such cases toocompress and upload this data tooan [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="9b467-128">Inny sposób toopersist dzienniki i innych poleceń i zadań danych jest wyjściowy toouse hello [konwencje pliku wsadowego Azure](batch-task-output.md) biblioteki.</span><span class="sxs-lookup"><span data-stu-id="9b467-128">Another way toopersist logs and other job and task output data is toouse hello [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="9b467-129">Zadanie przygotowanie zadania</span><span class="sxs-lookup"><span data-stu-id="9b467-129">Job preparation task</span></span>
<span data-ttu-id="9b467-130">Przed wykonaniem zadania wsadowego wykonuje hello zadanie przygotowanie zadania w każdym węźle obliczeń, który jest toorun zaplanowanego zadania.</span><span class="sxs-lookup"><span data-stu-id="9b467-130">Before execution of a job's tasks, Batch executes hello job preparation task on each compute node that is scheduled toorun a task.</span></span> <span data-ttu-id="9b467-131">Domyślnie hello usługa partia zadań czeka na powitania zadanie przygotowanie zadania toobe wykonany przed uruchomieniem tooexecute zaplanowanego zadania hello w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="9b467-131">By default, hello Batch service waits for hello job preparation task toobe completed before running hello tasks scheduled tooexecute on hello node.</span></span> <span data-ttu-id="9b467-132">Można jednak skonfigurować usługi hello nie toowait.</span><span class="sxs-lookup"><span data-stu-id="9b467-132">However, you can configure hello service not toowait.</span></span> <span data-ttu-id="9b467-133">Jeśli ponowne uruchomienie węzła hello, hello zadanie przygotowanie zadania zostanie ponownie uruchomione, ale można również wyłączyć to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="9b467-133">If hello node restarts, hello job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="9b467-134">Witaj zadanie przygotowanie zadania jest wykonywany tylko na węzłach, które są toorun zaplanowanego zadania.</span><span class="sxs-lookup"><span data-stu-id="9b467-134">hello job preparation task is executed only on nodes that are scheduled toorun a task.</span></span> <span data-ttu-id="9b467-135">Zapobiega to hello niepotrzebnych wykonywanie przygotowanie zadania, w przypadku, gdy węzeł nie jest przypisany zadania.</span><span class="sxs-lookup"><span data-stu-id="9b467-135">This prevents hello unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="9b467-136">Taka sytuacja może wystąpić, gdy hello liczba zadań dla zadania jest mniejsza niż hello liczby węzłów w puli.</span><span class="sxs-lookup"><span data-stu-id="9b467-136">This can occur when hello number of tasks for a job is less than hello number of nodes in a pool.</span></span> <span data-ttu-id="9b467-137">Ma również zastosowanie podczas [wykonywanie zadań jednoczesnych](batch-parallel-node-tasks.md) jest włączone, jeśli liczba zadań hello jest niższa niż hello całkowita liczba zadań jednoczesnych możliwe niektóre węzły dlatego bezczynności.</span><span class="sxs-lookup"><span data-stu-id="9b467-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if hello task count is lower than hello total possible concurrent tasks.</span></span> <span data-ttu-id="9b467-138">Uruchamiając nie hello zadanie przygotowanie zadania w węzłach bezczynności, możesz można kupować mniej opłat za transfer danych.</span><span class="sxs-lookup"><span data-stu-id="9b467-138">By not running hello job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="9b467-139">[JobPreparationTask] [ net_job_prep_cloudjob] różni się od [CloudPool.StartTask] [ pool_starttask] w tym JobPreparationTask wykonuje na powitania na początku każdego zadania, natomiast StartTask wykonuje, tylko gdy węzeł obliczeniowy najpierw dołącza puli lub ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="9b467-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at hello start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="9b467-140">Zadanie zwolnienie zadania</span><span class="sxs-lookup"><span data-stu-id="9b467-140">Job release task</span></span>
<span data-ttu-id="9b467-141">Gdy zadanie zostanie oznaczone jako wykonane, hello zadania Zwolnienie zadania jest wykonywany w każdym węźle puli hello wykonywane co najmniej jedno zadanie.</span><span class="sxs-lookup"><span data-stu-id="9b467-141">Once a job is marked as completed, hello job release task is executed on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="9b467-142">Zadania są oznaczone jako ukończone, wysyłając żądanie przerwania.</span><span class="sxs-lookup"><span data-stu-id="9b467-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="9b467-143">Witaj usługa partia zadań, a następnie ustawia hello stanu zadania za*przerywanie*kończy żadnych zadań aktywnych lub nie działają, skojarzone z zadaniem hello i uruchamia hello zadania Zwolnienie zadania.</span><span class="sxs-lookup"><span data-stu-id="9b467-143">hello Batch service then sets hello job state too*terminating*, terminates any active or running tasks associated with hello job, and runs hello job release task.</span></span> <span data-ttu-id="9b467-144">zadanie Hello przenosi toohello *ukończone* stanu.</span><span class="sxs-lookup"><span data-stu-id="9b467-144">hello job then moves toohello *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="9b467-145">Usuwanie zadania wykonuje również hello zadania Zwolnienie zadania.</span><span class="sxs-lookup"><span data-stu-id="9b467-145">Job deletion also executes hello job release task.</span></span> <span data-ttu-id="9b467-146">Jednak jeśli zadanie zostało zakończone, hello zwolnienie zadania nie jest uruchamiane po raz drugi Jeśli zadanie hello później zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="9b467-146">However, if a job has already been terminated, hello release task is not run a second time if hello job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="9b467-147">Zadania w środowisku przedprodukcyjnym i zwolnij zadania związane z partiami platformy .NET</span><span class="sxs-lookup"><span data-stu-id="9b467-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="9b467-148">Przypisz toouse zadanie przygotowanie zadania, [JobPreparationTask] [ net_job_prep] zadania tooyour obiektów [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] właściwości .</span><span class="sxs-lookup"><span data-stu-id="9b467-148">toouse a job preparation task, assign a [JobPreparationTask][net_job_prep] object tooyour job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="9b467-149">Podobnie, zainicjować [JobReleaseTask] [ net_job_release] i przypisz mu zadania tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] hello tooset właściwości zadanie zwolnienie zadania.</span><span class="sxs-lookup"><span data-stu-id="9b467-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it tooyour job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property tooset hello job's release task.</span></span>

<span data-ttu-id="9b467-150">W poniższym przykładzie `myBatchClient` jest wystąpieniem [BatchClient][net_batch_client], i `myPool` jest istniejącej puli w ramach hello konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="9b467-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within hello Batch account.</span></span>

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="9b467-151">Jak wspomniano wcześniej, hello zwolnienie zadania jest wykonywany, gdy zadanie zostanie przerwane lub usunięty.</span><span class="sxs-lookup"><span data-stu-id="9b467-151">As mentioned earlier, hello release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="9b467-152">Zakończ zadanie z [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="9b467-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="9b467-153">Usuń zadanie o [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="9b467-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="9b467-154">Zwykle przerwanie lub usunąć zadania po zakończeniu jego zadań podrzędnych lub gdy został osiągnięty limit czasu, który został zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="9b467-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="9b467-155">Przykładowy kod w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="9b467-155">Code sample on GitHub</span></span>
<span data-ttu-id="9b467-156">toosee przygotowania i wersji zadania akcji, zapoznaj się z hello [JobPrepRelease] [ job_prep_release_sample] przykładowy projekt w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="9b467-156">toosee job preparation and release tasks in action, check out hello [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="9b467-157">Ta aplikacja konsoli hello następujące:</span><span class="sxs-lookup"><span data-stu-id="9b467-157">This console application does hello following:</span></span>

1. <span data-ttu-id="9b467-158">Tworzona jest pula z dwoma węzłami "małe".</span><span class="sxs-lookup"><span data-stu-id="9b467-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="9b467-159">Tworzy zadanie przygotowanie zadania, wersji i zadań standardowych.</span><span class="sxs-lookup"><span data-stu-id="9b467-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="9b467-160">Uruchamia hello zadanie przygotowanie zadania, który najpierw zapisuje plik tekstowy tooa identyfikator węzła hello w katalogu "udostępniony" węzła.</span><span class="sxs-lookup"><span data-stu-id="9b467-160">Runs hello job preparation task, which first writes hello node ID tooa text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="9b467-161">Uruchomienie zadania na każdym węźle, który zapisuje jego toohello identyfikator zadania tego samego pliku tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9b467-161">Runs a task on each node that writes its task ID toohello same text file.</span></span>
5. <span data-ttu-id="9b467-162">Po wykonaniu wszystkich zadań (lub osiągnięciu limitu czasu hello), drukuje zawartość hello każdego węzła tekstowego pliku toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="9b467-162">Once all tasks are completed (or hello timeout is reached), prints hello contents of each node's text file toohello console.</span></span>
6. <span data-ttu-id="9b467-163">Po zakończeniu zadania hello jest uruchamiane hello zadania zlecenia zadań toodelete hello pliku hello węzła.</span><span class="sxs-lookup"><span data-stu-id="9b467-163">When hello job is completed, runs hello job release task toodelete hello file from hello node.</span></span>
7. <span data-ttu-id="9b467-164">Drukuje hello kody hello zadanie przygotowanie zakończenia i zwolnij zadań dla każdego węzła, na którym są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="9b467-164">Prints hello exit codes of hello job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="9b467-165">Wstrzymuje wykonanie tooallow potwierdzenie usunięcia zadania i/lub puli.</span><span class="sxs-lookup"><span data-stu-id="9b467-165">Pauses execution tooallow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="9b467-166">Dane wyjściowe z aplikacji przykładowej hello jest podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9b467-166">Output from hello sample application is similar toohello following:</span></span>

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> <span data-ttu-id="9b467-167">Powodu toohello zmiennej tworzenia i czasu rozpoczęcia węzłów w nowej puli (niektóre węzły są gotowe do zadań przed innymi) mogą pojawić się różne wyniki.</span><span class="sxs-lookup"><span data-stu-id="9b467-167">Due toohello variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="9b467-168">W szczególności ponieważ zadania hello zakończył się szybko, jednym z węzłów hello puli może wykonywać wszystkie zadania hello zadania.</span><span class="sxs-lookup"><span data-stu-id="9b467-168">Specifically, because hello tasks complete quickly, one of hello pool's nodes may execute all of hello job's tasks.</span></span> <span data-ttu-id="9b467-169">W takim przypadku można zauważyć tego hello zadania przedprodukcyjnym i zwolnij zadania nie istnieją dla węzła hello, wykonywania żadnych zadań.</span><span class="sxs-lookup"><span data-stu-id="9b467-169">If this occurs, you will notice that hello job prep and release tasks do not exist for hello node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a><span data-ttu-id="9b467-170">Przejrzyj zadanie przygotowanie i zadania wersji w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9b467-170">Inspect job preparation and release tasks in hello Azure portal</span></span>
<span data-ttu-id="9b467-171">Po uruchomieniu hello przykładowej aplikacji, można użyć hello [portalu Azure] [ portal] tooview hello właściwości hello zadania i jego zadań, a nawet pobierać plik tekstowy udostępnionego hello jest modyfikowany przez hello zadania.</span><span class="sxs-lookup"><span data-stu-id="9b467-171">When you run hello sample application, you can use hello [Azure portal][portal] tooview hello properties of hello job and its tasks, or even download hello shared text file that is modified by hello job's tasks.</span></span>

<span data-ttu-id="9b467-172">Witaj Poniższy zrzut ekranu przedstawia hello **przygotowanie zadania bloku** w portalu Azure po uruchomieniu hello przykładowej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9b467-172">hello screenshot below shows hello **Preparation tasks blade** in hello Azure portal after a run of hello sample application.</span></span> <span data-ttu-id="9b467-173">Przejdź toohello *JobPrepReleaseSampleJob* właściwości po zakończeniu zadania (ale przed usunięciem zadania, a pula) i kliknij przycisk **zadań przygotowawczych** lub **wersji zadania** tooview ich właściwości.</span><span class="sxs-lookup"><span data-stu-id="9b467-173">Navigate toohello *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** tooview their properties.</span></span>

![Właściwości przygotowanie zadania w portalu Azure][1]

## <a name="next-steps"></a><span data-ttu-id="9b467-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9b467-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="9b467-176">Pakiety aplikacji</span><span class="sxs-lookup"><span data-stu-id="9b467-176">Application packages</span></span>
<span data-ttu-id="9b467-177">W dodatku toohello zadanie przygotowanie zadania umożliwia także hello [pakietów aplikacji](batch-application-packages.md) funkcji partii tooprepare obliczeniowe węzłów do wykonania zadania.</span><span class="sxs-lookup"><span data-stu-id="9b467-177">In addition toohello job preparation task, you can also use hello [application packages](batch-application-packages.md) feature of Batch tooprepare compute nodes for task execution.</span></span> <span data-ttu-id="9b467-178">Ta funkcja jest szczególnie przydatna w przypadku wdrażania aplikacji, które nie wymagają uruchomiony Instalator, aplikacje, które zawierają wiele plików (100 +) lub aplikacji, które wymagają kontroli wersji strict.</span><span class="sxs-lookup"><span data-stu-id="9b467-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="9b467-179">Instalowanie aplikacji i danych na potrzeby przemieszczania</span><span class="sxs-lookup"><span data-stu-id="9b467-179">Installing applications and staging data</span></span>
<span data-ttu-id="9b467-180">Ten wpis na forum MSDN zawiera omówienie kilka metod przygotowywania węzły do uruchamiania zadań:</span><span class="sxs-lookup"><span data-stu-id="9b467-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="9b467-181">[Instalowanie aplikacji i danych na partii przemieszczania węzły obliczeniowe][forum_post]</span><span class="sxs-lookup"><span data-stu-id="9b467-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="9b467-182">Napisane przez jeden z członków zespołu partii zadań Azure hello, omówiono kilka technik służy węzłów toocompute toodeploy aplikacji i danych.</span><span class="sxs-lookup"><span data-stu-id="9b467-182">Written by one of hello Azure Batch team members, it discusses several techniques that you can use toodeploy applications and data toocompute nodes.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
