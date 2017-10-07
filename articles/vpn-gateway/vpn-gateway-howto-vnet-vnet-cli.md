---
title: "Połączenie wirtualnej sieci tooanother sieci wirtualnej: wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono łączenie sieci wirtualnych przy użyciu usługi Azure Resource Manager oraz interfejsu wiersza polecenia platformy Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="6bd07-103">Konfigurowanie połączenia bramy sieci VPN między sieciami wirtualnymi przy użyciu interfejsu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6bd07-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="6bd07-104">W tym artykule opisano sposób toocreate połączenie bramy sieci VPN między sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="6bd07-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="6bd07-105">Witaj sieci wirtualne mogą być w hello tych samych lub różnych regionów, a z hello takie same lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6bd07-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="6bd07-106">Podczas łączenia sieci wirtualne z różnych subskrypcji, subskrypcje hello nie ma potrzeby toobe skojarzone z hello tej samej dzierżawy usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6bd07-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="6bd07-107">Witaj opisanych w tym artykule mają zastosowanie modelu wdrażania usługi Resource Manager toohello i użyć wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6bd07-107">hello steps in this article apply toohello Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="6bd07-108">Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="6bd07-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6bd07-109">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6bd07-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="6bd07-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bd07-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="6bd07-111">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6bd07-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="6bd07-112">Portal Azure (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="6bd07-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="6bd07-113">Łączenie różnych modeli wdrażania — witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6bd07-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="6bd07-114">Łączenie różnych modeli wdrażania — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="6bd07-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="6bd07-115">Połączenie wirtualnej sieci tooanother sieć wirtualną (VNet-VNet) jest podobne tooconnecting lokalizacji sieci wirtualnej tooan lokalnej lokacji.</span><span class="sxs-lookup"><span data-stu-id="6bd07-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="6bd07-116">Oba typy łączności Użyj tooprovide bramy sieci VPN przy użyciu protokołu IPsec/IKE bezpiecznego tunelu.</span><span class="sxs-lookup"><span data-stu-id="6bd07-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="6bd07-117">Jeśli Twoje sieci wirtualne są w hello tego samego regionu, może być tooconsider łącząc je przy użyciu sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="6bd07-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="6bd07-118">W przypadku komunikacji równorzędnej sieci wirtualnych nie jest używana brama sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="6bd07-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="6bd07-119">Aby uzyskać więcej informacji, zobacz temat [Komunikacja równorzędna sieci wirtualnych](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6bd07-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="6bd07-120">Komunikację między sieciami wirtualnymi można łączyć z konfiguracjami obejmującymi wiele lokacji.</span><span class="sxs-lookup"><span data-stu-id="6bd07-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="6bd07-121">Dzięki temu można ustanowić topologii sieci, łączące łączności między lokalizacjami z połączeniem sieciowym między wirtualnych, jak pokazano w powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="6bd07-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Informacje o połączeniach](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="6bd07-123"><a name="why"></a>Dlaczego łączy się sieci wirtualne?</span><span class="sxs-lookup"><span data-stu-id="6bd07-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="6bd07-124">Warto sieci wirtualnych tooconnect hello z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="6bd07-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="6bd07-125">**Niezależna od regionu nadmiarowość i obecność geograficzna**</span><span class="sxs-lookup"><span data-stu-id="6bd07-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="6bd07-126">Można tworzyć własne replikacje geograficzne lub przeprowadzać synchronizację z bezpiecznym połączeniem bez przechodzenia przez punkty końcowe dostępne z Internetu.</span><span class="sxs-lookup"><span data-stu-id="6bd07-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="6bd07-127">Usługi Azure Traffic Manager i Load Balancer pozwalają skonfigurować obciążenie o wysokiej dostępności z nadmiarowością geograficzną w wielu regionach świadczenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="6bd07-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="6bd07-128">Przykładem ważne jest tooset się SQL zawsze włączone grupy dostępności rozsyłanie się w różnych regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6bd07-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="6bd07-129">**Regionalne aplikacje wielowarstwowe z izolacją lub granicami administracyjnymi**</span><span class="sxs-lookup"><span data-stu-id="6bd07-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="6bd07-130">Poziomu hello sam region, możesz skonfigurować aplikacje wielowarstwowe z wieloma sieciami wirtualnymi, połączonych ze sobą tooisolation lub wymagań administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="6bd07-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="6bd07-131">Aby uzyskać więcej informacji o połączeniach sieci wirtualnej do sieci wirtualnej, zobacz hello [wirtualnymi — często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="6bd07-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="6bd07-132">Która instrukcje mają zastosowanie w moim przypadku?</span><span class="sxs-lookup"><span data-stu-id="6bd07-132">Which set of steps should I use?</span></span>

<span data-ttu-id="6bd07-133">W tym artykule przedstawiono dwa różne zestawy kroków.</span><span class="sxs-lookup"><span data-stu-id="6bd07-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="6bd07-134">Jeden zestaw kroków [sieci wirtualnych, które znajdują się w hello tej samej subskrypcji](#samesub)i drugi dla [sieci wirtualnych, które znajdują się w różnych subskrypcji](#difsub).</span><span class="sxs-lookup"><span data-stu-id="6bd07-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="6bd07-135"><a name="samesub"></a>Połączyć sieci wirtualnych, które znajdują się w hello tej samej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6bd07-135"><a name="samesub"></a>Connect VNets that are in hello same subscription</span></span>

![Diagram połączenia między sieciami wirtualnymi (v2v)](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="6bd07-137">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="6bd07-137">Before you begin</span></span>

<span data-ttu-id="6bd07-138">Przed rozpoczęciem należy zainstalować najnowszą wersję hello hello polecenia interfejsu wiersza polecenia (2.0 lub nowszej).</span><span class="sxs-lookup"><span data-stu-id="6bd07-138">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="6bd07-139">Informacje o instalowaniu hello polecenia interfejsu wiersza polecenia, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6bd07-139">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="6bd07-140"><a name="Plan"></a>Planowanie zakresów adresów IP</span><span class="sxs-lookup"><span data-stu-id="6bd07-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="6bd07-141">Hello następujące kroki utworzymy dwie sieci wirtualne wraz z ich bramy odpowiednich podsieci i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6bd07-141">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="6bd07-142">Następnie utworzymy połączenie sieci VPN między Witaj dwie sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="6bd07-142">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="6bd07-143">Jest ważne tooplan zakresów adresów IP powitania dla konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="6bd07-143">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="6bd07-144">Niezbędne jest upewnienie się, że zakresy sieci wirtualnej ani sieci lokalnej nie zachodzą na siebie w jakikolwiek sposób.</span><span class="sxs-lookup"><span data-stu-id="6bd07-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="6bd07-145">W tych przykładach nie uwzględniamy serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="6bd07-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="6bd07-146">Jeśli chcesz, aby w sieciach wirtualnych działało rozpoznawanie nazw, zobacz artykuł o [rozpoznawaniu nazw](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="6bd07-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="6bd07-147">Używamy hello następujące wartości w przykładach hello:</span><span class="sxs-lookup"><span data-stu-id="6bd07-147">We use hello following values in hello examples:</span></span>

<span data-ttu-id="6bd07-148">**Wartości dla sieci TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="6bd07-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="6bd07-149">Nazwa sieci wirtualnej: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="6bd07-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="6bd07-150">Grupa zasobów: TestRG1</span><span class="sxs-lookup"><span data-stu-id="6bd07-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="6bd07-151">Lokalizacja: Wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="6bd07-151">Location: East US</span></span>
* <span data-ttu-id="6bd07-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6bd07-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="6bd07-153">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="6bd07-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="6bd07-154">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="6bd07-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="6bd07-155">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="6bd07-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="6bd07-156">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="6bd07-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="6bd07-157">Publiczny adres IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="6bd07-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="6bd07-158">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="6bd07-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="6bd07-159">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="6bd07-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="6bd07-160">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="6bd07-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="6bd07-161">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="6bd07-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="6bd07-162">**Wartości dla sieci TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="6bd07-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="6bd07-163">Nazwa sieci wirtualnej: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="6bd07-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="6bd07-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6bd07-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="6bd07-165">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="6bd07-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="6bd07-166">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="6bd07-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="6bd07-167">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="6bd07-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="6bd07-168">Grupa zasobów: TestRG4</span><span class="sxs-lookup"><span data-stu-id="6bd07-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="6bd07-169">Lokalizacja: West US</span><span class="sxs-lookup"><span data-stu-id="6bd07-169">Location: West US</span></span>
* <span data-ttu-id="6bd07-170">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="6bd07-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="6bd07-171">Publiczny adres IP: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="6bd07-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="6bd07-172">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="6bd07-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="6bd07-173">Połączenie: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="6bd07-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="6bd07-174">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="6bd07-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="6bd07-175"><a name="Connect"></a>Krok 1 — Połącz tooyour subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6bd07-175"><a name="Connect"></a>Step 1 - Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="6bd07-176"><a name="TestVNet1"></a>Krok 2 — Tworzenie i konfigurowanie sieci TestVNet1</span><span class="sxs-lookup"><span data-stu-id="6bd07-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="6bd07-177">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="6bd07-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="6bd07-178">Utwórz TestVNet1 i hello podsieci dla TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="6bd07-178">Create TestVNet1 and hello subnets for TestVNet1.</span></span> <span data-ttu-id="6bd07-179">W tym przykładzie jest tworzona sieć wirtualna TestVNet1 i podsieć o nazwie FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="6bd07-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="6bd07-180">Utwórz przestrzeń adresową dodatkowe hello podsieci wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6bd07-180">Create an additional address space for hello backend subnet.</span></span> <span data-ttu-id="6bd07-181">Zwróć uwagę, w tym kroku, możemy określić przestrzeń adresowa hello zarówno utworzony wcześniej czy hello dodatkową przestrzeń adresów czy chcemy tooadd.</span><span class="sxs-lookup"><span data-stu-id="6bd07-181">Notice that in this step, we specify both hello address space that we created earlier, and hello additional address space that we want tooadd.</span></span> <span data-ttu-id="6bd07-182">Jest to spowodowane hello [zaktualizować sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet#update) polecenia zastępuje hello poprzednie ustawienia.</span><span class="sxs-lookup"><span data-stu-id="6bd07-182">This is because hello [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites hello previous settings.</span></span> <span data-ttu-id="6bd07-183">Upewnij się, że toospecify na wszystkie prefiksy adresów hello, korzystając z tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="6bd07-183">Make sure toospecify all of hello address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="6bd07-184">Utwórz hello podsieci wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6bd07-184">Create hello backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="6bd07-185">Utwórz podsieć bramy hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-185">Create hello gateway subnet.</span></span> <span data-ttu-id="6bd07-186">Należy zauważyć, że podsieci bramy hello o nazwie "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="6bd07-186">Notice that hello gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="6bd07-187">Nazwa jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="6bd07-187">This name is required.</span></span> <span data-ttu-id="6bd07-188">W tym przykładzie podsieć bramy hello używa /27.</span><span class="sxs-lookup"><span data-stu-id="6bd07-188">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="6bd07-189">Mimo że jest możliwe toocreate jak /29 podsieć bramy, zaleca się utworzenie większej podsieć, która zawiera więcej adresów, wybierając co najmniej /28 lub /27.</span><span class="sxs-lookup"><span data-stu-id="6bd07-189">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="6bd07-190">Umożliwi to za mało adresów tooaccommodate możliwe dodatkowe konfiguracje, które można w hello przyszłych.</span><span class="sxs-lookup"><span data-stu-id="6bd07-190">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="6bd07-191">Żądaj publicznego adresu IP adres toobe toohello przydzielone bramy utworzone sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6bd07-191">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="6bd07-192">Należy zauważyć, że hello AllocationMethod jest dynamiczny.</span><span class="sxs-lookup"><span data-stu-id="6bd07-192">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="6bd07-193">Nie można określić hello adresu IP, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="6bd07-193">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="6bd07-194">Jest dynamicznie przydzielonego tooyour bramy.</span><span class="sxs-lookup"><span data-stu-id="6bd07-194">It's dynamically allocated tooyour gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="6bd07-195">Tworzenie bramy sieci wirtualnej powitania dla TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="6bd07-195">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="6bd07-196">Konfiguracje połączeń między sieciami wirtualnymi wymagają zastosowania wartości RouteBased obiektu VpnType.</span><span class="sxs-lookup"><span data-stu-id="6bd07-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="6bd07-197">Po uruchomieniu tego polecenia, używając hello parametr — nie - oczekiwania nie widać żadnych opinie i danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6bd07-197">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="6bd07-198">Witaj — nie - oczekiwania parametr umożliwia toocreate bramy hello w tle hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-198">hello '--no-wait' parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="6bd07-199">Nie oznacza tej bramy VPN hello zakończy tworzenie natychmiast.</span><span class="sxs-lookup"><span data-stu-id="6bd07-199">It does not mean that hello VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="6bd07-200">Tworzenie bramy może potrwać często 45 minut lub dłużej, w zależności od bramy hello jednostka SKU, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="6bd07-200">Creating a gateway can often take 45 minutes or more, depending on hello gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="6bd07-201"><a name="TestVNet4"></a>Krok 3 — Tworzenie i konfigurowanie sieci TestVNet4</span><span class="sxs-lookup"><span data-stu-id="6bd07-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="6bd07-202">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="6bd07-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="6bd07-203">Utwórz sieć TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="6bd07-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="6bd07-204">Utwórz dodatkowe podsieci dla sieci TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="6bd07-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="6bd07-205">Utwórz podsieć bramy hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-205">Create hello gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="6bd07-206">Prześlij żądanie dotyczące publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6bd07-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="6bd07-207">Utwórz bramę sieci wirtualnej TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-207">Create hello TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="6bd07-208"><a name="createconnect"></a>Krok 4 — Utwórz hello połączenia</span><span class="sxs-lookup"><span data-stu-id="6bd07-208"><a name="createconnect"></a>Step 4 - Create hello connections</span></span>

<span data-ttu-id="6bd07-209">Mamy teraz dwie sieci wirtualne z bramami sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="6bd07-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="6bd07-210">Witaj następnym krokiem jest toocreate połączenia bramy sieci VPN między hello bram sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6bd07-210">hello next step is toocreate VPN gateway connections between hello virtual network gateways.</span></span> <span data-ttu-id="6bd07-211">Jeśli użyto hello przykładach z bram sieci wirtualnej są w różnych grupach zasobów.</span><span class="sxs-lookup"><span data-stu-id="6bd07-211">If you used hello examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="6bd07-212">Gdy bramy znajdują się w różnych grupach zasobów, należy tooidentify i określ hello identyfikatorów zasobów dla każdej bramy podczas nawiązywania połączenia.</span><span class="sxs-lookup"><span data-stu-id="6bd07-212">When gateways are in different resource groups, you need tooidentify and specify hello resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="6bd07-213">Jeśli Twoje sieci wirtualne są w hello tej samej grupie zasobów, można użyć hello [drugi zestaw instrukcji](#samerg) wystarczy identyfikatorów zasobów hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="6bd07-213">If your VNets are in hello same resource group, you can use hello [second set of instructions](#samerg) because you don't need toospecify hello resource IDs.</span></span>

### <span data-ttu-id="6bd07-214"><a name="diffrg"></a>tooconnect sieci wirtualnych, które znajdują się w różnych grupach zasobów</span><span class="sxs-lookup"><span data-stu-id="6bd07-214"><a name="diffrg"></a>tooconnect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="6bd07-215">Pobierz hello identyfikator VNet1GW zasobów z danych wyjściowych hello hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6bd07-215">Get hello Resource ID of VNet1GW from hello output of hello following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="6bd07-216">W danych wyjściowych hello Znajdź hello "identyfikator:" wiersza.</span><span class="sxs-lookup"><span data-stu-id="6bd07-216">In hello output, find hello "id:" line.</span></span> <span data-ttu-id="6bd07-217">wartości Hello w cudzysłowy hello są potrzebne toocreate hello połączenia w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-217">hello values within hello quotes are needed toocreate hello connection in hello next section.</span></span> <span data-ttu-id="6bd07-218">Skopiuj te wartości tooa edytora tekstów, takiego jak Notatnik, dzięki czemu można łatwo je wklejać podczas tworzenia połączenia.</span><span class="sxs-lookup"><span data-stu-id="6bd07-218">Copy these values tooa text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="6bd07-219">Przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6bd07-219">Example output:</span></span>

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  <span data-ttu-id="6bd07-220">Skopiuj wartości powitania po **"id":** w cudzysłowy hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-220">Copy hello values after **"id":** within hello quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="6bd07-221">Pobierz hello identyfikator VNet4GW zasobów i skopiuj hello wartości tooa edytora tekstu.</span><span class="sxs-lookup"><span data-stu-id="6bd07-221">Get hello Resource ID of VNet4GW and copy hello values tooa text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="6bd07-222">Utwórz połączenie tooTestVNet4 TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-222">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="6bd07-223">W tym kroku utworzysz hello połączenia z TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="6bd07-223">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="6bd07-224">Brak klucza współdzielonego, do którego odwołuje się przykłady hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-224">There is a shared key referenced in hello examples.</span></span> <span data-ttu-id="6bd07-225">Możesz użyć własnych wartości dla klucza udostępnionego hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-225">You can use your own values for hello shared key.</span></span> <span data-ttu-id="6bd07-226">ważne, czy element jest klucz udostępniony hello Hello muszą być zgodne, dla obu połączeń.</span><span class="sxs-lookup"><span data-stu-id="6bd07-226">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="6bd07-227">Tworzenie połączenia trwa krótko podczas toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6bd07-227">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="6bd07-228">Utwórz połączenie tooTestVNet1 TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-228">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="6bd07-229">Ten krok jest podobne toohello, jeden powyżej, z wyjątkiem połączeń hello jest tworzony z TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="6bd07-229">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="6bd07-230">Upewnij się, że klucze hello udostępnionych pasują do siebie.</span><span class="sxs-lookup"><span data-stu-id="6bd07-230">Make sure hello shared keys match.</span></span> <span data-ttu-id="6bd07-231">Trwa kilka minut tooestablish hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="6bd07-231">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="6bd07-232">Sprawdź połączenia.</span><span class="sxs-lookup"><span data-stu-id="6bd07-232">Verify your connections.</span></span> <span data-ttu-id="6bd07-233">Zobacz sekcję [Weryfikowanie połączenia](#verify).</span><span class="sxs-lookup"><span data-stu-id="6bd07-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="6bd07-234"><a name="samerg"></a>tooconnect sieci wirtualnych, które znajdują się w hello same grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="6bd07-234"><a name="samerg"></a>tooconnect VNets that reside in hello same resource group</span></span>

1. <span data-ttu-id="6bd07-235">Utwórz połączenie tooTestVNet4 TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-235">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="6bd07-236">W tym kroku utworzysz hello połączenia z TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="6bd07-236">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="6bd07-237">Grupy zasobów hello powiadomienia są hello sam w przykładach hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-237">Notice hello resource groups are hello same in hello examples.</span></span> <span data-ttu-id="6bd07-238">Widoczny jest również określany w przykładach hello klucza wspólnego.</span><span class="sxs-lookup"><span data-stu-id="6bd07-238">You also see a shared key referenced in hello examples.</span></span> <span data-ttu-id="6bd07-239">Możesz użyć własnych wartości dla klucza udostępnionego hello, jednak hello klucz współużytkowany musi być zgodna dla obu połączeń.</span><span class="sxs-lookup"><span data-stu-id="6bd07-239">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="6bd07-240">Tworzenie połączenia trwa krótko podczas toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6bd07-240">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="6bd07-241">Utwórz połączenie tooTestVNet1 TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-241">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="6bd07-242">Ten krok jest podobne toohello, jeden powyżej, z wyjątkiem połączeń hello jest tworzony z TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="6bd07-242">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="6bd07-243">Upewnij się, że klucze hello udostępnionych pasują do siebie.</span><span class="sxs-lookup"><span data-stu-id="6bd07-243">Make sure hello shared keys match.</span></span> <span data-ttu-id="6bd07-244">Trwa kilka minut tooestablish hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="6bd07-244">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="6bd07-245">Sprawdź połączenia.</span><span class="sxs-lookup"><span data-stu-id="6bd07-245">Verify your connections.</span></span> <span data-ttu-id="6bd07-246">Zobacz sekcję [Weryfikowanie połączenia](#verify).</span><span class="sxs-lookup"><span data-stu-id="6bd07-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="6bd07-247"><a name="difsub"></a>Łączenie sieci wirtualnych, które należą do różnych subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6bd07-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![Diagram połączenia między sieciami wirtualnymi (v2v)](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="6bd07-249">W tym scenariuszu nawiązywane jest połączenie między sieciami wirtualnymi TestVNet1 i TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="6bd07-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="6bd07-250">Witaj sieci wirtualne znajdują się różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6bd07-250">hello VNets reside different subscriptions.</span></span> <span data-ttu-id="6bd07-251">Subskrypcje Hello nie są skojarzone z hello toobe tej samej dzierżawy usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6bd07-251">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="6bd07-252">Hello czynności dla tej konfiguracji dodać dodatkowego połączenia do wirtualnymi w kolejności tooconnect TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="6bd07-252">hello steps for this configuration add an additional VNet-to-VNet connection in order tooconnect TestVNet1 tooTestVNet5.</span></span>

### <span data-ttu-id="6bd07-253"><a name="TestVNet1diff"></a>Krok 5 — Tworzenie i konfigurowanie sieci TestVNet1</span><span class="sxs-lookup"><span data-stu-id="6bd07-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="6bd07-254">Te instrukcje są nadal kroki hello w powyższej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-254">These instructions continue from hello steps in hello preceding sections.</span></span> <span data-ttu-id="6bd07-255">Należy wykonać [krok 1](#Connect) i [krok 2](#TestVNet1) toocreate i skonfiguruj TestVNet1 oraz hello bramy sieci VPN dla TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="6bd07-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="6bd07-256">W przypadku tej konfiguracji nie jest wymagane toocreate TestVNet4 z poprzedniej sekcji hello, mimo że, jeśli tworzysz, nie będzie ona konflikt z tych kroków.</span><span class="sxs-lookup"><span data-stu-id="6bd07-256">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="6bd07-257">Po ukończeniu kroków 1 i 2 przejdź do kroku 6 (poniżej).</span><span class="sxs-lookup"><span data-stu-id="6bd07-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="6bd07-258"><a name="verifyranges"></a>Krok 6 - Sprawdź, czy zakresy adresów IP hello</span><span class="sxs-lookup"><span data-stu-id="6bd07-258"><a name="verifyranges"></a>Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="6bd07-259">Podczas tworzenia dodatkowych połączeń, jest ważne tooverify, który hello przestrzeń adresową hello nowej sieci wirtualnej nie zachodzi na inne zakresy sieci wirtualnej lub zakresy bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="6bd07-259">When creating additional connections, it's important tooverify that hello IP address space of hello new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="6bd07-260">W tym ćwiczeniu program hello następujące wartości hello TestVNet5:</span><span class="sxs-lookup"><span data-stu-id="6bd07-260">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="6bd07-261">**Wartości dla sieci TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="6bd07-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="6bd07-262">Nazwa sieci wirtualnej: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="6bd07-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="6bd07-263">Grupa zasobów: TestRG5</span><span class="sxs-lookup"><span data-stu-id="6bd07-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="6bd07-264">Lokalizacja: Japan East</span><span class="sxs-lookup"><span data-stu-id="6bd07-264">Location: Japan East</span></span>
* <span data-ttu-id="6bd07-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6bd07-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="6bd07-266">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="6bd07-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="6bd07-267">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="6bd07-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="6bd07-268">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="6bd07-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="6bd07-269">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="6bd07-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="6bd07-270">Publiczny adres IP: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="6bd07-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="6bd07-271">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="6bd07-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="6bd07-272">Połączenie: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="6bd07-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="6bd07-273">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="6bd07-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="6bd07-274"><a name="TestVNet5"></a>Krok 7 — Tworzenie i konfigurowanie sieci TestVNet5</span><span class="sxs-lookup"><span data-stu-id="6bd07-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="6bd07-275">Ten krok należy wykonać w kontekście hello hello nową subskrypcję, 5 subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6bd07-275">This step must be done in hello context of hello new subscription, Subscription 5.</span></span> <span data-ttu-id="6bd07-276">Ta część może zostać wykonana przez administratora hello w innej organizacji, który jest właścicielem hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6bd07-276">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span> <span data-ttu-id="6bd07-277">tooswitch między subskrypcjami "listy kont az — wszystkie" toolist hello subskrypcje dostępne tooyour konta, a następnie użyj "skonfigurowane konto az — subskrypcji <subscriptionID>" tooswitch toohello subskrypcji, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="6bd07-277">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="6bd07-278">Upewnij się, że możesz są połączone tooSubscription 5, a następnie utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="6bd07-278">Make sure you are connected tooSubscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="6bd07-279">Utwórz sieć wirtualną TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="6bd07-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="6bd07-280">Dodaj podsieci.</span><span class="sxs-lookup"><span data-stu-id="6bd07-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="6bd07-281">Dodaj podsieć bramy hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-281">Add hello gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="6bd07-282">Prześlij żądanie dotyczące publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6bd07-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="6bd07-283">Utwórz bramę TestVNet5 hello</span><span class="sxs-lookup"><span data-stu-id="6bd07-283">Create hello TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="6bd07-284"><a name="connections5"></a>Krok 8 — Utwórz hello połączenia</span><span class="sxs-lookup"><span data-stu-id="6bd07-284"><a name="connections5"></a>Step 8 - Create hello connections</span></span>

<span data-ttu-id="6bd07-285">Możemy podzielić ten krok do dwóch sesji CLI oznaczona jako **[subskrypcji 1]**, i **[subskrypcji 5]** hello bramy znajdują się w różnych subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="6bd07-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because hello gateways are in hello different subscriptions.</span></span> <span data-ttu-id="6bd07-286">tooswitch między subskrypcjami "listy kont az — wszystkie" toolist hello subskrypcje dostępne tooyour konta, a następnie użyj "skonfigurowane konto az — subskrypcji <subscriptionID>" tooswitch toohello subskrypcji, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="6bd07-286">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="6bd07-287">**[Subskrypcji 1]**  Logowania i połącz tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="6bd07-287">**[Subscription 1]** Log in and connect tooSubscription 1.</span></span> <span data-ttu-id="6bd07-288">Witaj uruchom następujące polecenie tooget hello nazwy i Identyfikatora hello bramy z danych wyjściowych hello:</span><span class="sxs-lookup"><span data-stu-id="6bd07-288">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="6bd07-289">Kopiuj dane wyjściowe powitania dla "identyfikator:".</span><span class="sxs-lookup"><span data-stu-id="6bd07-289">Copy hello output for "id:".</span></span> <span data-ttu-id="6bd07-290">Wyślij hello identyfikator i nazwa hello hello sieci wirtualnej bramy (VNet1GW) toohello administratora subskrypcji 5 za pomocą poczty e-mail lub innej metody.</span><span class="sxs-lookup"><span data-stu-id="6bd07-290">Send hello ID and hello name of hello VNet gateway (VNet1GW) toohello administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="6bd07-291">Przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6bd07-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="6bd07-292">**[Subskrypcji 5]**  Logowania i połącz tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="6bd07-292">**[Subscription 5]** Log in and connect tooSubscription 5.</span></span> <span data-ttu-id="6bd07-293">Witaj uruchom następujące polecenie tooget hello nazwy i Identyfikatora hello bramy z danych wyjściowych hello:</span><span class="sxs-lookup"><span data-stu-id="6bd07-293">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="6bd07-294">Kopiuj dane wyjściowe powitania dla "identyfikator:".</span><span class="sxs-lookup"><span data-stu-id="6bd07-294">Copy hello output for "id:".</span></span> <span data-ttu-id="6bd07-295">Wyślij hello identyfikator i nazwa hello hello sieci wirtualnej bramy (VNet5GW) toohello administratora subskrypcji 1 za pośrednictwem poczty e-mail lub innej metody.</span><span class="sxs-lookup"><span data-stu-id="6bd07-295">Send hello ID and hello name of hello VNet gateway (VNet5GW) toohello administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="6bd07-296">**[Subskrypcji 1]**  w tym kroku, tworzenia połączenia hello z TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="6bd07-296">**[Subscription 1]** In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="6bd07-297">Możesz użyć własnych wartości dla klucza udostępnionego hello, jednak hello klucz współużytkowany musi być zgodna dla obu połączeń.</span><span class="sxs-lookup"><span data-stu-id="6bd07-297">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="6bd07-298">Tworzenie połączenia może zająć chwilę podczas toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6bd07-298">Creating a connection can take a short while toocomplete.</span></span> <span data-ttu-id="6bd07-299">Upewnij się, że połączenie tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="6bd07-299">Make sure you connect tooSubscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="6bd07-300">**[Subskrypcji 5]**  Ten krok jest podobne toohello, jeden powyżej, z wyjątkiem połączeń hello jest tworzony z TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="6bd07-300">**[Subscription 5]** This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="6bd07-301">Upewnij się, że hello udostępnionych kluczy dopasowania i Połącz z tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="6bd07-301">Make sure that hello shared keys match and that you connect tooSubscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="6bd07-302"><a name="verify"></a>Zweryfikuj hello połączenia</span><span class="sxs-lookup"><span data-stu-id="6bd07-302"><a name="verify"></a>Verify hello connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="6bd07-303"><a name="faq"></a>Często zadawane pytania dotyczące połączeń między sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="6bd07-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="6bd07-304">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6bd07-304">Next steps</span></span>

* <span data-ttu-id="6bd07-305">Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6bd07-305">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="6bd07-306">Aby uzyskać więcej informacji, zobacz hello [dokumentacji maszyn wirtualnych](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="6bd07-306">For more information, see hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="6bd07-307">Uzyskać informacji na temat protokołu BGP, zobacz hello [Omówienie protokołu BGP](vpn-gateway-bgp-overview.md) i [jak tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6bd07-307">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
