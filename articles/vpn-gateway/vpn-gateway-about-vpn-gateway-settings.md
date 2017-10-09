---
title: "Ustawienia bramy aaaVPN Azure połączeń między różnymi lokalizacjami | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o ustawieniach bramy sieci VPN dla bramy sieci wirtualnej platformy Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="efed1-103">Ustawienia konfiguracji bramy sieci VPN — informacje</span><span class="sxs-lookup"><span data-stu-id="efed1-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="efed1-104">Brama sieci VPN jest typu bramy sieci wirtualnej, która wysyła szyfrowanego ruchu sieciowego między sieci wirtualnej i Twojej lokalizacji lokalnej przez publicznego połączenia.</span><span class="sxs-lookup"><span data-stu-id="efed1-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="efed1-105">Umożliwia także ruchu toosend bramy sieci VPN między sieciami wirtualnymi w hello Azure sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="efed1-105">You can also use a VPN gateway toosend traffic between virtual networks across hello Azure backbone.</span></span>

<span data-ttu-id="efed1-106">Połączenie bramy sieci VPN zależy od konfiguracji hello wielu zasobów, z których każdy zawiera konfigurowalnych ustawień.</span><span class="sxs-lookup"><span data-stu-id="efed1-106">A VPN gateway connection relies on hello configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="efed1-107">Witaj sekcje w tym artykule omówiono w nim hello zasoby i ustawienia, które dotyczą tooa bramy sieci VPN do sieci wirtualnej utworzonej w modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="efed1-107">hello sections in this article discuss hello resources and settings that relate tooa VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="efed1-108">Dla każdego połączenia rozwiązania hello można znaleźć opisy i diagramy topologii [o bramy sieci VPN](vpn-gateway-about-vpngateways.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="efed1-108">You can find descriptions and topology diagrams for each connection solution in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="efed1-109"><a name="gwtype"></a>Typy bramy</span><span class="sxs-lookup"><span data-stu-id="efed1-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="efed1-110">Każdej sieci wirtualnej może istnieć tylko jedna brama sieci wirtualnej każdego typu.</span><span class="sxs-lookup"><span data-stu-id="efed1-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="efed1-111">Podczas tworzenia bramy sieci wirtualnej, należy typu bramy hello są poprawne dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="efed1-111">When you are creating a virtual network gateway, you must make sure that hello gateway type is correct for your configuration.</span></span>

<span data-ttu-id="efed1-112">Dostępne wartości elementu GatewayType - Hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="efed1-112">hello available values for -GatewayType are:</span></span>

* <span data-ttu-id="efed1-113">Vpn</span><span class="sxs-lookup"><span data-stu-id="efed1-113">Vpn</span></span>
* <span data-ttu-id="efed1-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="efed1-114">ExpressRoute</span></span>

<span data-ttu-id="efed1-115">Brama sieci VPN wymaga hello `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="efed1-115">A VPN gateway requires hello `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="efed1-116">Przykład:</span><span class="sxs-lookup"><span data-stu-id="efed1-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="efed1-117"><a name="gwsku"></a>Jednostki SKU bramy</span><span class="sxs-lookup"><span data-stu-id="efed1-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a><span data-ttu-id="efed1-118">Konfigurowanie bramy hello jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="efed1-118">Configure hello gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="efed1-119">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="efed1-119">Azure portal</span></span>

<span data-ttu-id="efed1-120">Jeśli używasz hello toocreate portalu usługi Azure Resource Manager bramę sieci wirtualnej, można wybrać jednostka SKU bramy hello za pomocą listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="efed1-120">If you use hello Azure portal toocreate a Resource Manager virtual network gateway, you can select hello gateway SKU by using hello dropdown.</span></span> <span data-ttu-id="efed1-121">dostępne są opcje Hello odpowiada toohello typu bramy i wybranego typu sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="efed1-121">hello options you are presented with correspond toohello Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="efed1-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="efed1-122">PowerShell</span></span>

<span data-ttu-id="efed1-123">Witaj poniższym przykładzie programu PowerShell określa hello `-GatewaySku` jako VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="efed1-123">hello following PowerShell example specifies hello `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="efed1-124"><a name="resize"></a>Zmień (rozmiar) jednostka SKU bramy</span><span class="sxs-lookup"><span data-stu-id="efed1-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="efed1-125">Jeśli chcesz tooupgrade Twojego tooa jednostki SKU bramy SKU bardziej wydajne, można użyć hello `Resize-AzureRmVirtualNetworkGateway` polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="efed1-125">If you want tooupgrade your gateway SKU tooa more powerful SKU, you can use hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="efed1-126">Możesz również obniżyć rozmiar jednostki SKU bramy hello za pomocą tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="efed1-126">You can also downgrade hello gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="efed1-127">Poniższy przykład PowerShell Hello pokazuje bramy SKU zmieniany tooVpnGw2.</span><span class="sxs-lookup"><span data-stu-id="efed1-127">hello following PowerShell example shows a gateway SKU being resized tooVpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="efed1-128"><a name="connectiontype"></a>Typy połączeń</span><span class="sxs-lookup"><span data-stu-id="efed1-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="efed1-129">W modelu wdrażania usługi Resource Manager hello każdej konfiguracji wymaga typu połączenia bramy określonej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="efed1-129">In hello Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="efed1-130">Witaj PowerShell Menedżera zasobów dostępnych wartości dla `-ConnectionType` są:</span><span class="sxs-lookup"><span data-stu-id="efed1-130">hello available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="efed1-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="efed1-131">IPsec</span></span>
* <span data-ttu-id="efed1-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="efed1-132">Vnet2Vnet</span></span>
* <span data-ttu-id="efed1-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="efed1-133">ExpressRoute</span></span>
* <span data-ttu-id="efed1-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="efed1-134">VPNClient</span></span>

<span data-ttu-id="efed1-135">W hello poniższy przykład programu PowerShell, utworzymy połączenia S2S, który wymaga typu połączenia hello *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="efed1-135">In hello following PowerShell example, we create a S2S connection that requires hello connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="efed1-136"><a name="vpntype"></a>Typy z siecią VPN</span><span class="sxs-lookup"><span data-stu-id="efed1-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="efed1-137">Podczas tworzenia bramy sieci wirtualnej hello konfiguracji bramy sieci VPN, należy określić typ sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="efed1-137">When you create hello virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="efed1-138">Witaj typ sieci VPN jest zależna od topologii połączenia hello, które mają toocreate.</span><span class="sxs-lookup"><span data-stu-id="efed1-138">hello VPN type that you choose depends on hello connection topology that you want toocreate.</span></span> <span data-ttu-id="efed1-139">Na przykład połączeń P2S wymaga typu RouteBased sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="efed1-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="efed1-140">Typ sieci VPN można również są zależne od sprzętu hello, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="efed1-140">A VPN type can also depend on hello hardware that you are using.</span></span> <span data-ttu-id="efed1-141">Konfiguracje S2S wymagają urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="efed1-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="efed1-142">Niektóre urządzenia sieci VPN obsługują tylko określonego typu sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="efed1-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="efed1-143">Hello wybranego typu sieci VPN musi spełniać wszystkie wymagania połączenia hello hello rozwiązania, które chcesz toocreate.</span><span class="sxs-lookup"><span data-stu-id="efed1-143">hello VPN type you select must satisfy all hello connection requirements for hello solution you want toocreate.</span></span> <span data-ttu-id="efed1-144">Na przykład, jeśli chcesz toocreate połączenia bramy sieci VPN S2S i połączenia bramy sieci VPN P2S hello tej samej sieci wirtualnej, należy użyć typu sieci VPN *RouteBased* ponieważ P2S wymaga typu RouteBased sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="efed1-144">For example, if you want toocreate a S2S VPN gateway connection and a P2S VPN gateway connection for hello same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="efed1-145">Musisz także tooverify, że urządzenie sieci VPN obsługiwane połączenia sieci VPN typu RouteBased.</span><span class="sxs-lookup"><span data-stu-id="efed1-145">You would also need tooverify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="efed1-146">Po utworzeniu bramy sieci wirtualnej nie można zmienić typu sieci VPN hello.</span><span class="sxs-lookup"><span data-stu-id="efed1-146">Once a virtual network gateway has been created, you can't change hello VPN type.</span></span> <span data-ttu-id="efed1-147">Masz toodelete hello bramy sieci wirtualnej i Utwórz nowe.</span><span class="sxs-lookup"><span data-stu-id="efed1-147">You have toodelete hello virtual network gateway and create a new one.</span></span> <span data-ttu-id="efed1-148">Istnieją dwa typy sieci VPN:</span><span class="sxs-lookup"><span data-stu-id="efed1-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="efed1-149">Witaj poniższym przykładzie programu PowerShell określa hello `-VpnType` jako *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="efed1-149">hello following PowerShell example specifies hello `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="efed1-150">Podczas tworzenia bramy, należy się upewnić, że hello - VpnType są poprawne dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="efed1-150">When you are creating a gateway, you must make sure that hello -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="efed1-151"><a name="requirements"></a>Wymagania dotyczące bramy</span><span class="sxs-lookup"><span data-stu-id="efed1-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="efed1-152"><a name="gwsub"></a>Podsieć bramy</span><span class="sxs-lookup"><span data-stu-id="efed1-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="efed1-153">Przed utworzeniem bramy sieci VPN, należy utworzyć podsieć bramy.</span><span class="sxs-lookup"><span data-stu-id="efed1-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="efed1-154">podsieć bramy Hello zawiera adresy IP hello tego hello bramy sieci wirtualnej maszyny wirtualne i usługi użycia.</span><span class="sxs-lookup"><span data-stu-id="efed1-154">hello gateway subnet contains hello IP addresses that hello virtual network gateway VMs and services use.</span></span> <span data-ttu-id="efed1-155">Podczas tworzenia bramy sieci wirtualnej bramy maszyny wirtualne są wdrożone toohello podsieć bramy i skonfigurować ustawienia bramy sieci VPN hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="efed1-155">When you create your virtual network gateway, gateway VMs are deployed toohello gateway subnet and configured with hello required VPN gateway settings.</span></span> <span data-ttu-id="efed1-156">Nigdy nie należy wdrożyć podsieć bramy toohello cokolwiek innego (na przykład kolejnych maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="efed1-156">You must never deploy anything else (for example, additional VMs) toohello gateway subnet.</span></span> <span data-ttu-id="efed1-157">podsieć bramy Hello muszą nosić nazwy "GatewaySubnet" toowork poprawnie.</span><span class="sxs-lookup"><span data-stu-id="efed1-157">hello gateway subnet must be named 'GatewaySubnet' toowork properly.</span></span> <span data-ttu-id="efed1-158">Nazw podsieci bramy hello umożliwia "GatewaySubnet" Azure znać to jest brama sieci wirtualnej hello toodeploy hello podsieci maszyn wirtualnych i usług do.</span><span class="sxs-lookup"><span data-stu-id="efed1-158">Naming hello gateway subnet 'GatewaySubnet' lets Azure know that this is hello subnet toodeploy hello virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="efed1-159">Podczas tworzenia podsieci bramy hello Określ zawiera hello liczbę adresów IP, które hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="efed1-159">When you create hello gateway subnet, you specify hello number of IP addresses that hello subnet contains.</span></span> <span data-ttu-id="efed1-160">Witaj adresów IP w podsieci bramy hello są maszyny wirtualne bramy toohello przydzielone i bramą usługi.</span><span class="sxs-lookup"><span data-stu-id="efed1-160">hello IP addresses in hello gateway subnet are allocated toohello gateway VMs and gateway services.</span></span> <span data-ttu-id="efed1-161">Niektóre konfiguracje wymagają więcej adresów IP od innych.</span><span class="sxs-lookup"><span data-stu-id="efed1-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="efed1-162">Spójrz na powitania instrukcje dotyczące konfiguracji hello mają toocreate i sprawdź, czy podsieci bramy hello ma toocreate spełnia te wymagania.</span><span class="sxs-lookup"><span data-stu-id="efed1-162">Look at hello instructions for hello configuration that you want toocreate and verify that hello gateway subnet you want toocreate meets those requirements.</span></span> <span data-ttu-id="efed1-163">Ponadto można toomake się, że podsieć bramy zawiera za mało IP adresów tooaccommodate możliwe przyszłych dodatkowe konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="efed1-163">Additionally, you may want toomake sure your gateway subnet contains enough IP addresses tooaccommodate possible future additional configurations.</span></span> <span data-ttu-id="efed1-164">Podczas tworzenia podsieci bramy jak /29, zaleca się utworzenie podsieć bramy /28 i większych (/ 28, /27, /26 itp.).</span><span class="sxs-lookup"><span data-stu-id="efed1-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="efed1-165">W ten sposób dodawania funkcji w przyszłości, hello możesz nie mieć tootear bramy sieci, a następnie usuń i Utwórz ponownie tooallow podsieci bramy hello więcej adresów IP.</span><span class="sxs-lookup"><span data-stu-id="efed1-165">That way, if you add functionality in hello future, you won't have tootear your gateway, then delete and recreate hello gateway subnet tooallow for more IP addresses.</span></span>

<span data-ttu-id="efed1-166">Witaj poniższym przykładzie programu PowerShell Menedżera zasobów zawiera podsieć bramy o nazwie GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="efed1-166">hello following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="efed1-167">Można zauważyć, że w notacji CIDR hello określa /27, co umożliwia obsługę za mało adresów IP w przypadku większości konfiguracji, które obecnie istnieją.</span><span class="sxs-lookup"><span data-stu-id="efed1-167">You can see hello CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="efed1-168"><a name="lng"></a>Bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="efed1-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="efed1-169">Podczas tworzenia konfiguracji bramy sieci VPN, Brama sieci lokalnej hello często reprezentuje Twojej lokalizacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="efed1-169">When creating a VPN gateway configuration, hello local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="efed1-170">W hello klasycznego modelu wdrażania hello bramy sieci lokalnej została określona tooas lokacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="efed1-170">In hello classic deployment model, hello local network gateway was referred tooas a Local Site.</span></span> 

<span data-ttu-id="efed1-171">Nadaj nazwę bramy sieci lokalnej hello, hello publiczny adres IP urządzenia sieci VPN lokalne powitania i określ hello prefiksy adresów, które znajdują się w lokalizacji lokalnej hello.</span><span class="sxs-lookup"><span data-stu-id="efed1-171">You give hello local network gateway a name, hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are located on hello on-premises location.</span></span> <span data-ttu-id="efed1-172">Azure analizuje hello prefiksy adresów docelowy dla ruchu sieciowego, sprawdza konfigurację hello, określony dla bramy sieci lokalnej i odpowiednio kieruje pakiety.</span><span class="sxs-lookup"><span data-stu-id="efed1-172">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="efed1-173">Należy także określić bramy sieci lokalnej dla konfiguracji do wirtualnymi, które używają połączenia bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="efed1-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="efed1-174">Poniższy przykład PowerShell Hello tworzy nową bramę sieci lokalnej:</span><span class="sxs-lookup"><span data-stu-id="efed1-174">hello following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="efed1-175">Czasami trzeba ustawienia bramy sieci lokalnej hello toomodify.</span><span class="sxs-lookup"><span data-stu-id="efed1-175">Sometimes you need toomodify hello local network gateway settings.</span></span> <span data-ttu-id="efed1-176">Na przykład podczas dodawania lub modyfikowania zakres adresów hello, lub jeśli zmieni adres IP hello hello urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="efed1-176">For example, when you add or modify hello address range, or if hello IP address of hello VPN device changes.</span></span> <span data-ttu-id="efed1-177">Klasyczne sieci wirtualnej można zmienić te ustawienia w portalu klasycznym hello na stronie sieci lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="efed1-177">For a classic VNet, you can change these settings in hello classic portal on hello Local Networks page.</span></span> <span data-ttu-id="efed1-178">Dla Menedżera zasobów, zobacz [zmodyfikować ustawienia bramy sieci lokalnej za pomocą programu PowerShell](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="efed1-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="efed1-179"><a name="resources"></a>Polecenia cmdlet programu PowerShell i interfejsów API REST</span><span class="sxs-lookup"><span data-stu-id="efed1-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="efed1-180">Aby uzyskać dodatkowe zasoby techniczne i szczegółowe wymagania składni, korzystając z interfejsów API REST, poleceń cmdlet programu PowerShell lub interfejsu wiersza polecenia Azure konfiguracji bramy sieci VPN, zobacz hello następujące strony:</span><span class="sxs-lookup"><span data-stu-id="efed1-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="efed1-181">**Wdrożenie klasyczne**</span><span class="sxs-lookup"><span data-stu-id="efed1-181">**Classic**</span></span> | <span data-ttu-id="efed1-182">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="efed1-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="efed1-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="efed1-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="efed1-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="efed1-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="efed1-185">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="efed1-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="efed1-186">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="efed1-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="efed1-187">Nieobsługiwane</span><span class="sxs-lookup"><span data-stu-id="efed1-187">Not supported</span></span> | [<span data-ttu-id="efed1-188">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="efed1-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="efed1-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="efed1-189">Next steps</span></span>

<span data-ttu-id="efed1-190">Aby uzyskać więcej informacji o konfiguracjach dostępnych połączeń, zobacz [o bramy sieci VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="efed1-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>