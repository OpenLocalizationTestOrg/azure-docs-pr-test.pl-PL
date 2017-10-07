---
title: "Macierz aaaSupport dla lokacji dodatkowej tooa replikacji z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Podsumowanie hello obsługiwane systemy operacyjne oraz składniki usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 0b2bbc86aff52308d5a90a56d7a3ff4286877740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="support-matrix-for-replication-tooa-secondary-site-with-azure-site-recovery"></a>Tabela wsparcia dla lokacji dodatkowej tooa replikacji z usługą Azure Site Recovery

Ten artykuł zawiera podsumowanie, co jest obsługiwane, gdy używasz usługi Azure Site Recovery tooreplicate tooa lokalnego dodatkowej lokacji.

## <a name="deployment-options"></a>Opcje wdrażania

**Wdrożenie** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (lub bez SCVMM)**
--- | --- | --- | ---
**Witryna Azure Portal** | Lokalnej lokacji oprogramowania VMware toosecondary maszyn wirtualnych VMware.<br/><br/> Pobierz hello [Podręcznik użytkownika InMage Scout](http://download.microsoft.com/download/E/0/8/E08B3BCE-3631-4CED-8E65-E3E7D252D06D/InMage_Scout_Standard_User_Guide_8.0.1.pdf) (niedostępne w hello portalu Azure). | Lokalnych maszyn wirtualnych funkcji Hyper-V w chmurach tooa dodatkowej VMM chmurze VMM.<br></br> Nie jest obsługiwane bez programu VMM  <br/><br/> Tylko replikacji w funkcji Hyper-V standardowa. Sieć SAN nie jest obsługiwane.
**Portal klasyczny** | Tylko tryb konserwacji. Nie można utworzyć nowego magazynu. | Tylko w trybie konserwacji<br></br> Nie jest obsługiwane bez SCVMM
**PowerShell** | Nieobsługiwane | Obsługiwane<br></br> Nie jest obsługiwane bez SCVMM

## <a name="on-premises-servers"></a>Serwery lokalne

### <a name="virtualization-servers"></a>Serwerami wirtualizacji

**Wdrożenie** | **Pomoc techniczna**
--- | ---
**Maszyna wirtualna oprogramowania VMware/fizyczne serwera** | vSphere w wersji 6.0, 5.5 lub 5.1 z najnowszymi aktualizacjami
**Funkcja Hyper-V (w programie VMM)** | Program VMM 2016 i VMM 2012 R2

  >[!Note]
  > Chmury VMM 2016 z systemu Windows Server 2016 i 2012 R2 hosty nie są obecnie obsługiwane.

### <a name="host-servers"></a>Serwery hosta

**Wdrożenie** | **Pomoc techniczna**
--- | ---
**Maszyna wirtualna oprogramowania VMware/fizyczne serwera** | vCenter 5.5 lub 6.0 (Obsługa tylko funkcji 5.5)
**Funkcja Hyper-V (bez VMM)** | Nie obsługiwana konfiguracja replikacji tooa lokacji dodatkowej
**Funkcja Hyper-V w programie VMM** | Windows Server 2016 i Windows Server 2012 R2 z najnowszymi aktualizacjami hello.<br/><br/> Hosty z systemem Windows Server 2016 powinny być zarządzane przez program VMM 2016.

## <a name="support-for-replicated-machine-os-versions"></a>Obsługa wersji systemu operacyjnego zreplikowanej maszyny
Witaj w poniższej tabeli przedstawiono podsumowanie obsługi systemów operacyjnych w różnych scenariuszy wdrażania podczas przy użyciu usługi Azure Site Recovery. Ta obsługa dotyczy na dowolne obciążenia uruchomione na powitania określonych systemu operacyjnego.

**Serwer VMware/fizyczne** | **Funkcja Hyper-V (w programie VMM)**
--- | --- | ---
64-bitowego systemu Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 z na co najmniej z dodatkiem SP1<br/><br/> Red Hat Enterprise Linux 6.7, 7.1, 7.2 <br/><br/> Centos 6.5, 6.6, 6.7, 7.0, 7.1, 7.2 <br/><br/> Oracle Linux przedsiębiorstwa 6.4 lub 6.5 systemem jądra zgodne Red Hat hello lub podzielenie Enterprise jądra wersji 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 z dodatkiem SP3 | Gość żadnego systemu operacyjnego [obsługiwane przez funkcję Hyper-V](https://technet.microsoft.com/library/mt126277.aspx)

>[!Note]
>Mogą być replikowane tylko maszyn z systemem Linux z hello następującego magazynu: plików systemowych (EXT3, ETX4, ReiserFS, XFS); Mapowanie urządzeń wielościeżkowych oprogramowania; Menedżer woluminów (LVM2).
>Serwery fizyczne z HP CCISS kontrolera magazynu nie są obsługiwane.
>system plików ReiserFS Hello jest obsługiwana tylko w systemie SUSE Linux Enterprise Server 11 z dodatkiem SP3.

## <a name="network-configuration"></a>Konfiguracja sieci

### <a name="hosts"></a>Hosts

**Konfiguracja** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (w programie VMM)**
--- | --- | ---
Tworzenie zespołu kart sieciowych | Tak | Tak
SIECI VLAN | Tak | Tak
IPv4 | Tak | Tak
Protokół IPv6 | Nie | Nie

### <a name="guest-vms"></a>Maszyny wirtualne gości

**Konfiguracja** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (w programie VMM)**
--- | --- | ---
Tworzenie zespołu kart sieciowych | Nie | Nie
IPv4 | Tak | Tak
Protokół IPv6 | Nie | Nie
Statyczny adres IP (z systemem Windows) | Tak | Tak
Statyczny adres IP (Linux) | Tak | Tak
Obsługa wielu kart Sieciowych | Tak | Tak


## <a name="storage"></a>Magazyn

### <a name="host-storage"></a>Magazyn hosta

**Magazyn (hosta)** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (w programie VMM)**
--- | --- | ---
SYSTEMU PLIKÓW NFS | Tak | Nie dotyczy
SMB 3.0 | Nie dotyczy | Tak
SIECI SAN (ISCSI) | Tak | Tak
Wiele ścieżek (MPIO) | Tak | Tak

### <a name="guest-or-physical-server-storage"></a>Gość lub magazynu serwera fizycznego

**Konfiguracja** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (w programie VMM)**
--- | --- | ---
VMDK | Tak | Nie dotyczy
DYSK VHD/VHDX | Nie dotyczy | Tak (w górę dyski too16)
Gł 2 maszyny Wirtualnej | Nie dotyczy | Tak
Udostępniony dysk klastra | Tak  | Nie
Zaszyfrowanego dysku | Nie | Nie
Z INTERFEJSEM UEFI| Nie | Nie dotyczy
SYSTEMU PLIKÓW NFS | Nie | Nie
SMB 3.0 | Nie | Nie
DYSK RDM | Tak | Nie dotyczy
Na dysku > 1 TB | Nie | Tak
Wolumin dysku rozłożone > 1 TB<br/><br/> LVM | Tak | Tak
Funkcja miejsca do magazynowania | Nie | Tak
Dodaj lub usuń gorących dysku | Nie | Nie
Wykluczanie dysku | Nie | Tak
Wiele ścieżek (MPIO) | Nie dotyczy | Tak

## <a name="vaults"></a>magazynów

**Akcja** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (w programie VMM)**
--- | --- | ---
Przenieś magazynów między grupami zasobów (lub wielu subskrypcji) | Nie | Nie
Przenieść magazyn, sieć, maszyn wirtualnych platformy Azure w grupach zasobów (lub wielu subskrypcji) | Nie | Nie

## <a name="provider-and-agent"></a>Dostawca i agent

**Nazwa** | **Opis** | **Najnowsza wersja** | **Szczegóły**
--- | --- | --- | --- | ---
**Dostawca usługi Azure Site Recovery** | Współrzędne komunikacji między serwerami lokalnymi i Azure <br/><br/> Zainstalowana na lokalnych serwerach VMM lub na serwerach funkcji Hyper-V, jeśli serwer VMM nie jest | 5.1.19 ([dostępna z portalu](http://aka.ms/downloaddra)) | [Najnowsze funkcje i poprawki](https://support.microsoft.com/kb/3155002)
**Usługa mobilności** | Koordynuje replikację między serwerami lokalnymi VMware lub serwerów fizycznych i hello lokacji dodatkowej<br/><br/> Zainstalowana na maszynie Wirtualnej VMware lub serwerów fizycznych, które mają tooreplicate  | N/d (dostępne w portalu) | Nie dotyczy


## <a name="next-steps"></a>Następne kroki

- [Replikowanie maszyn wirtualnych funkcji Hyper-V w lokacji dodatkowej tooa chmury VMM](site-recovery-vmm-to-vmm.md)
- [Replikowanie maszyn wirtualnych VMware i serwery fizyczne tooa dodatkowej lokacji](site-recovery-vmware-to-vmware.md)
