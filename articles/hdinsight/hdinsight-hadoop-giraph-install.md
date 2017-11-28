---
title: "aaaInstall i użyj Giraph na platformie Hadoop clusters w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klaster toocustomize HDInsight z Giraph i jak toouse Giraph."
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
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="1577b-103">Zainstalować i używać Giraph w klastrach HDInsight opartych na systemie Windows</span><span class="sxs-lookup"><span data-stu-id="1577b-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="1577b-104">Dowiedz się, jak toocustomize systemu Windows na podstawie klastra usługi HDInsight przy użyciu akcji skryptu Giraph i jak toouse Giraph tooprocess dużych wykresów.</span><span class="sxs-lookup"><span data-stu-id="1577b-104">Learn how toocustomize Windows based HDInsight cluster with Giraph using Script Action, and how toouse Giraph tooprocess large-scale graphs.</span></span> <span data-ttu-id="1577b-105">Uzyskać informacji o używaniu Giraph z klastra opartych na systemie Linux, zobacz [zainstalować Giraph w klastrach HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1577b-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1577b-106">Witaj czynnościach w ramach tego dokumentu działać tylko w przypadku klastrów usługi HDInsight opartych na systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="1577b-106">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1577b-107">HDInsight jest dostępna tylko w systemie Windows dla wersji starszej niż HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="1577b-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="1577b-108">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1577b-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1577b-109">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="1577b-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="1577b-110">Aby uzyskać informacje na temat tooinstall Giraph w klastrze usługi HDInsight opartej na systemie Linux, zobacz [zainstalować Giraph w klastrach HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1577b-110">For information on how tooinstall Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="1577b-111">Giraph można zainstalować w klastrze (na platformie Hadoop, Storm, HBase, Spark) w usłudze Azure HDInsight dowolnego typu za pomocą *akcji skryptu*.</span><span class="sxs-lookup"><span data-stu-id="1577b-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="1577b-112">Przykładowy skrypt tooinstall Giraph w klastrze usługi HDInsight jest dostępna z obiektu blob magazynu Azure w trybie tylko do odczytu w [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="1577b-112">A sample script tooinstall Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="1577b-113">Witaj przykładowy skrypt działa tylko w przypadku klastra HDInsight w wersji 3.1.</span><span class="sxs-lookup"><span data-stu-id="1577b-113">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="1577b-114">Aby uzyskać więcej informacji o wersjach klastra usługi HDInsight, zobacz [wersji klastra usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="1577b-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="1577b-115">**Pokrewne artykuły**</span><span class="sxs-lookup"><span data-stu-id="1577b-115">**Related articles**</span></span>

* [<span data-ttu-id="1577b-116">Zainstaluj Giraph na klastrów platformy Hadoop w HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="1577b-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="1577b-117">[Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-provision-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1577b-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="1577b-118">[Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="1577b-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="1577b-119">[Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="1577b-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="1577b-120">Co to jest Giraph?</span><span class="sxs-lookup"><span data-stu-id="1577b-120">What is Giraph?</span></span>
<span data-ttu-id="1577b-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> pozwala wykres tooperform przetwarzanie przy użyciu platformy Hadoop i mogą być używane z usługi Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1577b-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="1577b-122">Wykresy modelu relacje między obiektami, takimi jak hello połączeń między routerami w dużych sieci, takich jak Internet, hello lub relacje między osoby w sieciach społecznościowych (czasami określonego tooas społecznościowych wykres).</span><span class="sxs-lookup"><span data-stu-id="1577b-122">Graphs model relationships between objects, such as hello connections between routers on a large network like hello Internet, or relationships between people on social networks (sometimes referred tooas a social graph).</span></span> <span data-ttu-id="1577b-123">Wykres przetwarzania pozwala tooreason o hello relacje między obiektami na wykresie, takich jak:</span><span class="sxs-lookup"><span data-stu-id="1577b-123">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="1577b-124">Identyfikuje potencjalne znajomych oparte na bieżącej relacji.</span><span class="sxs-lookup"><span data-stu-id="1577b-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="1577b-125">Identyfikowanie hello najkrótszy trasy między dwoma komputerami w sieci.</span><span class="sxs-lookup"><span data-stu-id="1577b-125">Identifying hello shortest route between two computers in a network.</span></span>
* <span data-ttu-id="1577b-126">Obliczanie rangę strony hello stron sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1577b-126">Calculating hello page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="1577b-127">Zainstaluj Giraph przy użyciu portalu</span><span class="sxs-lookup"><span data-stu-id="1577b-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="1577b-128">Rozpocznij tworzenie klastra przy użyciu hello **Utwórz niestandardowy** opcji, zgodnie z opisem w [klastrów utworzyć Hadoop w HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1577b-128">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="1577b-129">Na powitania **akcji skryptu** strony kreatora powitania kliknij przycisk **dodać akcję skryptu** tooprovide szczegółowych informacji o hello akcji skryptu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="1577b-129">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="1577b-130">![Użyj akcji skryptu toocustomize klastra](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize akcji skryptu Użyj klastra")</span><span class="sxs-lookup"><span data-stu-id="1577b-130">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="1577b-131">Właściwość</span><span class="sxs-lookup"><span data-stu-id="1577b-131">Property</span></span></th><th><span data-ttu-id="1577b-132">Wartość</span><span class="sxs-lookup"><span data-stu-id="1577b-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="1577b-133">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1577b-133">Name</span></span></td>
            <td><span data-ttu-id="1577b-134">Określ nazwę hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="1577b-134">Specify a name for hello script action.</span></span> <span data-ttu-id="1577b-135">Na przykład <b>zainstalować Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="1577b-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="1577b-136">Identyfikator URI skryptu</span><span class="sxs-lookup"><span data-stu-id="1577b-136">Script URI</span></span></td>
            <td><span data-ttu-id="1577b-137">Określ hello identyfikator URI (Uniform Resource) toohello skrypt, który jest wywołana toocustomize hello klastra.</span><span class="sxs-lookup"><span data-stu-id="1577b-137">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="1577b-138">Na przykład <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="1577b-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="1577b-139">Typ węzła</span><span class="sxs-lookup"><span data-stu-id="1577b-139">Node Type</span></span></td>
            <td><span data-ttu-id="1577b-140">Określ hello węzłów, na których uruchomiono hello dostosowywania skryptu.</span><span class="sxs-lookup"><span data-stu-id="1577b-140">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="1577b-141">Możesz wybrać <b>we wszystkich węzłach</b>, <b>tylko węzły główne</b>, lub <b>tylko węzłów procesu roboczego</b>.</span><span class="sxs-lookup"><span data-stu-id="1577b-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="1577b-142">Parametry</span><span class="sxs-lookup"><span data-stu-id="1577b-142">Parameters</span></span></td>
            <td><span data-ttu-id="1577b-143">Określ parametry hello, jeśli są wymagane przez skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="1577b-143">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="1577b-144">Hello skryptu tooinstall Giraph nie wymaga żadnych parametrów, więc można to pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="1577b-144">hello script tooinstall Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="1577b-145">Więcej niż jeden tooinstall akcji skryptu można dodać wiele składników w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="1577b-145">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="1577b-146">Po dodaniu hello skryptów, kliknij przycisk toostart znacznikiem wyboru hello tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="1577b-146">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="1577b-147">Korzystanie z systemu Giraph</span><span class="sxs-lookup"><span data-stu-id="1577b-147">Use Giraph</span></span>
<span data-ttu-id="1577b-148">Używamy hello SimpleShortestPathsComputation przykład toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementacji do znajdowania hello najkrótszy ścieżki między obiektami na wykresie.</span><span class="sxs-lookup"><span data-stu-id="1577b-148">We use hello SimpleShortestPathsComputation example toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding hello shortest path between objects in a graph.</span></span> <span data-ttu-id="1577b-149">Użyj hello następujące kroki tooupload hello przykładowych danych i hello próbki jar, uruchomienie zadania przy użyciu przykład SimpleShortestPathsComputation Witaj, a następnie Wyświetl hello wyniki.</span><span class="sxs-lookup"><span data-stu-id="1577b-149">Use hello following steps tooupload hello sample data and hello sample jar, run a job by using hello SimpleShortestPathsComputation example, and then view hello results.</span></span>

1. <span data-ttu-id="1577b-150">Przekaż przykładowe tooAzure plik danych magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="1577b-150">Upload a sample data file tooAzure Blob storage.</span></span> <span data-ttu-id="1577b-151">Na lokalnej stacji roboczej, Utwórz nowy plik o nazwie **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="1577b-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="1577b-152">Powinien on zawierać hello następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="1577b-152">It should contain hello following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="1577b-153">Przekaż hello tiny_graph.txt toohello podstawowego magazynu plików dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1577b-153">Upload hello tiny_graph.txt file toohello primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="1577b-154">Aby uzyskać instrukcje na temat danych tooupload, zobacz [przekazywanie danych dotyczących zadań Hadoop w usłudze HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="1577b-154">For instructions on how tooupload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="1577b-155">Te dane w tym artykule opisano relacje między obiektami w ukierunkowanego wykresu, używając formatu hello [źródła\_identyfikator, źródło\_wartość [[dest\_identyfikator], [krawędzi\_wartość],...]]. Każdy wiersz zawiera relację między **źródła\_identyfikator** obiektu i co najmniej jeden **dest\_identyfikator** obiektów.</span><span class="sxs-lookup"><span data-stu-id="1577b-155">This data describes a relationship between objects in a directed graph, by using hello format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="1577b-156">Witaj **krawędzi\_wartość** (lub wagi) można traktować jako siły hello lub odległość hello połączenie między **source_id** i **dest\_identyfikator**.</span><span class="sxs-lookup"><span data-stu-id="1577b-156">hello **edge\_value** (or weight) can be thought of as hello strength or distance of hello connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="1577b-157">Rysowane, i przy użyciu wartości hello (lub wagi) jako hello odległość między obiektami, hello powyżej danych może wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="1577b-157">Drawn out, and using hello value (or weight) as hello distance between objects, hello above data might look like this:</span></span>

    ![tiny_graph.txt rysowane jako okręgi wiersze z różnymi odległość między](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="1577b-159">Uruchom przykład Witaj SimpleShortestPathsComputation.</span><span class="sxs-lookup"><span data-stu-id="1577b-159">Run hello SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="1577b-160">Użyj powitania po przykład Witaj toorun poleceń cmdlet programu Azure PowerShell przy użyciu pliku tiny_graph.txt hello jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="1577b-160">Use hello following Azure PowerShell cmdlets toorun hello example by using hello tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1577b-161">Obsługa programu Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i została usunięta z dniem 1 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="1577b-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="1577b-162">Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1577b-162">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="1577b-163">Wykonaj kroki hello [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello najnowszą wersję programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1577b-163">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="1577b-164">Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="1577b-164">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

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
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="1577b-165">W hello powyżej przykładzie, Zastąp **clustername** o nazwie hello klastra usługi HDInsight, zawierający Giraph zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="1577b-165">In hello above example, replace **clustername** with hello name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="1577b-166">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="1577b-166">View hello results.</span></span> <span data-ttu-id="1577b-167">Po zakończeniu zadania hello hello wyniki będą przechowywane w dwóch plikach danych wyjściowych w hello **wasb: / / / przykład/out/shotestpaths** folderu.</span><span class="sxs-lookup"><span data-stu-id="1577b-167">Once hello job has finished, hello results will be stored in two output files in hello **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="1577b-168">Witaj plików są nazywane **części m-00001** i **części m-00002**.</span><span class="sxs-lookup"><span data-stu-id="1577b-168">hello files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="1577b-169">Wykonaj następujące kroki toodownload i widoku wyjściowego hello hello:</span><span class="sxs-lookup"><span data-stu-id="1577b-169">Perform hello following steps toodownload and view hello output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="1577b-170">Spowoduje to utworzenie hello **shortestpaths przykład/wyjście** struktura katalogów w bieżącym katalogu hello na stacji roboczej i Witaj dwie dane wyjściowe pliki toothat lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="1577b-170">This will create hello **example/output/shortestpaths** directory structure in hello current directory on your workstation, and download hello two output files toothat location.</span></span>

    <span data-ttu-id="1577b-171">Użyj hello **Cat** polecenia cmdlet toodisplay hello zawartość plików hello:</span><span class="sxs-lookup"><span data-stu-id="1577b-171">Use hello **Cat** cmdlet toodisplay hello contents of hello files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="1577b-172">dane wyjściowe Hello powinna zostać wyświetlona podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="1577b-172">hello output should appear similar toohello following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="1577b-173">przykład Witaj SimpleShortestPathComputation jest zakodowany toostart z obiektem ID 1 i Znajdź hello najkrótszy ścieżki tooother obiektów.</span><span class="sxs-lookup"><span data-stu-id="1577b-173">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="1577b-174">Dlatego hello dane wyjściowe powinny zostać odczytany jako `destination_id distance`, gdzie odległości jest wartość hello (lub wagi) krawędzi hello pokonać między obiektu ID 1 i identyfikatora hello docelowej.</span><span class="sxs-lookup"><span data-stu-id="1577b-174">So hello output should be read as `destination_id distance`, where distance is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="1577b-175">Wizualizacja to, możesz sprawdzić wyniki hello przez podróży hello najkrótszy ścieżek między 1 Identyfikatora i wszystkie inne obiekty.</span><span class="sxs-lookup"><span data-stu-id="1577b-175">Visualizing this, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="1577b-176">Należy pamiętać, że hello najkrótszy ścieżki między ID 1 i 4 identyfikator wynosi 5.</span><span class="sxs-lookup"><span data-stu-id="1577b-176">Note that hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="1577b-177">Jest to hello całkowita odległość między <span style="color:orange">ID 1 i 3</span>, a następnie <span style="color:red">identyfikator 3 i 4</span>.</span><span class="sxs-lookup"><span data-stu-id="1577b-177">This is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Rysowanie obiektów jako kółka za pomocą najmniejszej ścieżek między](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="1577b-179">Zainstaluj Giraph przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1577b-179">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="1577b-180">Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="1577b-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="1577b-181">Witaj w przykładzie pokazano, jak tooinstall Spark przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1577b-181">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="1577b-182">Należy toocustomize hello skryptu toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="1577b-182">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="1577b-183">Zainstaluj Giraph przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1577b-183">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="1577b-184">Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="1577b-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="1577b-185">Witaj w przykładzie pokazano, jak tooinstall Spark przy użyciu hello zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="1577b-185">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="1577b-186">Należy toocustomize hello skryptu toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="1577b-186">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="1577b-187">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1577b-187">See also</span></span>
* [<span data-ttu-id="1577b-188">Zainstaluj Giraph na klastrów platformy Hadoop w HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="1577b-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="1577b-189">[Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-provision-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1577b-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="1577b-190">[Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="1577b-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="1577b-191">[Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="1577b-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="1577b-192">[Zainstalować i używać platformy Spark w klastrach HDInsight][hdinsight-install-spark]: Akcja skryptu próbki o instalowaniu Spark.</span><span class="sxs-lookup"><span data-stu-id="1577b-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="1577b-193">[Zainstalować język R w klastrach HDInsight][hdinsight-install-r]: Akcja skryptu próbki o instalowaniu R.</span><span class="sxs-lookup"><span data-stu-id="1577b-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="1577b-194">[Zainstaluj w klastrach HDInsight Solr](hdinsight-hadoop-solr-install.md): Akcja skryptu próbki o instalowaniu Solr.</span><span class="sxs-lookup"><span data-stu-id="1577b-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
