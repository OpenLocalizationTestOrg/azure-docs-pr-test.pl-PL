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
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a>Pobieranie tabel ARP w hello klasycznego modelu wdrażania
> [!div class="op_single_selector"]
> * [Program PowerShell — model usługi Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell — model klasyczny](expressroute-troubleshooting-arp-classic.md)
> 
> 

W tym artykule przedstawiono kroki hello pobieranie hello protokołu ARP (Address Resolution Protocol) tabel dla obwodu usługi ExpressRoute Azure.

> [!IMPORTANT]
> Ten dokument jest zamierzone toohelp zdiagnozować i rozwiązać problemy z prostego. Nie jest zamierzone toobe zastępczy pomocy technicznej firmy Microsoft. Jeśli nie możesz rozwiązać problemu hello przy użyciu hello następujące wytyczne, otwórz żądanie pomocy technicznej o [Microsoft Azure Pomoc i obsługa techniczna](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Tabele Resolution Protocol (ARP) i protokołu ARP adresów
ARP to protokół warstwy 2, który jest zdefiniowany w [RFC 826](https://tools.ietf.org/html/rfc826). Protokół ARP jest używane toomap adresu IP (adres MAC) tooan Ethernet.

Tabeli protokołu ARP udostępnia mapowanie adresu IPv4 hello i adres MAC dla konkretnego komunikacji równorzędnej. Witaj tabeli protokołu ARP dla obwodu usługi ExpressRoute komunikacji równorzędnej zapewnia hello następujące informacje dla każdego interfejsu (podstawowych i pomocniczych):

1. Mapowanie lokalnego interfejsu adres IP routera adres tooa MAC
2. Mapowanie ExpressRoute interfejsu adres IP routera adres tooa MAC
3. wiek Hello hello mapowania

Tabele ARP może pomóc z sprawdzanie poprawności konfiguracji warstwy 2 i rozwiązywanie problemów z podstawowych problemów z łącznością warstwy 2.

Poniżej przedstawiono przykładowy tabeli protokołu ARP:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


powitania po sekcji zawiera informacje dotyczące sposobu tooview hello ARP tabel, które są widoczne przez routery brzegowe ExpressRoute hello.

## <a name="prerequisites-for-using-arp-tables"></a>Wymagania wstępne dotyczące korzystania z protokołu ARP tabel
Upewnij się, że masz następujące hello przed kontynuowaniem:

* Nieprawidłowa obwodu ExpressRoute, skonfigurowanej z co najmniej jeden komunikacji równorzędnej. obwodu Hello musi być w pełni skonfigurowane przez dostawcę łączności hello. Użytkownik (lub dostawcą połączenia) należy skonfigurować co najmniej jeden z komunikacji hello równorzędnych (Azure publicznego prywatne, Azure lub Microsoft) w tym obwodzie.
* Zakresy adresów IP, które są używane do konfigurowania komunikacji hello równorzędnych (Azure publicznego prywatne, Azure i firmy Microsoft). Przejrzyj hello IP address przypisania przykłady w hello [strony wymagania routingu usługi ExpressRoute](expressroute-routing.md) tooget zrozumienia jak adresy IP są mapowane toointerfaces Twojego aise i po stronie ExpressRoute hello. Informacje o konfiguracji komunikacji równorzędnej hello można uzyskać, przeglądając hello [strony konfiguracji komunikacji równorzędnej ExpressRoute](expressroute-howto-routing-classic.md).
* Informacje z dostawcą sieci zespołu lub łączności adresy MAC hello hello interfejsów, które są używane z tych adresów IP.
* Witaj najnowsze moduł programu Windows PowerShell dla platformy Azure (wersja 1,50 lub nowsza).

## <a name="arp-tables-for-your-expressroute-circuit"></a>Tabele ARP dla obwodu usługi ExpressRoute
Ta sekcja zawiera instrukcje dotyczące sposobu tooview hello ARP tabel dla każdego typu komunikacji równorzędnej przy użyciu programu PowerShell. Przed kontynuowaniem należy lub dostawcą połączenia musi tooconfigure hello komunikacji równorzędnej. Każdy obwód ma dwie ścieżki (podstawowych i pomocniczych). Możesz sprawdzić hello tabeli protokołu ARP dla każdej ścieżki niezależnie.

### <a name="arp-tables-for-azure-private-peering"></a>Tabele ARP dla platformy Azure prywatnej komunikacji równorzędnej
następujące polecenia cmdlet Hello zawiera hello ARP tabel Azure prywatnej komunikacji równorzędnej:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

Poniżej przedstawiono przykładowe dane wyjściowe dla jednej ze ścieżek hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Tabele ARP dla platformy Azure publicznej komunikacji równorzędnej:
następujące polecenia cmdlet Hello zawiera hello ARP tabel Azure publicznej komunikacji równorzędnej:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

Poniżej przedstawiono przykładowe dane wyjściowe dla jednej ze ścieżek hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Poniżej przedstawiono przykładowe dane wyjściowe dla jednej ze ścieżek hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Tabele ARP dla komunikacji równorzędnej firmy Microsoft
Witaj następujące polecenie cmdlet udostępnia hello ARP tabel dla komunikacji równorzędnej firmy Microsoft:

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


Poniżej przedstawiono przykładowe dane wyjściowe dla jednej ze ścieżek hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Jak toouse tych informacji
Hello tabeli protokołu ARP komunikacji równorzędnej może być używane toovalidate warstwy 2 konfiguracją i łącznością. Ta sekcja zawiera omówienie wygląd tabele ARP w różnych scenariuszach.

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a>Tabeli protokołu ARP, kiedy obwód jest w stan operacyjny (oczekiwany)
* Witaj tabeli protokołu ARP ma wpis dla strony lokalne powitania przy użyciu prawidłowego adresu IP i MAC, a podobne objęcia powitania po stronie firmy Microsoft.
* Witaj oktet ostatniego adresu IP lokalnymi hello zawsze jest liczbą nieparzystą.
* Witaj oktet ostatniego hello adresu IP firmy Microsoft jest zawsze liczbą parzystą.
* Witaj tego samego adresu MAC jest wyświetlana na powitania po stronie firmy Microsoft dla wszystkich trzech komunikacji równorzędnych (Podstawowe/pomocnicze).

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a>Tabeli protokołu ARP po lokalnymi lub gdy po stronie dostawcy łączności hello problemów
 W tabeli protokołu ARP hello pojawi się tylko jeden wpis. Przedstawia on hello mapowanie między adres MAC hello i hello adres IP, który jest używany na powitania po stronie firmy Microsoft.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> Jeśli wystąpi problem takie, otwórz obsługi żądania z Twojej tooresolve dostawcy łączności.
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a>Tabeli protokołu ARP problemów po powitania po stronie firmy Microsoft
* Nie będą widzieć tabeli protokołu ARP wyświetlany dla komunikacji równorzędnej, jeśli występują problemy na powitania po stronie firmy Microsoft.
* Otwórz żądanie pomocy technicznej o [Microsoft Azure Pomoc i obsługa techniczna](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Określ, czy masz problem z łącznością warstwy 2.

## <a name="next-steps"></a>Następne kroki
* Sprawdź poprawność konfiguracji warstwy 3 dla obwodu usługi ExpressRoute:
  * Pobierz stan hello podsumowania toodetermine trasy sesje BGP.
  * Pobierz toodetermine tabeli tras, prefiksów, które są rozgłaszane między ExpressRoute.
* Zweryfikuj transferu danych, przeglądając bajtów i wylogowanie.
* Otwórz żądanie pomocy technicznej o [Microsoft Azure Pomoc i obsługa techniczna](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) Jeśli nadal występują problemy.

