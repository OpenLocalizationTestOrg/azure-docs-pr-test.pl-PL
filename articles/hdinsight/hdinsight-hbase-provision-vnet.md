---
title: aaaCreate HBase clusters w sieci wirtualnej - Azure | Dokumentacja firmy Microsoft
description: "Rozpoczynanie pracy z bazy danych HBase w usłudze Azure HDInsight. Dowiedz się, jak toocreate HDInsight HBase clusters w sieci wirtualnej Azure."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="58bac-104">Tworzenie klastrów HBase w usłudze HDInsight w sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="58bac-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="58bac-105">Dowiedz się, jak toocreate Azure HDInsight HBase clusters w [sieci wirtualnej Azure][1].</span><span class="sxs-lookup"><span data-stu-id="58bac-105">Learn how toocreate Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="58bac-106">Dzięki integracji sieci wirtualnej, klastrów HBase może być wdrożone toohello sam wirtualnych sieci jako aplikacje tak że aplikacje mogą komunikować się bezpośrednio, z bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="58bac-106">With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="58bac-107">Witaj korzyści:</span><span class="sxs-lookup"><span data-stu-id="58bac-107">hello benefits include:</span></span>

* <span data-ttu-id="58bac-108">Bezpośrednie połączenie między hello sieci web aplikacji toohello węzłów klastra HBase hello, co umożliwia komunikację za pomocą procedury zdalnej bazy danych HBase w języku Java wywoływania interfejsów API (RPC).</span><span class="sxs-lookup"><span data-stu-id="58bac-108">Direct connectivity of hello web application toohello nodes of hello HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="58bac-109">Większa wydajność, ponieważ nie ma ruchu przejdź przez wiele bram i moduły równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="58bac-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="58bac-110">Witaj możliwości tooprocess poufne informacje w bardziej bezpieczny sposób bez narażania publiczny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="58bac-110">hello ability tooprocess sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="58bac-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="58bac-111">Prerequisites</span></span>
<span data-ttu-id="58bac-112">Przed rozpoczęciem tego samouczka, musi mieć hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="58bac-112">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="58bac-113">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="58bac-113">**An Azure subscription**.</span></span> <span data-ttu-id="58bac-114">Zobacz artykuł [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="58bac-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="58bac-115">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="58bac-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="58bac-116">Zobacz [instalacja i używanie programu Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="58bac-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="58bac-117">Tworzenie klastra HBase w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="58bac-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="58bac-118">W tej sekcji, utworzyć klaster HBase opartych na systemie Linux z hello zależne konto magazynu Azure w sieci wirtualnej platformy Azure przy użyciu [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="58bac-118">In this section, you create a Linux-based HBase cluster with hello dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="58bac-119">Inne metody tworzenia klastrów i opis ustawień hello, zobacz [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="58bac-119">For other cluster creation methods and understanding hello settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="58bac-120">Więcej informacji o używaniu toocreate szablonu Hadoop klastrów w usłudze HDInsight, zobacz [klastrów utworzyć Hadoop w HDInsight przy użyciu szablonów usługi Azure Resource Manager](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="58bac-120">For more information about using a template toocreate Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="58bac-121">Niektóre właściwości są zakodowane na stałe do hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="58bac-121">Some properties are hard-coded into hello template.</span></span> <span data-ttu-id="58bac-122">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="58bac-122">For example:</span></span>
>
> * <span data-ttu-id="58bac-123">**Lokalizacja**: wschodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="58bac-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="58bac-124">**Wersja klastra**: 3.5</span><span class="sxs-lookup"><span data-stu-id="58bac-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="58bac-125">**Liczba węzłów procesu roboczego klastra**: 2</span><span class="sxs-lookup"><span data-stu-id="58bac-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="58bac-126">**Domyślne konto magazynu**: unikatowy ciąg</span><span class="sxs-lookup"><span data-stu-id="58bac-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="58bac-127">**Nazwa sieci wirtualnej**: &lt;nazwa klastra >-Sieć wirtualna</span><span class="sxs-lookup"><span data-stu-id="58bac-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="58bac-128">**Przestrzeń adresową sieci wirtualnej**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="58bac-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="58bac-129">**Nazwa podsieci**: podsieć1</span><span class="sxs-lookup"><span data-stu-id="58bac-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="58bac-130">**Zakres adresów podsieci**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="58bac-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="58bac-131">&lt;Nazwa klastra > jest zastępowany nazwą klastra hello udzielać przy użyciu szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="58bac-131">&lt;Cluster Name> is replaced with hello cluster name you provide when using hello template.</span></span>
>
>

1. <span data-ttu-id="58bac-132">Kliknij przycisk hello następującego szablonu hello tooopen obrazu w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="58bac-132">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="58bac-133">Szablon Hello znajduje się w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="58bac-133">hello template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="58bac-134">Z hello **wdrożenie niestandardowe** bloku, wprowadź hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="58bac-134">From hello **Custom deployment** blade, enter hello following properties:</span></span>

   * <span data-ttu-id="58bac-135">**Subskrypcja**: wybierz klaster usługi HDInsight hello toocreate subskrypcji platformy Azure używana, hello zależne konto magazynu i hello sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="58bac-135">**Subscription**: Select an Azure subscription used toocreate hello HDInsight cluster, hello dependent Storage account and hello Azure virtual network.</span></span>
   * <span data-ttu-id="58bac-136">**Grupa zasobów**: Wybierz **Utwórz nowy**i określ nazwę nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="58bac-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="58bac-137">**Lokalizacja**: Wybierz lokalizację dla grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="58bac-137">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="58bac-138">**ClusterName**: Wprowadź nazwę toobe klastra Hadoop hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="58bac-138">**ClusterName**: Enter a name for hello Hadoop cluster toobe created.</span></span>
   * <span data-ttu-id="58bac-139">**Nazwa logowania i hasło klastra**: hello domyślna nazwa logowania jest **admin**.</span><span class="sxs-lookup"><span data-stu-id="58bac-139">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="58bac-140">**Nazwa użytkownika SSH i hasło**: hello domyślna nazwa użytkownika to **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="58bac-140">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="58bac-141">Tę nazwę można zmienić.</span><span class="sxs-lookup"><span data-stu-id="58bac-141">You can rename it.</span></span>
   * <span data-ttu-id="58bac-142">**Zgadzam się toohello warunki użytkowania hello podanych powyżej**: (Wybierz)</span><span class="sxs-lookup"><span data-stu-id="58bac-142">**I agree toohello terms and hello conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="58bac-143">Kliknij pozycję **Kup**.</span><span class="sxs-lookup"><span data-stu-id="58bac-143">Click **Purchase**.</span></span> <span data-ttu-id="58bac-144">Trwa około 20 minut toocreate klastra.</span><span class="sxs-lookup"><span data-stu-id="58bac-144">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="58bac-145">Po utworzeniu klastra hello, możesz kliknąć hello bloku klastra w portalu tooopen hello go.</span><span class="sxs-lookup"><span data-stu-id="58bac-145">Once hello cluster is created, you can click hello cluster blade in hello portal tooopen it.</span></span>

<span data-ttu-id="58bac-146">Po ukończeniu samouczka hello można toodelete hello klastra.</span><span class="sxs-lookup"><span data-stu-id="58bac-146">After you complete hello tutorial, you might want toodelete hello cluster.</span></span> <span data-ttu-id="58bac-147">Dzięki usłudze HDInsight dane są przechowywane w usłudze Azure Storage, więc można bezpiecznie usunąć klaster, gdy nie jest używany.</span><span class="sxs-lookup"><span data-stu-id="58bac-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="58bac-148">Opłaty za klaster usługi HDInsight są naliczane nawet wtedy, gdy nie jest używany.</span><span class="sxs-lookup"><span data-stu-id="58bac-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="58bac-149">Ponieważ hello opłaty za klaster hello są wielokrotnie większe niż hello opłaty za magazyn, warto gospodarczego toodelete klastrów, gdy nie są używane.</span><span class="sxs-lookup"><span data-stu-id="58bac-149">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> <span data-ttu-id="58bac-150">Witaj instrukcje dotyczące usuwania klastra znajdują się [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu hello portalu Azure](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="58bac-150">For hello instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="58bac-151">Praca z nowego klastra HBase toobegin można użyć procedur hello w [rozpocząć korzystanie z platformy Hadoop w usłudze HDInsight HBase](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="58bac-151">toobegin working with your new HBase cluster, you can use hello procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="58bac-152">Połącz toohello klastra HBase przy użyciu interfejsów API RPC Java HBase</span><span class="sxs-lookup"><span data-stu-id="58bac-152">Connect toohello HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="58bac-153">Tworzenie infrastruktury jako usługi (IaaS) maszyny wirtualnej w tej samej sieci wirtualnej platformy Azure hello i hello tej samej podsieci.</span><span class="sxs-lookup"><span data-stu-id="58bac-153">Create an infrastructure as a service (IaaS) virtual machine into hello same Azure virtual network and hello same subnet.</span></span> <span data-ttu-id="58bac-154">Aby uzyskać instrukcje dotyczące tworzenia nowej maszyny wirtualnej IaaS, zobacz [tworzenia maszyny wirtualnej systemem Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="58bac-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="58bac-155">Następujące kroki hello w tym dokumencie, należy użyć następującej wartości konfiguracji sieci hello hello:</span><span class="sxs-lookup"><span data-stu-id="58bac-155">When following hello steps in this document, you must use hello following values for hello Network configuration:</span></span>

   * <span data-ttu-id="58bac-156">**Sieć wirtualna**: &lt;nazwa klastra >-Sieć wirtualna</span><span class="sxs-lookup"><span data-stu-id="58bac-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="58bac-157">**Podsieci**: podsieć1</span><span class="sxs-lookup"><span data-stu-id="58bac-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="58bac-158">Zastąp &lt;nazwa klastra > o nazwie hello są używane podczas tworzenia klastra usługi HDInsight hello w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="58bac-158">Replace &lt;Cluster name> with hello name you used when creating hello HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="58bac-159">Używając tych wartości, hello maszyna wirtualna jest umieszczona w hello sama sieć wirtualna i podsieć jako hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58bac-159">Using these values, hello virtual machine is placed in hello same virtual network and subnet as hello HDInsight cluster.</span></span> <span data-ttu-id="58bac-160">Ta konfiguracja pozwala toodirectly komunikują się ze sobą.</span><span class="sxs-lookup"><span data-stu-id="58bac-160">This configuration allows them toodirectly communicate with each other.</span></span> <span data-ttu-id="58bac-161">Brak toocreate sposób klastra usługi HDInsight z węzłem krawędzi puste.</span><span class="sxs-lookup"><span data-stu-id="58bac-161">There is a way toocreate an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="58bac-162">węzeł brzegowy Hello może być używane toomanage hello klastra.</span><span class="sxs-lookup"><span data-stu-id="58bac-162">hello edge node can be used toomanage hello cluster.</span></span>  <span data-ttu-id="58bac-163">Aby uzyskać więcej informacji, zobacz [użycia węzłów pusty krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="58bac-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="58bac-164">Korzystając z tooHBase tooconnect aplikacji Java zdalnie, możesz korzystać hello pełną nazwę domeny (FQDN).</span><span class="sxs-lookup"><span data-stu-id="58bac-164">When using a Java application tooconnect tooHBase remotely, you must use hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="58bac-165">toodetermine, należy uzyskać sufiks DNS konkretnego połączenia hello hello klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="58bac-165">toodetermine this, you must get hello connection-specific DNS suffix of hello HBase cluster.</span></span> <span data-ttu-id="58bac-166">toodo, których można używać jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="58bac-166">toodo that, you can use one of hello following methods:</span></span>

   * <span data-ttu-id="58bac-167">Użyj toomake przeglądarki sieci Web Ambari wywołania:</span><span class="sxs-lookup"><span data-stu-id="58bac-167">Use a Web browser toomake an Ambari call:</span></span>

     <span data-ttu-id="58bac-168">Przeglądaj toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / hostuje? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="58bac-168">Browse toohttps://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="58bac-169">Monitor przechodzi w stan to plik JSON o hello sufiksów DNS.</span><span class="sxs-lookup"><span data-stu-id="58bac-169">It turns a JSON file with hello DNS suffixes.</span></span>
   * <span data-ttu-id="58bac-170">Użyj narzędzia Ambari hello witryny sieci Web:</span><span class="sxs-lookup"><span data-stu-id="58bac-170">Use hello Ambari website:</span></span>

     1. <span data-ttu-id="58bac-171">Przeglądaj zbyt https://&lt;ClusterName >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="58bac-171">Browse too https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="58bac-172">Kliknij przycisk **hostów** z górnego menu hello.</span><span class="sxs-lookup"><span data-stu-id="58bac-172">Click **Hosts** from hello top menu.</span></span>
   * <span data-ttu-id="58bac-173">Użyj wywołań REST toomake Curl:</span><span class="sxs-lookup"><span data-stu-id="58bac-173">Use Curl toomake REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="58bac-174">W hello zwrócone dane JavaScript Object Notation (JSON), Znajdź pozycję "host_name" hello.</span><span class="sxs-lookup"><span data-stu-id="58bac-174">In hello JavaScript Object Notation (JSON) data returned, find hello "host_name" entry.</span></span> <span data-ttu-id="58bac-175">Zawiera ona hello FQDN hello węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="58bac-175">It contains hello FQDN for hello nodes in hello cluster.</span></span> <span data-ttu-id="58bac-176">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="58bac-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="58bac-177">Witaj część hello domeny nazwa rozpoczynający się od nazwy klastra hello jest hello sufiks DNS.</span><span class="sxs-lookup"><span data-stu-id="58bac-177">hello portion of hello domain name beginning with hello cluster name is hello DNS suffix.</span></span> <span data-ttu-id="58bac-178">Na przykład mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="58bac-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="58bac-179">Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="58bac-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="58bac-180">Użyj powitania po hello tooregister skrypt programu PowerShell usługi Azure **Get ClusterDetail** funkcji, która może być sufiks DNS używany tooreturn hello:</span><span class="sxs-lookup"><span data-stu-id="58bac-180">Use hello following Azure PowerShell script tooregister hello **Get-ClusterDetail** function, which can be used tooreturn hello DNS suffix:</span></span>

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     <span data-ttu-id="58bac-181">Po uruchamianie skryptu programu Azure PowerShell hello następujące hello Użyj polecenie sufiks DNS hello tooreturn przy użyciu hello **Get ClusterDetail** funkcji.</span><span class="sxs-lookup"><span data-stu-id="58bac-181">After running hello Azure PowerShell script, use hello following command tooreturn hello DNS suffix by using hello **Get-ClusterDetail** function.</span></span> <span data-ttu-id="58bac-182">Określ nazwę klastra HDInsight HBase, nazwę administratora i hasło administratora kopii, korzystając z tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="58bac-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="58bac-183">To polecenie zwraca hello sufiks DNS.</span><span class="sxs-lookup"><span data-stu-id="58bac-183">This command returns hello DNS suffix.</span></span> <span data-ttu-id="58bac-184">Na przykład **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="58bac-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

<span data-ttu-id="58bac-185">tooverify, który hello maszyny wirtualnej mogą komunikować się z hello klastra HBase, użyj polecenia hello `ping headnode0.<dns suffix>` z hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="58bac-185">tooverify that hello virtual machine can communicate with hello HBase cluster, use hello command `ping headnode0.<dns suffix>` from hello virtual machine.</span></span> <span data-ttu-id="58bac-186">Na przykład headnode0.mycluster.b1.cloudapp.net ping.</span><span class="sxs-lookup"><span data-stu-id="58bac-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="58bac-187">toouse tych informacji w aplikacji Java, można wykonać kroki hello w [aplikacji Java toobuild Użyj Maven, korzystających z bazy danych HBase w usłudze HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate aplikacji.</span><span class="sxs-lookup"><span data-stu-id="58bac-187">toouse this information in a Java application, you can follow hello steps in [Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate an application.</span></span> <span data-ttu-id="58bac-188">Aplikacja hello toohave połączenia zdalnego serwera bazy danych HBase tooa, zmodyfikuj hello **hbase-site.xml** pliku w ten przykład toouse hello FQDN dozorcy.</span><span class="sxs-lookup"><span data-stu-id="58bac-188">toohave hello application connect tooa remote HBase server, modify hello **hbase-site.xml** file in this example toouse hello FQDN for Zookeeper.</span></span> <span data-ttu-id="58bac-189">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="58bac-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="58bac-190">Aby uzyskać więcej informacji na temat rozpoznawania nazw w sieci wirtualnych platformy Azure w tym jak toouse własny serwer DNS, zobacz [rozpoznawania nazw (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="58bac-190">For more information about name resolution in Azure virtual networks, including how toouse your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="58bac-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="58bac-191">Next steps</span></span>
<span data-ttu-id="58bac-192">W tym samouczku można przedstawiono sposób toocreate klaster HBase.</span><span class="sxs-lookup"><span data-stu-id="58bac-192">In this tutorial, you learned how toocreate an HBase cluster.</span></span> <span data-ttu-id="58bac-193">toolearn więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="58bac-193">toolearn more, see:</span></span>

* [<span data-ttu-id="58bac-194">Rozpoczynanie pracy z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="58bac-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="58bac-195">Użyj węzłami pusty krawędzi w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="58bac-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="58bac-196">Konfigurowanie replikacji bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="58bac-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="58bac-197">Tworzenie klastrów Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="58bac-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="58bac-198">Rozpoczynanie pracy z platformą Hadoop w usłudze HDInsight przy użyciu bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="58bac-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="58bac-199">Analizowanie Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="58bac-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="58bac-200">[Omówienie sieci wirtualnej][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="58bac-200">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Szczegóły udostępniania dla nowego klastra HBase hello"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Użyj akcji skryptu toocustomize klastra HBase"

[azure-preview-portal]: https://portal.azure.com
