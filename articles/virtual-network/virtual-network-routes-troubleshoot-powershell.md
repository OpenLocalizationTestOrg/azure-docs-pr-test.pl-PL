---
title: "Rozwiązywanie problemów z tras - PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązywać problemy z trasy w modelu wdrażania usługi Azure Resource Manager przy użyciu programu Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 141e3c571d744470fd07e99538b6e38d4144e8d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="df365-103">Rozwiązywanie problemów z tras za pomocą programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="df365-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="df365-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="df365-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="df365-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="df365-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="df365-106">Jeśli występują problemy z połączeniem sieciowym do lub z sieci maszyny wirtualnej Azure (VM), tras może mieć wpływ na Twoje ruch maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="df365-106">If you are experiencing network connectivity issues to or from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="df365-107">Ten artykuł zawiera omówienie funkcji diagnostyki dla tras do dalszego rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="df365-107">This article provides an overview of diagnostics capabilities for routes to help troubleshoot further.</span></span>

<span data-ttu-id="df365-108">Tabele tras są skojarzone z podsieciami i obowiązują na wszystkich interfejsach sieciowych (NIC) w tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="df365-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="df365-109">Następujące typy tras może odnosić się do każdego interfejsu sieciowego:</span><span class="sxs-lookup"><span data-stu-id="df365-109">The following types of routes can be applied to each network interface:</span></span>

* <span data-ttu-id="df365-110">**Trasy systemowe:** Domyślnie każda podsieć utworzona w sieci wirtualnej platformy Azure (VNet) ma tabel tras systemu, które umożliwiają lokalnej sieci wirtualnej ruch, ruch lokalnej za pośrednictwem bramy sieci VPN i ruchu internetowego.</span><span class="sxs-lookup"><span data-stu-id="df365-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="df365-111">Istnieją również tras systemowych dla połączyć za pomocą sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="df365-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="df365-112">**Trasy protokołu BGP:** propagowane do interfejsów sieciowych za pośrednictwem usługi ExpressRoute lub połączeń VPN lokacja lokacja.</span><span class="sxs-lookup"><span data-stu-id="df365-112">**BGP routes:** Propagated to network interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="df365-113">Dowiedz się więcej o routingu BGP, odczytując [protokołu BGP z bramy sieci VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) i [omówienie ExpressRoute](../expressroute/expressroute-introduction.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="df365-113">Learn more about BGP routing by reading the [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="df365-114">**Trasy zdefiniowane przez użytkownika (przez):** korzystając z wirtualnych urządzeń sieciowych lub są wymuszone tunelowanie ruch do sieci lokalnej za pośrednictwem sieci VPN lokacja lokacja, może być zdefiniowana przez użytkownika tras (Udr) skojarzone z tabeli tras podsieci.</span><span class="sxs-lookup"><span data-stu-id="df365-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic to an on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="df365-115">Jeśli nie masz doświadczenia w obsłudze Udr, przeczytaj [trasy zdefiniowane przez użytkownika](virtual-networks-udr-overview.md#user-defined-routes) artykułu.</span><span class="sxs-lookup"><span data-stu-id="df365-115">If you're not familiar with UDRs, read the [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="df365-116">Przy użyciu różnych tras, które można zastosować do interfejsu sieciowego może być trudne do ustalenia, obowiązują agregacji trasy.</span><span class="sxs-lookup"><span data-stu-id="df365-116">With the various routes that can be applied to a network interface, it can be difficult to determine which aggregate routes are effective.</span></span> <span data-ttu-id="df365-117">Do rozwiązywania problemów łączności sieciowej maszyny Wirtualnej, można wyświetlić wszystkie skuteczne trasy dla interfejsu sieciowego w modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="df365-117">To help troubleshoot VM network connectivity, you can view all the effective routes for a network interface in the Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="df365-118">Rozwiązywanie problemów z przepływem ruchu maszyny Wirtualnej za pomocą skuteczne tras</span><span class="sxs-lookup"><span data-stu-id="df365-118">Using Effective Routes to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="df365-119">W tym artykule używa następujący scenariusz jako przykład ilustrujący sposób rozwiązywania skuteczne trasy dla interfejsu sieciowego:</span><span class="sxs-lookup"><span data-stu-id="df365-119">This article uses the following scenario as an example to illustrate how to troubleshoot the effective routes for a network interface:</span></span>

<span data-ttu-id="df365-120">Maszyna wirtualna (*VM1*) podłączone do sieci wirtualnej (*VNet1*, prefiks: 10.9.0.0/16) nie może połączyć się VM(VM3) w nowo peered sieci wirtualnej (*VNet3*, prefiks 10.10.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="df365-120">A VM (*VM1*) connected to the VNet (*VNet1*, prefix: 10.9.0.0/16) fails to connect to a VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="df365-121">Brak Udr lub BGP kieruje stosowane do interfejsu sieciowego VM1 NIC1 podłączony do maszyny Wirtualnej, są stosowane tylko tras systemowych.</span><span class="sxs-lookup"><span data-stu-id="df365-121">There are no UDRs or BGP routes applied to VM1-NIC1 network interface connected to the VM, only system routes are applied.</span></span>

<span data-ttu-id="df365-122">W tym artykule opisano sposób ustalić przyczynę niepowodzenia połączenia przy użyciu możliwości wprowadzenia trasy w modelu wdrażania zarządzania zasobami Azure.</span><span class="sxs-lookup"><span data-stu-id="df365-122">This article explains how to determine the cause of the connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="df365-123">Podczas w przykładzie użyto tylko tras systemowych, te same kroki może służyć do określenia błędów połączenia przychodzącego i wychodzącego przez dowolnego typu trasy.</span><span class="sxs-lookup"><span data-stu-id="df365-123">While the example uses only system routes, the same steps can be used to determine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="df365-124">Jeśli maszyna wirtualna ma więcej niż jedną kartę Sieciową podłączoną, sprawdź skuteczne trasy dla każdej z kart sieciowych do diagnozowania problemów z łącznością sieciową z maszyny Wirtualnej i.</span><span class="sxs-lookup"><span data-stu-id="df365-124">If your VM has more than one NIC attached, check effective routes for each of the NICs to diagnose network connectivity issues to and from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="df365-125">Widok skuteczne trasy dla maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="df365-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="df365-126">Aby wyświetlić trasy agregacji, które są stosowane do maszyny Wirtualnej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="df365-126">To see the aggregate routes that are applied to a VM, complete the following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="df365-127">Widok skuteczne trasy dla interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="df365-127">View effective routes for a network interface</span></span>
<span data-ttu-id="df365-128">Aby wyświetlić trasy agregacji, które są stosowane do interfejsu sieciowego, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="df365-128">To see the aggregate routes that are applied to a network interface, complete the following steps:</span></span>

1. <span data-ttu-id="df365-129">Uruchom sesję programu PowerShell systemu Azure i logowania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="df365-129">Start an Azure PowerShell session and login to Azure.</span></span> <span data-ttu-id="df365-130">Jeśli nie masz doświadczenia w obsłudze programu Azure PowerShell, przeczytaj [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="df365-130">If you’re not familiar with Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="df365-131">Poniższe polecenie zwraca wszystkie trasy stosowany do karty sieciowej o nazwie *VM1 NIC1* w grupie zasobów *RG1*.</span><span class="sxs-lookup"><span data-stu-id="df365-131">The following command returns all routes applied to a network interface named *VM1-NIC1* in the resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="df365-132">Jeśli nie znasz nazwę karty sieciowej, wpisz następujące polecenie, aby pobrać wszystkie interfejsy sieciowe group.* zasobu nazwy</span><span class="sxs-lookup"><span data-stu-id="df365-132">If you don’t know the name of a network interface, type the following command to retrieve the names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="df365-133">Następujące dane wyjściowe wygląda podobnie do danych wyjściowych dla każdej trasy stosowana do podsieci, którą jest połączona karta sieciowa:</span><span class="sxs-lookup"><span data-stu-id="df365-133">The following output looks similar to the output for each route applied to the subnet the NIC is connected to:</span></span>
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   <span data-ttu-id="df365-134">Zwróć uwagę następujące opcje w danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="df365-134">Notice the following in the output:</span></span>
   
   * <span data-ttu-id="df365-135">**Nazwa**: Nazwa trasy skuteczne może być pusty, chyba że jawnie określone dla tras zdefiniowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="df365-135">**Name**: Name of the effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="df365-136">**Stan**: wskazuje stan skuteczne trasy.</span><span class="sxs-lookup"><span data-stu-id="df365-136">**State**: Indicates state of the effective route.</span></span> <span data-ttu-id="df365-137">Możliwe wartości to "Active" lub "Nieprawidłowe"</span><span class="sxs-lookup"><span data-stu-id="df365-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="df365-138">**AddressPrefixes**: Określa prefiks adresu skuteczne trasy w notacji CIDR.</span><span class="sxs-lookup"><span data-stu-id="df365-138">**AddressPrefixes**: Specifies the address prefix of the effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="df365-139">**Typ następnego przeskoku**: wskazuje następnego skoku dla danej trasy.</span><span class="sxs-lookup"><span data-stu-id="df365-139">**nextHopType**: Indicates the next hop for the given route.</span></span> <span data-ttu-id="df365-140">Możliwe wartości to *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, lub *Null*.</span><span class="sxs-lookup"><span data-stu-id="df365-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="df365-141">Wartość *Null* dla **Typ następnego przeskoku** przez może oznaczać nieprawidłową trasy.</span><span class="sxs-lookup"><span data-stu-id="df365-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="df365-142">Na przykład jeśli **Typ następnego przeskoku** jest *VirtualAppliance* i urządzenie wirtualne sieci maszyny Wirtualnej nie jest w stanie zainicjowano obsługę administracyjną uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="df365-142">For example, if **nextHopType** is *VirtualAppliance* and the network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="df365-143">Jeśli **Typ następnego przeskoku** jest *właściwość VPNGateway* i nie ma żadnych bramy elastycznie/uruchomiony w danej sieci wirtualnej, trasa mogą być nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="df365-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in the given VNet, the route may become invalid.</span></span>
   * <span data-ttu-id="df365-144">**Adres IP następnego przeskoku**: Określa adres IP następnego przeskoku skuteczne trasy.</span><span class="sxs-lookup"><span data-stu-id="df365-144">**NextHopIpAddress**: Specifies the IP address of the next hop of the effective route.</span></span>
   
   <span data-ttu-id="df365-145">Poniższe polecenie zwraca trasy w łatwiejsze wyświetlić tabelę:</span><span class="sxs-lookup"><span data-stu-id="df365-145">The following command returns the routes in an easier to view table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="df365-146">Następujące dane wyjściowe są niektóre z danych wyjściowych dla scenariusza opisanego wcześniej:</span><span class="sxs-lookup"><span data-stu-id="df365-146">The following output is some of the output received for the scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="df365-147">Brak trasy do *WestUS VNet3* sieciami wirtualnymi (prefiks 10.10.0.0/16)** z *WestUS VNet1* (prefiksu 10.9.0.0/16) w danych wyjściowych z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="df365-147">There is no route listed to the *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in the output from the previous step.</span></span> <span data-ttu-id="df365-148">Jak pokazano na poniższej ilustracji, równorzędna sieci wirtualnej Połącz z *WestUS VNet3* sieci wirtualnej jest w *Rozłączono* stanu.</span><span class="sxs-lookup"><span data-stu-id="df365-148">As shown in the following picture, the VNet peering link with the *WestUS-VNet3* VNet is in the *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="df365-149">Łącze dwukierunkowe dla komunikacji równorzędnej jest uszkodzona, który wyjaśnia dlaczego VM1 nie może połączyć się VM3 w *WestUS VNet3* sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="df365-149">The bi-directional link for the peering is broken, which explains why VM1 could not connect to VM3 in the *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="df365-150">Konfiguracja dwukierunkowe sieci wirtualnej komunikacji równorzędnej łącze ponownie *WestUS VNet1* i *WestUS VNet3* sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="df365-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="df365-151">Dane wyjściowe zwrócone w wyniku łącze sieci wirtualnej komunikacji równorzędnej jest poprawnie ustanowić następująco:</span><span class="sxs-lookup"><span data-stu-id="df365-151">The output returned after the VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="df365-152">Po określeniu problem, można dodać, usunąć, lub zmień tras i tabel tras.</span><span class="sxs-lookup"><span data-stu-id="df365-152">Once you determine the issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="df365-153">Wpisz następujące polecenie, aby wyświetlić listę poleceń używanych w tym celu:</span><span class="sxs-lookup"><span data-stu-id="df365-153">Type the following command to see a list of the commands used to do so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="df365-154">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="df365-154">Considerations</span></span>
<span data-ttu-id="df365-155">Zwrócono kilka rzeczy, które należy wziąć pod uwagę podczas przeglądania listy tras:</span><span class="sxs-lookup"><span data-stu-id="df365-155">A few things to keep in mind when reviewing the list of routes returned:</span></span>

* <span data-ttu-id="df365-156">Routing jest oparta na Najdłuższy prefiks dopasowania (LPM) Wybierane spośród Udr, trasy protokołu BGP i systemu.</span><span class="sxs-lookup"><span data-stu-id="df365-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="df365-157">Jeśli istnieje więcej niż jedna trasa z tym samym dopasowaniem LPM, następnie wybór trasy odbywa się w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="df365-157">If there is more than one route with the same LPM match, then a route is selected based on its origin in the following order:</span></span>
  
  * <span data-ttu-id="df365-158">Trasa zdefiniowana przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="df365-158">User-defined route</span></span>
  * <span data-ttu-id="df365-159">Trasa protokołu BGP</span><span class="sxs-lookup"><span data-stu-id="df365-159">BGP route</span></span>
  * <span data-ttu-id="df365-160">Trasa systemowa (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="df365-160">System (Default) route</span></span>
    
    <span data-ttu-id="df365-161">Skuteczne trasy może zobaczyć tylko skuteczne ścieżek, które są dopasowaniem LPM oparte na trasach są one dostępne.</span><span class="sxs-lookup"><span data-stu-id="df365-161">With effective routes, you can only see effective routes that are LPM match based on all the availble routes.</span></span> <span data-ttu-id="df365-162">Przez pokazanie, jak trasy faktycznie są oceniane pod kątem danej karty Sieciowej, dzięki temu znacznie łatwiejsze Rozwiązywanie problemów z określonej trasy, które mogą mieć wpływ na łączność z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="df365-162">By showing how the routes are actually evaluated for a given NIC, this makes it a lot easier to troubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="df365-163">Jeśli masz Udr i wysyłania ruchu do sieci (NVA), urządzenie wirtualne z *VirtualAppliance* jako **Typ następnego przeskoku**, upewnij się, że przekazywanie IP jest włączona na NVA odbieranie ruchu lub pakietów porzucone.</span><span class="sxs-lookup"><span data-stu-id="df365-163">If you have UDRs and are sending traffic to a network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on the NVA receiving the traffic or packets are dropped.</span></span> 
* <span data-ttu-id="df365-164">Jeśli włączono wymuszony tunelowania cały ruch wychodzący z Internetem będą kierowane do lokalnego.</span><span class="sxs-lookup"><span data-stu-id="df365-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed to on-premises.</span></span> <span data-ttu-id="df365-165">Protokołu RDP/SSH z Internetu do maszyny Wirtualnej może nie działać z tym ustawieniem, w zależności od tego, jak lokalną obsługuje ten ruch.</span><span class="sxs-lookup"><span data-stu-id="df365-165">RDP/SSH from Internet to your VM may not work with this setting, depending on how the on-premises handles this traffic.</span></span> 
  <span data-ttu-id="df365-166">Tunelowanie wymuszone można włączyć:</span><span class="sxs-lookup"><span data-stu-id="df365-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="df365-167">Jeśli przy użyciu sieci VPN typu lokacja lokacja, ustawiając trasy zdefiniowane przez użytkownika (przez) z Typ następnego przeskoku jako brama sieci VPN</span><span class="sxs-lookup"><span data-stu-id="df365-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="df365-168">Jeśli trasa domyślna jest anonsowana za pośrednictwem protokołu BGP</span><span class="sxs-lookup"><span data-stu-id="df365-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="df365-169">Dla sieci wirtualnej komunikacji równorzędnej ruchu działał prawidłowo, trasa systemu o **Typ następnego przeskoku** *VNetPeering* musi istnieć dla zakresu prefiksu peered sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="df365-169">For VNet peering traffic to work correctly, a system route with **nextHopType** *VNetPeering* must exist for the peered VNet’s prefix range.</span></span> <span data-ttu-id="df365-170">Jeśli taka trasa nie istnieje, a łącze sieci wirtualnej komunikacji równorzędnej wygląda OK:</span><span class="sxs-lookup"><span data-stu-id="df365-170">If such a route doesn’t exist and the VNet peering link looks OK:</span></span>
  * <span data-ttu-id="df365-171">Poczekaj kilka sekund, a następnie spróbuj ponownie, jeśli jest to nowo utworzonego łącze komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="df365-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="df365-172">Od czasu do czasu zajmuje więcej czasu propagowania tras dla wszystkich interfejsów sieciowych w podsieci.</span><span class="sxs-lookup"><span data-stu-id="df365-172">It occasionally takes longer to propagate routes to all the network interfaces in a subnet.</span></span>
  * <span data-ttu-id="df365-173">Zasady grupy zabezpieczeń sieci (NSG) może mieć wpływ na przepływów ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="df365-173">Network Security Group (NSG) rules may be impacting the traffic flows.</span></span> <span data-ttu-id="df365-174">Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z grup zabezpieczeń sieci](virtual-network-nsg-troubleshoot-powershell.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="df365-174">For more information, see the [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

