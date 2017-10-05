---
title: "Samouczek — korzystanie z biblioteki klienta usługi Azure Batch dla programu .NET | Microsoft Docs"
description: "Podstawowe pojęcia dotyczące usługi Azure Batch i tworzenie prostego rozwiązania przy użyciu platformy .NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf8fdca51a6a4ad1b7cd4fe6980543199f6b36e0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-building-solutions-with-the-batch-client-library-for-net"></a><span data-ttu-id="9ddc0-103">Rozpoczynanie tworzenia rozwiązań za pomocą biblioteki klienta usługi Batch dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="9ddc0-103">Get started building solutions with the Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ddc0-104">.NET</span><span class="sxs-lookup"><span data-stu-id="9ddc0-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="9ddc0-105">Python</span><span class="sxs-lookup"><span data-stu-id="9ddc0-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="9ddc0-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="9ddc0-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="9ddc0-107">W tym artykule omawiamy podstawy usługi [Azure Batch][azure_batch] i biblioteki [Batch .NET][net_api] na podstawie przykładowej aplikacji w języku C#.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-107">Learn the basics of [Azure Batch][azure_batch] and the [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="9ddc0-108">Wyjaśniamy, jak przykładowa aplikacja korzysta z usługi Batch do przetwarzania równoległego obciążenia w chmurze oraz współpracuje z usługą [Azure Storage](../storage/common/storage-introduction.md) w celu przygotowania i pobrania plików.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-108">We look at how the sample application leverages the Batch service to process a parallel workload in the cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="9ddc0-109">Przedstawiono tu typowy przepływ pracy w aplikacji usługi Batch oraz wyjaśniono podstawowe zagadnienia dotyczące najważniejszych składników usługi Batch, np. zadań, podzadań, pul i węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-109">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="9ddc0-110">![Przepływ pracy rozwiązania w usłudze Batch (podstawowy)][11]</span><span class="sxs-lookup"><span data-stu-id="9ddc0-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="9ddc0-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9ddc0-111">Prerequisites</span></span>
<span data-ttu-id="9ddc0-112">W tym artykule założono, że masz praktyczną wiedzę na temat języka C# i programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="9ddc0-113">Przyjęto również założenie, że jesteś w stanie spełnić wymagania dotyczące tworzenia konta, które zostały wyszczególnione poniżej dla platformy Azure oraz usług Batch i Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-113">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="9ddc0-114">Konta</span><span class="sxs-lookup"><span data-stu-id="9ddc0-114">Accounts</span></span>
* <span data-ttu-id="9ddc0-115">**Konto platformy Azure**: jeśli nie masz jeszcze subskrypcji platformy Azure, [utwórz bezpłatne konto platformy Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="9ddc0-116">**Konto usługi Batch**: po uzyskaniu subskrypcji platformy Azure [utwórz konto usługi Azure Batch](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="9ddc0-117">**Konto magazynu**: zobacz sekcję [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) w temacie [Informacje o kontach magazynu Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ddc0-118">Usługa Batch obsługuje obecnie *tylko* typ konta magazynu **ogólnego przeznaczenia**, zgodnie z opisem w kroku 5 [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) w temacie [Informacje o kontach magazynu Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-118">Batch currently supports *only* the **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="9ddc0-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9ddc0-119">Visual Studio</span></span>
<span data-ttu-id="9ddc0-120">Do utworzenia przykładowego projektu potrzebny jest program **Visual Studio 2015 lub nowszy**.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-120">You must have **Visual Studio 2015 or newer** to build the sample project.</span></span> <span data-ttu-id="9ddc0-121">Bezpłatne i próbne wersje programu Visual Studio można znaleźć w [omówieniu produktów Visual Studio][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-121">You can find free and trial versions of Visual Studio in the [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="9ddc0-122">Przykład kodu *DotNetTutorial*</span><span class="sxs-lookup"><span data-stu-id="9ddc0-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="9ddc0-123">[DotNetTutorial][github_dotnettutorial] to jeden z wielu przykładów kodu usługi Batch w repozytorium [azure-batch-samples][github_samples] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-123">The [DotNetTutorial][github_dotnettutorial] sample is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="9ddc0-124">Możesz pobrać wszystkie przykłady, klikając przycisk **Clone or download > Download ZIP** (Sklonuj lub pobierz > Pobierz plik ZIP) na stronie głównej repozytorium lub klikając bezpośredni link pobierania pliku [azure-batch-samples-master.zip][github_samples_zip].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-124">You can download all the samples by clicking  **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="9ddc0-125">Po wyodrębnieniu zawartości pliku ZIP rozwiązanie można znaleźć w następującym folderze:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-125">Once you've extracted the contents of the ZIP file, you can find the solution in the following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="9ddc0-126">Azure Batch Explorer (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="9ddc0-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="9ddc0-127">[Azure Batch Explorer][github_batchexplorer] to bezpłatne narzędzie, które znajduje się w repozytorium [azure-batch-samples][github_samples] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-127">The [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="9ddc0-128">Chociaż nie jest wymagane do ukończenia tego samouczka, może przydać się podczas tworzenia i debugowania rozwiązań w usłudze Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-128">While not required to complete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="9ddc0-129">Omówienie przykładowego projektu DotNetTutorial</span><span class="sxs-lookup"><span data-stu-id="9ddc0-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="9ddc0-130">Przykładowy kod *DotNetTutorial* jest rozwiązaniem programu Visual Studio, które obejmuje dwa projekty: **DotNetTutorial** i **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-130">The *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="9ddc0-131">**DotNetTutorial** jest aplikacją kliencką, która współdziała z usługami Batch i Storage w celu wykonania równoległego obciążenia w węzłach obliczeniowych (maszyny wirtualne).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-131">**DotNetTutorial** is the client application that interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="9ddc0-132">Aplikacja DotNetTutorial jest uruchamiana na lokalnej stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="9ddc0-133">**TaskApplication** to program uruchamiany w węzłach obliczeniowych na platformie Azure, który wykonuje faktyczną pracę.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-133">**TaskApplication** is the program that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="9ddc0-134">W naszym przykładzie `TaskApplication.exe` analizuje tekst w pliku pobranym z usługi Azure Storage (plik wejściowy).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-134">In the sample, `TaskApplication.exe` parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="9ddc0-135">Następnie tworzy plik tekstowy (plik wyjściowy) zawierający listę trzech słów najczęściej występujących w pliku wejściowym.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-135">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="9ddc0-136">Po utworzeniu pliku wyjściowego program TaskApplication przekazuje plik do usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-136">After it creates the output file, TaskApplication uploads the file to Azure Storage.</span></span> <span data-ttu-id="9ddc0-137">Dzięki temu jest on dostępny do pobrania przez aplikację kliencką.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-137">This makes it available to the client application for download.</span></span> <span data-ttu-id="9ddc0-138">Program TaskApplication jest uruchamiany równolegle w wielu węzłach obliczeniowych w usłudze Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-138">TaskApplication runs in parallel on multiple compute nodes in the Batch service.</span></span>

<span data-ttu-id="9ddc0-139">Na poniższym diagramie przedstawiono podstawowe operacje wykonywane przez aplikację kliencką,*DotNetTutorial*, oraz aplikację, która jest wykonywana przez podzadania, *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-139">The following diagram illustrates the primary operations that are performed by the client application, *DotNetTutorial*, and the application that is executed by the tasks, *TaskApplication*.</span></span> <span data-ttu-id="9ddc0-140">Ten podstawowy przepływ pracy jest typowy dla wielu rozwiązań obliczeniowych utworzonych za pomocą usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="9ddc0-141">Chociaż nie przedstawiono tu wszystkich funkcji dostępnych w usłudze Batch, prawie każdy scenariusz usługi Batch obejmuje elementy tego przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-141">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="9ddc0-142">![Przykładowy przepływ pracy w usłudze Batch][8]</span><span class="sxs-lookup"><span data-stu-id="9ddc0-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="9ddc0-143">**Krok 1.**</span><span class="sxs-lookup"><span data-stu-id="9ddc0-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="9ddc0-144">Utwórz **kontenery** w usłudze Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="9ddc0-145">
[**Krok 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="9ddc0-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="9ddc0-146">Przekaż pliki aplikacji podzadań i pliki wejściowe do kontenerów.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-146">Upload task application files and input files to containers.</span></span><br/><span data-ttu-id="9ddc0-147">
[**Krok 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="9ddc0-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="9ddc0-148">Utwórz **pulę** w usłudze Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="9ddc0-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="9ddc0-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="9ddc0-150">Pula funkcji **StartTask** pobiera pliki binarne podzadań (TaskApplication), gdy zostają dołączone do puli.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-150">The pool **StartTask** downloads the task binary files (TaskApplication) to nodes as they join the pool.</span></span><br/><span data-ttu-id="9ddc0-151">
[**Krok 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="9ddc0-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="9ddc0-152">Utwórz **zadanie** w usłudze Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="9ddc0-153">
[**Krok 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="9ddc0-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="9ddc0-154">Dodaj **podzadania** do zadania.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-154">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="9ddc0-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="9ddc0-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="9ddc0-156">Zadania są zaplanowane do wykonania w węzłach.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-156">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="9ddc0-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="9ddc0-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="9ddc0-158">Każde zadanie pobiera dane wejściowe z usługi Azure Storage, a następnie rozpoczyna się wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="9ddc0-159">
[**Krok 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="9ddc0-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="9ddc0-160">Monitoruj podzadania.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="9ddc0-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="9ddc0-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="9ddc0-162">Gdy zadania zostaną ukończone, przekazują dane wyjściowe do usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-162">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/><span data-ttu-id="9ddc0-163">
[**Krok 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="9ddc0-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="9ddc0-164">Pobierz dane wyjściowe podzadań z usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-164">Download task output from Storage.</span></span>

<span data-ttu-id="9ddc0-165">Jak wspomniano wcześniej, nie wszystkie rozwiązania usługi Batch obejmują dokładnie te kroki i mogą obejmować wiele innych. Aplikacja przykładowa *DotNetTutorial* pokazuje jednak typowe procesy występujące w rozwiązaniu usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but the *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-the-dotnettutorial-sample-project"></a><span data-ttu-id="9ddc0-166">Kompilowanie przykładowego projektu *DotNetTutorial*</span><span class="sxs-lookup"><span data-stu-id="9ddc0-166">Build the *DotNetTutorial* sample project</span></span>
<span data-ttu-id="9ddc0-167">Aby pomyślnie uruchomić próbkę, należy najpierw określić poświadczenia konta Storage i usługi Batch w pliku `Program.cs` projektu *DotNetTutorial*.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-167">Before you can successfully run the sample, you must specify both Batch and Storage account credentials in the *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="9ddc0-168">Jeśli jeszcze tego nie zrobiono, otwórz rozwiązanie w programie Visual Studio, klikając dwukrotnie plik rozwiązania `DotNetTutorial.sln`.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-168">If you have not done so already, open the solution in Visual Studio by double-clicking the `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="9ddc0-169">Lub otwórz je w programie Visual Studio przy użyciu opcji menu **Plik > Otwórz > Projekt/Rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-169">Or open it from within Visual Studio by using the **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="9ddc0-170">Otwórz `Program.cs` w projekcie *DotNetTutorial*.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-170">Open `Program.cs` within the *DotNetTutorial* project.</span></span> <span data-ttu-id="9ddc0-171">Następnie dodaj poświadczenia określone w górnej części pliku:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-171">Then add your credentials as specified near the top of the file:</span></span>

```csharp
// Update the Batch and Storage account credential strings below with the values
// unique to your accounts. These are used when constructing connection strings
// for the Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="9ddc0-172">Jak wspomniano powyżej, musisz określić poświadczenia dla konta magazynu **ogólnego przeznaczenia** w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-172">As mentioned above, you must currently specify the credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="9ddc0-173">Aplikacje usługi Batch korzystają z magazynu obiektów blob w ramach konta magazynu **ogólnego przeznaczenia**.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-173">Your Batch applications use blob storage within the **general-purpose** storage account.</span></span> <span data-ttu-id="9ddc0-174">Nie określaj poświadczeń dla konta usługi Storage, które zostało utworzone przez wybranie typu konta *Magazyn obiektów Blob*.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-174">Do not specify the credentials for a Storage account that was created by selecting the *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="9ddc0-175">Poświadczenia konta usług Batch i Storage znajdziesz w blokach konta poszczególnych usług w witrynie [Azure Portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-175">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="9ddc0-176">![Poświadczenia usługi Batch w portalu][9]
![Poświadczenia usługi Storage w portalu][10]</span><span class="sxs-lookup"><span data-stu-id="9ddc0-176">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="9ddc0-177">Po zaktualizowaniu projektu przy użyciu poświadczeń kliknij prawym przyciskiem myszy rozwiązanie w Eksploratorze rozwiązań i kliknij przycisk **Kompiluj rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-177">Now that you've updated the project with your credentials, right-click the solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="9ddc0-178">Jeśli zostanie wyświetlony monit, potwierdź przywrócenie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-178">Confirm the restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="9ddc0-179">Jeśli pakiety nie zostaną automatycznie przywrócone lub zostaną wyświetlone błędy z informacją o nieudanej próbie przywrócenia pakietów, sprawdź, czy jest zainstalowany [Menedżer pakietów NuGet][nuget_packagemgr].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-179">If the NuGet packages are not automatically restored, or if you see errors about a failure to restore the packages, ensure that you have the [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="9ddc0-180">Następnie włącz pobieranie brakujących pakietów.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-180">Then enable the download of missing packages.</span></span> <span data-ttu-id="9ddc0-181">Zobacz sekcję [Enabling Package Restore During Build][nuget_restore] (Włączanie przywracania pakietów podczas kompilacji), która zawiera instrukcje dotyczące włączania pobierania pakietów.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-181">See [Enabling Package Restore During Build][nuget_restore] to enable package download.</span></span>
>
>

<span data-ttu-id="9ddc0-182">W poniższych sekcjach przykładowa aplikacja została podzielona na kroki wykonywane w celu przetworzenia obciążenia w usłudze Batch. Kroki te zostały szczegółowo opisane.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-182">In the following sections, we break down the sample application into the steps that it performs to process a workload in the Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="9ddc0-183">Podczas wykonywania instrukcji w dalszej części tego artykułu warto korzystać z informacji z otwartego rozwiązania w programie Visual Studio, ponieważ nie omówiono tu wszystkich wierszy kodu z próbki.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-183">We encourage you to refer to the open solution in Visual Studio while you work your way through the rest of this article, since not every line of code in the sample is discussed.</span></span>

<span data-ttu-id="9ddc0-184">Przejdź do góry metody `MainAsync` w pliku `Program.cs` projektu *DotNetTutorial*, aby rozpocząć od kroku 1.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-184">Navigate to the top of the `MainAsync` method in the *DotNetTutorial* project's `Program.cs` file to start with Step 1.</span></span> <span data-ttu-id="9ddc0-185">Wszystkie kroki poniżej odpowiadają mniej więcej postępowi wywołań metody w elemencie `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-185">Each step below then roughly follows the progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="9ddc0-186">Krok 1: tworzenie kontenerów w usłudze Storage</span><span class="sxs-lookup"><span data-stu-id="9ddc0-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="9ddc0-187">![Tworzenie kontenerów w usłudze Azure Storage][1]
</span><span class="sxs-lookup"><span data-stu-id="9ddc0-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="9ddc0-188">Usługa Batch ma wbudowaną funkcję obsługi interakcji z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="9ddc0-189">Kontenery na koncie usługi Storage będą udostępniać pliki potrzebne zadaniom, które będą uruchamiane na koncie usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-189">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="9ddc0-190">Kontenery zapewniają również miejsce do przechowywania danych wyjściowych wytworzonych przez zadania.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-190">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="9ddc0-191">Najpierw aplikacja kliencka *DotNetTutorial* tworzy trzy kontenery w usłudze [Azure Blob Storage](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="9ddc0-191">The first thing the *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="9ddc0-192">**aplikacja**: ten kontener będzie przechowywać aplikację uruchomioną przez podzadania oraz wszelkie ich zależności, np. biblioteki dll.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-192">**application**: This container will store the application run by the tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="9ddc0-193">**dane wejściowe**: podzadania będą pobierać pliki danych do przetwarzania z kontenera *wejściowego*.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-193">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="9ddc0-194">**dane wyjściowe**: gdy podzadania ukończą przetwarzanie plików wejściowych, przekażą wyniki do kontenera *wyjściowego*.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-194">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="9ddc0-195">Do interakcji z kontem usługi Storage i tworzenia kontenerów należy użyć [biblioteki Azure Storage Client Library dla platformy .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-195">In order to interact with a Storage account and create containers, we use the [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="9ddc0-196">Należy utworzyć odwołanie do konta za pomocą elementu [CloudStorageAccount][net_cloudstorageaccount] i przy jego użyciu utworzyć element [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-196">We create a reference to the account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct the Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve the storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create the blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="9ddc0-197">Należy używać odwołania `blobClient` w całej aplikacji i przekazać go jako parametr do kilku metod.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-197">We use the `blobClient` reference throughout the application and pass it as a parameter to several methods.</span></span> <span data-ttu-id="9ddc0-198">Przykładem może być blok kodu, który następuje od razu po powyższym, w ramach którego wywołuje się element `CreateContainerIfNotExistAsync` na potrzeby tworzenia kontenerów.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-198">An example of this is in the code block that immediately follows the above, where we call `CreateContainerIfNotExistAsync` to actually create the containers.</span></span>

```csharp
// Use the blob client to create the containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

<span data-ttu-id="9ddc0-199">Po utworzeniu kontenerów aplikacja może teraz przekazać pliki, które będą używane przez podzadania.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-199">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> <span data-ttu-id="9ddc0-200">W temacie [How to use Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) (Jak korzystać z usługi Blob Storage w ramach platformy .NET) znajduje się szczegółowe omówienie korzystania z kontenerów i obiektów blob w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-200">[How to use Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="9ddc0-201">Powinna to być jedna z najważniejszych pozycji do przeczytania po rozpoczęciu pracy z usługą Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-201">It should be near the top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="9ddc0-202">Krok 2: przekazanie aplikacji podzadań i plików danych</span><span class="sxs-lookup"><span data-stu-id="9ddc0-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="9ddc0-203">![Przekazywanie aplikacji zadania podrzędnego i plików danych wejściowych do kontenerów][2]
</span><span class="sxs-lookup"><span data-stu-id="9ddc0-203">![Upload task application and input (data) files to containers][2]
</span></span><br/>

<span data-ttu-id="9ddc0-204">Podczas przekazywania plików aplikacja *DotNetTutorial* najpierw definiuje kolekcje **aplikacji** i ścieżki plików **wejściowych** na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-204">In the file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="9ddc0-205">Następnie przekazuje te pliki do kontenerów, które zostały utworzone w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-205">Then it uploads these files to the containers that you created in the previous step.</span></span>

```csharp
// Paths to the executable and its dependencies that will be executed by the tasks
List<string> applicationFilePaths = new List<string>
{
    // The DotNetTutorial project includes a project reference to TaskApplication,
    // allowing us to determine the path of the task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// The collection of data files that are to be processed by the tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload the application and its dependencies to Azure Storage. This is the
// application that will process the data files, and will be executed by each
// of the tasks on the compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload the data files. This is the data that will be processed by each of
// the tasks that are executed on the compute nodes within the pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="9ddc0-206">W pliku `Program.cs` istnieją dwie metody używane w procesie przekazywania:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-206">There are two methods in `Program.cs` that are involved in the upload process:</span></span>

* <span data-ttu-id="9ddc0-207">`UploadFilesToContainerAsync`: ta metoda zwraca kolekcję obiektów [ResourceFile][net_resourcefile] (omówionych poniżej) i wywołuje wewnętrznie element `UploadFileToContainerAsync` w celu przekazania wszystkich plików przekazywanych w parametrze *filePaths*.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` to upload each file that is passed in the *filePaths* parameter.</span></span>
* <span data-ttu-id="9ddc0-208">`UploadFileToContainerAsync`: ta metoda faktycznie wykonuje przekazanie pliku i tworzy obiekty [ResourceFile][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-208">`UploadFileToContainerAsync`: This is the method that actually performs the file upload and creates the [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="9ddc0-209">Po przekazaniu pliku uzyskuje sygnaturę dostępu współdzielonego (SAS) i zwraca obiekt ResourceFile, który go reprezentuje.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-209">After uploading the file, it obtains a shared access signature (SAS) for the file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="9ddc0-210">Sygnatury dostępu współdzielonego zostały również omówione poniżej.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} to container [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set the expiry time and permissions for the blob shared access signature.
        // In this case, no start time is specified, so the shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct the SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="9ddc0-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="9ddc0-211">ResourceFiles</span></span>
<span data-ttu-id="9ddc0-212">Klasa [ResourceFile][net_resourcefile] zawiera podzadania w usłudze Batch z adresem URL do pliku w usłudze Azure Storage, które są pobierane do węzła obliczeniowego przed uruchomieniem tego podzadania.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="9ddc0-213">Właściwość [ResourceFile.BlobSource][net_resourcefile_blobsource] określa pełny adres URL pliku przechowywanego w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-213">The [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="9ddc0-214">Adres URL może także zawierać sygnaturę dostępu współdzielonego (SAS), która zapewnia bezpieczny dostęp do pliku.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-214">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="9ddc0-215">Większość typów podzadań w usłudze Batch dla platformy .NET obejmuje właściwość *ResourceFiles*, w tym następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="9ddc0-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="9ddc0-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="9ddc0-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="9ddc0-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="9ddc0-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="9ddc0-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="9ddc0-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="9ddc0-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="9ddc0-220">Przykładowa aplikacja DotNetTutorial nie używa typów zadań JobPreparationTask ani JobReleaseTask, ale więcej informacji o nich można znaleźć w temacie [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md) (Uruchamianie podzadań przygotowania i ukończenia zadania w węzłach obliczeniowych w usłudze Azure Batch).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-220">The DotNetTutorial sample application does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="9ddc0-221">Sygnatura dostępu współdzielonego (SAS)</span><span class="sxs-lookup"><span data-stu-id="9ddc0-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="9ddc0-222">Sygnatury dostępu współdzielonego to ciągi, które — w przypadku dołączenia ich do adresu URL — zapewniają bezpieczny dostęp do kontenerów i obiektów blob w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-222">Shared access signatures are strings which—when included as part of a URL—provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="9ddc0-223">Aplikacja DotNetTutorial używa adresów URL sygnatury dostępu współdzielonego kontenera i obiektów blob i służy do pokazania, jak uzyskać te ciągi sygnatur dostępu współdzielonego za pomocą usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-223">The DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="9ddc0-224">**Sygnatury dostępu współdzielonego obiektów Blob**: funkcja StartTask puli w aplikacji DotNetTutorial używa sygnatur dostępu współdzielonego obiektów blob podczas pobierania danych binarnych aplikacji i plików danych wejściowych za pomocą usługi Storage (zobacz krok 3 poniżej).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-224">**Blob shared access signatures**: The pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads the application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="9ddc0-225">Metoda `UploadFileToContainerAsync` w elemencie `Program.cs` aplikacji DotNetTutorial obejmuje kod, który uzyskuje dostęp do sygnatur dostępu współdzielonego poszczególnych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-225">The `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="9ddc0-226">Odbywa się to przez wywołanie metody [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="9ddc0-227">**Sygnatury dostępu współdzielonego kontenera**: gdy poszczególne podzadania zakończą pracę w węźle obliczeniowym, przekażą pliki wyjściowe do kontenera *wyjściowego* w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-227">**Container shared access signatures**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="9ddc0-228">W tym celu funkcja TaskApplication używa sygnatury dostępu współdzielonego kontenera, która zapewnia prawo do zapisu w kontenerze w ramach ścieżki, gdy przekazuje plik.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-228">To do so, TaskApplication uses a container shared access signature that provides write access to the container as part of the path when it uploads the file.</span></span> <span data-ttu-id="9ddc0-229">Uzyskiwanie sygnatury dostępu współdzielonego kontenera odbywa się w podobny sposób, jak w przypadku uzyskiwania sygnatury dostępu współdzielonego obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-229">Obtaining the container shared access signature is done in a similar fashion as when obtaining the blob shared access signature.</span></span> <span data-ttu-id="9ddc0-230">W aplikacji DotNetTutorial będzie widać, że metoda pomocnika `GetContainerSasUrl` wywołuje w tym celu metodę [CloudBlobContainer.GetSharedAccessSignature][net_sas_container].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-230">In DotNetTutorial, you will find that the `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] to do so.</span></span> <span data-ttu-id="9ddc0-231">Więcej informacji na temat sposobu, w jaki aplikacja TaskApplication korzysta z sygnatury dostępu współdzielonego kontenera znajduje się w sekcji „Krok 6: monitorowanie podzadań.”</span><span class="sxs-lookup"><span data-stu-id="9ddc0-231">You'll read more about how TaskApplication uses the container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="9ddc0-232">Aby dowiedzieć się więcej o zapewnieniu bezpiecznego dostępu do danych na koncie usługi Storage, zapoznaj się z dwuczęściową serią dotyczącą sygnatur dostępu współdzielonego: [Part 1: Understanding the shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (Część 1: opis modelu sygnatury dostępu współdzielonego [SAS]) i [Part 2: Create and use a shared access signature (SAS) with the Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) (Część 2: tworzenie i korzystanie z sygnatury dostępu współdzielonego [SAS] w magazynie Blob Storage).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-232">Check out the two-part series on shared access signatures, [Part 1: Understanding the shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="9ddc0-233">Krok 3: tworzenie puli usługi Batch</span><span class="sxs-lookup"><span data-stu-id="9ddc0-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="9ddc0-234">![Tworzenie puli usługi Batch][3]
</span><span class="sxs-lookup"><span data-stu-id="9ddc0-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="9ddc0-235">**Pula** usługi Batch jest kolekcją węzłów obliczeniowych (maszyn wirtualnych), w których usługa Batch wykonuje podzadania danego zadania.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="9ddc0-236">Po przekazaniu plików aplikacji i danych do konta usługi Storage przy użyciu interfejsów API usługi Azure Storage element *DotNetTutorial* rozpoczyna wykonywanie wywołań do usługi Batch przy użyciu interfejsów API udostępnionych przez bibliotekę technologii .NET usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-236">After uploading the application and data files to the Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls to the Batch service with APIs provided by the Batch .NET library.</span></span> <span data-ttu-id="9ddc0-237">Kod najpierw tworzy element [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-237">The code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="9ddc0-238">Następnie w przykładzie tworzona jest pula węzłów obliczeniowych na koncie usługi Batch z wywołaniem funkcji `CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-238">Next, the sample creates a pool of compute nodes in the Batch account with a call to `CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="9ddc0-239">Funkcja `CreatePoolIfNotExistsAsync` używa metody [BatchClient.PoolOperations.CreatePool][net_pool_create], aby utworzyć nową pulę w usłudze Batch:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-239">`CreatePoolIfNotExistsAsync` uses the [BatchClient.PoolOperations.CreatePool][net_pool_create] method to create a new pool in the Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create the unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign the StartTask that will be executed when compute nodes join the pool.
        // In this case, we copy the StartTask's resource files (that will be automatically downloaded
        // to the node by the StartTask) into the shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for the StartTask that copies the task application files to the
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need to manually exit with a 0 for Batch to recognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow the specific error code PoolExists since that is expected if the pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("The pool {0} already existed when we tried to create it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="9ddc0-240">Podczas tworzenia puli za pomocą funkcji [CreatePool][net_pool_create] należy określić liczbę parametrów, np. liczbę węzłów obliczeniowych, [rozmiar węzłów](../cloud-services/cloud-services-sizes-specs.md) oraz system operacyjny węzłów.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as the number of compute nodes, the [size of the nodes](../cloud-services/cloud-services-sizes-specs.md), and the nodes' operating system.</span></span> <span data-ttu-id="9ddc0-241">W aplikacji *DotNetTutorial* używamy funkcji [CloudServiceConfiguration][net_cloudserviceconfiguration] do określenia systemu Windows Server 2012 R2 z [usług Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] to specify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="9ddc0-242">Można również tworzyć pule węzłów obliczeniowych, które są maszynami wirtualnymi platformy Azure, wybierając element [VirtualMachineConfiguration][net_virtualmachineconfiguration] dla puli.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying the [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="9ddc0-243">Pulę węzłów obliczeniowych maszyn wirtualnych można utworzyć na podstawie [obrazów systemu Linux](batch-linux-nodes.md) lub Windows.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="9ddc0-244">Źródłem obrazów maszyny wirtualnej może być:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-244">The source for your VM images can be either:</span></span>

- <span data-ttu-id="9ddc0-245">Witryna [Marketplace usługi Azure Virtual Machines][vm_marketplace], która udostępnia gotowe do użycia obrazy systemów Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-245">The [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="9ddc0-246">Obraz niestandardowy przygotowywany i udostępniany przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="9ddc0-247">Aby uzyskać szczegółowe informacje o obrazach niestandardowych, zobacz [Tworzenie rozbudowanych rozwiązań przetwarzania równoległego przy użyciu usługi Batch](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ddc0-248">W usłudze Batch opłaty są naliczane za zasoby obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="9ddc0-249">Aby zminimalizować koszty przed uruchomieniem próbki, można zmniejszyć parametr `targetDedicatedComputeNodes` do 1.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-249">To minimize costs, you can lower `targetDedicatedComputeNodes` to 1 before you run the sample.</span></span>
>
>

<span data-ttu-id="9ddc0-250">Wraz z fizycznymi właściwościami węzłów można też określić funkcję [StartTask][net_pool_starttask] dla puli.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for the pool.</span></span> <span data-ttu-id="9ddc0-251">Funkcja StartTask jest wykonywana w każdym węźle, gdy tylko ten węzeł zostanie dołączony do puli, oraz za każdym razem, gdy węzeł będzie uruchamiany ponownie.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-251">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="9ddc0-252">Funkcja StartTask jest szczególnie przydatna podczas instalowania aplikacji w węzłach obliczeniowych przed wykonaniem podzadań.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-252">The StartTask is especially useful for installing applications on compute nodes prior to the execution of tasks.</span></span> <span data-ttu-id="9ddc0-253">Na przykład jeśli podzadania przetwarzają dane za pomocą skryptów języka Python, można użyć funkcji StartTask do zainstalowania języka Python w węzłach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-253">For example, if your tasks process data by using Python scripts, you could use a StartTask to install Python on the compute nodes.</span></span>

<span data-ttu-id="9ddc0-254">W tej przykładowej aplikacji podzadanie StartTask kopiuje pliki, które pobiera z usługi Storage (określone za pomocą właściwości [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles]) z katalogu roboczego podzadania StartTask do współdzielonego katalogu, do którego mają dostęp *wszystkie* podzadania uruchomione w węźle.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-254">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from the StartTask working directory to the shared directory that *all* tasks running on the node can access.</span></span> <span data-ttu-id="9ddc0-255">Powoduje to skopiowanie pliku `TaskApplication.exe` i jego zależności do udostępnionego katalogu w każdym węźle, gdy węzeł dołącza do puli, aby dostęp do niego miały wszystkie podzadania uruchomione w węźle.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-255">Essentially, this copies `TaskApplication.exe` and its dependencies to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="9ddc0-256">Funkcja **pakietów aplikacji** w usłudze Azure Batch udostępnia inny sposób pobrania aplikacji do węzła obliczeniowego w puli.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-256">The **application packages** feature of Azure Batch provides another way to get your application onto the compute nodes in a pool.</span></span> <span data-ttu-id="9ddc0-257">Szczegółowe informacje można znaleźć w artykule [Deploy applications to compute nodes with Batch application packages (Wdrażanie aplikacji w węzłach obliczeniowych za pomocą pakietów aplikacji usługi Batch)](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-257">See [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="9ddc0-258">W powyższym fragmencie kodu warto również zwrócić uwagę na użycie dwóch zmiennych środowiskowych we właściwości *CommandLine* funkcji StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` i `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-258">Also notable in the code snippet above is the use of two environment variables in the *CommandLine* property of the StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="9ddc0-259">Każdy węzeł obliczeniowy w puli usługi Batch jest automatycznie konfigurowany za pomocą kilku zmiennych środowiskowych właściwych dla usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="9ddc0-260">Wszystkie procesy wykonywane przez zadanie mają dostęp do tych zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-260">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="9ddc0-261">Informacje na temat zmiennych środowiskowych dostępnych w węzłach obliczeniowych w puli usługi Batch oraz katalogów roboczych podzadań znajdują się w sekcjach [Ustawienia środowiska dla podzadań](batch-api-basics.md#environment-settings-for-tasks) oraz [Pliki i katalogi](batch-api-basics.md#files-and-directories) w artykule [Batch feature overview for developers](batch-api-basics.md) (Omówienie funkcji usługi Batch dla deweloperów).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-261">To find out more about the environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see the [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in the [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="9ddc0-262">Krok 4: tworzenie zadania w usłudze Batch</span><span class="sxs-lookup"><span data-stu-id="9ddc0-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="9ddc0-263">![Tworzenie zadania w usłudze Batch][4]</span><span class="sxs-lookup"><span data-stu-id="9ddc0-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="9ddc0-264">**Zadanie** usługi Batch jest kolekcją podzadań i jest skojarzone z pulą węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="9ddc0-265">Podzadania tego zadania są wykonywane w węzłach obliczeniowych skojarzonej puli.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-265">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="9ddc0-266">Zadań można użyć nie tylko do organizowania i śledzenia podzadań w powiązanych obciążeniach, ale także do nakładania pewnych ograniczeń — takich jak maksymalny czas wykonywania zadania (a co za tym idzie podzadań, które ono obejmuje), a także priorytet zadania w odniesieniu do innych zadań w ramach konta usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) as well as job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="9ddc0-267">Jednak w tym przykładzie zadanie jest skojarzone tylko z pulą, która została utworzona w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-267">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="9ddc0-268">Żadne dodatkowe właściwości nie są konfigurowane.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-268">No additional properties are configured.</span></span>

<span data-ttu-id="9ddc0-269">Wszystkie zadania usługi Batch są skojarzone z określoną pulą.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="9ddc0-270">To skojarzenie wskazuje, w których węzłach będą wykonywane podzadania wchodzące w skład zadania.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-270">This association indicates which nodes the job's tasks will execute on.</span></span> <span data-ttu-id="9ddc0-271">Należy to określić za pomocą właściwości [CloudJob.PoolInformation][net_job_poolinfo], jak pokazano we fragmencie kodu poniżej.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-271">You specify this by using the [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in the code snippet below.</span></span>

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

<span data-ttu-id="9ddc0-272">Teraz, kiedy zadanie zostało utworzone, są dodawane podzadania, aby wykonać pracę.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-272">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="9ddc0-273">Krok 5: dodawanie podzadań do zadania</span><span class="sxs-lookup"><span data-stu-id="9ddc0-273">Step 5: Add tasks to job</span></span>
<span data-ttu-id="9ddc0-274">![Dodawanie podzadań do zadania][5]</span><span class="sxs-lookup"><span data-stu-id="9ddc0-274">![Add tasks to job][5]</span></span><br/><span data-ttu-id="9ddc0-275">
*(1) Podzadania są dodawane do zadania, (2) podzadania są planowane do uruchomienia w węzłach i (3) podzadania pobierają pliki danych do przetwarzania*</span><span class="sxs-lookup"><span data-stu-id="9ddc0-275">
*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="9ddc0-276">**Podzadania** usługi Batch to pojedyncze jednostki robocze, które są wykonywane w węzłach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-276">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="9ddc0-277">Podzadanie ma wiersz polecenia i uruchamia skrypty lub pliki wykonywalne określone w tym wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-277">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="9ddc0-278">Aby praca została rzeczywiście wykonana, należy dodać podzadania do zadania.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-278">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="9ddc0-279">Każde podzadanie typu [CloudTask][net_task] jest konfigurowane za pomocą właściwości wiersza polecenia i właściwości [ResourceFiles][net_task_resourcefiles] (tak jak w przypadku podzadania StartTask w puli), które podzadanie pobiera do węzła, zanim zostanie automatycznie wykonany jego wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="9ddc0-280">W przykładowym projekcie aplikacji *DotNetTutorial* każde podzadanie przetwarza tylko jeden plik.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-280">In the *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="9ddc0-281">W związku z tym jego kolekcja ResourceFiles zawiera jeden element.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks to job [{1}]...", inputFiles.Count, jobId);

    // Create a collection to hold the tasks that we'll be adding to the job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of the tasks. Because we copied the task application to the
    // node's shared directory with the pool's StartTask, we can access it via
    // the shared directory on the node that the task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add the tasks as a collection, as opposed to issuing a separate AddTask call
    // for each. Bulk task submission helps to ensure efficient underlying API calls
    // to the Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="9ddc0-282">Podczas uzyskiwania dostępu do zmiennych środowiskowych (takich jak `%AZ_BATCH_NODE_SHARED_DIR%`) lub wykonywania aplikacji nieznajdującej się w parametrze `PATH` węzła wiersze poleceń podzadań muszą rozpoczynać się od `cmd /c`.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in the node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="9ddc0-283">Spowoduje to jawne wykonanie interpretera poleceń i przesłanie do niego instrukcji zakończenia po wypełnieniu polecenia.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-283">This will explicitly execute the command interpreter and instruct it to terminate after carrying out your command.</span></span> <span data-ttu-id="9ddc0-284">Nie jest to konieczne, jeśli podzadania wykonują aplikację w parametrze `PATH` węzła (np. *robocopy.exe* lub *powershell.exe*) i żadne zmienne środowiskowe nie są używane.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-284">This requirement is unnecessary if your tasks execute an application in the node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="9ddc0-285">W pętli `foreach` w powyższym fragmencie kodu widać, że wiersz polecenia dla podzadania jest zbudowany w taki sposób, że trzy argumenty wiersza polecenia są przekazywane do pliku *TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-285">Within the `foreach` loop in the code snippet above, you can see that the command line for the task is constructed such that three command-line arguments are passed to *TaskApplication.exe*:</span></span>

1. <span data-ttu-id="9ddc0-286">**Pierwszy argument** jest ścieżką pliku do przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-286">The **first argument** is the path of the file to process.</span></span> <span data-ttu-id="9ddc0-287">Jest to ścieżka lokalna do pliku zgodnie z jego lokalizacją w węźle.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-287">This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="9ddc0-288">Gdy obiekt ResourceFile w `UploadFileToContainerAsync` został utworzony po raz pierwszy, jak powyżej, nazwa pliku została użyta dla tej właściwości (jako parametr do konstruktora ResourceFile).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-288">When the ResourceFile object in `UploadFileToContainerAsync` was first created above, the file name was used for this property (as a parameter to the ResourceFile constructor).</span></span> <span data-ttu-id="9ddc0-289">Oznacza to, że plik znajduje się w tym samym katalogu co plik *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-289">This indicates that the file can be found in the same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="9ddc0-290">**Drugi argument** określa, że *N* wyrazów na samej górze będzie zapisywanych do pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-290">The **second argument** specifies that the top *N* words should be written to the output file.</span></span> <span data-ttu-id="9ddc0-291">W przykładzie zostało to zakodowane na stałe, aby pierwsze trzy słowa zostały zapisane do pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-291">In the sample, this is hard-coded so that the top three words are written to the output file.</span></span>
3. <span data-ttu-id="9ddc0-292">**Trzeci argument** jest sygnaturą dostępu współdzielonego (SAS), która zapewnia prawo do zapisu kontenera **wyjściowego** w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-292">The **third argument** is the shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="9ddc0-293">Plik *TaskApplication.exe* korzysta z tego adresu URL sygnatury dostępu współdzielonego, gdy przekazuje plik wyjściowy do usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-293">*TaskApplication.exe* uses this shared access signature URL when it uploads the output file to Azure Storage.</span></span> <span data-ttu-id="9ddc0-294">Kod do tej czynności można znaleźć w metodzie `UploadFileToContainer` w pliku `Program.cs` projektu funkcji TaskApplication:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-294">You can find the code for this in the `UploadFileToContainer` method in the TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference to the container using the SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload the file (as a new blob) to the container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when the Batch service
                // sets the CloudTask.ExecutionInformation.ExitCode for the task that
                // executed this application, it properly indicates that there was a
                // problem with the task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="9ddc0-295">Krok 6: monitorowanie podzadań</span><span class="sxs-lookup"><span data-stu-id="9ddc0-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="9ddc0-296">![Monitorowanie podzadań][6]</span><span class="sxs-lookup"><span data-stu-id="9ddc0-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="9ddc0-297">
*Aplikacja kliencka (1) monitoruje podzadania pod kątem stanu ukończenia i powodzenia, a (2) podzadania przekazują dane wynikowe do usługi Azure Storage*</span><span class="sxs-lookup"><span data-stu-id="9ddc0-297">
*The client application (1) monitors the tasks for completion and success status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="9ddc0-298">Gdy podzadania są dodawane do zadania, zostają automatycznie dodane do kolejki i zaplanowane do wykonania w węzłach obliczeniowych w puli skojarzonej z zadaniem.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-298">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="9ddc0-299">Na podstawie określonych przez użytkownika ustawień usługa Batch samodzielnie obsługuje dodawanie podzadań do kolejki, ich planowanie, ponawianie prób ich wykonania oraz inne czynności administracyjne.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-299">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="9ddc0-300">Istnieje wiele sposobów, w jakie można monitorować wykonanie podzadań.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-300">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="9ddc0-301">Aplikacja DotNetTutorial stanowi prosty przykład zgłaszania tylko w przypadku ukończenia oraz stanów powodzenia lub niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="9ddc0-302">W metodzie `MonitorTasks` w parametrze `Program.cs` programu DotNetTutorial istnieją trzy pojęcia w usłudze Batch dla platformy .NET, które wymagają omówienia.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-302">Within the `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="9ddc0-303">Są one wymienione poniżej w kolejności ich występowania:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="9ddc0-304">**ODATADetailLevel**: określenie funkcji [ODATADetailLevel][net_odatadetaillevel] na liście operacji (takich jak uzyskanie listy podzadań zadania) jest niezbędne do zapewnienia wydajności aplikacji usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="9ddc0-305">Zaplanuj przeczytanie tematu [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) (Wydajne wysyłanie zapytań do usługi Azure Batch), jeśli planujesz wykonać dowolny rodzaj monitorowania stanu w aplikacjach usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-305">Add [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) to your reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="9ddc0-306">**TaskStateMonitor**: funkcja [TaskStateMonitor][net_taskstatemonitor] zapewnia aplikacjom usługi Batch dla platformy .NET narzędzia pomocy do monitorowania stanów podzadań.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="9ddc0-307">W przypadku parametru `MonitorTasks` *DotNetTutorial* oczekuje, aż wszystkie podzadania zostaną w określonym czasie objęte zasięgiem funkcji [TaskState.Completed][net_taskstate].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks to reach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="9ddc0-308">Następnie kończy zadanie.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-308">Then it terminates the job.</span></span>
3. <span data-ttu-id="9ddc0-309">**TerminateJobAsync**: zakończenie zadania za pomocą funkcji [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (lub blokującej funkcji JobOperations.TerminateJob) spowoduje, że zadanie zostanie oznaczone jako zakończone.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or the blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="9ddc0-310">Należy tak koniecznie zrobić, jeśli rozwiązanie usługi Batch korzysta z funkcji [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-310">It is essential to do so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="9ddc0-311">Jest to szczególny typ podzadania, który opisano w temacie [Job preparation and completion tasks](batch-job-prep-release.md) (Przygotowanie zadania i podzadania związane z ukończeniem).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="9ddc0-312">Metoda `MonitorTasks` z pliku aplikacji *DotNetTutorial* `Program.cs` jest wyświetlana poniżej:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-312">The `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed to reach the Completed state within the timeout period.";

    // Obtain the collection of tasks currently managed by the job. Note that we use
    // a detail level to  specify that only the "id" property of each task should be
    // populated. Using a detail level for all list operations helps to lower
    // response time from the Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor to monitor the state of our tasks. In this case, we
    // will wait for all tasks to reach the Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached the "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property to ensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update the detail level to populate only the task id and executionInfo
    // properties. We refresh the tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate the task's properties with the latest info from the Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with the task. It is important to note that
            // the task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that the application executed by the task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within the specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="9ddc0-313">Krok 7: pobranie danych wyjściowych podzadań</span><span class="sxs-lookup"><span data-stu-id="9ddc0-313">Step 7: Download task output</span></span>
<span data-ttu-id="9ddc0-314">![Pobieranie danych wyjściowych zadań podrzędnych z usługi Storage][7]</span><span class="sxs-lookup"><span data-stu-id="9ddc0-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="9ddc0-315">Po ukończeniu zadania można pobrać dane wyjściowe podzadań przy użyciu usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-315">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="9ddc0-316">Odbywa się to przy użyciu wywołania do funkcji `DownloadBlobsFromContainerAsync` w pliku `Program.cs` *DotNetTutorial*:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-316">This is done with a call to `DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference to a previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all the block blobs in the specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference to the current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents to a file in the specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded to {0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="9ddc0-317">Wywołanie do funkcji `DownloadBlobsFromContainerAsync` w aplikacji *DotNetTutorial* określa, że pliki powinny zostać pobrane do folderu `%TEMP%`.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-317">The call to `DownloadBlobsFromContainerAsync` in the *DotNetTutorial* application specifies that the files should be downloaded to your `%TEMP%` folder.</span></span> <span data-ttu-id="9ddc0-318">Można także swobodnie modyfikować tę lokalizację danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-318">Feel free to modify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="9ddc0-319">Krok 8: usuwanie kontenerów</span><span class="sxs-lookup"><span data-stu-id="9ddc0-319">Step 8: Delete containers</span></span>
<span data-ttu-id="9ddc0-320">Ponieważ użytkownik jest rozliczany za dane przechowywane w usłudze Azure Storage, zawsze dobrym rozwiązaniem jest usunięcie obiektów blob, które nie są już potrzebne do zadań w ramach usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-320">Because you are charged for data that resides in Azure Storage, it's always a good idea to remove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="9ddc0-321">W pliku `Program.cs` programu DotNetTutorial odbywa się to przy użyciu trzech wywołań do metody pomocy `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-321">In DotNetTutorial's `Program.cs`, this is done with three calls to the helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="9ddc0-322">Sama metoda jedynie uzyskuje odwołanie do kontenera, a następnie wywołuje funkcję [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-322">The method itself merely obtains a reference to the container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="9ddc0-323">Krok 9: usuwanie zadania i puli</span><span class="sxs-lookup"><span data-stu-id="9ddc0-323">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="9ddc0-324">W ostatnim kroku zostaje wyświetlony monit o usunięcie zadania i puli, które zostały utworzone przez aplikację DotNetTutorial.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-324">In the final step, you're prompted to delete the job and the pool that were created by the DotNetTutorial application.</span></span> <span data-ttu-id="9ddc0-325">Mimo że nie są naliczane opłaty za same zadania i podzadania, *są* naliczane opłaty za węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="9ddc0-326">W związku z tym zaleca się przydzielanie węzłów tylko zależnie do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="9ddc0-327">Usuwanie nieużywanych pul może odbywać się podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="9ddc0-328">Dla obu obiektów [JobOperations][net_joboperations] i [PoolOperations][net_pooloperations] klienta BatchClient istnieją odpowiednie metody usuwania, które są wywoływane, jeśli użytkownik potwierdzi usunięcie:</span><span class="sxs-lookup"><span data-stu-id="9ddc0-328">The BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if the user confirms deletion:</span></span>

```csharp
// Clean up the resources we've created in the Batch account if the user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> <span data-ttu-id="9ddc0-329">Należy pamiętać, że opłaty są naliczane za zasoby obliczeniowe — usunięcie nieużywanych pul zminimalizuje koszty.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="9ddc0-330">Ponadto należy pamiętać, że usunięcie puli spowoduje usunięcie wszystkich węzłów obliczeniowych w tej puli i że po usunięciu puli danych z węzłów nie da się odzyskać.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.</span></span>
>
>

## <a name="run-the-dotnettutorial-sample"></a><span data-ttu-id="9ddc0-331">Uruchamianie aplikacji przykładowej *DotNetTutorial*</span><span class="sxs-lookup"><span data-stu-id="9ddc0-331">Run the *DotNetTutorial* sample</span></span>
<span data-ttu-id="9ddc0-332">Po uruchomieniu aplikacji przykładowej dane wyjściowe w konsoli będą wyglądać mniej więcej w taki sposób.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-332">When you run the sample application, the console output will be similar to the following.</span></span> <span data-ttu-id="9ddc0-333">W czasie wykonywania nastąpi wstrzymanie operacji w momencie wyświetlenia paska zadań `Awaiting task completion, timeout in 00:30:00...` podczas uruchamiania węzłów obliczeniowych puli.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> <span data-ttu-id="9ddc0-334">Użyj witryny [Azure Portal][azure_portal] do monitorowania puli, węzłów obliczeniowych, zadania i podzadań w trakcie wykonywania i po nim.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-334">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="9ddc0-335">Użyj witryny [Azure Portal][azure_portal] lub programu [Azure Storage Explorer][storage_explorers] do wyświetlania zasobów usługi Storage (kontenerów i obiektów blob) tworzonych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-335">Use the [Azure portal][azure_portal] or the [Azure Storage Explorer][storage_explorers] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

<span data-ttu-id="9ddc0-336">Typowy czas wykonywania wynosi **mniej więcej 5 minut** w przypadku uruchomienia aplikacji w konfiguracji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-336">Typical execution time is **approximately 5 minutes** when you run the application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe to container [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll to container [application]...
Uploading file ..\..\taskdata1.txt to container [input]...
Uploading file ..\..\taskdata2.txt to container [input]...
Uploading file ..\..\taskdata3.txt to container [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks to job [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within the specified timeout period.
Downloading all files from container [output]...
All files downloaded to C:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="9ddc0-337">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ddc0-337">Next steps</span></span>
<span data-ttu-id="9ddc0-338">Możesz swobodnie wprowadzać zmiany w funkcjach *DotNetTutorial* i *TaskApplication*, aby eksperymentować z różnymi scenariuszami obliczeniowymi.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-338">Feel free to make changes to *DotNetTutorial* and *TaskApplication* to experiment with different compute scenarios.</span></span> <span data-ttu-id="9ddc0-339">Spróbuj na przykład dodać opóźnienie wykonywania do funkcji *TaskApplication*, tak jak w przypadku funkcji [Thread.Sleep][net_thread_sleep], w celu symulowania podzadań długotrwałych i monitorowania ich w portalu.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-339">For example, try adding an execution delay to *TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="9ddc0-340">Spróbuj dodać więcej podzadań lub dostosować liczbę węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-340">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="9ddc0-341">Dodaj logikę, pod kątem której będzie odbywać się sprawdzanie, i zezwól na użycie istniejącej puli, aby przyspieszyć czas wykonywania (*wskazówka*: zobacz plik `ArticleHelpers.cs` w projekcie [Microsoft.Azure.Batch.Samples.Common][github_samples_common] w repozytorium [azure-batch-samples][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="9ddc0-341">Add logic to check for and allow the use of an existing pool to speed execution time (*hint*: check out `ArticleHelpers.cs` in the [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="9ddc0-342">Po zapoznaniu się z podstawowym przepływem pracy rozwiązania w usłudze Batch nadszedł czas, aby poszerzyć wiedzę na temat dodatkowych funkcji tej usługi.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-342">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="9ddc0-343">Przejrzyj artykuł [Overview of Azure Batch features](batch-api-basics.md) (Omówienie funkcji w usłudze Azure Batch), który zalecamy użytkownikom rozpoczynającym korzystanie z tej usługi.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-343">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="9ddc0-344">Przeczytaj inne artykuły dotyczące programowania w usłudze Batch w części **Development in-depth** (Szczegółowy opis programowania) w [ścieżce szkoleniowej dotyczącej usługi Batch][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-344">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="9ddc0-345">Zapoznaj się z inną implementacją przetwarzania obciążenia „N najczęściej występujących słów” za pomocą usługi Batch w przykładzie [TopNWords][github_topnwords].</span><span class="sxs-lookup"><span data-stu-id="9ddc0-345">Check out a different implementation of processing the "top N words" workload by using Batch in the [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="9ddc0-346">Przejrzyj [informacje o wersji](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) platformy .NET dla usługi Batch, aby poznać najnowsze zmiany w bibliotece.</span><span class="sxs-lookup"><span data-stu-id="9ddc0-346">Review the Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for the latest changes in the library.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Tworzenie kontenerów w usłudze Azure Storage"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Przekazywanie aplikacji podzadań i plików danych wejściowych do kontenerów"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Tworzenie puli usługi Batch"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Tworzenie zadania w usłudze Batch"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Dodawanie podzadań do zadania"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Monitorowanie podzadań"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Pobieranie danych wyjściowych podzadań z usługi Storage"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Przepływ pracy w rozwiązaniu usługi Batch (pełny diagram)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Poświadczenia usługi Batch w portalu"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Poświadczenia usługi Storage w portalu"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Przepływ pracy rozwiązania w usłudze Batch (diagram minimalny)"
