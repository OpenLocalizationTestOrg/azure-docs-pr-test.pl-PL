---
title: "Konfigurowanie połączeń usługi ExpressRoute i sieci VPN typu lokacja-lokacja, które mogą współistnieć: wersja klasyczna: Azure | Microsoft Docs"
description: "W tym artykule przedstawiono konfigurowanie ExpressRoute, jak i połączenie sieci VPN typu lokacja-lokacja, które mogą współistnieć na powitania klasycznego modelu wdrażania."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="76512-103">Konfigurowanie współistniejących połączeń usługi ExpressRoute i połączeń typu lokacja-lokacja (wersja klasyczna)</span><span class="sxs-lookup"><span data-stu-id="76512-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="76512-104">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="76512-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="76512-105">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="76512-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="76512-106">Witaj możliwości tooconfigure sieci VPN typu lokacja-lokacja i ExpressRoute ma kilka zalet.</span><span class="sxs-lookup"><span data-stu-id="76512-106">Having hello ability tooconfigure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="76512-107">Konfigurowanie sieci VPN typu lokacja-lokacja jako ścieżka bezpiecznego trybu failover dla ExressRoute lub użyj toosites tooconnect sieci VPN typu lokacja-lokacja, które nie są połączone za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="76512-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="76512-108">Omówimy tooconfigure kroki hello oba scenariusze, w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="76512-108">We will cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="76512-109">Ten artykuł dotyczy toohello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="76512-109">This article applies toohello classic deployment model.</span></span> <span data-ttu-id="76512-110">Ta konfiguracja nie jest dostępna w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="76512-110">This configuration is not available in hello portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="76512-111">**Modele wdrażania Azure — informacje**</span><span class="sxs-lookup"><span data-stu-id="76512-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="76512-112">Obwody usługi ExpressRoute musi być wstępnie skonfigurowany przed wykonaniem instrukcji hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="76512-112">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="76512-113">Upewnij się, że zbyt po przewodnikach hello[utworzyć obwodu usługi ExpressRoute](expressroute-howto-circuit-classic.md) i [Konfigurowanie routingu](expressroute-howto-routing-classic.md) przed wykonaniem kroków hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="76512-113">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow hello steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="76512-114">Limity i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="76512-114">Limits and limitations</span></span>
* <span data-ttu-id="76512-115">**Routing tranzytowy nie jest obsługiwany.**</span><span class="sxs-lookup"><span data-stu-id="76512-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="76512-116">Nie można skierować połączenia (przez platformę Azure) między lokalną siecią połączoną za pośrednictwem sieci VPN typu lokacja-lokacja i lokalną siecią połączoną za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="76512-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="76512-117">**Połączenia typu punkt-lokacja nie są obsługiwane.**</span><span class="sxs-lookup"><span data-stu-id="76512-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="76512-118">Nie można włączyć toohello połączenia VPN punkt lokacja tej samej sieci wirtualnej, który jest połączony tooExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="76512-118">You can't enable point-to-site VPN connections toohello same VNet that is connected tooExpressRoute.</span></span> <span data-ttu-id="76512-119">Punkt lokacja sieci VPN i ExpressRoute nie mogą współistnieć na powitania sam sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="76512-119">Point-to-site VPN and ExpressRoute cannot coexist for hello same VNet.</span></span>
* <span data-ttu-id="76512-120">**Wymuszanie tunelowania nie można włączyć na powitania Brama VPN lokacja-lokacja.**</span><span class="sxs-lookup"><span data-stu-id="76512-120">**Forced tunneling cannot be enabled on hello Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="76512-121">Możesz tylko "wymusić" wszystkie powiązane z Internetu ruchu wstecz tooyour sieci lokalnej za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="76512-121">You can only "force" all Internet-bound traffic back tooyour on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="76512-122">**Podstawowa brama jednostki SKU nie jest obsługiwana.**</span><span class="sxs-lookup"><span data-stu-id="76512-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="76512-123">Należy użyć bramy z systemem innym niż — podstawowy SKU dla obu hello [bramę usługi ExpressRoute](expressroute-about-virtual-network-gateways.md) i hello [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="76512-123">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="76512-124">**Obsługiwana jest tylko brama sieci VPN oparta na trasach.**</span><span class="sxs-lookup"><span data-stu-id="76512-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="76512-125">Należy użyć [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) opartej na trasach.</span><span class="sxs-lookup"><span data-stu-id="76512-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="76512-126">**Dla bramy sieci VPN należy skonfigurować trasę statyczną.**</span><span class="sxs-lookup"><span data-stu-id="76512-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="76512-127">Jeśli sieci lokalnej jest tooboth połączenia ExpressRoute, a Site-to-Site VPN, musi mieć tras statycznych skonfigurowana w Twojej sieci lokalnej tooroute hello Site-to-Site VPN połączenia toohello publicznej sieci Internet.</span><span class="sxs-lookup"><span data-stu-id="76512-127">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="76512-128">**Najpierw należy skonfigurować bramę usługi ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="76512-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="76512-129">Należy najpierw utworzyć bramę usługi ExpressRoute hello przed dodaniem hello Brama VPN lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="76512-129">You must create hello ExpressRoute gateway first before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="76512-130">Projekty konfiguracji</span><span class="sxs-lookup"><span data-stu-id="76512-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="76512-131">Konfigurowanie sieci VPN typu lokacja-lokacja jako ścieżki pracy awaryjnej dla usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="76512-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="76512-132">Połączenie sieci VPN typu lokacja-lokacja można skonfigurować do przechowywania kopii zapasowych dla usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="76512-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="76512-133">Dotyczy to tylko toovirtual sieci połączonych toohello Azure prywatnej komunikacji równorzędnej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="76512-133">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="76512-134">Nie ma rozwiązania pracy awaryjnej opartego na sieci VPN dla usług dostępnych przez publiczne sesje komunikacji równorzędnej platformy Azure ani komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="76512-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="76512-135">Witaj obwodu ExpressRoute jest zawsze hello łącze podstawowe.</span><span class="sxs-lookup"><span data-stu-id="76512-135">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="76512-136">Dane będą przepływać za pomocą ścieżki sieci VPN typu lokacja-lokacja hello tylko wtedy, gdy hello obwodu usługi expressroute nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="76512-136">Data will flow through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="76512-137">Podczas obwodu ExpressRoute preferowanych za pośrednictwem połączenia VPN lokacja-lokacja po obu trasy są takie same Witaj, Azure użyje hello Najdłuższy prefiks dopasowania toochoose hello trasy do miejsca docelowego hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="76512-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Współistnienie](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="76512-139">Konfigurowanie sieci VPN typu lokacja-lokacja toosites tooconnect, nie są połączone za pośrednictwem usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="76512-139">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="76512-140">Można skonfigurować sieci, której niektóre Lokacje łączą się bezpośrednio tooAzure za pośrednictwem połączenia VPN lokacja-lokacja, a niektóre witryny łączenie się za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="76512-140">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Współistnienie](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="76512-142">Nie można skonfigurować sieci wirtualnej jako routera tranzytowego.</span><span class="sxs-lookup"><span data-stu-id="76512-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="76512-143">Wybieranie toouse kroki hello</span><span class="sxs-lookup"><span data-stu-id="76512-143">Selecting hello steps toouse</span></span>
<span data-ttu-id="76512-144">Istnieją dwa różne zestawy toochoose procedury od w kolejności tooconfigure połączeń, które mogą współistnieć.</span><span class="sxs-lookup"><span data-stu-id="76512-144">There are two different sets of procedures toochoose from in order tooconfigure connections that can coexist.</span></span> <span data-ttu-id="76512-145">procedury konfiguracji Hello, która zostanie wybrana zależy od tego, czy masz istniejącej sieci wirtualnej ma tooconnect do, czy chcesz toocreate nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="76512-145">hello configuration procedure that you select will depend on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="76512-146">Nie ma sieci wirtualnej i toocreate, co potrzebne.</span><span class="sxs-lookup"><span data-stu-id="76512-146">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="76512-147">Jeśli nie masz już sieć wirtualną, ta procedura przeprowadzi możesz tworzenia nowej sieci wirtualnej przy użyciu hello klasycznego modelu wdrażania i tworzenie nowych połączeń sieci VPN ExpressRoute, jak i lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="76512-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using hello classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="76512-148">tooconfigure, wykonaj kroki hello w sekcji artykule hello [toocreate nowej sieci wirtualnej i ważnych połączeń](#new).</span><span class="sxs-lookup"><span data-stu-id="76512-148">tooconfigure, follow hello steps in hello article section [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="76512-149">Mam już sieć wirtualną wdrożoną w ramach modelu klasycznego.</span><span class="sxs-lookup"><span data-stu-id="76512-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="76512-150">Być może masz już gotową sieć wirtualną z istniejącym połączeniem sieci VPN typu lokacja-lokacja lub połączeniem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="76512-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="76512-151">Witaj sekcji artykule [tooconfigure coexsiting połączeń dla już istniejącej sieci wirtualnej](#add) przeprowadzi użytkownika przez proces usuwania hello bramy, a następnie utworzyć nowe połączenia ExpressRoute, jak i sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="76512-151">hello article section [tooconfigure coexsiting connections for an already existing VNet](#add) will walk you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="76512-152">Należy pamiętać, że podczas tworzenia nowych połączeń hello, hello czynności musi wykonać w bardzo określonej kolejności.</span><span class="sxs-lookup"><span data-stu-id="76512-152">Note that when creating hello new connections, hello steps must be completed in a very specific order.</span></span> <span data-ttu-id="76512-153">Nie należy używać instrukcji hello w innych artykułach toocreate połączenia i bram.</span><span class="sxs-lookup"><span data-stu-id="76512-153">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="76512-154">W tej procedurze tworzenia połączeń, które mogą współistnieć będzie wymagają toodelete możesz bramy, a następnie skonfiguruj nowych bram.</span><span class="sxs-lookup"><span data-stu-id="76512-154">In this procedure, creating connections that can coexist will require you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="76512-155">Oznacza to, że konieczne będzie przestojów w przypadku połączeń między lokalizacjami w przypadku usunięcia i ponownego tworzenia bramy i połączenia, ale nie będzie konieczne toomigrate poszczególnych maszyn wirtualnych lub usług tooa nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="76512-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="76512-156">Maszyn wirtualnych i usług będą nadal mogli toocommunicate się za pośrednictwem usługi równoważenia obciążenia hello podczas konfigurowania bramy, jeśli są one skonfigurowane toodo tak.</span><span class="sxs-lookup"><span data-stu-id="76512-156">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="76512-157"><a name="new"></a>toocreate nowej sieci wirtualnej i ważnych połączeń</span><span class="sxs-lookup"><span data-stu-id="76512-157"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="76512-158">Ta procedura zawiera instrukcje tworzenia sieci wirtualnej i połączeń typu lokacja-lokacja oraz usługi ExpressRoute, które będą współistnieć.</span><span class="sxs-lookup"><span data-stu-id="76512-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="76512-159">Będziesz potrzebować tooinstall hello najnowszą wersję hello poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76512-159">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="76512-160">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76512-160">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="76512-161">Należy pamiętać, że polecenia cmdlet hello, który ma być używany dla tej konfiguracji mogą być nieco inne niż co można zapoznać się z.</span><span class="sxs-lookup"><span data-stu-id="76512-161">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="76512-162">Polecenia cmdlet hello toouse się, że można określić w tej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="76512-162">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="76512-163">Utwórz schemat dla sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="76512-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="76512-164">Aby uzyskać więcej informacji na temat hello schemat konfiguracji, zobacz [schemat konfiguracji sieci wirtualnej Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="76512-164">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="76512-165">Podczas tworzenia schematu, upewnij się, że używasz hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="76512-165">When you create your schema, make sure you use hello following values:</span></span>
   
   * <span data-ttu-id="76512-166">Witaj podsieci bramy sieci wirtualnej hello musi być /27 lub krótszy prefiksu (na przykład /26 lub /25).</span><span class="sxs-lookup"><span data-stu-id="76512-166">hello gateway subnet for hello virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="76512-167">Typ połączenia bramy Hello jest "dedykowany".</span><span class="sxs-lookup"><span data-stu-id="76512-167">hello gateway connection type is "Dedicated".</span></span>
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. <span data-ttu-id="76512-168">Po utworzeniu i konfigurowanie pliku schematu xml, Przekaż plik hello.</span><span class="sxs-lookup"><span data-stu-id="76512-168">After creating and configuring your xml schema file, upload hello file.</span></span> <span data-ttu-id="76512-169">Spowoduje to utworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="76512-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="76512-170">Użyj następującego polecenia cmdlet tooupload hello pliku, zastępując wartość hello własne.</span><span class="sxs-lookup"><span data-stu-id="76512-170">Use hello following cmdlet tooupload your file, replacing hello value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="76512-171"><a name="gw"></a>Utwórz bramę usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="76512-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="76512-172">Należy się toospecify hello GatewaySKU jako *standardowe*, *wysokowydajnej*, lub *UltraPerformance* i hello elementu GatewayType jako *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="76512-172">Be sure toospecify hello GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="76512-173">Użyj hello następujące przykładowe, zastępując hello własne wartości.</span><span class="sxs-lookup"><span data-stu-id="76512-173">Use hello following sample, substituting hello values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="76512-174">Połącz obwodu ExpressRoute toohello hello ExpressRoute bramy.</span><span class="sxs-lookup"><span data-stu-id="76512-174">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="76512-175">Po wykonaniu tego kroku hello połączenie między siecią lokalną a Azure za pośrednictwem usługi ExpressRoute, zostanie nawiązane.</span><span class="sxs-lookup"><span data-stu-id="76512-175">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="76512-176"><a name="vpngw"></a>Następnie utwórz bramę sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="76512-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="76512-177">Witaj GatewaySKU musi być *standardowe*, *wysokowydajnej*, lub *UltraPerformance* i hello elementu GatewayType musi być *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="76512-177">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="76512-178">Ustawienia bramy w tooretrieve hello sieci wirtualnej, tym hello identyfikator bramy i hello publicznego adresu IP, użyj hello `Get-AzureVirtualNetworkGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="76512-178">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. <span data-ttu-id="76512-179">Utwórz obiekt bramy sieci VPN witryny lokalnej.</span><span class="sxs-lookup"><span data-stu-id="76512-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="76512-180">To polecenie nie powoduje skonfigurowania bramy lokalnej sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="76512-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="76512-181">Zamiast pozwala tooprovide hello bramy lokalnej ustawienia, takie jak hello publicznego adresu IP i hello lokalnej przestrzeni adresów, dzięki czemu hello bramy sieci VPN platformy Azure można łączyć tooit.</span><span class="sxs-lookup"><span data-stu-id="76512-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="76512-182">Witaj lokalnej lokacji hello sieci VPN typu lokacja-lokacja nie jest zdefiniowany w hello netcfg.</span><span class="sxs-lookup"><span data-stu-id="76512-182">hello local site for hello Site-to-Site VPN is not defined in hello netcfg.</span></span> <span data-ttu-id="76512-183">Zamiast tego należy użyć tego polecenia cmdlet toospecify hello lokacji lokalnej parametrów.</span><span class="sxs-lookup"><span data-stu-id="76512-183">Instead, you must use this cmdlet toospecify hello local site parameters.</span></span> <span data-ttu-id="76512-184">Nie można zdefiniować za pomocą portalu lub hello netcfg pliku.</span><span class="sxs-lookup"><span data-stu-id="76512-184">You cannot define it using either portal, or hello netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="76512-185">Użyj hello następujące przykładowe, zastępując wartości hello własne.</span><span class="sxs-lookup"><span data-stu-id="76512-185">Use hello following sample, replacing hello values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="76512-186">Jeżeli sieć lokalna ma wiele tras, możesz je wszystkie przekazać w postaci tablicy.</span><span class="sxs-lookup"><span data-stu-id="76512-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="76512-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="76512-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="76512-188">Ustawienia bramy w tooretrieve hello sieci wirtualnej, tym hello identyfikator bramy i hello publicznego adresu IP, użyj hello `Get-AzureVirtualNetworkGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="76512-188">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="76512-189">Zobacz poniższy przykład hello.</span><span class="sxs-lookup"><span data-stu-id="76512-189">See hello following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="76512-190">Konfigurowanie bramy lokalnej sieci VPN urządzenia tooconnect toohello nowe.</span><span class="sxs-lookup"><span data-stu-id="76512-190">Configure your local VPN device tooconnect toohello new gateway.</span></span> <span data-ttu-id="76512-191">Użyj informacji hello, którego został pobrany w kroku 6 podczas konfigurowania urządzenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="76512-191">Use hello information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="76512-192">Więcej informacji na temat konfigurowania urządzenia VPN znajduje się w artykule [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md) (Konfigurowanie urządzenia VPN).</span><span class="sxs-lookup"><span data-stu-id="76512-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="76512-193">Łącze hello bramy sieci VPN typu lokacja-lokacja w Azure toohello bramy lokalnej.</span><span class="sxs-lookup"><span data-stu-id="76512-193">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>
   
    <span data-ttu-id="76512-194">W tym przykładzie connectedEntityId to identyfikator bramy lokalnej hello, który można znaleźć, uruchamiając `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="76512-194">In this example, connectedEntityId is hello local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="76512-195">VirtualNetworkGatewayId można znaleźć przy użyciu hello `Get-AzureVirtualNetworkGateway` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="76512-195">You can find virtualNetworkGatewayId by using hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="76512-196">Po wykonaniu tego kroku zostanie nawiązane połączenie hello między siecią lokalną a Azure za pośrednictwem hello połączenie sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="76512-196">After this step, hello connection between your local network and Azure via hello Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="76512-197"><a name="add"></a>tooconfigure coexsiting połączeń dla już istniejącej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="76512-197"><a name="add"></a>tooconfigure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="76512-198">Jeśli masz istniejącą sieć wirtualną, należy sprawdzić rozmiar podsieci bramy hello.</span><span class="sxs-lookup"><span data-stu-id="76512-198">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="76512-199">Podsieć bramy hello jest /28 lub /29, należy najpierw usunąć bramę sieci wirtualnej hello, Zwiększ rozmiar podsieci bramy hello.</span><span class="sxs-lookup"><span data-stu-id="76512-199">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="76512-200">Witaj kroki opisane w tej sekcji opisano, jak toodo który.</span><span class="sxs-lookup"><span data-stu-id="76512-200">hello steps in this section will show you how toodo that.</span></span>

<span data-ttu-id="76512-201">Jeśli podsieć bramy hello jest /27 lub większy i sieć wirtualna hello jest połączony za pośrednictwem usługi ExpressRoute, można pominąć kroki hello poniżej i przejść za["Krok 6 — utworzenie bramy sieci VPN typu lokacja-lokacja"](#vpngw) hello w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="76512-201">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="76512-202">Po usunięciu hello istniejącą bramę lokalnego lokalnej spowoduje utratę hello sieci wirtualnej tooyour połączenia podczas pracy w tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="76512-202">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="76512-203">Będziesz potrzebować tooinstall hello najnowszą wersję hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="76512-203">You'll need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="76512-204">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) Aby uzyskać więcej informacji o instalowaniu hello poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76512-204">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="76512-205">Należy pamiętać, że polecenia cmdlet hello, który ma być używany dla tej konfiguracji mogą być nieco inne niż co można zapoznać się z.</span><span class="sxs-lookup"><span data-stu-id="76512-205">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="76512-206">Polecenia cmdlet hello toouse się, że można określić w tej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="76512-206">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="76512-207">Usuń hello istniejącą bramę usługi ExpressRoute lub sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="76512-207">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="76512-208">Użyj hello następującego polecenia cmdlet, zastępując wartości hello własne.</span><span class="sxs-lookup"><span data-stu-id="76512-208">Use hello following cmdlet, replacing hello values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="76512-209">Eksportuj hello schemat sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="76512-209">Export hello virtual network schema.</span></span> <span data-ttu-id="76512-210">Użyj hello następującego polecenia cmdlet programu PowerShell, zastępując wartości hello własne.</span><span class="sxs-lookup"><span data-stu-id="76512-210">Use hello following PowerShell cmdlet, replacing hello values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="76512-211">Edytuj schemat pliku konfiguracji sieci hello tak, aby podsieci bramy hello jest /27 lub krótszy prefiksu (na przykład /26 lub /25).</span><span class="sxs-lookup"><span data-stu-id="76512-211">Edit hello network configuration file schema so that hello gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="76512-212">Zobacz poniższy przykład hello.</span><span class="sxs-lookup"><span data-stu-id="76512-212">See hello following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="76512-213">Jeśli masz za mało adresów IP pozostałych w rozmiar podsieci bramy sieci wirtualnej tooincrease hello należy tooadd więcej przestrzeni adresów IP.</span><span class="sxs-lookup"><span data-stu-id="76512-213">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span> <span data-ttu-id="76512-214">Aby uzyskać więcej informacji na temat hello schemat konfiguracji, zobacz [schemat konfiguracji sieci wirtualnej Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="76512-214">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="76512-215">Jeśli poprzednie Brama VPN lokacja-lokacja, należy również zmienić typ połączenia hello zbyt**dedykowana**.</span><span class="sxs-lookup"><span data-stu-id="76512-215">If your previous gateway was a Site-to-Site VPN, you must also change hello connection type too**Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="76512-216">Na tym etapie będziesz mieć sieć wirtualną bez bram.</span><span class="sxs-lookup"><span data-stu-id="76512-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="76512-217">toocreate nowych bram i zakończenie połączenia, można przystąpić do [krok 4 — Utwórz bramę usługi ExpressRoute](#gw), liczba znalezionych w hello poprzedzających zestaw kroków.</span><span class="sxs-lookup"><span data-stu-id="76512-217">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76512-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="76512-218">Next steps</span></span>
<span data-ttu-id="76512-219">Aby uzyskać więcej informacji na temat połączenia ExpressRoute, zobacz hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="76512-219">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

