---
title: "Konfigurowanie połączeń usługi ExpressRoute i sieci VPN typu lokacja-lokacja, które mogą współistnieć: wersja klasyczna: Azure | Microsoft Docs"
description: "Ten artykuł zawiera instrukcje dotyczące konfigurowania połączeń usługi ExpressRoute oraz sieci VPN typu lokacja-lokacja, które mogą współistnieć, w klasycznym modelu wdrożenia."
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
ms.openlocfilehash: 09d1649f0ca0cf4ca464d95b29461cad3fe51788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="0b513-103">Konfigurowanie współistniejących połączeń usługi ExpressRoute i połączeń typu lokacja-lokacja (wersja klasyczna)</span><span class="sxs-lookup"><span data-stu-id="0b513-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b513-104">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0b513-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="0b513-105">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="0b513-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="0b513-106">Możliwość skonfigurowania sieci VPN typu lokacja-lokacja i usługi ExpressRoute niesie ze sobą pewne korzyści.</span><span class="sxs-lookup"><span data-stu-id="0b513-106">Having the ability to configure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="0b513-107">Sieć VPN typu lokacja-lokacja można skonfigurować jako bezpieczną ścieżkę pracy awaryjnej dla usługi ExpressRoute lub użyć jej do połączenia z witrynami, które nie zostały połączone za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="0b513-108">Ten artykuł zawiera instrukcje konfiguracji obu scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="0b513-108">We will cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="0b513-109">Dotyczy on klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0b513-109">This article applies to the classic deployment model.</span></span> <span data-ttu-id="0b513-110">Ta konfiguracja nie jest dostępna w portalu.</span><span class="sxs-lookup"><span data-stu-id="0b513-110">This configuration is not available in the portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="0b513-111">**Modele wdrażania Azure — informacje**</span><span class="sxs-lookup"><span data-stu-id="0b513-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="0b513-112">Przed wykonaniem poniższych instrukcji należy wstępnie skonfigurować obwody usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-112">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="0b513-113">Przed wykonaniem poniższych kroków należy koniecznie wykonać instrukcje [tworzenia obwodu usługi ExpressRoute](expressroute-howto-circuit-classic.md) i [konfigurowania routingu](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="0b513-113">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow the steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="0b513-114">Limity i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="0b513-114">Limits and limitations</span></span>
* <span data-ttu-id="0b513-115">**Routing tranzytowy nie jest obsługiwany.**</span><span class="sxs-lookup"><span data-stu-id="0b513-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="0b513-116">Nie można skierować połączenia (przez platformę Azure) między lokalną siecią połączoną za pośrednictwem sieci VPN typu lokacja-lokacja i lokalną siecią połączoną za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="0b513-117">**Połączenia typu punkt-lokacja nie są obsługiwane.**</span><span class="sxs-lookup"><span data-stu-id="0b513-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="0b513-118">Nie można włączyć połączeń VPN typu punkt-lokacja do tej samej sieci wirtualnej, która jest połączona z usługą ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-118">You can't enable point-to-site VPN connections to the same VNet that is connected to ExpressRoute.</span></span> <span data-ttu-id="0b513-119">Sieć VPN typu punkt-lokacja i usługa ExpressRoute nie mogą współistnieć dla tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0b513-119">Point-to-site VPN and ExpressRoute cannot coexist for the same VNet.</span></span>
* <span data-ttu-id="0b513-120">**Nie można włączyć tunelowania wymuszonego dla bramy sieci VPN typu lokacja-lokacja.**</span><span class="sxs-lookup"><span data-stu-id="0b513-120">**Forced tunneling cannot be enabled on the Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="0b513-121">Można tylko „wymusić” przesyłanie całego ruchu skierowanego do Internetu z powrotem do sieci lokalnej za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-121">You can only "force" all Internet-bound traffic back to your on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="0b513-122">**Podstawowa brama jednostki SKU nie jest obsługiwana.**</span><span class="sxs-lookup"><span data-stu-id="0b513-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="0b513-123">Należy użyć innej niż podstawowa bramy jednostki SKU zarówno dla [bramy usługi ExpressRoute](expressroute-about-virtual-network-gateways.md), jak i [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="0b513-123">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="0b513-124">**Obsługiwana jest tylko brama sieci VPN oparta na trasach.**</span><span class="sxs-lookup"><span data-stu-id="0b513-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="0b513-125">Należy użyć [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) opartej na trasach.</span><span class="sxs-lookup"><span data-stu-id="0b513-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="0b513-126">**Dla bramy sieci VPN należy skonfigurować trasę statyczną.**</span><span class="sxs-lookup"><span data-stu-id="0b513-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="0b513-127">Jeśli sieć lokalna jest połączona z usługą ExpressRoute oraz siecią VPN typu lokacja-lokacja, aby skierować połączenie sieci VPN typu lokacja-lokacja do publicznego Internetu, trzeba mieć skonfigurowaną trasę statyczną w sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="0b513-127">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="0b513-128">**Najpierw należy skonfigurować bramę usługi ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="0b513-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="0b513-129">Przed dodaniem bramy sieci VPN typu lokacja-lokacja należy utworzyć bramę usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-129">You must create the ExpressRoute gateway first before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="0b513-130">Projekty konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0b513-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="0b513-131">Konfigurowanie sieci VPN typu lokacja-lokacja jako ścieżki pracy awaryjnej dla usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="0b513-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="0b513-132">Połączenie sieci VPN typu lokacja-lokacja można skonfigurować do przechowywania kopii zapasowych dla usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="0b513-133">Dotyczy to tylko sieci wirtualnych połączonych ze ścieżką prywatnej sieci równorzędnej Azure.</span><span class="sxs-lookup"><span data-stu-id="0b513-133">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="0b513-134">Nie ma rozwiązania pracy awaryjnej opartego na sieci VPN dla usług dostępnych przez publiczne sesje komunikacji równorzędnej platformy Azure ani komunikacji równorzędnej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0b513-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="0b513-135">Obwód usługi ExpressRoute jest zawsze połączeniem podstawowym.</span><span class="sxs-lookup"><span data-stu-id="0b513-135">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="0b513-136">Dane będą przepływać przez ścieżkę sieci VPN typu lokacja-lokacja tylko w wypadku awarii obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-136">Data will flow through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="0b513-137">Obwód usługi ExpressRoute jest preferowany w porównaniu z siecią VPN typu lokacja-lokacja, jeśli obydwie trasy są takie same, a na platformie Azure dopasowanie najdłuższego prefiksu będzie używane do wybierania trasy do miejsca docelowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="0b513-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![Współistnienie](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="0b513-139">Konfigurowanie sieci VPN typu lokacja-lokacja do łączenia z witrynami niepołączonymi przez usługę ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="0b513-139">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="0b513-140">Można skonfigurować sieć w taki sposób, by niektóre witryny łączyły się bezpośrednio z platformą Azure za pośrednictwem sieci VPN typu lokacja-lokacja, a niektóre przez usługę ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-140">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Współistnienie](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="0b513-142">Nie można skonfigurować sieci wirtualnej jako routera tranzytowego.</span><span class="sxs-lookup"><span data-stu-id="0b513-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="0b513-143">Wybieranie czynności do wykonania</span><span class="sxs-lookup"><span data-stu-id="0b513-143">Selecting the steps to use</span></span>
<span data-ttu-id="0b513-144">Istnieją dwa różne zestawy procedur do wyboru służące do konfigurowania połączeń, które mogą współistnieć.</span><span class="sxs-lookup"><span data-stu-id="0b513-144">There are two different sets of procedures to choose from in order to configure connections that can coexist.</span></span> <span data-ttu-id="0b513-145">Wybór procedury konfiguracji będzie zależeć od tego, czy masz istniejącą sieć wirtualną, z którą chcesz się połączyć, czy chcesz utworzyć nową.</span><span class="sxs-lookup"><span data-stu-id="0b513-145">The configuration procedure that you select will depend on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="0b513-146">Nie mam sieci wirtualnej i muszę ją utworzyć.</span><span class="sxs-lookup"><span data-stu-id="0b513-146">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="0b513-147">Jeśli nie masz jeszcze sieci wirtualnej, ta procedura zawiera instrukcje tworzenia nowej sieci wirtualnej za pomocą klasycznego modelu wdrożenia i tworzenia nowych połączeń usługi ExpressRoute i sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="0b513-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using the classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="0b513-148">Aby przeprowadzić konfigurację, wykonaj kroki opisane w sekcji artykułu [Aby utworzyć nową sieć wirtualną i współistniejące połączenia](#new).</span><span class="sxs-lookup"><span data-stu-id="0b513-148">To configure, follow the steps in the article section [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="0b513-149">Mam już sieć wirtualną wdrożoną w ramach modelu klasycznego.</span><span class="sxs-lookup"><span data-stu-id="0b513-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="0b513-150">Być może masz już gotową sieć wirtualną z istniejącym połączeniem sieci VPN typu lokacja-lokacja lub połączeniem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="0b513-151">Sekcja artykułu [Aby skonfigurować współistniejące połączenia dla już istniejących sieci wirtualnych](#add) zawiera instrukcje usuwania bramy, a następnie tworzenia nowych połączeń usługi ExpressRoute i połączeń VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="0b513-151">The article section [To configure coexsiting connections for an already existing VNet](#add) will walk you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="0b513-152">Należy pamiętać, że podczas tworzenia nowych połączeń kroki muszą być wykonywane po kolei.</span><span class="sxs-lookup"><span data-stu-id="0b513-152">Note that when creating the new connections, the steps must be completed in a very specific order.</span></span> <span data-ttu-id="0b513-153">Do tworzenia bram i połączeń nie używaj instrukcji z innych artykułów.</span><span class="sxs-lookup"><span data-stu-id="0b513-153">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="0b513-154">W tej procedurze tworzenie połączeń, które mogą współistnieć, wymaga usunięcia bramy, a następnie skonfigurowania nowych bram.</span><span class="sxs-lookup"><span data-stu-id="0b513-154">In this procedure, creating connections that can coexist will require you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="0b513-155">Oznacza to, że podczas usuwania i odtwarzania bramy oraz połączeń wystąpi przestój względem połączeń obejmujących wiele lokalizacji, ale nie trzeba będzie migrować żadnych maszyn wirtualnych ani usług do nowej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0b513-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="0b513-156">Podczas konfigurowania bramy maszyny wirtualne i usługi będą mogły nadal komunikować się za pośrednictwem modułu równoważenia obciążenia, jeżeli zostały w taki sposób skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="0b513-156">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="0b513-157"><a name="new"></a>Aby utworzyć nową sieć wirtualną i współistniejące połączenia</span><span class="sxs-lookup"><span data-stu-id="0b513-157"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="0b513-158">Ta procedura zawiera instrukcje tworzenia sieci wirtualnej i połączeń typu lokacja-lokacja oraz usługi ExpressRoute, które będą współistnieć.</span><span class="sxs-lookup"><span data-stu-id="0b513-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="0b513-159">Niezbędne jest zainstalowanie najnowszej wersji poleceń cmdlet programu Azure PowerShell. </span><span class="sxs-lookup"><span data-stu-id="0b513-159">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="0b513-160">Aby uzyskać więcej informacji na temat instalowania poleceń cmdlet programu Azure PowerShell, zobacz artykuł [How to install and configure Azure PowerShell](/powershell/azure/overview) (Instalowanie i konfigurowanie programu Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="0b513-160">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="0b513-161">Pamiętaj, że polecenia cmdlet, które zostaną użyte do tej konfiguracji, mogą trochę różnić się od tych, które znasz.</span><span class="sxs-lookup"><span data-stu-id="0b513-161">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="0b513-162">Koniecznie użyj poleceń cmdlet podanych w tych instrukcjach.</span><span class="sxs-lookup"><span data-stu-id="0b513-162">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="0b513-163">Utwórz schemat dla sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0b513-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="0b513-164">Więcej informacji na temat schematu konfiguracji znajduje się w artykule [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx) (Schemat konfiguracji sieci wirtualnej Azure).</span><span class="sxs-lookup"><span data-stu-id="0b513-164">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="0b513-165">Podczas tworzenia schematu pamiętaj, aby użyć następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="0b513-165">When you create your schema, make sure you use the following values:</span></span>
   
   * <span data-ttu-id="0b513-166">Wartość podsieci bramy dla sieci wirtualnej musi wynosić /27; prefiks może też być krótszy (np. /26 lub /25).</span><span class="sxs-lookup"><span data-stu-id="0b513-166">The gateway subnet for the virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="0b513-167">Typ połączenia bramy ma wartość „Dedykowane”.</span><span class="sxs-lookup"><span data-stu-id="0b513-167">The gateway connection type is "Dedicated".</span></span>
     
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
3. <span data-ttu-id="0b513-168">Po utworzeniu i skonfigurowaniu pliku schematu xml przekaż plik.</span><span class="sxs-lookup"><span data-stu-id="0b513-168">After creating and configuring your xml schema file, upload the file.</span></span> <span data-ttu-id="0b513-169">Spowoduje to utworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0b513-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="0b513-170">Użyj poniższego polecenia cmdlet do przekazania pliku, zastępując wartość swoją własną.</span><span class="sxs-lookup"><span data-stu-id="0b513-170">Use the following cmdlet to upload your file, replacing the value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="0b513-171"><a name="gw"></a>Utwórz bramę usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="0b513-172">Koniecznie określ wartość *Standard*, *HighPerformance* lub *UltraPerformance* dla parametru GatewaySKU oraz wartość *DynamicRouting* dla parametru GatewayType.</span><span class="sxs-lookup"><span data-stu-id="0b513-172">Be sure to specify the GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="0b513-173">Użyj poniższego przykładu, podstawiając wartości zamiast swoich własnych.</span><span class="sxs-lookup"><span data-stu-id="0b513-173">Use the following sample, substituting the values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="0b513-174">Połącz bramę usługi ExpressRoute z obwodem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-174">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="0b513-175">Po ukończeniu tego kroku zostanie nawiązane połączenie między siecią lokalną i platformą Azure za pośrednictwem usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0b513-175">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="0b513-176"><a name="vpngw"></a>Następnie utwórz bramę sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="0b513-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="0b513-177">Parametr GatewaySKU musi mieć wartość *Standard*, *HighPerformance* lub *UltraPerformance*, a parametr GatewayType — *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="0b513-177">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="0b513-178">Aby pobrać ustawienia bramy sieci wirtualnej, w tym identyfikator bramy i publiczny adres IP, użyj polecenia `Get-AzureVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="0b513-178">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for the following virtual network: GNSDesMoines
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
7. <span data-ttu-id="0b513-179">Utwórz obiekt bramy sieci VPN witryny lokalnej.</span><span class="sxs-lookup"><span data-stu-id="0b513-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="0b513-180">To polecenie nie powoduje skonfigurowania bramy lokalnej sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="0b513-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="0b513-181">Umożliwia raczej zapewnienie ustawień bramy lokalnej, np. publicznego adresu IP i lokalnej przestrzeni adresowej, aby brama sieci VPN Azure mogła się z nimi połączyć.</span><span class="sxs-lookup"><span data-stu-id="0b513-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="0b513-182">Lokalna witryna dla sieci VPN typu lokacja-lokacja nie jest definiowana w pliku netcfg.</span><span class="sxs-lookup"><span data-stu-id="0b513-182">The local site for the Site-to-Site VPN is not defined in the netcfg.</span></span> <span data-ttu-id="0b513-183">Zamiast tego musisz użyć tego polecenia cmdlet do określania lokalnych parametrów witryny.</span><span class="sxs-lookup"><span data-stu-id="0b513-183">Instead, you must use this cmdlet to specify the local site parameters.</span></span> <span data-ttu-id="0b513-184">Nie możesz jej definiować przy użyciu portalu ani pliku netcfg.</span><span class="sxs-lookup"><span data-stu-id="0b513-184">You cannot define it using either portal, or the netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="0b513-185">Użyj poniższego przykładu, zastępując wartości swoimi własnymi.</span><span class="sxs-lookup"><span data-stu-id="0b513-185">Use the following sample, replacing the values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="0b513-186">Jeżeli sieć lokalna ma wiele tras, możesz je wszystkie przekazać w postaci tablicy.</span><span class="sxs-lookup"><span data-stu-id="0b513-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="0b513-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="0b513-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="0b513-188">Aby pobrać ustawienia bramy sieci wirtualnej, w tym identyfikator bramy i publiczny adres IP, użyj polecenia `Get-AzureVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="0b513-188">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="0b513-189">Zobacz poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="0b513-189">See the following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="0b513-190">Skonfiguruj lokalne urządzenie sieci VPN do połączenia z nową bramą.</span><span class="sxs-lookup"><span data-stu-id="0b513-190">Configure your local VPN device to connect to the new gateway.</span></span> <span data-ttu-id="0b513-191">Podczas konfigurowania urządzenia VPN użyj informacji pobranych w kroku 6.</span><span class="sxs-lookup"><span data-stu-id="0b513-191">Use the information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="0b513-192">Więcej informacji na temat konfigurowania urządzenia VPN znajduje się w artykule [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md) (Konfigurowanie urządzenia VPN).</span><span class="sxs-lookup"><span data-stu-id="0b513-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="0b513-193">Połącz bramę sieci VPN typu lokacja-lokacja na platformie Azure z bramą lokalną.</span><span class="sxs-lookup"><span data-stu-id="0b513-193">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>
   
    <span data-ttu-id="0b513-194">W tym przykładzie connectedEntityId jest identyfikatorem bramy lokalnej, który można znaleźć, uruchamiając polecenie `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="0b513-194">In this example, connectedEntityId is the local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="0b513-195">Identyfikator VirtualNetworkGatewayId można znaleźć przy użyciu polecenia cmdlet `Get-AzureVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="0b513-195">You can find virtualNetworkGatewayId by using the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="0b513-196">Po wykonaniu tego kroku zostanie nawiązane połączenie między siecią lokalną i platformą Azure za pośrednictwem połączenia VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="0b513-196">After this step, the connection between your local network and Azure via the Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="0b513-197"><a name="add"></a>Aby skonfigurować współistniejące połączenia dla istniejącej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0b513-197"><a name="add"></a>To configure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="0b513-198">Jeśli masz istniejącą sieć wirtualną, sprawdź rozmiar podsieci bramy.</span><span class="sxs-lookup"><span data-stu-id="0b513-198">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="0b513-199">Jeśli podsieć bramy ma wartość /28 lub /29, musisz najpierw usunąć bramę sieci wirtualnej i zwiększyć rozmiar podsieci bramy.</span><span class="sxs-lookup"><span data-stu-id="0b513-199">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="0b513-200">W krokach w tej sekcji przedstawiono, jak to zrobić.</span><span class="sxs-lookup"><span data-stu-id="0b513-200">The steps in this section will show you how to do that.</span></span>

<span data-ttu-id="0b513-201">Jeśli podsieć bramy ma wartość /27 lub większą, a sieć wirtualna jest połączona za pośrednictwem usługi ExpressRoute, możesz pominąć poniższe kroki i przejść do tematu [„Krok 6 — tworzenie bramy sieci VPN typu lokacja-lokacja”](#vpngw) w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0b513-201">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="0b513-202">Po usunięciu istniejącej bramy podczas pracy nad tą konfiguracją lokalizacja miejscowa straci połączenie z siecią wirtualną.</span><span class="sxs-lookup"><span data-stu-id="0b513-202">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="0b513-203">Niezbędne jest zainstalowanie najnowszej wersji poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0b513-203">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="0b513-204">Aby uzyskać więcej informacji na temat instalowania poleceń cmdlet programu Azure PowerShell, zobacz artykuł [How to install and configure Azure PowerShell](/powershell/azure/overview) (Instalowanie i konfigurowanie programu Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="0b513-204">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="0b513-205">Pamiętaj, że polecenia cmdlet, które zostaną użyte do tej konfiguracji, mogą trochę różnić się od tych, które znasz.</span><span class="sxs-lookup"><span data-stu-id="0b513-205">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="0b513-206">Koniecznie użyj poleceń cmdlet podanych w tych instrukcjach.</span><span class="sxs-lookup"><span data-stu-id="0b513-206">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="0b513-207">Usuń istniejącą bramę usługi ExpressRoute lub sieci VPN typu lokacja-lokacja.</span><span class="sxs-lookup"><span data-stu-id="0b513-207">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="0b513-208">Użyj poniższego polecenia cmdlet, zastępując wartości swoimi własnymi.</span><span class="sxs-lookup"><span data-stu-id="0b513-208">Use the following cmdlet, replacing the values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="0b513-209">Wyeksportuj schemat sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0b513-209">Export the virtual network schema.</span></span> <span data-ttu-id="0b513-210">Użyj poniższego polecenia cmdlet programu PowerShell, zastępując wartości swoimi własnymi.</span><span class="sxs-lookup"><span data-stu-id="0b513-210">Use the following PowerShell cmdlet, replacing the values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="0b513-211">Edytuj schemat pliku konfiguracji sieci w taki sposób, aby wartość podsieci bramy wynosiła /27 lub miała krótszy prefiks (np. /26 lub /25).</span><span class="sxs-lookup"><span data-stu-id="0b513-211">Edit the network configuration file schema so that the gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="0b513-212">Zobacz poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="0b513-212">See the following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0b513-213">Jeśli nie masz wystarczającej liczby adresów IP w sieci wirtualnej, aby zwiększyć rozmiar podsieci bramy, dodaj więcej przestrzeni adresowej IP.</span><span class="sxs-lookup"><span data-stu-id="0b513-213">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span> <span data-ttu-id="0b513-214">Więcej informacji na temat schematu konfiguracji znajduje się w artykule [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx) (Schemat konfiguracji sieci wirtualnej Azure).</span><span class="sxs-lookup"><span data-stu-id="0b513-214">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="0b513-215">Jeśli poprzednia brama pochodziła z sieci VPN typu lokacja-lokacja, musisz również zmienić typ połączenia na **Dedykowane**.</span><span class="sxs-lookup"><span data-stu-id="0b513-215">If your previous gateway was a Site-to-Site VPN, you must also change the connection type to **Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="0b513-216">Na tym etapie będziesz mieć sieć wirtualną bez bram.</span><span class="sxs-lookup"><span data-stu-id="0b513-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="0b513-217">W celu utworzenia nowych bram i wykonania połączeń wykonaj instrukcje z części [Krok 4 — tworzenie bramy usługi ExpressRoute](#gw) znajdujące się w poprzednim zestawie kroków.</span><span class="sxs-lookup"><span data-stu-id="0b513-217">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b513-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0b513-218">Next steps</span></span>
<span data-ttu-id="0b513-219">Więcej informacji na temat usługi ExpressRoute znajduje się w artykule [ExpressRoute FAQ](expressroute-faqs.md) (Usługa ExpressRoute — często zadawane pytania).</span><span class="sxs-lookup"><span data-stu-id="0b513-219">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

