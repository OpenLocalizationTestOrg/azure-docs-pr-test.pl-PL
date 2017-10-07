---
title: "lokacja dodatkowa tooa replikacji aaaEnable funkcji Hyper-V z usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooenable replikację dla maszyn wirtualnych funkcji Hyper-V, replikacja tooa, lokacji dodatkowej programu System Center VMM, z usługą Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a>Krok 9: Włącz lokacji dodatkowej tooa replikację dla maszyn wirtualnych funkcji Hyper-V


Po skonfigurowaniu zasad replikacji, należy używać lokacji programu System Center Virtual Machine Manager (VMM) dodatkowej tooa tego artykułu tooenable replikacji lokalnym funkcji Hyper-V maszyn wirtualnych (VM), za pomocą [usługi Azure Site Recovery](site-recovery-overview.md).

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="select-vms-tooreplicate"></a>Wybierz tooreplicate maszyny wirtualne

1. Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**. 

    ![Włączanie replikacji](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. W **źródła**, wybierz serwer VMM hello i hello chmury, w których hello znajdują się hosty funkcji Hyper-V ma tooreplicate. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. W **docelowego**, sprawdź hello pomocniczy serwer programu VMM i w chmurze.
4. W **maszyn wirtualnych**, wybierz hello maszyny wirtualne mają tooprotect z listy hello.

    ![Włączanie ochrony maszyny wirtualnej](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

Możesz śledzić postępy hello **Włącz ochronę** akcji w **zadania** > **zadania usługi Site Recovery**. Po hello **zakończenia ochrony** zadanie zostało ukończone, hello początkowej replikacji i maszyny wirtualnej hello jest gotowy do trybu failover.

Należy pamiętać, że:

- Można również włączyć ochronę maszyn wirtualnych w konsoli programu VMM hello. Kliknij przycisk **Włącz ochronę** na pasku narzędzi hello we właściwościach maszyny wirtualnej hello > **usługi Azure Site Recovery** kartę.
- Po włączeniu replikacji można wyświetlić właściwości hello maszyny Wirtualnej w **elementy replikowane**. Na powitania **Essentials** pulpitu nawigacyjnego, wyświetlane są informacje dotyczące zasad replikacji hello hello maszyny Wirtualnej i jej stan. Kliknij przycisk **właściwości** więcej szczegółów.

## <a name="onboard-existing-vms"></a>Dodaj istniejące maszyny wirtualne

Jeśli masz istniejące maszyny wirtualne w programie VMM, które są replikowane z funkcji Hyper-V Replica, możesz dołączyć je do replikacji usługi Azure Site Recovery w następujący sposób:

1. Upewnij się, że serwer hello funkcji Hyper-V hosting hello istniejącej maszyny Wirtualnej znajduje się w chmurze podstawowej hello oraz tego serwera funkcji Hyper-V hello obsługującego maszyny wirtualnej repliki hello znajduje się w chmurze dodatkowej hello.
2. Upewnij się, że skonfigurowano zasady replikacji dla chmury VMM podstawowej hello.
3. Włącz replikację hello podstawowej maszyny wirtualnej. Azure Site Recovery i VMM upewnij się, że hello tego samego hosta repliki i maszyny wirtualnej zostanie wykryte i będzie używał usługi Azure Site Recovery i ponownie ustanowić replikację przy użyciu hello określonych ustawień.


## <a name="next-steps"></a>Następne kroki

Przejdź za[kroku 10: testować tryb failover](vmm-to-vmm-walkthrough-test-failover.md).
