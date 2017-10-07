---
title: "Architektura hello aaaReview dla lokacji dodatkowej tooa replikacji funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera omówienie architektury hello replikowania lokalnych maszyn wirtualnych funkcji Hyper-V tooa programu System Center VMM lokacja dodatkowa z usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a>Krok 1: Przegląd architektury powitania dla lokacji dodatkowej tooa replikacji funkcji Hyper-V

W tym artykule opisano składniki hello i procesów podczas replikowania lokalnych maszyn wirtualnych (VM) funkcji Hyper-V w chmurach programu System Center Virtual Machine Manager (VMM), tooa lokacja dodatkowa programu VMM przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md)w hello portalu Azure.

Opublikuj wszelkie komentarze u dołu hello tego artykułu lub hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Składniki architektury

Oto, co jest potrzebne do replikowania maszyn wirtualnych funkcji Hyper-V tooa dodatkowej lokacji programu VMM.

**Składnik** | **Lokalizacja** | **Szczegóły**
--- | --- | ---
**Azure** | Subskrypcja na platformie Azure. | Tworzenie magazynu usług odzyskiwania w hello subskrypcji platformy Azure, tooorchestrate i zarządzanie usługą replikacji między lokacjami programu VMM.
**Serwer VMM** | Potrzebujesz podstawowej i dodatkowej lokalizacji z programem VMM. | Zalecamy, aby serwer VMM w lokacji głównej hello i jeden w lokacji dodatkowej hello 
**Serwer funkcji Hyper-V** |  Jeden lub więcej funkcji Hyper-V serwerami hosta w hello głównych i dodatkowych chmurach VMM. | Dane są replikowane między hello podstawowych i pomocniczych serwerów Hyper-V hosta za pośrednictwem sieci LAN hello lub sieci VPN, korzystających z uwierzytelniania Kerberos lub certyfikatów.  
**Maszyny wirtualne funkcji Hyper-V** | Na serwerze hosta funkcji Hyper-V. | serwer hosta źródłowego Hello powinien mieć co najmniej jedną maszynę Wirtualną, które mają tooreplicate.

## <a name="replication-process"></a>Proces replikacji

1. Konfigurowanie hello konto platformy Azure, utworzyć magazyn usług odzyskiwania i określ sposób tooreplicate.
2. Możesz skonfigurować hello źródłowa i docelowa ustawienia replikacji, takich jak instalowanie hello dostawcy usługi Azure Site Recovery na serwerach VMM oraz agenta usług odzyskiwania Microsoft Azure hello na każdym hoście funkcji Hyper-V.
3. Możesz utworzyć zasady replikacji dla źródła hello chmury VMM. Hello zasady są stosowane tooall maszyn wirtualnych znajdujących się na hostach w chmurze hello.
4. Możesz włączyć replikację dla każdego programu VMM i następuje Replikacja początkowa maszyny wirtualnej zgodnie z ustawieniami hello, którą wybierzesz.
5. Po replikacji początkowej rozpocznie się replikacja zmian różnicowych. Śledzone zmiany elementu są przechowywane w pliku hrl.


![Lokalne tooon lokalnej](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a>Proces pracy w trybie failover i podczas powrotu po awarii

1. Planowane lub nieplanowane przejście w tryb [failover](site-recovery-failover.md) można uruchomić między lokacjami lokalnymi. Jeśli realizacja planowanego trybu failover, a następnie źródłowe maszyny wirtualne są zamknięte tooensure bez utraty danych.
2. Można przełączyć jednego komputera lub utworzyć [planów odzyskiwania](site-recovery-create-recovery-plans.md) tooorchestrate pracy w trybie failover wiele maszyn.
4. Jeśli nieplanowany tryb failover tooa lokacji dodatkowej, należy wykonać po hello trybu failover maszyny w lokalizacji dodatkowej hello nie są włączone dla ochrony lub replikacji. Po przeprowadzeniu planowany tryb failover po hello w tryb failover maszyny w lokalizacji dodatkowej hello są chronione.
5. Następnie Zatwierdź hello trybu failover toostart podczas uzyskiwania dostępu do hello obciążenia z hello repliki maszyny Wirtualnej.
6. Gdy lokacji głównej jest ponownie dostępny, zainicjowaniu tooreplicate replikacji odwrotnej z toohello lokacji dodatkowej hello podstawowego. Replikacji odwrotnej przełącza hello maszyny wirtualne w stanie chronionym hello dodatkowego centrum danych jest jednak nadal hello lokalizacji usługi active.
7. toomake hello lokacji głównej do lokalizacji usługi active hello ponownie inicjuje planowanego trybu failover z tooprimary dodatkowej, następuje innego replikacji odwrotnej.



## <a name="next-steps"></a>Następne kroki

Przejdź za[krok 2: Przejrzyj hello wymagania wstępne i ograniczenia](vmm-to-vmm-walkthrough-prerequisites.md).
