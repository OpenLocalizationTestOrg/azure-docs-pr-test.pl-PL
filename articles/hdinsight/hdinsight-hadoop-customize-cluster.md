---
title: "aaaCustomize klastrów usługi HDInsight przy użyciu skryptu akcje - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocustomize HDInsight clusters za pomocą akcji skryptu."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="c9507-103">Dostosowywanie klastrów usługi HDInsight opartej na systemie Windows za pomocą akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="c9507-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="c9507-104">**Akcja skryptu** mogą być używane tooinvoke [niestandardowych skryptów](hdinsight-hadoop-script-actions.md) podczas procesu tworzenia klastra hello instalowania dodatkowego oprogramowania na klastrze.</span><span class="sxs-lookup"><span data-stu-id="c9507-104">**Script Action** can be used tooinvoke [custom scripts](hdinsight-hadoop-script-actions.md) during hello cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="c9507-105">Hello informacje w tym artykule jest określonym na podstawie tooWindows klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9507-105">hello information in this article is specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="c9507-106">W klastrach opartych na systemie Linux, zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c9507-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9507-107">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c9507-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c9507-108">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="c9507-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="c9507-109">Klastry usługi HDInsight można dostosować w różnych innych metod, a także takie jak tym dodatkowych kont usługi Azure Storage, zmiana hello Hadoop plików konfiguracji (core-site.xml, hive-site.xml, itp.) lub dodawanie współdzielone biblioteki (np. Hive, Oozie) w typowe lokalizacje hello klastra.</span><span class="sxs-lookup"><span data-stu-id="c9507-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing hello Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in hello cluster.</span></span> <span data-ttu-id="c9507-110">Te modyfikacje może odbywać się za pomocą programu Azure PowerShell, hello Azure HDInsight .NET SDK, lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c9507-110">These customizations can be done through Azure PowerShell, hello Azure HDInsight .NET SDK, or hello Azure portal.</span></span> <span data-ttu-id="c9507-111">Aby uzyskać więcej informacji, zobacz [klastrów utworzyć Hadoop w usłudze HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="c9507-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="c9507-112">Akcja skryptu w procesie tworzenia klastra hello</span><span class="sxs-lookup"><span data-stu-id="c9507-112">Script Action in hello cluster creation process</span></span>
<span data-ttu-id="c9507-113">Akcja skryptu jest używana tylko podczas hello procesu tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="c9507-113">Script Action is only used while a cluster is in hello process of being created.</span></span> <span data-ttu-id="c9507-114">Witaj poniższym diagramie przedstawiono podczas wykonywania akcji skryptu podczas procesu tworzenia hello:</span><span class="sxs-lookup"><span data-stu-id="c9507-114">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="c9507-115">![Dostosowywanie klastrów usługi HDInsight i etapy podczas tworzenia klastra][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="c9507-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="c9507-116">Podczas wykonywania skryptu hello hello klastra wprowadza hello **ClusterCustomization** etapu.</span><span class="sxs-lookup"><span data-stu-id="c9507-116">When hello script is running, hello cluster enters hello **ClusterCustomization** stage.</span></span> <span data-ttu-id="c9507-117">Na tym etapie hello skrypt jest uruchamiany w ramach konta administratora systemu hello, równolegle na powitania wszystkie określone węzłów w klastrze hello i zapewnia uprawnienia administrator o pełnych uprawnieniach w węzłach hello.</span><span class="sxs-lookup"><span data-stu-id="c9507-117">At this stage, hello script is run under hello system admin account, in parallel on all hello specified nodes in hello cluster, and provides full admin privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="c9507-118">Ponieważ użytkownik ma uprawnienia administratora w węzłach klastra hello podczas **ClusterCustomization** etapie, można użyć hello skryptu tooperform operacje takie jak zatrzymanie i uruchomienie usług, w tym usług związanych z usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c9507-118">Because you have admin privileges on hello cluster nodes during the **ClusterCustomization** stage, you can use hello script tooperform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="c9507-119">Jako część skryptu hello, należy się upewnić, tym hello Ambari usług i innych usług związanych z Hadoop są gotowe do działania przed zakończeniu hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="c9507-119">So, as part of hello script, you must ensure that hello Ambari services and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="c9507-120">Te usługi są wymagane toosuccessfully ustalić hello kondycję i stan hello klastra podczas jego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="c9507-120">These services are required toosuccessfully ascertain hello health and state of hello cluster while it is being created.</span></span> <span data-ttu-id="c9507-121">Jeśli zmienisz żadnej konfiguracji w klastrze, który ma wpływ na tych usług, należy użyć funkcji pomocnika hello, które znajdują się.</span><span class="sxs-lookup"><span data-stu-id="c9507-121">If you change any configuration on the cluster that affects these services, you must use hello helper functions that are provided.</span></span> <span data-ttu-id="c9507-122">Aby uzyskać więcej informacji o funkcji pomocnika, zobacz [skryptów tworzenie akcji skryptu dla usługi HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="c9507-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="c9507-123">dane wyjściowe Hello i dzienników błędów hello skryptu hello są przechowywane w hello domyślne konto magazynu określone dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="c9507-123">hello output and hello error logs for hello script are stored in hello default Storage account you specified for hello cluster.</span></span> <span data-ttu-id="c9507-124">Witaj dzienniki są przechowywane w tabeli o nazwie hello **u < \cluster-name-fragment >< \time-stamp > setuplog**.</span><span class="sxs-lookup"><span data-stu-id="c9507-124">hello logs are stored in a table with hello name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="c9507-125">Są to dzienniki agregacji ze skryptu hello uruchamiania we wszystkich węzłach hello (węzła głównego i węzły procesów roboczych) w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="c9507-125">These are aggregate logs from hello script run on all hello nodes (head node and worker nodes) in hello cluster.</span></span>

<span data-ttu-id="c9507-126">Każdy klaster może akceptować wiele akcji skryptu, które jest wywoływane w kolejności hello, w którym są określone.</span><span class="sxs-lookup"><span data-stu-id="c9507-126">Each cluster can accept multiple script actions that are invoked in hello order in which they are specified.</span></span> <span data-ttu-id="c9507-127">Skrypt może uruchomionego na powitania węzła głównego i hello węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="c9507-127">A script can be ran on hello head node, hello worker nodes, or both.</span></span>

<span data-ttu-id="c9507-128">Usługa HDInsight zapewnia kilka hello tooinstall skrypty następujące składniki w klastrach HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c9507-128">HDInsight provides several scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="c9507-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c9507-129">Name</span></span> | <span data-ttu-id="c9507-130">Skrypt</span><span class="sxs-lookup"><span data-stu-id="c9507-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="c9507-131">**Zainstaluj Spark**</span><span class="sxs-lookup"><span data-stu-id="c9507-131">**Install Spark**</span></span> |<span data-ttu-id="c9507-132">https://hdiconfigactions.blob.Core.Windows.NET/sparkconfigactionv03/Spark-Installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="c9507-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="c9507-133">Zobacz [instalacji i używania platformy Spark w usłudze HDInsight clusters][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="c9507-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="c9507-134">**Zainstalować język R**</span><span class="sxs-lookup"><span data-stu-id="c9507-134">**Install R**</span></span> |<span data-ttu-id="c9507-135">https://hdiconfigactions.blob.Core.Windows.NET/rconfigactionv02/r-Installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="c9507-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="c9507-136">Zobacz [instalacji i używania R w klastrach HDInsight][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="c9507-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="c9507-137">**Zainstaluj Solr**</span><span class="sxs-lookup"><span data-stu-id="c9507-137">**Install Solr**</span></span> |<span data-ttu-id="c9507-138">https://hdiconfigactions.blob.Core.Windows.NET/solrconfigactionv01/solr-Installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="c9507-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="c9507-139">Zobacz [instalacji i używania Solr w usłudze HDInsight clusters](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="c9507-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="c9507-140">- **Zainstaluj Giraph**</span><span class="sxs-lookup"><span data-stu-id="c9507-140">- **Install Giraph**</span></span> |<span data-ttu-id="c9507-141">https://hdiconfigactions.blob.Core.Windows.NET/giraphconfigactionv01/giraph-Installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="c9507-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="c9507-142">Zobacz [instalacji i używania Giraph w usłudze HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="c9507-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="c9507-143">**Wstępne ładowanie bibliotek technologii Hive**</span><span class="sxs-lookup"><span data-stu-id="c9507-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="c9507-144">https://hdiconfigactions.blob.Core.Windows.NET/setupcustomhivelibsv01/Setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="c9507-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="c9507-145">Zobacz [dodać Hive bibliotek w klastrach HDInsight](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="c9507-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-hello-azure-portal"></a><span data-ttu-id="c9507-146">Skrypty wywołania przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c9507-146">Call scripts using hello Azure portal</span></span>
<span data-ttu-id="c9507-147">**Z hello portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="c9507-147">**From hello Azure portal**</span></span>

1. <span data-ttu-id="c9507-148">Rozpocznij tworzenie klastra, zgodnie z opisem w [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c9507-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="c9507-149">W obszarze Konfiguracja opcjonalna dla hello **akcji skryptu** bloku, kliknij przycisk **dodać akcję skryptu** tooprovide szczegółowych informacji o hello akcji skryptu, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="c9507-149">Under Optional Configuration, for hello **Script Actions** blade, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="c9507-150">![Użyj akcji skryptu toocustomize klastra](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize akcji skryptu Użyj klastra")</span><span class="sxs-lookup"><span data-stu-id="c9507-150">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="c9507-151">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c9507-151">Property</span></span></th><th><span data-ttu-id="c9507-152">Wartość</span><span class="sxs-lookup"><span data-stu-id="c9507-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="c9507-153">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c9507-153">Name</span></span></td>
            <td><span data-ttu-id="c9507-154">Określ nazwę hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="c9507-154">Specify a name for hello script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="c9507-155">Identyfikator URI skryptu</span><span class="sxs-lookup"><span data-stu-id="c9507-155">Script URI</span></span></td>
            <td><span data-ttu-id="c9507-156">Określ hello URI toohello skrypt, który jest wywołana toocustomize hello klastra.</span><span class="sxs-lookup"><span data-stu-id="c9507-156">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="c9507-157">s</span><span class="sxs-lookup"><span data-stu-id="c9507-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="c9507-158">HEAD/proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="c9507-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="c9507-159">Określ węzły hello (**Head** lub **procesu roboczego**) na których dostosowanie hello skrypt jest uruchamiany.</b>.</span><span class="sxs-lookup"><span data-stu-id="c9507-159">Specify hello nodes (**Head** or **Worker**) on which hello customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="c9507-160">Parametry</span><span class="sxs-lookup"><span data-stu-id="c9507-160">Parameters</span></span></td>
            <td><span data-ttu-id="c9507-161">Określ parametry hello, jeśli są wymagane przez skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="c9507-161">Specify hello parameters, if required by hello script.</span></span></td></tr>
    </table>

    <span data-ttu-id="c9507-162">Naciśnij klawisz ENTER tooadd więcej niż jednego skryptu akcji tooinstall wiele składników w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="c9507-162">Press ENTER tooadd more than one script action tooinstall multiple components on hello cluster.</span></span>
3. <span data-ttu-id="c9507-163">Kliknij przycisk **wybierz** toosave hello konfigurację akcji skryptu i kontynuować tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="c9507-163">Click **Select** toosave hello script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="c9507-164">Skrypty wywołania przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9507-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="c9507-165">Tego poniższy skrypt programu PowerShell pokazano, jak tooinstall Spark w systemie Windows na podstawie klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9507-165">This following PowerShell script demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="c9507-166">tooinstall innego oprogramowania, konieczne będzie pliku skryptu hello tooreplace w skrypcie hello:</span><span class="sxs-lookup"><span data-stu-id="c9507-166">tooinstall other software, you will need tooreplace hello script file in hello script:</span></span>

<span data-ttu-id="c9507-167">Po wyświetleniu monitu wprowadź poświadczenia hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="c9507-167">When prompted, enter hello credentials for hello cluster.</span></span> <span data-ttu-id="c9507-168">Może upłynąć kilka minut przed utworzeniem klastra hello.</span><span class="sxs-lookup"><span data-stu-id="c9507-168">It can take several minutes before hello cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="c9507-169">Skrypty wywołania przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c9507-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="c9507-170">Witaj poniższym przykładzie pokazano sposób tooinstall Spark w systemie Windows na podstawie klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9507-170">hello following sample demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="c9507-171">tooinstall innego oprogramowania, konieczne będzie pliku skryptu hello tooreplace w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="c9507-171">tooinstall other software, you will need tooreplace hello script file in hello code.</span></span>

<span data-ttu-id="c9507-172">**toocreate klastra usługi HDInsight Spark**</span><span class="sxs-lookup"><span data-stu-id="c9507-172">**toocreate an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="c9507-173">Tworzenie aplikacji konsolowej C# w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c9507-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="c9507-174">Z hello Konsola Menedżera pakietów Nuget uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="c9507-174">From hello Nuget Package Manager Console, run hello following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="c9507-175">Użyj hello następujące instrukcje using w pliku Program.cs hello:</span><span class="sxs-lookup"><span data-stu-id="c9507-175">Use hello following using statements in hello Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="c9507-176">Umieść kod hello w klasie hello hello następujący:</span><span class="sxs-lookup"><span data-stu-id="c9507-176">Place hello code in hello class with hello following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="c9507-177">Naciśnij klawisz **F5** toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c9507-177">Press **F5** toorun hello application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="c9507-178">Obsługa oprogramowania typu open source używane w klastrach HDInsight</span><span class="sxs-lookup"><span data-stu-id="c9507-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="c9507-179">Hello usługi HDInsight systemu Microsoft Azure to elastyczna platforma, która umożliwia toobuild aplikacje danych big data w chmurze hello przy użyciu ekosystem technologii open source utworzona wokół Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c9507-179">hello Microsoft Azure HDInsight service is a flexible platform that enables you toobuild big-data applications in hello cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="c9507-180">Microsoft Azure udostępnia ogólnego poziomu wsparcia dla technologii open source, zgodnie z opisem w hello **obsługuje zakresu** sekcji hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">witryny sieci Web często zadawane pytania dotyczące obsługi Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="c9507-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in hello **Support Scope** section of hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="c9507-181">Hello usługa HDInsight zapewnia dodatkowy poziom obsługi dla niektórych składników hello zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="c9507-181">hello HDInsight service provides an additional level of support for some of hello components, as described below.</span></span>

<span data-ttu-id="c9507-182">Istnieją dwa typy składników open source, które są dostępne w hello usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c9507-182">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="c9507-183">**Wbudowanych składników** — te składniki są wstępnie zainstalowane w klastrach HDInsight i podaj podstawowych funkcji programu hello klastra.</span><span class="sxs-lookup"><span data-stu-id="c9507-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="c9507-184">Na przykład YARN ResourceManager, język zapytań Hive hello (HiveQL) i biblioteki Mahout hello należy toothis kategorii.</span><span class="sxs-lookup"><span data-stu-id="c9507-184">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="c9507-185">Pełna lista składniki klastra jest dostępna w [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight?](hdinsight-component-versioning.md) </a>.</span><span class="sxs-lookup"><span data-stu-id="c9507-185">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="c9507-186">**Niestandardowe składniki** -, jako użytkownik hello klastra, można zainstalować lub użyć w obciążenie jakiegokolwiek składnika dostępne w społeczności hello lub utworzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c9507-186">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

<span data-ttu-id="c9507-187">Wbudowane składniki są w pełni obsługiwane, a Microsoft Support będzie pomocy tooisolate i rozwiązać problemy toothese powiązane składniki.</span><span class="sxs-lookup"><span data-stu-id="c9507-187">Built-in components are fully supported, and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>

> [!WARNING]
> <span data-ttu-id="c9507-188">Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane i Microsoft Support będzie pomocy tooisolate i rozwiązać problemy toothese powiązane składniki.</span><span class="sxs-lookup"><span data-stu-id="c9507-188">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="c9507-189">Niestandardowe składniki odbierania toohelp Obsługa uzasadnione ekonomicznie toofurther należy rozwiązać problem hello.</span><span class="sxs-lookup"><span data-stu-id="c9507-189">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="c9507-190">Może to spowodować nad rozwiązaniem problemu hello lub proszenia tooengage dostępnych kanałów dla hello otwarty technologii źródła wykryto głębokie doświadczenia z tej technologii.</span><span class="sxs-lookup"><span data-stu-id="c9507-190">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="c9507-191">Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="c9507-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="c9507-192">Witaj usługi HDInsight udostępnia kilka metod toouse niestandardowych składników.</span><span class="sxs-lookup"><span data-stu-id="c9507-192">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="c9507-193">Niezależnie od tego, jak składnik jest używany lub zainstalowany w klastrze hello hello sam poziom obsługi ma zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="c9507-193">Regardless of how a component is used or installed on hello cluster, hello same level of support applies.</span></span> <span data-ttu-id="c9507-194">Poniżej znajduje się lista hello Najczęstszym że składnikach niestandardowych mogą być używane w klastrach HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c9507-194">Below is a list of hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="c9507-195">Przesyłanie zadań — usługi Hadoop i innych typów zadań, które wykonać albo użyć niestandardowych składników mogą być przesłane toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="c9507-195">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>
2. <span data-ttu-id="c9507-196">Dostosowywanie klastra — podczas tworzenia klastra, można określić dodatkowe ustawienia i niestandardowych składników, które zostaną zainstalowane w węzłach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="c9507-196">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on hello cluster nodes.</span></span>
3. <span data-ttu-id="c9507-197">Próbek - dla popularnych niestandardowych składników, firma Microsoft i inne osoby mogą powodować przykłady sposobu użycia tych składników na powitania klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c9507-197">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="c9507-198">Te przykłady są udostępniane bez obsługi.</span><span class="sxs-lookup"><span data-stu-id="c9507-198">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="c9507-199">Tworzenie skryptów akcji skryptu</span><span class="sxs-lookup"><span data-stu-id="c9507-199">Develop Script Action scripts</span></span>
<span data-ttu-id="c9507-200">Zobacz [skryptów tworzenie akcji skryptu dla usługi HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="c9507-200">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="c9507-201">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c9507-201">See also</span></span>
* <span data-ttu-id="c9507-202">[Tworzenie klastrów Hadoop w usłudze HDInsight] [ hdinsight-provision-cluster] zawiera instrukcje dotyczące sposobu toocreate HDInsight klastra przy użyciu niestandardowych opcji.</span><span class="sxs-lookup"><span data-stu-id="c9507-202">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="c9507-203">[Tworzenie skryptów akcji skryptu dla usługi HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="c9507-203">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="c9507-204">[Zainstalować i używać platformy Spark w usłudze hdinsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="c9507-204">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="c9507-205">[Zainstaluj i użyj języka R w klastrach HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="c9507-205">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="c9507-206">[Zainstalować i używać Solr w klastrach HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="c9507-206">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="c9507-207">[Zainstalować i używać Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="c9507-207">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Etapy podczas tworzenia klastra"
