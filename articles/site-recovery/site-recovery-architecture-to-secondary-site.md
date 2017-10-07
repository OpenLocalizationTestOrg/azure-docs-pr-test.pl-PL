---
title: "aaaHow działa lokalnie maszyny replikacji tooa lokalnego dodatkowej lokacji w usłudze Azure Site Recovery? | Microsoft Docs"
description: "Ten artykuł zawiera omówienie składników i architektury używany podczas replikowania lokalnych maszyn wirtualnych i serwerów fizycznych tooa lokacji dodatkowej z hello usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: raynew
ms.openlocfilehash: 097a3f43446fec69ed7f9e0b7f11e8d11f41cc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-on-premises-machine-replication-tooa-secondary-site-work-in-site-recovery"></a>Sposób lokalnego komputera replikacji tooa lokacji dodatkowej pracy w usłudze Site Recovery?

W tym artykule opisano składniki hello i procesów podczas replikowania lokalnych maszyn wirtualnych i serwerów fizycznych tooAzure, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) usługi.

Można replikować hello następującej lokacji dodatkowej lokalnymi tooa:
- Lokalne maszyny wirtualne funkcji Hyper-V i maszyny wirtualne funkcji Hyper-V na hostach autonomicznych i w klastrach funkcji Hyper-V zarządzanych w chmurach programu System Center Virtual Machine Manager (VMM).
- Lokalne maszyny wirtualne VMware oraz serwery fizyczne z systemami Windows i Linux. W tym scenariuszu replikacja jest zarządzana przez program Scout.

Opublikuj wszelkie komentarze u dołu hello tego artykułu lub hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="replicate-hyper-v-vms-tooa-secondary-on-premises-site"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V tooa lokalnej dodatkowej lokacji


### <a name="architectural-components"></a>Składniki architektury

Oto, co jest potrzebne do replikowania maszyn wirtualnych funkcji Hyper-V tooa dodatkowej lokacji.

**Składnik** | **Lokalizacja** | **Szczegóły**
--- | --- | ---
**Azure** | Będziesz potrzebować konta w usługach firmy Microsoft. |
**Serwer VMM** | Zalecamy, aby serwer VMM w lokacji głównej hello i jeden w lokacji dodatkowej hello | Każdy serwer VMM powinien być toohello połączenia internetowego.<br/><br/> Każdy serwer powinien mieć co najmniej jedną prywatną chmurę VMM, z zestawem profilu możliwości hello funkcji Hyper-V.<br/><br/> Witaj dostawcy usługi Azure Site Recovery należy zainstalować na serwerze VMM hello. Witaj dostawca koordynuje i organizuje replikację za pomocą hello usługi Site Recovery za pośrednictwem hello internet. Komunikacja między hello dostawcy i na platformie Azure, jest bezpieczna i szyfrowana.
**Serwer funkcji Hyper-V** |  Jeden lub więcej funkcji Hyper-V serwerami hosta w hello głównych i dodatkowych chmurach VMM.<br/><br/> Serwery powinny być połączone toohello internet.<br/><br/> Dane są replikowane między hello podstawowych i pomocniczych serwerów Hyper-V hosta za pośrednictwem sieci LAN hello lub sieci VPN, korzystających z uwierzytelniania Kerberos lub certyfikatów.  
**Maszyny wirtualne funkcji Hyper-V** | Znajduje się na serwerze hosta funkcji Hyper-V źródła hello. | serwer hosta źródłowego Hello powinien mieć co najmniej jedną maszynę Wirtualną, które mają tooreplicate.

### <a name="replication-process"></a>Proces replikacji

1. Konfigurowanie hello konto platformy Azure.
2. Należy utworzyć magazyn usługi Replication Services na potrzeby usługi Site Recovery i skonfigurować ustawienia magazynu, w tym następujące elementy:

    - Witaj replikacji źródłowa i docelowa (w lokacjach głównych i dodatkowych).
    - Instalacja hello dostawcy usługi Azure Site Recovery i agent usług odzyskiwania Microsoft Azure hello. Witaj dostawca jest zainstalowany na serwerach VMM i hello agenta na każdym hoście funkcji Hyper-V.
    - Należy utworzyć zasady replikacji dla źródłowej chmury programu VMM. Hello zasady są stosowane tooall maszyn wirtualnych znajdujących się na hostach w chmurze hello.
    - Należy włączyć replikację maszyn wirtualnych funkcji Hyper-V. Zgodnie z ustawieniami zasad replikacji hello następuje Replikacja początkowa.
4. Dane zmiany są śledzone, a replikacja zmian zmienia toobegins po zakończeniu replikacji początkowej hello. Śledzone zmiany elementu są przechowywane w pliku hrl.
5. Uruchomienie testu toomake trybu failover, czy wszystko działa połączenie.

**Rysunek 1: Program VMM tooVMM replikacji**

![Lokalne tooon lokalnej](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback-process"></a>Proces pracy w trybie failover i podczas powrotu po awarii

1. Planowane lub nieplanowane przejście w tryb [failover](site-recovery-failover.md) można uruchomić między lokacjami lokalnymi. Jeśli realizacja planowanego trybu failover, a następnie źródłowe maszyny wirtualne są zamknięte tooensure bez utraty danych.
2. Można przełączyć jednego komputera lub utworzyć [planów odzyskiwania](site-recovery-create-recovery-plans.md) tooorchestrate pracy w trybie failover wiele maszyn.
4. Jeśli nieplanowany tryb failover tooa lokacji dodatkowej, należy wykonać po hello trybu failover maszyny w lokalizacji dodatkowej hello nie są włączone dla ochrony lub replikacji. Po przeprowadzeniu planowany tryb failover po hello w tryb failover maszyny w lokalizacji dodatkowej hello są chronione.
5. Następnie Zatwierdź hello trybu failover toostart podczas uzyskiwania dostępu do hello obciążenia z hello repliki maszyny Wirtualnej.
6. Gdy lokacji głównej jest ponownie dostępny, zainicjowaniu tooreplicate replikacji odwrotnej z toohello lokacji dodatkowej hello podstawowego. Replikacji odwrotnej przełącza hello maszyny wirtualne w stanie chronionym hello dodatkowego centrum danych jest jednak nadal hello lokalizacji usługi active.
7. toomake hello lokacji głównej do lokalizacji usługi active hello ponownie inicjuje planowanego trybu failover z tooprimary dodatkowej, następuje innego replikacji odwrotnej.




## <a name="replicate-vmware-vmsphysical-servers-tooa-secondary-site"></a>Replikowanie maszyn wirtualnych VMware/fizycznych serwerów tooa lokacji dodatkowej

Replikowania maszyn wirtualnych VMware lub serwerów fizycznych tooa dodatkowej lokacji przy użyciu InMage Scout, za pomocą tych architektury składników:


### <a name="architectural-components"></a>Składniki architektury

**Składnik** | **Lokalizacja** | **Szczegóły**
--- | --- | ---
**Azure** | InMage Scout. | tooobtain InMage Scout, potrzebujesz subskrypcji platformy Azure.<br/><br/> Po utworzeniu magazynu usług odzyskiwania pobranie programu InMage Scout i zainstalować hello najnowsze aktualizacje tooset hello wdrożenia.
**Serwer przetwarzania** | Znajduje się w lokacji głównej | Możesz wdrożyć hello procesu serwera toohandle pamięci podręcznej, kompresji i optymalizacji danych.<br/><br/> Umożliwia on również obsługę instalacji wypychanej hello ma tooprotect toomachines Unified Agent.
**Serwer konfiguracji** | Znajduje się w lokacji dodatkowej | Hello serwer konfiguracji zarządza, konfigurowania i monitorowania wdrażania, albo za pomocą witryny sieci Web hello zarządzania lub konsoli vContinuum hello.
**Serwer vContinuum** | Opcjonalny. Zainstalowane w hello sam lokalizacji co powitania serwera konfiguracji. | Zapewnia on konsolę do monitorowania chronionego środowiska i zarządzania nim.
**Główny serwer docelowy** | Znajduje się w lokacji dodatkowej hello | Witaj głównym serwerze docelowym przechowywane są zreplikowane dane. Go odbiera dane z serwera przetwarzania hello, tworzy maszynę repliki w lokacji dodatkowej hello i przechowuje punkty przechowywania danych hello.<br/><br/> Hello liczby potrzebnych serwerów głównego celu zależy od hello liczba maszyny, który jest chronisz.<br/><br/> Chcesz lokacji głównej toofail toohello Wstecz, należy najpierw głównego serwera docelowego za. Witaj Unified Agent jest zainstalowany na tym serwerze.
**Program VMware ESX/ESXi i serwer vCenter** |  Maszyny wirtualne są hostowane na hostach ESX/ESXi. Hosty są zarządzane za pomocą serwera vCenter | Należy tooreplicate infrastruktury VMware maszyn wirtualnych VMware.
**Maszyny wirtualne/serwery fizyczne** |  Unified Agent został zainstalowany na maszynach wirtualnych VMware i serwerów fizycznych, które chcesz tooreplicate. | Witaj agent działa jako dostawca komunikacji między wszystkimi składnikami hello.


### <a name="replication-process"></a>Proces replikacji

1. Skonfigurować serwery składników hello w każdej lokacji (Konfiguracja, proces, główny serwer docelowy), a następnie zainstalować hello Unified Agent na maszynach, które mają tooreplicate.
2. Po replikacji początkowej agent hello na każdej maszynie wysyła serwera przetwarzania toohello zmiany replikacji różnicowej.
3. Hello serwer przetwarzania optymalizuje hello danych i transferuje je toohello główny serwer docelowy w lokacji dodatkowej hello. Witaj serwer konfiguracji zarządza procesem replikacji hello.

**Rysunek 2: VMware tooVMware replikacji**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)


## <a name="next-steps"></a>Następne kroki

Przejrzyj hello [macierz obsługi](site-recovery-support-matrix-to-sec-site.md)
