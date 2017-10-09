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
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a>Jak tooconfigure protokołu BGP na bramy sieci VPN platformy Azure przy użyciu programu PowerShell
W tym artykule przedstawiono hello kroki tooenable protokołu BGP na połączenie sieci VPN typu lokacja-lokacja (S2S) między lokalizacjami i połączenia do wirtualnymi przy użyciu modelu wdrażania usługi Resource Manager hello i programu PowerShell.

## <a name="about-bgp"></a>BGP — informacje
Protokół BGP jest hello standardowy protokół routingu często używane w hello Internet tooexchange routingu i uzyskiwanie informacji między dwie lub więcej sieci. Protokół BGP umożliwia bramy sieci VPN hello Azure i lokalnymi urządzeniami sieci VPN, nazywane elementów równorzędnych BGP lub sąsiadów, tooexchange "tras" który poinformuje zarówno bramy na powitania dostępności i uzyskiwanie tych prefiksy toogo za pośrednictwem bramy hello lub routery związane. Protokół BGP można także włączyć routing tranzytowy między wieloma sieciami przez propagowania tras BGP bramy uczy się z jednego tooall elementu równorzędnego protokołu BGP innych elementów równorzędnych protokołu BGP.

Zobacz [Omówienie protokołu BGP z bramy sieci VPN Azure](vpn-gateway-bgp-overview.md) więcej omówienie zalet protokołu BGP i toounderstand hello wymagania techniczne i zagadnienia dotyczące użycia protokołu BGP.

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>Wprowadzenie do korzystania z protokołu BGP w bramach sieci VPN platformy Azure

W tym artykule przedstawiono hello toodo kroki hello następujące zadania:

* [Część 1 - Włącz protokół BGP dla bramy sieci VPN platformy Azure](#enablebgp)
* [Część 2 - ustanowić połączenia między lokalizacjami z protokołem BGP](#crossprembgp)
* [Część 3 — ustanowienie połączenia do wirtualnymi z protokołem BGP](#v2vbgp)

Każda część instrukcji hello formularzy podstawowego bloku konstrukcyjnego włączenia protokołu BGP w połączenie sieciowe. Po ukończeniu wszystkich trzech części kompilacji topologii hello pokazane na powitania po diagramu:

![Topologii protokołu BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

Możesz łączyć toobuild razem części sieci bardziej złożonymi, a z wieloma przeskokami, przesyłania, które spełni wymagania organizacji.

## <a name ="enablebgp"></a>Część 1 — Konfigurowanie protokołu BGP na powitania bramy sieci VPN platformy Azure
kroki konfiguracji Hello skonfigurować hello parametry BGP bramy sieci VPN platformy Azure hello pokazane na powitania po diagramu:

![Protokół BGP bramy](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>Przed rozpoczęciem
* Sprawdź, czy masz subskrypcję platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).
* Zainstaluj polecenia cmdlet programu PowerShell usługi Azure Resource Manager hello. Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). 

### <a name="step-1---create-and-configure-vnet1"></a>Krok 1 — Tworzenie i konfigurowanie VNet1
#### <a name="1-declare-your-variables"></a>1. Zadeklarowanie zmiennych
W tym ćwiczeniu Rozpoczniemy przez zadeklarowanie naszych zmiennych. Witaj poniższy przykład deklaruje hello zmienne używania hello wartości w tym ćwiczeniu. Należy się, że wartości hello tooreplace własnymi podczas konfigurowania w środowisku produkcyjnym. Można używać tych zmiennych, jeśli używasz za pośrednictwem toobecome kroki hello zapoznać się z tym typem konfiguracji. Modyfikuj zmienne hello, a następnie skopiuj i Wklej w konsoli programu PowerShell.

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Połączyć subskrypcję tooyour i utworzyć nową grupę zasobów
Witaj toouse poleceń cmdlet Menedżera zasobów, upewnij się, że Przełącz tryb tooPowerShell. Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

Otwórz konsolę programu PowerShell i Połącz konto tooyour. Użyj następujących hello przykładowe toohelp, gdy nawiązujesz połączenie:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Utworzenie sieci TestVNet1
Witaj poniższy przykład tworzy sieć wirtualną o nazwie TestVNet1 i trzy podsieci, co GatewaySubnet o nazwie jedną o nazwie frontonu i jedną o nazwie wewnętrznej bazy danych. Podczas zastępowania wartości ważne jest, aby podsieć bramy zawsze nosiła nazwę GatewaySubnet. W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>Krok 2 — Tworzenie hello bramy sieci VPN dla TestVNet1 z parametrami BGP
#### <a name="1-create-hello-ip-and-subnet-configurations"></a>1. Utwórz hello konfiguracje adresów IP i podsieci
Żądaj publicznego adresu IP adres toobe toohello przydzielone bramy utworzone sieci wirtualnej. Zostanie również definiować hello wymagane podsieci i konfiguracje adresów IP.

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a>2. Utwórz bramę sieci VPN hello z hello jako liczba
Tworzenie bramy sieci wirtualnej powitania dla TestVNet1. Protokół BGP wymaga TestVNet1 opartej na trasach bramy sieci VPN, a także hello dodanie parametru - Asn, tooset hello numeru ASN (AS Number). Jeśli parametr ASN hello nie jest ustawiona, jest przypisany numer ASN 65515. Tworzenie bramy może trochę potrwać (30 minut lub więcej toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a>3. Uzyskaj adres IP elementu równorzędnego protokołu BGP Azure hello
Po utworzeniu bramy hello należy adresem IP elementu równorzędnego protokołu BGP hello tooobtain hello bramy sieci VPN platformy Azure. Ten adres jest wymagane tooconfigure hello bramy sieci VPN platformy Azure jako element równorzędny BGP dla lokalnego urządzenia sieci VPN.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

ostatnie polecenie Hello przedstawia hello odpowiednich konfiguracji protokołu BGP na powitania bramy sieci VPN platformy Azure; na przykład:

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

Po utworzeniu bramy hello można używać tego połączenia między lokalizacjami tooestablish bramy albo wirtualnymi do połączenia z protokołem BGP. Witaj sekcje przeprowadzenie hello kroki toocomplete hello wykonywania.

## <a name ="crossprembbgp"></a>Część 2 - ustanowić połączenia między lokalizacjami z protokołem BGP

tooestablish połączenia między różnymi lokalizacjami, należy toocreate toorepresent bramy sieci lokalnej lokalnego urządzenia sieci VPN i połączeń tooconnect hello bramy sieci VPN z hello bramy sieci lokalnej. Gdy istnieją artykuły, które pomagają tych kroków, ten artykuł zawiera parametry konfiguracji protokołu BGP hello wymagane toospecify hello dodatkowych właściwości.

![Protokół BGP dla między lokalizacjami](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

Przed kontynuowaniem upewnij się, że zostały wykonane [część 1](#enablebgp) tego ćwiczenia.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Krok 1 — Tworzenie i konfigurowanie hello bramy sieci lokalnej

#### <a name="1-declare-your-variables"></a>1. Zadeklarowanie zmiennych

Tego ćwiczenia jest nadal wyświetlany na diagramie hello konfiguracji hello toobuild. Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

Kilka rzeczy toonote dotyczącymi parametrów bramy sieci lokalnej hello:

* Witaj bramy sieci lokalnej może być w hello takie same lub innej lokalizacji i zasobów grupy jako hello bramy sieci VPN. Ten przykład przedstawia je w różnych grupach zasobów w różnych lokalizacjach.
* Prefiks minimalna Hello potrzebne toodeclare dla bramy sieci lokalnej hello jest adres hosta hello adresu IP elementu równorzędnego protokołu BGP na urządzeniu sieci VPN. W takim przypadku jest /32 prefiksu "10.52.255.254/32".
* Przypomnienia należy użyć innego protokołu BGP numerów ASN między lokalnymi sieciami i sieci wirtualnej platformy Azure. Są one takie same hello, należy najpierw toochange ASN Twojej sieci wirtualnej Jeśli lokalnego urządzenia sieci VPN już używa hello numeru ASN toopeer z innych sąsiadów BGP.

Przed kontynuowaniem upewnij się, że są nadal połączonych tooSubscription 1.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Tworzenie bramy sieci lokalnej powitania dla Site5

Należy się, że grupa zasobów hello toocreate, jeśli nie został utworzony, przed utworzeniem bramy sieci lokalnej hello. Zwróć uwagę, Witaj dwie dodatkowe parametry dla bramy sieci lokalnej hello: numer Asn i BgpPeerAddress.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Krok 2 — Połącz hello bramy sieci wirtualnej i Brama sieci lokalnej

#### <a name="1-get-hello-two-gateways"></a>1. Pobierz Witaj dwie bramy

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Utwórz połączenie tooSite5 TestVNet1 hello

W tym kroku utworzysz hello połączenia z TestVNet1 tooSite5. Należy określić "-wartość $True" tooenable BGP dla tego połączenia. Jak już wspomniano, jest możliwe toohave połączeń zarówno protokołu BGP, jak i z systemem innym niż BGP dla hello tej samej bramy sieci VPN platformy Azure. Jeśli protokół BGP jest włączony we właściwości połączenia hello, Azure nie włączyć protokół BGP dla tego połączenia nawet, jeśli parametry protokołu BGP jest już skonfigurowane na obu bram.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

Witaj poniższy przykład wymieniono hello parametry wprowadzane do hello sekcji konfiguracji protokołu BGP na urządzeniu lokalnym sieci VPN w tym ćwiczeniu:

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Witaj połączenie jest nawiązywane po kilku minutach i uruchomieniu sesji komunikacji równorzędnej BGP hello, po nawiązaniu połączenia IPsec hello.

## <a name ="v2vbgp"></a>Część 3 — ustanowienie połączenia do wirtualnymi z protokołem BGP

W tej sekcji dodaje wirtualnymi do połączenia z protokołem BGP, jak pokazano w powitania po diagramu:

![Protokół BGP dla sieci wirtualnej do sieci wirtualnej](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

Witaj, postępując zgodnie z instrukcjami nadal z poprzednich kroków hello. Należy wykonać [części I](#enablebgp) toocreate i skonfiguruj TestVNet1 oraz hello bramy sieci VPN z protokołem BGP. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Krok 1 — Tworzenie TestVNet2 i hello bramy sieci VPN

Jest ważne toomake się, że przestrzeń adresów IP hello nowej sieci wirtualnej hello, TestVNet2, nakłada się ze wszystkimi zakresy sieci wirtualnej.

W tym przykładzie hello sieci wirtualnych należy toohello tej samej subskrypcji. Można skonfigurować do wirtualnymi połączeń między różnych subskrypcji. Aby uzyskać więcej informacji, zobacz [skonfigurować połączenia do wirtualnymi](vpn-gateway-vnet-vnet-rm-ps.md). Upewnij się, że możesz dodać hello "-wartość $True" podczas tworzenia hello tooenable połączeń protokołu BGP.

#### <a name="1-declare-your-variables"></a>1. Zadeklarowanie zmiennych

Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2. Utwórz TestVNet2 w hello nową grupę zasobów

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3. Tworzenie bramy sieci VPN powitania dla TestVNet2 z parametrami BGP

Żądaj publicznego adresu IP adres toobe toohello przydzielone bramy utworzysz sieci wirtualnej i zdefiniuj hello wymagane podsieci i konfiguracje adresów IP.

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Utwórz bramę sieci VPN hello z hello jako numer. Konieczne jest przesłonięcie hello domyślny numer ASN w Twojej bramy sieci VPN platformy Azure. Witaj numerów ASN dla hello połączone sieci wirtualne muszą być różne tooenable BGP i routing tranzytowy.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a>Krok 2 — Połącz hello TestVNet1 i TestVNet2 bram

W tym przykładzie zarówno bramy znajdują się w hello tej samej subskrypcji. Można wykonać ten krok w hello tej samej sesji programu PowerShell.

#### <a name="1-get-both-gateways"></a>1. Pobierz obu bram

Upewnij się, zaloguj się i połącz tooSubscription 1.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. Utwórz zarówno połączenia

W tym kroku utworzysz hello połączenia z TestVNet1 tooTestVNet2 i hello połączenia z TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Należy się tooenable BGP dla obu połączeń.
> 
> 

Po wykonaniu tych czynności hello połączenie jest nawiązywane po kilku minutach. Sesja komunikacji równorzędnej BGP Hello działa po zakończeniu hello połączenia do wirtualnymi.

Jeśli ukończono wszystkie trzy elementy w tym ćwiczeniu zostało ustanowione powitania od topologii sieci:

![Protokół BGP dla sieci wirtualnej do sieci wirtualnej](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>Następne kroki

Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
