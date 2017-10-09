---
title: "aaaSet się zasady replikacji w przypadku tooAzure replikacji maszyny Wirtualnej funkcji Hyper-V (w programie VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooset się zasady replikacji w przypadku tooAzure replikacji maszyny Wirtualnej funkcji Hyper-V (w programie VMM) z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a>Krok 10: Konfigurowanie zasad replikacji dla maszyny Wirtualnej funkcji Hyper-V tooAzure replikacji (w programie VMM)


Po skonfigurowaniu [mapowania sieci](vmm-to-azure-walkthrough-network-mapping.md), użyj tego artykułu tooconfigure zasad replikacji T\tooreplicate lokalnych maszyn wirtualnych funkcji Hyper-V zarządzanych w tooAzure chmur programu System Center Virtual Machine Manager (VMM), za pomocą hello [ Usługa Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="create-a-policy"></a>Tworzenie zasad

1. Kliknij przycisk toocreate nowe zasady replikacji, **przygotowanie infrastruktury** > **ustawienia replikacji** > **+ Utwórz i skojarz**.

    ![Sieć](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. W obszarze **Utwórz i skojarz zasady** określ nazwę zasad.
3. W **częstotliwość kopiowania**, określić, jak często dane różnicowe tooreplicate po replikacji początkowej hello (co 30 sekund, 5 lub 15 minut).

    > [!NOTE]
    >  30 częstotliwość drugiego nie jest obsługiwane podczas replikowania toopremium magazynu. ograniczenie Hello jest określana przez hello liczby migawek dla obiekt blob (w 100) obsługiwane przez Magazyn w warstwie premium. [Dowiedz się więcej](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. W **przechowywania punktu odzyskiwania**, określ w godzinach, jak długo będą hello okna przechowywania dla każdego punktu odzyskiwania. Chronione maszyny można odzyskać tooany punktu, w tym oknie.
5. W obszarze **Częstotliwość migawek spójności aplikacji** określ, jak często (1–12 godzin) będą tworzone punkty odzyskiwania zawierające migawki spójne z aplikacjami. Funkcja Hyper-V wykorzystuje dwa typy migawek — standardową migawkę, która jest przyrostową migawką całej maszyny wirtualnej hello i migawki spójne z aplikacją, która tworzy migawkę danych aplikacji hello wewnątrz maszyny wirtualnej hello punktu w czasie. Migawki spójne z aplikacjami Użyj tooensure usługi kopiowania woluminów w tle (VSS), które aplikacje są w spójnym stanie podczas hello migawki. Należy pamiętać, że po włączeniu migawek spójnych z aplikacją ma wpływ na powitania wydajność aplikacji uruchomionych na źródłowych maszynach wirtualnych. Upewnij się, że ustawiona wartość hello jest mniejsza niż liczba hello punktów odzyskiwania dodatkowe, które można skonfigurować.
6. W **czas rozpoczęcia replikacji początkowej**, wskazuje, kiedy toostart hello replikacji początkowej. Hello replikacja odbywa się za pośrednictwem przepustowości połączenia z Internetem, może być tooschedule ją poza najbardziej obciążonymi godzinami.
7. W **Szyfruj dane przechowywane na platformie Azure**, określ, czy tooencrypt dane w stanie spoczynku w magazynie Azure. Następnie kliknij przycisk **OK**.

    ![Zasady replikacji](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. Podczas tworzenia nowych zasad jest ona automatycznie skojarzona z hello chmury VMM. Kliknij przycisk **OK**. Dodatkowe chmury VMM (oraz hello maszyn wirtualnych w nich) można skojarzyć z zasadami replikacji w **replikacji** > nazwa_zasady > **Skojarz chmurę VMM**.

    ![Zasady replikacji](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 11: Włączanie replikacji](vmm-to-azure-walkthrough-enable-replication.md)
