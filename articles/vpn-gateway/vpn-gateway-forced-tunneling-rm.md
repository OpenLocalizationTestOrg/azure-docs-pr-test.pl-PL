---
title: "Skonfigurować wymuszanie tunelowania dla połączenia usługi Azure Site to Site: Resource Manager | Dokumentacja firmy Microsoft"
description: "Jak tooredirect lub \"force\" wszystkie powiązane z Internetu ruchu wstecz tooyour lokalizacji lokalnej."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a><span data-ttu-id="b6a3c-103">Skonfiguruj tunelowanie wymuszone przy użyciu modelu wdrażania usługi Azure Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="b6a3c-103">Configure forced tunneling using hello Azure Resource Manager deployment model</span></span>

<span data-ttu-id="b6a3c-104">Wymuszone tunelowanie umożliwia przekierowanie lub "force" wszystkie powiązane z Internetu ruchu wstecz tooyour lokalnej lokalizacji za pośrednictwem tunelu VPN typu lokacja-lokacja dla inspekcji i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="b6a3c-105">Jest to wymagane krytycznych dla większości organizacji IT zasad.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="b6a3c-106">Bez tunelowania wymuszonego ruch do Internetu z maszyn wirtualnych na platformie Azure zawsze przechodzi od infrastruktury sieci platformy Azure bezpośrednio limit toohello Internet, bez tooallow opcji hello możesz ruchu hello tooinspect lub inspekcji.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure always traverses from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="b6a3c-107">Nieautoryzowany dostęp do Internetu potencjalnie może spowodować ujawnienie tooinformation lub inne rodzaje naruszeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

<span data-ttu-id="b6a3c-108">W tym artykule przedstawiono konfigurowanie wymuszonego tunelowania dla sieci wirtualnych utworzonych przy użyciu modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-108">This article walks you through configuring forced tunneling for virtual networks created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="b6a3c-109">Tunelowanie wymuszone można skonfigurować przy użyciu programu PowerShell, nie za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="b6a3c-110">Tooconfigure wymuszonego tunelowania dla hello klasycznego modelu wdrażania, wybierz opcję klasycznego artykułu z następującej listy rozwijanej hello:</span><span class="sxs-lookup"><span data-stu-id="b6a3c-110">If you want tooconfigure forced tunneling for hello classic deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6a3c-111">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="b6a3c-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="b6a3c-112">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b6a3c-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a><span data-ttu-id="b6a3c-113">Około wymuszonego tunelowania</span><span class="sxs-lookup"><span data-stu-id="b6a3c-113">About forced tunneling</span></span>

<span data-ttu-id="b6a3c-114">powitania po diagram ilustruje sposób wymuszonego tunelowania działa.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-114">hello following diagram illustrates how forced tunneling works.</span></span> 

![Wymuszone tunelowanie](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

<span data-ttu-id="b6a3c-116">W przykładzie hello powyżej hello tunelowane nie wymusza podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-116">In hello example above, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="b6a3c-117">Witaj obciążeń w podsieci frontonu hello można kontynuować tooaccept i odpowiada na żądania toocustomer z hello Internet bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-117">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="b6a3c-118">Witaj podsieci w warstwie pośredniej i wewnętrznej bazy danych zostało wymuszone tunelowane.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-118">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="b6a3c-119">Wszystkie połączenia wychodzące z tymi dwiema podsieciami toohello Internet będzie tooan wymuszonym lub ponownie przekierowanego lokacji lokalnej za pośrednictwem jednego powitalne tuneli S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-119">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="b6a3c-120">Pozwala toorestrict i inspekcję dostępu do Internetu na maszynach wirtualnych lub w chmurze usługi na platformie Azure, pozostawiając tooenable architektury usługa wielowarstwowa wymagane.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-120">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="b6a3c-121">Jeśli w sieci wirtualne nie żadne obciążenia internetowy, również można zastosować wymuszonego tunelowania toohello całej sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-121">If there are no Internet-facing workloads in your virtual networks, you also can apply forced tunneling toohello entire virtual networks.</span></span>

## <a name="requirements-and-considerations"></a><span data-ttu-id="b6a3c-122">Wymagania i uwagi</span><span class="sxs-lookup"><span data-stu-id="b6a3c-122">Requirements and considerations</span></span>

<span data-ttu-id="b6a3c-123">Wymuszanie tunelowania na platformie Azure jest skonfigurowana za pośrednictwem sieci wirtualnej trasy zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-123">Forced tunneling in Azure is configured via virtual network user-defined routes.</span></span> <span data-ttu-id="b6a3c-124">Przekierowywanie ruchu tooan w lokalnym witryny jest wyrażona jako brama sieci VPN platformy Azure toohello trasy domyślnej.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-124">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="b6a3c-125">Aby uzyskać więcej informacji dotyczących użytkownika routingu i sieci wirtualnych, zobacz [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6a3c-125">For more information about user-defined routing and virtual networks, see [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

* <span data-ttu-id="b6a3c-126">Każda podsieć sieci wirtualnej ma wbudowane, tabelę routingu systemu.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-126">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="b6a3c-127">Tabela routingu Hello system ma hello następujące trzy grupy tras:</span><span class="sxs-lookup"><span data-stu-id="b6a3c-127">hello system routing table has hello following three groups of routes:</span></span>
  
  * <span data-ttu-id="b6a3c-128">**Tras lokalnych sieci wirtualnej:** bezpośrednio toohello docelowego maszyny wirtualne w hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-128">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="b6a3c-129">**Trasy lokalnymi:** toohello bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-129">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="b6a3c-130">**Trasa domyślna:** bezpośrednio toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-130">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="b6a3c-131">Pakiety przeznaczone toohello prywatnych adresów IP nie pasuje do żadnego hello dwoma poprzednimi trasy są usuwane.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-131">Packets destined toohello private IP addresses not covered by hello previous two routes are dropped.</span></span>
* <span data-ttu-id="b6a3c-132">Ta procedura używa trasy zdefiniowane przez użytkownika (przez) toocreate routingu tooadd tabeli trasy domyślnej, a następnie skojarzyć hello routingu tabeli tooyour sieci wirtualnej adresy podsieci używane tooenable wymuszone tunelowanie korzysta z tych podsieci.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-132">This procedure uses user-defined routes (UDR) toocreate a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="b6a3c-133">Tunelowanie wymuszone, muszą być skojarzone z sieci wirtualnej, który ma bramy sieci VPN opartej na trasach.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-133">Forced tunneling must be associated with a VNet that has a route-based VPN gateway.</span></span> <span data-ttu-id="b6a3c-134">Należy tooset "domyślnej witryny" między sieci wirtualnej podłączonej toohello hello między lokalizacjami lokalnych witryn.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-134">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span> <span data-ttu-id="b6a3c-135">Ponadto hello w lokalnym urządzenie sieci VPN musi być skonfigurowane przy użyciu 0.0.0.0/0 jako selektorów ruchu.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-135">Also, hello on-premises VPN device must be configured using 0.0.0.0/0 as traffic selectors.</span></span> 
* <span data-ttu-id="b6a3c-136">ExpressRoute wymuszonego tunelowania nie jest skonfigurowany za pomocą ten mechanizm, ale zamiast tego jest włączana przez anonsuje trasę domyślną za pośrednictwem hello BGP usługi ExpressRoute sesje komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-136">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="b6a3c-137">Aby uzyskać więcej informacji, zobacz hello [dokumentacja usługi ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).</span><span class="sxs-lookup"><span data-stu-id="b6a3c-137">For more information, see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/).</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="b6a3c-138">Przegląd konfiguracji</span><span class="sxs-lookup"><span data-stu-id="b6a3c-138">Configuration overview</span></span>

<span data-ttu-id="b6a3c-139">Witaj procedury ułatwia tworzenie grupy zasobów i sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-139">hello following procedure helps you create a resource group and a VNet.</span></span> <span data-ttu-id="b6a3c-140">Następnie będzie utworzyć bramę sieci VPN i skonfigurować wymuszanie tunelowania.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-140">You'll then create a VPN gateway and configure forced tunneling.</span></span> <span data-ttu-id="b6a3c-141">W tej procedurze hello sieci wirtualnej "Sieci wirtualnej MultiTier" zawiera trzy podsieci: "Frontend", "Midtier" i "Zaplecze", z czterema między lokalizacjami połączeń: "DefaultSiteHQ" i trzy gałęzie.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-141">In this procedure, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend', with four cross-premises connections: 'DefaultSiteHQ', and three Branches.</span></span>

<span data-ttu-id="b6a3c-142">kroki procedury Hello ustawiono hello "DefaultSiteHQ" hello domyślne lokacji połączenie dla wymuszone tunelowanie i skonfigurować hello "Midtier" i "Zaplecze" podsieci toouse wymuszonego tunelowania.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-142">hello procedure steps set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello 'Midtier' and 'Backend' subnets toouse forced tunneling.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b6a3c-143">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b6a3c-143">Before you begin</span></span>

<span data-ttu-id="b6a3c-144">Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-144">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="b6a3c-145">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-145">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="toolog-in"></a><span data-ttu-id="b6a3c-146">toolog w</span><span class="sxs-lookup"><span data-stu-id="b6a3c-146">toolog in</span></span>

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a><span data-ttu-id="b6a3c-147">Konfigurowanie wymuszonego tunelowania</span><span class="sxs-lookup"><span data-stu-id="b6a3c-147">Configure forced tunneling</span></span>

1. <span data-ttu-id="b6a3c-148">Utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-148">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. <span data-ttu-id="b6a3c-149">Tworzenie sieci wirtualnej i określenia podsieci.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-149">Create a virtual network and specify subnets.</span></span>

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. <span data-ttu-id="b6a3c-150">Utwórz hello bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-150">Create hello local network gateways.</span></span>

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. <span data-ttu-id="b6a3c-151">Utwórz regułę trasy hello tabeli i trasy.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-151">Create hello route table and route rule.</span></span>

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. <span data-ttu-id="b6a3c-152">Kojarzenie toohello tabeli tras hello Midtier i podsieci wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-152">Associate hello route table toohello Midtier and Backend subnets.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="b6a3c-153">Utwórz hello bramy z domyślnej witryny.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-153">Create hello Gateway with a default site.</span></span> <span data-ttu-id="b6a3c-154">Ten krok zajmuje niektórych toocomplete czasu, czasami 45 minut lub dłużej, ponieważ są tworzenia i konfigurowania bramy hello.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-154">This step takes some time toocomplete, sometimes 45 minutes or more, because you are creating and configuring hello gateway.</span></span><br> <span data-ttu-id="b6a3c-155">Witaj **- GatewayDefaultSite** jest hello parametrów polecenia cmdlet, umożliwiający hello wymuszone routingu toowork konfiguracji, dlatego podjąć tooconfigure szczególną uwagę prawidłowo tego ustawienia.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-155">hello **-GatewayDefaultSite** is hello cmdlet parameter that allows hello forced routing configuration toowork, so take care tooconfigure this setting properly.</span></span> <span data-ttu-id="b6a3c-156">Ten parametr jest dostępna w programie PowerShell 1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-156">This parameter is available in PowerShell 1.0 or later.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. <span data-ttu-id="b6a3c-157">Nawiązywać połączenia sieci VPN hello lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="b6a3c-157">Establish hello Site-to-Site VPN connections.</span></span>

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```