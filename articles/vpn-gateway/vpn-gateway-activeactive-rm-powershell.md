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
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="3621d-103">Skonfigurować połączenia sieci VPN S2S aktywny aktywny z bramy sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3621d-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="3621d-104">W tym artykule przedstawiono hello kroki toocreate aktywny aktywny między lokalizacjami i wirtualnymi do połączeń przy użyciu modelu wdrażania usługi Resource Manager hello i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3621d-104">This article walks you through hello steps toocreate active-active cross-premises and VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="3621d-105">O wysokiej dostępności między lokalizacjami połączeń</span><span class="sxs-lookup"><span data-stu-id="3621d-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="3621d-106">tooachieve wysokiej dostępności i wirtualnymi do łączności między lokalizacjami, należy wdrożyć wiele bram sieci VPN i ustanowienia wielu równoległych połączeń między sieciami i Azure.</span><span class="sxs-lookup"><span data-stu-id="3621d-106">tooachieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="3621d-107">Zobacz [wysokiej dostępności między lokalizacjami i łączności do wirtualnymi](vpn-gateway-highlyavailable.md) Omówienie opcji łączności i topologii.</span><span class="sxs-lookup"><span data-stu-id="3621d-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="3621d-108">Ten artykuł zawiera instrukcje hello tooset się aktywny aktywny między lokalizacjami połączenie sieci VPN i aktywny aktywny połączenie między dwiema sieciami wirtualnymi:</span><span class="sxs-lookup"><span data-stu-id="3621d-108">This article provides hello instructions tooset up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="3621d-109">Część 1 — Tworzenie i konfigurowanie bramy sieci VPN platformy Azure w trybie aktywny / aktywny</span><span class="sxs-lookup"><span data-stu-id="3621d-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="3621d-110">Część 2 - zestawiania połączeń między różnymi lokalizacjami aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="3621d-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="3621d-111">Część 3 — ustanowienie połączenia do wirtualnymi aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="3621d-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="3621d-112">Część 4 — aktualizacja istniejącej bramy między aktywny aktywny i aktywnego gotowości</span><span class="sxs-lookup"><span data-stu-id="3621d-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="3621d-113">Można połączyć te razem toobuild topologii sieci bardziej złożonych, wysokiej dostępności, która odpowiada Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="3621d-113">You can combine these together toobuild a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3621d-114">Należy pamiętać, że w trybie aktywny aktywny hello używa hello tylko następujące wersje produktu:</span><span class="sxs-lookup"><span data-stu-id="3621d-114">Please note that hello active-active mode uses only hello following SKUs:</span></span> 
  * <span data-ttu-id="3621d-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="3621d-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="3621d-116">Wysokowydajnej (dla starego starszej wersji jednostki SKU)</span><span class="sxs-lookup"><span data-stu-id="3621d-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="3621d-117"><a name ="aagateway"></a>Część 1 — Tworzenie i konfigurowanie aktywny aktywny bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="3621d-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="3621d-118">następujące kroki Hello skonfiguruje bramy sieci VPN platformy Azure w trybach aktywny aktywny.</span><span class="sxs-lookup"><span data-stu-id="3621d-118">hello following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="3621d-119">Witaj podstawowych różnic między bramami aktywny aktywny i aktywnego gotowości hello:</span><span class="sxs-lookup"><span data-stu-id="3621d-119">hello key differences between hello active-active and active-standby gateways:</span></span>

* <span data-ttu-id="3621d-120">Należy toocreate dwóch konfiguracji IP bramy z dwóch publicznych adresów IP</span><span class="sxs-lookup"><span data-stu-id="3621d-120">You need toocreate two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="3621d-121">Należy ustawić flagę EnableActiveActiveFeature hello</span><span class="sxs-lookup"><span data-stu-id="3621d-121">You need set hello EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="3621d-122">Jednostka SKU bramy Hello musi być VpnGw1, VpnGw2, VpnGw3 lub wysokowydajnej (starszej wersji jednostki SKU).</span><span class="sxs-lookup"><span data-stu-id="3621d-122">hello gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="3621d-123">Witaj inne właściwości są hello taki sam jak hello bramy z systemem innym niż — aktywny aktywny.</span><span class="sxs-lookup"><span data-stu-id="3621d-123">hello other properties are hello same as hello non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="3621d-124">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="3621d-124">Before you begin</span></span>
* <span data-ttu-id="3621d-125">Sprawdź, czy masz subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3621d-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="3621d-126">Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3621d-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3621d-127">Polecenia cmdlet programu PowerShell usługi Azure Resource Manager hello tooinstall jest potrzebny.</span><span class="sxs-lookup"><span data-stu-id="3621d-127">You'll need tooinstall hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="3621d-128">Zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3621d-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="3621d-129">Krok 1 — Tworzenie i konfigurowanie VNet1</span><span class="sxs-lookup"><span data-stu-id="3621d-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="3621d-130">1. Zadeklarowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="3621d-130">1. Declare your variables</span></span>
<span data-ttu-id="3621d-131">To ćwiczenie rozpoczniemy od zadeklarowania zmiennych.</span><span class="sxs-lookup"><span data-stu-id="3621d-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="3621d-132">w poniższym przykładzie Hello deklaruje zmienne hello używania hello wartości w tym ćwiczeniu.</span><span class="sxs-lookup"><span data-stu-id="3621d-132">hello example below declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="3621d-133">Należy się, że wartości hello tooreplace własnymi podczas konfigurowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="3621d-133">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="3621d-134">Można używać tych zmiennych, jeśli używasz za pośrednictwem toobecome kroki hello zapoznać się z tym typem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3621d-134">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="3621d-135">Modyfikuj zmienne hello, a następnie skopiuj i Wklej w konsoli programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3621d-135">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="3621d-136">2. Połączyć subskrypcję tooyour i utworzyć nową grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="3621d-136">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="3621d-137">Upewnij się, że przełącznik tooPowerShell tryb toouse hello poleceń cmdlet Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="3621d-137">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="3621d-138">Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3621d-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="3621d-139">Otwórz konsolę programu PowerShell i Połącz konto tooyour.</span><span class="sxs-lookup"><span data-stu-id="3621d-139">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="3621d-140">Użyj następujących hello przykładowe toohelp, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="3621d-140">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="3621d-141">3. Utworzenie sieci TestVNet1</span><span class="sxs-lookup"><span data-stu-id="3621d-141">3. Create TestVNet1</span></span>
<span data-ttu-id="3621d-142">Poniższy przykład Hello tworzy sieć wirtualną o nazwie TestVNet1 i trzy podsieci, co GatewaySubnet o nazwie jedną o nazwie frontonu i jedną o nazwie wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3621d-142">hello sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="3621d-143">Podczas zastępowania wartości ważne jest, aby podsieć bramy zawsze nosiła nazwę GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="3621d-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="3621d-144">W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="3621d-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="3621d-145">Krok 2 — Tworzenie hello bramy sieci VPN dla TestVNet1 w trybie aktywny / aktywny</span><span class="sxs-lookup"><span data-stu-id="3621d-145">Step 2 - Create hello VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="3621d-146">1. Tworzenie hello publicznych adresów IP i konfiguracje adresów IP bramy</span><span class="sxs-lookup"><span data-stu-id="3621d-146">1. Create hello public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="3621d-147">Żądanie dwa publiczne adresy toobe toohello przydzielone brama IP utworzone sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3621d-147">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="3621d-148">Zostanie również definiować hello podsieci i wymagane konfiguracje adresów IP.</span><span class="sxs-lookup"><span data-stu-id="3621d-148">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="3621d-149">2. Tworzenie bramy sieci VPN hello z konfiguracją aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="3621d-149">2. Create hello VPN gateway with active-active configuration</span></span>
<span data-ttu-id="3621d-150">Tworzenie bramy sieci wirtualnej powitania dla TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="3621d-150">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="3621d-151">Zauważ, że istnieją dwa wpisy GatewayIpConfig, i hello EnableActiveActiveFeature flaga jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="3621d-151">Note that there are two GatewayIpConfig entries, and hello EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="3621d-152">Tworzenie bramy może trochę potrwać (45 minut lub więcej toocomplete).</span><span class="sxs-lookup"><span data-stu-id="3621d-152">Creating a gateway can take a while (45 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a><span data-ttu-id="3621d-153">3. Uzyskaj hello bramy publicznych adresów IP i adres IP elementu równorzędnego protokołu BGP hello</span><span class="sxs-lookup"><span data-stu-id="3621d-153">3. Obtain hello gateway public IP addresses and hello BGP Peer IP address</span></span>
<span data-ttu-id="3621d-154">Po utworzeniu bramy hello należy adresem IP elementu równorzędnego protokołu BGP hello tooobtain hello bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3621d-154">Once hello gateway is created, you will need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="3621d-155">Ten adres jest wymagane tooconfigure hello bramy sieci VPN platformy Azure jako element równorzędny BGP dla lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="3621d-155">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="3621d-156">Użyj następującego polecenia cmdlet tooshow Witaj dwie publiczne adresy IP przydzielone dla bramy sieci VPN, a ich odpowiednie adresy IP elementu równorzędnego protokołu BGP dla każdego wystąpienia bramy hello:</span><span class="sxs-lookup"><span data-stu-id="3621d-156">Use hello following cmdlets tooshow hello two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

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

<span data-ttu-id="3621d-157">kolejność Hello hello publicznych adresów IP dla wystąpień bramy hello i hello, które są odpowiednie adresy komunikacji równorzędnej BGP hello takie same.</span><span class="sxs-lookup"><span data-stu-id="3621d-157">hello order of hello public IP addresses for hello gateway instances and hello corresponding BGP Peering Addresses are hello same.</span></span> <span data-ttu-id="3621d-158">W tym przykładzie hello bramy maszyny Wirtualnej z publicznego adresu IP z 40.112.190.5 użyje 10.12.255.4 jako adres komunikacji równorzędnej BGP, a brama hello z 138.91.156.129 użyje 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="3621d-158">In this example, hello gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and hello gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="3621d-159">Te informacje są potrzebne podczas konfigurowania w lokalnej sieci VPN urządzeń nawiązujących połączenie toohello aktywny aktywny bramy.</span><span class="sxs-lookup"><span data-stu-id="3621d-159">This information is needed when you set up your on premises VPN devices connecting toohello active-active gateway.</span></span> <span data-ttu-id="3621d-160">Brama Hello jest wyświetlany na diagramie hello poniżej przy użyciu wszystkich adresów:</span><span class="sxs-lookup"><span data-stu-id="3621d-160">hello gateway is shown in hello diagram below with all addresses:</span></span>

![aktywny aktywny bramy](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="3621d-162">Po utworzeniu bramy hello, używając tej bramy tooestablish aktywny aktywny obejmującym różne pomieszczenia lub połączenia do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="3621d-162">Once hello gateway is created, you can use this gateway tooestablish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="3621d-163">następujące sekcje Hello przeprowadzi hello kroki toocomplete hello wykonywania.</span><span class="sxs-lookup"><span data-stu-id="3621d-163">hello following sections will walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="3621d-164"><a name ="aacrossprem"></a>Część 2 - nawiązywania połączenia między lokalizacjami aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="3621d-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="3621d-165">tooestablish połączenia między różnymi lokalizacjami, należy toocreate toorepresent bramy sieci lokalnej lokalnego urządzenia sieci VPN i bramy sieci VPN platformy Azure hello tooconnect połączenia przy użyciu hello bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="3621d-165">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello Azure VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="3621d-166">W tym przykładzie Brama sieci VPN platformy Azure hello jest w trybie aktywny / aktywny.</span><span class="sxs-lookup"><span data-stu-id="3621d-166">In this example, hello Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="3621d-167">W związku z tym nawet, jeśli istnieje tylko jeden lokalnego urządzenia sieci VPN (bramy sieci lokalnej) i jednego połączenia zasobów, zarówno wystąpień bramy sieci VPN platformy Azure zostanie ustanowiona tunel S2S VPN, jak hello lokalnego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3621d-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with hello on-premises device.</span></span>

<span data-ttu-id="3621d-168">Przed kontynuowaniem upewnij się, zostały ukończone [część 1](#aagateway) tego ćwiczenia.</span><span class="sxs-lookup"><span data-stu-id="3621d-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="3621d-169">Krok 1 — Tworzenie i konfigurowanie hello bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="3621d-169">Step 1 - Create and configure hello local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="3621d-170">1. Zadeklarowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="3621d-170">1. Declare your variables</span></span>
<span data-ttu-id="3621d-171">Tego ćwiczenia będą nadal wyświetlane na diagramie hello konfiguracji hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="3621d-171">This exercise will continue toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="3621d-172">Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3621d-172">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="3621d-173">Kilka rzeczy toonote dotyczącymi parametrów bramy sieci lokalnej hello:</span><span class="sxs-lookup"><span data-stu-id="3621d-173">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="3621d-174">Witaj bramy sieci lokalnej może być w hello takie same lub innej lokalizacji i zasobów grupy jako hello bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="3621d-174">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="3621d-175">W tym przykładzie przedstawiono je w różnych grupach zasobów, ale w hello tej samej lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3621d-175">This example shows them in different resource groups but in hello same Azure location.</span></span>
* <span data-ttu-id="3621d-176">Jeśli istnieje tylko jeden lokalnego urządzenia sieci VPN zgodnie z powyższym, hello aktywny aktywny połączenia można pracować z lub bez protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="3621d-176">If there is only one on-premises VPN device as shown above, hello active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="3621d-177">W tym przykładzie użyto BGP hello połączenia między lokalizacjami.</span><span class="sxs-lookup"><span data-stu-id="3621d-177">This example uses BGP for hello cross-premises connection.</span></span>
* <span data-ttu-id="3621d-178">Jeśli protokół BGP jest włączony, należy toodeclare dla bramy sieci lokalnej hello prefiks hello jest adres hosta hello adresu IP elementu równorzędnego protokołu BGP na urządzeniu sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="3621d-178">If BGP is enabled, hello prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="3621d-179">W takim przypadku jest /32 prefiksu "10.52.255.253/32".</span><span class="sxs-lookup"><span data-stu-id="3621d-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="3621d-180">Przypomnienia należy użyć innego protokołu BGP numerów ASN między lokalnymi sieciami i sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3621d-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="3621d-181">Są one takie same hello, należy najpierw toochange ASN Twojej sieci wirtualnej Jeśli lokalnego urządzenia sieci VPN już używa hello numeru ASN toopeer z innych sąsiadów BGP.</span><span class="sxs-lookup"><span data-stu-id="3621d-181">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="3621d-182">2. Tworzenie bramy sieci lokalnej powitania dla Site5</span><span class="sxs-lookup"><span data-stu-id="3621d-182">2. Create hello local network gateway for Site5</span></span>
<span data-ttu-id="3621d-183">Przed kontynuowaniem upewnij się, że są nadal połączonych tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="3621d-183">Before you continue, please make sure you are still connected tooSubscription 1.</span></span> <span data-ttu-id="3621d-184">Utwórz grupę zasobów hello, jeśli nie został jeszcze utworzony.</span><span class="sxs-lookup"><span data-stu-id="3621d-184">Create hello resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="3621d-185">Krok 2 — Połącz hello bramy sieci wirtualnej i Brama sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="3621d-185">Step 2 - Connect hello VNet gateway and local network gateway</span></span>
#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="3621d-186">1. Pobierz Witaj dwie bramy</span><span class="sxs-lookup"><span data-stu-id="3621d-186">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="3621d-187">2. Utwórz połączenie tooSite5 TestVNet1 hello</span><span class="sxs-lookup"><span data-stu-id="3621d-187">2. Create hello TestVNet1 tooSite5 connection</span></span>
<span data-ttu-id="3621d-188">W tym kroku utworzysz hello połączenia z TestVNet1 tooSite5_1 z ustawić także "wartość" $True.</span><span class="sxs-lookup"><span data-stu-id="3621d-188">In this step, you will create hello connection from TestVNet1 tooSite5_1 with "EnableBGP" set too$True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="3621d-189">3. Parametry sieci VPN i protokołu BGP dla lokalnego urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="3621d-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="3621d-190">przykład Witaj poniżej wymieniono hello parametry, które wejdzie w hello sekcji konfiguracji protokołu BGP na urządzeniu lokalnym sieci VPN w tym ćwiczeniu:</span><span class="sxs-lookup"><span data-stu-id="3621d-190">hello example below lists hello parameters you will enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="3621d-191">Site5 ASN: 65050</span><span class="sxs-lookup"><span data-stu-id="3621d-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="3621d-192">IP protokołu BGP Site5: 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="3621d-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="3621d-193">Prefiksy tooannounce: (na przykład) 10.51.0.0/16 i 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="3621d-193">Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="3621d-194">ASN sieci wirtualnej platformy Azure: 65010</span><span class="sxs-lookup"><span data-stu-id="3621d-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="3621d-195">Azure IP BGP sieci wirtualnej 1: 10.12.255.4 dla too40.112.190.5 tunelu</span><span class="sxs-lookup"><span data-stu-id="3621d-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5</span></span>
    - <span data-ttu-id="3621d-196">Azure IP BGP sieci wirtualnej 2: 10.12.255.5 dla too138.91.156.129 tunelu</span><span class="sxs-lookup"><span data-stu-id="3621d-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129</span></span>
    - <span data-ttu-id="3621d-197">Trasy statyczne: 10.12.255.4/32 docelowego, 10.12.255.5/32 docelowego too40.112.190.5 interfejsu tunelu następnego skoku hello sieci VPN, następnego skoku hello VPN tunelu interfejsu too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="3621d-197">Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5                        Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129</span></span>
    - <span data-ttu-id="3621d-198">eBGP wielokrotnego przeskoku: Upewnij się opcja "wielokrotnego przeskoku" hello, eBGP jest włączona na twoim urządzeniu, w razie potrzeby</span><span class="sxs-lookup"><span data-stu-id="3621d-198">eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="3621d-199">Po za kilka minut, a sesja komunikacji równorzędnej BGP hello rozpocznie się po nawiązaniu połączenia IPsec hello należy ustanowić Hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="3621d-199">hello connection should be established after a few minutes, and hello BGP peering session will start once hello IPsec connection is established.</span></span> <span data-ttu-id="3621d-200">W tym przykładzie został skonfigurowany do tej pory tylko jeden lokalnego urządzenia sieci VPN, co hello diagramie pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="3621d-200">This example so far has configured only one on-premises VPN device, resulting in hello diagram shown below:</span></span>

![aktywny aktywny crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a><span data-ttu-id="3621d-202">Krok 3 — Połącz dwa lokalnej sieci VPN urządzenia toohello aktywny aktywny VPN bramy</span><span class="sxs-lookup"><span data-stu-id="3621d-202">Step 3 - Connect two on-premises VPN devices toohello active-active VPN gateway</span></span>
<span data-ttu-id="3621d-203">Jeśli masz dwie urządzenia sieci VPN na powitania sam lokalnej sieci, Podwójna nadmiarowości można osiągnąć za łączącego hello Azure urządzenie bramy VPN toohello drugiej sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="3621d-203">If you have two VPN devices at hello same on-premises network, you can achieve dual redundancy by connecting hello Azure VPN gateway toohello second VPN device.</span></span>

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a><span data-ttu-id="3621d-204">1. Tworzenie bramy sieci lokalnej drugi hello dla Site5</span><span class="sxs-lookup"><span data-stu-id="3621d-204">1. Create hello second local network gateway for Site5</span></span>
<span data-ttu-id="3621d-205">Należy pamiętać, że adres IP bramy hello, prefiks adresu i adres komunikacji równorzędnej BGP dla bramy sieci lokalnej drugi hello musi nie nakładają się na powitania poprzedniej bramy sieci lokalnej dla hello takie same lokalnej sieci.</span><span class="sxs-lookup"><span data-stu-id="3621d-205">Note that hello gateway IP address, address prefix, and BGP peering address for hello second local network gateway must not overlap with hello previous local network gateway for hello same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a><span data-ttu-id="3621d-206">2. Połączenia bramy sieci wirtualnej hello i hello druga Brama sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="3621d-206">2. Connect hello VNet gateway and hello second local network gateway</span></span>
<span data-ttu-id="3621d-207">Utwórz połączenie hello z TestVNet1 tooSite5_2 "Wartość" Ustaw zbyt$ True</span><span class="sxs-lookup"><span data-stu-id="3621d-207">Create hello connection from TestVNet1 tooSite5_2 with "EnableBGP" set too$True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="3621d-208">3. Parametry sieci VPN i protokołu BGP dla drugiego lokalnego urządzenia sieci VPN</span><span class="sxs-lookup"><span data-stu-id="3621d-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="3621d-209">Podobnie poniższe parametry hello list zostanie wejdzie w hello drugiego urządzenia sieci VPN:</span><span class="sxs-lookup"><span data-stu-id="3621d-209">Similarly, below lists hello parameters you will enter into hello second VPN device:</span></span>

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

<span data-ttu-id="3621d-210">Po ustaleniu hello połączenia (tunele) należy podwójne nadmiarowe urządzenia sieci VPN i tunele, połączenie sieci lokalnej i Azure:</span><span class="sxs-lookup"><span data-stu-id="3621d-210">Once hello connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![podwójny nadmiarowość crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="3621d-212"><a name ="aav2v"></a>Część 3 — ustanowienie połączenia do wirtualnymi aktywny aktywny</span><span class="sxs-lookup"><span data-stu-id="3621d-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="3621d-213">W tej sekcji tworzy aktywny aktywny wirtualnymi do połączenia z protokołem BGP.</span><span class="sxs-lookup"><span data-stu-id="3621d-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="3621d-214">Poniższe instrukcje Hello nadal z poprzednich kroków hello wymienionych powyżej.</span><span class="sxs-lookup"><span data-stu-id="3621d-214">hello instructions below continue from hello previous steps listed above.</span></span> <span data-ttu-id="3621d-215">Należy wykonać [część 1](#aagateway) toocreate i skonfiguruj TestVNet1 oraz hello bramy sieci VPN z protokołem BGP.</span><span class="sxs-lookup"><span data-stu-id="3621d-215">You must complete [Part 1](#aagateway) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="3621d-216">Krok 1 — Tworzenie TestVNet2 i hello bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="3621d-216">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>
<span data-ttu-id="3621d-217">Jest ważne toomake się, że przestrzeń adresów IP hello nowej sieci wirtualnej hello, TestVNet2, nakłada się ze wszystkimi zakresy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3621d-217">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="3621d-218">W tym przykładzie hello sieci wirtualnych należy toohello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3621d-218">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="3621d-219">Można skonfigurować do wirtualnymi połączeń między różnych subskrypcji; Zobacz zbyt[skonfigurować połączenia do wirtualnymi](vpn-gateway-vnet-vnet-rm-ps.md) toolearn więcej szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="3621d-219">You can set up VNet-to-VNet connections between different subscriptions; please refer too[Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) toolearn more details.</span></span> <span data-ttu-id="3621d-220">Upewnij się, że możesz dodać hello "-wartość $True" podczas tworzenia hello tooenable połączeń protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="3621d-220">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="3621d-221">1. Zadeklarowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="3621d-221">1. Declare your variables</span></span>
<span data-ttu-id="3621d-222">Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3621d-222">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="3621d-223">2. Utwórz TestVNet2 w hello nową grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="3621d-223">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="3621d-224">3. Tworzenie bramy sieci VPN hello aktywny aktywny dla TestVNet2</span><span class="sxs-lookup"><span data-stu-id="3621d-224">3. Create hello active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="3621d-225">Żądanie dwa publiczne adresy toobe toohello przydzielone brama IP utworzone sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3621d-225">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="3621d-226">Zostanie również definiować hello podsieci i wymagane konfiguracje adresów IP.</span><span class="sxs-lookup"><span data-stu-id="3621d-226">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="3621d-227">Utwórz bramę sieci VPN hello z hello jako numer i hello flagi "EnableActiveActiveFeature".</span><span class="sxs-lookup"><span data-stu-id="3621d-227">Create hello VPN gateway with hello AS number and hello "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="3621d-228">Należy pamiętać, że konieczne jest przesłonięcie hello domyślny numer ASN w Twojej bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3621d-228">Note that you must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="3621d-229">Witaj numerów ASN dla hello połączone sieci wirtualne muszą być różne tooenable BGP i routing tranzytowy.</span><span class="sxs-lookup"><span data-stu-id="3621d-229">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="3621d-230">Krok 2 — Połącz hello TestVNet1 i TestVNet2 bram</span><span class="sxs-lookup"><span data-stu-id="3621d-230">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="3621d-231">W tym przykładzie zarówno bramy znajdują się w hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3621d-231">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="3621d-232">Można wykonać ten krok w hello tej samej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3621d-232">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="3621d-233">1. Pobierz obu bram</span><span class="sxs-lookup"><span data-stu-id="3621d-233">1. Get both gateways</span></span>
<span data-ttu-id="3621d-234">Upewnij się, zaloguj się i połącz tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="3621d-234">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="3621d-235">2. Utwórz zarówno połączenia</span><span class="sxs-lookup"><span data-stu-id="3621d-235">2. Create both connections</span></span>
<span data-ttu-id="3621d-236">W tym kroku utworzysz hello połączenia z TestVNet1 tooTestVNet2 i hello połączenia z TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="3621d-236">In this step, you will create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="3621d-237">Należy się tooenable BGP dla obu połączeń.</span><span class="sxs-lookup"><span data-stu-id="3621d-237">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="3621d-238">Po wykonaniu tych czynności hello połączenie zostanie nawiązane za kilka minut, a sesji komunikacji równorzędnej BGP hello będą się po zakończeniu hello wirtualnymi do połączenia z nadmiarowością podwójne:</span><span class="sxs-lookup"><span data-stu-id="3621d-238">After completing these steps, hello connection will be establish in a few minutes, and hello BGP peering session will be up once hello VNet-to-VNet connection is completed with dual redundancy:</span></span>

![aktywny aktywny v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="3621d-240"><a name ="aaupdate"></a>Część 4 — aktualizacja istniejącej bramy między aktywny aktywny i aktywnego gotowości</span><span class="sxs-lookup"><span data-stu-id="3621d-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="3621d-241">Witaj ostatniej sekcji opisano, jak można skonfigurować istniejącą bramę sieci VPN platformy Azure w trybie aktywny tooactive aktywnego gotowości lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="3621d-241">hello last section will describe how you can configure an existing Azure VPN gateway from active-standby tooactive-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="3621d-242">Ta sekcja zawiera tooresize kroki hello starszej wersji jednostki SKU (stary jednostki SKU) utworzone bramy sieci VPN z tooHighPerformance standardowa.</span><span class="sxs-lookup"><span data-stu-id="3621d-242">This section includes hello steps tooresize a legacy SKU (old SKU) of an already created VPN gateway from Standard tooHighPerformance.</span></span> <span data-ttu-id="3621d-243">Te kroki nie uaktualniaj starego tooone starszej wersji jednostki SKU z hello nowe jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="3621d-243">These steps do not upgrade an old legacy SKU tooone of hello new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a><span data-ttu-id="3621d-244">Skonfiguruj bramę aktywny tooactive aktywnego gotowości bramy</span><span class="sxs-lookup"><span data-stu-id="3621d-244">Configure an active-standby gateway tooactive-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="3621d-245">1. Parametry bramy</span><span class="sxs-lookup"><span data-stu-id="3621d-245">1. Gateway parameters</span></span>
<span data-ttu-id="3621d-246">Poniższy przykład Hello konwertuje bramy aktywnego gotowości bramy aktywny aktywny.</span><span class="sxs-lookup"><span data-stu-id="3621d-246">hello following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="3621d-247">Możesz toocreate innym publicznym adresem IP, a następnie dodać drugi konfigurację IP bramy.</span><span class="sxs-lookup"><span data-stu-id="3621d-247">You need toocreate another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="3621d-248">Poniżej przedstawiono hello używane parametry:</span><span class="sxs-lookup"><span data-stu-id="3621d-248">Below shows hello parameters used:</span></span>

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

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a><span data-ttu-id="3621d-249">2. Utwórz hello publicznego adresu IP, a następnie dodaj hello drugi konfiguracji IP bramy</span><span class="sxs-lookup"><span data-stu-id="3621d-249">2. Create hello public IP address, then add hello second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a><span data-ttu-id="3621d-250">3. Włącz bramę hello aktywny aktywny tryb i aktualizacji</span><span class="sxs-lookup"><span data-stu-id="3621d-250">3. Enable active-active mode and update hello gateway</span></span>
<span data-ttu-id="3621d-251">Witaj obiektu bramy musi być ustawiona w PowerShell tootrigger hello rzeczywistej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="3621d-251">You must set hello gateway object in PowerShell tootrigger hello actual update.</span></span> <span data-ttu-id="3621d-252">Jednostka SKU bramy sieci wirtualnej hello Hello musi również zostać zmieniony tooHighPerformance (po zmianie rozmiaru), ponieważ zostało utworzone wcześniej jako Standard.</span><span class="sxs-lookup"><span data-stu-id="3621d-252">hello SKU of hello virtual network gateway must also be changed (resized) tooHighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="3621d-253">Ta aktualizacja może potrwać 30 minut too45.</span><span class="sxs-lookup"><span data-stu-id="3621d-253">This update can take 30 too45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a><span data-ttu-id="3621d-254">Skonfiguruj bramę wstrzymania tooactive aktywny aktywny bramy</span><span class="sxs-lookup"><span data-stu-id="3621d-254">Configure an active-active gateway tooactive-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="3621d-255">1. Parametry bramy</span><span class="sxs-lookup"><span data-stu-id="3621d-255">1. Gateway parameters</span></span>
<span data-ttu-id="3621d-256">Użyj hello takie same parametry jak wyżej, uzyskać nazwę hello hello konfiguracji adresu IP ma tooremove.</span><span class="sxs-lookup"><span data-stu-id="3621d-256">Use hello same parameters as above, get hello name of hello IP configuration you want tooremove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a><span data-ttu-id="3621d-257">2. Usuń konfigurację IP bramy hello i wyłączyć hello aktywny aktywny tryb</span><span class="sxs-lookup"><span data-stu-id="3621d-257">2. Remove hello gateway IP configuration and disable hello active-active mode</span></span>
<span data-ttu-id="3621d-258">Podobnie należy ustawić obiektu bramy hello w PowerShell tootrigger hello rzeczywistej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="3621d-258">Similarly, you must set hello gateway object in PowerShell tootrigger hello actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="3621d-259">Ta aktualizacja może potrwać too30 zbyt 45 minut.</span><span class="sxs-lookup"><span data-stu-id="3621d-259">This update can take up too30 too 45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3621d-260">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3621d-260">Next steps</span></span>
<span data-ttu-id="3621d-261">Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3621d-261">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="3621d-262">Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3621d-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
