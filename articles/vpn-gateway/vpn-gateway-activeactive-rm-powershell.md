---
title: "Skonfigurować połączenia sieci VPN S2S aktywny aktywny dla bram sieci VPN: usługi Azure Resource Manager: programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono konfigurowanie aktywny aktywny połączeń przy użyciu bramy sieci VPN platformy Azure przy użyciu usługi Azure Resource Manager i programu PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a>Skonfigurować połączenia sieci VPN S2S aktywny aktywny z bramy sieci VPN platformy Azure

W tym artykule przedstawiono hello kroki toocreate aktywny aktywny między lokalizacjami i wirtualnymi do połączeń przy użyciu modelu wdrażania usługi Resource Manager hello i programu PowerShell.

## <a name="about-highly-available-cross-premises-connections"></a>O wysokiej dostępności między lokalizacjami połączeń
tooachieve wysokiej dostępności i wirtualnymi do łączności między lokalizacjami, należy wdrożyć wiele bram sieci VPN i ustanowienia wielu równoległych połączeń między sieciami i Azure. Zobacz [wysokiej dostępności między lokalizacjami i łączności do wirtualnymi](vpn-gateway-highlyavailable.md) Omówienie opcji łączności i topologii.

Ten artykuł zawiera instrukcje hello tooset się aktywny aktywny między lokalizacjami połączenie sieci VPN i aktywny aktywny połączenie między dwiema sieciami wirtualnymi:

* [Część 1 — Tworzenie i konfigurowanie bramy sieci VPN platformy Azure w trybie aktywny / aktywny](#aagateway)
* [Część 2 - zestawiania połączeń między różnymi lokalizacjami aktywny aktywny](#aacrossprem)
* [Część 3 — ustanowienie połączenia do wirtualnymi aktywny aktywny](#aav2v)
* [Część 4 — aktualizacja istniejącej bramy między aktywny aktywny i aktywnego gotowości](#aaupdate)

Można połączyć te razem toobuild topologii sieci bardziej złożonych, wysokiej dostępności, która odpowiada Twoim potrzebom.

> [!IMPORTANT]
> Należy pamiętać, że w trybie aktywny aktywny hello używa hello tylko następujące wersje produktu: 
  * VpnGw1, VpnGw2, VpnGw3
  * Wysokowydajnej (dla starego starszej wersji jednostki SKU)
> 
> 

## <a name ="aagateway"></a>Część 1 — Tworzenie i konfigurowanie aktywny aktywny bramy sieci VPN
następujące kroki Hello skonfiguruje bramy sieci VPN platformy Azure w trybach aktywny aktywny. Witaj podstawowych różnic między bramami aktywny aktywny i aktywnego gotowości hello:

* Należy toocreate dwóch konfiguracji IP bramy z dwóch publicznych adresów IP
* Należy ustawić flagę EnableActiveActiveFeature hello
* Jednostka SKU bramy Hello musi być VpnGw1, VpnGw2, VpnGw3 lub wysokowydajnej (starszej wersji jednostki SKU).

Witaj inne właściwości są hello taki sam jak hello bramy z systemem innym niż — aktywny aktywny. 

### <a name="before-you-begin"></a>Przed rozpoczęciem
* Sprawdź, czy masz subskrypcję platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).
* Polecenia cmdlet programu PowerShell usługi Azure Resource Manager hello tooinstall jest potrzebny. Zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell.

### <a name="step-1---create-and-configure-vnet1"></a>Krok 1 — Tworzenie i konfigurowanie VNet1
#### <a name="1-declare-your-variables"></a>1. Zadeklarowanie zmiennych
To ćwiczenie rozpoczniemy od zadeklarowania zmiennych. w poniższym przykładzie Hello deklaruje zmienne hello używania hello wartości w tym ćwiczeniu. Należy się, że wartości hello tooreplace własnymi podczas konfigurowania w środowisku produkcyjnym. Można używać tych zmiennych, jeśli używasz za pośrednictwem toobecome kroki hello zapoznać się z tym typem konfiguracji. Modyfikuj zmienne hello, a następnie skopiuj i Wklej w konsoli programu PowerShell.

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
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
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Połączyć subskrypcję tooyour i utworzyć nową grupę zasobów
Upewnij się, że przełącznik tooPowerShell tryb toouse hello poleceń cmdlet Menedżera zasobów. Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

Otwórz konsolę programu PowerShell i Połącz konto tooyour. Użyj następujących hello przykładowe toohelp, gdy nawiązujesz połączenie:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Utworzenie sieci TestVNet1
Poniższy przykład Hello tworzy sieć wirtualną o nazwie TestVNet1 i trzy podsieci, co GatewaySubnet o nazwie jedną o nazwie frontonu i jedną o nazwie wewnętrznej bazy danych. Podczas zastępowania wartości ważne jest, aby podsieć bramy zawsze nosiła nazwę GatewaySubnet. W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a>Krok 2 — Tworzenie hello bramy sieci VPN dla TestVNet1 w trybie aktywny / aktywny
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a>1. Tworzenie hello publicznych adresów IP i konfiguracje adresów IP bramy
Żądanie dwa publiczne adresy toobe toohello przydzielone brama IP utworzone sieci wirtualnej. Zostanie również definiować hello podsieci i wymagane konfiguracje adresów IP.

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a>2. Tworzenie bramy sieci VPN hello z konfiguracją aktywny aktywny
Tworzenie bramy sieci wirtualnej powitania dla TestVNet1. Zauważ, że istnieją dwa wpisy GatewayIpConfig, i hello EnableActiveActiveFeature flaga jest ustawiona. Tworzenie bramy może trochę potrwać (45 minut lub więcej toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a>3. Uzyskaj hello bramy publicznych adresów IP i adres IP elementu równorzędnego protokołu BGP hello
Po utworzeniu bramy hello należy adresem IP elementu równorzędnego protokołu BGP hello tooobtain hello bramy sieci VPN platformy Azure. Ten adres jest wymagane tooconfigure hello bramy sieci VPN platformy Azure jako element równorzędny BGP dla lokalnego urządzenia sieci VPN.

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

Użyj następującego polecenia cmdlet tooshow Witaj dwie publiczne adresy IP przydzielone dla bramy sieci VPN, a ich odpowiednie adresy IP elementu równorzędnego protokołu BGP dla każdego wystąpienia bramy hello:

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

kolejność Hello hello publicznych adresów IP dla wystąpień bramy hello i hello, które są odpowiednie adresy komunikacji równorzędnej BGP hello takie same. W tym przykładzie hello bramy maszyny Wirtualnej z publicznego adresu IP z 40.112.190.5 użyje 10.12.255.4 jako adres komunikacji równorzędnej BGP, a brama hello z 138.91.156.129 użyje 10.12.255.5. Te informacje są potrzebne podczas konfigurowania w lokalnej sieci VPN urządzeń nawiązujących połączenie toohello aktywny aktywny bramy. Brama Hello jest wyświetlany na diagramie hello poniżej przy użyciu wszystkich adresów:

![aktywny aktywny bramy](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

Po utworzeniu bramy hello, używając tej bramy tooestablish aktywny aktywny obejmującym różne pomieszczenia lub połączenia do wirtualnymi. następujące sekcje Hello przeprowadzi hello kroki toocomplete hello wykonywania.

## <a name ="aacrossprem"></a>Część 2 - nawiązywania połączenia między lokalizacjami aktywny aktywny
tooestablish połączenia między różnymi lokalizacjami, należy toocreate toorepresent bramy sieci lokalnej lokalnego urządzenia sieci VPN i bramy sieci VPN platformy Azure hello tooconnect połączenia przy użyciu hello bramy sieci lokalnej. W tym przykładzie Brama sieci VPN platformy Azure hello jest w trybie aktywny / aktywny. W związku z tym nawet, jeśli istnieje tylko jeden lokalnego urządzenia sieci VPN (bramy sieci lokalnej) i jednego połączenia zasobów, zarówno wystąpień bramy sieci VPN platformy Azure zostanie ustanowiona tunel S2S VPN, jak hello lokalnego urządzenia.

Przed kontynuowaniem upewnij się, zostały ukończone [część 1](#aagateway) tego ćwiczenia.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Krok 1 — Tworzenie i konfigurowanie hello bramy sieci lokalnej
#### <a name="1-declare-your-variables"></a>1. Zadeklarowanie zmiennych
Tego ćwiczenia będą nadal wyświetlane na diagramie hello konfiguracji hello toobuild. Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

Kilka rzeczy toonote dotyczącymi parametrów bramy sieci lokalnej hello:

* Witaj bramy sieci lokalnej może być w hello takie same lub innej lokalizacji i zasobów grupy jako hello bramy sieci VPN. W tym przykładzie przedstawiono je w różnych grupach zasobów, ale w hello tej samej lokalizacji platformy Azure.
* Jeśli istnieje tylko jeden lokalnego urządzenia sieci VPN zgodnie z powyższym, hello aktywny aktywny połączenia można pracować z lub bez protokołu BGP. W tym przykładzie użyto BGP hello połączenia między lokalizacjami.
* Jeśli protokół BGP jest włączony, należy toodeclare dla bramy sieci lokalnej hello prefiks hello jest adres hosta hello adresu IP elementu równorzędnego protokołu BGP na urządzeniu sieci VPN. W takim przypadku jest /32 prefiksu "10.52.255.253/32".
* Przypomnienia należy użyć innego protokołu BGP numerów ASN między lokalnymi sieciami i sieci wirtualnej platformy Azure. Są one takie same hello, należy najpierw toochange ASN Twojej sieci wirtualnej Jeśli lokalnego urządzenia sieci VPN już używa hello numeru ASN toopeer z innych sąsiadów BGP.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Tworzenie bramy sieci lokalnej powitania dla Site5
Przed kontynuowaniem upewnij się, że są nadal połączonych tooSubscription 1. Utwórz grupę zasobów hello, jeśli nie został jeszcze utworzony.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Krok 2 — Połącz hello bramy sieci wirtualnej i Brama sieci lokalnej
#### <a name="1-get-hello-two-gateways"></a>1. Pobierz Witaj dwie bramy

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Utwórz połączenie tooSite5 TestVNet1 hello
W tym kroku utworzysz hello połączenia z TestVNet1 tooSite5_1 z ustawić także "wartość" $True.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a>3. Parametry sieci VPN i protokołu BGP dla lokalnego urządzenia sieci VPN
przykład Witaj poniżej wymieniono hello parametry, które wejdzie w hello sekcji konfiguracji protokołu BGP na urządzeniu lokalnym sieci VPN w tym ćwiczeniu:

    - Site5 ASN: 65050
    - IP protokołu BGP Site5: 10.52.255.253
    - Prefiksy tooannounce: (na przykład) 10.51.0.0/16 i 10.52.0.0/16
    - ASN sieci wirtualnej platformy Azure: 65010
    - Azure IP BGP sieci wirtualnej 1: 10.12.255.4 dla too40.112.190.5 tunelu
    - Azure IP BGP sieci wirtualnej 2: 10.12.255.5 dla too138.91.156.129 tunelu
    - Trasy statyczne: 10.12.255.4/32 docelowego, 10.12.255.5/32 docelowego too40.112.190.5 interfejsu tunelu następnego skoku hello sieci VPN, następnego skoku hello VPN tunelu interfejsu too138.91.156.129
    - eBGP wielokrotnego przeskoku: Upewnij się opcja "wielokrotnego przeskoku" hello, eBGP jest włączona na twoim urządzeniu, w razie potrzeby

Po za kilka minut, a sesja komunikacji równorzędnej BGP hello rozpocznie się po nawiązaniu połączenia IPsec hello należy ustanowić Hello połączenia. W tym przykładzie został skonfigurowany do tej pory tylko jeden lokalnego urządzenia sieci VPN, co hello diagramie pokazano poniżej:

![aktywny aktywny crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a>Krok 3 — Połącz dwa lokalnej sieci VPN urządzenia toohello aktywny aktywny VPN bramy
Jeśli masz dwie urządzenia sieci VPN na powitania sam lokalnej sieci, Podwójna nadmiarowości można osiągnąć za łączącego hello Azure urządzenie bramy VPN toohello drugiej sieci VPN.

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a>1. Tworzenie bramy sieci lokalnej drugi hello dla Site5
Należy pamiętać, że adres IP bramy hello, prefiks adresu i adres komunikacji równorzędnej BGP dla bramy sieci lokalnej drugi hello musi nie nakładają się na powitania poprzedniej bramy sieci lokalnej dla hello takie same lokalnej sieci.

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a>2. Połączenia bramy sieci wirtualnej hello i hello druga Brama sieci lokalnej
Utwórz połączenie hello z TestVNet1 tooSite5_2 "Wartość" Ustaw zbyt$ True

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a>3. Parametry sieci VPN i protokołu BGP dla drugiego lokalnego urządzenia sieci VPN
Podobnie poniższe parametry hello list zostanie wejdzie w hello drugiego urządzenia sieci VPN:

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Po ustaleniu hello połączenia (tunele) należy podwójne nadmiarowe urządzenia sieci VPN i tunele, połączenie sieci lokalnej i Azure:

![podwójny nadmiarowość crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a>Część 3 — ustanowienie połączenia do wirtualnymi aktywny aktywny
W tej sekcji tworzy aktywny aktywny wirtualnymi do połączenia z protokołem BGP. 

Poniższe instrukcje Hello nadal z poprzednich kroków hello wymienionych powyżej. Należy wykonać [część 1](#aagateway) toocreate i skonfiguruj TestVNet1 oraz hello bramy sieci VPN z protokołem BGP. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Krok 1 — Tworzenie TestVNet2 i hello bramy sieci VPN
Jest ważne toomake się, że przestrzeń adresów IP hello nowej sieci wirtualnej hello, TestVNet2, nakłada się ze wszystkimi zakresy sieci wirtualnej.

W tym przykładzie hello sieci wirtualnych należy toohello tej samej subskrypcji. Można skonfigurować do wirtualnymi połączeń między różnych subskrypcji; Zobacz zbyt[skonfigurować połączenia do wirtualnymi](vpn-gateway-vnet-vnet-rm-ps.md) toolearn więcej szczegółowych informacji. Upewnij się, że możesz dodać hello "-wartość $True" podczas tworzenia hello tooenable połączeń protokołu BGP.

#### <a name="1-declare-your-variables"></a>1. Zadeklarowanie zmiennych
Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
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
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
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

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a>3. Tworzenie bramy sieci VPN hello aktywny aktywny dla TestVNet2
Żądanie dwa publiczne adresy toobe toohello przydzielone brama IP utworzone sieci wirtualnej. Zostanie również definiować hello podsieci i wymagane konfiguracje adresów IP.

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

Utwórz bramę sieci VPN hello z hello jako numer i hello flagi "EnableActiveActiveFeature". Należy pamiętać, że konieczne jest przesłonięcie hello domyślny numer ASN w Twojej bramy sieci VPN platformy Azure. Witaj numerów ASN dla hello połączone sieci wirtualne muszą być różne tooenable BGP i routing tranzytowy.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
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

Po wykonaniu tych czynności hello połączenie zostanie nawiązane za kilka minut, a sesji komunikacji równorzędnej BGP hello będą się po zakończeniu hello wirtualnymi do połączenia z nadmiarowością podwójne:

![aktywny aktywny v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a>Część 4 — aktualizacja istniejącej bramy między aktywny aktywny i aktywnego gotowości
Witaj ostatniej sekcji opisano, jak można skonfigurować istniejącą bramę sieci VPN platformy Azure w trybie aktywny tooactive aktywnego gotowości lub na odwrót.

> [!NOTE]
> Ta sekcja zawiera tooresize kroki hello starszej wersji jednostki SKU (stary jednostki SKU) utworzone bramy sieci VPN z tooHighPerformance standardowa. Te kroki nie uaktualniaj starego tooone starszej wersji jednostki SKU z hello nowe jednostki SKU.
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a>Skonfiguruj bramę aktywny tooactive aktywnego gotowości bramy
#### <a name="1-gateway-parameters"></a>1. Parametry bramy
Poniższy przykład Hello konwertuje bramy aktywnego gotowości bramy aktywny aktywny. Możesz toocreate innym publicznym adresem IP, a następnie dodać drugi konfigurację IP bramy. Poniżej przedstawiono hello używane parametry:

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a>2. Utwórz hello publicznego adresu IP, a następnie dodaj hello drugi konfiguracji IP bramy

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a>3. Włącz bramę hello aktywny aktywny tryb i aktualizacji
Witaj obiektu bramy musi być ustawiona w PowerShell tootrigger hello rzeczywistej aktualizacji. Jednostka SKU bramy sieci wirtualnej hello Hello musi również zostać zmieniony tooHighPerformance (po zmianie rozmiaru), ponieważ zostało utworzone wcześniej jako Standard.

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

Ta aktualizacja może potrwać 30 minut too45.

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a>Skonfiguruj bramę wstrzymania tooactive aktywny aktywny bramy
#### <a name="1-gateway-parameters"></a>1. Parametry bramy
Użyj hello takie same parametry jak wyżej, uzyskać nazwę hello hello konfiguracji adresu IP ma tooremove.

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a>2. Usuń konfigurację IP bramy hello i wyłączyć hello aktywny aktywny tryb
Podobnie należy ustawić obiektu bramy hello w PowerShell tootrigger hello rzeczywistej aktualizacji.

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

Ta aktualizacja może potrwać too30 zbyt 45 minut.

## <a name="next-steps"></a>Następne kroki
Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
