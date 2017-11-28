---
title: "aaaExtend HDInsight z siecią wirtualną - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse sieci wirtualnej Azure tooconnect HDInsight tooother chmury zasobów lub zasobów w centrum danych."
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
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="fe402-103">Rozszerzenie Azure HDInsight przy użyciu sieci wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fe402-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="fe402-104">Dowiedz się, jak toouse HDInsight z [sieci wirtualnej Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe402-104">Learn how toouse HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="fe402-105">Przy użyciu sieci wirtualnej platformy Azure umożliwia hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="fe402-105">Using an Azure Virtual Network enables hello following scenarios:</span></span>

* <span data-ttu-id="fe402-106">Łączenie tooHDInsight bezpośrednio z sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-106">Connecting tooHDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="fe402-107">Łączenie HDInsight toodata są przechowywane w sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe402-107">Connecting HDInsight toodata stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="fe402-108">Bezpośrednio dostęp do usług Hadoop, które nie są dostępne publicznie ponad hello internet.</span><span class="sxs-lookup"><span data-stu-id="fe402-108">Directly accessing Hadoop services that are not available publicly over hello internet.</span></span> <span data-ttu-id="fe402-109">Na przykład interfejsy API Kafka lub hello interfejsu API języka Java HBase.</span><span class="sxs-lookup"><span data-stu-id="fe402-109">For example, Kafka APIs or hello HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="fe402-110">Witaj informacje w tym dokumencie wymaga zrozumienia sieci TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="fe402-110">hello information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="fe402-111">Jeśli nie masz doświadczenia z TCP/IP w sieci, należy partnera z osobą, która jest przed wprowadzeniem modyfikacji tooproduction sieci.</span><span class="sxs-lookup"><span data-stu-id="fe402-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications tooproduction networks.</span></span>

## <a name="planning"></a><span data-ttu-id="fe402-112">Planowanie</span><span class="sxs-lookup"><span data-stu-id="fe402-112">Planning</span></span>

<span data-ttu-id="fe402-113">Oto Hello hello pytania, na które należy odpowiedzieć przy planowaniu tooinstall HDInsight w sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="fe402-113">hello following are hello questions that you must answer when planning tooinstall HDInsight in a virtual network:</span></span>

* <span data-ttu-id="fe402-114">Potrzebujesz tooinstall HDInsight do istniejącej sieci wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="fe402-114">Do you need tooinstall HDInsight into an existing virtual network?</span></span> <span data-ttu-id="fe402-115">Lub w przypadku tworzenia nowej sieci?</span><span class="sxs-lookup"><span data-stu-id="fe402-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="fe402-116">Jeśli korzystasz z istniejącej sieci wirtualnej, może być konieczne konfiguracji sieci hello toomodify przed zainstalowaniem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe402-116">If you are using an existing virtual network, you may need toomodify hello network configuration before you can install HDInsight.</span></span> <span data-ttu-id="fe402-117">Aby uzyskać więcej informacji, zobacz hello [Dodaj istniejącej sieci wirtualnej HDInsight tooan](#existingvnet) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-117">For more information, see hello [add HDInsight tooan existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="fe402-118">Czy chcesz tooconnect hello sieci wirtualnej zawierający sieci wirtualnej tooanother HDInsight lub sieci lokalnej?</span><span class="sxs-lookup"><span data-stu-id="fe402-118">Do you want tooconnect hello virtual network containing HDInsight tooanother virtual network or your on-premises network?</span></span>

    <span data-ttu-id="fe402-119">tooeasily pracy z zasobami w sieciach, należy może toocreate niestandardowe DNS i skonfigurować przesyłania dalej DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-119">tooeasily work with resources across networks, you may need toocreate a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="fe402-120">Aby uzyskać więcej informacji, zobacz hello [łączenie wielu sieci](#multinet) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-120">For more information, see hello [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="fe402-121">Czy chcesz toorestrict/przekierowanie ruchu przychodzącego i wychodzącego tooHDInsight?</span><span class="sxs-lookup"><span data-stu-id="fe402-121">Do you want toorestrict/redirect inbound or outbound traffic tooHDInsight?</span></span>

    <span data-ttu-id="fe402-122">HDInsight musi mieć nieograniczony komunikację z określonych adresów IP w centrum danych Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-122">HDInsight must have unrestricted communication with specific IP addresses in hello Azure data center.</span></span> <span data-ttu-id="fe402-123">Istnieje kilka portów, które może do komunikacji z klientem za pośrednictwem zapór.</span><span class="sxs-lookup"><span data-stu-id="fe402-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="fe402-124">Aby uzyskać więcej informacji, zobacz hello [kontrolowanie ruchu w sieci](#networktraffic) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-124">For more information, see hello [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="fe402-125"><a id="existingvnet"></a>Dodaj HDInsight tooan istniejącej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fe402-125"><a id="existingvnet"></a>Add HDInsight tooan existing virtual network</span></span>

<span data-ttu-id="fe402-126">Wykonaj kroki hello w tej sekcji toodiscover jak tooadd nowe tooan HDInsight istniejącej sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe402-126">Use hello steps in this section toodiscover how tooadd a new HDInsight tooan existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="fe402-127">Nie można dodać istniejącego klastra usługi HDInsight w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="fe402-128">Dla sieci wirtualnej hello jest używany klasyczny lub modelu wdrażania usługi Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="fe402-128">Are you using a classic or Resource Manager deployment model for hello virtual network?</span></span>

    <span data-ttu-id="fe402-129">HDInsight 3.4 i większa wymaga sieci wirtualnej Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="fe402-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="fe402-130">Wcześniejszych wersji usługi hdinsight wymagane klasycznej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="fe402-131">Istniejącej sieci w przypadku klasycznych sieci wirtualnej, należy utworzyć sieć wirtualną Resource Manager a następnie połącz hello dwa.</span><span class="sxs-lookup"><span data-stu-id="fe402-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect hello two.</span></span> <span data-ttu-id="fe402-132">[Łączenie klasycznych sieci wirtualnych toonew sieci wirtualnych](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fe402-132">[Connecting classic VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="fe402-133">Po dołączone do usługi HDInsight w sieci usługi Resource Manager hello mogą współdziałać z zasobów w sieci klasycznego hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-133">Once joined, HDInsight installed in hello Resource Manager network can interact with resources in hello classic network.</span></span>

2. <span data-ttu-id="fe402-134">Należy używać tunelowania wymuszonego?</span><span class="sxs-lookup"><span data-stu-id="fe402-134">Do you use forced tunneling?</span></span> <span data-ttu-id="fe402-135">Wymuszanie tunelowania jest ustawienia podsieci, wymuszający wychodzącego Internet ruchu tooa urządzenia do inspekcji i rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="fe402-135">Forced tunneling is a subnet setting that forces outbound Internet traffic tooa device for inspection and logging.</span></span> <span data-ttu-id="fe402-136">HDInsight nie obsługuje wymuszanie tunelowania.</span><span class="sxs-lookup"><span data-stu-id="fe402-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="fe402-137">Usuń wymuszanie tunelowania przed zainstalowaniem usługi HDInsight do podsieci albo utwórz nową podsieć dla usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe402-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="fe402-138">Używasz grup zabezpieczeń sieci, trasy zdefiniowane przez użytkownika lub urządzenia sieci wirtualne toorestrict ruchu do lub z sieci wirtualnej hello?</span><span class="sxs-lookup"><span data-stu-id="fe402-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances toorestrict traffic into or out of hello virtual network?</span></span>

    <span data-ttu-id="fe402-139">Jako zarządzanej usługi HDInsight wymaga adresów IP tooseveral nieograniczonego dostępu w centrum danych Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-139">As a managed service, HDInsight requires unrestricted access tooseveral IP addresses in hello Azure data center.</span></span> <span data-ttu-id="fe402-140">tooallow komunikacji z tych adresów IP, zaktualizuj żadnych istniejących grup zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fe402-140">tooallow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="fe402-141">HDInsight obsługuje wielu usług, które korzystają z różnych portów.</span><span class="sxs-lookup"><span data-stu-id="fe402-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="fe402-142">Nie należy blokować ruchu toothese portów.</span><span class="sxs-lookup"><span data-stu-id="fe402-142">Do not block traffic toothese ports.</span></span> <span data-ttu-id="fe402-143">Lista portów tooallow przez urządzenie wirtualne zapory, zobacz hello [zabezpieczeń](#security) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-143">For a list of ports tooallow through virtual appliance firewalls, see hello [Security](#security) section.</span></span>

    <span data-ttu-id="fe402-144">toofind istniejącej konfiguracji zabezpieczeń, hello Użyj następującego polecenia programu Azure PowerShell lub interfejsu wiersza polecenia Azure:</span><span class="sxs-lookup"><span data-stu-id="fe402-144">toofind your existing security configuration, use hello following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="fe402-145">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="fe402-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="fe402-146">Aby uzyskać więcej informacji, zobacz hello [Rozwiązywanie problemów z grup zabezpieczeń sieci](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-146">For more information, see hello [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="fe402-147">Reguły grupy zabezpieczeń sieci są stosowane w kolejności, w oparciu o priorytet reguły.</span><span class="sxs-lookup"><span data-stu-id="fe402-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="fe402-148">Hello pierwszy pasujący wzorzec ruchu hello dotyczy reguła, a nie inne są stosowane dla tego ruchu.</span><span class="sxs-lookup"><span data-stu-id="fe402-148">hello first rule that matches hello traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="fe402-149">Kolejność reguł z najbardziej ograniczająca tooleast ograniczająca.</span><span class="sxs-lookup"><span data-stu-id="fe402-149">Order rules from most permissive tooleast permissive.</span></span> <span data-ttu-id="fe402-150">Aby uzyskać więcej informacji, zobacz hello [filtrowania ruchu sieciowego z grup zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-150">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="fe402-151">Trasy definiowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe402-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="fe402-152">Aby uzyskać więcej informacji, zobacz hello [Rozwiązywanie problemów z tras](../virtual-network/virtual-network-routes-troubleshoot-portal.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-152">For more information, see hello [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="fe402-153">Tworzenie klastra usługi HDInsight i wybierz hello Azure Virtual Network podczas konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fe402-153">Create an HDInsight cluster and select hello Azure Virtual Network during configuration.</span></span> <span data-ttu-id="fe402-154">Wykonaj kroki hello w hello następującego procesu tworzenia klastra hello toounderstand dokumentów:</span><span class="sxs-lookup"><span data-stu-id="fe402-154">Use hello steps in hello following documents toounderstand hello cluster creation process:</span></span>

    * [<span data-ttu-id="fe402-155">Tworzenie usługi HDInsight przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fe402-155">Create HDInsight using hello Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * <span data-ttu-id="fe402-156">[Create HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) (Tworzenie klastrów usługi HDInsight przy użyciu programu Azure PowerShell)</span><span class="sxs-lookup"><span data-stu-id="fe402-156">[Create HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>
    * [<span data-ttu-id="fe402-157">Tworzenie usługi HDInsight przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="fe402-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="fe402-158">Tworzenie usługi HDInsight przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe402-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="fe402-159">Dodawanie HDInsight tooa sieci wirtualnej jest to krok konfiguracji opcjonalnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-159">Adding HDInsight tooa virtual network is an optional configuration step.</span></span> <span data-ttu-id="fe402-160">Należy się, że sieć wirtualna hello tooselect podczas konfigurowania klastra hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-160">Be sure tooselect hello virtual network when configuring hello cluster.</span></span>

## <span data-ttu-id="fe402-161"><a id="multinet"></a>Łączenie wielu sieci</span><span class="sxs-lookup"><span data-stu-id="fe402-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="fe402-162">Hello największych wyzwań z konfiguracji usługi sieciowej jest rozpoznawania nazw między sieciami hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-162">hello biggest challenge with a multi-network configuration is name resolution between hello networks.</span></span>

<span data-ttu-id="fe402-163">Platforma Azure udostępnia rozpoznawanie nazw dla usług Azure, które są zainstalowane w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="fe402-164">To rozwiązanie nazwa wbudowanego umożliwia toohello tooconnect HDInsight następujące zasoby przy użyciu w pełni kwalifikowaną nazwą domeny (FQDN):</span><span class="sxs-lookup"><span data-stu-id="fe402-164">This built-in name resolution allows HDInsight tooconnect toohello following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="fe402-165">Dowolnego zasobu, który jest dostępny w hello internet.</span><span class="sxs-lookup"><span data-stu-id="fe402-165">Any resource that is available on hello internet.</span></span> <span data-ttu-id="fe402-166">Na przykład microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="fe402-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="fe402-167">Dowolnego zasobu, który jest w hello tej samej sieci wirtualnej Azure, używając hello __wewnętrzna nazwa DNS__ hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="fe402-167">Any resource that is in hello same Azure Virtual Network, by using hello __internal DNS name__ of hello resource.</span></span> <span data-ttu-id="fe402-168">Na przykład podczas rozpoznawania nazwy domyślnej hello hello poniżej przedstawiono przykład wewnętrzny DNS nazwy przypisanej tooHDInsight węzłów procesu roboczego:</span><span class="sxs-lookup"><span data-stu-id="fe402-168">For example, when using hello default name resolution, hello following are example internal DNS names assigned tooHDInsight worker nodes:</span></span>

    * <span data-ttu-id="fe402-169">wn0 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="fe402-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="fe402-170">wn2 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="fe402-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="fe402-171">Oba te węzły mogą komunikować się bezpośrednio ze sobą oraz inne węzły w usłudze HDInsight, za pomocą wewnętrznej nazwy DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="fe402-172">rozpoznawanie nazw domyślne Hello jest __nie__ Zezwalaj HDInsight tooresolve hello nazw zasobów w sieci, które są przyłączone do toohello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-172">hello default name resolution does __not__ allow HDInsight tooresolve hello names of resources in networks that are joined toohello virtual network.</span></span> <span data-ttu-id="fe402-173">Na przykład jest typowe toojoin toohello sieci wirtualnej sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-173">For example, it is common toojoin your on-premises network toohello virtual network.</span></span> <span data-ttu-id="fe402-174">Z tylko hello domyślne rozpoznawania nazw HDInsight nie może uzyskiwać dostęp do zasobów w sieci lokalnej hello według nazwy.</span><span class="sxs-lookup"><span data-stu-id="fe402-174">With only hello default name resolution, HDInsight cannot access resources in hello on-premises network by name.</span></span> <span data-ttu-id="fe402-175">Witaj przeciwną również ma wartość true, zasobów w sieci lokalnej nie może uzyskać dostęp do zasobów w sieci wirtualnej hello według nazwy.</span><span class="sxs-lookup"><span data-stu-id="fe402-175">hello opposite is also true, resources in your on-premises network cannot access resources in hello virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="fe402-176">Należy utworzyć hello niestandardowy serwer DNS i skonfigurować toouse sieci wirtualnej hello hello go przed utworzeniem klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe402-176">You must create hello custom DNS server and configure hello virtual network toouse it before creating hello HDInsight cluster.</span></span>

<span data-ttu-id="fe402-177">rozpoznawanie nazw tooenable między zasobami w przyłączone do sieci i hello sieci wirtualnej, należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="fe402-177">tooenable name resolution between hello virtual network and resources in joined networks, you must perform hello following actions:</span></span>

1. <span data-ttu-id="fe402-178">Utwórz niestandardowy serwer DNS w sieci wirtualnej platformy Azure, w którym planujesz tooinstall HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-178">Create a custom DNS server in hello Azure Virtual Network where you plan tooinstall HDInsight.</span></span>

2. <span data-ttu-id="fe402-179">Skonfiguruj hello sieci wirtualnej toouse hello niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-179">Configure hello virtual network toouse hello custom DNS server.</span></span>

3. <span data-ttu-id="fe402-180">Znajdź hello Azure przypisać sufiksu DNS dla sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-180">Find hello Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="fe402-181">Ta wartość jest zbyt podobne`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="fe402-181">This value is similar too`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="fe402-182">Aby uzyskać informacje o hello sufiks DNS, zobacz hello [przykład: niestandardowe DNS](#example-dns) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-182">For information on finding hello DNS suffix, see hello [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="fe402-183">Konfiguruj przekazywanie między serwerami DNS hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-183">Configure forwarding between hello DNS servers.</span></span> <span data-ttu-id="fe402-184">Konfiguracja Hello zależy od typu hello sieci zdalnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-184">hello configuration depends on hello type of remote network.</span></span>

    * <span data-ttu-id="fe402-185">W przypadku sieci zdalnej hello sieci lokalnej, konfigurowanie systemu DNS w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fe402-185">If hello remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="fe402-186">__Niestandardowe DNS__ (w sieci wirtualnej hello):</span><span class="sxs-lookup"><span data-stu-id="fe402-186">__Custom DNS__ (in hello virtual network):</span></span>

            * <span data-ttu-id="fe402-187">Przesyłania żądań dla sufiksu DNS hello hello sieci wirtualnej toohello Azure cyklicznego programu rozpoznawania nazw (168.63.129.16).</span><span class="sxs-lookup"><span data-stu-id="fe402-187">Forward requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="fe402-188">Azure obsługuje żądania zasobów w sieci wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="fe402-188">Azure handles requests for resources in hello virtual network</span></span>

            * <span data-ttu-id="fe402-189">Przekazuj wszystkie inne żądania toohello lokalnego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-189">Forward all other requests toohello on-premises DNS server.</span></span> <span data-ttu-id="fe402-190">Witaj w lokalnym DNS obsługuje wszystkie inne żądania dotyczące rozpoznawania nazw, nawet żądania zasobów internetowych, takich jak Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="fe402-190">hello on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="fe402-191">__DNS lokalnymi__: przekazywania żądań hello sieci wirtualnej sufiks toohello niestandardowe DNS serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-191">__On-premises DNS__: Forward requests for hello virtual network DNS suffix toohello custom DNS server.</span></span> <span data-ttu-id="fe402-192">Witaj niestandardowy serwer DNS przekazuje następnie toohello Azure cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="fe402-192">hello custom DNS server then forwards toohello Azure recursive resolver.</span></span>

        <span data-ttu-id="fe402-193">Tej konfiguracji żądania trasy dla w pełni kwalifikowana nazwy domeny, które zawierają hello sufiks DNS hello sieci wirtualnej toohello niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-193">This configuration routes requests for fully qualified domain names that contain hello DNS suffix of hello virtual network toohello custom DNS server.</span></span> <span data-ttu-id="fe402-194">Wszystkie żądania (nawet w przypadku publicznych adresów internetowych) są obsługiwane przez serwer DNS lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="fe402-194">All other requests (even for public internet addresses) are handled by hello on-premises DNS server.</span></span>

    * <span data-ttu-id="fe402-195">W przypadku sieci zdalnej hello innej sieci wirtualnej platformy Azure, konfigurowanie systemu DNS w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fe402-195">If hello remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="fe402-196">__Niestandardowe DNS__ (w każdej sieci wirtualnej):</span><span class="sxs-lookup"><span data-stu-id="fe402-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="fe402-197">Żądania dla sufiksu DNS hello hello sieci wirtualnych są przesyłane dalej toohello niestandardowych serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-197">Requests for hello DNS suffix of hello virtual networks are forwarded toohello custom DNS servers.</span></span> <span data-ttu-id="fe402-198">Witaj DNS w każdej sieci wirtualnej jest odpowiedzialny za rozpoznawania zasobów w sieci.</span><span class="sxs-lookup"><span data-stu-id="fe402-198">hello DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="fe402-199">Przekazuj wszystkie inne żądania toohello Azure cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="fe402-199">Forward all other requests toohello Azure recursive resolver.</span></span> <span data-ttu-id="fe402-200">Witaj cyklicznego programu rozpoznawania nazw jest odpowiedzialny za rozwiązania lokalnego i zasobów w Internecie.</span><span class="sxs-lookup"><span data-stu-id="fe402-200">hello recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="fe402-201">powitania serwera DNS dla każdej sieci przekazuje żądania toohello innych, oparte na sufiks DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-201">hello DNS server for each network forwards requests toohello other, based on DNS suffix.</span></span> <span data-ttu-id="fe402-202">Inne żądania są rozpoznawane przy użyciu hello Azure cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="fe402-202">Other requests are resolved using hello Azure recursive resolver.</span></span>

    <span data-ttu-id="fe402-203">Na przykład każdej konfiguracji zobacz hello [przykład: niestandardowe DNS](#example-dns) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-203">For an example of each configuration, see hello [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="fe402-204">Aby uzyskać więcej informacji, zobacz hello [rozpoznawanie nazwy dla maszyn wirtualnych i wystąpień roli](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-204">For more information, see hello [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-toohadoop-services"></a><span data-ttu-id="fe402-205">Bezpośrednie połączenie usługi tooHadoop</span><span class="sxs-lookup"><span data-stu-id="fe402-205">Directly connect tooHadoop services</span></span>

<span data-ttu-id="fe402-206">Większość dokumentacji w usłudze HDInsight założono, że klaster toohello dostęp za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="fe402-206">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="fe402-207">Na przykład, że możesz połączyć https://CLUSTERNAME.azurehdinsight.net toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="fe402-207">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="fe402-208">Ten adres używa hello publicznego bramy, która nie jest dostępna, jeśli używasz grup NSG lub Udr toorestrict dostęp z hello internet.</span><span class="sxs-lookup"><span data-stu-id="fe402-208">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="fe402-209">tooconnect tooAmbari i stron sieci web za pośrednictwem hello sieci wirtualnej, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="fe402-209">tooconnect tooAmbari and other web pages through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="fe402-210">toodiscover hello wewnętrzny pełni kwalifikowanych nazw domen (FQDN) węzły klastra usługi HDInsight hello, użyj jednej z hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="fe402-210">toodiscover hello internal fully qualified domain names (FQDN) of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

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

    <span data-ttu-id="fe402-211">Liście hello węzłów zwrócił Znajdź hello nazwy FQDN dla hello węzłów głównych i użyj hello nazw FQDN tooconnect tooAmbari i innych usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="fe402-211">In hello list of nodes returned, find hello FQDN for hello head nodes and use hello FQDNs tooconnect tooAmbari and other web services.</span></span> <span data-ttu-id="fe402-212">Na przykład użyć `http://<headnode-fqdn>:8080` tooaccess Ambari.</span><span class="sxs-lookup"><span data-stu-id="fe402-212">For example, use `http://<headnode-fqdn>:8080` tooaccess Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fe402-213">Niektórych usług hostowanych na węzłach głównych hello są tylko aktywne na jednym węźle naraz.</span><span class="sxs-lookup"><span data-stu-id="fe402-213">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="fe402-214">Jeśli spróbujesz uzyskiwanie dostępu do usługi na jednym węźle głównym i zwraca błąd 404, Przełącz toohello innych węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="fe402-214">If you try accessing a service on one head node and it returns a 404 error, switch toohello other head node.</span></span>

2. <span data-ttu-id="fe402-215">węzeł hello toodetermine i port, który usługa jest dostępna, zobacz hello [porty używane przez usługi Hadoop w usłudze HDInsight](./hdinsight-hadoop-port-settings-for-services.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-215">toodetermine hello node and port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="fe402-216"><a id="networktraffic"></a>Kontrolowanie ruchu w sieci</span><span class="sxs-lookup"><span data-stu-id="fe402-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="fe402-217">Ruch sieciowy w sieciach wirtualnych platformy Azure mogą być kontrolowane za pomocą hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="fe402-217">Network traffic in an Azure Virtual Networks can be controlled using hello following methods:</span></span>

* <span data-ttu-id="fe402-218">**Sieciowe grupy zabezpieczeń** (NSG) pozwalają toofilter ruchu przychodzącego i wychodzącego toohello sieci.</span><span class="sxs-lookup"><span data-stu-id="fe402-218">**Network security groups** (NSG) allow you toofilter inbound and outbound traffic toohello network.</span></span> <span data-ttu-id="fe402-219">Aby uzyskać więcej informacji, zobacz hello [filtrowania ruchu sieciowego z grup zabezpieczeń sieci](../virtual-network/virtual-networks-nsg.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-219">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="fe402-220">HDInsight nie obsługuje ograniczenia ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="fe402-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="fe402-221">**Trasy zdefiniowane przez użytkownika** (przez) zdefiniuj, jak przepływa ruch między zasobami w sieci hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-221">**User-defined routes** (UDR) define how traffic flows between resources in hello network.</span></span> <span data-ttu-id="fe402-222">Aby uzyskać więcej informacji, zobacz hello [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../virtual-network/virtual-networks-udr-overview.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-222">For more information, see hello [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="fe402-223">**Sieci wirtualnych urządzeń** replikować hello funkcjonalność urządzeń, takich jak routery i zapory.</span><span class="sxs-lookup"><span data-stu-id="fe402-223">**Network virtual appliances** replicate hello functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="fe402-224">Aby uzyskać więcej informacji, zobacz hello [urządzenia sieciowe](https://azure.microsoft.com/solutions/network-appliances) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-224">For more information, see hello [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="fe402-225">Jako usługa zarządzana HDInsight wymaga nieograniczony dostęp do usług kondycji i zarządzania tooAzure w hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="fe402-225">As a managed service, HDInsight requires unrestricted access tooAzure health and management services in hello Azure cloud.</span></span> <span data-ttu-id="fe402-226">Przy użyciu grup NSG i Udr, należy się upewnić, że HDInsight tych usług można nadal komunikować się z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe402-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="fe402-227">HDInsight udostępnia usługi na kilku portów.</span><span class="sxs-lookup"><span data-stu-id="fe402-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="fe402-228">Używając urządzenie wirtualne zapory, musisz zezwolić na ruch na powitania porty używane w przypadku tych usług.</span><span class="sxs-lookup"><span data-stu-id="fe402-228">When using a virtual appliance firewall, you must allow traffic on hello ports used for these services.</span></span> <span data-ttu-id="fe402-229">Aby uzyskać więcej informacji zobacz sekcję hello [wymagane porty].</span><span class="sxs-lookup"><span data-stu-id="fe402-229">For more information, see hello [Required ports] section.</span></span>

### <span data-ttu-id="fe402-230"><a id="hdinsight-ip"></a>HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe402-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="fe402-231">Jeśli planujesz używanie **sieciowej grupy zabezpieczeń** lub **trasy zdefiniowane przez użytkownika** toocontrol ruch sieciowy, wykonaj następujące akcje przed zainstalowaniem usługi HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="fe402-231">If you plan on using **network security groups** or **user-defined routes** toocontrol network traffic, perform hello following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="fe402-232">Zidentyfikuj hello planowanie toouse HDInsight region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe402-232">Identify hello Azure region that you plan toouse for HDInsight.</span></span>

2. <span data-ttu-id="fe402-233">Określ adresy IP hello wymagane przez HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe402-233">Identify hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="fe402-234">Aby uzyskać więcej informacji, zobacz hello [adresy IP wymagane przez HDInsight](#hdinsight-ip) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-234">For more information, see hello [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="fe402-235">Tworzenie lub modyfikowanie grup zabezpieczeń sieci hello lub zdefiniowanej przez użytkownika tras dla podsieci hello zaplanowanie tooinstall HDInsight do.</span><span class="sxs-lookup"><span data-stu-id="fe402-235">Create or modify hello network security groups or user-defined routes for hello subnet that you plan tooinstall HDInsight into.</span></span>

    * <span data-ttu-id="fe402-236">__Sieciowe grupy zabezpieczeń__: Zezwalaj na __przychodzących__ ruch na porcie __443__ z hello adresów IP.</span><span class="sxs-lookup"><span data-stu-id="fe402-236">__Network security groups__: allow __inbound__ traffic on port __443__ from hello IP addresses.</span></span>
    * <span data-ttu-id="fe402-237">__Trasy zdefiniowane przez użytkownika__: Utwórz adres IP tooeach trasy i ustaw hello __następnego przeskoku typu__ too__Internet__.</span><span class="sxs-lookup"><span data-stu-id="fe402-237">__User-defined routes__: create a route tooeach IP address and set hello __Next hop type__ too__Internet__.</span></span>

<span data-ttu-id="fe402-238">Aby uzyskać więcej informacji na sieciowych grup zabezpieczeń lub trasy zdefiniowane przez użytkownika Zobacz hello następującej dokumentacji:</span><span class="sxs-lookup"><span data-stu-id="fe402-238">For more information on network security groups or user-defined routes, see hello following documentation:</span></span>

* [<span data-ttu-id="fe402-239">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="fe402-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="fe402-240">Trasy zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe402-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="fe402-241">Wymuszone tunelowanie</span><span class="sxs-lookup"><span data-stu-id="fe402-241">Forced tunneling</span></span>

<span data-ttu-id="fe402-242">Wymuszanie tunelowania jest zdefiniowane przez użytkownika konfiguracji routingu, gdzie cały ruch z podsieci jest wymuszone tooa określonej sieci lub lokalizacji, takiej jak sieć lokalną.</span><span class="sxs-lookup"><span data-stu-id="fe402-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced tooa specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="fe402-243">HDInsight jest __nie__ obsługi wymuszonego tunelowania.</span><span class="sxs-lookup"><span data-stu-id="fe402-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="fe402-244"><a id="hdinsight-ip"></a>Wymaganych adresów IP</span><span class="sxs-lookup"><span data-stu-id="fe402-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe402-245">Witaj kondycji Azure i usługi zarządzania musi być w stanie toocommunicate z usługą HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe402-245">hello Azure health and management services must be able toocommunicate with HDInsight.</span></span> <span data-ttu-id="fe402-246">Jeśli używasz grup zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, zezwalać na ruch z hello adresów IP dla tych tooreach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe402-246">If you use network security groups or user-defined routes, allow traffic from hello IP addresses for these services tooreach HDInsight.</span></span>
>
> <span data-ttu-id="fe402-247">Jeśli nie używasz ruch toocontrol trasy zdefiniowane przez użytkownika i grupy zabezpieczeń sieci, można zignorować w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-247">If you do not use network security groups or user-defined routes toocontrol traffic, you can ignore this section.</span></span>

<span data-ttu-id="fe402-248">Jeśli używasz grup zabezpieczeń sieci lub trasy zdefiniowane przez użytkownika, musisz zezwolić na ruch z hello Azure kondycji i zarządzania tooreach usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe402-248">If you use network security groups or user-defined routes, you must allow traffic from hello Azure health and management services tooreach HDInsight.</span></span> <span data-ttu-id="fe402-249">Użyj hello następujące adresy IP hello toofind kroki, które może:</span><span class="sxs-lookup"><span data-stu-id="fe402-249">Use hello following steps toofind hello IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="fe402-250">Zawsze musi zezwalać na ruch z hello następujących adresów IP:</span><span class="sxs-lookup"><span data-stu-id="fe402-250">You must always allow traffic from hello following IP addresses:</span></span>

    | <span data-ttu-id="fe402-251">Adres IP</span><span class="sxs-lookup"><span data-stu-id="fe402-251">IP address</span></span> | <span data-ttu-id="fe402-252">Port dozwolone</span><span class="sxs-lookup"><span data-stu-id="fe402-252">Allowed port</span></span> | <span data-ttu-id="fe402-253">Kierunek</span><span class="sxs-lookup"><span data-stu-id="fe402-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="fe402-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="fe402-254">168.61.49.99</span></span> | <span data-ttu-id="fe402-255">443</span><span class="sxs-lookup"><span data-stu-id="fe402-255">443</span></span> | <span data-ttu-id="fe402-256">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-256">Inbound</span></span> |
    | <span data-ttu-id="fe402-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="fe402-257">23.99.5.239</span></span> | <span data-ttu-id="fe402-258">443</span><span class="sxs-lookup"><span data-stu-id="fe402-258">443</span></span> | <span data-ttu-id="fe402-259">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-259">Inbound</span></span> |
    | <span data-ttu-id="fe402-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="fe402-260">168.61.48.131</span></span> | <span data-ttu-id="fe402-261">443</span><span class="sxs-lookup"><span data-stu-id="fe402-261">443</span></span> | <span data-ttu-id="fe402-262">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-262">Inbound</span></span> |
    | <span data-ttu-id="fe402-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="fe402-263">138.91.141.162</span></span> | <span data-ttu-id="fe402-264">443</span><span class="sxs-lookup"><span data-stu-id="fe402-264">443</span></span> | <span data-ttu-id="fe402-265">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-265">Inbound</span></span> |

2. <span data-ttu-id="fe402-266">W przypadku klastra HDInsight w jednym z następujących regionach hello, następnie należy zezwolić na ruch z hello adresów IP dla regionu hello:</span><span class="sxs-lookup"><span data-stu-id="fe402-266">If your HDInsight cluster is in one of hello following regions, then you must allow traffic from hello IP addresses listed for hello region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fe402-267">Jeśli hello region platformy Azure, którego używasz, nie jest wyświetlana, następnie używać tylko hello cztery adresów IP z kroku 1.</span><span class="sxs-lookup"><span data-stu-id="fe402-267">If hello Azure region you are using is not listed, then only use hello four IP addresses from step 1.</span></span>

    | <span data-ttu-id="fe402-268">Kraj</span><span class="sxs-lookup"><span data-stu-id="fe402-268">Country</span></span> | <span data-ttu-id="fe402-269">Region</span><span class="sxs-lookup"><span data-stu-id="fe402-269">Region</span></span> | <span data-ttu-id="fe402-270">Dozwolonych adresów IP</span><span class="sxs-lookup"><span data-stu-id="fe402-270">Allowed IP addresses</span></span> | <span data-ttu-id="fe402-271">Port dozwolone</span><span class="sxs-lookup"><span data-stu-id="fe402-271">Allowed port</span></span> | <span data-ttu-id="fe402-272">Kierunek</span><span class="sxs-lookup"><span data-stu-id="fe402-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="fe402-273">Azja</span><span class="sxs-lookup"><span data-stu-id="fe402-273">Asia</span></span> | <span data-ttu-id="fe402-274">Azja Wschodnia</span><span class="sxs-lookup"><span data-stu-id="fe402-274">East Asia</span></span> | <span data-ttu-id="fe402-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="fe402-275">23.102.235.122</span></span></br><span data-ttu-id="fe402-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="fe402-276">52.175.38.134</span></span> | <span data-ttu-id="fe402-277">443</span><span class="sxs-lookup"><span data-stu-id="fe402-277">443</span></span> | <span data-ttu-id="fe402-278">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-279">Azja Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="fe402-279">Southeast Asia</span></span> | <span data-ttu-id="fe402-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="fe402-280">13.76.245.160</span></span></br><span data-ttu-id="fe402-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="fe402-281">13.76.136.249</span></span> | <span data-ttu-id="fe402-282">443</span><span class="sxs-lookup"><span data-stu-id="fe402-282">443</span></span> | <span data-ttu-id="fe402-283">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-283">Inbound</span></span> |
    | <span data-ttu-id="fe402-284">Australia</span><span class="sxs-lookup"><span data-stu-id="fe402-284">Australia</span></span> | <span data-ttu-id="fe402-285">Australia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="fe402-285">Australia East</span></span> | <span data-ttu-id="fe402-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="fe402-286">104.210.84.115</span></span></br><span data-ttu-id="fe402-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="fe402-287">13.75.152.195</span></span> | <span data-ttu-id="fe402-288">443</span><span class="sxs-lookup"><span data-stu-id="fe402-288">443</span></span> | <span data-ttu-id="fe402-289">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-290">Australia Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="fe402-290">Australia Southeast</span></span> | <span data-ttu-id="fe402-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="fe402-291">13.77.2.56</span></span></br><span data-ttu-id="fe402-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="fe402-292">13.77.2.94</span></span> | <span data-ttu-id="fe402-293">443</span><span class="sxs-lookup"><span data-stu-id="fe402-293">443</span></span> | <span data-ttu-id="fe402-294">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-294">Inbound</span></span> |
    | <span data-ttu-id="fe402-295">Brazylia</span><span class="sxs-lookup"><span data-stu-id="fe402-295">Brazil</span></span> | <span data-ttu-id="fe402-296">Brazylia Południowa</span><span class="sxs-lookup"><span data-stu-id="fe402-296">Brazil South</span></span> | <span data-ttu-id="fe402-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="fe402-297">191.235.84.104</span></span></br><span data-ttu-id="fe402-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="fe402-298">191.235.87.113</span></span> | <span data-ttu-id="fe402-299">443</span><span class="sxs-lookup"><span data-stu-id="fe402-299">443</span></span> | <span data-ttu-id="fe402-300">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-300">Inbound</span></span> |
    | <span data-ttu-id="fe402-301">Kanada</span><span class="sxs-lookup"><span data-stu-id="fe402-301">Canada</span></span> | <span data-ttu-id="fe402-302">Kanada Wschodnia</span><span class="sxs-lookup"><span data-stu-id="fe402-302">Canada East</span></span> | <span data-ttu-id="fe402-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="fe402-303">52.229.127.96</span></span></br><span data-ttu-id="fe402-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="fe402-304">52.229.123.172</span></span> | <span data-ttu-id="fe402-305">443</span><span class="sxs-lookup"><span data-stu-id="fe402-305">443</span></span> | <span data-ttu-id="fe402-306">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-307">Kanada Środkowa</span><span class="sxs-lookup"><span data-stu-id="fe402-307">Canada Central</span></span> | <span data-ttu-id="fe402-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="fe402-308">52.228.37.66</span></span></br><span data-ttu-id="fe402-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="fe402-309">52.228.45.222</span></span> | <span data-ttu-id="fe402-310">443</span><span class="sxs-lookup"><span data-stu-id="fe402-310">443</span></span> | <span data-ttu-id="fe402-311">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-311">Inbound</span></span> |
    | <span data-ttu-id="fe402-312">Chiny</span><span class="sxs-lookup"><span data-stu-id="fe402-312">China</span></span> | <span data-ttu-id="fe402-313">Chiny Północne</span><span class="sxs-lookup"><span data-stu-id="fe402-313">China North</span></span> | <span data-ttu-id="fe402-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="fe402-314">42.159.96.170</span></span></br><span data-ttu-id="fe402-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="fe402-315">139.217.2.219</span></span> | <span data-ttu-id="fe402-316">443</span><span class="sxs-lookup"><span data-stu-id="fe402-316">443</span></span> | <span data-ttu-id="fe402-317">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-318">Chiny Wschodnie</span><span class="sxs-lookup"><span data-stu-id="fe402-318">China East</span></span> | <span data-ttu-id="fe402-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="fe402-319">42.159.198.178</span></span></br><span data-ttu-id="fe402-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="fe402-320">42.159.234.157</span></span> | <span data-ttu-id="fe402-321">443</span><span class="sxs-lookup"><span data-stu-id="fe402-321">443</span></span> | <span data-ttu-id="fe402-322">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-322">Inbound</span></span> |
    | <span data-ttu-id="fe402-323">Europa</span><span class="sxs-lookup"><span data-stu-id="fe402-323">Europe</span></span> | <span data-ttu-id="fe402-324">Europa Północna</span><span class="sxs-lookup"><span data-stu-id="fe402-324">North Europe</span></span> | <span data-ttu-id="fe402-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="fe402-325">52.164.210.96</span></span></br><span data-ttu-id="fe402-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="fe402-326">13.74.153.132</span></span> | <span data-ttu-id="fe402-327">443</span><span class="sxs-lookup"><span data-stu-id="fe402-327">443</span></span> | <span data-ttu-id="fe402-328">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-329">Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="fe402-329">West Europe</span></span>| <span data-ttu-id="fe402-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="fe402-330">52.166.243.90</span></span></br><span data-ttu-id="fe402-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="fe402-331">52.174.36.244</span></span> | <span data-ttu-id="fe402-332">443</span><span class="sxs-lookup"><span data-stu-id="fe402-332">443</span></span> | <span data-ttu-id="fe402-333">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-333">Inbound</span></span> |
    | <span data-ttu-id="fe402-334">Niemcy</span><span class="sxs-lookup"><span data-stu-id="fe402-334">Germany</span></span> | <span data-ttu-id="fe402-335">Niemcy Środkowe</span><span class="sxs-lookup"><span data-stu-id="fe402-335">Germany Central</span></span> | <span data-ttu-id="fe402-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="fe402-336">51.4.146.68</span></span></br><span data-ttu-id="fe402-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="fe402-337">51.4.146.80</span></span> | <span data-ttu-id="fe402-338">443</span><span class="sxs-lookup"><span data-stu-id="fe402-338">443</span></span> | <span data-ttu-id="fe402-339">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-340">Niemcy Północno-Wschodnie</span><span class="sxs-lookup"><span data-stu-id="fe402-340">Germany Northeast</span></span> | <span data-ttu-id="fe402-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="fe402-341">51.5.150.132</span></span></br><span data-ttu-id="fe402-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="fe402-342">51.5.144.101</span></span> | <span data-ttu-id="fe402-343">443</span><span class="sxs-lookup"><span data-stu-id="fe402-343">443</span></span> | <span data-ttu-id="fe402-344">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-344">Inbound</span></span> |
    | <span data-ttu-id="fe402-345">Indie</span><span class="sxs-lookup"><span data-stu-id="fe402-345">India</span></span> | <span data-ttu-id="fe402-346">Indie Środkowe</span><span class="sxs-lookup"><span data-stu-id="fe402-346">Central India</span></span> | <span data-ttu-id="fe402-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="fe402-347">52.172.153.209</span></span></br><span data-ttu-id="fe402-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="fe402-348">52.172.152.49</span></span> | <span data-ttu-id="fe402-349">443</span><span class="sxs-lookup"><span data-stu-id="fe402-349">443</span></span> | <span data-ttu-id="fe402-350">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-350">Inbound</span></span> |
    | <span data-ttu-id="fe402-351">Japonia</span><span class="sxs-lookup"><span data-stu-id="fe402-351">Japan</span></span> | <span data-ttu-id="fe402-352">Japonia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="fe402-352">Japan East</span></span> | <span data-ttu-id="fe402-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="fe402-353">13.78.125.90</span></span></br><span data-ttu-id="fe402-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="fe402-354">13.78.89.60</span></span> | <span data-ttu-id="fe402-355">443</span><span class="sxs-lookup"><span data-stu-id="fe402-355">443</span></span> | <span data-ttu-id="fe402-356">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-357">Japonia Zachodnia</span><span class="sxs-lookup"><span data-stu-id="fe402-357">Japan West</span></span> | <span data-ttu-id="fe402-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="fe402-358">40.74.125.69</span></span></br><span data-ttu-id="fe402-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="fe402-359">138.91.29.150</span></span> | <span data-ttu-id="fe402-360">443</span><span class="sxs-lookup"><span data-stu-id="fe402-360">443</span></span> | <span data-ttu-id="fe402-361">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-361">Inbound</span></span> |
    | <span data-ttu-id="fe402-362">Korea</span><span class="sxs-lookup"><span data-stu-id="fe402-362">Korea</span></span> | <span data-ttu-id="fe402-363">Korea Środkowa</span><span class="sxs-lookup"><span data-stu-id="fe402-363">Korea Central</span></span> | <span data-ttu-id="fe402-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="fe402-364">52.231.39.142</span></span></br><span data-ttu-id="fe402-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="fe402-365">52.231.36.209</span></span> | <span data-ttu-id="fe402-366">433</span><span class="sxs-lookup"><span data-stu-id="fe402-366">433</span></span> | <span data-ttu-id="fe402-367">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-368">Korea Południowa</span><span class="sxs-lookup"><span data-stu-id="fe402-368">Korea South</span></span> | <span data-ttu-id="fe402-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="fe402-369">52.231.203.16</span></span></br><span data-ttu-id="fe402-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="fe402-370">52.231.205.214</span></span> | <span data-ttu-id="fe402-371">443</span><span class="sxs-lookup"><span data-stu-id="fe402-371">443</span></span> | <span data-ttu-id="fe402-372">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-372">Inbound</span></span>
    | <span data-ttu-id="fe402-373">Wielka Brytania</span><span class="sxs-lookup"><span data-stu-id="fe402-373">United Kingdom</span></span> | <span data-ttu-id="fe402-374">Zachodnie Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="fe402-374">UK West</span></span> | <span data-ttu-id="fe402-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="fe402-375">51.141.13.110</span></span></br><span data-ttu-id="fe402-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="fe402-376">51.141.7.20</span></span> | <span data-ttu-id="fe402-377">443</span><span class="sxs-lookup"><span data-stu-id="fe402-377">443</span></span> | <span data-ttu-id="fe402-378">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-379">Południowe Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="fe402-379">UK South</span></span> | <span data-ttu-id="fe402-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="fe402-380">51.140.47.39</span></span></br><span data-ttu-id="fe402-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="fe402-381">51.140.52.16</span></span> | <span data-ttu-id="fe402-382">443</span><span class="sxs-lookup"><span data-stu-id="fe402-382">443</span></span> | <span data-ttu-id="fe402-383">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-383">Inbound</span></span> |
    | <span data-ttu-id="fe402-384">Stany Zjednoczone</span><span class="sxs-lookup"><span data-stu-id="fe402-384">United States</span></span> | <span data-ttu-id="fe402-385">Środkowe stany USA</span><span class="sxs-lookup"><span data-stu-id="fe402-385">Central US</span></span> | <span data-ttu-id="fe402-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="fe402-386">13.67.223.215</span></span></br><span data-ttu-id="fe402-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="fe402-387">40.86.83.253</span></span> | <span data-ttu-id="fe402-388">443</span><span class="sxs-lookup"><span data-stu-id="fe402-388">443</span></span> | <span data-ttu-id="fe402-389">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-390">Środkowo-północne stany USA</span><span class="sxs-lookup"><span data-stu-id="fe402-390">North Central US</span></span> | <span data-ttu-id="fe402-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="fe402-391">157.56.8.38</span></span></br><span data-ttu-id="fe402-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="fe402-392">157.55.213.99</span></span> | <span data-ttu-id="fe402-393">443</span><span class="sxs-lookup"><span data-stu-id="fe402-393">443</span></span> | <span data-ttu-id="fe402-394">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-395">Środkowo-zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="fe402-395">West Central US</span></span> | <span data-ttu-id="fe402-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="fe402-396">52.161.23.15</span></span></br><span data-ttu-id="fe402-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="fe402-397">52.161.10.167</span></span> | <span data-ttu-id="fe402-398">443</span><span class="sxs-lookup"><span data-stu-id="fe402-398">443</span></span> | <span data-ttu-id="fe402-399">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="fe402-400">Zachodnie stany USA 2</span><span class="sxs-lookup"><span data-stu-id="fe402-400">West US 2</span></span> | <span data-ttu-id="fe402-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="fe402-401">52.175.211.210</span></span></br><span data-ttu-id="fe402-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="fe402-402">52.175.222.222</span></span> | <span data-ttu-id="fe402-403">443</span><span class="sxs-lookup"><span data-stu-id="fe402-403">443</span></span> | <span data-ttu-id="fe402-404">Przychodzący</span><span class="sxs-lookup"><span data-stu-id="fe402-404">Inbound</span></span> |

    <span data-ttu-id="fe402-405">Dla informacji na temat hello IP dotyczy toouse systemu Azure dla instytucji rządowych, zobacz hello [Azure dla instytucji rządowych analizy i analiza](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-405">For information on hello IP addresses toouse for Azure Government, see hello [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="fe402-406">Jeśli używasz niestandardowego serwera DNS z sieci wirtualnej, należy także zezwolić na dostęp z __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="fe402-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="fe402-407">Ten adres jest platformy Azure, cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="fe402-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="fe402-408">Aby uzyskać więcej informacji, zobacz hello [rozpoznawanie nazw dla maszyn wirtualnych i roli wystąpień](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-408">For more information, see hello [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="fe402-409">Aby uzyskać więcej informacji, zobacz hello [kontrolowanie ruchu w sieci](#networktraffic) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-409">For more information, see hello [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="fe402-410"><a id="hdinsight-ports"></a>Wymagane porty</span><span class="sxs-lookup"><span data-stu-id="fe402-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="fe402-411">Jeśli planowane jest użycie sieci **urządzenie wirtualne zapory** toosecure hello sieci wirtualnej, a użytkownik musi zezwolić na ruch wychodzący na powitania następujące porty:</span><span class="sxs-lookup"><span data-stu-id="fe402-411">If you plan on using a network **virtual appliance firewall** toosecure hello virtual network, you must allow outbound traffic on hello following ports:</span></span>

* <span data-ttu-id="fe402-412">53</span><span class="sxs-lookup"><span data-stu-id="fe402-412">53</span></span>
* <span data-ttu-id="fe402-413">443</span><span class="sxs-lookup"><span data-stu-id="fe402-413">443</span></span>
* <span data-ttu-id="fe402-414">1433</span><span class="sxs-lookup"><span data-stu-id="fe402-414">1433</span></span>
* <span data-ttu-id="fe402-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="fe402-415">11000-11999</span></span>
* <span data-ttu-id="fe402-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="fe402-416">14000-14999</span></span>

<span data-ttu-id="fe402-417">Listę portów dla określonych usług, zobacz hello [porty używane przez usługi Hadoop w usłudze HDInsight](hdinsight-hadoop-port-settings-for-services.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-417">For a list of ports for specific services, see hello [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="fe402-418">Aby uzyskać więcej informacji na reguły zapory dla urządzenia wirtualnego, zobacz hello [scenariuszu urządzenie wirtualne](../virtual-network/virtual-network-scenario-udr-gw-nva.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="fe402-418">For more information on firewall rules for virtual appliances, see hello [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="fe402-419"><a id="hdinsight-nsg"></a>Przykład: sieciowych grup zabezpieczeń z usługą HDInsight</span><span class="sxs-lookup"><span data-stu-id="fe402-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="fe402-420">Przykłady Hello w tej sekcji pokazują, jak grupy zabezpieczeń sieci toocreate zasady umożliwiające toocommunicate HDInsight z hello usług zarządzania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe402-420">hello examples in this section demonstrate how toocreate network security group rules that allow HDInsight toocommunicate with hello Azure management services.</span></span> <span data-ttu-id="fe402-421">Przed użyciem przykłady hello, Dostosuj hello IP adresów toomatch hello widocznych dla hello region platformy Azure, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="fe402-421">Before using hello examples, adjust hello IP addresses toomatch hello ones for hello Azure region you are using.</span></span> <span data-ttu-id="fe402-422">Te informacje można znaleźć w hello [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-422">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="fe402-423">Szablonu zarządzania zasobami platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fe402-423">Azure Resource Management template</span></span>

<span data-ttu-id="fe402-424">Witaj następujące zarządzanie zasobami szablon tworzy sieć wirtualną, która ogranicza ruchu przychodzącego, ale zezwala na ruch sieciowy z adresów IP hello wymagane przez HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe402-424">hello following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="fe402-425">Ten szablon tworzy klaster usługi HDInsight w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-425">This template also creates an HDInsight cluster in hello virtual network.</span></span>

* [<span data-ttu-id="fe402-426">Wdrażanie zabezpieczonej sieci wirtualnej platformy Azure i klaster usługi HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="fe402-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="fe402-427">Zmień hello adresy IP używane w ten przykład toomatch hello region platformy Azure, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="fe402-427">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="fe402-428">Te informacje można znaleźć w hello [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-428">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="fe402-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe402-429">Azure PowerShell</span></span>

<span data-ttu-id="fe402-430">Użyj powitania po toocreate skrypt programu PowerShell siecią wirtualną, która ogranicza ruchu przychodzącego i zezwala na ruch z hello adresów IP dla regionu Europa Północna, Europa hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-430">Use hello following PowerShell script toocreate a virtual network that restricts inbound traffic and allows traffic from hello IP addresses for hello North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe402-431">Zmień hello adresy IP używane w ten przykład toomatch hello region platformy Azure, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="fe402-431">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="fe402-432">Te informacje można znaleźć w hello [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-432">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
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
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="fe402-433">W tym przykładzie pokazano, jak tooadd tooallow reguły ruchu przychodzącego ruchu sieciowego na adresach IP hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="fe402-433">This example demonstrates how tooadd rules tooallow inbound traffic on hello required IP addresses.</span></span> <span data-ttu-id="fe402-434">Nie zawiera toorestrict reguły ruchu przychodzącego dostęp z innych źródeł.</span><span class="sxs-lookup"><span data-stu-id="fe402-434">It does not contain a rule toorestrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="fe402-435">Witaj poniższy przykład przedstawia sposób tooenable SSH dostęp z Internetu hello:</span><span class="sxs-lookup"><span data-stu-id="fe402-435">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="fe402-436">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fe402-436">Azure CLI</span></span>

<span data-ttu-id="fe402-437">Użyj hello następujące kroki toocreate sieci wirtualnej, który ogranicza ruchu przychodzącego, ale zezwala na ruch sieciowy z adresów IP hello wymagane przez usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fe402-437">Use hello following steps toocreate a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="fe402-438">Witaj Użyj następującego polecenia toocreate nową sieciową grupę zabezpieczeń o nazwie `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="fe402-438">Use hello following command toocreate a new network security group named `hdisecure`.</span></span> <span data-ttu-id="fe402-439">Zastąp **RESOURCEGROUPNAME** z grupą zasobów hello zawierający hello sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe402-439">Replace **RESOURCEGROUPNAME** with hello resource group that contains hello Azure Virtual Network.</span></span> <span data-ttu-id="fe402-440">Zastąp **lokalizacji** hello lokalizacji (regionu) tej grupy hello został utworzony w.</span><span class="sxs-lookup"><span data-stu-id="fe402-440">Replace **LOCATION** with hello location (region) that hello group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="fe402-441">Po utworzeniu grupy hello otrzymasz informacji na temat hello nowej grupy.</span><span class="sxs-lookup"><span data-stu-id="fe402-441">Once hello group has been created, you receive information on hello new group.</span></span>

2. <span data-ttu-id="fe402-442">Użyj powitania po tooadd reguły toohello nową grupę zabezpieczeń sieci umożliwiająca komunikacji przychodzącej na porcie 443 z hello Azure HDInsight usługi kondycji i zarządzania.</span><span class="sxs-lookup"><span data-stu-id="fe402-442">Use hello following tooadd rules toohello new network security group that allow inbound communication on port 443 from hello Azure HDInsight health and management service.</span></span> <span data-ttu-id="fe402-443">Zastąp **RESOURCEGROUPNAME** o nazwie hello hello grupy zasobów, zawierającą hello sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fe402-443">Replace **RESOURCEGROUPNAME** with hello name of hello resource group that contains hello Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="fe402-444">Zmień hello adresy IP używane w ten przykład toomatch hello region platformy Azure, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="fe402-444">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="fe402-445">Te informacje można znaleźć w hello [HDInsight z grup zabezpieczeń sieci i trasy zdefiniowane przez użytkownika](#hdinsight-ip) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-445">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="fe402-446">tooretrieve hello Unikatowy identyfikator dla tej grupy zabezpieczeń sieci hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="fe402-446">tooretrieve hello unique identifier for this network security group, use hello following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="fe402-447">To polecenie zwraca wartość toohello podobne, następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="fe402-447">This command returns a value similar toohello following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="fe402-448">Użyj podwójnych cudzysłowów wokół identyfikatora w poleceniu hello, jeśli nie otrzymasz hello oczekiwano wyników.</span><span class="sxs-lookup"><span data-stu-id="fe402-448">Use double-quotes around id in hello command if you don't get hello expected results.</span></span>

4. <span data-ttu-id="fe402-449">Hello Użyj następującego polecenia tooapply hello zabezpieczeń grupy tooa podsieci.</span><span class="sxs-lookup"><span data-stu-id="fe402-449">Use hello following command tooapply hello network security group tooa subnet.</span></span> <span data-ttu-id="fe402-450">Zastąp hello __GUID__ i __RESOURCEGROUPNAME__ z hello te zwracane z hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="fe402-450">Replace hello __GUID__ and __RESOURCEGROUPNAME__ values with hello ones returned from hello previous step.</span></span> <span data-ttu-id="fe402-451">Zastąp __VNETNAME__ i __SUBNETNAME__ z hello wirtualnej nazwy sieciowej i nazwy podsieci, które mają toocreate.</span><span class="sxs-lookup"><span data-stu-id="fe402-451">Replace __VNETNAME__ and __SUBNETNAME__ with hello virtual network name and subnet name that you want toocreate.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="fe402-452">Po zakończeniu wykonywania tego polecenia można zainstalować usługi HDInsight na powitania sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-452">Once this command completes, you can install HDInsight into hello Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe402-453">Te czynności tylko otworzyć dostępu toohello HDInsight kondycji i zarządzania usługi na powitania chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="fe402-453">These steps only open access toohello HDInsight health and management service on hello Azure cloud.</span></span> <span data-ttu-id="fe402-454">Wszystkie inne dostępu toohello klastra usługi HDInsight z hello zewnętrznej sieci wirtualnej jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="fe402-454">Any other access toohello HDInsight cluster from outside hello Virtual Network is blocked.</span></span> <span data-ttu-id="fe402-455">tooenable dostępu z zewnętrznej sieci wirtualnej hello, należy dodać dodatkowych reguł sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="fe402-455">tooenable access from outside hello virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="fe402-456">Witaj poniższy przykład przedstawia sposób tooenable SSH dostęp z Internetu hello:</span><span class="sxs-lookup"><span data-stu-id="fe402-456">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="fe402-457"><a id="example-dns"></a>Przykład: Konfiguracji DNS</span><span class="sxs-lookup"><span data-stu-id="fe402-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="fe402-458">Rozpoznawanie nazw między sieci wirtualnej i sieci połączonych lokalnie</span><span class="sxs-lookup"><span data-stu-id="fe402-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="fe402-459">W tym przykładzie powoduje hello następujące założenia:</span><span class="sxs-lookup"><span data-stu-id="fe402-459">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="fe402-460">Masz sieć wirtualna Azure, która jest tooan połączone siecią lokalną przy użyciu bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="fe402-460">You have an Azure Virtual Network that is connected tooan on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="fe402-461">Hello niestandardowy serwer DNS w sieci wirtualnej hello działa jako system operacyjny hello Linux lub Unix.</span><span class="sxs-lookup"><span data-stu-id="fe402-461">hello custom DNS server in hello virtual network is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="fe402-462">[Powiąż](https://www.isc.org/downloads/bind/) jest zainstalowany na powitania niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-462">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS server.</span></span>

<span data-ttu-id="fe402-463">Na powitania niestandardowy serwer DNS w sieci wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="fe402-463">On hello custom DNS server in hello virtual network:</span></span>

1. <span data-ttu-id="fe402-464">Użyj programu Azure PowerShell lub interfejsu wiersza polecenia Azure toofind hello sufiksu DNS sieci wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="fe402-464">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of hello virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="fe402-465">Na powitania niestandardowy serwer DNS dla sieci wirtualnej hello, użyj następującego tekstu jako zawartość hello hello hello `/etc/bind/named.conf.local` pliku:</span><span class="sxs-lookup"><span data-stu-id="fe402-465">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="fe402-466">Zastąp hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` wartość sufiksu DNS hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-466">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="fe402-467">Ta konfiguracja kieruje wszystkie żądania sufiks DNS hello hello sieci wirtualnej toohello Azure cyklicznego programu rozpoznawania nazw DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-467">This configuration routes all DNS requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver.</span></span>

2. <span data-ttu-id="fe402-468">Na powitania niestandardowy serwer DNS dla sieci wirtualnej hello, użyj następującego tekstu jako zawartość hello hello hello `/etc/bind/named.conf.options` pliku:</span><span class="sxs-lookup"><span data-stu-id="fe402-468">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="fe402-469">Zastąp hello `10.0.0.0/16` wartość z zakresu adresów IP hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-469">Replace hello `10.0.0.0/16` value with hello IP address range of your virtual network.</span></span> <span data-ttu-id="fe402-470">Ten wpis umożliwia adresy żądań rozpoznawania nazw w tym zakresie.</span><span class="sxs-lookup"><span data-stu-id="fe402-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="fe402-471">Dodaj zakres adresów IP hello toohello sieci lokalne powitania `acl goodclients { ... }` sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe402-471">Add hello IP address range of hello on-premises network toohello `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="fe402-472">Wpis umożliwia żądań rozpoznawania nazw z zasobów w sieci lokalnej hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-472">entry allows name resolution requests from resources in hello on-premises network.</span></span>
    
    * <span data-ttu-id="fe402-473">Zastąp wartość hello `192.168.0.1` o adresie IP hello lokalnego serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-473">Replace hello value `192.168.0.1` with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="fe402-474">Ten wpis kieruje wszystkich innych żądań toohello lokalnymi DNS serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-474">This entry routes all other DNS requests toohello on-premises DNS server.</span></span>

3. <span data-ttu-id="fe402-475">Konfiguracja hello toouse, uruchom ponownie powiązania.</span><span class="sxs-lookup"><span data-stu-id="fe402-475">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="fe402-476">Na przykład `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="fe402-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="fe402-477">Dodaj serwer DNS warunkowego przesyłania dalej toohello lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="fe402-477">Add a conditional forwarder toohello on-premises DNS server.</span></span> <span data-ttu-id="fe402-478">Skonfiguruj hello warunkowego przesyłania dalej toosend żądań hello sufiksu DNS z kroku 1 toohello niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-478">Configure hello conditional forwarder toosend requests for hello DNS suffix from step 1 toohello custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fe402-479">Dokumentacja hello oprogramowania DNS dla szczegółowych informacji na temat tooadd warunkowego przesyłania dalej.</span><span class="sxs-lookup"><span data-stu-id="fe402-479">Consult hello documentation for your DNS software for specifics on how tooadd a conditional forwarder.</span></span>

<span data-ttu-id="fe402-480">Po wykonaniu tych czynności możesz połączyć tooresources w każdej sieci przy użyciu w pełni kwalifikowanych nazw domen (FQDN).</span><span class="sxs-lookup"><span data-stu-id="fe402-480">After completing these steps, you can connect tooresources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="fe402-481">Teraz można zainstalować usługi HDInsight w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-481">You can now install HDInsight into hello virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="fe402-482">Rozpoznawanie nazw między dwiema połączone sieci wirtualne</span><span class="sxs-lookup"><span data-stu-id="fe402-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="fe402-483">W tym przykładzie powoduje hello następujące założenia:</span><span class="sxs-lookup"><span data-stu-id="fe402-483">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="fe402-484">Masz dwie sieci wirtualnych Azure, które są połączone przy użyciu bramy sieci VPN lub komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="fe402-485">Hello niestandardowy serwer DNS w obu sieci działa jako system operacyjny hello Linux lub Unix.</span><span class="sxs-lookup"><span data-stu-id="fe402-485">hello custom DNS server in both networks is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="fe402-486">[Powiąż](https://www.isc.org/downloads/bind/) jest zainstalowany na powitania niestandardowych serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-486">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS servers.</span></span>

1. <span data-ttu-id="fe402-487">Użyj programu Azure PowerShell lub interfejsu wiersza polecenia Azure toofind hello sufiksu DNS obu sieci wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="fe402-487">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="fe402-488">Witaj Użyj następującego tekstu jako zawartość hello hello `/etc/bind/named.config.local` pliku na powitania niestandardowy serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-488">Use hello following text as hello contents of hello `/etc/bind/named.config.local` file on hello custom DNS server.</span></span> <span data-ttu-id="fe402-489">Na powitania niestandardowy serwer DNS w sieci zarówno wirtualnych, należy wprowadzić tę zmianę.</span><span class="sxs-lookup"><span data-stu-id="fe402-489">Make this change on hello custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    <span data-ttu-id="fe402-490">Zastąp hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` wartości z sufiksem DNS hello hello __innych__ sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fe402-490">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of hello __other__ virtual network.</span></span> <span data-ttu-id="fe402-491">Ten wpis kieruje żądania dla sufiksu DNS hello toohello sieci zdalnej hello niestandardowe DNS w sieci.</span><span class="sxs-lookup"><span data-stu-id="fe402-491">This entry routes requests for hello DNS suffix of hello remote network toohello custom DNS in that network.</span></span>

3. <span data-ttu-id="fe402-492">Na powitania niestandardowych serwerów DNS w sieci zarówno wirtualnych, użyj następującego tekstu jako zawartość hello hello hello `/etc/bind/named.conf.options` pliku:</span><span class="sxs-lookup"><span data-stu-id="fe402-492">On hello custom DNS servers in both virtual networks, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
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

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="fe402-493">Zastąp hello `10.0.0.0/16` i `10.1.0.0/16` wartości z adresem IP hello odnoszą się do zakresów sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="fe402-493">Replace hello `10.0.0.0/16` and `10.1.0.0/16` values with hello IP address ranges of your virtual networks.</span></span> <span data-ttu-id="fe402-494">Ten wpis umożliwia zasobów w każdej sieci żądań toomake hello serwerów DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-494">This entry allows resources in each network toomake requests of hello DNS servers.</span></span>

    <span data-ttu-id="fe402-495">Wszystkie żądania, które nie są dostępne dla sufiksów DNS hello hello sieciami wirtualnymi (na przykład microsoft.com) jest obsługiwane przez hello Azure cyklicznego programu rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="fe402-495">Any requests that are not for hello DNS suffixes of hello virtual networks (for example, microsoft.com) is handled by hello Azure recursive resolver.</span></span>

4. <span data-ttu-id="fe402-496">Konfiguracja hello toouse, uruchom ponownie powiązania.</span><span class="sxs-lookup"><span data-stu-id="fe402-496">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="fe402-497">Na przykład `sudo service bind9 restart` na obu serwerach DNS.</span><span class="sxs-lookup"><span data-stu-id="fe402-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="fe402-498">Po wykonaniu tych czynności możesz połączyć tooresources w hello sieci wirtualnej przy użyciu w pełni kwalifikowanych nazw domen (FQDN).</span><span class="sxs-lookup"><span data-stu-id="fe402-498">After completing these steps, you can connect tooresources in hello virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="fe402-499">Teraz można zainstalować usługi HDInsight w sieci wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="fe402-499">You can now install HDInsight into hello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe402-500">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe402-500">Next steps</span></span>

* <span data-ttu-id="fe402-501">Na przykład na trasie konfiguracji sieci lokalnej tooan tooconnect HDInsight, zobacz [sieć lokalną tooan połączyć HDInsight](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="fe402-501">For an end-to-end example of configuring HDInsight tooconnect tooan on-premises network, see [Connect HDInsight tooan on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="fe402-502">Aby uzyskać więcej informacji o sieci wirtualnych platformy Azure, zobacz hello [Omówienie usługi Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe402-502">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="fe402-503">Aby uzyskać więcej informacji dotyczących grup zabezpieczeń sieci, zobacz [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="fe402-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="fe402-504">Aby uzyskać więcej informacji dotyczących tras zdefiniowanych przez użytkownika, zobacz [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe402-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>