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
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a>Skonfiguruj tunelowanie wymuszone przy użyciu modelu wdrażania usługi Azure Resource Manager hello

Wymuszone tunelowanie umożliwia przekierowanie lub "force" wszystkie powiązane z Internetu ruchu wstecz tooyour lokalnej lokalizacji za pośrednictwem tunelu VPN typu lokacja-lokacja dla inspekcji i inspekcji. Jest to wymagane krytycznych dla większości organizacji IT zasad. Bez tunelowania wymuszonego ruch do Internetu z maszyn wirtualnych na platformie Azure zawsze przechodzi od infrastruktury sieci platformy Azure bezpośrednio limit toohello Internet, bez tooallow opcji hello możesz ruchu hello tooinspect lub inspekcji. Nieautoryzowany dostęp do Internetu potencjalnie może spowodować ujawnienie tooinformation lub inne rodzaje naruszeń zabezpieczeń.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

W tym artykule przedstawiono konfigurowanie wymuszonego tunelowania dla sieci wirtualnych utworzonych przy użyciu modelu wdrażania usługi Resource Manager hello. Tunelowanie wymuszone można skonfigurować przy użyciu programu PowerShell, nie za pośrednictwem portalu hello. Tooconfigure wymuszonego tunelowania dla hello klasycznego modelu wdrażania, wybierz opcję klasycznego artykułu z następującej listy rozwijanej hello:

> [!div class="op_single_selector"]
> * [PowerShell — model klasyczny](vpn-gateway-about-forced-tunneling.md)
> * [Program PowerShell — model usługi Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a>Około wymuszonego tunelowania

powitania po diagram ilustruje sposób wymuszonego tunelowania działa. 

![Wymuszone tunelowanie](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

W przykładzie hello powyżej hello tunelowane nie wymusza podsieci frontonu. Witaj obciążeń w podsieci frontonu hello można kontynuować tooaccept i odpowiada na żądania toocustomer z hello Internet bezpośrednio. Witaj podsieci w warstwie pośredniej i wewnętrznej bazy danych zostało wymuszone tunelowane. Wszystkie połączenia wychodzące z tymi dwiema podsieciami toohello Internet będzie tooan wymuszonym lub ponownie przekierowanego lokacji lokalnej za pośrednictwem jednego powitalne tuneli S2S VPN.

Pozwala toorestrict i inspekcję dostępu do Internetu na maszynach wirtualnych lub w chmurze usługi na platformie Azure, pozostawiając tooenable architektury usługa wielowarstwowa wymagane. Jeśli w sieci wirtualne nie żadne obciążenia internetowy, również można zastosować wymuszonego tunelowania toohello całej sieci wirtualnych.

## <a name="requirements-and-considerations"></a>Wymagania i uwagi

Wymuszanie tunelowania na platformie Azure jest skonfigurowana za pośrednictwem sieci wirtualnej trasy zdefiniowane przez użytkownika. Przekierowywanie ruchu tooan w lokalnym witryny jest wyrażona jako brama sieci VPN platformy Azure toohello trasy domyślnej. Aby uzyskać więcej informacji dotyczących użytkownika routingu i sieci wirtualnych, zobacz [trasy zdefiniowane przez użytkownika i przesyłanie dalej IP](../virtual-network/virtual-networks-udr-overview.md).

* Każda podsieć sieci wirtualnej ma wbudowane, tabelę routingu systemu. Tabela routingu Hello system ma hello następujące trzy grupy tras:
  
  * **Tras lokalnych sieci wirtualnej:** bezpośrednio toohello docelowego maszyny wirtualne w hello tej samej sieci wirtualnej.
  * **Trasy lokalnymi:** toohello bramy sieci VPN platformy Azure.
  * **Trasa domyślna:** bezpośrednio toohello Internet. Pakiety przeznaczone toohello prywatnych adresów IP nie pasuje do żadnego hello dwoma poprzednimi trasy są usuwane.
* Ta procedura używa trasy zdefiniowane przez użytkownika (przez) toocreate routingu tooadd tabeli trasy domyślnej, a następnie skojarzyć hello routingu tabeli tooyour sieci wirtualnej adresy podsieci używane tooenable wymuszone tunelowanie korzysta z tych podsieci.
* Tunelowanie wymuszone, muszą być skojarzone z sieci wirtualnej, który ma bramy sieci VPN opartej na trasach. Należy tooset "domyślnej witryny" między sieci wirtualnej podłączonej toohello hello między lokalizacjami lokalnych witryn. Ponadto hello w lokalnym urządzenie sieci VPN musi być skonfigurowane przy użyciu 0.0.0.0/0 jako selektorów ruchu. 
* ExpressRoute wymuszonego tunelowania nie jest skonfigurowany za pomocą ten mechanizm, ale zamiast tego jest włączana przez anonsuje trasę domyślną za pośrednictwem hello BGP usługi ExpressRoute sesje komunikacji równorzędnej. Aby uzyskać więcej informacji, zobacz hello [dokumentacja usługi ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="configuration-overview"></a>Przegląd konfiguracji

Witaj procedury ułatwia tworzenie grupy zasobów i sieci wirtualnej. Następnie będzie utworzyć bramę sieci VPN i skonfigurować wymuszanie tunelowania. W tej procedurze hello sieci wirtualnej "Sieci wirtualnej MultiTier" zawiera trzy podsieci: "Frontend", "Midtier" i "Zaplecze", z czterema między lokalizacjami połączeń: "DefaultSiteHQ" i trzy gałęzie.

kroki procedury Hello ustawiono hello "DefaultSiteHQ" hello domyślne lokacji połączenie dla wymuszone tunelowanie i skonfigurować hello "Midtier" i "Zaplecze" podsieci toouse wymuszonego tunelowania.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell.

### <a name="toolog-in"></a>toolog w

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a>Konfigurowanie wymuszonego tunelowania

1. Utwórz grupę zasobów.

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. Tworzenie sieci wirtualnej i określenia podsieci.

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. Utwórz hello bramy sieci lokalnej.

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. Utwórz regułę trasy hello tabeli i trasy.

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. Kojarzenie toohello tabeli tras hello Midtier i podsieci wewnętrznej bazy danych.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Utwórz hello bramy z domyślnej witryny. Ten krok zajmuje niektórych toocomplete czasu, czasami 45 minut lub dłużej, ponieważ są tworzenia i konfigurowania bramy hello.<br> Witaj **- GatewayDefaultSite** jest hello parametrów polecenia cmdlet, umożliwiający hello wymuszone routingu toowork konfiguracji, dlatego podjąć tooconfigure szczególną uwagę prawidłowo tego ustawienia. Ten parametr jest dostępna w programie PowerShell 1.0 lub nowszej.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. Nawiązywać połączenia sieci VPN hello lokacja-lokacja.

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