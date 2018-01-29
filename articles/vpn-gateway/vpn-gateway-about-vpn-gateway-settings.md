---
title: "Ustawienia bramy sieci VPN między lokalizacjami połączenia platformy Azure | Dokumentacja firmy Microsoft"
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
ms.date: 10/12/2017
ms.author: cherylmc
ms.openlocfilehash: d265c72cfc02710afb630f3b8258602c936d1ebc
ms.sourcegitcommit: 1131386137462a8a959abb0f8822d1b329a4e474
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/13/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a>Ustawienia konfiguracji bramy sieci VPN — informacje

Brama sieci VPN jest typu bramy sieci wirtualnej, która wysyła szyfrowanego ruchu sieciowego między sieci wirtualnej i Twojej lokalizacji lokalnej przez publicznego połączenia. Umożliwia także bramy sieci VPN na wysyłanie ruchu między sieciami wirtualnymi w Azure sieci szkieletowej.

Połączenie bramy sieci VPN zależy od konfiguracji wielu zasobów, z których każdy zawiera konfigurowalnych ustawień. Informacje zawarte w tym artykule omówiono w nim, zasoby i ustawienia, które odnoszą się do bramy sieci VPN do sieci wirtualnej utworzonej w modelu wdrażania usługi Resource Manager. Możesz znaleźć opisy i diagramy topologii dla każdego rozwiązania połączenia w [o bramy sieci VPN](vpn-gateway-about-vpngateways.md) artykułu.

## <a name="gwtype"></a>Typy bramy

Każdej sieci wirtualnej może istnieć tylko jedna brama sieci wirtualnej każdego typu. Podczas tworzenia bramy sieci wirtualnej, należy się upewnić, że typ bramy jest poprawny dla danej konfiguracji.

Dostępne wartości elementu GatewayType - są:

* Vpn
* ExpressRoute

Brama sieci VPN wymaga `-GatewayType` *Vpn*.

Przykład:

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>Jednostki SKU bramy

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-the-gateway-sku"></a>Konfigurowanie bramy jednostki SKU

#### <a name="azure-portal"></a>Azure Portal

Jeśli używasz portalu Azure do tworzenia bramy sieci wirtualnej Resource Manager, korzystając z listy rozwijanej można wybrać jednostka SKU bramy. Dostępne są opcje odpowiadają typu bramy i wybranego typu sieci VPN.

#### <a name="powershell"></a>PowerShell

W poniższym przykładzie programu PowerShell Określa `-GatewaySku` jako VpnGw1.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>Zmień (rozmiar) jednostka SKU bramy

Jeśli chcesz uaktualnić jednostka SKU bramy do bardziej zaawansowanych wersji produktu, możesz użyć `Resize-AzureRmVirtualNetworkGateway` polecenia cmdlet programu PowerShell. Możesz również obniżyć bramy, rozmiar jednostki SKU za pomocą tego polecenia cmdlet.

W poniższym przykładzie programu PowerShell pokazano zmieniany na VpnGw2 jednostki SKU bramy.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>Typy połączeń

W modelu wdrażania Menedżera zasobów każdej konfiguracji wymaga typu połączenia bramy określonej sieci wirtualnej. Dostępne wartości opcji `-ConnectionType` w programie PowerShell w usłudze Resource Manager to:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

W poniższym przykładzie programu PowerShell, utworzymy połączeń S2S, który wymaga typu połączenia *IPsec*.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>Typy z siecią VPN

Podczas tworzenia bramy sieci wirtualnej dla konfiguracji bramy sieci VPN, należy określić typ sieci VPN. Możesz wybrać typ sieci VPN zależy od topologii połączenia, który chcesz utworzyć. Na przykład połączeń P2S wymaga typu RouteBased sieci VPN. Typ sieci VPN można również są zależne od sprzętu, którego używasz. Konfiguracje S2S wymagają urządzenia sieci VPN. Niektóre urządzenia sieci VPN obsługują tylko określonego typu sieci VPN.

Wybranego typu sieci VPN musi spełniać wszystkie połączenia wymagania dotyczące rozwiązania się, że chcesz utworzyć. Na przykład, jeśli chcesz utworzyć połączenie bramy sieci S2S VPN i połączenia bramy sieci P2S VPN dla tej samej sieci wirtualnej, można skorzystać typ sieci VPN *RouteBased* ponieważ P2S wymaga typu RouteBased sieci VPN. Należy także sprawdzić, czy urządzenie sieci VPN obsługiwany połączenia sieci VPN typu RouteBased. 

Po utworzeniu bramy sieci wirtualnej nie można zmienić typu sieci VPN. Należy usunąć bramę sieci wirtualnej i Utwórz nowe. Istnieją dwa typy sieci VPN:

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

W poniższym przykładzie programu PowerShell Określa `-VpnType` jako *RouteBased*. Podczas tworzenia bramy musisz upewnić się, że typ -VpnType jest prawidłowy dla danej konfiguracji.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>Wymagania dotyczące bramy

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>Podsieć bramy

Przed utworzeniem bramy sieci VPN, należy utworzyć podsieć bramy. Podsieć bramy zawiera adresy IP, których bramy sieci wirtualnej maszyn wirtualnych i usług. Podczas tworzenia bramy sieci wirtualnej maszyny wirtualne bramy są wdrażane do podsieci bramy i skonfigurowane wymagane ustawienia bramy sieci VPN. Do podsieci bramy nigdy nie należy wdrożyć cokolwiek innego (na przykład kolejnych maszyn wirtualnych). Podsieć bramy musi być o nazwie "GatewaySubnet" działała poprawnie. Nazw podsieci bramy "GatewaySubnet" umożliwia wiedzieli, że jest to podsieci w celu wdrożenia bramy sieci wirtualnej maszyn wirtualnych i usług Azure.

Podczas tworzenia podsieci bramy należy określić liczbę zawartych w niej adresów IP. Adresy IP w podsieci bramy są przydzielone do usługi bramy i maszyny wirtualne bramy. Niektóre konfiguracje wymagają więcej adresów IP od innych. Przyjrzyj się instrukcje dotyczące konfiguracji, który chcesz utworzyć i sprawdź, czy podsieci bramy, w której chcesz utworzyć spełnia te wymagania. Można ponadto upewnij się, że podsieć bramy zawiera za mało adresów IP w celu uwzględnienia możliwych przyszłych dodatkowe konfiguracje. Podczas tworzenia podsieci bramy jak /29, zaleca się utworzenie podsieć bramy /28 i większych (/ 28, /27, /26 itp.). W ten sposób dodania funkcji w przyszłości, nie trzeba usunąć bramy, a następnie usuń i Utwórz ponownie podsieć bramy, aby umożliwić więcej adresów IP.

W poniższym przykładzie programu PowerShell Menedżera zasobów zawiera podsieć bramy o nazwie GatewaySubnet. Można zauważyć, że w notacji CIDR określa /27, co umożliwia obsługę za mało adresów IP w przypadku większości konfiguracji, które obecnie istnieją.

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>Bramy sieci lokalnej

Podczas tworzenia konfiguracji bramy sieci VPN, Brama sieci lokalnej często reprezentuje Twojej lokalizacji lokalnej. W klasycznym modelu wdrażania brama sieci była określana jako lokacja lokalna. 

Nadaj nazwę lokalnego urządzenia sieci VPN, publiczny adres IP bramy sieci lokalnej i określić prefiksy adresów, które znajdują się w lokalizacji lokalnej. Azure analizuje prefiksy adresów docelowy dla ruchu sieciowego, sprawdza konfigurację, którą określono dla bramy sieci lokalnej i odpowiednio kieruje pakiety. Należy także określić bramy sieci lokalnej dla konfiguracji do wirtualnymi, które używają połączenia bramy sieci VPN.

W poniższym przykładzie programu PowerShell tworzy nową bramę sieci lokalnej:

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

Czasami trzeba zmodyfikować ustawienia bramy sieci lokalnej. Na przykład podczas dodawania lub modyfikowania zakres adresów, lub jeśli zmieni adres IP urządzenia sieci VPN. Zobacz [zmodyfikować ustawienia bramy sieci lokalnej za pomocą programu PowerShell](vpn-gateway-modify-local-network-gateway.md).

## <a name="resources"></a>Polecenia cmdlet programu PowerShell i interfejsów API REST

Dodatkowe zasoby techniczne i wymagania określonej składni, korzystając z interfejsów API REST, poleceń cmdlet programu PowerShell lub interfejsu wiersza polecenia Azure konfiguracji bramy sieci VPN zobacz następujące strony:

| **Wdrożenie klasyczne** | **Resource Manager** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [Interfejs API REST](https://msdn.microsoft.com/library/jj154113) |[Interfejs API REST](/rest/api/network/virtualnetworkgateways) |
| Nieobsługiwane | [Interfejs wiersza polecenia platformy Azure](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji o konfiguracjach dostępnych połączeń, zobacz [o bramy sieci VPN](vpn-gateway-about-vpngateways.md).
