---
title: "Pobieranie ARP tabel: Menedżer zasobów: Azure ExpressRoute Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje dotyczące pobierania protokołu ARP tabel dla obwodu usługi ExpressRoute"
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: a65b1ba2998eae33b3e73bd2492fbbf025eb5946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-resource-manager-deployment-model"></a><span data-ttu-id="3d2d4-103">Pobieranie ARP tabele w modelu wdrażania usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3d2d4-103">Getting ARP tables in the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d2d4-104">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3d2d4-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="3d2d4-105">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="3d2d4-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="3d2d4-106">W tym artykule przedstawiono kroki, aby dowiedzieć się więcej tabel ARP dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-106">This article walks you through the steps to learn the ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3d2d4-107">Ten dokument jest przeznaczony ułatwiające diagnozowanie i rozwiązywanie problemów proste.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="3d2d4-108">Nie ma być zastępczy pomocy technicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="3d2d4-109">Należy otworzyć bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) Jeśli nie możesz rozwiązać problemu, przy użyciu wskazówek opisanych poniżej.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable to solve the problem using the guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="3d2d4-110">Tabele Resolution Protocol (ARP) i protokołu ARP adresów</span><span class="sxs-lookup"><span data-stu-id="3d2d4-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="3d2d4-111">Protokół ARP (Address Resolution Protocol) to protokół warstwy 2 zdefiniowane w [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="3d2d4-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="3d2d4-112">ARP są używane do mapowania adres Ethernet (adresu MAC) z adresem ip.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-112">ARP is used to map the Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="3d2d4-113">W tabeli protokołu ARP udostępnia mapowanie adresu ipv4 i adres MAC dla konkretnego komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-113">The ARP table provides a mapping of the ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="3d2d4-114">W tabeli protokołu ARP dla obwodu usługi ExpressRoute komunikacji równorzędnej zawiera następujące informacje dla każdego interfejsu (podstawowych i pomocniczych)</span><span class="sxs-lookup"><span data-stu-id="3d2d4-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="3d2d4-115">Mapowanie adresu ip interfejsu lokalnego routera z adresem MAC</span><span class="sxs-lookup"><span data-stu-id="3d2d4-115">Mapping of on-premises router interface ip address to the MAC address</span></span>
2. <span data-ttu-id="3d2d4-116">Mapowanie adresu ip interfejsu routera ExpressRoute adres MAC</span><span class="sxs-lookup"><span data-stu-id="3d2d4-116">Mapping of ExpressRoute router interface ip address to the MAC address</span></span>
3. <span data-ttu-id="3d2d4-117">Wiek mapowania</span><span class="sxs-lookup"><span data-stu-id="3d2d4-117">Age of the mapping</span></span>

<span data-ttu-id="3d2d4-118">Tabele ARP może pomóc sprawdzić poprawność konfiguracji warstwy 2 i rozwiązywanie problemów z podstawowych warstwy 2 problemy z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="3d2d4-119">Przykład tabeli protokołu ARP:</span><span class="sxs-lookup"><span data-stu-id="3d2d4-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="3d2d4-120">Poniższa sekcja zawiera informacje dotyczące sposobu wyświetlania tabele ARP widziana przez routery brzegowe ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-120">The following section provides information on how you can view the ARP tables seen by the ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="3d2d4-121">Wymagania wstępne dotyczące uczenia tabele ARP</span><span class="sxs-lookup"><span data-stu-id="3d2d4-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="3d2d4-122">Sprawdź, czy mają następujące przed postęp w dalszych</span><span class="sxs-lookup"><span data-stu-id="3d2d4-122">Ensure that you have the following before you progress further</span></span>

* <span data-ttu-id="3d2d4-123">Nieprawidłowa obwodu usługi expressroute skonfigurowana z co najmniej jeden komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="3d2d4-124">Obwód musi być w pełni skonfigurowane przez dostawcę łączności.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="3d2d4-125">Użytkownik (lub dostawcą połączenia) należy skonfigurować co najmniej jeden z komunikacji równorzędnych (Azure publicznego prywatne, Azure i firmy Microsoft) w tym obwodzie.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-125">You (or your connectivity provider) must have configured at least one of the peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="3d2d4-126">Zakresów adresów IP używanych do konfigurowania komunikacji równorzędnych (Azure publicznego prywatne, Azure i firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="3d2d4-126">IP address ranges used for configuring the peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="3d2d4-127">Przejrzyj przykłady przypisania adresów ip w [strony wymagania routingu usługi ExpressRoute](expressroute-routing.md) do zawierają opis sposobu adresy ip są mapowane na interfejsy użytkownika po stronie i po stronie usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-127">Review the ip address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how ip addresses are mapped to interfaces on your side and on the ExpressRoute side.</span></span> <span data-ttu-id="3d2d4-128">Można uzyskać informacji o konfiguracji komunikacji równorzędnej, przeglądając [strony konfiguracji komunikacji równorzędnej ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="3d2d4-128">You can get information on the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="3d2d4-129">Informacje z zespołem sieci / dostawca połączenia na adresach MAC interfejsy używane z tych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-129">Information from your networking team / connectivity provider on the MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="3d2d4-130">Musi mieć najnowsze modułu programu PowerShell dla platformy Azure (wersja 1,50 lub nowsza).</span><span class="sxs-lookup"><span data-stu-id="3d2d4-130">You must have the latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-the-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="3d2d4-131">Pobieranie protokołu ARP tabel dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3d2d4-131">Getting the ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="3d2d4-132">Ta sekcja zawiera instrukcje na sposób wyświetlania tabel ARP na komunikacji równorzędnej przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-132">This section provides instructions on how you can view the ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="3d2d4-133">Użytkownik lub dostawcą połączenia należy skonfigurować komunikację równorzędną przed osiągnięciem dodatkowe.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-133">You or your connectivity provider must have configured the peering before progressing further.</span></span> <span data-ttu-id="3d2d4-134">Każdy obwód ma dwie ścieżki (podstawowych i pomocniczych).</span><span class="sxs-lookup"><span data-stu-id="3d2d4-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="3d2d4-135">Można sprawdzić w tabeli protokołu ARP dla każdej ścieżki niezależnie.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="3d2d4-136">Tabele ARP dla platformy Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="3d2d4-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="3d2d4-137">Następujące polecenie cmdlet udostępnia protokołu ARP tabel dla platformy Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="3d2d4-137">The following cmdlet provides the ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="3d2d4-138">Przykładowe dane wyjściowe są wyświetlane poniżej dla jednej ze ścieżek</span><span class="sxs-lookup"><span data-stu-id="3d2d4-138">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="3d2d4-139">Tabele ARP dla platformy Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="3d2d4-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="3d2d4-140">Następujące polecenie cmdlet udostępnia protokołu ARP tabel dla platformy Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="3d2d4-140">The following cmdlet provides the ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="3d2d4-141">Przykładowe dane wyjściowe są wyświetlane poniżej dla jednej ze ścieżek</span><span class="sxs-lookup"><span data-stu-id="3d2d4-141">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="3d2d4-142">Tabele ARP dla komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3d2d4-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="3d2d4-143">Następujące polecenie cmdlet udostępnia protokołu ARP tabel dla komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3d2d4-143">The following cmdlet provides the ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="3d2d4-144">Przykładowe dane wyjściowe są wyświetlane poniżej dla jednej ze ścieżek</span><span class="sxs-lookup"><span data-stu-id="3d2d4-144">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="3d2d4-145">Jak używać tych informacji</span><span class="sxs-lookup"><span data-stu-id="3d2d4-145">How to use this information</span></span>
<span data-ttu-id="3d2d4-146">W tabeli protokołu ARP komunikacji równorzędnej może służyć do określenia Sprawdź poprawność konfiguracji warstwy 2 i połączenia.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-146">The ARP table of a peering can be used to determine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="3d2d4-147">Ta sekcja zawiera omówienie wygląd tabele ARP w różnych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="3d2d4-148">Tabeli protokołu ARP, kiedy obwód jest w stan operacyjny (oczekiwany stan)</span><span class="sxs-lookup"><span data-stu-id="3d2d4-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="3d2d4-149">W tabeli protokołu ARP będzie mieć wpis dla strony lokalnymi z prawidłowym adresem IP i adres MAC i podobne objęcia po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-149">The ARP table will have an entry for the on-premises side with a valid IP address and MAC address and a similar entry for the Microsoft side.</span></span> 
* <span data-ttu-id="3d2d4-150">Ostatni oktet lokalny adres ip zawsze jest liczbą nieparzystą.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-150">The last octet of the on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="3d2d4-151">Ostatni oktet adresu ip firmy Microsoft jest zawsze liczbą parzystą.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-151">The last octet of the Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="3d2d4-152">Ten sam adres MAC pojawią się po stronie firmy Microsoft dla wszystkich 3 komunikacji równorzędnych (podstawowy / dodatkowej).</span><span class="sxs-lookup"><span data-stu-id="3d2d4-152">The same MAC address will appear on the Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="3d2d4-153">Tabeli protokołu ARP, kiedy lokalnymi / po stronie dostawcy połączenie, ma problemy</span><span class="sxs-lookup"><span data-stu-id="3d2d4-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="3d2d4-154">Jeśli występują problemy z lokalnymi lub dostawca połączenia, które mogą być widoczne czy albo tylko jeden wpis pojawią się w tabeli protokołu ARP lub adres MAC lokalnego będą wyświetlane niekompletne.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-154">If there are issues with the on-premises or connectivity provider you may see that either only one entry will appear in the ARP table or the on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="3d2d4-155">Wyświetli mapowanie między adres MAC i adres IP używany po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-155">This will show the mapping between the MAC address and IP address used in the Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="3d2d4-156">lub</span><span class="sxs-lookup"><span data-stu-id="3d2d4-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="3d2d4-157">Otwórz żądanie obsługi z dostawcą połączenia debugowanie takich problemów.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-157">Open a support request with your connectivity provider to debug such issues.</span></span> <span data-ttu-id="3d2d4-158">Jeśli w tabeli protokołu ARP nie mają adresy IP interfejsów mapowane na adresy MAC, przejrzyj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="3d2d4-158">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
> 
> 1. <span data-ttu-id="3d2d4-159">Jeśli adres IP pierwszego /30 podsieci dla skojarzenia między MSEE PR i MSEE jest używany w interfejsie MSEE PR.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-159">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="3d2d4-160">Azure zawsze używa jako drugiego adresu IP dla MSEEs.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-160">Azure always uses the second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="3d2d4-161">Upewnij się, jeśli klienta (C-znacznik) oraz znaczników sieci VLAN usługi (S-Tag) zgodne na pary MSEE PR i MSEE.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-161">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="3d2d4-162">Tabeli protokołu ARP problemów po stronie firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3d2d4-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="3d2d4-163">Nie będą widzieć tabeli protokołu ARP wyświetlany dla komunikacji równorzędnej, jeśli występują problemy po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-163">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span> 
* <span data-ttu-id="3d2d4-164">Otwórz bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="3d2d4-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="3d2d4-165">Określ, czy masz problem z łącznością warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3d2d4-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d2d4-166">Next Steps</span></span>
* <span data-ttu-id="3d2d4-167">Sprawdź poprawność konfiguracji warstwy 3 dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3d2d4-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="3d2d4-168">Uzyskać podsumowanie do ustalenia stanu sesji BGP trasy</span><span class="sxs-lookup"><span data-stu-id="3d2d4-168">Get route summary to determine the state of BGP sessions</span></span> 
  * <span data-ttu-id="3d2d4-169">Pobierz tabelę tras, aby określić prefiksy, które są rozgłaszane między ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3d2d4-169">Get route table to determine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="3d2d4-170">Zweryfikuj transferu danych, przeglądając bajtów we / wy</span><span class="sxs-lookup"><span data-stu-id="3d2d4-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="3d2d4-171">Otwórz bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) Jeśli nadal występują problemy.</span><span class="sxs-lookup"><span data-stu-id="3d2d4-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

