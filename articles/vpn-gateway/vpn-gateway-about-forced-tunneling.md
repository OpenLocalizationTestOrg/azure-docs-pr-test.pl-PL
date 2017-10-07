---
title: "Skonfigurować wymuszanie tunelowania dla połączenia usługi Azure Site to Site: klasycznym | Dokumentacja firmy Microsoft"
description: "Jak tooredirect lub \"force\" wszystkie powiązane z Internetu ruchu wstecz tooyour lokalizacji lokalnej."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a>Konfigurowanie przy użyciu tunelowania wymuszonego hello klasycznego modelu wdrażania

Wymuszone tunelowanie umożliwia przekierowanie lub "force" wszystkie powiązane z Internetu ruchu wstecz tooyour lokalnej lokalizacji za pośrednictwem tunelu VPN typu lokacja-lokacja dla inspekcji i inspekcji. Jest to wymagane krytycznych dla większości organizacji IT zasad. Bez tunelowania wymuszonego ruch do Internetu z maszyn wirtualnych na platformie Azure będzie zawsze przechodzenie od infrastruktury sieci platformy Azure bezpośrednio limit toohello Internet, bez tooallow opcji hello możesz ruchu hello tooinspect lub inspekcji. Nieautoryzowany dostęp do Internetu potencjalnie może spowodować ujawnienie tooinformation lub inne rodzaje naruszeń zabezpieczeń.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

W tym artykule przedstawiono konfigurowanie wymuszonego tunelowania dla sieci wirtualnych utworzonych przy użyciu hello klasycznego modelu wdrażania. Tunelowanie wymuszone można skonfigurować przy użyciu programu PowerShell, nie za pośrednictwem portalu hello. Tooconfigure wymuszonego tunelowania dla modelu wdrażania usługi Resource Manager hello, zaznacz klasycznego artykułu z następującej listy rozwijanej hello:

> [!div class="op_single_selector"]
> * [PowerShell — model klasyczny](vpn-gateway-about-forced-tunneling.md)
> * [Program PowerShell — model usługi Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a>Wymagania i uwagi
Wymuszanie tunelowania na platformie Azure jest skonfigurowana za pośrednictwem sieci wirtualnej trasy zdefiniowane przez użytkownika (przez). Przekierowywanie ruchu tooan w lokalnym witryny jest wyrażona jako brama sieci VPN platformy Azure toohello trasy domyślnej. Witaj poniższej sekcji przedstawiono hello obecne ograniczenie hello tabeli routingu i tras dla sieci wirtualnej platformy Azure:

* Każda podsieć sieci wirtualnej ma wbudowane, tabelę routingu systemu. Tabela routingu Hello system ma hello następujące trzy grupy tras:

  * **Tras lokalnych sieci wirtualnej:** bezpośrednio toohello docelowego maszyny wirtualne w hello tej samej sieci wirtualnej.
  * **Trasy lokalnymi:** toohello bramy sieci VPN platformy Azure.
  * **Trasa domyślna:** bezpośrednio toohello Internet. Pakiety przeznaczone toohello prywatnych adresów IP nie pasuje do żadnego hello dwoma poprzednimi trasy zostaną usunięte.
* Hello wersji z tras zdefiniowanych przez użytkownika można utworzyć routingu tooadd tabeli trasy domyślnej i następnie skojarzyć hello routingu tabeli tooyour sieci wirtualnej adresy podsieci używane tooenable wymuszone tunelowanie korzysta z tych podsieci.
* Należy tooset "domyślnej witryny" między sieci wirtualnej podłączonej toohello hello między lokalizacjami lokalnych witryn.
* Wymuszanie tunelowania musi być skojarzony z sieć wirtualną, która ma dynamiczne routingu bramy sieci VPN (nie bramy statyczne).
* ExpressRoute wymuszonego tunelowania nie jest skonfigurowany za pomocą ten mechanizm, ale zamiast tego jest włączana przez anonsuje trasę domyślną za pośrednictwem hello BGP usługi ExpressRoute sesje komunikacji równorzędnej. Zobacz hello [dokumentacja usługi ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) Aby uzyskać więcej informacji.

## <a name="configuration-overview"></a>Przegląd konfiguracji
W hello poniższy przykład tunelowane hello nie wymusza podsieci frontonu. Witaj obciążeń w podsieci frontonu hello można kontynuować tooaccept i odpowiada na żądania toocustomer z hello Internet bezpośrednio. Witaj podsieci w warstwie pośredniej i wewnętrznej bazy danych zostało wymuszone tunelowane. Wszystkie połączenia wychodzące z tymi dwiema podsieciami toohello Internet będzie tooan wymuszonym lub ponownie przekierowanego lokacji lokalnej za pośrednictwem jednego powitalne tuneli S2S VPN.

Pozwala toorestrict i inspekcję dostępu do Internetu na maszynach wirtualnych lub w chmurze usługi na platformie Azure, pozostawiając tooenable architektury usługa wielowarstwowa wymagane. Możesz również zastosować wymuszonego tunelowania toohello całe sieci wirtualne Jeśli w sieci wirtualne nie żadne obciążenia skierowane do Internetu.

![Wymuszone tunelowanie](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a>Przed rozpoczęciem
Sprawdź, czy masz hello poniższych elementach przed rozpoczęciem konfiguracji.

* Subskrypcja platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).
* Skonfigurowanej sieci wirtualnej. 
* Witaj najnowszą wersję hello poleceń cmdlet programu Azure PowerShell. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell.

## <a name="configure-forced-tunneling"></a>Konfigurowanie wymuszonego tunelowania
Hello procedury pomoże określić wymuszanie tunelowania do sieci wirtualnej. kroki konfiguracji Hello odpowiada pliku konfiguracji sieci toohello w sieci wirtualnej.

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

W tym przykładzie hello sieci wirtualnej "Sieci wirtualnej MultiTier" zawiera trzy podsieci: podsieci "Frontend", "Midtier" i "Zaplecze", w przypadku połączeń między różnymi lokalizacjami cztery: "DefaultSiteHQ" i trzy gałęzie. 

kroki Hello będzie hello "DefaultSiteHQ" jako hello domyślne lokacji połączenie tunelowania wymuszonego i konfigurowanie hello Midtier i wewnętrznej bazy danych podsieci toouse wymuszonego tunelowania.

1. Tworzy tabelę routingu. Użyj następującego polecenia cmdlet toocreate hello tabeli routingu.

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. Dodaj tabelę routingu toohello trasy domyślnej. 

  Witaj poniższy przykład umożliwia dodanie domyślną trasę toohello tabelę routingu utworzone w kroku 1. Należy pamiętać, że hello tylko trasy obsługiwane jest prefiks docelowy hello toohello "0.0.0.0/0" następnego skoku "Właściwość VPNGateway".

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. Kojarzenie hello routingu tabeli toohello podsieci. 

  Po utworzeniu tabeli routingu i dodać trasy, użyj następującego przykładu tooadd hello lub skojarzyć podsieci tooa tabeli hello trasy w sieci wirtualnej. przykład Witaj dodaje hello trasy tabeli "MyRouteTable" toohello Midtier i podsieci wewnętrznej bazy danych z MultiTier wirtualnymi.

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. Przypisz domyślnej witryny dla wymuszonego tunelowania. 

  W hello poprzedzających krok hello przykładowe polecenia cmdlet skrypty utworzone hello tabeli routingu i skojarzone tootwo tabeli tras hello hello podsieci sieci wirtualnej. pozostały krok Hello jest tooselect lokalnej lokacji między hello połączeń obejmujący wiele lokacji sieci wirtualnej hello jako hello domyślnej witryny lub tunelu.

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a>Dodatkowe polecenia cmdlet programu PowerShell
### <a name="toodelete-a-route-table"></a>toodelete tabelę tras

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a>toolist tabelę tras

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a>toodelete tras z tabeli tras

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a>tooremove tras z podsiecią

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a>Tabela tras hello toolist skojarzony z podsiecią

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a>tooremove domyślnej witryny z bramy sieci VPN w sieci wirtualnej

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```