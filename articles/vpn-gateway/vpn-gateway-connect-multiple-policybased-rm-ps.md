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
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="d3261-103">Połączenia sieci VPN platformy Azure bram toomultiple urządzeń lokalnych, na podstawie zasad sieci VPN przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3261-103">Connect Azure VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="d3261-104">W tym artykule opisano, jak skonfigurować Azure opartej na trasach sieci VPN bramy tooconnect toomultiple urządzeń lokalnych, na podstawie zasad sieci VPN korzystania z niestandardowych zasad IPsec i IKE połączeń sieci VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="d3261-104">This article helps you configure an Azure route-based VPN gateway tooconnect toomultiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="d3261-105">Temat bram sieci VPN opartych na zasadach i opartej na trasach</span><span class="sxs-lookup"><span data-stu-id="d3261-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="d3261-106">Zasady - *a* opartej na trasach urządzenia sieci VPN różnią się w konfiguracji selektorów ruchu IPsec hello połączenia:</span><span class="sxs-lookup"><span data-stu-id="d3261-106">Policy- *vs.* route-based VPN devices differ in how hello IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="d3261-107">**Oparte na zasadach** urządzenia sieci VPN przy użyciu kombinacji hello prefiksy z obu toodefine sieci, jak ruch jest szyfrowany/odszyfrowywany przez tunel protokołu IPsec.</span><span class="sxs-lookup"><span data-stu-id="d3261-107">**Policy-based** VPN devices use hello combinations of prefixes from both networks toodefine how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="d3261-108">Zazwyczaj jest tworzony na urządzeniach zapory, które wykonują filtrowanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="d3261-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="d3261-109">Protokół IPsec tunelu szyfrowania i odszyfrowywania są dodawane filtrowanie pakietów toohello i aparat przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="d3261-109">IPsec tunnel encryption and decryption are added toohello packet filtering and processing engine.</span></span>
* <span data-ttu-id="d3261-110">**Oparte na trasach** urządzenia sieci VPN przy użyciu dowolnego z każdym (symbol wieloznaczny) ruchu selektorów, a let routingu przekazywania tabele tuneli IPsec toodifferent bezpośredniego ruchu.</span><span class="sxs-lookup"><span data-stu-id="d3261-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic toodifferent IPsec tunnels.</span></span> <span data-ttu-id="d3261-111">Zazwyczaj jest tworzony na platformach routera, gdzie każdy tunelu IPsec ma formę interfejsu sieciowego lub VTI (interfejsu tunelu wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="d3261-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="d3261-112">Witaj poniższych diagramach wyróżnić dwa modele hello:</span><span class="sxs-lookup"><span data-stu-id="d3261-112">hello following diagrams highlight hello two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="d3261-113">Przykład sieci VPN opartych na zasadach</span><span class="sxs-lookup"><span data-stu-id="d3261-113">Policy-based VPN example</span></span>
![oparte na zasadach](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="d3261-115">Przykład sieci VPN opartej na trasach</span><span class="sxs-lookup"><span data-stu-id="d3261-115">Route-based VPN example</span></span>
![oparte na trasach](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="d3261-117">Pomocy technicznej platformy Azure dla sieci VPN opartych na zasadach</span><span class="sxs-lookup"><span data-stu-id="d3261-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="d3261-118">Obecnie usługa Azure obsługuje oba tryby bramy sieci VPN: opartej na trasach bramy sieci VPN i bramy sieci VPN opartych na zasadach.</span><span class="sxs-lookup"><span data-stu-id="d3261-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="d3261-119">Zostały one utworzone na różnych platformach wewnętrznego, które powodują różne specyfikacje:</span><span class="sxs-lookup"><span data-stu-id="d3261-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="d3261-120">**Brama sieci VPN PolicyBased**</span><span class="sxs-lookup"><span data-stu-id="d3261-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="d3261-121">**Brama sieci VPN z siecią typu RouteBased**</span><span class="sxs-lookup"><span data-stu-id="d3261-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="d3261-122">**Jednostka SKU bramy Azure**</span><span class="sxs-lookup"><span data-stu-id="d3261-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="d3261-123">Podstawowa</span><span class="sxs-lookup"><span data-stu-id="d3261-123">Basic</span></span>                       | <span data-ttu-id="d3261-124">Basic, Standard, wysokowydajnej</span><span class="sxs-lookup"><span data-stu-id="d3261-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="d3261-125">**Wersja IKE**</span><span class="sxs-lookup"><span data-stu-id="d3261-125">**IKE version**</span></span>          | <span data-ttu-id="d3261-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="d3261-126">IKEv1</span></span>                       | <span data-ttu-id="d3261-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="d3261-127">IKEv2</span></span>                                    |
| <span data-ttu-id="d3261-128">**Maks. Połączeń S2S**</span><span class="sxs-lookup"><span data-stu-id="d3261-128">**Max. S2S connections**</span></span> | <span data-ttu-id="d3261-129">**1**</span><span class="sxs-lookup"><span data-stu-id="d3261-129">**1**</span></span>                       | <span data-ttu-id="d3261-130">Basic/Standard: 10</span><span class="sxs-lookup"><span data-stu-id="d3261-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="d3261-131">Wysokowydajnej: 30</span><span class="sxs-lookup"><span data-stu-id="d3261-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="d3261-132">Za pomocą niestandardowych zasad IPsec i IKE hello można teraz skonfigurować Azure opartej na trasach VPN bramy toouse ruchu na podstawie prefiksu selektorów z opcją "**PolicyBasedTrafficSelectors**", urządzenia sieci VPN opartych na zasadach lokalnych tooon tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d3261-132">With hello custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways toouse prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", tooconnect tooon-premises policy-based VPN devices.</span></span> <span data-ttu-id="d3261-133">Ta funkcja umożliwia tooconnect z sieci wirtualnej platformy Azure i toomultiple bramy sieci VPN opartych na zasadach urządzenia sieci VPN/zapory usuwanie hello limit pojedynczego połączenia z hello bieżącej platformy Azure na podstawie zasad bramy sieci VPN lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="d3261-133">This capability allows you tooconnect from an Azure virtual network and VPN gateway toomultiple on-premises policy-based VPN/firewall devices, removing hello single connection limit from hello current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="d3261-134">tooenable to połączenie, musi obsługiwać lokalnego urządzenia sieci VPN opartych na zasadach **IKEv2** tooconnect toohello Azure opartej na trasach bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="d3261-134">tooenable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** tooconnect toohello Azure route-based VPN gateways.</span></span> <span data-ttu-id="d3261-135">Sprawdź specyfikację urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="d3261-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="d3261-136">Hello lokalnej sieci łączących się za pośrednictwem urządzenia sieci VPN opartych na zasadach z mechanizm ten może łączyć się tylko z toohello sieci wirtualnej platformy Azure; **nie można ich przesyłania tooother sieci lokalnej lub sieci wirtualnych za pośrednictwem hello tej samej bramy sieci VPN platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="d3261-136">hello on-premises networks connecting through policy-based VPN devices with this mechanism can only connect toohello Azure virtual network; **they cannot transit tooother on-premises networks or virtual networks via hello same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="d3261-137">Opcja konfiguracji Hello jest częścią niestandardowych zasad IPsec i IKE połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="d3261-137">hello configuration option is part of hello custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="d3261-138">Po włączeniu hello ruchu na podstawie zasad selektor, opcja należy określić zasady pełną hello (algorytmów szyfrowania i integralności IPsec i IKE, silnych kluczy i okresy istnienia SA).</span><span class="sxs-lookup"><span data-stu-id="d3261-138">If you enable hello policy-based traffic selector option, you must specify hello complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="d3261-139">powitania po diagram przedstawia Dlaczego routing tranzytowy za pośrednictwem bramy sieci VPN platformy Azure nie działa z opcją opartych na zasadach hello:</span><span class="sxs-lookup"><span data-stu-id="d3261-139">hello following diagram shows why transit routing via Azure VPN gateway doesn't work with hello policy-based option:</span></span>

![przesyłania opartych na zasadach](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="d3261-141">Jak pokazano na diagramie hello, hello bramy sieci VPN platformy Azure ma selektorów ruchu z tooeach sieci wirtualnej hello prefiksy sieci lokalne powitania, ale nie hello połączenia między prefiksy.</span><span class="sxs-lookup"><span data-stu-id="d3261-141">As shown in hello diagram, hello Azure VPN gateway has traffic selectors from hello virtual network tooeach of hello on-premises network prefixes, but not hello cross-connection prefixes.</span></span> <span data-ttu-id="d3261-142">Na przykład lokalnej lokacji 2, lokacji 3 i 4 lokacji można każdego komunikacji tooVNet1 odpowiednio, ale nie można połączyć za pośrednictwem hello sieci VPN platformy Azure bramy tooeach innych.</span><span class="sxs-lookup"><span data-stu-id="d3261-142">For example, on-premises site 2, site 3, and site 4 can each communicate tooVNet1 respectively, but cannot connect via hello Azure VPN gateway tooeach other.</span></span> <span data-ttu-id="d3261-143">Witaj diagram przedstawia hello krzyżowe ruchu selektorów, które nie są dostępne w hello bramy sieci VPN platformy Azure zgodnie z tą konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="d3261-143">hello diagram shows hello cross-connect traffic selectors that are not available in hello Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="d3261-144">Konfigurowanie połączenia selektorów ruchu na podstawie zasad</span><span class="sxs-lookup"><span data-stu-id="d3261-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="d3261-145">Witaj instrukcje w tym wykonaj artykułu hello sam przykład zgodnie z opisem w [zasady IPsec/IKE skonfigurować dla połączeń S2S lub wirtualnymi do](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish połączenia sieci VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="d3261-145">hello instructions in this article follow hello same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish a S2S VPN connection.</span></span> <span data-ttu-id="d3261-146">Przedstawiono to w powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="d3261-146">This is shown in hello following diagram:</span></span>

![zasady s2s](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="d3261-148">Witaj połączeń tooenable przepływu pracy:</span><span class="sxs-lookup"><span data-stu-id="d3261-148">hello workflow tooenable this connectivity:</span></span>
1. <span data-ttu-id="d3261-149">Tworzenie sieci wirtualnej hello, Brama sieci VPN i bramy sieci lokalnej dla połączenia między lokalizacjami</span><span class="sxs-lookup"><span data-stu-id="d3261-149">Create hello virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="d3261-150">Tworzenie zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="d3261-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="d3261-151">Zastosuj zasady hello, podczas tworzenia połączenia S2S lub do wirtualnymi i **włączyć hello selektorów ruchu na podstawie zasad** hello połączenia</span><span class="sxs-lookup"><span data-stu-id="d3261-151">Apply hello policy when you create a S2S or VNet-to-VNet connection, and **enable hello policy-based traffic selectors** on hello connection</span></span>
4. <span data-ttu-id="d3261-152">Jeśli połączenie hello jest już utworzony, można zastosować lub zaktualizować hello zasad tooan istniejącego połączenia</span><span class="sxs-lookup"><span data-stu-id="d3261-152">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="d3261-153">Włącz selektorów opartych na zasadach ruchu dla połączenia</span><span class="sxs-lookup"><span data-stu-id="d3261-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="d3261-154">Upewnij się, że zostały wykonane [część 3 artykułu zasad IPsec/IKE skonfigurować hello](vpn-gateway-ipsecikepolicy-rm-powershell.md) dla tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d3261-154">Make sure you have completed [Part 3 of hello Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="d3261-155">Witaj przykładzie użyto następujących hello same parametry i kroki:</span><span class="sxs-lookup"><span data-stu-id="d3261-155">hello following example uses hello same parameters and steps:</span></span>

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="d3261-156">Krok 1 — Tworzenie sieci wirtualnej hello, Brama sieci VPN i bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="d3261-156">Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a><span data-ttu-id="d3261-157">1. Deklarowanie zmiennych i połączenia tooyour subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d3261-157">1. Declare your variables & connect tooyour subscription</span></span>
<span data-ttu-id="d3261-158">W tym ćwiczeniu Rozpoczniemy przez zadeklarowanie naszych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="d3261-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="d3261-159">Należy się, że wartości hello tooreplace własnymi podczas konfigurowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="d3261-159">Be sure tooreplace hello values with your own when configuring for production.</span></span>

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
<span data-ttu-id="d3261-160">Witaj toouse poleceń cmdlet Menedżera zasobów, upewnij się, że Przełącz tryb tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3261-160">toouse hello Resource Manager cmdlets, make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="d3261-161">Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="d3261-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="d3261-162">Otwórz konsolę programu PowerShell i Połącz konto tooyour.</span><span class="sxs-lookup"><span data-stu-id="d3261-162">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="d3261-163">Użyj następujących hello przykładowe toohelp, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="d3261-163">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="d3261-164">2. Tworzenie sieci wirtualnej hello, Brama sieci VPN i bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="d3261-164">2. Create hello virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="d3261-165">Witaj poniższy przykład tworzy hello sieci wirtualnej, TestVNet1 z trzech podsieci i hello bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="d3261-165">hello following example creates hello virtual network, TestVNet1 with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="d3261-166">Zastępowanie wartości, jest ważne, aby zawsze nazwę podsieci bramy w szczególności "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="d3261-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="d3261-167">W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="d3261-167">If you name it something else, your gateway creation fails.</span></span>

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="d3261-168">Krok 2 — Tworzenie połączenia sieci VPN S2S przy użyciu zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="d3261-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="d3261-169">1. Tworzenie zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="d3261-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3261-170">Należy toocreate zasady IPsec i IKE w kolejności tooenable opcji "UsePolicyBasedTrafficSelectors" hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="d3261-170">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="d3261-171">Witaj poniższy przykład tworzy zasady IPsec i IKE z te algorytmy i parametry:</span><span class="sxs-lookup"><span data-stu-id="d3261-171">hello following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="d3261-172">IKEv2: DHGroup24 AES256, SHA384</span><span class="sxs-lookup"><span data-stu-id="d3261-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="d3261-173">Protokół IPsec: AES256, SHA256, PFS24, skojarzenia zabezpieczeń okres istnienia 3600 s & 2048KB</span><span class="sxs-lookup"><span data-stu-id="d3261-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="d3261-174">2. Utwórz połączenie sieci VPN S2S hello z selektorów ruchu na podstawie zasad i zasady IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="d3261-174">2. Create hello S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="d3261-175">Tworzenie połączenia sieci VPN S2S i stosowanie zasad IPsec i IKE hello utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="d3261-175">Create an S2S VPN connection and apply hello IPsec/IKE policy created in hello previous step.</span></span> <span data-ttu-id="d3261-176">Należy pamiętać o hello dodatkowy parametr "-UsePolicyBasedTrafficSelectors $True" co pozwala selektorów ruchu na podstawie zasad na powitania połączenia.</span><span class="sxs-lookup"><span data-stu-id="d3261-176">Be aware of hello additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on hello connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="d3261-177">Po wykonaniu czynności hello hello połączenia sieci VPN S2S będzie używać hello zdefiniowane zasady IPsec i IKE i Włącz selektorów ruchu na podstawie zasad na powitania połączenia.</span><span class="sxs-lookup"><span data-stu-id="d3261-177">After completing hello steps, hello S2S VPN connection will use hello IPsec/IKE policy defined, and enable policy-based traffic selectors on hello connection.</span></span> <span data-ttu-id="d3261-178">Możesz powtarzać hello same kroki tooadd więcej połączeń tooadditional urządzeń lokalnych, na podstawie zasad sieci VPN z hello tej samej bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d3261-178">You can repeat hello same steps tooadd more connections tooadditional on-premises policy-based VPN devices from hello same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="d3261-179">Zaktualizuj selektorów opartych na zasadach ruchu dla połączenia</span><span class="sxs-lookup"><span data-stu-id="d3261-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="d3261-180">Hello ostatniej sekcji pokazano, jak opcja tooupdate hello ruchu na podstawie zasad selektory dla istniejącego połączenia sieci VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="d3261-180">hello last section shows you how tooupdate hello policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-hello-connection"></a><span data-ttu-id="d3261-181">1. Pobierz dane o połączeniu hello</span><span class="sxs-lookup"><span data-stu-id="d3261-181">1. Get hello connection</span></span>
<span data-ttu-id="d3261-182">Pobierz zasób połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="d3261-182">Get hello connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a><span data-ttu-id="d3261-183">2. Zaznacz opcję selektorów, hello ruchu na podstawie zasad</span><span class="sxs-lookup"><span data-stu-id="d3261-183">2. Check hello policy-based traffic selectors option</span></span>
<span data-ttu-id="d3261-184">Witaj następujący wiersz zawiera czy selektorów ruchu na podstawie zasad hello są używane do połączenia hello:</span><span class="sxs-lookup"><span data-stu-id="d3261-184">hello following line shows whether hello policy-based traffic selectors are used for hello connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="d3261-185">Jeśli wiersz hello zwraca "**True**", następnie selektorów ruchu na podstawie zasad są skonfigurowane na powitania połączenia; w przeciwnym razie zwraca wartość "**False**."</span><span class="sxs-lookup"><span data-stu-id="d3261-185">If hello line returns "**True**", then policy-based traffic selectors are configured on hello connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="d3261-186">3. Zaktualizuj selektorów ruchu na podstawie zasad hello połączenia</span><span class="sxs-lookup"><span data-stu-id="d3261-186">3. Update hello policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="d3261-187">Po uzyskaniu hello zasobu połączenia, można włączyć lub wyłączyć opcję hello.</span><span class="sxs-lookup"><span data-stu-id="d3261-187">Once you obtain hello connection resource, you can enable or disable hello option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="d3261-188">Wyłącz UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="d3261-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="d3261-189">Witaj poniższy przykład wyłącza hello ruchu na podstawie zasad selektorów opcję, ale pozostawia hello zasad IPsec i IKE bez zmian:</span><span class="sxs-lookup"><span data-stu-id="d3261-189">hello following example disables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="d3261-190">Włącz UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="d3261-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="d3261-191">Witaj poniższy przykład umożliwia włączenie opcji selektorów ruchu na podstawie zasad hello, ale pozostawia hello zasad IPsec i IKE bez zmian:</span><span class="sxs-lookup"><span data-stu-id="d3261-191">hello following example enables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="d3261-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d3261-192">Next steps</span></span>
<span data-ttu-id="d3261-193">Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d3261-193">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="d3261-194">Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3261-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="d3261-195">Sprawdź również [zasady IPsec/IKE skonfigurować dla połączeń sieci VPN S2S lub wirtualnymi do](vpn-gateway-ipsecikepolicy-rm-powershell.md) uzyskać więcej informacji dotyczących zasad protokołu IPsec/IKE niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="d3261-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
