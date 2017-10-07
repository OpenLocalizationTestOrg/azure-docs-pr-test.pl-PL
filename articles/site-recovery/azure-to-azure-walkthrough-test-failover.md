---
title: "aaaRun test trybu failover dla replikacji maszyny Wirtualnej platformy Azure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie hello kroki wymagane do uruchamiania test trybu failover dla maszyn wirtualnych platformy Azure replikacji tooanother region platformy Azure przy użyciu hello Azure Site Recovery usługi."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a>Krok 6: Uruchom test trybu failover dla replikacji maszyny Wirtualnej Azure

Po włączeniu replikacji dla maszyny wirtualnej platformy Azure (maszyny wirtualne), wykonaj kroki hello w tym artykule toorun testowy tryb failover z jednego regionu Azure tooanother, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

- Po zakończeniu artykułu hello powinien potwierdził test trybu failover, co najmniej jednej maszyny Wirtualnej platformy Azure można przełączyć tooyour dodatkowej region platformy Azure. 
- Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Replikacja maszyny Wirtualnej platformy Azure jest obecnie w przeglądzie.


## <a name="before-you-start"></a>Przed rozpoczęciem

- Przed uruchomieniem test trybu failover zaleca się zweryfikować hello właściwości maszyny Wirtualnej, a wprowadzone zmiany, które należy. dostęp można uzyskać właściwości maszyny Wirtualnej hello w **elementy replikowane**. Witaj **Essentials** blok zawiera informacje o ustawieniach maszyn i stanu.
- Zalecane jest użycie oddzielnej sieci maszyny Wirtualnej platformy Azure dla hello testowy tryb failover, a nie hello sieci (domyślne lub dostosować) który zostało skonfigurowane do pracy awaryjnej w środowisku produkcyjnym.
- Witaj test pracy awaryjnej przejdzie w tryb failover maszyn wirtualnych platformy Azure (wraz z ich magazynem) toohello dodatkowej region platformy Azure. Go nie są replikowane wszystkich zależnych aplikacji lub zasobów. Aplikacje działające na nie powiodło się przez maszyny wirtualne są zależne inne zasoby, takie jak usługi Active Directory i DNS, należy najpierw tooreplicate są zbyt, jeśli ich nie jest już dostępne w danym regionie pomocniczym. [Dowiedz się więcej](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- Jeśli chcesz tooaccess replikowane maszyny wirtualne po trybie failover z lokacji lokalnej, należy za[przygotowanie tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese maszyn wirtualnych.

## <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

1. W **ustawienia** > **elementy replikowane**, kliknij przycisk hello wirtualna **+ testowy tryb Failover** ikony. 

2. W **testowy tryb Failover**, wybierz toouse punktu odzyskiwania dla trybu failover hello:

    - **Najnowsze przetworzone**: kończy się niepowodzeniem hello maszyny Wirtualnej za pośrednictwem toohello najnowszy punkt odzyskiwania, który został przetworzony przez usługę Site Recovery hello. Sygnatura czasowa Hello jest wyświetlany. Ta opcja nie jest czas przetwarzania danych, dzięki czemu oferuje RTO niski (celu czasu odzyskiwania).
    - **Najnowsza wersja aplikacji spójne**: Ta opcja nie powiedzie się za pośrednictwem wszystkich maszyn wirtualnych toohello najnowszy całej aplikacji punkt odzyskiwania. Sygnatura czasowa Hello jest wyświetlany. 
    - **Niestandardowe**: wybrać dowolny punkt odzyskiwania.
 
3. Wybierz hello docelowej sieci wirtualnej platformy Azure toowhich maszyn wirtualnych Azure w regionie pomocniczym hello zostaną połączone po przejściu hello pracy awaryjnej.
4. toostart hello trybu failover, kliknij przycisk **OK**. tootrack postępu, kliknij przycisk tooopen wirtualna hello jego właściwości. Możesz też kliknąć przycisk hello **testowy tryb Failover** zadania w nazwie magazynu hello > **ustawienia** > **zadania** > **zadania usługi Site Recovery**.
5. Po hello trybu failover zakończy, hello replika maszyny Wirtualnej Azure pojawia się w hello portalu Azure > **maszyn wirtualnych**. Upewnij się, że tej maszyny Wirtualnej hello jest hello odpowiedni rozmiar, który połączył toohello odpowiedniej sieci i czy działa.
6. toodelete hello maszyn wirtualnych, które zostały utworzone podczas hello testowania trybu failover kliknij **oczyszczania testowy tryb failover** na powitania replikowane element lub hello planu odzyskiwania. W **uwagi**, zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover. 

[Dowiedz się więcej](site-recovery-test-failover-to-azure.md) o testowy tryb failover.

## <a name="next-steps"></a>Następne kroki

Po przetestowaniu trybu failover, w tym przewodniku została ukończona. Teraz Dowiedz się więcej o uruchamianiu przechodzenia w tryb failover w środowisku produkcyjnym:

- [Dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover i w jaki sposób toorun je.
- Dowiedz się więcej o niepowodzeniu przez wiele maszyn wirtualnych [przy użyciu planu odzyskiwania](site-recovery-create-recovery-plans.md).
- Dowiedz się więcej o [przy użyciu planów odzyskiwania](site-recovery-create-recovery-plans.md).
- Dowiedz się więcej o [ponownej ochrony maszyn wirtualnych platformy Azure](site-recovery-how-to-reprotect.md) po pracy awaryjnej.

