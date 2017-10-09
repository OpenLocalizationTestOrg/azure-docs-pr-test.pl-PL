---
title: "aaaAzure usługi Site Recovery macierzy obsługi replikacji z platformy Azure tooAzure | Dokumentacja firmy Microsoft"
description: "Podsumowanie hello obsługiwane systemy operacyjne i konfiguracje dla usługi Azure Site Recovery replikacji maszyn wirtualnych platformy Azure (maszyn wirtualnych) z jednego regionu tooanother na potrzeby odzyskiwania (DR) po awarii."
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
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: 75b2451b4c2069ca4b11deb0efe1329d43879eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-azure-tooazure"></a>Azure Site Recovery macierz obsługi replikacji z Azure tooAzure


>[!NOTE]
>
> Replikacja lokacji odzyskiwania maszyn wirtualnych platformy Azure jest obecnie w przeglądzie.

W tym artykule przedstawiono obsługiwane konfiguracje oraz składniki usługi Azure Site Recovery podczas replikacji i odzyskiwania maszyn wirtualnych platformy Azure z jednego regionu tooanother.

## <a name="user-interface-options"></a>Opcje interfejsu użytkownika

**Interfejs użytkownika** |  **Obsługiwane / nieobsługiwane**
--- | ---
**Witryna Azure Portal** | Obsługiwane
**Portal klasyczny** | Nieobsługiwane
**PowerShell** | Nie są obecnie obsługiwane
**Interfejs API REST** | Nie są obecnie obsługiwane
**Interfejs wiersza polecenia** | Nie są obecnie obsługiwane


## <a name="resource-move-support"></a>Obsługa przeniesienia zasobu

**Typ przenoszenia zasobów** | **Obsługiwane / nieobsługiwane** | **Uwagi**  
--- | --- | ---
**Przenieś magazyn między grupami zasobów** | Nieobsługiwane |Nie można przenieść magazyn usług odzyskiwania hello między grupami zasobów.
**Przenoszenie między grupami zasobów obliczeniowych, magazynu i sieci** | Nieobsługiwane |Jeśli przenosisz maszynę wirtualną (lub jej skojarzone składniki, takie jak magazyn i sieć) po włączeniu replikacji należy toodisable replikacji i włączyć replikację dla maszyny wirtualnej hello ponownie.


## <a name="support-for-deployment-models"></a>Obsługa modeli wdrażania

**Model wdrażania** | **Obsługiwane / nieobsługiwane** | **Uwagi**  
--- | --- | ---
**Wdrożenie klasyczne** | Obsługiwane | Można tylko replikowanie klasyczne maszyny wirtualnej i odzyskać ją jako maszynę wirtualną w klasycznym. Nie można go odzyskać jako maszynę wirtualną Menedżera zasobów. W przypadku wdrożenia klasyczne maszyny Wirtualnej bez sieci wirtualnej i bezpośrednio tooan region platformy Azure, nie jest obsługiwane.
**Resource Manager** | Obsługiwane |

## <a name="support-for-replicated-machine-os-versions"></a>Obsługa wersji systemu operacyjnego zreplikowanej maszyny

Witaj poniżej pomocy technicznej jest stosowana na dowolne obciążenia uruchomione na powitania określonych systemu operacyjnego.

#### <a name="windows"></a>Windows

- Windows Server 2016 (instalacja Server Core i serwer ze środowiskiem pulpitu) *
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 z na co najmniej z dodatkiem SP1

>[!NOTE]
>
> \*Windows Server 2016 Nano Server nie jest obsługiwane.

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 6.7, 6.8, 7.0, 7.1, 7.2, 7.3
- CentOS 6.5, 6.6, 6.7, 6.8, 7.0, 7.1, 7.2, 7.3
- Ubuntu 14.04 LTS Server [ (obsługiwane wersje jądra)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Ubuntu 16.04 LTS Server [ (obsługiwane wersje jądra)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Oracle Linux przedsiębiorstwa 6.4, 6.5 systemem jądra zgodne Red Hat hello lub podzielenie Enterprise jądra wersji 3 (UEK3)
- SUSE Linux Enterprise Server 11 z dodatkiem SP3

>[!NOTE]
>
> Serwery systemu Ubuntu przy użyciu hasła uwierzytelniania i logowania przy użyciu maszyn wirtualnych chmury tooconfigure hello init chmury pakietu, może mieć hasło systemem i logowania wyłączone podczas pracy awaryjnej (w zależności od konfiguracji cloudinit hello.) Logowanie oparte na hasłach można ją ponownie włączyć na maszynie wirtualnej hello poprzez zresetowanie hasła hello z menu ustawień hello (w obszarze hello Obsługa + sekcję Rozwiązywanie problemów) hello przejścia w tryb failover maszyny wirtualnej na powitania portalu Azure.

### <a name="supported-ubuntu-kernel-versions-for-azure-virtual-machines"></a>Obsługiwane wersje jądra Ubuntu maszyn wirtualnych platformy Azure

**Zlecenia** | **Wersja usługi mobilności** | **Wersja jądra** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0 117 — ogólne,<br/>3.16.0-25-Generic too3.16.0-77-ogólny<br/>3.19.0-18-Generic too3.19.0 80-ogólne,<br/>4.2.0-18-Generic too4.2.0 42 — ogólne,<br/>4.4.0-21-Generic too4.4.0 75 — ogólne |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0 121 — ogólne,<br/>3.16.0-25-Generic too3.16.0-77-ogólny<br/>3.19.0-18-Generic too3.19.0 80-ogólne,<br/>4.2.0-18-Generic too4.2.0 42 — ogólne,<br/>4.4.0-21-Generic too4.4.0 81 — ogólne |
16.04 LTS | 9.10 | 4.4.0-21-Generic too4.4.0 81 — ogólne,<br/>4.8.0-34-Generic too4.8.0 56-ogólne,<br/>4.10.0-14-Generic too4.10.0 24 — ogólne |

## <a name="supported-file-systems-and-guest-storage-configurations-on-azure-virtual-machines-running-linux-os"></a>Obsługiwanych systemów plików i konfiguracje magazynu gościa na maszynach wirtualnych Azure systemem operacyjnym Linux

* Systemy plików: ext3 ext4, ReiserFS (Suse Linux Enterprise Server tylko), XFS
* Menedżer woluminów: LVM2
* Oprogramowanie wielościeżkowego: mapowania urządzenia

## <a name="region-support"></a>Obsługa regionu

Można replikować i odzyskiwania maszyn wirtualnych między żadnych dwóch regionach w ramach hello tego samego klastra geograficznych.

**Geograficzne klastra** | **Regiony platformy Azure**
-- | --
Ameryka | Kanada Wschodnia, środkowe stany USA Kanada centralnej, Południowej, zachodnie środkowe stany USA, wschodnie stany USA, wschodnie stany USA 2, zachodnie stany USA, zachodnie stany USA 2, środkowe stany USA, północno środkowe stany USA
Europa | Wielka Brytania Zachodnia, Wielka Brytania Południowa, Europa Północna, Europa Zachodnia
Azja | Indie Południowa, Indie środkowe, Azja południowo-wschodnia, Azja Wschodnia, Japonia Wschodnia, Japonia Zachodnia, Korea środkowe, Korea południe
Australia   | Australia Wschodnia, Australia południowo-wschodnia

>[!NOTE]
>
> W regionie Brazylia Południowa tylko można replikować, i wykonać ich kopię tooone pracy awaryjnej południowo-środkowe stany, zachodnie centralnej nam, wschodnie stany USA, wschodnie stany USA 2, zachodnie stany USA, zachodnie stany USA 2 i północno-środkowe stany regionów i kończyć się niepowodzeniem.


## <a name="support-for-compute-configuration"></a>Obsługa konfiguracji obliczeniowej

**Konfiguracja** | **Obsługiwane/nieobsługiwane** | **Uwagi**
--- | --- | ---
Rozmiar | Wszelkie rozmiar maszyny Wirtualnej platformy Azure z co najmniej 2 rdzeni Procesora i 1 GB pamięci RAM | Odwołuje się zbyt[rozmiary maszyny wirtualnej platformy Azure](../virtual-machines/windows/sizes.md)
Zestawy dostępności | Obsługiwane | Jeśli używasz opcji domyślnej hello podczas wykonywania kroku "Włącz replikację" w portalu zestawu dostępności hello jest automatycznie tworzone w oparciu konfiguracji region źródła. Możesz zmienić hello docelowym zestawem dostępności w "elementu zreplikowane > Ustawienia > obliczenia i sieć > zestawu dostępności" dowolnej chwili.
Maszyny wirtualne korzyści (KONCENTRATOR) Użyj hybrydowego | Obsługiwane | Jeśli hello źródłowej maszyny Wirtualnej ma włączone licencji KONCENTRATORA, hello Test trybu failover lub trybu Failover maszyny Wirtualnej używa również hello Centrum licencji.
Zestawy skalowania maszyn wirtualnych | Nieobsługiwane |
Opublikowane Microsoft Azure obrazów w galerii- | Obsługiwane | Obsługiwane, jak długo hello maszyna wirtualna działa na system operacyjny obsługiwany przez usługę Site Recovery
Obrazów w galerii Azure - opublikowane innych firm | Obsługiwane | Obsługiwane, jak długo hello maszyna wirtualna działa na system operacyjny obsługiwany przez usługę Site Recovery.
Niestandardowe obrazy - opublikowane innych firm | Obsługiwane | Obsługiwane, jak długo hello maszyna wirtualna działa na system operacyjny obsługiwany przez usługę Site Recovery.
Migracja maszyn wirtualnych przy użyciu usługi Site Recovery | Obsługiwane | Jeśli jest maszyny VMware/fizyczne migracji tooAzure przy użyciu usługi Site Recovery, należy toouninstall hello starsza wersja usługi mobilności i uruchom ponownie maszynę hello przed replikowanie go tooanother region platformy Azure.

## <a name="support-for-storage-configuration"></a>Obsługa konfiguracji magazynu

**Konfiguracja** | **Obsługiwane/nieobsługiwane** | **Uwagi**
--- | --- | ---
Maksymalny rozmiar dysku systemu operacyjnego | 1023 GB | Odwołuje się zbyt[dysków używanych przez maszyny wirtualne.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Rozmiar dysku danych maksymalna | 1023 GB | Odwołuje się zbyt[dysków używanych przez maszyny wirtualne.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Liczba dysków z danymi | Maksymalnie 64 obsługiwana przez określony rozmiar maszyny Wirtualnej Azure | Odwołuje się zbyt[rozmiary maszyny wirtualnej platformy Azure](../virtual-machines/windows/sizes.md)
Tymczasowe dysku | Zawsze wyłączone z replikacji | Dysku tymczasowym został wykluczony z replikacji zawsze. Nie należy umieszczać żadnych danych na dysku tymczasowym zgodnie z harmonogramem wskazówki platformy Azure. Odwołuje się zbyt[dysku tymczasowym na maszynach wirtualnych Azure](../virtual-machines/windows/about-disks-and-vhds.md#temporary-disk) więcej szczegółów.
Dane zmienić częstotliwość na powitania dysku | Maksymalna liczba 6 MB/s na dysk | Jeśli hello uśrednianie danych zmienić częstotliwość na dysku hello jest stale poza 6 MB/s, replikacji nie będzie przechwytywać. Jeśli jest serii danych okazjonalne i częstotliwości zmian danych hello jest większa niż 6 MB/s przez pewien czas i zawiera, replikacja będzie przechwytywać. W takim przypadku można napotkać punktów odzyskiwania nieco opóźnione.
Dyski na kontach magazynu w warstwie standardowa | Obsługiwane |
Dyski na kontach magazynu w warstwie premium | Obsługiwane | Jeśli maszyna wirtualna zawiera dyski rozmieszczenie do konta magazynu w warstwie standardowa i premium, możesz wybrać inny element docelowy konta magazynu dla każdego dysku tooensure masz hello tej samej konfiguracji magazynu w docelowym regionie
Dyski standardowe zarządzane | Nieobsługiwane |  
Dysków zarządzanych w warstwie Premium | Nieobsługiwane |
Funkcja miejsca do magazynowania | Obsługiwane |         
Szyfrowanie magazynowanych (SSE) | Obsługiwane | W przypadku kont magazynu pamięci podręcznej i obiekt docelowy można wybrać SSE włączone konta magazynu.     
Szyfrowanie dysków Azure (ADE) | Nieobsługiwane |
Dodaj lub usuń gorących dysku | Nieobsługiwane | Dodaj lub Usuń dysk danych na powitania maszyny Wirtualnej, należy toodisable replikacji i włącz ponownie replikację hello maszyny Wirtualnej.
Wykluczanie dysku | Nieobsługiwane|   Domyślnie jest wykluczony dysku tymczasowym.
LRS | Obsługiwane |
GRS | Obsługiwane |
RA-GRS | Obsługiwane |
ZRS | Nieobsługiwane |  
Chłodny i gorących magazynu | Nieobsługiwane | Dyski maszyny wirtualnej nie są obsługiwane na magazynu chłodnego i gorących

>[!IMPORTANT]
> Upewnij się, że stosujesz hello [wskazówki magazynu](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) źródła wirtualnej Azure maszynami tooavoid wszelkie problemy z wydajnością. Jeśli wykonujesz hello domyślnych ustawień usługi Site Recovery spowoduje utworzenie kont magazynu wymagana hello na podstawie konfiguracji źródła hello. Jeśli należy dostosować i wybrać własne ustawienia, upewnij się, wykonaj hello (.. / storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) jako źródła maszyn wirtualnych.

## <a name="support-for-network-configuration"></a>Obsługa konfiguracji sieci
**Konfiguracja** | **Obsługiwane/nieobsługiwane** | **Uwagi**
--- | --- | ---
Interfejsu sieciowego (NIC) | Maksymalnie maksymalną liczbę kart sieciowych obsługiwanych przez określony rozmiar maszyny Wirtualnej Azure | Karty sieciowe są tworzone po utworzeniu hello maszyny Wirtualnej w ramach testowego trybu failover lub przejście w tryb Failover. Witaj liczba kart sieciowych na powitania pracy w trybie failover maszyny Wirtualnej zależy od liczby hello źródła hello karty sieciowe, które maszyna wirtualna ma w czasie hello włączania replikacji. Jeśli musisz usunąć kart interfejsu Sieciowego po włączeniu replikacji, liczba kart na powitania trybu failover maszyny Wirtualnej nie ma wpływu.
Internetowy moduł równoważenia obciążenia | Obsługiwane | Należy tooassociate hello wstępnie skonfigurowane przy użyciu skryptu automatyzacji azure w planie odzyskiwania usługi równoważenia obciążenia.
Wewnętrzny moduł równoważenia obciążenia | Obsługiwane | Należy tooassociate hello wstępnie skonfigurowane przy użyciu skryptu automatyzacji azure w planie odzyskiwania usługi równoważenia obciążenia.
Publiczny adres IP| Obsługiwane | Konieczne tooassociate już istniejącą publicznego adresu IP toohello karty Sieciowej lub utworzyć i skojarzyć toohello kart przy użyciu skryptu automatyzacji azure w planie odzyskiwania.
Grupa NSG w karcie Sieciowej (Resource Manager)| Obsługiwane | Należy tooassociate hello NSG toohello kart przy użyciu skryptu automatyzacji azure w planie odzyskiwania.  
NSG podsieci (Resource Manager i model klasyczny)| Obsługiwane | Należy tooassociate hello NSG toohello kart przy użyciu skryptu automatyzacji azure w planie odzyskiwania.
Grupy NSG na maszynie Wirtualnej (klasyczne)| Obsługiwane | Należy tooassociate hello NSG toohello kart przy użyciu skryptu automatyzacji azure w planie odzyskiwania.
Zastrzeżony adres IP (statyczny adres IP) / zachować źródłowy adres IP | Obsługiwane | Jeśli hello karty Sieciowej na powitania źródłowej maszyny Wirtualnej ma konfiguracji statycznych adresów IP i podsieci docelowej hello ma hello tego samego adresu IP, które są dostępne, jest ona przypisana toohello trybu failover maszyny Wirtualnej. Jeśli hello docelowej podsieci nie ma hello tego samego adresu IP dostępne, jeden z hello dostępnych adresów IP w podsieci hello jest zarezerwowana dla tej maszyny Wirtualnej. Można określić stałego adresu IP w wybranym "elementu zreplikowane > Ustawienia > obliczenia i sieć > interfejsów sieciowych. Można wybrać hello karty Sieciowej i określ hello podsieci i adres IP wybranych przez użytkownika.
Dynamicznego adresu IP| Obsługiwane | Jeśli hello karty Sieciowej na powitania źródłowej maszyny Wirtualnej ma dynamicznej konfiguracji IP, hello karty Sieciowej w tryb failover hello maszyny Wirtualnej jest również dynamiczne domyślnie. Można określić stałego adresu IP w wybranym "elementu zreplikowane > Ustawienia > obliczenia i sieć > interfejsów sieciowych. Można wybrać hello karty Sieciowej i określ hello podsieci i adres IP wybranych przez użytkownika.
Integracja z usługą Traffic Manager | Obsługiwane | Można wstępnie skonfigurować Menedżera ruchu w taki sposób, że ruch hello jest punkt końcowy routingiem toohello w regionie źródła na regularne końcowego podstawę i toohello w region docelowy w przypadku trybu failover.
Azure zarządzanych DNS | Obsługiwane |
Niestandardowe DNS  | Obsługiwane |    
Nieuwierzytelnione serwera Proxy | Obsługiwane | Odwołuje się zbyt[wytycznych sieci.](site-recovery-azure-to-azure-networking-guidance.md)    
Uwierzytelnionego serwera Proxy | Nieobsługiwane | Jeśli hello maszyna wirtualna używa wychodzące połączenie z uwierzytelnionego serwera proxy, nie mogą być replikowane za pomocą usługi Azure Site Recovery.  
TooSite witryny sieci VPN z lokalnymi (z lub bez ExpressRoute)| Obsługiwane | Upewnij się, że Udr hello i grup NSG są skonfigurowane w taki sposób, że ruch odzyskiwania lokacji hello nie jest kierowany lokalnych tooon. Odwołuje się zbyt[wytycznych sieci.](site-recovery-azure-to-azure-networking-guidance.md)  
Połączenie tooVNET sieci Wirtualnej | Obsługiwane | Odwołuje się zbyt[wytycznych sieci.](site-recovery-azure-to-azure-networking-guidance.md)  


## <a name="next-steps"></a>Następne kroki
- Dowiedz się więcej o [sieci wskazówki dotyczące replikowanie maszyn wirtualnych platformy Azure](site-recovery-azure-to-azure-networking-guidance.md)
- Włączyć ochronę obciążeń przez [replikowanie maszyn wirtualnych platformy Azure](site-recovery-azure-to-azure.md)
