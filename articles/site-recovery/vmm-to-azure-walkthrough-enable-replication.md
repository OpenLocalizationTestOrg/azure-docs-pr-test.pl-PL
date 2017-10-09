---
title: "chmur aaaEnable tooAzure replikację dla maszyn wirtualnych funkcji Hyper-V w programie VMM z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooenable tooAzure replikację dla maszyn wirtualnych funkcji Hyper-V w programie VMM chmur z hello usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 89a2c4fc-7e03-4a86-a2c0-52831ccebc1a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 1a39bf65490c59a89a5e891184cadfacc2adee6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-tooazure-for-hyper-v-vms-in-vmm-clouds"></a>Krok 11: Włączanie replikacji tooAzure dla maszyn wirtualnych funkcji Hyper-V w chmurach programu VMM

Po skonfigurowaniu zasad replikacji replikacji tego artykułu tooenable na maszynach wirtualnych funkcji Hyper-V lokalnymi (VM) zarządzane w chmurach programu System Center Virtual Machine Manager (VMM)), tooAzure przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md)w hello portalu Azure.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Przed rozpoczęciem

Upewnij się, że konto Azure ma poprawne hello [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate maszynach wirtualnych platformy Azure. [Dowiedz się więcej](../active-directory/role-based-access-built-in-roles.md) o kontroli dostępu opartej na rolach na platformie Azure.

## <a name="exclude-disks-from-replication"></a>Wykluczanie dysków z replikacji

Domyślnie wszystkie dyski na komputerze są replikowane. Dyski można wykluczyć z replikacji. Na przykład nie ma dysków tooreplicate przy użyciu danych tymczasowych lub dane, które odświeżył każdym komputerze lub ponownym uruchomieniem aplikacji (na przykład pagefile.sys lub tempdb serwera SQL). [Dowiedz się więcej](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Replikowanie maszyn wirtualnych

Włącz replikację dla maszyn wirtualnych w następujący sposób:  

1. Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**. Po włączeniu replikacji dla powitania po raz pierwszy, kliknij przycisk **+ Replikuj** w hello magazynu tooenable replikację dla dodatkowych maszyn.

    ![Włączanie replikacji](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication1.png)
2. W hello **źródła** bloku, wybierz powitania serwera programu VMM i chmury hello w których hello funkcji Hyper-V znajdują się hosty. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-source.png)
3. W **docelowego**, wybierz hello subskrypcję, model wdrożenia po pracy w trybie failover, i hello konto magazynu używane dla replikowanych danych.

    ![Włączanie replikacji](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-target.png)
4. Wybierz konto magazynu hello, które chcesz toouse. Jeśli chcesz toouse innego konta magazynu niż te, które masz, możesz [utworzyć](#set-up-an-azure-storage-account). Jeśli używasz konta magazynu w warstwie premium dla replikowanych danych, należy tooselect dodatkowego magazynu standardowego konta toostore dzienników replikacji które przechwytują zachodzące zmiany lokalne tooon data.toocreate konto magazynu przy użyciu modelu Resource Manager hello Kliknij przycisk **Utwórz nowy**. Jeśli toocreate konto magazynu przy użyciu modelu klasycznego hello, należy to zrobić [w portalu Azure hello](../storage/common/storage-create-storage-account.md). Następnie kliknij przycisk **OK**.
5. Wybierz hello Azure toowhich sieci i podsieci maszyn wirtualnych platformy Azure będą się łączyć, gdy są tworzone po pracy awaryjnej. Wybierz **Konfiguruj teraz dla wybranych maszyn**, tooapply hello sieci ustawienie tooall maszyn wybranych do ochrony. Wybierz **później skonfigurować**, hello tooselect sieć platformy Azure dla poszczególnych komputerów. Jeśli chcesz toouse inną sieć z tymi masz, możesz [utworzyć](#set-up-an-azure-network). toocreate sieci za pomocą funkcji hello modelu Resource Manager, kliknij przycisk **Utwórz nowy**. Jeśli toocreate sieci przy użyciu modelu klasycznego hello, należy to zrobić [w portalu Azure hello](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Wybierz podsieć, jeśli jest to konieczne. Następnie kliknij przycisk **OK**.
6. W **maszyn wirtualnych** > **wybierz maszyny wirtualne**, kliknij i zaznacz każdy komputer ma tooreplicate. Możesz wybrać tylko te maszyny, dla których można włączyć replikację. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication5.png)

7. W **właściwości** > **skonfigurować właściwości**, wybierz system operacyjny hello hello wybrane maszyn wirtualnych i hello dysku systemu operacyjnego.

    - Sprawdź, że hello maszyny Wirtualnej Azure nazwę (docelowy) jest zgodna z [wymagania maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - Domyślnie wybrane są wszystkie dyski hello hello maszyny Wirtualnej replikacji, ale można wyczyścić tooexclude dysków je.

        - Możesz tooexclude dysków tooreduce replikacji przepustowości. Na przykład nie ma dysków tooreplicate o dane tymczasowe, lub dane, które ma odświeżane za każdym razem komputera lub aplikacje ponownego uruchomienia (na przykład pagefile.sys lub tempdb programu Microsoft SQL Server). Witaj dysku można wykluczyć z replikacji przez unselecting hello dysku.
        - Wykluczyć można tylko dyski podstawowe. Nie można wykluczyć dysków systemu operacyjnego.
        - Nie zalecamy wykluczania dysków dynamicznych. Wewnątrz maszyny wirtualnej gościa usługa Site Recovery nie może ustalić, czy wirtualny dysk twardy jest dyskiem podstawowym, czy dynamicznym. Wszystkie dyski woluminu dynamicznego zależnego nie są wykluczone, chronionego dysku dynamicznego hello wyświetli jako dysk nie powiodło się podczas hello maszyny Wirtualnej nie powiedzie się za pośrednictwem i dane hello na tym dysku nie będą dostępne.
        - Po włączeniu replikacji nie można dodawać ani usuwać dysków do replikacji. Tooadd lub wykluczyć dysk, wymagają ochrony toodisable dla hello maszyny Wirtualnej, a następnie włącz go ponownie.
        - Dyski tworzone ręcznie na platformie Azure nie mają możliwości powrotu po awarii. Na przykład jeśli się nie powieść ponad trzy dyski, a następnie utwórz dwa bezpośrednio w maszynie Wirtualnej platformy Azure, tylko te trzy dyski hello, które zostały przełączone do trybu failover nie powiedzie się z tooHyper Azure-V. Nie można dołączyć dyski utworzone ręcznie w przypadku powrotu po awarii lub w replikacji odwrotnej z tooAzure funkcji Hyper-V.
        - Jeśli dysk jest potrzebna dla toooperate aplikacji zostaną wykluczone, po tooAzure pracy awaryjnej należy toocreate, który można uruchomić go ręcznie na platformie Azure, tak że hello replikowane aplikacji. Alternatywnie można zintegrować usługi Automatyzacja Azure do planu odzyskiwania toocreate hello dysku podczas pracy awaryjnej hello maszyny.

    Kliknij przycisk **OK** toosave zmiany. Później możesz skonfigurować dodatkowe właściwości.

    ![Włączanie replikacji](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

8. W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, wybierz zasady replikacji hello ma tooapply hello chronionych maszyn wirtualnych. Następnie kliknij przycisk **OK**. Możesz zmodyfikować zasady replikacji hello w **zasady replikacji** > nazwa_zasady > **Edytuj ustawienia**. Zastosowane zmiany są używane dla obecnie replikowanych i nowych maszyn.

   ![Włączanie replikacji](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication7.png)

Możesz śledzić postępy hello **Włącz ochronę** zadania w **zadania** > **zadania usługi Site Recovery**. Po hello **zakończenia ochrony** zadanie jest uruchamiane, hello maszyna jest gotowa do pracy awaryjnej.



## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 12: testować tryb failover](vmm-to-azure-walkthrough-test-failover.md)
