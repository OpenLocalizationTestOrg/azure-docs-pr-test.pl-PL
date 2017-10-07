---
title: "aaaTutorial - hello Użyj zestawu SDK usługi partia zadań Azure dla języka Python | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello podstawowych pojęciach dotyczących partii zadań Azure i utworzenie rozwiązania do prostych przy użyciu języka Python."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a><span data-ttu-id="e5f8b-103">Rozpoczynanie pracy z hello partii zestawu SDK dla języka Python</span><span class="sxs-lookup"><span data-stu-id="e5f8b-103">Get started with hello Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5f8b-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e5f8b-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="e5f8b-105">Python</span><span class="sxs-lookup"><span data-stu-id="e5f8b-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="e5f8b-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="e5f8b-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="e5f8b-107">Dowiedz się podstawy hello [partii zadań Azure] [ azure_batch] i hello [Python partii] [ py_azure_sdk] klienta jako omówimy małych aplikacji partii napisanych w języku Python.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="e5f8b-108">Opisano, jak dwie przykładowe skrypty Użyj hello partii usługi tooprocess równoległe obciążenie maszyn wirtualnych systemu Linux w chmurze hello i sposób ich interakcji z [usługi Azure Storage](../storage/common/storage-introduction.md) potrzeby przemieszczania plików i odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-108">We look at how two sample scripts use hello Batch service tooprocess a parallel workload on Linux virtual machines in hello cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="e5f8b-109">Będzie informacje wspólnego przepływu pracy aplikacji partii i Uzyskaj podstawową wiedzę na temat hello głównych składników usługi partia zadań takich jak zadania, zadania, pul i węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="e5f8b-110">![Przepływ pracy rozwiązania w usłudze Batch (podstawowy)][11]</span><span class="sxs-lookup"><span data-stu-id="e5f8b-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="e5f8b-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e5f8b-111">Prerequisites</span></span>
<span data-ttu-id="e5f8b-112">W tym artykule założono, że masz praktyczną wiedzę dotyczącą języka Python oraz znasz system Linux.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="e5f8b-113">Przyjęto założenie, że jesteś toosatisfy stanie hello tworzenie wymagania dotyczące konta określonych poniżej platformy Azure i hello partii i usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="e5f8b-114">Konta</span><span class="sxs-lookup"><span data-stu-id="e5f8b-114">Accounts</span></span>
* <span data-ttu-id="e5f8b-115">**Konto platformy Azure**: jeśli nie masz jeszcze subskrypcji platformy Azure, [utwórz bezpłatne konto platformy Azure][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="e5f8b-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="e5f8b-116">**Konto usługi Batch**: po uzyskaniu subskrypcji platformy Azure [utwórz konto usługi Azure Batch](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="e5f8b-117">**Konto magazynu**: zobacz sekcję [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) w temacie [Informacje o kontach magazynu Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="e5f8b-118">Przykład kodu</span><span class="sxs-lookup"><span data-stu-id="e5f8b-118">Code sample</span></span>
<span data-ttu-id="e5f8b-119">Samouczek Python Hello [przykładowy kod] [ github_article_samples] jest jednym z hello wiele przykładów kodu partii znaleziony w hello [azure partii próbek] [ github_samples] repozytorium na GitHub.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-119">hello Python tutorial [code sample][github_article_samples] is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="e5f8b-120">Wszystkie próbki hello można pobrać po kliknięciu **klonowania lub pobierania > Pobierz ZIP** na stronie głównej repozytorium hello lub przez kliknięcie przycisku hello [azure partii — przykłady master.zip] [ github_samples_zip]łącze bezpośrednie.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-120">You can download all hello samples by clicking **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="e5f8b-121">Gdy już wyodrębniono zawartość pliku ZIP hello hello hello dwa skrypty w tym samouczku znajdują się w hello `article_samples` katalogu:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-121">Once you've extracted hello contents of hello ZIP file, hello two scripts for this tutorial are found in hello `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="e5f8b-122">Środowisko Python</span><span class="sxs-lookup"><span data-stu-id="e5f8b-122">Python environment</span></span>
<span data-ttu-id="e5f8b-123">Witaj toorun *python_tutorial_client.py* przykładowy skrypt na na lokalnej stacji roboczej, należy **interpreter języka Python** zgodny z wersją **2.7** lub **3.3 +**.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-123">toorun hello *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="e5f8b-124">skrypt Hello przetestowano na systemie Linux i Windows.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-124">hello script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="e5f8b-125">Zależności kryptograficzne</span><span class="sxs-lookup"><span data-stu-id="e5f8b-125">cryptography dependencies</span></span>
<span data-ttu-id="e5f8b-126">Należy zainstalować zależności hello hello [kryptografii] [ crypto] biblioteki wymagane przez hello `azure-batch` i `azure-storage` pakietów języka Python.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-126">You must install hello dependencies for hello [cryptography][crypto] library, required by hello `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="e5f8b-127">Wykonaj jedną z hello następujące operacje odpowiednie dla danej platformy, lub można znaleźć toohello [instalacji kryptografii] [ crypto_install] szczegóły, aby uzyskać więcej informacji:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-127">Perform one of hello following operations appropriate for your platform, or refer toohello [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="e5f8b-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e5f8b-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="e5f8b-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="e5f8b-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="e5f8b-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="e5f8b-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="e5f8b-131">Windows</span><span class="sxs-lookup"><span data-stu-id="e5f8b-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="e5f8b-132">Jeśli instalacja Python 3.3 + w systemie Linux, użyj odpowiedniki python3 hello hello Python zależności.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-132">If installing for Python 3.3+ on Linux, use hello python3 equivalents for hello Python dependencies.</span></span> <span data-ttu-id="e5f8b-133">Na przykład na platformie Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="e5f8b-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="e5f8b-134">Pakiety platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e5f8b-134">Azure packages</span></span>
<span data-ttu-id="e5f8b-135">Następnie zainstaluj hello **partii zadań Azure** i **usługi Azure Storage** pakietów języka Python.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-135">Next, install hello **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="e5f8b-136">Oba pakiety można zainstalować za pomocą **pip** i hello *requirements.txt* znaleźć tutaj:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-136">You can install both packages by using **pip** and hello *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="e5f8b-137">Następujące problem **pip** polecenia pakietów hello tooinstall wsadowego i magazynowania:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-137">Issue following **pip** command tooinstall hello Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="e5f8b-138">Można także zainstalować hello [partii zadań azure] [ pypi_batch] i [magazyn azure] [ pypi_storage] Python pakietów ręcznego:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-138">Or, you can install hello [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="e5f8b-139">Jeśli używasz konta nieuprzywilejowanego, może być konieczne tooprefix poleceń z `sudo`.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-139">If you are using an unprivileged account, you may need tooprefix your commands with `sudo`.</span></span> <span data-ttu-id="e5f8b-140">Na przykład `sudo pip install -r requirements.txt`.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="e5f8b-141">Więcej informacji na temat instalowania pakietów dla środowiska Python znajduje się w temacie [Instalowanie pakietów][pypi_install] w witrynie python.org.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="e5f8b-142">Przykład kodu z samouczka dotyczącego usługi Batch dla środowiska Python</span><span class="sxs-lookup"><span data-stu-id="e5f8b-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="e5f8b-143">Przykładowy kod samouczek Python partii Hello składa się z dwóch skryptów języka Python i kilka plików danych.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-143">hello Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="e5f8b-144">**python_tutorial_client.PY**: współdziała z hello partii i magazynu usług tooexecute równoległe obciążenie obliczeniowe węzłach (maszynach wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-144">**python_tutorial_client.py**: Interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="e5f8b-145">Witaj *python_tutorial_client.py* skrypt jest uruchamiany na na lokalnej stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-145">hello *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="e5f8b-146">**python_tutorial_task.PY**: hello skrypt uruchamiany na węzłach w pracy rzeczywistej hello Azure tooperform obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-146">**python_tutorial_task.py**: hello script that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="e5f8b-147">W przykładowym hello *python_tutorial_task.py* analizuje hello tekst w pliku, który został pobrany z usługi Azure Storage (plik wejściowy hello).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-147">In hello sample, *python_tutorial_task.py* parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="e5f8b-148">Następnie tworzy plik tekstowy (plik wyjściowy hello) zawierający listę hello trzy najważniejsze wyrazy, które pojawiają się w pliku wejściowym hello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-148">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="e5f8b-149">Po utworzeniu pliku wyjściowego hello *python_tutorial_task.py* przekazywania hello tooAzure pliku magazynu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-149">After it creates hello output file, *python_tutorial_task.py* uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="e5f8b-150">Udostępnia pobierania toohello skrypt po stronie klienta uruchomione na stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-150">This makes it available for download toohello client script running on your workstation.</span></span> <span data-ttu-id="e5f8b-151">Witaj *python_tutorial_task.py* skrypt będzie uruchamiany równolegle na wielu węzłach w hello usługa partia zadań obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-151">hello *python_tutorial_task.py* script runs in parallel on multiple compute nodes in hello Batch service.</span></span>
* <span data-ttu-id="e5f8b-152">**./Data/taskdata\*.txt**: te pliki tekstowe trzy Podaj dane wejściowe hello zadania hello, które będą uruchamiane na powitania węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-152">**./data/taskdata\*.txt**: These three text files provide hello input for hello tasks that run on hello compute nodes.</span></span>

<span data-ttu-id="e5f8b-153">powitania po diagram ilustruje hello głównej operacje, które są wykonywane przez skrypty powitania klienta i zadań.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-153">hello following diagram illustrates hello primary operations that are performed by hello client and task scripts.</span></span> <span data-ttu-id="e5f8b-154">Ten podstawowy przepływ pracy jest typowy dla wielu rozwiązań obliczeniowych utworzonych za pomocą usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="e5f8b-155">Gdy nie wykazują wszystkich funkcji dostępnych w hello usługa partia zadań, niemal każdego scenariusza partii zawiera części ten przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-155">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="e5f8b-156">![Przykładowy przepływ pracy w usłudze Batch][8]</span><span class="sxs-lookup"><span data-stu-id="e5f8b-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="e5f8b-157">**Krok 1.**</span><span class="sxs-lookup"><span data-stu-id="e5f8b-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="e5f8b-158">Utwórz **kontenery** w usłudze Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="e5f8b-159">
[**Krok 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="e5f8b-160">Przekaż toocontainers plików skryptów i dane wejściowe zadania.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-160">Upload task script and input files toocontainers.</span></span><br/><span data-ttu-id="e5f8b-161">
[**Krok 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="e5f8b-162">Utwórz **pulę** w usłudze Batch.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="e5f8b-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="e5f8b-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="e5f8b-164">Witaj puli **StartTask** pliki do pobrania hello toonodes skryptu (python_tutorial_task.py) zadań zgodnie z ich przyłączyć hello puli.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-164">hello pool **StartTask** downloads hello task script (python_tutorial_task.py) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="e5f8b-165">
[**Krok 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="e5f8b-166">Utwórz **zadanie** w usłudze Batch.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="e5f8b-167">
[**Krok 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="e5f8b-168">Dodaj **zadania** toohello zadania.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-168">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="e5f8b-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="e5f8b-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="e5f8b-170">zadania Hello są zaplanowane tooexecute na węzłach.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-170">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="e5f8b-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="e5f8b-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="e5f8b-172">Każde zadanie pobiera dane wejściowe z usługi Azure Storage, a następnie rozpoczyna się wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="e5f8b-173">
[**Krok 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="e5f8b-174">Monitoruj podzadania.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="e5f8b-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="e5f8b-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="e5f8b-176">Jak czynności zostały wykonane, ich przekazywanie ich tooAzure danych wyjściowych magazynu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-176">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="e5f8b-177">
[**Krok 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="e5f8b-178">Pobierz dane wyjściowe podzadań z usługi Storage.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-178">Download task output from Storage.</span></span>

<span data-ttu-id="e5f8b-179">Jak wspomniano wcześniej, nie wszystkie rozwiązania usługi Batch obejmują dokładnie te kroki i mogą obejmować wiele innych, natomiast w tym przykładzie przedstawiono typowe procesy w ramach rozwiązania usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="e5f8b-180">Przygotowanie skryptu klienta</span><span class="sxs-lookup"><span data-stu-id="e5f8b-180">Prepare client script</span></span>
<span data-ttu-id="e5f8b-181">Przed uruchomieniem hello próbki dodać poświadczeń konta wsadowego i magazynowania za*python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-181">Before you run hello sample, add your Batch and Storage account credentials too*python_tutorial_client.py*.</span></span> <span data-ttu-id="e5f8b-182">Jeśli jeszcze tego nie zrobiono, otwórz plik hello w Twoje ulubione hello edytora i zaktualizuj następujące wiersze przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-182">If you have not done so already, open hello file in your favorite editor and update hello following lines with your credentials.</span></span>

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

<span data-ttu-id="e5f8b-183">Poświadczenia konta wsadowego i magazynowania w bloku konta hello każdej usługi można znaleźć w hello [portalu Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-183">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="e5f8b-184">![Partii poświadczeń w portalu hello][9]
![magazynu poświadczeń w portalu hello][10]</span><span class="sxs-lookup"><span data-stu-id="e5f8b-184">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="e5f8b-185">W hello następujące sekcje, możemy analizowanie hello krokami przez hello skrypty tooprocess obciążenia w hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-185">In hello following sections, we analyze hello steps used by hello scripts tooprocess a workload in hello Batch service.</span></span> <span data-ttu-id="e5f8b-186">Firma Microsoft zachęca toorefer regularnie toohello skryptów w edytorze podczas przechodzić przez rest hello hello artykułu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-186">We encourage you toorefer regularly toohello scripts in your editor while you work your way through hello rest of hello article.</span></span>

<span data-ttu-id="e5f8b-187">Przejdź toohello po wierszu **python_tutorial_client.py** toostart z kroku 1:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-187">Navigate toohello following line in **python_tutorial_client.py** toostart with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="e5f8b-188">Krok 1: tworzenie kontenerów w usłudze Storage</span><span class="sxs-lookup"><span data-stu-id="e5f8b-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="e5f8b-189">![Tworzenie kontenerów w usłudze Azure Storage][1]
</span><span class="sxs-lookup"><span data-stu-id="e5f8b-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="e5f8b-190">Usługa Batch ma wbudowaną funkcję obsługi interakcji z usługą Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="e5f8b-191">Kontenery na koncie magazynu będzie udostępniać hello pliki wymagane przez hello zadania, które są uruchamiane na koncie usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-191">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="e5f8b-192">kontenery Hello udostępniają danych wyjściowych hello toostore miejsce, który tworzy hello zadania.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-192">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="e5f8b-193">Po pierwsze Hello hello *python_tutorial_client.py* skrypt wykonuje tworzą trzy kontenery w [magazyn obiektów Blob Azure](../storage/common/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="e5f8b-193">hello first thing hello *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="e5f8b-194">**Aplikacja**: ten kontener zapisze skrypt w języku Python hello uruchamiania zadań hello *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-194">**application**: This container will store hello Python script run by hello tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="e5f8b-195">**wejściowy**: zadań pobierze tooprocess pliki danych hello z hello *wejściowych* kontenera.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-195">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="e5f8b-196">**dane wyjściowe**: gdy zadania ukończyć przetwarzania pliku wejściowego, przekaże one hello wyniki toohello *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-196">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="e5f8b-197">W kolejności toointeract z magazynu kont i Utwórz kontenerów, używamy hello [magazyn azure] [ pypi_storage] pakietu toocreate [BlockBlobService] [ py_blockblobservice] obiekt — Witaj "client obiektu blob".</span><span class="sxs-lookup"><span data-stu-id="e5f8b-197">In order toointeract with a Storage account and create containers, we use hello [azure-storage][pypi_storage] package toocreate a [BlockBlobService][py_blockblobservice] object--hello "blob client."</span></span> <span data-ttu-id="e5f8b-198">Następnie utworzymy trzy kontenery hello konto magazynu przy użyciu powitania klienta obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-198">We then create three containers in hello Storage account using hello blob client.</span></span>

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

<span data-ttu-id="e5f8b-199">Po utworzeniu hello kontenery aplikacji hello teraz przekazać hello pliki, które będą używane przez zadania hello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="e5f8b-200">[Jak toouse magazynu obiektów Blob platformy Azure w języku Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) zawiera omówienie pracy z usługą Azure Storage kontenerów i obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-200">[How toouse Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="e5f8b-201">Po rozpoczęciu pracy z instancją powinno być hello górze listy odczytu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="e5f8b-202">Krok 2: przekazywanie skryptu podzadań i plików danych</span><span class="sxs-lookup"><span data-stu-id="e5f8b-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="e5f8b-203">![Zadanie przekazywania aplikacji i wejściowych (dane) pliki toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="e5f8b-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="e5f8b-204">W pliku hello Przekaż operacji *python_tutorial_client.py* najpierw definiuje kolekcji **aplikacji** i **wejściowych** pliku ścieżki istniejących na komputerze lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-204">In hello file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="e5f8b-205">Następnie przekazanie tych kontenerach toohello pliki, które zostały utworzone w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="e5f8b-206">Przy użyciu listy zrozumienia, hello `upload_file_to_container` funkcja jest wywoływana dla każdego pliku w kolekcjach hello i dwa [ResourceFile] [ py_resource_file] kolekcje są wypełnione.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-206">Using list comprehension, hello `upload_file_to_container` function is called for each file in hello collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="e5f8b-207">Witaj `upload_file_to_container` funkcja pojawia się poniżej:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-207">hello `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a><span data-ttu-id="e5f8b-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="e5f8b-208">ResourceFiles</span></span>
<span data-ttu-id="e5f8b-209">A [ResourceFile] [ py_resource_file] zawiera zadania w partii hello adresu URL tooa plik z magazynu Azure, który jest pobrany tooa węźle obliczeń przed uruchomieniem tego zadania.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-209">A [ResourceFile][py_resource_file] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="e5f8b-210">Witaj [ResourceFile][py_resource_file]. **blob_source** właściwość określa hello pełny adres URL pliku hello, ponieważ znajduje się ona w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-210">hello [ResourceFile][py_resource_file].**blob_source** property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="e5f8b-211">adres URL Hello mogą również obejmować sygnatury dostępu współdzielonego (SAS) zawiera plik toohello bezpiecznego dostępu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-211">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="e5f8b-212">Większość typów podzadań w ramach usługi Batch obejmuje właściwość *ResourceFiles*, m.in.:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="e5f8b-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="e5f8b-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="e5f8b-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="e5f8b-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="e5f8b-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="e5f8b-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="e5f8b-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="e5f8b-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="e5f8b-217">W tym przykładzie używają hello JobPreparationTask lub JobReleaseTask typy zadań, lecz więcej o nich w [węzły obliczeniowe uruchamianie działań przygotowania i kończenia zadania w partii zadań Azure](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-217">This sample does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="e5f8b-218">Sygnatura dostępu współdzielonego (SAS)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="e5f8b-219">Sygnatury dostępu współdzielonego są ciągów, które zapewniają toocontainers bezpiecznego dostępu i obiekty BLOB w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-219">Shared access signatures are strings that provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="e5f8b-220">Witaj *python_tutorial_client.py* skrypt używa zarówno obiektów blob i kontener sygnatury dostępu współdzielonego i pokazuje, jak tooobtain te udostępniane dostęp ciągi podpisu z hello usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-220">hello *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="e5f8b-221">**Obiekt blob sygnatur dostępu współdzielonego**: hello puli StartTask używa obiektu blob sygnatur dostępu współdzielonego po pobraniu hello zadania skryptu i dane wejściowe pliki danych z magazynu (zobacz [kroku nr 3](#step-3-create-batch-pool) poniżej).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-221">**Blob shared access signatures**: hello pool's StartTask uses blob shared access signatures when it downloads hello task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="e5f8b-222">Witaj `upload_file_to_container` działać w *python_tutorial_client.py* zawiera hello kod, który uzyskuje sygnatury dostępu współdzielonego każdy obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-222">hello `upload_file_to_container` function in *python_tutorial_client.py* contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="e5f8b-223">Robi to poprzez wywołanie [BlockBlobService.make_blob_url] [ py_make_blob_url] hello modułu magazynu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in hello Storage module.</span></span>
* <span data-ttu-id="e5f8b-224">**Sygnatury dostępu współdzielonego kontenera**: zgodnie z każdego zadania zakończy pracę w węźle obliczeń hello, zostanie przesłany jego dane wyjściowe pliku toohello *dane wyjściowe* kontenera w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-224">**Container shared access signature**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="e5f8b-225">toodo, *python_tutorial_task.py* używa kontenera sygnatury dostępu współdzielonego, która zapewnia dostęp do zapisu toohello kontenera.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-225">toodo so, *python_tutorial_task.py* uses a container shared access signature that provides write access toohello container.</span></span> <span data-ttu-id="e5f8b-226">Witaj `get_container_sas_token` działać w *python_tutorial_client.py* uzyskuje sygnatury dostępu współdzielonego hello kontenera, który następnie jest przekazywany jako zadania toohello argumentu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-226">hello `get_container_sas_token` function in *python_tutorial_client.py* obtains hello container's shared access signature, which is then passed as a command-line argument toohello tasks.</span></span> <span data-ttu-id="e5f8b-227">Krok #5 [Dodaj zadania tooa zadania](#step-5-add-tasks-to-job), w tym artykule omówiono użycie hello kontenera hello sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-227">Step #5, [Add tasks tooa job](#step-5-add-tasks-to-job), discusses hello usage of hello container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="e5f8b-228">Wyewidencjonowanie hello dwuczęściową serii na sygnatur dostępu współdzielonego [część 1: modelu sygnatur dostępu Współdzielonego hello opis](../storage/common/storage-dotnet-shared-access-signature-part-1.md) i [część 2: tworzenie i używanie sygnatury dostępu Współdzielonego z hello usługa Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn więcej informacji na temat bezpieczny dostęp toodata na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-228">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with hello Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="e5f8b-229">Krok 3: tworzenie puli usługi Batch</span><span class="sxs-lookup"><span data-stu-id="e5f8b-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="e5f8b-230">![Tworzenie puli usługi Batch][3]
</span><span class="sxs-lookup"><span data-stu-id="e5f8b-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="e5f8b-231">**Pula** usługi Batch jest kolekcją węzłów obliczeniowych (maszyn wirtualnych), w których usługa Batch wykonuje podzadania danego zadania.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="e5f8b-232">Po jego przekazuje hello zadania skryptu i danych plików toohello konta magazynu, *python_tutorial_client.py* jego interakcji z usługi partia zadań hello jest uruchamiany przy użyciu modułu Python partii hello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-232">After it uploads hello task script and data files toohello Storage account, *python_tutorial_client.py* starts its interaction with hello Batch service by using hello Batch Python module.</span></span> <span data-ttu-id="e5f8b-233">toodo, [BatchServiceClient] [ py_batchserviceclient] utworzeniu:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-233">toodo so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="e5f8b-234">Następnie puli węzłów obliczeniowych jest tworzony w hello konta usługi partia zadań przy użyciu wywołania zbyt`create_pool`.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-234">Next, a pool of compute nodes is created in hello Batch account with a call too`create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="e5f8b-235">Podczas tworzenia puli, należy zdefiniować [PoolAddParameter] [ py_pooladdparam] , który określa kilka właściwości puli hello:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for hello pool:</span></span>

* <span data-ttu-id="e5f8b-236">**Identyfikator** hello puli (*identyfikator* — jest to wymagane)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-236">**ID** of hello pool (*id* - required)</span></span><p/><span data-ttu-id="e5f8b-237">Podobnie jak w przypadku większości obiektów w usłudze Batch nowa pula musi mieć unikatowy identyfikator w ramach konta usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="e5f8b-238">Kod odwołuje się toothis puli za pomocą jego Identyfikatora, a jest to, jak rozpoznać puli hello w hello Azure [portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="e5f8b-238">Your code refers toothis pool using its ID, and it's how you identify hello pool in hello Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="e5f8b-239">**Liczba węzłów obliczeniowych** (element *target_dedicated* — wymagany)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="e5f8b-240">Ta właściwość określa, jak wiele maszyn wirtualnych powinny zostać wdrożone w puli hello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-240">This property specifies how many VMs should be deployed in hello pool.</span></span> <span data-ttu-id="e5f8b-241">Jest ważne toonote, że wszystkie konta usługi partia zadań mają domyślnie **przydziału** czy limity hello liczba **rdzeni** (i w związku z tym węzły obliczeniowe) w ramach konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-241">It is important toonote that all Batch accounts have a default **quota** that limits hello number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="e5f8b-242">Można znaleźć hello przydziałów domyślnych i instrukcje na temat zbyt[Zwiększ limit przydziału](batch-quota-limit.md#increase-a-quota) (na przykład hello maksymalna liczba rdzeni w ramach konta usługi partia zadań) w [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-242">You can find hello default quotas and instructions on how too[increase a quota](batch-quota-limit.md#increase-a-quota) (such as hello maximum number of cores in your Batch account) in [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="e5f8b-243">Jeśli zaczniesz zastanawiać się: „Dlaczego moja pula nie może przekroczyć X rdzeni?”,</span><span class="sxs-lookup"><span data-stu-id="e5f8b-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="e5f8b-244">Ten limit przydziału rdzeni może spowodować hello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-244">this core quota may be hello cause.</span></span>
* <span data-ttu-id="e5f8b-245">**System operacyjny** dla węzłów (element *virtual_machine_configuration* **lub** *cloud_service_configuration* — wymagany)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="e5f8b-246">W skrypcie *python_tutorial_client.py* zostanie utworzona pula węzłów systemu Linux przy użyciu polecenia [VirtualMachineConfiguration][py_vm_config].</span><span class="sxs-lookup"><span data-stu-id="e5f8b-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="e5f8b-247">Witaj `select_latest_verified_vm_image_with_node_agent_sku` działać w `common.helpers` upraszcza pracy z [Marketplace maszyny wirtualne Azure] [ vm_marketplace] obrazów.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-247">hello `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="e5f8b-248">Więcej informacji o używaniu obrazów z rynku znajduje się w artykule [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) (Inicjowanie obsługi węzłów obliczeniowych systemu Linux w pulach usługi Azure Batch).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="e5f8b-249">**Rozmiar węzłów obliczeniowych** (element *vm_size* — wymagany)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="e5f8b-250">Ponieważ należy określać węzły obliczeniowe systemu Linux dla parametru [VirtualMachineConfiguration][py_vm_config], określamy rozmiar maszyny wirtualnej (`STANDARD_A1` w tym przykładzie) na podstawie artykułu [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Rozmiary maszyn wirtualnych na platformie Azure).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e5f8b-251">Więcej informacji znajduje się w artykule [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) (Inicjowanie obsługi węzłów obliczeniowych systemu Linux w pulach usługi Azure Batch).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="e5f8b-252">**Podzadanie uruchamiania** (element *start_task* — niewymagany)</span><span class="sxs-lookup"><span data-stu-id="e5f8b-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="e5f8b-253">Wraz z hello powyżej właściwości węzła fizycznego, można również określić [StartTask] [ py_starttask] puli hello (nie jest wymagane).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-253">Along with hello above physical node properties, you may also specify a [StartTask][py_starttask] for hello pool (it is not required).</span></span> <span data-ttu-id="e5f8b-254">Hello StartTask wykonywane na każdym węźle, ponieważ ten węzeł dołącza hello puli i każdym uruchomieniu węzła.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-254">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="e5f8b-255">Hello StartTask jest szczególnie przydatna w przypadku przygotowywania węzły obliczeniowe hello wykonywania zadań, takich jak instalowanie aplikacji hello, które uruchamiane zadań.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-255">hello StartTask is especially useful for preparing compute nodes for hello execution of tasks, such as installing hello applications that your tasks run.</span></span><p/><span data-ttu-id="e5f8b-256">W tej przykładowej aplikacji hello StartTask kopiuje hello pliki, które pobiera z magazynu (które są określane przy użyciu hello StartTask **resource_files** właściwości) z hello StartTask *katalog roboczy* toohello *udostępnionego* katalogu, w którym wszystkie zadania uruchomione w węźle hello może uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-256">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello StartTask's **resource_files** property) from hello StartTask *working directory* toohello *shared* directory that all tasks running on hello node can access.</span></span> <span data-ttu-id="e5f8b-257">Zasadniczo spowoduje to skopiowanie `python_tutorial_task.py` toohello udostępniony katalog w każdym węźle jako węzeł hello dołącza hello puli, tak aby wszystkie zadania, które będą uruchamiane w węźle hello do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-257">Essentially, this copies `python_tutorial_task.py` toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

<span data-ttu-id="e5f8b-258">Można zauważyć hello wywołania toohello `wrap_commands_in_shell` funkcji pomocnika.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-258">You may notice hello call toohello `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="e5f8b-259">Funkcja ta z kolekcji oddzielnych poleceń tworzy jeden wiersz polecenia odpowiedni dla właściwości wiersza polecenia podzadania.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="e5f8b-260">Godny uwagi we fragmencie kodu hello powyżej jest również użycie Witaj dwie zmienne środowiskowe w hello **wiersz polecenia** właściwości hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` i `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-260">Also notable in hello code snippet above is hello use of two environment variables in hello **command_line** property of hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="e5f8b-261">Każdy węzeł obliczeniowy w puli partii jest automatycznie konfigurowany z kilku zmiennych środowiskowych, które są określone tooBatch.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="e5f8b-262">Żaden proces, która jest wykonywana przez zadanie ma zmienne środowiskowe toothese dostępu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-262">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="e5f8b-263">toofind więcej informacji na temat hello zmiennych środowiskowych, które są dostępne w węzłach obliczeń w puli partii, jak również informacje o katalogach roboczych zadań, zobacz **ustawienia środowiska dla zadań** i **plików i katalogów**  w hello [Przegląd funkcji partii zadań Azure](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-263">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in hello [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="e5f8b-264">Krok 4: tworzenie zadania w usłudze Batch</span><span class="sxs-lookup"><span data-stu-id="e5f8b-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="e5f8b-265">![Tworzenie zadania w usłudze Batch][4]</span><span class="sxs-lookup"><span data-stu-id="e5f8b-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="e5f8b-266">**Zadanie** usługi Batch jest kolekcją podzadań i jest skojarzone z pulą węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="e5f8b-267">wykonanie Hello zadań w ramach zadania w węzłach obliczeń puli hello skojarzone.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-267">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="e5f8b-268">Można użyć zadania nie tylko do organizowaniu i śledzenia zadań w powiązanych obciążeń pracą, ale dla narzucania niektórych ograniczeń — takie jak hello maksymalną czasu wykonywania zadania hello (i przez rozszerzenie, jego zadań podrzędnych) i priorytet zadania w zadaniach tooother relacji hello konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) and job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="e5f8b-269">W tym przykładzie jednak hello zadanie jest skojarzone tylko z pulą hello, który został utworzony w kroku #3.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-269">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="e5f8b-270">Żadne dodatkowe właściwości nie są konfigurowane.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-270">No additional properties are configured.</span></span>

<span data-ttu-id="e5f8b-271">Wszystkie zadania usługi Batch są skojarzone z określoną pulą.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="e5f8b-272">To skojarzenie wskazuje węzły, które hello zadania wykonania na.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-272">This association indicates which nodes hello job's tasks execute on.</span></span> <span data-ttu-id="e5f8b-273">Określ pulę hello przy użyciu hello [PoolInformation] [ py_poolinfo] właściwości, jak pokazano w hello poniższy fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-273">You specify hello pool by using hello [PoolInformation][py_poolinfo] property, as shown in hello code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="e5f8b-274">Teraz, kiedy zadania został utworzony, zadania są dodawane tooperform hello pracy.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-274">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="e5f8b-275">Krok 5: Dodawanie toojob zadań</span><span class="sxs-lookup"><span data-stu-id="e5f8b-275">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="e5f8b-276">![Dodaj toojob zadań][5]</span><span class="sxs-lookup"><span data-stu-id="e5f8b-276">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="e5f8b-277">
*(1) zadania są dodawane toohello zadania, zadania (2) hello są zaplanowane toorun w węzłach i (3) hello zadania Pobierz tooprocess pliki danych hello*</span><span class="sxs-lookup"><span data-stu-id="e5f8b-277">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="e5f8b-278">Wsadowe **zadania** są hello poszczególnych jednostek pracy wykonywanych na powitania węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-278">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="e5f8b-279">Zadanie ma wiersza polecenia i uruchamia hello skrypty lub pliki wykonywalne, w tym wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-279">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="e5f8b-280">tooactually wykonywania pracy, zadań, należy dodać tooa zadania.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-280">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="e5f8b-281">Każdy [CloudTask] [ py_task] jest skonfigurowana właściwość wiersza polecenia i [ResourceFiles] [ py_resource_file] (tak jak StartTask hello puli) tego hello zadanie pobiera węzła toohello przed jego wiersza polecenia jest wykonywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="e5f8b-282">W przykładowym hello każde zadanie przetwarza tylko jeden plik.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-282">In hello sample, each task processes only one file.</span></span> <span data-ttu-id="e5f8b-283">W związku z tym jego kolekcja ResourceFiles zawiera jeden element.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-283">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> <span data-ttu-id="e5f8b-284">Podczas uzyskiwania dostępu do zmiennych środowiskowych takich jak `$AZ_BATCH_NODE_SHARED_DIR` lub wykonywanie aplikacji nie można odnaleźć w węźle hello `PATH`, wiersze poleceń zadań należy wywołać hello skorupach jawnie, takich jak z `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in hello node's `PATH`, task command lines must invoke hello shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="e5f8b-285">To wymaganie nie jest konieczne, jeśli zadania wykonywania aplikacji w węźle hello `PATH` i nie odwołuje się do zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-285">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="e5f8b-286">W ramach hello `for` pętli we fragmencie kodu hello powyżej, zobaczysz, że hello wiersz polecenia dla zadania hello składa się z pięciu argumentów wiersza polecenia, które są przekazywane za*python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-286">Within hello `for` loop in hello code snippet above, you can see that hello command line for hello task is constructed with five command-line arguments that are passed too*python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="e5f8b-287">**FilePath**: to jest plik toohello ścieżka lokalna hello, ponieważ znajduje się w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-287">**filepath**: This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="e5f8b-288">Gdy hello obiektu ResourceFile w `upload_file_to_container` został utworzony w kroku 2 powyżej, nazwa pliku hello była używana dla tej właściwości (hello `file_path` parametru w Konstruktorze ResourceFile hello).</span><span class="sxs-lookup"><span data-stu-id="e5f8b-288">When hello ResourceFile object in `upload_file_to_container` was created in Step 2 above, hello file name was used for this property (hello `file_path` parameter in hello ResourceFile constructor).</span></span> <span data-ttu-id="e5f8b-289">Wskazuje, czy plik hello znajdują się w hello takie same katalogu w węźle hello jako *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-289">This indicates that hello file can be found in hello same directory on hello node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="e5f8b-290">**NUMWORDS**: hello górnej *N* wyrazy mają być zapisywane toohello pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-290">**numwords**: hello top *N* words should be written toohello output file.</span></span>
3. <span data-ttu-id="e5f8b-291">**Konto magazynu**: hello nazwę konta magazynu, który jest właścicielem danych wyjściowych zadania hello hello kontenera toowhich hello należy przekazać.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-291">**storageaccount**: hello name of hello Storage account that owns hello container toowhich hello task output should be uploaded.</span></span>
4. <span data-ttu-id="e5f8b-292">**storagecontainer**: Nazwa hello hello toowhich kontenera magazynu hello output można przekazywać pliki.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-292">**storagecontainer**: hello name of hello Storage container toowhich hello output files should be uploaded.</span></span>
5. <span data-ttu-id="e5f8b-293">**sastoken**: sygnatury dostępu współdzielonego hello (SAS), która zapewnia dostęp do zapisu toohello **dane wyjściowe** kontenera w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-293">**sastoken**: hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="e5f8b-294">Hello *python_tutorial_task.py* skrypt używa tego sygnatury dostępu współdzielonego po utworzeniu jego odwołania BlockBlobService.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-294">hello *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="e5f8b-295">Zapewnia dostęp do zapisu toohello kontenera bez konieczności klucz dostępu dla konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-295">This provides write access toohello container without requiring an access key for hello storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="e5f8b-296">Krok 6: monitorowanie podzadań</span><span class="sxs-lookup"><span data-stu-id="e5f8b-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="e5f8b-297">![Monitorowanie podzadań][6]</span><span class="sxs-lookup"><span data-stu-id="e5f8b-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="e5f8b-298">
*Witaj zadania hello monitorów (1) dla stanu ukończenia i (2) hello zadania przekazać wynik tooAzure danych magazynu*</span><span class="sxs-lookup"><span data-stu-id="e5f8b-298">
*hello script (1) monitors hello tasks for completion status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="e5f8b-299">Jeśli zadania zostaną dodane zadania tooa, są automatycznie w kolejce i zaplanowane do uruchomienia w węzłach obliczeń w puli hello skojarzone z zadaniem hello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-299">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="e5f8b-300">Na podstawie hello ustawień przez użytkownika, partii obsługuje wszystkich zadań usługi kolejkowania, planowania, ponawianie próby i obowiązków administracyjnych innych zadań za Ciebie.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-300">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="e5f8b-301">Istnieje wiele metod toomonitoring wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-301">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="e5f8b-302">Witaj `wait_for_tasks_to_complete` działać w *python_tutorial_client.py* udostępnia prosty przykład monitorowania zadań dla niektórych stanu, w tym przypadku hello [ukończone] [ py_taskstate] Stan.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-302">hello `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, hello [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="e5f8b-303">Krok 7: pobranie danych wyjściowych podzadań</span><span class="sxs-lookup"><span data-stu-id="e5f8b-303">Step 7: Download task output</span></span>
<span data-ttu-id="e5f8b-304">![Pobieranie danych wyjściowych zadań podrzędnych z usługi Storage][7]</span><span class="sxs-lookup"><span data-stu-id="e5f8b-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="e5f8b-305">Teraz, hello ukończenia zadania, dane wyjściowe zadania hello hello można pobrać z magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-305">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="e5f8b-306">Odbywa się przy użyciu wywołania zbyt`download_blobs_from_container` w *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-306">This is done with a call too`download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> <span data-ttu-id="e5f8b-307">Witaj wywołanie za`download_blobs_from_container` w *python_tutorial_client.py* Określa, czy pliki hello powinny być pobrany tooyour katalogu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-307">hello call too`download_blobs_from_container` in *python_tutorial_client.py* specifies that hello files should be downloaded tooyour home directory.</span></span> <span data-ttu-id="e5f8b-308">Możesz wolnego toomodify to lokalizacji wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-308">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="e5f8b-309">Krok 8: usuwanie kontenerów</span><span class="sxs-lookup"><span data-stu-id="e5f8b-309">Step 8: Delete containers</span></span>
<span data-ttu-id="e5f8b-310">Naliczane są opłaty za dane przechowywane w usłudze Azure Storage, dlatego jest zawsze tooremove dobrym rozwiązaniem, wszystkie obiekty BLOB, które są już potrzebne dla zadań wsadowych.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-310">Because you are charged for data that resides in Azure Storage, it is always a good idea tooremove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="e5f8b-311">W *python_tutorial_client.py*, odbywa się z trzech wywołań zbyt[BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-311">In *python_tutorial_client.py*, this is done with three calls too[BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="e5f8b-312">Krok 9: Usuwanie hello zadania i hello puli</span><span class="sxs-lookup"><span data-stu-id="e5f8b-312">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="e5f8b-313">W ostatnim kroku hello są zostanie wyświetlony monit o toodelete hello zadania i hello puli utworzone przez hello *python_tutorial_client.py* skryptu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-313">In hello final step, you are prompted toodelete hello job and hello pool that were created by hello *python_tutorial_client.py* script.</span></span> <span data-ttu-id="e5f8b-314">Mimo że nie są naliczane opłaty za same zadania i podzadania, *są* naliczane opłaty za węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="e5f8b-315">W związku z tym zaleca się przydzielanie węzłów tylko zależnie do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="e5f8b-316">Usuwanie nieużywanych pul może odbywać się podczas konserwacji.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="e5f8b-317">Witaj BatchServiceClient [JobOperations] [ py_job] i [PoolOperations] [ py_pool] mają odpowiednie metody usunięcia, które są wywołuje się, jeśli potwierdzenie usunięcia:</span><span class="sxs-lookup"><span data-stu-id="e5f8b-317">hello BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="e5f8b-318">Należy pamiętać, że opłaty są naliczane za zasoby obliczeniowe — usunięcie nieużywanych pul zminimalizuje koszty.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="e5f8b-319">Ponadto należy pamiętać, że usunięcie puli spowoduje usunięcie wszystkich węzłów obliczeniowych w tej puli, a wszystkie dane na powitania węzły będą nieodwracalny po usunięciu hello puli.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-sample-script"></a><span data-ttu-id="e5f8b-320">Uruchom skrypt przykładowy hello</span><span class="sxs-lookup"><span data-stu-id="e5f8b-320">Run hello sample script</span></span>
<span data-ttu-id="e5f8b-321">Po uruchomieniu hello *python_tutorial_client.py* skryptu z samouczka hello [przykładowy kod][github_article_samples], dane wyjściowe konsoli hello jest podobne toohello poniżej.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-321">When you run hello *python_tutorial_client.py* script from hello tutorial [code sample][github_article_samples], hello console output is similar toohello following.</span></span> <span data-ttu-id="e5f8b-322">Jest wstrzymany w `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` podczas puli hello węzły obliczeniowe są tworzone uruchomiona, a polecenia hello w puli hello rozpoczęcia zadania są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while hello pool's compute nodes are created, started, and hello commands in hello pool's start task are executed.</span></span> <span data-ttu-id="e5f8b-323">Użyj hello [portalu Azure] [ azure_portal] toomonitor puli, węzły obliczeniowe, zadań i zadań podczas i po zakończeniu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-323">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="e5f8b-324">Użyj hello [portalu Azure] [ azure_portal] lub hello [Eksploratora usługi Microsoft Azure Storage] [ storage_explorer] tooview hello zasobów magazynu (kontenerów i obiektów blob) które są tworzone przez aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-324">Use hello [Azure portal][azure_portal] or hello [Microsoft Azure Storage Explorer][storage_explorer] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

> [!TIP]
> <span data-ttu-id="e5f8b-325">Uruchom hello *python_tutorial_client.py* skrypt z wewnątrz hello `azure-batch-samples/Python/Batch/article_samples` katalogu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-325">Run hello *python_tutorial_client.py* script from within hello `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="e5f8b-326">Ścieżka względna używa hello `common.helpers` importowania modułu, więc można napotkać `ImportError: No module named 'common'` Jeżeli nie uruchomisz hello skrypt w tym katalogu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-326">It uses a relative path for hello `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run hello script from within this directory.</span></span>
>
>

<span data-ttu-id="e5f8b-327">Typowy czas wykonywania jest **około 5-7 minut** po uruchomieniu próbki hello w konfiguracji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-327">Typical execution time is **approximately 5-7 minutes** when you run hello sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="e5f8b-328">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5f8b-328">Next steps</span></span>
<span data-ttu-id="e5f8b-329">Uznać za zmiany wolnego toomake*python_tutorial_client.py* i *python_tutorial_task.py* tooexperiment innej obliczania scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-329">Feel free toomake changes too*python_tutorial_client.py* and *python_tutorial_task.py* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="e5f8b-330">Na przykład, spróbuj opóźnienie wykonywania zbyt*python_tutorial_task.py* toosimulate długotrwałych zadań i monitorować je na powitania portalu.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-330">For example, try adding an execution delay too*python_tutorial_task.py* toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="e5f8b-331">Spróbuj dodać więcej zadań lub dostosowanie hello liczba węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-331">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="e5f8b-332">Dodaj logikę toocheck dla i Zezwalaj na użycie hello istniejących czas wykonywania toospeed puli.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-332">Add logic toocheck for and allow hello use of an existing pool toospeed execution time.</span></span>

<span data-ttu-id="e5f8b-333">Teraz, kiedy znasz hello podstawowy przepływ pracy rozwiązania partii, jest toodig czasu w toohello dodatkowe funkcje hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-333">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="e5f8b-334">Przejrzyj hello [funkcji partii omówienie Azure](batch-api-basics.md) artykułu, w którym firma Microsoft zaleca, jeśli masz nową usługę toohello.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-334">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="e5f8b-335">Uruchomienie hello inne artykuły programowanie partii w obszarze **programowanie szczegółowe** w hello [ścieżka szkoleniowa dotycząca partii][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="e5f8b-335">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="e5f8b-336">Zapoznaj się z inną implementację przetwarzania obciążenie hello "pierwszych N wyrazy" z partii w hello [TopNWords] [ github_topnwords] próbki.</span><span class="sxs-lookup"><span data-stu-id="e5f8b-336">Check out a different implementation of processing hello "top N words" workload with Batch in hello [TopNWords][github_topnwords] sample.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Tworzenie kontenerów w usłudze Azure Storage"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Zadanie przekazywania aplikacji i wejściowych (dane) pliki toocontainers"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Tworzenie puli usługi Batch"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Tworzenie zadania w usłudze Batch"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Dodaj toojob zadań"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Monitorowanie podzadań"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Pobieranie danych wyjściowych podzadań z usługi Storage"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Przepływ pracy w rozwiązaniu usługi Batch (pełny diagram)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Poświadczenia usługi Batch w portalu"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Poświadczenia usługi Storage w portalu"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Przepływ pracy rozwiązania w usłudze Batch (diagram minimalny)"
