---
title: "Użyj języka R w usłudze HDInsight, aby dostosować klastry - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zainstalować język R za pomocą akcji skryptu, a następnie użyj języka R w klastrach usługi HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 5b9b793d49217acd9f0c6c518596a7afb5600d69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="e1d66-103">Instalowanie i używanie języka R w klastrach usługi Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1d66-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="e1d66-104">Dowiedz się, dostosowywanie systemu Windows na podstawie klastra usługi HDInsight przy użyciu akcji skryptu języka R i sposobu użycia języka R w usłudze HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="e1d66-104">Learn how to customize Windows based HDInsight cluster with R using Script Action, and how to use R on HDInsight clusters.</span></span> <span data-ttu-id="e1d66-105">[Oferty HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) obejmuje R Server w ramach klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1d66-105">The [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="e1d66-106">Dzięki temu R skryptów na potrzeby uruchamiania rozproszone obliczenia MapReduce i Spark.</span><span class="sxs-lookup"><span data-stu-id="e1d66-106">This allows R scripts to use MapReduce and Spark to run distributed computations.</span></span> <span data-ttu-id="e1d66-107">Aby uzyskać więcej informacji, zobacz temat [Rozpoczęcie pracy z platformą R Server w usłudze HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e1d66-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="e1d66-108">Uzyskać informacji na temat używania R z systemem Linux klastrem, zobacz [instalacji i używania R w klastrach HDinsight Hadoop (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e1d66-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="e1d66-109">Można zainstalować język R w klastrze (na platformie Hadoop, Storm, HBase, Spark) w usłudze Azure HDInsight dowolnego typu za pomocą *akcji skryptu*.</span><span class="sxs-lookup"><span data-stu-id="e1d66-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="e1d66-110">Przykładowy skrypt, aby zainstalować język R w klastrze usługi HDInsight jest dostępna z obiektu blob magazynu Azure w trybie tylko do odczytu w [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="e1d66-110">A sample script to install R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="e1d66-111">**Pokrewne artykuły**</span><span class="sxs-lookup"><span data-stu-id="e1d66-111">**Related articles**</span></span>

* [<span data-ttu-id="e1d66-112">Zainstaluj i użyj języka R w klastrach HDinsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="e1d66-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="e1d66-113">[Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1d66-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="e1d66-114">[Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="e1d66-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="e1d66-115">Tworzenie skryptów akcji skryptu dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1d66-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="e1d66-116">Co to jest R?</span><span class="sxs-lookup"><span data-stu-id="e1d66-116">What is R?</span></span>
<span data-ttu-id="e1d66-117"><a href="http://www.r-project.org/" target="_blank">R projektu do statystycznego przetwarzania danych</a> jest otwarty języka źródłowego i środowiska do statystycznego przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="e1d66-117">The <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="e1d66-118">R zawiera setki kompilacji funkcji statystycznych i własnej język programowania, łączącą aspekty funkcjonalne i zorientowanym obiektowo programowania.</span><span class="sxs-lookup"><span data-stu-id="e1d66-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="e1d66-119">Umożliwia także rozbudowane funkcje graficzne.</span><span class="sxs-lookup"><span data-stu-id="e1d66-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="e1d66-120">R jest preferowanym środowisko programowania najbardziej professional chi i służące w wielu różnych pól.</span><span class="sxs-lookup"><span data-stu-id="e1d66-120">R is the preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="e1d66-121">R jest zgodny z magazynu obiektów Blob Azure (WASB), aby dane przechowywane mogą być przetwarzane przy użyciu języka R w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1d66-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="e1d66-122">Zainstalować język R</span><span class="sxs-lookup"><span data-stu-id="e1d66-122">Install R</span></span>
<span data-ttu-id="e1d66-123">A [przykładowy skrypt](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) zainstalować język R w usłudze HDInsight klastra jest dostępny w trybie tylko do odczytu obiektów blob w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e1d66-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) to install R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="e1d66-124">Ta sekcja zawiera instrukcje dotyczące sposobu użyć przykładowego skryptu podczas tworzenia klastra przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d66-124">This section provides instructions about how to use the sample script while creating the cluster using the Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="e1d66-125">Przykładowy skrypt został wprowadzony z klastra usługi HDInsight w wersji 3.1.</span><span class="sxs-lookup"><span data-stu-id="e1d66-125">The sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="e1d66-126">Aby uzyskać więcej informacji o wersjach klastra usługi HDInsight, zobacz [wersji klastra usługi HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e1d66-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="e1d66-127">Podczas tworzenia klastra usługi HDInsight w portalu, kliknij przycisk **konfiguracji opcjonalnej**, a następnie kliknij przycisk **akcji skryptu**.</span><span class="sxs-lookup"><span data-stu-id="e1d66-127">When you create an HDInsight cluster from the Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="e1d66-128">Na **akcji skryptu** strony, wprowadź następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="e1d66-128">On the **Script Actions** page, enter the following values:</span></span>

    <span data-ttu-id="e1d66-129">![Aby dostosować klastra, użyj akcji skryptu](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "użyj akcji skryptu, aby dostosować klastra")</span><span class="sxs-lookup"><span data-stu-id="e1d66-129">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="e1d66-130">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e1d66-130">Property</span></span></th><th><span data-ttu-id="e1d66-131">Wartość</span><span class="sxs-lookup"><span data-stu-id="e1d66-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="e1d66-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e1d66-132">Name</span></span></td>
            <td><span data-ttu-id="e1d66-133">Na przykład określić nazwę akcji skryptu <b>zainstalować R</b>.</span><span class="sxs-lookup"><span data-stu-id="e1d66-133">Specify a name for the script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="e1d66-134">Identyfikator URI skryptu</span><span class="sxs-lookup"><span data-stu-id="e1d66-134">Script URI</span></span></td>
            <td><span data-ttu-id="e1d66-135">Określ identyfikator URI do skryptu, które jest wywoływane, aby dostosować klastra, na przykład <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span><span class="sxs-lookup"><span data-stu-id="e1d66-135">Specify the URI to the script that is invoked to customize the cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="e1d66-136">Typ węzła</span><span class="sxs-lookup"><span data-stu-id="e1d66-136">Node Type</span></span></td>
            <td><span data-ttu-id="e1d66-137">Określ węzły, na których uruchomiono skryptu dostosowania.</span><span class="sxs-lookup"><span data-stu-id="e1d66-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="e1d66-138">Możesz wybrać <b>we wszystkich węzłach</b>, <b>tylko węzły główne</b>, lub <b>węzłów procesu roboczego</b> tylko.</span><span class="sxs-lookup"><span data-stu-id="e1d66-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="e1d66-139">Parametry</span><span class="sxs-lookup"><span data-stu-id="e1d66-139">Parameters</span></span></td>
            <td><span data-ttu-id="e1d66-140">Określ parametry, jeśli jest to wymagane przez skrypt.</span><span class="sxs-lookup"><span data-stu-id="e1d66-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="e1d66-141">Jednak skryptu, aby zainstalować język R nie wymaga żadnych parametrów, dzięki czemu można to pole pozostanie puste.</span><span class="sxs-lookup"><span data-stu-id="e1d66-141">However, the script to install R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="e1d66-142">Można dodać więcej niż jedna akcja skryptu, aby zainstalować wiele składników w klastrze.</span><span class="sxs-lookup"><span data-stu-id="e1d66-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="e1d66-143">Po dodaniu skryptów, kliknij znacznik wyboru, aby uruchomić crating klastra.</span><span class="sxs-lookup"><span data-stu-id="e1d66-143">After you have added the scripts, click the check mark to start crating the cluster.</span></span>

<span data-ttu-id="e1d66-144">Można także użyć skryptu zainstalować język R w usłudze HDInsight przy użyciu programu Azure PowerShell lub zestawu .NET SDK usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1d66-144">You can also use the script to install R on HDInsight by using Azure PowerShell or the HDInsight .NET SDK.</span></span> <span data-ttu-id="e1d66-145">Instrukcje dotyczące tych procedur znajdują się w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="e1d66-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="e1d66-146">Uruchom skrypty języka R</span><span class="sxs-lookup"><span data-stu-id="e1d66-146">Run R scripts</span></span>
<span data-ttu-id="e1d66-147">W tej sekcji opisano sposób uruchamiania skryptu języka R w klastrze Hadoop z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1d66-147">This section describes how to run an R script on the Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="e1d66-148">**Ustanów połączenie pulpitu zdalnego w klastrze**: Z portalu włączenie pulpitu zdalnego dla klastra zostały utworzone z języka R zainstalowanego, a następnie połącz się z klastrem.</span><span class="sxs-lookup"><span data-stu-id="e1d66-148">**Establish a Remote Desktop connection to the cluster**: From the Portal, enable Remote Desktop for the cluster you created with R installed, and then connect to the cluster.</span></span> <span data-ttu-id="e1d66-149">Aby uzyskać instrukcje, zobacz [Connect do klastrów usługi HDInsight za pomocą protokołu RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="e1d66-149">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="e1d66-150">**Otwórz konsolę R**: instalacji języka R umieszcza łącze do konsoli R na pulpicie węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="e1d66-150">**Open the R console**: The R installation puts a link to the R console on the desktop of the head node.</span></span> <span data-ttu-id="e1d66-151">Kliknij, aby otworzyć konsolę R.</span><span class="sxs-lookup"><span data-stu-id="e1d66-151">Click on it to open the R console.</span></span>
3. <span data-ttu-id="e1d66-152">**Uruchom skrypt języka R**: skrypt języka R można uruchomić bezpośrednio z konsoli R wklejenie go, wybierając ją i naciskając klawisz ENTER.</span><span class="sxs-lookup"><span data-stu-id="e1d66-152">**Run the R script**: The R script can be run directly from the R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="e1d66-153">Poniżej przedstawiono prosty przykład skrypt generuje liczb od 1 do 100 i mnoży je przez 2.</span><span class="sxs-lookup"><span data-stu-id="e1d66-153">Here is a simple example script that generates the numbers 1 to 100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="e1d66-154">Pierwsze dwa wiersze wywołania bibliotek RHadoop, które są instalowane z R. Końcowego wiersza drukuje wyniki w konsoli.</span><span class="sxs-lookup"><span data-stu-id="e1d66-154">The first two lines call the RHadoop libraries that are installed with R. The final line prints the results to the console.</span></span> <span data-ttu-id="e1d66-155">Dane wyjściowe powinny wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e1d66-155">The output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="e1d66-156">Zainstalować język R przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1d66-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="e1d66-157">Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="e1d66-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="e1d66-158">Przykład pokazuje, jak zainstalować Spark przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1d66-158">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="e1d66-159">Należy dostosować skrypt, aby użyć [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="e1d66-159">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="e1d66-160">Zainstalować język R przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e1d66-160">Install R using .NET SDK</span></span>
<span data-ttu-id="e1d66-161">Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="e1d66-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="e1d66-162">Przykład pokazuje, jak zainstalować Spark przy użyciu zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="e1d66-162">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="e1d66-163">Należy dostosować skrypt, aby użyć [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span><span class="sxs-lookup"><span data-stu-id="e1d66-163">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="e1d66-164">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e1d66-164">See also</span></span>
* [<span data-ttu-id="e1d66-165">Zainstaluj i użyj języka R w klastrach HDinsight Hadoop (Linux)</span><span class="sxs-lookup"><span data-stu-id="e1d66-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="e1d66-166">[Tworzenie klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md): ogólne informacje na temat tworzenia klastrów usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1d66-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="e1d66-167">[Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu][hdinsight-cluster-customize]: ogólne informacje na temat Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="e1d66-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="e1d66-168">Tworzenie skryptów akcji skryptu dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="e1d66-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="e1d66-169">[Zainstalować i używać platformy Spark w klastrach HDInsight][hdinsight-install-spark]: Akcja skryptu próbki o instalowaniu Spark</span><span class="sxs-lookup"><span data-stu-id="e1d66-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="e1d66-170">[Zainstaluj w klastrach HDInsight Giraph](hdinsight-hadoop-giraph-install.md): Akcja skryptu próbki o instalowaniu Giraph</span><span class="sxs-lookup"><span data-stu-id="e1d66-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="e1d66-171">[Zainstaluj w klastrach HDInsight Solr](hdinsight-hadoop-solr-install-linux.md): Akcja skryptu próbki o instalowaniu Solr.</span><span class="sxs-lookup"><span data-stu-id="e1d66-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
