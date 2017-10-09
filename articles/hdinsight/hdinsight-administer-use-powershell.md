---
title: "klastry aaaManage Hadoop w usłudze HDInsight przy użyciu programu PowerShell - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooperform administracyjne zadań hello klastrów platformy Hadoop w usłudze HDInsight przy użyciu programu Azure PowerShell."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="164da-103">Zarządzanie klastrami Hadoop w usłudze HDInsight przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="164da-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="164da-104">Program Azure PowerShell jest zaawansowane środowisko obsługi skryptów, można użyć toocontrol i zautomatyzować hello wdrażania i zarządzania obciążeń na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="164da-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="164da-105">W tym artykule dowiesz się, jak używać toomanage klastrów platformy Hadoop w usłudze Azure HDInsight przy użyciu konsoli programu Azure PowerShell do lokalnej za pośrednictwem hello programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="164da-105">In this article, you will learn how toomanage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through hello use of Windows PowerShell.</span></span> <span data-ttu-id="164da-106">Lista hello hello poleceń cmdlet programu PowerShell w usłudze HDInsight, zobacz [dokumentacji poleceń cmdlet usługi HDInsight][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="164da-106">For hello list of hello HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="164da-107">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="164da-107">**Prerequisites**</span></span>

<span data-ttu-id="164da-108">Przed rozpoczęciem tego artykułu, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="164da-108">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="164da-109">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="164da-109">**An Azure subscription**.</span></span> <span data-ttu-id="164da-110">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="164da-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="164da-111">Instalowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="164da-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="164da-112">Jeśli zainstalowano program Azure PowerShell w wersji 0,9 x, należy go odinstalować przed zainstalowaniem nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="164da-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="164da-113">Wersja hello toocheck hello zainstalowane środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="164da-113">toocheck hello version of hello installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="164da-114">toouninstall hello starszą wersję, uruchom programy i funkcje w Panelu sterowania hello.</span><span class="sxs-lookup"><span data-stu-id="164da-114">toouninstall hello older version, run Programs and Features in hello control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="164da-115">Tworzenie klastrów</span><span class="sxs-lookup"><span data-stu-id="164da-115">Create clusters</span></span>
<span data-ttu-id="164da-116">Zobacz [opartych na systemie Linux z tworzenia klastrów w usłudze HDInsight przy użyciu programu Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="164da-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="164da-117">Lista klastrów</span><span class="sxs-lookup"><span data-stu-id="164da-117">List clusters</span></span>
<span data-ttu-id="164da-118">W bieżącej subskrypcji hello, należy użyć następującego polecenia toolist hello wszystkich klastrów:</span><span class="sxs-lookup"><span data-stu-id="164da-118">Use hello following command toolist all clusters in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="164da-119">Pokaż klastra</span><span class="sxs-lookup"><span data-stu-id="164da-119">Show cluster</span></span>
<span data-ttu-id="164da-120">Użyj hello poniższe polecenie tooshow informacje określonego klastra w bieżącej subskrypcji hello:</span><span class="sxs-lookup"><span data-stu-id="164da-120">Use hello following command tooshow details of a specific cluster in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="164da-121">Usuwanie klastrów</span><span class="sxs-lookup"><span data-stu-id="164da-121">Delete clusters</span></span>
<span data-ttu-id="164da-122">Użyj hello następujące polecenia toodelete klastra:</span><span class="sxs-lookup"><span data-stu-id="164da-122">Use hello following command toodelete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="164da-123">Można również usunąć klaster przez usunięcie hello grupę zasobów, która zawiera hello klastra.</span><span class="sxs-lookup"><span data-stu-id="164da-123">You can also delete a cluster by removing hello resource group that contains hello cluster.</span></span> <span data-ttu-id="164da-124">Należy pamiętać, spowoduje to usunięcie wszystkich zasobów hello w grupie hello w tym hello domyślne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="164da-124">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="164da-125">Skalowanie klastrów</span><span class="sxs-lookup"><span data-stu-id="164da-125">Scale clusters</span></span>
<span data-ttu-id="164da-126">Skalowanie funkcji klastra Hello umożliwia toochange hello liczba węzłów procesu roboczego, używane przez klaster działa w usłudze Azure HDInsight bez konieczności toore — Tworzenie klastra hello.</span><span class="sxs-lookup"><span data-stu-id="164da-126">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="164da-127">Tylko klastry usługi HDInsight w wersji 3.1.3 lub nowszym są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="164da-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="164da-128">Jeśli masz pewności, jaka wersja hello klastra, można sprawdzić hello stronę właściwości.</span><span class="sxs-lookup"><span data-stu-id="164da-128">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="164da-129">Zobacz [klastrów listy i Pokaż](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="164da-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="164da-130">wpływ Hello Zmienianie hello liczby węzłów danych dla każdego typu obsługiwanych przez HDInsight klastra:</span><span class="sxs-lookup"><span data-stu-id="164da-130">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="164da-131">Usługa Hadoop</span><span class="sxs-lookup"><span data-stu-id="164da-131">Hadoop</span></span>

    <span data-ttu-id="164da-132">Można zwiększyć bezproblemowo hello liczba węzłów procesu roboczego w klastrze platformy Hadoop, który jest uruchomiony bez wpływu na wszystkie oczekujące lub uruchomione zadania.</span><span class="sxs-lookup"><span data-stu-id="164da-132">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="164da-133">W trakcie operacji hello również można przesłać nowe zadania.</span><span class="sxs-lookup"><span data-stu-id="164da-133">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="164da-134">Błędy w operacji skalowania bezpiecznie obsługi tak, aby hello klastra zawsze pozostanie w stanie funkcjonalności.</span><span class="sxs-lookup"><span data-stu-id="164da-134">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="164da-135">Podczas skalowania klastra usługi Hadoop w dół dzięki zmniejszeniu liczby hello węzły danych są ponownie uruchamiane niektórych usług hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="164da-135">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="164da-136">Powoduje to wszystkich uruchomionych i oczekujących zadań toofail na zakończenie hello hello operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="164da-136">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="164da-137">Można jednak Prześlij ponownie hello zadania po zakończeniu operacji hello.</span><span class="sxs-lookup"><span data-stu-id="164da-137">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="164da-138">HBase</span><span class="sxs-lookup"><span data-stu-id="164da-138">HBase</span></span>

    <span data-ttu-id="164da-139">Można bezproblemowo dodać lub usunąć klaster HBase tooyour węzłów, jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="164da-139">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="164da-140">Serwery regionalne automatycznie równoważy w ciągu kilku minut od zakończenia hello operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="164da-140">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="164da-141">Można jednak również ręcznie saldo serwerów regionalnych hello po zalogowaniu się headnode toohello klastra i uruchomione hello poniższych poleceń z poziomu okna wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="164da-141">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="164da-142">Storm</span><span class="sxs-lookup"><span data-stu-id="164da-142">Storm</span></span>

    <span data-ttu-id="164da-143">Można bezproblemowo dodać lub usunąć klaster Storm tooyour węzłów danych jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="164da-143">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="164da-144">Jednak po pomyślnym zakończeniu hello operacji skalowania, konieczne będzie toorebalance hello topologii.</span><span class="sxs-lookup"><span data-stu-id="164da-144">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="164da-145">Ponowne równoważenie można zrobić na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="164da-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="164da-146">STORM interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="164da-146">Storm web UI</span></span>
  * <span data-ttu-id="164da-147">Narzędzia interfejsu wiersza polecenia (CLI)</span><span class="sxs-lookup"><span data-stu-id="164da-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="164da-148">Zobacz toohello [dokumentację Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="164da-148">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="164da-149">Witaj interfejsu użytkownika sieci web platformy Storm w klastrze jest dostępny hello HDInsight:</span><span class="sxs-lookup"><span data-stu-id="164da-149">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![Zrównoważ skali storm w usłudze HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="164da-151">Poniżej przedstawiono przykładowy sposób hello toouse interfejsu wiersza polecenia polecenie topologii Storm hello toorebalance:</span><span class="sxs-lookup"><span data-stu-id="164da-151">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="164da-152">Witaj toochange rozmiar klastra usługi Hadoop przy użyciu programu Azure PowerShell, uruchom następujące polecenie na komputerze klienckim hello:</span><span class="sxs-lookup"><span data-stu-id="164da-152">toochange hello Hadoop cluster size by using Azure PowerShell, run hello following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="164da-153">Dostęp do przydzielenia/odwołania</span><span class="sxs-lookup"><span data-stu-id="164da-153">Grant/revoke access</span></span>
<span data-ttu-id="164da-154">Klastry HDInsight są powitania po HTTP usługi sieci web (wszystkie te usługi mają RESTful punkty końcowe):</span><span class="sxs-lookup"><span data-stu-id="164da-154">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="164da-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="164da-155">ODBC</span></span>
* <span data-ttu-id="164da-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="164da-156">JDBC</span></span>
* <span data-ttu-id="164da-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="164da-157">Ambari</span></span>
* <span data-ttu-id="164da-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="164da-158">Oozie</span></span>
* <span data-ttu-id="164da-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="164da-159">Templeton</span></span>

<span data-ttu-id="164da-160">Domyślnie te usługi są przyznawane dostępu.</span><span class="sxs-lookup"><span data-stu-id="164da-160">By default, these services are granted for access.</span></span> <span data-ttu-id="164da-161">Możesz można odwołać/Udziel dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="164da-161">You can revoke/grant hello access.</span></span> <span data-ttu-id="164da-162">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="164da-162">toorevoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="164da-163">toogrant:</span><span class="sxs-lookup"><span data-stu-id="164da-163">toogrant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="164da-164">Przez przyznawanie/odwoływanie dostępu hello, spowoduje zresetowanie hello klastra nazwę i hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="164da-164">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="164da-165">Ponadto można to zrobić za pomocą hello portalu.</span><span class="sxs-lookup"><span data-stu-id="164da-165">This can also be done via hello Portal.</span></span> <span data-ttu-id="164da-166">Zobacz [administrowania HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="164da-166">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="164da-167">Zaktualizuj poświadczenia użytkownika HTTP</span><span class="sxs-lookup"><span data-stu-id="164da-167">Update HTTP user credentials</span></span>
<span data-ttu-id="164da-168">To samo hello procedury jako [dostępu Grant/revoke HTTP](#grant/revoke-access). Jeśli klaster hello przyznano hello dostęp HTTP, należy je najpierw odwołać.</span><span class="sxs-lookup"><span data-stu-id="164da-168">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="164da-169">A następnie przyznać dostęp hello z nowymi poświadczeniami użytkownika HTTP.</span><span class="sxs-lookup"><span data-stu-id="164da-169">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="164da-170">Znajdź hello domyślne konto magazynu</span><span class="sxs-lookup"><span data-stu-id="164da-170">Find hello default storage account</span></span>
<span data-ttu-id="164da-171">Witaj następującego skryptu programu Powershell pokazano, jak tooget hello domyślna nazwa konta magazynu i hello domyślny klucz konta magazynu dla klastra.</span><span class="sxs-lookup"><span data-stu-id="164da-171">hello following Powershell script demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a><span data-ttu-id="164da-172">Znajdź hello grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="164da-172">Find hello resource group</span></span>
<span data-ttu-id="164da-173">W trybie Menedżera zasobów hello każdego klastra usługi HDInsight należy tooan grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="164da-173">In hello Resource Manager mode, each HDInsight cluster belongs tooan Azure resource group.</span></span>  <span data-ttu-id="164da-174">Grupa zasobów hello toofind:</span><span class="sxs-lookup"><span data-stu-id="164da-174">toofind hello resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="164da-175">Przesyłanie zadań</span><span class="sxs-lookup"><span data-stu-id="164da-175">Submit jobs</span></span>
<span data-ttu-id="164da-176">**zadania MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="164da-176">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="164da-177">Zobacz [próbek Uruchom MapReduce z Hadoop w HDInsight opartych na systemie Windows](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="164da-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="164da-178">**toosubmit zadań Hive**</span><span class="sxs-lookup"><span data-stu-id="164da-178">**toosubmit Hive jobs**</span></span>

<span data-ttu-id="164da-179">Zobacz [uruchamianie zapytań Hive przy użyciu programu PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="164da-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="164da-180">**toosubmit zadań Pig**</span><span class="sxs-lookup"><span data-stu-id="164da-180">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="164da-181">Zobacz [Pig uruchomienie zadania przy użyciu programu PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="164da-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="164da-182">**toosubmit Sqoop zadania**</span><span class="sxs-lookup"><span data-stu-id="164da-182">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="164da-183">Zobacz [Sqoop za pomocą usługi HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="164da-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="164da-184">**toosubmit Oozie zadania**</span><span class="sxs-lookup"><span data-stu-id="164da-184">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="164da-185">Zobacz [Oozie Użyj Hadoop toodefine i Uruchom przepływ pracy w usłudze HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="164da-185">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="164da-186">Przekazywanie danych tooAzure obiektu Blob magazynu</span><span class="sxs-lookup"><span data-stu-id="164da-186">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="164da-187">Zobacz [przekazywanie danych tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="164da-187">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="164da-188">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="164da-188">See Also</span></span>
* <span data-ttu-id="164da-189">[Dokumentację referencyjną polecenia cmdlet usługi HDInsight][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="164da-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="164da-190">[Administrowanie HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="164da-190">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="164da-191">[Administrowanie HDInsight przy użyciu interfejsu wiersza polecenia][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="164da-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="164da-192">[Tworzenie klastrów usługi HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="164da-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="164da-193">[Przekazywanie danych tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="164da-193">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="164da-194">[Przesyłanie zadań Hadoop programowo][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="164da-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="164da-195">[Wprowadzenie do usługi Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="164da-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
