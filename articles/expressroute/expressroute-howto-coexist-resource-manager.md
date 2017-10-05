---
title: "Konfigurowanie połączeń usługi ExpressRoute i sieci VPN typu lokacja-lokacja, które mogą współistnieć: usługa Resource Manager: Azure | Microsoft Docs"
description: "Ten artykuł zawiera instrukcje dotyczące konfigurowania połączeń usługi ExpressRoute oraz sieci VPN typu lokacja-lokacja, które mogą współistnieć, dla modelu usługi Resource Manager."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: b29147a37f9a90fc80e16b350ac9b91daac1d7f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="04245-103">Konfigurowanie współistniejących połączeń usługi ExpressRoute i połączeń typu lokacja-lokacja</span><span class="sxs-lookup"><span data-stu-id="04245-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="04245-104">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="04245-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="04245-105">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="04245-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="04245-106">Konfigurowanie sieci VPN typu lokacja-lokacja i współistniejących połączeń usługi ExpressRoute ma kilka zalet.</span><span class="sxs-lookup"><span data-stu-id="04245-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="04245-107">Sieć VPN typu lokacja-lokacja można skonfigurować jako bezpieczną ścieżkę trybu failover dla usługi ExpressRoute lub użyć tej sieci do połączenia z lokacjami, które nie zostały połączone za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04245-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="04245-108">Ten artykuł zawiera instrukcje konfiguracji obu scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="04245-108">We cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="04245-109">Ten artykuł ma zastosowanie w modelu wdrażania przy użyciu usługi Resource Manager i używa programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04245-109">This article applies to the Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="04245-110">Ta konfiguracja nie jest dostępna w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="04245-110">This configuration is not available in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04245-111">Przed wykonaniem poniższych instrukcji należy wstępnie skonfigurować obwody usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04245-111">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="04245-112">Przed kontynuowaniem należy koniecznie wykonać instrukcje [tworzenia obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i [konfigurowania routingu](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="04245-112">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="04245-113">Limity i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="04245-113">Limits and limitations</span></span>
* <span data-ttu-id="04245-114">**Routing tranzytowy nie jest obsługiwany.**</span><span class="sxs-lookup"><span data-stu-id="04245-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="04245-115">Nie można skierować połączenia (przez platformę Azure) między lokalną siecią połączoną za pośrednictwem sieci VPN typu lokacja-lokacja i lokalną siecią połączoną za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04245-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="04245-116">**Podstawowa brama jednostki SKU nie jest obsługiwana.**</span><span class="sxs-lookup"><span data-stu-id="04245-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="04245-117">Należy użyć innej niż podstawowa bramy jednostki SKU zarówno dla [bramy usługi ExpressRoute](expressroute-about-virtual-network-gateways.md), jak i [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="04245-117">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="04245-118">**Obsługiwana jest tylko brama sieci VPN oparta na trasach.**</span><span class="sxs-lookup"><span data-stu-id="04245-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="04245-119">Należy użyć [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) opartej na trasach.</span><span class="sxs-lookup"><span data-stu-id="04245-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="04245-120">**Dla bramy sieci VPN należy skonfigurować trasę statyczną.**</span><span class="sxs-lookup"><span data-stu-id="04245-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="04245-121">Jeśli sieć lokalna jest połączona z usługą ExpressRoute oraz siecią VPN typu lokacja-lokacja, aby skierować połączenie sieci VPN typu lokacja-lokacja do publicznego Internetu, trzeba mieć skonfigurowaną trasę statyczną w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="04245-121">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="04245-122">**Najpierw należy skonfigurować bramę usługi ExpressRoute i połączyć ją z obwodem.**</span><span class="sxs-lookup"><span data-stu-id="04245-122">**ExpressRoute gateway must be configured first and linked to a circuit.**</span></span> <span data-ttu-id="04245-123">Przed dodaniem bramy sieci VPN typu lokacja-lokacja utwórz bramę usługi ExpressRoute i połącz ją z obwodem.</span><span class="sxs-lookup"><span data-stu-id="04245-123">You must create the ExpressRoute gateway first and link it to a circuit before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="04245-124">Projekty konfiguracji</span><span class="sxs-lookup"><span data-stu-id="04245-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="04245-125">Konfigurowanie sieci VPN typu lokacja-lokacja jako ścieżki pracy awaryjnej dla usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="04245-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="04245-126">Połączenie sieci VPN typu lokacja-lokacja można skonfigurować do przechowywania kopii zapasowych dla usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04245-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="04245-127">Dotyczy to tylko sieci wirtualnych połączonych ze ścieżką prywatnej sieci równorzędnej Azure.</span><span class="sxs-lookup"><span data-stu-id="04245-127">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="04245-128">Nie ma rozwiązania pracy awaryjnej opartego na sieci VPN dla usług dostępnych przez publiczne sesje komunikacji równorzędnej platformy Azure ani komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="04245-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="04245-129">Obwód usługi ExpressRoute jest zawsze połączeniem podstawowym.</span><span class="sxs-lookup"><span data-stu-id="04245-129">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="04245-130">Dane przepływają przez ścieżkę sieci VPN typu lokacja-lokacja tylko w przypadku awarii obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04245-130">Data flows through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="04245-131">Obwód usługi ExpressRoute jest preferowany w porównaniu z siecią VPN typu lokacja-lokacja, jeśli obydwie trasy są takie same, a na platformie Azure dopasowanie najdłuższego prefiksu będzie używane do wybierania trasy do miejsca docelowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="04245-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![Współistnienie](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="04245-133">Konfigurowanie sieci VPN typu lokacja-lokacja do łączenia z witrynami niepołączonymi przez usługę ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="04245-133">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="04245-134">Można skonfigurować sieć w taki sposób, by niektóre witryny łączyły się bezpośrednio z platformą Azure za pośrednictwem sieci VPN typu lokacja-lokacja, a niektóre przez usługę ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04245-134">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Współistnienie](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="04245-136">Nie można skonfigurować sieci wirtualnej jako routera tranzytowego.</span><span class="sxs-lookup"><span data-stu-id="04245-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="04245-137">Wybieranie czynności do wykonania</span><span class="sxs-lookup"><span data-stu-id="04245-137">Selecting the steps to use</span></span>
<span data-ttu-id="04245-138">Istnieją dwa różne zestawy procedur do wyboru.</span><span class="sxs-lookup"><span data-stu-id="04245-138">There are two different sets of procedures to choose from.</span></span> <span data-ttu-id="04245-139">Wybór procedury konfiguracji zależy od tego, czy masz istniejącą sieć wirtualną, z którą chcesz się połączyć, czy chcesz utworzyć nową.</span><span class="sxs-lookup"><span data-stu-id="04245-139">The configuration procedure that you select depends on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="04245-140">Nie mam sieci wirtualnej i muszę ją utworzyć.</span><span class="sxs-lookup"><span data-stu-id="04245-140">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="04245-141">Jeśli nie masz jeszcze sieci wirtualnej, ta procedura zawiera instrukcje tworzenia nowej sieci wirtualnej za pomocą modelu wdrażania usługi Resource Manager i tworzenia nowych połączeń usługi ExpressRoute i sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="04245-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="04245-142">Aby skonfigurować sieć wirtualną, wykonaj kroki opisane w sekcji [Aby utworzyć nową sieć wirtualną i współistniejące połączenia](#new).</span><span class="sxs-lookup"><span data-stu-id="04245-142">To configure a virtual network, follow the steps in [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="04245-143">Mam już sieć wirtualną modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="04245-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="04245-144">Być może masz już gotową sieć wirtualną z istniejącym połączeniem sieci VPN typu lokacja-lokacja lub połączeniem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04245-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="04245-145">Sekcja [Aby skonfigurować współistniejące połączenia dla istniejącej sieci wirtualnej](#add) zawiera instrukcje usuwania bramy, a następnie tworzenia nowych połączeń usługi ExpressRoute i połączeń VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="04245-145">The [To configure coexisting connections for an already existing VNet](#add) section walks you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="04245-146">Podczas tworzenia nowych połączeń kroki muszą być wykonywane w określonej kolejności.</span><span class="sxs-lookup"><span data-stu-id="04245-146">When creating the new connections, the steps must be completed in a specific order.</span></span> <span data-ttu-id="04245-147">Do tworzenia bram i połączeń nie używaj instrukcji z innych artykułów.</span><span class="sxs-lookup"><span data-stu-id="04245-147">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="04245-148">W tej procedurze tworzenie połączeń, które mogą współistnieć, wymaga usunięcia Twojej bramy, a następnie skonfigurowania nowych bram.</span><span class="sxs-lookup"><span data-stu-id="04245-148">In this procedure, creating connections that can coexist requires you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="04245-149">Podczas usuwania i odtwarzania bramy oraz połączeń wystąpi przestój względem połączeń obejmujących wiele lokalizacji, ale nie trzeba będzie migrować żadnych maszyn wirtualnych ani usług do nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="04245-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="04245-150">Podczas konfigurowania bramy maszyny wirtualne i usługi będą mogły nadal komunikować się za pośrednictwem modułu równoważenia obciążenia, jeżeli zostały w taki sposób skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="04245-150">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="04245-151"><a name="new"></a>Aby utworzyć nową sieć wirtualną i współistniejące połączenia</span><span class="sxs-lookup"><span data-stu-id="04245-151"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="04245-152">Ta procedura zawiera instrukcje tworzenia sieci wirtualnej i połączeń typu lokacja-lokacja oraz usługi ExpressRoute, które będą współistnieć.</span><span class="sxs-lookup"><span data-stu-id="04245-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="04245-153">Zainstaluj najnowszą wersję poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04245-153">Install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="04245-154">Aby uzyskać więcej informacji na temat instalowania poleceń cmdlet, zobacz [How to install and configure Azure PowerShell](/powershell/azure/overview) (Instalowanie i konfigurowanie programu Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="04245-154">For information about installing the cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="04245-155">Polecenia cmdlet, których użyjesz do tej konfiguracji, mogą trochę różnić się od tych, które znasz.</span><span class="sxs-lookup"><span data-stu-id="04245-155">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="04245-156">Koniecznie użyj poleceń cmdlet podanych w tych instrukcjach.</span><span class="sxs-lookup"><span data-stu-id="04245-156">Be sure to use the cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="04245-157">Zaloguj się na swoje konto i skonfiguruj środowisko.</span><span class="sxs-lookup"><span data-stu-id="04245-157">Log in to your account and set up the environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="04245-158">Utwórz sieć wirtualną, w tym podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="04245-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="04245-159">Więcej informacji na temat konfigurowania sieci wirtualnej znajduje się w temacie [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md) (Konfigurowanie sieci wirtualnej Azure).</span><span class="sxs-lookup"><span data-stu-id="04245-159">For more information about the virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="04245-160">Wartość podsieci bramy musi wynosić /27; prefiks może też być krótszy (np. /26 lub /25).</span><span class="sxs-lookup"><span data-stu-id="04245-160">The Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="04245-161">Utwórz nową sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="04245-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="04245-162">Dodaj podsieci.</span><span class="sxs-lookup"><span data-stu-id="04245-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="04245-163">Zapisz konfigurację sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="04245-163">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="04245-164"><a name="gw"></a>Utwórz bramę usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04245-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="04245-165">Więcej informacji na temat konfigurowania bramy usługi ExpressRoute znajduje się w artykule [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md) (Konfigurowanie bramy usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="04245-165">For more information about the ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="04245-166">Opcja GatewaySKU musi mieć wartość *Standard*, *HighPerformance* lub *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="04245-166">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="04245-167">Połącz bramę usługi ExpressRoute z obwodem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04245-167">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="04245-168">Po ukończeniu tego kroku zostanie nawiązane połączenie między siecią lokalną i platformą Azure za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04245-168">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="04245-169">Więcej informacji na temat operacji łączenia znajduje się w artykule [Link VNets to ExpressRoute](expressroute-howto-linkvnet-arm.md) (Łączenie sieci wirtualnych z usługą ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="04245-169">For more information about the link operation, see [Link VNets to ExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="04245-170"><a name="vpngw"></a>Następnie utwórz bramę sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="04245-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="04245-171">Aby uzyskać więcej informacji dotyczących konfigurowania bramy sieci VPN, zobacz [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md) (Konfigurowanie sieci wirtualnej za pomocą połączenia lokacja-lokacja).</span><span class="sxs-lookup"><span data-stu-id="04245-171">For more information about the VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="04245-172">Opcja GatewaySKU musi mieć wartość *Standard*, *HighPerformance* lub *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="04245-172">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="04245-173">Parametr VpnType musi mieć wartość *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="04245-173">The VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="04245-174">Brama sieci VPN platformy Azure obsługuje protokół routingu BGP.</span><span class="sxs-lookup"><span data-stu-id="04245-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="04245-175">Można określić ASN (numer AS) dla tej sieci wirtualnej przez dodanie przełącznika -Asn w poniższym poleceniu.</span><span class="sxs-lookup"><span data-stu-id="04245-175">You can specify ASN (AS Number) for that Virtual Network by adding the -Asn switch in the following command.</span></span> <span data-ttu-id="04245-176">Nieokreślenie tego parametru spowoduje domyślne ustawienie numeru AS 65515.</span><span class="sxs-lookup"><span data-stu-id="04245-176">Not specifying that parameter will default to AS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="04245-177">Adres IP komunikacji równorzędnej protokołu BGP i numer AS używany przez platformę Azure na potrzeby bramy sieci VPN można znaleźć w zmiennych $azureVpn.BgpSettings.BgpPeeringAddress i $azureVpn.BgpSettings.Asn.</span><span class="sxs-lookup"><span data-stu-id="04245-177">You can find the BGP peering IP and the AS number that Azure uses for the VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="04245-178">Aby uzyskać więcej informacji, zobacz [Konfigurowanie protokołu BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) dla bramy usługi Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="04245-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="04245-179">Utwórz obiekt bramy sieci VPN witryny lokalnej.</span><span class="sxs-lookup"><span data-stu-id="04245-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="04245-180">To polecenie nie powoduje skonfigurowania bramy lokalnej sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="04245-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="04245-181">Umożliwia raczej zapewnienie ustawień bramy lokalnej, np. publicznego adresu IP i lokalnej przestrzeni adresowej, aby brama sieci VPN Azure mogła się z nimi połączyć.</span><span class="sxs-lookup"><span data-stu-id="04245-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
    <span data-ttu-id="04245-182">Jeśli Twoje lokalne urządzenie sieci VPN obsługuje tylko routing statyczny, możesz w następujący sposób skonfigurować trasy statyczne:</span><span class="sxs-lookup"><span data-stu-id="04245-182">If your local VPN device only supports static routing, you can configure the static routes in the following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="04245-183">Jeśli lokalne urządzenie sieci VPN obsługuje protokół BGP i chcesz włączyć routing dynamiczny, należy znać adres IP komunikacji równorzędnej protokołu BGP i numer AS używany przez lokalne urządzenie sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="04245-183">If your local VPN device supports the BGP and you want to enable dynamic routing, you need to know the BGP peering IP and the AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for the BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="04245-184">Skonfiguruj lokalne urządzenie sieci VPN do połączenia z nową bramą sieci VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="04245-184">Configure your local VPN device to connect to the new Azure VPN gateway.</span></span> <span data-ttu-id="04245-185">Więcej informacji na temat konfigurowania urządzenia VPN znajduje się w artykule [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md) (Konfigurowanie urządzenia VPN).</span><span class="sxs-lookup"><span data-stu-id="04245-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="04245-186">Połącz bramę sieci VPN typu lokacja-lokacja na platformie Azure z bramą lokalną.</span><span class="sxs-lookup"><span data-stu-id="04245-186">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="04245-187"><a name="add"></a>Aby skonfigurować współistniejące połączenia dla istniejącej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="04245-187"><a name="add"></a>To configure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="04245-188">Jeśli masz istniejącą sieć wirtualną, sprawdź rozmiar podsieci bramy.</span><span class="sxs-lookup"><span data-stu-id="04245-188">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="04245-189">Jeśli podsieć bramy ma wartość /28 lub /29, musisz najpierw usunąć bramę sieci wirtualnej i zwiększyć rozmiar podsieci bramy.</span><span class="sxs-lookup"><span data-stu-id="04245-189">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="04245-190">W krokach w tej sekcji pokazano, jak to zrobić.</span><span class="sxs-lookup"><span data-stu-id="04245-190">The steps in this section show you how to do that.</span></span>

<span data-ttu-id="04245-191">Jeśli podsieć bramy ma wartość /27 lub większą, a sieć wirtualna jest połączona za pośrednictwem usługi ExpressRoute, możesz pominąć poniższe kroki i przejść do tematu [„Krok 6 — tworzenie bramy sieci VPN typu lokacja-lokacja”](#vpngw) w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="04245-191">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="04245-192">Po usunięciu istniejącej bramy podczas pracy nad tą konfiguracją lokalizacja miejscowa straci połączenie z siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="04245-192">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="04245-193">Niezbędne jest zainstalowanie najnowszej wersji poleceń cmdlet programu Azure PowerShell. </span><span class="sxs-lookup"><span data-stu-id="04245-193">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="04245-194">Aby uzyskać więcej informacji na temat instalowania poleceń cmdlet, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="04245-194">For more information about installing cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="04245-195">Polecenia cmdlet, których użyjesz do tej konfiguracji, mogą trochę różnić się od tych, które znasz.</span><span class="sxs-lookup"><span data-stu-id="04245-195">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="04245-196">Koniecznie użyj poleceń cmdlet podanych w tych instrukcjach.</span><span class="sxs-lookup"><span data-stu-id="04245-196">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="04245-197">Usuń istniejącą bramę usługi ExpressRoute lub sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="04245-197">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="04245-198">Usuń podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="04245-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="04245-199">Dodaj podsieć bramy o wartości /27 lub większej.</span><span class="sxs-lookup"><span data-stu-id="04245-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="04245-200">Jeśli nie masz wystarczającej liczby adresów IP w sieci wirtualnej, aby zwiększyć rozmiar podsieci bramy, dodaj więcej przestrzeni adresowej IP.</span><span class="sxs-lookup"><span data-stu-id="04245-200">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="04245-201">Zapisz konfigurację sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="04245-201">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="04245-202">Na tym etapie masz sieć wirtualną bez bram.</span><span class="sxs-lookup"><span data-stu-id="04245-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="04245-203">W celu utworzenia nowych bram i wykonania połączeń wykonaj instrukcje z części [Krok 4 — tworzenie bramy usługi ExpressRoute](#gw) znajdujące się w poprzednim zestawie kroków.</span><span class="sxs-lookup"><span data-stu-id="04245-203">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="to-add-point-to-site-configuration-to-the-vpn-gateway"></a><span data-ttu-id="04245-204">Aby dodać konfigurację typu punkt-lokacja do bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="04245-204">To add point-to-site configuration to the VPN gateway</span></span>
<span data-ttu-id="04245-205">Możesz wykonać poniższe kroki, aby dodać konfigurację typu punkt-lokacja do bramy sieci VPN w konfiguracji współistnienia.</span><span class="sxs-lookup"><span data-stu-id="04245-205">You can follow the steps below to add Point-to-Site configuration to your VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="04245-206">Dodaj pulę adresów klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="04245-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="04245-207">Przekaż certyfikat główny sieci VPN do platformy Azure dla bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="04245-207">Upload the VPN root certificate to Azure for your VPN gateway.</span></span> <span data-ttu-id="04245-208">W tym przykładzie zakłada się, że certyfikat główny jest przechowywany na komputerze lokalnym, na którym są uruchamiane następujące polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04245-208">In this example, it's assumed that the root certificate is stored in the local machine where the following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="04245-209">Więcej informacji na temat sieci VPN typu punkt-lokacja znajduje się w artykule [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) (Konfigurowanie połączenia typu punkt-lokacja).</span><span class="sxs-lookup"><span data-stu-id="04245-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04245-210">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04245-210">Next steps</span></span>
<span data-ttu-id="04245-211">Więcej informacji na temat usługi ExpressRoute znajduje się w artykule [ExpressRoute FAQ](expressroute-faqs.md) (Usługa ExpressRoute — często zadawane pytania).</span><span class="sxs-lookup"><span data-stu-id="04245-211">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
