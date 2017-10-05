---
title: "Połączenie bramy sieci VPN platformy Azure do wielu urządzeń lokalnych, na podstawie zasad sieci VPN: usługi Azure Resource Manager: programu PowerShell | Dokumentacja firmy Microsoft"
description: "Ten artykuł przeprowadzi Cię przez skonfigurowanie Azure bramy sieci VPN opartej na trasach do wielu opartych na zasadach urządzenia sieci VPN za pomocą usługi Azure Resource Manager i programu PowerShell."
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
ms.openlocfilehash: 17211379ec61891982a02efca6730ca0da87c1ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-azure-vpn-gateways-to-multiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="d85c1-103">Połączenie bramy sieci VPN platformy Azure do wielu urządzeń lokalnych, na podstawie zasad sieci VPN przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="d85c1-103">Connect Azure VPN gateways to multiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="d85c1-104">W tym artykule opisano, jak skonfigurować opartej na trasach Brama sieci VPN do nawiązania połączenia wielu urządzeń lokalnych, na podstawie zasad sieci VPN korzystania z niestandardowych zasad IPsec i IKE połączeń sieci VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="d85c1-104">This article helps you configure an Azure route-based VPN gateway to connect to multiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="d85c1-105">Temat bram sieci VPN opartych na zasadach i opartej na trasach</span><span class="sxs-lookup"><span data-stu-id="d85c1-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="d85c1-106">Zasady - *a* opartej na trasach urządzenia sieci VPN różnią się w konfiguracji selektorów ruchu protokołu IPsec dla połączenia:</span><span class="sxs-lookup"><span data-stu-id="d85c1-106">Policy- *vs.* route-based VPN devices differ in how the IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="d85c1-107">**Oparte na zasadach** urządzenia sieci VPN przy użyciu kombinacji prefiksów z obu sieci, aby zdefiniować sposób ruch jest szyfrowany/odszyfrowywany przez tunel protokołu IPsec.</span><span class="sxs-lookup"><span data-stu-id="d85c1-107">**Policy-based** VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="d85c1-108">Zazwyczaj jest tworzony na urządzeniach zapory, które wykonują filtrowanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="d85c1-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="d85c1-109">IPsec tunelu szyfrowania i odszyfrowywania są dodawane do filtrowania i aparat przetwarzania pakietu.</span><span class="sxs-lookup"><span data-stu-id="d85c1-109">IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.</span></span>
* <span data-ttu-id="d85c1-110">**Oparte na trasach** urządzenia sieci VPN przy użyciu dowolnego z każdym (symbol wieloznaczny) ruchu selektorów, a let routingu/przekazywania ruchu bezpośredniego tabel do różnych tuneli protokołu IPsec.</span><span class="sxs-lookup"><span data-stu-id="d85c1-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels.</span></span> <span data-ttu-id="d85c1-111">Zazwyczaj jest tworzony na platformach routera, gdzie każdy tunelu IPsec ma formę interfejsu sieciowego lub VTI (interfejsu tunelu wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="d85c1-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="d85c1-112">Poniższych diagramach wyróżnić dwa modele:</span><span class="sxs-lookup"><span data-stu-id="d85c1-112">The following diagrams highlight the two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="d85c1-113">Przykład sieci VPN opartych na zasadach</span><span class="sxs-lookup"><span data-stu-id="d85c1-113">Policy-based VPN example</span></span>
![oparte na zasadach](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="d85c1-115">Przykład sieci VPN opartej na trasach</span><span class="sxs-lookup"><span data-stu-id="d85c1-115">Route-based VPN example</span></span>
![oparte na trasach](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="d85c1-117">Pomocy technicznej platformy Azure dla sieci VPN opartych na zasadach</span><span class="sxs-lookup"><span data-stu-id="d85c1-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="d85c1-118">Obecnie usługa Azure obsługuje oba tryby bramy sieci VPN: opartej na trasach bramy sieci VPN i bramy sieci VPN opartych na zasadach.</span><span class="sxs-lookup"><span data-stu-id="d85c1-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="d85c1-119">Zostały one utworzone na różnych platformach wewnętrznego, które powodują różne specyfikacje:</span><span class="sxs-lookup"><span data-stu-id="d85c1-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="d85c1-120">**Brama sieci VPN PolicyBased**</span><span class="sxs-lookup"><span data-stu-id="d85c1-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="d85c1-121">**Brama sieci VPN z siecią typu RouteBased**</span><span class="sxs-lookup"><span data-stu-id="d85c1-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="d85c1-122">**Jednostka SKU bramy Azure**</span><span class="sxs-lookup"><span data-stu-id="d85c1-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="d85c1-123">Podstawowa</span><span class="sxs-lookup"><span data-stu-id="d85c1-123">Basic</span></span>                       | <span data-ttu-id="d85c1-124">Basic, Standard, wysokowydajnej</span><span class="sxs-lookup"><span data-stu-id="d85c1-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="d85c1-125">**Wersja IKE**</span><span class="sxs-lookup"><span data-stu-id="d85c1-125">**IKE version**</span></span>          | <span data-ttu-id="d85c1-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="d85c1-126">IKEv1</span></span>                       | <span data-ttu-id="d85c1-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="d85c1-127">IKEv2</span></span>                                    |
| <span data-ttu-id="d85c1-128">**Maks. Połączeń S2S**</span><span class="sxs-lookup"><span data-stu-id="d85c1-128">**Max. S2S connections**</span></span> | <span data-ttu-id="d85c1-129">**1**</span><span class="sxs-lookup"><span data-stu-id="d85c1-129">**1**</span></span>                       | <span data-ttu-id="d85c1-130">Basic/Standard: 10</span><span class="sxs-lookup"><span data-stu-id="d85c1-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="d85c1-131">Wysokowydajnej: 30</span><span class="sxs-lookup"><span data-stu-id="d85c1-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="d85c1-132">Niestandardowe zasady IPsec i IKE, można teraz skonfigurować Azure bramy sieci VPN opartej na trasach do ruchu na podstawie prefiksu selektorów za pomocą opcji "**PolicyBasedTrafficSelectors**", aby nawiązać połączenie urządzenia sieci VPN na podstawie zasad lokalnych.</span><span class="sxs-lookup"><span data-stu-id="d85c1-132">With the custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways to use prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", to connect to on-premises policy-based VPN devices.</span></span> <span data-ttu-id="d85c1-133">Ta funkcja umożliwia nawiązanie połączenia z sieci wirtualnej platformy Azure i Brama sieci VPN z wieloma lokalnie na podstawie zasad urządzenia sieci VPN/zapory usuwanie limit pojedynczego połączenia z bieżącej platformy Azure na podstawie zasad bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="d85c1-133">This capability allows you to connect from an Azure virtual network and VPN gateway to multiple on-premises policy-based VPN/firewall devices, removing the single connection limit from the current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="d85c1-134">Aby włączyć to połączenie, musi obsługiwać lokalnego urządzenia sieci VPN opartych na zasadach **IKEv2** do nawiązania połączenia platformy Azure bramy sieci VPN opartej na trasach.</span><span class="sxs-lookup"><span data-stu-id="d85c1-134">To enable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** to connect to the Azure route-based VPN gateways.</span></span> <span data-ttu-id="d85c1-135">Sprawdź specyfikację urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="d85c1-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="d85c1-136">Sieciach lokalnych, łączących się za pośrednictwem urządzenia sieci VPN opartych na zasadach z tym mechanizm mogą łączyć się tylko z sieci wirtualnej platformy Azure; **nie można ich przesyłania do innych sieci lokalnej lub sieci wirtualnych za pomocą tej samej bramy sieci VPN platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="d85c1-136">The on-premises networks connecting through policy-based VPN devices with this mechanism can only connect to the Azure virtual network; **they cannot transit to other on-premises networks or virtual networks via the same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="d85c1-137">Opcja konfiguracji jest częścią niestandardowe zasady IPsec i IKE połączenia.</span><span class="sxs-lookup"><span data-stu-id="d85c1-137">The configuration option is part of the custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="d85c1-138">Po włączeniu opcji selektor ruchu na podstawie zasad, należy określić pełną zasad (algorytmów szyfrowania i integralności IPsec i IKE, silnych kluczy i okresy istnienia SA).</span><span class="sxs-lookup"><span data-stu-id="d85c1-138">If you enable the policy-based traffic selector option, you must specify the complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="d85c1-139">Na poniższym diagramie przedstawiono Dlaczego routing tranzytowy za pośrednictwem bramy sieci VPN platformy Azure nie działa z opcją opartych na zasadach:</span><span class="sxs-lookup"><span data-stu-id="d85c1-139">The following diagram shows why transit routing via Azure VPN gateway doesn't work with the policy-based option:</span></span>

![przesyłania opartych na zasadach](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="d85c1-141">Jak pokazano na rysunku, Brama sieci VPN platformy Azure ma selektorów ruch z sieci wirtualnej wszystkie prefiksy sieci lokalnej, ale nie prefiksy połączenia między.</span><span class="sxs-lookup"><span data-stu-id="d85c1-141">As shown in the diagram, the Azure VPN gateway has traffic selectors from the virtual network to each of the on-premises network prefixes, but not the cross-connection prefixes.</span></span> <span data-ttu-id="d85c1-142">Na przykład lokalnej lokacji 2, lokacja 3 i 4 lokacji można każdego komunikują się VNet1 odpowiednio, ale nie można połączyć za pośrednictwem bramy sieci VPN platformy Azure do siebie.</span><span class="sxs-lookup"><span data-stu-id="d85c1-142">For example, on-premises site 2, site 3, and site 4 can each communicate to VNet1 respectively, but cannot connect via the Azure VPN gateway to each other.</span></span> <span data-ttu-id="d85c1-143">Na diagramie przedstawiono selektorów ruchu cross-connect, które nie są dostępne w bramie sieci VPN platformy Azure zgodnie z tą konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="d85c1-143">The diagram shows the cross-connect traffic selectors that are not available in the Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="d85c1-144">Konfigurowanie połączenia selektorów ruchu na podstawie zasad</span><span class="sxs-lookup"><span data-stu-id="d85c1-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="d85c1-145">Instrukcje w tym artykule wykonaj tym samym przykładzie, zgodnie z opisem w [zasady IPsec/IKE skonfigurować dla połączeń S2S lub do wirtualnymi](vpn-gateway-ipsecikepolicy-rm-powershell.md) do nawiązywania połączenia S2S VPN.</span><span class="sxs-lookup"><span data-stu-id="d85c1-145">The instructions in this article follow the same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) to establish a S2S VPN connection.</span></span> <span data-ttu-id="d85c1-146">Jest to przedstawione na poniższym diagramie:</span><span class="sxs-lookup"><span data-stu-id="d85c1-146">This is shown in the following diagram:</span></span>

![zasady s2s](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="d85c1-148">Przepływ pracy łączność ta:</span><span class="sxs-lookup"><span data-stu-id="d85c1-148">The workflow to enable this connectivity:</span></span>
1. <span data-ttu-id="d85c1-149">Tworzenie sieci wirtualnej, Brama sieci VPN i bramy sieci lokalnej dla połączenia między lokalizacjami</span><span class="sxs-lookup"><span data-stu-id="d85c1-149">Create the virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="d85c1-150">Tworzenie zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="d85c1-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="d85c1-151">Stosowanie zasad podczas tworzenia połączenia S2S lub do wirtualnymi i **włączyć selektorów ruchu na podstawie zasad** połączenia</span><span class="sxs-lookup"><span data-stu-id="d85c1-151">Apply the policy when you create a S2S or VNet-to-VNet connection, and **enable the policy-based traffic selectors** on the connection</span></span>
4. <span data-ttu-id="d85c1-152">Jeśli połączenie jest już utworzony, można zastosować lub zaktualizuj zasady do istniejącego połączenia</span><span class="sxs-lookup"><span data-stu-id="d85c1-152">If the connection is already created, you can apply or update the policy to an existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="d85c1-153">Włącz selektorów opartych na zasadach ruchu dla połączenia</span><span class="sxs-lookup"><span data-stu-id="d85c1-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="d85c1-154">Upewnij się, że zostały wykonane [część 3 artykułu zasad IPsec/IKE skonfigurować](vpn-gateway-ipsecikepolicy-rm-powershell.md) dla tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d85c1-154">Make sure you have completed [Part 3 of the Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="d85c1-155">W poniższym przykładzie użyto te same parametry i kroki:</span><span class="sxs-lookup"><span data-stu-id="d85c1-155">The following example uses the same parameters and steps:</span></span>

### <a name="step-1---create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="d85c1-156">Krok 1 — Tworzenie sieci wirtualnej, Brama sieci VPN i bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="d85c1-156">Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-to-your-subscription"></a><span data-ttu-id="d85c1-157">1. Deklarowanie zmiennych & nawiązać połączenia z subskrypcją</span><span class="sxs-lookup"><span data-stu-id="d85c1-157">1. Declare your variables & connect to your subscription</span></span>
<span data-ttu-id="d85c1-158">W tym ćwiczeniu Rozpoczniemy przez zadeklarowanie naszych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="d85c1-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="d85c1-159">Podczas konfigurowania produktu należy pamiętać o zastąpieniu ich odpowiednimi wartościami.</span><span class="sxs-lookup"><span data-stu-id="d85c1-159">Be sure to replace the values with your own when configuring for production.</span></span>

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
<span data-ttu-id="d85c1-160">Aby używać poleceń cmdlet Menedżera zasobów, upewnij się, że można przełączyć do trybu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d85c1-160">To use the Resource Manager cmdlets, make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="d85c1-161">Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="d85c1-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="d85c1-162">Otwórz konsolę programu PowerShell i połącz się ze swoim kontem.</span><span class="sxs-lookup"><span data-stu-id="d85c1-162">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="d85c1-163">Użyj poniższego przykładu w celu łatwiejszego nawiązania połączenia:</span><span class="sxs-lookup"><span data-stu-id="d85c1-163">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="d85c1-164">2. Tworzenie sieci wirtualnej, Brama sieci VPN i bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="d85c1-164">2. Create the virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="d85c1-165">Poniższy przykład tworzy sieć wirtualną, TestVNet1 z trzech podsieci oraz bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="d85c1-165">The following example creates the virtual network, TestVNet1 with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="d85c1-166">Zastępowanie wartości, jest ważne, aby zawsze nazwę podsieci bramy w szczególności "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="d85c1-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="d85c1-167">W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="d85c1-167">If you name it something else, your gateway creation fails.</span></span>

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="d85c1-168">Krok 2 — Tworzenie połączenia sieci VPN S2S przy użyciu zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="d85c1-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="d85c1-169">1. Tworzenie zasad IPsec i IKE</span><span class="sxs-lookup"><span data-stu-id="d85c1-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d85c1-170">Należy utworzyć zasady IPsec i IKE, aby włączyć opcję "UsePolicyBasedTrafficSelectors" w połączeniu.</span><span class="sxs-lookup"><span data-stu-id="d85c1-170">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="d85c1-171">Poniższy przykład tworzy zasady IPsec i IKE z te algorytmy i parametry:</span><span class="sxs-lookup"><span data-stu-id="d85c1-171">The following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="d85c1-172">IKEv2: DHGroup24 AES256, SHA384</span><span class="sxs-lookup"><span data-stu-id="d85c1-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="d85c1-173">Protokół IPsec: AES256, SHA256, PFS24, skojarzenia zabezpieczeń okres istnienia 3600 s & 2048KB</span><span class="sxs-lookup"><span data-stu-id="d85c1-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="d85c1-174">2. Utworzyć połączenie sieci VPN S2S za pomocą zasad IPsec i IKE i selektorów ruchu na podstawie zasad</span><span class="sxs-lookup"><span data-stu-id="d85c1-174">2. Create the S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="d85c1-175">Tworzenie połączenia sieci VPN S2S i stosowanie zasad IPsec i IKE utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="d85c1-175">Create an S2S VPN connection and apply the IPsec/IKE policy created in the previous step.</span></span> <span data-ttu-id="d85c1-176">Należy pamiętać o dodatkowy parametr "-UsePolicyBasedTrafficSelectors $True" co pozwala selektorów ruchu na podstawie zasad połączenia.</span><span class="sxs-lookup"><span data-stu-id="d85c1-176">Be aware of the additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on the connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="d85c1-177">Po wykonaniu tych kroków, połączenia sieci VPN S2S spowoduje za pomocą zasad IPsec i IKE zdefiniowany i włączenie selektorów ruchu na podstawie zasad połączenia.</span><span class="sxs-lookup"><span data-stu-id="d85c1-177">After completing the steps, the S2S VPN connection will use the IPsec/IKE policy defined, and enable policy-based traffic selectors on the connection.</span></span> <span data-ttu-id="d85c1-178">Można powtórzyć te same kroki, aby dodać więcej połączeń do urządzenia sieci VPN opartych na zasadach dodatkowych lokalnych z tej samej bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d85c1-178">You can repeat the same steps to add more connections to additional on-premises policy-based VPN devices from the same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="d85c1-179">Zaktualizuj selektorów opartych na zasadach ruchu dla połączenia</span><span class="sxs-lookup"><span data-stu-id="d85c1-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="d85c1-180">W ostatniej sekcji widoczne, jak zaktualizować opcję selektorów ruchu na podstawie zasad dla istniejącego połączenia sieci VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="d85c1-180">The last section shows you how to update the policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-the-connection"></a><span data-ttu-id="d85c1-181">1. Pobierz dane o połączeniu</span><span class="sxs-lookup"><span data-stu-id="d85c1-181">1. Get the connection</span></span>
<span data-ttu-id="d85c1-182">Pobierz zasób połączenia.</span><span class="sxs-lookup"><span data-stu-id="d85c1-182">Get the connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-the-policy-based-traffic-selectors-option"></a><span data-ttu-id="d85c1-183">2. Zaznacz opcję selektorów ruchu na podstawie zasad</span><span class="sxs-lookup"><span data-stu-id="d85c1-183">2. Check the policy-based traffic selectors option</span></span>
<span data-ttu-id="d85c1-184">Następujący wiersz pokazuje, czy selektorów opartych na zasadach ruchu są używane do połączenia:</span><span class="sxs-lookup"><span data-stu-id="d85c1-184">The following line shows whether the policy-based traffic selectors are used for the connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="d85c1-185">Jeśli wiersz zwraca "**True**", następnie selektorów ruchu na podstawie zasad są skonfigurowane w ramach połączenia; w przeciwnym razie zwraca wartość "**False**."</span><span class="sxs-lookup"><span data-stu-id="d85c1-185">If the line returns "**True**", then policy-based traffic selectors are configured on the connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-the-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="d85c1-186">3. Zaktualizuj selektorów opartych na zasadach ruchu dla połączenia</span><span class="sxs-lookup"><span data-stu-id="d85c1-186">3. Update the policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="d85c1-187">Po uzyskaniu zasobu połączenia, można włączyć lub wyłączyć opcję.</span><span class="sxs-lookup"><span data-stu-id="d85c1-187">Once you obtain the connection resource, you can enable or disable the option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="d85c1-188">Wyłącz UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="d85c1-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="d85c1-189">Poniższy przykład wyłącza opcję selektorów ruchu na podstawie zasad, ale pozostawia zasad IPsec i IKE bez zmian:</span><span class="sxs-lookup"><span data-stu-id="d85c1-189">The following example disables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="d85c1-190">Włącz UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="d85c1-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="d85c1-191">Poniższy przykład włącza opcję selektorów ruchu na podstawie zasad, ale pozostawia zasad IPsec i IKE bez zmian:</span><span class="sxs-lookup"><span data-stu-id="d85c1-191">The following example enables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="d85c1-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d85c1-192">Next steps</span></span>
<span data-ttu-id="d85c1-193">Po zakończeniu procesu nawiązywania połączenia można dodać do sieci wirtualnych maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="d85c1-193">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="d85c1-194">Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d85c1-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="d85c1-195">Sprawdź również [zasady IPsec/IKE skonfigurować dla połączeń sieci VPN S2S lub wirtualnymi do](vpn-gateway-ipsecikepolicy-rm-powershell.md) uzyskać więcej informacji dotyczących zasad protokołu IPsec/IKE niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="d85c1-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
