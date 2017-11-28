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
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="ef926-103">Konfigurowanie współistniejących połączeń usługi ExpressRoute i połączeń typu lokacja-lokacja</span><span class="sxs-lookup"><span data-stu-id="ef926-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef926-104">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ef926-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="ef926-105">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="ef926-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="ef926-106">Konfigurowanie sieci VPN typu lokacja-lokacja i współistniejących połączeń usługi ExpressRoute ma kilka zalet.</span><span class="sxs-lookup"><span data-stu-id="ef926-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="ef926-107">Konfigurowanie sieci VPN lokacja-lokacja jako ścieżka bezpiecznego trybu failover dla ExressRoute lub użyj toosites tooconnect sieci VPN typu lokacja-lokacja, które nie są połączone za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef926-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="ef926-108">Firma Microsoft obejmuje tooconfigure kroki hello oba scenariusze, w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ef926-108">We cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="ef926-109">Ten artykuł dotyczy modelu wdrażania usługi Resource Manager toohello i korzysta z programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef926-109">This article applies toohello Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="ef926-110">Ta konfiguracja nie jest dostępna w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ef926-110">This configuration is not available in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef926-111">Obwody usługi ExpressRoute musi być wstępnie skonfigurowany przed wykonaniem instrukcji hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="ef926-111">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="ef926-112">Upewnij się, że zbyt po przewodnikach hello[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-arm.md) i [Konfigurowanie routingu](expressroute-howto-routing-arm.md) przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="ef926-112">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="ef926-113">Limity i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="ef926-113">Limits and limitations</span></span>
* <span data-ttu-id="ef926-114">**Routing tranzytowy nie jest obsługiwany.**</span><span class="sxs-lookup"><span data-stu-id="ef926-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="ef926-115">Nie można skierować połączenia (przez platformę Azure) między lokalną siecią połączoną za pośrednictwem sieci VPN typu lokacja-lokacja i lokalną siecią połączoną za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef926-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="ef926-116">**Podstawowa brama jednostki SKU nie jest obsługiwana.**</span><span class="sxs-lookup"><span data-stu-id="ef926-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="ef926-117">Należy użyć bramy z systemem innym niż — podstawowy SKU dla obu hello [bramę usługi ExpressRoute](expressroute-about-virtual-network-gateways.md) i hello [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="ef926-117">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="ef926-118">**Obsługiwana jest tylko brama sieci VPN oparta na trasach.**</span><span class="sxs-lookup"><span data-stu-id="ef926-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="ef926-119">Należy użyć [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) opartej na trasach.</span><span class="sxs-lookup"><span data-stu-id="ef926-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="ef926-120">**Dla bramy sieci VPN należy skonfigurować trasę statyczną.**</span><span class="sxs-lookup"><span data-stu-id="ef926-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="ef926-121">Jeśli sieci lokalnej jest tooboth połączenia ExpressRoute, a Site-to-Site VPN, musi mieć tras statycznych skonfigurowana w Twojej sieci lokalnej tooroute hello Site-to-Site VPN połączenia toohello publicznej sieci Internet.</span><span class="sxs-lookup"><span data-stu-id="ef926-121">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="ef926-122">**Bramę usługi ExpressRoute musi najpierw zostać skonfigurowany i połączony tooa obwodu.**</span><span class="sxs-lookup"><span data-stu-id="ef926-122">**ExpressRoute gateway must be configured first and linked tooa circuit.**</span></span> <span data-ttu-id="ef926-123">Musisz najpierw utworzyć bramę usługi ExpressRoute hello i połączyć ją obwodu tooa przed dodaniem Brama VPN lokacja-lokacja hello.</span><span class="sxs-lookup"><span data-stu-id="ef926-123">You must create hello ExpressRoute gateway first and link it tooa circuit before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="ef926-124">Projekty konfiguracji</span><span class="sxs-lookup"><span data-stu-id="ef926-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="ef926-125">Konfigurowanie sieci VPN typu lokacja-lokacja jako ścieżki pracy awaryjnej dla usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ef926-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="ef926-126">Połączenie sieci VPN typu lokacja-lokacja można skonfigurować do przechowywania kopii zapasowych dla usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef926-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="ef926-127">Dotyczy to tylko toovirtual sieci połączonych toohello Azure prywatnej komunikacji równorzędnej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="ef926-127">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="ef926-128">Nie ma rozwiązania pracy awaryjnej opartego na sieci VPN dla usług dostępnych przez publiczne sesje komunikacji równorzędnej platformy Azure ani komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ef926-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="ef926-129">Witaj obwodu ExpressRoute jest zawsze hello łącze podstawowe.</span><span class="sxs-lookup"><span data-stu-id="ef926-129">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="ef926-130">Dane przepływają za pomocą ścieżki sieci VPN typu lokacja-lokacja hello tylko wtedy, gdy hello obwodu usługi expressroute nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="ef926-130">Data flows through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="ef926-131">Podczas obwodu ExpressRoute preferowanych za pośrednictwem połączenia VPN lokacja-lokacja po obu trasy są takie same Witaj, Azure użyje hello Najdłuższy prefiks dopasowania toochoose hello trasy do miejsca docelowego hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="ef926-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Współistnienie](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="ef926-133">Konfigurowanie sieci VPN typu lokacja-lokacja toosites tooconnect, nie są połączone za pośrednictwem usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ef926-133">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="ef926-134">Można skonfigurować sieci, której niektóre Lokacje łączą się bezpośrednio tooAzure za pośrednictwem połączenia VPN lokacja-lokacja, a niektóre witryny łączenie się za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef926-134">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Współistnienie](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="ef926-136">Nie można skonfigurować sieci wirtualnej jako routera tranzytowego.</span><span class="sxs-lookup"><span data-stu-id="ef926-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="ef926-137">Wybieranie toouse kroki hello</span><span class="sxs-lookup"><span data-stu-id="ef926-137">Selecting hello steps toouse</span></span>
<span data-ttu-id="ef926-138">Istnieją dwa różne zestawy toochoose procedur z.</span><span class="sxs-lookup"><span data-stu-id="ef926-138">There are two different sets of procedures toochoose from.</span></span> <span data-ttu-id="ef926-139">procedury konfiguracji Hello, która zostanie wybrana zależy od tego, czy masz istniejącej sieci wirtualnej ma tooconnect do, czy chcesz toocreate nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ef926-139">hello configuration procedure that you select depends on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="ef926-140">Nie ma sieci wirtualnej i toocreate, co potrzebne.</span><span class="sxs-lookup"><span data-stu-id="ef926-140">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="ef926-141">Jeśli nie masz jeszcze sieci wirtualnej, ta procedura zawiera instrukcje tworzenia nowej sieci wirtualnej za pomocą modelu wdrażania usługi Resource Manager i tworzenia nowych połączeń usługi ExpressRoute i sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="ef926-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="ef926-142">tooconfigure sieci wirtualnej, wykonaj kroki hello w [toocreate nowej sieci wirtualnej i ważnych połączeń](#new).</span><span class="sxs-lookup"><span data-stu-id="ef926-142">tooconfigure a virtual network, follow hello steps in [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="ef926-143">Mam już sieć wirtualną modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef926-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="ef926-144">Być może masz już gotową sieć wirtualną z istniejącym połączeniem sieci VPN typu lokacja-lokacja lub połączeniem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef926-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="ef926-145">Witaj [tooconfigure ważnych połączeń dla już istniejącej sieci wirtualnej](#add) sekcja przeprowadzi Cię przez usuwanie hello bramy, a następnie utworzenie nowego połączenia sieci VPN ExpressRoute, jak i lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="ef926-145">hello [tooconfigure coexisting connections for an already existing VNet](#add) section walks you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="ef926-146">Podczas tworzenia nowych połączeń hello, hello czynności musi wykonać w dowolnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="ef926-146">When creating hello new connections, hello steps must be completed in a specific order.</span></span> <span data-ttu-id="ef926-147">Nie należy używać instrukcji hello w innych artykułach toocreate połączenia i bram.</span><span class="sxs-lookup"><span data-stu-id="ef926-147">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="ef926-148">W tej procedurze tworzenia połączeń, które mogą współistnieć wymaga toodelete możesz bramy, a następnie skonfiguruj nowych bram.</span><span class="sxs-lookup"><span data-stu-id="ef926-148">In this procedure, creating connections that can coexist requires you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="ef926-149">Konieczne będzie przestojów w przypadku połączeń między lokalizacjami w przypadku usunięcia i ponownego tworzenia bramy i połączenia, ale nie będzie konieczne toomigrate poszczególnych maszyn wirtualnych lub usług tooa nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ef926-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="ef926-150">Maszyn wirtualnych i usług będą nadal mogli toocommunicate się za pośrednictwem usługi równoważenia obciążenia hello podczas konfigurowania bramy, jeśli są one skonfigurowane toodo tak.</span><span class="sxs-lookup"><span data-stu-id="ef926-150">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="ef926-151"><a name="new"></a>toocreate nowej sieci wirtualnej i ważnych połączeń</span><span class="sxs-lookup"><span data-stu-id="ef926-151"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="ef926-152">Ta procedura zawiera instrukcje tworzenia sieci wirtualnej i połączeń typu lokacja-lokacja oraz usługi ExpressRoute, które będą współistnieć.</span><span class="sxs-lookup"><span data-stu-id="ef926-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="ef926-153">Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef926-153">Install hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ef926-154">Informacje o instalowaniu hello poleceń cmdlet, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ef926-154">For information about installing hello cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="ef926-155">poleceń cmdlet Hello, której użyjesz dla tej konfiguracji mogą być nieco inne niż co można zapoznać się z.</span><span class="sxs-lookup"><span data-stu-id="ef926-155">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="ef926-156">Polecenia cmdlet hello toouse się, że można określić w tej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="ef926-156">Be sure toouse hello cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="ef926-157">Zaloguj się na koncie tooyour i konfigurowanie środowiska hello.</span><span class="sxs-lookup"><span data-stu-id="ef926-157">Log in tooyour account and set up hello environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="ef926-158">Utwórz sieć wirtualną, w tym podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="ef926-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="ef926-159">Aby uzyskać więcej informacji o konfiguracji sieci wirtualnej hello, zobacz [konfiguracji sieci wirtualnej Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ef926-159">For more information about hello virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ef926-160">Witaj podsieć bramy musi być /27 lub krótszy prefiksu (na przykład /26 lub /25).</span><span class="sxs-lookup"><span data-stu-id="ef926-160">hello Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="ef926-161">Utwórz nową sieć wirtualną.</span><span class="sxs-lookup"><span data-stu-id="ef926-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="ef926-162">Dodaj podsieci.</span><span class="sxs-lookup"><span data-stu-id="ef926-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="ef926-163">Zapisz hello konfigurację sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ef926-163">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="ef926-164"><a name="gw"></a>Utwórz bramę usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ef926-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="ef926-165">Aby uzyskać więcej informacji o konfiguracji bramy ExpressRoute hello, zobacz [konfiguracji bramy ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ef926-165">For more information about hello ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="ef926-166">Witaj GatewaySKU musi być *standardowe*, *wysokowydajnej*, lub *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="ef926-166">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="ef926-167">Połącz obwodu ExpressRoute toohello hello ExpressRoute bramy.</span><span class="sxs-lookup"><span data-stu-id="ef926-167">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="ef926-168">Po wykonaniu tego kroku hello połączenie między siecią lokalną a Azure za pośrednictwem usługi ExpressRoute, zostanie nawiązane.</span><span class="sxs-lookup"><span data-stu-id="ef926-168">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="ef926-169">Aby uzyskać więcej informacji na temat operacji łączenia hello zobacz [tooExpressRoute łącze sieci wirtualnych](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ef926-169">For more information about hello link operation, see [Link VNets tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="ef926-170"><a name="vpngw"></a>Następnie utwórz bramę sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="ef926-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="ef926-171">Aby uzyskać więcej informacji o konfiguracji bramy sieci VPN hello, zobacz [Konfigurowanie sieci wirtualnej przy użyciu połączenia lokacja-lokacja](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ef926-171">For more information about hello VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="ef926-172">Witaj GatewaySKU musi być *standardowe*, *wysokowydajnej*, lub *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="ef926-172">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="ef926-173">Witaj VpnType musi *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="ef926-173">hello VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="ef926-174">Brama sieci VPN platformy Azure obsługuje protokół routingu BGP.</span><span class="sxs-lookup"><span data-stu-id="ef926-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="ef926-175">Można określić numeru ASN (AS Number) dla tej sieci wirtualnej przez dodanie przełącznika - Asn hello hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="ef926-175">You can specify ASN (AS Number) for that Virtual Network by adding hello -Asn switch in hello following command.</span></span> <span data-ttu-id="ef926-176">Ten parametr nie został podany będzie tooAS domyślny numer 65515.</span><span class="sxs-lookup"><span data-stu-id="ef926-176">Not specifying that parameter will default tooAS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="ef926-177">Witaj BGP komunikacja równorzędna IP i hello jako numer używanego dla bramy sieci VPN hello $azureVpn.BgpSettings.BgpPeeringAddress i $azureVpn.BgpSettings.Asn Azure można znaleźć.</span><span class="sxs-lookup"><span data-stu-id="ef926-177">You can find hello BGP peering IP and hello AS number that Azure uses for hello VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="ef926-178">Aby uzyskać więcej informacji, zobacz [Konfigurowanie protokołu BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) dla bramy usługi Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="ef926-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="ef926-179">Utwórz obiekt bramy sieci VPN witryny lokalnej.</span><span class="sxs-lookup"><span data-stu-id="ef926-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="ef926-180">To polecenie nie powoduje skonfigurowania bramy lokalnej sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ef926-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="ef926-181">Zamiast pozwala tooprovide hello bramy lokalnej ustawienia, takie jak hello publicznego adresu IP i hello lokalnej przestrzeni adresów, dzięki czemu hello bramy sieci VPN platformy Azure można łączyć tooit.</span><span class="sxs-lookup"><span data-stu-id="ef926-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
    <span data-ttu-id="ef926-182">W przypadku lokalnego urządzenia sieci VPN obsługuje tylko routing statyczny, można skonfigurować hello trasy statyczne w hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ef926-182">If your local VPN device only supports static routing, you can configure hello static routes in hello following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="ef926-183">Hello BGP obsługuje lokalnego urządzenia sieci VPN, ma tooenable routingu dynamicznego należy tooknow hello BGP równorzędna adresów IP i hello zgodnie z liczbą, która Twojej lokalnej sieci VPN korzysta z urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ef926-183">If your local VPN device supports hello BGP and you want tooenable dynamic routing, you need tooknow hello BGP peering IP and hello AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="ef926-184">Konfigurowanie bramy lokalnej sieci VPN urządzenia tooconnect toohello nowej sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ef926-184">Configure your local VPN device tooconnect toohello new Azure VPN gateway.</span></span> <span data-ttu-id="ef926-185">Więcej informacji na temat konfigurowania urządzenia VPN znajduje się w artykule [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md) (Konfigurowanie urządzenia VPN).</span><span class="sxs-lookup"><span data-stu-id="ef926-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="ef926-186">Łącze hello bramy sieci VPN typu lokacja-lokacja w Azure toohello bramy lokalnej.</span><span class="sxs-lookup"><span data-stu-id="ef926-186">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="ef926-187"><a name="add"></a>tooconfigure ważnych połączeń dla już istniejącej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ef926-187"><a name="add"></a>tooconfigure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="ef926-188">Jeśli masz istniejącą sieć wirtualną, należy sprawdzić rozmiar podsieci bramy hello.</span><span class="sxs-lookup"><span data-stu-id="ef926-188">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="ef926-189">Podsieć bramy hello jest /28 lub /29, należy najpierw usunąć bramę sieci wirtualnej hello, Zwiększ rozmiar podsieci bramy hello.</span><span class="sxs-lookup"><span data-stu-id="ef926-189">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="ef926-190">Witaj kroki opisane w tej sekcji opisano sposób toodo który.</span><span class="sxs-lookup"><span data-stu-id="ef926-190">hello steps in this section show you how toodo that.</span></span>

<span data-ttu-id="ef926-191">Jeśli podsieć bramy hello jest /27 lub większy i sieć wirtualna hello jest połączony za pośrednictwem usługi ExpressRoute, można pominąć kroki hello poniżej i przejść za["Krok 6 — utworzenie bramy sieci VPN typu lokacja-lokacja"](#vpngw) hello w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef926-191">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="ef926-192">Po usunięciu hello istniejącą bramę lokalnego lokalnej spowoduje utratę hello sieci wirtualnej tooyour połączenia podczas pracy w tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ef926-192">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="ef926-193">Będziesz potrzebować tooinstall hello najnowszą wersję hello poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef926-193">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ef926-194">Aby uzyskać więcej informacji na temat instalacji poleceń cmdlet, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ef926-194">For more information about installing cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="ef926-195">poleceń cmdlet Hello, której użyjesz dla tej konfiguracji mogą być nieco inne niż co można zapoznać się z.</span><span class="sxs-lookup"><span data-stu-id="ef926-195">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="ef926-196">Polecenia cmdlet hello toouse się, że można określić w tej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="ef926-196">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="ef926-197">Usuń hello istniejącą bramę usługi ExpressRoute lub sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="ef926-197">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="ef926-198">Usuń podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="ef926-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="ef926-199">Dodaj podsieć bramy o wartości /27 lub większej.</span><span class="sxs-lookup"><span data-stu-id="ef926-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ef926-200">Jeśli masz za mało adresów IP pozostałych w rozmiar podsieci bramy sieci wirtualnej tooincrease hello należy tooadd więcej przestrzeni adresów IP.</span><span class="sxs-lookup"><span data-stu-id="ef926-200">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="ef926-201">Zapisz hello konfigurację sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ef926-201">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="ef926-202">Na tym etapie masz sieć wirtualną bez bram.</span><span class="sxs-lookup"><span data-stu-id="ef926-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="ef926-203">toocreate nowych bram i zakończenie połączenia, można przystąpić do [krok 4 — Utwórz bramę usługi ExpressRoute](#gw), liczba znalezionych w hello poprzedzających zestaw kroków.</span><span class="sxs-lookup"><span data-stu-id="ef926-203">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a><span data-ttu-id="ef926-204">Brama sieci VPN toohello konfiguracji punkt lokacja tooadd</span><span class="sxs-lookup"><span data-stu-id="ef926-204">tooadd point-to-site configuration toohello VPN gateway</span></span>
<span data-ttu-id="ef926-205">Można wykonać procedurę hello poniżej bramy sieci VPN tooyour konfiguracji tooadd punkt-lokacja w Instalatorze współistnienie.</span><span class="sxs-lookup"><span data-stu-id="ef926-205">You can follow hello steps below tooadd Point-to-Site configuration tooyour VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="ef926-206">Dodaj pulę adresów klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ef926-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="ef926-207">Przekaż hello VPN głównego certyfikatu tooAzure dla bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="ef926-207">Upload hello VPN root certificate tooAzure for your VPN gateway.</span></span> <span data-ttu-id="ef926-208">W tym przykładzie zakłada się, że ten certyfikat główny hello jest przechowywany w hello komputera lokalnego, gdy są uruchamiane hello następującego polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef926-208">In this example, it's assumed that hello root certificate is stored in hello local machine where hello following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="ef926-209">Więcej informacji na temat sieci VPN typu punkt-lokacja znajduje się w artykule [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) (Konfigurowanie połączenia typu punkt-lokacja).</span><span class="sxs-lookup"><span data-stu-id="ef926-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef926-210">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef926-210">Next steps</span></span>
<span data-ttu-id="ef926-211">Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="ef926-211">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
