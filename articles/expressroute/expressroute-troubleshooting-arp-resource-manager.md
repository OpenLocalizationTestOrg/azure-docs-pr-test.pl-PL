---
title: "Pobieranie ARP tabel: Menedżer zasobów: Azure ExpressRoute Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje pobierania hello ARP tabel dla obwodu usługi ExpressRoute"
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
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a><span data-ttu-id="3f9a9-103">Pobieranie ARP tabele w modelu wdrażania usługi Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="3f9a9-103">Getting ARP tables in hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3f9a9-104">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3f9a9-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="3f9a9-105">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="3f9a9-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="3f9a9-106">W tym artykule przedstawiono hello kroki toolearn powitalne ARP tabel dla obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-106">This article walks you through hello steps toolearn hello ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3f9a9-107">Ten dokument jest zamierzone toohelp zdiagnozować i rozwiązać problemy z prostego.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="3f9a9-108">Nie jest zamierzone toobe zastępczy pomocy technicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="3f9a9-109">Należy otworzyć bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) przypadku toosolve hello problem przy użyciu wskazówek hello opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable toosolve hello problem using hello guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="3f9a9-110">Tabele Resolution Protocol (ARP) i protokołu ARP adresów</span><span class="sxs-lookup"><span data-stu-id="3f9a9-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="3f9a9-111">Protokół ARP (Address Resolution Protocol) to protokół warstwy 2 zdefiniowane w [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="3f9a9-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="3f9a9-112">Protokół ARP jest używane toomap hello adres Ethernet (adresu MAC) z adresem ip.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-112">ARP is used toomap hello Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="3f9a9-113">Witaj tabeli protokołu ARP udostępnia mapowanie adresu ipv4 hello i adres MAC dla konkretnego komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-113">hello ARP table provides a mapping of hello ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="3f9a9-114">Witaj tabeli protokołu ARP dla obwodu usługi ExpressRoute komunikacji równorzędnej zapewnia hello następujące informacje dla każdego interfejsu (podstawowych i pomocniczych)</span><span class="sxs-lookup"><span data-stu-id="3f9a9-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="3f9a9-115">Mapowanie adresu MAC toohello adres ip lokalnego routera — interfejs</span><span class="sxs-lookup"><span data-stu-id="3f9a9-115">Mapping of on-premises router interface ip address toohello MAC address</span></span>
2. <span data-ttu-id="3f9a9-116">Mapowanie adresu MAC toohello adres ip ExpressRoute router — interfejs</span><span class="sxs-lookup"><span data-stu-id="3f9a9-116">Mapping of ExpressRoute router interface ip address toohello MAC address</span></span>
3. <span data-ttu-id="3f9a9-117">Wiek hello mapowania</span><span class="sxs-lookup"><span data-stu-id="3f9a9-117">Age of hello mapping</span></span>

<span data-ttu-id="3f9a9-118">Tabele ARP może pomóc sprawdzić poprawność konfiguracji warstwy 2 i rozwiązywanie problemów z podstawowych warstwy 2 problemy z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="3f9a9-119">Przykład tabeli protokołu ARP:</span><span class="sxs-lookup"><span data-stu-id="3f9a9-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="3f9a9-120">Witaj Poniższa sekcja zawiera informacje dotyczące sposobu wyświetlania hello tabele ARP widziana przez routery brzegowe ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-120">hello following section provides information on how you can view hello ARP tables seen by hello ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="3f9a9-121">Wymagania wstępne dotyczące uczenia tabele ARP</span><span class="sxs-lookup"><span data-stu-id="3f9a9-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="3f9a9-122">Sprawdź, czy powitania po zanim postęp w dalszych</span><span class="sxs-lookup"><span data-stu-id="3f9a9-122">Ensure that you have hello following before you progress further</span></span>

* <span data-ttu-id="3f9a9-123">Nieprawidłowa obwodu usługi expressroute skonfigurowana z co najmniej jeden komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="3f9a9-124">obwodu Hello musi być w pełni skonfigurowane przez dostawcę łączności hello.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="3f9a9-125">Użytkownik (lub dostawcą połączenia) należy skonfigurować co najmniej jeden z komunikacji hello równorzędnych (Azure publicznego prywatne, Azure i firmy Microsoft) w tym obwodzie.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-125">You (or your connectivity provider) must have configured at least one of hello peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="3f9a9-126">Zakresów adresów IP używanych do konfigurowania komunikacji hello równorzędnych (Azure publicznego prywatne, Azure i firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="3f9a9-126">IP address ranges used for configuring hello peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="3f9a9-127">Przejrzyj hello ip address przypisania przykłady w hello [strony wymagania routingu usługi ExpressRoute](expressroute-routing.md) tooget zrozumienia jak adresy ip są mapowane toointerfaces na Twojej stronie, a na powitania po stronie usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-127">Review hello ip address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how ip addresses are mapped toointerfaces on your side and on hello ExpressRoute side.</span></span> <span data-ttu-id="3f9a9-128">Informacje o konfiguracji komunikacji równorzędnej hello można uzyskać, przeglądając hello [strony konfiguracji komunikacji równorzędnej ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="3f9a9-128">You can get information on hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="3f9a9-129">Informacje z zespołem sieci / używany dostawca połączenia na adresy MAC hello interfejsów z tych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-129">Information from your networking team / connectivity provider on hello MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="3f9a9-130">Musi mieć hello najnowsze modułu PowerShell platformy Azure (wersja 1,50 lub nowsza).</span><span class="sxs-lookup"><span data-stu-id="3f9a9-130">You must have hello latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="3f9a9-131">Pobieranie hello ARP tabel dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3f9a9-131">Getting hello ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="3f9a9-132">Ta sekcja zawiera instrukcje dotyczące sposobu wyświetlania hello ARP tabel na komunikacji równorzędnej przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-132">This section provides instructions on how you can view hello ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="3f9a9-133">Użytkownik lub dostawcą połączenia należy skonfigurować przed osiągnięciem dalszej komunikacji równorzędnej hello.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-133">You or your connectivity provider must have configured hello peering before progressing further.</span></span> <span data-ttu-id="3f9a9-134">Każdy obwód ma dwie ścieżki (podstawowych i pomocniczych).</span><span class="sxs-lookup"><span data-stu-id="3f9a9-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="3f9a9-135">Możesz sprawdzić hello tabeli protokołu ARP dla każdej ścieżki niezależnie.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="3f9a9-136">Tabele ARP dla platformy Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="3f9a9-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="3f9a9-137">następujące polecenia cmdlet Hello zapewnia hello ARP tabel Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="3f9a9-137">hello following cmdlet provides hello ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="3f9a9-138">Przykładowe dane wyjściowe są wyświetlane poniżej dla jednej ze ścieżek hello</span><span class="sxs-lookup"><span data-stu-id="3f9a9-138">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="3f9a9-139">Tabele ARP dla platformy Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="3f9a9-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="3f9a9-140">następujące polecenia cmdlet Hello przewiduje hello ARP tabel Azure publicznej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="3f9a9-140">hello following cmdlet provides hello ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="3f9a9-141">Przykładowe dane wyjściowe są wyświetlane poniżej dla jednej ze ścieżek hello</span><span class="sxs-lookup"><span data-stu-id="3f9a9-141">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="3f9a9-142">Tabele ARP dla komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3f9a9-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="3f9a9-143">Witaj następujące polecenie cmdlet udostępnia hello ARP tabel dla komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3f9a9-143">hello following cmdlet provides hello ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="3f9a9-144">Przykładowe dane wyjściowe są wyświetlane poniżej dla jednej ze ścieżek hello</span><span class="sxs-lookup"><span data-stu-id="3f9a9-144">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="3f9a9-145">Jak toouse tych informacji</span><span class="sxs-lookup"><span data-stu-id="3f9a9-145">How toouse this information</span></span>
<span data-ttu-id="3f9a9-146">Witaj tabeli protokołu ARP komunikacji równorzędnej może służyć toodetermine Sprawdź poprawność konfiguracji warstwy 2 i połączenia.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-146">hello ARP table of a peering can be used toodetermine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="3f9a9-147">Ta sekcja zawiera omówienie wygląd tabele ARP w różnych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="3f9a9-148">Tabeli protokołu ARP, kiedy obwód jest w stan operacyjny (oczekiwany stan)</span><span class="sxs-lookup"><span data-stu-id="3f9a9-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="3f9a9-149">Witaj tabeli protokołu ARP będzie mieć wpis dla strony lokalne powitania z prawidłowym adresem IP i adres MAC i podobne objęcia powitania po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-149">hello ARP table will have an entry for hello on-premises side with a valid IP address and MAC address and a similar entry for hello Microsoft side.</span></span> 
* <span data-ttu-id="3f9a9-150">Witaj oktet ostatniego adresu ip lokalnymi hello zawsze jest liczbą nieparzystą.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-150">hello last octet of hello on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="3f9a9-151">Witaj oktet ostatniego hello adresu ip firmy Microsoft jest zawsze liczbą parzystą.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-151">hello last octet of hello Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="3f9a9-152">Witaj, wyświetlania tego samego adresu MAC na powitania po stronie firmy Microsoft dla wszystkich 3 komunikacji równorzędnych (podstawowy / dodatkowej).</span><span class="sxs-lookup"><span data-stu-id="3f9a9-152">hello same MAC address will appear on hello Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="3f9a9-153">Tabeli protokołu ARP, kiedy lokalnymi / po stronie dostawcy połączenie, ma problemy</span><span class="sxs-lookup"><span data-stu-id="3f9a9-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="3f9a9-154">Jeśli występują problemy z lokalne powitania lub dostawca połączenia zobaczysz, że albo tylko jeden wpis pojawi się w hello ARP tabeli lub hello lokalnego adres MAC będą wyświetlane niekompletne.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-154">If there are issues with hello on-premises or connectivity provider you may see that either only one entry will appear in hello ARP table or hello on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="3f9a9-155">Wyświetli hello mapowanie między hello adres MAC i adres IP używany w powitania po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-155">This will show hello mapping between hello MAC address and IP address used in hello Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="3f9a9-156">lub</span><span class="sxs-lookup"><span data-stu-id="3f9a9-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="3f9a9-157">Otwórz żądanie obsługi z Twojej toodebug dostawcy łączności takich problemów.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-157">Open a support request with your connectivity provider toodebug such issues.</span></span> <span data-ttu-id="3f9a9-158">Jeśli nie ma tabeli protokołu ARP hello adresy IP interfejsów hello zamapowane tooMAC adresy, hello Przejrzyj następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="3f9a9-158">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
> 
> 1. <span data-ttu-id="3f9a9-159">Jeśli hello pierwszy adres IP podsieci hello /30 hello łącza między hello MSEE PR a MSEE jest używana w hello interfejsu MSEE PR.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-159">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="3f9a9-160">Azure zawsze używa hello drugiego adresu IP dla MSEEs.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-160">Azure always uses hello second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="3f9a9-161">Upewnij się, jeśli powitania klienta (C-znacznik) i znaczniki sieci VLAN usługi (S-Tag) odpowiadają na pary MSEE PR i MSEE.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-161">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="3f9a9-162">Tabeli protokołu ARP problemów po stronie firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="3f9a9-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="3f9a9-163">Nie będą widzieć tabeli protokołu ARP wyświetlany dla komunikacji równorzędnej, jeśli występują problemy na powitania po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-163">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span> 
* <span data-ttu-id="3f9a9-164">Otwórz bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="3f9a9-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="3f9a9-165">Określ, czy masz problem z łącznością warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3f9a9-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f9a9-166">Next Steps</span></span>
* <span data-ttu-id="3f9a9-167">Sprawdź poprawność konfiguracji warstwy 3 dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3f9a9-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="3f9a9-168">Pobierz stan hello podsumowania toodetermine trasy sesje BGP</span><span class="sxs-lookup"><span data-stu-id="3f9a9-168">Get route summary toodetermine hello state of BGP sessions</span></span> 
  * <span data-ttu-id="3f9a9-169">Pobierz prefiksów, które są rozgłaszane między ExpressRoute toodetermine tabeli tras</span><span class="sxs-lookup"><span data-stu-id="3f9a9-169">Get route table toodetermine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="3f9a9-170">Zweryfikuj transferu danych, przeglądając bajtów we / wy</span><span class="sxs-lookup"><span data-stu-id="3f9a9-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="3f9a9-171">Otwórz bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) Jeśli nadal występują problemy.</span><span class="sxs-lookup"><span data-stu-id="3f9a9-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

