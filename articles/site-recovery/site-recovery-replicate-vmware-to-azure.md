---
title: Replikowanie aplikacji (VMware do platformy Azure) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób skonfigurowania replikacji maszyn wirtualnych uruchomionych na VMware do platformy Azure."
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
ms.openlocfilehash: e0047a996c9bfd7d950b32f0871ddd7608924b42
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-applications-running-on-vmware-vms-to-azure"></a>Replikowanie aplikacji uruchomionych na maszynach wirtualnych VMware do platformy Azure



W tym artykule opisano sposób skonfigurowania replikacji maszyn wirtualnych uruchomionych na VMware do platformy Azure.
## <a name="prerequisites"></a>Wymagania wstępne

Zakłada się, że masz już

1.  [Konfigurowanie lokalnego środowiska źródłowego](site-recovery-set-up-vmware-to-azure.md)
2.  [Konfigurowanie środowiska docelowego na platformie Azure](site-recovery-prepare-target-vmware-to-azure.md)


## <a name="enable-replication"></a>Włączanie replikacji
#### <a name="before-you-start"></a>Przed rozpoczęciem
Podczas replikowania maszyn wirtualnych VMware, należy pamiętać, że:

* Twoje konto użytkownika usługi Azure musi mieć niektórych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) Aby włączyć replikację nowej maszyny wirtualnej na platformie Azure.
* Maszyny wirtualne VMware odnalezieniu co 15 minut. Może zająć 15 minut lub dłużej, aby były widoczne w portalu po odnajdywania. Podobnie odnajdowania może zająć 15 minut lub dłużej, po dodaniu nowego hosta serwera lub vSphere vCenter.
* Zmiany środowiska na maszynie wirtualnej (na przykład instalacji narzędzi VMware) może zająć 15 minut lub więcej do zaktualizowania w portalu.
* Można sprawdzić czas ostatniego odnalezionych w maszynach wirtualnych VMware w **ostatniego kontaktu w** w nagłówku hosta serwera/vSphere vCenter, **serwery konfiguracji** bloku.
* Aby dodać maszyn do replikacji bez oczekiwania na zaplanowanego odnajdywania, zaznacz serwer konfiguracji (nie klikaj pozycji go) i kliknij przycisk **Odśwież** przycisku.
* Po włączeniu replikacji, jeśli komputer jest gotowy, serwer przetwarzania automatycznie instaluje usługi mobilności na nim.


**Teraz Włącz replikację w następujący sposób**:

1. Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**. Po włączeniu replikacji po raz pierwszy kliknij pozycję **+ Replikuj** w magazynie, aby włączyć replikację dla dodatkowych maszyn.
2. W **źródła** bloku > **źródła**, wybierz serwer konfiguracji.
3. W **komputera typu**, wybierz pozycję **maszyn wirtualnych** lub **maszyn fizycznych**.
4. W **vCenter/vSphere Hypervisor**, wybierz serwer vCenter, który zarządza hostem vSphere lub wybierz host. To ustawienie nie jest istotne, Jeśli replikujesz maszyny fizyczne.
5. Wybierz serwer przetwarzania. Jeśli nie utworzono żadnych serwerów dodatkowych procesów to nazwa serwera konfiguracji. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication2.png)

6. W **docelowej** wybierz subskrypcji i grupy zasobów, w której chcesz utworzyć nieudane przez maszyny wirtualne. Wybierz model wdrażania, którego chcesz użyć na platformie Azure (model usługi Resource Manager lub model klasyczny) dla maszyn wirtualnych w trybie failover.
7. Wybierz konto magazynu Azure, którego chcesz użyć do replikacji danych. Należy pamiętać, że:

   * Możesz wybrać premium lub konta standard storage. W przypadku wybrania konta premium musisz określić dodatkowe konto magazynu dla dzienników trwającej replikacji. Konta muszą być w tym samym regionie co magazyn usług odzyskiwania.
   * Jeśli chcesz użyć innego konta magazynu niż te, które masz, możesz utworzyć jedną*łącze symbolu zastępczego do tworzenia konta magazynu przy użyciu zasobów manager, które zostały omówione w sekcji wprowadzenie*. Aby utworzyć konto magazynu przy użyciu usługi Resource Manager, kliknij przycisk **Utwórz nowy**. Jeśli chcesz utworzyć konto magazynu przy użyciu modelu klasycznego, należy to zrobić [w portalu Azure](../storage/common/storage-create-storage-account.md).

8. Wybierz sieć platformy Azure i podsieć, z którą połączy się maszyn wirtualnych platformy Azure, po ich uruchomieniu po pracy awaryjnej. Sieć musi znajdować się w tym samym regionie co magazyn Usług odzyskiwania. Wybierz opcję **Konfiguruj teraz dla wybranych maszyn**, aby zastosować ustawienia sieci do wszystkich maszyn wybranych do ochrony. Wybierz opcję **Konfiguruj później**, aby wybrać sieć platformy Azure dla poszczególnych maszyn. Jeśli nie masz sieci, należy [utworzyć](#set-up-an-azure-network). Aby utworzyć sieć przy użyciu usługi Resource Manager, kliknij przycisk **Utwórz nowy**. Jeśli chcesz utworzyć sieć przy użyciu modelu klasycznego, zrób to [w witrynie Azure Portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Wybierz podsieć, jeśli jest to konieczne. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-rep3.png)
9. W pozycji **Maszyny wirtualne** > **Wybierz maszyny wirtualne** kliknij i zaznacz każdą maszynę, którą chcesz replikować. Możesz wybrać tylko te maszyny, dla których można włączyć replikację. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication5.png)
10. W **właściwości** > **skonfigurować właściwości**, wybierz konto, które będzie używane przez serwer przetwarzania Aby automatycznie zainstalować usługi mobilności na maszynie.  
11. Domyślnie wszystkie dyski są replikowane. Aby wykluczyć dysków z replikacji, kliknij przycisk **wszystkie dyski** i wyczyść wszystkie dyski, które nie mają być replikowane.  Następnie kliknij przycisk **OK**. Później możesz skonfigurować dodatkowe właściwości. [Dowiedz się więcej](site-recovery-exclude-disk.md) o z wyjątkiem dysków.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication6.png)

12. W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, sprawdź, czy jest wybrane zasady replikacji poprawne. Można modyfikować ustawień zasad replikacji w **ustawienia** > **zasady replikacji** > nazwa_zasady > **Edytuj ustawienia**. Zmiany dotyczą zasady zostaną zastosowane do replikacji i nowe maszyny.
13. Włącz **spójności wielu maszyn wirtualnych** Jeśli chcesz zebrać maszyn w grupie replikacji i określ nazwę grupy. Następnie kliknij przycisk **OK**. Należy pamiętać, że:

    * Maszyny w replikacji grupy replikacji ze sobą i udostępnione punkty odzyskiwania spójna w razie awarii i spójności aplikacji podczas ich w tryb failover.
    * Zaleca się, że użytkownik zbiera maszyn wirtualnych i serwerów fizycznych, aby odzwierciedlały obciążeń. Włączenie spójności wielu maszyn wirtualnych może wpłynąć na wydajność obciążeń i należy używać tylko w przypadku maszyn działają te same obciążenia i wymagana jest spójność.

    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/enable-replication7.png)
14. Kliknij przycisk **włączyć replikację**. Możesz śledzić postęp **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**. Po uruchomieniu zadania **Sfinalizuj ochronę** maszyna jest gotowa do przejścia w tryb failover.

> [!NOTE]
> Jeśli komputer jest gotowy do instalacji wypychanej, który ma być zainstalowany składnik usługi mobilności, po włączeniu ochrony. Po składnik jest zainstalowany na komputerze, na którym uruchamia zadanie ochrony i kończy się niepowodzeniem. Po awarii należy ręcznie uruchomić ponownie każdej maszyny. Po ponownym uruchomieniu zadania ochrony rozpoczyna się ponownie i następuje Replikacja początkowa.
>
>

## <a name="view-and-manage-vm-properties"></a>Wyświetlanie właściwości maszyny wirtualnej i zarządzanie nimi

Zalecamy zweryfikowanie właściwości maszyny źródłowej. Pamiętaj, że nazwa maszyny wirtualnej Azure powinna być zgodna z [wymaganiami dotyczącymi maszyn wirtualnych Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. Kliknij przycisk **ustawienia** > **elementy replikowane** > i wybierz maszynę. **Essentials** blok zawiera informacje o ustawieniach maszyn i stanu.
2. W obszarze **Właściwości** możesz wyświetlić informacje dotyczące replikacji i trybu failover dla danej maszyny wirtualnej.
3. W pozycji **Obliczenia i sieć** > **Właściwości obliczeń** możesz określić nazwę i docelowy rozmiar maszyny wirtualnej Azure. Zmodyfikuj nazwę, aby spełniać wymagania dotyczące usługi Azure, jeśli potrzebujesz.
    ![Włączanie replikacji](./media/site-recovery-vmware-to-azure/VMProperties_AVSET.png)
 
4.  Możesz wybrać [grupy zasobów](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-resource-groups-guidelines) z komputera, który będzie częścią post w tryb failover. Możesz zmienić to ustawienie dowolnym momencie przed niepowodzeniem za pośrednictwem. POST w trybie Failover, w przypadku migrowania komputera do innej grupie zasobów, a następnie spowoduje przerwanie ustawienia ochrony maszyny.
5. Możesz wybrać [zestawu dostępności](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) przypadku komputerze musi być częścią jednej post w tryb failover. Podczas ustawiania wybór dostępności, sprawdź należy pamiętać, że:

    * Zostaną wyświetlone tylko zestawy dostępności należących do określonej grupy zasobów  
    * Komputery z różnych sieciach wirtualnych nie może być częścią tego samego zestawu dostępności
    * Tylko maszyny wirtualne o tym samym rozmiarze może być częścią tego samego zestawu dostępności
5. Można również wyświetlić i dodać informacje dotyczące sieci docelowej, podsieci i adres IP, który zostanie przypisany do maszyny Wirtualnej platformy Azure.
6. W **dysków**, możesz wyświetlać systemu operacyjnego i dysków z danymi na maszynie Wirtualnej, która będzie replikowana.

### <a name="network-adapters-and-ip-addressing"></a>Kart sieciowych i adresów IP 

- Możesz ustawić docelowy adres IP. Jeśli nie podasz adresu, maszyna w trybie failover będzie używać protokołu DHCP. Jeśli ustawisz adres, który nie jest dostępna w trybie failover, przejście w tryb failover nie będzie działać. Ten sam docelowy adres IP może być użyty do testowania trybu failover, jeśli adres jest dostępny w testowej sieci trybu failover.
- Liczba kart sieciowych zależy od rozmiaru określonego dla docelowej maszyny wirtualnej, zgodnie z poniższym:
    - Jeśli liczba kart sieciowych w maszynie źródłowej jest mniejsza lub równa liczbie kart sieciowych dozwolonych dla rozmiaru maszyny docelowej, maszyna docelowa będzie mieć taką samą liczbę kart sieciowych jak maszyna źródłowa.
    - Jeśli liczba kart sieciowych dla źródłowej maszyny wirtualnej przekracza liczbę dozwolonych kart sieciowych dla rozmiaru maszyny docelowej, zostanie użyta maksymalna liczba kart dla rozmiaru maszyny docelowej.
    - Przykładowo, jeśli maszyna źródłowa ma dwie karty sieciowe, a rozmiar maszyny docelowej obsługuje cztery karty, maszyna docelowa będzie mieć dwie karty sieciowe. Jeśli maszyna źródłowa ma dwie karty sieciowe, ale rozmiar maszyny docelowej obsługuje tylko jedną kartę, maszyna docelowa będzie mieć tylko jedną kartę sieciową.
    - Jeśli maszyna wirtualna ma wiele kart sieciowych, wszystkie będą łączyć z tą samą siecią.
    - Jeśli maszyna wirtualna ma wiele kart sieciowych, staje się pierwszym przedstawionego na liście *domyślne* karty sieciowej na maszynie wirtualnej platformy Azure.
   



## <a name="common-issues"></a>Typowe problemy

* Każdy dysk powinien być mniejszy niż 1TB.
* Dysk systemu operacyjnego powinien być dyskiem podstawowym, a nie dyskiem dynamicznym
* W przypadku maszyn wirtualnych drugiej generacji/z obsługą interfejsu UEFI wymagana jest rodzina systemu operacyjnego Windows, a dysk rozruchowy powinien być mniejszy niż 300 GB

## <a name="next-steps"></a>Następne kroki

Po zakończeniu ochrony, możesz spróbować [awaryjnie](site-recovery-failover.md) do sprawdzenia, czy aplikacja pojawia się na platformie Azure lub nie.

W przypadku, gdy chcesz wyłączyć ochronę, sprawdź jak [wyczyścić ustawienia rejestracji i ochrony](site-recovery-manage-registration-and-protection.md)
