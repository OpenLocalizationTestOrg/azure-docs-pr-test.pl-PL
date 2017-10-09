---
title: "Pobieranie ARP tabel: klasycznym: Azure ExpressRoute Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera instrukcje dotyczące pobierania hello ARP tabel dla obwodu usługi ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a><span data-ttu-id="e26ff-103">Pobieranie tabel ARP w hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="e26ff-103">Getting ARP tables in hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e26ff-104">Program PowerShell — model usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e26ff-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="e26ff-105">PowerShell — model klasyczny</span><span class="sxs-lookup"><span data-stu-id="e26ff-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="e26ff-106">W tym artykule przedstawiono kroki hello pobieranie hello protokołu ARP (Address Resolution Protocol) tabel dla obwodu usługi ExpressRoute Azure.</span><span class="sxs-lookup"><span data-stu-id="e26ff-106">This article walks you through hello steps for getting hello Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e26ff-107">Ten dokument jest zamierzone toohelp zdiagnozować i rozwiązać problemy z prostego.</span><span class="sxs-lookup"><span data-stu-id="e26ff-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="e26ff-108">Nie jest zamierzone toobe zastępczy pomocy technicznej firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e26ff-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="e26ff-109">Jeśli nie możesz rozwiązać problemu hello przy użyciu hello następujące wytyczne, otwórz żądanie pomocy technicznej o [Microsoft Azure Pomoc i obsługa techniczna](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="e26ff-109">If you can't solve hello problem by using hello following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="e26ff-110">Tabele Resolution Protocol (ARP) i protokołu ARP adresów</span><span class="sxs-lookup"><span data-stu-id="e26ff-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="e26ff-111">ARP to protokół warstwy 2, który jest zdefiniowany w [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="e26ff-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="e26ff-112">Protokół ARP jest używane toomap adresu IP (adres MAC) tooan Ethernet.</span><span class="sxs-lookup"><span data-stu-id="e26ff-112">ARP is used toomap an Ethernet address (MAC address) tooan IP address.</span></span>

<span data-ttu-id="e26ff-113">Tabeli protokołu ARP udostępnia mapowanie adresu IPv4 hello i adres MAC dla konkretnego komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="e26ff-113">An ARP table provides a mapping of hello IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="e26ff-114">Witaj tabeli protokołu ARP dla obwodu usługi ExpressRoute komunikacji równorzędnej zapewnia hello następujące informacje dla każdego interfejsu (podstawowych i pomocniczych):</span><span class="sxs-lookup"><span data-stu-id="e26ff-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="e26ff-115">Mapowanie lokalnego interfejsu adres IP routera adres tooa MAC</span><span class="sxs-lookup"><span data-stu-id="e26ff-115">Mapping of an on-premises router interface IP address tooa MAC address</span></span>
2. <span data-ttu-id="e26ff-116">Mapowanie ExpressRoute interfejsu adres IP routera adres tooa MAC</span><span class="sxs-lookup"><span data-stu-id="e26ff-116">Mapping of an ExpressRoute router interface IP address tooa MAC address</span></span>
3. <span data-ttu-id="e26ff-117">wiek Hello hello mapowania</span><span class="sxs-lookup"><span data-stu-id="e26ff-117">hello age of hello mapping</span></span>

<span data-ttu-id="e26ff-118">Tabele ARP może pomóc z sprawdzanie poprawności konfiguracji warstwy 2 i rozwiązywanie problemów z podstawowych problemów z łącznością warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="e26ff-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="e26ff-119">Poniżej przedstawiono przykładowy tabeli protokołu ARP:</span><span class="sxs-lookup"><span data-stu-id="e26ff-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="e26ff-120">powitania po sekcji zawiera informacje dotyczące sposobu tooview hello ARP tabel, które są widoczne przez routery brzegowe ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="e26ff-120">hello following section provides information about how tooview hello ARP tables that are seen by hello ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="e26ff-121">Wymagania wstępne dotyczące korzystania z protokołu ARP tabel</span><span class="sxs-lookup"><span data-stu-id="e26ff-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="e26ff-122">Upewnij się, że masz następujące hello przed kontynuowaniem:</span><span class="sxs-lookup"><span data-stu-id="e26ff-122">Ensure that you have hello following before you continue:</span></span>

* <span data-ttu-id="e26ff-123">Nieprawidłowa obwodu ExpressRoute, skonfigurowanej z co najmniej jeden komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="e26ff-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="e26ff-124">obwodu Hello musi być w pełni skonfigurowane przez dostawcę łączności hello.</span><span class="sxs-lookup"><span data-stu-id="e26ff-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="e26ff-125">Użytkownik (lub dostawcą połączenia) należy skonfigurować co najmniej jeden z komunikacji hello równorzędnych (Azure publicznego prywatne, Azure lub Microsoft) w tym obwodzie.</span><span class="sxs-lookup"><span data-stu-id="e26ff-125">You (or your connectivity provider) must configure at least one of hello peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="e26ff-126">Zakresy adresów IP, które są używane do konfigurowania komunikacji hello równorzędnych (Azure publicznego prywatne, Azure i firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="e26ff-126">IP address ranges that are used for configuring hello peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="e26ff-127">Przejrzyj hello IP address przypisania przykłady w hello [strony wymagania routingu usługi ExpressRoute](expressroute-routing.md) tooget zrozumienia jak adresy IP są mapowane toointerfaces Twojego aise i po stronie ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="e26ff-127">Review hello IP address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how IP addresses are mapped toointerfaces on your aise and on hello ExpressRoute side.</span></span> <span data-ttu-id="e26ff-128">Informacje o konfiguracji komunikacji równorzędnej hello można uzyskać, przeglądając hello [strony konfiguracji komunikacji równorzędnej ExpressRoute](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="e26ff-128">You can get information about hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="e26ff-129">Informacje z dostawcą sieci zespołu lub łączności adresy MAC hello hello interfejsów, które są używane z tych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="e26ff-129">Information from your networking team or connectivity provider about hello MAC addresses of hello interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="e26ff-130">Witaj najnowsze moduł programu Windows PowerShell dla platformy Azure (wersja 1,50 lub nowsza).</span><span class="sxs-lookup"><span data-stu-id="e26ff-130">hello latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="e26ff-131">Tabele ARP dla obwodu usługi ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e26ff-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="e26ff-132">Ta sekcja zawiera instrukcje dotyczące sposobu tooview hello ARP tabel dla każdego typu komunikacji równorzędnej przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e26ff-132">This section provides instructions about how tooview hello ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="e26ff-133">Przed kontynuowaniem należy lub dostawcą połączenia musi tooconfigure hello komunikacji równorzędnej.</span><span class="sxs-lookup"><span data-stu-id="e26ff-133">Before you continue, either you or your connectivity provider needs tooconfigure hello peering.</span></span> <span data-ttu-id="e26ff-134">Każdy obwód ma dwie ścieżki (podstawowych i pomocniczych).</span><span class="sxs-lookup"><span data-stu-id="e26ff-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="e26ff-135">Możesz sprawdzić hello tabeli protokołu ARP dla każdej ścieżki niezależnie.</span><span class="sxs-lookup"><span data-stu-id="e26ff-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="e26ff-136">Tabele ARP dla platformy Azure prywatnej komunikacji równorzędnej</span><span class="sxs-lookup"><span data-stu-id="e26ff-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="e26ff-137">następujące polecenia cmdlet Hello zawiera hello ARP tabel Azure prywatnej komunikacji równorzędnej:</span><span class="sxs-lookup"><span data-stu-id="e26ff-137">hello following cmdlet provides hello ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="e26ff-138">Poniżej przedstawiono przykładowe dane wyjściowe dla jednej ze ścieżek hello:</span><span class="sxs-lookup"><span data-stu-id="e26ff-138">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="e26ff-139">Tabele ARP dla platformy Azure publicznej komunikacji równorzędnej:</span><span class="sxs-lookup"><span data-stu-id="e26ff-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="e26ff-140">następujące polecenia cmdlet Hello zawiera hello ARP tabel Azure publicznej komunikacji równorzędnej:</span><span class="sxs-lookup"><span data-stu-id="e26ff-140">hello following cmdlet provides hello ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="e26ff-141">Poniżej przedstawiono przykładowe dane wyjściowe dla jednej ze ścieżek hello:</span><span class="sxs-lookup"><span data-stu-id="e26ff-141">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="e26ff-142">Poniżej przedstawiono przykładowe dane wyjściowe dla jednej ze ścieżek hello:</span><span class="sxs-lookup"><span data-stu-id="e26ff-142">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="e26ff-143">Tabele ARP dla komunikacji równorzędnej firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="e26ff-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="e26ff-144">Witaj następujące polecenie cmdlet udostępnia hello ARP tabel dla komunikacji równorzędnej firmy Microsoft:</span><span class="sxs-lookup"><span data-stu-id="e26ff-144">hello following cmdlet provides hello ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="e26ff-145">Poniżej przedstawiono przykładowe dane wyjściowe dla jednej ze ścieżek hello:</span><span class="sxs-lookup"><span data-stu-id="e26ff-145">Sample output is shown below for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="e26ff-146">Jak toouse tych informacji</span><span class="sxs-lookup"><span data-stu-id="e26ff-146">How toouse this information</span></span>
<span data-ttu-id="e26ff-147">Hello tabeli protokołu ARP komunikacji równorzędnej może być używane toovalidate warstwy 2 konfiguracją i łącznością.</span><span class="sxs-lookup"><span data-stu-id="e26ff-147">hello ARP table of a peering can be used toovalidate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="e26ff-148">Ta sekcja zawiera omówienie wygląd tabele ARP w różnych scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="e26ff-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="e26ff-149">Tabeli protokołu ARP, kiedy obwód jest w stan operacyjny (oczekiwany)</span><span class="sxs-lookup"><span data-stu-id="e26ff-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="e26ff-150">Witaj tabeli protokołu ARP ma wpis dla strony lokalne powitania przy użyciu prawidłowego adresu IP i MAC, a podobne objęcia powitania po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e26ff-150">hello ARP table has an entry for hello on-premises side with a valid IP and MAC address, and a similar entry for hello Microsoft side.</span></span>
* <span data-ttu-id="e26ff-151">Witaj oktet ostatniego adresu IP lokalnymi hello zawsze jest liczbą nieparzystą.</span><span class="sxs-lookup"><span data-stu-id="e26ff-151">hello last octet of hello on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="e26ff-152">Witaj oktet ostatniego hello adresu IP firmy Microsoft jest zawsze liczbą parzystą.</span><span class="sxs-lookup"><span data-stu-id="e26ff-152">hello last octet of hello Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="e26ff-153">Witaj tego samego adresu MAC jest wyświetlana na powitania po stronie firmy Microsoft dla wszystkich trzech komunikacji równorzędnych (Podstawowe/pomocnicze).</span><span class="sxs-lookup"><span data-stu-id="e26ff-153">hello same MAC address appears on hello Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a><span data-ttu-id="e26ff-154">Tabeli protokołu ARP po lokalnymi lub gdy po stronie dostawcy łączności hello problemów</span><span class="sxs-lookup"><span data-stu-id="e26ff-154">ARP table when it's on-premises or when hello connectivity-provider side has problems</span></span>
 <span data-ttu-id="e26ff-155">W tabeli protokołu ARP hello pojawi się tylko jeden wpis.</span><span class="sxs-lookup"><span data-stu-id="e26ff-155">Only one entry appears in hello ARP table.</span></span> <span data-ttu-id="e26ff-156">Przedstawia on hello mapowanie między adres MAC hello i hello adres IP, który jest używany na powitania po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e26ff-156">It shows hello mapping between hello MAC address and hello IP address that's used on hello Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="e26ff-157">Jeśli wystąpi problem takie, otwórz obsługi żądania z Twojej tooresolve dostawcy łączności.</span><span class="sxs-lookup"><span data-stu-id="e26ff-157">If you experience an issue like this, open a support request with your connectivity provider tooresolve it.</span></span>
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a><span data-ttu-id="e26ff-158">Tabeli protokołu ARP problemów po powitania po stronie firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="e26ff-158">ARP table when hello Microsoft side has problems</span></span>
* <span data-ttu-id="e26ff-159">Nie będą widzieć tabeli protokołu ARP wyświetlany dla komunikacji równorzędnej, jeśli występują problemy na powitania po stronie firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e26ff-159">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span>
* <span data-ttu-id="e26ff-160">Otwórz żądanie pomocy technicznej o [Microsoft Azure Pomoc i obsługa techniczna](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="e26ff-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="e26ff-161">Określ, czy masz problem z łącznością warstwy 2.</span><span class="sxs-lookup"><span data-stu-id="e26ff-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e26ff-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e26ff-162">Next steps</span></span>
* <span data-ttu-id="e26ff-163">Sprawdź poprawność konfiguracji warstwy 3 dla obwodu usługi ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="e26ff-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="e26ff-164">Pobierz stan hello podsumowania toodetermine trasy sesje BGP.</span><span class="sxs-lookup"><span data-stu-id="e26ff-164">Get a route summary toodetermine hello state of BGP sessions.</span></span>
  * <span data-ttu-id="e26ff-165">Pobierz toodetermine tabeli tras, prefiksów, które są rozgłaszane między ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e26ff-165">Get a route table toodetermine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="e26ff-166">Zweryfikuj transferu danych, przeglądając bajtów i wylogowanie.</span><span class="sxs-lookup"><span data-stu-id="e26ff-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="e26ff-167">Otwórz żądanie pomocy technicznej o [Microsoft Azure Pomoc i obsługa techniczna](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) Jeśli nadal występują problemy.</span><span class="sxs-lookup"><span data-stu-id="e26ff-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

