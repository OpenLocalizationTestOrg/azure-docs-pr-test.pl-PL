---
title: "przy użyciu fabryki danych i wsadowego zestawów danych na dużą skalę aaaProcess | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak potoku tooprocess dużych ilości danych w fabryce danych Azure przy użyciu możliwości przetwarzania równoległego partii zadań Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="c3521-103">Przetwarzanie dużych ilości danych za pomocą usług Data Factory i Batch</span><span class="sxs-lookup"><span data-stu-id="c3521-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="c3521-104">W tym artykule opisano architekturę rozwiązania próbki, które przenosi i przetwarzania dużych zestawów danych w sposób automatycznego i zaplanowane.</span><span class="sxs-lookup"><span data-stu-id="c3521-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="c3521-105">Umożliwia także wskazówki end-to-end tooimplement hello rozwiązania przy użyciu fabryki danych Azure i partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-105">It also provides an end-to-end walkthrough tooimplement hello solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="c3521-106">W tym artykule jest dłuższa niż artykułem typowe, ponieważ zawiera ona wskazówki przykładowe całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c3521-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="c3521-107">W przypadku nowych tooBatch i fabryki danych, informacje na temat tych usług i jak one współdziałają ze sobą.</span><span class="sxs-lookup"><span data-stu-id="c3521-107">If you are new tooBatch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="c3521-108">Jeśli znasz coś o usługach hello i są projektowanie/zaprojektowanie rozwiązania, może skupić się tylko na powitania [sekcji architektura](#architecture-of-sample-solution) hello artykułu i jeśli tworzysz prototypu lub rozwiązania, można również tootry out instrukcje krok po kroku w hello [wskazówki](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="c3521-108">If you know something about hello services and are designing/architecting a solution, you may focus just on hello [architecture section](#architecture-of-sample-solution) of hello article and if you are developing a prototype or a solution, you may also want tootry out step-by-step instructions in hello [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="c3521-109">Zapraszamy komentarze dotyczące tej zawartości i sposobie używania jej.</span><span class="sxs-lookup"><span data-stu-id="c3521-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="c3521-110">Po pierwsze Zobaczmy, jak może pomóc fabryki danych i instancji usługi przy użyciu przetwarzania dużych zestawów danych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in hello cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="c3521-111">Dlaczego usługa partia zadań Azure?</span><span class="sxs-lookup"><span data-stu-id="c3521-111">Why Azure Batch?</span></span>
<span data-ttu-id="c3521-112">Partia zadań Azure pozwala aplikacji na dużą skalę równoległych i wysokiej wydajności obliczeniowej (HPC) toorun wydajnie w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-112">Azure Batch enables you toorun large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="c3521-113">Jest usługą platformy, która planuje toorun pracy obliczeniowych w zarządzanej kolekcji maszyn wirtualnych, a można automatycznie skali obliczeniowe zasobów toomeet hello potrzeb zadań.</span><span class="sxs-lookup"><span data-stu-id="c3521-113">It's a platform service that schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="c3521-114">Za pomocą hello usługa partia zadań można definiować tooexecute zasobów obliczeniowych Azure aplikacji równolegle i na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="c3521-114">With hello Batch service, you define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="c3521-115">Mogą być uruchamiane na żądanie lub według harmonogramu zadań, a nie ma potrzeby toomanually tworzenie, konfigurowanie i zarządzanie klastra HPC, poszczególnych maszyn wirtualnych, sieci wirtualnych lub złożonych zadań i zadań planowania infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="c3521-115">You can run on-demand or scheduled jobs, and you don't need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="c3521-116">Zobacz następujące artykuły, jeśli nie masz doświadczenia z partii zadań Azure jako ułatwia zrozumienie architektury hello/implementacja opisanego w tym artykule rozwiązania hello hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-116">See hello following articles if you are not familiar with Azure Batch as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>   

* [<span data-ttu-id="c3521-117">Podstawowe informacje o partii zadań Azure</span><span class="sxs-lookup"><span data-stu-id="c3521-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="c3521-118">Przegląd funkcji partii</span><span class="sxs-lookup"><span data-stu-id="c3521-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="c3521-119">(opcjonalnie) toolearn więcej informacji na temat partii zadań Azure, zobacz hello [ścieżka szkoleniowa dotycząca partii zadań Azure](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="c3521-119">(optional) toolearn more about Azure Batch, see hello [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="c3521-120">Dlaczego fabryki danych Azure?</span><span class="sxs-lookup"><span data-stu-id="c3521-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="c3521-121">Fabryka danych jest usługa integracji danych opartych na chmurze, która organizuje i zautomatyzować przepływ hello i przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-121">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="c3521-122">Przy użyciu usługi fabryka danych hello, można utworzyć potoki zarządzanych danych, które przenoszenia danych z lokalnego i w chmurze, magazynu danych scentralizowane tooa magazynów danych (na przykład: magazyn obiektów Blob Azure), a procesu/Przekształcanie danych za pomocą usług, takich jak Azure HDInsight i Azure Uczenie maszynowe.</span><span class="sxs-lookup"><span data-stu-id="c3521-122">Using hello Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores tooa centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="c3521-123">Można również zaplanować toorun potoki danych w zaplanowanym czasie (co godzinę, codziennie, co tydzień, itp.) i monitorowanie i zarządzanie nimi na problemy tooidentify oka i podejmij akcję.</span><span class="sxs-lookup"><span data-stu-id="c3521-123">You can also schedule data pipelines toorun in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance tooidentify issues and take action.</span></span>

<span data-ttu-id="c3521-124">Zobacz następujące artykuły, jeśli nie masz doświadczenia z fabryką danych Azure jako ułatwia zrozumienie architektury hello/implementacja opisanego w tym artykule rozwiązania hello hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-124">See hello following articles if you are not familiar with Azure Data Factory as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>  

* [<span data-ttu-id="c3521-125">Wprowadzenie do fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="c3521-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="c3521-126">Tworzenie swój pierwszy potok danych</span><span class="sxs-lookup"><span data-stu-id="c3521-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="c3521-127">(opcjonalnie) toolearn więcej informacji na temat fabryki danych Azure, zobacz hello [ścieżka szkoleniowa dotycząca fabryki danych Azure](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="c3521-127">(optional) toolearn more about Azure Data Factory, see hello [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="c3521-128">Fabryki danych i partii razem</span><span class="sxs-lookup"><span data-stu-id="c3521-128">Data Factory and Batch together</span></span>
<span data-ttu-id="c3521-129">Fabryka danych zawiera wbudowane działania, takie jak działanie kopiowania toocopy/przeniesienia danych z źródła danych magazynu magazyn danych docelowy tooa i Hive działania tooprocess danych na platformie Azure przy użyciu klastrów platformy Hadoop (HDInsight).</span><span class="sxs-lookup"><span data-stu-id="c3521-129">Data Factory includes built-in activities such as Copy Activity toocopy/move data from a source data store tooa destination data store and Hive Activity tooprocess data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="c3521-130">Zobacz [działań przekształcania danych](data-factory-data-transformation-activities.md) listę obsługiwanych transformacji działania.</span><span class="sxs-lookup"><span data-stu-id="c3521-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="c3521-131">Również umożliwia możesz toocreate .NET działań niestandardowych danych toomove lub inny proces na własną logikę i Uruchom te działania na klaster Azure HDInsight lub w puli partii zadań Azure maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c3521-131">It also allows you toocreate custom .NET activities toomove or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="c3521-132">Korzystając z partii zadań Azure, można skonfigurować skali tooauto hello puli (Dodawanie lub usuwanie maszyn wirtualnych na podstawie obciążenia hello) na podstawie formuły, musisz podać.</span><span class="sxs-lookup"><span data-stu-id="c3521-132">When you use Azure Batch, you can configure hello pool tooauto-scale (add or remove VMs based on hello workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="c3521-133">Architektura przykładowe rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="c3521-133">Architecture of sample solution</span></span>
<span data-ttu-id="c3521-134">Mimo że architektura hello opisane w tym artykule jest prostym rozwiązaniem, jest odpowiednie toocomplex scenariuszy, takich jak modelowania branży usług finansowych, przetwarzania obrazów i renderowania i genomiczne analizy ryzyka.</span><span class="sxs-lookup"><span data-stu-id="c3521-134">Even though hello architecture described in this article is for a simple solution, it is relevant toocomplex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="c3521-135">Hello diagramie 1) jak fabryki danych organizuje przenoszenia danych i przetwarzania i 2) sposobu przetwarzania partii zadań Azure hello danych w sposób równoległy.</span><span class="sxs-lookup"><span data-stu-id="c3521-135">hello diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes hello data in a parallel manner.</span></span> <span data-ttu-id="c3521-136">Pobieranie i diagram hello wydruku dla ułatwienia (11 x 17 cali.</span><span class="sxs-lookup"><span data-stu-id="c3521-136">Download and print hello diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="c3521-137">lub rozmiaru A3): [aranżacji HPC i danych przy użyciu partii zadań Azure i fabryki danych](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="c3521-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="c3521-138">[![Diagram przetwarzania danych na dużą skalę](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="c3521-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="c3521-139">Witaj Poniższa lista zawiera podstawowe kroki hello hello procesu.</span><span class="sxs-lookup"><span data-stu-id="c3521-139">hello following list provides hello basic steps of hello process.</span></span> <span data-ttu-id="c3521-140">rozwiązanie Hello zawiera rozwiązania end-to-end hello toobuild kodu i wyjaśnienia.</span><span class="sxs-lookup"><span data-stu-id="c3521-140">hello solution includes code and explanations toobuild hello end-to-end solution.</span></span>

1. <span data-ttu-id="c3521-141">**Skonfiguruj partii zadań Azure z pulą węzłów obliczeniowych (VM)**.</span><span class="sxs-lookup"><span data-stu-id="c3521-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="c3521-142">Można określić hello liczba węzłów, a rozmiar każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="c3521-142">You can specify hello number of nodes and size of each node.</span></span>
2. <span data-ttu-id="c3521-143">**Tworzy wystąpienie fabryki danych Azure** skonfigurowanego jednostek, które reprezentują magazynu obiektów blob platformy Azure, usługa obliczeniowych partii zadań Azure danych wejścia/wyjścia i przepływu pracy/potoku z działaniami, które Przenieś i przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="c3521-144">**Tworzenie niestandardowego działania .NET w potoku fabryki danych hello**.</span><span class="sxs-lookup"><span data-stu-id="c3521-144">**Create a custom .NET activity in hello Data Factory pipeline**.</span></span> <span data-ttu-id="c3521-145">działanie Hello jest uruchamiany na powitania puli partii zadań Azure kodu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c3521-145">hello activity is your user code that runs on hello Azure Batch pool.</span></span>
4. <span data-ttu-id="c3521-146">**Przechowywania dużych ilości danych wejściowych jako obiekty BLOB w magazynie Azure**.</span><span class="sxs-lookup"><span data-stu-id="c3521-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="c3521-147">Danych jest podzielona na wycinków logiczne (zazwyczaj za czas).</span><span class="sxs-lookup"><span data-stu-id="c3521-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="c3521-148">**Fabryka danych kopiuje dane są przetwarzane równolegle** toohello lokalizacji dodatkowej.</span><span class="sxs-lookup"><span data-stu-id="c3521-148">**Data Factory copies data that is processed in parallel** toohello secondary location.</span></span>
6. <span data-ttu-id="c3521-149">**Fabryka danych uruchamia hello działań niestandardowych przy użyciu puli hello przydzielone przez partię**.</span><span class="sxs-lookup"><span data-stu-id="c3521-149">**Data Factory runs hello custom activity using hello pool allocated by Batch**.</span></span> <span data-ttu-id="c3521-150">Fabryka danych można uruchomić jednocześnie działań.</span><span class="sxs-lookup"><span data-stu-id="c3521-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="c3521-151">Każde działanie przetwarza wycinka danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="c3521-152">wyniki Hello są przechowywane w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-152">hello results are stored in Azure storage.</span></span>
7. <span data-ttu-id="c3521-153">**Fabryka danych przenosi hello wyniki końcowe tooa trzeci lokalizacji**, w celu dystrybucji za pośrednictwem aplikacji lub dla dalszego przetwarzania przez inne narzędzia.</span><span class="sxs-lookup"><span data-stu-id="c3521-153">**Data Factory moves hello final results tooa third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="c3521-154">Implementacja przykładowe rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="c3521-154">Implementation of sample solution</span></span>
<span data-ttu-id="c3521-155">Hello przykładowe rozwiązanie jest celowo proste i tooshow należy jak toouse fabryki danych i partii razem tooprocess zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-155">hello sample solution is intentionally simple and is tooshow you how toouse Data Factory and Batch together tooprocess datasets.</span></span> <span data-ttu-id="c3521-156">rozwiązanie powitania po prostu zlicza hello wystąpienia terminu wyszukiwania ("Microsoft") w organizacji w szeregów czasowych plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c3521-156">hello solution simply counts hello number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="c3521-157">Generuje on hello liczby toooutput plików.</span><span class="sxs-lookup"><span data-stu-id="c3521-157">It outputs hello count toooutput files.</span></span>

<span data-ttu-id="c3521-158">**Czas**: Jeśli znasz podstawowe informacje o Azure, fabryki danych i partii i zostały ukończone hello wymagania wstępne wymienione poniżej, firma Microsoft oszacować to rozwiązanie ma toocomplete 1 – 2 godz.</span><span class="sxs-lookup"><span data-stu-id="c3521-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed hello prerequisites listed below, we estimate this solution takes 1-2 hours toocomplete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c3521-159">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c3521-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="c3521-160">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c3521-160">Azure subscription</span></span>
<span data-ttu-id="c3521-161">Jeśli nie masz subskrypcji platformy Azure, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="c3521-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c3521-162">Zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3521-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="c3521-163">Konto magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="c3521-163">Azure storage account</span></span>
<span data-ttu-id="c3521-164">Używasz konta magazynu Azure do przechowywania danych hello w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="c3521-164">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="c3521-165">Jeśli nie masz konta magazynu platformy Azure, zobacz [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="c3521-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="c3521-166">Witaj przykładowe rozwiązanie korzysta z magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c3521-166">hello sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="c3521-167">Konto usługi partia zadań Azure</span><span class="sxs-lookup"><span data-stu-id="c3521-167">Azure Batch account</span></span>
<span data-ttu-id="c3521-168">Tworzenie konta usługi partia zadań Azure za pomocą hello [portalu Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="c3521-168">Create an Azure Batch account using hello [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="c3521-169">Zobacz [tworzenie i zarządzanie nimi konto partii zadań Azure](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c3521-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="c3521-170">Należy zwrócić uwagę hello partii zadań Azure konta nazwy i klucza konta.</span><span class="sxs-lookup"><span data-stu-id="c3521-170">Note hello Azure Batch account name and account key.</span></span> <span data-ttu-id="c3521-171">Można również użyć [AzureRmBatchAccount nowy](https://msdn.microsoft.com/library/mt603749.aspx) toocreate polecenia cmdlet konto partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate an Azure Batch account.</span></span> <span data-ttu-id="c3521-172">Zobacz [wprowadzenie do poleceń cmdlet programu PowerShell usługi partia zadań Azure](../batch/batch-powershell-cmdlets-get-started.md) szczegółowe instrukcje na temat używania tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c3521-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="c3521-173">Witaj przykładowe rozwiązanie używa danych tooprocess partii zadań Azure (pośrednio przez potok fabryki danych Azure) w sposób równoległy w puli węzłów obliczeniowych (zarządzanej kolekcji maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="c3521-173">hello sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) tooprocess data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="c3521-174">Azure puli partii maszyn wirtualnych (VM)</span><span class="sxs-lookup"><span data-stu-id="c3521-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="c3521-175">Utwórz **puli partii zadań Azure** z co najmniej 2 węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="c3521-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="c3521-176">W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **Przeglądaj** w hello menu po lewej stronie i kliknij przycisk **konta usługi partia zadań**.</span><span class="sxs-lookup"><span data-stu-id="c3521-176">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="c3521-177">Wybierz użytkownika hello tooopen konto partii zadań Azure **konta usługi partia zadań** bloku.</span><span class="sxs-lookup"><span data-stu-id="c3521-177">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
3. <span data-ttu-id="c3521-178">Kliknij przycisk **pule** kafelka.</span><span class="sxs-lookup"><span data-stu-id="c3521-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="c3521-179">W hello **pule** bloku, kliknij przycisk Dodaj na powitania narzędzi tooadd puli.</span><span class="sxs-lookup"><span data-stu-id="c3521-179">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
   1. <span data-ttu-id="c3521-180">Wpisz identyfikator puli hello (**identyfikator puli**).</span><span class="sxs-lookup"><span data-stu-id="c3521-180">Enter an ID for hello pool (**Pool ID**).</span></span> <span data-ttu-id="c3521-181">Uwaga hello **identyfikator puli hello**; potrzebne podczas tworzenia hello rozwiązania fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-181">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
   2. <span data-ttu-id="c3521-182">Określ **systemu Windows Server 2012 R2** hello ustawienia rodziny systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c3521-182">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
   3. <span data-ttu-id="c3521-183">Wybierz **warstwę cenową węzła**.</span><span class="sxs-lookup"><span data-stu-id="c3521-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="c3521-184">Wprowadź **2** jako wartość hello **docelowego w wersji dedykowanej** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="c3521-184">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="c3521-185">Wprowadź **2** jako wartość hello **maksymalna liczba zadań na węzeł** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="c3521-185">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="c3521-186">Kliknij przycisk **OK** toocreate hello puli.</span><span class="sxs-lookup"><span data-stu-id="c3521-186">Click **OK** toocreate hello pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="c3521-187">Eksplorator usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c3521-187">Azure Storage Explorer</span></span>
<span data-ttu-id="c3521-188">[Azure magazynu Explorer 6 (Narzędzia)](https://azurestorageexplorer.codeplex.com/) lub [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (z oprogramowania ClumsyLeaf).</span><span class="sxs-lookup"><span data-stu-id="c3521-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="c3521-189">Zapoznanie się i zmieniając hello danych w projektach usługi Azure Storage, w tym dzienniki hello aplikacji hostowanych w chmurze za pomocą tych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="c3521-189">You use these tools for inspecting and altering hello data in your Azure Storage projects including hello logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="c3521-190">Utworzyć kontener o nazwie **mojkontener** prywatny dostęp (Brak dostępu anonimowego)</span><span class="sxs-lookup"><span data-stu-id="c3521-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="c3521-191">Jeśli używasz **CloudXplorer**, tworzyć foldery i podfoldery z hello następujące struktury:</span><span class="sxs-lookup"><span data-stu-id="c3521-191">If you are using **CloudXplorer**, create folders and subfolders with hello following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="c3521-192">`Inputfolder`i `outputfolder` są folderów najwyższego poziomu w `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="c3521-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="c3521-193">Witaj `inputfolder` ma podfoldery z sygnaturami daty i godziny (RRRR-MM-DD-HH).</span><span class="sxs-lookup"><span data-stu-id="c3521-193">hello `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="c3521-194">Jeśli używasz **Eksploratora usługi Storage Azure**, w następnym kroku hello potrzebne pliki tooupload o nazwach: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c3521-194">If you are using **Azure Storage Explorer**, in hello next step, you need tooupload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="c3521-195">Ten krok automatycznie tworzy foldery hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-195">This step automatically creates hello folders.</span></span>
3. <span data-ttu-id="c3521-196">Utwórz plik tekstowy **plik.txt** na komputerze z zawartością, która ma hello — słowo kluczowe **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="c3521-196">Create a text file **file.txt** on your machine with content that has hello keyword **Microsoft**.</span></span> <span data-ttu-id="c3521-197">Na przykład: "test niestandardowe aktywności testów Microsoft działania niestandardowego Microsoft".</span><span class="sxs-lookup"><span data-stu-id="c3521-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="c3521-198">Przekaż toohello pliku hello następujące foldery wejściowego w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-198">Upload hello file toohello following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="c3521-199">Jeśli używasz **Eksploratora usługi Storage Azure**, Przekaż plik hello **plik.txt** za**mojkontener**.</span><span class="sxs-lookup"><span data-stu-id="c3521-199">If you are using **Azure Storage Explorer**, upload hello file **file.txt** too**mycontainer**.</span></span> <span data-ttu-id="c3521-200">Kliknij przycisk **kopiowania** na powitania narzędzi toocreate kopię hello obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c3521-200">Click **Copy** on hello toolbar toocreate a copy of hello blob.</span></span> <span data-ttu-id="c3521-201">W hello **kopiowania obiektu Blob** okno dialogowe, zmień hello **Nazwa docelowego obiektu blob** zbyt`inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="c3521-201">In hello **Copy Blob** dialog box, change hello **destination blob name** too`inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="c3521-202">Powtórz ten krok toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c3521-202">Repeat this step toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="c3521-203">Ta akcja powoduje automatyczne utworzenie hello folderów.</span><span class="sxs-lookup"><span data-stu-id="c3521-203">This action automatically creates hello folders.</span></span>
5. <span data-ttu-id="c3521-204">Tworzenie kontenera o nazwie: `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="c3521-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="c3521-205">Możesz przekazać hello działania niestandardowego zip pliku toothis kontenera.</span><span class="sxs-lookup"><span data-stu-id="c3521-205">You upload hello custom activity zip file toothis container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="c3521-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c3521-206">Visual Studio</span></span>
<span data-ttu-id="c3521-207">Zainstaluj program Microsoft Visual Studio 2012 lub nowszym toocreate hello niestandardowych partii działania toobe używane w hello rozwiązania fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-207">Install Microsoft Visual Studio 2012 or later toocreate hello custom Batch activity toobe used in hello Data Factory solution.</span></span>

### <a name="high-level-steps-toocreate-hello-solution"></a><span data-ttu-id="c3521-208">Ogólne kroki toocreate hello rozwiązania</span><span class="sxs-lookup"><span data-stu-id="c3521-208">High-level steps toocreate hello solution</span></span>
1. <span data-ttu-id="c3521-209">Utwórz niestandardowe działanie, które zawiera hello logikę przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-209">Create a custom activity that contains hello data processing logic.</span></span>
2. <span data-ttu-id="c3521-210">Tworzenie fabryki danych Azure, która używa niestandardowego działania hello:</span><span class="sxs-lookup"><span data-stu-id="c3521-210">Create an Azure data factory that uses hello custom activity:</span></span>

### <a name="create-hello-custom-activity"></a><span data-ttu-id="c3521-211">Tworzenie niestandardowego działania hello</span><span class="sxs-lookup"><span data-stu-id="c3521-211">Create hello custom activity</span></span>
<span data-ttu-id="c3521-212">Hello działania niestandardowego fabryki danych jest Puls hello tego rozwiązania próbki.</span><span class="sxs-lookup"><span data-stu-id="c3521-212">hello Data Factory custom activity is hello heart of this sample solution.</span></span> <span data-ttu-id="c3521-213">Witaj przykładowe rozwiązanie używa niestandardowego działania hello toorun partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-213">hello sample solution uses Azure Batch toorun hello custom activity.</span></span> <span data-ttu-id="c3521-214">Zobacz [skorzystać z działań niestandardowych w potoku fabryki danych Azure](data-factory-use-custom-activities.md) hello podstawowe informacje toodevelop niestandardowych działań i używania ich w fabryce danych Azure potoków.</span><span class="sxs-lookup"><span data-stu-id="c3521-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for hello basic information toodevelop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="c3521-215">toocreate działania niestandardowego .NET używanego w potoku fabryki danych Azure, należy toocreate **Biblioteka klas programu .NET** projektu z klasy, która implementuje który **IDotNetActivity** interfejsu.</span><span class="sxs-lookup"><span data-stu-id="c3521-215">toocreate a .NET custom activity that you can use in an Azure Data Factory pipeline, you need toocreate a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="c3521-216">Ten interfejs jest tylko jedna metoda: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="c3521-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="c3521-217">Oto hello podpis metody hello:</span><span class="sxs-lookup"><span data-stu-id="c3521-217">Here is hello signature of hello method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="c3521-218">Metoda Hello ma kilka kluczowych składników należy toounderstand.</span><span class="sxs-lookup"><span data-stu-id="c3521-218">hello method has a few key components that you need toounderstand.</span></span>

* <span data-ttu-id="c3521-219">Metoda Hello przyjmuje cztery parametry:</span><span class="sxs-lookup"><span data-stu-id="c3521-219">hello method takes four parameters:</span></span>

  1. <span data-ttu-id="c3521-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="c3521-220">**linkedServices**.</span></span> <span data-ttu-id="c3521-221">Wyliczalny lista połączonych usług połączonych źródeł danych wejścia/wyjścia (na przykład: magazyn obiektów Blob Azure) toohello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) toohello data factory.</span></span> <span data-ttu-id="c3521-222">W tym przykładzie istnieje tylko jeden połączonej usługi typu usługi Azure Storage używane dla danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c3521-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="c3521-223">**zestawy danych**.</span><span class="sxs-lookup"><span data-stu-id="c3521-223">**datasets**.</span></span> <span data-ttu-id="c3521-224">Jest to lista wyliczalny zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="c3521-225">Można użyć tego parametru tooget hello lokalizacji i schematów wynika z zestawów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c3521-225">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="c3521-226">**działanie**.</span><span class="sxs-lookup"><span data-stu-id="c3521-226">**activity**.</span></span> <span data-ttu-id="c3521-227">Tego parametru reprezentuje hello bieżącego obliczeniowe — w takim przypadku usługa partia zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-227">This parameter represents hello current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="c3521-228">**Rejestrator**.</span><span class="sxs-lookup"><span data-stu-id="c3521-228">**logger**.</span></span> <span data-ttu-id="c3521-229">Umożliwia rejestratora Hello komentarze debugowania tej powierzchni jako hello, poszukaj w dzienniku "Użytkownika" hello potoku.</span><span class="sxs-lookup"><span data-stu-id="c3521-229">hello logger lets you write debug comments that surface as hello “User” log for hello pipeline.</span></span>
* <span data-ttu-id="c3521-230">Witaj, metoda zwraca słownik, który może być działań niestandardowych toochain używane razem w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-230">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="c3521-231">Ta funkcja nie jest jeszcze zaimplementowana, więc Zwróć pusty słownik z metody hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-231">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>

#### <a name="procedure-create-hello-custom-activity"></a><span data-ttu-id="c3521-232">Procedura: Tworzenie niestandardowego działania hello</span><span class="sxs-lookup"><span data-stu-id="c3521-232">Procedure: Create hello custom activity</span></span>
1. <span data-ttu-id="c3521-233">Utwórz projekt Biblioteka klas programu .NET w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3521-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="c3521-234">Uruchom **programu Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="c3521-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="c3521-235">Kliknij przycisk **pliku**, punktu zbyt**nowy**i kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="c3521-235">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="c3521-236">Rozwiń węzeł **szablony**i wybierz **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="c3521-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="c3521-237">W tym przewodniku, należy użyć serwera C\#, ale można użyć dowolnego .NET języka toodevelop hello działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="c3521-237">In this walkthrough, you use C\#, but you can use any .NET language toodevelop hello custom activity.</span></span>
   4. <span data-ttu-id="c3521-238">Wybierz **biblioteki klas** z hello listy typów projektu na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="c3521-238">Select **Class Library** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="c3521-239">Wprowadź **MyDotNetActivity** dla hello **nazwa**.</span><span class="sxs-lookup"><span data-stu-id="c3521-239">Enter **MyDotNetActivity** for hello **Name**.</span></span>
   6. <span data-ttu-id="c3521-240">Wybierz **C:\\ADF** dla hello **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="c3521-240">Select **C:\\ADF** for hello **Location**.</span></span> <span data-ttu-id="c3521-241">Utwórz hello folder **ADF** Jeśli nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="c3521-241">Create hello folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="c3521-242">Kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="c3521-242">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="c3521-243">Kliknij przycisk **narzędzia**, punktu zbyt**Menedżera pakietów NuGet**i kliknij przycisk **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="c3521-243">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="c3521-244">W hello **Konsola Menedżera pakietów**, wykonaj następujące polecenie tooimport hello **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="c3521-244">In hello **Package Manager Console**, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="c3521-245">Importuj hello **usługi Azure Storage** pakietu NuGet w projekcie toohello.</span><span class="sxs-lookup"><span data-stu-id="c3521-245">Import hello **Azure Storage** NuGet package in toohello project.</span></span> <span data-ttu-id="c3521-246">Ten pakiet jest potrzebna, ponieważ używasz hello interfejsu API z magazynu obiektów Blob w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c3521-246">You need this package because you use hello Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="c3521-247">Dodaj następujące hello **przy użyciu** plik źródłowy toohello dyrektywy w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-247">Add hello following **using** directives toohello source file in hello project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="c3521-248">Zmień nazwę hello hello **przestrzeni nazw** za**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="c3521-248">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="c3521-249">Zmień nazwę hello klasy hello zbyt**MyDotNetActivity** i pochodną hello **IDotNetActivity** interfejsu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c3521-249">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="c3521-250">Witaj wdrożenie (Dodaj) **Execute** metody hello **IDotNetActivity** interfejsu toohello **MyDotNetActivity** hello klasy i skopiuj następujące metody toohello kodu przykładowej.</span><span class="sxs-lookup"><span data-stu-id="c3521-250">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span> <span data-ttu-id="c3521-251">Zobacz hello [wykonywanie metody](#execute-method) sekcji wyjaśnienie logiki hello używane w ramach tej metody.</span><span class="sxs-lookup"><span data-stu-id="c3521-251">See hello [Execute Method](#execute-method) section for explanation for hello logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="c3521-252">Dodaj następujące klasy toohello metody pomocnika hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-252">Add hello following helper methods toohello class.</span></span> <span data-ttu-id="c3521-253">Te metody są wywoływane przez hello **Execute** metody.</span><span class="sxs-lookup"><span data-stu-id="c3521-253">These methods are invoked by hello **Execute** method.</span></span> <span data-ttu-id="c3521-254">Przede wszystkim hello **Calculate** metody izoluje hello kodu, który iteruje po każdy obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="c3521-254">Most importantly, hello **Calculate** method isolates hello code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="c3521-255">Witaj **GetFolderPath** metoda zwraca folder toohello ścieżki hello hello tooand tego hello zestawu danych punktów **GetFileName** metoda zwraca nazwę hello hello obiekt blob/pliku, który hello wskazuje zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-255">hello **GetFolderPath** method returns hello path toohello folder that hello dataset points tooand hello **GetFileName** method returns hello name of hello blob/file that hello dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="c3521-256">Witaj **Calculate** metody oblicza hello liczbę wystąpień — słowo kluczowe **Microsoft** w hello plików wejściowych (obiekty BLOB w folderze hello).</span><span class="sxs-lookup"><span data-stu-id="c3521-256">hello **Calculate** method calculates hello number of instances of keyword **Microsoft** in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="c3521-257">Witaj terminu wyszukiwania ("Microsoft") jest ustalony w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-257">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>

1. <span data-ttu-id="c3521-258">Skompiluj projekt hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-258">Compile hello project.</span></span> <span data-ttu-id="c3521-259">Kliknij przycisk **kompilacji** hello menu i kliknij przycisk **Kompiluj rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="c3521-259">Click **Build** from hello menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="c3521-260">Uruchom **Eksploratora Windows**i przejdź zbyt**bin\\debugowania** lub **bin\\wersji** folder, w zależności od typu hello kompilacji.</span><span class="sxs-lookup"><span data-stu-id="c3521-260">Launch **Windows Explorer**, and navigate too**bin\\debug** or **bin\\release** folder depending on hello type of build.</span></span>
3. <span data-ttu-id="c3521-261">Utwórz plik zip **MyDotNetActivity.zip** zawierający wszystkie hello pliki binarne w hello  **\\bin\\debugowania** folderu.</span><span class="sxs-lookup"><span data-stu-id="c3521-261">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello **\\bin\\Debug** folder.</span></span> <span data-ttu-id="c3521-262">Możesz tooinclude hello MyDotNetActivity. **pdb** pliku, tak aby uzyskać dodatkowe szczegóły, takie jak numer wiersza w kodzie źródłowym hello, który spowodował problem hello, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="c3521-262">You may want tooinclude hello MyDotNetActivity.**pdb** file so that you get additional details such as line number in hello source code that caused hello issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="c3521-263">Przekaż **MyDotNetActivity.zip** jako kontener obiektów blob toohello obiektu blob: `customactivitycontainer` w hello Azure magazynu obiektów blob tego hello **StorageLinkedService** połączonej usługi w hello  **ADFTutorialDataFactory** używa.</span><span class="sxs-lookup"><span data-stu-id="c3521-263">Upload **MyDotNetActivity.zip** as a blob toohello blob container: `customactivitycontainer` in hello Azure blob storage that hello **StorageLinkedService** linked service in hello **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="c3521-264">Tworzenie kontenera obiektów blob hello `customactivitycontainer` Jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="c3521-264">Create hello blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="c3521-265">Execute — Metoda</span><span class="sxs-lookup"><span data-stu-id="c3521-265">Execute method</span></span>
<span data-ttu-id="c3521-266">Ta sekcja zawiera bardziej szczegółowe informacje i notatki dotyczące kodu hello w hello metody Execute.</span><span class="sxs-lookup"><span data-stu-id="c3521-266">This section provides more details and notes about hello code in hello Execute method.</span></span>

1. <span data-ttu-id="c3521-267">elementy członkowskie Hello iteracji w kolekcji wejściowych hello znajdują się w hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="c3521-267">hello members for iterating through hello input collection are found in hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="c3521-268">Iteracji w kolekcji obiektów blob hello wymaga użycia hello **BlobContinuationToken** klasy.</span><span class="sxs-lookup"><span data-stu-id="c3521-268">Iterating through hello blob collection requires using hello **BlobContinuationToken** class.</span></span> <span data-ttu-id="c3521-269">W zasadzie, należy użyć-pętli z tokenem hello jako mechanizm hello wyjścia hello pętli while.</span><span class="sxs-lookup"><span data-stu-id="c3521-269">In essence, you must use a do-while loop with hello token as hello mechanism for exiting hello loop.</span></span> <span data-ttu-id="c3521-270">Aby uzyskać więcej informacji, zobacz [jak toouse magazynu obiektów Blob z .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="c3521-270">For more information, see [How toouse Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="c3521-271">Podstawowe pętli jest następujący:</span><span class="sxs-lookup"><span data-stu-id="c3521-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="c3521-272">Zapoznaj się dokumentacją hello hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) metody, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c3521-272">See hello documentation for hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="c3521-273">Hello kodu pracuje nad hello zestawu obiektów blob logicznie znajdzie się w obrębie hello czy-pętli while.</span><span class="sxs-lookup"><span data-stu-id="c3521-273">hello code for working through hello set of blobs logically goes within hello do-while loop.</span></span> <span data-ttu-id="c3521-274">W hello **Execute** metoda, czy hello — gdy pętli przekazuje hello listę obiektów blob tooa metodę o nazwie **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="c3521-274">In hello **Execute** method, hello do-while loop passes hello list of blobs tooa method named **Calculate**.</span></span> <span data-ttu-id="c3521-275">Witaj, metoda zwraca ciąg zmiennej o nazwie **dane wyjściowe** czyli hello wyniku o iterowane za pośrednictwem wszystkich hello obiektów blob w segmencie hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-275">hello method returns a string variable named **output** that is hello result of having iterated through all hello blobs in hello segment.</span></span>

   <span data-ttu-id="c3521-276">Zwraca hello liczbę wystąpień hello wyszukiwany termin (**Microsoft**) w obiekcie blob hello przekazany toohello **Calculate** metody.</span><span class="sxs-lookup"><span data-stu-id="c3521-276">It returns hello number of occurrences of hello search term (**Microsoft**) in hello blob passed toohello **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="c3521-277">Raz hello **Calculate** metody przeprowadził hello pracy, jego musi być napisana tooa nowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="c3521-277">Once hello **Calculate** method has done hello work, it must be written tooa new blob.</span></span> <span data-ttu-id="c3521-278">Aby dla każdego zestawu obiektów blob przetwarzane z wynikami hello można pisać nowego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="c3521-278">So for every set of blobs processed, a new blob can be written with hello results.</span></span> <span data-ttu-id="c3521-279">Nowy obiekt blob toowrite tooa, pierwsze Znajdź hello wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-279">toowrite tooa new blob, first find hello output dataset.</span></span>

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="c3521-280">Kod Hello również wywołuje metodę pomocnika: **GetFolderPath** ścieżka folderu hello tooretrieve (nazwa kontenera magazynu hello).</span><span class="sxs-lookup"><span data-stu-id="c3521-280">hello code also calls a helper method: **GetFolderPath** tooretrieve hello folder path (hello storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="c3521-281">Witaj **GetFolderPath** tooan obiektu DataSet AzureBlobDataSet, który ma właściwość o nazwie FolderPath hello rzutowania.</span><span class="sxs-lookup"><span data-stu-id="c3521-281">hello **GetFolderPath** casts hello DataSet object tooan AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="c3521-282">Witaj Witaj wywołań kodu **GetFileName** metody tooretrieve hello nazwę pliku (obiektów blob).</span><span class="sxs-lookup"><span data-stu-id="c3521-282">hello code calls hello **GetFileName** method tooretrieve hello file name (blob name).</span></span> <span data-ttu-id="c3521-283">Kod Hello jest podobne toohello powyżej ścieżka folderu hello tooget kodu.</span><span class="sxs-lookup"><span data-stu-id="c3521-283">hello code is similar toohello above code tooget hello folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="c3521-284">Witaj nazwę pliku hello są zapisywane przez utworzenie obiekt URI.</span><span class="sxs-lookup"><span data-stu-id="c3521-284">hello name of hello file is written by creating a URI object.</span></span> <span data-ttu-id="c3521-285">Konstruktor URI Hello używa hello **BlobEndpoint** nazwa kontenera hello tooreturn właściwości.</span><span class="sxs-lookup"><span data-stu-id="c3521-285">hello URI constructor uses hello **BlobEndpoint** property tooreturn hello container name.</span></span> <span data-ttu-id="c3521-286">Witaj folderu ścieżka i nazwa pliku są dodawane tooconstruct hello dane wyjściowe identyfikator URI obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="c3521-286">hello folder path and file name are added tooconstruct hello output blob URI.</span></span>  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="c3521-287">Hello nazwę pliku hello został zapisany i teraz można zapisać ciągu wyjściowego hello ze hello **Calculate** nowego obiektu blob tooa metody:</span><span class="sxs-lookup"><span data-stu-id="c3521-287">hello name of hello file has been written and now you can write hello output string from hello **Calculate** method tooa new blob:</span></span>

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a><span data-ttu-id="c3521-288">Tworzenie fabryki danych hello</span><span class="sxs-lookup"><span data-stu-id="c3521-288">Create hello data factory</span></span>
<span data-ttu-id="c3521-289">W hello [tworzenia działań niestandardowych hello](#create-the-custom-activity) sekcji utworzone niestandardowe działania i hello przekazanego pliku zip z plików binarnych i hello PDB plików tooan kontenera obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-289">In hello [Create hello custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded hello zip file with binaries and hello PDB file tooan Azure blob container.</span></span> <span data-ttu-id="c3521-290">W tej sekcji utworzysz Azure **fabryki danych** z **potoku** używającą hello **działania niestandardowego**.</span><span class="sxs-lookup"><span data-stu-id="c3521-290">In this section, you create an Azure **data factory** with a **pipeline** that uses hello **custom activity**.</span></span>

<span data-ttu-id="c3521-291">Witaj zestawu danych wejściowych dla działań niestandardowych hello reprezentuje hello obiektów blob (pliki) w folderze wejściowych hello (`mycontainer\\inputfolder`) w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c3521-291">hello input dataset for hello custom activity represents hello blobs (files) in hello input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="c3521-292">Witaj wyjściowy zestaw danych dla działania hello reprezentuje obiekty BLOB danych wyjściowych hello w folderze wyjściowym hello (`mycontainer\\outputfolder`) w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c3521-292">hello output dataset for hello activity represents hello output blobs in hello output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="c3521-293">Upuść jeden lub więcej plików w folderach wejściowych hello:</span><span class="sxs-lookup"><span data-stu-id="c3521-293">Drop one or more files in hello input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="c3521-294">Na przykład usunąć jeden plik (plik.txt) z powitania po zawartości do poszczególnych folderów hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-294">For example, drop one file (file.txt) with hello following content into each of hello folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="c3521-295">Każdego folderu wejściowych odpowiada wycinek tooa w fabryce danych Azure, nawet wtedy, gdy hello znajduje się w nim pliki 2 lub większą.</span><span class="sxs-lookup"><span data-stu-id="c3521-295">Each input folder corresponds tooa slice in Azure Data Factory even if hello folder has 2 or more files.</span></span> <span data-ttu-id="c3521-296">Każdy wycinek jest przetwarzany przez potok hello, działania niestandardowego hello iterację wszystkich hello obiektów blob w folderze wejściowych powitania dla tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="c3521-296">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="c3521-297">Widać pięć pliki wyjściowe z hello sam zawartości.</span><span class="sxs-lookup"><span data-stu-id="c3521-297">You see five output files with hello same content.</span></span> <span data-ttu-id="c3521-298">Na przykład plik wyjściowy hello przetwarzanie hello plik w folderze hello 2015-11-16-00 ma hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="c3521-298">For example, hello output file from processing hello file in hello 2015-11-16-00 folder has hello following content:</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="c3521-299">Jeśli musisz porzucić wiele plików (plik.txt, Plik2.txt file3.txt) z hello folder wejściowy toohello tej samej zawartości, zobacz powitania po zawartości w pliku wyjściowym hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with hello same content toohello input folder, you see hello following content in hello output file.</span></span> <span data-ttu-id="c3521-300">Każdego folderu (2015-11-16-00 itp.) odpowiada wycinek tooa w tym przykładzie, mimo że hello znajduje się w nim wiele plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c3521-300">Each folder (2015-11-16-00, etc.) corresponds tooa slice in this sample even though hello folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="c3521-301">Plik wyjściowy Hello ma trzy wiersze teraz, po jednej dla każdego pliku wejściowego (blob) w folderze hello skojarzone z hello slice (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="c3521-301">hello output file has three lines now, one for each input file (blob) in hello folder associated with hello slice (2015-11-16-00).</span></span>

<span data-ttu-id="c3521-302">Zadanie jest tworzone dla każdej uruchamiania działania.</span><span class="sxs-lookup"><span data-stu-id="c3521-302">A task is created for each activity run.</span></span> <span data-ttu-id="c3521-303">W tym przykładzie istnieje tylko jedno działanie w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-303">In this sample, there is only one activity in hello pipeline.</span></span> <span data-ttu-id="c3521-304">Gdy wycinek jest przetwarzany przez potok hello, hello działania niestandardowego działa w partii zadań Azure tooprocess hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="c3521-304">When a slice is processed by hello pipeline, hello custom activity runs on Azure Batch tooprocess hello slice.</span></span> <span data-ttu-id="c3521-305">Ponieważ pięć wycinków (każdy wycinek może mieć wielu obiektów blob lub pliku), jest pięć zadań utworzona w partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="c3521-306">Po uruchomieniu zadania w partii, jest rzeczywiście hello działań niestandardowych z systemem.</span><span class="sxs-lookup"><span data-stu-id="c3521-306">When a task runs on Batch, it is actually hello custom activity that is running.</span></span>

<span data-ttu-id="c3521-307">Witaj następujące wskazówki zawiera dodatkowe szczegóły.</span><span class="sxs-lookup"><span data-stu-id="c3521-307">hello following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="c3521-308">Krok 1: Tworzenie fabryki danych hello</span><span class="sxs-lookup"><span data-stu-id="c3521-308">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="c3521-309">Po zalogowaniu toohello [portalu Azure](https://portal.azure.com/), hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c3521-309">After logging in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>

   1. <span data-ttu-id="c3521-310">Kliknij przycisk **nowy** w menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="c3521-310">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="c3521-311">Kliknij przycisk **dane i analiza** w hello **nowy** bloku.</span><span class="sxs-lookup"><span data-stu-id="c3521-311">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="c3521-312">Kliknij przycisk **fabryki danych** na powitania **analizy danych** bloku.</span><span class="sxs-lookup"><span data-stu-id="c3521-312">Click **Data Factory** on hello **Data analytics** blade.</span></span>
2. <span data-ttu-id="c3521-313">W hello **nowa fabryka danych** bloku, wprowadź **CustomActivityFactory** dla hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="c3521-313">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="c3521-314">Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="c3521-314">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="c3521-315">Jeśli wystąpi błąd hello: **nazwa fabryki danych "CustomActivityFactory" nie jest dostępna**, Zmień nazwę hello hello fabryki danych (na przykład **yournameCustomActivityFactory**) i spróbuj utworzyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="c3521-315">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="c3521-316">Kliknij przycisk **Nazwa grupy zasobów**i wybierz istniejącą grupę zasobów lub Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="c3521-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="c3521-317">Sprawdź, czy używasz hello poprawne subskrypcji i regionu, w którym ma toobe fabryki danych hello utworzone.</span><span class="sxs-lookup"><span data-stu-id="c3521-317">Verify that you are using hello correct subscription and region where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="c3521-318">Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** bloku.</span><span class="sxs-lookup"><span data-stu-id="c3521-318">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="c3521-319">Zobacz hello fabryki danych tworzona w hello **pulpitu nawigacyjnego** z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-319">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="c3521-320">Po hello fabryki danych został utworzony pomyślnie, zobacz strony fabryki danych hello, który umożliwia hello zawartość hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-320">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="c3521-321">Krok 2: Tworzenie usługi połączonej</span><span class="sxs-lookup"><span data-stu-id="c3521-321">Step 2: Create linked services</span></span>
<span data-ttu-id="c3521-322">Połączone usługi łączenie magazyny danych lub obliczeniowe fabryki danych Azure tooan usług.</span><span class="sxs-lookup"><span data-stu-id="c3521-322">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="c3521-323">W tym kroku zostanie połączony z **usługi Azure Storage** konta i **partii zadań Azure** tooyour konta usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-323">In this step, you link your **Azure Storage** account and **Azure Batch** account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="c3521-324">Tworzenie połączonej usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c3521-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="c3521-325">Kliknij hello **tworzenie i wdrażanie** Kafelek na powitania **FABRYKI danych** bloku **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="c3521-325">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="c3521-326">Zostanie wyświetlony hello Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-326">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="c3521-327">Kliknij przycisk **nowy magazyn danych** hello pasek poleceń i wybierz **magazynu Azure.**</span><span class="sxs-lookup"><span data-stu-id="c3521-327">Click **New data store** on hello command bar and choose **Azure storage.**</span></span> <span data-ttu-id="c3521-328">Powinny pojawić się hello skryptu JSON do tworzenia usługi Azure Storage połączonej usługi w edytorze hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-328">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="c3521-329">Zastąp **nazwa konta** hello nazwą konta magazynu Azure i **klucz konta** z klucz dostępu hello hello kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-329">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="c3521-330">toolearn jak tooget Twojego magazynu uzyskują dostęp do klucza, zobacz [widoku, kopiowania i regenerate magazynu klucze dostępu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="c3521-330">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="c3521-331">Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-331">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="c3521-332">Tworzenie usługi partia zadań Azure połączone</span><span class="sxs-lookup"><span data-stu-id="c3521-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="c3521-333">W tym kroku możesz utworzyć połączonej usługi dla Twojego **partii zadań Azure** konta, które jest używane toorun hello fabryki danych niestandardowego działania.</span><span class="sxs-lookup"><span data-stu-id="c3521-333">In this step, you create a linked service for your **Azure Batch** account that is used toorun hello Data Factory custom activity.</span></span>

1. <span data-ttu-id="c3521-334">Kliknij przycisk **nowych obliczeń** hello pasek poleceń i wybierz **partii zadań Azure.**</span><span class="sxs-lookup"><span data-stu-id="c3521-334">Click **New compute** on hello command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="c3521-335">Powinny pojawić się hello skryptu JSON do tworzenia partii zadań Azure połączonej usługi w edytorze hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-335">You should see hello JSON script for creating an Azure Batch linked service in hello editor.</span></span>
2. <span data-ttu-id="c3521-336">W hello skryptu JSON:</span><span class="sxs-lookup"><span data-stu-id="c3521-336">In hello JSON script:</span></span>

   1. <span data-ttu-id="c3521-337">Zastąp **nazwa konta** o nazwie hello konta partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-337">Replace **account name** with hello name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="c3521-338">Zastąp **klucz dostępu** z klucz dostępu hello hello konto partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-338">Replace **access key** with hello access key of hello Azure Batch account.</span></span>
   3. <span data-ttu-id="c3521-339">Wprowadź identyfikator hello puli hello hello **poolName** właściwości**.**</span><span class="sxs-lookup"><span data-stu-id="c3521-339">Enter hello ID of hello pool for hello **poolName** property**.**</span></span> <span data-ttu-id="c3521-340">Dla tej właściwości można określić albo nazwę puli lub puli identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="c3521-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="c3521-341">Wprowadź hello partii identyfikatora URI dla hello **batchUri** właściwości JSON.</span><span class="sxs-lookup"><span data-stu-id="c3521-341">Enter hello batch URI for hello **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="c3521-342">Witaj **adres URL** z hello **bloku konta usługi partia zadań Azure** jest zgodny z formatem hello: \<accountname\>.\< region\>. batch.azure.com. Dla hello **batchUri** właściwości w hello JSON, należy za**Usuń "accountname."**</span><span class="sxs-lookup"><span data-stu-id="c3521-342">hello **URL** from hello **Azure Batch account blade** is in hello following format: \<accountname\>.\<region\>.batch.azure.com. For hello **batchUri** property in hello JSON, you need too**remove "accountname."**</span></span> <span data-ttu-id="c3521-343">z hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c3521-343">from hello URL.</span></span> <span data-ttu-id="c3521-344">Przykład: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="c3521-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="c3521-345">Dla hello **poolName** właściwości, można również określić identyfikator hello hello puli zamiast nazwy hello hello puli.</span><span class="sxs-lookup"><span data-stu-id="c3521-345">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c3521-346">Hello usługi fabryka danych nie obsługuje opcji na żądanie dla partii zadań Azure, w przeciwieństwie do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c3521-346">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="c3521-347">Pulę partii zadań Azure można używać tylko w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="c3521-348">Określ **StorageLinkedService** dla hello **linkedServiceName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="c3521-348">Specify **StorageLinkedService** for hello **linkedServiceName** property.</span></span> <span data-ttu-id="c3521-349">Tej połączonej usługi utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-349">You created this linked service in hello previous step.</span></span> <span data-ttu-id="c3521-350">Ten magazyn jest używany jako obszaru przemieszczania dla plików i dzienników.</span><span class="sxs-lookup"><span data-stu-id="c3521-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="c3521-351">Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-351">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="c3521-352">Krok 3: Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="c3521-352">Step 3: Create datasets</span></span>
<span data-ttu-id="c3521-353">W tym kroku możesz utworzyć zestawy danych toorepresent w danych wejściowych i dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c3521-353">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="c3521-354">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="c3521-354">Create input dataset</span></span>
1. <span data-ttu-id="c3521-355">W hello **edytor** dla hello fabryki danych, kliknij przycisk **nowy zestaw danych** przycisk na powitania narzędzi i kliknij przycisk **magazynu obiektów Blob Azure** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-355">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="c3521-356">Zastąp hello JSON w okienku po prawej stronie powitania powitania po fragment kodu JSON:</span><span class="sxs-lookup"><span data-stu-id="c3521-356">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    <span data-ttu-id="c3521-357">Utworzyć potok w dalszej części tego przewodnika, czas rozpoczęcia: 2015-11-16T00:00:00Z i na końcu czasu: 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="c3521-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="c3521-358">Są to dane zaplanowane tooproduce **co godzinę**, więc istnieje 5 wycinków wejścia/wyjścia (między **00**: 00:00 -\> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="c3521-358">It is scheduled tooproduce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="c3521-359">Witaj **częstotliwość** i **interwał** dla zestawu danych wejściowych hello jest ustawiony za**godzina** i **1**, co oznacza, że hello danych wejściowych jest dostępny co godzinę.</span><span class="sxs-lookup"><span data-stu-id="c3521-359">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span>

    <span data-ttu-id="c3521-360">Poniżej przedstawiono hello godzin rozpoczęcia każdy wycinek, które jest reprezentowana przez **SliceStart** zmiennej systemowej w hello powyżej fragment kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="c3521-360">Here are hello start times for each slice, which is represented by **SliceStart** system variable in hello above JSON snippet.</span></span>

    | <span data-ttu-id="c3521-361">**Wycinek**</span><span class="sxs-lookup"><span data-stu-id="c3521-361">**Slice**</span></span> | <span data-ttu-id="c3521-362">**Godzina rozpoczęcia**</span><span class="sxs-lookup"><span data-stu-id="c3521-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="c3521-363">1</span><span class="sxs-lookup"><span data-stu-id="c3521-363">1</span></span>         | <span data-ttu-id="c3521-364">2015-11-16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="c3521-365">2</span><span class="sxs-lookup"><span data-stu-id="c3521-365">2</span></span>         | <span data-ttu-id="c3521-366">2015-11-16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="c3521-367">3</span><span class="sxs-lookup"><span data-stu-id="c3521-367">3</span></span>         | <span data-ttu-id="c3521-368">2015-11-16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="c3521-369">4</span><span class="sxs-lookup"><span data-stu-id="c3521-369">4</span></span>         | <span data-ttu-id="c3521-370">2015-11-16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="c3521-371">5</span><span class="sxs-lookup"><span data-stu-id="c3521-371">5</span></span>         | <span data-ttu-id="c3521-372">2015-11-16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="c3521-373">Witaj **folderPath** jest obliczana przy użyciu hello rok, miesiąc, dzień i godzinę część czas rozpoczęcia wycinek hello (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="c3521-373">hello **folderPath** is calculated by using hello year, month, day, and hour part of hello slice start time (**SliceStart**).</span></span> <span data-ttu-id="c3521-374">W związku z tym Oto jak folder wejściowy jest mapowane tooa wycinka.</span><span class="sxs-lookup"><span data-stu-id="c3521-374">Therefore, here is how an input folder is mapped tooa slice.</span></span>

    | <span data-ttu-id="c3521-375">**Wycinek**</span><span class="sxs-lookup"><span data-stu-id="c3521-375">**Slice**</span></span> | <span data-ttu-id="c3521-376">**Godzina rozpoczęcia**</span><span class="sxs-lookup"><span data-stu-id="c3521-376">**Start time**</span></span>          | <span data-ttu-id="c3521-377">**Folder wejściowy**</span><span class="sxs-lookup"><span data-stu-id="c3521-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="c3521-378">1</span><span class="sxs-lookup"><span data-stu-id="c3521-378">1</span></span>         | <span data-ttu-id="c3521-379">2015-11-16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="c3521-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="c3521-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="c3521-381">2</span><span class="sxs-lookup"><span data-stu-id="c3521-381">2</span></span>         | <span data-ttu-id="c3521-382">2015-11-16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="c3521-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="c3521-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="c3521-384">3</span><span class="sxs-lookup"><span data-stu-id="c3521-384">3</span></span>         | <span data-ttu-id="c3521-385">2015-11-16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="c3521-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="c3521-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="c3521-387">4</span><span class="sxs-lookup"><span data-stu-id="c3521-387">4</span></span>         | <span data-ttu-id="c3521-388">2015-11-16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="c3521-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="c3521-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="c3521-390">5</span><span class="sxs-lookup"><span data-stu-id="c3521-390">5</span></span>         | <span data-ttu-id="c3521-391">2015-11-16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="c3521-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="c3521-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="c3521-393">Kliknij przycisk **Wdróż** hello toocreate narzędzi i wdrożyć hello **InputDataset** tabeli.</span><span class="sxs-lookup"><span data-stu-id="c3521-393">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="c3521-394">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="c3521-394">Create output dataset</span></span>
<span data-ttu-id="c3521-395">W tym kroku utworzysz innego elementu dataset typu AzureBlob toorepresent hello wyjście danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-395">In this step, you create another dataset of type AzureBlob toorepresent hello output data.</span></span>

1. <span data-ttu-id="c3521-396">W hello **edytor** dla hello fabryki danych, kliknij przycisk **nowy zestaw danych** przycisk na powitania narzędzi i kliknij przycisk **magazynu obiektów Blob Azure** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-396">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="c3521-397">Zastąp hello JSON w okienku po prawej stronie powitania powitania po fragment kodu JSON:</span><span class="sxs-lookup"><span data-stu-id="c3521-397">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    <span data-ttu-id="c3521-398">Obiekt blob/plik wyjściowy jest generowany dla każdego wejściowego wycinka.</span><span class="sxs-lookup"><span data-stu-id="c3521-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="c3521-399">Oto, jak dla każdego wycinka nosi nazwę pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="c3521-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="c3521-400">Wszystkie pliki wyjściowe hello są generowane w jednym folderze wyjściowym: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="c3521-400">All hello output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="c3521-401">**Wycinek**</span><span class="sxs-lookup"><span data-stu-id="c3521-401">**Slice**</span></span> | <span data-ttu-id="c3521-402">**Godzina rozpoczęcia**</span><span class="sxs-lookup"><span data-stu-id="c3521-402">**Start time**</span></span>          | <span data-ttu-id="c3521-403">**Plik wyjściowy**</span><span class="sxs-lookup"><span data-stu-id="c3521-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="c3521-404">1</span><span class="sxs-lookup"><span data-stu-id="c3521-404">1</span></span>         | <span data-ttu-id="c3521-405">2015-11-16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="c3521-406">2015-11-16 -**00. txt**</span><span class="sxs-lookup"><span data-stu-id="c3521-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="c3521-407">2</span><span class="sxs-lookup"><span data-stu-id="c3521-407">2</span></span>         | <span data-ttu-id="c3521-408">2015-11-16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="c3521-409">2015-11-16 -**01. txt**</span><span class="sxs-lookup"><span data-stu-id="c3521-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="c3521-410">3</span><span class="sxs-lookup"><span data-stu-id="c3521-410">3</span></span>         | <span data-ttu-id="c3521-411">2015-11-16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="c3521-412">2015-11-16 -**02. txt**</span><span class="sxs-lookup"><span data-stu-id="c3521-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="c3521-413">4</span><span class="sxs-lookup"><span data-stu-id="c3521-413">4</span></span>         | <span data-ttu-id="c3521-414">2015-11-16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="c3521-415">2015-11-16 -**03. txt**</span><span class="sxs-lookup"><span data-stu-id="c3521-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="c3521-416">5</span><span class="sxs-lookup"><span data-stu-id="c3521-416">5</span></span>         | <span data-ttu-id="c3521-417">2015-11-16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="c3521-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="c3521-418">2015-11-16 -**04. txt**</span><span class="sxs-lookup"><span data-stu-id="c3521-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="c3521-419">Należy pamiętać, że hello wszystkie pliki w folderze wejściowych (na przykład: 2015-11-16-00) są częścią wycinek hello czas rozpoczęcia: 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="c3521-419">Remember that all hello files in an input folder (for example: 2015-11-16-00) are part of a slice with hello start time: 2015-11-16-00.</span></span> <span data-ttu-id="c3521-420">Podczas przetwarzania tego wycinka działania niestandardowego hello skanowania za pomocą każdego pliku i tworzy wiersz w pliku wyjściowym hello hello liczby wystąpień terminu wyszukiwania ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="c3521-420">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="c3521-421">Jeśli istnieją trzy pliki w folderze hello 2015-11-16-00, istnieją trzy wiersze w pliku wyjściowym hello: 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="c3521-421">If there are three files in hello folder 2015-11-16-00, there are three lines in hello output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="c3521-422">Kliknij przycisk **Wdróż** hello toocreate narzędzi i wdrożyć hello **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c3521-422">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a><span data-ttu-id="c3521-423">Krok 4: Tworzenie i uruchamianie potoku hello z działań niestandardowych</span><span class="sxs-lookup"><span data-stu-id="c3521-423">Step 4: Create and run hello pipeline with custom activity</span></span>
<span data-ttu-id="c3521-424">W tym kroku możesz utworzyć potok z jednego działania, hello działania niestandardowego utworzonego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c3521-424">In this step, you create a pipeline with one activity, hello custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3521-425">Jeśli nie zostały jeszcze przekazane hello **plik.txt** tooinput folderów w kontenerze obiektów blob hello zrobić przed utworzeniem hello potoku.</span><span class="sxs-lookup"><span data-stu-id="c3521-425">If you haven't uploaded hello **file.txt** tooinput folders in hello blob container, do so before creating hello pipeline.</span></span> <span data-ttu-id="c3521-426">Witaj **isPaused** właściwość jest ustawiona toofalse w potoku hello JSON, więc potoku hello uruchamia natychmiast jako hello **start** przypada w przeszłości hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-426">hello **isPaused** property is set toofalse in hello pipeline JSON, so hello pipeline runs immediately as hello **start** date is in hello past.</span></span>
>
>

1. <span data-ttu-id="c3521-427">W hello Edytor fabryki danych, kliknij przycisk **nowy potok** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="c3521-427">In hello Data Factory Editor, click **New pipeline** on hello command bar.</span></span> <span data-ttu-id="c3521-428">Jeśli polecenie hello nie jest widoczne, kliknij **... (Wielokropek)**  toosee go.</span><span class="sxs-lookup"><span data-stu-id="c3521-428">If you do not see hello command, click **... (Ellipsis)** toosee it.</span></span>
2. <span data-ttu-id="c3521-429">Zastąp hello JSON w okienku po prawej stronie powitania hello następującego skryptu JSON:</span><span class="sxs-lookup"><span data-stu-id="c3521-429">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="c3521-430">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="c3521-430">Note hello following points:</span></span>

   * <span data-ttu-id="c3521-431">Istnieje tylko jedno działanie w potoku hello i jest typu: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="c3521-431">There is only one activity in hello pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="c3521-432">**AssemblyName** jest ustawiona na nazwę toohello hello biblioteki DLL: **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="c3521-432">**AssemblyName** is set toohello name of hello DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="c3521-433">**Punkt wejścia** ustawiono zbyt**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="c3521-433">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="c3521-434">Zasadniczo jest \<przestrzeni nazw\>.\< ClassName\> w kodzie.</span><span class="sxs-lookup"><span data-stu-id="c3521-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="c3521-435">**PackageLinkedService** ustawiono zbyt**StorageLinkedService** wskazującego toohello magazynu obiektów blob, zawierający plik zip hello działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="c3521-435">**PackageLinkedService** is set too**StorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="c3521-436">Jeśli używasz różnych kont usługi Azure Storage dla wejścia/wyjścia plików i plik zip hello działań niestandardowych, masz toocreate innej usługi Azure Storage połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="c3521-436">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you have toocreate another Azure Storage linked service.</span></span> <span data-ttu-id="c3521-437">W tym artykule przyjęto założenie, że używasz hello tego samego konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-437">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="c3521-438">**PackageFile** ustawiono zbyt**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="c3521-438">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="c3521-439">Jest w formacie hello: \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="c3521-439">It is in hello format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="c3521-440">przyjmuje działania niestandardowego Hello **InputDataset** jako dane wejściowe i **OutputDataset** jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c3521-440">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="c3521-441">Witaj **linkedServiceName** właściwości niestandardowe działania hello punktów toohello **AzureBatchLinkedService**, który informuje usługi fabryka danych Azure tego działania niestandardowego hello musi toorun w partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-441">hello **linkedServiceName** property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch.</span></span>
   * <span data-ttu-id="c3521-442">Witaj **współbieżności** ustawienie jest ważne.</span><span class="sxs-lookup"><span data-stu-id="c3521-442">hello **concurrency** setting is important.</span></span> <span data-ttu-id="c3521-443">Jeśli używasz hello domyślną wartość, która ma wartość 1, nawet jeśli masz 2 lub obliczeniowe więcej węzłów w puli partii zadań Azure hello, wycinków hello są przetwarzane po kolei.</span><span class="sxs-lookup"><span data-stu-id="c3521-443">If you use hello default value, which is 1, even if you have 2 or more compute nodes in hello Azure Batch pool, hello slices are processed one after another.</span></span> <span data-ttu-id="c3521-444">W związku z tym nie korzystasz z możliwości przetwarzania równoległego hello partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-444">Therefore, you are not taking advantage of hello parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="c3521-445">Jeśli ustawisz **współbieżności** tooa wyższa wartość, powiedz 2, oznacza to dwa wycinków (odpowiada tootwo zadań w partii zadań Azure) mogą być przetwarzane w hello sam czas, w którym to przypadku obie maszyny wirtualne hello w hello są używane w puli partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-445">If you set **concurrency** tooa higher value, say 2, it means that two slices (corresponds tootwo tasks in Azure Batch) can be processed at hello same time, in which case, both hello VMs in hello Azure Batch pool are utilized.</span></span> <span data-ttu-id="c3521-446">W związku z tym odpowiednio ustawione hello właściwości współbieżności.</span><span class="sxs-lookup"><span data-stu-id="c3521-446">Therefore, set hello concurrency property appropriately.</span></span>
   * <span data-ttu-id="c3521-447">Tylko jedno zadanie (wycinek) jest wykonywana na maszynie Wirtualnej w dowolnym momencie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="c3521-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="c3521-448">Witaj przyczyna jest fakt, że domyślnie hello **maksymalna zadania dla maszyny Wirtualnej** ustawiono too1 puli partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-448">hello reason is that, by default, hello **Maximum tasks per VM** is set too1 for an Azure Batch pool.</span></span> <span data-ttu-id="c3521-449">W ramach wymagań wstępnych, pula jest utworzona z tym too2 zestaw właściwości, więc dwa wycinków fabryki danych może być uruchomiony na maszynie Wirtualnej na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="c3521-449">As part of prerequisites, you created a pool with this property set too2, so two Data Factory slices can be running on a VM at hello same time.</span></span>

    -   <span data-ttu-id="c3521-450">**isPaused** właściwość jest ustawieniem domyślnym toofalse.</span><span class="sxs-lookup"><span data-stu-id="c3521-450">**isPaused** property is set toofalse by default.</span></span> <span data-ttu-id="c3521-451">potok Hello uruchamia natychmiast w tym przykładzie, ponieważ wycinków hello uruchomić w przeszłości hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-451">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="c3521-452">Można ustawić tej właściwości tootrue toopause hello potoku i ustaw ją toorestart toofalse Wstecz.</span><span class="sxs-lookup"><span data-stu-id="c3521-452">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>

    -   <span data-ttu-id="c3521-453">Witaj **start** czasu i **zakończenia** czasy są od siebie pięć godzin i wycinki są tworzone co godzinę, więc pięć wycinków są produkowane przez potok hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-453">hello **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>

1. <span data-ttu-id="c3521-454">Kliknij przycisk **Wdróż** na pasku toodeploy hello potoku poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-454">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span>

#### <a name="step-5-test-hello-pipeline"></a><span data-ttu-id="c3521-455">Krok 5: Testowanie hello potoku</span><span class="sxs-lookup"><span data-stu-id="c3521-455">Step 5: Test hello pipeline</span></span>
<span data-ttu-id="c3521-456">W tym kroku należy przetestować potoku hello upuszczanie plików w folderach wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-456">In this step, you test hello pipeline by dropping files into hello input folders.</span></span> <span data-ttu-id="c3521-457">Zacznijmy testowania potoku hello z jednego pliku na jeden folder wejściowy.</span><span class="sxs-lookup"><span data-stu-id="c3521-457">Let’s start with testing hello pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="c3521-458">W bloku fabryki danych hello w hello portalu Azure, kliknij przycisk **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="c3521-458">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="c3521-459">W widoku diagramu hello, kliknij dwukrotnie plik wejściowy zestaw danych: **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c3521-459">In hello diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="c3521-460">Powinny pojawić się hello **InputDataset** blok z wszystkich pięciu wycinków gotowe.</span><span class="sxs-lookup"><span data-stu-id="c3521-460">You should see hello **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="c3521-461">Powiadomienie hello **czas rozpoczęcia WYCINEK** i **czas zakończenia WYCINEK** dla każdego wycinka.</span><span class="sxs-lookup"><span data-stu-id="c3521-461">Notice hello **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="c3521-462">W hello **widoku diagramu**, kliknij przycisk **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c3521-462">In hello **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="c3521-463">Powinny być widoczne czy hello pięć wycinki danych wyjściowych znajdują się w stanie gotowe hello już został utworzony.</span><span class="sxs-lookup"><span data-stu-id="c3521-463">You should see that hello five output slices are in hello Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="c3521-464">Użyj tooview portalu Azure hello **zadania** skojarzone z hello **wycinków** i sprawdzić, jakie maszyny Wirtualnej, każdy wycinek uruchomionego na.</span><span class="sxs-lookup"><span data-stu-id="c3521-464">Use Azure portal tooview hello **tasks** associated with hello **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="c3521-465">Zobacz [integracji fabryki danych i partii](#data-factory-and-batch-integration) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c3521-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="c3521-466">Powinny pojawić się pliki wyjściowe hello w hello `outputfolder` z `mycontainer` w Azure magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c3521-466">You should see hello output files in hello `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="c3521-467">Powinny pojawić się pięć plików wyjściowych, po jednej dla każdego wejściowego wycinka.</span><span class="sxs-lookup"><span data-stu-id="c3521-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="c3521-468">Każdy z hello output się, że plik powinien mieć zawartości toohello podobne następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c3521-468">Each of hello output file should have content similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="c3521-469">Witaj poniższym diagramie przedstawiono sposób wycinków fabryki danych hello mapowania tootasks w partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-469">hello following diagram illustrates how hello Data Factory slices map tootasks in Azure Batch.</span></span> <span data-ttu-id="c3521-470">W tym przykładzie wycinek ma tylko jeden przebieg.</span><span class="sxs-lookup"><span data-stu-id="c3521-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="c3521-471">Teraz spróbujmy z wieloma plikami w folderze.</span><span class="sxs-lookup"><span data-stu-id="c3521-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="c3521-472">Tworzenie plików: **Plik2.txt**, **file3.txt**, **file4.txt**, i **file5.txt** z hello tej samej zawartości, tak jak plik.txt w folderze hello: **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="c3521-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with hello same content as in file.txt in hello folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="c3521-473">W folderze wyjściowym hello **usunąć** hello pliku wyjściowego: **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="c3521-473">In hello output folder, **delete** hello output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="c3521-474">Teraz, w hello **OutputDataset** bloku, kliknij prawym przyciskiem myszy hello wycinek z **czas rozpoczęcia WYCINEK** ustawić także**2015-11-16 01:00:00 AM**i kliknij przycisk **Uruchom**toorerun/ponownie-process hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="c3521-474">Now, in hello **OutputDataset** blade, right-click hello slice with **SLICE START TIME** set too**11/16/2015 01:00:00 AM**, and click **Run** toorerun/re-process hello slice.</span></span> <span data-ttu-id="c3521-475">Teraz wycinek hello ma pięć plików zamiast jeden plik.</span><span class="sxs-lookup"><span data-stu-id="c3521-475">Now, hello slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="c3521-476">Po uruchomieniu hello wycinka i jego stan jest **gotowe**, sprawdź zawartość hello w pliku wyjściowym powitania dla tego wycinka (**2015-11-16-01.txt**) w hello `outputfolder` z `mycontainer` w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="c3521-476">After hello slice runs and its status is **Ready**, verify hello content in hello output file for this slice (**2015-11-16-01.txt**) in hello `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="c3521-477">Należy wiersz dla każdego pliku hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="c3521-477">There should be a line for each file of hello slice.</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="c3521-478">Jeśli nie została usunięta 2015 pliku wyjściowego hello-11-16-01.txt przed podjęciem próby z pięć plików wejściowych, zobacz jeden wiersz z hello wycinek poprzedniego uruchomienia i pięciu wierszach z hello wycinek bieżącego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="c3521-478">If you did not delete hello output file 2015-11-16-01.txt before trying with five input files, you see one line from hello previous slice run and five lines from hello current slice run.</span></span> <span data-ttu-id="c3521-479">Domyślnie zawartość hello jest plik dołączany toooutput, jeśli już istnieje.</span><span class="sxs-lookup"><span data-stu-id="c3521-479">By default, hello content is appended toooutput file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="c3521-480">Integracja z fabryki danych i usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="c3521-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="c3521-481">Witaj usługi fabryka danych tworzy zadanie w partii zadań Azure o nazwie hello: `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="c3521-481">hello Data Factory service creates a job in Azure Batch with hello name: `adf-poolname:job-xxx`.</span></span>

![Fabryka danych Azure - zadań wsadowych](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="c3521-483">Zadania w zadaniu hello jest tworzony przy każdym uruchomieniu działania wycinek.</span><span class="sxs-lookup"><span data-stu-id="c3521-483">A task in hello job is created for each activity run of a slice.</span></span> <span data-ttu-id="c3521-484">W przypadku 10 toobe gotowy wycinków przetwarzane 10 zadań są tworzone w hello zadania.</span><span class="sxs-lookup"><span data-stu-id="c3521-484">If there are 10 slices ready toobe processed, 10 tasks are created in hello job.</span></span> <span data-ttu-id="c3521-485">Może mieć więcej niż jeden wycinek typu uruchamiania równolegle, jeśli masz wiele węzłów obliczeniowych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-485">You can have more than one slice running in parallel if you have multiple compute nodes in hello pool.</span></span> <span data-ttu-id="c3521-486">Jeśli maksymalna zadań hello na obliczeniowe zbyt zestawu węzłów > 1, może istnieć więcej niż jedną slice uruchomionych na powitania obliczeniowych tej samej.</span><span class="sxs-lookup"><span data-stu-id="c3521-486">If hello maximum tasks per compute node is set too> 1, there can be more than one slice running on hello same compute.</span></span>

<span data-ttu-id="c3521-487">W tym przykładzie istnieje pięć wycinków, więc pięć zadań w partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="c3521-488">Z hello **współbieżności** ustawić także**5** hello w potoku JSON w fabryce danych Azure i **maksymalna zadania dla maszyny Wirtualnej** ustawić także**2** w partii zadań Azure Pula z **2** maszyn wirtualnych, hello zadań uruchamia szybkie (Sprawdź godziny rozpoczęcia i zakończenia zadania).</span><span class="sxs-lookup"><span data-stu-id="c3521-488">With hello **concurrency** set too**5** in hello pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set too**2** in Azure Batch pool with **2** VMs, hello tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="c3521-489">Użyj zadania wsadowego hello portalu tooview hello i jego zadań, które są skojarzone z hello **wycinków** i sprawdzić, jakie maszyny Wirtualnej, każdy wycinek uruchomionego na.</span><span class="sxs-lookup"><span data-stu-id="c3521-489">Use hello portal tooview hello Batch job and its tasks that are associated with hello **slices** and see what VM each slice ran on.</span></span>

![Fabryka danych Azure - zadań zadania wsadowego](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a><span data-ttu-id="c3521-491">Debugowanie hello potoku</span><span class="sxs-lookup"><span data-stu-id="c3521-491">Debug hello pipeline</span></span>
<span data-ttu-id="c3521-492">Debugowanie obejmuje kilka podstawowych technik:</span><span class="sxs-lookup"><span data-stu-id="c3521-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="c3521-493">Jeśli hello wycinek wejściowy nie jest ustawiona zbyt**gotowe**, potwierdź, że struktura folderów wejściowych hello jest poprawna i plik.txt istnieje w folderach wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="c3521-493">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and file.txt exists in hello input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="c3521-494">W hello **Execute** metody działania niestandardowego, użyj hello **IActivityLogger** toolog informacji o obiekcie, ułatwiające rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="c3521-494">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="c3521-495">wiadomości powitania rejestrowane widoczne w użytkownika hello\_plików dziennika 0.</span><span class="sxs-lookup"><span data-stu-id="c3521-495">hello logged messages show up in hello user\_0.log file.</span></span>

   <span data-ttu-id="c3521-496">W hello **OutputDataset** bloku, kliknij przycisk hello wycinek toosee hello **WYCINKA danych** bloku dla tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="c3521-496">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="c3521-497">Zostanie wyświetlony **uruchomień działania** dla tego wycinka.</span><span class="sxs-lookup"><span data-stu-id="c3521-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="c3521-498">Powinny pojawić się jeden uruchamiania dla wycinka hello działania.</span><span class="sxs-lookup"><span data-stu-id="c3521-498">You should see one activity run for hello slice.</span></span> <span data-ttu-id="c3521-499">Jeśli klikniesz przycisk **Uruchom** na pasku poleceń hello, można uruchomić inne działanie Uruchom hello tego samego wycinka.</span><span class="sxs-lookup"><span data-stu-id="c3521-499">If you click **Run** in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="c3521-500">Po kliknięciu przycisku uruchamiania działania hello Zobacz hello **szczegóły uruchomienia działania** bloku zawierającego listę plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="c3521-500">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="c3521-501">Zobacz zarejestrowane komunikaty w hello **użytkownika\_dziennika 0** pliku.</span><span class="sxs-lookup"><span data-stu-id="c3521-501">You see logged messages in hello **user\_0.log** file.</span></span> <span data-ttu-id="c3521-502">Po wystąpieniu błędu, zobacz trzech uruchomień działania ponieważ liczby ponownych prób hello ustawiono too3 w potoku hello/aktywność JSON.</span><span class="sxs-lookup"><span data-stu-id="c3521-502">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="c3521-503">Po kliknięciu przycisku uruchamiania działania hello możesz Zobacz pliki dziennika hello możesz przejrzeć tootroubleshoot hello błędu.</span><span class="sxs-lookup"><span data-stu-id="c3521-503">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="c3521-504">W hello listę plików dziennika, kliknij przycisk hello **0.log użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="c3521-504">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="c3521-505">W prawym panelu hello są wyniki hello przy użyciu hello **IActivityLogger.Write** metody.</span><span class="sxs-lookup"><span data-stu-id="c3521-505">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="c3521-506">Sprawdź system-0.log za wszelkie komunikaty o błędach systemu i wyjątki.</span><span class="sxs-lookup"><span data-stu-id="c3521-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="c3521-507">Zawierają hello **PDB** plików w pliku zip hello w celu hello szczegóły błędu mają informacje takie jak **stosu wywołań** po wystąpieniu błędu.</span><span class="sxs-lookup"><span data-stu-id="c3521-507">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="c3521-508">Wszystkie pliki w pliku zip hello Witaj dla działań niestandardowych hello musi znajdować się na powitania **najwyższego poziomu** z bez podfolderów.</span><span class="sxs-lookup"><span data-stu-id="c3521-508">All hello files in hello zip file for hello custom activity must be at hello **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="c3521-509">Upewnij się, że hello **assemblyName** (MyDotNetActivity.dll), **punktu wejścia** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip) i **packageLinkedService** (powinien Azure toohello punktu magazynu obiektów blob zawierający plik zip hello) są ustawione wartości toocorrect.</span><span class="sxs-lookup"><span data-stu-id="c3521-509">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
6. <span data-ttu-id="c3521-510">Stałe błędu i chcesz wycinek hello tooreprocess, kliknij prawym przyciskiem myszy hello wycinek hello **OutputDataset** bloku i kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="c3521-510">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="c3521-511">Zostanie wyświetlony **kontenera** w magazynie obiektów Blob Azure o nazwie: `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="c3521-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="c3521-512">Ten kontener nie jest automatycznie usuwana, ale można je bezpiecznie usunąć po zakończeniu testowania hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c3521-512">This container is not automatically deleted, but you can safely delete it after you are done testing hello solution.</span></span> <span data-ttu-id="c3521-513">Podobnie, hello rozwiązania fabryki danych tworzy partii zadań Azure **zadania** o nazwie: `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="c3521-513">Similarly, hello Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="c3521-514">Po Jeśli chcesz przetestować hello rozwiązania, można usunąć tego zadania.</span><span class="sxs-lookup"><span data-stu-id="c3521-514">You can delete this job after you test hello solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="c3521-515">działania niestandardowego Hello nie używa hello **app.config** plików z pakietu.</span><span class="sxs-lookup"><span data-stu-id="c3521-515">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="c3521-516">W związku z tym jeśli kod odczytuje wszelkie parametry połączenia z pliku konfiguracji hello, działa w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="c3521-516">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="c3521-517">Witaj najlepsze rozwiązanie przy użyciu partii zadań Azure jest toohold żadnych kluczy tajnych w **Azure KeyVault**, keyvault hello tooprotect główną usługi na podstawie certyfikatu, a dystrybucję hello certyfikatu tooAzure partii puli.</span><span class="sxs-lookup"><span data-stu-id="c3521-517">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello keyvault, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="c3521-518">Witaj działania niestandardowego .NET, a następnie mogą uzyskiwać dostęp do kluczy tajnych z hello KeyVault w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="c3521-518">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="c3521-519">To rozwiązanie jest rodzajowy i mogą być skalowane tooany typu klucza tajnego, nie tylko w parametrach połączenia.</span><span class="sxs-lookup"><span data-stu-id="c3521-519">This solution is a generic one and can scale tooany type of secret, not just connection string.</span></span>

    <span data-ttu-id="c3521-520">Istnieje obejście łatwiejsze (ale nie najlepiej): można utworzyć **Azure SQL połączona usługa** ustawień parametrów połączenia, tworzenie połączonej usługi i dataset hello łańcucha jako fikcyjny wejściowy zestaw danych tekst hello używa zestawu danych toohello niestandardowego działania .NET.</span><span class="sxs-lookup"><span data-stu-id="c3521-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="c3521-521">Mogą być następnie hello dostępu połączone usługi parametry połączenia w kodzie działania niestandardowego hello, powinny działać prawidłowo w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="c3521-521">You can then access hello linked service's connection string in hello custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-hello-sample"></a><span data-ttu-id="c3521-522">Rozszerzanie hello próbki</span><span class="sxs-lookup"><span data-stu-id="c3521-522">Extend hello sample</span></span>
<span data-ttu-id="c3521-523">Można rozszerzyć toolearn tej próbki więcej informacji na temat funkcji usługi fabryka danych Azure i partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-523">You can extend this sample toolearn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="c3521-524">Na przykład tooprocess wycinki inny zakres czasu, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c3521-524">For example, tooprocess slices in a different time range, do hello following steps:</span></span>

1. <span data-ttu-id="c3521-525">Dodaj następujące podfoldery hello hello `inputfolder`: 2015-11-16-05 2015-11-16-06 201-11-16-07, 2011-11-16-08, 2015-11-16-09 i miejscu plików wejściowych zawierających w tych folderach.</span><span class="sxs-lookup"><span data-stu-id="c3521-525">Add hello following subfolders in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="c3521-526">Zmień hello godziny zakończenia dla potoku hello z `2015-11-16T05:00:00Z` zbyt`2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="c3521-526">Change hello end time for hello pipeline from `2015-11-16T05:00:00Z` too`2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="c3521-527">W hello **widoku diagramu**, kliknij dwukrotnie hello **InputDataset**i Potwierdź, że wejściowy wycinków hello są gotowe.</span><span class="sxs-lookup"><span data-stu-id="c3521-527">In hello **Diagram View**, double-click hello **InputDataset**, and confirm that hello input slices are ready.</span></span> <span data-ttu-id="c3521-528">Kliknij dwukrotnie **OuptutDataset** toosee hello stanu wycinków danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c3521-528">Double-click **OuptutDataset** toosee hello state of output slices.</span></span> <span data-ttu-id="c3521-529">Jeśli są w stanie gotowe, sprawdź folder wyjściowy hello hello plików wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c3521-529">If they are in Ready state, check hello output folder for hello output files.</span></span>
2. <span data-ttu-id="c3521-530">Zwiększanie lub zmniejszanie hello **współbieżności** toounderstand ustawienie jak ma to wpływ na wydajność hello rozwiązania, szczególnie hello przetwarzania zachodzących w partii zadań Azure.</span><span class="sxs-lookup"><span data-stu-id="c3521-530">Increase or decrease hello **concurrency** setting toounderstand how it affects hello performance of your solution, especially hello processing that occurs on Azure Batch.</span></span> <span data-ttu-id="c3521-531">(Zobacz krok 4: tworzenie i uruchamianie potoku hello, aby uzyskać więcej informacji na temat hello **współbieżności** ustawienie.)</span><span class="sxs-lookup"><span data-stu-id="c3521-531">(See Step 4: Create and run hello pipeline for more on hello **concurrency** setting.)</span></span>
3. <span data-ttu-id="c3521-532">Tworzenie puli za pomocą/małe **maksymalna zadania dla maszyny Wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="c3521-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="c3521-533">toouse hello nowej puli, utworzoną przez siebie w hello aktualizacji usługi partia zadań Azure, połączone w rozwiązaniu do hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c3521-533">toouse hello new pool you created, update hello Azure Batch linked service in hello Data Factory solution.</span></span> <span data-ttu-id="c3521-534">(Zobacz krok 4: tworzenie i uruchamianie potoku hello, aby uzyskać więcej informacji na temat hello **maksymalna zadania dla maszyny Wirtualnej** ustawienie.)</span><span class="sxs-lookup"><span data-stu-id="c3521-534">(See Step 4: Create and run hello pipeline for more on hello **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="c3521-535">Tworzenie puli partii zadań Azure z **skalowania automatycznego** funkcji.</span><span class="sxs-lookup"><span data-stu-id="c3521-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="c3521-536">Automatyczne skalowanie węzłów obliczeniowych w puli partii zadań Azure to dynamiczne Dostosowywanie hello przetwarzania zasilania używanych przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="c3521-536">Automatically scaling compute nodes in an Azure Batch pool is hello dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="c3521-537">tutaj Hello przykładowa formuła osiąga hello następujące zachowanie: podczas tworzenia puli hello, rozpoczyna się od 1 maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c3521-537">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="c3521-538">Metryka $PendingTasks definiuje hello liczbę zadań uruchomiona + aktywny (w kolejce) stanu.</span><span class="sxs-lookup"><span data-stu-id="c3521-538">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="c3521-539">Formuła Hello znajduje hello średnią liczbę zadań oczekujących w hello ostatnich 180 sekund i odpowiednio ustawia TargetDedicated.</span><span class="sxs-lookup"><span data-stu-id="c3521-539">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="c3521-540">Gwarantuje, że TargetDedicated nigdy nie wykracza poza 25 maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c3521-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="c3521-541">Tak, jak nowe zadania są przesyłane, automatycznie zwiększa rozmiar puli i jako zakończenie zadania, maszyn wirtualnych stają się wolnego jeden po drugim i skalowanie automatyczne hello zmniejsza tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c3521-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="c3521-542">startingNumberOfVMs i maxNumberofVMs mogą być dostosowane tooyour potrzeb.</span><span class="sxs-lookup"><span data-stu-id="c3521-542">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>
 
    <span data-ttu-id="c3521-543">Formuła skalowania automatycznego:</span><span class="sxs-lookup"><span data-stu-id="c3521-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="c3521-544">Zobacz [automatycznie skali obliczeniowe węzłów w puli partii zadań Azure](../batch/batch-automatic-scaling.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c3521-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="c3521-545">Jeśli puli hello używa domyślnej hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello usługa partia zadań może zająć 15 do 30 minut tooprepare hello maszyny Wirtualnej przed uruchomieniem hello działania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="c3521-545">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="c3521-546">Jeśli pula hello jest przy użyciu różnych autoScaleEvaluationInterval, hello usługa partia zadań może zająć autoScaleEvaluationInterval + 10 minut.</span><span class="sxs-lookup"><span data-stu-id="c3521-546">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="c3521-547">W rozwiązaniu próbki hello hello **Execute** metoda wywołuje hello **Calculate** metody, która przetwarza dane wejściowe wycinek tooproduce wycinka danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c3521-547">In hello sample solution, hello **Execute** method invokes hello **Calculate** method that processes an input data slice tooproduce an output data slice.</span></span> <span data-ttu-id="c3521-548">Można napisać własny tooprocess — metoda dane wejściowe i Zastąp wywołanie metody Calculate hello w metody Execute hello metody tooyour połączeń.</span><span class="sxs-lookup"><span data-stu-id="c3521-548">You can write your own method tooprocess input data and replace hello Calculate method call in hello Execute method with a call tooyour method.</span></span>

### <a name="next-steps-consume-hello-data"></a><span data-ttu-id="c3521-549">Następne kroki: wykorzystują dane hello</span><span class="sxs-lookup"><span data-stu-id="c3521-549">Next steps: Consume hello data</span></span>
<span data-ttu-id="c3521-550">Po przetwarzania danych, można pobrać go online narzędzia, takie jak **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="c3521-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="c3521-551">Oto łącza toohelp zrozumienie usługi Power BI i w jaki sposób toouse go na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="c3521-551">Here are links toohelp you understand Power BI and how toouse it in Azure:</span></span>

* [<span data-ttu-id="c3521-552">Eksploruj zestawu danych w usłudze Power BI</span><span class="sxs-lookup"><span data-stu-id="c3521-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="c3521-553">Wprowadzenie do korzystania z hello Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c3521-553">Getting started with hello Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="c3521-554">Odświeżanie danych w usłudze Power BI</span><span class="sxs-lookup"><span data-stu-id="c3521-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="c3521-555">Azure i usługi Power BI — omówienie</span><span class="sxs-lookup"><span data-stu-id="c3521-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="c3521-556">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="c3521-556">References</span></span>
* [<span data-ttu-id="c3521-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c3521-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="c3521-558">Wprowadzenie tooAzure usługi fabryka danych</span><span class="sxs-lookup"><span data-stu-id="c3521-558">Introduction tooAzure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="c3521-559">Rozpoczynanie pracy z fabryką danych Azure</span><span class="sxs-lookup"><span data-stu-id="c3521-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="c3521-560">Korzystanie z działań niestandardowych w potoku usługi Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c3521-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="c3521-561">Partia zadań Azure</span><span class="sxs-lookup"><span data-stu-id="c3521-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="c3521-562">Podstawowe informacje o partii zadań Azure</span><span class="sxs-lookup"><span data-stu-id="c3521-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="c3521-563">Przegląd funkcji partii zadań Azure</span><span class="sxs-lookup"><span data-stu-id="c3521-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="c3521-564">Tworzenie i zarządzanie nimi konto partii zadań Azure w portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="c3521-564">Create and manage Azure Batch account in hello Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="c3521-565">Rozpoczynanie pracy z platformą .NET biblioteki usługi partia zadań Azure</span><span class="sxs-lookup"><span data-stu-id="c3521-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
