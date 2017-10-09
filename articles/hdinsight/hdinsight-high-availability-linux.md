---
title: "dostępność aaaHigh Hadoop - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klastry usługi HDInsight poprawy niezawodności i dostępności przy użyciu dodatkowego węzła głównego. Dowiedz się, jak to ma wpływ na usługi Hadoop, takich jak Ambari i Hive, oraz jak tooindividually połączyć tooeach węzła głównego przy użyciu protokołu SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "Wysoka dostępność usługi hadoop"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="4977e-105">Dostępność i niezawodność klastrów Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="4977e-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="4977e-106">Klastry HDInsight zapewniają dwóch węzłów głównych tooincrease hello dostępność i niezawodność usług Hadoop i zadania uruchomione.</span><span class="sxs-lookup"><span data-stu-id="4977e-106">HDInsight clusters provide two head nodes tooincrease hello availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="4977e-107">Hadoop osiąga wysokiej dostępności i niezawodności, replikowanie usług i danych w wielu węzłach w klastrze.</span><span class="sxs-lookup"><span data-stu-id="4977e-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="4977e-108">Jednak standardowe podziału Hadoop zwykle mają tylko pojedynczego węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="4977e-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="4977e-109">Wszelkie awarii jednego węzła głównego hello może spowodować hello klastra toostop pracy.</span><span class="sxs-lookup"><span data-stu-id="4977e-109">Any outage of hello single head node can cause hello cluster toostop working.</span></span> <span data-ttu-id="4977e-110">Usługa HDInsight zapewnia dostępność i niezawodność dwóch headnodes tooimprove Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4977e-110">HDInsight provides two headnodes tooimprove Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4977e-111">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4977e-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4977e-112">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="4977e-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="4977e-113">Dostępność i niezawodność węzłów</span><span class="sxs-lookup"><span data-stu-id="4977e-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="4977e-114">Węzły w klastrze usługi HDInsight są implementowane za pomocą usługi Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="4977e-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="4977e-115">Witaj poniższych sekcjach omówiono typy oddzielnego węzła hello używane z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4977e-115">hello following sections discuss hello individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="4977e-116">Nie wszystkie typy węzłów są używane dla typu klastra.</span><span class="sxs-lookup"><span data-stu-id="4977e-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="4977e-117">Na przykład typ klastra usługi Hadoop nie ma żadnych węzłów Nimbus.</span><span class="sxs-lookup"><span data-stu-id="4977e-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="4977e-118">Aby uzyskać więcej informacji na węzłach używana przez typy klastrów usługi HDInsight, zobacz hello klastra typy część hello [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4977e-118">For more information on nodes used by HDInsight cluster types, see hello Cluster types section of hello [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="4977e-119">HEAD węzłów</span><span class="sxs-lookup"><span data-stu-id="4977e-119">Head nodes</span></span>

<span data-ttu-id="4977e-120">tooensure wysoką dostępność usług Hadoop, usługa HDInsight zapewnia dwóch węzłów głównych.</span><span class="sxs-lookup"><span data-stu-id="4977e-120">tooensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="4977e-121">Obu węzłów głównych są aktywne i działa w klastrze HDInsight hello jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="4977e-121">Both head nodes are active and running within hello HDInsight cluster simultaneously.</span></span> <span data-ttu-id="4977e-122">Niektóre usługi, takie jak system plików HDFS lub YARN, są tylko aktywne, w jednym węźle głównym w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="4977e-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="4977e-123">Inne usługi, takie jak serwera HiveServer2 lub na potrzeby magazynu metadanych Hive są aktywne w obu węzłów głównych w hello tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="4977e-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at hello same time.</span></span>

<span data-ttu-id="4977e-124">Węzły HEAD (i inne węzły w usłudze HDInsight) ma wartość numeryczną jako część nazwy hosta hello hello węzła.</span><span class="sxs-lookup"><span data-stu-id="4977e-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of hello hostname of hello node.</span></span> <span data-ttu-id="4977e-125">Na przykład `hn0-CLUSTERNAME` lub `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="4977e-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4977e-126">Nie należy kojarzyć hello wartość liczbową z tego, czy węzeł jest podstawowy lub pomocniczy.</span><span class="sxs-lookup"><span data-stu-id="4977e-126">Do not associate hello numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="4977e-127">wartość liczbowa Hello jest tylko obecny tooprovide unikatową nazwę dla każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="4977e-127">hello numeric value is only present tooprovide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="4977e-128">Węzły Nimbus</span><span class="sxs-lookup"><span data-stu-id="4977e-128">Nimbus Nodes</span></span>

<span data-ttu-id="4977e-129">Węzły nimbus są dostępne z klastrami Storm.</span><span class="sxs-lookup"><span data-stu-id="4977e-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="4977e-130">węzły Nimbus Hello zapewniają podobne funkcje toohello Hadoop JobTracker przy dystrybucji i monitorowania przetwarzania między węzłami procesów roboczych.</span><span class="sxs-lookup"><span data-stu-id="4977e-130">hello Nimbus nodes provide similar functionality toohello Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="4977e-131">HDInsight dostarcza dwóch węzłów Nimbus, w przypadku klastrów Storm</span><span class="sxs-lookup"><span data-stu-id="4977e-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="4977e-132">Węzły dozorcy</span><span class="sxs-lookup"><span data-stu-id="4977e-132">Zookeeper nodes</span></span>

<span data-ttu-id="4977e-133">[Dozorcy](http://zookeeper.apache.org/) węzły są używane do wyboru wiodące głównego usługi na węzłach głównych.</span><span class="sxs-lookup"><span data-stu-id="4977e-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="4977e-134">Są one również używane tooinsure czy usług, danych (proces roboczy) węzły i bram wiedzieć, który węzła głównego głównej usługi jest aktywna na.</span><span class="sxs-lookup"><span data-stu-id="4977e-134">They are also used tooinsure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="4977e-135">Domyślnie usługa HDInsight zapewnia trzy węzły dozorcy.</span><span class="sxs-lookup"><span data-stu-id="4977e-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="4977e-136">Węzłów procesu roboczego</span><span class="sxs-lookup"><span data-stu-id="4977e-136">Worker nodes</span></span>

<span data-ttu-id="4977e-137">Węzłów procesu roboczego do wykonywania analizy danych rzeczywistych hello gdy zadanie jest toohello przesyłanego klastra.</span><span class="sxs-lookup"><span data-stu-id="4977e-137">Worker nodes perform hello actual data analysis when a job is submitted toohello cluster.</span></span> <span data-ttu-id="4977e-138">Jeśli węzłem procesu roboczego nie powiedzie się, hello zadanie, które zostało zostanie wykonana jest węzłem procesu roboczego tooanother zostało przesłane.</span><span class="sxs-lookup"><span data-stu-id="4977e-138">If a worker node fails, hello task that it was performing is submitted tooanother worker node.</span></span> <span data-ttu-id="4977e-139">Domyślnie HDInsight tworzy czterech węzłów procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="4977e-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="4977e-140">Możesz zmienić ten numer toosuit potrzeb podczas i po utworzeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="4977e-140">You can change this number toosuit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="4977e-141">Węzeł krawędzi</span><span class="sxs-lookup"><span data-stu-id="4977e-141">Edge node</span></span>

<span data-ttu-id="4977e-142">Węzeł krawędzi nie aktywnie uczestniczy w analizy danych w ramach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="4977e-142">An edge node does not actively participate in data analysis within hello cluster.</span></span> <span data-ttu-id="4977e-143">Jest on używany przez programistów i analityków danych, podczas pracy z platformą Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4977e-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="4977e-144">życie węzła krawędzi Hello w hello tej samej sieci wirtualnej platformy Azure jako hello inne węzły w klastrze hello i można uzyskać dostęp do wszystkich innych węzłów.</span><span class="sxs-lookup"><span data-stu-id="4977e-144">hello edge node lives in hello same Azure Virtual Network as hello other nodes in hello cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="4977e-145">można użyć węzła krawędzi Hello bez konieczności przełączania zasoby zadań analizy i krytycznych usług Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4977e-145">hello edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="4977e-146">Serwer R w usłudze HDInsight jest obecnie hello tylko klastra typ, który zawiera węzeł krawędzi domyślnie.</span><span class="sxs-lookup"><span data-stu-id="4977e-146">Currently, R Server on HDInsight is hello only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="4977e-147">R Server w usłudze HDInsight, węzłem krawędzi hello jest używany kod testu R lokalnie w węźle hello przed przesłaniem go toohello klastra na potrzeby przetwarzania rozproszonego.</span><span class="sxs-lookup"><span data-stu-id="4977e-147">For R Server on HDInsight, hello edge node is used test R code locally on hello node before submitting it toohello cluster for distributed processing.</span></span>

<span data-ttu-id="4977e-148">Informacje o korzystaniu z węzłem krawędzi z klastra o typie innym niż serwer R, zobacz hello [użycia węzłów krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4977e-148">For information on using an edge node with cluster types other than R Server, see hello [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-hello-nodes"></a><span data-ttu-id="4977e-149">Uzyskiwanie dostępu do węzłów hello</span><span class="sxs-lookup"><span data-stu-id="4977e-149">Accessing hello nodes</span></span>

<span data-ttu-id="4977e-150">Klastra toohello dostępu za pośrednictwem hello podano internet za pośrednictwem bramy sieci publicznej.</span><span class="sxs-lookup"><span data-stu-id="4977e-150">Access toohello cluster over hello internet is provided through a public gateway.</span></span> <span data-ttu-id="4977e-151">Dostęp jest ograniczony tooconnecting toohello głównymi węzłami i (jeśli istnieje) hello węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="4977e-151">Access is limited tooconnecting toohello head nodes and (if one exists) hello edge node.</span></span> <span data-ttu-id="4977e-152">Uruchomione w węzłach head hello tooservices dostępu nie odbywa się przez wiele węzłów głównych.</span><span class="sxs-lookup"><span data-stu-id="4977e-152">Access tooservices running on hello head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="4977e-153">Hello publicznego bramy trasy żądania toohello węzła głównego obsługującego hello żądanej usługi.</span><span class="sxs-lookup"><span data-stu-id="4977e-153">hello public gateway routes requests toohello head node that hosts hello requested service.</span></span> <span data-ttu-id="4977e-154">Na przykład Ambari znajduje się obecnie na powitania drugiego węzła głównego, hello brama kieruje przychodzące żądania dla węzła toothat Ambari.</span><span class="sxs-lookup"><span data-stu-id="4977e-154">For example, if Ambari is currently hosted on hello secondary head node, hello gateway routes incoming requests for Ambari toothat node.</span></span>

<span data-ttu-id="4977e-155">Dostęp za pośrednictwem bramy publicznego hello jest ograniczona tooport 443 (HTTPS), 22 i 23.</span><span class="sxs-lookup"><span data-stu-id="4977e-155">Access over hello public gateway is limited tooport 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="4977e-156">Port __443__ jest używane tooaccess Ambari i innych sieci web interfejsu użytkownika lub hostowanych w węzłach głównych hello interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="4977e-156">Port __443__ is used tooaccess Ambari and other web UI or REST APIs hosted on hello head nodes.</span></span>

* <span data-ttu-id="4977e-157">Port __22__ jest używane tooaccess hello głównej węzła głównego lub węzłem krawędzi przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="4977e-157">Port __22__ is used tooaccess hello primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="4977e-158">Port __23__ jest hello używane tooaccess drugiego węzła głównego przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="4977e-158">Port __23__ is used tooaccess hello secondary head node with SSH.</span></span> <span data-ttu-id="4977e-159">Na przykład `ssh username@mycluster-ssh.azurehdinsight.net` łączy toohello głównej węzła głównego o nazwie klastra hello **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="4977e-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects toohello primary head node of hello cluster named **mycluster**.</span></span>

<span data-ttu-id="4977e-160">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4977e-160">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="4977e-161">Wewnętrzne w pełni kwalifikowanej nazwy domeny (FQDN)</span><span class="sxs-lookup"><span data-stu-id="4977e-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="4977e-162">Węzły w klastrze HDInsight ma wewnętrzny adres IP i nazwy FQDN, która jest możliwy tylko z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="4977e-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from hello cluster.</span></span> <span data-ttu-id="4977e-163">Podczas uzyskiwania dostępu do usługi w klastrze hello przy użyciu hello wewnętrznej nazwy FQDN lub adres IP, należy używać narzędzia Ambari tooverify hello adres IP lub nazwa FQDN toouse podczas uzyskiwania dostępu do usługi hello.</span><span class="sxs-lookup"><span data-stu-id="4977e-163">When accessing services on hello cluster using hello internal FQDN or IP address, you should use Ambari tooverify hello IP or FQDN toouse when accessing hello service.</span></span>

<span data-ttu-id="4977e-164">Na przykład Witaj Oozie usługi można uruchomić tylko na jednym węźle głównym, a za pomocą hello `oozie` polecenia w sesji SSH wymaga hello adres URL toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="4977e-164">For example, hello Oozie service can only run on one head node, and using hello `oozie` command from an SSH session requires hello URL toohello service.</span></span> <span data-ttu-id="4977e-165">Ten adres URL można pobrać z Ambari przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4977e-165">This URL can be retrieved from Ambari by using hello following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="4977e-166">To polecenie zwraca wartość toohello podobne, następujące polecenie, które zawiera hello wewnętrznego adresu URL toouse z hello `oozie` polecenia:</span><span class="sxs-lookup"><span data-stu-id="4977e-166">This command returns a value similar toohello following command, which contains hello internal URL toouse with hello `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="4977e-167">Aby uzyskać więcej informacji na temat pracy z hello interfejsu API REST Ambari, zobacz [monitorować i zarządzać HDInsight przy użyciu interfejsu API REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="4977e-167">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="4977e-168">Uzyskiwanie dostępu do innych typów węzła</span><span class="sxs-lookup"><span data-stu-id="4977e-168">Accessing other node types</span></span>

<span data-ttu-id="4977e-169">Możesz połączyć toonodes, które są nie bezpośrednio dostępny przez hello internet przy użyciu następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="4977e-169">You can connect toonodes that are not directly accessible over hello internet by using hello following methods:</span></span>

* <span data-ttu-id="4977e-170">**SSH**: po nawiązaniu połączenia z węzłem głównym tooa przy użyciu protokołu SSH, można użyć protokołu SSH z hello węzła głównego tooconnect tooother węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="4977e-170">**SSH**: Once connected tooa head node using SSH, you can then use SSH from hello head node tooconnect tooother nodes in hello cluster.</span></span> <span data-ttu-id="4977e-171">Aby uzyskać więcej informacji, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4977e-171">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="4977e-172">**Tunel SSH**: Jeśli potrzebujesz tooaccess usługi sieci web hostowanych na jednym z węzłów hello, które nie jest widoczne toohello internet, należy użyć tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="4977e-172">**SSH Tunnel**: If you need tooaccess a web service hosted on one of hello nodes that is not exposed toohello internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="4977e-173">Aby uzyskać więcej informacji, zobacz hello [tunelu SSH za pomocą usługi HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4977e-173">For more information, see hello [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="4977e-174">**Sieć wirtualna platformy Azure**: Jeśli Twoje HDInsight klastra jest częścią sieci wirtualnej platformy Azure, dowolnego zasobu na hello sam sieci wirtualnej można uzyskać dostęp do wszystkich węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="4977e-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on hello same Virtual Network can directly access all nodes in hello cluster.</span></span> <span data-ttu-id="4977e-175">Aby uzyskać więcej informacji, zobacz hello [rozszerzyć HDInsight przy użyciu usługi Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4977e-175">For more information, see hello [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-toocheck-on-a-service-status"></a><span data-ttu-id="4977e-176">Jak toocheck stanu usługi</span><span class="sxs-lookup"><span data-stu-id="4977e-176">How toocheck on a service status</span></span>

<span data-ttu-id="4977e-177">Stan hello toocheck usługi działające na powitania węzłów głównych Użyj hello Interfejsu sieci Web Ambari lub hello interfejsu API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="4977e-177">toocheck hello status of services that run on hello head nodes, use hello Ambari Web UI or hello Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="4977e-178">Interfejs użytkownika sieci Web Ambari</span><span class="sxs-lookup"><span data-stu-id="4977e-178">Ambari Web UI</span></span>

<span data-ttu-id="4977e-179">Interfejs sieci Web Ambari Hello są widoczne w https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="4977e-179">hello Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="4977e-180">Zastąp **CLUSTERNAME** o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="4977e-180">Replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="4977e-181">Jeśli zostanie wyświetlony monit, wprowadź poświadczenia użytkownika hello HTTP dla klastra.</span><span class="sxs-lookup"><span data-stu-id="4977e-181">If prompted, enter hello HTTP user credentials for your cluster.</span></span> <span data-ttu-id="4977e-182">Witaj domyślna nazwa użytkownika HTTP jest **admin** i hasło hello jest hello hasła podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="4977e-182">hello default HTTP user name is **admin** and hello password is hello password you entered when creating hello cluster.</span></span>

<span data-ttu-id="4977e-183">Nadejściu na stronie Ambari hello hello zainstalowane usługi są wyświetlane na powitania po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="4977e-183">When you arrive on hello Ambari page, hello installed services are listed on hello left of hello page.</span></span>

![Zainstalowane usługi](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="4977e-185">Istnieje szereg ikony wyświetlane dalej stan tooindicate usługi tooa.</span><span class="sxs-lookup"><span data-stu-id="4977e-185">There are a series of icons that may appear next tooa service tooindicate status.</span></span> <span data-ttu-id="4977e-186">Wszystkie alerty dotyczące usługi tooa można wyświetlić przy użyciu hello **alerty** łącze u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="4977e-186">Any alerts related tooa service can be viewed using hello **Alerts** link at hello top of hello page.</span></span> <span data-ttu-id="4977e-187">Można wybrać więcej o tooview każdej usługi.</span><span class="sxs-lookup"><span data-stu-id="4977e-187">You can select each service tooview more information on it.</span></span>

<span data-ttu-id="4977e-188">Strony usługi hello zawiera informacje na powitania stanu i konfiguracji poszczególnych usług, natomiast nie dostarcza informacji, na którym jest uruchomiona usługa hello węzła głównego na.</span><span class="sxs-lookup"><span data-stu-id="4977e-188">While hello service page provides information on hello status and configuration of each service, it does not provide information on which head node hello service is running on.</span></span> <span data-ttu-id="4977e-189">tooview tej informacji, użyj hello **hostów** łącze u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="4977e-189">tooview this information, use hello **Hosts** link at hello top of hello page.</span></span> <span data-ttu-id="4977e-190">Ta strona wyświetla hosty w klastrze hello, w tym hello węzłów głównych.</span><span class="sxs-lookup"><span data-stu-id="4977e-190">This page displays hosts within hello cluster, including hello head nodes.</span></span>

![listy hostów](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="4977e-192">Wybór łącza hello jednego z węzłów głównych hello Wyświetla hello usług i składników uruchomione w tym węźle.</span><span class="sxs-lookup"><span data-stu-id="4977e-192">Selecting hello link for one of hello head nodes displays hello services and components running on that node.</span></span>

![Stan składnika](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="4977e-194">Aby uzyskać więcej informacji na temat używania narzędzia Ambari, zobacz [monitorowanie i zarządzanie nimi przy użyciu interfejsu użytkownika sieci Web Ambari hello HDInsight](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="4977e-194">For more information on using Ambari, see [Monitor and manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="4977e-195">Interfejs API REST Ambari</span><span class="sxs-lookup"><span data-stu-id="4977e-195">Ambari REST API</span></span>

<span data-ttu-id="4977e-196">Interfejs API REST Ambari Hello jest dostępna za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="4977e-196">hello Ambari REST API is available over hello internet.</span></span> <span data-ttu-id="4977e-197">Brama publicznego HDInsight Hello obsługuje routingu żądań toohello węzła głównego aktualnie obsługujący hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="4977e-197">hello HDInsight public gateway handles routing requests toohello head node that is currently hosting hello REST API.</span></span>

<span data-ttu-id="4977e-198">Możesz użyć następującego polecenia toocheck hello stanu usługi za pośrednictwem interfejsu API REST Ambari hello hello:</span><span class="sxs-lookup"><span data-stu-id="4977e-198">You can use hello following command toocheck hello state of a service through hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="4977e-199">Zastąp **hasło** z hasłem konta użytkownika (Administrator) hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="4977e-199">Replace **PASSWORD** with hello HTTP user (admin) account password.</span></span>
* <span data-ttu-id="4977e-200">Zastąp **CLUSTERNAME** o nazwie hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="4977e-200">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
* <span data-ttu-id="4977e-201">Zastąp **SERVICENAME** o nazwie hello hello usługi ma stan hello toocheck.</span><span class="sxs-lookup"><span data-stu-id="4977e-201">Replace **SERVICENAME** with hello name of hello service you want toocheck hello status of.</span></span>

<span data-ttu-id="4977e-202">Na przykład stan hello toocheck hello **HDFS** usługi w klastrze o nazwie **mycluster**, używając hasła **hasła**, należy użyć następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="4977e-202">For example, toocheck hello status of hello **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use hello following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="4977e-203">odpowiedź Hello jest podobne toohello po JSON:</span><span class="sxs-lookup"><span data-stu-id="4977e-203">hello response is similar toohello following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="4977e-204">Witaj adresu URL informuje NAS czy hello usługa jest obecnie uruchomiona na węzła głównego o nazwie **hn0 CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="4977e-204">hello URL tells us that hello service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="4977e-205">Witaj stanu informuje NAS czy obecnie jest uruchomiona usługa hello, lub **uruchomiono**.</span><span class="sxs-lookup"><span data-stu-id="4977e-205">hello state tells us that hello service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="4977e-206">Jeśli nie wiesz, jakie usługi są zainstalowane na powitania klastra, można użyć hello następujące polecenia tooretrieve listy:</span><span class="sxs-lookup"><span data-stu-id="4977e-206">If you do not know what services are installed on hello cluster, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="4977e-207">Aby uzyskać więcej informacji na temat pracy z hello interfejsu API REST Ambari, zobacz [monitorować i zarządzać HDInsight przy użyciu interfejsu API REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="4977e-207">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="4977e-208">Składniki usługi</span><span class="sxs-lookup"><span data-stu-id="4977e-208">Service components</span></span>

<span data-ttu-id="4977e-209">Usługi mogą obejmować składników, które mają stan hello toocheck indywidualnie.</span><span class="sxs-lookup"><span data-stu-id="4977e-209">Services may contain components that you wish toocheck hello status of individually.</span></span> <span data-ttu-id="4977e-210">Na przykład system plików HDFS zawiera składnik NameNode hello.</span><span class="sxs-lookup"><span data-stu-id="4977e-210">For example, HDFS contains hello NameNode component.</span></span> <span data-ttu-id="4977e-211">tooview informacji na temat składnika, polecenie hello będzie:</span><span class="sxs-lookup"><span data-stu-id="4977e-211">tooview information on a component, hello command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="4977e-212">Jeśli nie wiadomo, które składniki są dostarczane przez usługę, możesz użyć hello następujące polecenia tooretrieve listy:</span><span class="sxs-lookup"><span data-stu-id="4977e-212">If you do not know what components are provided by a service, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a><span data-ttu-id="4977e-213">Jak tooaccess dzienniki na powitania węzłów głównych</span><span class="sxs-lookup"><span data-stu-id="4977e-213">How tooaccess log files on hello head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="4977e-214">SSH</span><span class="sxs-lookup"><span data-stu-id="4977e-214">SSH</span></span>

<span data-ttu-id="4977e-215">Podczas węzła głównego tooa połączonych za pośrednictwem protokołu SSH, pliki dziennika można znaleźć w **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="4977e-215">While connected tooa head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="4977e-216">Na przykład **/var/log/hadoop-yarn/yarn** zawiera dzienników YARN.</span><span class="sxs-lookup"><span data-stu-id="4977e-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="4977e-217">Każdego węzła głównego może mieć wpisy dziennika unikatowy, dlatego należy sprawdzić dzienniki hello na obu.</span><span class="sxs-lookup"><span data-stu-id="4977e-217">Each head node can have unique log entries, so you should check hello logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="4977e-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="4977e-218">SFTP</span></span>

<span data-ttu-id="4977e-219">Można także połączyć toohello węzła głównego przy użyciu hello SSH protokołu transferu plików lub Secure File Transfer Protocol (SFTP) i pobierania plików dziennika hello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="4977e-219">You can also connect toohello head node using hello SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download hello log files directly.</span></span>

<span data-ttu-id="4977e-220">Podobne toousing klienta SSH, łącząc toohello klastra, które należy podać hello SSH konto nazwy użytkownika i hello SSH adresu hello klastra.</span><span class="sxs-lookup"><span data-stu-id="4977e-220">Similar toousing an SSH client, when connecting toohello cluster you must provide hello SSH user account name and hello SSH address of hello cluster.</span></span> <span data-ttu-id="4977e-221">Na przykład `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="4977e-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="4977e-222">Podaj hello hasło dla konta powitania po wyświetleniu monitu, lub Podaj klucz publiczny przy użyciu hello `-i` parametru.</span><span class="sxs-lookup"><span data-stu-id="4977e-222">Provide hello password for hello account when prompted, or provide a public key using hello `-i` parameter.</span></span>

<span data-ttu-id="4977e-223">Po nawiązaniu połączenia jest wyświetlana `sftp>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="4977e-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="4977e-224">Z wiersza polecenia, można zmienić katalogi, przekazywanie i pobieranie plików.</span><span class="sxs-lookup"><span data-stu-id="4977e-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="4977e-225">Na przykład hello następujące polecenia Zmień katalogi toohello **/var/log/hadoop/hdfs** katalogu, a następnie Pobierz wszystkie pliki w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="4977e-225">For example, hello following commands change directories toohello **/var/log/hadoop/hdfs** directory and then download all files in hello directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="4977e-226">Aby uzyskać listę dostępnych poleceń, wprowadź `help` na powitania `sftp>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="4977e-226">For a list of available commands, enter `help` at hello `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="4977e-227">Dostępne są także graficzne interfejsy, które pozwalają toovisualize hello systemu plików, gdy nawiązano połączenie przy użyciu protokołu SFTP.</span><span class="sxs-lookup"><span data-stu-id="4977e-227">There are also graphical interfaces that allow you toovisualize hello file system when connected using SFTP.</span></span> <span data-ttu-id="4977e-228">Na przykład [MobaXTerm](http://mobaxterm.mobatek.net/) pozwala systemu plików hello toobrowse za pomocą interfejsu tooWindows podobne Explorer.</span><span class="sxs-lookup"><span data-stu-id="4977e-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you toobrowse hello file system using an interface similar tooWindows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="4977e-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="4977e-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="4977e-230">tooaccess dziennik plików przy użyciu Ambari, należy użyć tunelu SSH.</span><span class="sxs-lookup"><span data-stu-id="4977e-230">tooaccess log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="4977e-231">Witaj interfejsów sieci web dla poszczególnych usług hello nie są widoczne publicznie na powitania Internet.</span><span class="sxs-lookup"><span data-stu-id="4977e-231">hello web interfaces for hello individual services are not exposed publicly on hello Internet.</span></span> <span data-ttu-id="4977e-232">Aby uzyskać informacje na temat używania tunelu SSH, zobacz hello [Użyj SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4977e-232">For information on using an SSH tunnel, see hello [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="4977e-233">Z hello Interfejsu sieci Web Ambari wybierz usługę hello chcesz dzienniki tooview (na przykład YARN).</span><span class="sxs-lookup"><span data-stu-id="4977e-233">From hello Ambari Web UI, select hello service you wish tooview logs for (for example, YARN).</span></span> <span data-ttu-id="4977e-234">Następnie użyj **szybkie linki** tooselect, które hello tooview węzła głównego w dziennikach.</span><span class="sxs-lookup"><span data-stu-id="4977e-234">Then use **Quick Links** tooselect which head node tooview hello logs for.</span></span>

![Przy użyciu szybkie linki tooview dzienniki](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a><span data-ttu-id="4977e-236">Jak tooconfigure hello rozmiaru węzła</span><span class="sxs-lookup"><span data-stu-id="4977e-236">How tooconfigure hello node size</span></span>

<span data-ttu-id="4977e-237">rozmiar Hello węzła można wybrać tylko podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="4977e-237">hello size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="4977e-238">Można znaleźć listę hello różne rozmiary maszyny Wirtualnej dla usługi HDInsight na powitania [cennikiem usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4977e-238">You can find a list of hello different VM sizes available for HDInsight on hello [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="4977e-239">Podczas tworzenia klastra, można określić rozmiaru hello hello węzłów.</span><span class="sxs-lookup"><span data-stu-id="4977e-239">When creating a cluster, you can specify hello size of hello nodes.</span></span> <span data-ttu-id="4977e-240">Witaj następujące informacje znajdują się wskazówki dotyczące sposobu przy użyciu rozmiaru hello toospecify hello [portalu Azure][preview-portal], [programu Azure PowerShell][azure-powershell], i hello [interfejsu wiersza polecenia Azure][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="4977e-240">hello following information provides guidance on how toospecify hello size using hello [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and hello [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="4977e-241">**Azure portal**: podczas tworzenia klastra, można ustawić rozmiaru hello węzłów hello używane przez klaster hello:</span><span class="sxs-lookup"><span data-stu-id="4977e-241">**Azure portal**: When creating a cluster, you can set hello size of hello nodes used by hello cluster:</span></span>

    ![Obraz kreatora tworzenia klastra z węzła rozmiar zaznaczenia](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="4977e-243">**Azure CLI**: korzystając z hello `azure hdinsight cluster create` polecenia, można ustawić rozmiaru hello hello head, proces roboczy i węzły dozorcy przy użyciu hello `--headNodeSize`, `--workerNodeSize`, i `--zookeeperNodeSize` parametrów.</span><span class="sxs-lookup"><span data-stu-id="4977e-243">**Azure CLI**: When using hello `azure hdinsight cluster create` command, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="4977e-244">**Program Azure PowerShell**: korzystając z hello `New-AzureRmHDInsightCluster` polecenia cmdlet, można ustawić rozmiaru hello hello head, proces roboczy i węzły dozorcy przy użyciu hello `-HeadNodeVMSize`, `-WorkerNodeSize`, i `-ZookeeperNodeSize` parametrów.</span><span class="sxs-lookup"><span data-stu-id="4977e-244">**Azure PowerShell**: When using hello `New-AzureRmHDInsightCluster` cmdlet, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4977e-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4977e-245">Next steps</span></span>

<span data-ttu-id="4977e-246">Użyj powitania po toolearn łącza więcej informacji na temat rzeczy, o których wspomniano w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="4977e-246">Use hello following links toolearn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="4977e-247">Dokumentacja REST Ambari</span><span class="sxs-lookup"><span data-stu-id="4977e-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="4977e-248">Instalowanie i konfigurowanie hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4977e-248">Install and configure hello Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="4977e-249">Zainstaluj i skonfiguruj program Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4977e-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="4977e-250">Zarządzanie HDInsight przy użyciu narzędzia Ambari</span><span class="sxs-lookup"><span data-stu-id="4977e-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="4977e-251">Obsługa administracyjna klastrów HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="4977e-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
