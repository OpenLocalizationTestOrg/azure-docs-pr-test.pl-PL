---
title: "Użyj węzłami pusty edge na klastrów platformy Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Jak dodać węzeł krawędzi pusty do klastra usługi HDInsight, który może być używany jako klient, a następnie/hosta testów aplikacji usługi HDInsight."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: e21dabcc6999b1f1047d334e782f723d0c03c2cb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="d6c6d-103">Użyj węzłami pusty edge na klastrów platformy Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6c6d-103">Use empty edge nodes on Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="d6c6d-104">Dowiedz się, jak dodać krawędzi pustego węzła do klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-104">Learn how to add an empty edge node to an HDInsight cluster.</span></span> <span data-ttu-id="d6c6d-105">Węzeł krawędzi pusty jest maszyny wirtualnej systemu Linux przy użyciu tego samego klienta narzędzi zainstalowane i skonfigurowane tak jak headnodes, ale bez żadnych usług Hadoop uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-105">An empty edge node is a Linux virtual machine with the same client tools installed and configured as in the headnodes, but with no Hadoop services running.</span></span> <span data-ttu-id="d6c6d-106">Za pomocą węzła krawędzi dostęp do klastra, testowanie aplikacji klienckich i hosting aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-106">You can use the edge node for accessing the cluster, testing your client applications, and hosting your client applications.</span></span> 

<span data-ttu-id="d6c6d-107">Można dodać krawędzi pustego węzła w istniejącym klastrze usługi HDInsight, do nowego klastra podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-107">You can add an empty edge node to an existing HDInsight cluster, to a new cluster when you create the cluster.</span></span> <span data-ttu-id="d6c6d-108">Dodawanie węzła krawędzi pusty jest wykonywane przy użyciu szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-108">Adding an empty edge node is done using Azure Resource Manager template.</span></span>  <span data-ttu-id="d6c6d-109">W poniższym przykładzie pokazano, jak jest wykonywane przy użyciu szablonu:</span><span class="sxs-lookup"><span data-stu-id="d6c6d-109">The following sample demonstrates how it is done using a template:</span></span>

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

<span data-ttu-id="d6c6d-110">Jak pokazano w przykładzie, opcjonalnie można wywołać [akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md) można wykonać dodatkowe czynności konfiguracyjne, takich jak instalowanie [Apache Hue](hdinsight-hadoop-hue-linux.md) w węźle krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-110">As shown in the sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) to perform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in the edge node.</span></span> <span data-ttu-id="d6c6d-111">Skrypt akcji skryptu musi być dostępny publicznie w sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-111">The script action script must be publicly accessible on the web.</span></span>  <span data-ttu-id="d6c6d-112">Na przykład jeśli skrypt jest przechowywany w magazynie Azure, użyj publiczne kontenery lub publiczne obiekty BLOB.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-112">For example, if the script is stored in Azure storage, use either public containers or public blobs.</span></span>

<span data-ttu-id="d6c6d-113">Rozmiar maszyny wirtualnej węzła krawędzi musi spełniać wymagania rozmiar maszyny wirtualnej węzła procesu roboczego HDInsight klastra.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-113">The edge node virtual machine size must meet the HDInsight cluster worker node vm size requirements.</span></span> <span data-ttu-id="d6c6d-114">Zalecany proces roboczy rozmiarów maszyn wirtualnych węzła, zobacz [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="d6c6d-114">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>

<span data-ttu-id="d6c6d-115">Po utworzeniu węzeł krawędzi, można połączyć się z węzłem krawędzi przy użyciu protokołu SSH i uruchamianie narzędzi klienta do dostępu do klastra usługi Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-115">After you have created an edge node, you can connect to the edge node using SSH, and run client tools to access the Hadoop cluster in HDInsight.</span></span>

> [!WARNING] 
> <span data-ttu-id="d6c6d-116">Przy użyciu węzła krawędzi pusta w usłudze HDInsight jest obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-116">Using an empty edge node with HDInsight is currently in preview.</span></span> <span data-ttu-id="d6c6d-117">Niestandardowe składniki, które są zainstalowane w węźle krawędzi otrzymywania uzasadnione ekonomicznie pomocy technicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-117">Custom components that are installed on the edge node receive commercially reasonable support from Microsoft.</span></span> <span data-ttu-id="d6c6d-118">Może to spowodować w rozwiązywaniu problemów występujących u użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-118">This might result in resolving problems you encounter.</span></span> <span data-ttu-id="d6c6d-119">Lub może być określonej zasoby społeczności, aby uzyskać dalszą pomoc.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-119">Or you may be referred to community resources for further assistance.</span></span> <span data-ttu-id="d6c6d-120">Poniżej przedstawiono niektóre najbardziej aktywne witryn uzyskiwanie pomocy od społeczności:</span><span class="sxs-lookup"><span data-stu-id="d6c6d-120">The following are some of the most active sites for getting help from the community:</span></span>
>
> * [<span data-ttu-id="d6c6d-121">Forum MSDN dla usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6c6d-121">MSDN forum for HDInsight</span></span>](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * <span data-ttu-id="d6c6d-122">[http://StackOverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="d6c6d-122">[http://stackoverflow.com](http://stackoverflow.com).</span></span>
>
> <span data-ttu-id="d6c6d-123">Jeśli korzystasz z technologii Apache, można znaleźć pomoc za pośrednictwem Apache witryny projektu na [http://apache.org](http://apache.org), takich jak [Hadoop](http://hadoop.apache.org/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-123">If you are using an Apache technology, you may be able to find assistance through the Apache project sites on [http://apache.org](http://apache.org), such as the [Hadoop](http://hadoop.apache.org/) site.</span></span>

## <a name="add-an-edge-node-to-an-existing-cluster"></a><span data-ttu-id="d6c6d-124">Dodawanie węzła krawędzi do istniejącego klastra</span><span class="sxs-lookup"><span data-stu-id="d6c6d-124">Add an edge node to an existing cluster</span></span>
<span data-ttu-id="d6c6d-125">W tej sekcji możesz Użyj szablonu usługi Resource Manager, aby dodać węzeł krawędzi w istniejącym klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-125">In this section, you use a Resource Manager template to add an edge node to an existing HDInsight cluster.</span></span>  <span data-ttu-id="d6c6d-126">Szablon usługi Resource Manager można znaleźć w [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="d6c6d-126">The Resource Manager template can be found in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span></span> <span data-ttu-id="d6c6d-127">Szablon usługi Resource Manager wywołuje znajdujący się w https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh akcji skryptu. Skrypt nie wykonywać żadnych akcji.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-127">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="d6c6d-128">Jest aby zademonstrować wywoływania akcji skryptu z szablonem usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-128">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="d6c6d-129">**Aby dodać węzeł krawędzi pusty do istniejącego klastra**</span><span class="sxs-lookup"><span data-stu-id="d6c6d-129">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="d6c6d-130">Tworzenie klastra usługi HDInsight, jeśli nie masz jeszcze.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-130">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="d6c6d-131">Zobacz [samouczek Hadoop: rozpoczynanie pracy z platformą Hadoop w usłudze HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6c6d-131">See [Hadoop tutorial: Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="d6c6d-132">Kliknij poniższy obraz, aby zalogować się do platformy Azure i otwórz szablon usługi Azure Resource Manager w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-132">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="d6c6d-133">Należy skonfigurować następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="d6c6d-133">Configure the following properties:</span></span>
   
   * <span data-ttu-id="d6c6d-134">**Subskrypcja**: Wybierz subskrypcję platformy Azure używana do tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-134">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="d6c6d-135">**Grupa zasobów**: Wybierz grupę zasobów, używany do istniejącego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-135">**Resource group**: Select the resource group used for the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="d6c6d-136">**Lokalizacja**: Wybierz lokalizację, w istniejącym klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-136">**Location**: Select the location of the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="d6c6d-137">**Nazwa klastra**: Wprowadź nazwę istniejącego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-137">**Cluster Name**: Enter the name of an existing HDInsight cluster.</span></span>
   * <span data-ttu-id="d6c6d-138">**Rozmiar węzła krawędzi**: Wybierz jeden z rozmiarów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-138">**Edge Node Size**: Select one of the VM sizes.</span></span> <span data-ttu-id="d6c6d-139">Rozmiar maszyny wirtualnej musi spełniać wymagania rozmiar maszyny wirtualnej węzła procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-139">The vm size must meet the worker node vm size requirements.</span></span> <span data-ttu-id="d6c6d-140">Zalecany proces roboczy rozmiarów maszyn wirtualnych węzła, zobacz [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="d6c6d-140">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>
   * <span data-ttu-id="d6c6d-141">**Krawędzi prefiksu węzła**: wartość domyślna to **nowe**.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-141">**Edge Node Prefix**: The default value is **new**.</span></span>  <span data-ttu-id="d6c6d-142">Przy użyciu wartości domyślnej, jest nazwa węzła krawędzi **nowe edgenode**.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-142">Using the default value, the edge node name is **new-edgenode**.</span></span>  <span data-ttu-id="d6c6d-143">Można dostosować prefiks z portalu.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-143">You can customize the prefix from the portal.</span></span> <span data-ttu-id="d6c6d-144">Można również dostosować pełną nazwę z szablonu.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-144">You can also customize the full name from the template.</span></span>

4. <span data-ttu-id="d6c6d-145">Sprawdź **akceptuję warunki i postanowienia, o których wspomniano**, a następnie kliknij przycisk **zakupu** można utworzyć węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-145">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the edge node.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="d6c6d-146">Upewnij się wybrać grupę zasobów platformy Azure dla istniejącego klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-146">Make sure to select the Azure resource group for the existing HDInsight cluster.</span></span>  <span data-ttu-id="d6c6d-147">W przeciwnym razie otrzymasz komunikat o błędzie "nie można wykonać żądanej operacji dla zasobu zagnieżdżonego.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-147">Otherwise, you get the error message "Can not perform requested operation on nested resource.</span></span> <span data-ttu-id="d6c6d-148">Zasobu nadrzędnego "&lt;ClusterName >' nie znaleziono."</span><span class="sxs-lookup"><span data-stu-id="d6c6d-148">Parent resource '&lt;ClusterName>' not found."</span></span>

## <a name="add-an-edge-node-when-creating-a-cluster"></a><span data-ttu-id="d6c6d-149">Dodaj węzeł krawędzi, podczas tworzenia klastra</span><span class="sxs-lookup"><span data-stu-id="d6c6d-149">Add an edge node when creating a cluster</span></span>
<span data-ttu-id="d6c6d-150">W tej sekcji użyjesz szablonu usługi Resource Manager do tworzenia klastra usługi HDInsight z węzłem krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-150">In this section, you use a Resource Manager template to create HDInsight cluster with an edge node.</span></span>  <span data-ttu-id="d6c6d-151">Szablon usługi Resource Manager można znaleźć w [galerię szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="d6c6d-151">The Resource Manager template can be found in the [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span></span> <span data-ttu-id="d6c6d-152">Szablon usługi Resource Manager wywołuje znajdujący się w https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh akcji skryptu. Skrypt nie wykonywać żadnych akcji.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-152">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="d6c6d-153">Jest aby zademonstrować wywoływania akcji skryptu z szablonem usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-153">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="d6c6d-154">**Aby dodać węzeł krawędzi pusty do istniejącego klastra**</span><span class="sxs-lookup"><span data-stu-id="d6c6d-154">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="d6c6d-155">Tworzenie klastra usługi HDInsight, jeśli nie masz jeszcze.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-155">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="d6c6d-156">Zobacz [rozpocząć korzystanie z platformy Hadoop w usłudze HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6c6d-156">See [Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="d6c6d-157">Kliknij poniższy obraz, aby zalogować się do platformy Azure i otwórz szablon usługi Azure Resource Manager w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-157">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="d6c6d-158">Należy skonfigurować następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="d6c6d-158">Configure the following properties:</span></span>
   
   * <span data-ttu-id="d6c6d-159">**Subskrypcja**: Wybierz subskrypcję platformy Azure używana do tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-159">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="d6c6d-160">**Grupa zasobów**: Utwórz nową grupę zasobów klastra.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-160">**Resource group**: Create a new resource group used for the cluster.</span></span>
   * <span data-ttu-id="d6c6d-161">**Lokalizacja**: Wybierz lokalizację dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-161">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="d6c6d-162">**Nazwa klastra**: Wprowadź nazwę dla nowego klastra utworzyć.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-162">**Cluster Name**: Enter a name for the new cluster to create.</span></span>
   * <span data-ttu-id="d6c6d-163">**Nazwa użytkownika logowania klastra**: Wprowadź nazwę użytkownika Hadoop HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-163">**Cluster Login User Name**: Enter the Hadoop HTTP user name.</span></span>  <span data-ttu-id="d6c6d-164">Nazwa domyślna to **admin**.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-164">The default name is **admin**.</span></span>
   * <span data-ttu-id="d6c6d-165">**Hasło logowania klastra**: Wprowadź hasło użytkownika Hadoop HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-165">**Cluster Login Password**: Enter the Hadoop HTTP user password.</span></span>
   * <span data-ttu-id="d6c6d-166">**SSH nazwy użytkownika**: Wprowadź nazwę użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-166">**Ssh User Name**: Enter the SSH user name.</span></span> <span data-ttu-id="d6c6d-167">Nazwa domyślna to **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-167">The default name is **sshuser**.</span></span>
   * <span data-ttu-id="d6c6d-168">**SSH hasła**: Wprowadź hasło użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-168">**Ssh Password**: Enter the SSH user password.</span></span>
   * <span data-ttu-id="d6c6d-169">**Zainstaluj akcji skryptu**: należy zachować wartość domyślną dla pośrednictwa w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-169">**Install Script Action**: Keep the default value for going through this tutorial.</span></span>
     
     <span data-ttu-id="d6c6d-170">Niektóre właściwości zostały zapisane na stałe w szablonie: typ klastra, liczba węzłów procesu roboczego klastra rozmiaru węzła krawędzi i nazwa węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-170">Some properties have been hardcoded in the template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span></span>
4. <span data-ttu-id="d6c6d-171">Sprawdź **akceptuję warunki i postanowienia, o których wspomniano**, a następnie kliknij przycisk **zakupu** do utworzenia klastra z węzłem krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-171">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the cluster with the edge node.</span></span>

## <a name="access-an-edge-node"></a><span data-ttu-id="d6c6d-172">Dostęp do węzła krawędzi</span><span class="sxs-lookup"><span data-stu-id="d6c6d-172">Access an edge node</span></span>
<span data-ttu-id="d6c6d-173">Węzeł brzegowy ssh punkt końcowy jest &lt;EdgeNodeName >.&lt; ClusterName >-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-173">The edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span></span>  <span data-ttu-id="d6c6d-174">Na przykład nowy edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-174">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span></span>

<span data-ttu-id="d6c6d-175">Węzeł krawędzi jest wyświetlany jako aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-175">The edge node appears as an application on the Azure portal.</span></span>  <span data-ttu-id="d6c6d-176">Portal zawiera informacje dostępu do węzła krawędzi przy użyciu protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-176">The portal gives you the information to access the edge node using SSH.</span></span>

<span data-ttu-id="d6c6d-177">**Aby sprawdzić punkt końcowy SSH węzła krawędzi**</span><span class="sxs-lookup"><span data-stu-id="d6c6d-177">**To verify the edge node SSH endpoint**</span></span>

1. <span data-ttu-id="d6c6d-178">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6c6d-178">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d6c6d-179">Otwórz klaster usługi HDInsight z węzłem krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-179">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="d6c6d-180">Kliknij przycisk **aplikacji** w bloku klastra.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-180">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="d6c6d-181">Zostanie wyświetlona węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-181">You shall see the edge node.</span></span>  <span data-ttu-id="d6c6d-182">Nazwa domyślna to **nowe edgenode**.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-182">The default name is **new-edgenode**.</span></span>
4. <span data-ttu-id="d6c6d-183">Kliknij węzeł krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-183">Click the edge node.</span></span> <span data-ttu-id="d6c6d-184">Zostanie wyświetlona punkt końcowy SSH.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-184">You shall see the SSH endpoint.</span></span>

<span data-ttu-id="d6c6d-185">**Aby korzystanie z programu Hive w węźle krawędzi**</span><span class="sxs-lookup"><span data-stu-id="d6c6d-185">**To use Hive on the edge node**</span></span>

1. <span data-ttu-id="d6c6d-186">Używanie protokołu SSH, aby połączyć się z węzłem krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-186">Use SSH to connect to the edge node.</span></span> <span data-ttu-id="d6c6d-187">Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d6c6d-187">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d6c6d-188">Po nawiązaniu połączenia z węzłem krawędzi przy użyciu protokołu SSH, użyj następującego polecenia, aby otworzyć konsolę gałęzi:</span><span class="sxs-lookup"><span data-stu-id="d6c6d-188">After you have connected to the edge node using SSH, use the following command to open the Hive console:</span></span>
   
        hive
3. <span data-ttu-id="d6c6d-189">Uruchom następujące polecenie, aby wyświetlić tabele programu Hive w klastrze:</span><span class="sxs-lookup"><span data-stu-id="d6c6d-189">Run the following command to show Hive tables in the cluster:</span></span>
   
        show tables;

## <a name="delete-an-edge-node"></a><span data-ttu-id="d6c6d-190">Usuń węzeł krawędzi</span><span class="sxs-lookup"><span data-stu-id="d6c6d-190">Delete an edge node</span></span>
<span data-ttu-id="d6c6d-191">W portalu Azure, można usunąć węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-191">You can delete an edge node from the Azure portal.</span></span>

<span data-ttu-id="d6c6d-192">**Dostępu węzła krawędzi**</span><span class="sxs-lookup"><span data-stu-id="d6c6d-192">**To access an edge node**</span></span>

1. <span data-ttu-id="d6c6d-193">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6c6d-193">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d6c6d-194">Otwórz klaster usługi HDInsight z węzłem krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-194">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="d6c6d-195">Kliknij przycisk **aplikacji** w bloku klastra.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-195">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="d6c6d-196">Zostanie wyświetlona lista węzłów krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-196">You shall see a list of edge nodes.</span></span>  
4. <span data-ttu-id="d6c6d-197">Kliknij prawym przyciskiem myszy węzeł krawędzi chcesz usunąć, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-197">Right-click the edge node you want to delete, and then click **Delete**.</span></span>
5. <span data-ttu-id="d6c6d-198">Kliknij przycisk **Tak**, aby potwierdzić.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-198">Click **Yes** to confirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6c6d-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6c6d-199">Next steps</span></span>
<span data-ttu-id="d6c6d-200">W tym artykule ma przedstawiono sposób dodawania węzła krawędzi oraz sposób dostępu do węzła krawędzi.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-200">In this article, you have learned how to add an edge node and how to access the edge node.</span></span> <span data-ttu-id="d6c6d-201">Aby dowiedzieć się więcej, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="d6c6d-201">To learn more, see the following articles:</span></span>

* <span data-ttu-id="d6c6d-202">[Instalowanie aplikacji usługi HDInsight](hdinsight-apps-install-applications.md): dowiedz się, jak instalować aplikacje usługi HDInsight w klastrach.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-202">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="d6c6d-203">[Instalowanie niestandardowych aplikacji usługi HDInsight](hdinsight-apps-install-custom-applications.md): Dowiedz się, jak wdrożyć aplikację usługi HDInsight nieopublikowane do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-203">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="d6c6d-204">[Publikowanie aplikacji usługi HDInsight](hdinsight-apps-publish-applications.md): dowiedz się, jak opublikować niestandardowe aplikacje usługi HDInsight w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-204">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="d6c6d-205">[MSDN: instalowanie aplikacji usługi HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): dowiedz się, jak zdefiniować aplikacje usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-205">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="d6c6d-206">[Dostosowywanie klastrów usługi HDInsight opartych na systemie Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md): dowiedz się, jak instalować dodatkowe aplikacje za pomocą akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-206">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="d6c6d-207">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md) (Tworzenie klastrów Hadoop w usłudze HDInsight opartych na systemie Linux przy użyciu szablonów usługi Resource Manager): dowiedz się, jak wywoływać szablony usługi Resource Manager w celu tworzenia klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6c6d-207">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span></span>

