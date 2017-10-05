---
title: "Tworzenie klastrów Hadoop na żądanie przy użyciu fabryki danych - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć na żądanie klastrów platformy Hadoop w usłudze HDInsight przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: e68f1d72965d9516e0552c84d03d234c21739390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="7f61f-103">Tworzenie na żądanie klastrów platformy Hadoop w usłudze HDInsight przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="7f61f-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="7f61f-104">[Fabryka danych Azure](../data-factory/data-factory-introduction.md) to usługa integracji danych opartych na chmurze, która organizuje i automatyzuje przepływu i przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="7f61f-105">Można go utworzyć HDInsight Hadoop klastra just-in-time do przetwarzania wycinka danych wejściowych i usunąć klaster, po zakończeniu przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="7f61f-105">It can create a HDInsight Hadoop cluster just-in-time to process an input data slice and delete the cluster when the processing is complete.</span></span> <span data-ttu-id="7f61f-106">Korzyści wynikające ze stosowania klastra usługi Hadoop w HDInsight na żądanie, należą:</span><span class="sxs-lookup"><span data-stu-id="7f61f-106">Some of the benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="7f61f-107">Tylko płatności dla zadania czasu jest zasilany z klastra usługi HDInsight Hadoop (oraz krótki czas bezczynności można konfigurować).</span><span class="sxs-lookup"><span data-stu-id="7f61f-107">You only pay for the time job is running on the HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="7f61f-108">Rozliczenia dla klastrów usługi HDInsight jest proporcjonalnie za minutę, czy są używane lub nie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-108">The billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="7f61f-109">Gdy używasz usługi HDInsight połączony na żądanie w fabryce danych klastry są tworzone na żądanie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-109">When you use an on-demand HDInsight linked service in Data Factory, the clusters are created on-demand.</span></span> <span data-ttu-id="7f61f-110">I klastrów są automatycznie usuwane po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="7f61f-110">And the clusters are deleted automatically when the jobs are completed.</span></span> <span data-ttu-id="7f61f-111">W związku z tym płacisz tylko za uruchomione czasu i krótki czas bezczynności (ustawienie time-to-live) zadanie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-111">Therefore, you only pay for the job running time and the brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="7f61f-112">Można utworzyć przepływu pracy za pomocą potoku fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="7f61f-113">Na przykład można mieć potoku, aby skopiować dane z lokalnego programu SQL Server do magazynu obiektów blob platformy Azure, przetwarzania danych przez uruchomienie skryptu Hive i Pig skrypt w klastrze usługi HDInsight Hadoop na żądanie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-113">For example, you can have the pipeline to copy data from an on-premises SQL Server to an Azure blob storage, process the data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="7f61f-114">Następnie skopiuj dane wynikowe do magazyn danych SQL Azure dla aplikacji korzystających ze BI.</span><span class="sxs-lookup"><span data-stu-id="7f61f-114">Then, copy the result data to an Azure SQL Data Warehouse for BI applications to consume.</span></span>
- <span data-ttu-id="7f61f-115">Można zaplanować uruchamianie okresowo (co godzinę, codziennie, co tydzień, co miesiąc, itp.) przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="7f61f-115">You can schedule the workflow to run periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="7f61f-116">W fabryce danych Azure fabryki danych może mieć co najmniej jeden potoki danych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="7f61f-117">Potoku danych ma co najmniej jednego działania.</span><span class="sxs-lookup"><span data-stu-id="7f61f-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="7f61f-118">Istnieją dwa typy działań: [działań przepływu danych](../data-factory/data-factory-data-movement-activities.md) i [działań przekształcania danych](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7f61f-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="7f61f-119">Działania przepływu danych (obecnie tylko działanie kopiowania) służy do przenoszenia danych z magazynu danych źródłowych w magazynie danych docelowym.</span><span class="sxs-lookup"><span data-stu-id="7f61f-119">You use data movement activities (currently, only Copy Activity) to move data from a source data store to a destination data store.</span></span> <span data-ttu-id="7f61f-120">Działania przekształcania danych służy do procesu przekształcenia danych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-120">You use data transformation activities to transform/process data.</span></span> <span data-ttu-id="7f61f-121">Działanie Hive HDInsight jest jednym z działania przekształcania obsługiwane przez fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-121">HDInsight Hive Activity is one of the transformation activities supported by Data Factory.</span></span> <span data-ttu-id="7f61f-122">Działanie przekształcania Hive jest służy w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="7f61f-122">You use the Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="7f61f-123">Można skonfigurować działanie gałęzi do używania klastra usługi HDInsight Hadoop lub klastra usługi Hadoop w HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-123">You can configure a hive activity to use your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="7f61f-124">W tym samouczku Hive działania w potoku fabryki danych jest skonfigurowany do używania klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-124">In this tutorial, the Hive activity in the data factory pipeline is configured to use an on-demand HDInsight cluster.</span></span> <span data-ttu-id="7f61f-125">W związku z tym po uruchomieniu działania do przetwarzania wycinka danych, Oto co się stanie:</span><span class="sxs-lookup"><span data-stu-id="7f61f-125">Therefore, when the activity runs to process a data slice, here is what happens:</span></span>

1. <span data-ttu-id="7f61f-126">Klastra usługi HDInsight Hadoop jest tworzona automatycznie dla możesz just-in-time przetwarzania wycinka.</span><span class="sxs-lookup"><span data-stu-id="7f61f-126">A HDInsight Hadoop cluster is automatically created for you just-in-time to process the slice.</span></span>  
2. <span data-ttu-id="7f61f-127">Dane wejściowe są przetwarzane przez uruchomienie skryptu HiveQL w klastrze.</span><span class="sxs-lookup"><span data-stu-id="7f61f-127">The input data is processed by running a HiveQL script on the cluster.</span></span>
3. <span data-ttu-id="7f61f-128">Klaster usługi HDInsight Hadoop jest usuwany po zakończeniu przetwarzania i klastra jest w stanie bezczynności skonfigurowanych ilość czasu (ustawienie timeToLive).</span><span class="sxs-lookup"><span data-stu-id="7f61f-128">The HDInsight Hadoop cluster is deleted after the processing is complete and the cluster is idle for the configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="7f61f-129">Jeśli dalej wycinek danych jest dostępne do przetwarzania z tego czasu bezczynności timeToLive, tego samego klastra służy do przetwarzania wycinka.</span><span class="sxs-lookup"><span data-stu-id="7f61f-129">If the next data slice is available for processing with in this timeToLive idle time, the same cluster is used to process the slice.</span></span>  

<span data-ttu-id="7f61f-130">W tym samouczku skrypt HiveQL skojarzone z działaniem hive wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7f61f-130">In this tutorial, the HiveQL script associated with the hive activity performs the following actions:</span></span>

1. <span data-ttu-id="7f61f-131">Tworzy tabelę zewnętrzną, który odwołuje się do danych dziennika raw sieci web przechowywany w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61f-131">Creates an external table that references the raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="7f61f-132">Partycje nieprzetworzone dane przez rok i miesiąc.</span><span class="sxs-lookup"><span data-stu-id="7f61f-132">Partitions the raw data by year and month.</span></span>
3. <span data-ttu-id="7f61f-133">Przechowuje dane podzielone na partycje w magazynie obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61f-133">Stores the partitioned data in the Azure blob storage.</span></span>

<span data-ttu-id="7f61f-134">W tym samouczku skrypt HiveQL skojarzone z działaniem hive tworzy tabelę zewnętrzną, który odwołuje się do danych dziennika raw sieci web przechowywany w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61f-134">In this tutorial, the HiveQL script associated with the hive activity creates an external table that references the raw web log data stored in the Azure Blob Storage.</span></span> <span data-ttu-id="7f61f-135">Poniżej przedstawiono przykładowe wiersze dla każdego miesiąca w pliku wejściowym.</span><span class="sxs-lookup"><span data-stu-id="7f61f-135">Here are the sample rows for each month in the input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="7f61f-136">Skrypt HiveQL partycje nieprzetworzone dane przez rok i miesiąc.</span><span class="sxs-lookup"><span data-stu-id="7f61f-136">The HiveQL script partitions the raw data by year and month.</span></span> <span data-ttu-id="7f61f-137">Tworzy trzech plików oparte na poprzednie dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="7f61f-137">It creates three output folders based on the previous input.</span></span> <span data-ttu-id="7f61f-138">Każdy folder zawiera plik z wpisów z każdego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="7f61f-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="7f61f-139">Aby uzyskać listę działań przekształcania danych fabryki danych oprócz działania Hive, zobacz [transformacji i analizy przy użyciu fabryki danych Azure](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7f61f-139">For a list of Data Factory data transformation activities in addition to Hive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7f61f-140">Obecnie można tworzyć tylko klastra usługi HDInsight w wersji 3.2 z fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61f-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f61f-141">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7f61f-141">Prerequisites</span></span>
<span data-ttu-id="7f61f-142">Przed rozpoczęciem instrukcje w tym artykule, musi mieć następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7f61f-142">Before you begin the instructions in this article, you must have the following items:</span></span>

* <span data-ttu-id="7f61f-143">[Subskrypcja platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7f61f-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7f61f-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f61f-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="7f61f-145">Przygotowanie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="7f61f-145">Prepare storage account</span></span>
<span data-ttu-id="7f61f-146">W tym scenariuszu można użyć do trzech kont magazynu:</span><span class="sxs-lookup"><span data-stu-id="7f61f-146">You can use up to three storage accounts in this scenario:</span></span>

- <span data-ttu-id="7f61f-147">domyślne konto magazynu dla klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f61f-147">default storage account for the HDInsight cluster</span></span>
- <span data-ttu-id="7f61f-148">Konto magazynu dla danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="7f61f-148">storage account for the input data</span></span>
- <span data-ttu-id="7f61f-149">Konto magazynu dla danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="7f61f-149">storage account for the output data</span></span>

<span data-ttu-id="7f61f-150">Aby uprościć samouczek, służy do służą do celów trzy jedno konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f61f-150">To simplify the tutorial, you use one storage account to serve the three purposes.</span></span> <span data-ttu-id="7f61f-151">Przykładowy skrypt programu PowerShell systemu Azure w tej sekcji wykonuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="7f61f-151">The Azure PowerShell sample script found in this section performs the following tasks:</span></span>

1. <span data-ttu-id="7f61f-152">Logowanie do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61f-152">Log in to Azure.</span></span>
2. <span data-ttu-id="7f61f-153">Utwórz grupę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61f-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="7f61f-154">Tworzenie konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7f61f-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="7f61f-155">Tworzenie kontenera obiektów Blob na koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="7f61f-155">Create a Blob container in the storage account</span></span>
5. <span data-ttu-id="7f61f-156">Skopiuj następujące dwa pliki do kontenera obiektów Blob:</span><span class="sxs-lookup"><span data-stu-id="7f61f-156">Copy the following two files to the Blob container:</span></span>

   * <span data-ttu-id="7f61f-157">Plik danych wejściowych: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="7f61f-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="7f61f-158">Skrypt HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="7f61f-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="7f61f-159">Oba pliki są przechowywane w publicznego kontenera obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="7f61f-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="7f61f-160">**Aby przygotować magazyn i skopiować pliki przy użyciu programu Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="7f61f-160">**To prepare the storage and copy the files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7f61f-161">Określ nazwy grupy zasobów platformy Azure i konto magazynu Azure, który zostanie utworzony przez skrypt.</span><span class="sxs-lookup"><span data-stu-id="7f61f-161">Specify names for the Azure resource group and the Azure storage account that will be created by the script.</span></span>
> <span data-ttu-id="7f61f-162">Zapisz **Nazwa grupy zasobów**, **nazwy konta magazynu**, i **klucz konta magazynu** wyjściowych przez skrypt.</span><span class="sxs-lookup"><span data-stu-id="7f61f-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by the script.</span></span> <span data-ttu-id="7f61f-163">Należy je w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="7f61f-163">You need them in the next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect to Azure
####################################
#region - Connect to Azure subscription
Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

Write-host "`nYou will use the following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="7f61f-164">Jeśli potrzebujesz pomocy przy użyciu skryptu programu PowerShell, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Storage](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="7f61f-164">If you need help with the PowerShell script, see [Using the Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="7f61f-165">Jeśli chcesz użyć wiersza polecenia platformy Azure, zobacz [dodatku](#appendix) sekcji skryptu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61f-165">If you like to use Azure CLI instead, see the [Appendix](#appendix) section for the Azure CLI script.</span></span>

<span data-ttu-id="7f61f-166">**Aby sprawdzić konto magazynu i zawartość**</span><span class="sxs-lookup"><span data-stu-id="7f61f-166">**To examine the storage account and the contents**</span></span>

1. <span data-ttu-id="7f61f-167">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f61f-167">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7f61f-168">Kliknij przycisk **grup zasobów** w lewym okienku.</span><span class="sxs-lookup"><span data-stu-id="7f61f-168">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="7f61f-169">Kliknij dwukrotnie nazwę grupy zasobów utworzonej za pomocą skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f61f-169">Double-click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="7f61f-170">Jeśli masz zbyt wiele grup zasobów na liście, użyj filtru.</span><span class="sxs-lookup"><span data-stu-id="7f61f-170">Use the filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="7f61f-171">Na **zasobów** kafelka, powinna mieć jeden zasób z listy, chyba że współużytkować grupy zasobów z innymi projektami.</span><span class="sxs-lookup"><span data-stu-id="7f61f-171">On the **Resources** tile, you shall have one resource listed unless you share the resource group with other projects.</span></span> <span data-ttu-id="7f61f-172">Ten zasób jest konto magazynu o nazwie określone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7f61f-172">That resource is the storage account with the name you specified earlier.</span></span> <span data-ttu-id="7f61f-173">Kliknij nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f61f-173">Click the storage account name.</span></span>
5. <span data-ttu-id="7f61f-174">Kliknij przycisk **obiekty BLOB** Kafelki.</span><span class="sxs-lookup"><span data-stu-id="7f61f-174">Click the **Blobs** tiles.</span></span>
6. <span data-ttu-id="7f61f-175">Kliknij przycisk **adfgetstarted** kontenera.</span><span class="sxs-lookup"><span data-stu-id="7f61f-175">Click the **adfgetstarted** container.</span></span> <span data-ttu-id="7f61f-176">Zobacz dwa foldery: **inputdata** i **skryptu**.</span><span class="sxs-lookup"><span data-stu-id="7f61f-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="7f61f-177">Otwórz folder, a następnie sprawdź pliki w folderach.</span><span class="sxs-lookup"><span data-stu-id="7f61f-177">Open the folder and check the files in the folders.</span></span> <span data-ttu-id="7f61f-178">Inputdata zawiera plik input.log z danych wejściowych i folder skryptu zawiera plik skrypt HiveQL.</span><span class="sxs-lookup"><span data-stu-id="7f61f-178">The inputdata contains the input.log file with input data and the script folder contains the HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="7f61f-179">Tworzenie fabryki danych przy użyciu szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7f61f-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="7f61f-180">Konto magazynu, dane wejściowe i skrypt HiveQL przygotowany można przystąpić do utworzenia fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61f-180">With the storage account, the input data, and the HiveQL script prepared, you are ready to create an Azure data factory.</span></span> <span data-ttu-id="7f61f-181">Istnieje kilka metod tworzenia fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="7f61f-182">Przez wdrożenie szablonu usługi Azure Resource Manager przy użyciu portalu Azure, w tym samouczku tworzenie fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using the Azure portal.</span></span> <span data-ttu-id="7f61f-183">Można także wdrożyć przy użyciu szablonu usługi Resource Manager [interfejsu wiersza polecenia Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) i [programu Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="7f61f-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="7f61f-184">Dla innych metod tworzenia fabryki danych, zobacz [samouczek: Tworzenie pierwszego fabrykę danych](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="7f61f-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="7f61f-185">Kliknij poniższy obraz, aby zalogować się do platformy Azure i otworzyć szablon usługi Resource Manager w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7f61f-185">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="7f61f-186">Szablon znajduje się w https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="7f61f-186">The template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="7f61f-187">Zobacz [jednostek fabryki danych w szablonie](#data-factory-entities-in-the-template) sekcji, aby uzyskać szczegółowe informacje na temat jednostek zdefiniowanych w szablonie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-187">See the [Data Factory entities in the template](#data-factory-entities-in-the-template) section for detailed information about entities defined in the template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="7f61f-188">Wybierz **Użyj istniejącego** opcja dla **grupy zasobów** ustawienie i wybierz nazwę grupy zasobów utworzonej w poprzednim kroku (przy użyciu skryptu programu PowerShell).</span><span class="sxs-lookup"><span data-stu-id="7f61f-188">Select **Use existing** option for the **Resource group** setting, and select the name of the resource group you created in the previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="7f61f-189">Wprowadź nazwę dla fabryki danych (**nazwa fabryki danych**).</span><span class="sxs-lookup"><span data-stu-id="7f61f-189">Enter a name for the data factory (**Data Factory Name**).</span></span> <span data-ttu-id="7f61f-190">Ta nazwa musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="7f61f-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="7f61f-191">Wprowadź **nazwy konta magazynu** i **klucz konta magazynu** zapisanej w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="7f61f-191">Enter the **storage account name** and **storage account key** you wrote down in the previous step.</span></span>
5. <span data-ttu-id="7f61f-192">Wybierz **akceptuję warunki i postanowienia** powyższych po odczytaniu za pośrednictwem **warunków i postanowień**.</span><span class="sxs-lookup"><span data-stu-id="7f61f-192">Select **I agree to the terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="7f61f-193">Wybierz **Przypnij do pulpitu nawigacyjnego** opcji.</span><span class="sxs-lookup"><span data-stu-id="7f61f-193">Select **Pin to dashboard** option.</span></span>
6. <span data-ttu-id="7f61f-194">Kliknij przycisk **zakupu/utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="7f61f-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="7f61f-195">Zostanie wyświetlony na pulpicie nawigacyjnym kafelka o nazwie **wdrażanie szablonu wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="7f61f-195">You see a tile on the Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="7f61f-196">Poczekaj na **grupy zasobów** zostanie otwarty blok grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f61f-196">Wait until the **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="7f61f-197">Możesz również kliknąć Kafelek zatytułowany jako nazwę grupy zasobów można otworzyć bloku grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f61f-197">You can also click the tile titled as your resource group name to open the resource group blade.</span></span>
6. <span data-ttu-id="7f61f-198">Kliknij Kafelek, aby otworzyć grupę zasobów, jeśli bloku grupy zasobów nie jest już otwarty.</span><span class="sxs-lookup"><span data-stu-id="7f61f-198">Click the tile to open the resource group if the resource group blade is not already open.</span></span> <span data-ttu-id="7f61f-199">Teraz zostanie wyświetlona jeden zasób fabryki więcej danych na liście oprócz zasobów konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f61f-199">Now you shall see one more data factory resource listed in addition to the storage account resource.</span></span>
7. <span data-ttu-id="7f61f-200">Kliknij nazwę fabrykę danych (wartość podana dla **nazwa fabryki danych** parametru).</span><span class="sxs-lookup"><span data-stu-id="7f61f-200">Click the name of your data factory (value you specified for the **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="7f61f-201">W bloku fabryki danych, kliknij przycisk **Diagram** kafelka.</span><span class="sxs-lookup"><span data-stu-id="7f61f-201">In the Data Factory blade, click the **Diagram** tile.</span></span> <span data-ttu-id="7f61f-202">Na diagramie przedstawiono jedno działanie z zestawem danych wejściowych i wyjściowy zestaw danych:</span><span class="sxs-lookup"><span data-stu-id="7f61f-202">The diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Azure diagram potoku działania Hive HDInsight fabryki danych na żądanie](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="7f61f-204">Nazwy są definiowane w szablonie usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7f61f-204">The names are defined in the Resource Manager template.</span></span>
9. <span data-ttu-id="7f61f-205">Kliknij dwukrotnie **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="7f61f-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="7f61f-206">Na **ostatnie zaktualizowane wycinków**, powinien zostać wyświetlony jeden wycinek typu.</span><span class="sxs-lookup"><span data-stu-id="7f61f-206">On the **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="7f61f-207">Jeśli stan jest **w toku**, poczekaj, aż zostanie zmieniona na **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="7f61f-207">If the status is **In progress**, wait until it is changed to **Ready**.</span></span> <span data-ttu-id="7f61f-208">Zwykle trwa około **20 minut** do tworzenia klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7f61f-208">It usually takes about **20 minutes** to create an HDInsight cluster.</span></span>

### <a name="check-the-data-factory-output"></a><span data-ttu-id="7f61f-209">Sprawdź dane wyjściowe z fabryki danych</span><span class="sxs-lookup"><span data-stu-id="7f61f-209">Check the data factory output</span></span>

1. <span data-ttu-id="7f61f-210">Użyj tej samej procedury podczas ostatniej sesji, aby sprawdzić kontenery adfgetstarted kontenera.</span><span class="sxs-lookup"><span data-stu-id="7f61f-210">Use the same procedure in the last session to check the containers of the adfgetstarted container.</span></span> <span data-ttu-id="7f61f-211">Istnieją dwa nowe kontenery oprócz **adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="7f61f-211">There are two new containers in addition to **adfgetsarted**:</span></span>

   * <span data-ttu-id="7f61f-212">Kontener o nazwie, który jest zgodny ze wzorcem: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="7f61f-212">A container with name that follows the pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="7f61f-213">Ten kontener jest domyślnym kontenerem dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7f61f-213">This container is the default container for the HDInsight cluster.</span></span>
   * <span data-ttu-id="7f61f-214">adfjobs: ten kontener jest kontenerem dla dzienników zadania ADF.</span><span class="sxs-lookup"><span data-stu-id="7f61f-214">adfjobs: This container is the container for the ADF job logs.</span></span>

     <span data-ttu-id="7f61f-215">Fabryka danych wyjściowych jest przechowywany w **afgetstarted** zgodnie z konfiguracją w szablonie usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7f61f-215">The data factory output is stored in **afgetstarted** as you configured in the Resource Manager template.</span></span>
2. <span data-ttu-id="7f61f-216">Kliknij przycisk **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="7f61f-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="7f61f-217">Kliknij dwukrotnie **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="7f61f-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="7f61f-218">Zostanie wyświetlony **roku = 2014** folderu, ponieważ wszystkie dzienniki sieci web są dniu 2014 roku.</span><span class="sxs-lookup"><span data-stu-id="7f61f-218">You see a **year=2014** folder because all the web logs are dated in year 2014.</span></span>

    ![Azure HDInsight fabryki danych na żądanie Hive potoku dane wyjściowe działania](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="7f61f-220">Jeśli możesz przejść do szczegółów listy, zostanie wyświetlona trzy foldery stycznia, lutego i marca.</span><span class="sxs-lookup"><span data-stu-id="7f61f-220">If you drill down the list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="7f61f-221">I ma dziennika dla każdego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="7f61f-221">And there is a log for each month.</span></span>

    ![Azure HDInsight fabryki danych na żądanie Hive potoku dane wyjściowe działania](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="7f61f-223">Jednostki usługi Data Factory w szablonie</span><span class="sxs-lookup"><span data-stu-id="7f61f-223">Data Factory entities in the template</span></span>
<span data-ttu-id="7f61f-224">Oto, jak szablon Menedżera zasobów najwyższego poziomu dla fabryki danych wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="7f61f-224">Here is how the top-level Resource Manager template for a data factory looks like:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="7f61f-225">Definiowanie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="7f61f-225">Define data factory</span></span>
<span data-ttu-id="7f61f-226">Fabrykę danych definiuje się w szablonie usługi Resource Manager jak pokazano w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="7f61f-226">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="7f61f-227">DataFactoryName to nazwa fabryki danych, które można określić podczas wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="7f61f-227">The dataFactoryName is the name of the data factory you specify when you deploy the template.</span></span> <span data-ttu-id="7f61f-228">Fabryka danych jest obecnie obsługiwane tylko w regionach wschodnie stany USA, zachodnie stany USA i Europa Północna, Europa.</span><span class="sxs-lookup"><span data-stu-id="7f61f-228">Data factory is currently only supported in the East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-the-data-factory"></a><span data-ttu-id="7f61f-229">Definiowanie jednostek w fabryce danych</span><span class="sxs-lookup"><span data-stu-id="7f61f-229">Defining entities within the data factory</span></span>
<span data-ttu-id="7f61f-230">Następujące jednostki usługi Data Factory są zdefiniowane w szablonie JSON:</span><span class="sxs-lookup"><span data-stu-id="7f61f-230">The following Data Factory entities are defined in the JSON template:</span></span>

* [<span data-ttu-id="7f61f-231">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7f61f-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="7f61f-232">Połączona usługa HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="7f61f-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="7f61f-233">Wejściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7f61f-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="7f61f-234">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7f61f-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="7f61f-235">Potok danych z działaniem kopiowania</span><span class="sxs-lookup"><span data-stu-id="7f61f-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="7f61f-236">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7f61f-236">Azure Storage linked service</span></span>
<span data-ttu-id="7f61f-237">Połączona usługa Azure Storage łączy konto magazynu Azure z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-237">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="7f61f-238">W tym samouczku tego samego konta magazynu jest używany jako domyślne konto magazynu usługi HDInsight, Magazyn danych wejściowych i przechowywania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-238">In this tutorial, the same storage account is used as the default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="7f61f-239">W związku z tym można zdefiniować tylko jednego magazynu Azure połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="7f61f-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="7f61f-240">W definicji połączonej usługi Określ nazwę i klucza konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61f-240">In the linked service definition, you specify the name and key of your Azure storage account.</span></span> <span data-ttu-id="7f61f-241">Szczegóły dotyczące właściwości JSON używanych do definiowania połączonej usługi Azure Storage zawiera temat [Połączona usługa Azure Storage](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="7f61f-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>

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
<span data-ttu-id="7f61f-242">Parametr **connectionString** używa parametrów storageAccountName i storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="7f61f-242">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="7f61f-243">Możesz określić wartości dla parametrów podczas wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="7f61f-243">You specify values for these parameters while deploying the template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="7f61f-244">Połączona usługa HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="7f61f-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="7f61f-245">W definicji usługi HDInsight połączony na żądanie można określić wartości parametrów konfiguracyjnych, które są używane przez usługi fabryka danych do tworzenia klastra usługi HDInsight Hadoop w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="7f61f-245">In the on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by the Data Factory service to create a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="7f61f-246">Szczegółowe informacje o właściwościach JSON używanych do definiowania połączonej usługi HDInsight na żądanie zawiera temat [Usługi połączone usługi Compute](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="7f61f-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="7f61f-247">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="7f61f-247">Note the following points:</span></span>

* <span data-ttu-id="7f61f-248">Tworzy fabrykę danych **opartych na systemie Linux** klastra usługi HDInsight dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-248">The Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="7f61f-249">Klaster usługi HDInsight Hadoop jest tworzony w tym samym regionie co konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f61f-249">The HDInsight Hadoop cluster is created in the same region as the storage account.</span></span>
* <span data-ttu-id="7f61f-250">Powiadomienie *timeToLive* ustawienie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-250">Notice the *timeToLive* setting.</span></span> <span data-ttu-id="7f61f-251">Fabryka danych automatycznie usuwa klastra, po bezczynności klastra przez 30 minut.</span><span class="sxs-lookup"><span data-stu-id="7f61f-251">The data factory deletes the cluster automatically after the cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="7f61f-252">Klaster usługi HDInsight tworzy **kontener domyślny** w magazynie obiektów blob określonym w kodzie JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="7f61f-252">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="7f61f-253">Usługa HDInsight nie powoduje usunięcia tego kontenera w przypadku usunięcia klastra.</span><span class="sxs-lookup"><span data-stu-id="7f61f-253">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="7f61f-254">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="7f61f-254">This behavior is by design.</span></span> <span data-ttu-id="7f61f-255">W przypadku połączonej usługi HDInsight na żądanie klaster usługi HDInsight jest tworzony za każdym razem, gdy trzeba przetworzyć wycinek — o ile w tym momencie nie istnieje aktywny klaster (**timeToLive**) — i zostaje usunięty po zakończeniu przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="7f61f-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

<span data-ttu-id="7f61f-256">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="7f61f-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f61f-257">Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="7f61f-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="7f61f-258">Jeśli nie są potrzebne do rozwiązywania problemów z zadaniami, można je usunąć, aby zmniejszyć koszt przechowywania.</span><span class="sxs-lookup"><span data-stu-id="7f61f-258">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="7f61f-259">Nazwy tych kontenerów są zgodne ze wzorcem: „adf**twojanazwafabrykidanych**-**nazwapołączonejusługi**-znacznikdatygodziny”.</span><span class="sxs-lookup"><span data-stu-id="7f61f-259">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="7f61f-260">Aby usunąć kontenery z usługi Azure Blob Storage, użyj takich narzędzi, jak [Microsoft Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="7f61f-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="7f61f-261">Wejściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7f61f-261">Azure blob input dataset</span></span>
<span data-ttu-id="7f61f-262">W definicji zestawu danych wejściowych należy określić nazwy kontenera obiektów blob, folderu i pliku zawierającego dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="7f61f-262">In the input dataset definition, you specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="7f61f-263">Szczegóły dotyczące właściwości JSON używanych do definiowania zestawu danych obiektów blob platformy Azure zawiera temat [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) (Właściwości zestawu danych obiektów blob plaformy Azure).</span><span class="sxs-lookup"><span data-stu-id="7f61f-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>

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

<span data-ttu-id="7f61f-264">Zwróć uwagę poniższe ustawienia określone w definicji JSON:</span><span class="sxs-lookup"><span data-stu-id="7f61f-264">Notice the following specific settings in the JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="7f61f-265">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7f61f-265">Azure Blob output dataset</span></span>
<span data-ttu-id="7f61f-266">W definicji zestawu danych wyjściowych należy określić nazwy kontenera obiektów blob i folder, który przechowuje danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-266">In the output dataset definition, you specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="7f61f-267">Szczegóły dotyczące właściwości JSON używanych do definiowania zestawu danych obiektów blob platformy Azure zawiera temat [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) (Właściwości zestawu danych obiektów blob plaformy Azure).</span><span class="sxs-lookup"><span data-stu-id="7f61f-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="7f61f-268">FolderPath Określa ścieżkę do folderu, który przechowuje danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="7f61f-268">The folderPath specifies the path to the folder that holds the output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="7f61f-269">[Dostępności zestawu danych](../data-factory/data-factory-create-datasets.md#dataset-availability) ustawienie wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="7f61f-269">The [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="7f61f-270">W fabryce danych Azure dostępności zestawu danych wyjściowych dysków potoku.</span><span class="sxs-lookup"><span data-stu-id="7f61f-270">In Azure Data Factory, output dataset availability drives the pipeline.</span></span> <span data-ttu-id="7f61f-271">W tym przykładzie wycinek jest tworzony co miesiąc ostatniego dnia miesiąca (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="7f61f-271">In this example, the slice is produced monthly on the last day of month (EndOfInterval).</span></span> <span data-ttu-id="7f61f-272">Aby uzyskać więcej informacji, zobacz [planowania fabryki danych i wykonywania](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="7f61f-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="7f61f-273">Potok danych</span><span class="sxs-lookup"><span data-stu-id="7f61f-273">Data pipeline</span></span>
<span data-ttu-id="7f61f-274">Należy zdefiniować potok, który przekształca danych przez uruchomienie skryptu Hive w klastrze usługi Azure HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="7f61f-275">Opisy elementów JSON używanych do definiowania potoku w tym przykładzie zawiera temat [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) (Kod JSON potoku).</span><span class="sxs-lookup"><span data-stu-id="7f61f-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span>

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

<span data-ttu-id="7f61f-276">Potok zawiera jedno działanie, HDInsightHive działania.</span><span class="sxs-lookup"><span data-stu-id="7f61f-276">The pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="7f61f-277">Jak zarówno rozpoczęcia i zakończenia daty są styczeń 2016 r., dane tylko jeden miesiąc (wycinek) jest przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="7f61f-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="7f61f-278">Zarówno *start* i *zakończenia* działania mają datę przeszłą, więc fabryki danych przetwarza dane bezpośrednio w miesiącu.</span><span class="sxs-lookup"><span data-stu-id="7f61f-278">Both *start* and *end* of the activity have a past date, so the Data Factory processes data for the month immediately.</span></span> <span data-ttu-id="7f61f-279">Jeśli punkt końcowy jest datą przyszłą, fabryki danych tworzy wycinek innym czasie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-279">If the end is a future date, the data factory creates another slice when the time comes.</span></span> <span data-ttu-id="7f61f-280">Aby uzyskać więcej informacji, zobacz [planowania fabryki danych i wykonywania](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="7f61f-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-the-tutorial"></a><span data-ttu-id="7f61f-281">Czyszczenie na koniec samouczka</span><span class="sxs-lookup"><span data-stu-id="7f61f-281">Clean up the tutorial</span></span>

### <a name="delete-the-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="7f61f-282">Usuń kontenerów obiektów blob utworzoną przez klaster usługi HDInsight na żądanie</span><span class="sxs-lookup"><span data-stu-id="7f61f-282">Delete the blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="7f61f-283">Z usługą HDInsight połączony na żądanie klaster usługi HDInsight jest tworzony za każdym razem, gdy wycinek ma zostać przetworzony, chyba że istnieje istniejącego klastra na żywo (timeToLive); i klastra jest usuwany po zakończeniu przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="7f61f-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (timeToLive); and the cluster is deleted when the processing is done.</span></span> <span data-ttu-id="7f61f-284">Dla każdego klastra fabryki danych Azure tworzy kontener obiektów blob w magazynie obiektów blob platformy Azure, używane jako konto domyślne stroage dla klastra.</span><span class="sxs-lookup"><span data-stu-id="7f61f-284">For each cluster, Azure Data Factory creates a blob container in the Azure blob storage used as the default stroage account for the cluster.</span></span> <span data-ttu-id="7f61f-285">Nawet po usunięciu klastra usługi HDInsight domyślnego kontenera magazynu obiektów blob i skojarzonego konta magazynu nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="7f61f-285">Even though HDInsight cluster is deleted, the default blob storage container and the associated storage account are not deleted.</span></span> <span data-ttu-id="7f61f-286">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="7f61f-286">This behavior is by design.</span></span> <span data-ttu-id="7f61f-287">Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="7f61f-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="7f61f-288">Jeśli nie są potrzebne do rozwiązywania problemów z zadaniami, można je usunąć, aby zmniejszyć koszt przechowywania.</span><span class="sxs-lookup"><span data-stu-id="7f61f-288">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="7f61f-289">Nazwy tych kontenerów są zgodne z następującym wzorcem: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="7f61f-289">The names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="7f61f-290">Usuń **adfjobs** i **adfyourdatafactoryname-linkedservicename-datetimestamp** folderów.</span><span class="sxs-lookup"><span data-stu-id="7f61f-290">Delete the **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="7f61f-291">Kontener adfjobs zawiera z fabryki danych Azure z dziennikami zadań.</span><span class="sxs-lookup"><span data-stu-id="7f61f-291">The adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-the-resource-group"></a><span data-ttu-id="7f61f-292">Usuń grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="7f61f-292">Delete the resource group</span></span>
<span data-ttu-id="7f61f-293">[Usługa Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) służy do wdrażania, zarządzania i monitorowania rozwiązanie w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="7f61f-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used to deploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="7f61f-294">Usunięcie grupy zasobów powoduje usunięcie wszystkich składników w grupie.</span><span class="sxs-lookup"><span data-stu-id="7f61f-294">Deleting a resource group deletes all the components inside the group.</span></span>  

1. <span data-ttu-id="7f61f-295">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f61f-295">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7f61f-296">Kliknij przycisk **grup zasobów** w lewym okienku.</span><span class="sxs-lookup"><span data-stu-id="7f61f-296">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="7f61f-297">Kliknij nazwę grupy zasobów utworzonej za pomocą skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f61f-297">Click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="7f61f-298">Jeśli masz zbyt wiele grup zasobów na liście, użyj filtru.</span><span class="sxs-lookup"><span data-stu-id="7f61f-298">Use the filter if you have too many resource groups listed.</span></span> <span data-ttu-id="7f61f-299">Nazwa grupy zasobów zostanie otwarty w nowym bloku.</span><span class="sxs-lookup"><span data-stu-id="7f61f-299">It opens the resource group in a new blade.</span></span>
4. <span data-ttu-id="7f61f-300">Na **zasobów** kafelka, użytkownik ma domyślne konto magazynu i fabryki danych, chyba że współużytkować grupy zasobów z innymi projektami na liście.</span><span class="sxs-lookup"><span data-stu-id="7f61f-300">On the **Resources** tile, you shall have the default storage account and the data factory listed unless you share the resource group with other projects.</span></span>
5. <span data-ttu-id="7f61f-301">Kliknij przycisk **usunąć** górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="7f61f-301">Click **Delete** on the top of the blade.</span></span> <span data-ttu-id="7f61f-302">To spowoduje usunięcie konta magazynu i dane przechowywane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f61f-302">Doing so deletes the storage account and the data stored in the storage account.</span></span>
6. <span data-ttu-id="7f61f-303">Wprowadź nazwę grupy zasobów, aby potwierdzić usunięcie, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="7f61f-303">Enter the resource group name to confirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="7f61f-304">W przypadku, gdy nie chcesz usunąć konto magazynu podczas usuwania grupy zasobów, należy wziąć pod uwagę następujące architektury, oddzielając danych biznesowych z domyślnego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7f61f-304">In case you don't want to delete the storage account when you delete the resource group, consider the following architecture by separating the business data from the default storage account.</span></span> <span data-ttu-id="7f61f-305">W takim przypadku jedna grupa zasobów dla konta magazynu danych biznesowych, i inne grupy zasobów dla domyślnego konta magazynu dla usługi HDInsight połączone usługi i fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-305">In this case, you have one resource group for the storage account with the business data, and the other resource group for the default storage account for HDInsight linked service and the data factory.</span></span> <span data-ttu-id="7f61f-306">Po usunięciu drugiej grupy zasobów nie ma wpływu na koncie magazynu danych biznesowych.</span><span class="sxs-lookup"><span data-stu-id="7f61f-306">When you delete the second resource group, it does not impact the business data storage account.</span></span> <span data-ttu-id="7f61f-307">W tym celu:</span><span class="sxs-lookup"><span data-stu-id="7f61f-307">To do so:</span></span>

* <span data-ttu-id="7f61f-308">Dodaj następujący element do grupy zasobów najwyższego poziomu, wraz z zasobów Microsoft.DataFactory/datafactories w szablonie usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7f61f-308">Add the following to the top-level resource group along with the Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="7f61f-309">Tworzy konto magazynu:</span><span class="sxs-lookup"><span data-stu-id="7f61f-309">It creates a storage account:</span></span>

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
* <span data-ttu-id="7f61f-310">Dodaj nowy punkt połączonej usługi do nowego konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="7f61f-310">Add a new linked service point to the new storage account:</span></span>

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
* <span data-ttu-id="7f61f-311">Skonfiguruj usługą usługi HDInsight na żądanie, połączony z dodatkowych dependsOn i additionalLinkedServiceNames:</span><span class="sxs-lookup"><span data-stu-id="7f61f-311">Configure the HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="7f61f-312">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f61f-312">Next steps</span></span>
<span data-ttu-id="7f61f-313">W tym artykule ma przedstawiono sposób tworzenia klastra usługi HDInsight na żądanie do przetworzenia zadań Hive za pomocą fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61f-313">In this article, you have learned how to use Azure Data Factory to create on-demand HDInsight cluster to process Hive jobs.</span></span> <span data-ttu-id="7f61f-314">Aby dowiedzieć się więcej:</span><span class="sxs-lookup"><span data-stu-id="7f61f-314">To read more:</span></span>

* [<span data-ttu-id="7f61f-315">Samouczek Hadoop: rozpoczynanie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f61f-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="7f61f-316">Tworzenie klastrów opartych na systemie Linux platformą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f61f-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="7f61f-317">Dokumentacja dotycząca usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="7f61f-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="7f61f-318">Dokumentacja fabryki danych</span><span class="sxs-lookup"><span data-stu-id="7f61f-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="7f61f-319">Dodatek</span><span class="sxs-lookup"><span data-stu-id="7f61f-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="7f61f-320">Skryptu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7f61f-320">Azure CLI script</span></span>
<span data-ttu-id="7f61f-321">Zamiast tego samouczka należy za pomocą programu Azure PowerShell można użyć wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f61f-321">You can use Azure CLI instead of using Azure PowerShell to do the tutorial.</span></span> <span data-ttu-id="7f61f-322">Aby użyć wiersza polecenia platformy Azure, należy najpierw zainstalować wiersza polecenia platformy Azure, zgodnie z poniższych instrukcji:</span><span class="sxs-lookup"><span data-stu-id="7f61f-322">To use Azure CLI, first install Azure CLI as per the following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-to-prepare-the-storage-and-copy-the-files"></a><span data-ttu-id="7f61f-323">Przygotuj magazyn i skopiować pliki za pomocą wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7f61f-323">Use Azure CLI to prepare the storage and copy the files</span></span>

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

<span data-ttu-id="7f61f-324">Nazwa kontenera jest *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="7f61f-324">The container name is *adfgetstarted*.</span></span> <span data-ttu-id="7f61f-325">Zachować, ponieważ jest on.</span><span class="sxs-lookup"><span data-stu-id="7f61f-325">Keep it as it is.</span></span> <span data-ttu-id="7f61f-326">W przeciwnym razie należy zaktualizować szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7f61f-326">Otherwise you need to update the Resource Manager template.</span></span> <span data-ttu-id="7f61f-327">Aby uzyskać pomoc dotyczącą tego skryptu interfejsu wiersza polecenia, zobacz [przy użyciu wiersza polecenia platformy Azure z usługą Azure Storage](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7f61f-327">If you need help with this CLI script, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
