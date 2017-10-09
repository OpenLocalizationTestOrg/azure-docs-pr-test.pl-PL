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
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="57fc7-103">Jak tooconfigure protokołu BGP na bramy sieci VPN platformy Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="57fc7-103">How tooconfigure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="57fc7-104">W tym artykule przedstawiono hello kroki tooenable protokołu BGP na połączenie sieci VPN typu lokacja-lokacja (S2S) między lokalizacjami i połączenia do wirtualnymi przy użyciu modelu wdrażania usługi Resource Manager hello i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57fc7-104">This article walks you through hello steps tooenable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="57fc7-105">BGP — informacje</span><span class="sxs-lookup"><span data-stu-id="57fc7-105">About BGP</span></span>
<span data-ttu-id="57fc7-106">Protokół BGP jest hello standardowy protokół routingu często używane w hello Internet tooexchange routingu i uzyskiwanie informacji między dwie lub więcej sieci.</span><span class="sxs-lookup"><span data-stu-id="57fc7-106">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="57fc7-107">Protokół BGP umożliwia bramy sieci VPN hello Azure i lokalnymi urządzeniami sieci VPN, nazywane elementów równorzędnych BGP lub sąsiadów, tooexchange "tras" który poinformuje zarówno bramy na powitania dostępności i uzyskiwanie tych prefiksy toogo za pośrednictwem bramy hello lub routery związane.</span><span class="sxs-lookup"><span data-stu-id="57fc7-107">BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="57fc7-108">Protokół BGP można także włączyć routing tranzytowy między wieloma sieciami przez propagowania tras BGP bramy uczy się z jednego tooall elementu równorzędnego protokołu BGP innych elementów równorzędnych protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="57fc7-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span>

<span data-ttu-id="57fc7-109">Zobacz [Omówienie protokołu BGP z bramy sieci VPN Azure](vpn-gateway-bgp-overview.md) więcej omówienie zalet protokołu BGP i toounderstand hello wymagania techniczne i zagadnienia dotyczące użycia protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="57fc7-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and toounderstand hello technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="57fc7-110">Wprowadzenie do korzystania z protokołu BGP w bramach sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="57fc7-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="57fc7-111">W tym artykule przedstawiono hello toodo kroki hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="57fc7-111">This article walks you through hello steps toodo hello following tasks:</span></span>

* [<span data-ttu-id="57fc7-112">Część 1 - Włącz protokół BGP dla bramy sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="57fc7-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="57fc7-113">Część 2 - ustanowić połączenia między lokalizacjami z protokołem BGP</span><span class="sxs-lookup"><span data-stu-id="57fc7-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="57fc7-114">Część 3 — ustanowienie połączenia do wirtualnymi z protokołem BGP</span><span class="sxs-lookup"><span data-stu-id="57fc7-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="57fc7-115">Każda część instrukcji hello formularzy podstawowego bloku konstrukcyjnego włączenia protokołu BGP w połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="57fc7-115">Each part of hello instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="57fc7-116">Po ukończeniu wszystkich trzech części kompilacji topologii hello pokazane na powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="57fc7-116">If you complete all three parts, you build hello topology as shown in hello following diagram:</span></span>

![Topologii protokołu BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="57fc7-118">Możesz łączyć toobuild razem części sieci bardziej złożonymi, a z wieloma przeskokami, przesyłania, które spełni wymagania organizacji.</span><span class="sxs-lookup"><span data-stu-id="57fc7-118">You can combine parts together toobuild a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="57fc7-119"><a name ="enablebgp"></a>Część 1 — Konfigurowanie protokołu BGP na powitania bramy sieci VPN platformy Azure</span><span class="sxs-lookup"><span data-stu-id="57fc7-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on hello Azure VPN Gateway</span></span>
<span data-ttu-id="57fc7-120">kroki konfiguracji Hello skonfigurować hello parametry BGP bramy sieci VPN platformy Azure hello pokazane na powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="57fc7-120">hello configuration steps set up hello BGP parameters of hello Azure VPN gateway as shown in hello following diagram:</span></span>

![Protokół BGP bramy](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="57fc7-122">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="57fc7-122">Before you begin</span></span>
* <span data-ttu-id="57fc7-123">Sprawdź, czy masz subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57fc7-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="57fc7-124">Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57fc7-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="57fc7-125">Zainstaluj polecenia cmdlet programu PowerShell usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="57fc7-125">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="57fc7-126">Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="57fc7-126">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="57fc7-127">Krok 1 — Tworzenie i konfigurowanie VNet1</span><span class="sxs-lookup"><span data-stu-id="57fc7-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="57fc7-128">1. Zadeklarowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="57fc7-128">1. Declare your variables</span></span>
<span data-ttu-id="57fc7-129">W tym ćwiczeniu Rozpoczniemy przez zadeklarowanie naszych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="57fc7-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="57fc7-130">Witaj poniższy przykład deklaruje hello zmienne używania hello wartości w tym ćwiczeniu.</span><span class="sxs-lookup"><span data-stu-id="57fc7-130">hello following example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="57fc7-131">Należy się, że wartości hello tooreplace własnymi podczas konfigurowania w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="57fc7-131">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="57fc7-132">Można używać tych zmiennych, jeśli używasz za pośrednictwem toobecome kroki hello zapoznać się z tym typem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="57fc7-132">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="57fc7-133">Modyfikuj zmienne hello, a następnie skopiuj i Wklej w konsoli programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57fc7-133">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="57fc7-134">2. Połączyć subskrypcję tooyour i utworzyć nową grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="57fc7-134">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="57fc7-135">Witaj toouse poleceń cmdlet Menedżera zasobów, upewnij się, że Przełącz tryb tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="57fc7-135">toouse hello Resource Manager cmdlets, Make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="57fc7-136">Więcej informacji znajduje się w temacie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Używanie programu Windows PowerShell z usługą Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="57fc7-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="57fc7-137">Otwórz konsolę programu PowerShell i Połącz konto tooyour.</span><span class="sxs-lookup"><span data-stu-id="57fc7-137">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="57fc7-138">Użyj następujących hello przykładowe toohelp, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="57fc7-138">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="57fc7-139">3. Utworzenie sieci TestVNet1</span><span class="sxs-lookup"><span data-stu-id="57fc7-139">3. Create TestVNet1</span></span>
<span data-ttu-id="57fc7-140">Witaj poniższy przykład tworzy sieć wirtualną o nazwie TestVNet1 i trzy podsieci, co GatewaySubnet o nazwie jedną o nazwie frontonu i jedną o nazwie wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="57fc7-140">hello following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="57fc7-141">Podczas zastępowania wartości ważne jest, aby podsieć bramy zawsze nosiła nazwę GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="57fc7-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="57fc7-142">W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="57fc7-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="57fc7-143">Krok 2 — Tworzenie hello bramy sieci VPN dla TestVNet1 z parametrami BGP</span><span class="sxs-lookup"><span data-stu-id="57fc7-143">Step 2 - Create hello VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-hello-ip-and-subnet-configurations"></a><span data-ttu-id="57fc7-144">1. Utwórz hello konfiguracje adresów IP i podsieci</span><span class="sxs-lookup"><span data-stu-id="57fc7-144">1. Create hello IP and subnet configurations</span></span>
<span data-ttu-id="57fc7-145">Żądaj publicznego adresu IP adres toobe toohello przydzielone bramy utworzone sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57fc7-145">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="57fc7-146">Zostanie również definiować hello wymagane podsieci i konfiguracje adresów IP.</span><span class="sxs-lookup"><span data-stu-id="57fc7-146">You'll also define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a><span data-ttu-id="57fc7-147">2. Utwórz bramę sieci VPN hello z hello jako liczba</span><span class="sxs-lookup"><span data-stu-id="57fc7-147">2. Create hello VPN gateway with hello AS number</span></span>
<span data-ttu-id="57fc7-148">Tworzenie bramy sieci wirtualnej powitania dla TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="57fc7-148">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="57fc7-149">Protokół BGP wymaga TestVNet1 opartej na trasach bramy sieci VPN, a także hello dodanie parametru - Asn, tooset hello numeru ASN (AS Number).</span><span class="sxs-lookup"><span data-stu-id="57fc7-149">BGP requires a Route-Based VPN gateway, and also hello addition parameter, -Asn, tooset hello ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="57fc7-150">Jeśli parametr ASN hello nie jest ustawiona, jest przypisany numer ASN 65515.</span><span class="sxs-lookup"><span data-stu-id="57fc7-150">If you do not set hello ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="57fc7-151">Tworzenie bramy może trochę potrwać (30 minut lub więcej toocomplete).</span><span class="sxs-lookup"><span data-stu-id="57fc7-151">Creating a gateway can take a while (30 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a><span data-ttu-id="57fc7-152">3. Uzyskaj adres IP elementu równorzędnego protokołu BGP Azure hello</span><span class="sxs-lookup"><span data-stu-id="57fc7-152">3. Obtain hello Azure BGP Peer IP address</span></span>
<span data-ttu-id="57fc7-153">Po utworzeniu bramy hello należy adresem IP elementu równorzędnego protokołu BGP hello tooobtain hello bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57fc7-153">Once hello gateway is created, you need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="57fc7-154">Ten adres jest wymagane tooconfigure hello bramy sieci VPN platformy Azure jako element równorzędny BGP dla lokalnego urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="57fc7-154">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="57fc7-155">ostatnie polecenie Hello przedstawia hello odpowiednich konfiguracji protokołu BGP na powitania bramy sieci VPN platformy Azure; na przykład:</span><span class="sxs-lookup"><span data-stu-id="57fc7-155">hello last command shows hello corresponding BGP configurations on hello Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="57fc7-156">Po utworzeniu bramy hello można używać tego połączenia między lokalizacjami tooestablish bramy albo wirtualnymi do połączenia z protokołem BGP.</span><span class="sxs-lookup"><span data-stu-id="57fc7-156">Once hello gateway is created, you can use this gateway tooestablish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="57fc7-157">Witaj sekcje przeprowadzenie hello kroki toocomplete hello wykonywania.</span><span class="sxs-lookup"><span data-stu-id="57fc7-157">hello following sections walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="57fc7-158"><a name ="crossprembbgp"></a>Część 2 - ustanowić połączenia między lokalizacjami z protokołem BGP</span><span class="sxs-lookup"><span data-stu-id="57fc7-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="57fc7-159">tooestablish połączenia między różnymi lokalizacjami, należy toocreate toorepresent bramy sieci lokalnej lokalnego urządzenia sieci VPN i połączeń tooconnect hello bramy sieci VPN z hello bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="57fc7-159">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="57fc7-160">Gdy istnieją artykuły, które pomagają tych kroków, ten artykuł zawiera parametry konfiguracji protokołu BGP hello wymagane toospecify hello dodatkowych właściwości.</span><span class="sxs-lookup"><span data-stu-id="57fc7-160">While there are articles that walk you through these steps, this article contains hello additional properties required toospecify hello BGP configuration parameters.</span></span>

![Protokół BGP dla między lokalizacjami](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="57fc7-162">Przed kontynuowaniem upewnij się, że zostały wykonane [część 1](#enablebgp) tego ćwiczenia.</span><span class="sxs-lookup"><span data-stu-id="57fc7-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="57fc7-163">Krok 1 — Tworzenie i konfigurowanie hello bramy sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="57fc7-163">Step 1 - Create and configure hello local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="57fc7-164">1. Zadeklarowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="57fc7-164">1. Declare your variables</span></span>

<span data-ttu-id="57fc7-165">Tego ćwiczenia jest nadal wyświetlany na diagramie hello konfiguracji hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="57fc7-165">This exercise continues toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="57fc7-166">Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="57fc7-166">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="57fc7-167">Kilka rzeczy toonote dotyczącymi parametrów bramy sieci lokalnej hello:</span><span class="sxs-lookup"><span data-stu-id="57fc7-167">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="57fc7-168">Witaj bramy sieci lokalnej może być w hello takie same lub innej lokalizacji i zasobów grupy jako hello bramy sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="57fc7-168">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="57fc7-169">Ten przykład przedstawia je w różnych grupach zasobów w różnych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="57fc7-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="57fc7-170">Prefiks minimalna Hello potrzebne toodeclare dla bramy sieci lokalnej hello jest adres hosta hello adresu IP elementu równorzędnego protokołu BGP na urządzeniu sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="57fc7-170">hello minimum prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="57fc7-171">W takim przypadku jest /32 prefiksu "10.52.255.254/32".</span><span class="sxs-lookup"><span data-stu-id="57fc7-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="57fc7-172">Przypomnienia należy użyć innego protokołu BGP numerów ASN między lokalnymi sieciami i sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57fc7-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="57fc7-173">Są one takie same hello, należy najpierw toochange ASN Twojej sieci wirtualnej Jeśli lokalnego urządzenia sieci VPN już używa hello numeru ASN toopeer z innych sąsiadów BGP.</span><span class="sxs-lookup"><span data-stu-id="57fc7-173">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

<span data-ttu-id="57fc7-174">Przed kontynuowaniem upewnij się, że są nadal połączonych tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="57fc7-174">Before you continue, make sure you are still connected tooSubscription 1.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="57fc7-175">2. Tworzenie bramy sieci lokalnej powitania dla Site5</span><span class="sxs-lookup"><span data-stu-id="57fc7-175">2. Create hello local network gateway for Site5</span></span>

<span data-ttu-id="57fc7-176">Należy się, że grupa zasobów hello toocreate, jeśli nie został utworzony, przed utworzeniem bramy sieci lokalnej hello.</span><span class="sxs-lookup"><span data-stu-id="57fc7-176">Be sure toocreate hello resource group if it is not created, before you create hello local network gateway.</span></span> <span data-ttu-id="57fc7-177">Zwróć uwagę, Witaj dwie dodatkowe parametry dla bramy sieci lokalnej hello: numer Asn i BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="57fc7-177">Notice hello two additional parameters for hello local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="57fc7-178">Krok 2 — Połącz hello bramy sieci wirtualnej i Brama sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="57fc7-178">Step 2 - Connect hello VNet gateway and local network gateway</span></span>

#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="57fc7-179">1. Pobierz Witaj dwie bramy</span><span class="sxs-lookup"><span data-stu-id="57fc7-179">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="57fc7-180">2. Utwórz połączenie tooSite5 TestVNet1 hello</span><span class="sxs-lookup"><span data-stu-id="57fc7-180">2. Create hello TestVNet1 tooSite5 connection</span></span>

<span data-ttu-id="57fc7-181">W tym kroku utworzysz hello połączenia z TestVNet1 tooSite5.</span><span class="sxs-lookup"><span data-stu-id="57fc7-181">In this step, you create hello connection from TestVNet1 tooSite5.</span></span> <span data-ttu-id="57fc7-182">Należy określić "-wartość $True" tooenable BGP dla tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="57fc7-182">You must specify "-EnableBGP $True" tooenable BGP for this connection.</span></span> <span data-ttu-id="57fc7-183">Jak już wspomniano, jest możliwe toohave połączeń zarówno protokołu BGP, jak i z systemem innym niż BGP dla hello tej samej bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57fc7-183">As discussed earlier, it is possible toohave both BGP and non-BGP connections for hello same Azure VPN Gateway.</span></span> <span data-ttu-id="57fc7-184">Jeśli protokół BGP jest włączony we właściwości połączenia hello, Azure nie włączyć protokół BGP dla tego połączenia nawet, jeśli parametry protokołu BGP jest już skonfigurowane na obu bram.</span><span class="sxs-lookup"><span data-stu-id="57fc7-184">Unless BGP is enabled in hello connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="57fc7-185">Witaj poniższy przykład wymieniono hello parametry wprowadzane do hello sekcji konfiguracji protokołu BGP na urządzeniu lokalnym sieci VPN w tym ćwiczeniu:</span><span class="sxs-lookup"><span data-stu-id="57fc7-185">hello following example lists hello parameters you enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="57fc7-186">Witaj połączenie jest nawiązywane po kilku minutach i uruchomieniu sesji komunikacji równorzędnej BGP hello, po nawiązaniu połączenia IPsec hello.</span><span class="sxs-lookup"><span data-stu-id="57fc7-186">hello connection is established after a few minutes, and hello BGP peering session starts once hello IPsec connection is established.</span></span>

## <span data-ttu-id="57fc7-187"><a name ="v2vbgp"></a>Część 3 — ustanowienie połączenia do wirtualnymi z protokołem BGP</span><span class="sxs-lookup"><span data-stu-id="57fc7-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="57fc7-188">W tej sekcji dodaje wirtualnymi do połączenia z protokołem BGP, jak pokazano w powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="57fc7-188">This section adds a VNet-to-VNet connection with BGP, as shown in hello following diagram:</span></span>

![Protokół BGP dla sieci wirtualnej do sieci wirtualnej](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="57fc7-190">Witaj, postępując zgodnie z instrukcjami nadal z poprzednich kroków hello.</span><span class="sxs-lookup"><span data-stu-id="57fc7-190">hello following instructions continue from hello previous steps.</span></span> <span data-ttu-id="57fc7-191">Należy wykonać [części I](#enablebgp) toocreate i skonfiguruj TestVNet1 oraz hello bramy sieci VPN z protokołem BGP.</span><span class="sxs-lookup"><span data-stu-id="57fc7-191">You must complete [Part I](#enablebgp) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="57fc7-192">Krok 1 — Tworzenie TestVNet2 i hello bramy sieci VPN</span><span class="sxs-lookup"><span data-stu-id="57fc7-192">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>

<span data-ttu-id="57fc7-193">Jest ważne toomake się, że przestrzeń adresów IP hello nowej sieci wirtualnej hello, TestVNet2, nakłada się ze wszystkimi zakresy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57fc7-193">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="57fc7-194">W tym przykładzie hello sieci wirtualnych należy toohello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="57fc7-194">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="57fc7-195">Można skonfigurować do wirtualnymi połączeń między różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="57fc7-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="57fc7-196">Aby uzyskać więcej informacji, zobacz [skonfigurować połączenia do wirtualnymi](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="57fc7-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="57fc7-197">Upewnij się, że możesz dodać hello "-wartość $True" podczas tworzenia hello tooenable połączeń protokołu BGP.</span><span class="sxs-lookup"><span data-stu-id="57fc7-197">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="57fc7-198">1. Zadeklarowanie zmiennych</span><span class="sxs-lookup"><span data-stu-id="57fc7-198">1. Declare your variables</span></span>

<span data-ttu-id="57fc7-199">Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="57fc7-199">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="57fc7-200">2. Utwórz TestVNet2 w hello nową grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="57fc7-200">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="57fc7-201">3. Tworzenie bramy sieci VPN powitania dla TestVNet2 z parametrami BGP</span><span class="sxs-lookup"><span data-stu-id="57fc7-201">3. Create hello VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="57fc7-202">Żądaj publicznego adresu IP adres toobe toohello przydzielone bramy utworzysz sieci wirtualnej i zdefiniuj hello wymagane podsieci i konfiguracje adresów IP.</span><span class="sxs-lookup"><span data-stu-id="57fc7-202">Request a public IP address toobe allocated toohello gateway you will create for your VNet and define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="57fc7-203">Utwórz bramę sieci VPN hello z hello jako numer.</span><span class="sxs-lookup"><span data-stu-id="57fc7-203">Create hello VPN gateway with hello AS number.</span></span> <span data-ttu-id="57fc7-204">Konieczne jest przesłonięcie hello domyślny numer ASN w Twojej bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57fc7-204">You must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="57fc7-205">Witaj numerów ASN dla hello połączone sieci wirtualne muszą być różne tooenable BGP i routing tranzytowy.</span><span class="sxs-lookup"><span data-stu-id="57fc7-205">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="57fc7-206">Krok 2 — Połącz hello TestVNet1 i TestVNet2 bram</span><span class="sxs-lookup"><span data-stu-id="57fc7-206">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="57fc7-207">W tym przykładzie zarówno bramy znajdują się w hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="57fc7-207">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="57fc7-208">Można wykonać ten krok w hello tej samej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57fc7-208">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="57fc7-209">1. Pobierz obu bram</span><span class="sxs-lookup"><span data-stu-id="57fc7-209">1. Get both gateways</span></span>

<span data-ttu-id="57fc7-210">Upewnij się, zaloguj się i połącz tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="57fc7-210">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="57fc7-211">2. Utwórz zarówno połączenia</span><span class="sxs-lookup"><span data-stu-id="57fc7-211">2. Create both connections</span></span>

<span data-ttu-id="57fc7-212">W tym kroku utworzysz hello połączenia z TestVNet1 tooTestVNet2 i hello połączenia z TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="57fc7-212">In this step, you create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="57fc7-213">Należy się tooenable BGP dla obu połączeń.</span><span class="sxs-lookup"><span data-stu-id="57fc7-213">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="57fc7-214">Po wykonaniu tych czynności hello połączenie jest nawiązywane po kilku minutach.</span><span class="sxs-lookup"><span data-stu-id="57fc7-214">After completing these steps, hello connection is established after a few minutes.</span></span> <span data-ttu-id="57fc7-215">Sesja komunikacji równorzędnej BGP Hello działa po zakończeniu hello połączenia do wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="57fc7-215">hello BGP peering session is up once hello VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="57fc7-216">Jeśli ukończono wszystkie trzy elementy w tym ćwiczeniu zostało ustanowione powitania od topologii sieci:</span><span class="sxs-lookup"><span data-stu-id="57fc7-216">If you completed all three parts of this exercise, you have established hello following network topology:</span></span>

![Protokół BGP dla sieci wirtualnej do sieci wirtualnej](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="57fc7-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="57fc7-218">Next steps</span></span>

<span data-ttu-id="57fc7-219">Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="57fc7-219">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="57fc7-220">Kroki opisano w sekcji [Tworzenie maszyny wirtualnej](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="57fc7-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
