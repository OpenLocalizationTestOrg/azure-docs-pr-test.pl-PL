---
title: "Odzyskiwanie lokacji sieciowych wskazówki dotyczące replikacji maszyn wirtualnych z platformy Azure tooAzure aaaAzure | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure Networking"
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
ms.date: 05/13/2017
ms.author: sujayt
ms.openlocfilehash: 3a3391b8c3512932d243458fd17d2a2b39248448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="networking-guidance-for-replicating-azure-virtual-machines"></a>Wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure Networking

>[!NOTE]
> Replikacja lokacji odzyskiwania maszyn wirtualnych platformy Azure jest obecnie w przeglądzie.

Ta sieć wskazówki dotyczące usługi Azure Site Recovery, podczas replikacji i odzyskiwania maszyn wirtualnych platformy Azure z jednego regionu tooanother hello szczegóły artykułu. Aby uzyskać więcej informacji o wymaganiach usługi Azure Site Recovery, zobacz hello [wymagania wstępne](site-recovery-prereq.md) artykułu.

## <a name="site-recovery-architecture"></a>Architektura odzyskiwania lokacji

Usługa Site Recovery zapewnia tooreplicate prosty i łatwy sposób aplikacji uruchomionych na tooanother maszyn wirtualnych platformy Azure region platformy Azure, dzięki czemu mogą zostać odzyskane, jeśli brak przerw w działaniu w regionie podstawowym hello. Dowiedz się więcej o [tego scenariusza i architekturze usługi Site Recovery](site-recovery-azure-to-azure-architecture.md).

## <a name="your-network-infrastructure"></a>Infrastruktura sieciowa użytkownika

Witaj Poniższy diagram przedstawia hello typowe środowiska platformy Azure dla aplikacji działających na maszynach wirtualnych platformy Azure:

![środowisko klienta](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Jeśli używasz usługi Azure ExpressRoute lub połączenie sieci VPN z tooAzure sieci lokalnej, środowisko hello wygląda następująco:

![środowisko klienta](./media/site-recovery-azure-to-azure-architecture/source-environment-expressroute.png)

Zazwyczaj klienci ochrony ich sieci za pomocą zapory i/lub grup zabezpieczeń sieci (NSG). Hello zapory można użyć na podstawie adresu URL albo opartego na protokole IP listę dozwolonych podobnej do kontrolowania łączność sieciową. Grupy NSG umożliwiają reguł przy użyciu połączenia sieciowego toocontrol zakresów IP.

>[!IMPORTANT]
> Jeśli używasz łączności sieciowej toocontrol uwierzytelnionego serwera proxy nie jest obsługiwane i nie można włączyć replikacji usługi Site Recovery. 

Witaj poniższych sekcjach omówiono hello sieci łączność wychodząca zmiany, które są wymagane w maszynach wirtualnych platformy Azure Site Recovery toowork replikacji.

## <a name="outbound-connectivity-for-azure-site-recovery-urls"></a>Łączność wychodząca dla adresy URL platformy Azure Site Recovery

Jeśli używasz dowolnego zapora oparta na adres URL serwera proxy toocontrol łączność wychodząca można toowhitelist się, że następujące wymagane adresy URL usługi Azure Site Recovery:


**ADRES URL** | **Cel**  
--- | ---
*.blob.core.windows.net | Wymagane, aby dane mogą być zapisywane konta magazynu pamięci podręcznej toohello w regionie źródła hello z hello maszyny Wirtualnej.
Login.microsoftonline.com | Wymagany w przypadku autoryzację i uwierzytelnianie toohello usługi Site Recovery adresy URL usługi.
*.hypervrecoverymanager.windowsazure.com | Wymagane, aby komunikacja usługi Site Recovery hello może wystąpić z hello maszyny Wirtualnej.
*. servicebus.windows.net | Wymagane, aby usługi Site Recovery hello monitorowania i diagnostyki danych mogą być zapisywane z hello maszyny Wirtualnej.

## <a name="outbound-connectivity-for-azure-site-recovery-ip-ranges"></a>Łączność wychodząca dla zakresów IP odzyskiwania lokacji platformy Azure

>[!NOTE]
> tooautomatically tworzenie reguł NSG hello wymagane na powitania sieciowej grupy zabezpieczeń, możesz [pobranie i użycie tego skryptu](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

>[!IMPORTANT]
> * Firma Microsoft zaleca utworzenie reguły NSG hello wymagane na testową grupę zabezpieczeń sieci i sprawdź, czy nie ma żadnych problemów przed utworzeniem reguły hello na grupę zabezpieczeń sieci produkcyjnych.
> * toocreate hello wymagana liczba reguły NSG, upewnij się, że Twoja subskrypcja jest białej. Skontaktuj się z pomocą techniczną tooincrease hello NSG reguły limit w ramach subskrypcji.

Jeśli używasz serwera proxy oparte na protokole IP zapory lub łączność wychodząca toocontrol reguły NSG hello następujące zakresy adresów IP, należy białej toobe, w zależności od lokalizacji źródłowej i docelowej hello hello maszyn wirtualnych:

- Wszystkie zakresy IP, które odpowiadają toohello lokalizacji źródła. (Możesz pobrać hello [zakresów IP](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Listę dozwolonych podobnej jest wymagana do danych mogą być zapisywane konta magazynu pamięci podręcznej toohello z hello maszyny Wirtualnej.

- Wszystkie zakresy IP, które odpowiadają tooOffice 365 [uwierzytelnianie i tożsamość punkty końcowe IPv4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

    >[!NOTE]
    > Nowe adresy IP zostaną dodane tooOffice 365 zakresy adresów IP w przyszłości hello, należy najpierw toocreate nowe reguły NSG.
    
- Punkt końcowy usługi odzyskiwania adresów IP lokacji ([dostępne w pliku XML](https://aka.ms/site-recovery-public-ips)), które zależą od lokalizacji docelowej: 

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

## <a name="sample-nsg-configuration"></a>Przykładowa konfiguracja grupy NSG
W tej sekcji wyjaśniono reguły NSG tooconfigure kroki hello, dzięki czemu replikacja usługi Site Recovery może działać na maszynie wirtualnej. Jeśli używasz łączność wychodząca toocontrol reguły NSG, należy użyć "Zezwalaj na HTTPS wychodzące" reguł dla wszystkich zakresów IP hello wymagane.

>[!Note]
> tooautomatically tworzenie reguł NSG hello wymagane na powitania sieciowej grupy zabezpieczeń, możesz [pobranie i użycie tego skryptu](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

Na przykład jeśli lokalizacji źródłowej maszyny Wirtualnej "Wschodnie stany USA" i lokalizacji docelowej replikacji jest "Centralnej nas", wykonaj kroki hello w dwóch następnych sekcjach hello.

>[!IMPORTANT]
> * Firma Microsoft zaleca utworzenie reguły NSG hello wymagane na testową grupę zabezpieczeń sieci i sprawdź, czy nie ma żadnych problemów przed utworzeniem reguły hello na grupę zabezpieczeń sieci produkcyjnych.
> * toocreate hello wymagana liczba reguły NSG, upewnij się, że Twoja subskrypcja jest białej. Skontaktuj się z pomocą techniczną tooincrease hello NSG reguły limit w ramach subskrypcji. 

### <a name="nsg-rules-on-hello-east-us-network-security-group"></a>Reguły NSG na grupę zabezpieczeń sieci hello w wschodnie stany USA

* Tworzenie reguł, które odpowiadają za[zakresy wschodnie stany USA IP](https://www.microsoft.com/download/confirmation.aspx?id=41653). Jest to wymagane, dzięki czemu dane mogą być zapisywane konta magazynu pamięci podręcznej toohello z hello maszyny Wirtualnej.

* Tworzenie reguł dla wszystkich zakresów IP, które odpowiadają tooOffice 365 [uwierzytelnianie i tożsamość punkty końcowe IPv4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Tworzenie reguł, które odpowiadają toohello lokalizacji docelowej:

   **Lokalizacja** | **Usługa Site Recovery adresów IP** |  **Usługa Site Recovery monitorowania IP**
    --- | --- | ---
   Środkowe stany USA | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

### <a name="nsg-rules-on-hello-central-us-network-security-group"></a>Reguły NSG na grupę zabezpieczeń sieci hello w środkowe stany USA

Te zasady są niezbędne, dzięki czemu można włączyć replikację z hello docelowego regionu toohello źródła region po pracy w trybie failover:

* Zasady, które odpowiadają za[zakresy IP USA centralnej](https://www.microsoft.com/download/confirmation.aspx?id=41653). Są wymagane, aby dane mogą być zapisywane konta magazynu pamięci podręcznej toohello z hello maszyny Wirtualnej.

* Zasady dla wszystkich zakresów IP, które odpowiadają tooOffice 365 [uwierzytelnianie i tożsamość punkty końcowe IPv4](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Lokalizacja źródłowa reguł, które odpowiadają toohello:

   **Lokalizacja** | **Usługa Site Recovery adresów IP** |  **Usługa Site Recovery monitorowania IP**
    --- | --- | ---
   Wschodnie stany USA | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration"></a>Wytyczne dotyczące istniejącą konfigurację usługi Azure do lokalnymi lub sieć VPN

Jeśli masz połączenie ExpressRoute lub sieci VPN między lokalnymi i hello źródło lokalizacji na platformie Azure, postępuj zgodnie z wytycznymi hello w tej sekcji.

### <a name="forced-tunneling-configuration"></a>W przypadku konfiguracji tunelowania wymuszonego

Typowa konfiguracja klienta jest toodefine trasy domyślnej (0.0.0.0/0), która wymusza wychodzących tooflow ruchu internetowego za pośrednictwem lokalizacji lokalne powitania. Firma Microsoft nie jest to zalecane. ruch związany z replikacją Hello i komunikacji usługi Site Recovery nie opuszczaj hello Azure granic. Witaj rozwiązanie jest tooadd zdefiniowane przez użytkownika tras (Udr) dla [tych zakresów IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges) tak, aby ruch związany z replikacją hello nie działa lokalnie.

### <a name="connectivity-between-hello-target-and-on-premises-location"></a>Łączność między hello lokalizacji docelowej i lokalnych

Wykonaj te wytyczne dotyczące połączeń między hello lokalizacji docelowej i hello lokalnej lokalizacji:
- Jeśli aplikacja wymaga tooconnect toohello lokalnymi maszynami lub w przypadku klientów nawiązujących połączenie toohello aplikacji z lokalnej za pośrednictwem sieci VPN/ExpressRoute, upewnij się, że masz co najmniej [połączenie lokacja lokacja](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) między docelowy Azure regionu i hello lokalnego centrum danych.

- Jeśli spodziewasz się dużej ilości tooflow ruchu między docelowy region platformy Azure i hello lokalnego centrum danych, należy utworzyć inny [połączenia ExpressRoute](../expressroute/expressroute-introduction.md) między hello docelowy Azure regionu i hello lokalnie w centrum danych.

- Jeśli chcesz tooretain adresów IP dla maszyn wirtualnych powitania po ich w tryb failover, Zachowaj połączenia lokacja do witryny/ExpressRoute region docelowy hello w stanie rozłączenia. Jest to toomake się, że nie zakresu konflikt między hello źródła region zakresów adresów IP i zakresów adresów IP region docelowy nie istnieje.

### <a name="best-practices-for-expressroute-configuration"></a>Najlepsze rozwiązania dotyczące konfiguracji usługi ExpressRoute
Wykonaj następujące najlepsze rozwiązania dla konfiguracji usługi ExpressRoute:

- Należy toocreate obwodu usługi ExpressRoute w obu hello regionach źródłowe i docelowe. Następnie należy toocreate połączenie między usługą:
  - sieć wirtualna Hello źródła i hello obwodu ExpressRoute.
  - sieć wirtualna Hello docelowych i hello obwodu ExpressRoute.

- W ramach standardowego ExpressRoute, możesz utworzyć obwody w hello tego samego regionu geograficznymi. obwody usługi ExpressRoute toocreate w różnych regionach geograficznymi, Azure ExpressRoute — wersja Premium jest wymagana, która obejmuje przyrostowe kosztów. (Jeśli już używasz usługi ExpressRoute — wersja Premium, jest nie żadnymi dodatkowymi kosztami.) Aby uzyskać więcej informacji, zobacz hello [dokumentu lokalizacje ExpressRoute](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) i [cennik usługi ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute/).

- Zalecane jest użycie różnych zakresów IP w regionach źródłowe i docelowe. Witaj obwodu usługi expressroute nie będzie można z tego samego adresu IP zakresów na powitania tooconnect z dwóch sieci wirtualnych platformy Azure z hello tym samym czasie.

- Można utworzyć sieci wirtualnych z hello tego samego adresu IP z zakresów w obu regionów, a następnie utwórz obwody usługi ExpressRoute w obu regionach. W przypadku hello zdarzenia pracy awaryjnej rozłączyć obwodu hello hello źródłowej sieci wirtualnej, a następnie połącz obwodu hello w sieci wirtualnej hello docelowej.

 >[!IMPORTANT]
 > W przypadku całkowicie dół regionu podstawowego hello operacji odłączenia hello może zakończyć się niepowodzeniem. Która uniemożliwi sieci wirtualnej docelowy hello uzyskiwanie połączenia ExpressRoute.

## <a name="next-steps"></a>Następne kroki
Włączyć ochronę obciążeń przez [replikowanie maszyn wirtualnych platformy Azure](site-recovery-azure-to-azure.md).
