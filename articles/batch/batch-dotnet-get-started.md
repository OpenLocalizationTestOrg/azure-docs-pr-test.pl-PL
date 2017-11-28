---
title: "aaaTutorial — Biblioteka klienta użyj hello partii zadań Azure dla platformy .NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello podstawowych pojęciach dotyczących partii zadań Azure i utworzenie rozwiązania do prostych przy użyciu platformy .NET."
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
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a><span data-ttu-id="d866c-103">Rozpoczynanie pracy kompilowanie rozwiązań za pomocą biblioteki klienta hello partii dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="d866c-103">Get started building solutions with hello Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d866c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d866c-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="d866c-105">Python</span><span class="sxs-lookup"><span data-stu-id="d866c-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="d866c-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="d866c-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="d866c-107">Dowiedz się podstawy hello [partii zadań Azure] [ azure_batch] i hello [partiami platformy .NET] [ net_api] biblioteki w tym artykule jako omówimy C# przykładowej aplikacji krok przez krok.</span><span class="sxs-lookup"><span data-stu-id="d866c-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="d866c-108">Przyjrzymy się jak hello Przykładowa aplikacja korzysta z tooprocess usługi partii hello równoległych obciążenia w chmurze hello i sposób interakcji z [usługi Azure Storage](../storage/common/storage-introduction.md) potrzeby przemieszczania plików i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="d866c-108">We look at how hello sample application leverages hello Batch service tooprocess a parallel workload in hello cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="d866c-109">Będzie informacje wspólnego przepływu pracy aplikacji partii i Uzyskaj podstawową wiedzę na temat hello głównych składników usługi partia zadań takich jak zadania, zadania, pul i węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="d866c-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="d866c-110">![Przepływ pracy rozwiązania w usłudze Batch (podstawowy)][11]</span><span class="sxs-lookup"><span data-stu-id="d866c-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="d866c-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d866c-111">Prerequisites</span></span>
<span data-ttu-id="d866c-112">W tym artykule założono, że masz praktyczną wiedzę na temat języka C# i programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d866c-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="d866c-113">Przyjęto założenie, że jesteś toosatisfy stanie hello tworzenie wymagania dotyczące konta określonych poniżej platformy Azure i hello partii i usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="d866c-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="d866c-114">Konta</span><span class="sxs-lookup"><span data-stu-id="d866c-114">Accounts</span></span>
* <span data-ttu-id="d866c-115">**Konto platformy Azure**: jeśli nie masz jeszcze subskrypcji platformy Azure, [utwórz bezpłatne konto platformy Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="d866c-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="d866c-116">**Konto usługi Batch**: po uzyskaniu subskrypcji platformy Azure [utwórz konto usługi Azure Batch](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d866c-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="d866c-117">**Konto magazynu**: zobacz sekcję [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) w temacie [Informacje o kontach magazynu Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d866c-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d866c-118">Obecnie partii obsługuje *tylko* hello **ogólnego przeznaczenia** typu konta magazynu, zgodnie z opisem w kroku #5 [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) w [o Azure konta magazynu](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d866c-118">Batch currently supports *only* hello **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="d866c-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d866c-119">Visual Studio</span></span>
<span data-ttu-id="d866c-120">Musi mieć **programu Visual Studio 2015 lub nowsza** toobuild hello przykładowy projekt.</span><span class="sxs-lookup"><span data-stu-id="d866c-120">You must have **Visual Studio 2015 or newer** toobuild hello sample project.</span></span> <span data-ttu-id="d866c-121">Bezpłatne i wersji próbnej wersji programu Visual Studio można znaleźć w hello [omówienie produktów Visual Studio][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="d866c-121">You can find free and trial versions of Visual Studio in hello [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="d866c-122">Przykład kodu *DotNetTutorial*</span><span class="sxs-lookup"><span data-stu-id="d866c-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="d866c-123">Witaj [DotNetTutorial] [ github_dotnettutorial] próbki jest jednym z hello wiele przykładów kodu partii znaleziony w hello [azure partii próbek] [ github_samples] repozytorium na GitHub.</span><span class="sxs-lookup"><span data-stu-id="d866c-123">hello [DotNetTutorial][github_dotnettutorial] sample is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="d866c-124">Wszystkie próbki hello można pobrać po kliknięciu **klonowania lub pobierania > Pobierz ZIP** na stronie głównej repozytorium hello lub przez kliknięcie przycisku hello [azure partii — przykłady master.zip] [ github_samples_zip]łącze bezpośrednie.</span><span class="sxs-lookup"><span data-stu-id="d866c-124">You can download all hello samples by clicking  **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="d866c-125">Po zostały wyodrębnione hello zawartość pliku ZIP hello, można znaleźć rozwiązania hello w hello następującego folderu:</span><span class="sxs-lookup"><span data-stu-id="d866c-125">Once you've extracted hello contents of hello ZIP file, you can find hello solution in hello following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="d866c-126">Azure Batch Explorer (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="d866c-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="d866c-127">Witaj [Eksploratora usługi partia zadań Azure] [ github_batchexplorer] to bezpłatne narzędzie, które znajduje się w hello [azure partii próbek] [ github_samples] repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="d866c-127">hello [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="d866c-128">Podczas toocomplete nie wymaga tego samouczka, może być przydatne podczas opracowywania i debugowania rozwiązań partii.</span><span class="sxs-lookup"><span data-stu-id="d866c-128">While not required toocomplete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="d866c-129">Omówienie przykładowego projektu DotNetTutorial</span><span class="sxs-lookup"><span data-stu-id="d866c-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="d866c-130">Witaj *DotNetTutorial* przykładowy kod jest rozwiązaniem Visual Studio, która zawiera dwa projekty: **DotNetTutorial** i **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="d866c-130">hello *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="d866c-131">**DotNetTutorial** jest aplikacją kliencką hello, która współdziała z tooexecute hello partii i magazynu usług równoległych obciążenie obliczeniowe węzłach (maszynach wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="d866c-131">**DotNetTutorial** is hello client application that interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="d866c-132">Aplikacja DotNetTutorial jest uruchamiana na lokalnej stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="d866c-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="d866c-133">**TaskApplication** to program hello, który jest uruchamiany na węzłach obliczeniowych Azure tooperform hello rzeczywistą pracę.</span><span class="sxs-lookup"><span data-stu-id="d866c-133">**TaskApplication** is hello program that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="d866c-134">W przykładowym hello `TaskApplication.exe` analizuje hello tekst w pliku, który został pobrany z usługi Azure Storage (plik wejściowy hello).</span><span class="sxs-lookup"><span data-stu-id="d866c-134">In hello sample, `TaskApplication.exe` parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="d866c-135">Następnie tworzy plik tekstowy (plik wyjściowy hello) zawierający listę hello trzy najważniejsze wyrazy, które pojawiają się w pliku wejściowym hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-135">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="d866c-136">Po utworzeniu pliku wyjściowego hello, TaskApplication przekazuje hello tooAzure pliku magazynu.</span><span class="sxs-lookup"><span data-stu-id="d866c-136">After it creates hello output file, TaskApplication uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="d866c-137">Dzięki temu aplikacja kliencka toohello dostępne do pobrania.</span><span class="sxs-lookup"><span data-stu-id="d866c-137">This makes it available toohello client application for download.</span></span> <span data-ttu-id="d866c-138">TaskApplication uruchamia się równolegle na wielu węzłach obliczeniowych w hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="d866c-138">TaskApplication runs in parallel on multiple compute nodes in hello Batch service.</span></span>

<span data-ttu-id="d866c-139">Witaj poniższym diagramie przedstawiono hello głównej operacje, które są wykonywane przez aplikację kliencką hello, *DotNetTutorial*i aplikacji hello, która jest wykonywana przez zadania hello *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="d866c-139">hello following diagram illustrates hello primary operations that are performed by hello client application, *DotNetTutorial*, and hello application that is executed by hello tasks, *TaskApplication*.</span></span> <span data-ttu-id="d866c-140">Ten podstawowy przepływ pracy jest typowy dla wielu rozwiązań obliczeniowych utworzonych za pomocą usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="d866c-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="d866c-141">Gdy nie wykazują wszystkich funkcji dostępnych w hello usługa partia zadań, niemal każdego scenariusza partii zawiera części ten przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="d866c-141">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="d866c-142">![Przykładowy przepływ pracy w usłudze Batch][8]</span><span class="sxs-lookup"><span data-stu-id="d866c-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="d866c-143">**Krok 1.**</span><span class="sxs-lookup"><span data-stu-id="d866c-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="d866c-144">Utwórz **kontenery** w usłudze Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d866c-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="d866c-145">
[**Krok 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="d866c-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="d866c-146">Pliki aplikacji zadania przekazywania i toocontainers plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="d866c-146">Upload task application files and input files toocontainers.</span></span><br/><span data-ttu-id="d866c-147">
[**Krok 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="d866c-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="d866c-148">Utwórz **pulę** w usłudze Batch.</span><span class="sxs-lookup"><span data-stu-id="d866c-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="d866c-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="d866c-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="d866c-150">Witaj puli **StartTask** pliki do pobrania hello toonodes pliki binarne (TaskApplication) zadań zgodnie z ich przyłączyć hello puli.</span><span class="sxs-lookup"><span data-stu-id="d866c-150">hello pool **StartTask** downloads hello task binary files (TaskApplication) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="d866c-151">
[**Krok 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="d866c-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="d866c-152">Utwórz **zadanie** w usłudze Batch.</span><span class="sxs-lookup"><span data-stu-id="d866c-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="d866c-153">
[**Krok 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="d866c-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="d866c-154">Dodaj **zadania** toohello zadania.</span><span class="sxs-lookup"><span data-stu-id="d866c-154">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="d866c-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="d866c-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="d866c-156">zadania Hello są zaplanowane tooexecute na węzłach.</span><span class="sxs-lookup"><span data-stu-id="d866c-156">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="d866c-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="d866c-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="d866c-158">Każde zadanie pobiera dane wejściowe z usługi Azure Storage, a następnie rozpoczyna się wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="d866c-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="d866c-159">
[**Krok 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="d866c-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="d866c-160">Monitoruj podzadania.</span><span class="sxs-lookup"><span data-stu-id="d866c-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="d866c-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="d866c-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="d866c-162">Jak czynności zostały wykonane, ich przekazywanie ich tooAzure danych wyjściowych magazynu.</span><span class="sxs-lookup"><span data-stu-id="d866c-162">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="d866c-163">
[**Krok 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="d866c-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="d866c-164">Pobierz dane wyjściowe podzadań z usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="d866c-164">Download task output from Storage.</span></span>

<span data-ttu-id="d866c-165">Jak wspomniano, nie każde rozwiązanie z partii wykonuje te kroki szczegółowe może obejmować wiele innych, ale hello *DotNetTutorial* aplikacja przykładowa prezentuje często używanych procesów, które można odnaleźć w rozwiązaniu partii.</span><span class="sxs-lookup"><span data-stu-id="d866c-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but hello *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-hello-dotnettutorial-sample-project"></a><span data-ttu-id="d866c-166">Tworzenie hello *DotNetTutorial* przykładowy projekt</span><span class="sxs-lookup"><span data-stu-id="d866c-166">Build hello *DotNetTutorial* sample project</span></span>
<span data-ttu-id="d866c-167">Można było pomyślnie uruchomić hello próbki, należy określić poświadczenia konta zarówno wsadowego i magazynowania w hello *DotNetTutorial* projektu `Program.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="d866c-167">Before you can successfully run hello sample, you must specify both Batch and Storage account credentials in hello *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="d866c-168">Jeśli jeszcze tego nie zrobiono, otwórz rozwiązanie hello w programie Visual Studio, klikając hello `DotNetTutorial.sln` pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d866c-168">If you have not done so already, open hello solution in Visual Studio by double-clicking hello `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="d866c-169">Lub otworzyć z poziomu programu Visual Studio za pomocą hello **Plik > Otwórz > Projekt/rozwiązanie** menu.</span><span class="sxs-lookup"><span data-stu-id="d866c-169">Or open it from within Visual Studio by using hello **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="d866c-170">Otwórz `Program.cs` w hello *DotNetTutorial* projektu.</span><span class="sxs-lookup"><span data-stu-id="d866c-170">Open `Program.cs` within hello *DotNetTutorial* project.</span></span> <span data-ttu-id="d866c-171">Następnie dodaj poświadczeń określonych hello górze pliku hello:</span><span class="sxs-lookup"><span data-stu-id="d866c-171">Then add your credentials as specified near hello top of hello file:</span></span>

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="d866c-172">Jak wspomniano powyżej, obecnie należy określić poświadczenia hello **ogólnego przeznaczenia** konta magazynu w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d866c-172">As mentioned above, you must currently specify hello credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="d866c-173">Aplikacje partii używać magazynu obiektów blob w ramach hello **ogólnego przeznaczenia** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d866c-173">Your Batch applications use blob storage within hello **general-purpose** storage account.</span></span> <span data-ttu-id="d866c-174">Nie określaj hello poświadczenia dla konta magazynu, który został utworzony przez wybranie hello *magazynu obiektów Blob* typ konta.</span><span class="sxs-lookup"><span data-stu-id="d866c-174">Do not specify hello credentials for a Storage account that was created by selecting hello *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="d866c-175">Poświadczenia konta wsadowego i magazynowania w bloku konta hello każdej usługi można znaleźć w hello [portalu Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="d866c-175">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="d866c-176">![Partii poświadczeń w portalu hello][9]
![magazynu poświadczeń w portalu hello][10]</span><span class="sxs-lookup"><span data-stu-id="d866c-176">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="d866c-177">Po zaktualizowaniu hello projektu przy użyciu poświadczeń, kliknij prawym przyciskiem myszy rozwiązanie hello w Eksploratorze rozwiązań i kliknij przycisk **Kompiluj rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="d866c-177">Now that you've updated hello project with your credentials, right-click hello solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="d866c-178">Witaj przywracania pakietów NuGet, upewnij się, jeśli zostanie wyświetlony monit.</span><span class="sxs-lookup"><span data-stu-id="d866c-178">Confirm hello restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="d866c-179">Jeśli nie przywrócono automatycznie pakietów NuGet hello lub zobacz błędy dotyczące pakietów hello toorestore błąd, upewnij się, że masz hello [Menedżera pakietów NuGet] [ nuget_packagemgr] zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="d866c-179">If hello NuGet packages are not automatically restored, or if you see errors about a failure toorestore hello packages, ensure that you have hello [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="d866c-180">Włącz pobieranie brakujących pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-180">Then enable hello download of missing packages.</span></span> <span data-ttu-id="d866c-181">Zobacz [włączenie pakietu przywrócić podczas kompilacji] [ nuget_restore] tooenable Pobieranie pakietu.</span><span class="sxs-lookup"><span data-stu-id="d866c-181">See [Enabling Package Restore During Build][nuget_restore] tooenable package download.</span></span>
>
>

<span data-ttu-id="d866c-182">W hello następujące sekcje możemy podzielić hello przykładowej aplikacji na powitania kroki wykonuje tooprocess obciążenia w hello usługa partia zadań i te kroki szczegółowo omówiono w nim.</span><span class="sxs-lookup"><span data-stu-id="d866c-182">In hello following sections, we break down hello sample application into hello steps that it performs tooprocess a workload in hello Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="d866c-183">Firma Microsoft zachęca toorefer toohello Otwórz rozwiązanie w programie Visual Studio podczas pracy swojemu za pośrednictwem hello dalszej części tego artykułu, ponieważ nie każdy wiersz kodu w przykładowym hello jest omówiona.</span><span class="sxs-lookup"><span data-stu-id="d866c-183">We encourage you toorefer toohello open solution in Visual Studio while you work your way through hello rest of this article, since not every line of code in hello sample is discussed.</span></span>

<span data-ttu-id="d866c-184">Przejdź do góry toohello hello `MainAsync` metoda hello *DotNetTutorial* projektu `Program.cs` pliku toostart z kroku 1.</span><span class="sxs-lookup"><span data-stu-id="d866c-184">Navigate toohello top of hello `MainAsync` method in hello *DotNetTutorial* project's `Program.cs` file toostart with Step 1.</span></span> <span data-ttu-id="d866c-185">Każdy krok poniżej, a następnie około odwołuje się postępu hello następujące metody `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="d866c-185">Each step below then roughly follows hello progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="d866c-186">Krok 1: tworzenie kontenerów w usłudze Storage</span><span class="sxs-lookup"><span data-stu-id="d866c-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="d866c-187">![Tworzenie kontenerów w usłudze Azure Storage][1]
</span><span class="sxs-lookup"><span data-stu-id="d866c-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="d866c-188">Usługa Batch ma wbudowaną funkcję obsługi interakcji z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d866c-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="d866c-189">Kontenery na koncie magazynu będzie udostępniać hello pliki wymagane przez hello zadania, które są uruchamiane na koncie usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="d866c-189">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="d866c-190">kontenery Hello udostępniają danych wyjściowych hello toostore miejsce, który tworzy hello zadania.</span><span class="sxs-lookup"><span data-stu-id="d866c-190">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="d866c-191">Po pierwsze Hello hello *DotNetTutorial* jest aplikacja kliencka jest utworzyć trzy kontenery w [magazyn obiektów Blob Azure](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="d866c-191">hello first thing hello *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="d866c-192">**Aplikacja**: ten kontener zapisze aplikacji hello uruchamiając hello zadania, jak również żadnego z jego zależności, takich jak biblioteki dll.</span><span class="sxs-lookup"><span data-stu-id="d866c-192">**application**: This container will store hello application run by hello tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="d866c-193">**wejściowy**: zadań pobierze tooprocess pliki danych hello z hello *wejściowych* kontenera.</span><span class="sxs-lookup"><span data-stu-id="d866c-193">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="d866c-194">**dane wyjściowe**: gdy zadania ukończyć przetwarzania pliku wejściowego, przekaże one hello wyniki toohello *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="d866c-194">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="d866c-195">W kolejności toointeract z magazynu kont i Utwórz kontenerów, używamy hello [biblioteki klienta magazynu Azure dla platformy .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="d866c-195">In order toointeract with a Storage account and create containers, we use hello [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="d866c-196">Możemy utworzyć konto toohello odwołanie z [CloudStorageAccount][net_cloudstorageaccount]i na którym utworzyć [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="d866c-196">We create a reference toohello account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="d866c-197">Używamy hello `blobClient` odwołania w całej aplikacji hello i przekaż go jako parametru metody tooseveral.</span><span class="sxs-lookup"><span data-stu-id="d866c-197">We use hello `blobClient` reference throughout hello application and pass it as a parameter tooseveral methods.</span></span> <span data-ttu-id="d866c-198">Na przykład znajduje się w bloku kodu hello poniższą hello powyżej, w którym nazywa się `CreateContainerIfNotExistAsync` tooactually utworzyć hello kontenerów.</span><span class="sxs-lookup"><span data-stu-id="d866c-198">An example of this is in hello code block that immediately follows hello above, where we call `CreateContainerIfNotExistAsync` tooactually create hello containers.</span></span>

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
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

<span data-ttu-id="d866c-199">Po utworzeniu hello kontenery aplikacji hello teraz przekazać hello pliki, które będą używane przez zadania hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="d866c-200">[Jak toouse magazynu obiektów Blob z .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) zawiera omówienie pracy z usługą Azure Storage kontenerów i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="d866c-200">[How toouse Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="d866c-201">Po rozpoczęciu pracy z instancją powinno być hello górze listy odczytu.</span><span class="sxs-lookup"><span data-stu-id="d866c-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="d866c-202">Krok 2: przekazanie aplikacji podzadań i plików danych</span><span class="sxs-lookup"><span data-stu-id="d866c-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="d866c-203">![Zadanie przekazywania aplikacji i wejściowych (dane) pliki toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="d866c-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="d866c-204">W pliku hello Przekaż operacji *DotNetTutorial* najpierw definiuje kolekcji **aplikacji** i **wejściowych** pliku ścieżki istniejących na komputerze lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-204">In hello file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="d866c-205">Następnie przekazanie tych kontenerach toohello pliki, które zostały utworzone w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="d866c-206">Istnieją dwie metody w `Program.cs` który są zaangażowane w procesu przekazywania hello:</span><span class="sxs-lookup"><span data-stu-id="d866c-206">There are two methods in `Program.cs` that are involved in hello upload process:</span></span>

* <span data-ttu-id="d866c-207">`UploadFilesToContainerAsync`: Ta metoda zwraca kolekcję [ResourceFile] [ net_resourcefile] obiektów (opisanych poniżej) i wewnętrznie wywołania `UploadFileToContainerAsync` tooupload każdego pliku przekazano hello *filePaths* parametru.</span><span class="sxs-lookup"><span data-stu-id="d866c-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` tooupload each file that is passed in hello *filePaths* parameter.</span></span>
* <span data-ttu-id="d866c-208">`UploadFileToContainerAsync`: Ta metoda hello faktycznie wykonuje hello przekazywania pliku i tworzy hello jest [ResourceFile] [ net_resourcefile] obiektów.</span><span class="sxs-lookup"><span data-stu-id="d866c-208">`UploadFileToContainerAsync`: This is hello method that actually performs hello file upload and creates hello [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="d866c-209">Po przekazaniu pliku hello, uzyskuje sygnatury dostępu współdzielonego (SAS) dla pliku hello i zwraca obiekt ResourceFile, który reprezentuje go.</span><span class="sxs-lookup"><span data-stu-id="d866c-209">After uploading hello file, it obtains a shared access signature (SAS) for hello file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="d866c-210">Sygnatury dostępu współdzielonego zostały również omówione poniżej.</span><span class="sxs-lookup"><span data-stu-id="d866c-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="d866c-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="d866c-211">ResourceFiles</span></span>
<span data-ttu-id="d866c-212">A [ResourceFile] [ net_resourcefile] zawiera zadania w partii hello adresu URL tooa plik z magazynu Azure, który jest pobrany tooa węźle obliczeń przed uruchomieniem tego zadania.</span><span class="sxs-lookup"><span data-stu-id="d866c-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="d866c-213">Witaj [ResourceFile.BlobSource] [ net_resourcefile_blobsource] właściwość określa hello pełny adres URL pliku hello, ponieważ znajduje się ona w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="d866c-213">hello [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="d866c-214">adres URL Hello mogą również obejmować sygnatury dostępu współdzielonego (SAS) zawiera plik toohello bezpiecznego dostępu.</span><span class="sxs-lookup"><span data-stu-id="d866c-214">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="d866c-215">Większość typów podzadań w usłudze Batch dla platformy .NET obejmuje właściwość *ResourceFiles*, w tym następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d866c-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="d866c-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="d866c-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="d866c-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="d866c-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="d866c-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="d866c-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="d866c-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="d866c-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="d866c-220">DotNetTutorial Przykładowa aplikacja Hello używają hello JobPreparationTask lub JobReleaseTask typy zadań, lecz więcej o nich w [węzły obliczeniowe uruchamianie działań przygotowania i kończenia zadania w partii zadań Azure](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="d866c-220">hello DotNetTutorial sample application does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="d866c-221">Sygnatura dostępu współdzielonego (SAS)</span><span class="sxs-lookup"><span data-stu-id="d866c-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="d866c-222">Ciągi są sygnatury dostępu współdzielonego, który — gdy dołączone jako część adresu URL — Podaj toocontainers bezpiecznego dostępu i obiekty BLOB w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d866c-222">Shared access signatures are strings which—when included as part of a URL—provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="d866c-223">Hello DotNetTutorial aplikacja korzysta z obu obiektów blob i kontener udostępnionych adresów URL sygnatury dostępu i pokazano, jak tooobtain te udostępniane dostęp ciągi podpisu z hello usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="d866c-223">hello DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="d866c-224">**Obiekt blob sygnatur dostępu współdzielonego**: hello puli StartTask w DotNetTutorial korzysta z sygnatur dostępu do udostępnionego obiektu blob podczas pobierania plików binarnych aplikacji hello i pliki danych wejściowych z magazynu (zobacz krok nr 3 poniżej).</span><span class="sxs-lookup"><span data-stu-id="d866c-224">**Blob shared access signatures**: hello pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads hello application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="d866c-225">Witaj `UploadFileToContainerAsync` metody w jego DotNetTutorial `Program.cs` zawiera hello kod, który uzyskuje sygnatury dostępu współdzielonego każdy obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="d866c-225">hello `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="d866c-226">Odbywa się to przez wywołanie metody [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="d866c-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="d866c-227">**Kontener sygnatury dostępu współdzielonego**: zgodnie z każdego zadania zakończy pracę w węźle obliczeń hello, zostanie przesłany jego dane wyjściowe pliku toohello *dane wyjściowe* kontenera w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="d866c-227">**Container shared access signatures**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="d866c-228">toodo, TaskApplication używa kontenera sygnatury dostępu współdzielonego, która zapewnia kontener toohello dostęp do zapisu jako część ścieżki hello, gdy jego przekazuje plik hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-228">toodo so, TaskApplication uses a container shared access signature that provides write access toohello container as part of hello path when it uploads hello file.</span></span> <span data-ttu-id="d866c-229">Uzyskiwanie sygnatury dostępu współdzielonego kontenera hello odbywa się w podobny sposób jak podczas uzyskiwania blob hello udostępnionych sygnatury dostępu.</span><span class="sxs-lookup"><span data-stu-id="d866c-229">Obtaining hello container shared access signature is done in a similar fashion as when obtaining hello blob shared access signature.</span></span> <span data-ttu-id="d866c-230">W DotNetTutorial, możesz znaleźć tego hello `GetContainerSasUrl` wywołania metody pomocnika [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo tak.</span><span class="sxs-lookup"><span data-stu-id="d866c-230">In DotNetTutorial, you will find that hello `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] toodo so.</span></span> <span data-ttu-id="d866c-231">Będzie przeczytać więcej informacji o używaniu kontenera hello TaskApplication udostępnionych sygnatury dostępu w "krok 6: zadań monitorowania."</span><span class="sxs-lookup"><span data-stu-id="d866c-231">You'll read more about how TaskApplication uses hello container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="d866c-232">Wyewidencjonowanie hello dwuczęściową serii na sygnatur dostępu współdzielonego [część 1: hello Opis udostępnionych model sygnatury dostępu Współdzielonego dostępu](../storage/common/storage-dotnet-shared-access-signature-part-1.md) i [część 2: tworzenie i używanie sygnatury dostępu współdzielonego (SAS) z magazynu obiektów Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn więcej informacji na temat zapewnianie bezpiecznego dostępu toodata na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="d866c-232">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="d866c-233">Krok 3: tworzenie puli usługi Batch</span><span class="sxs-lookup"><span data-stu-id="d866c-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="d866c-234">![Tworzenie puli usługi Batch][3]
</span><span class="sxs-lookup"><span data-stu-id="d866c-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="d866c-235">**Pula** usługi Batch jest kolekcją węzłów obliczeniowych (maszyn wirtualnych), w których usługa Batch wykonuje podzadania danego zadania.</span><span class="sxs-lookup"><span data-stu-id="d866c-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="d866c-236">Po przekazaniu aplikacji hello i toohello pliki danych konta magazynu z interfejsami API magazynu Azure, *DotNetTutorial* rozpoczyna wprowadzanie usługa partia zadań toohello wywołania z interfejsów API dostarczonych przez hello biblioteki partiami platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="d866c-236">After uploading hello application and data files toohello Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls toohello Batch service with APIs provided by hello Batch .NET library.</span></span> <span data-ttu-id="d866c-237">Witaj kod najpierw tworzy [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="d866c-237">hello code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="d866c-238">Następnie próbki hello tworzona jest pula węzłów obliczeniowych w hello konta usługi partia zadań przy użyciu wywołania zbyt`CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="d866c-238">Next, hello sample creates a pool of compute nodes in hello Batch account with a call too`CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="d866c-239">`CreatePoolIfNotExistsAsync`używa hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create] toocreate metody nowej puli w hello usługa partia zadań:</span><span class="sxs-lookup"><span data-stu-id="d866c-239">`CreatePoolIfNotExistsAsync` uses hello [BatchClient.PoolOperations.CreatePool][net_pool_create] method toocreate a new pool in hello Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="d866c-240">Po utworzeniu puli z [CreatePool][net_pool_create], można określić kilka parametrów, takich jak hello liczba węzłów obliczeniowych hello [rozmiar węzłów hello](../cloud-services/cloud-services-sizes-specs.md), i hello operacyjnego węzłów System.</span><span class="sxs-lookup"><span data-stu-id="d866c-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as hello number of compute nodes, hello [size of hello nodes](../cloud-services/cloud-services-sizes-specs.md), and hello nodes' operating system.</span></span> <span data-ttu-id="d866c-241">W *DotNetTutorial*, używamy [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify systemu Windows Server 2012 R2 z [usługi w chmurze](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="d866c-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="d866c-242">Można również tworzyć pule węzły obliczeniowe, które są maszynach wirtualnych Azure (VM), określając hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d866c-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying hello [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="d866c-243">Pulę węzłów obliczeniowych maszyn wirtualnych można utworzyć na podstawie [obrazów systemu Linux](batch-linux-nodes.md) lub Windows.</span><span class="sxs-lookup"><span data-stu-id="d866c-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="d866c-244">Źródło Hello obrazów maszyny Wirtualnej można:</span><span class="sxs-lookup"><span data-stu-id="d866c-244">hello source for your VM images can be either:</span></span>

- <span data-ttu-id="d866c-245">Hello [Marketplace maszyny wirtualne Azure][vm_marketplace], co umożliwia obrazów systemów Windows i Linux, które są gotowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="d866c-245">hello [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="d866c-246">Obraz niestandardowy przygotowywany i udostępniany przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d866c-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="d866c-247">Aby uzyskać szczegółowe informacje o obrazach niestandardowych, zobacz [Tworzenie rozbudowanych rozwiązań przetwarzania równoległego przy użyciu usługi Batch](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="d866c-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d866c-248">W usłudze Batch opłaty są naliczane za zasoby obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="d866c-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="d866c-249">koszty toominimize można obniżyć `targetDedicatedComputeNodes` too1 przed uruchomieniem hello próbki.</span><span class="sxs-lookup"><span data-stu-id="d866c-249">toominimize costs, you can lower `targetDedicatedComputeNodes` too1 before you run hello sample.</span></span>
>
>

<span data-ttu-id="d866c-250">Wraz z tych właściwości węzła fizycznego, można również określić [StartTask] [ net_pool_starttask] hello puli.</span><span class="sxs-lookup"><span data-stu-id="d866c-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for hello pool.</span></span> <span data-ttu-id="d866c-251">Hello StartTask wykonywane na każdym węźle, ponieważ ten węzeł dołącza hello puli i każdym uruchomieniu węzła.</span><span class="sxs-lookup"><span data-stu-id="d866c-251">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="d866c-252">Witaj StartTask jest szczególnie przydatna w przypadku instalowania aplikacji na węzły obliczeniowe wcześniejsze toohello wykonywanie zadań.</span><span class="sxs-lookup"><span data-stu-id="d866c-252">hello StartTask is especially useful for installing applications on compute nodes prior toohello execution of tasks.</span></span> <span data-ttu-id="d866c-253">Na przykład zadań przetwarzania danych przy użyciu skryptów języka Python, można użyć tooinstall StartTask Python na powitania węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="d866c-253">For example, if your tasks process data by using Python scripts, you could use a StartTask tooinstall Python on hello compute nodes.</span></span>

<span data-ttu-id="d866c-254">W tej przykładowej aplikacji hello StartTask kopiuje hello pliki, które pobiera z magazynu (które są określane przy użyciu hello [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] właściwości) z hello StartTask pracy katalogu toohello udostępnionego katalogu który *wszystkie* zadań uruchomionych w węźle hello może uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="d866c-254">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from hello StartTask working directory toohello shared directory that *all* tasks running on hello node can access.</span></span> <span data-ttu-id="d866c-255">Zasadniczo spowoduje to skopiowanie `TaskApplication.exe` i jego zależności toohello udostępniony katalog w każdym węźle jako węzeł hello dołącza pulę hello tak, aby wszystkie zadania, które będą uruchamiane w węźle hello do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="d866c-255">Essentially, this copies `TaskApplication.exe` and its dependencies toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="d866c-256">Witaj **pakietów aplikacji** funkcji partii zadań Azure zapewnia inny sposób tooget na powitania węzłów obliczeniowych w puli aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d866c-256">hello **application packages** feature of Azure Batch provides another way tooget your application onto hello compute nodes in a pool.</span></span> <span data-ttu-id="d866c-257">Zobacz [wdrożyć aplikacje toocompute węzły z pakietami aplikacji partii](batch-application-packages.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d866c-257">See [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="d866c-258">Godny uwagi we fragmencie kodu hello powyżej jest również użycie Witaj dwie zmienne środowiskowe w hello *CommandLine* właściwości hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` i `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="d866c-258">Also notable in hello code snippet above is hello use of two environment variables in hello *CommandLine* property of hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="d866c-259">Każdy węzeł obliczeniowy w puli partii jest automatycznie konfigurowany z kilku zmiennych środowiskowych, które są określone tooBatch.</span><span class="sxs-lookup"><span data-stu-id="d866c-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="d866c-260">Żaden proces, która jest wykonywana przez zadanie ma zmienne środowiskowe toothese dostępu.</span><span class="sxs-lookup"><span data-stu-id="d866c-260">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="d866c-261">toofind więcej informacji na temat hello zmiennych środowiskowych, które są dostępne w węzłach obliczeń w puli partii i informacji na temat zadań katalogów roboczych, zobacz hello [ustawienia środowiska dla zadań](batch-api-basics.md#environment-settings-for-tasks) i [plików i katalogów ](batch-api-basics.md#files-and-directories) części hello [Przegląd funkcji partii dla deweloperów](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="d866c-261">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see hello [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in hello [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="d866c-262">Krok 4: tworzenie zadania w usłudze Batch</span><span class="sxs-lookup"><span data-stu-id="d866c-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="d866c-263">![Tworzenie zadania w usłudze Batch][4]</span><span class="sxs-lookup"><span data-stu-id="d866c-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="d866c-264">**Zadanie** usługi Batch jest kolekcją podzadań i jest skojarzone z pulą węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="d866c-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="d866c-265">wykonanie Hello zadań w ramach zadania w węzłach obliczeń puli hello skojarzone.</span><span class="sxs-lookup"><span data-stu-id="d866c-265">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="d866c-266">Można użyć zadania nie tylko do organizowaniu i śledzenia zadań w powiązanych obciążeń pracą, ale nakładaniu pewne ograniczenia — takie jak hello maksymalną czasu wykonywania zadania hello (i przez rozszerzenie, jego zadań podrzędnych), a także priorytet zadania w zadaniach tooother relacji hello partii konto.</span><span class="sxs-lookup"><span data-stu-id="d866c-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) as well as job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="d866c-267">W tym przykładzie jednak hello zadanie jest skojarzone tylko z pulą hello, który został utworzony w kroku #3.</span><span class="sxs-lookup"><span data-stu-id="d866c-267">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="d866c-268">Żadne dodatkowe właściwości nie są konfigurowane.</span><span class="sxs-lookup"><span data-stu-id="d866c-268">No additional properties are configured.</span></span>

<span data-ttu-id="d866c-269">Wszystkie zadania usługi Batch są skojarzone z określoną pulą.</span><span class="sxs-lookup"><span data-stu-id="d866c-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="d866c-270">To skojarzenie wskazuje węzły, które hello zadania będą wykonywane na.</span><span class="sxs-lookup"><span data-stu-id="d866c-270">This association indicates which nodes hello job's tasks will execute on.</span></span> <span data-ttu-id="d866c-271">Określ to przy użyciu hello [CloudJob.PoolInformation] [ net_job_poolinfo] właściwości, jak pokazano w hello poniższy fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="d866c-271">You specify this by using hello [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in hello code snippet below.</span></span>

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

<span data-ttu-id="d866c-272">Teraz, kiedy zadania został utworzony, zadania są dodawane tooperform hello pracy.</span><span class="sxs-lookup"><span data-stu-id="d866c-272">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="d866c-273">Krok 5: Dodawanie toojob zadań</span><span class="sxs-lookup"><span data-stu-id="d866c-273">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="d866c-274">![Dodaj toojob zadań][5]</span><span class="sxs-lookup"><span data-stu-id="d866c-274">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="d866c-275">
*(1) zadania są dodawane toohello zadania, zadania (2) hello są zaplanowane toorun w węzłach i (3) hello zadania Pobierz tooprocess pliki danych hello*</span><span class="sxs-lookup"><span data-stu-id="d866c-275">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="d866c-276">Wsadowe **zadania** są hello poszczególnych jednostek pracy wykonywanych na powitania węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="d866c-276">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="d866c-277">Zadanie ma wiersza polecenia i uruchamia hello skrypty lub pliki wykonywalne, w tym wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="d866c-277">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="d866c-278">tooactually wykonywania pracy, zadań, należy dodać tooa zadania.</span><span class="sxs-lookup"><span data-stu-id="d866c-278">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="d866c-279">Każdy [CloudTask] [ net_task] jest konfigurowana przy użyciu właściwości wiersza polecenia i [ResourceFiles] [ net_task_resourcefiles] (tak jak StartTask hello puli) który zadanie Hello pobiera węzła toohello przed jego wiersza polecenia jest wykonywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d866c-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="d866c-280">W hello *DotNetTutorial* przykładowy projekt, każde zadanie przetwarza tylko jeden plik.</span><span class="sxs-lookup"><span data-stu-id="d866c-280">In hello *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="d866c-281">W związku z tym jego kolekcja ResourceFiles zawiera jeden element.</span><span class="sxs-lookup"><span data-stu-id="d866c-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
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

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="d866c-282">Podczas uzyskiwania dostępu do zmiennych środowiskowych takich jak `%AZ_BATCH_NODE_SHARED_DIR%` lub wykonywanie aplikacji nie można odnaleźć w węźle hello `PATH`, wiersze poleceń zadań musi być poprzedzona znakiem `cmd /c`.</span><span class="sxs-lookup"><span data-stu-id="d866c-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in hello node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="d866c-283">Zostanie jawnie wykonania hello interpreter poleceń i poinstruować go tooterminate po przeprowadzeniu polecenia.</span><span class="sxs-lookup"><span data-stu-id="d866c-283">This will explicitly execute hello command interpreter and instruct it tooterminate after carrying out your command.</span></span> <span data-ttu-id="d866c-284">To wymaganie nie jest konieczne, jeśli zadania wykonywania aplikacji w węźle hello `PATH` (takich jak *robocopy.exe* lub *powershell.exe*) i są używane nie zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="d866c-284">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="d866c-285">W ramach hello `foreach` pętli we fragmencie kodu hello powyżej, zobaczysz, że hello wiersz polecenia dla zadania hello jest tworzony w taki sposób, że trzech argumentów wiersza polecenia są przekazywane za*TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="d866c-285">Within hello `foreach` loop in hello code snippet above, you can see that hello command line for hello task is constructed such that three command-line arguments are passed too*TaskApplication.exe*:</span></span>

1. <span data-ttu-id="d866c-286">Witaj **pierwszy argument** to ścieżka hello hello tooprocess pliku.</span><span class="sxs-lookup"><span data-stu-id="d866c-286">hello **first argument** is hello path of hello file tooprocess.</span></span> <span data-ttu-id="d866c-287">To jest plik toohello ścieżka lokalna hello, ponieważ znajduje się w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-287">This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="d866c-288">Gdy hello obiektu ResourceFile w `UploadFileToContainerAsync` została pierwotnie utworzona powyżej, nazwa pliku hello została użyta dla tej właściwości (jako parametru konstruktora ResourceFile toohello).</span><span class="sxs-lookup"><span data-stu-id="d866c-288">When hello ResourceFile object in `UploadFileToContainerAsync` was first created above, hello file name was used for this property (as a parameter toohello ResourceFile constructor).</span></span> <span data-ttu-id="d866c-289">Wskazuje, czy plik hello znajdują się w hello takie same katalogu jako *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="d866c-289">This indicates that hello file can be found in hello same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="d866c-290">Witaj **drugi argument** Określa, że top hello *N* wyrazy mają być zapisywane toohello pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="d866c-290">hello **second argument** specifies that hello top *N* words should be written toohello output file.</span></span> <span data-ttu-id="d866c-291">W przykładowym hello to jest ustalony, aby top trzy słowa hello są zapisywane toohello pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="d866c-291">In hello sample, this is hard-coded so that hello top three words are written toohello output file.</span></span>
3. <span data-ttu-id="d866c-292">Witaj **trzeci argument** jest sygnatury dostępu współdzielonego hello (SAS), która zapewnia dostęp do zapisu toohello **dane wyjściowe** kontenera w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="d866c-292">hello **third argument** is hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="d866c-293">*TaskApplication.exe* używa tego wspólnego dostępu podpisu adresu URL, gdy przekazuje on tooAzure pliku wyjściowego hello magazynu.</span><span class="sxs-lookup"><span data-stu-id="d866c-293">*TaskApplication.exe* uses this shared access signature URL when it uploads hello output file tooAzure Storage.</span></span> <span data-ttu-id="d866c-294">Witaj kodu dla tego można znaleźć w hello `UploadFileToContainer` metody w projekcie TaskApplication hello `Program.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="d866c-294">You can find hello code for this in hello `UploadFileToContainer` method in hello TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
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

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="d866c-295">Krok 6: monitorowanie podzadań</span><span class="sxs-lookup"><span data-stu-id="d866c-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="d866c-296">![Monitorowanie podzadań][6]</span><span class="sxs-lookup"><span data-stu-id="d866c-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="d866c-297">
*powitania klienta aplikacji (1) monitory hello zadań związanych uzupełniania i stan sukcesu i (2) hello zadania przekazywania wynik danych tooAzure magazynu*</span><span class="sxs-lookup"><span data-stu-id="d866c-297">
*hello client application (1) monitors hello tasks for completion and success status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="d866c-298">Jeśli zadania zostaną dodane zadania tooa, są automatycznie w kolejce i zaplanowane do uruchomienia w węzłach obliczeń w puli hello skojarzone z zadaniem hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-298">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="d866c-299">Na podstawie hello ustawień przez użytkownika, partii obsługuje wszystkich zadań usługi kolejkowania, planowania, ponawianie próby i obowiązków administracyjnych innych zadań za Ciebie.</span><span class="sxs-lookup"><span data-stu-id="d866c-299">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="d866c-300">Istnieje wiele metod toomonitoring wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="d866c-300">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="d866c-301">Aplikacja DotNetTutorial stanowi prosty przykład zgłaszania tylko w przypadku ukończenia oraz stanów powodzenia lub niepowodzenia.</span><span class="sxs-lookup"><span data-stu-id="d866c-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="d866c-302">W ramach hello `MonitorTasks` metody w jego DotNetTutorial `Program.cs`, istnieją trzy pojęcia partiami platformy .NET, które gwarantuje dyskusji.</span><span class="sxs-lookup"><span data-stu-id="d866c-302">Within hello `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="d866c-303">Są one wymienione poniżej w kolejności ich występowania:</span><span class="sxs-lookup"><span data-stu-id="d866c-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="d866c-304">**ODATADetailLevel**: określenie funkcji [ODATADetailLevel][net_odatadetaillevel] na liście operacji (takich jak uzyskanie listy podzadań zadania) jest niezbędne do zapewnienia wydajności aplikacji usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="d866c-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="d866c-305">Dodaj [wydajnie zapytania usługi partia zadań Azure hello](batch-efficient-list-queries.md) tooyour odczytywania listy, jeśli planujesz wykonanie dowolny rodzaj monitorowanie stanu w aplikacjach partii.</span><span class="sxs-lookup"><span data-stu-id="d866c-305">Add [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md) tooyour reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="d866c-306">**TaskStateMonitor**: funkcja [TaskStateMonitor][net_taskstatemonitor] zapewnia aplikacjom usługi Batch dla platformy .NET narzędzia pomocy do monitorowania stanów podzadań.</span><span class="sxs-lookup"><span data-stu-id="d866c-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="d866c-307">W `MonitorTasks`, *DotNetTutorial* czeka na wszystkich zadań tooreach [TaskState.Completed] [ net_taskstate] przed upływem limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="d866c-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks tooreach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="d866c-308">Następnie kończy zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-308">Then it terminates hello job.</span></span>
3. <span data-ttu-id="d866c-309">**TerminateJobAsync**: przerywanie zadania o [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (lub hello blokuje JobOperations.TerminateJob) oznacza to zadanie jako zakończone.</span><span class="sxs-lookup"><span data-stu-id="d866c-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or hello blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="d866c-310">Jest ważne toodo tak więc jeśli rozwiązanie partii używa [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="d866c-310">It is essential toodo so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="d866c-311">Jest to szczególny typ podzadania, który opisano w temacie [Job preparation and completion tasks](batch-job-prep-release.md) (Przygotowanie zadania i podzadania związane z ukończeniem).</span><span class="sxs-lookup"><span data-stu-id="d866c-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="d866c-312">Witaj `MonitorTasks` metody z *DotNetTutorial*w `Program.cs` pojawia się poniżej:</span><span class="sxs-lookup"><span data-stu-id="d866c-312">hello `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
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

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="d866c-313">Krok 7: pobranie danych wyjściowych podzadań</span><span class="sxs-lookup"><span data-stu-id="d866c-313">Step 7: Download task output</span></span>
<span data-ttu-id="d866c-314">![Pobieranie danych wyjściowych zadań podrzędnych z usługi Storage][7]</span><span class="sxs-lookup"><span data-stu-id="d866c-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="d866c-315">Teraz, hello ukończenia zadania, dane wyjściowe zadania hello hello można pobrać z magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d866c-315">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="d866c-316">Odbywa się przy użyciu wywołania zbyt`DownloadBlobsFromContainerAsync` w *DotNetTutorial*w `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d866c-316">This is done with a call too`DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="d866c-317">Witaj wywołanie za`DownloadBlobsFromContainerAsync` w hello *DotNetTutorial* aplikacji określa, że pliki hello powinny być pobrany tooyour `%TEMP%` folderu.</span><span class="sxs-lookup"><span data-stu-id="d866c-317">hello call too`DownloadBlobsFromContainerAsync` in hello *DotNetTutorial* application specifies that hello files should be downloaded tooyour `%TEMP%` folder.</span></span> <span data-ttu-id="d866c-318">Możesz wolnego toomodify to lokalizacji wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="d866c-318">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="d866c-319">Krok 8: usuwanie kontenerów</span><span class="sxs-lookup"><span data-stu-id="d866c-319">Step 8: Delete containers</span></span>
<span data-ttu-id="d866c-320">Naliczane są opłaty za dane przechowywane w usłudze Azure Storage, dlatego jest zawsze blob tooremove dobrym rozwiązaniem, które nie są już potrzebne dla zadań wsadowych.</span><span class="sxs-lookup"><span data-stu-id="d866c-320">Because you are charged for data that resides in Azure Storage, it's always a good idea tooremove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="d866c-321">W jego DotNetTutorial `Program.cs`, jest to zrobić za pomocą metody pomocniczej toohello trzy wywołania `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="d866c-321">In DotNetTutorial's `Program.cs`, this is done with three calls toohello helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="d866c-322">metody Hello jedynie uzyskuje kontenera toohello odwołania, a następnie wywołuje [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="d866c-322">hello method itself merely obtains a reference toohello container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

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

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="d866c-323">Krok 9: Usuwanie hello zadania i hello puli</span><span class="sxs-lookup"><span data-stu-id="d866c-323">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="d866c-324">W ostatnim kroku hello jest monitem toodelete hello zadania i hello puli utworzone przez aplikację DotNetTutorial hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-324">In hello final step, you're prompted toodelete hello job and hello pool that were created by hello DotNetTutorial application.</span></span> <span data-ttu-id="d866c-325">Mimo że nie są naliczane opłaty za same zadania i podzadania, *są* naliczane opłaty za węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="d866c-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="d866c-326">W związku z tym zaleca się przydzielanie węzłów tylko zależnie do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="d866c-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="d866c-327">Usuwanie nieużywanych pul może odbywać się podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="d866c-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="d866c-328">Witaj BatchClient [JobOperations] [ net_joboperations] i [PoolOperations] [ net_pooloperations] mają odpowiednie metody usunięcia, które są nazywane, jeśli Hello użytkownika stanowi potwierdzenie usunięcia:</span><span class="sxs-lookup"><span data-stu-id="d866c-328">hello BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if hello user confirms deletion:</span></span>

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
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
> <span data-ttu-id="d866c-329">Należy pamiętać, że opłaty są naliczane za zasoby obliczeniowe — usunięcie nieużywanych pul zminimalizuje koszty.</span><span class="sxs-lookup"><span data-stu-id="d866c-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="d866c-330">Ponadto należy pamiętać, że usunięcie puli spowoduje usunięcie wszystkich węzłów obliczeniowych w tej puli, a wszystkie dane na powitania węzły będą nieodwracalny po usunięciu hello puli.</span><span class="sxs-lookup"><span data-stu-id="d866c-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-dotnettutorial-sample"></a><span data-ttu-id="d866c-331">Uruchom hello *DotNetTutorial* próbki</span><span class="sxs-lookup"><span data-stu-id="d866c-331">Run hello *DotNetTutorial* sample</span></span>
<span data-ttu-id="d866c-332">Po uruchomieniu hello przykładowej aplikacji, dane wyjściowe konsoli hello będzie podobne następujące toohello.</span><span class="sxs-lookup"><span data-stu-id="d866c-332">When you run hello sample application, hello console output will be similar toohello following.</span></span> <span data-ttu-id="d866c-333">W czasie wykonywania wystąpią wstrzymany w `Awaiting task completion, timeout in 00:30:00...` podczas puli hello węzły obliczeniowe są uruchamiane.</span><span class="sxs-lookup"><span data-stu-id="d866c-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while hello pool's compute nodes are started.</span></span> <span data-ttu-id="d866c-334">Użyj hello [portalu Azure] [ azure_portal] toomonitor puli, węzły obliczeniowe, zadań i zadań podczas i po zakończeniu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d866c-334">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="d866c-335">Użyj hello [portalu Azure] [ azure_portal] lub hello [Eksploratora usługi Storage Azure] [ storage_explorers] zasobów magazynu hello tooview (kontenerów i obiektów blob) znajdujących się utworzone przez aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-335">Use hello [Azure portal][azure_portal] or hello [Azure Storage Explorer][storage_explorers] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

<span data-ttu-id="d866c-336">Typowy czas wykonywania jest **około 5 minut** po uruchomieniu aplikacji hello w konfiguracji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="d866c-336">Typical execution time is **approximately 5 minutes** when you run hello application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="d866c-337">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d866c-337">Next steps</span></span>
<span data-ttu-id="d866c-338">Uznać za zmiany wolnego toomake*DotNetTutorial* i *TaskApplication* tooexperiment innej obliczania scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="d866c-338">Feel free toomake changes too*DotNetTutorial* and *TaskApplication* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="d866c-339">Na przykład, spróbuj opóźnienie wykonywania zbyt*TaskApplication*, takich jak [Thread.Sleep][net_thread_sleep], toosimulate długotrwałych zadań i monitorować je w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-339">For example, try adding an execution delay too*TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="d866c-340">Spróbuj dodać więcej zadań lub dostosowanie hello liczba węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="d866c-340">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="d866c-341">Dodaj logikę toocheck dla i Zezwalaj na użycie hello istniejących czas wykonywania toospeed puli (*wskazówka*: Zapoznaj się z `ArticleHelpers.cs` w hello [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] projektu w [azure partii próbek][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="d866c-341">Add logic toocheck for and allow hello use of an existing pool toospeed execution time (*hint*: check out `ArticleHelpers.cs` in hello [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="d866c-342">Teraz, kiedy znasz hello podstawowy przepływ pracy rozwiązania partii, jest toodig czasu w toohello dodatkowe funkcje hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="d866c-342">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="d866c-343">Przejrzyj hello [funkcji partii omówienie Azure](batch-api-basics.md) artykułu, w którym firma Microsoft zaleca, jeśli masz nową usługę toohello.</span><span class="sxs-lookup"><span data-stu-id="d866c-343">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="d866c-344">Uruchomienie hello inne artykuły programowanie partii w obszarze **programowanie szczegółowe** w hello [ścieżka szkoleniowa dotycząca partii][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="d866c-344">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="d866c-345">Zapoznaj się z inną implementację przetwarzania obciążenia hello "pierwszych N słów" za pomocą partii w hello [TopNWords] [ github_topnwords] próbki.</span><span class="sxs-lookup"><span data-stu-id="d866c-345">Check out a different implementation of processing hello "top N words" workload by using Batch in hello [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="d866c-346">Przejrzyj hello partiami platformy .NET [informacje o wersji](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) hello najnowszych zmian w bibliotece hello.</span><span class="sxs-lookup"><span data-stu-id="d866c-346">Review hello Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for hello latest changes in hello library.</span></span>

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
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Zadanie przekazywania aplikacji i wejściowych (dane) pliki toocontainers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Tworzenie puli usługi Batch"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Tworzenie zadania w usłudze Batch"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Dodaj toojob zadań"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Monitorowanie podzadań"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Pobieranie danych wyjściowych podzadań z usługi Storage"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Przepływ pracy w rozwiązaniu usługi Batch (pełny diagram)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Poświadczenia usługi Batch w portalu"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Poświadczenia usługi Storage w portalu"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Przepływ pracy rozwiązania w usłudze Batch (diagram minimalny)"
