---
title: "Dostosowywanie klastrów usługi HDInsight przy użyciu ładowania początkowego - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dostosować klastry usługi HDInsight przy użyciu ładowania początkowego."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ab2ebf0c-e961-4e95-8151-9724ee22d769
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c7a6fafa90eac66774d564c82c926c662baf784c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="77999-103">Dostosowywanie klastrów usługi HDInsight przy użyciu ładowania początkowego</span><span class="sxs-lookup"><span data-stu-id="77999-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="77999-104">Czasami użytkownik chce skonfigurować pliki konfiguracyjne, które obejmują:</span><span class="sxs-lookup"><span data-stu-id="77999-104">Sometimes, you want to configure the configuration files, which include:</span></span>

* <span data-ttu-id="77999-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="77999-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="77999-106">Core-site.xml</span><span class="sxs-lookup"><span data-stu-id="77999-106">core-site.xml</span></span>
* <span data-ttu-id="77999-107">Gateway.XML</span><span class="sxs-lookup"><span data-stu-id="77999-107">gateway.xml</span></span>
* <span data-ttu-id="77999-108">hbase env.xml</span><span class="sxs-lookup"><span data-stu-id="77999-108">hbase-env.xml</span></span>
* <span data-ttu-id="77999-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="77999-109">hbase-site.xml</span></span>
* <span data-ttu-id="77999-110">System plików hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="77999-110">hdfs-site.xml</span></span>
* <span data-ttu-id="77999-111">env.xml gałęzi</span><span class="sxs-lookup"><span data-stu-id="77999-111">hive-env.xml</span></span>
* <span data-ttu-id="77999-112">gałąź site.xml</span><span class="sxs-lookup"><span data-stu-id="77999-112">hive-site.xml</span></span>
* <span data-ttu-id="77999-113">mapred lokacji</span><span class="sxs-lookup"><span data-stu-id="77999-113">mapred-site</span></span>
* <span data-ttu-id="77999-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="77999-114">oozie-site.xml</span></span>
* <span data-ttu-id="77999-115">oozie env.xml</span><span class="sxs-lookup"><span data-stu-id="77999-115">oozie-env.xml</span></span>
* <span data-ttu-id="77999-116">STORM-site.xml</span><span class="sxs-lookup"><span data-stu-id="77999-116">storm-site.xml</span></span>
* <span data-ttu-id="77999-117">tez site.xml</span><span class="sxs-lookup"><span data-stu-id="77999-117">tez-site.xml</span></span>
* <span data-ttu-id="77999-118">webhcat site.xml</span><span class="sxs-lookup"><span data-stu-id="77999-118">webhcat-site.xml</span></span>
* <span data-ttu-id="77999-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="77999-119">yarn-site.xml</span></span>

<span data-ttu-id="77999-120">Istnieją trzy metody do początkowego użycia:</span><span class="sxs-lookup"><span data-stu-id="77999-120">There are three methods to use bootstrap:</span></span>

* <span data-ttu-id="77999-121">Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="77999-121">Use Azure PowerShell</span></span>
* <span data-ttu-id="77999-122">Korzystanie z zestawu SDK dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="77999-122">Use .NET SDK</span></span>
* <span data-ttu-id="77999-123">Korzystanie z szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="77999-123">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="77999-124">Aby uzyskać informacje na temat instalowania dodatkowych składników w klastrze usługi HDInsight podczas tworzenia zobacz:</span><span class="sxs-lookup"><span data-stu-id="77999-124">For information on installing additional components on HDInsight cluster during the creation time, see:</span></span>

* [<span data-ttu-id="77999-125">Dostosowywanie klastrów usługi HDInsight przy użyciu akcji skryptu (Linux)</span><span class="sxs-lookup"><span data-stu-id="77999-125">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="77999-126">Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="77999-126">Use Azure PowerShell</span></span>
<span data-ttu-id="77999-127">Poniższy kod programu PowerShell dostosowuje konfiguracji gałęzi:</span><span class="sxs-lookup"><span data-stu-id="77999-127">The following PowerShell code customizes a Hive configuration:</span></span>

    # hive-site.xml configuration
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $existingResourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $clusterSizeInNodes `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -Config $config 

<span data-ttu-id="77999-128">Zakończenie pracy skryptu programu PowerShell można znaleźć w [dodatek A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span><span class="sxs-lookup"><span data-stu-id="77999-128">A complete working PowerShell script can be found in [Appendix-A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span></span>

<span data-ttu-id="77999-129">**Aby sprawdzić zmiany:**</span><span class="sxs-lookup"><span data-stu-id="77999-129">**To verify the change:**</span></span>

1. <span data-ttu-id="77999-130">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="77999-130">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="77999-131">Z menu po lewej stronie kliknij **klastrów usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="77999-131">From the left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="77999-132">Jeśli nie widzisz, kliknij przycisk **więcej usług** pierwszy.</span><span class="sxs-lookup"><span data-stu-id="77999-132">If you don't see it, click **More services** first.</span></span>
3. <span data-ttu-id="77999-133">Kliknij utworzony przy użyciu skryptu środowiska PowerShell klastra.</span><span class="sxs-lookup"><span data-stu-id="77999-133">Click the cluster you just created using the PowerShell script.</span></span>
4. <span data-ttu-id="77999-134">Kliknij przycisk **pulpitu nawigacyjnego** od górnej krawędzi bloku, aby otworzyć Interfejs użytkownika narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="77999-134">Click **Dashboard** from the top of the blade to open the Ambari UI.</span></span>
5. <span data-ttu-id="77999-135">Kliknij przycisk **Hive** z menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="77999-135">Click **Hive** from the left menu.</span></span>
6. <span data-ttu-id="77999-136">Kliknij przycisk **serwera HiveServer2** z **Podsumowanie**.</span><span class="sxs-lookup"><span data-stu-id="77999-136">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="77999-137">Kliknij przycisk **Configs** kartę.</span><span class="sxs-lookup"><span data-stu-id="77999-137">Click the **Configs** tab.</span></span>
8. <span data-ttu-id="77999-138">Kliknij przycisk **Hive** z menu po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="77999-138">Click **Hive** from the left menu.</span></span>
9. <span data-ttu-id="77999-139">Kliknij przycisk **zaawansowane** kartę.</span><span class="sxs-lookup"><span data-stu-id="77999-139">Click the **Advanced** tab.</span></span>
10. <span data-ttu-id="77999-140">Przewiń w dół, a następnie rozwiń węzeł **zaawansowane witryny hive**.</span><span class="sxs-lookup"><span data-stu-id="77999-140">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="77999-141">Wyszukaj **hive.metastore.client.socket.timeout** w sekcji.</span><span class="sxs-lookup"><span data-stu-id="77999-141">Look for **hive.metastore.client.socket.timeout** in the section.</span></span>

<span data-ttu-id="77999-142">Niektóre przykłady więcej o dostosowywaniu inne pliki konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="77999-142">Some more samples on customizing other configuration files:</span></span>

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

<span data-ttu-id="77999-143">Aby uzyskać więcej informacji, zobacz blog Azim Uddin zatytułowany [tworzenia klastra usługi HDInsight dostosowywanie](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="77999-143">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="77999-144">Korzystanie z zestawu SDK dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="77999-144">Use .NET SDK</span></span>
<span data-ttu-id="77999-145">Zobacz [opartych na systemie Linux z tworzenia klastrów w usłudze HDInsight przy użyciu zestawu .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span><span class="sxs-lookup"><span data-stu-id="77999-145">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="77999-146">Użyj Menedżera zasobów szablonu</span><span class="sxs-lookup"><span data-stu-id="77999-146">Use Resource Manager template</span></span>
<span data-ttu-id="77999-147">Bootstrap można użyć w szablonie usługi Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="77999-147">You can use bootstrap in Resource Manager template:</span></span>

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop dostosowuje klastra ładowania początkowego szablonu usługi Azure Resource Manager](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="77999-149">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="77999-149">See also</span></span>
* <span data-ttu-id="77999-150">[Tworzenie klastrów Hadoop w usłudze HDInsight] [ hdinsight-provision-cluster] zawiera instrukcje dotyczące sposobu tworzenia klastra usługi HDInsight przy użyciu niestandardowych opcji.</span><span class="sxs-lookup"><span data-stu-id="77999-150">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="77999-151">[Tworzenie skryptów akcji skryptu dla usługi HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="77999-151">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="77999-152">[Zainstalować i używać platformy Spark w usłudze hdinsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="77999-152">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="77999-153">[Zainstaluj i użyj języka R w klastrach HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="77999-153">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="77999-154">[Zainstalować i używać Solr w klastrach HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="77999-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="77999-155">[Zainstalować i używać Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="77999-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="77999-156">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Etapy podczas tworzenia klastra"</span><span class="sxs-lookup"><span data-stu-id="77999-156">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>

## <a name="appx-a-powershell-sample"></a><span data-ttu-id="77999-157">Próbka a. Appx programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="77999-157">Appx-A: PowerShell sample</span></span>
<span data-ttu-id="77999-158">Ten skrypt programu PowerShell tworzy klaster usługi HDInsight i dostosowuje ustawienie gałęzi:</span><span class="sxs-lookup"><span data-stu-id="77999-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

    ####################################
    # Set these variables
    ####################################
    #region - used for creating Azure service names
    $nameToken = "<ENTER AN ALIAS>" 
    #endregion

    #region - cluster user accounts
    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"

    $sshUserName = "sshuser" #HDInsight ssh user name
    $sshPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"
    #endregion

    ####################################
    # Service names and varialbes
    ####################################
    #region - service names
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    $location = "East US 2"
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    ####################################
    # Connect to Azure
    ####################################
    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an HDInsight cluster
    ####################################
    # Create dependent components
    ####################################
    Write-Host "Creating a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Creating the default storage account and default blob container ..."  -ForegroundColor Green
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS

    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageContext #use the cluster name as the container name

    ####################################
    # Create a configuration object
    ####################################
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    ####################################
    # Create an HDInsight cluster
    ####################################
    $httpPW = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$httpPW)

    $sshPW = ConvertTo-SecureString -String $sshPassword -AsPlainText -Force
    $sshCredential = New-Object System.Management.Automation.PSCredential($sshUserName,$sshPW)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -Location $location `
        -ClusterSizeInNodes 1 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -SshCredential $sshCredential `
        -Config $config

    ####################################
    # Verify the cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
