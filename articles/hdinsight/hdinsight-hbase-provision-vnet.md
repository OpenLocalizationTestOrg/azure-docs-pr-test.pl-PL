---
title: "Tworzenie klastrów HBase w sieci wirtualnej - Azure | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z bazy danych HBase w usłudze Azure HDInsight. Informacje o sposobie tworzenia klastrów HDInsight HBase w sieci wirtualnej Azure."
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
ms.openlocfilehash: 668bd494ce3274188af56cf7d6253cec7af9abbc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="06ac5-104">Tworzenie klastrów HBase w usłudze HDInsight w sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="06ac5-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="06ac5-105">Dowiedz się, jak utworzyć klaster Azure HDInsight HBase w [sieci wirtualnej Azure][1].</span><span class="sxs-lookup"><span data-stu-id="06ac5-105">Learn how to create Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="06ac5-106">Dzięki integracji sieci wirtualnej klastrów HBase można wdrożyć do tej samej sieci wirtualnej jako aplikacje, dzięki czemu aplikacje mogą komunikować się z bazą danych HBase bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="06ac5-106">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="06ac5-107">Korzyści:</span><span class="sxs-lookup"><span data-stu-id="06ac5-107">The benefits include:</span></span>

* <span data-ttu-id="06ac5-108">Bezpośrednie połączenie między aplikacji sieci web do węzłów klastra HBase, co umożliwia komunikację za pomocą procedury zdalnej bazy danych HBase w języku Java wywoływania interfejsów API (RPC).</span><span class="sxs-lookup"><span data-stu-id="06ac5-108">Direct connectivity of the web application to the nodes of the HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="06ac5-109">Większa wydajność, ponieważ nie ma ruchu przejdź przez wiele bram i moduły równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="06ac5-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="06ac5-110">Możliwość przetworzenia poufne informacje w bardziej bezpieczny sposób bez narażania publiczny punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="06ac5-110">The ability to process sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="06ac5-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="06ac5-111">Prerequisites</span></span>
<span data-ttu-id="06ac5-112">Przed przystąpieniem do wykonywania kroków opisanych w tym samouczku musisz mieć poniższe:</span><span class="sxs-lookup"><span data-stu-id="06ac5-112">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="06ac5-113">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="06ac5-113">**An Azure subscription**.</span></span> <span data-ttu-id="06ac5-114">Zobacz artykuł [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="06ac5-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="06ac5-115">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="06ac5-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="06ac5-116">Zobacz [instalacja i używanie programu Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="06ac5-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="06ac5-117">Tworzenie klastra HBase w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="06ac5-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="06ac5-118">W tej sekcji, utworzyć klaster HBase opartych na systemie Linux z zależne konto magazynu Azure w sieci wirtualnej platformy Azure przy użyciu [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="06ac5-118">In this section, you create a Linux-based HBase cluster with the dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="06ac5-119">Inne metody tworzenia klastrów i opis ustawień, zobacz [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="06ac5-119">For other cluster creation methods and understanding the settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="06ac5-120">Aby uzyskać więcej informacji na temat przy użyciu szablonu do tworzenia klastrów Hadoop w usłudze HDInsight, zobacz [klastrów utworzyć Hadoop w HDInsight przy użyciu szablonów usługi Azure Resource Manager](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="06ac5-120">For more information about using a template to create Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="06ac5-121">Niektóre właściwości są zakodowane na stałe do szablonu.</span><span class="sxs-lookup"><span data-stu-id="06ac5-121">Some properties are hard-coded into the template.</span></span> <span data-ttu-id="06ac5-122">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="06ac5-122">For example:</span></span>
>
> * <span data-ttu-id="06ac5-123">**Lokalizacja**: wschodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="06ac5-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="06ac5-124">**Wersja klastra**: 3.5</span><span class="sxs-lookup"><span data-stu-id="06ac5-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="06ac5-125">**Liczba węzłów procesu roboczego klastra**: 2</span><span class="sxs-lookup"><span data-stu-id="06ac5-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="06ac5-126">**Domyślne konto magazynu**: unikatowy ciąg</span><span class="sxs-lookup"><span data-stu-id="06ac5-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="06ac5-127">**Nazwa sieci wirtualnej**: &lt;nazwa klastra >-Sieć wirtualna</span><span class="sxs-lookup"><span data-stu-id="06ac5-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="06ac5-128">**Przestrzeń adresową sieci wirtualnej**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="06ac5-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="06ac5-129">**Nazwa podsieci**: podsieć1</span><span class="sxs-lookup"><span data-stu-id="06ac5-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="06ac5-130">**Zakres adresów podsieci**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="06ac5-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="06ac5-131">&lt;Nazwa klastra > jest zastępowany nazwą klastra, podaj przy użyciu szablonu.</span><span class="sxs-lookup"><span data-stu-id="06ac5-131">&lt;Cluster Name> is replaced with the cluster name you provide when using the template.</span></span>
>
>

1. <span data-ttu-id="06ac5-132">Kliknij poniższy obraz, aby otworzyć szablon w usłudze Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="06ac5-132">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="06ac5-133">Szablon znajduje się w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="06ac5-133">The template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="06ac5-134">Z **wdrożenie niestandardowe** bloku, wprowadź następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="06ac5-134">From the **Custom deployment** blade, enter the following properties:</span></span>

   * <span data-ttu-id="06ac5-135">**Subskrypcja**: Wybierz subskrypcję platformy Azure, używany do tworzenia klastra usługi HDInsight, zależne konto magazynu i sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="06ac5-135">**Subscription**: Select an Azure subscription used to create the HDInsight cluster, the dependent Storage account and the Azure virtual network.</span></span>
   * <span data-ttu-id="06ac5-136">**Grupa zasobów**: Wybierz **Utwórz nowy**i określ nazwę nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="06ac5-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="06ac5-137">**Lokalizacja**: Wybierz lokalizację dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="06ac5-137">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="06ac5-138">**ClusterName**: Wprowadź nazwę klastra usługi Hadoop, która ma zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="06ac5-138">**ClusterName**: Enter a name for the Hadoop cluster to be created.</span></span>
   * <span data-ttu-id="06ac5-139">**Nazwa logowania i hasło klastra**: domyślna nazwa logowania to **admin**.</span><span class="sxs-lookup"><span data-stu-id="06ac5-139">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="06ac5-140">**Nazwa użytkownika i hasło SSH**: domyślna nazwa użytkownika to **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="06ac5-140">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="06ac5-141">Tę nazwę można zmienić.</span><span class="sxs-lookup"><span data-stu-id="06ac5-141">You can rename it.</span></span>
   * <span data-ttu-id="06ac5-142">**Akceptuję warunki i postanowienia, o których wspomniano**: (Wybierz)</span><span class="sxs-lookup"><span data-stu-id="06ac5-142">**I agree to the terms and the conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="06ac5-143">Kliknij pozycję **Kup**.</span><span class="sxs-lookup"><span data-stu-id="06ac5-143">Click **Purchase**.</span></span> <span data-ttu-id="06ac5-144">Utworzenie klastra trwa około 20 minut.</span><span class="sxs-lookup"><span data-stu-id="06ac5-144">It takes about around 20 minutes to create a cluster.</span></span> <span data-ttu-id="06ac5-145">Po utworzeniu klastra można kliknąć bloku klastra w portalu, aby go otworzyć.</span><span class="sxs-lookup"><span data-stu-id="06ac5-145">Once the cluster is created, you can click the cluster blade in the portal to open it.</span></span>

<span data-ttu-id="06ac5-146">Po ukończeniu samouczka możesz usunąć klaster.</span><span class="sxs-lookup"><span data-stu-id="06ac5-146">After you complete the tutorial, you might want to delete the cluster.</span></span> <span data-ttu-id="06ac5-147">Dzięki usłudze HDInsight dane są przechowywane w usłudze Azure Storage, więc można bezpiecznie usunąć klaster, gdy nie jest używany.</span><span class="sxs-lookup"><span data-stu-id="06ac5-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="06ac5-148">Opłaty za klaster usługi HDInsight są naliczane nawet wtedy, gdy nie jest używany.</span><span class="sxs-lookup"><span data-stu-id="06ac5-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="06ac5-149">Ponieważ opłaty za klaster są wielokrotnie większe niż opłaty za magazyn, ze względów ekonomicznych warto usuwać klastry, gdy nie są używane.</span><span class="sxs-lookup"><span data-stu-id="06ac5-149">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="06ac5-150">Instrukcje dotyczące usuwania klastra znajdują się [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu portalu Azure](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="06ac5-150">For the instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="06ac5-151">Aby rozpocząć pracę z nowego klastra HBase, można użyć procedur w [rozpocząć korzystanie z platformy Hadoop w usłudze HDInsight HBase](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="06ac5-151">To begin working with your new HBase cluster, you can use the procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-to-the-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="06ac5-152">Połącz się z klastrem HBase przy użyciu interfejsów API RPC Java HBase</span><span class="sxs-lookup"><span data-stu-id="06ac5-152">Connect to the HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="06ac5-153">Tworzenie infrastruktury jako usługi (IaaS) maszyny wirtualnej w tej samej sieci wirtualnej platformy Azure i tej samej podsieci.</span><span class="sxs-lookup"><span data-stu-id="06ac5-153">Create an infrastructure as a service (IaaS) virtual machine into the same Azure virtual network and the same subnet.</span></span> <span data-ttu-id="06ac5-154">Aby uzyskać instrukcje dotyczące tworzenia nowej maszyny wirtualnej IaaS, zobacz [tworzenia maszyny wirtualnej systemem Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="06ac5-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="06ac5-155">Gdy czynności opisane w tym dokumencie, należy użyć następujących wartości dla konfiguracji sieci:</span><span class="sxs-lookup"><span data-stu-id="06ac5-155">When following the steps in this document, you must use the following values for the Network configuration:</span></span>

   * <span data-ttu-id="06ac5-156">**Sieć wirtualna**: &lt;nazwa klastra >-Sieć wirtualna</span><span class="sxs-lookup"><span data-stu-id="06ac5-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="06ac5-157">**Podsieci**: podsieć1</span><span class="sxs-lookup"><span data-stu-id="06ac5-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="06ac5-158">Zastąp &lt;nazwa klastra > o nazwie używane podczas tworzenia klastra usługi HDInsight w poprzednich krokach.</span><span class="sxs-lookup"><span data-stu-id="06ac5-158">Replace &lt;Cluster name> with the name you used when creating the HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="06ac5-159">Używając tych wartości, maszyna wirtualna jest umieszczona w tej samej sieci wirtualnej i podsieci co klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="06ac5-159">Using these values, the virtual machine is placed in the same virtual network and subnet as the HDInsight cluster.</span></span> <span data-ttu-id="06ac5-160">Ta konfiguracja pozwala na bezpośrednio komunikować się ze sobą.</span><span class="sxs-lookup"><span data-stu-id="06ac5-160">This configuration allows them to directly communicate with each other.</span></span> <span data-ttu-id="06ac5-161">Istnieje możliwość tworzenia klastra usługi HDInsight z węzłem krawędzi puste.</span><span class="sxs-lookup"><span data-stu-id="06ac5-161">There is a way to create an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="06ac5-162">Węzeł brzegowy może służyć do zarządzania klastrem.</span><span class="sxs-lookup"><span data-stu-id="06ac5-162">The edge node can be used to manage the cluster.</span></span>  <span data-ttu-id="06ac5-163">Aby uzyskać więcej informacji, zobacz [użycia węzłów pusty krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="06ac5-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="06ac5-164">Nawiązać HBase zdalnie za pomocą aplikacji Java, należy użyć w pełni kwalifikowaną nazwę (FQDN).</span><span class="sxs-lookup"><span data-stu-id="06ac5-164">When using a Java application to connect to HBase remotely, you must use the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="06ac5-165">Aby to ustalić, należy uzyskać sufiks DNS konkretnego połączenia klastra HBase.</span><span class="sxs-lookup"><span data-stu-id="06ac5-165">To determine this, you must get the connection-specific DNS suffix of the HBase cluster.</span></span> <span data-ttu-id="06ac5-166">Aby to zrobić, użyj jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="06ac5-166">To do that, you can use one of the following methods:</span></span>

   * <span data-ttu-id="06ac5-167">Korzystanie z przeglądarki sieci Web do wywoływania Ambari:</span><span class="sxs-lookup"><span data-stu-id="06ac5-167">Use a Web browser to make an Ambari call:</span></span>

     <span data-ttu-id="06ac5-168">Przejdź do https://&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / hostuje? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="06ac5-168">Browse to https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="06ac5-169">Monitor przechodzi w stan to plik JSON o sufiksów DNS.</span><span class="sxs-lookup"><span data-stu-id="06ac5-169">It turns a JSON file with the DNS suffixes.</span></span>
   * <span data-ttu-id="06ac5-170">Za pomocą witryny sieci Web Ambari:</span><span class="sxs-lookup"><span data-stu-id="06ac5-170">Use the Ambari website:</span></span>

     1. <span data-ttu-id="06ac5-171">Przejdź do https://&lt;ClusterName >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="06ac5-171">Browse to  https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="06ac5-172">Kliknij przycisk **hostów** z górnego menu.</span><span class="sxs-lookup"><span data-stu-id="06ac5-172">Click **Hosts** from the top menu.</span></span>
   * <span data-ttu-id="06ac5-173">Użyj Curl w celu wykonywania wywołań REST:</span><span class="sxs-lookup"><span data-stu-id="06ac5-173">Use Curl to make REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="06ac5-174">W danych JavaScript Object Notation (JSON) zwrócone Znajdź pozycję "host_name".</span><span class="sxs-lookup"><span data-stu-id="06ac5-174">In the JavaScript Object Notation (JSON) data returned, find the "host_name" entry.</span></span> <span data-ttu-id="06ac5-175">Zawiera nazwę FQDN dla węzłów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="06ac5-175">It contains the FQDN for the nodes in the cluster.</span></span> <span data-ttu-id="06ac5-176">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="06ac5-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="06ac5-177">Część nazwy domeny rozpoczynający się od nazwy klastra jest sufiks DNS.</span><span class="sxs-lookup"><span data-stu-id="06ac5-177">The portion of the domain name beginning with the cluster name is the DNS suffix.</span></span> <span data-ttu-id="06ac5-178">Na przykład mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="06ac5-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="06ac5-179">Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="06ac5-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="06ac5-180">Użyj następującego skryptu programu Azure PowerShell do rejestrowania **Get ClusterDetail** funkcja, która może służyć do zwrócenia sufiks DNS:</span><span class="sxs-lookup"><span data-stu-id="06ac5-180">Use the following Azure PowerShell script to register the **Get-ClusterDetail** function, which can be used to return the DNS suffix:</span></span>

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
            Displays information to facilitate an HDInsight cluster-to-cluster scenario within the same virtual network.
            .Description
            This command shows the following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run the HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows the FQDN suffix of hosts in the cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows the value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows the value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run the HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows the FQDN suffix of hosts in the cluster.
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

     <span data-ttu-id="06ac5-181">Po uruchomieniu skryptu programu Azure PowerShell, użyj następującego polecenia do zwrócenia sufiks DNS przy użyciu **Get ClusterDetail** funkcji.</span><span class="sxs-lookup"><span data-stu-id="06ac5-181">After running the Azure PowerShell script, use the following command to return the DNS suffix by using the **Get-ClusterDetail** function.</span></span> <span data-ttu-id="06ac5-182">Określ nazwę klastra HDInsight HBase, nazwę administratora i hasło administratora kopii, korzystając z tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="06ac5-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="06ac5-183">To polecenie zwraca sufiks DNS.</span><span class="sxs-lookup"><span data-stu-id="06ac5-183">This command returns the DNS suffix.</span></span> <span data-ttu-id="06ac5-184">Na przykład **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="06ac5-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change the primary DNS suffix configuration of the virtual machine. This enables the virtual machine to automatically resolve the host name of the HBase cluster without explicit specification of the suffix. For example, the *workernode0* host name will be correctly resolved to workernode0 of the HBase cluster.

    To make the configuration change:

    1. RDP into the virtual machine.
    2. Open **Local Group Policy Editor**. The executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** to the value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot the virtual machine.
-->

<span data-ttu-id="06ac5-185">Aby sprawdzić, czy maszyny wirtualne mogą komunikować się z klastra HBase, użyj polecenia `ping headnode0.<dns suffix>` z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06ac5-185">To verify that the virtual machine can communicate with the HBase cluster, use the command `ping headnode0.<dns suffix>` from the virtual machine.</span></span> <span data-ttu-id="06ac5-186">Na przykład headnode0.mycluster.b1.cloudapp.net ping.</span><span class="sxs-lookup"><span data-stu-id="06ac5-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="06ac5-187">Aby użyć tych informacji w aplikacji Java, można wykonać kroki opisane w [Użyj Maven do tworzenia aplikacji Java korzystających z bazy danych HBase w usłudze HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="06ac5-187">To use this information in a Java application, you can follow the steps in [Use Maven to build Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) to create an application.</span></span> <span data-ttu-id="06ac5-188">Aby połączyć się ze zdalnym serwerem bazy danych HBase aplikacji, należy zmodyfikować **hbase-site.xml** pliku w tym przykładzie do zastosowania nazwy FQDN dla dozorcy.</span><span class="sxs-lookup"><span data-stu-id="06ac5-188">To have the application connect to a remote HBase server, modify the **hbase-site.xml** file in this example to use the FQDN for Zookeeper.</span></span> <span data-ttu-id="06ac5-189">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="06ac5-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="06ac5-190">Aby uzyskać więcej informacji na temat rozpoznawania nazw w usłudze Azure sieci wirtualnych oraz o sposobie używania własnych serwera DNS, zobacz [rozpoznawania nazw (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="06ac5-190">For more information about name resolution in Azure virtual networks, including how to use your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="06ac5-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="06ac5-191">Next steps</span></span>
<span data-ttu-id="06ac5-192">W tym samouczku przedstawiono sposób utworzyć klaster HBase.</span><span class="sxs-lookup"><span data-stu-id="06ac5-192">In this tutorial, you learned how to create an HBase cluster.</span></span> <span data-ttu-id="06ac5-193">Aby dowiedzieć się więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="06ac5-193">To learn more, see:</span></span>

* [<span data-ttu-id="06ac5-194">Rozpoczynanie pracy z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="06ac5-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="06ac5-195">Użyj węzłami pusty krawędzi w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="06ac5-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="06ac5-196">Konfigurowanie replikacji bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="06ac5-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="06ac5-197">Tworzenie klastrów Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="06ac5-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="06ac5-198">Rozpoczynanie pracy z platformą Hadoop w usłudze HDInsight przy użyciu bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="06ac5-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="06ac5-199">Analizowanie Twitter wskaźniki nastrojów klientów z bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="06ac5-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="06ac5-200">[Omówienie sieci wirtualnej][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="06ac5-200">[Virtual Network Overview][vnet-overview]</span></span>

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
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Szczegóły udostępniania dla nowego klastra HBase"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Użyj akcji skryptu, aby dostosować klastra HBase"

[azure-preview-portal]: https://portal.azure.com
