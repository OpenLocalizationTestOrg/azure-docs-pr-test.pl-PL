---
title: aaaRun test trybu failover dla funkcji Hyper-V tooAzure replikacji (z programu System Center VMM) | Dokumentacja firmy Microsoft
description: "Przedstawiono instrukcje hello, potrzebne do uruchomienia dla maszyn wirtualnych funkcji Hyper-V w chmurach VMM replikowanie tooAzure przy użyciu usługi Azure Site Recovery hello test trybu failover."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7b562a23-7ba7-48ee-905d-c22b4b5d6466
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: fc60e536f2eeb6f95dde3d347f364f3bf8bfdf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-for-hyper-v-replication-with-vmm-tooazure"></a>Krok 11: Uruchom test trybu failover dla funkcji Hyper-V tooAzure replikacji (w programie VMM)

Po [włączyć replikację dla maszyn wirtualnych funkcji Hyper-V](vmm-to-azure-walkthrough-enable-replication.md), użyj tego toorun artykułu test trybu failover z lokalnych maszyn wirtualnych funkcji Hyper-V zarządzane w tooAzure chmur programu System Center Virtual Machine Manager (VMM), za pomocą hello [ Usługa Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Przed rozpoczęciem

Aby uruchomić test trybu failover, zalecamy Sprawdź hello właściwości maszyny Wirtualnej i wprowadź wymagane zmiany należy. dostęp można uzyskać właściwości maszyny Wirtualnej hello w **elementy replikowane**. Witaj **Essentials** blok zawiera informacje o ustawieniach maszyn i stanu.

## <a name="managed-disk-considerations"></a>Zagadnienia dotyczące dysków zarządzanych

[Dyski zarządzane](../virtual-machines/windows/managed-disks-overview.md) uprościć zarządzanie dyskami na maszynach wirtualnych platformy Azure, zarządzając hello konta magazynu skojarzone z hello dysków maszyny Wirtualnej. 

- Dyski zarządzane są tworzone i dołączyć toohello maszyny Wirtualnej, tylko wtedy, gdy występuje tooAzure trybu failover. Po włączeniu ochrony danych z lokalnych maszyn wirtualnych replikowanych toostorage kont.
- Dyski zarządzane mogą być tworzone tylko dla maszyn wirtualnych, które są wdrażane za pomocą modelu wdrażania Menedżera zasobów hello.
- Powrót po awarii z platformy Azure tooan w lokalnym środowisku funkcji Hyper-V nie jest obsługiwana dla komputerów z dyskami zarządzanych. Należy ustawić tylko **Użyj zarządzanego dysków** za**tak** Jeśli podczas wykonywania migracji tylko (trybu failover tooAzure bez powrotu po awarii)
- To ustawienie jest włączone, zestawy dostępności tylko w grupach zasobów, które ma **Użyj zarządzanego dysków** włączona można wybrać. Maszyny wirtualne z dyskami zarządzanych musi być w zestawach dostępności z **Użyj zarządzanego dysków** ustawić także**tak**. Jeśli ustawienie hello nie jest włączone dla maszyn wirtualnych, można można wybrać tylko zestawów dostępności w grupach zasobów bez dysków zarządzanych włączone. [Dowiedz się więcej](../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set).
- - Jeśli hello konto magazynu, którego można użyć na potrzeby replikacji został zaszyfrowany przy użyciu szyfrowania usługi magazynu, dyski zarządzanego nie można utworzyć podczas pracy awaryjnej. W takim przypadku albo nie zezwalaj na używanie dysków zarządzanych lub Wyłącz ochronę dla maszyny Wirtualnej hello i ją ponownie włączyć toouse konta magazynu, który nie ma włączone szyfrowanie. [Dowiedz się więcej](../virtual-machines/windows/managed-disks-overview.md#managed-disks-and-encryption).

 
## <a name="network-considerations"></a>Zagadnienia dotyczące sieci
    
- Można ustawić hello docelowego adresu IP adres toobe używany dla hello maszyny Wirtualnej Azure po pracy awaryjnej. Jeśli nie podasz adresu, hello maszyny przełączonej będzie używać protokołu DHCP. Jeśli ustawisz adres, który nie jest dostępna w trybie failover hello trybu failover zakończy się niepowodzeniem. Witaj, sam docelowy adres IP może być używane do testowania trybu failover, jeśli adres hello jest dostępny w testowej sieci trybu failover hello.
- Hello liczbę kart sieciowych jest zależna hello rozmiar dla hello docelowej maszyny wirtualnej, w następujący sposób:
    - Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest mniejsza lub równa toohello liczba kart dozwoloną dla rozmiaru maszyny docelowej hello, a następnie hello docelowa będzie mieć hello samą liczbę kart sieciowych jako źródło hello.
    - Jeśli hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello przekracza liczbę hello dozwoloną dla hello rozmiar docelowy, a następnie maksymalny rozmiar docelowy hello będą używane.
    - Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe i rozmiaru maszyny docelowej hello obsługuje cztery karty, maszyna docelowa hello będzie mieć dwie karty sieciowe. Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello rozmiar docelowy obsługiwanych obsługuje tylko jedną maszyna docelowa hello będzie mieć tylko jedną kartę.     
- Jeśli hello maszyna wirtualna ma wiele kart sieciowych, wszystkie będą łączyć toohello tej samej sieci.
- Jeśli maszyna wirtualna hello ma wiele kart sieciowych, a następnie hello przedstawionego na liście hello staje się hello *domyślne* karty sieciowej w hello maszyny wirtualnej platformy Azure.


## <a name="view-and-manage-vm-settings"></a>Wyświetl i zarządzaj nimi ustawienia maszyny Wirtualnej

Firma Microsoft zaleca, sprawdź właściwości hello hello komputera źródłowego, przed uruchomieniem trybu failover.

1. W **chronione elementy**, kliknij przycisk **elementy replikowane**i kliknij przycisk hello maszyny Wirtualnej.

    ![Włączanie replikacji](./media/vmm-to-azure-walkthrough-test-failover/test-failover1.png)
2. W hello **elementu zreplikowane** okienku wyświetlane podsumowanie informacji, stan kondycji i hello najnowszych dostępnych punktów odzyskiwania maszyny Wirtualnej. Kliknij przycisk **właściwości** tooview więcej szczegółowych informacji.

    ![Włączanie replikacji](./media/vmm-to-azure-walkthrough-test-failover/test-failover2.png)
3. W **obliczenia i sieć**, można wykonywać następujące czynności:
    - Zmodyfikuj nazwę maszyny Wirtualnej Azure hello. Nazwa Hello musi spełniać [wymagania dotyczące usługi Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Określ failover post [grupy zasobów].
    - Określony rozmiar docelowy hello maszyny Wirtualnej Azure
    - Wybierz [zestawu dostępności](../virtual-machines/windows/tutorial-availability-sets.md).
    - Określ, czy toouse [dyskach zarządzanych](#managed-disk-considerations). Wybierz **tak**, jeśli chcesz tooattach dysków zarządzanych tooyour maszyny na tooAzure migracji.
    - Wyświetlanie i modyfikowanie ustawień sieciowych, takich jak hello sieć/podsieć, w których hello maszyny Wirtualnej Azure zostaną umieszczone po pracy awaryjnej i hello adresu IP, który zostanie przypisany tooit.

    ![Włączanie replikacji](./media/vmm-to-azure-walkthrough-test-failover/test-failover4.png)
4. W **dysków**, znajdują się informacje o systemie operacyjnym hello i dysków z danymi na hello maszyny Wirtualnej.


## <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

Teraz uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami.

- Jeśli chcesz, aby tooAzure tooconnect maszyn wirtualnych za pomocą protokołu RDP po przejściu w tryb failover, [przygotowanie tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - test toofully należy toocopy usługi Active Directory i DNS w środowisku testowym. [Dowiedz się więcej](site-recovery-active-directory.md#test-failover-considerations).
 - Aby uzyskać pełne informacje dotyczące testowania trybu failover, przeczytaj [w tym artykule](site-recovery-test-failover-to-azure.md) artykułu.
 
 Teraz można uruchomić trybu failover:

1. toofail na jednym komputerze, w **elementy replikowane**, kliknij przycisk hello maszyny Wirtualnej > **+ testowy tryb Failover** ikony.
2. Planowanie toofail za pośrednictwem odzyskiwania, **plany odzyskiwania**, kliknij prawym przyciskiem myszy hello planu > **testowy tryb Failover**. toocreate planu odzyskiwania [wykonaj te instrukcje](site-recovery-create-recovery-plans.md).
3. W **testowy tryb Failover**, wybierz pozycję toowhich sieć platformy Azure hello maszyny wirtualne Azure zostaną połączone po pracy awaryjnej.
4. Kliknij przycisk **OK** toobegin hello w tryb failover. Możesz śledzić postępy, klikając na powitania wirtualna tooopen jego właściwości lub na powitania **testowy tryb Failover** zadania w nazwie magazynu > **zadania** > **zadania usługi Site Recovery**.
5. Po zakończeniu pracy awaryjnej hello również powinno być możliwe toosee repliki hello Azure machine są wyświetlane w portalu Azure hello > **maszyn wirtualnych**. Należy upewnić się, że tej maszyny Wirtualnej hello jest hello odpowiedni rozmiar, który połączył toohello odpowiedniej sieci i czy działa.
6. Przygotowanie do nawiązywania połączeń po pracy awaryjnej należy toohello tooconnect stanie maszyny Wirtualnej platformy Azure.
7. Po zakończeniu kliknij **oczyszczania testowy tryb failover** na powitania planu odzyskiwania. W **uwagi** zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover. Spowoduje to usunięcie hello maszyn wirtualnych, które zostały utworzone podczas testowania trybu failover.



## <a name="next-steps"></a>Następne kroki

- [Dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover i w jaki sposób toorun je.
- [Przeczytaj informacje o awarii](site-recovery-failback-from-azure-to-hyper-v.md), toofail Wstecz i replikowania maszyn wirtualnych platformy Azure ponownie chmury VMM toohello głównej lokalnymi.

