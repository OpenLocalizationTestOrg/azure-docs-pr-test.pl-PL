---
title: "Połączenie sieci wirtualnej platformy Azure tooanother sieci wirtualnej: programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono procedurę łączenia sieci wirtualnych przy użyciu usługi Azure Resource Manager i programu PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="321e9-103">Konfigurowanie połączenia bramy sieci VPN między sieciami wirtualnymi przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="321e9-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="321e9-104">W tym artykule opisano sposób toocreate połączenie bramy sieci VPN między sieciami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="321e9-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="321e9-105">Witaj sieci wirtualne mogą być w hello tych samych lub różnych regionów, a z hello takie same lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="321e9-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="321e9-106">Podczas łączenia sieci wirtualne z różnych subskrypcji, subskrypcje hello nie ma potrzeby toobe skojarzone z hello tej samej dzierżawy usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="321e9-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="321e9-107">Witaj opisanych w tym artykule mają zastosowanie modelu wdrażania usługi Resource Manager toohello i przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="321e9-107">hello steps in this article apply toohello Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="321e9-108">Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="321e9-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="321e9-109">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="321e9-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="321e9-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="321e9-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="321e9-111">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="321e9-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="321e9-112">Portal Azure (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="321e9-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="321e9-113">Łączenie różnych modeli wdrażania — witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="321e9-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="321e9-114">Łączenie różnych modeli wdrażania — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="321e9-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="321e9-115">Połączenie wirtualnej sieci tooanother sieć wirtualną (VNet-VNet) jest podobne tooconnecting lokalizacji sieci wirtualnej tooan lokalnej lokacji.</span><span class="sxs-lookup"><span data-stu-id="321e9-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="321e9-116">Oba typy łączności Użyj tooprovide bramy sieci VPN przy użyciu protokołu IPsec/IKE bezpiecznego tunelu.</span><span class="sxs-lookup"><span data-stu-id="321e9-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="321e9-117">Jeśli Twoje sieci wirtualne są w hello tego samego regionu, może być tooconsider łącząc je przy użyciu sieci wirtualnej komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="321e9-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="321e9-118">W przypadku komunikacji równorzędnej sieci wirtualnych nie jest używana brama sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="321e9-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="321e9-119">Aby uzyskać więcej informacji, zobacz temat [Komunikacja równorzędna sieci wirtualnych](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="321e9-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="321e9-120">Komunikację między sieciami wirtualnymi można łączyć z konfiguracjami obejmującymi wiele lokacji.</span><span class="sxs-lookup"><span data-stu-id="321e9-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="321e9-121">Dzięki temu można ustanowić topologii sieci, łączące łączności między lokalizacjami z połączeniem sieciowym między wirtualnych, jak pokazano w powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="321e9-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Informacje o połączeniach](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="321e9-123">Dlaczego łączy się sieci wirtualne?</span><span class="sxs-lookup"><span data-stu-id="321e9-123">Why connect virtual networks?</span></span>

<span data-ttu-id="321e9-124">Warto sieci wirtualnych tooconnect hello z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="321e9-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="321e9-125">**Niezależna od regionu nadmiarowość i obecność geograficzna**</span><span class="sxs-lookup"><span data-stu-id="321e9-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="321e9-126">Można tworzyć własne replikacje geograficzne lub przeprowadzać synchronizację z bezpiecznym połączeniem bez przechodzenia przez punkty końcowe dostępne z Internetu.</span><span class="sxs-lookup"><span data-stu-id="321e9-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="321e9-127">Usługi Azure Traffic Manager i Load Balancer pozwalają skonfigurować obciążenie o wysokiej dostępności z nadmiarowością geograficzną w wielu regionach świadczenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="321e9-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="321e9-128">Przykładem ważne jest tooset się SQL zawsze włączone grupy dostępności rozsyłanie się w różnych regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="321e9-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="321e9-129">**Regionalne aplikacje wielowarstwowe z izolacją lub granicami administracyjnymi**</span><span class="sxs-lookup"><span data-stu-id="321e9-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="321e9-130">Poziomu hello sam region, możesz skonfigurować aplikacje wielowarstwowe z wieloma sieciami wirtualnymi, połączonych ze sobą tooisolation lub wymagań administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="321e9-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="321e9-131">Aby uzyskać więcej informacji o połączeniach sieci wirtualnej do sieci wirtualnej, zobacz hello [wirtualnymi — często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="321e9-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="321e9-132">Która instrukcje mają zastosowanie w moim przypadku?</span><span class="sxs-lookup"><span data-stu-id="321e9-132">Which set of steps should I use?</span></span>

<span data-ttu-id="321e9-133">W tym artykule przedstawiono dwa różne zestawy kroków.</span><span class="sxs-lookup"><span data-stu-id="321e9-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="321e9-134">Jeden zestaw kroków [sieci wirtualnych, które znajdują się w hello tej samej subskrypcji](#samesub)i drugi dla [sieci wirtualnych, które znajdują się w różnych subskrypcji](#difsub).</span><span class="sxs-lookup"><span data-stu-id="321e9-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="321e9-135">Witaj Najważniejsza różnica między zestawami hello jest Określa, czy można tworzyć i konfigurować wszystkie wirtualne zasoby sieciowe i bramy w hello tej samej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="321e9-135">hello key difference between hello sets is whether you can create and configure all virtual network and gateway resources within hello same PowerShell session.</span></span>

<span data-ttu-id="321e9-136">Hello kroki opisane w tym artykule używać zmiennych zadeklarowanych na początku hello każdej sekcji.</span><span class="sxs-lookup"><span data-stu-id="321e9-136">hello steps in this article use variables that are declared at hello beginning of each section.</span></span> <span data-ttu-id="321e9-137">Jeśli już korzystasz z istniejących sieciach wirtualnych, należy zmodyfikować hello zmienne tooreflect hello ustawienia we własnym środowisku.</span><span class="sxs-lookup"><span data-stu-id="321e9-137">If you already are working with existing VNets, modify hello variables tooreflect hello settings in your own environment.</span></span> <span data-ttu-id="321e9-138">Jeśli chcesz, aby w sieciach wirtualnych działało rozpoznawanie nazw, zobacz artykuł o [rozpoznawaniu nazw](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="321e9-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="321e9-139"><a name="samesub"></a>Jak tooconnect sieci wirtualnych należących hello tej samej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="321e9-139"><a name="samesub"></a>How tooconnect VNets that are in hello same subscription</span></span>

![Diagram połączenia między sieciami wirtualnymi (v2v)](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="321e9-141">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="321e9-141">Before you begin</span></span>

<span data-ttu-id="321e9-142">Przed rozpoczęciem, należy tooinstall hello najnowszej wersji hello Azure Resource Manager poleceń cmdlet programu PowerShell, co najmniej 4.0 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="321e9-142">Before beginning, you need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="321e9-143">Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="321e9-143">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="321e9-144"><a name="Step1"></a>Krok 1 — Planowanie zakresów adresów IP</span><span class="sxs-lookup"><span data-stu-id="321e9-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="321e9-145">Hello następujące kroki utworzymy dwie sieci wirtualne wraz z ich bramy odpowiednich podsieci i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="321e9-145">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="321e9-146">Następnie utworzymy połączenie sieci VPN między Witaj dwie sieci wirtualne.</span><span class="sxs-lookup"><span data-stu-id="321e9-146">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="321e9-147">Jest ważne tooplan zakresów adresów IP powitania dla konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="321e9-147">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="321e9-148">Niezbędne jest upewnienie się, że zakresy sieci wirtualnej ani sieci lokalnej nie zachodzą na siebie w jakikolwiek sposób.</span><span class="sxs-lookup"><span data-stu-id="321e9-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="321e9-149">W tych przykładach nie uwzględniamy serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="321e9-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="321e9-150">Jeśli chcesz, aby w sieciach wirtualnych działało rozpoznawanie nazw, zobacz artykuł o [rozpoznawaniu nazw](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="321e9-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="321e9-151">Używamy hello następujące wartości w przykładach hello:</span><span class="sxs-lookup"><span data-stu-id="321e9-151">We use hello following values in hello examples:</span></span>

<span data-ttu-id="321e9-152">**Wartości dla sieci TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="321e9-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="321e9-153">Nazwa sieci wirtualnej: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="321e9-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="321e9-154">Grupa zasobów: TestRG1</span><span class="sxs-lookup"><span data-stu-id="321e9-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="321e9-155">Lokalizacja: Wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="321e9-155">Location: East US</span></span>
* <span data-ttu-id="321e9-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="321e9-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="321e9-157">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="321e9-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="321e9-158">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="321e9-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="321e9-159">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="321e9-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="321e9-160">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="321e9-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="321e9-161">Publiczny adres IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="321e9-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="321e9-162">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="321e9-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="321e9-163">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="321e9-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="321e9-164">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="321e9-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="321e9-165">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="321e9-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="321e9-166">**Wartości dla sieci TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="321e9-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="321e9-167">Nazwa sieci wirtualnej: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="321e9-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="321e9-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="321e9-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="321e9-169">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="321e9-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="321e9-170">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="321e9-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="321e9-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="321e9-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="321e9-172">Grupa zasobów: TestRG4</span><span class="sxs-lookup"><span data-stu-id="321e9-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="321e9-173">Lokalizacja: West US</span><span class="sxs-lookup"><span data-stu-id="321e9-173">Location: West US</span></span>
* <span data-ttu-id="321e9-174">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="321e9-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="321e9-175">Publiczny adres IP: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="321e9-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="321e9-176">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="321e9-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="321e9-177">Połączenie: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="321e9-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="321e9-178">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="321e9-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="321e9-179"><a name="Step2"></a>Krok 2 — Tworzenie i konfigurowanie sieci TestVNet1</span><span class="sxs-lookup"><span data-stu-id="321e9-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="321e9-180">Zadeklaruj swoje zmienne.</span><span class="sxs-lookup"><span data-stu-id="321e9-180">Declare your variables.</span></span> <span data-ttu-id="321e9-181">W tym przykładzie deklaruje zmienne hello używania hello wartości w tym ćwiczeniu.</span><span class="sxs-lookup"><span data-stu-id="321e9-181">This example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="321e9-182">W większości przypadków należy zastąpić własnymi hello wartości.</span><span class="sxs-lookup"><span data-stu-id="321e9-182">In most cases, you should replace hello values with your own.</span></span> <span data-ttu-id="321e9-183">Jednak można używać tych zmiennych, jeśli używasz za pośrednictwem toobecome kroki hello zapoznać się z tym typem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="321e9-183">However, you can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="321e9-184">Modyfikuj zmienne hello w razie potrzeby, a następnie skopiuj i wklej je w konsoli programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="321e9-184">Modify hello variables if needed, then copy and paste them into your PowerShell console.</span></span>

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
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
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. <span data-ttu-id="321e9-185">Połącz tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="321e9-185">Connect tooyour account.</span></span> <span data-ttu-id="321e9-186">Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="321e9-186">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="321e9-187">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="321e9-187">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="321e9-188">Określ, które mają toouse subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="321e9-188">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="321e9-189">Utwórz nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="321e9-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="321e9-190">Utwórz hello konfiguracje podsieci dla TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="321e9-190">Create hello subnet configurations for TestVNet1.</span></span> <span data-ttu-id="321e9-191">Poniższy przykład pozwala utworzyć sieć wirtualną o nazwie TestVNet1 oraz trzy podsieci noszące kolejno nazwy GatewaySubnet, FrontEnd i Backend.</span><span class="sxs-lookup"><span data-stu-id="321e9-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="321e9-192">Podczas zastępowania wartości ważne jest, aby podsieć bramy zawsze nosiła nazwę GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="321e9-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="321e9-193">W przypadku nadania jej innej nazwy proces tworzenia bramy zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="321e9-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="321e9-194">Witaj poniższym przykładzie użyto hello zmienne, które należy wcześniej.</span><span class="sxs-lookup"><span data-stu-id="321e9-194">hello following example uses hello variables that you set earlier.</span></span> <span data-ttu-id="321e9-195">W tym przykładzie podsieć bramy hello używa /27.</span><span class="sxs-lookup"><span data-stu-id="321e9-195">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="321e9-196">Mimo że jest możliwe toocreate jak /29 podsieć bramy, zaleca się utworzenie większej podsieć, która zawiera więcej adresów, wybierając co najmniej /28 lub /27.</span><span class="sxs-lookup"><span data-stu-id="321e9-196">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="321e9-197">Umożliwi to za mało adresów tooaccommodate możliwe dodatkowe konfiguracje, które można w hello przyszłych.</span><span class="sxs-lookup"><span data-stu-id="321e9-197">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="321e9-198">Utwórz sieć TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="321e9-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="321e9-199">Żądaj publicznego adresu IP adres toobe toohello przydzielone bramy utworzone sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="321e9-199">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="321e9-200">Należy zauważyć, że hello AllocationMethod jest dynamiczny.</span><span class="sxs-lookup"><span data-stu-id="321e9-200">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="321e9-201">Nie można określić hello adresu IP, które mają toouse.</span><span class="sxs-lookup"><span data-stu-id="321e9-201">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="321e9-202">Jest dynamicznie przydzielonego tooyour bramy.</span><span class="sxs-lookup"><span data-stu-id="321e9-202">It's dynamically allocated tooyour gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="321e9-203">Utwórz hello konfigurację bramy.</span><span class="sxs-lookup"><span data-stu-id="321e9-203">Create hello gateway configuration.</span></span> <span data-ttu-id="321e9-204">Konfiguracja bramy Hello definiuje podsieć hello oraz hello toouse w publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="321e9-204">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="321e9-205">Użyj toocreate przykład hello konfigurację bramy.</span><span class="sxs-lookup"><span data-stu-id="321e9-205">Use hello example toocreate your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="321e9-206">Utwórz bramę powitania dla TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="321e9-206">Create hello gateway for TestVNet1.</span></span> <span data-ttu-id="321e9-207">W tym kroku utworzysz hello bramy sieci wirtualnej dla programu TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="321e9-207">In this step, you create hello virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="321e9-208">Konfiguracje połączeń między sieciami wirtualnymi wymagają zastosowania wartości RouteBased obiektu VpnType.</span><span class="sxs-lookup"><span data-stu-id="321e9-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="321e9-209">Tworzenie bramy może potrwać często 45 minut lub dłużej, w zależności od hello bramy wybranej jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="321e9-209">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="321e9-210">Krok 3 — Tworzenie i konfigurowanie sieci TestVNet4</span><span class="sxs-lookup"><span data-stu-id="321e9-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="321e9-211">Po skonfigurowaniu sieci TestVNet1 utwórz sieć TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="321e9-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="321e9-212">Wykonaj kroki hello poniżej, zastępując wartości hello własne w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="321e9-212">Follow hello steps below, replacing hello values with your own when needed.</span></span> <span data-ttu-id="321e9-213">Ten krok może odbywać się w obrębie hello sama sesja programu PowerShell, ponieważ jest on hello sam subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="321e9-213">This step can be done within hello same PowerShell session because it is in hello same subscription.</span></span>

1. <span data-ttu-id="321e9-214">Zadeklaruj swoje zmienne.</span><span class="sxs-lookup"><span data-stu-id="321e9-214">Declare your variables.</span></span> <span data-ttu-id="321e9-215">Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="321e9-215">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. <span data-ttu-id="321e9-216">Utwórz nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="321e9-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="321e9-217">Utwórz hello konfiguracje podsieci dla TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="321e9-217">Create hello subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="321e9-218">Utwórz sieć TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="321e9-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="321e9-219">Prześlij żądanie dotyczące publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="321e9-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="321e9-220">Utwórz hello konfigurację bramy.</span><span class="sxs-lookup"><span data-stu-id="321e9-220">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="321e9-221">Utwórz bramę TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="321e9-221">Create hello TestVNet4 gateway.</span></span> <span data-ttu-id="321e9-222">Tworzenie bramy może potrwać często 45 minut lub dłużej, w zależności od hello bramy wybranej jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="321e9-222">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a><span data-ttu-id="321e9-223">Krok 4 — Utwórz hello połączenia</span><span class="sxs-lookup"><span data-stu-id="321e9-223">Step 4 - Create hello connections</span></span>

1. <span data-ttu-id="321e9-224">Użyj obu bram sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="321e9-224">Get both virtual network gateways.</span></span> <span data-ttu-id="321e9-225">Jeśli oba hello bramy znajdują się w hello tej samej subskrypcji, ponieważ są one przykład Witaj, można wykonać ten krok w hello tej samej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="321e9-225">If both of hello gateways are in hello same subscription, as they are in hello example, you can complete this step in hello same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="321e9-226">Utwórz połączenie tooTestVNet4 TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="321e9-226">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="321e9-227">W tym kroku utworzysz hello połączenia z TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="321e9-227">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="321e9-228">Zobaczysz przywoływany w przykładach hello klucza wspólnego.</span><span class="sxs-lookup"><span data-stu-id="321e9-228">You'll see a shared key referenced in hello examples.</span></span> <span data-ttu-id="321e9-229">Możesz użyć własnych wartości dla klucza udostępnionego hello.</span><span class="sxs-lookup"><span data-stu-id="321e9-229">You can use your own values for hello shared key.</span></span> <span data-ttu-id="321e9-230">ważne, czy element jest klucz udostępniony hello Hello muszą być zgodne, dla obu połączeń.</span><span class="sxs-lookup"><span data-stu-id="321e9-230">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="321e9-231">Tworzenie połączenia może zająć chwilę podczas toocomplete.</span><span class="sxs-lookup"><span data-stu-id="321e9-231">Creating a connection can take a short while toocomplete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="321e9-232">Utwórz połączenie tooTestVNet1 TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="321e9-232">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="321e9-233">Ten krok jest podobne toohello, jeden powyżej, z wyjątkiem połączeń hello jest tworzony z TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="321e9-233">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="321e9-234">Upewnij się, że klucze hello udostępnionych pasują do siebie.</span><span class="sxs-lookup"><span data-stu-id="321e9-234">Make sure hello shared keys match.</span></span> <span data-ttu-id="321e9-235">zostanie nawiązane połączenie powitania po kilku minutach.</span><span class="sxs-lookup"><span data-stu-id="321e9-235">hello connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="321e9-236">Weryfikowanie połączenia.</span><span class="sxs-lookup"><span data-stu-id="321e9-236">Verify your connection.</span></span> <span data-ttu-id="321e9-237">Zobacz sekcję hello [jak tooverify połączenia](#verify).</span><span class="sxs-lookup"><span data-stu-id="321e9-237">See hello section [How tooverify your connection](#verify).</span></span>

## <span data-ttu-id="321e9-238"><a name="difsub"></a>Jak tooconnect sieci wirtualne będące w ramach różnych subskrypcji</span><span class="sxs-lookup"><span data-stu-id="321e9-238"><a name="difsub"></a>How tooconnect VNets that are in different subscriptions</span></span>

![Diagram połączenia między sieciami wirtualnymi (v2v)](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="321e9-240">W tym scenariuszu nawiązywane jest połączenie między sieciami wirtualnymi TestVNet1 i TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="321e9-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="321e9-241">Sieci TestVNet1 i TestVNet5 znajdują się w innych subskrypcjach.</span><span class="sxs-lookup"><span data-stu-id="321e9-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="321e9-242">Subskrypcje Hello nie są skojarzone z hello toobe tej samej dzierżawy usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="321e9-242">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="321e9-243">Witaj różnica między te czynności i poprzedniego zestawu hello jest, niektóre kroki konfiguracji hello potrzeby toobe wykonywane w osobnej sesji programu PowerShell w kontekście hello hello drugi subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="321e9-243">hello difference between these steps and hello previous set is that some of hello configuration steps need toobe performed in a separate PowerShell session in hello context of hello second subscription.</span></span> <span data-ttu-id="321e9-244">Szczególnie gdy hello dwa subskrypcji należy toodifferent organizacji.</span><span class="sxs-lookup"><span data-stu-id="321e9-244">Especially when hello two subscriptions belong toodifferent organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="321e9-245">Krok 5 — Tworzenie i konfigurowanie sieci TestVNet1</span><span class="sxs-lookup"><span data-stu-id="321e9-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="321e9-246">Należy wykonać [krok 1](#Step1) i [krok 2](#Step2) z hello poprzedniej sekcji toocreate i skonfiguruj TestVNet1 oraz hello bramy sieci VPN dla TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="321e9-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from hello previous section toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="321e9-247">W przypadku tej konfiguracji nie jest wymagane toocreate TestVNet4 z poprzedniej sekcji hello, mimo że, jeśli tworzysz, nie będzie ona konflikt z tych kroków.</span><span class="sxs-lookup"><span data-stu-id="321e9-247">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="321e9-248">Po wykonaniu kroku 1 i 2 Kontynuuj krok 6 toocreate TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="321e9-248">Once you complete Step 1 and Step 2, continue with Step 6 toocreate TestVNet5.</span></span> 

### <a name="step-6---verify-hello-ip-address-ranges"></a><span data-ttu-id="321e9-249">Krok 6 - Sprawdź, czy zakresy adresów IP hello</span><span class="sxs-lookup"><span data-stu-id="321e9-249">Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="321e9-250">Jest ważne toomake się, że przestrzeń adresów IP hello nowej sieci wirtualnej hello, TestVNet5, nakłada się ze wszystkimi zakresy sieci wirtualnej lub zakresy bramy sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="321e9-250">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="321e9-251">W tym przykładzie hello sieci wirtualne mogą należeć toodifferent organizacji.</span><span class="sxs-lookup"><span data-stu-id="321e9-251">In this example, hello virtual networks may belong toodifferent organizations.</span></span> <span data-ttu-id="321e9-252">W tym ćwiczeniu program hello następujące wartości hello TestVNet5:</span><span class="sxs-lookup"><span data-stu-id="321e9-252">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="321e9-253">**Wartości dla sieci TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="321e9-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="321e9-254">Nazwa sieci wirtualnej: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="321e9-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="321e9-255">Grupa zasobów: TestRG5</span><span class="sxs-lookup"><span data-stu-id="321e9-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="321e9-256">Lokalizacja: Japan East</span><span class="sxs-lookup"><span data-stu-id="321e9-256">Location: Japan East</span></span>
* <span data-ttu-id="321e9-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="321e9-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="321e9-258">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="321e9-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="321e9-259">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="321e9-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="321e9-260">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="321e9-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="321e9-261">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="321e9-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="321e9-262">Publiczny adres IP: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="321e9-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="321e9-263">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="321e9-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="321e9-264">Połączenie: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="321e9-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="321e9-265">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="321e9-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="321e9-266">Krok 7 — Tworzenie i konfigurowanie sieci TestVNet5</span><span class="sxs-lookup"><span data-stu-id="321e9-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="321e9-267">Ten krok należy wykonać w kontekście hello hello nową subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="321e9-267">This step must be done in hello context of hello new subscription.</span></span> <span data-ttu-id="321e9-268">Ta część może zostać wykonana przez administratora hello w innej organizacji, który jest właścicielem hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="321e9-268">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span>

1. <span data-ttu-id="321e9-269">Zadeklaruj swoje zmienne.</span><span class="sxs-lookup"><span data-stu-id="321e9-269">Declare your variables.</span></span> <span data-ttu-id="321e9-270">Należy się tooreplace hello wartościami hello te mają toouse dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="321e9-270">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. <span data-ttu-id="321e9-271">Połącz toosubscription 5.</span><span class="sxs-lookup"><span data-stu-id="321e9-271">Connect toosubscription 5.</span></span> <span data-ttu-id="321e9-272">Otwórz konsolę programu PowerShell i Połącz konto tooyour.</span><span class="sxs-lookup"><span data-stu-id="321e9-272">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="321e9-273">Użyj następujących hello przykładowe toohelp, gdy nawiązujesz połączenie:</span><span class="sxs-lookup"><span data-stu-id="321e9-273">Use hello following sample toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="321e9-274">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="321e9-274">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="321e9-275">Określ, które mają toouse subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="321e9-275">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="321e9-276">Utwórz nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="321e9-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="321e9-277">Utwórz hello konfiguracje podsieci dla TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="321e9-277">Create hello subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="321e9-278">Utwórz sieć wirtualną TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="321e9-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="321e9-279">Prześlij żądanie dotyczące publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="321e9-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="321e9-280">Utwórz hello konfigurację bramy.</span><span class="sxs-lookup"><span data-stu-id="321e9-280">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="321e9-281">Utwórz bramę TestVNet5 hello.</span><span class="sxs-lookup"><span data-stu-id="321e9-281">Create hello TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a><span data-ttu-id="321e9-282">Krok 8 — Utwórz hello połączenia</span><span class="sxs-lookup"><span data-stu-id="321e9-282">Step 8 - Create hello connections</span></span>

<span data-ttu-id="321e9-283">W tym przykładzie hello bramy znajdują się w różnych subskrypcji hello, możemy zostały podzielone w tym kroku dwóch sesji programu PowerShell oznaczony jako [subskrypcji 1] i [subskrypcji 5].</span><span class="sxs-lookup"><span data-stu-id="321e9-283">In this example, because hello gateways are in hello different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="321e9-284">**[Subskrypcji 1]**  Bramy sieci wirtualnej hello get dla 1 subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="321e9-284">**[Subscription 1]** Get hello virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="321e9-285">Zaloguj się i połącz tooSubscription 1 przed uruchomieniem hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="321e9-285">Log in and connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="321e9-286">Skopiuj dane wyjściowe hello hello następujące elementy i wysłać te administratora toohello 5 subskrypcji za pośrednictwem poczty e-mail lub innej metody.</span><span class="sxs-lookup"><span data-stu-id="321e9-286">Copy hello output of hello following elements and send these toohello administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="321e9-287">Te dwa elementy mają wartości toohello podobne następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="321e9-287">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="321e9-288">**[Subskrypcji 5]**  Bramy sieci wirtualnej hello get 5 subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="321e9-288">**[Subscription 5]** Get hello virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="321e9-289">Zaloguj się i połącz tooSubscription 5 przed uruchomieniem hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="321e9-289">Log in and connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="321e9-290">Skopiuj dane wyjściowe hello hello następujące elementy i wysłać te administratora toohello 1 subskrypcji za pośrednictwem poczty e-mail lub innej metody.</span><span class="sxs-lookup"><span data-stu-id="321e9-290">Copy hello output of hello following elements and send these toohello administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="321e9-291">Te dwa elementy mają wartości toohello podobne następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="321e9-291">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="321e9-292">**[Subskrypcji 1]**  Utworzyć hello TestVNet1 tooTestVNet5 połączenia.</span><span class="sxs-lookup"><span data-stu-id="321e9-292">**[Subscription 1]** Create hello TestVNet1 tooTestVNet5 connection.</span></span> <span data-ttu-id="321e9-293">W tym kroku utworzysz hello połączenia z TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="321e9-293">In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="321e9-294">Witaj różnica polega na tym, że vnet5gw $ nie można uzyskać bezpośrednio, ponieważ znajduje się w innej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="321e9-294">hello difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="321e9-295">Należy toocreate nowy obiekt programu PowerShell z wartościami hello przekazywane z zakresu od 1 do subskrypcji w powyższych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="321e9-295">You will need toocreate a new PowerShell object with hello values communicated from Subscription 1 in hello steps above.</span></span> <span data-ttu-id="321e9-296">Przykład Witaj Użyj poniżej.</span><span class="sxs-lookup"><span data-stu-id="321e9-296">Use hello example below.</span></span> <span data-ttu-id="321e9-297">Zamień na powitania nazwa, identyfikator i klucz udostępniony własne wartości.</span><span class="sxs-lookup"><span data-stu-id="321e9-297">Replace hello Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="321e9-298">ważne, czy element jest klucz udostępniony hello Hello muszą być zgodne, dla obu połączeń.</span><span class="sxs-lookup"><span data-stu-id="321e9-298">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="321e9-299">Tworzenie połączenia może zająć chwilę podczas toocomplete.</span><span class="sxs-lookup"><span data-stu-id="321e9-299">Creating a connection can take a short while toocomplete.</span></span>

  <span data-ttu-id="321e9-300">Połącz tooSubscription 1 przed uruchomieniem hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="321e9-300">Connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="321e9-301">**[Subskrypcji 5]**  Utworzyć hello TestVNet5 tooTestVNet1 połączenia.</span><span class="sxs-lookup"><span data-stu-id="321e9-301">**[Subscription 5]** Create hello TestVNet5 tooTestVNet1 connection.</span></span> <span data-ttu-id="321e9-302">Ten krok jest podobne toohello, jeden powyżej, z wyjątkiem połączeń hello jest tworzony z TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="321e9-302">This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="321e9-303">Witaj, sam proces tworzenia obiekt programu PowerShell, na podstawie wartości hello uzyskane z 1 subskrypcji w tym miejscu dotyczy również.</span><span class="sxs-lookup"><span data-stu-id="321e9-303">hello same process of creating a PowerShell object based on hello values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="321e9-304">W tym kroku upewnij się, że hello udostępnionych klucze pasują do siebie.</span><span class="sxs-lookup"><span data-stu-id="321e9-304">In this step, be sure that hello shared keys match.</span></span>

  <span data-ttu-id="321e9-305">Połącz tooSubscription 5 przed uruchomieniem hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="321e9-305">Connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="321e9-306"><a name="verify"></a>Jak tooverify połączenia</span><span class="sxs-lookup"><span data-stu-id="321e9-306"><a name="verify"></a>How tooverify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="321e9-307"><a name="faq"></a>Często zadawane pytania dotyczące połączeń między sieciami wirtualnymi</span><span class="sxs-lookup"><span data-stu-id="321e9-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="321e9-308">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="321e9-308">Next steps</span></span>

* <span data-ttu-id="321e9-309">Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="321e9-309">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="321e9-310">Zobacz hello [dokumentacji maszyn wirtualnych](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="321e9-310">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="321e9-311">Uzyskać informacji na temat protokołu BGP, zobacz hello [Omówienie protokołu BGP](vpn-gateway-bgp-overview.md) i [jak tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="321e9-311">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
