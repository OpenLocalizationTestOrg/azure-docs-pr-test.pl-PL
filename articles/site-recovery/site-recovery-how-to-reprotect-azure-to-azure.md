---
title: "tooReprotect aaaHow od przejścia w tryb failover maszyn wirtualnych platformy Azure wstecz tooprimary region platformy Azure | Dokumentacja firmy Microsoft"
description: "Po pracy w trybie failover maszyny wirtualne z jednego tooanother region platformy Azure można użyć usługi Azure Site Recovery tooprotect hello maszyny w kierunku odwrotnym. Dowiedz się więcej czynności hello jak toodo ponownej ochrony przed ponownie trybu failover."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 991c7ee8f489e84c250230bf73f3e99015c5f051
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-tooprimary-region"></a>Ponownej ochrony od przejścia w tryb failover Azure regionu tooprimary Wstecz



>[!NOTE]
>
> Replikacja lokacji odzyskiwania maszyn wirtualnych platformy Azure jest obecnie w przeglądzie.


## <a name="overview"></a>Omówienie
Gdy użytkownik [pracy awaryjnej](site-recovery-failover.md) hello maszyn wirtualnych z jednego regionu Azure tooanother hello maszyny wirtualne są w stanie niechronionym. Jeśli chcesz toobring ich toohello regionu podstawowego, należy toofirst zabezpieczeniu hello maszyn wirtualnych, a następnie trybu failover. Nie ma żadnej różnicy między jak failover w jednym kierunku lub innych. Podobnie po Włączanie ochrony maszyn wirtualnych hello, nie ma żadnej różnicy między trybu failover po ponownej ochrony hello lub post powrotu po awarii.
przepływy pracy hello tooexplain ponownej ochrony i tooavoid pomyłek, użyjemy lokacji głównej hello hello chronionych maszyn jako regionu Azja Wschodnia, a lokacja odzyskiwania hello hello maszyn jako regionu Azja Wschodnia południowo. Podczas pracy w trybie failover będzie trybu failover hello maszyn wirtualnych toohello południowo Azja Wschodnia regionu. Przed możesz powrotu po awarii należy maszyn wirtualnych hello tooreprotect z tyłu tooEast południowo Azja Wschodnia Azja. W tym artykule opisano kroki hello na temat tooreprotect.

> [!WARNING]
> Jeśli masz [ukończone migracji](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)przeniesionego hello maszyny wirtualnej tooanother zasobów grupy lub został usunięty hello maszyny wirtualnej platformy Azure, nie powrotu po awarii po.

Po zakończeniu ponownej ochrony i replikowania hello chronionych maszyn wirtualnych, można zainicjować trybu failover na powitania toobring maszyn wirtualnych ich kopii tooEast regionu Azja.

Opublikuj komentarze lub pytania na końcu hello tym artykułem lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Wymagania wstępne
1. maszyny wirtualne Hello powinien zostały przekazane.
2. lokacji docelowej Hello — w takim przypadku regionu Azja Wschodnia Azure hello powinny być dostępne i powinno być możliwe tooaccess/utworzyć nowe zasoby, w tym regionie.

## <a name="steps-tooreprotect"></a>Kroki tooreprotect

Poniżej są hello maszynę wirtualną przy użyciu wartości domyślnych hello tooreprotect czynności.

1. W **magazynu** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, która jest Failover, a następnie wybierz **ponownego włączenia ochrony**. Możesz również kliknąć hello komputera i wybierz pozycję **ponownego włączenia ochrony** z hello przyciski poleceń.

![Kliknij prawym przyciskiem myszy tooreprotect](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. W bloku hello zauważyć kierunku hello ochrony, **Azja południowo-wschodnia, Azja tooEast**, jest już wybrana.

![Włącz ponownie ochronę bloku](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. Przejrzyj hello **zasobów grupy, sieci, magazynu i dostępności zestawy** informacje i kliknij przycisk OK. Jeśli istnieją wszystkie zasoby oznaczone (nowy), będzie można utworzyć jako część hello Włącz ponownie ochronę.

To będzie wyzwalacz zadania Wznów zadanie, które najpierw będzie obsługiwał lokacji docelowej hello (SEA w tym przypadku) z hello najnowsze dane, a po który zakończeniu zreplikuje delty hello przed trybu failover można z powrotem tooSoutheast Azja.

### <a name="reprotect-customization"></a>Włącz ponownie ochronę dostosowania
Jeśli chcesz, aby toochoose hello wyodrębniania sieci konta lub hello magazynu podczas Włącz ponownie ochronę, możesz zrobić, za pomocą hello Dostosowywanie opcji podanego w bloku ponownej ochrony hello.

![Dostosowywanie opcji](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

Można dostosować hello następujące właściwości he docelowej maszyny wirtualnej podczas ponownej ochrony.

![Dostosowywanie bloku](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|Właściwość |Uwagi  |
|---------|---------|
|Docelowa grupa zasobów     | Można wybrać toochange hello docelowa grupa zasobów w którym zostanie utworzona th maszyny wirtualnej. W ramach hello ponownej ochrony hello docelowa maszyna wirtualna zostanie usunięta, dlatego można wybrać nową grupę zasobów, w którym można utworzyć hello wirtualna post w tryb failover         |
|Docelowy sieci wirtualnej     | Nie można zmienić sieci podczas ponownej ochrony hello. Witaj toochange sieci, ponów hello mapowania sieci.         |
|Magazyn docelowy     | Można zmienić konta magazynu hello maszyny wirtualnej hello toowhich zostanie utworzony po pracy awaryjnej.         |
|Pamięć podręczna     | Można określić konto magazynu pamięci podręcznej, która będzie używana podczas replikacji. Przejście z ustawieniami domyślnymi hello nowe konto magazynu pamięci podręcznej zostanie utworzony, jeśli jeszcze nie istnieje.         |
|Zestaw dostępności     |Jeśli maszyna wirtualna hello w Azja Wschodnia jest częścią zestawu dostępności, można wybrać zbiór dostępności dla docelowej maszyny wirtualnej hello w Azji Południowo-Wschodnia. Ustawienia domyślne znajdzie hello istniejącego zestawu dostępności SEA i spróbuj toouse go. W trakcie dostosowywania realizowanego można określić zupełnie nowy zestaw AV.         |


### <a name="what-happens-during-reprotect"></a>Co się dzieje podczas ponownej ochrony?

Podobnie jak po hello najpierw włączyć ochronę, są następujące artefaktów hello, tworzonych użycie wartości domyślnych hello.
1. Konto magazynu pamięci podręcznej pobiera utworzony w hello regionu Azja Wschodnia.
2. Jeśli hello docelowe konto magazynu (hello oryginalnego konta magazynu hello Azja południowo-wschodnia maszyny Wirtualnej) nie istnieje, zostanie utworzony nowy. Nazwa Hello jest hello Azja Wschodnia maszyny wirtualnej na konto magazynu z "asr" sufiksem.
3. Jeśli zestaw docelowy AV hello nie istnieje, a domyślne hello wykrywa, że potrzebuje toocreate nowe AV ustawiona, zostanie utworzony jako część hello Wznów zadanie. Jeśli dostosowano hello Włącz ponownie ochronę, a następnie zestaw AV wybrane hello jest używany.
4.

Oto Hello hello listę kroków, które się zdarzyć, gdy użytkownik zainicjuje zadanie ponownej ochrony. Jest to w stronie docelowej wielkość hello hello istnieje maszyny wirtualnej.

1. Witaj wymagane artefaktów są tworzone w ramach ponownej ochrony. Jeśli już istnieją, a następnie są używane ponownie.
2. maszyny wirtualnej (Azja południowo-wschodnia) po stronie docelowej Hello jest najpierw wyłączony, jeśli została uruchomiona.
3. Hello docelowej po stronie dysku maszyny wirtualnej jest kopiowana za pomocą usługi Azure Site Recovery do kontenera jako inicjatora obiektu blob.
4. Maszyna wirtualna po stronie docelowej Hello jest usuwany.
5. Obiekt blob inicjatora Hello jest używany przez tooreplicate maszyny wirtualnej (Azja Wschodnia) po stronie źródła hello bieżącej. Dzięki temu, że są replikowane tylko różnice.
6. istotne zmiany Hello między dysku źródłowego hello i obiektów blob inicjatora hello są synchronizowane. Może to zająć kilka toocomplete czas.
7. Po hello Wznów zadanie zostało ukończone, replikacja różnicowa hello rozpoczyna się, który tworzy punkt odzyskiwania zgodnie z zasadami hello.

> [!NOTE]
> Nie można włączyć ochrony na poziomie planu odzyskiwania. Może być tylko Wznów w na poziomie maszyny Wirtualnej.

Po Wznów hello powiedzie się, maszyny wirtualnej hello przejdzie w stan chronionych.

## <a name="next-steps"></a>Następne kroki

Po wprowadzeniu chronionych stan maszyny wirtualnej hello można zainicjować trybu failover. trybu failover Hello Zamknij maszynę wirtualną hello w regionie Azure Azja Wschodnia i następnie utworzy i rozruchu maszyny wirtualnej regionu Azja południowo-wschodnia hello. Dlatego jest mała przestojów w przypadku aplikacji hello. Tak wybierz hello czasu dla trybu failover, gdy aplikacja może tolerować przestoju. Zaleca się przetestowanie trybu failover hello maszyny wirtualnej toomake się, że jej jest powtarzający się prawidłowo, przed rozpoczęciem pracy awaryjnej.

-   [Kroki tooinitiate testowanie trybu failover maszyny wirtualnej hello](site-recovery-test-failover-to-azure.md)

-   [Kroki tooinitiate pracy w trybie failover maszyny wirtualnej hello](site-recovery-failover.md)
