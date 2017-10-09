---
title: "Połączenia sieci VPN platformy Azure bram toomultiple urządzeń lokalnych, na podstawie zasad sieci VPN: usługi Azure Resource Manager: programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono konfigurowanie Azure opartej na trasach urządzenia sieci VPN bramy toomultiple na podstawie zasad sieci VPN za pomocą usługi Azure Resource Manager i programu PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a>Połączenia sieci VPN platformy Azure bram toomultiple urządzeń lokalnych, na podstawie zasad sieci VPN przy użyciu programu PowerShell

W tym artykule opisano, jak skonfigurować Azure opartej na trasach sieci VPN bramy tooconnect toomultiple urządzeń lokalnych, na podstawie zasad sieci VPN korzystania z niestandardowych zasad IPsec i IKE połączeń sieci VPN S2S.

## <a name="about-policy-based-and-route-based-vpn-gateways"></a>Temat bram sieci VPN opartych na zasadach i opartej na trasach

Zasady - *a* opartej na trasach urządzenia sieci VPN różnią się w konfiguracji selektorów ruchu IPsec hello połączenia:

* **Oparte na zasadach** urządzenia sieci VPN przy użyciu kombinacji hello prefiksy z obu toodefine sieci, jak ruch jest szyfrowany/odszyfrowywany przez tunel protokołu IPsec. Zazwyczaj jest tworzony na urządzeniach zapory, które wykonują filtrowanie pakietów. Protokół IPsec tunelu szyfrowania i odszyfrowywania są dodawane filtrowanie pakietów toohello i aparat przetwarzania.
* **Oparte na trasach** urządzenia sieci VPN przy użyciu dowolnego z każdym (symbol wieloznaczny) ruchu selektorów, a let routingu przekazywania tabele tuneli IPsec toodifferent bezpośredniego ruchu. Zazwyczaj jest tworzony na platformach routera, gdzie każdy tunelu IPsec ma formę interfejsu sieciowego lub VTI (interfejsu tunelu wirtualnej).

Witaj poniższych diagramach wyróżnić dwa modele hello:

### <a name="policy-based-vpn-example"></a>Przykład sieci VPN opartych na zasadach
![oparte na zasadach](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a>Przykład sieci VPN opartej na trasach
![oparte na trasach](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a>Pomocy technicznej platformy Azure dla sieci VPN opartych na zasadach
Obecnie usługa Azure obsługuje oba tryby bramy sieci VPN: opartej na trasach bramy sieci VPN i bramy sieci VPN opartych na zasadach. Zostały one utworzone na różnych platformach wewnętrznego, które powodują różne specyfikacje:

|                          | **Brama sieci VPN PolicyBased** | **Brama sieci VPN z siecią typu RouteBased**               |
| ---                      | ---                         | ---                                      |
| **Jednostka SKU bramy Azure**    | Podstawowa                       | Basic, Standard, wysokowydajnej         |
| **Wersja IKE**          | IKEv1                       | IKEv2                                    |
| **Maks. Połączeń S2S** | **1**                       | Basic/Standard: 10<br> Wysokowydajnej: 30 |
|                          |                             |                                          |

Za pomocą niestandardowych zasad IPsec i IKE hello można teraz skonfigurować Azure opartej na trasach VPN bramy toouse ruchu na podstawie prefiksu selektorów z opcją "**PolicyBasedTrafficSelectors**", urządzenia sieci VPN opartych na zasadach lokalnych tooon tooconnect. Ta funkcja umożliwia tooconnect z sieci wirtualnej platformy Azure i toomultiple bramy sieci VPN opartych na zasadach urządzenia sieci VPN/zapory usuwanie hello limit pojedynczego połączenia z hello bieżącej platformy Azure na podstawie zasad bramy sieci VPN lokalnymi.

> [!IMPORTANT]
> 1. tooenable to połączenie, musi obsługiwać lokalnego urządzenia sieci VPN opartych na zasadach **IKEv2** tooconnect toohello Azure opartej na trasach bramy sieci VPN. Sprawdź specyfikację urządzenia sieci VPN.
> 2. Hello lokalnej sieci łączących się za pośrednictwem urządzenia sieci VPN opartych na zasadach z mechanizm ten może łączyć się tylko z toohello sieci wirtualnej platformy Azure; **nie można ich przesyłania tooother sieci lokalnej lub sieci wirtualnych za pośrednictwem hello tej samej bramy sieci VPN platformy Azure**.
> 3. Opcja konfiguracji Hello jest częścią niestandardowych zasad IPsec i IKE połączenia hello. Po włączeniu hello ruchu na podstawie zasad selektor, opcja należy określić zasady pełną hello (algorytmów szyfrowania i integralności IPsec i IKE, silnych kluczy i okresy istnienia SA).

powitania po diagram przedstawia Dlaczego routing tranzytowy za pośrednictwem bramy sieci VPN platformy Azure nie działa z opcją opartych na zasadach hello:

![przesyłania opartych na zasadach](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

Jak pokazano na diagramie hello, hello bramy sieci VPN platformy Azure ma selektorów ruchu z tooeach sieci wirtualnej hello prefiksy sieci lokalne powitania, ale nie hello połączenia między prefiksy. Na przykład lokalnej lokacji 2, lokacji 3 i 4 lokacji można każdego komunikacji tooVNet1 odpowiednio, ale nie można połączyć za pośrednictwem hello sieci VPN platformy Azure bramy tooeach innych. Witaj diagram przedstawia hello krzyżowe ruchu selektorów, które nie są dostępne w hello bramy sieci VPN platformy Azure zgodnie z tą konfiguracją.

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a>Konfigurowanie połączenia selektorów ruchu na podstawie zasad

Witaj instrukcje w tym wykonaj artykułu hello sam przykład zgodnie z opisem w [zasady IPsec/IKE skonfigurować dla połączeń S2S lub wirtualnymi do](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish połączenia sieci VPN S2S. Przedstawiono to w powitania po diagramu:

![zasady s2s](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

Witaj połączeń tooenable przepływu pracy:
1. Tworzenie sieci wirtualnej hello, Brama sieci VPN i bramy sieci lokalnej dla połączenia między lokalizacjami
2. Tworzenie zasad IPsec i IKE
3. Zastosuj zasady hello, podczas tworzenia połączenia S2S lub do wirtualnymi i **włączyć hello selektorów ruchu na podstawie zasad** hello połączenia
4. Jeśli połączenie hello jest już utworzony, można zastosować lub zaktualizować hello zasad tooan istniejącego połączenia

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a>Włącz selektorów opartych na zasadach ruchu dla połączenia

Upewnij się, że zostały wykonane [część 3 artykułu zasad IPsec/IKE skonfigurować hello](vpn-gateway-ipsecikepolicy-rm-powershell.md) dla tej sekcji. Witaj przykładzie użyto następujących hello same parametry i kroki:

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>Krok 1 — Tworzenie sieci wirtualnej hello, Brama sieci VPN i bramy sieci lokalnej

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a>1. Deklarowanie zmiennych i połączenia tooyour subskrypcji
W tym ćwiczeniu Rozpoczniemy przez zadeklarowanie naszych zmiennych. Należy się, że wartości hello tooreplace własnymi podczas konfigurowania w środowisku produkcyjnym.

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
Witaj toouse poleceń cmdlet Menedżera zasobów, upewnij się, że Przełącz tryb tooPowerShell. Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).

Otwórz konsolę programu PowerShell i Połącz konto tooyour. Użyj następujących hello przykładowe toohelp, gdy nawiązujesz połączenie:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>2. Tworzenie sieci wirtualnej hello, Brama sieci VPN i bramy sieci lokalnej
Witaj poniższy przykład tworzy hello sieci wirtualnej, TestVNet1 z trzech podsieci i hello bramy sieci VPN. Zastępowanie wartości, jest ważne, aby zawsze nazwę podsieci bramy w szczególności "GatewaySubnet". W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a>Krok 2 — Tworzenie połączenia sieci VPN S2S przy użyciu zasad IPsec i IKE

#### <a name="1-create-an-ipsecike-policy"></a>1. Tworzenie zasad IPsec i IKE

> [!IMPORTANT]
> Należy toocreate zasady IPsec i IKE w kolejności tooenable opcji "UsePolicyBasedTrafficSelectors" hello połączenia.

Witaj poniższy przykład tworzy zasady IPsec i IKE z te algorytmy i parametry:
* IKEv2: DHGroup24 AES256, SHA384
* Protokół IPsec: AES256, SHA256, PFS24, skojarzenia zabezpieczeń okres istnienia 3600 s & 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a>2. Utwórz połączenie sieci VPN S2S hello z selektorów ruchu na podstawie zasad i zasady IPsec/IKE
Tworzenie połączenia sieci VPN S2S i stosowanie zasad IPsec i IKE hello utworzony w poprzednim kroku hello. Należy pamiętać o hello dodatkowy parametr "-UsePolicyBasedTrafficSelectors $True" co pozwala selektorów ruchu na podstawie zasad na powitania połączenia.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

Po wykonaniu czynności hello hello połączenia sieci VPN S2S będzie używać hello zdefiniowane zasady IPsec i IKE i Włącz selektorów ruchu na podstawie zasad na powitania połączenia. Możesz powtarzać hello same kroki tooadd więcej połączeń tooadditional urządzeń lokalnych, na podstawie zasad sieci VPN z hello tej samej bramy sieci VPN platformy Azure.

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a>Zaktualizuj selektorów opartych na zasadach ruchu dla połączenia
Hello ostatniej sekcji pokazano, jak opcja tooupdate hello ruchu na podstawie zasad selektory dla istniejącego połączenia sieci VPN S2S.

### <a name="1-get-hello-connection"></a>1. Pobierz dane o połączeniu hello
Pobierz zasób połączenia hello.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a>2. Zaznacz opcję selektorów, hello ruchu na podstawie zasad
Witaj następujący wiersz zawiera czy selektorów ruchu na podstawie zasad hello są używane do połączenia hello:

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

Jeśli wiersz hello zwraca "**True**", następnie selektorów ruchu na podstawie zasad są skonfigurowane na powitania połączenia; w przeciwnym razie zwraca wartość "**False**."

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a>3. Zaktualizuj selektorów ruchu na podstawie zasad hello połączenia
Po uzyskaniu hello zasobu połączenia, można włączyć lub wyłączyć opcję hello.

#### <a name="disable-usepolicybasedtrafficselectors"></a>Wyłącz UsePolicyBasedTrafficSelectors
Witaj poniższy przykład wyłącza hello ruchu na podstawie zasad selektorów opcję, ale pozostawia hello zasad IPsec i IKE bez zmian:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a>Włącz UsePolicyBasedTrafficSelectors
Witaj poniższy przykład umożliwia włączenie opcji selektorów ruchu na podstawie zasad hello, ale pozostawia hello zasad IPsec i IKE bez zmian:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a>Następne kroki
Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Sprawdź również [zasady IPsec/IKE skonfigurować dla połączeń sieci VPN S2S lub wirtualnymi do](vpn-gateway-ipsecikepolicy-rm-powershell.md) uzyskać więcej informacji dotyczących zasad protokołu IPsec/IKE niestandardowych.
