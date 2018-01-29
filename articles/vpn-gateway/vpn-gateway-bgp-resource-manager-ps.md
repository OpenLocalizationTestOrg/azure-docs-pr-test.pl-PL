---
title: "Konfigurowanie protokołu BGP na bramy sieci VPN platformy Azure: Menedżer zasobów: programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono konfigurowanie protokołu BGP z bramy sieci VPN platformy Azure przy użyciu usługi Azure Resource Manager i programu PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: b00a3fe7ba4b12c2e9c486188c292cd6fafb60a3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-configure-bgp-on-azure-vpn-gateways-using-powershell"></a>Jak można skonfigurować protokołu BGP na bramy sieci VPN platformy Azure przy użyciu programu PowerShell
W tym artykule przedstawiono kroki, aby włączyć protokół BGP dla połączenia sieci VPN typu lokacja-lokacja (S2S) między lokalizacjami i połączenia do wirtualnymi przy użyciu modelu wdrażania usługi Resource Manager i programu PowerShell.

## <a name="about-bgp"></a>BGP — informacje
BGP to standardowy protokół routingu używany często w Internecie do wymiany informacji o routingu i osiągalności między dwiema lub wieloma sieciami. Protokół BGP umożliwia bramy sieci VPN platformy Azure i lokalnymi urządzeń sieci VPN, nazywany elementów równorzędnych BGP lub sąsiadów do programu exchange "tras" informujących zarówno bramy na dostępność i uzyskiwanie dla tych prefiksów przechodzić przez bramy lub routery związane. Protokół BGP umożliwia również włączenie routingu tranzytowego między wieloma sieciami poprzez propagowanie tras, których brama BGP uczy się od jednego elementu równorzędnego BGP, we wszystkich innych elementach równorzędnych BGP.

Zobacz [Omówienie protokołu BGP z bramy sieci VPN Azure](vpn-gateway-bgp-overview.md) dla omówione więcej korzyści BGP i zrozumieć wymagania techniczne i zagadnienia dotyczące użycia protokołu BGP.

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>Wprowadzenie do korzystania z protokołu BGP w bramach sieci VPN platformy Azure

W tym artykule przedstawiono kroki umożliwiające wykonywanie następujących zadań:

* [Część 1 - Włącz protokół BGP dla bramy sieci VPN platformy Azure](#enablebgp)
* [Część 2 - ustanowić połączenia między lokalizacjami z protokołem BGP](#crossprembgp)
* [Część 3 — ustanowienie połączenia do wirtualnymi z protokołem BGP](#v2vbgp)

Każda część instrukcji formularzy podstawowego bloku konstrukcyjnego włączenia protokołu BGP w połączenie sieciowe. Po ukończeniu wszystkich trzech części kompilacji topologii jak pokazano na poniższym diagramie:

![Topologii protokołu BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

Możesz łączyć części ze sobą w celu kompilacji przesyłania bardziej złożonymi, hop wielu, sieci, która odpowiada Twoim potrzebom.

## <a name ="enablebgp"></a>Część 1 — Konfigurowanie protokołu BGP dla bramy sieci VPN platformy Azure
Kroki konfiguracji Ustaw parametry BGP bramy sieci VPN platformy Azure, jak pokazano na poniższym diagramie:

![Protokół BGP bramy](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>Przed rozpoczęciem
* Sprawdź, czy masz subskrypcję platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).
* Zainstaluj polecenia cmdlet programu PowerShell usługi Azure Resource Manager. Aby uzyskać więcej informacji na temat instalowania poleceń cmdlet programu PowerShell, zobacz artykuł [How to install and configure Azure PowerShell](/powershell/azure/overview) (Instalowanie i konfigurowanie programu Azure PowerShell). 

### <a name="step-1---create-and-configure-vnet1"></a>Krok 1 — Tworzenie i konfigurowanie VNet1
#### <a name="1-declare-your-variables"></a>1. Zadeklarowanie zmiennych
W tym ćwiczeniu Rozpoczniemy przez zadeklarowanie naszych zmiennych. Poniższy przykład deklaruje zmienne przy użyciu wartości dla tego testu. Podczas konfigurowania produktu należy pamiętać o zastąpieniu ich odpowiednimi wartościami. Tych zmiennych można użyć, aby wykonać opisane kroki w celu zapoznania się z tego typu konfiguracją. Zmodyfikuj zmienne, a następnie skopiuj je i wklej do konsoli programu PowerShell.

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a>2. Połączyć subskrypcję i Utwórz nową grupę zasobów
Aby używać poleceń cmdlet Menedżera zasobów, upewnij się, że można przełączyć do trybu programu PowerShell. Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

Otwórz konsolę programu PowerShell i połącz się ze swoim kontem. Użyj poniższego przykładu w celu łatwiejszego nawiązania połączenia:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Utworzenie sieci TestVNet1
Poniższy przykład tworzy sieć wirtualną o nazwie TestVNet1 i trzy podsieci, co GatewaySubnet o nazwie jedną o nazwie frontonu i jedną o nazwie wewnętrznej bazy danych. Podczas zastępowania wartości ważne jest, aby podsieć bramy zawsze nosiła nazwę GatewaySubnet. W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>Krok 2 — Tworzenie bramy sieci VPN dla TestVNet1 z parametrami BGP
#### <a name="1-create-the-ip-and-subnet-configurations"></a>1. Tworzenie konfiguracji adresów IP i podsieci
Następnie zostaje przesłane żądanie przydzielenia publicznego adresu IP do bramy, która zostanie utworzona dla sieci wirtualnej. Zostanie również definiować wymagane podsieci i konfiguracje adresów IP.

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-the-vpn-gateway-with-the-as-number"></a>2. Tworzenie bramy sieci VPN z numerem AS
Utwórz bramę sieci wirtualnej dla sieci TestVNet1. Protokół BGP wymaga bramy sieci VPN opartej na trasach, a także parametr dodanie - Asn, aby ustawić właściwość ASN (AS Number) dla TestVNet1. Jeśli parametr numer ASN nie jest ustawiona, jest przypisany numer ASN 65515. Tworzenie bramy może potrwać co najmniej 30 minut.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-the-azure-bgp-peer-ip-address"></a>3. Uzyskaj adres IP elementu równorzędnego protokołu BGP platformy Azure
Po utworzeniu bramy należy uzyskać adres IP elementu równorzędnego protokołu BGP dla bramy sieci VPN platformy Azure. Ten adres jest potrzebne do skonfigurowania bramy sieci VPN platformy Azure jako element równorzędny BGP dla lokalnego urządzenia sieci VPN.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

Ostatnie polecenie pokazuje odpowiednich konfiguracji protokołu BGP dla bramy sieci VPN platformy Azure; na przykład:

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

Po utworzeniu bramy można użyć tej bramy do nawiązywania połączenia między lokalizacjami lub wirtualnymi do połączenia z protokołem BGP. Poniższe sekcje przeprowadzenie kroki, aby ukończyć wykonywania.

## <a name ="crossprembbgp"></a>Część 2 - ustanowić połączenia między lokalizacjami z protokołem BGP

Nawiązanie połączenia między różnymi lokalizacjami, musisz utworzyć bramy sieci lokalnej do reprezentowania lokalnego urządzenia sieci VPN i połączenia bramy sieci VPN bramy sieci lokalnej. Gdy istnieją artykuły, które pomagają tych kroków, ten artykuł zawiera dodatkowe właściwości, które są wymagane, aby określić parametry konfiguracji protokołu BGP.

![Protokół BGP dla między lokalizacjami](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

Przed kontynuowaniem upewnij się, że zostały wykonane [część 1](#enablebgp) tego ćwiczenia.

### <a name="step-1---create-and-configure-the-local-network-gateway"></a>Krok 1 — Tworzenie i konfigurowanie bramy sieci lokalnej

#### <a name="1-declare-your-variables"></a>1. Zadeklarowanie zmiennych

Tego ćwiczenia w dalszym ciągu przy tworzeniu konfiguracji przedstawione na diagramie. Należy pamiętać o zastąpieniu przykładowych wartości tymi, które mają zostać użyte w danej konfiguracji.

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

Kilka rzeczy do uwzględnienia dotyczącymi parametrów bramy sieci lokalnej:

* Brama sieci lokalnej może być w tej samej lub innej lokalizacji i grupy zasobów jako brama sieci VPN. Ten przykład przedstawia je w różnych grupach zasobów w różnych lokalizacjach.
* Minimalna prefiks, musisz zadeklarować dla bramy sieci lokalnej jest adres hosta, adresu IP elementu równorzędnego protokołu BGP na urządzeniu sieci VPN. W takim przypadku jest /32 prefiksu "10.52.255.254/32".
* Przypomnienia należy użyć innego protokołu BGP numerów ASN między lokalnymi sieciami i sieci wirtualnej platformy Azure. Jeśli są one takie same, musisz zmienić numer ASN Twojej sieci wirtualnej, jeśli lokalnego urządzenia sieci VPN używa już właściwość ASN do elementu równorzędnego z innych sąsiadów BGP.

Przed kontynuowaniem upewnij się, że nadal masz połączenie z subskrypcją 1.

#### <a name="2-create-the-local-network-gateway-for-site5"></a>2. Tworzenie bramy sieci lokalnej dla Site5

Pamiętaj utworzyć grupę zasobów, jeśli nie został utworzony, przed utworzeniem bramy sieci lokalnej. Zwróć uwagę, dwie dodatkowe parametry dla bramy sieci lokalnej: numer Asn i BgpPeerAddress.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a>Krok 2 — połączenie bramy sieci wirtualnej i Brama sieci lokalnej

#### <a name="1-get-the-two-gateways"></a>1. Pobierz dwóch bram

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a>2. Utwórz TestVNet1 Site5 połączenia

W tym kroku należy utworzyć połączenie z TestVNet1 do Site5. Należy określić "-wartość $True" Aby włączyć protokół BGP dla tego połączenia. Jak już wspomniano, istnieje możliwość połączenia zarówno protokołu BGP, jak i z systemem innym niż BGP dla tej samej bramy sieci VPN platformy Azure. Jeśli protokół BGP jest włączony we właściwości połączenia, Azure nie włączyć protokół BGP dla tego połączenia, nawet jeśli parametry protokołu BGP jest już skonfigurowane na obu bram.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

Poniższy przykład zawiera listę parametrów wprowadzone w sekcji konfiguracji protokołu BGP na lokalnego urządzenia sieci VPN w tym ćwiczeniu:

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being the VPN tunnel interface on your device
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

Po kilku minutach zostanie nawiązane połączenie, a sesji komunikacji równorzędnej BGP rozpoczyna się po nawiązaniu połączenia IPsec.

## <a name ="v2vbgp"></a>Część 3 — ustanowienie połączenia do wirtualnymi z protokołem BGP

W tej sekcji dodaje połączenie do wirtualnymi z obsługą protokołu BGP, jak pokazano na poniższym diagramie:

![Protokół BGP dla sieci wirtualnej do sieci wirtualnej](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

Poniższe instrukcje nadal z poprzednich kroków. Należy wykonać [części I](#enablebgp) do tworzenia i konfigurowania TestVNet1 i bramy sieci VPN z protokołem BGP. 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a>Krok 1 — Tworzenie TestVNet2 i bramy sieci VPN

Należy się upewnić, że przestrzeń adresową nową sieć wirtualną TestVNet2, nie mogą się pokrywać ze wszystkimi zakresy sieci wirtualnej.

W tym przykładzie sieci wirtualne należą do tej samej subskrypcji. Można skonfigurować do wirtualnymi połączeń między różnych subskrypcji. Aby uzyskać więcej informacji, zobacz [skonfigurować połączenia do wirtualnymi](vpn-gateway-vnet-vnet-rm-ps.md). Upewnij się, że możesz dodać "-wartość $True" podczas tworzenia połączenia, aby włączyć protokół BGP.

#### <a name="1-declare-your-variables"></a>1. Zadeklarowanie zmiennych

Należy pamiętać o zastąpieniu przykładowych wartości tymi, które mają zostać użyte w danej konfiguracji.

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a>2. Utwórz TestVNet2 w nowej grupy zasobów

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3. Tworzenie bramy sieci VPN dla TestVNet2 z parametrami BGP

Żądaj publicznego adresu IP do przydzielenia do bramy utworzysz sieci wirtualnej i zdefiniuj wymagane podsieci i konfiguracje adresów IP.

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Utwórz bramę sieci VPN z numerem AS. Należy zmienić domyślny numer ASN w Twojej bramy sieci VPN platformy Azure. Numery ASN dla połączonych sieci wirtualnych musi być inna, aby włączyć protokół BGP i routing tranzytowy.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a>Krok 2 — Połącz bram TestVNet1 i TestVNet2

W tym przykładzie zarówno bramy znajdują się w tej samej subskrypcji. Ten krok można wykonać w tej samej sesji programu PowerShell.

#### <a name="1-get-both-gateways"></a>1. Pobierz obu bram

Pamiętaj o zalogowaniu się i połączeniu z subskrypcją 1.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. Utwórz zarówno połączenia

W tym kroku utworzysz połączenie z TestVNet1 TestVNet2 i połączenie z TestVNet2 do TestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Pamiętaj włączyć protokół BGP dla obu połączeń.
> 
> 

Po wykonaniu tych kroków, połączenie zostanie nawiązane po kilku minutach. Sesja komunikacji równorzędnej BGP działa po zakończeniu połączenia do wirtualnymi.

Jeśli ukończono wszystkie trzy elementy w tym ćwiczeniu zostały ustalone następujące topologii sieci:

![Protokół BGP dla sieci wirtualnej do sieci wirtualnej](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>Następne kroki

Po zakończeniu procesu nawiązywania połączenia można dodać do sieci wirtualnych maszyny wirtualne. Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).