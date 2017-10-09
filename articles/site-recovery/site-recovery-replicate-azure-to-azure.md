---
title: aplikacje aaaReplicate (Azure tooAzure) | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak tooset replikacji wirtualnej maszyny działa w jednym regionie Azure zbyt innego regionu na platformie Azure."
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
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a>Replikowanie maszyn wirtualnych platformy Azure tooanother region platformy Azure



>[!NOTE]
>
> Replikacja lokacji odzyskiwania maszyn wirtualnych platformy Azure jest obecnie w przeglądzie.

W tym artykule opisano, jak tooset replikacji wirtualnej maszyny działa w jednym regionie Azure tooanother region platformy Azure.

## <a name="prerequisites"></a>Wymagania wstępne

* Artykuł Hello przyjęto założenie, że już wiedzę na temat odzyskiwania lokacji i magazynu usług odzyskiwania. Należy toohave sprzed "Magazyn usług odzyskiwania", utworzony.

    >[!NOTE]
    >
    > Zalecane jest utworzenie hello "Magazyn usług odzyskiwania" w hello lokalizację tooreplicate sieci maszyn wirtualnych. Na przykład jeśli lokalizacja docelowej środkowe stany USA, należy utworzyć magazynu w środkowe stany USA.

* Jeśli używane są zasady grupy zabezpieczeń sieci (NSG) lub połączenie internetowe toooutbound dostępu zapory serwera proxy toocontrol na powitania maszynach wirtualnych platformy Azure, upewnij się, że ten użytkownik dozwolonych hello wymagane adresy URL lub adresów IP. Odwołuje się zbyt[sieci wytycznych](./site-recovery-azure-to-azure-networking-guidance.md) więcej szczegółów.

* Jeśli masz usługi ExpressRoute lub połączenie sieci VPN między lokalnymi i hello źródła lokalizacji na platformie Azure, wykonaj [lokacji zagadnienia związane z lokalnym tooon Azure ExpressRoute / konfiguracji sieci VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) dokumentu.

* Twoje konto użytkownika systemu Azure wymaga toohave niektórych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikacji maszyny wirtualnej platformy Azure.

* Subskrypcji platformy Azure powinna być włączona toocreate maszyn wirtualnych w miejscu docelowym hello ma toouse jako region odzyskiwania po awarii. Możesz skontaktować się przydział wymagany hello tooenable pomocy technicznej.

## <a name="enable-replication-from-azure-site-recovery-vault"></a>Włącz replikację z magazynu usługi Azure Site Recovery
Na tej ilustracji możemy będą replikowane maszyny wirtualne uruchomione w toohello lokalizacji platformy Azure "Azja Wschodnia" hello "Azja południowo-wschodnia" lokalizacji. Witaj obejmuje następujące czynności:

 Kliknij przycisk **+ Replikuj** w hello magazynu tooenable replikacji hello maszyn wirtualnych.

1. **Źródło:** odnosi się toohello punkt początkowy maszyn hello, w tym przypadku jest **Azure**.

2. **Lokalizacja źródłowa:** jest hello region platformy Azure, z którym chcesz tooprotect maszyn wirtualnych. Na tej ilustracji lokalizacji źródłowej hello będzie "Azja Wschodnia"

3. **Model wdrażania:** odnosi się model wdrożenia usługi Azure toohello hello maszyny źródłowej. Można wybrać obu classic lub Menedżera zasobów i komputery należące do określonego modelu toohello zostaną wyświetlone w celu ochrony w hello następnego kroku.

      >[!NOTE]
      >
      > Można tylko replikowanie klasyczne maszyny wirtualnej i odzyskać ją jako maszynę wirtualną w klasycznym. Nie można go odzyskać jako maszynę wirtualną Menedżera zasobów.

4. **Grupa zasobów:** tego toowhich grupy zasobów hello należą źródła maszyn wirtualnych. W celu ochrony w następnym krokiem hello wyświetlą się hello wszystkich maszyn wirtualnych w obszarze hello wybranej grupy zasobów.

    ![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

W **maszyny wirtualnej > Wybierz maszyny wirtualne**, kliknij i zaznacz każdy komputer ma tooreplicate. Możesz wybrać tylko te maszyny, dla których można włączyć replikację. Następnie kliknij przycisk OK.
    ![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)


W sekcji Ustawienia można skonfigurować właściwości lokacji docelowej

1. **Lokalizacja docelowa:** hello lokalizacja, gdzie będą replikowane dane źródłowe maszyny wirtualnej. W zależności od lokalizacji wybranych maszyn Site Recovery umożliwi hello listę regionów odpowiedniego elementu docelowego.

    > [!TIP]
    > Zalecane jest lokalizacja docelowa tookeep takie same jak odzyskiwania usług magazynu.

2. **Docelowa grupa zasobów:** jest toowhich grupy zasobów hello wszystkie zreplikowanej maszyny wirtualne będą należeć. Domyślnie funkcja automatycznego odzyskiwania systemu utworzy nową grupę zasobów w regionie docelowym hello z nazwą składającą się z sufiksem "asr". W przypadku grupy zasobów utworzonej przez ASR już istnieje, zostanie ono użyte ponownie. Możesz również toocustomize go jak pokazano w poniższej sekcji hello.    
3. **Sieć wirtualna docelowa:** domyślnie ASR spowoduje utworzenie nowej sieci wirtualnej w region docelowy hello z nazwą składającą się z sufiksem "asr". To zostanie zamapowane tooyour źródłowej sieci i będzie służyć do przyszłych ochrony.

    > [!NOTE]
    > [Sprawdź szczegóły sieci](site-recovery-network-mapping-azure-to-azure.md) tooknow więcej informacji na temat mapowania sieci.

4. **Docelowa kont magazynu:** domyślnie ASR utworzy hello nowe docelowe konto magazynu mimicking konfigurację magazynu maszyny Wirtualnej źródłowego. W przypadku konta magazynu utworzone przez usługi ASR już istnieje, zostanie ono użyte ponownie.

5. **Buforowanie kont magazynu:** ASR wymaga konta dodatkowego magazynu o nazwie magazynu pamięci podręcznej w regionie źródła hello. Witaj wszystkie zmiany wykonywane na powitania źródłowe maszyny wirtualne są śledzone i przed replikowanie tych lokalizacji docelowej toohello wysyłane toocache konta magazynu.

6. **Zestaw dostępności:** domyślnie ASR utworzy nowy zestawem dostępności w region docelowy hello z nazwą składającą się z sufiksem "asr". W przypadku, gdy zestaw dostępności utworzony przez ASR już istnieje, zostanie ono użyte ponownie.

7.  **Zasady replikacji:** definiuje ustawienia hello częstotliwości odzyskiwania punktu przechowywania historii i aplikacji migawki dotyczącej spójności. Domyślnie funkcja automatycznego odzyskiwania systemu utworzy nowe zasady replikacji z ustawieniami domyślnymi 24 godzin przechowywania punktu odzyskiwania i "60 minut częstotliwości migawki dotyczącej spójności aplikacji.

    ![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a>Dostosowywanie zasobami obiektów docelowych

W przypadku, gdy chcesz toochange hello domyślne używane przez usługi ASR, możesz zmienić ustawienia hello na podstawie Twoich potrzeb.

1. **Dostosowywanie:** kliknij go toochange hello wartości domyślne używane przez usługi ASR.

2. **Docelowa grupa zasobów:** hello grupy zasobów można wybrać z listy hello wszystkich grup zasobów hello istniejące w lokalizacji docelowej hello w ramach subskrypcji hello.

3. **Sieć wirtualna docelowa:** hello listę wszystkich hello sieci wirtualnej można znaleźć w miejscu docelowym hello.

4. **Zestaw dostępności:** można dodawać tylko dostępność zestawów ustawień toohello maszyn wirtualnych, które są częścią dostępności w regionie źródła.

5. **Konta magazynu docelowego:**

![Włącz replikację](./media/site-recovery-replicate-azure-to-azure/customize.PNG) kliknij **tworzenie zasobu docelowego** i włączyć replikację


Gdy są chronione maszyny wirtualne można sprawdzić hello stan kondycji maszyn wirtualnych w obszarze **zreplikowane elementy**

>[!NOTE]
>Podczas hello replikacji początkowej można możliwość, że stan przyjmuje toorefresh czasu i nie widzisz postępu przez pewien czas. Możesz kliknąć przycisk Odśwież hello na początku hello hello bloku tooget hello najnowszy stan.
>

![Włączanie replikacji](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a>Następne kroki
- [Dowiedz się więcej](site-recovery-test-failover-to-azure.md) uruchomiony test trybu failover.
- [Dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover i w jaki sposób toorun je.
- Dowiedz się więcej o [przy użyciu planów odzyskiwania](site-recovery-create-recovery-plans.md) tooreduce RTO.
- Dowiedz się więcej o [ponownej ochrony maszyn wirtualnych platformy Azure](site-recovery-how-to-reprotect.md) po pracy awaryjnej.
