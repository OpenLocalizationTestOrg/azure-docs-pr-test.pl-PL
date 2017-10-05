---
title: "Analizowanie danych opóźnienie transmitowane przy użyciu platformy Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać jednego skryptu środowiska Windows PowerShell do tworzenia klastra usługi HDInsight, uruchamiać zadania Hive, uruchom zadanie Sqoop i usunąć klaster."
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
ms.openlocfilehash: 77790136c9bd3a4e3f7dcabea2fbe0bcffb6eafe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="63b6a-103">Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="63b6a-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="63b6a-104">Gałąź umożliwia uruchomionych zadań MapReduce z Hadoop za pomocą skryptów języka przypominającego SQL o nazwie  *[HiveQL][hadoop-hiveql]*, które można zastosować do podsumowania, wyszukiwanie i analizowania dużych ilości danych.</span><span class="sxs-lookup"><span data-stu-id="63b6a-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63b6a-105">Kroki opisane w tym dokumencie wymagają klastra usługi HDInsight opartej na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="63b6a-105">The steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="63b6a-106">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="63b6a-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="63b6a-107">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="63b6a-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="63b6a-108">Opis czynności, które pracy z opartą na systemie Linux klastrem, zobacz [analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="63b6a-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="63b6a-109">Jedną z najważniejszych zalet usługi Azure HDInsight polega na rozdzieleniu magazynu danych i zasobów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="63b6a-109">One of the major benefits of Azure HDInsight is the separation of data storage and compute.</span></span> <span data-ttu-id="63b6a-110">HDInsight używa magazynu obiektów Blob platformy Azure do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="63b6a-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="63b6a-111">Typowe zadania obejmuje trzy części:</span><span class="sxs-lookup"><span data-stu-id="63b6a-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="63b6a-112">**Przechowywanie danych w magazynie obiektów Blob Azure.**</span><span class="sxs-lookup"><span data-stu-id="63b6a-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="63b6a-113">Na przykład pogodowe danych czujnika, danych, dzienników sieci web, a w tym przypadku transmitowane opóźnienie danych są zapisywane w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="63b6a-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="63b6a-114">**Uruchamianie zadań.**</span><span class="sxs-lookup"><span data-stu-id="63b6a-114">**Run jobs.**</span></span> <span data-ttu-id="63b6a-115">Gdy nadejdzie czas przetwarzania danych, należy uruchomić skrypt programu Windows PowerShell (lub aplikacja kliencka) do tworzenia klastra usługi HDInsight, uruchamiania zadań i usunąć klaster.</span><span class="sxs-lookup"><span data-stu-id="63b6a-115">When it is time to process the data, you run a Windows PowerShell script (or a client application) to create an HDInsight cluster, run jobs, and delete the cluster.</span></span> <span data-ttu-id="63b6a-116">Zadania zapisać danych wyjściowych do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="63b6a-116">The jobs save output data to Azure Blob storage.</span></span> <span data-ttu-id="63b6a-117">Dane są przechowywane, nawet po usunięciu klastra.</span><span class="sxs-lookup"><span data-stu-id="63b6a-117">The output data is retained even after the cluster is deleted.</span></span> <span data-ttu-id="63b6a-118">W ten sposób płacisz za tylko co użytkownik ma używane.</span><span class="sxs-lookup"><span data-stu-id="63b6a-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="63b6a-119">**Pobieranie danych wyjściowych z magazynu obiektów Blob Azure**, lub w tym samouczku, należy wyeksportować dane do bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-119">**Retrieve the output from Azure Blob storage**, or in this tutorial, export the data to an Azure SQL database.</span></span>

<span data-ttu-id="63b6a-120">Na poniższym diagramie przedstawiono scenariusza i struktura tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="63b6a-120">The following diagram illustrates the scenario and the structure of this tutorial:</span></span>

![HDI. FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="63b6a-122">Należy pamiętać, że numery na diagramie odpowiadają tytuły sekcji.</span><span class="sxs-lookup"><span data-stu-id="63b6a-122">Note that the numbers in the diagram correspond to the section titles.</span></span> <span data-ttu-id="63b6a-123">**M** oznacza głównego procesu.</span><span class="sxs-lookup"><span data-stu-id="63b6a-123">**M** stands for the main process.</span></span> <span data-ttu-id="63b6a-124">**A** oznacza zawartość w dodatku.</span><span class="sxs-lookup"><span data-stu-id="63b6a-124">**A** stands for the content in the appendix.</span></span>

<span data-ttu-id="63b6a-125">Głównych części samouczka przedstawiono sposób użycia jednego skryptu środowiska Windows PowerShell do wykonywania następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="63b6a-125">The main portion of the tutorial shows you how to use one Windows PowerShell script to perform the following tasks:</span></span>

* <span data-ttu-id="63b6a-126">Tworzenie klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="63b6a-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="63b6a-127">Uruchom zadania Hive w klastrze do obliczenia średniej opóźnień na lotniskach.</span><span class="sxs-lookup"><span data-stu-id="63b6a-127">Run a Hive job on the cluster to calculate average delays at airports.</span></span> <span data-ttu-id="63b6a-128">Dane opóźnienia przesyłane są przechowywane na koncie magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63b6a-128">The flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="63b6a-129">Uruchom zadanie Sqoop, aby wyeksportować dane wyjściowe zadania Hive do bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-129">Run a Sqoop job to export the Hive job output to an Azure SQL database.</span></span>
* <span data-ttu-id="63b6a-130">Usuń klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="63b6a-130">Delete the HDInsight cluster.</span></span>

<span data-ttu-id="63b6a-131">W dodatkach instrukcje można znaleźć przekazywanie danych opóźnienie transmitowane, ciąg zapytania Hive tworzenia/przekazywania i przygotowywanie bazy danych Azure SQL dla zadania Sqoop.</span><span class="sxs-lookup"><span data-stu-id="63b6a-131">In the appendixes, you can find the instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing the Azure SQL database for the Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="63b6a-132">Kroki opisane w tym dokumencie dotyczą klastrów usługi HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="63b6a-132">The steps in this document are specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="63b6a-133">Opis czynności, które pracy z opartą na systemie Linux klastrem, zobacz [analizowanie danych opóźnienie transmitowane przy użyciu Hive w usłudze HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span><span class="sxs-lookup"><span data-stu-id="63b6a-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="63b6a-134">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="63b6a-134">Prerequisites</span></span>
<span data-ttu-id="63b6a-135">Przed przystąpieniem do wykonywania kroków opisanych w tym samouczku musisz mieć poniższe:</span><span class="sxs-lookup"><span data-stu-id="63b6a-135">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="63b6a-136">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="63b6a-136">**An Azure subscription**.</span></span> <span data-ttu-id="63b6a-137">Zobacz artykuł [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="63b6a-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="63b6a-138">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="63b6a-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="63b6a-139">Obsługa programu Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i została usunięta z dniem 1 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="63b6a-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="63b6a-140">W czynnościach opisanych w niniejszym dokumencie są używane nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="63b6a-140">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="63b6a-141">Wykonaj kroki opisane w temacie [Instalowanie i konfigurowanie środowiska Azure PowerShell](/powershell/azureps-cmdlets-docs), aby zainstalować najnowszą wersję środowiska Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63b6a-141">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="63b6a-142">Jeśli masz skrypty wymagające modyfikacji w celu użycia nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz temat [Migrowanie do narzędzi programistycznych opartych na usłudze Azure Resource Manager w celu obsługi klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md), aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="63b6a-142">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="63b6a-143">**Pliki używane w tym samouczku**</span><span class="sxs-lookup"><span data-stu-id="63b6a-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="63b6a-144">W tym samouczku używana wydajności na czas linii lotniczych dane transmitowane z [badań i innowacyjnych administracyjnej technologii, biura statystyk transportu lub RICIE][rita-website].</span><span class="sxs-lookup"><span data-stu-id="63b6a-144">This tutorial uses the on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="63b6a-145">Kopię danych, został przesłany do kontenera magazynu obiektów Blob platformy Azure z uprawnieniem dostępu publicznego obiektu Blob.</span><span class="sxs-lookup"><span data-stu-id="63b6a-145">A copy of the data has been uploaded to an Azure Blob storage container with the Public Blob access permission.</span></span>
<span data-ttu-id="63b6a-146">Część skrypt programu PowerShell kopiuje dane z publicznym kontenerze obiektów blob do domyślnego kontenera obiektów blob klastra.</span><span class="sxs-lookup"><span data-stu-id="63b6a-146">A part of your PowerShell script copies the data from the public blob container to the default blob container of your cluster.</span></span> <span data-ttu-id="63b6a-147">Skrypt HiveQL również zostanie skopiowany do tego samego kontenera obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="63b6a-147">The HiveQL script is also copied to the same Blob container.</span></span>
<span data-ttu-id="63b6a-148">Jeśli chcesz dowiedzieć się, jak get/przekazywania danych do konta magazynu i Utwórz/przekazywania pliku skrypt HiveQL, zobacz [dodatek a.](#appendix-a) i [dodatek B](#appendix-b).</span><span class="sxs-lookup"><span data-stu-id="63b6a-148">If you want to learn how to get/upload the data to your own Storage account, and how to create/upload the HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="63b6a-149">W poniższej tabeli wymieniono pliki używane w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="63b6a-149">The following table lists the files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="63b6a-150">Pliki</span><span class="sxs-lookup"><span data-stu-id="63b6a-150">Files</span></span></th><th><span data-ttu-id="63b6a-151">Opis</span><span class="sxs-lookup"><span data-stu-id="63b6a-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="63b6a-152">Plik skryptu HiveQL używane przez zadania Hive.</span><span class="sxs-lookup"><span data-stu-id="63b6a-152">The HiveQL script file used by the Hive job.</span></span> <span data-ttu-id="63b6a-153">Ten skrypt został przekazany do konta magazynu obiektów Blob platformy Azure z dostępem public.</span><span class="sxs-lookup"><span data-stu-id="63b6a-153">This script has been uploaded to an Azure Blob storage account with the public access.</span></span> <span data-ttu-id="63b6a-154"><a href="#appendix-b">Dodatek B</a> zawiera instrukcje dotyczące przygotowania i przekazywanie tego pliku do swojego konta magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63b6a-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file to your own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="63b6a-155">Dane wejściowe zadania Hive.</span><span class="sxs-lookup"><span data-stu-id="63b6a-155">Input data for the Hive job.</span></span> <span data-ttu-id="63b6a-156">Dane przekazane do konta magazynu obiektów Blob platformy Azure z dostępem public.</span><span class="sxs-lookup"><span data-stu-id="63b6a-156">The data has been uploaded to an Azure Blob storage account with the public access.</span></span> <span data-ttu-id="63b6a-157"><a href="#appendix-a">Dodatek a.</a> zawiera instrukcje dotyczące pobierania danych i przekazywanie danych do swojego konta magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63b6a-157"><a href="#appendix-a">Appendix A</a> has instructions on getting the data and uploading the data to your own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="63b6a-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="63b6a-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="63b6a-159">Ścieżka danych wyjściowych zadania Hive.</span><span class="sxs-lookup"><span data-stu-id="63b6a-159">The output path for the Hive job.</span></span> <span data-ttu-id="63b6a-160">Domyślny kontener jest używany do przechowywania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="63b6a-160">The default container is used for storing the output data.</span></span></td></tr>
<tr><td><span data-ttu-id="63b6a-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="63b6a-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="63b6a-162">Folder stan zadania Hive na domyślny kontener.</span><span class="sxs-lookup"><span data-stu-id="63b6a-162">The Hive job status folder on the default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="63b6a-163">Tworzenie klastra i uruchamianie zadania Hive/Sqoop</span><span class="sxs-lookup"><span data-stu-id="63b6a-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="63b6a-164">MapReduce z Hadoop jest przetwarzanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="63b6a-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="63b6a-165">Najbardziej ekonomiczny sposób uruchamiania zadania Hive jest utworzenie klastra zadania i usunąć zadanie po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="63b6a-165">The most cost-effective way to run a Hive job is to create a cluster for the job, and delete the job after the job is completed.</span></span> <span data-ttu-id="63b6a-166">Poniższy skrypt obejmuje całego procesu.</span><span class="sxs-lookup"><span data-stu-id="63b6a-166">The following script covers the whole process.</span></span>
<span data-ttu-id="63b6a-167">Aby uzyskać więcej informacji na temat tworzenia klastra usługi HDInsight i uruchamiania zadań Hive, zobacz [klastrów utworzyć Hadoop w usłudze HDInsight] [ hdinsight-provision] i [używanie Hive z usługą HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="63b6a-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="63b6a-168">**Uruchamianie zapytań Hive programu Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="63b6a-168">**To run the Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="63b6a-169">Tworzenie bazy danych Azure SQL i tabeli dla danych wyjściowych zadania Sqoop zgodnie z instrukcjami podanymi w [dodatku C](#appendix-c).</span><span class="sxs-lookup"><span data-stu-id="63b6a-169">Create an Azure SQL database and the table for the Sqoop job output by using the instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="63b6a-170">Otwórz program Windows PowerShell ISE, a następnie uruchom następujący skrypt:</span><span class="sxs-lookup"><span data-stu-id="63b6a-170">Open Windows PowerShell ISE, and run the following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure the follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on the version, the folder can be different

    ###########################################
    # (Optional) configure the following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter the Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use the cluster name

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

    # Create the default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create the HDInsight cluster
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
    # Prepare the HiveQL script and source data
    ###########################################

    # Create the temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download the sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data to default container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit the Hive job
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
    # Submit the Sqoop job
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
    # Delete the cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="63b6a-171">Połączenia z bazą danych SQL i zobacz opóźnienia średni transmitowane przez Miasto w tabeli AvgDelays:</span><span class="sxs-lookup"><span data-stu-id="63b6a-171">Connect to your SQL database and see average flight delays by city in the AvgDelays table:</span></span>

    ![HDI. FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="63b6a-173"><a id="appendix-a"></a>Dodatek a. — Przekaż transmitowane opóźnienie dane do magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="63b6a-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data to Azure Blob storage</span></span>
<span data-ttu-id="63b6a-174">Przekazywanie plików danych i plików skryptu po stronie HiveQL (zobacz [dodatek B](#appendix-b)) wymaga niektórych planowania.</span><span class="sxs-lookup"><span data-stu-id="63b6a-174">Uploading the data file and the HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="63b6a-175">Będzie przechowywać pliki danych i pliku HiveQL przed utworzeniem klastra usługi HDInsight i uruchamiania zadań Hive.</span><span class="sxs-lookup"><span data-stu-id="63b6a-175">The idea is to store the data files and the HiveQL file before creating an HDInsight cluster and running the Hive job.</span></span> <span data-ttu-id="63b6a-176">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="63b6a-176">You have two options:</span></span>

* <span data-ttu-id="63b6a-177">**Użyj tego samego konta magazynu Azure, który będzie używany przez klaster usługi HDInsight jako domyślny system plików.**</span><span class="sxs-lookup"><span data-stu-id="63b6a-177">**Use the same Azure Storage account that will be used by the HDInsight cluster as the default file system.**</span></span> <span data-ttu-id="63b6a-178">Ponieważ klaster usługi HDInsight nie będzie mieć klucz dostępu do konta magazynu, nie trzeba wprowadzać żadnych dodatkowych zmian.</span><span class="sxs-lookup"><span data-stu-id="63b6a-178">Because the HDInsight cluster will have the Storage account access key, you don't need to make any additional changes.</span></span>
* <span data-ttu-id="63b6a-179">**Użyj innego konta usługi Azure Storage z systemu plików domyślnego klastra usługi HDInsight.**</span><span class="sxs-lookup"><span data-stu-id="63b6a-179">**Use a different Azure Storage account from the HDInsight cluster default file system.**</span></span> <span data-ttu-id="63b6a-180">Jeśli jest to możliwe, należy zmodyfikować tworzenia część programu Windows PowerShell skrypt znalezione w [klaster tworzenia usługi HDInsight i uruchamiania zadań Hive/Sqoop](#runjob) połączenia konta magazynu jako dodatkowe konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="63b6a-180">If this is the case, you must modify the creation part of the Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) to link the Storage account as an additional Storage account.</span></span> <span data-ttu-id="63b6a-181">Aby uzyskać instrukcje, zobacz [klastrów utworzyć Hadoop w usłudze HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="63b6a-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="63b6a-182">Klaster usługi HDInsight wie, następnie klucz dostępu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="63b6a-182">The HDInsight cluster then knows the access key for the Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="63b6a-183">Ścieżki do magazynu obiektów Blob dla pliku danych jest trudna kodowanych w pliku skryptu HiveQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-183">The Blob storage path for the data file is hard coded in the HiveQL script file.</span></span> <span data-ttu-id="63b6a-184">Należy zaktualizować go odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="63b6a-184">You must update it accordingly.</span></span>

<span data-ttu-id="63b6a-185">**Aby pobrać dane transmitowane**</span><span class="sxs-lookup"><span data-stu-id="63b6a-185">**To download the flight data**</span></span>

1. <span data-ttu-id="63b6a-186">Przejdź do [badań i Nowatorska technologia administracji, biura statystyk transportu][rita-website].</span><span class="sxs-lookup"><span data-stu-id="63b6a-186">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="63b6a-187">Na stronie wybierz następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="63b6a-187">On the page, select the following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="63b6a-188">Nazwa</span><span class="sxs-lookup"><span data-stu-id="63b6a-188">Name</span></span></th><th><span data-ttu-id="63b6a-189">Wartość</span><span class="sxs-lookup"><span data-stu-id="63b6a-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="63b6a-190">Filtr roku</span><span class="sxs-lookup"><span data-stu-id="63b6a-190">Filter Year</span></span></td><td><span data-ttu-id="63b6a-191">2013</span><span class="sxs-lookup"><span data-stu-id="63b6a-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="63b6a-192">Filtruj okres</span><span class="sxs-lookup"><span data-stu-id="63b6a-192">Filter Period</span></span></td><td><span data-ttu-id="63b6a-193">Stycznia</span><span class="sxs-lookup"><span data-stu-id="63b6a-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="63b6a-194">Pola</span><span class="sxs-lookup"><span data-stu-id="63b6a-194">Fields</span></span></td><td><span data-ttu-id="63b6a-195">*Rok*, *FlightDate*, *UniqueCarrier*, *operatora*, *FlightNum*, *OriginAirportID*, *pochodzenia*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*,  *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (Usuń zaznaczenie wszystkich innych pól)</span><span class="sxs-lookup"><span data-stu-id="63b6a-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="63b6a-196">
3.Kliknij przycisk **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="63b6a-196">
3. Click **Download**.</span></span>
<span data-ttu-id="63b6a-197">4.</span><span class="sxs-lookup"><span data-stu-id="63b6a-197">4.</span></span> <span data-ttu-id="63b6a-198">Rozpakuj plik **C:\Tutorials\FlightDelay\2013Data** folderu.</span><span class="sxs-lookup"><span data-stu-id="63b6a-198">Unzip the file to the **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="63b6a-199">Każdy plik jest plikiem CSV i jest rozmiar około 60GB.</span><span class="sxs-lookup"><span data-stu-id="63b6a-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="63b6a-200">5.</span><span class="sxs-lookup"><span data-stu-id="63b6a-200">5.</span></span> <span data-ttu-id="63b6a-201">Zmień nazwę miesiąca, który zawiera dane dla pliku.</span><span class="sxs-lookup"><span data-stu-id="63b6a-201">Rename the file to the name of the month that it contains data for.</span></span> <span data-ttu-id="63b6a-202">Na przykład, czy nazwę pliku zawierającego dane stycznia *January.csv*.</span><span class="sxs-lookup"><span data-stu-id="63b6a-202">For example, the file containing the January data would be named *January.csv*.</span></span>
<span data-ttu-id="63b6a-203">6.</span><span class="sxs-lookup"><span data-stu-id="63b6a-203">6.</span></span> <span data-ttu-id="63b6a-204">Powtórz kroki 2 i 5, aby pobrać plik dla każdej z 12 miesięcy w 2013.</span><span class="sxs-lookup"><span data-stu-id="63b6a-204">Repeat steps 2 and 5 to download a file for each of the 12 months in 2013.</span></span> <span data-ttu-id="63b6a-205">Konieczne będzie co najmniej jeden plik do uruchamiania w samouczku.</span><span class="sxs-lookup"><span data-stu-id="63b6a-205">You will need a minimum of one file to run the tutorial.</span></span>

<span data-ttu-id="63b6a-206">**Aby przekazać dane opóźnienie przesyłane do magazynu obiektów Blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="63b6a-206">**To upload the flight delay data to Azure Blob storage**</span></span>

1. <span data-ttu-id="63b6a-207">Przygotowanie parametrów:</span><span class="sxs-lookup"><span data-stu-id="63b6a-207">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="63b6a-208">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="63b6a-208">Variable Name</span></span></th><th><span data-ttu-id="63b6a-209">Uwagi</span><span class="sxs-lookup"><span data-stu-id="63b6a-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="63b6a-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="63b6a-210">$storageAccountName</span></span></td><td><span data-ttu-id="63b6a-211">Konto magazynu Azure, której chcesz przekazać dane do.</span><span class="sxs-lookup"><span data-stu-id="63b6a-211">The Azure Storage account where you want to upload the data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="63b6a-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="63b6a-212">$blobContainerName</span></span></td><td><span data-ttu-id="63b6a-213">Gdzie chcesz przekazać dane do kontenera obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="63b6a-213">The Blob container where you want to upload the data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="63b6a-214">Otwórz program Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="63b6a-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="63b6a-215">3.</span><span class="sxs-lookup"><span data-stu-id="63b6a-215">3.</span></span> <span data-ttu-id="63b6a-216">Wklej poniższy skrypt w okienku skryptów:</span><span class="sxs-lookup"><span data-stu-id="63b6a-216">Paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure storage account name for creating a new HDInsight cluster. If the account doesn't exist, the script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure blob container name for creating a new HDInsight cluster. If not specified, the HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # The source folder
    $destFolder = "tutorials/flightdelay/2013data"     #The blob name prefix for the files to be uploaded
    #EndRegion

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating the Azure Storage account and the Blob container..." -ForegroundColor Green
    # Validate the Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "The storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate the container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "The Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy the file from local workstation to Azure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName to $blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "The source folder on the workstation doesn't exist" -ForegroundColor Red
    }

    # List the uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="63b6a-217">Naciśnij klawisz **F5**, aby uruchomić skrypt.</span><span class="sxs-lookup"><span data-stu-id="63b6a-217">Press **F5** to run the script.</span></span>

<span data-ttu-id="63b6a-218">Jeśli chcesz użyć innej metody do przekazywania plików, upewnij się, czy ścieżka pliku jest samouczki/flightdelay/danych.</span><span class="sxs-lookup"><span data-stu-id="63b6a-218">If you choose to use a different method for uploading the files, please make sure the file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="63b6a-219">Aby uzyskać dostęp do plików składnia jest następująca:</span><span class="sxs-lookup"><span data-stu-id="63b6a-219">The syntax for accessing the files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="63b6a-220">Ścieżka samouczki/flightdelay/danych jest folder wirtualny utworzony po przekazaniu plików.</span><span class="sxs-lookup"><span data-stu-id="63b6a-220">The path tutorials/flightdelay/data is the virtual folder you created when you uploaded the files.</span></span> <span data-ttu-id="63b6a-221">Sprawdź, czy pliki 12, po jednej dla każdego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="63b6a-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="63b6a-222">Zaktualizuj zapytanie Hive można odczytać z nowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="63b6a-222">You must update the Hive query to read from the new location.</span></span>
>
> <span data-ttu-id="63b6a-223">Należy albo skonfigurować uprawnienia dostępu do kontenera do być publiczne lub konto magazynu z klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="63b6a-223">You must either configure the container access permission to be public or bind the Storage account to the HDInsight cluster.</span></span> <span data-ttu-id="63b6a-224">W przeciwnym razie nie będzie dostęp do plików danych ciąg zapytania Hive.</span><span class="sxs-lookup"><span data-stu-id="63b6a-224">Otherwise, the Hive query string will not be able to access the data files.</span></span>

- - -

## <span data-ttu-id="63b6a-225"><a id="appendix-b"></a>Dodatek B — tworzenie i przekazywanie skrypt HiveQL</span><span class="sxs-lookup"><span data-stu-id="63b6a-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="63b6a-226">Przy użyciu programu Azure PowerShell, można uruchomić wiele instrukcje HiveQL jeden naraz lub pakietu w pliku skryptu za pomocą instrukcji HiveQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span></span> <span data-ttu-id="63b6a-227">W tej sekcji przedstawiono sposób utworzyć skrypt HiveQL i Prześlij skrypt do magazynu obiektów Blob platformy Azure przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63b6a-227">This section shows you how to create a HiveQL script and upload the script to Azure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="63b6a-228">Gałąź wymaga skrypty HiveQL, które mają być przechowywane w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="63b6a-228">Hive requires the HiveQL scripts to be stored in Azure Blob storage.</span></span>

<span data-ttu-id="63b6a-229">Skrypt HiveQL będzie wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="63b6a-229">The HiveQL script will perform the following:</span></span>

1. <span data-ttu-id="63b6a-230">**Tabelę delays_raw**, w przypadku, gdy tabela już istnieje.</span><span class="sxs-lookup"><span data-stu-id="63b6a-230">**Drop the delays_raw table**, in case the table already exists.</span></span>
2. <span data-ttu-id="63b6a-231">**Tworzenie tabeli Hive zewnętrznych delays_raw** wskazanie lokalizacji magazynu obiektów Blob z plikami opóźnienie transmitowane.</span><span class="sxs-lookup"><span data-stu-id="63b6a-231">**Create the delays_raw external Hive table** pointing to the Blob storage location with the flight delay files.</span></span> <span data-ttu-id="63b6a-232">To zapytanie określa, czy pola są rozdzielone "," i zakończenia wierszy przy "\n".</span><span class="sxs-lookup"><span data-stu-id="63b6a-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="63b6a-233">Stanowi to problem, gdy wartości pól zawierać przecinków, ponieważ gałąź nie może odróżnić przecinkami, która jest ogranicznik pola i jedną, która jest częścią wartość pola (co ma miejsce w wartości pól dla źródła\_MIASTA\_nazwę i DOCELOWY\_MIASTA\_nazwy).</span><span class="sxs-lookup"><span data-stu-id="63b6a-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is the case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="63b6a-234">Aby rozwiązać ten problem, zapytanie tworzy TEMP kolumn do przechowywania danych, niepoprawnie podzielonej na kolumny.</span><span class="sxs-lookup"><span data-stu-id="63b6a-234">To address this, the query creates TEMP columns to hold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="63b6a-235">**Tabelę opóźnienia**, w przypadku, gdy tabela już istnieje.</span><span class="sxs-lookup"><span data-stu-id="63b6a-235">**Drop the delays table**, in case the table already exists.</span></span>
4. <span data-ttu-id="63b6a-236">**Utwórz tabelę opóźnienia**.</span><span class="sxs-lookup"><span data-stu-id="63b6a-236">**Create the delays table**.</span></span> <span data-ttu-id="63b6a-237">Warto wyczyścić dane przed dalsze przetwarzanie.</span><span class="sxs-lookup"><span data-stu-id="63b6a-237">It is helpful to clean up the data before further processing.</span></span> <span data-ttu-id="63b6a-238">To zapytanie tworzy nową tabelę, *opóźnienia*, z tabeli delays_raw.</span><span class="sxs-lookup"><span data-stu-id="63b6a-238">This query creates a new table, *delays*, from the delays_raw table.</span></span> <span data-ttu-id="63b6a-239">Należy pamiętać, że kolumny TEMP (jak już wspomniano) nie są kopiowane, a **podciąg** funkcja służy do usuwania cudzysłów z danych.</span><span class="sxs-lookup"><span data-stu-id="63b6a-239">Note that the TEMP columns (as mentioned previously) are not copied, and that the **substring** function is used to remove quotation marks from the data.</span></span>
5. <span data-ttu-id="63b6a-240">**Obliczenia bazy danych pogody średnie opóźnienie i grup wyników przez nazwę miejscowości.**</span><span class="sxs-lookup"><span data-stu-id="63b6a-240">**Compute the average weather delay and groups the results by city name.**</span></span> <span data-ttu-id="63b6a-241">Będzie on również zapisuje wyniki do magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="63b6a-241">It will also output the results to Blob storage.</span></span> <span data-ttu-id="63b6a-242">Zapytanie spowoduje usunięcie apostrofów z danych i pominie wiersze, w których wartość **weather_delay** ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="63b6a-242">Note that the query will remove apostrophes from the data and will exclude rows where the value for **weather_delay** is null.</span></span> <span data-ttu-id="63b6a-243">Jest to konieczne, ponieważ Sqoop, używane w dalszej części tego samouczka nie bezpiecznie obsłużyć te wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="63b6a-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="63b6a-244">Aby uzyskać pełną listę poleceń HiveQL, zobacz [Hive języka definicji danych][hadoop-hiveql].</span><span class="sxs-lookup"><span data-stu-id="63b6a-244">For a full list of the HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="63b6a-245">Każde polecenie HiveQL musi kończyć się średnikiem.</span><span class="sxs-lookup"><span data-stu-id="63b6a-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="63b6a-246">**Aby utworzyć plik skryptu HiveQL**</span><span class="sxs-lookup"><span data-stu-id="63b6a-246">**To create a HiveQL script file**</span></span>

1. <span data-ttu-id="63b6a-247">Przygotowanie parametrów:</span><span class="sxs-lookup"><span data-stu-id="63b6a-247">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="63b6a-248">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="63b6a-248">Variable Name</span></span></th><th><span data-ttu-id="63b6a-249">Uwagi</span><span class="sxs-lookup"><span data-stu-id="63b6a-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="63b6a-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="63b6a-250">$storageAccountName</span></span></td><td><span data-ttu-id="63b6a-251">Gdzie chcesz przekazać skrypt HiveQL, aby konto usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="63b6a-251">The Azure Storage account where you want to upload the HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="63b6a-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="63b6a-252">$blobContainerName</span></span></td><td><span data-ttu-id="63b6a-253">Kontener obiektów Blob, gdy chcesz przekazać skrypt HiveQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-253">The Blob container where you want to upload the HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="63b6a-254">Otwórz program Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="63b6a-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="63b6a-255">3.</span><span class="sxs-lookup"><span data-stu-id="63b6a-255">3.</span></span> <span data-ttu-id="63b6a-256">Skopiuj i wklej poniższy skrypt w okienku skryptów:</span><span class="sxs-lookup"><span data-stu-id="63b6a-256">Copy and paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure storage account name for creating a new HDInsight cluster. If the account doesn't exist, the script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure blob container name for creating a new HDInsight cluster. If not specified, the HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # The HiveQL script file is exported as this file before it's uploaded to Blob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # The HiveQL script file will be uploaded to Blob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by the HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating the Azure Storage account and the Blob container..." -ForegroundColor Green
    # Validate the Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "The storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate the container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "The Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate the file and file path

    # Check if a file with the same file name already exists on the workstation
    Write-Host "`nvalidating the folder structure on the workstation for saving the HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'The file, ' $hqlLocalFileName ', exists.  Do you want to overwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create the folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write the Hive script into a local file
    Write-Host "`nWriting the Hive script into a file on your workstation ..." `
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

    #region - Upload the Hive script to the default Blob container
    Write-Host "`nUploading the Hive script to the default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload the file from local workstation to Blob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of the PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="63b6a-257">Poniżej przedstawiono zmiennych w skrypcie:</span><span class="sxs-lookup"><span data-stu-id="63b6a-257">Here are the variables used in the script:</span></span>

   * <span data-ttu-id="63b6a-258">**$hqlLocalFileName** -skrypt zapisuje plik skryptu HiveQL lokalnie przed przekazaniem go do magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="63b6a-258">**$hqlLocalFileName** - The script saves the HiveQL script file locally before uploading it to Blob storage.</span></span> <span data-ttu-id="63b6a-259">Jest to nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="63b6a-259">This is the file name.</span></span> <span data-ttu-id="63b6a-260">Wartość domyślna to <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span><span class="sxs-lookup"><span data-stu-id="63b6a-260">The default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="63b6a-261">**$hqlBlobName** — jest to nazwa obiektu blob pliku skryptu HiveQL używana w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63b6a-261">**$hqlBlobName** - This is the HiveQL script file blob name used in the Azure Blob storage.</span></span> <span data-ttu-id="63b6a-262">Wartość domyślna to tutorials/flightdelay/flightdelays.hql.</span><span class="sxs-lookup"><span data-stu-id="63b6a-262">The default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="63b6a-263">Ponieważ plik zostanie zapisany bezpośrednio do magazynu obiektów Blob platformy Azure, nie istnieje "/" na początku nazwy obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="63b6a-263">Because the file will be written directly to Azure Blob storage, there is NOT a "/" at the beginning of the blob name.</span></span> <span data-ttu-id="63b6a-264">Jeśli chcesz uzyskać dostęp do pliku z magazynu obiektów Blob, należy dodać "/" na początku nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="63b6a-264">If you want to access the file from Blob storage, you will need to add a "/" at the beginning of the file name.</span></span>
   * <span data-ttu-id="63b6a-265">**$srcDataFolder** i **$dstDataFolder** -= "data samouczki/flightdelay" = "samouczki flightdelay/wyjściowej"</span><span class="sxs-lookup"><span data-stu-id="63b6a-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="63b6a-266"><a id="appendix-c"></a>Dodatek C — przygotowanie bazy danych Azure SQL dla danych wyjściowych zadania Sqoop</span><span class="sxs-lookup"><span data-stu-id="63b6a-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for the Sqoop job output</span></span>
<span data-ttu-id="63b6a-267">**Aby przygotować bazy danych SQL (Scalaj to przy użyciu skryptu Sqoop)**</span><span class="sxs-lookup"><span data-stu-id="63b6a-267">**To prepare the SQL database (merge this with the Sqoop script)**</span></span>

1. <span data-ttu-id="63b6a-268">Przygotowanie parametrów:</span><span class="sxs-lookup"><span data-stu-id="63b6a-268">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="63b6a-269">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="63b6a-269">Variable Name</span></span></th><th><span data-ttu-id="63b6a-270">Uwagi</span><span class="sxs-lookup"><span data-stu-id="63b6a-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="63b6a-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="63b6a-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="63b6a-272">Nazwa serwera bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-272">The name of the Azure SQL database server.</span></span> <span data-ttu-id="63b6a-273">Wprowadź nic do utworzenia nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="63b6a-273">Enter nothing to create a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="63b6a-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="63b6a-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="63b6a-275">Nazwa logowania dla serwera bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-275">The login name for the Azure SQL database server.</span></span> <span data-ttu-id="63b6a-276">Jeśli $sqlDatabaseServerName jest istniejący serwer, logowania i hasło logowania są używane do uwierzytelniania z serwerem.</span><span class="sxs-lookup"><span data-stu-id="63b6a-276">If $sqlDatabaseServerName is an existing server, the login and login password are used to authenticate with the server.</span></span> <span data-ttu-id="63b6a-277">W przeciwnym razie są one używane do utworzenia nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="63b6a-277">Otherwise they are used to create a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="63b6a-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="63b6a-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="63b6a-279">Hasło nazwy logowania dla serwera bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-279">The login password for the Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="63b6a-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="63b6a-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="63b6a-281">Ta wartość jest używana tylko wtedy, gdy tworzysz nowy serwer bazy danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="63b6a-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="63b6a-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="63b6a-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="63b6a-283">Baza danych SQL, użyty do utworzenia tabeli AvgDelays zadania Sqoop.</span><span class="sxs-lookup"><span data-stu-id="63b6a-283">The SQL database used to create the AvgDelays table for the Sqoop job.</span></span> <span data-ttu-id="63b6a-284">Utworzy bazę danych o nazwie HDISqoop pozostawić je puste.</span><span class="sxs-lookup"><span data-stu-id="63b6a-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="63b6a-285">Nazwa tabeli dla danych wyjściowych zadania Sqoop jest AvgDelays.</span><span class="sxs-lookup"><span data-stu-id="63b6a-285">The table name for the Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="63b6a-286">Otwórz program Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="63b6a-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="63b6a-287">3.</span><span class="sxs-lookup"><span data-stu-id="63b6a-287">3.</span></span> <span data-ttu-id="63b6a-288">Skopiuj i wklej poniższy skrypt w okienku skryptów:</span><span class="sxs-lookup"><span data-stu-id="63b6a-288">Copy and paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the region to create the Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify the database name if you have one created. Otherwise use "" to have the script create one for you.
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

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. Note that this allows Azure traffic from any Azure subscription to access the server.
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

    #region -  Execute an SQL command to create the AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of the PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="63b6a-289">Skrypt używa representational stanu usługi transfer (REST), http://bot.whatismyipaddress.com, można pobrać zewnętrzny adres IP.</span><span class="sxs-lookup"><span data-stu-id="63b6a-289">The script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, to retrieve your external IP address.</span></span> <span data-ttu-id="63b6a-290">Adres IP jest używany do utworzenia reguły zapory dla serwera bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-290">The IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="63b6a-291">Poniżej przedstawiono niektóre zmienne używane w skrypcie:</span><span class="sxs-lookup"><span data-stu-id="63b6a-291">Here are some variables used in the script:</span></span>

   * <span data-ttu-id="63b6a-292">**$ipAddressRestService** — wartość domyślna to http://bot.whatismyipaddress.com.</span><span class="sxs-lookup"><span data-stu-id="63b6a-292">**$ipAddressRestService** - The default value is http://bot.whatismyipaddress.com.</span></span> <span data-ttu-id="63b6a-293">Jest on publiczny adres IP usługi REST do pobierania zewnętrzny adres IP.</span><span class="sxs-lookup"><span data-stu-id="63b6a-293">It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="63b6a-294">Korzystania z innych usług, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="63b6a-294">You can use other services if you want.</span></span> <span data-ttu-id="63b6a-295">Zewnętrzny adres IP pobrane za pośrednictwem usługi będzie służyć do utworzenia reguły zapory dla serwera bazy danych Azure SQL, dzięki czemu można dostęp do bazy danych ze stacji roboczej (przy użyciu skryptu programu Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="63b6a-295">The external IP address retrieved through the service will be used to create a firewall rule for your Azure SQL database server, so that you can access the database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="63b6a-296">**$fireWallRuleName** — jest to nazwa reguły zapory dla serwera bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-296">**$fireWallRuleName** - This is the name of the firewall rule for the Azure SQL database server.</span></span> <span data-ttu-id="63b6a-297">Nazwa domyślna to <u>FlightDelay</u>.</span><span class="sxs-lookup"><span data-stu-id="63b6a-297">The default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="63b6a-298">Można zmienić jego nazwę, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="63b6a-298">You can rename it if you want.</span></span>
   * <span data-ttu-id="63b6a-299">**$sqlDatabaseMaxSizeGB** — ta wartość jest używana tylko wtedy, gdy tworzysz nowy serwer bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-299">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="63b6a-300">Wartość domyślna wynosi 10GB.</span><span class="sxs-lookup"><span data-stu-id="63b6a-300">The default value is 10GB.</span></span> <span data-ttu-id="63b6a-301">10GB to wystarczający do celów tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="63b6a-301">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="63b6a-302">**$sqlDatabaseName** — ta wartość jest używana tylko wtedy, gdy tworzysz nową bazę danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-302">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="63b6a-303">Wartość domyślna to HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="63b6a-303">The default value is HDISqoop.</span></span> <span data-ttu-id="63b6a-304">Jeśli należy zmienić jego nazwę, należy zaktualizować odpowiednio skrypt programu Windows PowerShell Sqoop.</span><span class="sxs-lookup"><span data-stu-id="63b6a-304">If you rename it, you must update the Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="63b6a-305">Naciśnij klawisz **F5**, aby uruchomić skrypt.</span><span class="sxs-lookup"><span data-stu-id="63b6a-305">Press **F5** to run the script.</span></span>
5. <span data-ttu-id="63b6a-306">Sprawdzanie poprawności danych wyjściowych skryptu.</span><span class="sxs-lookup"><span data-stu-id="63b6a-306">Validate the script output.</span></span> <span data-ttu-id="63b6a-307">Upewnij się, że skrypt został uruchomiony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="63b6a-307">Make sure the script ran successfully.</span></span>

## <span data-ttu-id="63b6a-308"><a id="nextsteps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="63b6a-308"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="63b6a-309">Teraz można poznać sposób przekazywania pliku do magazynu obiektów Blob platformy Azure, jak wypełnianie tabeli Hive za pomocą danych z magazynu obiektów Blob platformy Azure, sposób uruchamiania zapytań Hive i sposobu użycia Sqoop do eksportowania danych z systemu plików HDFS do bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="63b6a-309">Now you understand how to upload a file to Azure Blob storage, how to populate a Hive table by using the data from Azure Blob storage, how to run Hive queries, and how to use Sqoop to export data from HDFS to an Azure SQL database.</span></span> <span data-ttu-id="63b6a-310">Aby dowiedzieć się więcej, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="63b6a-310">To learn more, see the following articles:</span></span>

* <span data-ttu-id="63b6a-311">[Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="63b6a-311">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="63b6a-312">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="63b6a-312">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="63b6a-313">[Korzystanie z Oozie z usługą HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="63b6a-313">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="63b6a-314">[Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="63b6a-314">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="63b6a-315">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="63b6a-315">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="63b6a-316">[Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="63b6a-316">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
