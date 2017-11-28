---
title: "aaaPersist i zadań tooAzure magazynu z biblioteką konwencje plików hello danych wyjściowych dla platformy .NET — partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse biblioteki konwencje plików usługi partia zadań Azure dla platformy .NET toopersist partii zadań i tooAzure dane wyjściowe zadania magazynu i widoku hello utrwalone w danych wyjściowych w hello portalu Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a><span data-ttu-id="c9753-103">Utrwalanie zadań i zadań tooAzure danych magazynu z biblioteki konwencje pliku wsadowego hello .NET toopersist</span><span class="sxs-lookup"><span data-stu-id="c9753-103">Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="c9753-104">Dane zadania jednokierunkowej toopersist jest toouse hello [biblioteki konwencje plików usługi partia zadań Azure dla platformy .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="c9753-104">One way toopersist task data is toouse hello [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="c9753-105">Witaj biblioteki konwencje plików upraszcza proces hello przechowywania danych wyjściowych zadania tooAzure danych przechowywania i pobierania jej.</span><span class="sxs-lookup"><span data-stu-id="c9753-105">hello File Conventions library simplifies hello process of storing task output data tooAzure Storage and retrieving it.</span></span> <span data-ttu-id="c9753-106">Witaj konwencje plików biblioteki w kodzie zarówno zadania, jak i klienta można używać &mdash; w kodzie zadań utrwalanie plików, a w kliencie code toolist i pobrać je.</span><span class="sxs-lookup"><span data-stu-id="c9753-106">You can use hello File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code toolist and retrieve them.</span></span> <span data-ttu-id="c9753-107">Kod zadań można również użyć hello biblioteki tooretrieve hello dane wyjściowe zadania nadrzędnego, takich jak w [zadań zależności](batch-task-dependencies.md) scenariusza.</span><span class="sxs-lookup"><span data-stu-id="c9753-107">Your task code can also use hello library tooretrieve hello output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="c9753-108">pliki z biblioteki konwencje plików hello wyjściowe tooretrieve, wystawiając według Identyfikatora i celem można zlokalizować hello plików dla danego zadania lub zadania.</span><span class="sxs-lookup"><span data-stu-id="c9753-108">tooretrieve output files with hello File Conventions library, you can locate hello files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="c9753-109">Nie trzeba tooknow hello nazwy i lokalizacje plików hello.</span><span class="sxs-lookup"><span data-stu-id="c9753-109">You don't need tooknow hello names or locations of hello files.</span></span> <span data-ttu-id="c9753-110">Na przykład można użyć wszystkich plików pośrednich hello konwencje plików biblioteki toolist dla danego zadania lub Pobierz plik podglądu dla danego zadania.</span><span class="sxs-lookup"><span data-stu-id="c9753-110">For example, you can use hello File Conventions library toolist all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="c9753-111">Począwszy od wersji 2017-05-01, hello interfejsu API partii usługi obsługuje trwałych tooAzure danych wyjściowych magazynu dla zadań i zadania Menedżer zadania, które będą uruchamiane w pulach utworzone za pomocą hello konfiguracji maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c9753-111">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools created with hello virtual machine configuration.</span></span> <span data-ttu-id="c9753-112">Witaj interfejsu API partii usługi zawiera toopersist mówiąc w uproszczeniu, dane wyjściowe z kodem hello, tworzy zadanie, który służy jako alternatywne toohello konwencje plików biblioteki.</span><span class="sxs-lookup"><span data-stu-id="c9753-112">hello Batch service API provides a simple way toopersist output from within hello code that creates a task and serves as an alternative toohello File Conventions library.</span></span> <span data-ttu-id="c9753-113">Dane wyjściowe toopersist partii klienta aplikacji można modyfikować, bez konieczności aplikacji hello tooupdate, która działa zadania.</span><span class="sxs-lookup"><span data-stu-id="c9753-113">You can modify your Batch client applications toopersist output without needing tooupdate hello application that your task is running.</span></span> <span data-ttu-id="c9753-114">Aby uzyskać więcej informacji, zobacz [utrwalić tooAzure danych zadań magazynu z hello interfejsu API usługi partii](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="c9753-114">For more information, see [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a><span data-ttu-id="c9753-115">Kiedy używać danych wyjściowych zadania toopersist hello konwencje plik biblioteki?</span><span class="sxs-lookup"><span data-stu-id="c9753-115">When do I use hello File Conventions library toopersist task output?</span></span>

<span data-ttu-id="c9753-116">Partia zadań Azure zawiera więcej niż jednym ze sposobów toopersist dane wyjściowe zadania.</span><span class="sxs-lookup"><span data-stu-id="c9753-116">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="c9753-117">Witaj konwencje plików jest najlepiej nadaje się toothese scenariusze:</span><span class="sxs-lookup"><span data-stu-id="c9753-117">hello File Conventions is best suited toothese scenarios:</span></span>

- <span data-ttu-id="c9753-118">Można łatwo zmodyfikować hello kod aplikacji hello, że zadanie działa toopersist plików za pomocą hello konwencje plików biblioteki.</span><span class="sxs-lookup"><span data-stu-id="c9753-118">You can easily modify hello code for hello application that your task is running toopersist files using hello File Conventions library.</span></span>
- <span data-ttu-id="c9753-119">Podczas zadania hello jest nadal uruchomiona, które mają toostream tooAzure danych magazynu.</span><span class="sxs-lookup"><span data-stu-id="c9753-119">You want toostream data tooAzure Storage while hello task is still running.</span></span>
- <span data-ttu-id="c9753-120">Chcesz, aby dane toopersist z zestawów utworzonych za pomocą konfiguracji usługi w chmurze hello lub hello konfiguracji maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c9753-120">You want toopersist data from pools created with either hello cloud service configuration or hello virtual machine configuration.</span></span>
- <span data-ttu-id="c9753-121">Aplikacja kliencka lub innych zadań w hello zadania toolocate potrzeb, a pliki wyjściowe zadań za pomocą Identyfikatora lub w celu pobrania.</span><span class="sxs-lookup"><span data-stu-id="c9753-121">Your client application or other tasks in hello job needs toolocate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="c9753-122">Ma tooview dane wyjściowe zadania w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c9753-122">You want tooview task output in hello Azure portal.</span></span>

<span data-ttu-id="c9753-123">Jeśli scenariusz różni się od wymienione powyżej, może być konieczne tooconsider inny sposób.</span><span class="sxs-lookup"><span data-stu-id="c9753-123">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="c9753-124">Aby uzyskać więcej informacji dotyczących innych opcji trwałych danych wyjściowych zadania, zobacz [utrwalanie i zadań output tooAzure magazynu](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="c9753-124">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-hello-batch-file-conventions-standard"></a><span data-ttu-id="c9753-125">Co to jest hello standardowych konwencji pliku wsadowego?</span><span class="sxs-lookup"><span data-stu-id="c9753-125">What is hello Batch File Conventions standard?</span></span>

<span data-ttu-id="c9753-126">Witaj [standard konwencje pliku wsadowego](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) zawiera schemat nazewnictwa dla hello docelowego kontenerów i obiektów blob ścieżki toowhich zapisu plików wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c9753-126">hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for hello destination containers and blob paths toowhich your output files are written.</span></span> <span data-ttu-id="c9753-127">TooAzure utrwalonego plików magazynu, który odpowiednia toohello standardowej konwencji pliku są automatycznie dostępne do wyświetlenia w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c9753-127">Files persisted tooAzure Storage that adhere toohello File Conventions standard are automatically available for viewing in hello Azure portal.</span></span> <span data-ttu-id="c9753-128">Hello portal zna hello konwencji nazewnictwa i dlatego można wyświetlać pliki zgodnymi tooit.</span><span class="sxs-lookup"><span data-stu-id="c9753-128">hello portal is aware of hello naming convention and so can display files that adhere tooit.</span></span>

<span data-ttu-id="c9753-129">Hello konwencje plików biblioteki dla platformy .NET automatycznie nazwy kontenery magazynu, a pliki wyjściowe zadań zgodnie z toohello konwencje plików standardowych.</span><span class="sxs-lookup"><span data-stu-id="c9753-129">hello File Conventions library for .NET automatically names your storage containers and task output files according toohello File Conventions standard.</span></span> <span data-ttu-id="c9753-130">Hello konwencje plików biblioteki są także pliki wyjściowe tooquery metod w usłudze Azure Storage według Identyfikatora toojob, identyfikator zadania lub cel.</span><span class="sxs-lookup"><span data-stu-id="c9753-130">hello File Conventions library also provides methods tooquery output files in Azure Storage according toojob ID, task ID, or purpose.</span></span>   

<span data-ttu-id="c9753-131">Jeśli tworzysz języka innego niż .NET, można zaimplementować standard konwencje plików hello samodzielnie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9753-131">If you are developing with a language other than .NET, you can implement hello File Conventions standard yourself in your application.</span></span> <span data-ttu-id="c9753-132">Aby uzyskać więcej informacji, zobacz [temat standardowych konwencji pliku wsadowego hello](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="c9753-132">For more information, see [About hello Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a><span data-ttu-id="c9753-133">Łącze tooyour konta usługi Azure Storage konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="c9753-133">Link an Azure Storage account tooyour Batch account</span></span>

<span data-ttu-id="c9753-134">toopersist magazynu przy użyciu hello konwencje plik biblioteki, należy najpierw połączyć tooyour konta usługi Azure Storage konta usługi partia zadań tooAzure danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c9753-134">toopersist output data tooAzure Storage using hello File Conventions library, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="c9753-135">Jeśli jeszcze tego nie zrobiono tego wcześniej, łączenie tooyour konta magazynu konta usługi partia zadań za pomocą hello [portalu Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="c9753-135">If you haven't done so already, link a Storage account tooyour Batch account by using hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="c9753-136">Przejdź tooyour konta usługi partia zadań w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c9753-136">Navigate tooyour Batch account in hello Azure portal.</span></span> 
2. <span data-ttu-id="c9753-137">W obszarze **ustawienia**, wybierz pozycję **konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="c9753-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="c9753-138">Jeśli nie masz już konto magazynu skojarzonych z Twoim kontem usługi partia zadań, kliknij przycisk **konta magazynu, (Brak)**.</span><span class="sxs-lookup"><span data-stu-id="c9753-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="c9753-139">Wybierz konto magazynu z listy powitania dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c9753-139">Select a Storage account from hello list for your subscription.</span></span> <span data-ttu-id="c9753-140">Aby uzyskać najlepszą wydajność, należy użyć konta usługi Azure Storage, który znajduje się w hello tym samym regionie co hello konta usługi partia zadań, na którym są uruchomione zadania.</span><span class="sxs-lookup"><span data-stu-id="c9753-140">For best performance, use an Azure Storage account that is in hello same region as hello Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="c9753-141">Utrwalić danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="c9753-141">Persist output data</span></span>

<span data-ttu-id="c9753-142">toopersist i zadań wysyłania danych z biblioteką konwencje plików hello, utworzyć kontener w usłudze Azure Storage, a następnie zapisz hello dane wyjściowe toohello kontenera.</span><span class="sxs-lookup"><span data-stu-id="c9753-142">toopersist job and task output data with hello File Conventions library, create a container in Azure Storage, then save hello output toohello container.</span></span> <span data-ttu-id="c9753-143">Użyj hello [biblioteki klienta usługi Azure Storage dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage) w Twojej zadań kodu tooupload hello zadań dane wyjściowe toohello kontenerze.</span><span class="sxs-lookup"><span data-stu-id="c9753-143">Use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code tooupload hello task output toohello container.</span></span> 

<span data-ttu-id="c9753-144">Aby uzyskać więcej informacji na temat pracy z kontenerów i obiektów blob w magazynie Azure, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="c9753-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="c9753-145">Wszystkie dane wyjściowe poleceń i zadań utrwalone z konwencjami pliku hello biblioteki są przechowywane w samym kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="c9753-145">All job and task outputs persisted with hello File Conventions library are stored in hello same container.</span></span> <span data-ttu-id="c9753-146">Duża liczba zadań toopersist plików na powitania sam czas [magazynu ograniczenie](../storage/common/storage-performance-checklist.md#blobs) może wtedy zostać wymuszone.</span><span class="sxs-lookup"><span data-stu-id="c9753-146">If a large number of tasks try toopersist files at hello same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="c9753-147">Tworzenie kontenera magazynu</span><span class="sxs-lookup"><span data-stu-id="c9753-147">Create storage container</span></span>

<span data-ttu-id="c9753-148">tooAzure dane wyjściowe zadania toopersist magazynowania, najpierw utworzyć kontener wywołując [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="c9753-148">toopersist task output tooAzure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="c9753-149">Ta metoda rozszerzenia przyjmuje [CloudStorageAccount] [ net_cloudstorageaccount] obiektu jako parametr.</span><span class="sxs-lookup"><span data-stu-id="c9753-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="c9753-150">Tworzy kontener o nazwie zgodnie z toohello konwencje plików standard, tak aby jego zawartość jest wykrywalny przez hello Azure portal i hello metod pobierania omówione w dalszej części artykułu hello.</span><span class="sxs-lookup"><span data-stu-id="c9753-150">It creates a container named according toohello File Conventions standard,so that its contents are discoverable by hello Azure portal and hello retrieval methods discussed later in hello article.</span></span>

<span data-ttu-id="c9753-151">Zwykle umieścić toocreate kodu hello kontener w aplikacji klienta &mdash; hello aplikacji do tworzenia z puli, zadań i zadań.</span><span class="sxs-lookup"><span data-stu-id="c9753-151">You typically place hello code toocreate a container in your client application &mdash; hello application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="c9753-152">Zadanie magazynu danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="c9753-152">Store task outputs</span></span>

<span data-ttu-id="c9753-153">Teraz, gdy zostały przygotowane kontenera w magazynie Azure, zadania można zapisać danych wyjściowych toohello kontenera przy użyciu hello [TaskOutputStorage] [ net_taskoutputstorage] w bibliotece konwencje plików hello znaleziono klasy.</span><span class="sxs-lookup"><span data-stu-id="c9753-153">Now that you've prepared a container in Azure Storage, tasks can save output toohello container by using hello [TaskOutputStorage][net_taskoutputstorage] class found in hello File Conventions library.</span></span>

<span data-ttu-id="c9753-154">W kodzie zadań, należy najpierw utworzyć [TaskOutputStorage] [ net_taskoutputstorage] obiekt, a następnie po ukończeniu zadania hello pracy Wywołaj hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] toosave metody tooAzure jego dane wyjściowe magazynu.</span><span class="sxs-lookup"><span data-stu-id="c9753-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when hello task has completed its work, call hello [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method toosave its output tooAzure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="c9753-155">Witaj `kind` parametru hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) metody kategoryzuje hello utrwalone plików.</span><span class="sxs-lookup"><span data-stu-id="c9753-155">hello `kind` parameter of hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes hello persisted files.</span></span> <span data-ttu-id="c9753-156">Istnieją cztery wstępnie zdefiniowane [TaskOutputKind] [ net_taskoutputkind] typów: `TaskOutput`, `TaskPreview`, `TaskLog`, i `TaskIntermediate.` można również definiować niestandardowe kategorie danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c9753-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="c9753-157">Te typy danych wyjściowych pozwala toospecify, jakiego typu dane wyjściowe toolist później kwerendy partii dla hello utrwalone dane wyjściowe z danego zadania.</span><span class="sxs-lookup"><span data-stu-id="c9753-157">These output types allow you toospecify which type of outputs toolist when you later query Batch for hello persisted outputs of a given task.</span></span> <span data-ttu-id="c9753-158">Innymi słowy wśród wyjść hello zadania można filtrować listy hello na jeden z typów danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="c9753-158">In other words, when you list hello outputs for a task, you can filter hello list on one of hello output types.</span></span> <span data-ttu-id="c9753-159">Na przykład "Udostępnij hello *Podgląd* dane wyjściowe zadania *109*."</span><span class="sxs-lookup"><span data-stu-id="c9753-159">For example, "Give me hello *preview* output for task *109*."</span></span> <span data-ttu-id="c9753-160">Więcej informacji na temat wyświetlania i pobierania danych wyjściowych jest wyświetlana w [pobrać dane wyjściowe](#retrieve-output) dalszej części artykułu hello.</span><span class="sxs-lookup"><span data-stu-id="c9753-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in hello article.</span></span>

> [!TIP]
> <span data-ttu-id="c9753-161">Witaj rodzaj wyjścia decyduje również o którym w hello Azure portal określonego pliku pojawi się: *TaskOutput*-skategoryzowane pliki są wyświetlane w obszarze **pliki wyjściowe zadania**, i *TaskLog*pliki są wyświetlane w obszarze **zadań dzienniki**.</span><span class="sxs-lookup"><span data-stu-id="c9753-161">hello output kind also determines where in hello Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="c9753-162">Dane wyjściowe zadania magazynu</span><span class="sxs-lookup"><span data-stu-id="c9753-162">Store job outputs</span></span>

<span data-ttu-id="c9753-163">Ponadto wyniki zadań toostoring, można przechowywać dane wyjściowe hello skojarzone z zadaniem całego.</span><span class="sxs-lookup"><span data-stu-id="c9753-163">In addition toostoring task outputs, you can store hello outputs associated with an entire job.</span></span> <span data-ttu-id="c9753-164">Na przykład w zadaniu scalania hello zadania renderowania movie, można utrwalić filmu hello pełni renderowane jako dane wyjściowe zadania.</span><span class="sxs-lookup"><span data-stu-id="c9753-164">For example, in hello merge task of a movie rendering job, you could persist hello fully rendered movie as a job output.</span></span> <span data-ttu-id="c9753-165">Po zakończeniu zadania aplikacji klienta, można wyświetlić listę i pobrać dane wyjściowe hello hello zadania, a jest nie wymagają tooquery hello poszczególne zadania.</span><span class="sxs-lookup"><span data-stu-id="c9753-165">When your job is completed, your client application can list and retrieve hello outputs for hello job, and does not need tooquery hello individual tasks.</span></span>

<span data-ttu-id="c9753-166">Przechowywanie danych wyjściowych zadania przez wywołanie hello [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] metody, a następnie określ hello [JobOutputKind] [ net_joboutputkind] i nazwa pliku:</span><span class="sxs-lookup"><span data-stu-id="c9753-166">Store job output by calling hello [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify hello [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="c9753-167">Jak hello **TaskOutputKind** typu dla danych wyjściowych zadania, możesz użyć hello [JobOutputKind] [ net_joboutputkind] toocategorize typ zadania elementu utrwalone plików.</span><span class="sxs-lookup"><span data-stu-id="c9753-167">As with hello **TaskOutputKind** type for task outputs, you use hello [JobOutputKind][net_joboutputkind] type toocategorize a job's persisted files.</span></span> <span data-ttu-id="c9753-168">Ten parametr umożliwia toolater zapytanie dla określonego typu danych wyjściowych (lista).</span><span class="sxs-lookup"><span data-stu-id="c9753-168">This parameter allows you toolater query for (list) a specific type of output.</span></span> <span data-ttu-id="c9753-169">Witaj **JobOutputKind** typu kategoriami zarówno dane wyjściowe, jak i w wersji zapoznawczej i obsługuje tworzenie niestandardowych kategorii.</span><span class="sxs-lookup"><span data-stu-id="c9753-169">hello **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="c9753-170">Dzienniki zadania magazynu</span><span class="sxs-lookup"><span data-stu-id="c9753-170">Store task logs</span></span>

<span data-ttu-id="c9753-171">Ponadto toopersisting magazynu toodurable plików podczas zadania lub zadania wykonuje, może być konieczne toopersist pliki, które są aktualizowane podczas wykonywania zadania hello &mdash; pliki dziennika lub `stdout.txt` i `stderr.txt`, na przykład.</span><span class="sxs-lookup"><span data-stu-id="c9753-171">In addition toopersisting a file toodurable storage when a task or job completes, you may need toopersist files that are updated during hello execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="c9753-172">W tym celu hello biblioteki konwencje plików usługi partia zadań Azure udostępnia hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] metody.</span><span class="sxs-lookup"><span data-stu-id="c9753-172">For this purpose, hello Azure Batch File Conventions library provides hello [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="c9753-173">Z [SaveTrackedAsync][net_savetrackedasync], można śledzić pliku tooa aktualizacje w węźle hello (interwałem określonym przez użytkownika) i utrwalić tooAzure tych aktualizacji magazynu.</span><span class="sxs-lookup"><span data-stu-id="c9753-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates tooa file on hello node (at an interval that you specify) and persist those updates tooAzure Storage.</span></span>

<span data-ttu-id="c9753-174">W hello następującego fragmentu kodu, używamy [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` w usłudze Azure Storage co 15 s podczas wykonywania zadań hello hello:</span><span class="sxs-lookup"><span data-stu-id="c9753-174">In hello following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage every 15 seconds during hello execution of hello task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="c9753-175">Witaj oznaczone jako sekcji `Code tooprocess data and produce output file(s)` to symbol zastępczy hello kod, który przeprowadza się zwykle zadania.</span><span class="sxs-lookup"><span data-stu-id="c9753-175">hello commented section `Code tooprocess data and produce output file(s)` is a placeholder for hello code that your task would normally perform.</span></span> <span data-ttu-id="c9753-176">Na przykład może być kodu, który pobiera dane z usługi Azure Storage i wykonuje przekształcenie lub obliczeń na nim.</span><span class="sxs-lookup"><span data-stu-id="c9753-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="c9753-177">ważnym elementem Hello ta Wstawka kodu jest prezentacja jak może zawijać się taki kod w `using` tooperiodically bloku zaktualizować plik z [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="c9753-177">hello important part of this snippet is demonstrating how you can wrap such code in a `using` block tooperiodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="c9753-178">agent węzła Hello jest program, który jest uruchamiany na każdym węźle w puli hello i udostępnia interfejs polecenia i kontroli hello między węzłem hello a hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="c9753-178">hello node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="c9753-179">Witaj `Task.Delay` wywołanie jest wymagane na końcu hello to `using` tooensure bloku, który hello agenta węzła ma zawartość hello tooflush czas standardowy plik stdout.txt toohello w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="c9753-179">hello `Task.Delay` call is required at hello end of this `using` block tooensure that hello node agent has time tooflush hello contents of standard out toohello stdout.txt file on hello node.</span></span> <span data-ttu-id="c9753-180">Bez tego opóźnienia jest możliwe toomiss hello ostatniego kilka sekund w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c9753-180">Without this delay, it is possible toomiss hello last few seconds of output.</span></span> <span data-ttu-id="c9753-181">Tego opóźnienia nie może być wymagane dla wszystkich plików.</span><span class="sxs-lookup"><span data-stu-id="c9753-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="c9753-182">Po włączeniu pliku śledzenia z **SaveTrackedAsync**, tylko *dołącza* pliku śledzonych toohello są tooAzure utrwalonego magazynu.</span><span class="sxs-lookup"><span data-stu-id="c9753-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* toohello tracked file are persisted tooAzure Storage.</span></span> <span data-ttu-id="c9753-183">Ta metoda służy tylko do śledzenia-obracanie pliki dziennika lub innych plików, które zostały napisane toowith Dołącz toohello operacje na końcu pliku hello.</span><span class="sxs-lookup"><span data-stu-id="c9753-183">Use this method only for tracking non-rotating log files or other files that are written toowith append operations toohello end of hello file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="c9753-184">Pobieranie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="c9753-184">Retrieve output data</span></span>

<span data-ttu-id="c9753-185">Podczas pobierania danych wyjściowych utrwalonego za pomocą biblioteki konwencje pliku wsadowego Azure hello, w tym zadań i zadania skoncentrowane na sposób.</span><span class="sxs-lookup"><span data-stu-id="c9753-185">When you retrieve your persisted output using hello Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="c9753-186">Użytkownik może prosić o hello wyjściowe dla danego zadania lub zadania bez konieczności tooknow ścieżki w usłudze Azure Storage lub nawet jego nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="c9753-186">You can request hello output for given task or job without needing tooknow its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="c9753-187">Zamiast tego można zażądać plików wyjściowych przez zadanie lub zadania identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="c9753-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="c9753-188">Hello poniższy fragment kodu iteruje zadania, niektóre informacje na temat plików wyjściowych hello hello zadania drukowania i pobiera pliki z magazynu.</span><span class="sxs-lookup"><span data-stu-id="c9753-188">hello following code snippet iterates through a job's tasks, prints some information about hello output files for hello task, and then downloads its files from Storage.</span></span>

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a><span data-ttu-id="c9753-189">Pliki wyjściowe widoku w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c9753-189">View output files in hello Azure portal</span></span>

<span data-ttu-id="c9753-190">Witaj portalu Azure Wyświetla pliki wyjściowe zadań i dzienników, które są trwałe tooa połączone konta magazynu platformy Azure przy użyciu hello [standard konwencje pliku wsadowego](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="c9753-190">hello Azure portal displays task output files and logs that are persisted tooa linked Azure Storage account using hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="c9753-191">Można zaimplementować te konwencje samodzielnie hello preferowanego języka lub hello konwencje plików biblioteki można używać w aplikacji platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="c9753-191">You can implement these conventions yourself in hello a language of your choice, or you can use hello File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="c9753-192">tooenable hello wyświetlania plików wyjściowych w portalu hello, musi spełniać następujące wymagania hello:</span><span class="sxs-lookup"><span data-stu-id="c9753-192">tooenable hello display of your output files in hello portal, you must satisfy hello following requirements:</span></span>

1. <span data-ttu-id="c9753-193">[Łączenie konta usługi Azure Storage](#requirement-linked-storage-account) tooyour konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="c9753-193">[Link an Azure Storage account](#requirement-linked-storage-account) tooyour Batch account.</span></span>
2. <span data-ttu-id="c9753-194">Odpowiednia toohello wstępnie zdefiniowane konwencje nazewnictwa dla plików i kontenery magazynu podczas przechowywanie danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c9753-194">Adhere toohello predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="c9753-195">Można znaleźć definicji hello tych konwencji w hello konwencje plików biblioteki [README][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="c9753-195">You can find hello definition of these conventions in hello File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="c9753-196">Jeśli używasz hello [konwencje plików usługi partia zadań Azure] [ nuget_package] toopersist biblioteki z danych wyjściowych, pliki są zachowywane zgodnie z toohello standardowej konwencji pliku.</span><span class="sxs-lookup"><span data-stu-id="c9753-196">If you use hello [Azure Batch File Conventions][nuget_package] library toopersist your output, your files are persisted according toohello File Conventions standard.</span></span>

<span data-ttu-id="c9753-197">dane wyjściowe zadania tooview pliki i loguje hello portalu Azure, przejdź toohello zadań, której wyjście myślisz, następnie kliknij opcję **zapisane pliki wyjściowe** lub **zapisane dzienniki**.</span><span class="sxs-lookup"><span data-stu-id="c9753-197">tooview task output files and logs in hello Azure portal, navigate toohello task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="c9753-198">Ten obraz zawiera hello **zapisane pliki wyjściowe** hello zadania o identyfikatorze "007":</span><span class="sxs-lookup"><span data-stu-id="c9753-198">This image shows hello **Saved output files** for hello task with ID "007":</span></span>

<span data-ttu-id="c9753-199">![Wyniki zadań bloku w hello portalu Azure][2]</span><span class="sxs-lookup"><span data-stu-id="c9753-199">![Task outputs blade in hello Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="c9753-200">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="c9753-200">Code sample</span></span>

<span data-ttu-id="c9753-201">Witaj [PersistOutputs] [ github_persistoutputs] przykładowy projekt jest jednym z hello [przykłady kodu partii zadań Azure] [ github_samples] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9753-201">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="c9753-202">To rozwiązanie Visual Studio pokazano, jak toouse hello Azure partii pliku konwencje biblioteki toopersist zadań output toodurable magazynu.</span><span class="sxs-lookup"><span data-stu-id="c9753-202">This Visual Studio solution demonstrates how toouse hello Azure Batch File Conventions library toopersist task output toodurable storage.</span></span> <span data-ttu-id="c9753-203">Witaj toorun przykładowe, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c9753-203">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="c9753-204">Witaj Otwórz projekt w **programu Visual Studio 2015 lub nowsza**.</span><span class="sxs-lookup"><span data-stu-id="c9753-204">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="c9753-205">Dodaj wsadowego i magazynowania **poświadczenia konta** za**AccountSettings.settings** w projekcie Microsoft.Azure.Batch.Samples.Common hello.</span><span class="sxs-lookup"><span data-stu-id="c9753-205">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="c9753-206">**Tworzenie** (ale nie jest uruchomiony) hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c9753-206">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="c9753-207">Jeśli zostanie wyświetlony monit, należy przywrócić wszystkie pakiety NuGet.</span><span class="sxs-lookup"><span data-stu-id="c9753-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="c9753-208">Użyj hello Azure portalu tooupload [pakiet aplikacji](batch-application-packages.md) dla **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="c9753-208">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="c9753-209">Zawierają hello `PersistOutputsTask.exe` i jego zestawów zależnych hello zip pakietu, identyfikator aplikacji hello zestawu zbyt wersja pakietu "PersistOutputsTask" i aplikacji hello zbyt "1.0".</span><span class="sxs-lookup"><span data-stu-id="c9753-209">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="c9753-210">**Uruchom** (Uruchom) hello **PersistOutputs** projektu.</span><span class="sxs-lookup"><span data-stu-id="c9753-210">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="c9753-211">Gdy zostanie wyświetlony monit o toochoose hello trwałości technologii toouse dla uruchomionego hello próbki, wprowadź **1** próbki hello toorun przy użyciu danych wyjściowych zadania toopersist hello konwencje plików biblioteki.</span><span class="sxs-lookup"><span data-stu-id="c9753-211">When prompted toochoose hello persistence technology toouse for running hello sample, enter **1** toorun hello sample using hello File Conventions library toopersist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c9753-212">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c9753-212">Next steps</span></span>

### <a name="get-hello-batch-file-conventions-library-for-net"></a><span data-ttu-id="c9753-213">Pobierz hello konwencje pliku wsadowego biblioteki dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="c9753-213">Get hello Batch File Conventions library for .NET</span></span>

<span data-ttu-id="c9753-214">Biblioteka konwencje pliku wsadowego powitania dla platformy .NET jest dostępna na [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="c9753-214">hello Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="c9753-215">Biblioteka Hello rozszerza hello [CloudJob] [ net_cloudjob] i [CloudTask] [ net_cloudtask] klas z nowych metod.</span><span class="sxs-lookup"><span data-stu-id="c9753-215">hello library extends hello [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="c9753-216">Zobacz też hello [odwołania dokumentacji](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) hello konwencje plików biblioteki.</span><span class="sxs-lookup"><span data-stu-id="c9753-216">Also see hello [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for hello File Conventions library.</span></span>

<span data-ttu-id="c9753-217">Witaj [kod źródłowy] [ github_file_conventions] hello konwencje plików biblioteki są dostępne w serwisie GitHub w hello Microsoft Azure SDK dla platformy .NET repozytorium.</span><span class="sxs-lookup"><span data-stu-id="c9753-217">hello [source code][github_file_conventions] for hello File Conventions library is available on GitHub in hello Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="c9753-218">Eksploruj inne podejścia trwałych danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="c9753-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="c9753-219">Zobacz [utrwalanie i zadań output tooAzure magazynu](batch-task-output.md) omówienie trwałych danych zadań i zadania.</span><span class="sxs-lookup"><span data-stu-id="c9753-219">See [Persist job and task output tooAzure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="c9753-220">Zobacz [utrwalić tooAzure danych zadań magazynu z hello interfejsu API usługi partii](batch-task-output-files.md) toolearn jak toopersist hello interfejsu API usługi partii toouse dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c9753-220">See [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md) toolearn how toouse hello Batch service API toopersist output data.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Pliki wyjściowe zapisane i zapisane dzienniki selektory w portalu"
[2]: ./media/batch-task-output/task-output-02.png "Wyniki zadań bloku w hello portalu Azure"
