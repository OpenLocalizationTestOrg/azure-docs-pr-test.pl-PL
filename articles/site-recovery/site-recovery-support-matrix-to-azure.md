---
title: "Macierz obsługi usługi Site Recovery aaaAzure replikowania tooAzure | Dokumentacja firmy Microsoft"
description: "Podsumowanie hello obsługiwane systemy operacyjne oraz składniki usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajanaki
ms.openlocfilehash: eae1db2ff1392d272f6b2eb0e3410da19d09da7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-on-premises-tooazure"></a>Azure Site Recovery macierz obsługi replikacji z lokalnych tooAzure


W tym artykule przedstawiono obsługiwane konfiguracje oraz składniki usługi Azure Site Recovery podczas replikacji i odzyskiwanie tooAzure. Aby uzyskać więcej informacji o wymaganiach usługi Azure Site Recovery, zobacz hello [wymagania wstępne](site-recovery-prereq.md).


## <a name="support-for-deployment-options"></a>Obsługa opcje wdrażania

**Wdrożenie** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (z/bez programu Virtual Machine Manager)** |
--- | --- | ---
**Witryna Azure Portal** | Lokalny magazyn tooAzure maszyn wirtualnych VMware, z usługi Azure Resource Manager lub klasycznego magazynu i sieci.<br/><br/> TooResource trybu failover Manager lub klasycznych maszyn wirtualnych. | Lokalny magazyn tooAzure maszyn wirtualnych funkcji Hyper-V, z Menedżerem zasobów lub klasycznego magazynu i sieci.<br/><br/> TooResource trybu failover Manager lub klasycznych maszyn wirtualnych.
**Portal klasyczny** | Tylko tryb konserwacji. Nie można utworzyć nowego magazynu. | Tylko tryb konserwacji.
**PowerShell** | Nie są obecnie obsługiwane. | Obsługiwane


## <a name="support-for-datacenter-management-servers"></a>Obsługa serwerów zarządzania Centrum danych

### <a name="virtualization-management-entities"></a>Jednostki zarządzania wirtualizacji

**Wdrożenie** | **Pomoc techniczna**
--- | ---
**Maszyna wirtualna oprogramowania VMware/fizyczne serwera** | vCenter 6.5, 6.0 lub 5.5
**Funkcja Hyper-V (z programu Virtual Machine Manager)** | Program System Center Virtual Machine Manager 2016 i System Center Virtual Machine Manager 2012 R2

  >[!Note]
  > W chmurze programu System Center Virtual Machine Manager 2016 z systemem Windows Server 2016 i 2012 R2 hostów nie jest obecnie obsługiwany.

### <a name="host-servers"></a>Serwery hosta

**Wdrożenie** | **Pomoc techniczna**
--- | ---
**Maszyna wirtualna oprogramowania VMware/fizyczne serwera** | vSphere 6.5, 6.0, 5.5
**Funkcja Hyper-V (z/bez programu Virtual Machine Manager)** | Windows Server 2016, Windows Server 2012 R2 z najnowszymi aktualizacjami.<br></br>Jeśli używany jest program SCVMM, hosty z systemem Windows Server 2016 zarządzane w programie SCVMM 2016.


  >[!Note]
  >Lokacji funkcji Hyper-V, która łączy hostach z systemem Windows Server 2016 i 2012 R2 nie jest obecnie obsługiwany. Tooan alternatywnej lokalizacji odzyskiwania dla maszyn wirtualnych na hoście systemu Windows Server 2016 nie jest obecnie obsługiwany.

## <a name="support-for-replicated-machine-os-versions"></a>Obsługa wersji systemu operacyjnego zreplikowanej maszyny

Maszyny wirtualne, które są chronione muszą spełniać [wymagania dotyczące usługi Azure](#failed-over-azure-vm-requirements) podczas replikowania tooAzure.
Witaj w poniższej tabeli podsumowano obsługi systemu operacyjnego replikowanych w różnych scenariuszy wdrażania podczas korzystania z usługi Azure Site Recovery. Ta obsługa dotyczy na dowolne obciążenia uruchomione na powitania określonych systemu operacyjnego.

 **Serwer VMware/fizyczne** | **Funkcja Hyper-V (lub bez VMM)** |
--- | --- |
64-bitowego systemu Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 z na co najmniej z dodatkiem SP1<br/>*Windows Server 2016* — obecnie na maszynach wirtualnych VMware i serwery fizyczne nie jest obsługiwany. <br/><br/> Red Hat Enterprise Linux: 5.2 too5.11, 6.1 too6.8, 7.0 too7.3 <br/><br/>Centów systemu operacyjnego: 5.2 too5.11, 6.1 too6.8, 7.0 too7.3 <br/><br/>Ubuntu 14.04 LTS serwera[ (obsługiwane wersje jądra)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Ubuntu 16.04 LTS server[ (obsługiwane wersje jądra)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Oracle Linux przedsiębiorstwa 6.4, 6.5 systemem jądra zgodne Red Hat hello lub podzielenie Enterprise jądra wersji 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 z dodatkiem SP3 <br/><br/> SUSE Linux Enterprise Server 11 z dodatkiem SP4 <br/>(Uaktualnienie replikowanie maszyn z SLES 11 z dodatkiem SP3 tooSLES 11 z dodatkiem SP4 nie jest obsługiwane. Jeśli zreplikowanej maszyny został uaktualniony z tooSLES 11SP3 SLES 11 z dodatkiem SP4, zostanie muszą toodisable replikacji oraz zapewnić ochronę maszyny hello ponownie po uaktualnieniu hello.) | Wszelkie system operacyjny gościa [obsługiwany przez platformę Azure](https://technet.microsoft.com/library/cc794868.aspx)


>[!IMPORTANT]
>(Dotyczy tooVMware/serwery fizyczne replikowane tooAzure)
>
> Red Hat Enterprise Linux Server 7 + i CentOS 7 + serwery 3.10.0-514 wersji jądra jest obsługiwana, począwszy od wersji 9,8 hello usługi mobilności odzyskiwania lokacji Azure.<br/><br/>
> Klienci na powitania 3.10.0-514 jądra przy użyciu wersji usługi mobilności jest niższa niż wersja 9,8 hello są wymagane toodisable replikacji, wersja hello aktualizacji tooversion usługi mobilności hello 9,8, a następnie ponownie włączyć replikację.


### <a name="supported-ubuntu-kernel-versions-for-vmwarephysical-servers"></a>Ubuntu wersji jądra programu VMware/serwery fizyczne

**Zlecenia** | **Wersja usługi mobilności** | **Wersja jądra** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0 117 — ogólne,<br/>3.16.0-25-Generic too3.16.0-77-ogólny<br/>3.19.0-18-Generic too3.19.0 80-ogólne,<br/>4.2.0-18-Generic too4.2.0 42 — ogólne,<br/>4.4.0-21-Generic too4.4.0 75 — ogólne |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0 121 — ogólne,<br/>3.16.0-25-Generic too3.16.0-77-ogólny<br/>3.19.0-18-Generic too3.19.0 80-ogólne,<br/>4.2.0-18-Generic too4.2.0 42 — ogólne,<br/>4.4.0-21-Generic too4.4.0 81 — ogólne |
16.04 LTS | 9.10 | 4.4.0-21-Generic too4.4.0 81 — ogólne,<br/>4.8.0-34-Generic too4.8.0 56-ogólne,<br/>4.10.0-14-Generic too4.10.0 24 — ogólne |


## <a name="supported-file-systems-and-guest-storage-configurations-on-linux-vmwarephysical-servers"></a>Systemy plików obsługiwanych i konfiguracje magazynu gościa w systemie Linux (VMware/serwery fizyczne)

następujące Hello plików systemów i magazynu konfiguracji oprogramowania jest obsługiwana na serwerach Linux działających na serwerach programu VMware lub fizycznych:
* Systemy plików: ext3 ext4, ReiserFS (Suse Linux Enterprise Server tylko), XFS
* Menedżer woluminów: LVM2
* Oprogramowanie wielościeżkowego: mapowania urządzenia

Parawirtualnego systemu magazynu (urządzenia wyeksportowane przez sterowniki parawirtualnego systemu) nie są obsługiwane.<br/>
Urządzenia We/Wy bloku wielu kolejki nie są obsługiwane.<br/>
Serwery fizyczne z kontrolera magazynu HP CCISS hello nie są obsługiwane.<br/>

>[!Note]
> Na następujących katalogów hello serwerów Linux (jeśli skonfigurowany jako osobne partycje /-systemów plików) wszystkie muszą być na powitania samego dysku (dysk systemu operacyjnego hello) na serwerze źródłowym hello: / (root), / Boot usr, /usr/local, /var, etc<br/><br/>
> Funkcje XFSv5 na XFS systemy plików, takich jak metadanych sumy kontrolnej są obsługiwane począwszy od wersji 9.10 hello usługi mobilności. Jeśli używasz funkcji XFSv5, upewnij się, że używasz wersji usługi mobilności 9.10 lub nowszej. Można użyć hello xfs_info narzędzie toocheck hello XFS superblock hello partycji. Jeśli ftype ustawiono too1, następnie XFSv5 funkcje są używane.
>


## <a name="support-for-network-configuration"></a>Obsługa konfiguracji sieci
następujące tabele Hello podsumowanie Obsługa konfiguracji sieci w różnych scenariuszy wdrażania, które używają usługi Azure Site Recovery tooreplicate tooAzure.

### <a name="host-network-configuration"></a>Konfiguracja sieci hosta

**Konfiguracja** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (z/bez programu Virtual Machine Manager)**
--- | --- | ---
Tworzenie zespołu kart sieciowych | Tak<br/><br/>Nieobsługiwane, gdy są replikowane maszyny fizycznej| Tak
SIECI VLAN | Tak | Tak
IPv4 | Tak | Tak
Protokół IPv6 | Nie | Nie

### <a name="guest-vm-network-configuration"></a>Konfiguracja sieci maszyny Wirtualnej gościa

**Konfiguracja** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (z/bez programu Virtual Machine Manager)**
--- | --- | ---
Tworzenie zespołu kart sieciowych | Nie | Nie
IPv4 | Tak | Tak
Protokół IPv6 | Nie | Nie
Statyczny adres IP (z systemem Windows) | Tak | Tak
Statyczny adres IP (Linux) | Tak <br/><br/>Maszyny wirtualne jest skonfigurowany toouse DHCP w przypadku powrotu po awarii  | Nie
Obsługa wielu kart Sieciowych | Tak | Tak

### <a name="failed-over-azure-vm-network-configuration"></a>Konfiguracja sieci maszyny Wirtualnej Azure przełączona w tryb failover

**Sieć platformy Azure** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (z/bez programu Virtual Machine Manager)**
--- | --- | ---
ExpressRoute | Tak | Tak
ILB | Tak | Tak
ELB | Tak | Tak
Traffic Manager | Tak | Tak
Obsługa wielu kart Sieciowych | Tak | Tak
Zastrzeżony adres IP | Tak | Tak
IPv4 | Tak | Tak
Zachowaj źródłowy adres IP | Tak | Tak


## <a name="support-for-storage"></a>Obsługa magazynu
następujące tabele Hello podsumowanie Obsługa konfiguracji magazynu w różnych scenariuszy wdrażania, które używają usługi Azure Site Recovery tooreplicate tooAzure.

### <a name="host-storage-configuration"></a>Konfiguracja magazynu hosta

**Konfiguracja** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (z/bez programu Virtual Machine Manager)**
--- | --- | --- | ---
SYSTEMU PLIKÓW NFS | Tak, aby VMware<br/><br/> Nie dla serwerów fizycznych | Nie dotyczy
SMB 3.0 | Nie dotyczy | Tak
SIECI SAN (ISCSI) | Tak | Tak
Wiele ścieżek (MPIO)<br></br>Przetestowana: moduł DSM firmy Microsoft, EMC PowerPath 5.7 z dodatkiem SP4, EMC PowerPath DSM dla CLARiiON | Tak | Tak

### <a name="guest-or-physical-server-storage-configuration"></a>Gość lub serwerze fizycznym magazynu konfiguracji

**Konfiguracja** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (z/bez programu Virtual Machine Manager)**
--- | --- | ---
VMDK | Tak | Nie dotyczy
DYSK VHD/VHDX | Nie dotyczy | Tak
Gł 2 maszyny Wirtualnej | Nie dotyczy | Tak
INTERFEJSEM EFI/UEFI| Nie | Tak
Udostępniony dysk klastra | Nie | Nie
Zaszyfrowanego dysku | Nie | Nie
SYSTEMU PLIKÓW NFS | Nie | Nie dotyczy
SMB 3.0 | Nie | Nie
DYSK RDM | Tak<br/><br/> Brak serwerów fizycznych | Nie dotyczy
Na dysku > 1 TB | Tak<br/><br/>Maksymalnie 4095 GB | Tak<br/><br/>Maksymalnie 4095 GB
Dysk o rozmiarze sektora 4K | Tak | Tak, obsługiwane w maszynach wirtualnych generacji 1<br/><br/>Nie są obsługiwane w maszynach wirtualnych generacji 2.
Wolumin dysku rozłożone > 1 TB<br/><br/> Zarządzanie woluminami LVM logiczne | Tak | Tak
Funkcja miejsca do magazynowania | Nie | Tak
Dodaj lub usuń gorących dysku | Nie | Nie
Wykluczanie dysku | Tak | Tak
Wiele ścieżek (MPIO) | Nie dotyczy | Tak

**Magazyn platformy Azure** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (z/bez programu Virtual Machine Manager)**
--- | --- | ---
LRS | Tak | Tak
GRS | Tak | Tak
RA-GRS | Tak | Tak
Magazynu chłodnego | Nie | Nie
Magazynu gorącego| Nie | Nie
Szyfrowanie rest(SSE)| Tak | Tak
Premium Storage | Tak | Tak
Import/Eksport usługi | Nie | Nie


## <a name="support-for-azure-compute-configuration"></a>Obsługa konfiguracji obliczeń platformy Azure

**Obliczanie funkcji** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (z/bez programu Virtual Machine Manager)**
--- | --- | --- 
Zestawy dostępności | Tak | Tak
CENTRUM | Tak | Tak  
Dyski zarządzane | Tak | Tak<br/><br/>Powrót po awarii tooon lokalnego z maszyny Wirtualnej platformy Azure z dyskami zarządzanego nie jest obecnie obsługiwane.

## <a name="failed-over-azure-vm-requirements"></a>Wymagania dotyczące maszyny Wirtualnej Azure przełączona w tryb failover

Można wdrożyć maszyny wirtualne tooreplicate odzyskiwania lokacji i serwery fizyczne z dowolnego systemu operacyjnego, obsługiwany przez platformę Azure. Jest to większość wersji systemów Windows i Linux. Lokalnych maszyn wirtualnych, które mają być tooreplicate musi spełniać następujące wymagania dotyczące usługi Azure podczas replikowania tooAzure hello.

**Jednostki** | **Wymagania** | **Szczegóły**
--- | --- | ---
**System operacyjny gościa** | Replikacji funkcji Hyper-V tooAzure: Usługa Site Recovery obsługuje wszystkich systemów operacyjnych, które są [obsługiwany przez platformę Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx). <br/><br/> VMware i replikacji na serwerze fizycznym: Sprawdź hello systemu Windows i Linux [wymagania wstępne](site-recovery-vmware-to-azure-classic.md) | Sprawdzanie wymagań wstępnych zakończy się niepowodzeniem, jeśli jest nieobsługiwany.
**Architektura systemu operacyjnego gościa** | 64-bitowych | Sprawdzanie wymagań wstępnych zakończy się niepowodzeniem, jeśli nieobsługiwane
**Rozmiar dysku systemu operacyjnego** | Konfigurowanie too2048 GB w przypadku replikowania **maszyn wirtualnych VMware lub serwerów fizycznych tooAzure**.<br/><br/>Maksymalnie 2048 GB dla **funkcji Hyper-V generacji 1** maszyn wirtualnych.<br/><br/>Maksymalnie 300 GB dla **maszyn wirtualnych funkcji Hyper-V generacji 2**.  | Sprawdzanie wymagań wstępnych zakończy się niepowodzeniem, jeśli nieobsługiwane
**Liczba dysków systemu operacyjnego** | 1 | Sprawdzanie wymagań wstępnych zakończy się niepowodzeniem, jeśli jest nieobsługiwany.
**Liczba dysków danych** | Replikowanie 64 lub mniej, jeśli **tooAzure maszyn wirtualnych VMware**; 16 lub mniej przypadku replikowania **tooAzure maszyn wirtualnych funkcji Hyper-V** | Sprawdzanie wymagań wstępnych zakończy się niepowodzeniem, jeśli nieobsługiwane
**Rozmiar wirtualnego dysku twardego dysku danych** | Zapasowej too4095 GB | Sprawdzanie wymagań wstępnych zakończy się niepowodzeniem, jeśli nieobsługiwane
**Karty sieciowe** | Wiele kart sieciowych są obsługiwane. |
**Udostępniony wirtualny dysk twardy** | Nieobsługiwane | Sprawdzanie wymagań wstępnych zakończy się niepowodzeniem, jeśli nieobsługiwane
**FC dysku** | Nieobsługiwane | Sprawdzanie wymagań wstępnych zakończy się niepowodzeniem, jeśli nieobsługiwane
**Format dysku twardego** | WIRTUALNEGO DYSKU TWARDEGO <br/><br/> VHDX | Mimo że VHDX nie jest obecnie obsługiwany na platformie Azure, Usługa Site Recovery automatycznie konwertuje VHDX tooVHD podczas przejścia w tryb failover tooAzure. Jeśli nie zostanie ponownie tooon lokalne powitania maszyny wirtualne nadal formatu VHDX hello toouse.
**Funkcja BitLocker** | Nieobsługiwane | Przed rozpoczęciem ochrony maszyny wirtualnej, należy wyłączyć funkcję BitLocker.
**Nazwa maszyny Wirtualnej** | Od 1 do 63 znaków. Ograniczone tooletters, cyfry i łączniki. Nazwa maszyny Wirtualnej Hello musi zaczynać i kończyć literą lub cyfrą. | Zaktualizuj wartość hello w hello właściwości maszyny wirtualnej w usłudze Site Recovery.
**Typu maszyny Wirtualnej** | Generacja 1<br/><br/> Generacja 2 — systemu Windows | Maszyny wirtualne generacji 2 z typem dysku systemu operacyjnego, Basic (zawierającej co najmniej dwa woluminy danych w formacie VHDX) i mniejsza niż 300 GB miejsca na dysku są obsługiwane.<br></br>Maszyn wirtualnych systemu Linux generacji 2 nie są obsługiwane. [Dowiedz się więcej](https://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)|

## <a name="support-for-recovery-services-vault-actions"></a>Wspieranie działań magazyn usług odzyskiwania

**Akcja** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (nie programu Virtual Machine Manager)** | **Funkcja Hyper-V (z programu Virtual Machine Manager)**
--- | --- | --- | ---
Przenieś magazyn między grupami zasobów<br/><br/> W obrębie subskrypcji oraz | Nie | Nie | Nie
Przenieść magazyn, sieć, maszyn wirtualnych platformy Azure w grupach zasobów<br/><br/> W obrębie subskrypcji oraz | Nie | Nie | Nie


## <a name="support-for-provider-and-agent"></a>Obsługa dostawca i Agent

**Nazwa** | **Opis** | **Najnowsza wersja** | **Szczegóły**
--- | --- | --- | --- | ---
**Dostawca usługi Azure Site Recovery** | Współrzędne komunikacji między serwerami lokalnymi i Azure <br/><br/> Zainstalowana na serwerach programu Virtual Machine Manager lokalnie lub na serwerach funkcji Hyper-V, jeśli serwer programu Virtual Machine Manager nie jest | 5.1.19 ([dostępna z portalu](http://aka.ms/downloaddra)) | [Najnowsze funkcje i poprawki](https://support.microsoft.com/kb/3155002)
**Instalacja usługi Azure Site Recovery Unified (VMware tooAzure)** | Współrzędne komunikacji między serwerami lokalnymi VMware i Azure <br/><br/> Zainstalowana na lokalnych serwerach VMware | 9.3.4246.1 (dostępne w portalu) | [Najnowsze funkcje i poprawki](https://support.microsoft.com/kb/3155002)
**Usługa mobilności** | Koordynuje replikację między lokalnymi VMware serwerów/serwery fizyczne i Azure/dodatkowej lokacji<br/><br/> Zainstalowana na maszynie Wirtualnej VMware lub serwerów fizycznych mają tooreplicate  | N/d (dostępne w portalu) | Nie dotyczy
**Agent usług odzyskiwania Azure firmy Microsoft (MARS)** | Koordynuje replikację między maszynami wirtualnymi funkcji Hyper-V i platformą Azure<br/><br/> Zainstalowane na serwerach funkcji Hyper-V lokalnej (z lub bez serwera programu Virtual Machine Manager) | Najnowszą wersję agenta ([dostępna z portalu](http://aka.ms/latestmarsagent)) |






## <a name="next-steps"></a>Następne kroki
[Sprawdzanie wymagań wstępnych](site-recovery-prereq.md)
