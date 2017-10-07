---
title: trasy aaaTroubleshoot - PowerShell | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tootroubleshoot trasy w modelu wdrażania usługi Azure Resource Manager hello przy użyciu programu Azure PowerShell."
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
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="33bc9-103">Rozwiązywanie problemów z tras za pomocą programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="33bc9-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33bc9-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="33bc9-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="33bc9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="33bc9-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="33bc9-106">Jeśli występują tooor problemy dotyczące łączności sieciowej z sieci maszyny wirtualnej Azure (VM), tras może mieć wpływ na Twoje ruch maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="33bc9-106">If you are experiencing network connectivity issues tooor from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="33bc9-107">Ten artykuł zawiera omówienie funkcji diagnostyki dla tras toohelp dalsze poszukiwanie rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="33bc9-107">This article provides an overview of diagnostics capabilities for routes toohelp troubleshoot further.</span></span>

<span data-ttu-id="33bc9-108">Tabele tras są skojarzone z podsieciami i obowiązują na wszystkich interfejsach sieciowych (NIC) w tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="33bc9-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="33bc9-109">następujące typy tras Hello może być zastosowane tooeach interfejsu sieciowego:</span><span class="sxs-lookup"><span data-stu-id="33bc9-109">hello following types of routes can be applied tooeach network interface:</span></span>

* <span data-ttu-id="33bc9-110">**Trasy systemowe:** Domyślnie każda podsieć utworzona w sieci wirtualnej platformy Azure (VNet) ma tabel tras systemu, które umożliwiają lokalnej sieci wirtualnej ruch, ruch lokalnej za pośrednictwem bramy sieci VPN i ruchu internetowego.</span><span class="sxs-lookup"><span data-stu-id="33bc9-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="33bc9-111">Istnieją również tras systemowych dla połączyć za pomocą sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="33bc9-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="33bc9-112">**Trasy protokołu BGP:** propagowane interfejsów toonetwork za pośrednictwem usługi ExpressRoute lub połączeń VPN lokacja lokacja.</span><span class="sxs-lookup"><span data-stu-id="33bc9-112">**BGP routes:** Propagated toonetwork interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="33bc9-113">Dowiedz się więcej o routingu BGP, odczytując hello [protokołu BGP z bramy sieci VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) i [omówienie ExpressRoute](../expressroute/expressroute-introduction.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="33bc9-113">Learn more about BGP routing by reading hello [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="33bc9-114">**Trasy zdefiniowane przez użytkownika (przez):** Jeśli używasz wirtualnych urządzeń sieciowych lub są wymuszone tunelowanie ruchu tooan sieci lokalnej za pośrednictwem sieci VPN lokacja lokacja, może być zdefiniowana przez użytkownika tras (Udr) skojarzone z tabeli tras podsieci.</span><span class="sxs-lookup"><span data-stu-id="33bc9-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic tooan on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="33bc9-115">Jeśli nie masz doświadczenia w obsłudze Udr, przeczytaj hello [trasy zdefiniowane przez użytkownika](virtual-networks-udr-overview.md#user-defined-routes) artykułu.</span><span class="sxs-lookup"><span data-stu-id="33bc9-115">If you're not familiar with UDRs, read hello [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="33bc9-116">Z hello różne trasy, które mogą być zastosowane tooa interfejsu sieciowego, może być trudne toodetermine obowiązują agregacji trasy.</span><span class="sxs-lookup"><span data-stu-id="33bc9-116">With hello various routes that can be applied tooa network interface, it can be difficult toodetermine which aggregate routes are effective.</span></span> <span data-ttu-id="33bc9-117">toohelp rozwiązywania problemów z połączeniami sieci maszyny Wirtualnej, można wyświetlić wszystkie hello skuteczne trasy dla interfejsu sieciowego w modelu wdrażania usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="33bc9-117">toohelp troubleshoot VM network connectivity, you can view all hello effective routes for a network interface in hello Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="33bc9-118">Przy użyciu przepływu ruchu maszyny Wirtualnej tootroubleshoot skuteczne tras</span><span class="sxs-lookup"><span data-stu-id="33bc9-118">Using Effective Routes tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="33bc9-119">W tym artykule wykorzystano powitania po scenariusz jako tooillustrate przykład, jak skuteczne hello tootroubleshoot trasy dla interfejsu sieciowego:</span><span class="sxs-lookup"><span data-stu-id="33bc9-119">This article uses hello following scenario as an example tooillustrate how tootroubleshoot hello effective routes for a network interface:</span></span>

<span data-ttu-id="33bc9-120">Maszyna wirtualna (*VM1*) połączony toohello sieci wirtualnej (*VNet1*, prefiks: 10.9.0.0/16) nie powiedzie się tooa tooconnect VM(VM3) w nowo peered sieci wirtualnej (*VNet3*, prefiks 10.10.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="33bc9-120">A VM (*VM1*) connected toohello VNet (*VNet1*, prefix: 10.9.0.0/16) fails tooconnect tooa VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="33bc9-121">Brak Udr lub BGP kieruje zastosowane NIC1 tooVM1 sieci interfejs podłączony toohello maszyny Wirtualnej, są stosowane tylko tras systemowych.</span><span class="sxs-lookup"><span data-stu-id="33bc9-121">There are no UDRs or BGP routes applied tooVM1-NIC1 network interface connected toohello VM, only system routes are applied.</span></span>

<span data-ttu-id="33bc9-122">W tym artykule opisano, jak toodetermine hello. Przyczyna niepowodzenia połączenia hello przy użyciu możliwości wprowadzenia trasy w modelu wdrażania zarządzania zasobami Azure.</span><span class="sxs-lookup"><span data-stu-id="33bc9-122">This article explains how toodetermine hello cause of hello connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="33bc9-123">Gdy hello przykładzie użyto tylko tras systemowych, hello te same kroki można używane toodetermine błędów połączenia przychodzącego i wychodzącego przez dowolnego typu trasy.</span><span class="sxs-lookup"><span data-stu-id="33bc9-123">While hello example uses only system routes, hello same steps can be used toodetermine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="33bc9-124">Jeśli maszyna wirtualna ma więcej niż jedną kartę Sieciową podłączoną, sprawdź skuteczne trasy dla każdego hello tooand sieci toodiagnose kart sieciowych problemy dotyczące łączności z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="33bc9-124">If your VM has more than one NIC attached, check effective routes for each of hello NICs toodiagnose network connectivity issues tooand from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="33bc9-125">Widok skuteczne trasy dla maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="33bc9-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="33bc9-126">toosee hello agregacji tras, na których są stosowane tooa maszyny Wirtualnej, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="33bc9-126">toosee hello aggregate routes that are applied tooa VM, complete hello following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="33bc9-127">Widok skuteczne trasy dla interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="33bc9-127">View effective routes for a network interface</span></span>
<span data-ttu-id="33bc9-128">toosee hello agregacji tras, na których są stosowane tooa interfejsu sieciowego, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="33bc9-128">toosee hello aggregate routes that are applied tooa network interface, complete hello following steps:</span></span>

1. <span data-ttu-id="33bc9-129">Uruchom tooAzure sesji i logowania programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33bc9-129">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="33bc9-130">Jeśli nie masz doświadczenia w obsłudze programu Azure PowerShell, przeczytaj hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="33bc9-130">If you’re not familiar with Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="33bc9-131">Witaj poniższe polecenie zwraca wszystkie trasy stosowane tooa sieciowej o nazwie *VM1 NIC1* w grupie zasobów hello *RG1*.</span><span class="sxs-lookup"><span data-stu-id="33bc9-131">hello following command returns all routes applied tooa network interface named *VM1-NIC1* in hello resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="33bc9-132">Jeśli nie znasz nazwy hello interfejsu sieciowego, wpisz hello następujące nazwy hello tooretrieve poleceń wszystkie interfejsy sieciowe group.* zasobów</span><span class="sxs-lookup"><span data-stu-id="33bc9-132">If you don’t know hello name of a network interface, type hello following command tooretrieve hello names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="33bc9-133">Witaj następujące dane wyjściowe wyglądają podobne toohello dane wyjściowe dla każdej trasy stosowane hello podsieci toohello, karta sieciowa jest połączona z:</span><span class="sxs-lookup"><span data-stu-id="33bc9-133">hello following output looks similar toohello output for each route applied toohello subnet hello NIC is connected to:</span></span>
   
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
   
   <span data-ttu-id="33bc9-134">Zwróć uwagę hello następujących danych wyjściowych hello:</span><span class="sxs-lookup"><span data-stu-id="33bc9-134">Notice hello following in hello output:</span></span>
   
   * <span data-ttu-id="33bc9-135">**Nazwa**: Nazwa trasy efektywne hello może być pusty, chyba że jawnie określone dla tras zdefiniowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="33bc9-135">**Name**: Name of hello effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="33bc9-136">**Stan**: wskazuje stan hello skuteczne trasy.</span><span class="sxs-lookup"><span data-stu-id="33bc9-136">**State**: Indicates state of hello effective route.</span></span> <span data-ttu-id="33bc9-137">Możliwe wartości to "Active" lub "Nieprawidłowe"</span><span class="sxs-lookup"><span data-stu-id="33bc9-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="33bc9-138">**AddressPrefixes**: Określa prefiks adresu hello hello skuteczne trasy w notacji CIDR.</span><span class="sxs-lookup"><span data-stu-id="33bc9-138">**AddressPrefixes**: Specifies hello address prefix of hello effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="33bc9-139">**Typ następnego przeskoku**: wskazuje hello następnego skoku dla hello podane trasy.</span><span class="sxs-lookup"><span data-stu-id="33bc9-139">**nextHopType**: Indicates hello next hop for hello given route.</span></span> <span data-ttu-id="33bc9-140">Możliwe wartości to *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, lub *Null*.</span><span class="sxs-lookup"><span data-stu-id="33bc9-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="33bc9-141">Wartość *Null* dla **Typ następnego przeskoku** przez może oznaczać nieprawidłową trasy.</span><span class="sxs-lookup"><span data-stu-id="33bc9-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="33bc9-142">Na przykład jeśli **Typ następnego przeskoku** jest *VirtualAppliance* i urządzenie wirtualne sieci hello maszyna wirtualna nie jest w stanie zainicjowano obsługę administracyjną uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="33bc9-142">For example, if **nextHopType** is *VirtualAppliance* and hello network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="33bc9-143">Jeśli **Typ następnego przeskoku** jest *właściwość VPNGateway* i nie Brak bramy elastycznie/uruchomiony w hello podanej sieci wirtualnej, trasa hello mogą być nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="33bc9-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in hello given VNet, hello route may become invalid.</span></span>
   * <span data-ttu-id="33bc9-144">**Adres IP następnego przeskoku**: Określa adres IP następnego przeskoku trasy efektywne hello hello hello.</span><span class="sxs-lookup"><span data-stu-id="33bc9-144">**NextHopIpAddress**: Specifies hello IP address of hello next hop of hello effective route.</span></span>
   
   <span data-ttu-id="33bc9-145">Witaj poniższe polecenie zwraca trasy hello łatwiejsze tabeli tooview:</span><span class="sxs-lookup"><span data-stu-id="33bc9-145">hello following command returns hello routes in an easier tooview table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="33bc9-146">Hello następujące dane wyjściowe są niektóre hello danych wyjściowych dla scenariusza hello opisanych powyżej:</span><span class="sxs-lookup"><span data-stu-id="33bc9-146">hello following output is some of hello output received for hello scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="33bc9-147">Nie istnieje żadne toohello trasy wymienione *WestUS VNet3* sieciami wirtualnymi (prefiks 10.10.0.0/16)** z *WestUS VNet1* (prefiksu 10.9.0.0/16) w danych wyjściowych hello hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="33bc9-147">There is no route listed toohello *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in hello output from hello previous step.</span></span> <span data-ttu-id="33bc9-148">Jak pokazano na poniższej ilustracji hello, hello sieci wirtualnej komunikacji równorzędnej łącza z hello *WestUS VNet3* sieci wirtualnej jest w hello *Rozłączono* stanu.</span><span class="sxs-lookup"><span data-stu-id="33bc9-148">As shown in hello following picture, hello VNet peering link with hello *WestUS-VNet3* VNet is in hello *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="33bc9-149">Hello łącze dwukierunkowe dla komunikacji równorzędnej hello jest uszkodzona, który wyjaśnia dlaczego VM1 nie może połączyć tooVM3 w hello *WestUS VNet3* sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="33bc9-149">hello bi-directional link for hello peering is broken, which explains why VM1 could not connect tooVM3 in hello *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="33bc9-150">Konfiguracja dwukierunkowe sieci wirtualnej komunikacji równorzędnej łącze ponownie *WestUS VNet1* i *WestUS VNet3* sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="33bc9-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="33bc9-151">Witaj dane wyjściowe zwrócone w wyniku hello sieci wirtualnej komunikacji równorzędnej łącze jest poprawnie ustanowić następujące:</span><span class="sxs-lookup"><span data-stu-id="33bc9-151">hello output returned after hello VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="33bc9-152">Po określeniu hello problem, można dodać, usunąć, lub zmień tras i tabel tras.</span><span class="sxs-lookup"><span data-stu-id="33bc9-152">Once you determine hello issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="33bc9-153">Hello wpisz następujące polecenie toosee listę poleceń hello używane toodo tak:</span><span class="sxs-lookup"><span data-stu-id="33bc9-153">Type hello following command toosee a list of hello commands used toodo so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="33bc9-154">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="33bc9-154">Considerations</span></span>
<span data-ttu-id="33bc9-155">Zwrócono kilka rzeczy tookeep pamiętać podczas przeglądania listy hello tras:</span><span class="sxs-lookup"><span data-stu-id="33bc9-155">A few things tookeep in mind when reviewing hello list of routes returned:</span></span>

* <span data-ttu-id="33bc9-156">Routing jest oparta na Najdłuższy prefiks dopasowania (LPM) Wybierane spośród Udr, trasy protokołu BGP i systemu.</span><span class="sxs-lookup"><span data-stu-id="33bc9-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="33bc9-157">Jeśli istnieje więcej niż jedna trasa z hello sam LPM zgodne, a następnie, wybór trasy odbywa się w następującej kolejności hello:</span><span class="sxs-lookup"><span data-stu-id="33bc9-157">If there is more than one route with hello same LPM match, then a route is selected based on its origin in hello following order:</span></span>
  
  * <span data-ttu-id="33bc9-158">Trasa zdefiniowana przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="33bc9-158">User-defined route</span></span>
  * <span data-ttu-id="33bc9-159">Trasa protokołu BGP</span><span class="sxs-lookup"><span data-stu-id="33bc9-159">BGP route</span></span>
  * <span data-ttu-id="33bc9-160">Trasa systemowa (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="33bc9-160">System (Default) route</span></span>
    
    <span data-ttu-id="33bc9-161">Skuteczne trasy może zobaczyć tylko skuteczne ścieżek, które są oparte na wszystkich tras dostępnego hello dopasowaniem LPM.</span><span class="sxs-lookup"><span data-stu-id="33bc9-161">With effective routes, you can only see effective routes that are LPM match based on all hello availble routes.</span></span> <span data-ttu-id="33bc9-162">Przez pokazanie, jak trasy hello faktycznie są oceniane pod kątem danej karty Sieciowej, ułatwia to znacznie łatwiejsze trasy określonych tootroubleshoot, które mogą mieć wpływ na łączność z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="33bc9-162">By showing how hello routes are actually evaluated for a given NIC, this makes it a lot easier tootroubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="33bc9-163">Jeśli masz Udr i wysyłania ruchu tooa sieci urządzenie wirtualne (NVA) z *VirtualAppliance* jako **Typ następnego przeskoku**, upewnij się, że przesyłanie dalej IP jest włączona na odbieranie ruchu hello hello NVA lub pakiety są usuwane.</span><span class="sxs-lookup"><span data-stu-id="33bc9-163">If you have UDRs and are sending traffic tooa network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on hello NVA receiving hello traffic or packets are dropped.</span></span> 
* <span data-ttu-id="33bc9-164">Włączenie tunelowania wymuszony cały ruch wychodzący z Internetem będzie routingiem tooon firmą.</span><span class="sxs-lookup"><span data-stu-id="33bc9-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed tooon-premises.</span></span> <span data-ttu-id="33bc9-165">Protokołu RDP/SSH z tooyour Internet, maszyna wirtualna może nie działać to ustawienie, w zależności od sposobu hello lokalnymi obsługuje ten ruch.</span><span class="sxs-lookup"><span data-stu-id="33bc9-165">RDP/SSH from Internet tooyour VM may not work with this setting, depending on how hello on-premises handles this traffic.</span></span> 
  <span data-ttu-id="33bc9-166">Tunelowanie wymuszone można włączyć:</span><span class="sxs-lookup"><span data-stu-id="33bc9-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="33bc9-167">Jeśli przy użyciu sieci VPN typu lokacja lokacja, ustawiając trasy zdefiniowane przez użytkownika (przez) z Typ następnego przeskoku jako brama sieci VPN</span><span class="sxs-lookup"><span data-stu-id="33bc9-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="33bc9-168">Jeśli trasa domyślna jest anonsowana za pośrednictwem protokołu BGP</span><span class="sxs-lookup"><span data-stu-id="33bc9-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="33bc9-169">Dla sieci równorzędne — ruch toowork poprawnie, trasa systemu o **Typ następnego przeskoku** *VNetPeering* musi istnieć na powitania połączyć za pomocą sieci wirtualnej firmy prefiks zakresu.</span><span class="sxs-lookup"><span data-stu-id="33bc9-169">For VNet peering traffic toowork correctly, a system route with **nextHopType** *VNetPeering* must exist for hello peered VNet’s prefix range.</span></span> <span data-ttu-id="33bc9-170">Jeśli taka trasa nie istnieje i hello sieci wirtualnej komunikacji równorzędnej łącze wygląda OK:</span><span class="sxs-lookup"><span data-stu-id="33bc9-170">If such a route doesn’t exist and hello VNet peering link looks OK:</span></span>
  * <span data-ttu-id="33bc9-171">Poczekaj kilka sekund, a następnie spróbuj ponownie, jeśli jest to nowo utworzonego łącze komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="33bc9-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="33bc9-172">Od czasu do czasu zajmuje dłużej tras toopropagate interfejsów sieciowych hello tooall w podsieci.</span><span class="sxs-lookup"><span data-stu-id="33bc9-172">It occasionally takes longer toopropagate routes tooall hello network interfaces in a subnet.</span></span>
  * <span data-ttu-id="33bc9-173">Zasady grupy zabezpieczeń sieci (NSG) może mieć wpływ na powitania przepływów ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="33bc9-173">Network Security Group (NSG) rules may be impacting hello traffic flows.</span></span> <span data-ttu-id="33bc9-174">Aby uzyskać więcej informacji, zobacz hello [Rozwiązywanie problemów z grup zabezpieczeń sieci](virtual-network-nsg-troubleshoot-powershell.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="33bc9-174">For more information, see hello [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

