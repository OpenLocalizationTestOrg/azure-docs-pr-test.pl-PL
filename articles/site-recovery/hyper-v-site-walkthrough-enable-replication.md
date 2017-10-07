---
title: "aaaEnable replikację dla maszyn wirtualnych funkcji Hyper-V, replikacja tooAzure (bez programu System Center VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy tooenable tooAzure replikację dla maszyn wirtualnych funkcji Hyper-V przy użyciu usługi Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a>Krok 10: Włączanie replikacji maszyn wirtualnych funkcji Hyper-V, replikacja tooAzure


W tym artykule opisano sposób replikacji tooenable dla lokalnych maszyn wirtualnych funkcji Hyper-V (nie zarządzanych przez program System Center VMM) tooAzure przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="before-you-start"></a>Przed rozpoczęciem

Przed rozpoczęciem należy upewnić się, że konto użytkownika usługi Azure ma hello wymagane [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikację nowego tooAzure maszyny wirtualnej.

## <a name="exclude-disks-from-replication"></a>Wykluczanie dysków z replikacji

Domyślnie wszystkie dyski na komputerze są replikowane. Dyski można wykluczyć z replikacji. Na przykład nie ma dysków tooreplicate przy użyciu danych tymczasowych lub dane, które odświeżył każdym komputerze lub ponownym uruchomieniem aplikacji (na przykład pagefile.sys lub tempdb serwera SQL). [Dowiedz się więcej](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a>Replikowanie maszyn wirtualnych

Włącz replikację dla maszyn wirtualnych w następujący sposób:          

1. Kliknij przycisk **Replikowanie aplikacji** > **źródła**. Po skonfigurowaniu replikacji dla powitania po raz pierwszy, możesz kliknąć **+ Replikuj** tooenable replikację dla dodatkowych maszyn.

    ![Włączanie replikacji](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. W **źródła**, wybierz pozycję witryny hello funkcji Hyper-V. Następnie kliknij przycisk **OK**.
3. W **docelowego**, wybierz subskrypcję magazynu hello i hello model trybu failover ma toouse na platformie Azure (Zarządzanie zasobu lub classic) po pracy awaryjnej.
4. Wybierz konto magazynu hello, które chcesz toouse. Jeśli nie masz konta toouse, możesz [utworzyć](#set-up-an-azure-storage-account). Następnie kliknij przycisk **OK**.
5. Wybierz hello Azure toowhich sieci i podsieci maszyn wirtualnych platformy Azure będzie Połącz, gdy są tworzone trybu failover.

    - Wybierz tooapply hello ustawienia tooall komputerów sieci można włączyć replikacji **Konfiguruj teraz dla wybranych maszyn**.
    - Wybierz **później skonfigurować** hello tooselect sieć platformy Azure dla poszczególnych komputerów.
    - Jeśli nie masz sieci ma toouse, możesz [utworzyć](#set-up-an-azure-network). Wybierz podsieć, jeśli jest to konieczne. Następnie kliknij przycisk **OK**.

   ![Włączanie replikacji](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. W **maszyn wirtualnych** > **wybierz maszyny wirtualne**, kliknij i zaznacz każdy komputer ma tooreplicate. Możesz wybrać tylko te maszyny, dla których można włączyć replikację. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. W **właściwości** > **skonfigurować właściwości**, wybierz system operacyjny hello hello wybrane maszyn wirtualnych i hello dysku systemu operacyjnego.
8. Sprawdź, że hello maszyny Wirtualnej Azure nazwę (docelowy) jest zgodna z [wymagania maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. Domyślnie wybrane są wszystkie dyski hello hello maszyny Wirtualnej do replikacji. Wyczyść dysków tooexclude je.
10. Kliknij przycisk **OK** toosave zmiany. Później możesz skonfigurować dodatkowe właściwości.

    ![Włączanie replikacji](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, wybierz zasady replikacji hello ma tooapply hello chronionych maszyn wirtualnych. Następnie kliknij przycisk **OK**. Możesz zmodyfikować zasady replikacji hello w **zasady replikacji** > Nazwa zasady > **Edytuj ustawienia**. Zastosowane zmiany będą używane dla obecnie replikowanych i nowych maszyn.


   ![Włączanie replikacji](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

Możesz śledzić postępy hello **Włącz ochronę** zadania w **zadania** > **zadania usługi Site Recovery**. Po hello **zakończenia ochrony** zadania działa hello maszyna jest gotowa do pracy awaryjnej.


## <a name="next-steps"></a>Następne kroki


Przejdź do zbyt[krok 11: testować tryb failover](hyper-v-site-walkthrough-test-failover.md)
