---
title: "Tworzenie klastrów Hadoop przy użyciu programu PowerShell - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć klastry Hadoop, HBase, Storm i Spark w systemie Linux dla usługi HDInsight przy użyciu programu Azure PowerShell."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ca75974e6ec4f60739137d4cb5458bbfd735de3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="9108c-103">Tworzenie klastrów z systemem Linux w usłudze HDInsight przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9108c-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="9108c-104">Program Azure PowerShell jest zaawansowane środowisko obsługi skryptów, który służy do kontrolowania i automatyzowania wdrażania i zarządzania obciążeń w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9108c-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="9108c-105">Ten dokument zawiera informacje o sposobie tworzenia klastra usługi HDInsight opartej na systemie Linux przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9108c-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="9108c-106">Zawiera również przykład skryptu.</span><span class="sxs-lookup"><span data-stu-id="9108c-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="9108c-107">Program Azure PowerShell jest dostępny tylko na komputerach klienckich z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="9108c-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="9108c-108">Jeśli używasz klienta systemu Linux, Unix lub Mac OS X, zobacz [tworzenia klastra usługi HDInsight opartej na systemie Linux przy użyciu interfejsu wiersza polecenia Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) informacji o przy użyciu wiersza polecenia platformy Azure, aby utworzyć klaster.</span><span class="sxs-lookup"><span data-stu-id="9108c-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9108c-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9108c-109">Prerequisites</span></span>
<span data-ttu-id="9108c-110">Musi mieć następujące przed rozpoczęciem tej procedury:</span><span class="sxs-lookup"><span data-stu-id="9108c-110">You must have the following before starting this procedure:</span></span>

* <span data-ttu-id="9108c-111">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9108c-111">An Azure subscription.</span></span> <span data-ttu-id="9108c-112">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9108c-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="9108c-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9108c-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="9108c-114">Obsługa programu Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i została usunięta z dniem 1 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="9108c-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="9108c-115">W czynnościach opisanych w niniejszym dokumencie są używane nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9108c-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="9108c-116">Wykonaj kroki opisane w [instalacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) do zainstalowania najnowszej wersji programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9108c-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="9108c-117">Jeśli masz skrypty wymagające modyfikacji w celu użycia nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz temat [Migrowanie do narzędzi programistycznych opartych na usłudze Azure Resource Manager w celu obsługi klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md), aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="9108c-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="9108c-118">Tworzenie klastra</span><span class="sxs-lookup"><span data-stu-id="9108c-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="9108c-119">Aby utworzyć klaster usługi HDInsight przy użyciu programu Azure PowerShell, należy wykonać następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="9108c-119">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span></span>

* <span data-ttu-id="9108c-120">Tworzenie grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9108c-120">Create an Azure resource group</span></span>
* <span data-ttu-id="9108c-121">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9108c-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="9108c-122">Tworzenie kontenera obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9108c-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="9108c-123">Tworzenie klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="9108c-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="9108c-124">Poniższy skrypt pokazuje, jak utworzyć nowy klaster:</span><span class="sxs-lookup"><span data-stu-id="9108c-124">The following script demonstrates how to create a new cluster:</span></span>

<span data-ttu-id="9108c-125">[!code-powershell[główne](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span><span class="sxs-lookup"><span data-stu-id="9108c-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span></span>

<span data-ttu-id="9108c-126">Wartości określone dla logowania do klastra są używane do utworzenia konta użytkownika platformy Hadoop dla klastra.</span><span class="sxs-lookup"><span data-stu-id="9108c-126">The values you specify for the cluster login are used to create the Hadoop user account for the cluster.</span></span> <span data-ttu-id="9108c-127">Podłącz do usług hostowanych w klastrze, takich jak web UI lub interfejsów API REST za pomocą tego konta.</span><span class="sxs-lookup"><span data-stu-id="9108c-127">Use this account to connect to services hosted on the cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="9108c-128">Wartości określone dla użytkownika SSH są używane do utworzenia użytkownika SSH dla klastra.</span><span class="sxs-lookup"><span data-stu-id="9108c-128">The values you specify for the SSH user are used to create the SSH user for the cluster.</span></span> <span data-ttu-id="9108c-129">Aby uruchomić sesję zdalną SSH w klastrze i uruchom zadania, należy użyć tego konta.</span><span class="sxs-lookup"><span data-stu-id="9108c-129">Use this account to start a remote SSH session on the cluster and run jobs.</span></span> <span data-ttu-id="9108c-130">Aby uzyskać więcej informacji, zobacz dokument [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9108c-130">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9108c-131">Jeśli planujesz użyć więcej niż 32 węzłami procesów roboczych (lub podczas tworzenia klastra przez skalowanie klastra po utworzeniu), należy również określić rozmiaru węzła głównego z co najmniej 8 rdzeniami i 14 GB pamięci RAM.</span><span class="sxs-lookup"><span data-stu-id="9108c-131">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="9108c-132">Aby uzyskać więcej informacji na węzeł rozmiary i koszty, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9108c-132">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="9108c-133">Może upłynąć do 20 minut na utworzenie klastra.</span><span class="sxs-lookup"><span data-stu-id="9108c-133">It can take up to 20 minutes to create a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="9108c-134">Tworzenie klastra: obiekt konfiguracji</span><span class="sxs-lookup"><span data-stu-id="9108c-134">Create cluster: Configuration object</span></span>

<span data-ttu-id="9108c-135">Można również utworzyć HDInsight konfiguracji obiektów przy użyciu `New-AzureRmHDInsightClusterConfig` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9108c-135">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="9108c-136">Następnie można zmodyfikować ten obiekt konfiguracji, aby włączyć dodatkowe opcje konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="9108c-136">You can then modify this configuration object to enable additional configuration options for your cluster.</span></span> <span data-ttu-id="9108c-137">Na koniec użyj `-Config` parametr `New-AzureRmHDInsightCluster` polecenia cmdlet do korzystania z konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9108c-137">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span></span>

<span data-ttu-id="9108c-138">Poniższy skrypt tworzy obiekt konfiguracji, aby skonfigurować serwer R na typ klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9108c-138">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="9108c-139">Konfiguracja umożliwia węzeł krawędzi, programu RStudio i konta dodatkowego miejsca do magazynowania.</span><span class="sxs-lookup"><span data-stu-id="9108c-139">The configuration enables an edge node, RStudio, and an additional storage account.</span></span>

<span data-ttu-id="9108c-140">[!code-powershell[główne](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span><span class="sxs-lookup"><span data-stu-id="9108c-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span></span>

> [!WARNING]
> <span data-ttu-id="9108c-141">Używanie konta magazynu w innej lokalizacji niż klastra usługi HDInsight nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="9108c-141">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span> <span data-ttu-id="9108c-142">Korzystając z tego przykładu, należy utworzyć konto dodatkowego magazynu w tej samej lokalizacji co serwer.</span><span class="sxs-lookup"><span data-stu-id="9108c-142">When using this example, create the additional storage account in the same location as the server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="9108c-143">Dostosowywanie klastrów</span><span class="sxs-lookup"><span data-stu-id="9108c-143">Customize clusters</span></span>

* <span data-ttu-id="9108c-144">Zobacz [HDInsight dostosować klastry za pomocą początkowego](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="9108c-144">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="9108c-145">Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9108c-145">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="9108c-146">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="9108c-146">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="9108c-147">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="9108c-147">Troubleshoot</span></span>

<span data-ttu-id="9108c-148">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="9108c-148">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9108c-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9108c-149">Next steps</span></span>

<span data-ttu-id="9108c-150">Teraz, że pomyślnie utworzono klaster usługi HDInsight, użyj następujących zasobów, aby dowiedzieć się, jak pracować z klastra.</span><span class="sxs-lookup"><span data-stu-id="9108c-150">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="9108c-151">Klastry Hadoop</span><span class="sxs-lookup"><span data-stu-id="9108c-151">Hadoop clusters</span></span>

* [<span data-ttu-id="9108c-152">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9108c-152">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9108c-153">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9108c-153">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9108c-154">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="9108c-154">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="9108c-155">Klastrów HBase</span><span class="sxs-lookup"><span data-stu-id="9108c-155">HBase clusters</span></span>

* [<span data-ttu-id="9108c-156">Rozpoczynanie pracy z bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9108c-156">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="9108c-157">Tworzenie aplikacji Java bazy danych hbase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9108c-157">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="9108c-158">Klastry STORM</span><span class="sxs-lookup"><span data-stu-id="9108c-158">Storm clusters</span></span>

* [<span data-ttu-id="9108c-159">Tworzenie topologii Java dla Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9108c-159">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="9108c-160">Użyj składników języka Python w Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9108c-160">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="9108c-161">Wdrażanie i monitorowanie topologii z systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="9108c-161">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="9108c-162">Klastry Spark</span><span class="sxs-lookup"><span data-stu-id="9108c-162">Spark clusters</span></span>

* [<span data-ttu-id="9108c-163">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="9108c-163">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="9108c-164">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="9108c-164">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="9108c-165">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="9108c-165">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="9108c-166">Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności</span><span class="sxs-lookup"><span data-stu-id="9108c-166">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="9108c-167">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="9108c-167">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

