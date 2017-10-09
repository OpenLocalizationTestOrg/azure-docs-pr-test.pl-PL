---
title: "aaaAbout 3 strona bramy sieci VPN urządzenia konfiguracji tooconnect tooAzure VPN | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie 3 konfiguracji urządzenia sieci VPN firmy podłączania tooAzure bramy sieci VPN."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 3bb4fc94bc625386c2d0a02e1dcbdeb38ee0665e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>Omówienie 3 konfiguracji urządzenia sieci VPN firmy
Ten artykuł zawiera omówienie lokalnej konfiguracji urządzenia sieci VPN dla połączenia bramy sieci VPN tooAzure. Przykładowe Hello sieci wirtualnej platformy Azure i sieci VPN bramy Instalator będzie używana tooconnect toodifferent lokalnej sieci VPN urządzenia z hello takie same parametry.

## <a name="device-requirements"></a>Wymagania dotyczące urządzeń
Bramy sieci VPN platformy Azure na użytek standardowych pakietów protokołu IPsec i IKE tunel S2S VPN. Odwołuje się zbyt[urządzenia sieci VPN o](vpn-gateway-about-vpn-devices.md) dla hello szczegółowe parametry protokołu IPsec i IKE i domyślne algorytmów kryptograficznych dla bram sieci VPN platformy Azure. Opcjonalnie można określić kombinację dokładne hello algorytmów kryptograficznych i kluczy sile dla określonego połączenia, zgodnie z opisem w [o wymaganiach dotyczących kryptograficznych](vpn-gateway-about-compliance-crypto.md).

## <a name ="singletunnel"></a>Jeden tunel VPN
Topologia pierwszy Hello składa się z jednego tunelu S2S VPN między bramą sieci VPN platformy Azure i lokalnego urządzenia sieci VPN. Opcjonalnie można skonfigurować protokołu BGP przez tunel VPN hello.

![jednego tunelu](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

Odwołuje się zbyt[konfigurowania połączenia lokacja lokacja](vpn-gateway-howto-site-to-site-resource-manager-portal.md) wskazówki szczegółowe, krok po kroku. Hello poniższych sekcjach znajduje się lista parametrów hello i Podaj próbki toohelp skrypt programu PowerShell, możesz rozpocząć pracę.

### <a name="network-and-vpn-gateway-information"></a>Informacji bramy sieci VPN i sieci
W tej sekcji znajduje się lista parametrów hello przykłady hello powyżej.

| **Parametr**                | **Wartość**                    |
| ---                          | ---                          |
| Prefiksy adresów sieci wirtualnej        | 10.11.0.0/16<br>10.12.0.0/16 |
| Adres IP bramy sieci VPN platformy Azure         | Brama sieci VPN platformy Azure IP         |
| Prefiksy adresów lokalnych | 10.51.0.0/16<br>10.52.0.0/16 |
| Lokalny adres IP urządzenia sieci VPN    | Lokalny adres IP urządzenia sieci VPN    |
| * Numer ASN BGP sieci wirtualnej                | 65010                        |
| * Azure IP elementu równorzędnego protokołu BGP           | 10.12.255.30                 |
| * Lokalnymi BGP ASN         | 65050                        |
| * IP elementu równorzędnego BGP lokalnej     | 10.52.255.254                |

* (*) Parametry opcjonalne dla protokołu BGP tylko

### <a name="sample-powershell-script"></a>Przykładowy skrypt programu PowerShell
[Utwórz połączenie sieci VPN S2S przy użyciu programu PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) ma hello szczegółowe instrukcje. Ta sekcja zawiera przykładowe tooget skryptu, uruchamiany.

```powershell
# Declare your variables

$Sub1          = "Replace_With_Your_Subcription_Name"
$RG1           = "TestRG1"
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
$VNet1ASN      = 65010
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GWIPName1     = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection15  = "VNet1toSite5"
$LNGName5      = "Site5"
$LNGPrefix50   = "10.52.255.254/32"
$LNGPrefix51   = "10.51.0.0/16"
$LNGPrefix52   = "10.52.0.0/16"
$LNGIP5        = "Your_VPN_Device_IP"
$LNGASN5       = 65050
$BGPPeerIP5    = "10.52.255.254"

# Connect tooyour subscription and create a new resource group

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1

# Create virtual network

$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

# Create VPN gateway

$gwpip1    = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1     = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN

# Create local network gateway

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix51,$LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5

# Create hello S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <a name ="policybased"></a>[Opcjonalnie] Za pomocą niestandardowych zasad IPsec i IKE z "UsePolicyBasedTrafficSelectors"
Jeśli urządzenia sieci VPN nie obsługują selektorów "dowolny z każdym" ruchu (na podstawie/VTI-opartej na trasach konfiguracji), należy toocreate niestandardowych zasad IPsec i IKE, a Skonfiguruj opcję "UsePolicyBasedTrafficSelectors", zgodnie z opisem w [w tym artykule ](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> Należy toocreate zasady IPsec i IKE w kolejności tooenable opcji "UsePolicyBasedTrafficSelectors" hello połączenia.

Witaj Poniższy przykładowy skrypt tworzy zasady IPsec i IKE z hello algorytmów i parametry:
* IKEv2: DHGroup24 AES256, SHA384
* Protokół IPsec: AES256 SHA1, PFS24, skojarzenia zabezpieczeń okres istnienia 7200 sekund & 20480000KB (20GB)

Następnie stosuje hello zasad i umożliwia "UesPolicyBasedTrafficSelectors" hello połączenia.

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[Opcjonalnie] Użyj protokołu BGP dla połączenia sieci VPN S2S
Można opcjonalnie użyć protokołu BGP na powitania połączenia. Zobacz [BGP dla bramy sieci VPN](vpn-gateway-bgp-resource-manager-ps.md). Istnieją dwie różnice:

prefiksy adresów lokalne powitania można adres jednego hosta, adres IP elementu równorzędnego protokołu BGP lokalne powitania:

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

Należy ustawić "-wartość" zbyt$ True podczas tworzenia połączenia hello:

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>Następne kroki
Zobacz [konfigurowania bramy sieci VPN aktywny-aktywny między lokalizacjami i połączeń między wirtualnymi do](vpn-gateway-activeactive-rm-powershell.md) procedury tooconfigure aktywny aktywny między lokalizacjami i połączeń do wirtualnymi.

