---
title: replikacja klastra HBase aaaConfigure w ramach sieci wirtualnej - Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak replikacji bazy danych HBase tooconfigure obciążenia równoważenia wysokiej dostępności, zero przestoju migracji/update z jednego tooanother wersji usługi HDInsight i odzyskiwania po awarii."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="50732-103">Konfigurowanie replikacji bazy danych HBase klastra w ramach sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="50732-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="50732-104">Dowiedz się, jak tooconfigure replikacji bazy danych HBase w jedną sieć wirtualną (VNet) lub między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="50732-104">Learn how tooconfigure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="50732-105">Replikacja klastra używa metodologii wypychania źródła.</span><span class="sxs-lookup"><span data-stu-id="50732-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="50732-106">Klaster HBase można źródła lub miejsca docelowego, lub jego jednocześnie spełnić obie role.</span><span class="sxs-lookup"><span data-stu-id="50732-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="50732-107">Replikacja jest asynchroniczne, a celem hello replikacji jest spójność ostateczna.</span><span class="sxs-lookup"><span data-stu-id="50732-107">Replication is asynchronous, and hello goal of replication is eventual consistency.</span></span> <span data-ttu-id="50732-108">Odebrania źródła hello rodziny kolumn tooa edycji z włączoną replikacją, tej edycji jest propagowany tooall klastrów docelowych.</span><span class="sxs-lookup"><span data-stu-id="50732-108">When hello source receives an edit tooa column family with replication enabled, that edit is propagated tooall destination clusters.</span></span> <span data-ttu-id="50732-109">Gdy dane są replikowane z jednego klastra tooanother, hello źródłowego klastra i wszystkich klastrów, które mają już używane dane hello są śledzone tooprevent replikacji pętle.</span><span class="sxs-lookup"><span data-stu-id="50732-109">When data is replicated from one cluster tooanother, hello source cluster and all clusters that have already consumed hello data are tracked tooprevent replication loops.</span></span>

<span data-ttu-id="50732-110">W tym samouczku skonfigurujesz replikacji źródłowego i docelowego.</span><span class="sxs-lookup"><span data-stu-id="50732-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="50732-111">Dla innych topologiach klastra [Apache HBase podręcznik](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="50732-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="50732-112">HBase replikacji przypadków użycia pojedynczej sieci wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="50732-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="50732-113">Równoważenie obciążenia — na przykład uruchomione skanowanie lub zadań MapReduce w klastrze docelowym hello i wprowadzania danych w klastrze źródłowym hello</span><span class="sxs-lookup"><span data-stu-id="50732-113">Load balancing--for example, running scans or MapReduce jobs on hello destination cluster and ingesting data on hello source cluster</span></span>
* <span data-ttu-id="50732-114">Wysoka dostępność</span><span class="sxs-lookup"><span data-stu-id="50732-114">High availability</span></span>
* <span data-ttu-id="50732-115">Migrowanie danych z jednego tooanother klastra HBase</span><span class="sxs-lookup"><span data-stu-id="50732-115">Migrating data from one HBase cluster tooanother</span></span>
* <span data-ttu-id="50732-116">Uaktualnianie klastra usługi Azure HDInsight z jednej wersji tooanother</span><span class="sxs-lookup"><span data-stu-id="50732-116">Upgrading an Azure HDInsight cluster from one version tooanother</span></span>

<span data-ttu-id="50732-117">HBase przypadków użycia replikacji dla dwóch sieci wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="50732-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="50732-118">Odzyskiwanie po awarii</span><span class="sxs-lookup"><span data-stu-id="50732-118">Disaster recovery</span></span>
* <span data-ttu-id="50732-119">Równoważenie obciążenia i partycjonowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="50732-119">Load balancing and partitioning hello application</span></span>
* <span data-ttu-id="50732-120">Wysoka dostępność</span><span class="sxs-lookup"><span data-stu-id="50732-120">High availability</span></span>

<span data-ttu-id="50732-121">Klastry są replikowane za pomocą [akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md) skrypty znajdujące się w [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="50732-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50732-122">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="50732-122">Prerequisites</span></span>
<span data-ttu-id="50732-123">Przed rozpoczęciem tego samouczka musisz dysponować subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="50732-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="50732-124">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="50732-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-hello-environments"></a><span data-ttu-id="50732-125">Konfigurowanie środowisk hello</span><span class="sxs-lookup"><span data-stu-id="50732-125">Configure hello environments</span></span>

<span data-ttu-id="50732-126">Istnieją trzy możliwe konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="50732-126">There are three possible configurations:</span></span>

- <span data-ttu-id="50732-127">Dwoma klastrami HBase w jednej sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="50732-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="50732-128">Dwoma klastrami HBase w dwóch różnych sieciach wirtualnych w hello tego samego regionu</span><span class="sxs-lookup"><span data-stu-id="50732-128">Two HBase clusters in two different virtual networks in hello same region</span></span>
- <span data-ttu-id="50732-129">Dwoma klastrami HBase w dwóch różnych sieciach wirtualnych w dwóch różnych regionach (replikacja geograficzna)</span><span class="sxs-lookup"><span data-stu-id="50732-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="50732-130">toomake go łatwiejsze środowisk hello tooconfigure, utworzono niektóre [szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50732-130">toomake it easier tooconfigure hello environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="50732-131">Jeśli wolisz tooconfigure hello środowisk przy użyciu innych metod, zobacz:</span><span class="sxs-lookup"><span data-stu-id="50732-131">If you prefer tooconfigure hello environments by using other methods, see:</span></span>

- [<span data-ttu-id="50732-132">Tworzenie klastrów opartych na systemie Linux platformą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="50732-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="50732-133">Tworzenie klastrów HBase w sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="50732-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="50732-134">Skonfiguruj jedną sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="50732-134">Configure one virtual network</span></span>

<span data-ttu-id="50732-135">Kliknij przycisk powitania po obrazu toocreate dwóch klastrów HBase w hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="50732-135">Click hello following image toocreate two HBase clusters in hello same virtual network.</span></span> <span data-ttu-id="50732-136">Szablon Hello jest przechowywany w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="50732-136">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a><span data-ttu-id="50732-137">Skonfigurować dwie sieci wirtualne w hello tego samego regionu</span><span class="sxs-lookup"><span data-stu-id="50732-137">Configure two virtual networks in hello same region</span></span>

<span data-ttu-id="50732-138">Kliknij przycisk powitania po toocreate obrazu dwie sieci wirtualne sieci wirtualnej komunikacji równorzędnej i dwoma klastrami HBase w hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="50732-138">Click hello following image toocreate two virtual networks with VNet peering and two HBase clusters in hello same region.</span></span> <span data-ttu-id="50732-139">Szablon Hello jest przechowywany w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="50732-139">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



<span data-ttu-id="50732-140">Ten scenariusz wymaga [sieci wirtualnej komunikacji równorzędnej](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50732-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="50732-141">Szablon Hello umożliwia sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="50732-141">hello template enables VNet peering.</span></span>   

<span data-ttu-id="50732-142">Replikacja bazy danych HBase korzysta hello dozorcy maszyn wirtualnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="50732-142">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="50732-143">Skonfiguruj statyczne adresy IP dla węzły dozorcy HBase docelowego hello.</span><span class="sxs-lookup"><span data-stu-id="50732-143">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="50732-144">**tooconfigure statycznych adresów IP**</span><span class="sxs-lookup"><span data-stu-id="50732-144">**tooconfigure static IP addresses**</span></span>

1. <span data-ttu-id="50732-145">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="50732-145">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="50732-146">W menu po lewej stronie powitania kliknij **grup zasobów**.</span><span class="sxs-lookup"><span data-stu-id="50732-146">From hello left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="50732-147">Kliknij grupę zasobów zawierającą klaster HBase hello docelowego.</span><span class="sxs-lookup"><span data-stu-id="50732-147">Click your resource group that contains hello destination HBase cluster.</span></span> <span data-ttu-id="50732-148">Jest to grupa zasobów hello określonej stosowania hello Menedżera zasobów szablonu toocreate hello środowiska.</span><span class="sxs-lookup"><span data-stu-id="50732-148">This is hello resource group that you specified when you used hello Resource Manager template toocreate hello environment.</span></span> <span data-ttu-id="50732-149">Można użyć toonarrow filtru hello pozycji listy hello.</span><span class="sxs-lookup"><span data-stu-id="50732-149">You can use hello filter toonarrow down hello list.</span></span> <span data-ttu-id="50732-150">Lista zasobów zawiera dwie sieci wirtualne hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="50732-150">You can see a list of resources that contains hello two virtual networks.</span></span>
4. <span data-ttu-id="50732-151">Kliknij przycisk hello sieć wirtualna, która zawiera klastra HBase hello docelowego.</span><span class="sxs-lookup"><span data-stu-id="50732-151">Click hello virtual network that contains hello destination HBase cluster.</span></span> <span data-ttu-id="50732-152">Na przykład kliknij pozycję **xxxx vnet2**.</span><span class="sxs-lookup"><span data-stu-id="50732-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="50732-153">Widać trzech urządzeń o nazwach rozpoczynających się od **kart-zookeepermode -**.</span><span class="sxs-lookup"><span data-stu-id="50732-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="50732-154">Te urządzenia są maszyny wirtualne dozorcy hello trzech.</span><span class="sxs-lookup"><span data-stu-id="50732-154">Those devices are hello three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="50732-155">Kliknij jeden z hello dozorcy maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="50732-155">Click one of hello ZooKeeper VMs.</span></span>
6. <span data-ttu-id="50732-156">Kliknij przycisk **konfiguracje adresów IP**.</span><span class="sxs-lookup"><span data-stu-id="50732-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="50732-157">Kliknij przycisk **ipConfig1** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="50732-157">Click **ipConfig1** from hello list.</span></span>
8. <span data-ttu-id="50732-158">Kliknij przycisk **statycznych**i zanotuj adres IP rzeczywistego hello.</span><span class="sxs-lookup"><span data-stu-id="50732-158">Click **Static**, and write down hello actual IP address.</span></span> <span data-ttu-id="50732-159">Po uruchomieniu replikacji tooenable akcji skryptu hello należy hello adresu IP.</span><span class="sxs-lookup"><span data-stu-id="50732-159">You will need hello IP address when you run hello script action tooenable replication.</span></span>

  ![HDInsight HBase replikacji dozorcy statycznego adresu IP](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="50732-161">Powtórz krok 6 tooset hello statyczny adres IP dla hello innych dwa węzły dozorcy.</span><span class="sxs-lookup"><span data-stu-id="50732-161">Repeat step 6 tooset hello static IP address for hello other two ZooKeeper nodes.</span></span>

<span data-ttu-id="50732-162">W scenariuszu sieci wirtualnej między hello, musisz użyć hello **- ip** przełącznika podczas wywoływania metody hello **hdi_enable_replication.sh** akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="50732-162">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="50732-163">Skonfigurować dwie sieci wirtualne w dwóch różnych regionach.</span><span class="sxs-lookup"><span data-stu-id="50732-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="50732-164">Kliknij przycisk powitania po toocreate obrazu dwie sieci wirtualne w dwóch różnych regionach.</span><span class="sxs-lookup"><span data-stu-id="50732-164">Click hello following image toocreate two virtual networks in two different regions.</span></span> <span data-ttu-id="50732-165">Szablon Hello jest przechowywany w publicznego kontenera obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="50732-165">hello template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

<span data-ttu-id="50732-166">Tworzenie bramy sieci VPN między dwiema sieciami wirtualnymi hello.</span><span class="sxs-lookup"><span data-stu-id="50732-166">Create a VPN gateway between hello two virtual networks.</span></span> <span data-ttu-id="50732-167">Aby uzyskać instrukcje, zobacz [tworzenie sieci wirtualnej za pomocą połączenia lokacja lokacja](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="50732-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="50732-168">Replikacja bazy danych HBase korzysta hello dozorcy maszyn wirtualnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="50732-168">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="50732-169">Skonfiguruj statyczne adresy IP dla węzły dozorcy HBase docelowego hello.</span><span class="sxs-lookup"><span data-stu-id="50732-169">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="50732-170">tooconfigure statycznego adresu IP, zobacz sekcję "Konfigurowanie dwie sieci wirtualne w hello tego samego regionu" hello, w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="50732-170">tooconfigure static IP, see hello "Configure two virtual networks in hello same region" section in this article.</span></span>

<span data-ttu-id="50732-171">W scenariuszu sieci wirtualnej między hello, musisz użyć hello **- ip** przełącznika podczas wywoływania metody hello **hdi_enable_replication.sh** akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="50732-171">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="50732-172">Danych testu obciążenia</span><span class="sxs-lookup"><span data-stu-id="50732-172">Load test data</span></span>

<span data-ttu-id="50732-173">Podczas replikowania klastra, należy określić hello tooreplicate tabel.</span><span class="sxs-lookup"><span data-stu-id="50732-173">When you replicate a cluster, you must specify hello tables tooreplicate.</span></span> <span data-ttu-id="50732-174">W tej sekcji zostanie załadowany niektóre dane w klastrze źródłowym hello.</span><span class="sxs-lookup"><span data-stu-id="50732-174">In this section, you will load some data into hello source cluster.</span></span> <span data-ttu-id="50732-175">W następnej sekcji hello spowoduje włączenie replikacji między dwoma klastrami hello.</span><span class="sxs-lookup"><span data-stu-id="50732-175">In hello next section, you will enable replication between hello two clusters.</span></span>

<span data-ttu-id="50732-176">Postępuj zgodnie z instrukcjami hello [samouczek HBase: rozpoczęcie pracy z opartą na systemie Linux platformą Hadoop w usłudze HDInsight przy użyciu bazy danych Apache HBase](hdinsight-hbase-tutorial-get-started-linux.md) toocreate **kontaktów** tabeli i wstawić dane do tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="50732-176">Follow hello instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate a **Contacts** table and insert some data into hello table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="50732-177">Włączanie replikacji</span><span class="sxs-lookup"><span data-stu-id="50732-177">Enable replication</span></span>

<span data-ttu-id="50732-178">Witaj następujące kroki pokazują, jak toocall hello skryptu akcji skryptu z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="50732-178">hello following steps show how toocall hello script action script from hello Azure portal.</span></span> <span data-ttu-id="50732-179">Do uruchomienia akcji skryptu za pomocą programu Azure PowerShell i hello Azure interfejsu wiersza polecenia (CLI), zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="50732-179">For running a script action by using Azure PowerShell and hello Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="50732-180">**Replikacja bazy danych HBase tooenable z hello portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="50732-180">**tooenable HBase replication from hello Azure portal**</span></span>

1. <span data-ttu-id="50732-181">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="50732-181">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="50732-182">Otwórz klaster HBase hello źródła.</span><span class="sxs-lookup"><span data-stu-id="50732-182">Open hello source HBase cluster.</span></span>
3. <span data-ttu-id="50732-183">W menu klastra hello, kliknij **akcji skryptu**.</span><span class="sxs-lookup"><span data-stu-id="50732-183">From hello cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="50732-184">Kliknij przycisk **przesłać nowe** od góry hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="50732-184">Click **Submit New** from hello top of hello blade.</span></span>
5. <span data-ttu-id="50732-185">Wybierz lub wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="50732-185">Select or enter hello following information:</span></span>

  - <span data-ttu-id="50732-186">**Nazwa**: wprowadź **włączyć replikację**.</span><span class="sxs-lookup"><span data-stu-id="50732-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="50732-187">**Adres URL skryptu bash**: wprowadź **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="50732-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="50732-188">**HEAD**: wybrane.</span><span class="sxs-lookup"><span data-stu-id="50732-188">**Head**: Selected.</span></span> <span data-ttu-id="50732-189">Wyczyść hello innych typów węzłów.</span><span class="sxs-lookup"><span data-stu-id="50732-189">Clear hello other node types.</span></span>
  - <span data-ttu-id="50732-190">**Parametry**: hello następujące przykładowe parametry. Włączanie replikacji wszystkie istniejące tabele hello i skopiuj wszystkie dane hello z klastra docelowego toohello hello źródła klastra:</span><span class="sxs-lookup"><span data-stu-id="50732-190">**Parameters**: hello following sample parameters enable replication for all hello existing tables and copy all hello data from hello source cluster toohello destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="50732-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="50732-191">Click **Create**.</span></span> <span data-ttu-id="50732-192">Witaj skryptu może zająć trochę czasu, szczególnie, gdy argument - COPYDATA: hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="50732-192">hello script can take some time, especially when hello -copydata argument is used.</span></span>

<span data-ttu-id="50732-193">Wymagane argumenty:</span><span class="sxs-lookup"><span data-stu-id="50732-193">Required arguments:</span></span>

|<span data-ttu-id="50732-194">Nazwa</span><span class="sxs-lookup"><span data-stu-id="50732-194">Name</span></span>|<span data-ttu-id="50732-195">Opis</span><span class="sxs-lookup"><span data-stu-id="50732-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="50732-196">-s, - src-klaster</span><span class="sxs-lookup"><span data-stu-id="50732-196">-s, --src-cluster</span></span> | <span data-ttu-id="50732-197">Podaj nazwę DNS hello klastra HBase hello źródła.</span><span class="sxs-lookup"><span data-stu-id="50732-197">Specify hello DNS name of hello source HBase cluster.</span></span> <span data-ttu-id="50732-198">Na przykład: hbsrccluster -s, klaster — src = hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="50732-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="50732-199">-d, klaster — czasu letniego</span><span class="sxs-lookup"><span data-stu-id="50732-199">-d, --dst-cluster</span></span> | <span data-ttu-id="50732-200">Podaj nazwę DNS hello hello przeznaczenia (repliki) klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="50732-200">Specify hello DNS name of hello destination (replica) HBase cluster.</span></span> <span data-ttu-id="50732-201">Na przykład: dsthbcluster -s, klaster — src = dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="50732-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="50732-202">-sp, w--src hasła narzędzia ambari</span><span class="sxs-lookup"><span data-stu-id="50732-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="50732-203">Określ hasło administratora hello dla narzędzia Ambari na klaster HBase hello źródła.</span><span class="sxs-lookup"><span data-stu-id="50732-203">Specify hello admin password for Ambari on hello source HBase cluster.</span></span> |
|<span data-ttu-id="50732-204">— punkt dystrybucji, w czasu letniego — hasła narzędzia ambari</span><span class="sxs-lookup"><span data-stu-id="50732-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="50732-205">Określ hasło administratora hello dla narzędzia Ambari na klaster HBase hello docelowego.</span><span class="sxs-lookup"><span data-stu-id="50732-205">Specify hello admin password for Ambari on hello destination HBase cluster.</span></span>|

<span data-ttu-id="50732-206">Argumenty opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="50732-206">Optional arguments:</span></span>

|<span data-ttu-id="50732-207">Nazwa</span><span class="sxs-lookup"><span data-stu-id="50732-207">Name</span></span>|<span data-ttu-id="50732-208">Opis</span><span class="sxs-lookup"><span data-stu-id="50732-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="50732-209">-su,--src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="50732-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="50732-210">Określ nazwy użytkownika administratora hello Ambari na klaster HBase hello źródła.</span><span class="sxs-lookup"><span data-stu-id="50732-210">Specify hello admin username for Ambari on hello source HBase cluster.</span></span> <span data-ttu-id="50732-211">Witaj, wartość domyślna to **admin**.</span><span class="sxs-lookup"><span data-stu-id="50732-211">hello default value is **admin**.</span></span> |
|<span data-ttu-id="50732-212">-du, czasu letniego — ambari użytkownika</span><span class="sxs-lookup"><span data-stu-id="50732-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="50732-213">Podaj nazwę użytkownika administratora hello dla narzędzia Ambari, na klaster HBase hello docelowego.</span><span class="sxs-lookup"><span data-stu-id="50732-213">Specify hello admin username for Ambari on hello destination HBase cluster.</span></span> <span data-ttu-id="50732-214">Witaj, wartość domyślna to **admin**.</span><span class="sxs-lookup"><span data-stu-id="50732-214">hello default value is **admin**.</span></span> |
|<span data-ttu-id="50732-215">-t,--lista tabeli</span><span class="sxs-lookup"><span data-stu-id="50732-215">-t, --table-list</span></span> | <span data-ttu-id="50732-216">Określ toobe tabel hello replikowane.</span><span class="sxs-lookup"><span data-stu-id="50732-216">Specify hello tables toobe replicated.</span></span> <span data-ttu-id="50732-217">Na przykład:--lista tabeli = "Tabela1; table2 Tabela3".</span><span class="sxs-lookup"><span data-stu-id="50732-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="50732-218">Jeśli nie określisz tabel, replikacja wszystkich istniejących tabel HBase.</span><span class="sxs-lookup"><span data-stu-id="50732-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="50732-219">-m,--maszyny</span><span class="sxs-lookup"><span data-stu-id="50732-219">-m, --machine</span></span> | <span data-ttu-id="50732-220">Określ hello węzła głównego w którym zostanie uruchomiony hello akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="50732-220">Specify hello head node where hello script action will run.</span></span> <span data-ttu-id="50732-221">wartość Hello jest hn1 lub hn0.</span><span class="sxs-lookup"><span data-stu-id="50732-221">hello value is either hn1 or hn0.</span></span> <span data-ttu-id="50732-222">Ponieważ hn0 jest zazwyczaj coraz bardziej zajęty, zalecamy używanie hn1.</span><span class="sxs-lookup"><span data-stu-id="50732-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="50732-223">Użyj tej opcji, po uruchomieniu skryptu hello $0 jako akcja skryptu z portalu usługi HDInsight hello lub Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50732-223">You use this option when you're running hello $0 script as a script action from hello HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="50732-224">-ip</span><span class="sxs-lookup"><span data-stu-id="50732-224">-ip</span></span> | <span data-ttu-id="50732-225">Ten argument jest wymagany, gdy w przypadku włączenia replikacji między dwiema sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="50732-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="50732-226">Ten argument działa jako przełącznika toouse hello statycznych adresów IP dozorcy węzłów z klastrów repliki zamiast nazw FQDN.</span><span class="sxs-lookup"><span data-stu-id="50732-226">This argument acts as a switch toouse hello static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="50732-227">Hello statyczne adresy IP muszą toobe wstępnie przed włączeniem replikacji.</span><span class="sxs-lookup"><span data-stu-id="50732-227">hello static IPs need toobe preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="50732-228">-cp, - COPYDATA:</span><span class="sxs-lookup"><span data-stu-id="50732-228">-cp, -copydata</span></span> | <span data-ttu-id="50732-229">Włącz migrację hello istniejące dane w tabelach hello, w którym replikacja jest włączona.</span><span class="sxs-lookup"><span data-stu-id="50732-229">Enable hello migration of existing data on hello tables where replication is enabled.</span></span> |
|<span data-ttu-id="50732-230">-obr. / min, - replikacja-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="50732-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="50732-231">Włącz replikację na Phoenix tabel systemowych.</span><span class="sxs-lookup"><span data-stu-id="50732-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="50732-232">*Użyj tej opcji z rozwagą.*</span><span class="sxs-lookup"><span data-stu-id="50732-232">*Use this option with caution.*</span></span> <span data-ttu-id="50732-233">Firma Microsoft zaleca, ponownie utwórz tabele Phoenix w klastrach repliki przed skorzystaniem z tego skryptu.</span><span class="sxs-lookup"><span data-stu-id="50732-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="50732-234">-h, — pomoc</span><span class="sxs-lookup"><span data-stu-id="50732-234">-h, --help</span></span> | <span data-ttu-id="50732-235">Wyświetl informacje o użyciu.</span><span class="sxs-lookup"><span data-stu-id="50732-235">Display usage information.</span></span> |

<span data-ttu-id="50732-236">Witaj print_usage() części hello [skryptu](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) zawiera szczegółowy opis parametrów.</span><span class="sxs-lookup"><span data-stu-id="50732-236">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="50732-237">Po akcji skryptu hello jest pomyślnie wdrożone, można użyć klastra HBase docelowego toohello tooconnect SSH i sprawdź, czy dane hello zostały zreplikowane.</span><span class="sxs-lookup"><span data-stu-id="50732-237">After hello script action is successfully deployed, you can use SSH tooconnect toohello destination HBase cluster, and verify hello data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="50732-238">Scenariusze replikacji</span><span class="sxs-lookup"><span data-stu-id="50732-238">Replication scenarios</span></span>

<span data-ttu-id="50732-239">Hello poniższej liście przedstawiono niektórych przypadków użycia ogólne i ich ustawienia parametru:</span><span class="sxs-lookup"><span data-stu-id="50732-239">hello following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="50732-240">**Włączanie replikacji na wszystkich tabel między klastrami hello dwa**.</span><span class="sxs-lookup"><span data-stu-id="50732-240">**Enable replication on all tables between hello two clusters**.</span></span> <span data-ttu-id="50732-241">Ten scenariusz nie wymaga hello kopiowania/migracji istniejących danych w tabelach hello i nie używa Phoenix tabel.</span><span class="sxs-lookup"><span data-stu-id="50732-241">This scenario does not require hello copy/migration of existing data on hello tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="50732-242">Użyj hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="50732-242">Use hello following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="50732-243">**Włącz replikację na określonych tabel**.</span><span class="sxs-lookup"><span data-stu-id="50732-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="50732-244">Użyj po replikacji tooenable parametry table1 i table2, Tabela3 hello:</span><span class="sxs-lookup"><span data-stu-id="50732-244">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="50732-245">**Włącz replikację na określonych tabel i skopiuj hello istniejących danych**.</span><span class="sxs-lookup"><span data-stu-id="50732-245">**Enable replication on specific tables and copy hello existing data**.</span></span> <span data-ttu-id="50732-246">Użyj po replikacji tooenable parametry table1 i table2, Tabela3 hello:</span><span class="sxs-lookup"><span data-stu-id="50732-246">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="50732-247">**Włączanie replikacji na wszystkich tabel z replikacji metadanych phoenix ze źródła toodestination**.</span><span class="sxs-lookup"><span data-stu-id="50732-247">**Enable replication on all tables with replicating phoenix metadata from source toodestination**.</span></span> <span data-ttu-id="50732-248">Phoenix metadanych replikacji nie jest doskonała i powinno być włączone, należy zachować ostrożność przy.</span><span class="sxs-lookup"><span data-stu-id="50732-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="50732-249">Skopiuj i przeprowadzić migrację danych</span><span class="sxs-lookup"><span data-stu-id="50732-249">Copy and migrate data</span></span>

<span data-ttu-id="50732-250">Istnieją dwa skrypty akcji skryptu oddzielne kopiowanie migracji danych po włączeniu replikacji:</span><span class="sxs-lookup"><span data-stu-id="50732-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="50732-251">[Skrypt dla małych tabel](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (kilka gigabajtów kopia rozmiarze i ogólną jest toofinish oczekiwanego w mniej niż godzinę)</span><span class="sxs-lookup"><span data-stu-id="50732-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected toofinish in less than one hour)</span></span>

- <span data-ttu-id="50732-252">[Skrypt dla dużych tabel](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (Oczekiwano tootake dłużej niż godzinę toocopy)</span><span class="sxs-lookup"><span data-stu-id="50732-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected tootake longer than one hour toocopy)</span></span>

<span data-ttu-id="50732-253">Możesz wykonać hello tej samej procedury w [włączyć replikację](#enable-replication) akcji skryptu hello toocall z hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="50732-253">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="50732-254">Witaj print_usage() części hello [skryptu](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) zawiera szczegółowy opis parametrów.</span><span class="sxs-lookup"><span data-stu-id="50732-254">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="50732-255">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="50732-255">Scenarios</span></span>

- <span data-ttu-id="50732-256">**Skopiuj określonych tabel (test1 test2 i test3) dla wszystkich wierszy edytować do tej chwili (bieżąca sygnatura czasowa)**:</span><span class="sxs-lookup"><span data-stu-id="50732-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="50732-257">lub</span><span class="sxs-lookup"><span data-stu-id="50732-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="50732-258">**Skopiuj określonych tabel z określonego przedziału czasu**:</span><span class="sxs-lookup"><span data-stu-id="50732-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="50732-259">Wyłącz replikację</span><span class="sxs-lookup"><span data-stu-id="50732-259">Disable replication</span></span>

<span data-ttu-id="50732-260">toodisable replikacji, użyj innego skryptu akcji skryptu znajdujący się w [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="50732-260">toodisable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="50732-261">Możesz wykonać hello tej samej procedury w [włączyć replikację](#enable-replication) akcji skryptu hello toocall z hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="50732-261">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="50732-262">Witaj print_usage() części hello [skryptu](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) zawiera szczegółowy opis parametrów.</span><span class="sxs-lookup"><span data-stu-id="50732-262">hello print_usage() section of hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="50732-263">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="50732-263">Scenarios</span></span>

- <span data-ttu-id="50732-264">**Wyłącz replikację dla wszystkich tabel**:</span><span class="sxs-lookup"><span data-stu-id="50732-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="50732-265">lub</span><span class="sxs-lookup"><span data-stu-id="50732-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="50732-266">**Wyłącz replikację w określonych tabel (Tabela1 table2 i Tabela3)**:</span><span class="sxs-lookup"><span data-stu-id="50732-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="50732-267">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="50732-267">Next steps</span></span>

<span data-ttu-id="50732-268">W tym samouczku można przedstawiono sposób replikacji bazy danych HBase tooconfigure między dwoma centrami danych.</span><span class="sxs-lookup"><span data-stu-id="50732-268">In this tutorial, you learned how tooconfigure HBase replication across two datacenters.</span></span> <span data-ttu-id="50732-269">toolearn więcej informacji na temat usługi HDInsight i HBase, zobacz:</span><span class="sxs-lookup"><span data-stu-id="50732-269">toolearn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="50732-270">[Rozpoczynanie pracy z bazy danych Apache HBase w usłudze HDInsight][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="50732-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="50732-271">[HDInsight HBase — omówienie][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="50732-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="50732-272">[Tworzenie klastrów HBase w sieci wirtualnej platformy Azure][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="50732-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="50732-273">[Analizowanie w czasie rzeczywistym usługi Twitter wskaźniki nastrojów klientów z bazy danych HBase][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="50732-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="50732-274">[Analizowanie danych czujnika za pomocą Storm i bazy danych HBase w usłudze HDInsight (Hadoop)][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="50732-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
