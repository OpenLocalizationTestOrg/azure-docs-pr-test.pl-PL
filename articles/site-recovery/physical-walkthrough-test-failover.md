---
title: "aaaRun test trybu failover dla serwera fizycznego tooAzure replikacji z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello, potrzebne do uruchomienia test trybu failover dla [replikowanie tooAzure przy użyciu usługi Azure Site Recovery hello serwerów fizycznych."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f8ed5ce585c5574be3018ce15339c4fd3b527eaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-of-physical-servers-tooazure"></a>Krok 11: Uruchom test trybu failover tooAzure serwerów fizycznych

W tym artykule opisano sposób toorun test trybu failover z lokalnymi tooAzure serwerów fizycznych, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Przed rozpoczęciem

Aby uruchomić test trybu failover, zalecamy Sprawdź właściwości serwera hello i wprowadź wymagane zmiany należy. dostęp można uzyskać właściwości maszyny Wirtualnej hello w **elementy replikowane**. Witaj **Essentials** blok zawiera informacje o ustawienia maszyny i stanu.

## <a name="managed-disk-considerations"></a>Zagadnienia dotyczące dysków zarządzanych

[Dyski zarządzane](../virtual-machines/windows/managed-disks-overview.md) uprościć zarządzanie dyskami na maszynach wirtualnych platformy Azure, zarządzając hello konta magazynu skojarzone z hello dysków maszyny Wirtualnej. 

- Po włączeniu ochrony dla serwera, dane maszyny Wirtualnej są replikowane tooa konta magazynu. Dyski zarządzane są tworzone i dołączyć toohello maszyny Wirtualnej, tylko w przypadku pracy awaryjnej.
- Dyski zarządzane mogą być tworzone tylko w przypadku wdrażania przy użyciu modelu Resource Manager hello maszynach wirtualnych platformy Azure.  
- To ustawienie jest włączone, zestawy dostępności tylko w grupach zasobów, które ma **Użyj zarządzanego dysków** włączona można wybrać. Maszyny wirtualne z dyskami zarządzanych musi być w zestawach dostępności z **Użyj zarządzanego dysków** ustawić także**tak**. Jeśli ustawienie hello nie jest włączone dla maszyn wirtualnych, można można wybrać tylko zestawów dostępności w grupach zasobów bez dysków zarządzanych włączone.
- [Dowiedz się więcej](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) o dostępności i dysków zarządzanych ustawia.
- Jeśli hello konto magazynu, którego można użyć na potrzeby replikacji został zaszyfrowany przy użyciu szyfrowania usługi magazynu, dyski zarządzanego nie można utworzyć podczas pracy awaryjnej. W takim przypadku albo nie zezwalaj na używanie dysków zarządzanych lub Wyłącz ochronę dla maszyny Wirtualnej hello i ją ponownie włączyć toouse konta magazynu, który nie ma włączone szyfrowanie. [Dowiedz się więcej](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="network-considerations"></a>Zagadnienia dotyczące sieci

Można ustawić hello docelowy adres IP dla maszyny Wirtualnej platformy Azure utworzonych po pracy awaryjnej.

- Jeśli nie podasz adresu, hello maszyny przełączonej będzie używać protokołu DHCP.
- Jeśli ustawisz adres, który nie jest dostępna w trybie failover, trybu failover nie będzie działać.
- Witaj, sam docelowy adres IP może być używane do testowania trybu failover, jeśli adres hello jest dostępny w testowej sieci trybu failover hello.
- Hello liczbę kart sieciowych zależy od rozmiaru hello, określonego dla docelowej maszyny wirtualnej hello:

     - Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest hello taki sam jak lub mniejsza niż hello liczba kart sieciowych dozwolonych dla rozmiaru maszyny docelowej hello, a następnie hello docelowa będzie mieć hello samą liczbę kart sieciowych jako źródło hello.
     - Jeśli hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello przekracza hello dozwolonej liczby dla rozmiaru docelowego hello, zostanie użyta maksymalna wielkość hello docelowej.
     - Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe, a rozmiar maszyny docelowej hello obsługuje cztery, maszyna docelowa hello będzie mieć dwie karty sieciowe. Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello rozmiar docelowy obsługiwanych obsługuje tylko jedną maszyna docelowa hello będzie mieć tylko jedną kartę.     
   - Jeśli maszyna wirtualna hello ma wiele kart sieciowych, wszystkie będą łączyć toohello tej samej sieci.
   - Jeśli maszyna wirtualna hello ma wiele kart sieciowych, a następnie hello przedstawionego na liście hello staje się hello *domyślne* karty sieciowej w hello maszyny wirtualnej platformy Azure.
 - [Dowiedz się więcej](vmware-walkthrough-network.md) dotyczące adresowania IP.



## <a name="view-and-modify-vm-settings"></a>Wyświetlanie i modyfikowanie ustawień maszyny Wirtualnej

Firma Microsoft zaleca, sprawdź właściwości hello powitania serwera źródłowego, przed uruchomieniem trybu failover.

1. W **chronione elementy**, kliknij przycisk **elementy replikowane**i kliknij przycisk hello maszyny.
2. W hello **elementu zreplikowane** okienku wyświetlane podsumowanie informacji o maszynie, stan kondycji i hello najnowszych dostępnych punktów odzyskiwania. Kliknij przycisk **właściwości** tooview więcej szczegółowych informacji.
3. W **obliczenia i sieć**, można wykonywać następujące czynności:
    - Zmodyfikuj nazwę maszyny Wirtualnej Azure hello. Nazwa Hello musi spełniać [wymagania dotyczące usługi Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Określ failover post [grupy zasobów].
    - Określony rozmiar docelowy hello maszyny Wirtualnej Azure
    - Wybierz [zestawu dostępności](../virtual-machines/windows/tutorial-availability-sets.md).
    - Określ, czy toouse [dyskach zarządzanych](#managed-disk-considerations). Wybierz **tak**, jeśli chcesz tooattach dysków zarządzanych tooyour maszyny na tooAzure migracji.
    - Wyświetlanie i modyfikowanie ustawień sieciowych, takich jak hello sieć/podsieć, w których hello maszyny Wirtualnej Azure zostaną umieszczone po pracy awaryjnej i hello adresu IP, który zostanie przypisany tooit.
4. W **dysków**, znajdują się informacje o systemie operacyjnym hello i dysków z danymi na hello maszyny Wirtualnej.

## <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

Po skonfigurowaniu wszystko, uruchom test toomake trybu failover, czy wszystko działa zgodnie z oczekiwaniami.

- Jeśli chcesz, aby tooAzure tooconnect maszyn wirtualnych za pomocą protokołu RDP po przejściu w tryb failover, [przygotowanie tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - test toofully należy toocopy usługi Active Directory i DNS w środowisku testowym. [Dowiedz się więcej](site-recovery-active-directory.md#test-failover-considerations).
 - Aby uzyskać pełne informacje dotyczące testowania trybu failover, przeczytaj [w tym artykule](site-recovery-test-failover-to-azure.md) artykułu.
- Uzyskać szybkie omówienie wideo, przed rozpoczęciem:

     
     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]

Teraz można uruchomić trybu failover:

1. toofail na jednym komputerze, w **ustawienia** > **elementy replikowane**, kliknij maszynę hello > **+ testowy tryb Failover** ikony.

    ![Testowanie trybu failover](./media/physical-walkthrough-test-failover/test-failover.png)

2. Planowanie toofail za pośrednictwem odzyskiwania, **ustawienia** > **plany odzyskiwania**, plan powitania kliknij prawym przyciskiem myszy > **testowy tryb Failover**. toocreate planu odzyskiwania [wykonaj te instrukcje](site-recovery-create-recovery-plans.md).  

3. W **testowy tryb Failover**, wybierz pozycję toowhich sieć platformy Azure hello maszyny wirtualne Azure zostaną połączone po pracy awaryjnej.

4. Kliknij przycisk **OK** toobegin hello w tryb failover. Możesz śledzić postępy, klikając na powitania maszyny tooopen jego właściwości lub na powitania **testowy tryb Failover** zadania w nazwie magazynu > **ustawienia** > **zadania**  >  **Zadania usługi site Recovery**.

5. Po zakończeniu pracy awaryjnej hello, należy także stanie toosee hello repliki maszyny Wirtualnej platformy Azure są wyświetlane w portalu Azure hello > **maszyn wirtualnych**. Należy upewnić się, że tej maszyny Wirtualnej hello jest hello odpowiedni rozmiar, który połączył toohello odpowiedniej sieci i czy działa.

6. Przygotowanie do nawiązywania połączeń po pracy awaryjnej należy toohello tooconnect stanie maszyny Wirtualnej platformy Azure.

### <a name="delete-test-failover-vms"></a>Usuń test trybu failover maszyny wirtualne

1. Po zakończeniu kliknij **oczyszczania testowy tryb failover** na maszynie lub hello planu odzyskiwania.
2. W **uwagi**, zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover.
3. Akcja oczyszczania Hello usuwa maszynach wirtualnych platformy Azure, które zostały utworzone podczas testowania trybu failover.

## <a name="summary"></a>Podsumowanie

Jeśli hello testowy tryb failover ukończone pomyślnie, replikowania serwerów fizycznych i została sprawdzona, że można przełączyć tooAzure. Teraz możesz uruchomić tryb failover zgodnie z wymaganiami organizacji. 

Należy pamiętać, że obecnie nie można przerwać z Azure tooa serwera fizycznego. Masz toofail kopii tooa maszyny Wirtualnej VMware. Oznacza to, że należy lokalnej infrastruktury programu VMware w kolejności toofail Wstecz. [Dowiedz się więcej](site-recovery-failback-azure-to-vmware.md) o awarii wstecz tooVMware maszynach wirtualnych platformy Azure.


## <a name="next-steps"></a>Następne kroki

- [Uruchomić tryb failover](site-recovery-failover.md) zgodnie z potrzebami.
