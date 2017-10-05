---
title: "Tabela wsparcia dla replikacji do lokacji dodatkowej z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Podsumowanie obsługiwanych systemów operacyjnych oraz składniki usługi Azure Site Recovery"
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
ms.openlocfilehash: db7ee5251f2e2016081e55ca4b295e284c8b08cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="support-matrix-for-replication-to-a-secondary-site-with-azure-site-recovery"></a>Tabela wsparcia dla replikacji do lokacji dodatkowej z usługą Azure Site Recovery

Ten artykuł zawiera podsumowanie, co jest obsługiwane, gdy używasz usługi Azure Site Recovery można replikować do lokacji dodatkowej lokalnymi.

## <a name="deployment-options"></a>Opcje wdrażania

**Wdrożenie** | **Serwer VMware/fizyczne** | **Funkcja Hyper-V (lub bez SCVMM)**
--- | --- | --- | ---
**Witryna Azure Portal** | Lokalnych maszyn wirtualnych VMware do lokacji dodatkowej VMware.<br/><br/> Pobierz [Podręcznik użytkownika InMage Scout](http://download.microsoft.com/download/E/0/8/E08B3BCE-3631-4CED-8E65-E3E7D252D06D/InMage_Scout_Standard_User_Guide_8.0.1.pdf) (niedostępne w portalu Azure). | Lokalnych maszyn wirtualnych funkcji Hyper-V w chmurach VMM do dodatkowej chmury VMM.<br></br> Nie jest obsługiwane bez programu VMM  <br/><br/> Tylko replikacji w funkcji Hyper-V standardowa. Sieć SAN nie jest obsługiwane.
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
**Funkcja Hyper-V (bez VMM)** | Nie obsługiwana konfiguracja replikacji do lokacji dodatkowej
**Funkcja Hyper-V w programie VMM** | Windows Server 2016 i Windows Server 2012 R2 z najnowszymi aktualizacjami.<br/><br/> Hosty z systemem Windows Server 2016 powinny być zarządzane przez program VMM 2016.

## <a name="support-for-replicated-machine-os-versions"></a>Obsługa wersji systemu operacyjnego zreplikowanej maszyny
Poniższa tabela zawiera podsumowanie obsługi systemów operacyjnych w różnych scenariuszy wdrażania podczas przy użyciu usługi Azure Site Recovery. Ta obsługa dotyczy dowolne obciążenia uruchomione na wymienione systemu operacyjnego.

**Serwer VMware/fizyczne** | **Funkcja Hyper-V (w programie VMM)**
--- | --- | ---
64-bitowego systemu Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 z na co najmniej z dodatkiem SP1<br/><br/> Red Hat Enterprise Linux 6.7, 7.1, 7.2 <br/><br/> Centos 6.5, 6.6, 6.7, 7.0, 7.1, 7.2 <br/><br/> Oracle Linux przedsiębiorstwa 6.4 lub 6.5 systemem Red Hat zgodne jądra lub podzielenie Enterprise jądra wersji 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 z dodatkiem SP3 | Gość żadnego systemu operacyjnego [obsługiwane przez funkcję Hyper-V](https://technet.microsoft.com/library/mt126277.aspx)

>[!Note]
>Mogą być replikowane tylko maszyn z systemem Linux z następującego magazynu: plików systemowych (EXT3, ETX4, ReiserFS, XFS); Mapowanie urządzeń wielościeżkowych oprogramowania; Menedżer woluminów (LVM2).
>Serwery fizyczne z HP CCISS kontrolera magazynu nie są obsługiwane.
>System plików ReiserFS jest obsługiwany tylko w systemie SUSE Linux Enterprise Server 11 z dodatkiem SP3.

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
DYSK VHD/VHDX | Nie dotyczy | Tak (maksymalnie 16 dysków)
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
**Usługa mobilności** | Koordynuje replikację między serwerami lokalnymi VMware lub serwerów fizycznych i lokacji dodatkowej<br/><br/> Zainstalowana na maszynie Wirtualnej VMware lub serwerów fizycznych, które chcesz replikować  | N/d (dostępne w portalu) | Nie dotyczy


## <a name="next-steps"></a>Następne kroki

- [Replikowanie maszyn wirtualnych funkcji Hyper-V w chmurach VMM do lokacji dodatkowej](site-recovery-vmm-to-vmm.md)
- [Replikacja maszyn wirtualnych VMware i serwerów fizycznych do lokacji dodatkowej](site-recovery-vmware-to-vmware.md)
