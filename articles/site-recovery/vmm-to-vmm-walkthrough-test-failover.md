---
title: "aaaRun test trybu failover dla lokacji dodatkowej tooa replikacji maszyny Wirtualnej funkcji Hyper-V z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toorun test trybu failover dla maszyny Wirtualnej funkcji Hyper-V tooa replikacji, lokacji dodatkowej programu System Center VMM, z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a>Krok 10: Uruchom test trybu failover dla lokacji dodatkowej tooa replikacji funkcji Hyper-V


Po włączeniu replikacji maszyn wirtualnych funkcji Hyper-V (maszyn wirtualnych) z [usługi Azure Site Recovery](site-recovery-overview.md), użyj tego artykułu toorun test trybu failover. Test trybu failover sprawdza, czy działa replikacja bez wpływu na środowisko produkcyjne. 


Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Przed rozpoczęciem

- Podczas jest wyzwalają test trybu failover, można określić hello sieci toowhich hello testu replikę, którą nawiążą połączenie maszyny wirtualne. [Dowiedz się więcej](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) o opcjach sieci hello.
- Zaleca się, że nie wybrano sieci z wybranym podczas mapowania sieci.
- Witaj instrukcje w tym artykule opisano sposób toofail za pośrednictwem jednej maszyny Wirtualnej. Przeczytaj informacje o [Tworzenie planów odzyskiwania](site-recovery-create-recovery-plans.md) Jeśli chcesz toofail przez wiele maszyn wirtualnych jednocześnie.
- Przeczytaj informacje o [ograniczenia dotyczące testowy tryb failover](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).
- Witaj adres IP podany tooa maszyny Wirtualnej podczas testowania trybu failover jest hello otrzyma tego samego adresu IP, który hello maszyny Wirtualnej dla planowanego lub nieplanowanego trybu failover (przy założeniu, że adres IP hello jest dostępny w testowej sieci trybu failover hello). Jeśli adres IP hello jest niedostępna w testowej sieci trybu failover hello, hello maszyna wirtualna odbiera innego adresu IP, który jest dostępny w testowej sieci trybu failover hello.
- Jeśli chcesz toodo test trybu failover w sieci produkcyjnej dla pełnej niepoprawny maszyny łączności sieciowej na całej trasie, należy pamiętać, że:
    - powitalne podstawowej maszyny Wirtualnej należy zamknąć podczas prowadzenia hello testowy tryb failover. W przeciwnym razie dwóch maszyn wirtualnych o tej samej tożsamości będzie uruchomiony w hello hello sam sieci na powitania tym samym czasie. 
    - Jeśli wprowadzisz zmiany tootest maszyn wirtualnych, te zmiany zostaną utracone podczas oczyszczania hello testowania trybu failover. Te zmiany nie są replikowane toohello wstecz podstawowej maszyny Wirtualnej.
    - Testowanie sieci produkcyjnej prowadzi toodowntime dla obciążeń produkcyjnych. Poproś użytkowników nie toouse aplikacji hello gdy wyszczególniania odzyskiwania po awarii hello jest w toku.  


## <a name="run-a-test-failover-for-a-vm"></a>Uruchom test trybu failover dla maszyny Wirtualnej

1. toofail za pośrednictwem jednej maszyny Wirtualnej w **elementy replikowane**, kliknij przycisk hello maszyny Wirtualnej > **testowy tryb Failover**.
2. W **testowego trybu Failover**, określ, jak testu maszyn wirtualnych zostaną połączone toonetworks po hello testowy tryb failover. 
3. Kliknij przycisk **OK** toobegin hello w tryb failover. Śledzenie postępów hello **zadania** kartę.
5. Po zakończeniu trybu failover Sprawdź pomyślnie test hello uruchamiania maszyn wirtualnych.
6. Gdy wszystko będzie gotowe, kliknij przycisk **oczyszczania testowy tryb failover** na powitania planu odzyskiwania.
7. W **uwagi**, zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover. Ten krok polega na usunięciu hello maszyn wirtualnych i sieci, które zostały utworzone podczas testowania trybu failover.


## <a name="next-steps"></a>Następne kroki

Po przetestowaniu wdrożenia hello więcej informacji na temat innych typów [pracy awaryjnej](site-recovery-failover.md).
