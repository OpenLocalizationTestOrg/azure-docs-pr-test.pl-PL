---
title: "aaaStorSimple przejścia w tryb failover tooa odzyskiwania po awarii urządzenia chmury StorSimple | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toofail za pośrednictwem sieci tooa urządzenie fizyczne serii StorSimple 8000 chmury urządzenia."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a>Tryb failover tooyour urządzenia chmury StorSimple

## <a name="overview"></a>Omówienie

W tym samouczku opisano toofail wymagane kroki hello za pośrednictwem tooa urządzenia fizycznego StorSimple 8000 serii StorSimple urządzenia chmury, w przypadku awarii. StorSimple używa hello urządzenia trybu failover funkcji toomigrate danych z urządzenia fizycznego źródła w hello datacenter tooa urządzenia chmury działających na platformie Azure. wskazówki Hello w tym samouczku dotyczy urządzeń fizycznych serii tooStorSimple 8000 oraz chmury urządzenia z wersjami oprogramowania aktualizacji, 3 lub nowszym.

toolearn więcej informacji na temat trybu failover urządzeń i jak jest używane toorecover po awarii, przejdź zbyt[trybu Failover i odzyskiwania po awarii dla urządzeń z serii StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail przez urządzenie fizyczne tooanother urządzenia fizycznego StorSimple Przejdź zbyt[awaryjnie urządzenia fizycznego StorSimple tooa](storsimple-8000-device-failover-physical-device.md). toofail za pośrednictwem tooitself urządzeń, przejdź zbyt[awaryjnie toohello takie same urządzenia fizycznego StorSimple](storsimple-8000-device-failover-same-device.md).

## <a name="prerequisites"></a>Wymagania wstępne

- Upewnij się, należy przejrzeć hello zagadnienia dotyczące urządzenia trybu failover. Aby uzyskać więcej informacji, przejdź zbyt[typowe kwestie dotyczące pracy w trybie failover urządzenia](storsimple-8000-device-failover-disaster-recovery.md).

- Muszą mieć urządzenia chmury StorSimple utworzeniu i skonfigurowaniu przed uruchomieniem tej procedury. Jeśli uruchomienia aktualizacji oprogramowania w wersji 3 lub później, należy rozważyć użycie urządzenia 8020 chmury dla hello odzyskiwania po awarii. Witaj model 8020 ma 64 TB i używa magazyn w warstwie Premium. Aby uzyskać więcej informacji, przejdź zbyt[wdrażanie i zarządzanie nimi urządzenia chmury StorSimple](storsimple-8000-cloud-appliance-u2.md).

## <a name="steps-toofail-over-tooa-cloud-appliance"></a>Kroki toofail za pośrednictwem urządzenia do chmury tooa

Wykonaj następujące kroki toorestore hello urządzenia tooa docelowego urządzenia chmury StorSimple hello.

1.  Sprawdź, czy ten kontener woluminów hello żądane toofail za pośrednictwem skojarzone migawki w chmurze. Aby uzyskać więcej informacji, przejdź zbyt[kopii zapasowych toocreate usługi StorSimple za pomocą Menedżera urządzeń](storsimple-8000-manage-backup-policies-u2.md).
2. Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **urządzeń**. W hello **urządzeń** bloku, przejdź toohello listy urządzeń połączonych z usługą.
    ![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)
3. Wybierz, a następnie kliknij przycisk urządzenia źródłowego. urządzenia źródłowego Hello ma hello kontenery woluminów, które mają toofail za pośrednictwem. Przejdź za**Ustawienia > kontenery woluminów**.

    ![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. Wybierz kontener woluminów za pośrednictwem urządzenia tooanother chcesz toofail. Kliknij przycisk Lista kontenera woluminów hello hello toodisplay woluminów, w tym kontenerze. Wybierz wolumin, kliknij prawym przyciskiem myszy i kliknij przycisk **Przełącz do trybu Offline** tootake hello woluminu w trybie offline.

    ![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. Powtórz ten proces dla wszystkich woluminów hello w hello kontenera woluminów.

     ![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. Hello Powtórz poprzedni krok dla wszystkich hello kontenery woluminów chcesz toofail za pośrednictwem tooanother urządzenia.

7. Przejdź wstecz toohello **urządzeń** bloku. Na pasku poleceń hello, kliknij **awaryjnie**.

    ![Kliknij opcję niepowodzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. W hello **awaryjnie** blok, wykonaj następujące kroki hello:
   
    1. Kliknij przycisk **źródła**. Wybierz toofail kontenery woluminów hello za pośrednictwem. **Tylko hello kontenery woluminów z migawkami skojarzonej chmury i woluminy w trybie offline są wyświetlane.**
        ![Wybierz źródło](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)
    2. Kliknij przycisk **docelowej**. Wybierz urządzenia chmury docelowy z listy rozwijanej hello dostępnych urządzeń. **Tylko urządzenia hello, które mają wystarczającą pojemność tooaccommodate źródła kontenery woluminów są wyświetlane na liście hello.**

        ![Wybierz element docelowy](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. Przejrzyj ustawienia trybu failover hello w obszarze **Podsumowanie** i wybierz hello wyboru wskazujące, że woluminy hello w kontenerach wybranego woluminu w trybie offline. 

        ![Przejrzyj ustawienia trybu failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. Tworzone jest zadanie trybu failover. tryb failover hello toomonitor zadania, kliknij przycisk hello powiadomienie o zadaniu.

    ![Monitor, zadanie trybu failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. Po zakończeniu pracy awaryjnej hello, przejdź wstecz toohello **urządzeń** bloku.

    1. Wybierz urządzenie hello, używany jako docelowy hello hello pracy awaryjnej.

       ![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. Kliknij przycisk **kontenery woluminów**. Wszystkie kontenery woluminów hello, wraz z woluminów hello ze starym urządzeniem hello, powinien być wyświetlany.

       Kontener woluminów hello, który przejścia w tryb failover jest przypięty lokalnie woluminów, woluminy są nie powiodła się za pośrednictwem jako woluminy warstwowe. Woluminów przypiętych lokalnie nie są obsługiwane na urządzeniu z StorSimple w chmurze.

       ![Kontenery woluminów docelowego widoku](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a>Następne kroki

* Po wykonaniu trybu failover może być konieczne zbyt[dezaktywację lub usunięcie urządzenia StorSimple](storsimple-8000-deactivate-and-delete-device.md).

* Informacje dotyczące sposobu toouse hello Menedżera urządzeń StorSimple usługi znajduje się zbyt[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

