---
title: "aaaPlan sieci do replikacji tooAzure VMware z usługą Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano planowanie wymagane sieci podczas replikowania maszyn wirtualnych platformy Azure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: sujayt
ms.openlocfilehash: e4036351ca707bd4966cf2a855d4a162f88153e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-azure-vm-replication"></a>Krok 3: Planowanie sieci w przypadku replikacji maszyny Wirtualnej Azure

Po zweryfikowaniu hello [wymagania wstępne dotyczące wdrażania](azure-to-azure-walkthrough-prerequisites.md), przeczytaj ten hello toounderstand artykułu sieci uwagi dotyczące replikacji i odzyskiwania maszyn wirtualnych platformy Azure (maszyn wirtualnych) z tooanother jeden region platformy Azure przy użyciu hello Usługa Azure Site Recovery. 

- Po zakończeniu hello artykuł ma wyraźnego zrozumienia, jak tooset się wychodzących dostępu do maszyn wirtualnych Azure możesz mają tooreplicate i jak tooconnect z lokalnej lokacji toothose maszyn wirtualnych.
- Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
> Azure replikację maszyny Wirtualnej z usługą Site Recovery jest obecnie w przeglądzie.



## <a name="network-overview"></a>Omówienie sieci

Zwykle maszynach wirtualnych platformy Azure znajdują się w podsieci platformy Azure wirtualnych sieci /, a w przypadku połączenia z Twojej tooAzure lokacji lokalnej przy użyciu usługi Azure ExpressRoute lub połączeń sieci VPN.

Sieci są zwykle chronione przy użyciu zapory lub sieci grup zabezpieczeń (NSG). Zapory można użyć na podstawie adresu URL na listach opartych na protokole TCP/IP, toocontrol łączność sieciową. Grupy NSG za pomocą adresu IP na podstawie zakresu reguł. 


Oczekiwano toowork odzyskiwania lokacji należy toomake niektóre zmiany w wychodzących łączność z maszyn wirtualnych, które mają tooreplicate. Usługa Site Recovery nie obsługuje użycia łączności sieciowej toocontrol uwierzytelniania serwera proxy. Jeśli uwierzytelnianie serwera proxy, nie można włączyć replikacji. 


Witaj Poniższy diagram przedstawia typowe środowisko dla aplikacji działających na maszynach wirtualnych platformy Azure.

![środowisko klienta](./media/azure-to-azure-walkthrough-network/source-environment.png)

**Środowiska maszyny Wirtualnej platformy Azure**

Można również zainstalować tooAzure połączenia, skonfiguruj z lokacji lokalnej, za pomocą usługi Azure ExpressRoute lub połączeń sieci VPN. 

![środowisko klienta](./media/azure-to-azure-walkthrough-network/source-environment-expressroute.png)

**TooAzure połączenia lokalnego**



## <a name="outbound-connectivity-for-urls"></a>Łączność wychodząca dla adresu URL

Jeśli korzystasz z zapory oparte na adresach URL łączność wychodząca toocontrol serwera proxy, upewnij się, że musisz zezwolić na te adresy URL używane przez usługę Site Recovery

**ADRES URL** | **Szczegóły**  
--- | ---
*.blob.core.windows.net | Umożliwia toobe danych z hello maszyny Wirtualnej, konta magazynu pamięci podręcznej toohello w regionie źródła hello.
Login.microsoftonline.com | Udostępnia tooSite autoryzację i uwierzytelnianie adresów URL usługi odzyskiwania.
*.hypervrecoverymanager.windowsazure.com | Umożliwia komunikację z hello usługi Site Recovery z hello maszyny Wirtualnej.
*. servicebus.windows.net | Wymagane, aby usługi Site Recovery hello monitorowania i diagnostyki danych mogą być zapisywane z hello maszyny Wirtualnej.

## <a name="outbound-connectivity-for-ip-address-ranges"></a>Łączność wychodząca dla zakresów adresów IP

- Może automatycznie tworzyć reguły hello wymagane na powitania NSG, pobierania i uruchamiając [ten skrypt](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).
- Zalecamy Tworzenie reguły NSG hello wymagane dla testu NSG i sprawdź, czy nie ma żadnych problemów, przed utworzeniem reguły hello produkcyjnych NSG.
- toocreate hello wymagana liczba reguły NSG, upewnij się, że Twoja subskrypcja jest białej. Skontaktuj się z pomocą techniczną tooincrease hello NSG reguły limit w ramach subskrypcji.
Jeśli używasz serwera proxy oparte na protokole IP zapory lub łączność wychodząca toocontrol reguły NSG hello następujące zakresy adresów IP, należy białej toobe, w zależności od lokalizacji źródłowej i docelowej hello hello maszyn wirtualnych:

    - Wszystkie zakresy adresów IP, które odpowiadają toohello lokalizacji źródła. Pobieranie hello [zakresy](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Listę dozwolonych podobnej jest wymagana, dzięki czemu dane mogą być zapisywane konta magazynu pamięci podręcznej toohello z hello maszyny Wirtualnej.
    - Wszystkie zakresy IP, które odpowiadają tooOffice 365 [uwierzytelnianie i tożsamość punkty końcowe IPv4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity). Nowe adresy IP zostaną dodane tooOffice 365 zakresy adresów IP, należy najpierw toocreate nowe reguły NSG.
-     Adresy IP punktu końcowego usługi odzyskiwania lokacji ([dostępne w pliku XML](https://aka.ms/site-recovery-public-ips)), które zależą od lokalizacji docelowej: 

   **Lokalizacja docelowa** | **Usługa Site Recovery adresów IP** |  **Usługa Site Recovery monitorowania IP**
   --- | --- | ---
   Azja Wschodnia | 52.175.17.132</br>40.83.121.61 | 13.94.47.61
   Azja Południowo-Wschodnia | 52.187.58.193</br>52.187.169.104 | 13.76.179.223
   Indie Środkowe | 52.172.187.37</br>52.172.157.193 | 104.211.98.185
   Indie Południowe | 52.172.46.220</br>52.172.13.124 | 104.211.224.190
   Środkowo-północne stany USA | 23.96.195.247</br>23.96.217.22 | 168.62.249.226
   Europa Północna | 40.69.212.238</br>13.74.36.46 | 52.169.18.8
   Europa Zachodnia | 52.166.13.64</br>52.166.6.245 | 40.68.93.145
   Wschodnie stany USA | 13.82.88.226</br>40.71.38.173 | 104.45.147.24
   Zachodnie stany USA | 40.83.179.48</br>13.91.45.163 | 104.40.26.199
   Środkowo-południowe stany USA | 13.84.148.14</br>13.84.172.239 | 104.210.146.250
   Środkowe stany USA | 40.69.144.231</br>40.69.167.116 | 52.165.34.144
   Wschodnie stany USA 2 | 52.184.158.163</br>52.225.216.31 | 40.79.44.59
   Japonia Wschodnia | 52.185.150.140</br>13.78.87.185 | 138.91.1.105
   Japonia Zachodnia | 52.175.146.69</br>52.175.145.200 | 138.91.17.38
   Brazylia Południowa | 191.234.185.172</br>104.41.62.15 | 23.97.97.36
   Australia Wschodnia | 104.210.113.114</br>40.126.226.199 | 191.239.64.144
   Australia Południowo-Wschodnia | 13.70.159.158</br>13.73.114.68 | 191.239.160.45
   Kanada Środkowa | 52.228.36.192</br>52.228.39.52 | 40.85.226.62
   Kanada Wschodnia | 52.229.125.98</br>52.229.126.170 | 40.86.225.142
   Środkowo-zachodnie stany USA | 52.161.20.168</br>13.78.230.131 | 13.78.149.209
   Zachodnie stany USA 2 | 52.183.45.166</br>52.175.207.234 | 13.66.228.204
   Zachodnie Zjednoczone Królestwo | 51.141.3.203</br>51.140.226.176 | 51.141.14.113
   Południowe Zjednoczone Królestwo | 51.140.43.158</br>51.140.29.146 | 51.140.189.52

## <a name="example-nsg-configuration"></a>Przykładowa konfiguracja grupy NSG

W tej sekcji przedstawiono, jak reguły tooconfigure NSG tak, aby działa replikacji dla maszyny Wirtualnej. Jeśli używasz łączność wychodząca toocontrol reguły NSG, należy użyć "Zezwalaj na HTTPS wychodzące" reguł dla wszystkich zakresów IP hello wymagane.

W tym przykładzie hello lokalizacji źródłowej maszyny Wirtualnej jest "Wschodnie stany USA". Lokalizacja docelowa replikacji Hello jest środkowe stany USA.


### <a name="example"></a>Przykład

#### <a name="east-us"></a>Wschodnie stany USA

1. Tworzenie reguł, które odpowiadają za[zakresy wschodnie stany USA IP](https://www.microsoft.com/download/confirmation.aspx?id=41653). Jest to wymagane, dzięki czemu dane mogą być zapisywane konta magazynu pamięci podręcznej toohello z hello maszyny Wirtualnej.
2. Tworzenie reguł dla wszystkich zakresów IP, które odpowiadają tooOffice 365 [uwierzytelnianie i tożsamość punkty końcowe IPv4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Tworzenie reguł, które odpowiadają toohello lokalizacji docelowej:

   **Lokalizacja** | **Usługa Site Recovery adresów IP** |  **Usługa Site Recovery monitorowania IP**
    --- | --- | ---
   Środkowe stany USA | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

#### <a name="central-us"></a>Środkowe stany USA

Te zasady są niezbędne, aby z hello docelowej toohello źródła regionu, można włączyć replikacji po pracy awaryjnej.

1. Tworzenie reguł, które odpowiadają za[zakresy IP USA centralnej](https://www.microsoft.com/download/confirmation.aspx?id=41653).
2. Tworzenie reguł dla wszystkich zakresów IP, które odpowiadają tooOffice 365 [uwierzytelnianie i tożsamość punkty końcowe IPv4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Tworzenie reguł, które odpowiadają toohello lokalizacji źródłowej:

   **Lokalizacja** | **Usługa Site Recovery adresów IP** |  **Usługa Site Recovery monitorowania IP**
    --- | --- | ---
   Wschodnie stany USA | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="existing-on-premises-connection"></a>Istniejącymi lokalnymi połączenia

Jeśli masz połączenie ExpressRoute lub sieci VPN między lokalnymi lokacji i lokalizacji źródłowej hello na platformie Azure, wykonaj następujące wytyczne:

**Konfiguracja** | **Szczegóły**
--- | ---
**Wymuszone tunelowanie** | Zwykle trasa domyślna (0.0.0.0/0) wymusza wychodzących tooflow ruchu internetowego za pośrednictwem hello lokalnej lokalizacji. Nie zaleca tego. Ruch związany z replikacją i komunikacji usługi Site Recovery powinny pozostać w obrębie platformy Azure.<br/><br/> Jako rozwiązanie, należy dodać trasy zdefiniowane przez użytkownika (Udr) dla [tych zakresów IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges), dzięki czemu ruch hello nie działa lokalnie.
**Łączność** | Jeśli aplikacje wymagają tooconnect tooon lokalne maszyny lub na klientach lokalnych łączyć toohello aplikacji za pośrednictwem lokalnej za pośrednictwem sieci VPN/ExpressRoute, upewnij się, musisz mieć co najmniej [połączenie lokacja lokacja](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), między docelowy hello region platformy Azure i Witaj lokacji lokalnej.<br/><br/> W przypadku wysokiej między docelowy hello region platformy Azure i lokacji lokalnej hello natężeniu ruchu, należy utworzyć inny [połączenia ExpressRoute](../expressroute/expressroute-introduction.md), między region docelowy hello i lokalnie.<br/><br/> Jeśli chcesz tooretain adresów IP dla maszyn wirtualnych po pracy awaryjnej, Zachowaj połączenia lokacja do witryny/ExpressRoute region docelowy hello w stanie rozłączenia. Dzięki temu nie ma żadnych kolizji zakresu między hello źródłowa i docelowa zakresów adresów IP.
**ExpressRoute** | Utworzyć obwodu usługi ExpressRoute hello regionów źródłowe i docelowe.<br/><br/> Utwórz połączenie między siecią źródła hello i obwodu ExpressRoute hello oraz między hello Sieć docelowa i hello obwodu.<br/><br/> Zalecane jest użycie różnych zakresów IP w regionach źródłowe i docelowe. Hello obwodu nie będzie możliwe tooconnect toomore niż Azure jednej sieci z hello same zakresy IP na powitania tym samym czasie.<br/><br/> Można utworzyć sieci wirtualnych z hello tego samego adresu IP z zakresów w obu regionów, a następnie utwórz obwody usługi ExpressRoute w obu regionach. Dla trybu failover rozłączyć obwodu hello hello źródłowej sieci wirtualnej, a następnie połącz obwodu hello w sieci wirtualnej hello docelowej.<br/><br/> W przypadku całkowicie dół regionu podstawowego hello operacji odłączenia hello może zakończyć się niepowodzeniem. W takim przypadku sieci wirtualnej hello docelowych nie będzie otrzymywał połączenie ExpressRoute.
**ExpressRoute — wersja Premium** | Możesz utworzyć obwody w hello tego samego regionu geograficznymi.<br/><br/> obwody toocreate w różnych regionach geograficznymi, muszą Azure ExpressRoute — wersja Premium.<br/><br/> Z Premium koszt hello jest przyrostowe. Jeśli już używasz programu, nie ma żadnych dodatkowych kosztów.<br/><br/> Dowiedz się więcej o [lokalizacje](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) i [cennik](https://azure.microsoft.com/pricing/details/expressroute/).



## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 4: Tworzenie magazynu](azure-to-azure-walkthrough-vault.md)

