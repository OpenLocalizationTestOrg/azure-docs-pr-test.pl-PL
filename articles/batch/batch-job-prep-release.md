---
title: "Utwórz zadania przygotowanie zadania i zakończenie zadania na węzłach obliczeniowych - partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Użyj poziom zadania przygotowanie zadania, aby zminimalizować transfer danych w węzłach obliczeniowych partii zadań Azure, a następnie zwolnij zadania oczyszczania węzła po zakończeniu zadania."
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
ms.openlocfilehash: 6a2525c02ce7bd3969469d2e28a5fccc948f89b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="cc4b5-103">Uruchom zadanie przygotowanie i wersji zadania w partii węzły obliczeniowe</span><span class="sxs-lookup"><span data-stu-id="cc4b5-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="cc4b5-104">Zadanie usługi partia zadań Azure często wymaga pewnej formy instalacji, przed jego zadania są wykonywane, a po zadania konserwacji, po zakończeniu jego zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="cc4b5-105">Może być konieczne pobranie typowych zadań, danych wejściowych do węzłów obliczeniowych lub przekazać dane wyjściowe zadania do magazynu Azure po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-105">You might need to download common task input data to your compute nodes, or upload task output data to Azure Storage after the job completes.</span></span> <span data-ttu-id="cc4b5-106">Można użyć **zadania przygotowanie** i **zadania wersji** zadania do wykonania tych operacji.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-106">You can use **job preparation** and **job release** tasks to perform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="cc4b5-107">Co to są zadanie przygotowanie i zwolnij zadania?</span><span class="sxs-lookup"><span data-stu-id="cc4b5-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="cc4b5-108">Przed uruchomieniem zadania, zadanie przygotowanie zadania działa we wszystkich węzłach obliczeniowych zaplanowane co najmniej jedno zadanie.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-108">Before a job's tasks run, the job preparation task runs on all compute nodes scheduled to run at least one task.</span></span> <span data-ttu-id="cc4b5-109">Po zakończeniu zadania zadania Zwolnienie zadania działa na każdym węźle w puli, która jest wykonywana co najmniej jedno zadanie.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-109">Once the job is completed, the job release task runs on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="cc4b5-110">Podobnie jak w przypadku normalnych partii zadań, można określić w wierszu polecenia można wywołać podczas wykonywania zadania zadanie przygotowanie lub wersji.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-110">As with normal Batch tasks, you can specify a command line to be invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="cc4b5-111">Zadania przygotowania i wersji oferują znanych partii zadań funkcje, takie jak pobieranie pliku ([pliki zasobów][net_job_prep_resourcefiles]), z podwyższonym poziomem uprawnień wykonywania, zmienne środowiskowe niestandardowych wykonywania maksymalny czas trwania, liczbę ponownych prób i czas przechowywania pliku.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="cc4b5-112">W poniższych sekcjach omówiono sposób użycia [JobPreparationTask] [ net_job_prep] i [JobReleaseTask] [ net_job_release] klasy znalezione w [partiami platformy .NET] [ api_net] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-112">In the following sections, you'll learn how to use the [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in the [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="cc4b5-113">Przygotowanie i wersji zadania są szczególnie przydatne w środowiskach "udostępniania puli", w którym puli węzłów obliczeniowych będzie się powtarzał między uruchomionych zadań i jest używany przez wiele zadań.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-to-use-job-preparation-and-release-tasks"></a><span data-ttu-id="cc4b5-114">Kiedy zadanie przygotowanie i zwolnić zadania</span><span class="sxs-lookup"><span data-stu-id="cc4b5-114">When to use job preparation and release tasks</span></span>
<span data-ttu-id="cc4b5-115">Przygotowanie zadania i wersji zadania są świetnie sprawdza się w następujących sytuacjach:</span><span class="sxs-lookup"><span data-stu-id="cc4b5-115">Job preparation and job release tasks are a good fit for the following situations:</span></span>

<span data-ttu-id="cc4b5-116">**Pobierz dane typowe zadania**</span><span class="sxs-lookup"><span data-stu-id="cc4b5-116">**Download common task data**</span></span>

<span data-ttu-id="cc4b5-117">Zadania wsadowe często wymagają ze wspólnego zestawu danych jako dane wejściowe dla zadania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-117">Batch jobs often require a common set of data as input for the job's tasks.</span></span> <span data-ttu-id="cc4b5-118">Na przykład w obliczeniach codzienne analizy ryzyka, danych rynkowych jest określonych zadań, jeszcze wspólne dla wszystkich zadań w zadaniu.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-118">For example, in daily risk analysis calculations, market data is job-specific, yet common to all tasks in the job.</span></span> <span data-ttu-id="cc4b5-119">Tych danych rynkowych, rozmiar, często kilku gigabajtów powinien zostać pobrany w każdym węźle obliczeń tylko raz, aby można go używać dowolnego zadania w węźle.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-119">This market data, often several gigabytes in size, should be downloaded to each compute node only once so that any task that runs on the node can use it.</span></span> <span data-ttu-id="cc4b5-120">Użyj **zadanie przygotowanie zadania** do pobrania tych danych do każdego węzła przed wykonywanie zadania innych zadań.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-120">Use a **job preparation task** to download this data to each node before the execution of the job's other tasks.</span></span>

<span data-ttu-id="cc4b5-121">**Usuń dane wyjściowe poleceń i zadań**</span><span class="sxs-lookup"><span data-stu-id="cc4b5-121">**Delete job and task output**</span></span>

<span data-ttu-id="cc4b5-122">W środowisku "udostępniania puli", gdzie węzły obliczeniowe puli nie są wycofany z eksploatacji między zadaniami, może być konieczne usunięcie danych zadania między działa.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need to delete job data between runs.</span></span> <span data-ttu-id="cc4b5-123">Może być konieczne, co pozwala zaoszczędzić miejsce na dysku w węzłach lub spełnia zasady zabezpieczeń w organizacji.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-123">You might need to conserve disk space on the nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="cc4b5-124">Użyj **zadania Zwolnienie zadania** do usuwania danych, która została pobrana przez zadanie przygotowanie zadania lub generowane podczas wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-124">Use a **job release task** to delete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="cc4b5-125">**Przechowywanie dziennika**</span><span class="sxs-lookup"><span data-stu-id="cc4b5-125">**Log retention**</span></span>

<span data-ttu-id="cc4b5-126">Warto przechowywać kopię plików dziennika, które generują zadań lub może ulec awarii pliki zrzutu, które mogą być generowane przez aplikacje nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-126">You might want to keep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="cc4b5-127">Użyj **zadania Zwolnienie zadania** w takich przypadkach podczas kompresji i przekazywanie tych danych na [usługi Azure Storage] [ azure_storage] konta.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-127">Use a **job release task** in such cases to compress and upload this data to an [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="cc4b5-128">Inny sposób, aby utrwalić dzienniki i innych poleceń i zadań output danych jest użycie [konwencje pliku wsadowego Azure](batch-task-output.md) biblioteki.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-128">Another way to persist logs and other job and task output data is to use the [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="cc4b5-129">Zadanie przygotowanie zadania</span><span class="sxs-lookup"><span data-stu-id="cc4b5-129">Job preparation task</span></span>
<span data-ttu-id="cc4b5-130">Przed wykonaniem zadania wsadowego wykonuje zadanie przygotowanie zadania w każdym węźle obliczeń, który jest zaplanowane do uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-130">Before execution of a job's tasks, Batch executes the job preparation task on each compute node that is scheduled to run a task.</span></span> <span data-ttu-id="cc4b5-131">Domyślnie usługa partia zadań czeka na zadanie przygotowanie zadania należy wykonać przed uruchomieniem zadania zaplanowane do wykonania na węźle.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-131">By default, the Batch service waits for the job preparation task to be completed before running the tasks scheduled to execute on the node.</span></span> <span data-ttu-id="cc4b5-132">Można jednak skonfigurować usługę nie chcesz czekać.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-132">However, you can configure the service not to wait.</span></span> <span data-ttu-id="cc4b5-133">Jeśli węzeł zostanie uruchomiony ponownie, zostanie ponownie uruchomione zadanie przygotowanie zadania, ale można również wyłączyć to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-133">If the node restarts, the job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="cc4b5-134">Zadanie przygotowanie zadania jest wykonywane tylko w przypadku węzłów, które są zaplanowane do uruchomienia zadania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-134">The job preparation task is executed only on nodes that are scheduled to run a task.</span></span> <span data-ttu-id="cc4b5-135">Zapobiega to niepotrzebnych wykonywanie przygotowanie zadania, w przypadku, gdy węzeł nie jest przypisany zadania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-135">This prevents the unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="cc4b5-136">Taka sytuacja może wystąpić, gdy liczba zadań dla zadania jest mniejsza niż liczba węzłów w puli.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-136">This can occur when the number of tasks for a job is less than the number of nodes in a pool.</span></span> <span data-ttu-id="cc4b5-137">Ma również zastosowanie podczas [wykonywanie zadań jednoczesnych](batch-parallel-node-tasks.md) jest włączony, dlatego jeśli bezczynności niektóre węzły liczby zadań jest niższa niż całkowita liczba zadań jednoczesnych możliwe.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if the task count is lower than the total possible concurrent tasks.</span></span> <span data-ttu-id="cc4b5-138">Przez nie uruchomione zadanie przygotowanie zadania w węzłach bezczynności, możesz można kupować mniej opłat za transfer danych.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-138">By not running the job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="cc4b5-139">[JobPreparationTask] [ net_job_prep_cloudjob] różni się od [CloudPool.StartTask] [ pool_starttask] w tym JobPreparationTask wykonuje się na początku każdego zadania, natomiast StartTask wykonuje tylko wtedy, gdy węzeł obliczeniowy najpierw dołącza pulę lub ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at the start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="cc4b5-140">Zadanie zwolnienie zadania</span><span class="sxs-lookup"><span data-stu-id="cc4b5-140">Job release task</span></span>
<span data-ttu-id="cc4b5-141">Gdy zadanie jest oznaczony jako ukończone, zadanie zwolnienie zadania jest wykonywany w każdym węźle w puli, która jest wykonywana co najmniej jedno zadanie.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-141">Once a job is marked as completed, the job release task is executed on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="cc4b5-142">Zadania są oznaczone jako ukończone, wysyłając żądanie przerwania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="cc4b5-143">Następnie usługa partia zadań ustawia stan zadania na *przerywanie*kończy żadnych zadań aktywnych lub nie działają, skojarzone z zadaniem i uruchamia zadanie zwolnienie zadania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-143">The Batch service then sets the job state to *terminating*, terminates any active or running tasks associated with the job, and runs the job release task.</span></span> <span data-ttu-id="cc4b5-144">Zadanie zostaje następnie przeniesiona do *ukończone* stanu.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-144">The job then moves to the *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="cc4b5-145">Usuwanie zadania wykonuje również zadania Zwolnienie zadania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-145">Job deletion also executes the job release task.</span></span> <span data-ttu-id="cc4b5-146">Jednak jeśli zadanie zostało zakończone, zwolnienie zadania nie uruchomieniu po raz drugi Jeśli zadanie później zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-146">However, if a job has already been terminated, the release task is not run a second time if the job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="cc4b5-147">Zadania w środowisku przedprodukcyjnym i zwolnij zadania związane z partiami platformy .NET</span><span class="sxs-lookup"><span data-stu-id="cc4b5-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="cc4b5-148">Aby użyć zadania przygotowanie zadania, Przypisz [JobPreparationTask] [ net_job_prep] obiektu z zadania [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] właściwości.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-148">To use a job preparation task, assign a [JobPreparationTask][net_job_prep] object to your job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="cc4b5-149">Podobnie, zainicjować [JobReleaseTask] [ net_job_release] i przypisz go do Twojego zadania [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] właściwości można ustawić zadanie zwolnienie zadania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it to your job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property to set the job's release task.</span></span>

<span data-ttu-id="cc4b5-150">W poniższym przykładzie `myBatchClient` jest wystąpieniem [BatchClient][net_batch_client], i `myPool` jest istniejącej puli w ramach konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within the Batch account.</span></span>

```csharp
// Create the CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify the command lines for the job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign the job preparation task to the job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign the job release task to the job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="cc4b5-151">Jak wspomniano wcześniej, zwolnienie zadania jest wykonywany, gdy zadanie zostanie przerwane lub usunięty.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-151">As mentioned earlier, the release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="cc4b5-152">Zakończ zadanie z [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="cc4b5-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="cc4b5-153">Usuń zadanie o [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="cc4b5-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="cc4b5-154">Zwykle przerwanie lub usunąć zadania po zakończeniu jego zadań podrzędnych lub gdy został osiągnięty limit czasu, który został zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate the job to mark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="cc4b5-155">Przykładowy kod w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="cc4b5-155">Code sample on GitHub</span></span>
<span data-ttu-id="cc4b5-156">Zobacz Przygotowanie zadania i zwolnienie zadania w akcji, zapoznaj się [JobPrepRelease] [ job_prep_release_sample] przykładowy projekt w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-156">To see job preparation and release tasks in action, check out the [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="cc4b5-157">Ta aplikacja konsoli wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cc4b5-157">This console application does the following:</span></span>

1. <span data-ttu-id="cc4b5-158">Tworzona jest pula z dwoma węzłami "małe".</span><span class="sxs-lookup"><span data-stu-id="cc4b5-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="cc4b5-159">Tworzy zadanie przygotowanie zadania, wersji i zadań standardowych.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="cc4b5-160">Uruchamia zadanie przygotowanie zadania, który najpierw zapisuje identyfikator węzła do pliku tekstowego w katalogu "udostępniony" węzła.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-160">Runs the job preparation task, which first writes the node ID to a text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="cc4b5-161">Uruchamia zadanie, na każdym węźle, który zapisuje Identyfikatora zadania do tego samego pliku tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-161">Runs a task on each node that writes its task ID to the same text file.</span></span>
5. <span data-ttu-id="cc4b5-162">Po wykonaniu wszystkich zadań (lub osiągnięto limit czasu), wyświetla zawartość pliku tekstowego każdego węzła do konsoli.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-162">Once all tasks are completed (or the timeout is reached), prints the contents of each node's text file to the console.</span></span>
6. <span data-ttu-id="cc4b5-163">Po zakończeniu zadania uruchamia zadanie zwolnienie zadania do usunięcia pliku z węzła.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-163">When the job is completed, runs the job release task to delete the file from the node.</span></span>
7. <span data-ttu-id="cc4b5-164">Drukuje kodów zakończenia zadania przygotowanie i wersji zadań dla każdego węzła, na którym są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-164">Prints the exit codes of the job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="cc4b5-165">Wstrzymuje wykonywanie umożliwia potwierdzenie usunięcia zadania i/lub puli.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-165">Pauses execution to allow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="cc4b5-166">Dane wyjściowe z przykładowej aplikacji są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="cc4b5-166">Output from the sample application is similar to the following:</span></span>

```
Attempting to create pool: JobPrepReleaseSamplePool
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

Waiting for job JobPrepReleaseSampleJob to reach state Completed
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

Sample complete, hit ENTER to exit...
```

> [!NOTE]
> <span data-ttu-id="cc4b5-167">Z powodu zmiennej tworzenia i uruchamiania czasu węzłów w nowej puli (niektóre węzły są gotowe do zadań przed innymi) mogą pojawić się różne wyniki.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-167">Due to the variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="cc4b5-168">W szczególności ponieważ zadania są wykonywane szybko, jednym z węzłów w puli może wykonywać wszystkie zadania podrzędne zadania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-168">Specifically, because the tasks complete quickly, one of the pool's nodes may execute all of the job's tasks.</span></span> <span data-ttu-id="cc4b5-169">W takim przypadku można zauważyć, że zadanie przygotowywanie i wersji zadania nie istnieją dla węzła, który wykonać żadnych zadań.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-169">If this occurs, you will notice that the job prep and release tasks do not exist for the node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-the-azure-portal"></a><span data-ttu-id="cc4b5-170">Przejrzyj zadanie przygotowanie i wersji zadania w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cc4b5-170">Inspect job preparation and release tasks in the Azure portal</span></span>
<span data-ttu-id="cc4b5-171">Po uruchomieniu aplikacji przykładowej, można użyć [portalu Azure] [ portal] wyświetlania właściwości zadania i jego zadań podrzędnych i nawet pobierania pliku tekstowego udostępnionego, który jest modyfikowany przez zadania.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-171">When you run the sample application, you can use the [Azure portal][portal] to view the properties of the job and its tasks, or even download the shared text file that is modified by the job's tasks.</span></span>

<span data-ttu-id="cc4b5-172">Poniżej przedstawiono zrzut ekranu **przygotowanie zadania bloku** w portalu Azure po uruchomieniu aplikacji przykładowej.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-172">The screenshot below shows the **Preparation tasks blade** in the Azure portal after a run of the sample application.</span></span> <span data-ttu-id="cc4b5-173">Przejdź do *JobPrepReleaseSampleJob* właściwości po zakończeniu zadania (ale przed usunięciem zadania, a pula) i kliknij przycisk **zadań przygotowawczych** lub **wersji zadania** do przeglądania właściwości.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-173">Navigate to the *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** to view their properties.</span></span>

![Właściwości przygotowanie zadania w portalu Azure][1]

## <a name="next-steps"></a><span data-ttu-id="cc4b5-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc4b5-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="cc4b5-176">Pakiety aplikacji</span><span class="sxs-lookup"><span data-stu-id="cc4b5-176">Application packages</span></span>
<span data-ttu-id="cc4b5-177">Oprócz zadanie przygotowanie zadania, można również użyć [pakietów aplikacji](batch-application-packages.md) funkcji partii do przygotowania do wykonania zadań węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-177">In addition to the job preparation task, you can also use the [application packages](batch-application-packages.md) feature of Batch to prepare compute nodes for task execution.</span></span> <span data-ttu-id="cc4b5-178">Ta funkcja jest szczególnie przydatna w przypadku wdrażania aplikacji, które nie wymagają uruchomiony Instalator, aplikacje, które zawierają wiele plików (100 +) lub aplikacji, które wymagają kontroli wersji strict.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="cc4b5-179">Instalowanie aplikacji i danych na potrzeby przemieszczania</span><span class="sxs-lookup"><span data-stu-id="cc4b5-179">Installing applications and staging data</span></span>
<span data-ttu-id="cc4b5-180">Ten wpis na forum MSDN zawiera omówienie kilka metod przygotowywania węzły do uruchamiania zadań:</span><span class="sxs-lookup"><span data-stu-id="cc4b5-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="cc4b5-181">[Instalowanie aplikacji i danych na partii przemieszczania węzły obliczeniowe][forum_post]</span><span class="sxs-lookup"><span data-stu-id="cc4b5-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="cc4b5-182">Napisane przez jeden z członków zespołu partii zadań Azure, opisano kilka metod, co umożliwia wdrażanie aplikacji i danych, aby węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="cc4b5-182">Written by one of the Azure Batch team members, it discusses several techniques that you can use to deploy applications and data to compute nodes.</span></span>

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
