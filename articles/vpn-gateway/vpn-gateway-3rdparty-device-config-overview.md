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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="098f5-103">Omówienie 3 konfiguracji urządzenia sieci VPN firmy</span><span class="sxs-lookup"><span data-stu-id="098f5-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="098f5-104">Ten artykuł zawiera omówienie lokalnej konfiguracji urządzenia sieci VPN dla połączenia bramy sieci VPN tooAzure.</span><span class="sxs-lookup"><span data-stu-id="098f5-104">This article provides an overview of on-premises VPN device configurations for connecting tooAzure VPN gateways.</span></span> <span data-ttu-id="098f5-105">Przykładowe Hello sieci wirtualnej platformy Azure i sieci VPN bramy Instalator będzie używana tooconnect toodifferent lokalnej sieci VPN urządzenia z hello takie same parametry.</span><span class="sxs-lookup"><span data-stu-id="098f5-105">hello sample Azure virtual network and VPN gateway setup will be used tooconnect toodifferent on-premises VPN devices with hello same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="098f5-106">Wymagania dotyczące urządzeń</span><span class="sxs-lookup"><span data-stu-id="098f5-106">Device requirements</span></span>
<span data-ttu-id="098f5-107">Bramy sieci VPN platformy Azure na użytek standardowych pakietów protokołu IPsec i IKE tunel S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="098f5-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="098f5-108">Odwołuje się zbyt[urządzenia sieci VPN o](vpn-gateway-about-vpn-devices.md) dla hello szczegółowe parametry protokołu IPsec i IKE i domyślne algorytmów kryptograficznych dla bram sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="098f5-108">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="098f5-109">Opcjonalnie można określić kombinację dokładne hello algorytmów kryptograficznych i kluczy sile dla określonego połączenia, zgodnie z opisem w [o wymaganiach dotyczących kryptograficznych](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="098f5-109">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="098f5-110"><a name ="singletunnel"></a>Jeden tunel VPN</span><span class="sxs-lookup"><span data-stu-id="098f5-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="098f5-111">Topologia pierwszy Hello składa się z jednego tunelu S2S VPN między bramą sieci VPN platformy Azure i lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="098f5-111">hello first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="098f5-112">Opcjonalnie można skonfigurować protokołu BGP przez tunel VPN hello.</span><span class="sxs-lookup"><span data-stu-id="098f5-112">You can optionally configure BGP across hello VPN tunnel.</span></span>

![jednego tunelu](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="098f5-114">Odwołuje się zbyt[konfigurowania połączenia lokacja lokacja](vpn-gateway-howto-site-to-site-resource-manager-portal.md) wskazówki szczegółowe, krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="098f5-114">Refer too[Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="098f5-115">Hello poniższych sekcjach znajduje się lista parametrów hello i Podaj próbki toohelp skrypt programu PowerShell, możesz rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="098f5-115">hello following sections list hello parameters and provide a sample PowerShell script toohelp you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="098f5-116">Informacji bramy sieci VPN i sieci</span><span class="sxs-lookup"><span data-stu-id="098f5-116">Network and VPN gateway information</span></span>
<span data-ttu-id="098f5-117">W tej sekcji znajduje się lista parametrów hello przykłady hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="098f5-117">This section list hello parameters for hello examples above.</span></span>

| <span data-ttu-id="098f5-118">**Parametr**</span><span class="sxs-lookup"><span data-stu-id="098f5-118">**Parameter**</span></span>                | <span data-ttu-id="098f5-119">**Wartość**</span><span class="sxs-lookup"><span data-stu-id="098f5-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="098f5-120">Prefiksy adresów sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="098f5-120">VNet address prefixes</span></span>        | <span data-ttu-id="098f5-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="098f5-121">10.11.0.0/16</span></span><br><span data-ttu-id="098f5-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="098f5-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="098f5-123">Adres IP bramy sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="098f5-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="098f5-124">Brama sieci VPN platformy Azure IP</span><span class="sxs-lookup"><span data-stu-id="098f5-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="098f5-125">Prefiksy adresów lokalnych</span><span class="sxs-lookup"><span data-stu-id="098f5-125">On-premises address prefixes</span></span> | <span data-ttu-id="098f5-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="098f5-126">10.51.0.0/16</span></span><br><span data-ttu-id="098f5-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="098f5-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="098f5-128">Lokalny adres IP urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="098f5-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="098f5-129">Lokalny adres IP urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="098f5-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="098f5-130">* Numer ASN BGP sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="098f5-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="098f5-131">65010</span><span class="sxs-lookup"><span data-stu-id="098f5-131">65010</span></span>                        |
| <span data-ttu-id="098f5-132">* Azure IP elementu równorzędnego protokołu BGP</span><span class="sxs-lookup"><span data-stu-id="098f5-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="098f5-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="098f5-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="098f5-134">* Lokalnymi BGP ASN</span><span class="sxs-lookup"><span data-stu-id="098f5-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="098f5-135">65050</span><span class="sxs-lookup"><span data-stu-id="098f5-135">65050</span></span>                        |
| <span data-ttu-id="098f5-136">* IP elementu równorzędnego BGP lokalnej</span><span class="sxs-lookup"><span data-stu-id="098f5-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="098f5-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="098f5-137">10.52.255.254</span></span>                |

* <span data-ttu-id="098f5-138">(*) Parametry opcjonalne dla protokołu BGP tylko</span><span class="sxs-lookup"><span data-stu-id="098f5-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="098f5-139">Przykładowy skrypt programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="098f5-139">Sample PowerShell script</span></span>
<span data-ttu-id="098f5-140">[Utwórz połączenie sieci VPN S2S przy użyciu programu PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) ma hello szczegółowe instrukcje.</span><span class="sxs-lookup"><span data-stu-id="098f5-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has hello detailed instructions.</span></span> <span data-ttu-id="098f5-141">Ta sekcja zawiera przykładowe tooget skryptu, uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="098f5-141">This section provides a sample script tooget you started.</span></span>

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

### <span data-ttu-id="098f5-142"><a name ="policybased"></a>[Opcjonalnie] Za pomocą niestandardowych zasad IPsec i IKE z "UsePolicyBasedTrafficSelectors"</span><span class="sxs-lookup"><span data-stu-id="098f5-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="098f5-143">Jeśli urządzenia sieci VPN nie obsługują selektorów "dowolny z każdym" ruchu (na podstawie/VTI-opartej na trasach konfiguracji), należy toocreate niestandardowych zasad IPsec i IKE, a Skonfiguruj opcję "UsePolicyBasedTrafficSelectors", zgodnie z opisem w [w tym artykule ](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="098f5-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need toocreate a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="098f5-144">Należy toocreate zasady IPsec i IKE w kolejności tooenable opcji "UsePolicyBasedTrafficSelectors" hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="098f5-144">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="098f5-145">Witaj Poniższy przykładowy skrypt tworzy zasady IPsec i IKE z hello algorytmów i parametry:</span><span class="sxs-lookup"><span data-stu-id="098f5-145">hello sample script below creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="098f5-146">IKEv2: DHGroup24 AES256, SHA384</span><span class="sxs-lookup"><span data-stu-id="098f5-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="098f5-147">Protokół IPsec: AES256 SHA1, PFS24, skojarzenia zabezpieczeń okres istnienia 7200 sekund & 20480000KB (20GB)</span><span class="sxs-lookup"><span data-stu-id="098f5-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="098f5-148">Następnie stosuje hello zasad i umożliwia "UesPolicyBasedTrafficSelectors" hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="098f5-148">It then applies hello policy and enables "UesPolicyBasedTrafficSelectors" on hello connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="098f5-149"><a name ="bgp"></a>[Opcjonalnie] Użyj protokołu BGP dla połączenia sieci VPN S2S</span><span class="sxs-lookup"><span data-stu-id="098f5-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="098f5-150">Można opcjonalnie użyć protokołu BGP na powitania połączenia.</span><span class="sxs-lookup"><span data-stu-id="098f5-150">You can optionally use BGP on hello connection.</span></span> <span data-ttu-id="098f5-151">Zobacz [BGP dla bramy sieci VPN](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="098f5-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="098f5-152">Istnieją dwie różnice:</span><span class="sxs-lookup"><span data-stu-id="098f5-152">There are two differences:</span></span>

<span data-ttu-id="098f5-153">prefiksy adresów lokalne powitania można adres jednego hosta, adres IP elementu równorzędnego protokołu BGP lokalne powitania:</span><span class="sxs-lookup"><span data-stu-id="098f5-153">hello on-premises address prefixes can be a single host address, hello on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="098f5-154">Należy ustawić "-wartość" zbyt$ True podczas tworzenia połączenia hello:</span><span class="sxs-lookup"><span data-stu-id="098f5-154">You must set "-EnableBGP" too$True when creating hello connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="098f5-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="098f5-155">Next steps</span></span>
<span data-ttu-id="098f5-156">Zobacz [konfigurowania bramy sieci VPN aktywny-aktywny między lokalizacjami i połączeń między wirtualnymi do](vpn-gateway-activeactive-rm-powershell.md) procedury tooconfigure aktywny aktywny między lokalizacjami i połączeń do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="098f5-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

