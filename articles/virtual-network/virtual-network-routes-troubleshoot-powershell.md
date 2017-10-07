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
# <a name="troubleshoot-routes-using-azure-powershell"></a>Rozwiązywanie problemów z tras za pomocą programu Azure PowerShell
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

Jeśli występują tooor problemy dotyczące łączności sieciowej z sieci maszyny wirtualnej Azure (VM), tras może mieć wpływ na Twoje ruch maszyny Wirtualnej. Ten artykuł zawiera omówienie funkcji diagnostyki dla tras toohelp dalsze poszukiwanie rozwiązania problemu.

Tabele tras są skojarzone z podsieciami i obowiązują na wszystkich interfejsach sieciowych (NIC) w tej podsieci. następujące typy tras Hello może być zastosowane tooeach interfejsu sieciowego:

* **Trasy systemowe:** Domyślnie każda podsieć utworzona w sieci wirtualnej platformy Azure (VNet) ma tabel tras systemu, które umożliwiają lokalnej sieci wirtualnej ruch, ruch lokalnej za pośrednictwem bramy sieci VPN i ruchu internetowego. Istnieją również tras systemowych dla połączyć za pomocą sieci wirtualnych.
* **Trasy protokołu BGP:** propagowane interfejsów toonetwork za pośrednictwem usługi ExpressRoute lub połączeń VPN lokacja lokacja. Dowiedz się więcej o routingu BGP, odczytując hello [protokołu BGP z bramy sieci VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) i [omówienie ExpressRoute](../expressroute/expressroute-introduction.md) artykułów.
* **Trasy zdefiniowane przez użytkownika (przez):** Jeśli używasz wirtualnych urządzeń sieciowych lub są wymuszone tunelowanie ruchu tooan sieci lokalnej za pośrednictwem sieci VPN lokacja lokacja, może być zdefiniowana przez użytkownika tras (Udr) skojarzone z tabeli tras podsieci. Jeśli nie masz doświadczenia w obsłudze Udr, przeczytaj hello [trasy zdefiniowane przez użytkownika](virtual-networks-udr-overview.md#user-defined-routes) artykułu.

Z hello różne trasy, które mogą być zastosowane tooa interfejsu sieciowego, może być trudne toodetermine obowiązują agregacji trasy. toohelp rozwiązywania problemów z połączeniami sieci maszyny Wirtualnej, można wyświetlić wszystkie hello skuteczne trasy dla interfejsu sieciowego w modelu wdrażania usługi Azure Resource Manager hello.

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a>Przy użyciu przepływu ruchu maszyny Wirtualnej tootroubleshoot skuteczne tras
W tym artykule wykorzystano powitania po scenariusz jako tooillustrate przykład, jak skuteczne hello tootroubleshoot trasy dla interfejsu sieciowego:

Maszyna wirtualna (*VM1*) połączony toohello sieci wirtualnej (*VNet1*, prefiks: 10.9.0.0/16) nie powiedzie się tooa tooconnect VM(VM3) w nowo peered sieci wirtualnej (*VNet3*, prefiks 10.10.0.0/16). Brak Udr lub BGP kieruje zastosowane NIC1 tooVM1 sieci interfejs podłączony toohello maszyny Wirtualnej, są stosowane tylko tras systemowych.

W tym artykule opisano, jak toodetermine hello. Przyczyna niepowodzenia połączenia hello przy użyciu możliwości wprowadzenia trasy w modelu wdrażania zarządzania zasobami Azure.
Gdy hello przykładzie użyto tylko tras systemowych, hello te same kroki można używane toodetermine błędów połączenia przychodzącego i wychodzącego przez dowolnego typu trasy.

> [!NOTE]
> Jeśli maszyna wirtualna ma więcej niż jedną kartę Sieciową podłączoną, sprawdź skuteczne trasy dla każdego hello tooand sieci toodiagnose kart sieciowych problemy dotyczące łączności z maszyny Wirtualnej.
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a>Widok skuteczne trasy dla maszyny wirtualnej
toosee hello agregacji tras, na których są stosowane tooa maszyny Wirtualnej, pełną hello następujące kroki:

### <a name="view-effective-routes-for-a-network-interface"></a>Widok skuteczne trasy dla interfejsu sieciowego
toosee hello agregacji tras, na których są stosowane tooa interfejsu sieciowego, pełną hello następujące kroki:

1. Uruchom tooAzure sesji i logowania programu Azure PowerShell. Jeśli nie masz doświadczenia w obsłudze programu Azure PowerShell, przeczytaj hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.
2. Witaj poniższe polecenie zwraca wszystkie trasy stosowane tooa sieciowej o nazwie *VM1 NIC1* w grupie zasobów hello *RG1*.
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Jeśli nie znasz nazwy hello interfejsu sieciowego, wpisz hello następujące nazwy hello tooretrieve poleceń wszystkie interfejsy sieciowe group.* zasobów
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   Witaj następujące dane wyjściowe wyglądają podobne toohello dane wyjściowe dla każdej trasy stosowane hello podsieci toohello, karta sieciowa jest połączona z:
   
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
   
   Zwróć uwagę hello następujących danych wyjściowych hello:
   
   * **Nazwa**: Nazwa trasy efektywne hello może być pusty, chyba że jawnie określone dla tras zdefiniowanych przez użytkownika. 
   * **Stan**: wskazuje stan hello skuteczne trasy. Możliwe wartości to "Active" lub "Nieprawidłowe"
   * **AddressPrefixes**: Określa prefiks adresu hello hello skuteczne trasy w notacji CIDR. 
   * **Typ następnego przeskoku**: wskazuje hello następnego skoku dla hello podane trasy. Możliwe wartości to *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, lub *Null*. Wartość *Null* dla **Typ następnego przeskoku** przez może oznaczać nieprawidłową trasy. Na przykład jeśli **Typ następnego przeskoku** jest *VirtualAppliance* i urządzenie wirtualne sieci hello maszyna wirtualna nie jest w stanie zainicjowano obsługę administracyjną uruchomiona. Jeśli **Typ następnego przeskoku** jest *właściwość VPNGateway* i nie Brak bramy elastycznie/uruchomiony w hello podanej sieci wirtualnej, trasa hello mogą być nieprawidłowe.
   * **Adres IP następnego przeskoku**: Określa adres IP następnego przeskoku trasy efektywne hello hello hello.
   
   Witaj poniższe polecenie zwraca trasy hello łatwiejsze tabeli tooview:
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   Hello następujące dane wyjściowe są niektóre hello danych wyjściowych dla scenariusza hello opisanych powyżej:
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. Nie istnieje żadne toohello trasy wymienione *WestUS VNet3* sieciami wirtualnymi (prefiks 10.10.0.0/16)** z *WestUS VNet1* (prefiksu 10.9.0.0/16) w danych wyjściowych hello hello w poprzednim kroku. Jak pokazano na poniższej ilustracji hello, hello sieci wirtualnej komunikacji równorzędnej łącza z hello *WestUS VNet3* sieci wirtualnej jest w hello *Rozłączono* stanu.
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    Hello łącze dwukierunkowe dla komunikacji równorzędnej hello jest uszkodzona, który wyjaśnia dlaczego VM1 nie może połączyć tooVM3 w hello *WestUS VNet3* sieci wirtualnej. Konfiguracja dwukierunkowe sieci wirtualnej komunikacji równorzędnej łącze ponownie *WestUS VNet1* i *WestUS VNet3* sieci wirtualnych. Witaj dane wyjściowe zwrócone w wyniku hello sieci wirtualnej komunikacji równorzędnej łącze jest poprawnie ustanowić następujące:
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    Po określeniu hello problem, można dodać, usunąć, lub zmień tras i tabel tras. Hello wpisz następujące polecenie toosee listę poleceń hello używane toodo tak:
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a>Zagadnienia do rozważenia
Zwrócono kilka rzeczy tookeep pamiętać podczas przeglądania listy hello tras:

* Routing jest oparta na Najdłuższy prefiks dopasowania (LPM) Wybierane spośród Udr, trasy protokołu BGP i systemu. Jeśli istnieje więcej niż jedna trasa z hello sam LPM zgodne, a następnie, wybór trasy odbywa się w następującej kolejności hello:
  
  * Trasa zdefiniowana przez użytkownika
  * Trasa protokołu BGP
  * Trasa systemowa (ustawienie domyślne)
    
    Skuteczne trasy może zobaczyć tylko skuteczne ścieżek, które są oparte na wszystkich tras dostępnego hello dopasowaniem LPM. Przez pokazanie, jak trasy hello faktycznie są oceniane pod kątem danej karty Sieciowej, ułatwia to znacznie łatwiejsze trasy określonych tootroubleshoot, które mogą mieć wpływ na łączność z maszyny Wirtualnej.
* Jeśli masz Udr i wysyłania ruchu tooa sieci urządzenie wirtualne (NVA) z *VirtualAppliance* jako **Typ następnego przeskoku**, upewnij się, że przesyłanie dalej IP jest włączona na odbieranie ruchu hello hello NVA lub pakiety są usuwane. 
* Włączenie tunelowania wymuszony cały ruch wychodzący z Internetem będzie routingiem tooon firmą. Protokołu RDP/SSH z tooyour Internet, maszyna wirtualna może nie działać to ustawienie, w zależności od sposobu hello lokalnymi obsługuje ten ruch. 
  Tunelowanie wymuszone można włączyć:
  * Jeśli przy użyciu sieci VPN typu lokacja lokacja, ustawiając trasy zdefiniowane przez użytkownika (przez) z Typ następnego przeskoku jako brama sieci VPN
  * Jeśli trasa domyślna jest anonsowana za pośrednictwem protokołu BGP
* Dla sieci równorzędne — ruch toowork poprawnie, trasa systemu o **Typ następnego przeskoku** *VNetPeering* musi istnieć na powitania połączyć za pomocą sieci wirtualnej firmy prefiks zakresu. Jeśli taka trasa nie istnieje i hello sieci wirtualnej komunikacji równorzędnej łącze wygląda OK:
  * Poczekaj kilka sekund, a następnie spróbuj ponownie, jeśli jest to nowo utworzonego łącze komunikacji równorzędnej. Od czasu do czasu zajmuje dłużej tras toopropagate interfejsów sieciowych hello tooall w podsieci.
  * Zasady grupy zabezpieczeń sieci (NSG) może mieć wpływ na powitania przepływów ruchu sieciowego. Aby uzyskać więcej informacji, zobacz hello [Rozwiązywanie problemów z grup zabezpieczeń sieci](virtual-network-nsg-troubleshoot-powershell.md) artykułu.

