---
title: "Zainstalować i używać Giraph na klastrów platformy Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dostosować klastra usługi HDInsight z Giraph i sposobu użycia Giraph."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: f0eb5c1f457380600463a370043f03e6d655a02c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="6ea01-103">Zainstalować i używać Giraph w klastrach HDInsight opartych na systemie Windows</span><span class="sxs-lookup"><span data-stu-id="6ea01-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="6ea01-104">Dowiedz się, jak dostosować klastra usługi HDInsight opartych na systemie Windows za pomocą Giraph za pomocą akcji skryptów i sposobu użycia Giraph przetwarzania dużych wykresów.</span><span class="sxs-lookup"><span data-stu-id="6ea01-104">Learn how to customize Windows based HDInsight cluster with Giraph using Script Action, and how to use Giraph to process large-scale graphs.</span></span> <span data-ttu-id="6ea01-105">Uzyskać informacji o używaniu Giraph z klastra opartych na systemie Linux, zobacz [zainstalować Giraph w klastrach HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6ea01-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ea01-106">Kroki opisane w tym dokumencie pracować tylko z klastrami HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="6ea01-106">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="6ea01-107">HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="6ea01-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="6ea01-108">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="6ea01-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6ea01-109">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="6ea01-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="6ea01-110">Aby uzyskać informacje dotyczące sposobu instalowania Giraph w klastrze usługi HDInsight opartej na systemie Linux, zobacz [zainstalować Giraph w klastrach HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6ea01-110">For information on how to install Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="6ea01-111">Giraph można zainstalować w klastrze (na platformie Hadoop, Storm, HBase, Spark) w usłudze Azure HDInsight dowolnego typu za pomocą *akcji skryptu*.</span><span class="sxs-lookup"><span data-stu-id="6ea01-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="6ea01-112">Przykładowy skrypt do zainstalowania Giraph w klastrze usługi HDInsight jest dostępna z obiektu blob magazynu Azure w trybie tylko do odczytu w [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="6ea01-112">A sample script to install Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="6ea01-113">Przykładowy skrypt działa tylko w przypadku klastra HDInsight w wersji 3.1.</span><span class="sxs-lookup"><span data-stu-id="6ea01-113">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="6ea01-114">Aby uzyskać więcej informacji o wersjach klastra usługi HDInsight, zobacz [wersji klastra usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="6ea01-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="6ea01-115">**Pokrewne artykuły**</span><span class="sxs-lookup"><span data-stu-id="6ea01-115">**Related articles**</span></span>

* [<span data-ttu-id="6ea01-116">Zainstaluj Giraph na klastrów platformy Hadoop w HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="6ea01-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="6ea01-117">[Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-provision-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ea01-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="6ea01-118">[Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="6ea01-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="6ea01-119">[Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="6ea01-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="6ea01-120">Co to jest Giraph?</span><span class="sxs-lookup"><span data-stu-id="6ea01-120">What is Giraph?</span></span>
<span data-ttu-id="6ea01-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> umożliwia wykonywanie wykresu przetwarzanie przy użyciu platformy Hadoop i mogą być używane z usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ea01-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="6ea01-122">Wykresy modelu relacje między obiektami, takimi jak połączeń między routerami w dużych sieci, takich jak Internet lub relacje między osób w sieciach społecznościowych (czasem określana jako społecznościowych wykresu).</span><span class="sxs-lookup"><span data-stu-id="6ea01-122">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span></span> <span data-ttu-id="6ea01-123">Wykres przetwarzania umożliwia przeglądanie informacji o relacje między obiektami na wykresie, takich jak:</span><span class="sxs-lookup"><span data-stu-id="6ea01-123">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="6ea01-124">Identyfikuje potencjalne znajomych oparte na bieżącej relacji.</span><span class="sxs-lookup"><span data-stu-id="6ea01-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="6ea01-125">Identyfikowanie najkrótszy trasy między dwoma komputerami w sieci.</span><span class="sxs-lookup"><span data-stu-id="6ea01-125">Identifying the shortest route between two computers in a network.</span></span>
* <span data-ttu-id="6ea01-126">Obliczanie rangę strony stron sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6ea01-126">Calculating the page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="6ea01-127">Zainstaluj Giraph przy użyciu portalu</span><span class="sxs-lookup"><span data-stu-id="6ea01-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="6ea01-128">Rozpocznij tworzenie klastra przy użyciu **Utwórz niestandardowy** opcji, zgodnie z opisem w [klastrów utworzyć Hadoop w HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="6ea01-128">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="6ea01-129">Na **akcji skryptu** strony kreatora, kliknij przycisk **dodać akcję skryptu** do udostępnienia szczegółów dotyczących akcji skryptu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="6ea01-129">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="6ea01-130">![Aby dostosować klastra, użyj akcji skryptu](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "użyj akcji skryptu, aby dostosować klastra")</span><span class="sxs-lookup"><span data-stu-id="6ea01-130">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="6ea01-131">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6ea01-131">Property</span></span></th><th><span data-ttu-id="6ea01-132">Wartość</span><span class="sxs-lookup"><span data-stu-id="6ea01-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="6ea01-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6ea01-133">Name</span></span></td>
            <td><span data-ttu-id="6ea01-134">Określ nazwę akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="6ea01-134">Specify a name for the script action.</span></span> <span data-ttu-id="6ea01-135">Na przykład <b>zainstalować Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="6ea01-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="6ea01-136">Identyfikator URI skryptu</span><span class="sxs-lookup"><span data-stu-id="6ea01-136">Script URI</span></span></td>
            <td><span data-ttu-id="6ea01-137">Określ identyfikator URI (Uniform Resource) do skryptu, które jest wywoływane, aby dostosować klastra.</span><span class="sxs-lookup"><span data-stu-id="6ea01-137">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="6ea01-138">Na przykład <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="6ea01-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="6ea01-139">Typ węzła</span><span class="sxs-lookup"><span data-stu-id="6ea01-139">Node Type</span></span></td>
            <td><span data-ttu-id="6ea01-140">Określ węzły, na których uruchomiono skryptu dostosowania.</span><span class="sxs-lookup"><span data-stu-id="6ea01-140">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="6ea01-141">Możesz wybrać <b>we wszystkich węzłach</b>, <b>tylko węzły główne</b>, lub <b>tylko węzłów procesu roboczego</b>.</span><span class="sxs-lookup"><span data-stu-id="6ea01-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="6ea01-142">Parametry</span><span class="sxs-lookup"><span data-stu-id="6ea01-142">Parameters</span></span></td>
            <td><span data-ttu-id="6ea01-143">Określ parametry, jeśli jest to wymagane przez skrypt.</span><span class="sxs-lookup"><span data-stu-id="6ea01-143">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="6ea01-144">Skrypt do zainstalowania Giraph nie wymaga żadnych parametrów, więc można to pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="6ea01-144">The script to install Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="6ea01-145">Można dodać więcej niż jedna akcja skryptu, aby zainstalować wiele składników w klastrze.</span><span class="sxs-lookup"><span data-stu-id="6ea01-145">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="6ea01-146">Po dodaniu skryptów, kliknij znacznik wyboru, aby rozpocząć tworzenie klastra.</span><span class="sxs-lookup"><span data-stu-id="6ea01-146">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="6ea01-147">Korzystanie z systemu Giraph</span><span class="sxs-lookup"><span data-stu-id="6ea01-147">Use Giraph</span></span>
<span data-ttu-id="6ea01-148">Możemy użyć przykładowego SimpleShortestPathsComputation pokazują podstawowe <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementacji odnajdywania najkrótszy ścieżki między obiektami na wykresie.</span><span class="sxs-lookup"><span data-stu-id="6ea01-148">We use the SimpleShortestPathsComputation example to demonstrate the basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding the shortest path between objects in a graph.</span></span> <span data-ttu-id="6ea01-149">Przekaż przykładowe dane i jar próbki, uruchom zadanie przy użyciu przykład SimpleShortestPathsComputation, wykonaj następujące kroki, a następnie przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="6ea01-149">Use the following steps to upload the sample data and the sample jar, run a job by using the SimpleShortestPathsComputation example, and then view the results.</span></span>

1. <span data-ttu-id="6ea01-150">Przekaż przykładowy plik danych do magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6ea01-150">Upload a sample data file to Azure Blob storage.</span></span> <span data-ttu-id="6ea01-151">Na lokalnej stacji roboczej, Utwórz nowy plik o nazwie **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="6ea01-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="6ea01-152">Powinien on zawierać następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="6ea01-152">It should contain the following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="6ea01-153">Przekaż plik tiny_graph.txt do podstawowego magazynu dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ea01-153">Upload the tiny_graph.txt file to the primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="6ea01-154">Aby uzyskać instrukcje na temat przekazywania danych, zobacz [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="6ea01-154">For instructions on how to upload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="6ea01-155">Te dane w tym artykule opisano relacje między obiektami w ukierunkowanego wykresu, w formacie [źródła\_identyfikator, źródło\_wartości [[dest\_identyfikator], [krawędzi\_wartość],...]].</span><span class="sxs-lookup"><span data-stu-id="6ea01-155">This data describes a relationship between objects in a directed graph, by using the format [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span></span> <span data-ttu-id="6ea01-156">Każdy wiersz zawiera relację między **źródła\_identyfikator** obiektu i co najmniej jeden **dest\_identyfikator** obiektów.</span><span class="sxs-lookup"><span data-stu-id="6ea01-156">Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="6ea01-157">**Krawędzi\_wartość** (lub wagi) mogą być uważane za siłę lub odległość połączenie między **source_id** i **dest\_identyfikator**.</span><span class="sxs-lookup"><span data-stu-id="6ea01-157">The **edge\_value** (or weight) can be thought of as the strength or distance of the connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="6ea01-158">Rysowane, i przy użyciu wartości (lub wagi) jako odległość między obiektami, powyższe dane może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="6ea01-158">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span></span>

    ![tiny_graph.txt rysowane jako okręgi wiersze z różnymi odległość między](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="6ea01-160">Uruchom przykład SimpleShortestPathsComputation.</span><span class="sxs-lookup"><span data-stu-id="6ea01-160">Run the SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="6ea01-161">Użyj następujących poleceń cmdlet programu Azure PowerShell do uruchamiania w przykładzie przy użyciu pliku tiny_graph.txt jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="6ea01-161">Use the following Azure PowerShell cmdlets to run the example by using the tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6ea01-162">Obsługa programu Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i została usunięta z dniem 1 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="6ea01-162">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="6ea01-163">W czynnościach opisanych w niniejszym dokumencie są używane nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6ea01-163">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="6ea01-164">Wykonaj kroki opisane w temacie [Instalowanie i konfigurowanie środowiska Azure PowerShell](/powershell/azureps-cmdlets-docs), aby zainstalować najnowszą wersję środowiska Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6ea01-164">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="6ea01-165">Jeśli masz skrypty wymagające modyfikacji w celu użycia nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz temat [Migrowanie do narzędzi programistycznych opartych na usłudze Azure Resource Manager w celu obsługi klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md), aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="6ea01-165">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create the definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run the job, write output to the Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="6ea01-166">W powyższym przykładzie Zastąp **clustername** o nazwie z klastrem usługi HDInsight, zawierający Giraph zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="6ea01-166">In the above example, replace **clustername** with the name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="6ea01-167">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="6ea01-167">View the results.</span></span> <span data-ttu-id="6ea01-168">Po zakończeniu zadania, wyniki będą przechowywane w dwóch plikach danych wyjściowych w **wasb: / / / przykład/out/shotestpaths** folderu.</span><span class="sxs-lookup"><span data-stu-id="6ea01-168">Once the job has finished, the results will be stored in two output files in the **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="6ea01-169">Pliki są nazywane **części m-00001** i **części m-00002**.</span><span class="sxs-lookup"><span data-stu-id="6ea01-169">The files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="6ea01-170">Wykonaj poniższe kroki, aby pobrać i wyświetlić dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6ea01-170">Perform the following steps to download and view the output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select the current subscription
    Select-AzureSubscription $subscriptionName

    # Create the Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download the job output to the workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="6ea01-171">Spowoduje to utworzenie **shortestpaths przykład/wyjście** struktura katalogów w bieżącym katalogu na stacji roboczej i pobierania dwa pliki wyjściowe do tej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="6ea01-171">This will create the **example/output/shortestpaths** directory structure in the current directory on your workstation, and download the two output files to that location.</span></span>

    <span data-ttu-id="6ea01-172">Użyj **Cat** polecenia cmdlet, aby wyświetlić zawartość plików:</span><span class="sxs-lookup"><span data-stu-id="6ea01-172">Use the **Cat** cmdlet to display the contents of the files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="6ea01-173">Dane wyjściowe powinny wyglądać podobnie jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="6ea01-173">The output should appear similar to the following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="6ea01-174">SimpleShortestPathComputation, który przykład jest trudna do uruchomienia z kodowanego obiektu ID 1 i znaleźć najkrótszy ścieżki do innych obiektów.</span><span class="sxs-lookup"><span data-stu-id="6ea01-174">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="6ea01-175">Dlatego dane wyjściowe powinny zostać odczytany jako `destination_id distance`, gdzie odległości jest wartość (lub wagi) krawędzi przemieścić się między obiektu ID 1 i identyfikatora docelowego.</span><span class="sxs-lookup"><span data-stu-id="6ea01-175">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="6ea01-176">Ta wizualizacja, można sprawdzić wyniki za podróży najkrótszy ścieżek między 1 Identyfikatora i wszystkie inne obiekty.</span><span class="sxs-lookup"><span data-stu-id="6ea01-176">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="6ea01-177">Należy pamiętać, że najkrótszy ścieżki między ID 1 i 4 identyfikator 5.</span><span class="sxs-lookup"><span data-stu-id="6ea01-177">Note that the shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="6ea01-178">Jest to całkowita liczba odległość między <span style="color:orange">ID 1 i 3</span>, a następnie <span style="color:red">identyfikator 3 i 4</span>.</span><span class="sxs-lookup"><span data-stu-id="6ea01-178">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Rysowanie obiektów jako kółka za pomocą najmniejszej ścieżek między](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="6ea01-180">Zainstaluj Giraph przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ea01-180">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="6ea01-181">Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="6ea01-181">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="6ea01-182">Przykład pokazuje, jak zainstalować Spark przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6ea01-182">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="6ea01-183">Należy dostosować skrypt, aby użyć [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="6ea01-183">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="6ea01-184">Zainstaluj Giraph przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6ea01-184">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="6ea01-185">Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="6ea01-185">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="6ea01-186">Przykład pokazuje, jak zainstalować Spark przy użyciu zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="6ea01-186">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="6ea01-187">Należy dostosować skrypt, aby użyć [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="6ea01-187">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="6ea01-188">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6ea01-188">See also</span></span>
* [<span data-ttu-id="6ea01-189">Zainstaluj Giraph na klastrów platformy Hadoop w HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="6ea01-189">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="6ea01-190">[Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-provision-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6ea01-190">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="6ea01-191">[Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="6ea01-191">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="6ea01-192">[Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="6ea01-192">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="6ea01-193">[Zainstalować i używać platformy Spark w klastrach HDInsight][hdinsight-install-spark]: Akcja skryptu próbki o instalowaniu Spark.</span><span class="sxs-lookup"><span data-stu-id="6ea01-193">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="6ea01-194">[Zainstalować język R w klastrach HDInsight][hdinsight-install-r]: Akcja skryptu próbki o instalowaniu R.</span><span class="sxs-lookup"><span data-stu-id="6ea01-194">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="6ea01-195">[Zainstaluj w klastrach HDInsight Solr](hdinsight-hadoop-solr-install.md): Akcja skryptu próbki o instalowaniu Solr.</span><span class="sxs-lookup"><span data-stu-id="6ea01-195">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
