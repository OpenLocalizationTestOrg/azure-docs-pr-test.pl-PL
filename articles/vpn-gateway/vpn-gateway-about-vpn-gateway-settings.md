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
# <a name="about-vpn-gateway-configuration-settings"></a>Ustawienia konfiguracji bramy sieci VPN — informacje

Brama sieci VPN jest typu bramy sieci wirtualnej, która wysyła szyfrowanego ruchu sieciowego między sieci wirtualnej i Twojej lokalizacji lokalnej przez publicznego połączenia. Umożliwia także ruchu toosend bramy sieci VPN między sieciami wirtualnymi w hello Azure sieci szkieletowej.

Połączenie bramy sieci VPN zależy od konfiguracji hello wielu zasobów, z których każdy zawiera konfigurowalnych ustawień. Witaj sekcje w tym artykule omówiono w nim hello zasoby i ustawienia, które dotyczą tooa bramy sieci VPN do sieci wirtualnej utworzonej w modelu wdrażania usługi Resource Manager. Dla każdego połączenia rozwiązania hello można znaleźć opisy i diagramy topologii [o bramy sieci VPN](vpn-gateway-about-vpngateways.md) artykułu.

## <a name="gwtype"></a>Typy bramy

Każdej sieci wirtualnej może istnieć tylko jedna brama sieci wirtualnej każdego typu. Podczas tworzenia bramy sieci wirtualnej, należy typu bramy hello są poprawne dla danej konfiguracji.

Dostępne wartości elementu GatewayType - Hello są następujące:

* Vpn
* ExpressRoute

Brama sieci VPN wymaga hello `-GatewayType` *Vpn*.

Przykład:

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>Jednostki SKU bramy

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a>Konfigurowanie bramy hello jednostki SKU

#### <a name="azure-portal"></a>Azure Portal

Jeśli używasz hello toocreate portalu usługi Azure Resource Manager bramę sieci wirtualnej, można wybrać jednostka SKU bramy hello za pomocą listy rozwijanej hello. dostępne są opcje Hello odpowiada toohello typu bramy i wybranego typu sieci VPN.

#### <a name="powershell"></a>PowerShell

Witaj poniższym przykładzie programu PowerShell określa hello `-GatewaySku` jako VpnGw1.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>Zmień (rozmiar) jednostka SKU bramy

Jeśli chcesz tooupgrade Twojego tooa jednostki SKU bramy SKU bardziej wydajne, można użyć hello `Resize-AzureRmVirtualNetworkGateway` polecenia cmdlet programu PowerShell. Możesz również obniżyć rozmiar jednostki SKU bramy hello za pomocą tego polecenia cmdlet.

Poniższy przykład PowerShell Hello pokazuje bramy SKU zmieniany tooVpnGw2.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>Typy połączeń

W modelu wdrażania usługi Resource Manager hello każdej konfiguracji wymaga typu połączenia bramy określonej sieci wirtualnej. Witaj PowerShell Menedżera zasobów dostępnych wartości dla `-ConnectionType` są:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

W hello poniższy przykład programu PowerShell, utworzymy połączenia S2S, który wymaga typu połączenia hello *IPsec*.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>Typy z siecią VPN

Podczas tworzenia bramy sieci wirtualnej hello konfiguracji bramy sieci VPN, należy określić typ sieci VPN. Witaj typ sieci VPN jest zależna od topologii połączenia hello, które mają toocreate. Na przykład połączeń P2S wymaga typu RouteBased sieci VPN. Typ sieci VPN można również są zależne od sprzętu hello, którego używasz. Konfiguracje S2S wymagają urządzenia sieci VPN. Niektóre urządzenia sieci VPN obsługują tylko określonego typu sieci VPN.

Hello wybranego typu sieci VPN musi spełniać wszystkie wymagania połączenia hello hello rozwiązania, które chcesz toocreate. Na przykład, jeśli chcesz toocreate połączenia bramy sieci VPN S2S i połączenia bramy sieci VPN P2S hello tej samej sieci wirtualnej, należy użyć typu sieci VPN *RouteBased* ponieważ P2S wymaga typu RouteBased sieci VPN. Musisz także tooverify, że urządzenie sieci VPN obsługiwane połączenia sieci VPN typu RouteBased. 

Po utworzeniu bramy sieci wirtualnej nie można zmienić typu sieci VPN hello. Masz toodelete hello bramy sieci wirtualnej i Utwórz nowe. Istnieją dwa typy sieci VPN:

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

Witaj poniższym przykładzie programu PowerShell określa hello `-VpnType` jako *RouteBased*. Podczas tworzenia bramy, należy się upewnić, że hello - VpnType są poprawne dla danej konfiguracji.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>Wymagania dotyczące bramy

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>Podsieć bramy

Przed utworzeniem bramy sieci VPN, należy utworzyć podsieć bramy. podsieć bramy Hello zawiera adresy IP hello tego hello bramy sieci wirtualnej maszyny wirtualne i usługi użycia. Podczas tworzenia bramy sieci wirtualnej bramy maszyny wirtualne są wdrożone toohello podsieć bramy i skonfigurować ustawienia bramy sieci VPN hello wymagane. Nigdy nie należy wdrożyć podsieć bramy toohello cokolwiek innego (na przykład kolejnych maszyn wirtualnych). podsieć bramy Hello muszą nosić nazwy "GatewaySubnet" toowork poprawnie. Nazw podsieci bramy hello umożliwia "GatewaySubnet" Azure znać to jest brama sieci wirtualnej hello toodeploy hello podsieci maszyn wirtualnych i usług do.

Podczas tworzenia podsieci bramy hello Określ zawiera hello liczbę adresów IP, które hello podsieci. Witaj adresów IP w podsieci bramy hello są maszyny wirtualne bramy toohello przydzielone i bramą usługi. Niektóre konfiguracje wymagają więcej adresów IP od innych. Spójrz na powitania instrukcje dotyczące konfiguracji hello mają toocreate i sprawdź, czy podsieci bramy hello ma toocreate spełnia te wymagania. Ponadto można toomake się, że podsieć bramy zawiera za mało IP adresów tooaccommodate możliwe przyszłych dodatkowe konfiguracje. Podczas tworzenia podsieci bramy jak /29, zaleca się utworzenie podsieć bramy /28 i większych (/ 28, /27, /26 itp.). W ten sposób dodawania funkcji w przyszłości, hello możesz nie mieć tootear bramy sieci, a następnie usuń i Utwórz ponownie tooallow podsieci bramy hello więcej adresów IP.

Witaj poniższym przykładzie programu PowerShell Menedżera zasobów zawiera podsieć bramy o nazwie GatewaySubnet. Można zauważyć, że w notacji CIDR hello określa /27, co umożliwia obsługę za mało adresów IP w przypadku większości konfiguracji, które obecnie istnieją.

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>Bramy sieci lokalnej

Podczas tworzenia konfiguracji bramy sieci VPN, Brama sieci lokalnej hello często reprezentuje Twojej lokalizacji lokalnej. W hello klasycznego modelu wdrażania hello bramy sieci lokalnej została określona tooas lokacji lokalnej. 

Nadaj nazwę bramy sieci lokalnej hello, hello publiczny adres IP urządzenia sieci VPN lokalne powitania i określ hello prefiksy adresów, które znajdują się w lokalizacji lokalnej hello. Azure analizuje hello prefiksy adresów docelowy dla ruchu sieciowego, sprawdza konfigurację hello, określony dla bramy sieci lokalnej i odpowiednio kieruje pakiety. Należy także określić bramy sieci lokalnej dla konfiguracji do wirtualnymi, które używają połączenia bramy sieci VPN.

Poniższy przykład PowerShell Hello tworzy nową bramę sieci lokalnej:

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

Czasami trzeba ustawienia bramy sieci lokalnej hello toomodify. Na przykład podczas dodawania lub modyfikowania zakres adresów hello, lub jeśli zmieni adres IP hello hello urządzenia sieci VPN. Klasyczne sieci wirtualnej można zmienić te ustawienia w portalu klasycznym hello na stronie sieci lokalne powitania. Dla Menedżera zasobów, zobacz [zmodyfikować ustawienia bramy sieci lokalnej za pomocą programu PowerShell](vpn-gateway-modify-local-network-gateway.md).

## <a name="resources"></a>Polecenia cmdlet programu PowerShell i interfejsów API REST

Aby uzyskać dodatkowe zasoby techniczne i szczegółowe wymagania składni, korzystając z interfejsów API REST, poleceń cmdlet programu PowerShell lub interfejsu wiersza polecenia Azure konfiguracji bramy sieci VPN, zobacz hello następujące strony:

| **Wdrożenie klasyczne** | **Resource Manager** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [Interfejs API REST](https://msdn.microsoft.com/library/jj154113) |[Interfejs API REST](/rest/api/network/virtualnetworkgateways) |
| Nieobsługiwane | [Interfejs wiersza polecenia platformy Azure](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji o konfiguracjach dostępnych połączeń, zobacz [o bramy sieci VPN](vpn-gateway-about-vpngateways.md).