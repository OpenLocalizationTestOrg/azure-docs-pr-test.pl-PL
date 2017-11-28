---
title: "aaaAnalyze transmitowane opóźnienie danych z platformą Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse jednego środowiska Windows PowerShell skryptu toocreate klastra usługi HDInsight, uruchom zadania Hive, uruchom zadanie Sqoop, a następnie usuń hello klastra."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="47cbe-103">Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="47cbe-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="47cbe-104">Gałąź umożliwia uruchomionych zadań MapReduce z Hadoop za pomocą skryptów języka przypominającego SQL o nazwie  *[HiveQL][hadoop-hiveql]*, które można zastosować do podsumowania, wyszukiwanie i analizowania dużych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="47cbe-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47cbe-105">Witaj czynności w tym dokumencie wymagają klastra usługi HDInsight opartej na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="47cbe-105">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="47cbe-106">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="47cbe-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="47cbe-107">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="47cbe-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="47cbe-108">Opis czynności, które pracy z opartą na systemie Linux klastrem, zobacz [analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="47cbe-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="47cbe-109">Jedną z najważniejszych zalet hello Azure HDInsight jest oddzielenie hello magazynu danych i zasobów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="47cbe-109">One of hello major benefits of Azure HDInsight is hello separation of data storage and compute.</span></span> <span data-ttu-id="47cbe-110">HDInsight używa magazynu obiektów Blob platformy Azure do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="47cbe-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="47cbe-111">Typowe zadania obejmuje trzy części:</span><span class="sxs-lookup"><span data-stu-id="47cbe-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="47cbe-112">**Przechowywanie danych w magazynie obiektów Blob Azure.**</span><span class="sxs-lookup"><span data-stu-id="47cbe-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="47cbe-113">Na przykład pogodowe danych czujnika, danych, dzienników sieci web, a w tym przypadku transmitowane opóźnienie danych są zapisywane w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="47cbe-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="47cbe-114">**Uruchamianie zadań.**</span><span class="sxs-lookup"><span data-stu-id="47cbe-114">**Run jobs.**</span></span> <span data-ttu-id="47cbe-115">Gdy nadejdzie czas tooprocess hello danych, uruchom skrypt programu Windows PowerShell (lub aplikacja kliencka) toocreate klastra usługi HDInsight, uruchamianie zadań, a następnie usuń hello klastra.</span><span class="sxs-lookup"><span data-stu-id="47cbe-115">When it is time tooprocess hello data, you run a Windows PowerShell script (or a client application) toocreate an HDInsight cluster, run jobs, and delete hello cluster.</span></span> <span data-ttu-id="47cbe-116">Witaj zadania zapisywania wyjściowych danych tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="47cbe-116">hello jobs save output data tooAzure Blob storage.</span></span> <span data-ttu-id="47cbe-117">dane wyjściowe Hello jest zachowywana, nawet po usunięciu hello klastra.</span><span class="sxs-lookup"><span data-stu-id="47cbe-117">hello output data is retained even after hello cluster is deleted.</span></span> <span data-ttu-id="47cbe-118">W ten sposób płacisz za tylko co użytkownik ma używane.</span><span class="sxs-lookup"><span data-stu-id="47cbe-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="47cbe-119">**Pobrać dane wyjściowe hello z magazynu obiektów Blob Azure**, lub w tym samouczku eksportu hello danych tooan — bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="47cbe-119">**Retrieve hello output from Azure Blob storage**, or in this tutorial, export hello data tooan Azure SQL database.</span></span>

<span data-ttu-id="47cbe-120">Witaj poniższym diagramie przedstawiono scenariusz hello i struktura hello tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="47cbe-120">hello following diagram illustrates hello scenario and hello structure of this tutorial:</span></span>

![HDI. FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="47cbe-122">Należy pamiętać, że numery hello na diagramie hello odpowiadają toohello tytuły sekcji.</span><span class="sxs-lookup"><span data-stu-id="47cbe-122">Note that hello numbers in hello diagram correspond toohello section titles.</span></span> <span data-ttu-id="47cbe-123">**M** oznacza hello głównego procesu.</span><span class="sxs-lookup"><span data-stu-id="47cbe-123">**M** stands for hello main process.</span></span> <span data-ttu-id="47cbe-124">**A** oznacza zawartość hello hello dodatku.</span><span class="sxs-lookup"><span data-stu-id="47cbe-124">**A** stands for hello content in hello appendix.</span></span>

<span data-ttu-id="47cbe-125">Hello głównych części samouczka hello pokazuje, jak toouse jednego środowiska Windows PowerShell skryptu tooperform hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="47cbe-125">hello main portion of hello tutorial shows you how toouse one Windows PowerShell script tooperform hello following tasks:</span></span>

* <span data-ttu-id="47cbe-126">Tworzenie klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47cbe-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="47cbe-127">Uruchom zadanie Hive hello klastra toocalculate średnie opóźnienia na lotniskach.</span><span class="sxs-lookup"><span data-stu-id="47cbe-127">Run a Hive job on hello cluster toocalculate average delays at airports.</span></span> <span data-ttu-id="47cbe-128">Witaj transmitowane opóźnienie dane są przechowywane na koncie magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47cbe-128">hello flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="47cbe-129">Uruchom Sqoop zadania tooexport hello Hive zadania dane wyjściowe tooan bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="47cbe-129">Run a Sqoop job tooexport hello Hive job output tooan Azure SQL database.</span></span>
* <span data-ttu-id="47cbe-130">Usuń hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47cbe-130">Delete hello HDInsight cluster.</span></span>

<span data-ttu-id="47cbe-131">W dodatkach hello hello instrukcje można znaleźć przekazywanie danych opóźnienie transmitowane, ciąg zapytania Hive tworzenia/przekazywania i przygotowywanie bazy danych Azure SQL hello hello Sqoop zadania.</span><span class="sxs-lookup"><span data-stu-id="47cbe-131">In hello appendixes, you can find hello instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing hello Azure SQL database for hello Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="47cbe-132">kroki Hello w tym dokumencie są określonej na podstawie tooWindows klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47cbe-132">hello steps in this document are specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="47cbe-133">Opis czynności, które pracy z opartą na systemie Linux klastrem, zobacz [analizowanie danych opóźnienie transmitowane przy użyciu Hive w usłudze HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span><span class="sxs-lookup"><span data-stu-id="47cbe-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="47cbe-134">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="47cbe-134">Prerequisites</span></span>
<span data-ttu-id="47cbe-135">Przed rozpoczęciem tego samouczka, musi mieć hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="47cbe-135">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="47cbe-136">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="47cbe-136">**An Azure subscription**.</span></span> <span data-ttu-id="47cbe-137">Zobacz artykuł [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="47cbe-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="47cbe-138">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="47cbe-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="47cbe-139">Obsługa programu Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i została usunięta z dniem 1 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="47cbe-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="47cbe-140">Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="47cbe-140">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="47cbe-141">Wykonaj kroki hello [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello najnowszą wersję programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47cbe-141">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="47cbe-142">Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="47cbe-142">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="47cbe-143">**Pliki używane w tym samouczku**</span><span class="sxs-lookup"><span data-stu-id="47cbe-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="47cbe-144">W tym samouczku używana hello punktualności linii lotniczych dane transmitowane z [badań i innowacyjnych administracyjnej technologii, biura statystyk transportu lub RICIE][rita-website].</span><span class="sxs-lookup"><span data-stu-id="47cbe-144">This tutorial uses hello on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="47cbe-145">Kopię powitalne dane zostały przekazane tooan kontenera magazynu obiektów Blob platformy Azure z uprawnieniem dostępu publicznego obiektu Blob hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-145">A copy of hello data has been uploaded tooan Azure Blob storage container with hello Public Blob access permission.</span></span>
<span data-ttu-id="47cbe-146">Część skrypt programu PowerShell kopiuje dane hello z hello publicznych obiektów blob kontenera toohello domyślnego kontenera obiektów blob klastra.</span><span class="sxs-lookup"><span data-stu-id="47cbe-146">A part of your PowerShell script copies hello data from hello public blob container toohello default blob container of your cluster.</span></span> <span data-ttu-id="47cbe-147">Hello HiveQL skryptu jest również skopiować toohello tego samego kontenera obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="47cbe-147">hello HiveQL script is also copied toohello same Blob container.</span></span>
<span data-ttu-id="47cbe-148">Jeśli chcesz, aby toolearn jak tooget/przekazywania hello danych tooyour właścicielem konta magazynu i jak hello toocreate/przekazywania HiveQL skryptu plików, zobacz [dodatek a.](#appendix-a) i [dodatek B](#appendix-b).</span><span class="sxs-lookup"><span data-stu-id="47cbe-148">If you want toolearn how tooget/upload hello data tooyour own Storage account, and how toocreate/upload hello HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="47cbe-149">Witaj poniższej tabeli wymieniono pliki hello używane w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="47cbe-149">hello following table lists hello files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="47cbe-150">Pliki</span><span class="sxs-lookup"><span data-stu-id="47cbe-150">Files</span></span></th><th><span data-ttu-id="47cbe-151">Opis</span><span class="sxs-lookup"><span data-stu-id="47cbe-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="47cbe-152">plik skryptu HiveQL Hello używany przez hello zadania Hive.</span><span class="sxs-lookup"><span data-stu-id="47cbe-152">hello HiveQL script file used by hello Hive job.</span></span> <span data-ttu-id="47cbe-153">Ten skrypt został przekazany tooan konta magazynu obiektów Blob Azure o dostępie hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-153">This script has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="47cbe-154"><a href="#appendix-b">Dodatek B</a> zawiera instrukcje dotyczące przygotowania i przekazywanie tego pliku tooyour własnych Azure konta magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="47cbe-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="47cbe-155">Dane wejściowe dla zadania Hive hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-155">Input data for hello Hive job.</span></span> <span data-ttu-id="47cbe-156">Witaj dane zostały przekazane tooan konta magazynu obiektów Blob Azure o dostępie hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-156">hello data has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="47cbe-157"><a href="#appendix-a">Dodatek a.</a> zawiera instrukcje dotyczące pobierania danych hello i przekazać hello danych tooyour własnych Azure konta magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="47cbe-157"><a href="#appendix-a">Appendix A</a> has instructions on getting hello data and uploading hello data tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="47cbe-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="47cbe-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="47cbe-159">Ścieżka wyjściowa Hello hello zadania Hive.</span><span class="sxs-lookup"><span data-stu-id="47cbe-159">hello output path for hello Hive job.</span></span> <span data-ttu-id="47cbe-160">Kontener domyślny Hello jest używany do przechowywania danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-160">hello default container is used for storing hello output data.</span></span></td></tr>
<tr><td><span data-ttu-id="47cbe-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="47cbe-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="47cbe-162">Witaj Hive zadania stanu folder hello domyślnego kontenera.</span><span class="sxs-lookup"><span data-stu-id="47cbe-162">hello Hive job status folder on hello default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="47cbe-163">Tworzenie klastra i uruchamianie zadania Hive/Sqoop</span><span class="sxs-lookup"><span data-stu-id="47cbe-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="47cbe-164">MapReduce z Hadoop jest przetwarzanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="47cbe-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="47cbe-165">Hello większości toorun ekonomiczny sposób zadania Hive jest toocreate klastra hello zadania i usunąć hello zadania po zakończeniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-165">hello most cost-effective way toorun a Hive job is toocreate a cluster for hello job, and delete hello job after hello job is completed.</span></span> <span data-ttu-id="47cbe-166">Witaj poniższy skrypt obejmuje hello całego procesu.</span><span class="sxs-lookup"><span data-stu-id="47cbe-166">hello following script covers hello whole process.</span></span>
<span data-ttu-id="47cbe-167">Aby uzyskać więcej informacji na temat tworzenia klastra usługi HDInsight i uruchamiania zadań Hive, zobacz [klastrów utworzyć Hadoop w usłudze HDInsight] [ hdinsight-provision] i [używanie Hive z usługą HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="47cbe-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="47cbe-168">**zapytań programu Hive hello toorun przez programu Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="47cbe-168">**toorun hello Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="47cbe-169">Tworzenie za pomocą instrukcji hello w tabeli bazy danych i hello Azure SQL dla danych wyjściowych zadania Sqoop hello [dodatku C](#appendix-c).</span><span class="sxs-lookup"><span data-stu-id="47cbe-169">Create an Azure SQL database and hello table for hello Sqoop job output by using hello instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="47cbe-170">Otwórz program Windows PowerShell ISE, a następnie uruchom hello następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="47cbe-170">Open Windows PowerShell ISE, and run hello following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="47cbe-171">Połączenia bazy danych SQL tooyour i zobacz opóźnienia średni transmitowane przez miasto tabeli AvgDelays hello:</span><span class="sxs-lookup"><span data-stu-id="47cbe-171">Connect tooyour SQL database and see average flight delays by city in hello AvgDelays table:</span></span>

    ![HDI. FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="47cbe-173"><a id="appendix-a"></a>Dodatek A - przekazywania transmitowane opóźnienie danych tooAzure magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="47cbe-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data tooAzure Blob storage</span></span>
<span data-ttu-id="47cbe-174">Przekazywanie hello plików danych i plików skryptów HiveQL hello (zobacz [dodatek B](#appendix-b)) wymaga niektórych planowania.</span><span class="sxs-lookup"><span data-stu-id="47cbe-174">Uploading hello data file and hello HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="47cbe-175">pomysł Hello jest toostore hello danych plików i plików HiveQL hello przed utworzeniem klastra usługi HDInsight i uruchamiania zadania Hive hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-175">hello idea is toostore hello data files and hello HiveQL file before creating an HDInsight cluster and running hello Hive job.</span></span> <span data-ttu-id="47cbe-176">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="47cbe-176">You have two options:</span></span>

* <span data-ttu-id="47cbe-177">**Użyj hello samo konto magazynu Azure, które będą używane przez klaster usługi HDInsight hello jako hello domyślnego systemu plików.**</span><span class="sxs-lookup"><span data-stu-id="47cbe-177">**Use hello same Azure Storage account that will be used by hello HDInsight cluster as hello default file system.**</span></span> <span data-ttu-id="47cbe-178">Ponieważ klaster usługi HDInsight hello będzie mieć klucz dostępu do konta magazynu hello, nie potrzebujesz toomake dodatkowe zmiany.</span><span class="sxs-lookup"><span data-stu-id="47cbe-178">Because hello HDInsight cluster will have hello Storage account access key, you don't need toomake any additional changes.</span></span>
* <span data-ttu-id="47cbe-179">**Użyj innego konta magazynu Azure z hello klastra usługi HDInsight domyślnego systemu plików.**</span><span class="sxs-lookup"><span data-stu-id="47cbe-179">**Use a different Azure Storage account from hello HDInsight cluster default file system.**</span></span> <span data-ttu-id="47cbe-180">Jeśli hello tak jest, należy zmodyfikować hello tworzenia część hello skrypt znalezione w programie Windows PowerShell [klaster tworzenia usługi HDInsight i uruchamiania zadań Hive/Sqoop](#runjob) toolink hello konta magazynu jako dodatkowe konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="47cbe-180">If this is hello case, you must modify hello creation part of hello Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) toolink hello Storage account as an additional Storage account.</span></span> <span data-ttu-id="47cbe-181">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Hadoop w usłudze HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="47cbe-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="47cbe-182">klaster usługi HDInsight Hello wie, następnie hello klucza dostępu dla konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-182">hello HDInsight cluster then knows hello access key for hello Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="47cbe-183">Witaj ścieżki do magazynu obiektów Blob dla pliku danych jest trudna kodowanych w pliku skryptu HiveQL hello powitalne.</span><span class="sxs-lookup"><span data-stu-id="47cbe-183">hello Blob storage path for hello data file is hard coded in hello HiveQL script file.</span></span> <span data-ttu-id="47cbe-184">Należy zaktualizować go odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="47cbe-184">You must update it accordingly.</span></span>

<span data-ttu-id="47cbe-185">**dane transmitowane hello toodownload**</span><span class="sxs-lookup"><span data-stu-id="47cbe-185">**toodownload hello flight data**</span></span>

1. <span data-ttu-id="47cbe-186">Przeglądaj zbyt[badań i innowacyjnych technologii administracji, biura statystyk transportu][rita-website].</span><span class="sxs-lookup"><span data-stu-id="47cbe-186">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="47cbe-187">Na stronie powitania wybierz hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="47cbe-187">On hello page, select hello following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="47cbe-188">Nazwa</span><span class="sxs-lookup"><span data-stu-id="47cbe-188">Name</span></span></th><th><span data-ttu-id="47cbe-189">Wartość</span><span class="sxs-lookup"><span data-stu-id="47cbe-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="47cbe-190">Filtr roku</span><span class="sxs-lookup"><span data-stu-id="47cbe-190">Filter Year</span></span></td><td><span data-ttu-id="47cbe-191">2013</span><span class="sxs-lookup"><span data-stu-id="47cbe-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="47cbe-192">Filtruj okres</span><span class="sxs-lookup"><span data-stu-id="47cbe-192">Filter Period</span></span></td><td><span data-ttu-id="47cbe-193">Stycznia</span><span class="sxs-lookup"><span data-stu-id="47cbe-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="47cbe-194">Pola</span><span class="sxs-lookup"><span data-stu-id="47cbe-194">Fields</span></span></td><td><span data-ttu-id="47cbe-195">*Rok*, *FlightDate*, *UniqueCarrier*, *operatora*, *FlightNum*, *OriginAirportID*, *pochodzenia*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*,  *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (Usuń zaznaczenie wszystkich innych pól)</span><span class="sxs-lookup"><span data-stu-id="47cbe-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="47cbe-196">
3.Kliknij przycisk **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="47cbe-196">
3. Click **Download**.</span></span>
<span data-ttu-id="47cbe-197">4.</span><span class="sxs-lookup"><span data-stu-id="47cbe-197">4.</span></span> <span data-ttu-id="47cbe-198">Rozpakuj hello pliku toohello **C:\Tutorials\FlightDelay\2013Data** folderu.</span><span class="sxs-lookup"><span data-stu-id="47cbe-198">Unzip hello file toohello **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="47cbe-199">Każdy plik jest plikiem CSV i jest rozmiar około 60GB.</span><span class="sxs-lookup"><span data-stu-id="47cbe-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="47cbe-200">5.</span><span class="sxs-lookup"><span data-stu-id="47cbe-200">5.</span></span> <span data-ttu-id="47cbe-201">Zmień nazwę toohello pliku hello hello miesiąca, który zawiera dane dla.</span><span class="sxs-lookup"><span data-stu-id="47cbe-201">Rename hello file toohello name of hello month that it contains data for.</span></span> <span data-ttu-id="47cbe-202">Na przykład, czy nazwany hello pliku zawierającego dane stycznia hello *January.csv*.</span><span class="sxs-lookup"><span data-stu-id="47cbe-202">For example, hello file containing hello January data would be named *January.csv*.</span></span>
<span data-ttu-id="47cbe-203">6.</span><span class="sxs-lookup"><span data-stu-id="47cbe-203">6.</span></span> <span data-ttu-id="47cbe-204">Powtórz kroki 2 i 5 toodownload pliku dla każdego hello 12 miesięcy w 2013.</span><span class="sxs-lookup"><span data-stu-id="47cbe-204">Repeat steps 2 and 5 toodownload a file for each of hello 12 months in 2013.</span></span> <span data-ttu-id="47cbe-205">Konieczne będzie co najmniej jednego pliku toorun hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="47cbe-205">You will need a minimum of one file toorun hello tutorial.</span></span>

<span data-ttu-id="47cbe-206">**tooupload hello transmitowane opóźnienie danych tooAzure magazynu obiektów Blob**</span><span class="sxs-lookup"><span data-stu-id="47cbe-206">**tooupload hello flight delay data tooAzure Blob storage**</span></span>

1. <span data-ttu-id="47cbe-207">Przygotowanie hello parametrów:</span><span class="sxs-lookup"><span data-stu-id="47cbe-207">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="47cbe-208">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="47cbe-208">Variable Name</span></span></th><th><span data-ttu-id="47cbe-209">Uwagi</span><span class="sxs-lookup"><span data-stu-id="47cbe-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="47cbe-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="47cbe-210">$storageAccountName</span></span></td><td><span data-ttu-id="47cbe-211">Witaj miejscu tooupload hello danych do konta usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="47cbe-211">hello Azure Storage account where you want tooupload hello data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="47cbe-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="47cbe-212">$blobContainerName</span></span></td><td><span data-ttu-id="47cbe-213">Witaj, w którym ma tooupload hello danych do kontenera obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="47cbe-213">hello Blob container where you want tooupload hello data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="47cbe-214">Otwórz program Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="47cbe-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="47cbe-215">3.</span><span class="sxs-lookup"><span data-stu-id="47cbe-215">3.</span></span> <span data-ttu-id="47cbe-216">Wklej hello następującego skryptu w okienku skryptów hello:</span><span class="sxs-lookup"><span data-stu-id="47cbe-216">Paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="47cbe-217">Naciśnij klawisz **F5** toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="47cbe-217">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="47cbe-218">Jeśli wybierzesz toouse inną metodę przekazywania plików hello, upewnij się, czy ścieżka pliku hello jest samouczki/flightdelay/danych.</span><span class="sxs-lookup"><span data-stu-id="47cbe-218">If you choose toouse a different method for uploading hello files, please make sure hello file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="47cbe-219">Składnia Hello dla uzyskiwania dostępu do plików hello jest następująca:</span><span class="sxs-lookup"><span data-stu-id="47cbe-219">hello syntax for accessing hello files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="47cbe-220">Ścieżka Hello samouczki/flightdelay/dane są hello wirtualny utworzony folder po przekazaniu plików hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-220">hello path tutorials/flightdelay/data is hello virtual folder you created when you uploaded hello files.</span></span> <span data-ttu-id="47cbe-221">Sprawdź, czy pliki 12, po jednej dla każdego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="47cbe-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="47cbe-222">Należy zaktualizować tooread zapytania Hive hello z hello nowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="47cbe-222">You must update hello Hive query tooread from hello new location.</span></span>
>
> <span data-ttu-id="47cbe-223">Należy skonfigurować hello kontenera dostępu uprawnienia toobe publicznego lub powiązać toohello konta magazynu hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47cbe-223">You must either configure hello container access permission toobe public or bind hello Storage account toohello HDInsight cluster.</span></span> <span data-ttu-id="47cbe-224">W przeciwnym razie wartość ciągu zapytania Hive hello nie będą mogli tooaccess hello danych plików.</span><span class="sxs-lookup"><span data-stu-id="47cbe-224">Otherwise, hello Hive query string will not be able tooaccess hello data files.</span></span>

- - -

## <span data-ttu-id="47cbe-225"><a id="appendix-b"></a>Dodatek B — tworzenie i przekazywanie skrypt HiveQL</span><span class="sxs-lookup"><span data-stu-id="47cbe-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="47cbe-226">Przy użyciu programu Azure PowerShell, można uruchomić wiele instrukcje HiveQL co w czasie, lub pakietu hello instrukcji HiveQL do pliku skryptu.</span><span class="sxs-lookup"><span data-stu-id="47cbe-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="47cbe-227">W tej sekcji przedstawiono, jak toocreate skrypt HiveQL i przekazywania hello skryptu tooAzure magazynu obiektów Blob przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47cbe-227">This section shows you how toocreate a HiveQL script and upload hello script tooAzure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="47cbe-228">Gałąź wymaga toobe skrypty HiveQL hello przechowywanych w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47cbe-228">Hive requires hello HiveQL scripts toobe stored in Azure Blob storage.</span></span>

<span data-ttu-id="47cbe-229">Witaj skrypt HiveQL zostaną wykonane następujące hello:</span><span class="sxs-lookup"><span data-stu-id="47cbe-229">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="47cbe-230">**Witaj delays_raw tabelę**, w przypadku, gdy tabela hello już istnieje.</span><span class="sxs-lookup"><span data-stu-id="47cbe-230">**Drop hello delays_raw table**, in case hello table already exists.</span></span>
2. <span data-ttu-id="47cbe-231">**Tworzenie tabeli Hive zewnętrznych delays_raw hello** wskazanie lokalizacji magazynu obiektów Blob toohello hello transmitowane opóźnienie plików.</span><span class="sxs-lookup"><span data-stu-id="47cbe-231">**Create hello delays_raw external Hive table** pointing toohello Blob storage location with hello flight delay files.</span></span> <span data-ttu-id="47cbe-232">To zapytanie określa, czy pola są rozdzielone "," i zakończenia wierszy przy "\n".</span><span class="sxs-lookup"><span data-stu-id="47cbe-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="47cbe-233">Stanowi to problem, gdy wartości pól zawierać przecinków, ponieważ gałąź nie może odróżnić przecinkami, która jest ogranicznik pola i jedną, która jest częścią wartość pola (co jest przypadku hello w wartości pól pochodzenia\_MIASTA\_nazwę i DOCELOWY\_ MIASTO\_nazwy).</span><span class="sxs-lookup"><span data-stu-id="47cbe-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is hello case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="47cbe-234">tooaddress hello tego zapytania tworzy TEMP kolumn danych toohold niepoprawnie jest podzielony na kolumny.</span><span class="sxs-lookup"><span data-stu-id="47cbe-234">tooaddress this, hello query creates TEMP columns toohold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="47cbe-235">**Tabelę opóźnienia hello**, w przypadku, gdy tabela hello już istnieje.</span><span class="sxs-lookup"><span data-stu-id="47cbe-235">**Drop hello delays table**, in case hello table already exists.</span></span>
4. <span data-ttu-id="47cbe-236">**Utwórz tabelę opóźnienia hello**.</span><span class="sxs-lookup"><span data-stu-id="47cbe-236">**Create hello delays table**.</span></span> <span data-ttu-id="47cbe-237">Jest przydatne tooclean zapasowych hello przed dalsze przetwarzanie.</span><span class="sxs-lookup"><span data-stu-id="47cbe-237">It is helpful tooclean up hello data before further processing.</span></span> <span data-ttu-id="47cbe-238">To zapytanie tworzy nową tabelę, *opóźnienia*, z tabeli delays_raw hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-238">This query creates a new table, *delays*, from hello delays_raw table.</span></span> <span data-ttu-id="47cbe-239">Należy pamiętać, że hello TEMP kolumn (jak już wspomniano) nie są kopiowane i że hello **podciąg** funkcji jest używane tooremove cudzysłów hello danych.</span><span class="sxs-lookup"><span data-stu-id="47cbe-239">Note that hello TEMP columns (as mentioned previously) are not copied, and that hello **substring** function is used tooremove quotation marks from hello data.</span></span>
5. <span data-ttu-id="47cbe-240">**Obliczeniowe hello pogody średnie opóźnienie i grup hello wyników przez nazwę miejscowości.**</span><span class="sxs-lookup"><span data-stu-id="47cbe-240">**Compute hello average weather delay and groups hello results by city name.**</span></span> <span data-ttu-id="47cbe-241">Zostanie również dane wyjściowe hello wyniki tooBlob magazynu.</span><span class="sxs-lookup"><span data-stu-id="47cbe-241">It will also output hello results tooBlob storage.</span></span> <span data-ttu-id="47cbe-242">Należy pamiętać, zapytania hello spowoduje usunięcie danych hello apostrofów i które pominie wierszy, gdzie wartość hello **weather_delay** ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="47cbe-242">Note that hello query will remove apostrophes from hello data and will exclude rows where hello value for **weather_delay** is null.</span></span> <span data-ttu-id="47cbe-243">Jest to konieczne, ponieważ Sqoop, używane w dalszej części tego samouczka nie bezpiecznie obsłużyć te wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="47cbe-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="47cbe-244">Aby uzyskać pełną listę poleceń HiveQL hello, zobacz [Hive języka definicji danych][hadoop-hiveql].</span><span class="sxs-lookup"><span data-stu-id="47cbe-244">For a full list of hello HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="47cbe-245">Każde polecenie HiveQL musi kończyć się średnikiem.</span><span class="sxs-lookup"><span data-stu-id="47cbe-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="47cbe-246">**plik skryptu HiveQL toocreate**</span><span class="sxs-lookup"><span data-stu-id="47cbe-246">**toocreate a HiveQL script file**</span></span>

1. <span data-ttu-id="47cbe-247">Przygotowanie hello parametrów:</span><span class="sxs-lookup"><span data-stu-id="47cbe-247">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="47cbe-248">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="47cbe-248">Variable Name</span></span></th><th><span data-ttu-id="47cbe-249">Uwagi</span><span class="sxs-lookup"><span data-stu-id="47cbe-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="47cbe-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="47cbe-250">$storageAccountName</span></span></td><td><span data-ttu-id="47cbe-251">Witaj konta magazynu Azure, gdzie chcesz skrypt HiveQL hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="47cbe-251">hello Azure Storage account where you want tooupload hello HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="47cbe-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="47cbe-252">$blobContainerName</span></span></td><td><span data-ttu-id="47cbe-253">Witaj, którym chcesz skrypt HiveQL hello tooupload kontenera obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="47cbe-253">hello Blob container where you want tooupload hello HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="47cbe-254">Otwórz program Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="47cbe-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="47cbe-255">3.</span><span class="sxs-lookup"><span data-stu-id="47cbe-255">3.</span></span> <span data-ttu-id="47cbe-256">Skopiuj i Wklej hello następującego skryptu w okienku skryptów hello:</span><span class="sxs-lookup"><span data-stu-id="47cbe-256">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="47cbe-257">Poniżej przedstawiono hello zmiennych w skrypcie hello:</span><span class="sxs-lookup"><span data-stu-id="47cbe-257">Here are hello variables used in hello script:</span></span>

   * <span data-ttu-id="47cbe-258">**$hqlLocalFileName** -skryptu hello zapisuje plik skryptu HiveQL hello lokalnie przed przekazaniem go tooBlob magazynu.</span><span class="sxs-lookup"><span data-stu-id="47cbe-258">**$hqlLocalFileName** - hello script saves hello HiveQL script file locally before uploading it tooBlob storage.</span></span> <span data-ttu-id="47cbe-259">Jest to nazwa pliku hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-259">This is hello file name.</span></span> <span data-ttu-id="47cbe-260">Witaj, wartość domyślna to <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span><span class="sxs-lookup"><span data-stu-id="47cbe-260">hello default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="47cbe-261">**$hqlBlobName** — jest to hello HiveQL nazwę pliku skryptu obiektów blob używane w hello magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47cbe-261">**$hqlBlobName** - This is hello HiveQL script file blob name used in hello Azure Blob storage.</span></span> <span data-ttu-id="47cbe-262">Wartość domyślna Hello jest tutorials/flightdelay/flightdelays.hql.</span><span class="sxs-lookup"><span data-stu-id="47cbe-262">hello default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="47cbe-263">Ponieważ hello zostanie zapisany plik bezpośrednio tooAzure magazynu obiektów Blob, nie istnieje "/" na początku hello hello nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="47cbe-263">Because hello file will be written directly tooAzure Blob storage, there is NOT a "/" at hello beginning of hello blob name.</span></span> <span data-ttu-id="47cbe-264">Jeśli chcesz tooaccess hello pliku z magazynu obiektów Blob, konieczne będzie tooadd "/" na początku hello hello nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="47cbe-264">If you want tooaccess hello file from Blob storage, you will need tooadd a "/" at hello beginning of hello file name.</span></span>
   * <span data-ttu-id="47cbe-265">**$srcDataFolder** i **$dstDataFolder** -= "data samouczki/flightdelay" = "samouczki flightdelay/wyjściowej"</span><span class="sxs-lookup"><span data-stu-id="47cbe-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="47cbe-266"><a id="appendix-c"></a>Dodatek C — przygotowanie bazy danych Azure SQL dla hello Sqoop dane wyjściowe zadania</span><span class="sxs-lookup"><span data-stu-id="47cbe-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for hello Sqoop job output</span></span>
<span data-ttu-id="47cbe-267">**Baza danych SQL hello tooprepare (Scal to z hello skryptu Sqoop)**</span><span class="sxs-lookup"><span data-stu-id="47cbe-267">**tooprepare hello SQL database (merge this with hello Sqoop script)**</span></span>

1. <span data-ttu-id="47cbe-268">Przygotowanie hello parametrów:</span><span class="sxs-lookup"><span data-stu-id="47cbe-268">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="47cbe-269">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="47cbe-269">Variable Name</span></span></th><th><span data-ttu-id="47cbe-270">Uwagi</span><span class="sxs-lookup"><span data-stu-id="47cbe-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="47cbe-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="47cbe-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="47cbe-272">Nazwa serwera bazy danych Azure SQL hello Hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-272">hello name of hello Azure SQL database server.</span></span> <span data-ttu-id="47cbe-273">Wprowadź nic toocreate nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="47cbe-273">Enter nothing toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="47cbe-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="47cbe-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="47cbe-275">Witaj nazwę logowania dla serwera bazy danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-275">hello login name for hello Azure SQL database server.</span></span> <span data-ttu-id="47cbe-276">$SqlDatabaseServerName w przypadku istniejącego serwera, używane tooauthenticate z serwerem hello są hello logowania i hasło logowania.</span><span class="sxs-lookup"><span data-stu-id="47cbe-276">If $sqlDatabaseServerName is an existing server, hello login and login password are used tooauthenticate with hello server.</span></span> <span data-ttu-id="47cbe-277">W przeciwnym razie są one używane toocreate nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="47cbe-277">Otherwise they are used toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="47cbe-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="47cbe-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="47cbe-279">Witaj hasło logowania dla serwera bazy danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-279">hello login password for hello Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="47cbe-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="47cbe-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="47cbe-281">Ta wartość jest używana tylko wtedy, gdy tworzysz nowy serwer bazy danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47cbe-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="47cbe-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="47cbe-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="47cbe-283">Baza danych SQL Hello używany toocreate hello AvgDelays tabeli dla hello Sqoop zadania.</span><span class="sxs-lookup"><span data-stu-id="47cbe-283">hello SQL database used toocreate hello AvgDelays table for hello Sqoop job.</span></span> <span data-ttu-id="47cbe-284">Utworzy bazę danych o nazwie HDISqoop pozostawić je puste.</span><span class="sxs-lookup"><span data-stu-id="47cbe-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="47cbe-285">Nazwa tabeli Hello hello Sqoop dane wyjściowe z zadania to AvgDelays.</span><span class="sxs-lookup"><span data-stu-id="47cbe-285">hello table name for hello Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="47cbe-286">Otwórz program Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="47cbe-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="47cbe-287">3.</span><span class="sxs-lookup"><span data-stu-id="47cbe-287">3.</span></span> <span data-ttu-id="47cbe-288">Skopiuj i Wklej hello następującego skryptu w okienku skryptów hello:</span><span class="sxs-lookup"><span data-stu-id="47cbe-288">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="47cbe-289">Witaj skrypt używa usługi transfer (REST) representational stanu, http://bot.whatismyipaddress.com, tooretrieve zewnętrzny adres IP.</span><span class="sxs-lookup"><span data-stu-id="47cbe-289">hello script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, tooretrieve your external IP address.</span></span> <span data-ttu-id="47cbe-290">adres IP Hello jest używany do utworzenia reguły zapory dla serwera bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="47cbe-290">hello IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="47cbe-291">Poniżej przedstawiono niektóre zmienne używane w skrypcie hello:</span><span class="sxs-lookup"><span data-stu-id="47cbe-291">Here are some variables used in hello script:</span></span>

   * <span data-ttu-id="47cbe-292">**$ipAddressRestService** -hello wartość domyślna to http://bot.whatismyipaddress.com. Jest on publiczny adres IP usługi REST do pobierania zewnętrzny adres IP.</span><span class="sxs-lookup"><span data-stu-id="47cbe-292">**$ipAddressRestService** - hello default value is http://bot.whatismyipaddress.com. It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="47cbe-293">Korzystania z innych usług, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="47cbe-293">You can use other services if you want.</span></span> <span data-ttu-id="47cbe-294">Hello pobrane za pośrednictwem usługi hello zewnętrzny adres IP będzie używany toocreate reguły zapory dla serwera bazy danych Azure SQL, aby umożliwić dostęp hello bazy danych ze stacji roboczej (przy użyciu skryptu programu Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="47cbe-294">hello external IP address retrieved through hello service will be used toocreate a firewall rule for your Azure SQL database server, so that you can access hello database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="47cbe-295">**$fireWallRuleName** — jest to nazwa hello hello reguły zapory dla serwera bazy danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-295">**$fireWallRuleName** - This is hello name of hello firewall rule for hello Azure SQL database server.</span></span> <span data-ttu-id="47cbe-296">Nazwa domyślnej Hello jest <u>FlightDelay</u>.</span><span class="sxs-lookup"><span data-stu-id="47cbe-296">hello default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="47cbe-297">Można zmienić jego nazwę, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="47cbe-297">You can rename it if you want.</span></span>
   * <span data-ttu-id="47cbe-298">**$sqlDatabaseMaxSizeGB** — ta wartość jest używana tylko wtedy, gdy tworzysz nowy serwer bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="47cbe-298">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="47cbe-299">Witaj, wartość domyślna to 10GB.</span><span class="sxs-lookup"><span data-stu-id="47cbe-299">hello default value is 10GB.</span></span> <span data-ttu-id="47cbe-300">10GB to wystarczający do celów tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="47cbe-300">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="47cbe-301">**$sqlDatabaseName** — ta wartość jest używana tylko wtedy, gdy tworzysz nową bazę danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="47cbe-301">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="47cbe-302">Wartość domyślna Hello jest HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="47cbe-302">hello default value is HDISqoop.</span></span> <span data-ttu-id="47cbe-303">Jeśli należy zmienić jego nazwę, należy zaktualizować odpowiednio skrypt programu Windows PowerShell Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-303">If you rename it, you must update hello Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="47cbe-304">Naciśnij klawisz **F5** toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="47cbe-304">Press **F5** toorun hello script.</span></span>
5. <span data-ttu-id="47cbe-305">Sprawdzanie poprawności danych wyjściowych skryptu hello.</span><span class="sxs-lookup"><span data-stu-id="47cbe-305">Validate hello script output.</span></span> <span data-ttu-id="47cbe-306">Upewnij się, że skrypt hello zostało wykonane pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="47cbe-306">Make sure hello script ran successfully.</span></span>

## <span data-ttu-id="47cbe-307"><a id="nextsteps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="47cbe-307"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="47cbe-308">Teraz wiesz, jak tooupload tooAzure pliku magazynu obiektów Blob, w jaki sposób toopopulate gałąź tabeli za pomocą hello danych z magazynu obiektów Blob platformy Azure, jak toorun Hive zapytań i w jaki sposób toouse Sqoop tooexport dane z bazy danych Azure SQL tooan systemu plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="47cbe-308">Now you understand how tooupload a file tooAzure Blob storage, how toopopulate a Hive table by using hello data from Azure Blob storage, how toorun Hive queries, and how toouse Sqoop tooexport data from HDFS tooan Azure SQL database.</span></span> <span data-ttu-id="47cbe-309">toolearn więcej, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="47cbe-309">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="47cbe-310">[Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="47cbe-310">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="47cbe-311">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="47cbe-311">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="47cbe-312">[Korzystanie z Oozie z usługą HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="47cbe-312">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="47cbe-313">[Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="47cbe-313">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="47cbe-314">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="47cbe-314">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="47cbe-315">[Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="47cbe-315">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
