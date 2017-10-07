---
title: "klastry Hadoop na żądanie przy użyciu fabryki danych - Azure HDInsight aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, klastrów Hadoop na żądanie, w usłudze HDInsight przy użyciu fabryki danych Azure."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="9cdb7-103">Tworzenie na żądanie klastrów platformy Hadoop w usłudze HDInsight przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="9cdb7-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="9cdb7-104">[Fabryka danych Azure](../data-factory/data-factory-introduction.md) to usługa integracji danych opartych na chmurze, która organizuje i zautomatyzować przepływ hello i przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="9cdb7-105">On można tworzyć HDInsight Hadoop tooprocess just in time klastra wycinek danych wejściowych i usunąć hello klastra po zakończeniu przetwarzania hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-105">It can create a HDInsight Hadoop cluster just-in-time tooprocess an input data slice and delete hello cluster when hello processing is complete.</span></span> <span data-ttu-id="9cdb7-106">Zalety hello przy użyciu klastra usługi Hadoop w HDInsight na żądanie, należą:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-106">Some of hello benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="9cdb7-107">Tylko płatności dla zadania czas hello jest uruchomiona na powitania klastra usługi HDInsight Hadoop (oraz można skonfigurować krótki czas bezczynności).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-107">You only pay for hello time job is running on hello HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="9cdb7-108">Witaj rozliczeń dla klastrów usługi HDInsight jest proporcjonalnie za minutę, czy są używane lub nie.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-108">hello billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="9cdb7-109">Gdy używasz usługi HDInsight połączony na żądanie w fabryce danych klastrów hello są tworzone na żądanie.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-109">When you use an on-demand HDInsight linked service in Data Factory, hello clusters are created on-demand.</span></span> <span data-ttu-id="9cdb7-110">I klastrów hello są usuwane automatycznie po zakończeniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-110">And hello clusters are deleted automatically when hello jobs are completed.</span></span> <span data-ttu-id="9cdb7-111">W związku z tym płacisz tylko za uruchomione czasu i krótki czas bezczynności (ustawienie time-to-live) hello zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-111">Therefore, you only pay for hello job running time and hello brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="9cdb7-112">Można utworzyć przepływu pracy za pomocą potoku fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="9cdb7-113">Na przykład można mieć hello potoku toocopy danych z lokalnego programu SQL Server tooan magazynu obiektów blob platformy Azure, dane hello proces przez uruchomienie skryptu Hive i Pig skrypt w klastrze usługi HDInsight Hadoop na żądanie.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-113">For example, you can have hello pipeline toocopy data from an on-premises SQL Server tooan Azure blob storage, process hello data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="9cdb7-114">Następnie skopiuj hello wynik tooan danych Azure SQL Data Warehouse dla tooconsume aplikacji analizy Biznesowej.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-114">Then, copy hello result data tooan Azure SQL Data Warehouse for BI applications tooconsume.</span></span>
- <span data-ttu-id="9cdb7-115">Można zaplanować hello przepływu pracy toorun okresowo (co godzinę, codziennie, co tydzień, co miesiąc, itp.).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-115">You can schedule hello workflow toorun periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="9cdb7-116">W fabryce danych Azure fabryki danych może mieć co najmniej jeden potoki danych.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="9cdb7-117">Potoku danych ma co najmniej jednego działania.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="9cdb7-118">Istnieją dwa typy działań: [działań przepływu danych](../data-factory/data-factory-data-movement-activities.md) i [działań przekształcania danych](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="9cdb7-119">Używasz danych toomove działania (obecnie tylko działanie kopiowania) przeniesienia danych z magazynu danych źródła danych magazynu tooa docelowego.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-119">You use data movement activities (currently, only Copy Activity) toomove data from a source data store tooa destination data store.</span></span> <span data-ttu-id="9cdb7-120">Możesz użyć danych przekształcania działania tootransform/przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-120">You use data transformation activities tootransform/process data.</span></span> <span data-ttu-id="9cdb7-121">Działanie Hive HDInsight jest jednym z hello transformacji działania obsługiwane przez fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-121">HDInsight Hive Activity is one of hello transformation activities supported by Data Factory.</span></span> <span data-ttu-id="9cdb7-122">Używasz hello Hive transformacji działania w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-122">You use hello Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="9cdb7-123">Toouse działania hive można skonfigurować klaster usługi HDInsight Hadoop lub klastra usługi Hadoop w HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-123">You can configure a hive activity toouse your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="9cdb7-124">W tym samouczku hello Hive działania w potoku fabryki danych hello jest toouse skonfigurowany klaster usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-124">In this tutorial, hello Hive activity in hello data factory pipeline is configured toouse an on-demand HDInsight cluster.</span></span> <span data-ttu-id="9cdb7-125">W związku z tym hello działanie zostanie uruchomione tooprocess wycinka danych, po co się stanie:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-125">Therefore, when hello activity runs tooprocess a data slice, here is what happens:</span></span>

1. <span data-ttu-id="9cdb7-126">Klastra usługi HDInsight Hadoop jest tworzony automatycznie dla możesz tooprocess just in time hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-126">A HDInsight Hadoop cluster is automatically created for you just-in-time tooprocess hello slice.</span></span>  
2. <span data-ttu-id="9cdb7-127">dane wejściowe Hello są przetwarzane, uruchamiając skrypt HiveQL na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-127">hello input data is processed by running a HiveQL script on hello cluster.</span></span>
3. <span data-ttu-id="9cdb7-128">Witaj klastra usługi HDInsight Hadoop jest usuwany po zakończeniu przetwarzania hello i hello klastra jest w stanie bezczynności hello skonfigurowane ilość czasu (ustawienie timeToLive).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-128">hello HDInsight Hadoop cluster is deleted after hello processing is complete and hello cluster is idle for hello configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="9cdb7-129">Jeśli hello dalej wycinek danych jest dostępna do przetwarzania z tego czasu bezczynności timeToLive, hello tego samego klastra jest używany tooprocess hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-129">If hello next data slice is available for processing with in this timeToLive idle time, hello same cluster is used tooprocess hello slice.</span></span>  

<span data-ttu-id="9cdb7-130">W tym samouczku hello skrypt HiveQL skojarzone z działaniem hive hello wykonuje hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-130">In this tutorial, hello HiveQL script associated with hello hive activity performs hello following actions:</span></span>

1. <span data-ttu-id="9cdb7-131">Tworzy tabelę zewnętrzną odwołania hello web nieprzetworzone dane dziennika przechowywanych w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-131">Creates an external table that references hello raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="9cdb7-132">Partycje hello nieprzetworzone dane przez rok i miesiąc.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-132">Partitions hello raw data by year and month.</span></span>
3. <span data-ttu-id="9cdb7-133">Magazyny hello danych podzielonej na partycje w hello magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-133">Stores hello partitioned data in hello Azure blob storage.</span></span>

<span data-ttu-id="9cdb7-134">W tym samouczku hello skrypt HiveQL skojarzone z działaniem hive hello tworzy tabelę zewnętrzną odwołania hello raw web dziennika danych przechowywanych w hello magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-134">In this tutorial, hello HiveQL script associated with hello hive activity creates an external table that references hello raw web log data stored in hello Azure Blob Storage.</span></span> <span data-ttu-id="9cdb7-135">Poniżej przedstawiono hello Przykładowe wiersze dla każdego miesiąca w pliku wejściowym hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-135">Here are hello sample rows for each month in hello input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="9cdb7-136">partycje skrypt HiveQL Hello hello nieprzetworzone dane przez rok i miesiąc.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-136">hello HiveQL script partitions hello raw data by year and month.</span></span> <span data-ttu-id="9cdb7-137">Tworzy trzy foldery dane wyjściowe na podstawie danych wprowadzonych z poprzednich hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-137">It creates three output folders based on hello previous input.</span></span> <span data-ttu-id="9cdb7-138">Każdy folder zawiera plik z wpisów z każdego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="9cdb7-139">Aby uzyskać listę działań przekształcania danych fabryki danych w działaniu tooHive dodanie, zobacz [transformacji i analizy przy użyciu fabryki danych Azure](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-139">For a list of Data Factory data transformation activities in addition tooHive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9cdb7-140">Obecnie można tworzyć tylko klastra usługi HDInsight w wersji 3.2 z fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cdb7-141">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9cdb7-141">Prerequisites</span></span>
<span data-ttu-id="9cdb7-142">Przed rozpoczęciem powitalne instrukcje w tym artykule, musi mieć hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-142">Before you begin hello instructions in this article, you must have hello following items:</span></span>

* <span data-ttu-id="9cdb7-143">[Subskrypcja platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="9cdb7-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="9cdb7-145">Przygotowanie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="9cdb7-145">Prepare storage account</span></span>
<span data-ttu-id="9cdb7-146">Możesz użyć toothree kont magazynu w tym scenariuszu:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-146">You can use up toothree storage accounts in this scenario:</span></span>

- <span data-ttu-id="9cdb7-147">domyślne konto magazynu dla klastra usługi HDInsight hello</span><span class="sxs-lookup"><span data-stu-id="9cdb7-147">default storage account for hello HDInsight cluster</span></span>
- <span data-ttu-id="9cdb7-148">Konto magazynu dla danych wejściowych hello</span><span class="sxs-lookup"><span data-stu-id="9cdb7-148">storage account for hello input data</span></span>
- <span data-ttu-id="9cdb7-149">Konto magazynu dla danych wyjściowych hello</span><span class="sxs-lookup"><span data-stu-id="9cdb7-149">storage account for hello output data</span></span>

<span data-ttu-id="9cdb7-150">Samouczek hello toosimplify, możesz użyć jednego magazynu konta tooserve hello trzy funkcje.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-150">toosimplify hello tutorial, you use one storage account tooserve hello three purposes.</span></span> <span data-ttu-id="9cdb7-151">Przykładowy skrypt programu Azure PowerShell Hello, w tej sekcji wykonuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-151">hello Azure PowerShell sample script found in this section performs hello following tasks:</span></span>

1. <span data-ttu-id="9cdb7-152">Zaloguj się za tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-152">Log in tooAzure.</span></span>
2. <span data-ttu-id="9cdb7-153">Utwórz grupę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="9cdb7-154">Tworzenie konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="9cdb7-155">Tworzenie kontenera obiektów Blob na koncie magazynu hello</span><span class="sxs-lookup"><span data-stu-id="9cdb7-155">Create a Blob container in hello storage account</span></span>
5. <span data-ttu-id="9cdb7-156">Skopiuj następujące dwa pliki toohello obiektów Blob kontenera hello:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-156">Copy hello following two files toohello Blob container:</span></span>

   * <span data-ttu-id="9cdb7-157">Plik danych wejściowych: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="9cdb7-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="9cdb7-158">Skrypt HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="9cdb7-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="9cdb7-159">Oba pliki są przechowywane w publicznego kontenera obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="9cdb7-160">**tooprepare hello magazynu i skopiuj hello plików przy użyciu programu Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="9cdb7-160">**tooprepare hello storage and copy hello files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9cdb7-161">Określ nazwy grupy zasobów platformy Azure hello i hello kontem magazynu platformy Azure, który zostanie utworzony przez skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-161">Specify names for hello Azure resource group and hello Azure storage account that will be created by hello script.</span></span>
> <span data-ttu-id="9cdb7-162">Zapisz **Nazwa grupy zasobów**, **nazwy konta magazynu**, i **klucz konta magazynu** wyjściowych przez skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by hello script.</span></span> <span data-ttu-id="9cdb7-163">Należy je w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-163">You need them in hello next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="9cdb7-164">Jeśli potrzebujesz pomocy dotyczącej hello skrypt programu PowerShell, zobacz [hello Using Azure PowerShell z usługą Azure Storage](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-164">If you need help with hello PowerShell script, see [Using hello Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="9cdb7-165">Jeśli chcesz toouse wiersza polecenia platformy Azure, zobacz hello [dodatku](#appendix) sekcji hello skryptu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-165">If you like toouse Azure CLI instead, see hello [Appendix](#appendix) section for hello Azure CLI script.</span></span>

<span data-ttu-id="9cdb7-166">**tooexamine hello magazynu konto i hello zawartość**</span><span class="sxs-lookup"><span data-stu-id="9cdb7-166">**tooexamine hello storage account and hello contents**</span></span>

1. <span data-ttu-id="9cdb7-167">Zaloguj się na toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-167">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9cdb7-168">Kliknij przycisk **grup zasobów** w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-168">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="9cdb7-169">Kliknij dwukrotnie nazwę grupy zasobów hello utworzone za pomocą skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-169">Double-click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="9cdb7-170">Użyj filtru hello, jeśli masz zbyt wiele grup zasobów na liście.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-170">Use hello filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="9cdb7-171">Na powitania **zasobów** kafelka, powinna mieć jeden zasób z listy, chyba że współużytkować hello grupy zasobów z innymi projektami.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-171">On hello **Resources** tile, you shall have one resource listed unless you share hello resource group with other projects.</span></span> <span data-ttu-id="9cdb7-172">Ten zasób jest hello konta magazynu o nazwie hello określone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-172">That resource is hello storage account with hello name you specified earlier.</span></span> <span data-ttu-id="9cdb7-173">Kliknij nazwę konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-173">Click hello storage account name.</span></span>
5. <span data-ttu-id="9cdb7-174">Kliknij przycisk hello **obiekty BLOB** Kafelki.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-174">Click hello **Blobs** tiles.</span></span>
6. <span data-ttu-id="9cdb7-175">Kliknij przycisk hello **adfgetstarted** kontenera.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-175">Click hello **adfgetstarted** container.</span></span> <span data-ttu-id="9cdb7-176">Zobacz dwa foldery: **inputdata** i **skryptu**.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="9cdb7-177">Otwórz hello folder i sprawdź hello plików w folderach hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-177">Open hello folder and check hello files in hello folders.</span></span> <span data-ttu-id="9cdb7-178">Hello inputdata zawiera plik input.log hello z danych wejściowych i hello skryptu folder zawiera plik skryptu hello HiveQL.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-178">hello inputdata contains hello input.log file with input data and hello script folder contains hello HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="9cdb7-179">Tworzenie fabryki danych przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9cdb7-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="9cdb7-180">Konta magazynu hello, hello danych wejściowych i hello skrypt HiveQL przygotowane są gotowe toocreate fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-180">With hello storage account, hello input data, and hello HiveQL script prepared, you are ready toocreate an Azure data factory.</span></span> <span data-ttu-id="9cdb7-181">Istnieje kilka metod tworzenia fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="9cdb7-182">Przez wdrożenie szablonu usługi Azure Resource Manager przy użyciu hello portalu Azure, w tym samouczku tworzenie fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using hello Azure portal.</span></span> <span data-ttu-id="9cdb7-183">Można także wdrożyć przy użyciu szablonu usługi Resource Manager [interfejsu wiersza polecenia Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) i [programu Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="9cdb7-184">Dla innych metod tworzenia fabryki danych, zobacz [samouczek: Tworzenie pierwszego fabrykę danych](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="9cdb7-185">Kliknij przycisk hello toosign obrazu w tooAzure i otwórz hello szablonu usługi Resource Manager w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-185">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> <span data-ttu-id="9cdb7-186">Szablon Hello znajduje się w https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-186">hello template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="9cdb7-187">Zobacz hello [jednostek fabryki danych w szablonie hello](#data-factory-entities-in-the-template) sekcji, aby uzyskać szczegółowe informacje na temat jednostek zdefiniowanych w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-187">See hello [Data Factory entities in hello template](#data-factory-entities-in-the-template) section for detailed information about entities defined in hello template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="9cdb7-188">Wybierz **Użyj istniejącego** opcję hello **grupy zasobów** ustawienie i wybierz hello nazwę grupy zasobów hello utworzony w poprzednim kroku hello (przy użyciu skryptu programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-188">Select **Use existing** option for hello **Resource group** setting, and select hello name of hello resource group you created in hello previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="9cdb7-189">Wprowadź nazwę dla fabryki danych hello (**nazwa fabryki danych**).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-189">Enter a name for hello data factory (**Data Factory Name**).</span></span> <span data-ttu-id="9cdb7-190">Ta nazwa musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="9cdb7-191">Wprowadź hello **nazwy konta magazynu** i **klucz konta magazynu** zapisanej w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-191">Enter hello **storage account name** and **storage account key** you wrote down in hello previous step.</span></span>
5. <span data-ttu-id="9cdb7-192">Wybierz **akceptuję warunki toohello** powyższych po odczytaniu za pośrednictwem **warunków i postanowień**.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-192">Select **I agree toohello terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="9cdb7-193">Wybierz **toodashboard numeru Pin** opcji.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-193">Select **Pin toodashboard** option.</span></span>
6. <span data-ttu-id="9cdb7-194">Kliknij przycisk **zakupu/utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="9cdb7-195">Zobacz kafelka na powitania pulpit nawigacyjny o nazwie **wdrażanie szablonu wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-195">You see a tile on hello Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="9cdb7-196">Poczekaj na powitania **grupy zasobów** zostanie otwarty blok grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-196">Wait until hello **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="9cdb7-197">Możesz również kliknąć Kafelek hello pod nazwą Twojej grupy nazwa tooopen hello zasobów bloku grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-197">You can also click hello tile titled as your resource group name tooopen hello resource group blade.</span></span>
6. <span data-ttu-id="9cdb7-198">Kliknięcie grupy zasobów hello hello kafelka tooopen bloku grupy zasobów hello nie jest jeszcze otwarty.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-198">Click hello tile tooopen hello resource group if hello resource group blade is not already open.</span></span> <span data-ttu-id="9cdb7-199">Teraz powinien zostać wyświetlony zasobów fabryki danych więcej oprócz wymienionych zasobów konta magazynu toohello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-199">Now you shall see one more data factory resource listed in addition toohello storage account resource.</span></span>
7. <span data-ttu-id="9cdb7-200">Kliknij nazwę hello w fabryce danych (wartość określona dla hello **nazwa fabryki danych** parametru).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-200">Click hello name of your data factory (value you specified for hello **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="9cdb7-201">W bloku fabryki danych powitania kliknij hello **Diagram** kafelka.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-201">In hello Data Factory blade, click hello **Diagram** tile.</span></span> <span data-ttu-id="9cdb7-202">Witaj diagram przedstawia jedno działanie z zestawem danych wejściowych i wyjściowy zestaw danych:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-202">hello diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Azure diagram potoku działania Hive HDInsight fabryki danych na żądanie](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="9cdb7-204">nazwy Hello są definiowane w szablonie usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-204">hello names are defined in hello Resource Manager template.</span></span>
9. <span data-ttu-id="9cdb7-205">Kliknij dwukrotnie **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="9cdb7-206">Na powitania **ostatnie zaktualizowane wycinków**, powinien zostać wyświetlony jeden wycinek typu.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-206">On hello **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="9cdb7-207">Jeśli jest w stanie hello **w toku**, poczekaj, aż zostanie on zmieniony zbyt**gotowe**.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-207">If hello status is **In progress**, wait until it is changed too**Ready**.</span></span> <span data-ttu-id="9cdb7-208">Zwykle trwa około **20 minut** toocreate klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-208">It usually takes about **20 minutes** toocreate an HDInsight cluster.</span></span>

### <a name="check-hello-data-factory-output"></a><span data-ttu-id="9cdb7-209">Sprawdź dane wyjściowe fabryki danych hello</span><span class="sxs-lookup"><span data-stu-id="9cdb7-209">Check hello data factory output</span></span>

1. <span data-ttu-id="9cdb7-210">Użyj hello same procedury w programie hello ostatniej sesji toocheck hello kontenery hello adfgetstarted kontenera.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-210">Use hello same procedure in hello last session toocheck hello containers of hello adfgetstarted container.</span></span> <span data-ttu-id="9cdb7-211">Istnieją dwa nowe kontenery dodatkowo zbyt**adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-211">There are two new containers in addition too**adfgetsarted**:</span></span>

   * <span data-ttu-id="9cdb7-212">Kontener o nazwie następującym wzorzec hello: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-212">A container with name that follows hello pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="9cdb7-213">Ten kontener jest hello domyślny kontener dla klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-213">This container is hello default container for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="9cdb7-214">adfjobs: ten kontener jest kontener hello ADF hello z dziennikami zadań.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-214">adfjobs: This container is hello container for hello ADF job logs.</span></span>

     <span data-ttu-id="9cdb7-215">dane wyjściowe fabryki danych Hello są przechowywane w **afgetstarted** zgodnie z konfiguracją w hello szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-215">hello data factory output is stored in **afgetstarted** as you configured in hello Resource Manager template.</span></span>
2. <span data-ttu-id="9cdb7-216">Kliknij przycisk **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="9cdb7-217">Kliknij dwukrotnie **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="9cdb7-218">Zostanie wyświetlony **roku = 2014** folderu, ponieważ wszystkie dzienniki sieci web hello są dniu 2014 roku.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-218">You see a **year=2014** folder because all hello web logs are dated in year 2014.</span></span>

    ![Azure HDInsight fabryki danych na żądanie Hive potoku dane wyjściowe działania](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="9cdb7-220">Jeśli możesz przejść do szczegółów listy hello, zostanie wyświetlona trzy foldery stycznia, lutego i marca.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-220">If you drill down hello list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="9cdb7-221">I ma dziennika dla każdego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-221">And there is a log for each month.</span></span>

    ![Azure HDInsight fabryki danych na żądanie Hive potoku dane wyjściowe działania](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="9cdb7-223">Obiekty fabryki danych w szablonie hello</span><span class="sxs-lookup"><span data-stu-id="9cdb7-223">Data Factory entities in hello template</span></span>
<span data-ttu-id="9cdb7-224">Oto, jak hello najwyższego poziomu szablonu usługi Resource Manager dla fabryki danych wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-224">Here is how hello top-level Resource Manager template for a data factory looks like:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a><span data-ttu-id="9cdb7-225">Definiowanie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="9cdb7-225">Define data factory</span></span>
<span data-ttu-id="9cdb7-226">Fabryka danych definiuje się w szablonie usługi Resource Manager hello pokazane na powitania następujące przykładowe:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-226">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="9cdb7-227">Hello dataFactoryName jest hello nazwa fabryki danych hello przez użytkownika podczas wdrażania szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-227">hello dataFactoryName is hello name of hello data factory you specify when you deploy hello template.</span></span> <span data-ttu-id="9cdb7-228">Fabryka danych jest obecnie obsługiwane tylko w regionach wschodnie stany USA, zachodnie stany USA i Europa Północna, Europa hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-228">Data factory is currently only supported in hello East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-hello-data-factory"></a><span data-ttu-id="9cdb7-229">Definiowanie jednostek w fabryce danych hello</span><span class="sxs-lookup"><span data-stu-id="9cdb7-229">Defining entities within hello data factory</span></span>
<span data-ttu-id="9cdb7-230">Hello następujące jednostek fabryki danych są definiowane w szablonie JSON hello:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-230">hello following Data Factory entities are defined in hello JSON template:</span></span>

* [<span data-ttu-id="9cdb7-231">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9cdb7-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="9cdb7-232">Połączona usługa HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="9cdb7-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="9cdb7-233">Wejściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9cdb7-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="9cdb7-234">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9cdb7-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="9cdb7-235">Potok danych z działaniem kopiowania</span><span class="sxs-lookup"><span data-stu-id="9cdb7-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="9cdb7-236">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9cdb7-236">Azure Storage linked service</span></span>
<span data-ttu-id="9cdb7-237">Hello Azure Storage połączone usługi łączy fabrykę danych toohello konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-237">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="9cdb7-238">W tym samouczku hello tego samego konta magazynu jest używany jako hello domyślne konto magazynu usługi HDInsight, Magazyn danych wejściowych i przechowywania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-238">In this tutorial, hello same storage account is used as hello default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="9cdb7-239">W związku z tym można zdefiniować tylko jednego magazynu Azure połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="9cdb7-240">W definicji usługi hello połączone Określ nazwę hello i klucza konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-240">In hello linked service definition, you specify hello name and key of your Azure storage account.</span></span> <span data-ttu-id="9cdb7-241">Zobacz [połączonej usługi magazynu Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) szczegółowe informacje o toodefine właściwości używane w formacie JSON połączonej usługi magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="9cdb7-242">Witaj **connectionString** używa hello parametry storageAccountName i storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-242">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="9cdb7-243">Podczas wdrażania szablonu hello można określić wartości tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-243">You specify values for these parameters while deploying hello template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="9cdb7-244">Połączona usługa HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="9cdb7-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="9cdb7-245">W hello HDInsight na żądanie połączone definicji usługi, można określić wartości parametrów konfiguracji, które są używane przez toocreate usługi fabryka danych hello klastra usługi HDInsight Hadoop w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-245">In hello on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by hello Data Factory service toocreate a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="9cdb7-246">Zobacz [obliczeniowe połączonych usług](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artykuł szczegółowe informacje o toodefine właściwości używane w formacie JSON na żądanie połączoną usługą usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="9cdb7-247">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-247">Note hello following points:</span></span>

* <span data-ttu-id="9cdb7-248">Witaj fabryki danych tworzy **opartych na systemie Linux** klastra usługi HDInsight dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-248">hello Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="9cdb7-249">Witaj klastra usługi HDInsight Hadoop jest tworzony w hello sam regionu co konto magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-249">hello HDInsight Hadoop cluster is created in hello same region as hello storage account.</span></span>
* <span data-ttu-id="9cdb7-250">Powiadomienie hello *timeToLive* ustawienie.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-250">Notice hello *timeToLive* setting.</span></span> <span data-ttu-id="9cdb7-251">fabryki danych Hello automatycznie usuwa hello klastra, po bezczynności hello klastra przez 30 minut.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-251">hello data factory deletes hello cluster automatically after hello cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="9cdb7-252">Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-252">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="9cdb7-253">Po usunięciu klastra hello HDInsight nie usunie tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-253">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="9cdb7-254">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-254">This behavior is by design.</span></span> <span data-ttu-id="9cdb7-255">Z usługą HDInsight połączony na żądanie, klastra usługi HDInsight jest tworzony za każdym razem, gdy wycinek musi toobe przetwarzane, o ile istnieje istniejącego klastra na żywo (**timeToLive**) i zostaną usunięte po zakończeniu przetwarzania hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

<span data-ttu-id="9cdb7-256">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cdb7-257">Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="9cdb7-258">Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-258">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="9cdb7-259">nazwy Hello kontenery wykonaj wzorca: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="9cdb7-259">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="9cdb7-260">Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="9cdb7-261">Wejściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9cdb7-261">Azure blob input dataset</span></span>
<span data-ttu-id="9cdb7-262">W definicji zestawu danych wejściowych hello należy określić nazwy hello folder, plik zawierający dane wejściowe hello i kontener obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-262">In hello input dataset definition, you specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="9cdb7-263">Zobacz [właściwości zestawu danych obiektów Blob platformy Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawu danych obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

<span data-ttu-id="9cdb7-264">Zwróć uwagę hello następujące ustawienia określone w definicji JSON hello:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-264">Notice hello following specific settings in hello JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="9cdb7-265">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9cdb7-265">Azure Blob output dataset</span></span>
<span data-ttu-id="9cdb7-266">W definicji zestawu danych wyjściowych hello należy określić nazwy hello kontenera obiektów blob i folderu, która przechowuje dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-266">In hello output dataset definition, you specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="9cdb7-267">Zobacz [właściwości zestawu danych obiektów Blob platformy Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) szczegółowe informacje o toodefine właściwości używane JSON zestawu danych obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

<span data-ttu-id="9cdb7-268">Witaj folderPath określa hello folder toohello ścieżki, która przechowuje dane wyjściowe hello:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-268">hello folderPath specifies hello path toohello folder that holds hello output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="9cdb7-269">Witaj [dostępności zestawu danych](../data-factory/data-factory-create-datasets.md#dataset-availability) ustawienie wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-269">hello [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="9cdb7-270">W fabryce danych Azure wyjściowej potoku hello dysków dostępności zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-270">In Azure Data Factory, output dataset availability drives hello pipeline.</span></span> <span data-ttu-id="9cdb7-271">W tym przykładzie wycinek hello jest tworzony co miesiąc na powitania ostatni dzień miesiąca (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-271">In this example, hello slice is produced monthly on hello last day of month (EndOfInterval).</span></span> <span data-ttu-id="9cdb7-272">Aby uzyskać więcej informacji, zobacz [planowania fabryki danych i wykonywania](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="9cdb7-273">Potok danych</span><span class="sxs-lookup"><span data-stu-id="9cdb7-273">Data pipeline</span></span>
<span data-ttu-id="9cdb7-274">Należy zdefiniować potok, który przekształca danych przez uruchomienie skryptu Hive w klastrze usługi Azure HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="9cdb7-275">Zobacz [JSON potoku](../data-factory/data-factory-create-pipelines.md#pipeline-json) opisy toodefine elementów JSON potoku, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span>

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="9cdb7-276">potok Hello zawiera jedno działanie, HDInsightHive działania.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-276">hello pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="9cdb7-277">Jak zarówno rozpoczęcia i zakończenia daty są styczeń 2016 r., dane tylko jeden miesiąc (wycinek) jest przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="9cdb7-278">Zarówno *start* i *zakończenia* hello działania mają datę przeszłą, więc hello fabryki danych przetwarza dane dla miesiąca hello natychmiast.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-278">Both *start* and *end* of hello activity have a past date, so hello Data Factory processes data for hello month immediately.</span></span> <span data-ttu-id="9cdb7-279">Jeśli zakończenie hello jest datą przyszłą, fabryki danych hello tworzy innego wycinek hello nastąpi.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-279">If hello end is a future date, hello data factory creates another slice when hello time comes.</span></span> <span data-ttu-id="9cdb7-280">Aby uzyskać więcej informacji, zobacz [planowania fabryki danych i wykonywania](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="9cdb7-281">Wyczyść hello samouczka</span><span class="sxs-lookup"><span data-stu-id="9cdb7-281">Clean up hello tutorial</span></span>

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="9cdb7-282">Usuń kontenerów obiektów blob hello utworzoną przez klaster usługi HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="9cdb7-282">Delete hello blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="9cdb7-283">Z usługą HDInsight połączony na żądanie klaster usługi HDInsight jest tworzony za każdym razem, gdy wycinek musi toobe przetwarzane, o ile istnieje istniejącego klastra na żywo (timeToLive); i hello klastra zostaną usunięte po zakończeniu przetwarzania hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (timeToLive); and hello cluster is deleted when hello processing is done.</span></span> <span data-ttu-id="9cdb7-284">Dla każdego klastra fabryki danych Azure tworzy kontener obiektów blob w hello używane jako konto stroage domyślne powitania dla klastra hello magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-284">For each cluster, Azure Data Factory creates a blob container in hello Azure blob storage used as hello default stroage account for hello cluster.</span></span> <span data-ttu-id="9cdb7-285">Nawet po usunięciu klastra usługi HDInsight hello domyślnego kontenera magazynu obiektów blob i hello skojarzone konto magazynu nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-285">Even though HDInsight cluster is deleted, hello default blob storage container and hello associated storage account are not deleted.</span></span> <span data-ttu-id="9cdb7-286">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-286">This behavior is by design.</span></span> <span data-ttu-id="9cdb7-287">Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="9cdb7-288">Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-288">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="9cdb7-289">nazwy Hello kontenery wykonaj wzorca: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-289">hello names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="9cdb7-290">Usuń hello **adfjobs** i **adfyourdatafactoryname-linkedservicename-datetimestamp** folderów.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-290">Delete hello **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="9cdb7-291">kontener adfjobs Hello zawiera z fabryki danych Azure z dziennikami zadań.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-291">hello adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-hello-resource-group"></a><span data-ttu-id="9cdb7-292">Usuń grupę zasobów hello</span><span class="sxs-lookup"><span data-stu-id="9cdb7-292">Delete hello resource group</span></span>
<span data-ttu-id="9cdb7-293">[Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) jest używane toodeploy, zarządzanie i monitorowanie rozwiązania jako grupa.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used toodeploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="9cdb7-294">Usunięcie grupy zasobów powoduje usunięcie wszystkich składników hello wewnątrz hello grupy.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-294">Deleting a resource group deletes all hello components inside hello group.</span></span>  

1. <span data-ttu-id="9cdb7-295">Zaloguj się na toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-295">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9cdb7-296">Kliknij przycisk **grup zasobów** w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-296">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="9cdb7-297">Kliknij nazwę grupy zasobów hello utworzone za pomocą skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-297">Click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="9cdb7-298">Użyj filtru hello, jeśli masz zbyt wiele grup zasobów na liście.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-298">Use hello filter if you have too many resource groups listed.</span></span> <span data-ttu-id="9cdb7-299">Witaj, grupy zasobów zostanie otwarty w nowym bloku.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-299">It opens hello resource group in a new blade.</span></span>
4. <span data-ttu-id="9cdb7-300">Na powitania **zasobów** kafelka, użytkownik ma hello domyślne konto magazynu i fabryki danych hello, chyba że współużytkować hello grupy zasobów z innymi projektami na liście.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-300">On hello **Resources** tile, you shall have hello default storage account and hello data factory listed unless you share hello resource group with other projects.</span></span>
5. <span data-ttu-id="9cdb7-301">Kliknij przycisk **usunąć** u góry hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-301">Click **Delete** on hello top of hello blade.</span></span> <span data-ttu-id="9cdb7-302">To spowoduje usunięcie konta magazynu hello i hello dane przechowywane na koncie magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-302">Doing so deletes hello storage account and hello data stored in hello storage account.</span></span>
6. <span data-ttu-id="9cdb7-303">Wprowadź hello zasobów grupy nazwa tooconfirm usunięcia, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-303">Enter hello resource group name tooconfirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="9cdb7-304">W przypadku, gdy nie ma konta magazynu hello toodelete podczas usuwania grupy zasobów hello, należy wziąć pod uwagę powitania po architektura oddzielając hello danych biznesowych z hello domyślne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-304">In case you don't want toodelete hello storage account when you delete hello resource group, consider hello following architecture by separating hello business data from hello default storage account.</span></span> <span data-ttu-id="9cdb7-305">W takim przypadku jedna grupa zasobów dla konta magazynu hello hello danych biznesowych i hello innej grupie zasobów dla hello domyślne konto magazynu dla usługi HDInsight połączonej usługi i hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-305">In this case, you have one resource group for hello storage account with hello business data, and hello other resource group for hello default storage account for HDInsight linked service and hello data factory.</span></span> <span data-ttu-id="9cdb7-306">Po usunięciu hello drugiej grupy zasobów nie wpływa na konto magazynu danych biznesowych hello.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-306">When you delete hello second resource group, it does not impact hello business data storage account.</span></span> <span data-ttu-id="9cdb7-307">toodo tak:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-307">toodo so:</span></span>

* <span data-ttu-id="9cdb7-308">Dodaj hello następujące grupy zasobów najwyższego poziomu toohello wraz z hello Microsoft.DataFactory/datafactories zasobów w szablonie usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-308">Add hello following toohello top-level resource group along with hello Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="9cdb7-309">Tworzy konto magazynu:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-309">It creates a storage account:</span></span>

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* <span data-ttu-id="9cdb7-310">Dodaj nowe konto nowego magazynu punktu toohello połączonej usługi:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-310">Add a new linked service point toohello new storage account:</span></span>

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* <span data-ttu-id="9cdb7-311">Skonfiguruj hello HDInsight na żądanie połączone usługi z dodatkowych dependsOn i additionalLinkedServiceNames:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-311">Configure hello HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a><span data-ttu-id="9cdb7-312">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9cdb7-312">Next steps</span></span>
<span data-ttu-id="9cdb7-313">W tym artykule wiesz już, jak tooprocess klastra usługi HDInsight toouse fabryki danych Azure toocreate na żądanie zadań Hive.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-313">In this article, you have learned how toouse Azure Data Factory toocreate on-demand HDInsight cluster tooprocess Hive jobs.</span></span> <span data-ttu-id="9cdb7-314">tooread więcej:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-314">tooread more:</span></span>

* [<span data-ttu-id="9cdb7-315">Samouczek Hadoop: rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9cdb7-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="9cdb7-316">Tworzenie klastrów opartych na systemie Linux platformą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9cdb7-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="9cdb7-317">Dokumentacja dotycząca usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="9cdb7-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="9cdb7-318">Dokumentacja fabryki danych</span><span class="sxs-lookup"><span data-stu-id="9cdb7-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="9cdb7-319">Dodatek</span><span class="sxs-lookup"><span data-stu-id="9cdb7-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="9cdb7-320">Skryptu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9cdb7-320">Azure CLI script</span></span>
<span data-ttu-id="9cdb7-321">Można użyć interfejsu wiersza polecenia Azure, zamiast przy użyciu programu Azure PowerShell toodo hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-321">You can use Azure CLI instead of using Azure PowerShell toodo hello tutorial.</span></span> <span data-ttu-id="9cdb7-322">toouse wiersza polecenia platformy Azure, najpierw zainstaluj wiersza polecenia platformy Azure zgodnie z instrukcjami hello:</span><span class="sxs-lookup"><span data-stu-id="9cdb7-322">toouse Azure CLI, first install Azure CLI as per hello following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a><span data-ttu-id="9cdb7-323">Użyj interfejsu wiersza polecenia Azure tooprepare hello magazynu i skopiuj pliki hello</span><span class="sxs-lookup"><span data-stu-id="9cdb7-323">Use Azure CLI tooprepare hello storage and copy hello files</span></span>

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

<span data-ttu-id="9cdb7-324">Nazwa kontenera Hello jest *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-324">hello container name is *adfgetstarted*.</span></span> <span data-ttu-id="9cdb7-325">Zachować, ponieważ jest on.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-325">Keep it as it is.</span></span> <span data-ttu-id="9cdb7-326">W przeciwnym razie należy szablonu usługi Resource Manager hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="9cdb7-326">Otherwise you need tooupdate hello Resource Manager template.</span></span> <span data-ttu-id="9cdb7-327">Aby uzyskać pomoc dotyczącą tego skryptu interfejsu wiersza polecenia, zobacz [hello używanie interfejsu wiersza polecenia Azure z usługą Azure Storage](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9cdb7-327">If you need help with this CLI script, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
