---
title: "Połącz z tooan sieci lokalnej sieci wirtualnej platformy Azure: sieci VPN typu lokacja-lokacja: programu PowerShell | Dokumentacja firmy Microsoft"
description: "Kroki toocreate połączenia IPsec z lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem hello publicznej sieci Internet. Ta procedura jest pomocna podczas tworzenia połączenia usługi VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji za pomocą programu PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a>Tworzenie sieci wirtualnej za pomocą połączenia sieci VPN typu lokacja-lokacja przy użyciu programu PowerShell

W tym artykule opisano, jak toouse połączenie bramy sieci VPN toocreate lokacja do lokacji programu PowerShell z lokalnej sieci toohello sieci wirtualnej. Witaj czynności w tym artykule dotyczą modelu wdrażania usługi Resource Manager toohello. Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [Interfejs wiersza polecenia](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Portal klasyczny (model klasyczny)](vpn-gateway-site-to-site-create.md)
> 
>


Połączenie bramy sieci VPN typu lokacja-lokacja jest używane tooconnect lokalnej sieci tooan sieci wirtualnej platformy Azure za pośrednictwem tunelu VPN IPsec/IKE (IKEv1 lub IKEv2). Ten typ połączenia wymaga sieci VPN urządzeń znajdujących się lokalnie posiadających zewnętrznie połączonej publicznego tooit przypisany adres IP. Więcej informacji o bramach sieci VPN można znaleźć w artykule [Informacje dotyczące bram sieci VPN](vpn-gateway-about-vpngateways.md).

![Diagram połączenia bramy VPN Gateway typu lokacja-lokacja obejmującego wiele lokalizacji](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <a name="before"></a>Przed rozpoczęciem

Sprawdź, czy zostały spełnione następujące kryteria przed rozpoczęciem konfiguracji hello:

* Upewnij się, że masz zgodne urządzenie sieci VPN i osoby, która jest w stanie tooconfigure go. Aby uzyskać więcej informacji o zgodnych urządzeniach sieci VPN i konfiguracji urządzeń, zobacz artykuł [Informacje o urządzeniach sieci VPN](vpn-gateway-about-vpn-devices.md).
* Sprawdź, czy masz dostępny zewnętrznie publiczny adres IPv4 urządzenia sieci VPN. Ten adres IP nie może się znajdować za translatorem adresów sieciowych.
* Jeśli nie znasz z zakresów adresów IP hello znajduje się w konfiguracji sieci lokalnej, należy toocoordinate z osobą, która Podaj te szczegóły należy. Podczas tworzenia tej konfiguracji należy określić hello prefiksów adresów IP zakresu czy Azure będzie przekierowywać tooyour lokalizacji lokalnej. Brak hello podsieci sieci lokalnej mogą za pośrednictwem laptop podsieci sieci wirtualnej hello, które mają tooconnect do.
* Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager. Polecenia cmdlet programu PowerShell są często aktualizowane i zazwyczaj konieczne będzie tooupdate Twojego środowiska PowerShell poleceń cmdlet tooget hello najnowszych funkcji. Jeśli nie zaktualizujesz poleceń cmdlet programu PowerShell hello wartości określonych może zakończyć się niepowodzeniem. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) uzyskać więcej informacji o pobieraniu i instalowaniu poleceń cmdlet programu PowerShell.

### <a name="example"></a>Przykładowe wartości

Przykłady Hello w tym artykule Użyj hello następujące wartości. Można użyć tych wartości toocreate środowiska testowego, lub zobacz toothem toobetter zrozumieć hello przykłady w tym artykule.

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <a name="Login"></a>1. Połącz tooyour subskrypcji

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="VNet"></a>2. Tworzenie sieci wirtualnej i podsieci bramy

Jeśli nie masz jeszcze sieci wirtualnej, utwórz ją. Podczas tworzenia sieci wirtualnej, upewnij się, że przestrzenie adresowe hello, które określisz nie nakłada przestrzeni adresowych hello wyposażonych w sieci lokalnej.

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="vnet"></a>toocreate sieć wirtualną i podsieć bramy

Ten przykład tworzy sieć wirtualną i podsieć bramy. Jeśli masz już sieć wirtualną, wymagającym tooadd podsieć bramy, aby wyświetlić [tooadd bramy podsieci tooa sieć wirtualną utworzono już](#gatewaysubnet).

Utwórz grupę zasobów:

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

Utwórz swoją sieć wirtualną.

1. Ustaw zmienne hello.

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. Utwórz hello sieci wirtualnej.

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <a name="gatewaysubnet"></a>tooadd bramy sieci wirtualnej tooa podsieci utworzono już

1. Ustaw zmienne hello.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. Utwórz podsieć bramy hello.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. Ustaw konfigurację hello.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## 3. <a name="localnet"></a>Utwórz bramę sieci lokalnej hello

Brama sieci lokalnej Hello zwykle oznacza tooyour lokalizacji lokalnej. Nadaj nazwę za pomocą którego Azure można znaleźć tooit, a następnie wprowadź adres IP hello hello lokacji z toowhich urządzenia sieci VPN między lokalnymi hello utworzy połączenie. Należy także określić hello prefiksów adresów IP, które zostaną przesłane za pomocą urządzenia sieci VPN toohello hello VPN bramy. Witaj prefiksy adresów, które określisz są prefiksy hello znajdujących się w sieci lokalnej. W przypadku zmiany sieci lokalnej, można łatwo aktualizować hello prefiksy.

Użyj hello następujące wartości:

* Witaj *GatewayIPAddress* jest adresem IP hello lokalnego urządzenia sieci VPN. Urządzenie sieci VPN nie może znajdować się za translatorem adresów sieciowych.
* Witaj *prefiks adresu* jest lokalnej przestrzeni adresowej.

tooadd bramy sieci lokalnej z prefiksem pojedynczy adres:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

tooadd bramy sieci lokalnej przy użyciu wielu prefiksy adresów:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

toomodify prefiksów adresów IP dla bramy sieci lokalnej:<br>
Zdarza się, że prefiksy bramy sieci lokalnej są zmieniane. kroki Hello podejmiesz toomodify Twojego adresu IP, który prefiksy zależą od tego, czy utworzono połączenia bramy sieci VPN. Zobacz hello [prefiksów adresów IP zmodyfikować dla bramy sieci lokalnej](#modify) sekcji tego artykułu.

## <a name="PublicIP"></a>4. Żądanie publicznego adresu IP

Brama sieci VPN musi mieć publiczny adres IP. Najpierw zażądać zasobu adresu IP hello i odwoływać się tooit podczas tworzenia bramy sieci wirtualnej. adres IP Hello jest przypisywane dynamicznie toohello zasobów, po utworzeniu bramy sieci VPN hello. Brama sieci VPN aktualnie obsługuje tylko *dynamiczne* przypisywanie publicznych adresów IP. Nie można zażądać przypisania statycznego publicznego adresu IP. Jednak nie oznacza to, że adres IP hello ulegnie zmianie po przypisaniu tooyour bramy sieci VPN. Hello czasu tylko zmiany adresu publicznego adresu IP hello jest po hello bramy zostanie usunięta i utworzona ponownie. Nie zmienia się on w przypadku zmiany rozmiaru, zresetowania ani przeprowadzania innych wewnętrznych czynności konserwacyjnych bądź uaktualnień bramy sieci VPN.

Żądanie do publicznego adresu IP przypisanego tooyour sieci wirtualnej bramy sieci VPN.

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a>5. Tworzenie konfiguracji adresów IP bramy hello

Konfiguracja bramy Hello definiuje podsieć hello oraz hello toouse w publicznych adresów IP. Użyj następującego przykładu toocreate hello konfigurację bramy:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a>6. Tworzenie bramy sieci VPN hello

Tworzenie bramy sieci VPN hello sieci wirtualnej. Tworzenie bramy sieci VPN może potrwać too45 minut lub więcej toocomplete.

Użyj hello następujące wartości:

* Witaj *elementu GatewayType -* Site-to-Site konfiguracja jest *Vpn*. Typ bramy Hello jest zawsze toohello określonej konfiguracji w przypadku wdrażania. Na przykład inne konfiguracje bramy mogą wymagać zastosowania wartości -GatewayType ExpressRoute.
* Witaj *- VpnType* może być *RouteBased* (określony tooas dynamiczne bramy w części dokumentacji), lub *PolicyBased* (określony tooas statycznych bramy w części dokumentacji ). Więcej informacji o typach bram sieci VPN można znaleźć w artykule [VPN Gateway — informacje](vpn-gateway-about-vpngateways.md).
* Wybierz hello jednostka SKU bramy, które mają toouse. Dla niektórych jednostek SKU istnieją ograniczenia konfiguracji. Aby uzyskać więcej informacji, zobacz [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku) (Jednostki SKU bramy). Jeśli wystąpi błąd podczas tworzenia bramy sieci VPN hello dotyczące hello - GatewaySku, sprawdź, że zainstalowano najnowszą wersję hello hello poleceń cmdlet programu PowerShell.

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <a name="ConfigureVPNDevice"></a>7. Konfiguracja urządzenia sieci VPN

Sieć lokalną tooan połączeń lokacja-lokacja wymagają urządzenia sieci VPN. W tym kroku konfigurowane jest urządzenie sieci VPN. Podczas konfigurowania urządzenia sieci VPN, potrzebne są następujące hello:

- Klucz współużytkowany. Jest to hello sam udostępniony klucz, który należy określić podczas tworzenia połączenia sieci VPN typu lokacja-lokacja. W naszych przykładach używamy podstawowego klucza współużytkowanego. Firma Microsoft zaleca, aby wygenerować bardziej złożonych toouse klucza.
- Witaj publiczny adres IP bramy sieci wirtualnej. Publiczny adres IP hello można wyświetlić za pomocą hello portalu Azure, programu PowerShell lub interfejsu wiersza polecenia. Witaj toofind publiczny adres IP bramy sieci wirtualnej przy użyciu programu PowerShell, użyj hello poniższy przykład:

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>8. Utwórz połączenie sieci VPN hello

Następnie należy utworzyć połączenie VPN lokacja-lokacja hello między bramą sieci wirtualnej i urządzenie sieci VPN. Należy się, że wartości hello tooreplace własnymi. klucz współużytkowany Hello musi odpowiadać wartości hello, używanego do konfiguracji urządzenia sieci VPN. Zwróć uwagę, że hello "-ConnectionType" lokacja-lokacja jest *IPsec*.

1. Ustaw zmienne hello.
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. Utwórz połączenie hello.
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

Automatycznie podczas hello zostanie nawiązane połączenie.

## <a name="toverify"></a>9. Sprawdź hello połączenia sieci VPN

Istnieje kilka różnych sposobów tooverify połączenia sieci VPN.

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="connectVM"></a>Maszyna wirtualna tooa tooconnect

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <a name="modify"></a>Modyfikowanie prefiksów adresów IP bramy sieci lokalnej

Zmiana hello prefiksów adresów IP, które mają być kierowane tooyour lokalnej lokalizacji można zmodyfikować hello bramy sieci lokalnej. Poniżej przedstawiono dwa zestawy instrukcji. instrukcje Hello, musisz wybrać zależą od tego, czy zostały już utworzone połączenie bramy.

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a>Modyfikowanie hello adres IP bramy dla bramy sieci lokalnej

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Następne kroki

*  Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne).
* Uzyskać informacji na temat protokołu BGP, zobacz hello [Omówienie protokołu BGP](vpn-gateway-bgp-overview.md) i [jak tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
