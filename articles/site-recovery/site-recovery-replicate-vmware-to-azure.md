---
title: Replikowanie aplikacji (VMware tooAzure) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak tooset replikacji wirtualnej maszyny działa w programie VMware do platformy Azure."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: asgang
ms.openlocfilehash: b07aabdacec521c7bd89e50f6a1427a774ff0287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-applications-running-on-vmware-vms-tooazure"></a>Replikowanie aplikacji uruchomionych na maszynach wirtualnych VMware tooAzure



W tym artykule opisano, jak tooset replikacji wirtualnej maszyny działa w programie VMware do platformy Azure.
## <a name="prerequisites"></a>Wymagania wstępne

Witaj artykule przyjęto założenie, że masz już

1.  [Konfigurowanie lokalnego środowiska źródłowego](site-recovery-set-up-vmware-to-azure.md)
2.  [Konfigurowanie środowiska docelowego na platformie Azure](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a>Włączanie replikacji
#### <a name="before-you-start"></a>Przed rozpoczęciem
Podczas replikowania maszyn wirtualnych VMware, należy pamiętać, że:

* Twoje konto użytkownika systemu Azure wymaga toohave niektórych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikację nowego tooAzure maszyny wirtualnej.
* Maszyny wirtualne VMware odnalezieniu co 15 minut. Może zająć 15 minut lub dłużej, aby je tooappear w portalu powitania po odnajdywania. Podobnie odnajdowania może zająć 15 minut lub dłużej, po dodaniu nowego hosta serwera lub vSphere vCenter.
* Zmiany środowiska na maszynie wirtualnej hello (takie jak Instalacja narzędzi VMware) może zająć 15 minut lub więcej toobe zaktualizowane w portalu hello.
* Możesz sprawdzić hello ostatnio odnalezione czasu w maszynach wirtualnych VMware hello **ostatniego kontaktu w** dla hello vCenter server/hostem vSphere, na powitania pole **serwery konfiguracji** bloku.
* tooadd maszyn do replikacji bez oczekiwania na powitania zaplanowanego odnajdywania, zaznacz serwer konfiguracji hello (nie klikaj pozycji go) i kliknij przycisk hello **Odśwież** przycisku.
* Po włączeniu replikacji, jeśli maszyny hello jest gotowy, serwer przetwarzania hello automatycznie instaluje usługi mobilności hello na nim.


**Teraz Włącz replikację w następujący sposób**:

1. Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**. Po włączeniu replikacji dla powitania po raz pierwszy, kliknij przycisk **+ Replikuj** w hello magazynu tooenable replikację dla dodatkowych maszyn.
2. W hello **źródła** bloku > **źródła**, wybierz pozycję powitania serwera konfiguracji.
3. W **komputera typu**, wybierz pozycję **maszyn wirtualnych** lub **maszyn fizycznych**.
4. W **vCenter/vSphere Hypervisor**, wybierz hello vCenter server zarządzającego hostem vSphere hello, lub wybierz hello host. To ustawienie nie jest istotne, Jeśli replikujesz maszyny fizyczne.
5. Wybierz serwer przetwarzania hello. Jeśli nie utworzono żadnych serwerów dodatkowych procesów będzie nazwa hello powitania serwera konfiguracji. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. W **docelowej** wybierz hello subskrypcji i grupy zasobów hello miejscu hello toocreate przejścia w tryb failover maszyny wirtualnej. Wybierz model wdrożenia hello, która ma toouse na platformie Azure (Zarządzanie zasobu lub classic) hello przejścia w tryb failover maszyny wirtualnej.
7. Wybierz konto magazynu Azure hello, które chcesz toouse do replikacji danych. Należy pamiętać, że:

   * Możesz wybrać premium lub konta standard storage. W przypadku wybrania konta premium należy toospecify dodatkowe konto magazynu dla dzienników trwającej replikacji. Konta muszą być w hello magazyn usług odzyskiwania i tym samym regionie co hello.
   * Jeśli chcesz toouse innego konta magazynu niż te, które masz możesz utworzyć jedną*łącze symbolu zastępczego do tworzenia konta magazynu przy użyciu zasobów manager, które zostały omówione w sekcji wprowadzenie*. Kliknij przycisk toocreate konto magazynu przy użyciu Menedżera zasobów **Utwórz nowy**. Jeśli chcesz toocreate konto magazynu przy użyciu modelu klasycznego hello, można to zrobić [w portalu Azure hello](../storage/common/storage-create-storage-account.md).

8. Wybierz hello Azure toowhich sieci i podsieci maszyn wirtualnych platformy Azure będą się łączyć, gdy zostaną uruchomione po pracy awaryjnej. sieć Hello musi znajdować się w hello magazyn usług odzyskiwania i tym samym regionie co hello. Wybierz **Konfiguruj teraz dla wybranych maszyn**, tooapply hello sieci ustawienie tooall maszyn wybranych do ochrony. Wybierz **później skonfigurować** hello tooselect sieć platformy Azure dla poszczególnych komputerów. Jeśli nie masz sieci, należy za[utworzyć](#set-up-an-azure-network). Kliknij toocreate sieci przy użyciu Menedżera zasobów **Utwórz nowy**. Jeśli toocreate sieci przy użyciu modelu klasycznego hello, należy to zrobić [w portalu Azure hello](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Wybierz podsieć, jeśli jest to konieczne. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. W **maszyn wirtualnych** > **wybierz maszyny wirtualne**, kliknij i zaznacz każdy komputer ma tooreplicate. Możesz wybrać tylko te maszyny, dla których można włączyć replikację. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. W **właściwości** > **skonfigurować właściwości**, wybierz pozycję hello konta, które będą używane przez hello procesu serwera tooautomatically Zainstaluj hello usługi mobilności na maszynie hello.  
11. Domyślnie wszystkie dyski są replikowane. dyski tooexclude z replikacji, kliknij przycisk **wszystkie dyski** i wyczyść wszystkie dyski, które nie mają tooreplicate.  Następnie kliknij przycisk **OK**. Później możesz skonfigurować dodatkowe właściwości. [Dowiedz się więcej](site-recovery-exclude-disk.md) o z wyjątkiem dysków.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, sprawdź, że hello poprawne wybrano zasady replikacji. Można modyfikować ustawień zasad replikacji w **ustawienia** > **zasady replikacji** > nazwa_zasady > **Edytuj ustawienia**. Zmiany można zastosować zasady tooa będą stosowane tooreplicating i nowych maszyn.
13. Włącz **spójności wielu maszyn wirtualnych** toogather maszyny do grupy replikacji, i określ nazwę grupy hello. Następnie kliknij przycisk **OK**. Należy pamiętać, że:

    * Maszyny w replikacji grupy replikacji ze sobą i udostępnione punkty odzyskiwania spójna w razie awarii i spójności aplikacji podczas ich w tryb failover.
    * Zaleca się, że użytkownik zbiera maszyn wirtualnych i serwerów fizycznych, aby odzwierciedlały obciążeń. Włączenie spójności wielu maszyn wirtualnych może wpłynąć na wydajność obciążeń i powinien być używany tylko przez hello są uruchomione maszyny tego samego obciążenia i wymagana jest spójność.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. Kliknij przycisk **włączyć replikację**. Możesz śledzić postępy hello **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**. Po hello **zakończenia ochrony** zadania działa hello maszyna jest gotowa do pracy awaryjnej.

> [!NOTE]
> Jeśli maszyna hello jest gotowy do wypychanej instalacji powitania po włączeniu ochrony zostanie zainstalowany składnik usługi mobilności. Po hello składnik jest zainstalowany na komputerze hello, który uruchamia zadanie ochrony i kończy się niepowodzeniem. Po awarii hello należy toomanually ponowne uruchomienie każdego komputera. Po hello ponownego uruchomienia hello ochrony zadania rozpoczyna się ponownie i następuje Replikacja początkowa.
>
>

## <a name="view-and-manage-vm-properties"></a>Wyświetlanie właściwości maszyny wirtualnej i zarządzanie nimi

Firma Microsoft zaleca sprawdzenie właściwości hello hello maszyny źródłowej. Pamiętaj o tej nazwie maszyny Wirtualnej Azure hello powinna być zgodna z [wymagania maszyny wirtualnej platformy Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Kliknij przycisk **ustawienia** > **elementy replikowane** > i wybierz hello maszyny. Witaj **Essentials** blok zawiera informacje o ustawieniach maszyn i stanu.
2. W **właściwości**, można wyświetlić replikacji i trybu failover informacje dotyczące hello maszyny Wirtualnej.
3. W **obliczenia i sieć** > **właściwości obliczeń**, można określić rozmiaru maszyny Wirtualnej Azure hello nazwę i obiekt docelowy. Zmodyfikować hello toocomply nazwy z wymagania dotyczące usługi Azure, jeśli potrzebujesz.
    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  Możesz wybrać [grupy zasobów](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) z komputera, który będzie częścią post w tryb failover. Możesz zmienić to ustawienie dowolnym momencie przed niepowodzeniem za pośrednictwem. POST w trybie Failover, w przypadku migrowania hello maszyny tooa innej grupie zasobów, a następnie ustawienia ochrony maszyny zostaną przerwane.
5. Możesz wybrać [zestawu dostępności](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) w razie potrzeby komputerze toobe być częścią jednej post w tryb failover. Podczas ustawiania wybór dostępności, sprawdź należy pamiętać, że:

    * Tylko zestawy dostępności toohello należące określony zostaną wyświetlone grupy zasobów  
    * Komputery z różnych sieciach wirtualnych nie może być częścią tego samego zestawu dostępności
    * Tylko maszyny wirtualne o tym samym rozmiarze może być częścią tego samego zestawu dostępności
5. Można również wyświetlić i dodać informacje dotyczące sieci docelowej hello, podsieci i adres IP, który zostanie przypisany toohello maszyny Wirtualnej platformy Azure.
6. W **dysków**, można sprawdzić hello systemu operacyjnego i dysków z danymi na hello maszyny Wirtualnej, która będzie replikowana.

### <a name="network-adapters-and-ip-addressing"></a>Kart sieciowych i adresów IP 

- Można ustawić hello docelowy adres IP. Jeśli nie podasz adresu, hello maszyny przełączonej będzie używać protokołu DHCP. Jeśli ustawisz adres, który nie jest dostępna w trybie failover hello trybu failover nie będzie działać. Witaj, sam docelowy adres IP może być używane do testowania trybu failover, jeśli adres hello jest dostępny w testowej sieci trybu failover hello.
- Hello liczbę kart sieciowych jest zależna hello rozmiar dla hello docelowej maszyny wirtualnej, w następujący sposób:
    - Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest mniejsza lub równa toohello liczba kart dozwoloną dla rozmiaru maszyny docelowej hello, a następnie hello docelowa będzie mieć hello samą liczbę kart sieciowych jako źródło hello.
    - Jeśli hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello przekracza liczbę hello dozwoloną dla hello rozmiar docelowy, a następnie maksymalny rozmiar docelowy hello będą używane.
    - Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe i rozmiaru maszyny docelowej hello obsługuje cztery karty, maszyna docelowa hello będzie mieć dwie karty sieciowe. Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello rozmiar docelowy obsługiwanych obsługuje tylko jedną maszyna docelowa hello będzie mieć tylko jedną kartę.
    - Jeśli maszyna wirtualna hello ma wiele kart sieciowych, wszystkie będą łączyć toohello tej samej sieci.
    - Jeśli maszyna wirtualna hello ma wiele kart sieciowych, a następnie hello przedstawionego na liście hello staje się hello *domyślne* karty sieciowej w hello maszyny wirtualnej platformy Azure.
   



## <a name="common-issues"></a>Typowe problemy

* Każdy dysk powinien być mniejszy niż 1TB.
* dysk systemu operacyjnego Hello powinien być dysku podstawowego i nie dynamicznego dysku
* 2 generacji z interfejsem UEFI włączona maszyn wirtualnych, hello rodziny systemów operacyjnych należy systemu Windows i dysku rozruchowego powinien być mniejszy niż 300GB.

## <a name="next-steps"></a>Następne kroki

Po zakończeniu ochrona powitalnych, możesz spróbować [awaryjnie](site-recovery-failover.md) toocheck Określa, czy aplikacja pojawia się na platformie Azure, czy nie.

W przypadku ochrony toodisable, należy sprawdzić jak zbyt[wyczyścić ustawienia rejestracji i ochrony](site-recovery-manage-registration-and-protection.md)
