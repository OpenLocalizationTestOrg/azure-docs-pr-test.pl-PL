---
title: "aaaEnable replikację dla maszyn wirtualnych VMware replikowanie tooAzure z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy tooenable tooAzure replikacji przy użyciu usługi Azure Site Recovery hello maszynach wirtualnych VMware"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 490782bbbfa3dd92c626d3985c75d771df53d566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-tooazure"></a>Krok 11: Włącz replikację tooAzure maszyn wirtualnych VMware


W tym artykule opisano, jak replikacja tooenable wirtualnych VMware lokalnej maszyny tooAzure przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Przed rozpoczęciem

- Maszyny wirtualne VMware muszą mieć hello [zainstalowanie składnika usługi Mobility](vmware-walkthrough-install-mobility.md). — Jeśli maszyna wirtualna jest gotowy do instalacji w trybie wypychania, serwer przetwarzania hello automatycznie instaluje usługi mobilności hello po włączeniu replikacji.
- Twoje konto użytkownika systemu Azure wymaga określonych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikacji tooAzure maszyny Wirtualnej
- Podczas dodawania lub modyfikowania maszyn wirtualnych, może upłynąć górę too15 minut lub dłużej dla efektu tootake zmiany i ich tooappear w portalu hello.
- Możesz sprawdzić czas hello ostatnio odnalezione dla maszyn wirtualnych w **serwery konfiguracji** > **ostatniego kontaktu w**.
- tooadd maszyn wirtualnych bez oczekiwania na powitania zaplanowanego odnajdywania, wyróżnij hello konfiguracji serwera (nie klikaj pozycji go) i kliknij przycisk **Odśwież**.



## <a name="exclude-disks-from-replication"></a>Wykluczanie dysków z replikacji

Domyślnie wszystkie dyski na komputerze są replikowane. Dyski można wykluczyć z replikacji. Na przykład nie ma dysków tooreplicate przy użyciu danych tymczasowych lub dane, które odświeżył każdym komputerze lub ponownym uruchomieniem aplikacji (na przykład pagefile.sys lub tempdb serwera SQL). [Dowiedz się więcej](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Replikowanie maszyn wirtualnych

Przed rozpoczęciem, Obejrzyj to szybki przegląd wideo

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**.
2. W **źródła**, wybierz pozycję powitania serwera konfiguracji.
3. W **komputera typu**, wybierz pozycję **maszyn wirtualnych**.
4. W **vCenter/vSphere Hypervisor**, wybierz hello vCenter server zarządzającego hostem vSphere hello, lub wybierz hello host.
5. Wybierz serwer przetwarzania hello. Jeśli nie utworzono żadnych serwerów dodatkowych procesów będzie powitania serwera konfiguracji. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. W **docelowego**, wybierz subskrypcję hello i hello grupy zasobów, w której ma zostać hello toocreate przejścia w tryb failover maszyn wirtualnych. Wybierz model wdrożenia hello, która ma toouse na platformie Azure (Zarządzanie zasobu lub classic) hello przejścia w tryb failover maszyn wirtualnych.


7. Wybierz konto magazynu Azure hello, które chcesz toouse do replikacji danych. Jeśli nie chcesz toouse konta, które zostały już skonfigurowane, można utworzyć nowy.

8. Wybierz hello Azure toowhich sieci i podsieci maszyn wirtualnych platformy Azure będą się łączyć, gdy są tworzone po pracy awaryjnej. Wybierz **Konfiguruj teraz dla wybranych maszyn**, tooapply hello sieci ustawienie tooall maszyn wybranych do ochrony. Wybierz **później skonfigurować** hello tooselect sieć platformy Azure dla poszczególnych komputerów. Jeśli nie chcesz toouse istniejącej sieci, można go utworzyć.

    ![Włączanie replikacji](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. W **maszyn wirtualnych** > **wybierz maszyny wirtualne**, kliknij i zaznacz każdy komputer ma tooreplicate. Możesz wybrać tylko te maszyny, dla których można włączyć replikację. Następnie kliknij przycisk **OK**.

    ![Włączanie replikacji](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. W **właściwości** > **skonfigurować właściwości**, wybierz pozycję hello konta, które będą używane przez hello procesu serwera tooautomatically Zainstaluj hello usługi mobilności na maszynie hello.
11. Domyślnie wszystkie dyski są replikowane. Kliknij przycisk **wszystkie dyski** i wyczyść wszystkie dyski, które nie mają tooreplicate. Następnie kliknij przycisk **OK**. Później można ustawić dodatkowe właściwości maszyny Wirtualnej.

    ![Włączanie replikacji](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, sprawdź, że hello poprawne wybrano zasady replikacji. Jeśli zmodyfikujesz zasady, zmiany zostaną zastosowane tooreplicating maszyny i toonew maszyny.
12. Włącz **spójności wielu maszyn wirtualnych** toogather maszyny do grupy replikacji, i określ nazwę grupy hello. Następnie kliknij przycisk **OK**. Należy pamiętać, że:

    * Komputery w grupach replikacji replikowane wspólnie i udostępnione punkty odzyskiwania spójna w razie awarii i spójności aplikacji podczas ich w tryb failover.
    * Zaleca się, że użytkownik zbiera maszyn wirtualnych i serwerów fizycznych, aby odzwierciedlały obciążeń. Włączenie spójności wielu maszyn wirtualnych może wpłynąć na wydajność obciążenia, a powinien być używany tylko przez hello są uruchomione maszyny tego samego obciążenia i wymagana jest spójność.

    ![Włączanie replikacji](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. Kliknij przycisk **włączyć replikację**. Możesz śledzić postępy hello **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**. Po hello **zakończenia ochrony** zadania działa hello maszyna jest gotowa do pracy awaryjnej.

## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 12: testować tryb failover](vmware-walkthrough-test-failover.md)
