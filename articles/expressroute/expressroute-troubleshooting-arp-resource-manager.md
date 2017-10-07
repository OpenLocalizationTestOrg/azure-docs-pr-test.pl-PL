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
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a>Pobieranie ARP tabele w modelu wdrażania usługi Resource Manager hello
> [!div class="op_single_selector"]
> * [Program PowerShell — model usługi Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell — model klasyczny](expressroute-troubleshooting-arp-classic.md)
> 
> 

W tym artykule przedstawiono hello kroki toolearn powitalne ARP tabel dla obwodu usługi ExpressRoute. 

> [!IMPORTANT]
> Ten dokument jest zamierzone toohelp zdiagnozować i rozwiązać problemy z prostego. Nie jest zamierzone toobe zastępczy pomocy technicznej firmy Microsoft. Należy otworzyć bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) przypadku toosolve hello problem przy użyciu wskazówek hello opisane poniżej.
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Tabele Resolution Protocol (ARP) i protokołu ARP adresów
Protokół ARP (Address Resolution Protocol) to protokół warstwy 2 zdefiniowane w [RFC 826](https://tools.ietf.org/html/rfc826). Protokół ARP jest używane toomap hello adres Ethernet (adresu MAC) z adresem ip.

Witaj tabeli protokołu ARP udostępnia mapowanie adresu ipv4 hello i adres MAC dla konkretnego komunikacji równorzędnej. Witaj tabeli protokołu ARP dla obwodu usługi ExpressRoute komunikacji równorzędnej zapewnia hello następujące informacje dla każdego interfejsu (podstawowych i pomocniczych)

1. Mapowanie adresu MAC toohello adres ip lokalnego routera — interfejs
2. Mapowanie adresu MAC toohello adres ip ExpressRoute router — interfejs
3. Wiek hello mapowania

Tabele ARP może pomóc sprawdzić poprawność konfiguracji warstwy 2 i rozwiązywanie problemów z podstawowych warstwy 2 problemy z połączeniem. 

Przykład tabeli protokołu ARP: 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


Witaj Poniższa sekcja zawiera informacje dotyczące sposobu wyświetlania hello tabele ARP widziana przez routery brzegowe ExpressRoute hello. 

## <a name="prerequisites-for-learning-arp-tables"></a>Wymagania wstępne dotyczące uczenia tabele ARP
Sprawdź, czy powitania po zanim postęp w dalszych

* Nieprawidłowa obwodu usługi expressroute skonfigurowana z co najmniej jeden komunikacji równorzędnej. obwodu Hello musi być w pełni skonfigurowane przez dostawcę łączności hello. Użytkownik (lub dostawcą połączenia) należy skonfigurować co najmniej jeden z komunikacji hello równorzędnych (Azure publicznego prywatne, Azure i firmy Microsoft) w tym obwodzie.
* Zakresów adresów IP używanych do konfigurowania komunikacji hello równorzędnych (Azure publicznego prywatne, Azure i firmy Microsoft). Przejrzyj hello ip address przypisania przykłady w hello [strony wymagania routingu usługi ExpressRoute](expressroute-routing.md) tooget zrozumienia jak adresy ip są mapowane toointerfaces na Twojej stronie, a na powitania po stronie usługi ExpressRoute. Informacje o konfiguracji komunikacji równorzędnej hello można uzyskać, przeglądając hello [strony konfiguracji komunikacji równorzędnej ExpressRoute](expressroute-howto-routing-arm.md).
* Informacje z zespołem sieci / używany dostawca połączenia na adresy MAC hello interfejsów z tych adresów IP.
* Musi mieć hello najnowsze modułu PowerShell platformy Azure (wersja 1,50 lub nowsza).

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a>Pobieranie hello ARP tabel dla obwodu usługi ExpressRoute
Ta sekcja zawiera instrukcje dotyczące sposobu wyświetlania hello ARP tabel na komunikacji równorzędnej przy użyciu programu PowerShell. Użytkownik lub dostawcą połączenia należy skonfigurować przed osiągnięciem dalszej komunikacji równorzędnej hello. Każdy obwód ma dwie ścieżki (podstawowych i pomocniczych). Możesz sprawdzić hello tabeli protokołu ARP dla każdej ścieżki niezależnie.

### <a name="arp-tables-for-azure-private-peering"></a>Tabele ARP dla platformy Azure prywatnej komunikacji równorzędnej
następujące polecenia cmdlet Hello zapewnia hello ARP tabel Azure prywatnej komunikacji równorzędnej

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

Przykładowe dane wyjściowe są wyświetlane poniżej dla jednej ze ścieżek hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Tabele ARP dla platformy Azure publicznej komunikacji równorzędnej
następujące polecenia cmdlet Hello przewiduje hello ARP tabel Azure publicznej komunikacji równorzędnej

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


Przykładowe dane wyjściowe są wyświetlane poniżej dla jednej ze ścieżek hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Tabele ARP dla komunikacji równorzędnej firmy Microsoft
Witaj następujące polecenie cmdlet udostępnia hello ARP tabel dla komunikacji równorzędnej firmy Microsoft

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


Przykładowe dane wyjściowe są wyświetlane poniżej dla jednej ze ścieżek hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Jak toouse tych informacji
Witaj tabeli protokołu ARP komunikacji równorzędnej może służyć toodetermine Sprawdź poprawność konfiguracji warstwy 2 i połączenia. Ta sekcja zawiera omówienie wygląd tabele ARP w różnych scenariuszach.

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a>Tabeli protokołu ARP, kiedy obwód jest w stan operacyjny (oczekiwany stan)
* Witaj tabeli protokołu ARP będzie mieć wpis dla strony lokalne powitania z prawidłowym adresem IP i adres MAC i podobne objęcia powitania po stronie firmy Microsoft. 
* Witaj oktet ostatniego adresu ip lokalnymi hello zawsze jest liczbą nieparzystą.
* Witaj oktet ostatniego hello adresu ip firmy Microsoft jest zawsze liczbą parzystą.
* Witaj, wyświetlania tego samego adresu MAC na powitania po stronie firmy Microsoft dla wszystkich 3 komunikacji równorzędnych (podstawowy / dodatkowej). 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a>Tabeli protokołu ARP, kiedy lokalnymi / po stronie dostawcy połączenie, ma problemy
Jeśli występują problemy z lokalne powitania lub dostawca połączenia zobaczysz, że albo tylko jeden wpis pojawi się w hello ARP tabeli lub hello lokalnego adres MAC będą wyświetlane niekompletne. Wyświetli hello mapowanie między hello adres MAC i adres IP używany w powitania po stronie firmy Microsoft. 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

lub
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> Otwórz żądanie obsługi z Twojej toodebug dostawcy łączności takich problemów. Jeśli nie ma tabeli protokołu ARP hello adresy IP interfejsów hello zamapowane tooMAC adresy, hello Przejrzyj następujące informacje:
> 
> 1. Jeśli hello pierwszy adres IP podsieci hello /30 hello łącza między hello MSEE PR a MSEE jest używana w hello interfejsu MSEE PR. Azure zawsze używa hello drugiego adresu IP dla MSEEs.
> 2. Upewnij się, jeśli powitania klienta (C-znacznik) i znaczniki sieci VLAN usługi (S-Tag) odpowiadają na pary MSEE PR i MSEE.
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a>Tabeli protokołu ARP problemów po stronie firmy Microsoft
* Nie będą widzieć tabeli protokołu ARP wyświetlany dla komunikacji równorzędnej, jeśli występują problemy na powitania po stronie firmy Microsoft. 
* Otwórz bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Określ, czy masz problem z łącznością warstwy 2. 

## <a name="next-steps"></a>Następne kroki
* Sprawdź poprawność konfiguracji warstwy 3 dla obwodu usługi ExpressRoute
  * Pobierz stan hello podsumowania toodetermine trasy sesje BGP 
  * Pobierz prefiksów, które są rozgłaszane między ExpressRoute toodetermine tabeli tras
* Zweryfikuj transferu danych, przeglądając bajtów we / wy
* Otwórz bilet pomocy technicznej z [pomocy technicznej firmy Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) Jeśli nadal występują problemy.

