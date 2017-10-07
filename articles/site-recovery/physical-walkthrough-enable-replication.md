---
title: "Replikacja serwerów fizycznych replikowanie tooAzure z usługą Azure Site Recovery aaaEnable | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello tooenable tooAzure replikacji są wymagane dla serwerów fizycznych za pomocą usługi Azure Site Recovery hello"
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
ms.openlocfilehash: dde4b1463023d2ccefa498f72bb51e57d60ac0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-physical-servers-tooazure"></a>Krok 10: Włącz replikację tooAzure serwerów fizycznych


W tym artykule opisano sposób replikacja tooenable lokalnego systemu Windows i Linux tooAzure serwerów fizycznych, przy użyciu hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Przed rozpoczęciem

- Serwery muszą mieć hello [zainstalowanie składnika usługi Mobility](physical-walkthrough-install-mobility.md).
- Maszyna wirtualna jest gotowy do instalacji w trybie wypychania, serwer przetwarzania hello automatycznie instaluje usługi mobilności hello po włączeniu replikacji.
- Po włączeniu maszyny do replikacji konta użytkownika platformy Azure wymaga określonych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooensure którego stanie toouse magazynu Azure, a Tworzenie maszyn wirtualnych platformy Azure.
- Podczas dodawania lub modyfikowania adresów IP dla serwerów, może upłynąć górę too15 minut lub dłużej dla efektu tootake zmiany i ich tooappear w portalu hello.


## <a name="exclude-disks-from-replication"></a>Wykluczanie dysków z replikacji

Domyślnie wszystkie dyski na komputerze są replikowane. Dyski można wykluczyć z replikacji. Na przykład nie ma dysków tooreplicate przy użyciu danych tymczasowych lub dane, które odświeżył każdym komputerze lub ponownym uruchomieniem aplikacji (na przykład pagefile.sys lub tempdb serwera SQL). [Dowiedz się więcej](site-recovery-exclude-disk.md)

## <a name="replicate-servers"></a>Replikacja serwerów

1. Kliknij kolejno pozycje **Krok 2. Replikowanie aplikacji** > **Źródło**.
2. W **źródła**, wybierz pozycję powitania serwera konfiguracji.
3. W **komputera typu**, wybierz pozycję **maszyn fizycznych**.
4. Wybierz serwer przetwarzania hello. Jeśli nie utworzono żadnych serwerów dodatkowych procesów będzie powitania serwera konfiguracji. Następnie kliknij przycisk **OK**.
5. W **docelowego**, wybierz subskrypcję hello i hello grupy zasobów, w której ma zostać hello toocreate przejścia w tryb failover maszyn wirtualnych. Wybierz model wdrożenia hello, która ma toouse na platformie Azure (Zarządzanie zasobu lub classic) hello przejścia w tryb failover maszyn wirtualnych.
6. Wybierz konto magazynu Azure hello, które chcesz toouse do replikacji danych. Jeśli nie chcesz toouse konta, które zostały już skonfigurowane, można utworzyć nowy.
7. Wybierz hello **sieć platformy Azure** i **podsieci** połączyć toowhich maszynach wirtualnych Azure po pracy awaryjnej. Wybierz **Konfiguruj teraz dla wybranych maszyn** tooapply hello sieci ustawienie tooall maszyn wybranych do ochrony. Wybierz **później skonfigurować** hello tooselect sieć platformy Azure dla poszczególnych komputerów. Jeśli nie chcesz toouse istniejącej sieci, można go utworzyć.

    ![Włączanie replikacji](./media/physical-walkthrough-enable-replication/targetsettings.png)

8. W **maszyn fizycznych**, kliknij przycisk **+ komputera fizycznego** , a następnie wprowadź hello **nazwa** i **adres IP**. Wybierz system operacyjny hello maszyny hello ma tooreplicate. Trwa kilka minut, aż maszyny są odnajdywane i wyświetlane na liście hello.
9. W **właściwości** > **skonfigurować właściwości**, wybierz pozycję hello konta, które będą używane przez hello procesu serwera tooautomatically Zainstaluj hello usługi mobilności na maszynie hello.
10. Domyślnie wszystkie dyski są replikowane. Kliknij przycisk **wszystkie dyski** i wyczyść wszystkie dyski, które nie mają tooreplicate. Następnie kliknij przycisk **OK**. Później można ustawić dodatkowe właściwości maszyny Wirtualnej.

    ![Włączanie replikacji](./media/physical-walkthrough-enable-replication/enable-replication6.png)
11. W **ustawienia replikacji** > **Konfigurowanie ustawień replikacji**, sprawdź, że hello poprawne wybrano zasady replikacji. Jeśli zmodyfikujesz zasady, zmiany zostaną zastosowane tooreplicating maszyny i toonew maszyny.
12. Włącz **spójności wielu maszyn wirtualnych** toogather maszyny do grupy replikacji, i określ nazwę grupy hello. Następnie kliknij przycisk **OK**. Należy pamiętać, że:

    * Komputery w grupach replikacji replikowane wspólnie i udostępnione punkty odzyskiwania spójna w razie awarii i spójności aplikacji podczas ich w tryb failover.
    * Zaleca się, że użytkownik zbiera serwerów fizycznych, aby odzwierciedlały obciążeń. Włączenie spójności wielu maszyn wirtualnych może wpłynąć na wydajność obciążenia, a powinien być używany tylko przez hello są uruchomione maszyny tego samego obciążenia i wymagana jest spójność.

13. Kliknij przycisk **włączyć replikację**. Możesz śledzić postępy hello **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**. Po hello **zakończenia ochrony** zadania działa hello maszyna jest gotowa do pracy awaryjnej.

## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 11: testować tryb failover](physical-walkthrough-test-failover.md)
