---
title: "przy użyciu programu PowerShell - Azure HDInsight klastrów Hadoop aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Hadoop, HBase, Storm i Spark klastrów w systemie Linux dla usługi HDInsight przy użyciu programu Azure PowerShell."
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
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="65529-103">Tworzenie klastrów z systemem Linux w usłudze HDInsight przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="65529-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="65529-104">Program Azure PowerShell jest zaawansowane środowisko obsługi skryptów, można użyć toocontrol i zautomatyzować hello wdrażania i zarządzania obciążeń w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="65529-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="65529-105">Ten dokument zawiera informacje dotyczące sposobu toocreate usługi HDInsight opartej na systemie Linux klaster przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65529-105">This document provides information about how toocreate a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="65529-106">Zawiera również przykład skryptu.</span><span class="sxs-lookup"><span data-stu-id="65529-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="65529-107">Program Azure PowerShell jest dostępny tylko na komputerach klienckich z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="65529-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="65529-108">Jeśli używasz klienta systemu Linux, Unix lub Mac OS X, zobacz [tworzenia klastra usługi HDInsight opartej na systemie Linux przy użyciu interfejsu wiersza polecenia Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) informacji o używaniu hello Azure CLI toocreate klastra.</span><span class="sxs-lookup"><span data-stu-id="65529-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using hello Azure CLI toocreate a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65529-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="65529-109">Prerequisites</span></span>
<span data-ttu-id="65529-110">Musi mieć następujące hello przed rozpoczęciem tej procedury:</span><span class="sxs-lookup"><span data-stu-id="65529-110">You must have hello following before starting this procedure:</span></span>

* <span data-ttu-id="65529-111">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="65529-111">An Azure subscription.</span></span> <span data-ttu-id="65529-112">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="65529-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="65529-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="65529-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="65529-114">Obsługa programu Azure PowerShell do celów zarządzania zasobami usługi HDInsight przy użyciu usługi Azure Service Manager jest **przestarzała** i została usunięta z dniem 1 stycznia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="65529-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="65529-115">Witaj czynnościach w ramach tego dokumentu Użyj hello nowe polecenia cmdlet usługi HDInsight współpracujące z usługą Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65529-115">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="65529-116">Wykonaj kroki hello [instalacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello najnowszą wersję programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65529-116">Please follow hello steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="65529-117">Jeśli masz skrypty tego toobe należy zmodyfikować toouse hello nowych poleceń cmdlet współpracujących z usługą Azure Resource Manager, zobacz [narzędzi tooAzure Migrowanie programowania opartego na Menedżera zasobów dla klastrów usługi HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="65529-117">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="65529-118">Tworzenie klastra</span><span class="sxs-lookup"><span data-stu-id="65529-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="65529-119">toocreate klastra usługi HDInsight przy użyciu programu Azure PowerShell, należy wykonać hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="65529-119">toocreate an HDInsight cluster by using Azure PowerShell, you must complete hello following procedures:</span></span>

* <span data-ttu-id="65529-120">Tworzenie grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="65529-120">Create an Azure resource group</span></span>
* <span data-ttu-id="65529-121">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="65529-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="65529-122">Tworzenie kontenera obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="65529-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="65529-123">Tworzenie klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="65529-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="65529-124">Witaj poniższy skrypt pokazuje, jak toocreate nowego klastra:</span><span class="sxs-lookup"><span data-stu-id="65529-124">hello following script demonstrates how toocreate a new cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

<span data-ttu-id="65529-125">podane dla logowania do klastra hello wartości Hello są hello toocreate używane konto użytkownika usługi Hadoop dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="65529-125">hello values you specify for hello cluster login are used toocreate hello Hadoop user account for hello cluster.</span></span> <span data-ttu-id="65529-126">Użyj tego tooservices tooconnect konta hostowanych w klastrze hello, takich jak web UI lub interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="65529-126">Use this account tooconnect tooservices hosted on hello cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="65529-127">Hello wartości określonej dla użytkownika SSH hello są użytkownika SSH hello toocreate używane dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="65529-127">hello values you specify for hello SSH user are used toocreate hello SSH user for hello cluster.</span></span> <span data-ttu-id="65529-128">Użyj tego konta toostart zdalnej sesji SSH w klastrze hello i uruchom zadania.</span><span class="sxs-lookup"><span data-stu-id="65529-128">Use this account toostart a remote SSH session on hello cluster and run jobs.</span></span> <span data-ttu-id="65529-129">Aby uzyskać więcej informacji, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="65529-129">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65529-130">Jeśli planujesz toouse więcej niż 32 węzłami procesów roboczych (na utworzenie klastra lub przez hello skalowania klastra po utworzeniu), należy również określić rozmiaru węzła głównego z co najmniej 8 rdzeniami i 14 GB pamięci RAM.</span><span class="sxs-lookup"><span data-stu-id="65529-130">If you plan toouse more than 32 worker nodes (either at cluster creation or by scaling hello cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="65529-131">Aby uzyskać więcej informacji na węzeł rozmiary i koszty, zobacz [cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="65529-131">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="65529-132">Może potrwać toocreate minut too20 klastra.</span><span class="sxs-lookup"><span data-stu-id="65529-132">It can take up too20 minutes toocreate a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="65529-133">Tworzenie klastra: obiekt konfiguracji</span><span class="sxs-lookup"><span data-stu-id="65529-133">Create cluster: Configuration object</span></span>

<span data-ttu-id="65529-134">Można również utworzyć HDInsight konfiguracji obiektów przy użyciu `New-AzureRmHDInsightClusterConfig` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="65529-134">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="65529-135">Następnie można zmodyfikować tej konfiguracji obiektu tooenable dodatkowe opcje konfiguracji dla klastra.</span><span class="sxs-lookup"><span data-stu-id="65529-135">You can then modify this configuration object tooenable additional configuration options for your cluster.</span></span> <span data-ttu-id="65529-136">Na koniec użyj hello `-Config` parametru hello `New-AzureRmHDInsightCluster` konfiguracji hello toouse polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="65529-136">Finally, use hello `-Config` parameter of hello `New-AzureRmHDInsightCluster` cmdlet toouse hello configuration.</span></span>

<span data-ttu-id="65529-137">Witaj poniższy skrypt tworzy tooconfigure obiekt konfiguracji R Server na typ klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="65529-137">hello following script creates a configuration object tooconfigure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="65529-138">Konfiguracja Hello pozwala węzeł krawędzi, programu RStudio i konto magazynu dodatkowe.</span><span class="sxs-lookup"><span data-stu-id="65529-138">hello configuration enables an edge node, RStudio, and an additional storage account.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> <span data-ttu-id="65529-139">Używanie konta magazynu w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="65529-139">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span> <span data-ttu-id="65529-140">Podczas korzystania z tego przykładu należy utworzyć konto magazynu dodatkowe hello w hello tej samej lokalizacji co powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="65529-140">When using this example, create hello additional storage account in hello same location as hello server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="65529-141">Dostosowywanie klastrów</span><span class="sxs-lookup"><span data-stu-id="65529-141">Customize clusters</span></span>

* <span data-ttu-id="65529-142">Zobacz [HDInsight dostosować klastry za pomocą początkowego](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="65529-142">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="65529-143">Zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="65529-143">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="65529-144">Usuń klaster hello</span><span class="sxs-lookup"><span data-stu-id="65529-144">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="65529-145">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="65529-145">Troubleshoot</span></span>

<span data-ttu-id="65529-146">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="65529-146">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65529-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="65529-147">Next steps</span></span>

<span data-ttu-id="65529-148">Po pomyślnym utworzeniu klastra usługi HDInsight, za pomocą hello następujące zasoby toolearn jak toowork z klastrem.</span><span class="sxs-lookup"><span data-stu-id="65529-148">Now that you have successfully created an HDInsight cluster, use hello following resources toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="65529-149">Klastry Hadoop</span><span class="sxs-lookup"><span data-stu-id="65529-149">Hadoop clusters</span></span>

* [<span data-ttu-id="65529-150">Korzystanie z programu Hive z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="65529-150">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="65529-151">Korzystanie z języka Pig z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="65529-151">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="65529-152">Korzystać z usługi MapReduce z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="65529-152">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="65529-153">Klastrów HBase</span><span class="sxs-lookup"><span data-stu-id="65529-153">HBase clusters</span></span>

* [<span data-ttu-id="65529-154">Rozpoczynanie pracy z bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="65529-154">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="65529-155">Tworzenie aplikacji Java bazy danych hbase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="65529-155">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="65529-156">Klastry STORM</span><span class="sxs-lookup"><span data-stu-id="65529-156">Storm clusters</span></span>

* [<span data-ttu-id="65529-157">Tworzenie topologii Java dla Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="65529-157">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="65529-158">Użyj składników języka Python w Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="65529-158">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="65529-159">Wdrażanie i monitorowanie topologii z systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="65529-159">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="65529-160">Klastry Spark</span><span class="sxs-lookup"><span data-stu-id="65529-160">Spark clusters</span></span>

* [<span data-ttu-id="65529-161">Tworzenie autonomicznych aplikacji przy użyciu języka Scala</span><span class="sxs-lookup"><span data-stu-id="65529-161">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="65529-162">Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy</span><span class="sxs-lookup"><span data-stu-id="65529-162">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="65529-163">Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej</span><span class="sxs-lookup"><span data-stu-id="65529-163">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="65529-164">Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight</span><span class="sxs-lookup"><span data-stu-id="65529-164">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="65529-165">Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="65529-165">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

