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
ms.openlocfilehash: a9f71b566ffdb163f95634835f64589a700d712f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="2d060-103">Skonfigurować połączenia sieci VPN S2S aktywny aktywny z bramy sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2d060-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="2d060-104">W tym artykule przedstawiono kroki, aby utworzyć między lokalizacjami aktywny aktywny i wirtualnymi do połączeń przy użyciu modelu wdrażania usługi Resource Manager i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d060-104">This article walks you through the steps to create active-active cross-premises and VNet-to-VNet connections using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="2d060-105">O wysokiej dostępności między lokalizacjami połączeń</span><span class="sxs-lookup"><span data-stu-id="2d060-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="2d060-106">Do uzyskania wysokiej dostępności między lokalizacjami i łączności do wirtualnymi, należy wdrożyć wiele bram sieci VPN i ustanowienia wielu równoległych połączeń między sieciami i Azure.</span><span class="sxs-lookup"><span data-stu-id="2d060-106">To achieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="2d060-107">Zobacz [wysokiej dostępności między lokalizacjami i łączności do wirtualnymi](vpn-gateway-highlyavailable.md) Omówienie opcji łączności i topologii.</span><span class="sxs-lookup"><span data-stu-id="2d060-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="2d060-108">Ten artykuł zawiera instrukcje dotyczące konfigurowania połączenia sieci VPN między lokalizacjami aktywny aktywny i aktywny aktywny połączenie między dwiema sieciami wirtualnymi:</span><span class="sxs-lookup"><span data-stu-id="2d060-108">This article provides the instructions to set up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="2d060-109">Część 1 — Tworzenie i konfigurowanie bramy sieci VPN platformy Azure w trybie aktywny / aktywny</span><span class="sxs-lookup"><span data-stu-id="2d060-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="2d060-110">Część 2 - zestawiania połączeń między różnymi lokalizacjami aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="2d060-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="2d060-111">Część 3 — ustanowienie połączenia do wirtualnymi aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="2d060-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="2d060-112">Część 4 — aktualizacja istniejącej bramy między aktywny aktywny i aktywnego gotowości</span><span class="sxs-lookup"><span data-stu-id="2d060-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="2d060-113">Można łączyć ze sobą do tworzenia topologii sieci bardziej złożonych, wysokiej dostępności, która odpowiada Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="2d060-113">You can combine these together to build a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d060-114">Należy pamiętać, że tryb aktywny aktywny używa tylko następujące wersje produktu:</span><span class="sxs-lookup"><span data-stu-id="2d060-114">Please note that the active-active mode uses only the following SKUs:</span></span> 
  * <span data-ttu-id="2d060-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="2d060-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="2d060-116">Wysokowydajnej (dla starego starszej wersji jednostki SKU)</span><span class="sxs-lookup"><span data-stu-id="2d060-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="2d060-117"><a name ="aagateway"></a>Część 1 — Tworzenie i konfigurowanie aktywny aktywny bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="2d060-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="2d060-118">Poniższe kroki skonfiguruje bramy sieci VPN platformy Azure w trybach aktywny aktywny.</span><span class="sxs-lookup"><span data-stu-id="2d060-118">The following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="2d060-119">Podstawowe różnice między bramami aktywny aktywny i aktywnego gotowości:</span><span class="sxs-lookup"><span data-stu-id="2d060-119">The key differences between the active-active and active-standby gateways:</span></span>

* <span data-ttu-id="2d060-120">Należy utworzyć dwie konfiguracje IP bramy z dwóch publicznych adresów IP</span><span class="sxs-lookup"><span data-stu-id="2d060-120">You need to create two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="2d060-121">Należy ustawić flagę EnableActiveActiveFeature</span><span class="sxs-lookup"><span data-stu-id="2d060-121">You need set the EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="2d060-122">Jednostka SKU bramy musi być VpnGw1, VpnGw2, VpnGw3 lub wysokowydajnej (starszej wersji jednostki SKU).</span><span class="sxs-lookup"><span data-stu-id="2d060-122">The gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="2d060-123">Inne właściwości są takie same jak bramy z systemem innym niż — aktywny aktywny.</span><span class="sxs-lookup"><span data-stu-id="2d060-123">The other properties are the same as the non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="2d060-124">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="2d060-124">Before you begin</span></span>
* <span data-ttu-id="2d060-125">Sprawdź, czy masz subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d060-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="2d060-126">Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d060-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2d060-127">Niezbędne jest zainstalowanie poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2d060-127">You'll need to install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="2d060-128">Zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji na temat instalacji poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d060-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="2d060-129">Krok 1 — Tworzenie i konfigurowanie VNet1</span><span class="sxs-lookup"><span data-stu-id="2d060-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="2d060-130">1. Zadeklarowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="2d060-130">1. Declare your variables</span></span>
<span data-ttu-id="2d060-131">To ćwiczenie rozpoczniemy od zadeklarowania zmiennych.</span><span class="sxs-lookup"><span data-stu-id="2d060-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="2d060-132">W poniższym przykładzie deklarujemy zmienne przy użyciu wartości podanych dla tego ćwiczenia.</span><span class="sxs-lookup"><span data-stu-id="2d060-132">The example below declares the variables using the values for this exercise.</span></span> <span data-ttu-id="2d060-133">Podczas konfigurowania produktu należy pamiętać o zastąpieniu ich odpowiednimi wartościami.</span><span class="sxs-lookup"><span data-stu-id="2d060-133">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="2d060-134">Tych zmiennych można użyć, aby wykonać opisane kroki w celu zapoznania się z tego typu konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="2d060-134">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="2d060-135">Zmodyfikuj zmienne, a następnie skopiuj je i wklej do konsoli programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d060-135">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="2d060-136">2. Połączyć subskrypcję i Utwórz nową grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="2d060-136">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="2d060-137">Upewnij się, że program PowerShell został przełączony do trybu umożliwiającego korzystanie z poleceń cmdlet usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2d060-137">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="2d060-138">Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="2d060-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="2d060-139">Otwórz konsolę programu PowerShell i połącz się ze swoim kontem.</span><span class="sxs-lookup"><span data-stu-id="2d060-139">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="2d060-140">Użyj poniższego przykładu w celu łatwiejszego nawiązania połączenia:</span><span class="sxs-lookup"><span data-stu-id="2d060-140">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="2d060-141">3. Utworzenie sieci TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2d060-141">3. Create TestVNet1</span></span>
<span data-ttu-id="2d060-142">Poniższy przykład pozwala utworzyć sieć wirtualną o nazwie TestVNet1 oraz trzy podsieci noszące kolejno nazwy GatewaySubnet, FrontEnd i BackEnd.</span><span class="sxs-lookup"><span data-stu-id="2d060-142">The sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="2d060-143">Podczas zastępowania wartości ważne jest, aby podsieć bramy zawsze nosiła nazwę GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="2d060-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="2d060-144">W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="2d060-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="2d060-145">Krok 2 — Tworzenie bramy sieci VPN dla TestVNet1 w trybie aktywny / aktywny</span><span class="sxs-lookup"><span data-stu-id="2d060-145">Step 2 - Create the VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-the-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="2d060-146">1. Tworzenie publicznych adresów IP i bramy konfiguracje adresów IP</span><span class="sxs-lookup"><span data-stu-id="2d060-146">1. Create the public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="2d060-147">Żądanie dwie publiczne adresy IP do przydzielenia do bramy, który spowoduje utworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2d060-147">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="2d060-148">Zostanie również definiować podsieci i wymagane konfiguracje adresów IP.</span><span class="sxs-lookup"><span data-stu-id="2d060-148">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-the-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="2d060-149">2. Tworzenie bramy sieci VPN z konfiguracją aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="2d060-149">2. Create the VPN gateway with active-active configuration</span></span>
<span data-ttu-id="2d060-150">Utwórz bramę sieci wirtualnej dla sieci TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2d060-150">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="2d060-151">Zauważ, że istnieją dwa wpisy GatewayIpConfig, i Flaga EnableActiveActiveFeature jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="2d060-151">Note that there are two GatewayIpConfig entries, and the EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="2d060-152">Tworzenie bramy może potrwać co najmniej 45 minut.</span><span class="sxs-lookup"><span data-stu-id="2d060-152">Creating a gateway can take a while (45 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-the-gateway-public-ip-addresses-and-the-bgp-peer-ip-address"></a><span data-ttu-id="2d060-153">3. Uzyskaj bramy publicznych adresów IP i adres IP elementu równorzędnego protokołu BGP</span><span class="sxs-lookup"><span data-stu-id="2d060-153">3. Obtain the gateway public IP addresses and the BGP Peer IP address</span></span>
<span data-ttu-id="2d060-154">Po utworzeniu bramy, należy uzyskać adres IP elementu równorzędnego protokołu BGP dla bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d060-154">Once the gateway is created, you will need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="2d060-155">Ten adres jest potrzebne do skonfigurowania bramy sieci VPN platformy Azure jako element równorzędny BGP dla lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="2d060-155">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="2d060-156">Pokaż dwie publiczne adresy IP przydzielone dla bramy sieci VPN, a ich odpowiednie adresy IP elementu równorzędnego protokołu BGP dla każdego wystąpienia bramy przy użyciu następujących poleceń cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2d060-156">Use the following cmdlets to show the two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

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

<span data-ttu-id="2d060-157">Kolejność publicznego adresu IP adresów dla wystąpień bramy i odpowiednie adresy komunikacji równorzędnej BGP są takie same.</span><span class="sxs-lookup"><span data-stu-id="2d060-157">The order of the public IP addresses for the gateway instances and the corresponding BGP Peering Addresses are the same.</span></span> <span data-ttu-id="2d060-158">W tym przykładzie bramy maszyny Wirtualnej z publicznego adresu IP z 40.112.190.5 użyje 10.12.255.4 jako adres komunikacji równorzędnej BGP i bramy z 138.91.156.129 użyje 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="2d060-158">In this example, the gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and the gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="2d060-159">Te informacje są potrzebne podczas konfigurowania na urządzeniach w sieci VPN lokalne nawiązywania połączenia z bramą aktywny aktywny.</span><span class="sxs-lookup"><span data-stu-id="2d060-159">This information is needed when you set up your on premises VPN devices connecting to the active-active gateway.</span></span> <span data-ttu-id="2d060-160">Brama jest wyświetlane na diagramie poniżej przy użyciu wszystkich adresów:</span><span class="sxs-lookup"><span data-stu-id="2d060-160">The gateway is shown in the diagram below with all addresses:</span></span>

![aktywny aktywny bramy](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="2d060-162">Po utworzeniu bramy można użyć ta brama między lokalizacjami aktywny aktywny lub wirtualnymi do połączenia.</span><span class="sxs-lookup"><span data-stu-id="2d060-162">Once the gateway is created, you can use this gateway to establish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="2d060-163">Poniższe sekcje przeprowadzi kroki, aby ukończyć wykonywania.</span><span class="sxs-lookup"><span data-stu-id="2d060-163">The following sections will walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="2d060-164"><a name ="aacrossprem"></a>Część 2 - nawiązywania połączenia między lokalizacjami aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="2d060-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="2d060-165">Nawiązanie połączenia między różnymi lokalizacjami, musisz utworzyć bramy sieci lokalnej do reprezentowania lokalnego urządzenia sieci VPN i połączenia bramy sieci VPN platformy Azure z bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="2d060-165">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the Azure VPN gateway with the local network gateway.</span></span> <span data-ttu-id="2d060-166">W tym przykładzie Brama sieci VPN platformy Azure jest w trybie aktywny / aktywny.</span><span class="sxs-lookup"><span data-stu-id="2d060-166">In this example, the Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="2d060-167">W związku z tym nawet, jeśli istnieje tylko jeden lokalnego urządzenia sieci VPN (bramy sieci lokalnej) i jednego połączenia zasobów, zarówno wystąpień bramy sieci VPN platformy Azure zostanie ustanowiona tunel S2S VPN z lokalnego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2d060-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with the on-premises device.</span></span>

<span data-ttu-id="2d060-168">Przed kontynuowaniem upewnij się, zostały ukończone [część 1](#aagateway) tego ćwiczenia.</span><span class="sxs-lookup"><span data-stu-id="2d060-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="2d060-169">Krok 1 — Tworzenie i konfigurowanie bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="2d060-169">Step 1 - Create and configure the local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="2d060-170">1. Zadeklarowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="2d060-170">1. Declare your variables</span></span>
<span data-ttu-id="2d060-171">Tego ćwiczenia jest kontynuowana konfiguracji przedstawione na diagramie.</span><span class="sxs-lookup"><span data-stu-id="2d060-171">This exercise will continue to build the configuration shown in the diagram.</span></span> <span data-ttu-id="2d060-172">Należy pamiętać o zastąpieniu przykładowych wartości tymi, które mają zostać użyte w danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2d060-172">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="2d060-173">Kilka rzeczy do uwzględnienia dotyczącymi parametrów bramy sieci lokalnej:</span><span class="sxs-lookup"><span data-stu-id="2d060-173">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="2d060-174">Brama sieci lokalnej może być w tej samej lub innej lokalizacji i grupy zasobów jako brama sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="2d060-174">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="2d060-175">Ten przykład przedstawia je w różnych grupach zasobów, ale w tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d060-175">This example shows them in different resource groups but in the same Azure location.</span></span>
* <span data-ttu-id="2d060-176">Jeśli istnieje tylko jeden lokalnego urządzenia sieci VPN zgodnie z powyższym, połączenia aktywny aktywny pracować z lub bez protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="2d060-176">If there is only one on-premises VPN device as shown above, the active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="2d060-177">W tym przykładzie użyto protokołu BGP dla połączenia między lokalizacjami.</span><span class="sxs-lookup"><span data-stu-id="2d060-177">This example uses BGP for the cross-premises connection.</span></span>
* <span data-ttu-id="2d060-178">Jeśli protokół BGP jest włączony, prefiksu, musisz zadeklarować dla bramy sieci lokalnej jest adres hosta, adresu IP elementu równorzędnego protokołu BGP na urządzeniu sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="2d060-178">If BGP is enabled, the prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="2d060-179">W takim przypadku jest /32 prefiksu "10.52.255.253/32".</span><span class="sxs-lookup"><span data-stu-id="2d060-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="2d060-180">Przypomnienia należy użyć innego protokołu BGP numerów ASN między lokalnymi sieciami i sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2d060-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="2d060-181">Jeśli są one takie same, musisz zmienić numer ASN Twojej sieci wirtualnej, jeśli lokalnego urządzenia sieci VPN używa już właściwość ASN do elementu równorzędnego z innych sąsiadów BGP.</span><span class="sxs-lookup"><span data-stu-id="2d060-181">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="2d060-182">2. Tworzenie bramy sieci lokalnej dla Site5</span><span class="sxs-lookup"><span data-stu-id="2d060-182">2. Create the local network gateway for Site5</span></span>
<span data-ttu-id="2d060-183">Przed kontynuowaniem upewnij się, że nadal masz połączenie z subskrypcją 1.</span><span class="sxs-lookup"><span data-stu-id="2d060-183">Before you continue, please make sure you are still connected to Subscription 1.</span></span> <span data-ttu-id="2d060-184">Utwórz grupę zasobów, jeśli nie został jeszcze utworzony.</span><span class="sxs-lookup"><span data-stu-id="2d060-184">Create the resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="2d060-185">Krok 2 — połączenie bramy sieci wirtualnej i Brama sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="2d060-185">Step 2 - Connect the VNet gateway and local network gateway</span></span>
#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="2d060-186">1. Pobierz dwóch bram</span><span class="sxs-lookup"><span data-stu-id="2d060-186">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="2d060-187">2. Utwórz TestVNet1 Site5 połączenia</span><span class="sxs-lookup"><span data-stu-id="2d060-187">2. Create the TestVNet1 to Site5 connection</span></span>
<span data-ttu-id="2d060-188">W tym kroku utworzysz połączenie z TestVNet1 do Site5_1 z "Wartość", wartość $True.</span><span class="sxs-lookup"><span data-stu-id="2d060-188">In this step, you will create the connection from TestVNet1 to Site5_1 with "EnableBGP" set to $True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="2d060-189">3. Parametry sieci VPN i protokołu BGP dla lokalnego urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="2d060-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="2d060-190">W poniższym przykładzie przedstawiono parametry, które wejdzie w sekcji konfiguracji protokołu BGP na urządzeniu lokalnym sieci VPN w tym ćwiczeniu:</span><span class="sxs-lookup"><span data-stu-id="2d060-190">The example below lists the parameters you will enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="2d060-191">Site5 ASN: 65050</span><span class="sxs-lookup"><span data-stu-id="2d060-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="2d060-192">IP protokołu BGP Site5: 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="2d060-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="2d060-193">Prefiksy ogłaszamy: (na przykład) 10.51.0.0/16 i 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2d060-193">Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="2d060-194">ASN sieci wirtualnej platformy Azure: 65010</span><span class="sxs-lookup"><span data-stu-id="2d060-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="2d060-195">Azure IP BGP sieci wirtualnej 1: 10.12.255.4 tunelu do 40.112.190.5</span><span class="sxs-lookup"><span data-stu-id="2d060-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5</span></span>
    - <span data-ttu-id="2d060-196">Azure IP BGP sieci wirtualnej 2: 10.12.255.5 tunelu do 138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="2d060-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129</span></span>
    - <span data-ttu-id="2d060-197">Trasy statyczne: 10.12.255.4/32 docelowego, następnego skoku tunelu VPN interfejsu do 40.112.190.5 10.12.255.5/32 docelowego, tunel VPN interfejsu do 138.91.156.129 następnego skoku</span><span class="sxs-lookup"><span data-stu-id="2d060-197">Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5                        Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129</span></span>
    - <span data-ttu-id="2d060-198">eBGP wielokrotnego przeskoku: Upewnij się opcja "wielokrotnego przeskoku" eBGP jest włączona na twoim urządzeniu, w razie potrzeby</span><span class="sxs-lookup"><span data-stu-id="2d060-198">eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="2d060-199">Można nawiązać połączenia, po upływie kilku minut, a sesja komunikacji równorzędnej BGP rozpocznie się po nawiązaniu połączenia protokołu IPsec.</span><span class="sxs-lookup"><span data-stu-id="2d060-199">The connection should be established after a few minutes, and the BGP peering session will start once the IPsec connection is established.</span></span> <span data-ttu-id="2d060-200">W tym przykładzie został skonfigurowany do tej pory tylko jeden lokalnego urządzenia sieci VPN, co na diagramie pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="2d060-200">This example so far has configured only one on-premises VPN device, resulting in the diagram shown below:</span></span>

![aktywny aktywny crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-to-the-active-active-vpn-gateway"></a><span data-ttu-id="2d060-202">Krok 3 — Połącz dwa lokalnego urządzenia sieci VPN dla bramy sieci VPN aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="2d060-202">Step 3 - Connect two on-premises VPN devices to the active-active VPN gateway</span></span>
<span data-ttu-id="2d060-203">Mając dwa urządzenia sieci VPN w tej samej sieci lokalnej, można osiągnąć dwie nadmiarowość, nawiązując połączenie bramy sieci VPN platformy Azure, do drugiego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="2d060-203">If you have two VPN devices at the same on-premises network, you can achieve dual redundancy by connecting the Azure VPN gateway to the second VPN device.</span></span>

#### <a name="1-create-the-second-local-network-gateway-for-site5"></a><span data-ttu-id="2d060-204">1. Utwórz drugi bramę sieci lokalnej dla Site5</span><span class="sxs-lookup"><span data-stu-id="2d060-204">1. Create the second local network gateway for Site5</span></span>
<span data-ttu-id="2d060-205">Należy pamiętać, że adres IP bramy, prefiks adresu i adres komunikacji równorzędnej BGP dla drugiego bramy sieci lokalnej musi nie nakładają się na poprzedniej bramy sieci lokalnej w tej samej sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="2d060-205">Note that the gateway IP address, address prefix, and BGP peering address for the second local network gateway must not overlap with the previous local network gateway for the same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-the-vnet-gateway-and-the-second-local-network-gateway"></a><span data-ttu-id="2d060-206">2. Połączenie bramy sieci wirtualnej, a druga Brama sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="2d060-206">2. Connect the VNet gateway and the second local network gateway</span></span>
<span data-ttu-id="2d060-207">Utwórz połączenie z TestVNet1 do Site5_2 z "Wartość", wartość $True</span><span class="sxs-lookup"><span data-stu-id="2d060-207">Create the connection from TestVNet1 to Site5_2 with "EnableBGP" set to $True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="2d060-208">3. Parametry sieci VPN i protokołu BGP dla drugiego lokalnego urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="2d060-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="2d060-209">Podobnie poniżej listy parametrów wprowadzany do drugiego urządzenia sieci VPN:</span><span class="sxs-lookup"><span data-stu-id="2d060-209">Similarly, below lists the parameters you will enter into the second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5
                         Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="2d060-210">Gdy jest nawiązane połączenie (tunele), konieczne będzie podwójne nadmiarowe urządzenia sieci VPN i tunele, połączenie sieci lokalnej i Azure:</span><span class="sxs-lookup"><span data-stu-id="2d060-210">Once the connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![podwójny nadmiarowość crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="2d060-212"><a name ="aav2v"></a>Część 3 — ustanowienie połączenia do wirtualnymi aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="2d060-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="2d060-213">W tej sekcji tworzy aktywny aktywny wirtualnymi do połączenia z protokołem BGP.</span><span class="sxs-lookup"><span data-stu-id="2d060-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="2d060-214">Poniższe instrukcje stanowią ciąg dalszy poprzedzających je kroków wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="2d060-214">The instructions below continue from the previous steps listed above.</span></span> <span data-ttu-id="2d060-215">Należy wykonać [część 1](#aagateway) do tworzenia i konfigurowania TestVNet1 i bramy sieci VPN z protokołem BGP.</span><span class="sxs-lookup"><span data-stu-id="2d060-215">You must complete [Part 1](#aagateway) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="2d060-216">Krok 1 — Tworzenie TestVNet2 i bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="2d060-216">Step 1 - Create TestVNet2 and the VPN gateway</span></span>
<span data-ttu-id="2d060-217">Należy się upewnić, że przestrzeń adresową nową sieć wirtualną TestVNet2, nie mogą się pokrywać ze wszystkimi zakresy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2d060-217">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="2d060-218">W tym przykładzie sieci wirtualne należą do tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2d060-218">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="2d060-219">Można skonfigurować do wirtualnymi połączeń między różnych subskrypcji; Zapoznaj się z [skonfigurować połączenia do wirtualnymi](vpn-gateway-vnet-vnet-rm-ps.md) Aby dowiedzieć się więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="2d060-219">You can set up VNet-to-VNet connections between different subscriptions; please refer to [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) to learn more details.</span></span> <span data-ttu-id="2d060-220">Upewnij się, że możesz dodać "-wartość $True" podczas tworzenia połączenia, aby włączyć protokół BGP.</span><span class="sxs-lookup"><span data-stu-id="2d060-220">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="2d060-221">1. Zadeklarowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="2d060-221">1. Declare your variables</span></span>
<span data-ttu-id="2d060-222">Należy pamiętać o zastąpieniu przykładowych wartości tymi, które mają zostać użyte w danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2d060-222">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="2d060-223">2. Utwórz TestVNet2 w nowej grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="2d060-223">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="2d060-224">3. Tworzenie bramy sieci VPN aktywny aktywny dla TestVNet2</span><span class="sxs-lookup"><span data-stu-id="2d060-224">3. Create the active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="2d060-225">Żądanie dwie publiczne adresy IP do przydzielenia do bramy, który spowoduje utworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2d060-225">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="2d060-226">Zostanie również definiować podsieci i wymagane konfiguracje adresów IP.</span><span class="sxs-lookup"><span data-stu-id="2d060-226">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="2d060-227">Utwórz bramę sieci VPN z liczbą AS a flagi "EnableActiveActiveFeature".</span><span class="sxs-lookup"><span data-stu-id="2d060-227">Create the VPN gateway with the AS number and the "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="2d060-228">Należy pamiętać, że na Twojej bramy sieci VPN platformy Azure, należy zastąpić domyślny numer ASN.</span><span class="sxs-lookup"><span data-stu-id="2d060-228">Note that you must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="2d060-229">Numery ASN dla połączonych sieci wirtualnych musi być inna, aby włączyć protokół BGP i routing tranzytowy.</span><span class="sxs-lookup"><span data-stu-id="2d060-229">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="2d060-230">Krok 2 — Połącz bram TestVNet1 i TestVNet2</span><span class="sxs-lookup"><span data-stu-id="2d060-230">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="2d060-231">W tym przykładzie zarówno bramy znajdują się w tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2d060-231">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="2d060-232">Ten krok można wykonać w tej samej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d060-232">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="2d060-233">1. Pobierz obu bram</span><span class="sxs-lookup"><span data-stu-id="2d060-233">1. Get both gateways</span></span>
<span data-ttu-id="2d060-234">Pamiętaj o zalogowaniu się i połączeniu z subskrypcją 1.</span><span class="sxs-lookup"><span data-stu-id="2d060-234">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="2d060-235">2. Utwórz zarówno połączenia</span><span class="sxs-lookup"><span data-stu-id="2d060-235">2. Create both connections</span></span>
<span data-ttu-id="2d060-236">W tym kroku utworzysz połączenie z TestVNet1 TestVNet2 i połączenie z TestVNet2 do TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2d060-236">In this step, you will create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="2d060-237">Pamiętaj włączyć protokół BGP dla obu połączeń.</span><span class="sxs-lookup"><span data-stu-id="2d060-237">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="2d060-238">Po wykonaniu tych kroków, połączenie zostanie nawiązane w kilka minut, a Protokół BGP sesji połączenia równorzędnego będzie się po zakończeniu połączenia do wirtualnymi z nadmiarowością podwójne:</span><span class="sxs-lookup"><span data-stu-id="2d060-238">After completing these steps, the connection will be establish in a few minutes, and the BGP peering session will be up once the VNet-to-VNet connection is completed with dual redundancy:</span></span>

![aktywny aktywny v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="2d060-240"><a name ="aaupdate"></a>Część 4 — aktualizacja istniejącej bramy między aktywny aktywny i aktywnego gotowości</span><span class="sxs-lookup"><span data-stu-id="2d060-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="2d060-241">Ostatniej sekcji opisano, jak skonfigurować istniejącą bramę sieci VPN platformy Azure z aktywnego gotowości aktywny aktywny tryb lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="2d060-241">The last section will describe how you can configure an existing Azure VPN gateway from active-standby to active-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="2d060-242">Ta sekcja zawiera kroki, aby zmienić rozmiar starszej wersji jednostki SKU (stary jednostki SKU) utworzone bramy sieci VPN ze standardowego na wysokowydajnej.</span><span class="sxs-lookup"><span data-stu-id="2d060-242">This section includes the steps to resize a legacy SKU (old SKU) of an already created VPN gateway from Standard to HighPerformance.</span></span> <span data-ttu-id="2d060-243">Te kroki nie uaktualniaj starego starszej wersji jednostki SKU na jedną z nowych wersji produktu.</span><span class="sxs-lookup"><span data-stu-id="2d060-243">These steps do not upgrade an old legacy SKU to one of the new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-to-active-active-gateway"></a><span data-ttu-id="2d060-244">Skonfiguruj bramę aktywnego gotowości do bramy aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="2d060-244">Configure an active-standby gateway to active-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="2d060-245">1. Parametry bramy</span><span class="sxs-lookup"><span data-stu-id="2d060-245">1. Gateway parameters</span></span>
<span data-ttu-id="2d060-246">Poniższy przykład konwertuje bramy aktywnego gotowości do bramy aktywny aktywny.</span><span class="sxs-lookup"><span data-stu-id="2d060-246">The following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="2d060-247">Należy utworzyć inny publiczny adres IP, a następnie dodać drugi konfigurację IP bramy.</span><span class="sxs-lookup"><span data-stu-id="2d060-247">You need to create another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="2d060-248">Poniżej przedstawiono parametry używane:</span><span class="sxs-lookup"><span data-stu-id="2d060-248">Below shows the parameters used:</span></span>

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

#### <a name="2-create-the-public-ip-address-then-add-the-second-gateway-ip-configuration"></a><span data-ttu-id="2d060-249">2. Utwórz publiczny adres IP, a następnie dodać drugi konfigurację IP bramy</span><span class="sxs-lookup"><span data-stu-id="2d060-249">2. Create the public IP address, then add the second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-the-gateway"></a><span data-ttu-id="2d060-250">3. Włącz tryb aktywny aktywny i zaktualizować bramę</span><span class="sxs-lookup"><span data-stu-id="2d060-250">3. Enable active-active mode and update the gateway</span></span>
<span data-ttu-id="2d060-251">Należy ustawić obiektu bramy w programie PowerShell, aby wyzwolić rzeczywistej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="2d060-251">You must set the gateway object in PowerShell to trigger the actual update.</span></span> <span data-ttu-id="2d060-252">Jednostka SKU bramy sieci wirtualnej muszą także zmienić (po zmianie rozmiaru) na wysokowydajnej, ponieważ zostało utworzone wcześniej jako Standard.</span><span class="sxs-lookup"><span data-stu-id="2d060-252">The SKU of the virtual network gateway must also be changed (resized) to HighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="2d060-253">Ta aktualizacja może potrwać od 30 do 45 minut.</span><span class="sxs-lookup"><span data-stu-id="2d060-253">This update can take 30 to 45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-to-active-standby-gateway"></a><span data-ttu-id="2d060-254">Skonfiguruj bramę aktywny aktywny do aktywnego gotowości bramy</span><span class="sxs-lookup"><span data-stu-id="2d060-254">Configure an active-active gateway to active-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="2d060-255">1. Parametry bramy</span><span class="sxs-lookup"><span data-stu-id="2d060-255">1. Gateway parameters</span></span>
<span data-ttu-id="2d060-256">Użyj tych samych parametrach jak wyżej, uzyskać nazwy konfiguracji adresu IP, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="2d060-256">Use the same parameters as above, get the name of the IP configuration you want to remove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-the-gateway-ip-configuration-and-disable-the-active-active-mode"></a><span data-ttu-id="2d060-257">2. Usuń konfigurację IP bramy i Wyłącz tryb aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="2d060-257">2. Remove the gateway IP configuration and disable the active-active mode</span></span>
<span data-ttu-id="2d060-258">Podobnie należy ustawić obiektu bramy w programie PowerShell, aby wyzwolić rzeczywistej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="2d060-258">Similarly, you must set the gateway object in PowerShell to trigger the actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="2d060-259">Ta aktualizacja może potrwać do 30 do 45 minut.</span><span class="sxs-lookup"><span data-stu-id="2d060-259">This update can take up to 30 to  45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d060-260">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2d060-260">Next steps</span></span>
<span data-ttu-id="2d060-261">Po zakończeniu procesu nawiązywania połączenia można dodać do sieci wirtualnych maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="2d060-261">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="2d060-262">Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2d060-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>