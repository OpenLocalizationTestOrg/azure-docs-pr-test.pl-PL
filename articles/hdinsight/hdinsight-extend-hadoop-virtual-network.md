---
title: "Rozszerzenie usługi HDInsight za pomocą sieci wirtualnej - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać sieci wirtualnej platformy Azure do łączenia usługi HDInsight do innych zasobów w chmurze lub zasobów w centrum danych."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 380423ec42ad4905c73fcd57501102e9f7062e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="e5831-103">Rozszerzenie Azure HDInsight przy użyciu sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e5831-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="e5831-104">Dowiedz się, jak używać usługi HDInsight za pomocą [sieci wirtualnej Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5831-104">Learn how to use HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="e5831-105">Przy użyciu sieci wirtualnej platformy Azure umożliwia następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="e5831-105">Using an Azure Virtual Network enables the following scenarios:</span></span>

* <span data-ttu-id="e5831-106">Łączenie z usługą HDInsight bezpośrednio z sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-106">Connecting to HDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="e5831-107">Łączenie z danymi usługi HDInsight są przechowywane w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5831-107">Connecting HDInsight to data stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="e5831-108">Bezpośredni dostęp do usług Hadoop, które nie są dostępne publicznie w Internecie.</span><span class="sxs-lookup"><span data-stu-id="e5831-108">Directly accessing Hadoop services that are not available publicly over the internet.</span></span> <span data-ttu-id="e5831-109">Na przykład interfejsy API Kafka lub interfejsu API języka Java HBase.</span><span class="sxs-lookup"><span data-stu-id="e5831-109">For example, Kafka APIs or the HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="e5831-110">Informacje przedstawione w tym dokumencie wymaga zrozumienia sieci TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="e5831-110">The information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="e5831-111">Jeśli nie masz doświadczenia z TCP/IP w sieci, należy partnera z osobą, która jest przed dokonaniem zmiany w sieciach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="e5831-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications to production networks.</span></span>

## <a name="planning"></a><span data-ttu-id="e5831-112">Planowanie</span><span class="sxs-lookup"><span data-stu-id="e5831-112">Planning</span></span>

<span data-ttu-id="e5831-113">Poniżej przedstawiono pytania, na które musi odpowiedzieć w przypadku planowania instalacji usługi HDInsight w sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e5831-113">The following are the questions that you must answer when planning to install HDInsight in a virtual network:</span></span>

* <span data-ttu-id="e5831-114">Czy trzeba zainstalować usługi HDInsight w istniejącej sieci wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="e5831-114">Do you need to install HDInsight into an existing virtual network?</span></span> <span data-ttu-id="e5831-115">Lub w przypadku tworzenia nowej sieci?</span><span class="sxs-lookup"><span data-stu-id="e5831-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="e5831-116">Jeśli korzystasz z istniejącej sieci wirtualnej, może być konieczne modyfikowanie konfiguracji sieciowej, przed zainstalowaniem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-116">If you are using an existing virtual network, you may need to modify the network configuration before you can install HDInsight.</span></span> <span data-ttu-id="e5831-117">Aby uzyskać więcej informacji, zobacz [dodać HDInsight do istniejącej sieci wirtualnej](#existingvnet) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-117">For more information, see the [add HDInsight to an existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="e5831-118">Czy chcesz połączyć sieć wirtualną zawierający HDInsight do innej sieci wirtualnej lub w sieci lokalnej?</span><span class="sxs-lookup"><span data-stu-id="e5831-118">Do you want to connect the virtual network containing HDInsight to another virtual network or your on-premises network?</span></span>

    <span data-ttu-id="e5831-119">Aby łatwo pracy z zasobami w sieciach, może być konieczne utworzyć niestandardowe DNS i skonfigurować przesyłania dalej DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-119">To easily work with resources across networks, you may need to create a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="e5831-120">Aby uzyskać więcej informacji, zobacz [łączenie wielu sieci](#multinet) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-120">For more information, see the [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="e5831-121">Czy chcesz ograniczyć/przekierowanie ruchu przychodzącego i wychodzącego do usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5831-121">Do you want to restrict/redirect inbound or outbound traffic to HDInsight?</span></span>

    <span data-ttu-id="e5831-122">HDInsight musi mieć nieograniczony komunikację z określonych adresów IP w centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="e5831-122">HDInsight must have unrestricted communication with specific IP addresses in the Azure data center.</span></span> <span data-ttu-id="e5831-123">Istnieje kilka portów, które może do komunikacji z klientem za pośrednictwem zapór.</span><span class="sxs-lookup"><span data-stu-id="e5831-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="e5831-124">Aby uzyskać więcej informacji, zobacz [kontrolowanie ruchu w sieci](#networktraffic) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-124">For more information, see the [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="e5831-125"><a id="existingvnet"></a>Dodaj HDInsight do istniejącej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e5831-125"><a id="existingvnet"></a>Add HDInsight to an existing virtual network</span></span>

<span data-ttu-id="e5831-126">Wykonaj kroki w tej sekcji, aby dowiedzieć się, jak dodać nowy HDInsight do istniejącej sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5831-126">Use the steps in this section to discover how to add a new HDInsight to an existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="e5831-127">Nie można dodać istniejącego klastra usługi HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="e5831-128">Dla sieci wirtualnej jest używany klasyczny lub modelu wdrażania usługi Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="e5831-128">Are you using a classic or Resource Manager deployment model for the virtual network?</span></span>

    <span data-ttu-id="e5831-129">HDInsight 3.4 i większa wymaga sieci wirtualnej Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="e5831-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="e5831-130">Wcześniejszych wersji usługi hdinsight wymagane klasycznej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="e5831-131">Istniejącej sieci w przypadku klasycznych sieci wirtualnej, należy utworzyć sieć wirtualną Resource Manager i połącz dwa.</span><span class="sxs-lookup"><span data-stu-id="e5831-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect the two.</span></span> <span data-ttu-id="e5831-132">[Klasyczne sieci wirtualne nawiązywania połączenia z nowej sieci wirtualnych](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5831-132">[Connecting classic VNets to new VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="e5831-133">Po dołączone do usługi HDInsight w sieci usługi Resource Manager może współdziałać z zasobów w klasycznej sieci.</span><span class="sxs-lookup"><span data-stu-id="e5831-133">Once joined, HDInsight installed in the Resource Manager network can interact with resources in the classic network.</span></span>

2. <span data-ttu-id="e5831-134">Należy używać tunelowania wymuszonego?</span><span class="sxs-lookup"><span data-stu-id="e5831-134">Do you use forced tunneling?</span></span> <span data-ttu-id="e5831-135">Wymuszanie tunelowania jest ustawienia podsieci, która wymusza wychodzący ruch internetowy do urządzenie na potrzeby inspekcji i rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="e5831-135">Forced tunneling is a subnet setting that forces outbound Internet traffic to a device for inspection and logging.</span></span> <span data-ttu-id="e5831-136">HDInsight nie obsługuje wymuszanie tunelowania.</span><span class="sxs-lookup"><span data-stu-id="e5831-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="e5831-137">Usuń wymuszanie tunelowania przed zainstalowaniem usługi HDInsight do podsieci albo utwórz nową podsieć dla usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="e5831-138">Używasz grup zabezpieczeń sieci, trasy zdefiniowane przez użytkownika lub urządzenia sieci wirtualne do ograniczania ruchu do lub z sieci wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="e5831-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances to restrict traffic into or out of the virtual network?</span></span>

    <span data-ttu-id="e5831-139">Jako zarządzanej usługi HDInsight wymaga nieograniczony dostęp do wielu adresów IP w centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="e5831-139">As a managed service, HDInsight requires unrestricted access to several IP addresses in the Azure data center.</span></span> <span data-ttu-id="e5831-140">Aby umożliwić komunikację z tych adresów IP, zaktualizuj istniejących grup zabezpieczeń sieci ani trasy zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e5831-140">To allow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="e5831-141">HDInsight obsługuje wielu usług, które korzystają z różnych portów.</span><span class="sxs-lookup"><span data-stu-id="e5831-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="e5831-142">Nie blokuje ruchu skierowanego do tych portów.</span><span class="sxs-lookup"><span data-stu-id="e5831-142">Do not block traffic to these ports.</span></span> <span data-ttu-id="e5831-143">Aby uzyskać listę portów, aby umożliwić przez urządzenie wirtualne zapory, zobacz [zabezpieczeń](#security) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-143">For a list of ports to allow through virtual appliance firewalls, see the [Security](#security) section.</span></span>

    <span data-ttu-id="e5831-144">Aby znaleźć istniejącej konfiguracji zabezpieczeń, użyj następujących poleceń programu Azure PowerShell lub interfejsu wiersza polecenia Azure:</span><span class="sxs-lookup"><span data-stu-id="e5831-144">To find your existing security configuration, use the following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="e5831-145">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="e5831-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="e5831-146">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z grup zabezpieczeń sieci](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-146">For more information, see the [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="e5831-147">Reguły grupy zabezpieczeń sieci są stosowane w kolejności, w oparciu o priorytet reguły.</span><span class="sxs-lookup"><span data-stu-id="e5831-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="e5831-148">Zastosowano pierwszej reguły, która odpowiada wzorcowi ruchu, a nie inne są stosowane dla tego ruchu.</span><span class="sxs-lookup"><span data-stu-id="e5831-148">The first rule that matches the traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="e5831-149">Kolejność reguł z najbardziej ograniczająca najbardziej ograniczająca.</span><span class="sxs-lookup"><span data-stu-id="e5831-149">Order rules from most permissive to least permissive.</span></span> <span data-ttu-id="e5831-150">Aby uzyskać więcej informacji, zobacz [filtrowania ruchu sieciowego z grup zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-150">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="e5831-151">Trasy definiowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="e5831-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="e5831-152">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z tras](../virtual-network/virtual-network-routes-troubleshoot-portal.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-152">For more information, see the [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="e5831-153">Tworzenie klastra usługi HDInsight i wybierz sieć wirtualną Azure podczas konfigurowania.</span><span class="sxs-lookup"><span data-stu-id="e5831-153">Create an HDInsight cluster and select the Azure Virtual Network during configuration.</span></span> <span data-ttu-id="e5831-154">Zrozumienie procesu tworzenia klastra, wykonaj kroki w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="e5831-154">Use the steps in the following documents to understand the cluster creation process:</span></span>

    * <span data-ttu-id="e5831-155">[Create HDInsight using the Azure portal](hdinsight-hadoop-create-linux-clusters-portal.md) (Tworzenie klastrów usługi HDInsight za pomocą usługi Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="e5831-155">[Create HDInsight using the Azure portal](hdinsight-hadoop-create-linux-clusters-portal.md)</span></span>
    * <span data-ttu-id="e5831-156">[Create HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) (Tworzenie klastrów usługi HDInsight przy użyciu programu Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="e5831-156">[Create HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>
    * [<span data-ttu-id="e5831-157">Tworzenie usługi HDInsight przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="e5831-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="e5831-158">Tworzenie usługi HDInsight przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e5831-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="e5831-159">Dodawanie HDInsight do sieci wirtualnej jest to krok konfiguracji opcjonalnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-159">Adding HDInsight to a virtual network is an optional configuration step.</span></span> <span data-ttu-id="e5831-160">Należy wybrać sieć wirtualną podczas konfigurowania klastra.</span><span class="sxs-lookup"><span data-stu-id="e5831-160">Be sure to select the virtual network when configuring the cluster.</span></span>

## <span data-ttu-id="e5831-161"><a id="multinet"></a>Łączenie wielu sieci</span><span class="sxs-lookup"><span data-stu-id="e5831-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="e5831-162">Największych wyzwanie z konfiguracji usługi sieciowej jest rozpoznawania nazw między sieciami.</span><span class="sxs-lookup"><span data-stu-id="e5831-162">The biggest challenge with a multi-network configuration is name resolution between the networks.</span></span>

<span data-ttu-id="e5831-163">Platforma Azure udostępnia rozpoznawanie nazw dla usług Azure, które są zainstalowane w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="e5831-164">To rozwiązanie nazwa wbudowanego umożliwia HDInsight połączyć się z następującymi zasobami za pomocą w pełni kwalifikowaną nazwą domeny (FQDN):</span><span class="sxs-lookup"><span data-stu-id="e5831-164">This built-in name resolution allows HDInsight to connect to the following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="e5831-165">Zasób, który jest dostępny w Internecie.</span><span class="sxs-lookup"><span data-stu-id="e5831-165">Any resource that is available on the internet.</span></span> <span data-ttu-id="e5831-166">Na przykład microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="e5831-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="e5831-167">Dowolnego zasobu, który znajduje się w tej samej sieci wirtualnej Azure, używając __wewnętrzna nazwa DNS__ zasobu.</span><span class="sxs-lookup"><span data-stu-id="e5831-167">Any resource that is in the same Azure Virtual Network, by using the __internal DNS name__ of the resource.</span></span> <span data-ttu-id="e5831-168">Na przykład podczas rozpoznawania nazwy domyślnej, poniżej przedstawiono przykład wewnętrznej nazwy DNS przypisane do węzłów procesu roboczego usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e5831-168">For example, when using the default name resolution, the following are example internal DNS names assigned to HDInsight worker nodes:</span></span>

    * <span data-ttu-id="e5831-169">wn0 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="e5831-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="e5831-170">wn2 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="e5831-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="e5831-171">Oba te węzły mogą komunikować się bezpośrednio ze sobą oraz inne węzły w usłudze HDInsight, za pomocą wewnętrznej nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="e5831-172">Rozpoznawanie nazw domyślny jest __nie__ Zezwalaj HDInsight do rozpoznawania nazw zasobów w sieci, które są przyłączone do sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-172">The default name resolution does __not__ allow HDInsight to resolve the names of resources in networks that are joined to the virtual network.</span></span> <span data-ttu-id="e5831-173">Na przykład jest wspólne, aby dołączyć do sieci wirtualnej sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-173">For example, it is common to join your on-premises network to the virtual network.</span></span> <span data-ttu-id="e5831-174">Tylko domyślny rozpoznawania nazw HDInsight nie uzyskiwanie dostępu do zasobów w sieci lokalnej według nazwy.</span><span class="sxs-lookup"><span data-stu-id="e5831-174">With only the default name resolution, HDInsight cannot access resources in the on-premises network by name.</span></span> <span data-ttu-id="e5831-175">Odwrotny również ma wartość true, zasobów w sieci lokalnej nie może uzyskać dostęp do zasobów w sieci wirtualnej według nazwy.</span><span class="sxs-lookup"><span data-stu-id="e5831-175">The opposite is also true, resources in your on-premises network cannot access resources in the virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="e5831-176">Należy utworzyć niestandardowy serwer DNS i skonfiguruj sieć wirtualną w celu używania go przed utworzeniem klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-176">You must create the custom DNS server and configure the virtual network to use it before creating the HDInsight cluster.</span></span>

<span data-ttu-id="e5831-177">Aby włączyć rozpoznawanie nazw między zasobami w przyłączone do sieci i sieci wirtualnej, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e5831-177">To enable name resolution between the virtual network and resources in joined networks, you must perform the following actions:</span></span>

1. <span data-ttu-id="e5831-178">Utwórz niestandardowy serwer DNS w sieci wirtualnej platformy Azure, której zamierzasz zainstalować usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-178">Create a custom DNS server in the Azure Virtual Network where you plan to install HDInsight.</span></span>

2. <span data-ttu-id="e5831-179">Skonfiguruj sieć wirtualną do użycia niestandardowego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-179">Configure the virtual network to use the custom DNS server.</span></span>

3. <span data-ttu-id="e5831-180">Znajdź Azure przypisane sufiksu DNS dla sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-180">Find the Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="e5831-181">Ta wartość jest podobny do `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="e5831-181">This value is similar to `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="e5831-182">Aby uzyskać informacje o sufiks DNS, zobacz [przykład: niestandardowe DNS](#example-dns) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-182">For information on finding the DNS suffix, see the [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="e5831-183">Konfiguruj przekazywanie między serwerami DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-183">Configure forwarding between the DNS servers.</span></span> <span data-ttu-id="e5831-184">Konfiguracja zależy od wybranego typu sieci zdalnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-184">The configuration depends on the type of remote network.</span></span>

    * <span data-ttu-id="e5831-185">W przypadku sieci zdalnej przez sieć lokalną DNS należy skonfigurować następująco:</span><span class="sxs-lookup"><span data-stu-id="e5831-185">If the remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="e5831-186">__Niestandardowe DNS__ (w sieci wirtualnej):</span><span class="sxs-lookup"><span data-stu-id="e5831-186">__Custom DNS__ (in the virtual network):</span></span>

            * <span data-ttu-id="e5831-187">Przesyłania żądań dla sufiksu DNS w sieci wirtualnej do platformy Azure cyklicznego programu rozpoznawania nazw (168.63.129.16).</span><span class="sxs-lookup"><span data-stu-id="e5831-187">Forward requests for the DNS suffix of the virtual network to the Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="e5831-188">Azure obsługuje żądania zasobów w sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e5831-188">Azure handles requests for resources in the virtual network</span></span>

            * <span data-ttu-id="e5831-189">Przekazuj wszystkie żądania do lokalnego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-189">Forward all other requests to the on-premises DNS server.</span></span> <span data-ttu-id="e5831-190">DNS lokalnymi obsługuje wszystkich innych żądań rozpoznawania nazw, nawet żądania zasobów internetowych, takich jak Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="e5831-190">The on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="e5831-191">__DNS lokalnymi__: przesyłać żądania dla sufiksu DNS sieci wirtualnej do niestandardowego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-191">__On-premises DNS__: Forward requests for the virtual network DNS suffix to the custom DNS server.</span></span> <span data-ttu-id="e5831-192">Niestandardowy serwer DNS przekazuje następnie do platformy Azure cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="e5831-192">The custom DNS server then forwards to the Azure recursive resolver.</span></span>

        <span data-ttu-id="e5831-193">Tej konfiguracji żądania trasy dla w pełni kwalifikowane nazwy domen, zawierające sufiks DNS w sieci wirtualnej do niestandardowego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-193">This configuration routes requests for fully qualified domain names that contain the DNS suffix of the virtual network to the custom DNS server.</span></span> <span data-ttu-id="e5831-194">Wszystkie żądania (nawet w przypadku publicznych adresów internetowych) są obsługiwane przez lokalny serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-194">All other requests (even for public internet addresses) are handled by the on-premises DNS server.</span></span>

    * <span data-ttu-id="e5831-195">W przypadku sieci zdalnej inna sieć wirtualna Azure DNS należy skonfigurować następująco:</span><span class="sxs-lookup"><span data-stu-id="e5831-195">If the remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="e5831-196">__Niestandardowe DNS__ (w każdej sieci wirtualnej):</span><span class="sxs-lookup"><span data-stu-id="e5831-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="e5831-197">Żądania dla sufiksu DNS, sieci wirtualnych są przekazywane do niestandardowych serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-197">Requests for the DNS suffix of the virtual networks are forwarded to the custom DNS servers.</span></span> <span data-ttu-id="e5831-198">Serwer DNS w każdej sieci wirtualnej jest odpowiedzialny za rozpoznawania zasobów w sieci.</span><span class="sxs-lookup"><span data-stu-id="e5831-198">The DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="e5831-199">Przesyła wszystkich innych żądaniach Azure cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="e5831-199">Forward all other requests to the Azure recursive resolver.</span></span> <span data-ttu-id="e5831-200">Cyklicznego programu rozpoznawania nazw jest odpowiedzialny za rozwiązania lokalnego i zasobów w Internecie.</span><span class="sxs-lookup"><span data-stu-id="e5831-200">The recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="e5831-201">Serwer DNS dla każdej sieci przekazuje żądania do drugiej strony, na podstawie sufiksu DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-201">The DNS server for each network forwards requests to the other, based on DNS suffix.</span></span> <span data-ttu-id="e5831-202">Inne żądania zostaną rozwiązane, za pomocą usługi Azure cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="e5831-202">Other requests are resolved using the Azure recursive resolver.</span></span>

    <span data-ttu-id="e5831-203">Na przykład każdej konfiguracji zobacz [przykład: niestandardowe DNS](#example-dns) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-203">For an example of each configuration, see the [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="e5831-204">Aby uzyskać więcej informacji, zobacz [rozpoznawanie nazwy dla maszyn wirtualnych i wystąpień roli](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-204">For more information, see the [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-to-hadoop-services"></a><span data-ttu-id="e5831-205">Bezpośrednio z usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="e5831-205">Directly connect to Hadoop services</span></span>

<span data-ttu-id="e5831-206">Większość dokumentacji w usłudze HDInsight założono, że dostęp do klastra za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="e5831-206">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="e5831-207">Na przykład czy możesz połączyć się z klastrem w https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="e5831-207">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="e5831-208">Ten adres używa publicznego brama nie jest dostępna w przypadku użycia grup NSG lub Udr ograniczyć dostęp z Internetu.</span><span class="sxs-lookup"><span data-stu-id="e5831-208">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="e5831-209">Aby połączyć się Ambari i stron sieci web za pośrednictwem sieci wirtualnej, użyj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e5831-209">To connect to Ambari and other web pages through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="e5831-210">Aby odnaleźć wewnętrzny pełni kwalifikowanych nazw domen (FQDN) węzły klastra usługi HDInsight, użyj jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="e5831-210">To discover the internal fully qualified domain names (FQDN) of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    <span data-ttu-id="e5831-211">Na liście węzłów zwrócił znaleźć nazwę FQDN dla węzłów głównych i nawiązywania Ambari i innych usług sieci web przy użyciu nazw FQDN.</span><span class="sxs-lookup"><span data-stu-id="e5831-211">In the list of nodes returned, find the FQDN for the head nodes and use the FQDNs to connect to Ambari and other web services.</span></span> <span data-ttu-id="e5831-212">Na przykład użyć `http://<headnode-fqdn>:8080` do narzędzia Ambari.</span><span class="sxs-lookup"><span data-stu-id="e5831-212">For example, use `http://<headnode-fqdn>:8080` to access Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e5831-213">Niektóre usługi hostowanej o węzłach głównych są tylko aktywne na jednym węźle naraz.</span><span class="sxs-lookup"><span data-stu-id="e5831-213">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="e5831-214">Jeśli spróbujesz uzyskiwanie dostępu do usługi na jednym węźle głównym i zwraca błąd 404, przełącz się do innego węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="e5831-214">If you try accessing a service on one head node and it returns a 404 error, switch to the other head node.</span></span>

2. <span data-ttu-id="e5831-215">Aby określić węzeł i port, który usługa jest dostępna na, zobacz [porty używane przez usługi Hadoop w usłudze HDInsight](./hdinsight-hadoop-port-settings-for-services.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-215">To determine the node and port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="e5831-216"><a id="networktraffic"></a>Kontrolowanie ruchu w sieci</span><span class="sxs-lookup"><span data-stu-id="e5831-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="e5831-217">Ruch sieciowy w sieciach wirtualnych platformy Azure można sterować przy użyciu następujących metod:</span><span class="sxs-lookup"><span data-stu-id="e5831-217">Network traffic in an Azure Virtual Networks can be controlled using the following methods:</span></span>

* <span data-ttu-id="e5831-218">**Sieciowe grupy zabezpieczeń** (NSG) umożliwiają filtrowanie ruchu przychodzącego i wychodzącego do sieci.</span><span class="sxs-lookup"><span data-stu-id="e5831-218">**Network security groups** (NSG) allow you to filter inbound and outbound traffic to the network.</span></span> <span data-ttu-id="e5831-219">Aby uzyskać więcej informacji, zobacz [filtrowania ruchu sieciowego z grup zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-219">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="e5831-220">HDInsight nie obsługuje ograniczenia ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="e5831-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="e5831-221">**Trasy zdefiniowane przez użytkownika** (przez) zdefiniuj, jak przepływa ruch między zasobami w sieci.</span><span class="sxs-lookup"><span data-stu-id="e5831-221">**User-defined routes** (UDR) define how traffic flows between resources in the network.</span></span> <span data-ttu-id="e5831-222">Aby uzyskać więcej informacji, zobacz [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../virtual-network/virtual-networks-udr-overview.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-222">For more information, see the [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="e5831-223">**Sieci wirtualnych urządzeń** replikować funkcjonalność urządzeń, takich jak routery i zapory.</span><span class="sxs-lookup"><span data-stu-id="e5831-223">**Network virtual appliances** replicate the functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="e5831-224">Aby uzyskać więcej informacji, zobacz [urządzenia sieciowe](https://azure.microsoft.com/solutions/network-appliances) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-224">For more information, see the [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="e5831-225">Jako zarządzanej usługi HDInsight wymaga nieograniczony dostęp do usług platformy Azure kondycji i zarządzania w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="e5831-225">As a managed service, HDInsight requires unrestricted access to Azure health and management services in the Azure cloud.</span></span> <span data-ttu-id="e5831-226">Przy użyciu grup NSG i Udr, należy się upewnić, że HDInsight tych usług można nadal komunikować się z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="e5831-227">HDInsight udostępnia usługi na kilku portów.</span><span class="sxs-lookup"><span data-stu-id="e5831-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="e5831-228">Używając urządzenie wirtualne zapory, musisz zezwolić na ruch na portach używanych na potrzeby tych usług.</span><span class="sxs-lookup"><span data-stu-id="e5831-228">When using a virtual appliance firewall, you must allow traffic on the ports used for these services.</span></span> <span data-ttu-id="e5831-229">Aby uzyskać więcej informacji zobacz sekcję [wymagane porty].</span><span class="sxs-lookup"><span data-stu-id="e5831-229">For more information, see the [Required ports] section.</span></span>

### <span data-ttu-id="e5831-230"><a id="hdinsight-ip"></a>HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="e5831-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="e5831-231">Jeśli planujesz używanie **sieciowej grupy zabezpieczeń** lub **trasy zdefiniowane przez użytkownika** do kontroli ruchu sieciowego, wykonaj następujące czynności przed zainstalowaniem usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e5831-231">If you plan on using **network security groups** or **user-defined routes** to control network traffic, perform the following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="e5831-232">Określ region platformy Azure, które będą używane dla usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-232">Identify the Azure region that you plan to use for HDInsight.</span></span>

2. <span data-ttu-id="e5831-233">Określ adresy IP wymagane przez usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-233">Identify the IP addresses required by HDInsight.</span></span> <span data-ttu-id="e5831-234">Aby uzyskać więcej informacji, zobacz [adresy IP wymagane przez HDInsight](#hdinsight-ip) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-234">For more information, see the [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="e5831-235">Utwórz lub zmodyfikuj grupy zabezpieczeń sieci lub zdefiniowanej przez użytkownika tras dla podsieci, które zamierzasz zainstalować HDInsight do.</span><span class="sxs-lookup"><span data-stu-id="e5831-235">Create or modify the network security groups or user-defined routes for the subnet that you plan to install HDInsight into.</span></span>

    * <span data-ttu-id="e5831-236">__Sieciowe grupy zabezpieczeń__: Zezwalaj na __przychodzących__ ruch na porcie __443__ z adresu IP, adresy.</span><span class="sxs-lookup"><span data-stu-id="e5831-236">__Network security groups__: allow __inbound__ traffic on port __443__ from the IP addresses.</span></span>
    * <span data-ttu-id="e5831-237">__Trasy zdefiniowane przez użytkownika__: Utwórz trasę do każdego adresu IP i ustaw __następnego przeskoku typu__ do __Internet__.</span><span class="sxs-lookup"><span data-stu-id="e5831-237">__User-defined routes__: create a route to each IP address and set the __Next hop type__ to __Internet__.</span></span>

<span data-ttu-id="e5831-238">Aby uzyskać więcej informacji na sieciowych grup zabezpieczeń lub trasy zdefiniowane przez użytkownika Zobacz następującą dokumentację:</span><span class="sxs-lookup"><span data-stu-id="e5831-238">For more information on network security groups or user-defined routes, see the following documentation:</span></span>

* [<span data-ttu-id="e5831-239">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="e5831-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="e5831-240">Trasy zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="e5831-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="e5831-241">Wymuszone tunelowanie</span><span class="sxs-lookup"><span data-stu-id="e5831-241">Forced tunneling</span></span>

<span data-ttu-id="e5831-242">Wymuszanie tunelowania jest zdefiniowane przez użytkownika Konfiguracja routingu którym cały ruch z podsieci będzie zmuszony do określonej sieci lub lokalizacji, takiej jak sieć lokalną.</span><span class="sxs-lookup"><span data-stu-id="e5831-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced to a specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="e5831-243">HDInsight jest __nie__ obsługi wymuszonego tunelowania.</span><span class="sxs-lookup"><span data-stu-id="e5831-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="e5831-244"><a id="hdinsight-ip"></a>Wymaganych adresów IP</span><span class="sxs-lookup"><span data-stu-id="e5831-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5831-245">Usług kondycji oraz zarządzania platformy Azure musi mieć możliwość komunikacji z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-245">The Azure health and management services must be able to communicate with HDInsight.</span></span> <span data-ttu-id="e5831-246">Jeśli używasz grup zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, zezwalać na ruch z adresów IP dla tych usług do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-246">If you use network security groups or user-defined routes, allow traffic from the IP addresses for these services to reach HDInsight.</span></span>
>
> <span data-ttu-id="e5831-247">Jeśli nie używasz grup zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika do kontroli ruchu, można zignorować w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-247">If you do not use network security groups or user-defined routes to control traffic, you can ignore this section.</span></span>

<span data-ttu-id="e5831-248">Jeśli używasz grup zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, musisz zezwolić na ruch z usług kondycji i zarządzania Azure do usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-248">If you use network security groups or user-defined routes, you must allow traffic from the Azure health and management services to reach HDInsight.</span></span> <span data-ttu-id="e5831-249">Wykonaj następujące kroki, aby znaleźć adresy IP, które może:</span><span class="sxs-lookup"><span data-stu-id="e5831-249">Use the following steps to find the IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="e5831-250">Zawsze musi zezwalać na ruch z następujących adresów IP:</span><span class="sxs-lookup"><span data-stu-id="e5831-250">You must always allow traffic from the following IP addresses:</span></span>

    | <span data-ttu-id="e5831-251">Adres IP</span><span class="sxs-lookup"><span data-stu-id="e5831-251">IP address</span></span> | <span data-ttu-id="e5831-252">Port dozwolone</span><span class="sxs-lookup"><span data-stu-id="e5831-252">Allowed port</span></span> | <span data-ttu-id="e5831-253">Kierunek</span><span class="sxs-lookup"><span data-stu-id="e5831-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="e5831-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="e5831-254">168.61.49.99</span></span> | <span data-ttu-id="e5831-255">443</span><span class="sxs-lookup"><span data-stu-id="e5831-255">443</span></span> | <span data-ttu-id="e5831-256">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-256">Inbound</span></span> |
    | <span data-ttu-id="e5831-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="e5831-257">23.99.5.239</span></span> | <span data-ttu-id="e5831-258">443</span><span class="sxs-lookup"><span data-stu-id="e5831-258">443</span></span> | <span data-ttu-id="e5831-259">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-259">Inbound</span></span> |
    | <span data-ttu-id="e5831-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="e5831-260">168.61.48.131</span></span> | <span data-ttu-id="e5831-261">443</span><span class="sxs-lookup"><span data-stu-id="e5831-261">443</span></span> | <span data-ttu-id="e5831-262">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-262">Inbound</span></span> |
    | <span data-ttu-id="e5831-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="e5831-263">138.91.141.162</span></span> | <span data-ttu-id="e5831-264">443</span><span class="sxs-lookup"><span data-stu-id="e5831-264">443</span></span> | <span data-ttu-id="e5831-265">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-265">Inbound</span></span> |

2. <span data-ttu-id="e5831-266">W przypadku klastra HDInsight w jednym z następujących regionach, następnie należy zezwolić na ruch z wymienionych dla tego obszaru adresów IP:</span><span class="sxs-lookup"><span data-stu-id="e5831-266">If your HDInsight cluster is in one of the following regions, then you must allow traffic from the IP addresses listed for the region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e5831-267">Jeśli nie ma region platformy Azure, którego używasz, następnie używać tylko cztery adresów IP z kroku 1.</span><span class="sxs-lookup"><span data-stu-id="e5831-267">If the Azure region you are using is not listed, then only use the four IP addresses from step 1.</span></span>

    | <span data-ttu-id="e5831-268">Kraj</span><span class="sxs-lookup"><span data-stu-id="e5831-268">Country</span></span> | <span data-ttu-id="e5831-269">Region</span><span class="sxs-lookup"><span data-stu-id="e5831-269">Region</span></span> | <span data-ttu-id="e5831-270">Dozwolonych adresów IP</span><span class="sxs-lookup"><span data-stu-id="e5831-270">Allowed IP addresses</span></span> | <span data-ttu-id="e5831-271">Port dozwolone</span><span class="sxs-lookup"><span data-stu-id="e5831-271">Allowed port</span></span> | <span data-ttu-id="e5831-272">Kierunek</span><span class="sxs-lookup"><span data-stu-id="e5831-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="e5831-273">Azja</span><span class="sxs-lookup"><span data-stu-id="e5831-273">Asia</span></span> | <span data-ttu-id="e5831-274">Azja Wschodnia</span><span class="sxs-lookup"><span data-stu-id="e5831-274">East Asia</span></span> | <span data-ttu-id="e5831-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="e5831-275">23.102.235.122</span></span></br><span data-ttu-id="e5831-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="e5831-276">52.175.38.134</span></span> | <span data-ttu-id="e5831-277">443</span><span class="sxs-lookup"><span data-stu-id="e5831-277">443</span></span> | <span data-ttu-id="e5831-278">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-279">Azja Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="e5831-279">Southeast Asia</span></span> | <span data-ttu-id="e5831-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="e5831-280">13.76.245.160</span></span></br><span data-ttu-id="e5831-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="e5831-281">13.76.136.249</span></span> | <span data-ttu-id="e5831-282">443</span><span class="sxs-lookup"><span data-stu-id="e5831-282">443</span></span> | <span data-ttu-id="e5831-283">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-283">Inbound</span></span> |
    | <span data-ttu-id="e5831-284">Australia</span><span class="sxs-lookup"><span data-stu-id="e5831-284">Australia</span></span> | <span data-ttu-id="e5831-285">Australia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="e5831-285">Australia East</span></span> | <span data-ttu-id="e5831-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="e5831-286">104.210.84.115</span></span></br><span data-ttu-id="e5831-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="e5831-287">13.75.152.195</span></span> | <span data-ttu-id="e5831-288">443</span><span class="sxs-lookup"><span data-stu-id="e5831-288">443</span></span> | <span data-ttu-id="e5831-289">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-290">Australia Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="e5831-290">Australia Southeast</span></span> | <span data-ttu-id="e5831-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="e5831-291">13.77.2.56</span></span></br><span data-ttu-id="e5831-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="e5831-292">13.77.2.94</span></span> | <span data-ttu-id="e5831-293">443</span><span class="sxs-lookup"><span data-stu-id="e5831-293">443</span></span> | <span data-ttu-id="e5831-294">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-294">Inbound</span></span> |
    | <span data-ttu-id="e5831-295">Brazylia</span><span class="sxs-lookup"><span data-stu-id="e5831-295">Brazil</span></span> | <span data-ttu-id="e5831-296">Brazylia Południowa</span><span class="sxs-lookup"><span data-stu-id="e5831-296">Brazil South</span></span> | <span data-ttu-id="e5831-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="e5831-297">191.235.84.104</span></span></br><span data-ttu-id="e5831-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="e5831-298">191.235.87.113</span></span> | <span data-ttu-id="e5831-299">443</span><span class="sxs-lookup"><span data-stu-id="e5831-299">443</span></span> | <span data-ttu-id="e5831-300">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-300">Inbound</span></span> |
    | <span data-ttu-id="e5831-301">Kanada</span><span class="sxs-lookup"><span data-stu-id="e5831-301">Canada</span></span> | <span data-ttu-id="e5831-302">Kanada Wschodnia</span><span class="sxs-lookup"><span data-stu-id="e5831-302">Canada East</span></span> | <span data-ttu-id="e5831-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="e5831-303">52.229.127.96</span></span></br><span data-ttu-id="e5831-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="e5831-304">52.229.123.172</span></span> | <span data-ttu-id="e5831-305">443</span><span class="sxs-lookup"><span data-stu-id="e5831-305">443</span></span> | <span data-ttu-id="e5831-306">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-307">Kanada Środkowa</span><span class="sxs-lookup"><span data-stu-id="e5831-307">Canada Central</span></span> | <span data-ttu-id="e5831-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="e5831-308">52.228.37.66</span></span></br><span data-ttu-id="e5831-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="e5831-309">52.228.45.222</span></span> | <span data-ttu-id="e5831-310">443</span><span class="sxs-lookup"><span data-stu-id="e5831-310">443</span></span> | <span data-ttu-id="e5831-311">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-311">Inbound</span></span> |
    | <span data-ttu-id="e5831-312">Chiny</span><span class="sxs-lookup"><span data-stu-id="e5831-312">China</span></span> | <span data-ttu-id="e5831-313">Chiny Północne</span><span class="sxs-lookup"><span data-stu-id="e5831-313">China North</span></span> | <span data-ttu-id="e5831-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="e5831-314">42.159.96.170</span></span></br><span data-ttu-id="e5831-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="e5831-315">139.217.2.219</span></span> | <span data-ttu-id="e5831-316">443</span><span class="sxs-lookup"><span data-stu-id="e5831-316">443</span></span> | <span data-ttu-id="e5831-317">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-318">Chiny Wschodnie</span><span class="sxs-lookup"><span data-stu-id="e5831-318">China East</span></span> | <span data-ttu-id="e5831-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="e5831-319">42.159.198.178</span></span></br><span data-ttu-id="e5831-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="e5831-320">42.159.234.157</span></span> | <span data-ttu-id="e5831-321">443</span><span class="sxs-lookup"><span data-stu-id="e5831-321">443</span></span> | <span data-ttu-id="e5831-322">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-322">Inbound</span></span> |
    | <span data-ttu-id="e5831-323">Europa</span><span class="sxs-lookup"><span data-stu-id="e5831-323">Europe</span></span> | <span data-ttu-id="e5831-324">Europa Północna</span><span class="sxs-lookup"><span data-stu-id="e5831-324">North Europe</span></span> | <span data-ttu-id="e5831-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="e5831-325">52.164.210.96</span></span></br><span data-ttu-id="e5831-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="e5831-326">13.74.153.132</span></span> | <span data-ttu-id="e5831-327">443</span><span class="sxs-lookup"><span data-stu-id="e5831-327">443</span></span> | <span data-ttu-id="e5831-328">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-329">Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="e5831-329">West Europe</span></span>| <span data-ttu-id="e5831-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="e5831-330">52.166.243.90</span></span></br><span data-ttu-id="e5831-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="e5831-331">52.174.36.244</span></span> | <span data-ttu-id="e5831-332">443</span><span class="sxs-lookup"><span data-stu-id="e5831-332">443</span></span> | <span data-ttu-id="e5831-333">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-333">Inbound</span></span> |
    | <span data-ttu-id="e5831-334">Niemcy</span><span class="sxs-lookup"><span data-stu-id="e5831-334">Germany</span></span> | <span data-ttu-id="e5831-335">Niemcy Środkowe</span><span class="sxs-lookup"><span data-stu-id="e5831-335">Germany Central</span></span> | <span data-ttu-id="e5831-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="e5831-336">51.4.146.68</span></span></br><span data-ttu-id="e5831-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="e5831-337">51.4.146.80</span></span> | <span data-ttu-id="e5831-338">443</span><span class="sxs-lookup"><span data-stu-id="e5831-338">443</span></span> | <span data-ttu-id="e5831-339">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-340">Niemcy Północno-Wschodnie</span><span class="sxs-lookup"><span data-stu-id="e5831-340">Germany Northeast</span></span> | <span data-ttu-id="e5831-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="e5831-341">51.5.150.132</span></span></br><span data-ttu-id="e5831-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="e5831-342">51.5.144.101</span></span> | <span data-ttu-id="e5831-343">443</span><span class="sxs-lookup"><span data-stu-id="e5831-343">443</span></span> | <span data-ttu-id="e5831-344">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-344">Inbound</span></span> |
    | <span data-ttu-id="e5831-345">Indie</span><span class="sxs-lookup"><span data-stu-id="e5831-345">India</span></span> | <span data-ttu-id="e5831-346">Indie Środkowe</span><span class="sxs-lookup"><span data-stu-id="e5831-346">Central India</span></span> | <span data-ttu-id="e5831-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="e5831-347">52.172.153.209</span></span></br><span data-ttu-id="e5831-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="e5831-348">52.172.152.49</span></span> | <span data-ttu-id="e5831-349">443</span><span class="sxs-lookup"><span data-stu-id="e5831-349">443</span></span> | <span data-ttu-id="e5831-350">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-350">Inbound</span></span> |
    | <span data-ttu-id="e5831-351">Japonia</span><span class="sxs-lookup"><span data-stu-id="e5831-351">Japan</span></span> | <span data-ttu-id="e5831-352">Japonia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="e5831-352">Japan East</span></span> | <span data-ttu-id="e5831-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="e5831-353">13.78.125.90</span></span></br><span data-ttu-id="e5831-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="e5831-354">13.78.89.60</span></span> | <span data-ttu-id="e5831-355">443</span><span class="sxs-lookup"><span data-stu-id="e5831-355">443</span></span> | <span data-ttu-id="e5831-356">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-357">Japonia Zachodnia</span><span class="sxs-lookup"><span data-stu-id="e5831-357">Japan West</span></span> | <span data-ttu-id="e5831-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="e5831-358">40.74.125.69</span></span></br><span data-ttu-id="e5831-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="e5831-359">138.91.29.150</span></span> | <span data-ttu-id="e5831-360">443</span><span class="sxs-lookup"><span data-stu-id="e5831-360">443</span></span> | <span data-ttu-id="e5831-361">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-361">Inbound</span></span> |
    | <span data-ttu-id="e5831-362">Korea Południowa</span><span class="sxs-lookup"><span data-stu-id="e5831-362">Korea</span></span> | <span data-ttu-id="e5831-363">Korea Środkowa</span><span class="sxs-lookup"><span data-stu-id="e5831-363">Korea Central</span></span> | <span data-ttu-id="e5831-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="e5831-364">52.231.39.142</span></span></br><span data-ttu-id="e5831-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="e5831-365">52.231.36.209</span></span> | <span data-ttu-id="e5831-366">433</span><span class="sxs-lookup"><span data-stu-id="e5831-366">433</span></span> | <span data-ttu-id="e5831-367">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-368">Korea Południowa</span><span class="sxs-lookup"><span data-stu-id="e5831-368">Korea South</span></span> | <span data-ttu-id="e5831-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="e5831-369">52.231.203.16</span></span></br><span data-ttu-id="e5831-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="e5831-370">52.231.205.214</span></span> | <span data-ttu-id="e5831-371">443</span><span class="sxs-lookup"><span data-stu-id="e5831-371">443</span></span> | <span data-ttu-id="e5831-372">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-372">Inbound</span></span>
    | <span data-ttu-id="e5831-373">Wielka Brytania</span><span class="sxs-lookup"><span data-stu-id="e5831-373">United Kingdom</span></span> | <span data-ttu-id="e5831-374">Zachodnie Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="e5831-374">UK West</span></span> | <span data-ttu-id="e5831-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="e5831-375">51.141.13.110</span></span></br><span data-ttu-id="e5831-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="e5831-376">51.141.7.20</span></span> | <span data-ttu-id="e5831-377">443</span><span class="sxs-lookup"><span data-stu-id="e5831-377">443</span></span> | <span data-ttu-id="e5831-378">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-379">Południowe Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="e5831-379">UK South</span></span> | <span data-ttu-id="e5831-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="e5831-380">51.140.47.39</span></span></br><span data-ttu-id="e5831-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="e5831-381">51.140.52.16</span></span> | <span data-ttu-id="e5831-382">443</span><span class="sxs-lookup"><span data-stu-id="e5831-382">443</span></span> | <span data-ttu-id="e5831-383">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-383">Inbound</span></span> |
    | <span data-ttu-id="e5831-384">Stany Zjednoczone</span><span class="sxs-lookup"><span data-stu-id="e5831-384">United States</span></span> | <span data-ttu-id="e5831-385">Środkowe stany USA</span><span class="sxs-lookup"><span data-stu-id="e5831-385">Central US</span></span> | <span data-ttu-id="e5831-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="e5831-386">13.67.223.215</span></span></br><span data-ttu-id="e5831-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="e5831-387">40.86.83.253</span></span> | <span data-ttu-id="e5831-388">443</span><span class="sxs-lookup"><span data-stu-id="e5831-388">443</span></span> | <span data-ttu-id="e5831-389">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-390">Środkowo-północne stany USA</span><span class="sxs-lookup"><span data-stu-id="e5831-390">North Central US</span></span> | <span data-ttu-id="e5831-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="e5831-391">157.56.8.38</span></span></br><span data-ttu-id="e5831-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="e5831-392">157.55.213.99</span></span> | <span data-ttu-id="e5831-393">443</span><span class="sxs-lookup"><span data-stu-id="e5831-393">443</span></span> | <span data-ttu-id="e5831-394">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-395">Środkowo-zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="e5831-395">West Central US</span></span> | <span data-ttu-id="e5831-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="e5831-396">52.161.23.15</span></span></br><span data-ttu-id="e5831-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="e5831-397">52.161.10.167</span></span> | <span data-ttu-id="e5831-398">443</span><span class="sxs-lookup"><span data-stu-id="e5831-398">443</span></span> | <span data-ttu-id="e5831-399">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="e5831-400">Zachodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="e5831-400">West US 2</span></span> | <span data-ttu-id="e5831-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="e5831-401">52.175.211.210</span></span></br><span data-ttu-id="e5831-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="e5831-402">52.175.222.222</span></span> | <span data-ttu-id="e5831-403">443</span><span class="sxs-lookup"><span data-stu-id="e5831-403">443</span></span> | <span data-ttu-id="e5831-404">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="e5831-404">Inbound</span></span> |

    <span data-ttu-id="e5831-405">Aby uzyskać informacje dotyczące adresów IP do użycia na potrzeby Azure dla instytucji rządowych, zobacz [Azure dla instytucji rządowych analizy i analiza](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-405">For information on the IP addresses to use for Azure Government, see the [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="e5831-406">Jeśli używasz niestandardowego serwera DNS z sieci wirtualnej, należy także zezwolić na dostęp z __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="e5831-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="e5831-407">Ten adres jest platformy Azure, cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="e5831-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="e5831-408">Aby uzyskać więcej informacji, zobacz [rozpoznawanie nazw dla maszyn wirtualnych i roli wystąpień](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-408">For more information, see the [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="e5831-409">Aby uzyskać więcej informacji, zobacz [kontrolowanie ruchu w sieci](#networktraffic) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-409">For more information, see the [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="e5831-410"><a id="hdinsight-ports"></a>Wymagane porty</span><span class="sxs-lookup"><span data-stu-id="e5831-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="e5831-411">Jeśli planowane jest użycie sieci **urządzenie wirtualne zapory** do zabezpieczania sieci wirtualnej, musisz zezwolić na ruch wychodzący na następujące porty:</span><span class="sxs-lookup"><span data-stu-id="e5831-411">If you plan on using a network **virtual appliance firewall** to secure the virtual network, you must allow outbound traffic on the following ports:</span></span>

* <span data-ttu-id="e5831-412">53</span><span class="sxs-lookup"><span data-stu-id="e5831-412">53</span></span>
* <span data-ttu-id="e5831-413">443</span><span class="sxs-lookup"><span data-stu-id="e5831-413">443</span></span>
* <span data-ttu-id="e5831-414">1433</span><span class="sxs-lookup"><span data-stu-id="e5831-414">1433</span></span>
* <span data-ttu-id="e5831-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="e5831-415">11000-11999</span></span>
* <span data-ttu-id="e5831-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="e5831-416">14000-14999</span></span>

<span data-ttu-id="e5831-417">Aby uzyskać listę portów do określonych usług, zobacz [porty używane przez usługi Hadoop w usłudze HDInsight](hdinsight-hadoop-port-settings-for-services.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-417">For a list of ports for specific services, see the [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="e5831-418">Aby uzyskać więcej informacji na reguły zapory dla urządzenia wirtualnego, zobacz [scenariuszu urządzenie wirtualne](../virtual-network/virtual-network-scenario-udr-gw-nva.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e5831-418">For more information on firewall rules for virtual appliances, see the [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="e5831-419"><a id="hdinsight-nsg"></a>Przykład: sieciowych grup zabezpieczeń z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5831-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="e5831-420">Przykłady w tej sekcji przedstawiają sposób tworzenia zabezpieczeń sieci zasady grupy, zezwalających na HDInsight do komunikowania się z usługami zarządzania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5831-420">The examples in this section demonstrate how to create network security group rules that allow HDInsight to communicate with the Azure management services.</span></span> <span data-ttu-id="e5831-421">Przed użyciem w przykładach, Dostosuj adresy IP, aby odpowiadały na region platformy Azure, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="e5831-421">Before using the examples, adjust the IP addresses to match the ones for the Azure region you are using.</span></span> <span data-ttu-id="e5831-422">Niniejsze informacje można znaleźć [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-422">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="e5831-423">Szablonu zarządzania zasobami platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e5831-423">Azure Resource Management template</span></span>

<span data-ttu-id="e5831-424">Następujący szablon zarządzanie zasobami tworzy sieć wirtualną, która ogranicza ruchu przychodzącego, ale zezwala na ruch sieciowy z adresów IP wymaganych przez usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-424">The following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span> <span data-ttu-id="e5831-425">Ten szablon umożliwia również tworzenie klastra usługi HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-425">This template also creates an HDInsight cluster in the virtual network.</span></span>

* [<span data-ttu-id="e5831-426">Wdrażanie zabezpieczonej sieci wirtualnej platformy Azure i klaster usługi HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="e5831-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="e5831-427">Zmień adresy IP używane w tym przykładzie, aby dopasować region platformy Azure, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="e5831-427">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="e5831-428">Niniejsze informacje można znaleźć [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-428">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="e5831-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5831-429">Azure PowerShell</span></span>

<span data-ttu-id="e5831-430">Użyj następującego skryptu programu PowerShell można utworzyć sieci wirtualnej, która ogranicza ruchu przychodzącego i zezwala na ruch sieciowy z adresów IP dla regionu Europa Północna.</span><span class="sxs-lookup"><span data-stu-id="e5831-430">Use the following PowerShell script to create a virtual network that restricts inbound traffic and allows traffic from the IP addresses for the North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5831-431">Zmień adresy IP używane w tym przykładzie, aby dopasować region platformy Azure, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="e5831-431">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="e5831-432">Niniejsze informacje można znaleźć [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-432">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with the resource group the virtual network is in"
$subnetName = "Replace with the name of the subnet that you plan to use for HDInsight"
# Get the Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get the region the Virtual network is in.
$location = $vnet.Location
# Get the subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for the HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set the changes to the security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply the NSG to the subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="e5831-433">W tym przykładzie pokazano, jak dodać reguły zezwalające na ruch przychodzący na wymaganych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="e5831-433">This example demonstrates how to add rules to allow inbound traffic on the required IP addresses.</span></span> <span data-ttu-id="e5831-434">Nie zawiera zasadę, aby ograniczyć dostęp dla ruchu przychodzącego z innych źródeł.</span><span class="sxs-lookup"><span data-stu-id="e5831-434">It does not contain a rule to restrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="e5831-435">W poniższym przykładzie pokazano, jak włączyć SSH dostępu z Internetu:</span><span class="sxs-lookup"><span data-stu-id="e5831-435">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="e5831-436">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e5831-436">Azure CLI</span></span>

<span data-ttu-id="e5831-437">Poniższe kroki umożliwiają utworzenie sieci wirtualnej, która ogranicza ruchu przychodzącego, ale zezwala na ruch sieciowy z adresów IP wymaganych przez usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5831-437">Use the following steps to create a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="e5831-438">Użyj następującego polecenia, aby utworzyć nową grupę zabezpieczeń sieci o nazwie `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="e5831-438">Use the following command to create a new network security group named `hdisecure`.</span></span> <span data-ttu-id="e5831-439">Zastąp **RESOURCEGROUPNAME** z grupą zasobów, który zawiera sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5831-439">Replace **RESOURCEGROUPNAME** with the resource group that contains the Azure Virtual Network.</span></span> <span data-ttu-id="e5831-440">Zastąp **lokalizacji** z grupa została utworzona w lokalizacji (regionu).</span><span class="sxs-lookup"><span data-stu-id="e5831-440">Replace **LOCATION** with the location (region) that the group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="e5831-441">Po utworzeniu grupy, pojawi się informacji na temat nowej grupy.</span><span class="sxs-lookup"><span data-stu-id="e5831-441">Once the group has been created, you receive information on the new group.</span></span>

2. <span data-ttu-id="e5831-442">Użyj następującego polecenia można dodać reguły do nowej grupy zabezpieczeń sieci Zezwalaj na komunikację ruchu przychodzącego na porcie 443 w usłudze Azure HDInsight kondycji i zarządzania.</span><span class="sxs-lookup"><span data-stu-id="e5831-442">Use the following to add rules to the new network security group that allow inbound communication on port 443 from the Azure HDInsight health and management service.</span></span> <span data-ttu-id="e5831-443">Zastąp **RESOURCEGROUPNAME** z nazwą grupy zasobów, który zawiera sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e5831-443">Replace **RESOURCEGROUPNAME** with the name of the resource group that contains the Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e5831-444">Zmień adresy IP używane w tym przykładzie, aby dopasować region platformy Azure, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="e5831-444">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="e5831-445">Niniejsze informacje można znaleźć [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-445">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="e5831-446">Aby pobrać Unikatowy identyfikator dla tej grupy zabezpieczeń sieci, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e5831-446">To retrieve the unique identifier for this network security group, use the following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="e5831-447">To polecenie zwraca wartość podobny do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="e5831-447">This command returns a value similar to the following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="e5831-448">Otrzymasz oczekiwanych rezultatów, użyj podwójnych cudzysłowów wokół identyfikatora w poleceniu.</span><span class="sxs-lookup"><span data-stu-id="e5831-448">Use double-quotes around id in the command if you don't get the expected results.</span></span>

4. <span data-ttu-id="e5831-449">Użyj następującego polecenia, aby zastosować sieciową grupę zabezpieczeń do podsieci.</span><span class="sxs-lookup"><span data-stu-id="e5831-449">Use the following command to apply the network security group to a subnet.</span></span> <span data-ttu-id="e5831-450">Zastąp __GUID__ i __RESOURCEGROUPNAME__ wartości z tymi zwracane z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="e5831-450">Replace the __GUID__ and __RESOURCEGROUPNAME__ values with the ones returned from the previous step.</span></span> <span data-ttu-id="e5831-451">Zastąp __VNETNAME__ i __SUBNETNAME__ z wirtualną nazwą sieciową i nazwę podsieci, która ma zostać utworzona.</span><span class="sxs-lookup"><span data-stu-id="e5831-451">Replace __VNETNAME__ and __SUBNETNAME__ with the virtual network name and subnet name that you want to create.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="e5831-452">Po zakończeniu wykonywania tego polecenia, można zainstalować usługi HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-452">Once this command completes, you can install HDInsight into the Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5831-453">Te kroki otwierać tylko dostęp do usługi HDInsight kondycji i zarządzania w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="e5831-453">These steps only open access to the HDInsight health and management service on the Azure cloud.</span></span> <span data-ttu-id="e5831-454">Inne dostęp do klastra usługi HDInsight z spoza sieci wirtualnej jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="e5831-454">Any other access to the HDInsight cluster from outside the Virtual Network is blocked.</span></span> <span data-ttu-id="e5831-455">Aby włączyć dostęp spoza sieci wirtualnej, należy dodać dodatkowych reguł sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e5831-455">To enable access from outside the virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="e5831-456">W poniższym przykładzie pokazano, jak włączyć SSH dostępu z Internetu:</span><span class="sxs-lookup"><span data-stu-id="e5831-456">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="e5831-457"><a id="example-dns"></a>Przykład: Konfiguracji DNS</span><span class="sxs-lookup"><span data-stu-id="e5831-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="e5831-458">Rozpoznawanie nazw między sieci wirtualnej i sieci połączonych lokalnie</span><span class="sxs-lookup"><span data-stu-id="e5831-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="e5831-459">W tym przykładzie powoduje, że następujące założenia:</span><span class="sxs-lookup"><span data-stu-id="e5831-459">This example makes the following assumptions:</span></span>

* <span data-ttu-id="e5831-460">Masz sieci wirtualnej Azure, która jest połączona z siecią lokalną przy użyciu bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="e5831-460">You have an Azure Virtual Network that is connected to an on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="e5831-461">Niestandardowy serwer DNS w sieci wirtualnej działa jako systemu operacyjnego Linux lub Unix.</span><span class="sxs-lookup"><span data-stu-id="e5831-461">The custom DNS server in the virtual network is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="e5831-462">[Powiąż](https://www.isc.org/downloads/bind/) jest zainstalowany na serwerze DNS niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="e5831-462">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS server.</span></span>

<span data-ttu-id="e5831-463">Na niestandardowy serwer DNS w sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e5831-463">On the custom DNS server in the virtual network:</span></span>

1. <span data-ttu-id="e5831-464">Użyj programu Azure PowerShell lub interfejsu wiersza polecenia Azure, aby znaleźć sufiks DNS w sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e5831-464">Use either Azure PowerShell or Azure CLI to find the DNS suffix of the virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="e5831-465">Na niestandardowy serwer DNS dla sieci wirtualnej, użyj następującego fragmentu jako zawartość `/etc/bind/named.conf.local` pliku:</span><span class="sxs-lookup"><span data-stu-id="e5831-465">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="e5831-466">Zastąp `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` wartość sufiksu DNS, sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e5831-466">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="e5831-467">Ta konfiguracja kieruje wszystkie żądania DNS dla sufiksu DNS w sieci wirtualnej do platformy Azure cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="e5831-467">This configuration routes all DNS requests for the DNS suffix of the virtual network to the Azure recursive resolver.</span></span>

2. <span data-ttu-id="e5831-468">Na niestandardowy serwer DNS dla sieci wirtualnej, użyj następującego fragmentu jako zawartość `/etc/bind/named.conf.options` pliku:</span><span class="sxs-lookup"><span data-stu-id="e5831-468">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    // TODO: Add the IP range of the joined network to this list
    acl goodclients {
        10.0.0.0/16; # IP address range of the virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent to the following
            forwarders {
                192.168.0.1; # Replace with the IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="e5831-469">Zastąp `10.0.0.0/16` wartość z zakresu adresów IP sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-469">Replace the `10.0.0.0/16` value with the IP address range of your virtual network.</span></span> <span data-ttu-id="e5831-470">Ten wpis umożliwia adresy żądań rozpoznawania nazw w tym zakresie.</span><span class="sxs-lookup"><span data-stu-id="e5831-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="e5831-471">Dodaj zakres adresów IP w sieci lokalnej do `acl goodclients { ... }` sekcji.</span><span class="sxs-lookup"><span data-stu-id="e5831-471">Add the IP address range of the on-premises network to the `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="e5831-472">Wpis umożliwia żądań rozpoznawania nazw z zasobów w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-472">entry allows name resolution requests from resources in the on-premises network.</span></span>
    
    * <span data-ttu-id="e5831-473">Zastąp wartość `192.168.0.1` przy użyciu adresu IP serwera DNS lokalnie.</span><span class="sxs-lookup"><span data-stu-id="e5831-473">Replace the value `192.168.0.1` with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="e5831-474">Ten wpis kieruje wszystkich innych żądaniach DNS do lokalnego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-474">This entry routes all other DNS requests to the on-premises DNS server.</span></span>

3. <span data-ttu-id="e5831-475">Do korzystania z konfiguracji, uruchom ponownie powiązania.</span><span class="sxs-lookup"><span data-stu-id="e5831-475">To use the configuration, restart Bind.</span></span> <span data-ttu-id="e5831-476">Na przykład `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="e5831-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="e5831-477">Dodaj warunkowego przesyłania dalej do lokalnego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-477">Add a conditional forwarder to the on-premises DNS server.</span></span> <span data-ttu-id="e5831-478">Konfigurowanie warunkowego przesyłania dalej do wysyłania żądań dla sufiksu DNS z kroku 1 do niestandardowego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-478">Configure the conditional forwarder to send requests for the DNS suffix from step 1 to the custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e5831-479">W dokumentacji oprogramowania DNS dla szczegółowych informacji na temat dodawania warunkowego przesyłania dalej.</span><span class="sxs-lookup"><span data-stu-id="e5831-479">Consult the documentation for your DNS software for specifics on how to add a conditional forwarder.</span></span>

<span data-ttu-id="e5831-480">Po wykonaniu tych czynności można połączyć się z zasobami w sieci, albo przy użyciu w pełni kwalifikowanych nazw domen (FQDN).</span><span class="sxs-lookup"><span data-stu-id="e5831-480">After completing these steps, you can connect to resources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="e5831-481">Teraz można zainstalować usługi HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-481">You can now install HDInsight into the virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="e5831-482">Rozpoznawanie nazw między dwiema połączone sieci wirtualne</span><span class="sxs-lookup"><span data-stu-id="e5831-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="e5831-483">W tym przykładzie powoduje, że następujące założenia:</span><span class="sxs-lookup"><span data-stu-id="e5831-483">This example makes the following assumptions:</span></span>

* <span data-ttu-id="e5831-484">Masz dwie sieci wirtualnych Azure, które są połączone przy użyciu bramy sieci VPN lub komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="e5831-485">Niestandardowy serwer DNS w obu sieci działa jako systemu operacyjnego Linux lub Unix.</span><span class="sxs-lookup"><span data-stu-id="e5831-485">The custom DNS server in both networks is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="e5831-486">[Powiąż](https://www.isc.org/downloads/bind/) jest zainstalowany na niestandardowych serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-486">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS servers.</span></span>

1. <span data-ttu-id="e5831-487">Użyj programu Azure PowerShell lub interfejsu wiersza polecenia Azure, aby znaleźć sufiks DNS obie sieci wirtualne:</span><span class="sxs-lookup"><span data-stu-id="e5831-487">Use either Azure PowerShell or Azure CLI to find the DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="e5831-488">Skorzystaj z poniższego tekstu jako zawartość `/etc/bind/named.config.local` pliku na niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-488">Use the following text as the contents of the `/etc/bind/named.config.local` file on the custom DNS server.</span></span> <span data-ttu-id="e5831-489">To zrobić na serwerze DNS niestandardowych w obu sieciach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e5831-489">Make this change on the custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The IP address of the DNS server in the other virtual network
    };
    ```

    <span data-ttu-id="e5831-490">Zastąp `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` wartości z sufiksem DNS __innych__ sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-490">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of the __other__ virtual network.</span></span> <span data-ttu-id="e5831-491">Ten wpis kieruje żądania dla sufiksu DNS w sieci zdalnej niestandardowe DNS w sieci.</span><span class="sxs-lookup"><span data-stu-id="e5831-491">This entry routes requests for the DNS suffix of the remote network to the custom DNS in that network.</span></span>

3. <span data-ttu-id="e5831-492">W niestandardowych serwerów DNS w sieci zarówno wirtualnych, użyj następującego fragmentu jako zawartość `/etc/bind/named.conf.options` pliku:</span><span class="sxs-lookup"><span data-stu-id="e5831-492">On the custom DNS servers in both virtual networks, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    acl goodclients {
        10.1.0.0/16; # The IP address range of one virtual network
        10.0.0.0/16; # The IP address range of the other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="e5831-493">Zastąp `10.0.0.0/16` i `10.1.0.0/16` wartości IP odnoszą się do zakresów sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="e5831-493">Replace the `10.0.0.0/16` and `10.1.0.0/16` values with the IP address ranges of your virtual networks.</span></span> <span data-ttu-id="e5831-494">Ten wpis umożliwia zasobów w każdej sieci na wysyłanie żądań do serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-494">This entry allows resources in each network to make requests of the DNS servers.</span></span>

    <span data-ttu-id="e5831-495">Wszystkie żądania, które nie są dostępne dla sufiksów DNS, sieci wirtualnych (na przykład microsoft.com) jest obsługiwane przez Azure cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="e5831-495">Any requests that are not for the DNS suffixes of the virtual networks (for example, microsoft.com) is handled by the Azure recursive resolver.</span></span>

4. <span data-ttu-id="e5831-496">Do korzystania z konfiguracji, uruchom ponownie powiązania.</span><span class="sxs-lookup"><span data-stu-id="e5831-496">To use the configuration, restart Bind.</span></span> <span data-ttu-id="e5831-497">Na przykład `sudo service bind9 restart` na obu serwerach DNS.</span><span class="sxs-lookup"><span data-stu-id="e5831-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="e5831-498">Po wykonaniu tych czynności można połączyć się z zasobami w sieci wirtualnej przy użyciu w pełni kwalifikowanych nazw domen (FQDN).</span><span class="sxs-lookup"><span data-stu-id="e5831-498">After completing these steps, you can connect to resources in the virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="e5831-499">Teraz można zainstalować usługi HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e5831-499">You can now install HDInsight into the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5831-500">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5831-500">Next steps</span></span>

* <span data-ttu-id="e5831-501">Na przykład na trasie konfigurowania usługi HDInsight można nawiązać połączenia z siecią lokalną, zobacz [HDInsight połączenia z siecią lokalną](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="e5831-501">For an end-to-end example of configuring HDInsight to connect to an on-premises network, see [Connect HDInsight to an on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="e5831-502">Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz [Omówienie usługi Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5831-502">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="e5831-503">Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, zobacz [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="e5831-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="e5831-504">Aby uzyskać więcej informacji dotyczących tras zdefiniowanych przez użytkownika, zobacz [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5831-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>