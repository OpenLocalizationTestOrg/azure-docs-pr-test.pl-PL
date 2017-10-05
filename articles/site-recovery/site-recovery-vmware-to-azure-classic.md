---
title: "Replikowanie maszyn wirtualnych VMware i serwerów fizycznych do platformy Azure w klasycznym portalu | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób wdrażania usługi Azure Site Recovery do organizowania replikacji, trybu failover i odzyskiwania maszyn wirtualnych VMware lokalnymi i systemem Windows lub Linux serwerów fizycznych do platformy Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a9022c1f-43c1-4d38-841f-52540025fb46
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-vmware-to-azure
ms.openlocfilehash: 73c3fb5cf4056ddb9554f598ec7f173d81802f17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-to-azure-with-azure-site-recovery"></a>Replikowanie maszyn wirtualnych VMware i serwerów fizycznych do platformy Azure z usługą Azure Site Recovery
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](site-recovery-vmware-to-azure.md)
> * [Klasyczny portal](site-recovery-vmware-to-azure-classic.md)
> * [Klasyczny portal (starsze)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Usługa Azure Site Recovery przyczynia się do ciągłości i odzyskiwaniem po awarii (BCDR) odzyskiwania strategią biznesową poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Maszyny można replikować do platformy Azure lub lokalnego pomocniczego centrum danych. Aby uzyskać szybki przegląd, zobacz [co to jest Azure Site Recovery?](site-recovery-overview.md).

## <a name="overview"></a>Omówienie
W tym artykule opisano sposób:

* **Replikowanie maszyn wirtualnych VMware do platformy Azure**: Wdrażanie usługi Site Recovery koordynowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych VMware lokalnego do magazynu Azure.
* **Replikacja serwerów fizycznych do platformy Azure**: Wdrażanie usługi Azure Site Recovery koordynowanie replikacji, trybu failover i odzyskiwania lokalnych systemu Windows i Linux serwerów fizycznych do platformy Azure.

> [!NOTE]
> W tym artykule opisano sposób replikowania na platformie Azure. Jeśli chcesz replikować do dodatkowego centrum danych w maszynach wirtualnych VMware lub serwerach fizycznych systemu Windows i Linux, zobacz [VMware odzyskiwania lokacji do programu VMware](site-recovery-vmware-to-vmware.md).
>
>

Zamieść wszelkie komentarze lub pytania w dolnej części tego artykułu lub na [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="enhanced-deployment"></a>Wdrożenia rozszerzonego
Ten artykuł zawiera instrukcje dotyczące wdrożenia rozszerzonego w klasycznym portalu Azure. Zalecane jest użycie tej wersji dla wszystkich nowych wdrożeń. Jeśli został już wdrożony przy użyciu wcześniejszej wersji starszej wersji, zaleca się przeprowadzenie migracji do nowej wersji. Aby uzyskać więcej informacji na temat migracji, zobacz [VMware odzyskiwania lokacji do starszych klasycznego Azure](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment).

Wdrożenia rozszerzonego jest dużej aktualizacji. Poniżej przedstawiono podsumowanie ulepszeń, które wprowadziliśmy:

* **Bez infrastruktury maszyn wirtualnych na platformie Azure**: dane są replikowane bezpośrednio do konta magazynu platformy Azure. Ponadto jest niepotrzebna do przygotowywania infrastruktury maszyn wirtualnych (na przykład serwer konfiguracji lub główny serwer docelowy) dla replikacji i trybu failover został w miarę potrzeb wdrożenia starszej wersji.  
* **Ujednolicone instalacji**: jedna instalacja zapewnia prostą konfigurację i skalowalność składnikami lokalnymi.
* **Zabezpieczanie wdrożenia**: cały ruch jest szyfrowany i komunikacji zarządzania replikacji są wysyłane za pośrednictwem protokołu HTTPS 443.
* **Punkty odzyskiwania**: Obsługa awarii i odzyskiwania zapewniających spójność aplikacji punkty środowiska systemu Windows i Linux oraz obsługę zarówno pojedynczy spójny konfiguracji maszyny Wirtualnej i wielu maszyn wirtualnych.
* **Testowanie trybu failover**: Obsługa Brak testowy tryb failover na platformie Azure, bez wpływu na produkcję lub wstrzymując replikacji.
* **Nieplanowane przełączenie awaryjne**: Obsługa nieplanowanego trybu failover do platformy Azure z rozszerzoną opcję, aby automatycznie wyłączyć maszyny wirtualne przed trybu failover.
* **Powrót po awarii**: zintegrowane powrotu po awarii, który replikuje tylko zmiany różnicowe lokacji lokalnej.
* **vSphere w wersji 6.0**: ograniczoną obsługę VMware vSphere w wersji 6.0 wdrożeń.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>Jak Usługa Site Recovery pomaga chronić maszyn wirtualnych i serwerów fizycznych?
* VMware Administratorzy mogą skonfigurować poza nim zabezpieczenia do ochrony Azure z firmowych obciążeń i aplikacji uruchomionych na maszynach wirtualnych VMware. Menedżerowie serwera może replikować lokalnych fizycznych serwerów z systemem Windows i Linux na platformie Azure.
* Konsola usługi Azure Site Recovery zapewnia pojedynczą lokalizację prostą konfigurację i zarządzanie replikacji, pracy awaryjnej i procesów odzyskiwania.
* Jeśli replikujesz maszyny wirtualne VMware, które są zarządzane przez serwer vCenter, Usługa Site Recovery może automatycznie odnajdywać tych maszyn wirtualnych. Jeśli komputery znajdują się na hoście ESXi, Site Recovery umożliwia odnajdywanie maszyn wirtualnych na hoście.
* Po uruchomieniu łatwe przechodzenia w tryb failover z infrastruktury lokalnej na platformie Azure, użytkownik może zakończyć się niepowodzeniem (przywracanie) z platformy Azure z powrotem do maszyny Wirtualnej VMware serwerów w lokacji lokalnej.
* Możesz skonfigurować plany odzyskiwania, które grupują obciążeń aplikacji, które są warstwowy na wielu komputerach. Jeśli nie zostanie przez te plany, Usługa Site Recovery zapewnia spójności wielu maszyn wirtualnych, aby obciążeniami tej samej maszyny można odzyskać razem z punktem spójności danych.

## <a name="supported-operating-systems"></a>Obsługiwane systemy operacyjne
### <a name="windows-64-bit-only"></a>Systemu Windows (tylko w 64 bity)
* Windows Server 2008 R2 z dodatkiem SP1 +
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux (64-bitowy tylko)
* Red Hat Enterprise Linux 7.2, 6.7 i 7.1
* CentOS 6.5, 6.6 6.7, 7.0, 7.1 i 7.2
* Oracle Linux przedsiębiorstwa 6.4 i 6.5 systemem Red Hat jądra zgodny lub podzielenie Enterprise jądra wersji 3 (UEK3)
* SUSE Linux Enterprise Server 11 z dodatkiem SP3

## <a name="scenario-architecture"></a>Architektura scenariusza
Składniki scenariusza:

* **Serwer zarządzania lokalnymi**: serwer zarządzania działa składnikami usługi Site Recovery:
  * **Serwer konfiguracji**: koordynowania komunikacji i zarządza procesami replikacji i odzyskiwania danych.
  * **Serwer przetwarzania**: działa jako brama replikacji. Odbiera dane z chronionych maszyn źródłowych; optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania; i wysyła dane replikacji do magazynu Azure. Również obsługę instalacji wypychanej usługi mobilności na chronionych maszynach i przeprowadza automatyczne odnajdywanie maszyn wirtualnych VMware.
  * **Główny serwer docelowy**: służy do obsługi replikacji danych podczas powrotu po awarii z platformy Azure.
    Można także wdrożyć serwer zarządzania, który działa tylko jako serwera przetwarzania skalowania wdrożenia.
* **Usługa mobilności**: ten składnik jest wdrażana na każdej maszynie (maszyny Wirtualnej VMware lub serwerów fizycznych), który chcesz replikować do platformy Azure. Go przechwytywania zapisów danych na komputerze i przekazuje je do serwera przetwarzania.
* **Azure**: nie trzeba tworzyć żadnych maszyn wirtualnych platformy Azure do obsługi replikacji i trybu failover. Usługa Site Recovery obsługuje zarządzanie danymi, a dane są replikowane bezpośrednio do magazynu Azure. Replikowane maszyny wirtualne Azure są automatycznie uruchomione tylko wtedy, gdy występuje trybu failover na platformie Azure. Jednak chcesz awarii platformy Azure z powrotem do lokacji lokalnej, należy skonfigurować maszyny Wirtualnej platformy Azure do działania jako serwer przetwarzania.

Poniższa ilustracja (utworzony przez Henry Robalino) przedstawia interakcje między tymi składnikami:

![Architektura składników](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>Planowanie pojemności
Podczas planowania pojemności, tutaj przez co należy wziąć pod uwagę informacje:

* **Środowisko źródłowe**: Planowanie pojemności lub wymagań maszyny infrastruktury i źródła VMware.
* **Serwer zarządzania**: Planowanie lokalnych serwerów zarządzania systemem składnikami usługi Site Recovery.
* **Przepustowość sieci między źródłowego do docelowego**: Planowanie wymagane dla replikacji między źródłem i Azure przepustowości sieci.

### <a name="source-environment-considerations"></a>Zagadnienia dotyczące środowiska źródłowego
* **Maksymalna szybkość codziennych zmian**: chronionej maszyny można użyć tylko jednego serwera przetwarzania. Serwer pojedynczego procesu może obsługiwać maksymalnie 2 TB danych zmiany na dzień. W związku z tym 2 TB jest maksymalną codziennych danych zmienić szybkość, z której jest obsługiwana dla komputera chronionego.
* **Maksymalna przepustowość**: zreplikowanej maszyny mogą należeć do jednego konta magazynu na platformie Azure. Konto magazynu w warstwie standardowa może obsługiwać maksymalnie 20 000 żądań na sekundę, a firma Microsoft zaleca zachowanie numeru IOPS na maszynie źródłowej do 20 000. Na przykład jeśli maszyna źródłowa z dyskami 5, a każdy dysk generuje 120 IOPS (o rozmiarze 8 KB) w źródle, zostanie w obrębie platformy Azure limitu IOPS dysku 500. Liczba kont magazynu wymagana = Suma źródłowych IOPs/20 000.

### <a name="management-server-considerations"></a>Zagadnienia dotyczące serwera zarządzania
Serwer zarządzania działa składnikami usługi Site Recovery, które optymalizacji danych, replikacji i zarządzania. Powinna być w stanie obsłużyć codzienne pojemności szybkość zmian we wszystkich obciążeń uruchomionych na chronionych komputerach i ma wystarczającą przepustowość do ciągłej replikacji danych do magazynu Azure. W szczególności:

* Serwer przetwarzania odbiera dane replikacji z chronionych maszyn i optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania przed wysłaniem go do platformy Azure. Serwer zarządzania powinien mieć wystarczające zasoby, aby wykonać te zadania.
* Serwer przetwarzania używa dyskowej pamięci podręcznej. Zalecamy dysk pamięci podręcznej oddzielne 600 GB lub więcej obsługi zmian danych przechowywanych w przypadku wąskich gardeł lub awarii. Podczas wdrażania można skonfigurować pamięć podręczną na dowolnym dysku, który ma co najmniej 5 GB miejsca do magazynowania, ale 600 GB jest zalecane minimalne.
* Najlepszym rozwiązaniem zaleca się, że serwer zarządzania znajduje się w tej samej sieci, a segment sieci LAN jako maszyn, które chcesz chronić. Może znajdować się w innej sieci, ale maszyny, które chcesz chronić powinni mieć wgląd sieci L3 do niego.

Zalecenia dotyczące rozmiaru dla serwera zarządzania podsumowano w poniższej tabeli:

| **Procesor CPU serwera zarządzania** | **Pamięci** | **Rozmiar pamięci podręcznej dysku** | **Częstotliwość zmian danych** | **Chronione maszyny** |
| --- | --- | --- | --- | --- |
| 8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz) |16 GB |300 GB |500 GB lub mniej |Wdrażanie serwera zarządzania przy użyciu tych ustawień, aby replikować maszyny mniej niż 100. |
| 12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz) |18 GB |600 GB |500 GB do 1 TB |Wdrażanie serwera zarządzania przy użyciu tych ustawień, aby replikować maszyny 100 150. |
| 16 Vcpu (2 sockets * 8 rdzeni @ 2,5 GHz) |32 GB |1 TB |1 TB do 2 TB |Wdrażanie serwera zarządzania przy użyciu tych ustawień, aby replikować maszyny 150 – 200. |
| Wdrażanie inny serwer przetwarzania | | |> 2 TB |Wdrażanie serwerów dodatkowych procesów, Jeśli replikujesz ponad 200 maszyn lub zmiana codziennych danych szybkość przekracza 2 TB. |

Gdzie:

* Każda maszyna źródłowa jest skonfigurowany z 3 dyski 100 GB.
* My używamy najlepszymi magazynu 8 dysków SAS 10 000 obr. / min z RAID 10 dla pamięci podręcznej dysku pomiarów.

### <a name="network-bandwidth-from-source-to-target"></a>Przepustowość sieci między źródłowego do docelowego
Upewnij się, że obliczenia przepustowości, które będą wymagane dla replikacji początkowej i replikacja różnicowa przy użyciu [planisty wydajności](site-recovery-capacity-planner.md).

#### <a name="throttling-bandwidth-used-for-replication"></a>Ograniczanie przepustowości używanych w przypadku replikacji
Ruch VMware zreplikowanej w systemie Azure przechodzi przez serwer określonego procesu. Możesz ograniczyć przepustowość, która jest dostępna dla replikacji usługi Site Recovery na tym serwerze w następujący sposób:

1. Otwieranie przystawki MMC kopia zapasowa Azure firmy Microsoft na serwerze zarządzania głównego lub na serwerze zarządzania systemem dodatkowe zainicjowana serwerów procesu. Domyślnie skrót do usługi Kopia zapasowa Microsoft Azure jest tworzony na pulpicie. Alternatywnie można znaleźć je w C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. W przystawce kliknij pozycję **Zmień właściwości**.

    ![Wartość ograniczenia przepustowości Zmień właściwości](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. Na **ograniczania** karcie, określ przepustowości, który może służyć do usługi Site Recovery replikacji oraz planowanie zastosowania.

    ![Wartość ograniczenia przepustowości replikacji](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

Można również ustawić ograniczanie za pomocą programu PowerShell. Oto przykład:

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>Maksymalizacja przepustowości
Aby zwiększyć przepustowość wykorzystywany do replikacji za pomocą usługi Azure Site Recovery, należy zmienić wartość klucza rejestru.

Następujący klucz określa liczbę wątków na replikację dysku, które są używane podczas replikacji:

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 W sieci o nadmiarowych zasobach ten klucz rejestru musi zostać zmienione z jej wartości domyślnej. Firma Microsoft obsługuje maksymalnie 32.  

Aby uzyskać więcej informacji o planowaniu pojemności szczegółowe, zobacz [planowania pojemności Site Recovery](site-recovery-capacity-planner.md).

### <a name="additional-process-servers"></a>Serwery dodatkowych procesów
Jeśli zachodzi konieczność ochrony ponad 200 maszyn lub częstotliwość codziennych zmian jest większa, że 2 TB, można dodać dodatkowych serwerów do obsługi obciążenia. Aby skalować w poziomie, można:

* Zwiększ liczbę serwerów zarządzania. Na przykład można chronić maksymalnie 400 maszyn przy użyciu dwóch serwerów zarządzania.
* Dodaj serwer dodatkowych procesów i ich używać do obsługi ruchu zamiast (lub oprócz) serwera zarządzania.

W tej tabeli opisano scenariusz, w którym:

* Konfigurowanie oryginalnego serwera zarządzania do użycia jako tylko serwer konfiguracji.
* Konfigurowanie serwera dodatkowych procesów.
* Możesz skonfigurować chronionych maszyn wirtualnych do używania serwera dodatkowych procesów.
* Każda maszyna chronionego źródła jest skonfigurowany z trzech dysków 100 GB.

| **Oryginalny serwer zarządzania**<br/><br/>(serwer konfiguracji) | **Serwer przetwarzania dodatkowe** | **Rozmiar pamięci podręcznej dysku** | **Częstotliwość zmian danych** | **Chronione maszyny** |
| --- | --- | --- | --- | --- |
| 8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz), 16 GB pamięci RAM |4 Vcpu (2 sockets * 2 rdzenie @ 2,5 GHz), 8 GB pamięci RAM |300 GB |250 GB lub mniej |Można replikować maszyny 85 lub mniej. |
| 8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz), 16 GB pamięci RAM |8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz), 12 GB pamięci RAM |600 GB |250 GB do 1 TB |Można replikować maszyny 85 150. |
| 12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz), 18 GB pamięci RAM |12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz) 24 GB pamięci RAM |1 TB |1 TB do 2 TB |Można replikować maszyny 150 225. |

Jak skalować serwery zależy od swoich preferencji modelu skalowania w górę i skalowania w poziomie. Skalowanie w górę przez wdrożenie kilku wysokiej klasy zarządzania i serwerów procesu lub skalowanie w poziomie przez wdrożenie więcej serwerów z mniejszą liczbą zasobów. Na przykład: Jeśli trzeba chronić 220 maszyny, można wykonać jedną z następujących czynności:

* Konfigurowanie oryginalnego serwera zarządzania z 12 Vcpu i 18 GB pamięci RAM. Skonfiguruj serwer dodatkowych procesów 12 Vcpu i 24 GB pamięci RAM. Skonfiguruj chronione maszyny do korzystania z dodatkowych procesów serwera.
* Skonfiguruj dwa serwery zarządzania (Vcpu, 16 GB pamięci RAM 2 x 8) i dwa serwery dodatkowych procesów (Vcpu i 4vCPUs x 1, aby obsłużyć 135 + 85 maszyny (220) 1 x 8). Skonfiguruj chronione maszyny, aby korzystać z dodatkowych procesów serwerów.

Postępuj zgodnie z instrukcjami [wdrażania serwerów dodatkowych procesów](#deploy-additional-process-servers) serwera dodatkowych procesów.

## <a name="before-you-start-deployment"></a>Przed rozpoczęciem wdrażania
Następująca tabela zawiera podsumowanie wymagań wstępnych dotyczących wdrażania tego scenariusza.

### <a name="azure-prerequisites"></a>Wymagania wstępne platformy Azure
| **Wymagania wstępne** | **Szczegóły** |
| --- | --- |
| **Konto platformy Azure** |Potrzebujesz konta platformy [Microsoft Azure](https://azure.microsoft.com/). Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). Aby uzyskać więcej informacji o cenach usługi Site Recovery, zobacz [usługi Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Magazyn platformy Azure** |Potrzebujesz konta magazynu usługi Azure Storage do przechowywania replikowanych danych. Replikowane dane są przechowywane w magazynie Azure, a maszyny wirtualne Azure są uruchomione podczas pracy awaryjnej. <br/><br/>Potrzebujesz [standardowego konta magazynu geograficznie nadmiarowego](../storage/storage-redundancy.md#geo-redundant-storage). Konto musi znajdować się w tym samym regionie co usługa Site Recovery i być skojarzone z tą samą subskrypcją. Replikacja do kont magazynu w warstwie premium nie jest obecnie obsługiwane i nie powinny być używane.<br/><br/>Nie obsługujemy Przenoszenie konta magazynu utworzone za pomocą [portalu Azure](../storage/storage-create-storage-account.md) między grupami zasobów. Aby uzyskać więcej informacji, zobacz [wprowadzenie do usługi Microsoft Azure Storage](../storage/storage-introduction.md).<br/><br/> |
| **Sieć platformy Azure** |Potrzebujesz sieci wirtualnej platformy Azure, które maszyny wirtualne Azure będą się łączyć podczas pracy awaryjnej. Sieć wirtualna platformy Azure musi znajdować się w tym samym regionie co magazyn usługi Site Recovery.<br/><br/>Aby zakończyć się niepowodzeniem po trybu failover na platformie Azure, należy sieci VPN połączenia (lub usługa Azure ExpressRoute) skonfigurowana z sieci platformy Azure do lokacji lokalnej. |

### <a name="on-premises-prerequisites"></a>Lokalne wymagania wstępne
| **Wymagania wstępne** | **Szczegóły** |
| --- | --- |
| **Serwer zarządzania** |Należy lokalnego serwera Windows 2012 R2, który jest uruchomiony na maszynie wirtualnej lub serwerze fizycznym. Wszystkie składniki usługi Site Recovery lokalne są instalowane na tym serwerze zarządzania.<br/><br/> Zaleca się wdrożenie serwera jako wysokiej dostępności maszyny Wirtualnej VMware. Powrót po awarii do lokacji lokalnej z platformy Azure jest zawsze do maszyn wirtualnych VMware niezależnie od tego, czy zostanie przełączone do trybu failover maszyn wirtualnych lub serwerach fizycznych. Jeśli nie skonfigurujesz serwer zarządzania jako maszyny Wirtualnej VMware, należy skonfigurować oddzielny główny serwer docelowy jako maszyny Wirtualnej VMware na odbieranie ruchu w przypadku powrotu po awarii.<br/><br/>Serwer nie powinien być kontrolerem domeny.<br/><br/>Serwer powinien mieć statyczny adres IP.<br/><br/>Nazwa hosta serwera powinny być 15 znaków lub mniej.<br/><br/>Tylko ustawień regionalnych systemu operacyjnego należy angielskiej wersji językowej.<br/><br/>Serwer zarządzania wymaga dostępu do Internetu.<br/><br/>Potrzebny jest wychodzący dostęp z serwera w następujący sposób: tymczasowego dostępu na HTTP 80 podczas instalacji składników usługi Site Recovery (do pobrania MySQL); stałe wychodzący dostęp na protokołu HTTPS 443 do zarządzania replikacją; bieżące wychodzący dostęp do na HTTPS 9443 dla ruchu replikacji (ten port może być modyfikowany).<br/><br/> Upewnij się, że te adresy URL są dostępne z serwera zarządzania: <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>-https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.mysql.com/Get/Archives/MySQL-5.5/MySQL-5.5.37-Win32.msi](https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>Jeśli masz reguły zapory oparte na adresie IP na serwerze, sprawdź, czy reguły zezwalają na komunikację z platformą Azure. Musisz zezwolić na użycie [zakresów adresów IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653) oraz portu 443 protokołu HTTPS. Należy również dozwolonych zakresy adresów IP dla regionu Azure Twojej subskrypcji i zachodnie stany USA. Adres URL [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi](https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi") jest pobierania MySQL. |
| **Host VMware vCenter/ESXi** |Należy co najmniej jeden VMware vSphere ESX/ESXi funkcji hypervisor maszyn wirtualnych VMware, zarządzanie systemem w wersji 6.0, 5.5 lub 5.1 ESX/ESXi z najnowszymi aktualizacjami.<br/><br/> Zaleca się wdrożenie serwera VMware vCenter do zarządzania hostach ESXi. VCenter w wersji 6.0 lub 5.5 powinna ona działać z najnowszymi aktualizacjami.<br/><br/>Warto zauważyć, że usługa Site Recovery nie obsługuje vCenter nowe funkcje vSphere w wersji 6.0, takich jak między vCenter vMotion, woluminy i magazynu usługi rejestracji urządzeń. Obsługa odzyskiwania lokacji jest ograniczona do funkcji, które były również dostępne w wersji 5.5. |
| **Chronione maszyny** |**Azure**<br/><br/>Komputery, które chcesz chronić powinna być zgodna z [wymagania wstępne platformy Azure](site-recovery-prereq.md) do tworzenia maszyn wirtualnych platformy Azure.<br><br/>Jeśli chcesz połączyć z maszynami wirtualnymi Azure po pracy awaryjnej, należy włączyć połączenia pulpitu zdalnego w zaporze lokalnej.<br/><br/>Pojemności poszczególnych dysków na chronionych komputerach nie powinny przekraczać 1023 GB. Maszyna wirtualna może mieć maksymalnie 64 dyski (w związku z tym maksymalnie 64 TB pojemności). Jeśli masz dysków większych niż 1 TB, należy wziąć pod uwagę przy użyciu replikacji bazy danych, takich jak SQL Server AlwaysOn lub Oracle Data Guard.<br/><br/>Minimalna 2 GB wolnego miejsca na dysku instalacyjnym do instalacji składnika.<br/><br/>Klastry udostępnionych dysków gościa nie są obsługiwane. W przypadku wdrożenia klastra, należy wziąć pod uwagę przy użyciu replikacji bazy danych, takich jak SQL Server AlwaysOn lub Oracle Data Guard.<br/><br/>Unified Extensible Firmware Interface (UEFI) / Extensible Firmware Interface rozruchu nie jest obsługiwana.<br/><br/>Nazwy komputerów powinna zawierać od 1 do 63 znaków (litery, cyfry i łączniki). Nazwa musi zaczynać się literą lub cyfrą i kończyć literą lub cyfrą. Po włączeniu ochrony komputera, można zmodyfikować nazwę platformy Azure.<br/><br/>**Maszyny wirtualne VMware**<br/><br>Musisz zainstalować VMware vSphere PowerCLI 6.0. na serwerze zarządzania (serwer konfiguracji).<br/><br/>Maszyny wirtualne VMware, które chcesz chronić powinien mieć narzędzi VMware zainstalowany i uruchomiony.<br/><br/>Jeśli źródło maszyny Wirtualnej ma wiele kart, po przejściu w tryb failover Azure zostanie przekonwertowane na jedną kartę Sieciową.<br/><br/>Jeśli dysk iSCSI chronionych maszyn wirtualnych, Usługa Site Recovery konwertuje chronionego dysku iSCSI maszyny Wirtualnej do pliku VHD w przypadku niepowodzenia maszyny Wirtualnej za pośrednictwem usługi Azure. Jeśli obiekt docelowy iSCSI może być osiągnięta poprzez maszyny Wirtualnej Azure, zostanie nawiązać połączenie obiektu docelowego iSCSI i zasadniczo Zobacz dwa dyski: dysku VHD na maszynie Wirtualnej platformy Azure i dysku źródłowego iSCSI. W takim przypadku należy rozłączyć miejsce docelowe iSCSI, która pojawia się na maszynie Wirtualnej Azure przełączona w tryb failover.<br/><br/>Aby uzyskać więcej informacji o uprawnieniach użytkownika VMware odzyskiwania tej lokacji musi, zobacz [uprawnień VMware vCenter dostępu](#vmware-permissions-for-vcenter-access).<br/><br/> **Windows Server maszyny (maszyny Wirtualnej VMware lub serwerów fizycznych)**<br/><br/>Serwer powinien działać obsługiwanych 64-bitowym systemie operacyjnym: Windows Server 2012 R2, Windows Server 2012 lub Windows Server 2008 R2 z na co najmniej z dodatkiem SP1.<br/><br/>System operacyjny powinien być zainstalowany na dysku C, a dysk systemu operacyjnego powinien być dyskiem podstawowym z systemem Windows. (Systemu operacyjnego nie można zainstalować na dysku dynamicznym systemu Windows.)<br/><br/>W przypadku komputerów z systemem Windows Server 2008 R2 musisz mieć .NET Framework 3.5.1 zainstalowane.<br/><br/>Należy podać nazwę konta administratora (musi być administratorem lokalnym na komputerze z systemem Windows) dla instalacji wypychanej usługi mobilności na serwerach z systemem Windows. Podane konto jest kontem domeny, należy najpierw wyłączyć kontroli dostępu użytkownika zdalnego na komputerze lokalnym. Aby uzyskać więcej informacji, zobacz [zainstalować instalacji wypychanej usługi mobilności](#install-the-mobility-service-with-push-installation).<br/><br/>Dysk RDM usługi Site Recovery obsługuje maszyn wirtualnych. Podczas powrotu po awarii usługa Site Recovery będzie używał dysk RDM, jeśli oryginalne źródło maszyny Wirtualnej i dysk RDM są dostępne. Jeśli nie są dostępne, podczas powrotu po awarii, Usługa Site Recovery utworzy nowy plik VMDK dla każdego dysku.<br/><br/>**Maszyny z systemem Linux**<br/><br/>Należy obsługiwanych 64-bitowym systemie operacyjnym: Red Hat Enterprise Linux 6.7; Centos 6.5, 6.6 lub 6.7; Oracle Linux przedsiębiorstwa 6.4 lub 6.5 systemem Red Hat jądra zgodny lub podzielenie Enterprise jądra wersji 3 (UEK3); SUSE Linux Enterprise Server 11 z dodatkiem SP3.<br/><br/>plik/etc/hosts na chronionych komputerach powinien zawierać wpisów, które mapują nazwę hosta lokalnego na adresy IP skojarzone z wszystkich kart sieciowych. <br/><br/>Jeśli chcesz nawiązać połączenie maszyny wirtualnej platformy Azure systemem Linux po trybu failover przy użyciu klienta Secure Shell (ssh), upewnij się, że Usługa Secure Shell na chronionej maszynie ma ustawione uruchamianie automatycznie przy rozruchu systemu oraz że reguły zapory zezwalają na ssh połączenia z nią.<br/><br/>Ochrony można włączyć tylko dla systemu Linux maszyn z następującego magazynu: plików systemowych (EXT3, ETX4, ReiserFS, XFS); Urządzenia oprogramowania wielościeżkowego mapowania (wielościeżkowego); Menedżer woluminów (LVM2). Serwery fizyczne z HP CCISS kontrolera magazynu nie są obsługiwane. System plików ReiserFS jest obsługiwany tylko w systemie SUSE Linux Enterprise Server 11 z dodatkiem SP3.<br/><br/>Dysk RDM usługi Site Recovery obsługuje maszyn wirtualnych. Podczas powrotu po awarii dla systemu Linux Usługa Site Recovery nie używać ponownie dysk RDM. Zamiast tego tworzy nowy plik VMDK dla każdego odpowiedniego dysk RDM. |

Tylko w przypadku maszyny Wirtualnej systemu Linux: Sprawdź, czy ustawienie disk.enableUUID=true jest ustawiony w parametrach konfiguracji maszyny wirtualnej w środowisku programu VMware. Jeśli ten wiersz nie istnieje, dodaj ją. Jest to wymagane, aby zapewnić spójne UUID VMDK tak, aby go instaluje poprawnie. Bez tego ustawienia powrotu po awarii spowoduje, że pełne pobieranie nawet, jeśli maszyna wirtualna jest dostępna na lokalnym. Dodanie to ustawienie zapewnia, że tylko zmiany różnicowe są przekazywane ponownie podczas powrotu po awarii.

## <a name="step-1-create-a-vault"></a>Krok 1: Tworzenie magazynu
1. Zaloguj się w witrynie [Azure Portal](https://manage.windowsazure.com/).
2. Rozwiń węzeł **usług danych** > **usług odzyskiwania** i kliknij przycisk **magazynie usługi Site Recovery**.
3. Kliknij pozycje **Utwórz nowe** > **Szybkie tworzenie**.
4. W polu **Nazwa** wprowadź przyjazną nazwę identyfikującą magazyn.
5. W polu **Region** wybierz region geograficzny dla magazynu. Aby sprawdzić obsługiwane regiony, zobacz [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Kliknij pozycję **Utwórz magazyn**.
    ![Tworzenie magazynu](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

Sprawdź informacje na pasku stanu, aby potwierdzić pomyślne utworzenie magazynu. Magazyn będzie wyświetlany jako **Active** w głównym **usług odzyskiwania** strony.

## <a name="step-2-set-up-an-azure-network"></a>Krok 2: Konfigurowanie sieci platformy Azure
Skonfiguruj sieć platformy Azure, aby maszyny wirtualne platformy Azure zostanie podłączony do sieci po pracy awaryjnej i tak, aby w przypadku powrotu po awarii do lokacji lokalnej mogą działać zgodnie z oczekiwaniami.

1. W portalu Azure wybierz **Utwórz sieć wirtualną** i określić nazwę sieciową, zakres adresów IP i nazwy podsieci.
2. Jeśli trzeba powrotu po awarii, należy dodać do sieci VPN/ExpressRoute. Nawet po trybu failover do sieci można dodać sieci VPN/ExpressRoute.

Aby uzyskać więcej informacji o sieci platformy Azure, zobacz [omówienie sieci wirtualnej](../virtual-network/virtual-networks-overview.md).

> [!NOTE]
> [Migracja sieci](../azure-resource-manager/resource-group-move-resources.md) w grupach zasobów w ramach tej samej subskrypcji lub w różnych subskrypcjach nie jest obsługiwana dla sieci używanych do wdrażania usługi Site Recovery.
>
>

## <a name="step-3-install-the-vmware-components"></a>Krok 3: Instalowanie składników programu VMware
Jeśli chcesz replikować maszyny wirtualne VMware, wykonaj następujące czynności na serwerze zarządzania:

1. [Pobierz](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) i zainstaluj VMware vSphere PowerCLI 6.0.
2. Uruchom ponownie serwer.

## <a name="step-4-download-a-vault-registration-key"></a>Krok 4: Pobieranie klucza rejestracji magazynu
1. Z serwera zarządzania Otwórz konsolę usługi Site Recovery na platformie Azure. Na **usług odzyskiwania** kliknij magazyn, aby otworzyć **Szybki Start** strony. Można również otworzyć **Szybki Start** strony w dowolnym momencie, klikając ikonę.

    ![Ikonę szybkiego startu](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. Na **Szybki Start** kliknij przycisk **przygotowanie zasobów docelowych** > **Pobierz klucz rejestracji**. Plik rejestracji jest generowany automatycznie. Jest on prawidłowy przez pięć dni po jego wygenerowaniu.

## <a name="step-5-install-the-management-server"></a>Krok 5: Instalowanie serwera zarządzania
> [!TIP]
> Upewnij się, że te adresy URL są dostępne z serwera zarządzania:
>
> * *.hypervrecoverymanager.windowsazure.com
> * *.accesscontrol.windows.net
> * *.backup.windowsazure.com
> * *.blob.core.windows.net
> * *.store.core.windows.net
> * https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi
> * https://www.msftncsi.com/ncsi.txt
>
>



>[!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Setup-Registration/player]



1. Na **Szybki Start** pozycję Pobierz plik instalacyjny ujednoliconego do serwera.
2. Uruchom plik instalacyjny, aby uruchomić Instalatora **instalacja Unified usługi Site Recovery** kreatora.
3. W obszarze **Przed rozpoczęciem** wybierz pozycję **Zainstaluj serwer konfiguracji i serwer przetwarzania**.

   ![Przed rozpoczęciem](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. W **licencji na oprogramowanie innych firm**, kliknij przycisk **akceptuję** do pobrania i zainstalowania MySQL.

    ![Oprogramowanie innych producentów](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. W **rejestracji**, wyszukaj i wybierz klucz rejestracji, który został pobrany z magazynu.

    ![Rejestracja](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. W **internetowe**, określ, jak dostawca uruchomiony na serwerze konfiguracji będą łączyć się usługi Azure Site Recovery za pośrednictwem Internetu.

   * Jeśli chcesz łączyć się z serwerem proxy aktualnie skonfigurowanym na maszynie, wybierz opcję **Połącz przy użyciu istniejących ustawień serwera proxy**.
   * Jeśli chcesz, aby dostawca łączył się bezpośrednio, wybierz opcję **Połącz bezpośrednio bez serwera proxy**.
   * Jeśli istniejący serwer proxy wymaga uwierzytelnienia, lub jeśli chcesz użyć niestandardowego serwera proxy dla połączenia dostawcy, wybierz opcję **Połącz przy użyciu niestandardowych ustawień serwera proxy**.
     * Jeśli używasz niestandardowego serwera proxy, należy określić adres, port oraz poświadczenia.
     * Jeśli używasz serwera proxy, możesz już zezwolono następujące adresy URL:
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![Zapora](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. W **Sprawdzanie wymagań wstępnych**, Instalator zostanie uruchomiony wyboru, aby upewnić się, że można uruchomić instalacji.

    ![Wymagania wstępne](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     Jeśli zostanie wyświetlone ostrzeżenie dotyczące **kontroli synchronizacji czasu globalnego**, sprawdź, czy czas zegara systemowego (ustawienia **Data i godzina**) jest taki sam jak dla strefy czasowej.

     ![Czas synchronizacji problem](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. W **konfiguracji MySQL**, tworzenie poświadczeń do logowania się na wystąpienie serwera MySQL, który zostanie zainstalowany.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. W obszarze **Szczegóły środowiska** wybierz, czy zamierzasz replikować maszyny wirtualne programu VMware. Jeśli Instalator sprawdza, czy zainstalowano PowerCLI 6.0.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. W obszarze **Lokalizacja instalacji** wybierz, gdzie mają zostać zainstalowane pliki binarne i gdzie ma być przechowywana pamięć podręczną. Można wybrać dysk, który ma co najmniej 5 GB dostępnego miejsca na dysku, ale zalecamy dysk pamięci podręcznej z co najmniej 600 GB dostępnego miejsca na dysku.

   ![Lokalizacja instalacji](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. W **wybór sieci**, określ odbiornika (kartę sieciową i SSL port) na którym serwer konfiguracji będzie wysyłać i odbierać dane replikacji. Można zmodyfikować domyślny port (9443). Oprócz tego portu przez serwer sieci web, która organizuje operacje replikacji użyty zostanie port 443. Nie należy używać 443 do odbierania ruchu związanego z replikacją.

    ![Wybór sieci](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. W obszarze **Podsumowanie** przejrzyj informacje i kliknij przycisk **Zainstaluj**. Po zakończeniu instalacji generowane jest hasło. Będzie on potrzebny podczas włączania replikacji, dlatego skopiuj go i przechowuj go w bezpiecznej lokalizacji.

   ![Podsumowanie](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> Można skonfigurować serwera proxy agenta usług odzyskiwania Microsoft Azure.
> Po zakończeniu instalacji uruchom powłokę usług odzyskiwania Microsoft Azure, z menu Start systemu Windows. W otwartym oknie polecenie Uruchom następujący zestaw poleceń, aby skonfigurować ustawienia serwera proxy.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-the-command-line"></a>Uruchom Instalatora z wiersza polecenia
Kreator ujednoliconego można również uruchomić z wiersza polecenia w następujący sposób:

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]

Gdzie:

* /ServerMode: obowiązkowy. Określa, czy instalacji należy zainstalować serwer konfiguracji i procesu lub tylko do procesu serwera (używane do instalowania dodatkowych procesów serwerów). Wartości wejściowe: CS, PS.
* InstallDrive: obowiązkowy. Określa folder, w którym są zainstalowane składniki.
* / MySQLCredFilePath. Obowiązkowy. Określa ścieżkę do pliku, w którym są przechowywane poświadczenia serwera MySQL. Pobierz szablon, aby utworzyć plik.
* / VaultCredFilePath. Obowiązkowy. Lokalizacja pliku poświadczeń magazynu.
* /EnvType. Obowiązkowy. Typ instalacji. Wartości: VMware, NonVMware.
* / PSIP i /CSIP. Obowiązkowy. Adres IP serwera przetwarzania i serwer konfiguracji.
* /PassphraseFilePath. Obowiązkowy. Lokalizacja pliku hasło.
* / ByPassProxy. Opcjonalny. Określa serwer zarządzania, który łączy do platformy Azure bez serwera proxy.
* /ProxySettingsFilePath. Opcjonalny. Określa ustawienia dla niestandardowego serwera proxy (domyślny serwer proxy na serwerze, który wymaga uwierzytelniania) lub niestandardowego serwera proxy.

## <a name="step-6-set-up-credentials-for-the-vcenter-server"></a>Krok 6: Konfigurowanie poświadczenia dla serwera vCenter
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

Serwer przetwarzania może automatycznie odnajdować maszyn wirtualnych VMware, które są zarządzane przez serwer vCenter. Automatycznego wykrywania usługi Site Recovery potrzebuje konta i poświadczenia, które mają dostęp do serwera vCenter. Nie jest to istotne, Jeśli replikujesz tylko na serwerach fizycznych.

Aby ustawić konta i poświadczeń:

1. Na serwerze vCenter tworzenie roli (**Azure_Site_Recovery**) na poziomie vCenter z [wymagane uprawnienia](#vmware-permissions-for-vcenter-access).
2. Przypisz **Azure_Site_Recovery** do użytkownika vCenter.

   > [!NOTE]
   > VCenter konto użytkownika, który ma rolę tylko do odczytu można uruchomić trybu failover bez zamykania chronionych maszyn źródłowych. Jeśli chcesz wyłączyć te maszyny, konieczne będzie Azure_Site_Recovery roli. Jeśli jest tylko migrowania maszyn wirtualnych VMware do platformy Azure i nie ma potrzeby wykonaj powrót po awarii, wystarczy rolę tylko do odczytu.
   >
   >
3. Aby dodać konto, otwórz **cspsconfigtool**. Jest dostępna jako skrót na pulpicie i znajduje się w folderze \home\svsystems\bin [Lokalizacja instalacji].
4. Na karcie **Zarządzaj kontami** kliknij pozycję **Dodaj konto**.

    ![Dodawanie konta](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. W **szczegóły konta**, Dodaj poświadczenia, które mogą służyć do uzyskiwania dostępu do serwera vCenter. Może potrwać ponad 15 minut dla nazwy konta, które mają być widoczne w portalu. Natychmiastową aktualizację, kliknij przycisk **Odśwież** na **serwery konfiguracji** kartę.

    ![Szczegóły](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>Krok 7: Dodawanie serwery vCenter i hostach ESXi
Jeśli replikujesz maszyny wirtualne VMware, należy dodać serwer vCenter (lub hosta ESXi).

1. Na **serwerów** > **serwery konfiguracji** wybierz opcję **Dodaj serwer vCenter**.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. Dodaj serwer vCenter lub szczegóły hosta ESXi, nazwę konta, które określono, aby uzyskać dostęp serwer vCenter w poprzednim kroku, a serwer przetwarzania, który będzie używany do odnajdywanie maszyn wirtualnych VMware, które są zarządzane przez serwer vCenter. Serwer vCenter lub hosta ESXi powinien znajdować się w tej samej sieci co serwer, na którym jest zainstalowany serwer przetwarzania.

   > [!NOTE]
   > W przypadku dodawania serwera vCenter lub hosta ESXi przy użyciu konta, które nie ma uprawnień administratora na serwerze vCenter lub hosta, upewnij się, że vCenter lub ESXi konta mają następujące uprawnienia: centrum danych, Magazyn danych, Folder, Jost, sieci, zasobów, Maszyna wirtualna i vSphere rozproszonego przełącznika. Serwer vCenter musi mieć włączone uprawnienia widoków magazynu.
   >
   >

    ![Dodanie serwera vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. Po zakończeniu odnajdowania serwera vCenter zostaną wyświetlone na **serwery konfiguracji** kartę.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>Krok 8: Tworzenie grupy ochrony
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

Logiczne grupowanie maszyn wirtualnych lub serwerach fizycznych, które mają być chronione przy użyciu tych samych ustawień ochrony są grupy ochrony. Zastosuj ustawienia ochrony do grupy ochrony, a te ustawienia są stosowane do wszystkich komputerów (wirtualnych lub fizycznych), dodanie do grupy.

1. Przejdź do **chronione elementy** > **grupy ochrony** i kliknij ikonę, aby dodać grupę ochrony.

    ![Tworzenie grupy ochrony](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. Na **ustawień grupy ochrony określ** Określ nazwę grupy. W **z** listy rozwijanej wybierz serwer konfiguracji, na którym chcesz utworzyć grupę. **Docelowy** jest Microsoft Azure.

    ![Ustawienia grupy ochrony](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. Na **Określanie ustawień replikacji** Skonfiguruj ustawienia replikacji, które będą używane dla wszystkich komputerów w grupie.

    ![Grupy ochrony następuje replikacja](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **Spójność wielu maszyn wirtualnych**: Jeśli włączenie tej funkcji, tworzy punktów odzyskiwania zapewniających spójność aplikacji udostępnione na komputerach w grupie ochrony. To ustawienie jest najodpowiedniejsze, gdy wszystkie komputery w grupie ochrony są tego samego obciążenia. Wszystkie maszyny zostaną przywrócone do tego samego punktu danych. Jest to możliwe jest replikowanie maszyn wirtualnych VMware lub serwerów fizycznych (Windows lub Linux).
   * **Próg RPO**: ustawia cel punktu odzyskiwania. Alerty są generowane, gdy replikacji ciągłej ochrony danych przekracza skonfigurowaną wartość progu cel punktu odzyskiwania.
   * **Przechowywania punktu odzyskiwania**: Określa okna przechowywania. Chronione maszyny można odzyskać do dowolnego punktu, w tym przedziale czasu.
   * **Częstotliwość migawek spójnych z aplikacją**: Określa, jak często punkty odzyskiwania, zawierające migawki spójne z aplikacjami zostaną utworzone.

Po wybraniu znacznik wyboru grupy ochrony zostanie utworzona z podanej nazwy. Ponadto drugiej grupy ochrony jest tworzony z nazwą *Nazwa grupy ochrony*- powrotu po awarii. Tej grupy ochrony jest używana, jeśli awarii w celu przywrócenia lokacji lokalnej po w tryb failover na platformie Azure. Można monitorować grup ochrony, jak są tworzone na **chronione elementy** strony.

## <a name="step-9-install-the-mobility-service"></a>Krok 9: Instalowanie usługi mobilności
Aby włączyć ochronę dla maszyn wirtualnych i serwerów fizycznych, należy najpierw zainstalować usługę mobilności. Można to zrobić na dwa sposoby:

* Push i automatycznie Zainstaluj usługę na każdym komputerze z serwerem przetwarzania. Dodaj maszyny do grupy ochrony i już korzystania odpowiednią wersję usługi mobilności, występują nie instalacji wypychanej. Można również przeprowadzenie automatycznej instalacji usługi za pomocą metodę wypychania przedsiębiorstwa, takich jak WSUS lub System Center Configuration Manager. Upewnij się, że po skonfigurowaniu serwera zarządzania przed tym.
* Zainstaluj usługę ręcznie na każdym komputerze, który chcesz chronić. Upewnij się, że po skonfigurowaniu serwera zarządzania przed tym.

### <a name="install-the-mobility-service-with-push-installation"></a>Zainstaluj instalacji wypychanej usługi mobilności
Podczas dodawania komputerów do grupy ochrony, usługa mobilności jest wypychana i automatycznie zainstalowane na każdym komputerze za pomocą serwera przetwarzania.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Przygotowanie do wypychania automatycznego na maszynach z systemem Windows
Aby przygotować maszyny z systemem Windows, dzięki czemu można automatycznie zainstalować usługi mobilności za pomocą serwera przetwarzania:

1. Utwórz konta używanego przez serwer przetwarzania dostęp do komputera. Konto musi mieć uprawnienia administratora (lokalnego lub domeny). Te poświadczenia są używane tylko dla instalacji wypychanej usługi mobilności.

   > [!NOTE]
   > Jeśli nie używasz konta domeny, należy wyłączyć kontroli dostępu użytkownika zdalnego na komputerze lokalnym. Aby to zrobić, w rejestrze w HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, Dodaj wpis DWORD LocalAccountTokenFilterPolicy o wartości 1 w obszarze. Aby dodać wpis rejestru polecenia Otwórz interfejs wiersza polecenia lub przy użyciu programu PowerShell, wpisz  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .
   >
   >
2. Zapory systemu Windows na komputerze, który chcesz chronić, wybierz **Zezwalaj aplikacji lub funkcji za pośrednictwem zapory**i Włącz **udostępnianie plików i drukarek** i **zarządzania systemem Windows Instrumentacja**. Dla maszyn, które należą do domeny można skonfigurować zasady zapory z obiektu zasad grupy.

   ![Ustawienia zapory](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. Dodaj utworzone konto:

   * Otwórz narzędzie **cspsconfigtool**. Jest dostępna jako skrót na pulpicie i znajduje się w folderze \home\svsystems\bin [Lokalizacja instalacji].
   * Na karcie **Zarządzaj kontami** kliknij pozycję **Dodaj konto**.
   * Dodaj utworzone konto. Po dodaniu konta, musisz podać poświadczenia, po dodaniu komputera do grupy ochrony.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Przygotowanie do wypychania automatycznego na serwerach z systemem Linux
1. Upewnij się, że maszyny systemu Linux, które chcesz chronić jest obsługiwane zgodnie z opisem w [lokalne wstępnych](#on-premises-prerequisites). Upewnij się, że istnieje połączenie sieciowe między komputerem, który chcesz chronić i serwera zarządzania, który uruchamia serwer przetwarzania.
2. Utwórz konta używanego przez serwer przetwarzania dostęp do komputera. Konto powinno być użytkownika głównego na serwer źródłowy z systemem Linux. Te poświadczenia są używane tylko dla instalacji wypychanej usługi mobilności.

   * Otwórz narzędzie **cspsconfigtool**. Jest dostępna jako skrót na pulpicie i znajduje się w folderze \home\svsystems\bin [Lokalizacja instalacji].
   * Na karcie **Zarządzaj kontami** kliknij pozycję **Dodaj konto**.
   * Dodaj utworzone konto. Po dodaniu konta, musisz podać poświadczenia, po dodaniu komputera do grupy ochrony.
3. Sprawdź, czy plik /etc/hosts na źródłowym serwerze z systemem Linux zawiera wpisy mapujące lokalną nazwę hosta na adres IP skojarzony ze wszystkimi kartami sieciowymi.
4. Zainstaluj najnowsze openssh, openssh serwera i biblioteki openssl pakietów na komputerze, który chcesz chronić.
5. Upewnij się, że SSH jest włączona i uruchomiona na port 22.
6. Włącz podsystem SFTP i uwierzytelnianie hasłem w pliku sshd_config w następujący sposób:

   * Zaloguj się jako element główny.
   * W pliku /etc/ssh/sshd_config Znajdź wiersz rozpoczynający się od PasswordAuthentication.
   * Usuń znaczniki komentarza i zmień wartość **no** na **yes**.
   * Znajdź wiersz zaczynający się od ciągu **Subsystem** i usuń znaczniki komentarza.

     ![Linux przesłonić domyślny nie podsystemów](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-the-mobility-service-manually"></a>Ręcznie zainstalować usługi mobilności
Pliki instalacyjne są dostępne w \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository C:\Program Files (x86).

| Źródłowy system operacyjny | Plik instalacyjny usługi mobilności |
| --- | --- |
| Windows Server (tylko wersja 64-bitowa) |Microsoft-ASR_UA_9*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6 (tylko wersja 64-bitowa) |Microsoft-ASR_UA_9*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3 (tylko wersja 64-bitowa) |Microsoft-ASR_UA_9*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5 (tylko wersja 64-bitowa) |Microsoft-ASR_UA_9*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-the-mobility-service-manually-on-a-windows-server"></a>Ręcznie zainstalować usługi mobilności w systemie Windows server
1. Pobierz i zainstaluj odpowiedni instalator.
2. W obszarze **Przed rozpoczęciem** wybierz pozycję **Usługa mobilności**.

    ![Instalacja usługi mobilności](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. W **szczegóły konfiguracji serwera**, podaj adres IP serwera zarządzania i hasło, który został wygenerowany podczas instalowania składników serwera zarządzania. Hasło można pobrać przez uruchomienie  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** na serwerze zarządzania.

    ![Usługa mobilności](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. W **zainstalować lokalizacji**, zachowaj domyślną lokalizację i kliknij przycisk **dalej** do rozpoczęcia instalacji.
5. W **postęp instalacji**, sprawdź instalację i uruchom ponownie komputer, jeśli zostanie wyświetlony monit.

Można także zainstalować, wpisując w wierszu polecenia następujący tekst:

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

W poprzednim poleceniu:

* / Roli: obowiązkowy. Określa, czy usługa mobilności powinna zostać zainstalowana.
* / InstallLocation: obowiązkowy. Określa, gdzie zainstalować usługę.
* / PassphraseFilePath: obowiązkowy. Określa hasło serwera konfiguracji.
* / LogFilePath: obowiązkowy. Określa lokalizację pliku dziennika instalacji.

#### <a name="uninstall-the-mobility-service-manually"></a>Ręczne odinstalowanie usługi mobilności
Usługa mobilności można odinstalować za pomocą **Odinstaluj lub zmień program** w Panelu sterowania lub przy użyciu wiersza polecenia.

To polecenie, aby odinstalować usługi mobilności przy użyciu wiersza polecenia:

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-the-ip-address-of-the-management-server"></a>Zmienianie adresu IP serwera zarządzania
Po uruchomieniu kreatora można zmienić adres IP serwera zarządzania w następujący sposób:

1. Otwórz hostconfig.exe pliku (znajdujący się na pulpicie).
2. Na **Global** Zmień adres IP serwera zarządzania.

   > [!NOTE]
   > Zmień tylko adres IP serwera zarządzania. Numer portu do komunikacji serwera zarządzania musi być 443, i **użycie protokołu HTTPS** należy włączyć po lewej. Nie należy zmieniać hasła.
   >
   >

    ![Adres IP serwera zarządzania](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-the-mobility-service-manually-on-a-linux-server"></a>Ręcznie zainstalować usługi mobilności na serwerze z systemem Linux
1. Skopiuj odpowiednie tar archiwum maszyny systemu Linux, który chcesz chronić. Zobacz tabelę w obszarze [ręcznie zainstalować usługi mobilności](#install-the-mobility-service-manually) ustalenie, który tar archiwum możesz należy używać.
2. Otwórz powłokę programu, a następnie wyodrębnij z archiwum zip tar na ścieżkę lokalną, uruchamiając:`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. Utwórz plik o nazwie passphrase.txt w katalogu lokalnym, do którego wyodrębniono zawartość archiwum tar. Aby to zrobić, skopiuj hasło z Recovery\private\connection.passphrase witryny Azure C:\ProgramData\Microsoft na serwerze zarządzania i zapisz go w passphrase.txt, uruchamiając  *`echo <passphrase> >passphrase.txt`*  w powłoce.
4. Zainstaluj usługę mobilności, wprowadzając następujące polecenie:*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. Określ wewnętrzny adres IP serwera zarządzania, a następnie upewnij się, że wybrano portu 443.

#### <a name="install-the-mobility-service-from-the-command-line"></a>Zainstaluj usługę mobilności z wiersza polecenia

Skopiuj hasło z \InMage Systems\private\connection C:\Program Files (x86) na serwerze zarządzania i zapisz go jako "passphrase.txt" na serwerze zarządzania. Następnie uruchom następujące polecenia. W naszym przykładzie adres IP serwera zarządzania jest 104.40.75.37 i portu HTTPS jest 443:

Aby zainstalować serwer produkcyjny:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

Aby zainstalować główny serwer docelowy:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>Krok 10: Włącz ochronę maszyny
Aby włączyć ochronę, należy dodać maszyn wirtualnych i serwerów fizycznych do grupy ochrony. Przed rozpoczęciem należy pamiętać, że jeśli chronisz maszyny wirtualne VMware:

* Maszyny wirtualne VMware odnalezieniu co 15 minut, a może potrwać ponad 15 minut były widoczne w portalu usługi Site Recovery po odnajdywania.
* Zmiany środowiska na maszynie wirtualnej (na przykład instalacji narzędzi VMware) również może potrwać ponad 15 minut do aktualizacji w usłudze Site Recovery.
* Można sprawdzić czas ostatniego odnalezionych w maszynach wirtualnych VMware w **ostatniego kontaktu w** dla hosta serwera/ESXi vCenter na pole **serwery konfiguracji** kartę.
* Po dodaniu oprogramowania vCenter Server lub hosta ESXi po utworzeniu grupy ochrony może potrwać ponad 15 minut do portalu usługi Azure Site Recovery odświeżyć i maszyn wirtualnych do umieszczenia w **Dodaj maszyny do grupy ochrony** okno dialogowe.
* Jeśli chcesz bezzwłocznie ją kontynuować i dodać maszyny do grupy ochrony bez oczekiwania na zaplanowanego odnajdywania, zaznacz serwer konfiguracji (nie klikaj pozycji go) i kliknij przycisk **Odśwież**.

Ponadto:

* Firma Microsoft zaleca projektowania grup ochrony, tak aby odzwierciedlały obciążeń. Na przykład dodać maszyny z systemem określonej aplikacji do tej samej grupy.
* Podczas dodawania komputerów do grupy ochrony, serwer przetwarzania wypychanie i automatycznie instaluje usługi mobilności, jeśli nie jest już zainstalowana. Musisz mieć mechanizm wypychania przygotowany zgodnie z opisem w poprzednim kroku.

### <a name="add-machines-to-a-protection-group"></a>Dodaj maszyny do grupy ochrony

1. Przejdź do **chronione elementy** > **grupy ochrony** > **maszyny** > **Dodaj maszyny**.
2. W przypadku ochrony maszyn wirtualnych VMware, **wybierz maszyny wirtualne**, wybierz serwer vCenter, który zarządza maszyn wirtualnych (lub hosta EXSi, na którym jest uruchomiony), a następnie wybierz maszyn.

    ![Włącz ochronę maszyny wirtualne](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. W przypadku ochrony serwerów fizycznych, **wybierz maszyny wirtualne**, otwórz **Dodawanie maszyn fizycznych** kreatora i Podaj przyjazną nazwę i adres IP. Następnie wybierz rodziny systemów operacyjnych.

   ![Włącz ochronę serwerów fizycznych](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. W **określić zasoby docelowe**, wybierz konto magazynu, którego używasz do replikacji i zdecyduj, czy ustawienia powinny być używane dla wszystkich obciążeń. Konta Premium magazynu nie są obecnie obsługiwane.

   > [!NOTE]
   > Nie obsługujemy Przenoszenie konta magazynu utworzone za pomocą [portalu Azure](../storage/storage-create-storage-account.md) między grupami zasobów.                           
   > [Migracja kont magazynu](../azure-resource-manager/resource-group-move-resources.md) w grupach zasobów w ramach tej samej subskrypcji lub w różnych subskrypcjach nie jest obsługiwana dla kont magazynu używanych do wdrażania usługi Site Recovery.
   >
   >

    ![Konfigurowanie ustawień obiektu docelowego](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. W **Określ konta**, wybierz konto, które [Konfigurowanie](#install-the-mobility-service-with-push-installation) do użycia na potrzeby automatycznej instalacji usługi mobilności.

    ![Określ konta](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. Kliknij znacznik wyboru, aby zakończyć dodawanie komputerów do grupy ochrony i Rozpocznij replikację początkową dla każdej maszyny.

   > [!NOTE]
   > Jeśli przygotowano instalacji wypychanej usługi mobilności automatycznie jest zainstalowany na komputerach, które nie mają go, ponieważ są one dodawane do grupy ochrony. Po zainstalowaniu usługi zadanie ochrony rozpoczyna się i kończy się niepowodzeniem. Po awarii należy ręcznie uruchomić ponownie każdej maszynie, który miał zainstalowaną usługę mobilności. Po uruchomieniu zadania ochrony rozpoczyna się od nowa i następuje Replikacja początkowa.
   >
   >

Możesz monitorować stan na **zadania** strony.

![Monitor stanu na stronie zadań](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

Można również monitorować stan ochrony w **chronione elementy** > *Nazwa grupy ochrony* > **maszyn wirtualnych**. Po zakończeniu replikacji początkowej i dane są synchronizowane, stan komputera zmieni się na **chronione**.

![Monitor stanu w chronione elementy](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>Krok 11: Zestaw właściwości maszyny chronionych.
1. Po uzyskaniu maszynę **chronione** stanu, można skonfigurować właściwości trybu failover. Informacje dotyczące grupy ochrony, wybierz komputer, a następnie otwórz **Konfiguruj** kartę.
2. Usługa Site Recovery sugeruje właściwości dla maszyny Wirtualnej platformy Azure i automatycznie wykrywa, że ustawienia sieci lokalnej.

    ![Ustaw właściwości maszyny wirtualnej](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. Możesz zmienić te ustawienia:

   * **Nazwa maszyny Wirtualnej platformy Azure**: jest to nazwa, które będzie mieć maszyny platformy Azure po pracy awaryjnej. Nazwa musi spełniać wymagania dotyczące usługi Azure.
   * **Rozmiar maszyny Wirtualnej Azure**: liczba kart sieciowych jest zależna od rozmiaru do docelowej maszyny wirtualnej. Aby uzyskać więcej informacji na temat rozmiarów i kart, zobacz [rozmiaru tabel](../virtual-machines/linux/sizes.md). Należy pamiętać, że:

     * Podczas modyfikowania rozmiaru maszyny wirtualnej i zapisać ustawienia, liczba kart sieciowych ulegnie zmianie po otwarciu **Konfiguruj** karcie następnym razem. Minimalna liczba kart sieciowych docelowych maszyn wirtualnych jest równa z minimalną liczbą kart sieciowych na źródłowej maszynie wirtualnej. Maksymalna liczba kart sieciowych zależy od rozmiaru maszyny wirtualnej.
       * Jeśli liczba kart sieciowych na maszynie źródłowej jest większa niż liczba kart sieciowych dozwolonych dla rozmiaru maszyny docelowej, element docelowy ma taką samą liczbę kart jako źródło.
       * Jeśli liczba kart sieciowych dla źródłowej maszyny wirtualnej przekracza dozwolony rozmiar docelowy numer, maksymalny rozmiar docelowy będą używane.
        Na przykład, jeśli maszyna źródłowa ma dwie karty sieciowe, a rozmiar maszyny docelowej obsługuje cztery karty, maszyna docelowa będzie mieć dwie karty sieciowe. Jeśli maszyna źródłowa ma dwie karty sieciowe, ale rozmiar docelowy obsługiwanych obsługuje tylko jeden, maszyna docelowa będzie mieć tylko jedną kartę.
     * Jeśli maszyna wirtualna ma wiele kart sieciowych, wszystkie karty powinny być połączone z tą samą siecią platformy Azure.
   * **Sieć platformy Azure**: należy określić sieć platformy Azure, maszyny wirtualne Azure zostaną podłączone do po pracy awaryjnej. Jeśli nie określono, maszynach wirtualnych platformy Azure nie będzie podłączona do żadnej sieci. Ponadto należy określić sieci platformy Azure, jeśli chcesz powrotu po awarii z platformy Azure do lokacji lokalnej. Powrót po awarii wymaga połączenia sieci VPN między sieci platformy Azure i siecią lokalną.
   * **Azure podsieć adresówIP/**: dla każdej karty sieciowej, wybierz podsieć, do której należy łączyć maszyny Wirtualnej platformy Azure. Należy pamiętać, że jeśli karta sieciowa komputera źródłowego jest skonfigurowany do korzystania ze statycznego adresu IP, można określić statyczny adres IP dla maszyny Wirtualnej platformy Azure. Jeśli nie podasz statycznego adresu IP, dowolny dostępny adres IP zostaną przydzielone. Jeśli jest określony docelowy adres IP, ale jest już używany przez inną maszynę Wirtualną na platformie Azure, trybu failover zakończy się niepowodzeniem. Jeśli karta sieciowa komputera źródłowego jest skonfigurowany do korzystania z protokołu DHCP, będziesz mieć DHCP jako ustawienie dla platformy Azure.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>Krok 12: Utwórz plan odzyskiwania i tryb failover
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

Można uruchomić trybu failover dla pojedynczego komputera, lub możesz w trybie Failover wiele maszyn wirtualnych służących do wykonywania tego samego zadania lub uruchomienie tego samego obciążenia. Aby przenosić wiele maszyn jednocześnie, należy je dodać do planu odzyskiwania.

Aby utworzyć plan odzyskiwania:

1. Na **plany odzyskiwania** kliknij przycisk **dodać planu odzyskiwania** i Dodaj planu odzyskiwania. Określ szczegóły planowania i wybierz **Azure** jako element docelowy.

 ![Konfigurowanie planu odzyskiwania](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. W **Wybieranie maszyny wirtualnej**, wybierz grupę ochrony, a następnie wybierz maszyn w grupie można dodać do planu odzyskiwania.

 ![Dodaj maszyny wirtualne](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

Można dostosować planu do tworzenia grup i sekwencji kolejności, w którym maszyny w planie odzyskiwania są nie w trybie Failover. Można również dodać skryptów i wyświetla monit o ręczne akcje. Skrypty można tworzyć ręcznie lub za pomocą [elementów Runbook automatyzacji Azure](site-recovery-runbook-automation.md). Aby uzyskać więcej informacji na temat dostosowywania plany odzyskiwania, zobacz [Tworzenie planów odzyskiwania](site-recovery-create-recovery-plans.md).

## <a name="run-a-failover"></a>Tryb failover
Przed uruchomieniem trybu failover:

* Upewnij się, że serwer zarządzania jest uruchomiona i dostępna. Jeśli nie, trybu failover zakończy się niepowodzeniem.
* Jeśli uruchomisz nieplanowany tryb failover:

  * Jeśli jest to możliwe, przed uruchomieniem nieplanowanego trybu failover należy wyłączyć maszyny główne. Dzięki temu maszyny źródłowe i replikowane nie będą uruchomione w tym samym czasie. Jeśli replikujesz maszyny wirtualne VMware, po uruchomieniu nieplanowanego trybu failover, można określić usługi Site Recovery należy spróbować zamknąć maszyny źródłowej. W zależności od stanu lokacji głównej może być lub może nie działać. Site Recovery nie oferuje tej opcji, Jeśli replikujesz serwerów fizycznych.
  * Nieplanowany tryb failover zatrzymuje replikacji danych z maszyn głównych, aby żaden przyrost danych nie będzie transferowany po rozpoczęciu nieplanowanego trybu failover.
  * Jeśli chcesz nawiązać połączenia z maszyny wirtualnej repliki na platformie Azure po w tryb failover, należy włączyć Podłączanie pulpitu zdalnego na maszynie źródłowej przed uruchomieniem trybu failover. Następnie Zezwalaj na połączenie RDP przez zaporę. Należy również umożliwić RDP na publiczny punkt końcowy maszyny wirtualnej platformy Azure po pracy awaryjnej. Postępuj zgodnie z [najlepsze rozwiązania](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) aby upewnić się, że RDP działa po przejściu w tryb failover.

> [!NOTE]
> Aby uzyskać najlepszą wydajność podczas pracy w trybie failover na platformie Azure, upewnij się, że na chronionej maszynie zainstalowano agenta platformy Azure. To pomaga rozruchu maszyny szybciej oraz diagnozowanie problemów. Azure Agent jest dostępna dla [Linux](https://github.com/Azure/WALinuxAgent) i [Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover
Uruchom test trybu failover, aby symulować Twojej pracy awaryjnej i procesów odzyskiwania w sieci izolowanej nie ma wpływu na środowisko produkcyjne, który umożliwia zwykłej replikacji nadal normalnego. Testowy tryb failover jest initiatd w źródle i uruchomić ją na kilka sposobów:

* **Określ sieć platformy Azure, nie**: po uruchomieniu testu w trybie failover bez sieci test sprawdza, czy maszyny wirtualne start i są wyświetlane poprawnie w systemie Azure. Maszyny wirtualne nie będzie podłączona do sieci platformy Azure po pracy awaryjnej.
* **Określ sieć platformy Azure**: tego typu Failover sprawdza, czy całe środowisko replikacji funkcjonuje zgodnie z oczekiwaniami oraz że maszyn wirtualnych platformy Azure są podłączone do określonej sieci.

Aby uruchomić test trybu failover:

1. Na **plany odzyskiwania** , wybierz plan i kliknij przycisk **testowy tryb Failover**.

 ![Wybierz plan](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. W **potwierdzić testowego trybu Failover**, wybierz pozycję **Brak** aby wskazać, że nie chcesz używać sieci platformy Azure do testowania trybu failover, lub wybierz sieć, do którego zostanie podłączona testu maszyn wirtualnych po pracy awaryjnej. Kliknij znacznik wyboru, aby uruchomić tryb failover.

 ![Wybierz odpowiednią opcję](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. Monitorować postęp trybu failover na **zadania** kartę.

 ![Monitoruj postęp](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Po zakończeniu pracy awaryjnej, należy także widoczna replika Azure maszyny są wyświetlane w **maszyn wirtualnych** w portalu Azure. Jeśli chcesz zainicjować połączenie RDP z maszyny Wirtualnej Azure, konieczne będzie otwarcie portu 3389 na punkt końcowy maszyny Wirtualnej.
5. Po wprowadzeniu zakończone, gdy tryb failover osiągnie **Complete** przeprowadzanie testów, kliknij przycisk **ukończenia testowej** aby zakończyć. W **uwagi**, zarejestrować i zapisać wszelkie obserwacje związane z testowania trybu failover.
6. Kliknij przycisk **przejścia w tryb failover testu** automatycznie czyszczenie środowiska testowego. Po zakończeniu testowania trybu failover zostaną wyświetlone **Complete** stanu. Wszystkie elementy lub maszyny wirtualne utworzone automatycznie podczas testowania trybu failover są usuwane. Jeśli testowy tryb failover trwa dłużej niż dwa tygodnie, wymusił zakończenie.

### <a name="run-an-unplanned-failover"></a>Uruchom nieplanowanego trybu failover
Nieplanowany tryb failover jest inicjowane z platformy Azure i można wykonać, nawet jeśli lokacja podstawowa jest niedostępna.

1. Na **plany odzyskiwania** , wybierz plan i kliknij przycisk **pracy awaryjnej** > **nieplanowany tryb Failover**.

 ![Wybierz plan](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. Jeśli replikujesz maszyny wirtualne VMware, możesz spróbować zamknąć lokalnych maszyn wirtualnych. Jest to akcja optymalnych i tryb failover trwa czy nakład pracy zakończy się powodzeniem, czy nie. Jeśli to się nie powiedzie, szczegóły błędu pojawią się na **zadania** w obszarze **nieplanowanego trybu Failover zadania**.

 ![Opcja wyłączania lokalnych maszyn wirtualnych](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > Ta opcja jest niedostępna, Jeśli replikujesz serwerów fizycznych. Musisz spróbuj zamknąć te ręcznie, jeśli to możliwe.
 >
 >

3. W **potwierdzić trybu Failover**, sprawdź kierunek pracy awaryjnej (na platformie Azure) i wybierz punkt odzyskiwania, który ma być używany do pracy awaryjnej. Jeśli podczas konfigurowania właściwości replikacji włączono wielu maszyn wirtualnych, można odzyskać do ostatniego punktu odzyskiwania aplikacji lub spójna w razie awarii. Możesz też wybrać **punkt odzyskiwania niestandardowe** odzyskiwanie do wcześniejszego punktu w czasie. Kliknij znacznik wyboru, aby uruchomić tryb failover.

 ![Potwierdź kierunek trybu failover](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. Poczekaj na zakończenie zadania nieplanowanego trybu failover. Możesz monitorować postęp trybu failover na **zadania** kartę. Nawet jeśli występują błędy podczas nieplanowanego trybu failover, planu odzyskiwania uruchamia do czasu ukończenia. Należy także widoczna replika Azure maszyny są wyświetlane w **maszyn wirtualnych** w portalu Azure.

### <a name="connect-to-replicated-azure-virtual-machines-after-failover"></a>Połącz replikowane maszyny wirtualne platformy Azure po trybu failover
Aby połączyć się replikowane maszyny wirtualne na platformie Azure po pracy awaryjnej, potrzebne są:

- Podłączanie pulpitu zdalnego, włączone na komputerze podstawowym.
- Zapora systemu Windows na podstawowej maszynie ustawioną Zezwalaj na RDP.
- RDP dodane do publicznego punktu końcowego maszyny wirtualnej platformy Azure.

Aby uzyskać więcej informacji na temat konfigurowania, zobacz [Rozwiązywanie problemów z połączeń usług pulpitu zdalnego po trybu failover przy użyciu usługi ASR](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

## <a name="deploy-additional-process-servers"></a>Wdrażanie serwerów dodatkowych procesów
Jeśli użytkownik musi skalowania wdrożenia ponad 200 maszyn źródłowych lub całkowita szybkość zmian codzienne przekracza 2 TB, należy procesu dodatkowych serwerów do obsługi natężenia ruchu. Aby skonfigurować serwer dodatkowych procesów, sprawdź wymagania [serwery dodatkowych procesów](#additional-process-servers), a następnie ponowne skonfigurowanie serwera przetwarzania, zgodnie z instrukcjami w poniższej. Po skonfigurowaniu serwera można skonfigurować maszyn źródłowych z niego korzystać.

### <a name="set-up-an-additional-process-server"></a>Konfigurowanie serwera dodatkowych procesów
Konfigurowanie serwera dodatkowych procesów w następujący sposób:

* Uruchom Kreatora jednolity sposób konfigurowania serwera zarządzania jako serwera przetwarzania.
* Do zarządzania replikacją danych przy użyciu tylko nowego serwera przetwarzania, należy dokonać migracji z chronionych maszyn.

### <a name="install-the-process-server"></a>Zainstaluj serwer przetwarzania
1. Na **Szybki Start** pozycję Pobierz plik instalacyjny ujednoliconego instalacji składników usługi Site Recovery. Uruchom Instalatora.
2. W obszarze **Przed rozpoczęciem** wybierz pozycję **Dodaj dodatkowe serwery przetwarzania w celu zwiększenia skali wdrożenia**.

 ![Dodawanie serwera przetwarzania](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. Ukończ pracę kreatora, jak w przypadku należy [Konfigurowanie](#step-5-install-the-management-server) pierwszego serwera zarządzania.
4. W **szczegóły konfiguracji serwera**, wprowadź adres IP z oryginalnego serwera zarządzania, na którym zainstalowano serwer konfiguracji, a następnie wprowadź hasło. Jeśli nie masz hasła, uruchom  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** na oryginalnym serwerze zarządzania, można go pobrać.

 ![Szczegóły konfiguracji serwera](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-to-use-the-new-process-server"></a>Migruj maszyny, aby użyć nowego serwera przetwarzania
1. Otwórz **serwery konfiguracji** > **serwera** > *nazwa oryginalnego serwera zarządzania* > **serwera Szczegóły**.

 ![Szczegóły serwera](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. W **serwerów procesu** listy, wybierz **Zmień serwer przetwarzania** obok serwera, który chcesz zmienić.

 ![Zaktualizuj serwer przetwarzania](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. Wybierz **Zmień serwer przetwarzania**, wybierz pozycję **docelowy serwer przetwarzania**, a następnie wybierz nowy serwer zarządzania. Następnie wybierz maszyny wirtualne, które będą obsługiwać nowego serwera przetwarzania. Kliknij ikonę informacji, aby uzyskać informacje o serwerze. Średnie miejsce potrzebne do replikacji każdej wybranej maszyny wirtualnej do nowego serwera przetwarzania zostanie wyświetlony podejmowanie decyzji dotyczących obciążenia. Kliknij znacznik wyboru, aby rozpocząć replikację do nowego serwera przetwarzania.

 ![Zmień serwer przetwarzania](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>Uprawnienia programu VMware vCenter dostępu
Serwer przetwarzania może automatycznie odnajdować maszyn wirtualnych na serwerze vCenter. Aby przeprowadzić odnajdywanie automatyczne, należy zdefiniować rolę (Azure_Site_Recovery) na poziomie vCenter, aby umożliwić odzyskiwania lokacji w celu uzyskania dostępu do serwera vCenter. Jeśli potrzebujesz do migrowania maszyn VMware do platformy Azure i nie należy do powrotu po awarii z platformy Azure, można określić tylko do odczytu roli, do której jest wystarczająca. Ustawić uprawnienia, zgodnie z opisem w [krok 6: Skonfiguruj poświadczenia dla serwera vCenter](#step-6-set-up-credentials-for-the-vcenter-server). W poniższej tabeli przedstawiono podsumowanie uprawnienia roli:

| **Rola** | **Szczegóły** | **Uprawnienia** |
| --- | --- | --- |
| Azure_Site_Recovery roli |Maszyna wirtualna oprogramowania VMware odnajdywania |Przypisz odpowiednie uprawnienia na serwerze v Centrum:<br/><br/>Magazyn danych: Przydzielić miejsca, Magazyn danych przeglądania, operacje na plikach niskiego poziomu, usuń plik, pliki maszyny wirtualnej aktualizacji<br/><br/>Sieci: Przypisywanie sieci<br/><br/>Zasób: Przypisywanie maszyny wirtualnej do puli zasobów, migracji wyłączenia zasilania maszyny wirtualnej, migracji wyłączyć na maszynie wirtualnej<br/><br/>Zadania: Utwórz zadanie, zadania aktualizacji<br/><br/>Maszyny wirtualnej > konfiguracji<br/><br/>Maszyny wirtualnej > interakcja > odpowiedzi na pytanie, połączenie z urządzeniem, skonfiguruj dysków CD, konfigurowanie dyskietka, wyłącz zasilanie, zainstaluj narzędzia VMware<br/><br/>Maszyny wirtualnej > spisu > Tworzenie, rejestrowanie, wyrejestrowywanie<br/><br/>Maszyny wirtualnej > inicjowania obsługi administracyjnej > Zezwalaj na pobieranie maszyny wirtualnej, przekazywanie plików maszyny wirtualnej Zezwalaj<br/><br/>Maszyny wirtualnej > migawki > Usuń migawki |
| Rola użytkownika vCenter |Maszyna wirtualna oprogramowania VMware odnajdywania i pracy awaryjnej bez zamknięcia źródłowej maszyny Wirtualnej |Przypisz odpowiednie uprawnienia na serwerze v Centrum:<br/><br/>Obiekt centrum danych > Propagowanie do obiektu podrzędnego roli = tylko do odczytu <br/><br/>Użytkownik jest przypisany na poziomie centrum danych i w związku z tym ma dostęp do wszystkich obiektów w centrum danych. Jeśli chcesz ograniczyć dostęp, Przypisz **dostępu** roli z **propagowany do podrzędnego** obiektu do obiektów podrzędnych (hosty ESX, datastores maszyn wirtualnych i sieci). |
| Rola użytkownika vCenter |Praca w trybie failover i powrót po awarii |Przypisz odpowiednie uprawnienia na serwerze v Centrum:<br/><br/>Obiekt Datacenter — propagowany do obiektu podrzędnego roli = Azure_Site_Recovery<br/><br/>Użytkownik jest przypisany na poziomie centrum danych i w związku z tym ma dostęp do wszystkich obiektów w centrum danych.  Jeśli chcesz ograniczyć dostęp, przypisz ** dostępu ** roli z **propagowany do obiektu podrzędnego** do obiektu podrzędnego (hosty ESX, datastores maszyn wirtualnych i sieci). |

## <a name="third-party-software-notices-and-information"></a>Uwagi oprogramowania innych firm i informacji
<!--Do Not Translate or Localize-->

Oprogramowania i oprogramowania układowego w Microsoft produktu lub usługi jest oparta na lub zawiera materiały z projektów wymienionych poniżej (zbiorczo "Kod innych firm").  Firma Microsoft dokłada nie twórca kodu innych firm.  Oryginalne informacje o prawach autorskich i licencji, w którym firma Microsoft otrzymała taki kod innych firm są ustawiane przedstawionym poniżej.

Informacje przedstawione w sekcji A dotyczy składniki kodu innych firm z projekty wymienione poniżej. Te licencje i informacje znajdują się tylko do celów informacyjnych.  Ten kod innych firm jest trwa relicensed dla Ciebie przez firmę Microsoft zgodnie z warunkami licencjonowania oprogramowania firmy Microsoft dla produktów firmy Microsoft lub usługi.  

Informacje przedstawione w sekcji B dotyczy składników kodu innych firm, które są udostępniane użytkownikowi przez firmę Microsoft w obszarze oryginalnego postanowień licencyjnych.

Pełny plik można znaleźć na [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Firma Microsoft zastrzega sobie wszelkie prawa niewymienione w tym dokumencie, przez domniemanie, drodze estoppelu lub w inny sposób.

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o powrotu po awarii](site-recovery-failback-azure-to-vmware-classic.md) przełączyć maszyny przełączona w tryb failover działające na platformie Azure z powrotem do środowiska lokalnego.
