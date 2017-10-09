---
title: "tryb failover aaaStorSimple, urządzenie fizyczne serii StorSimple 8000 tooa odzyskiwania po awarii | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toofail za pośrednictwem StorSimple 8000 serii urządzenie fizyczne tooanother urządzenia fizycznego."
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
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a>Tryb failover urządzenia fizycznego StorSimple 8000 tooa serii

## <a name="overview"></a>Omówienie

W tym samouczku opisano toofail wymagane kroki hello za pośrednictwem StorSimple 8000 serii urządzenie fizyczne tooanother urządzenia fizycznego StorSimple w przypadku awarii. StorSimple używa hello urządzenia trybu failover funkcji toomigrate danych z urządzenia fizycznego źródła w hello urządzenie fizyczne tooanother centrum danych. wskazówki Hello w tym samouczku dotyczy urządzeń fizycznych serii tooStorSimple 8000 wersjami oprogramowania aktualizacji 3 lub nowszym.

toolearn więcej informacji na temat trybu failover urządzeń i jak jest używane toorecover po awarii, przejdź zbyt[trybu Failover i odzyskiwania po awarii dla urządzeń z serii StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail za pośrednictwem tooa urządzenia fizycznego StorSimple urządzenia chmury StorSimple, przejdź zbyt[awaryjnie tooa urządzenia chmury StorSimple](storsimple-8000-device-failover-cloud-appliance.md). toofail za pośrednictwem tooitself urządzenie fizyczne, przejdź zbyt[awaryjnie toohello takie same urządzenia fizycznego StorSimple](storsimple-8000-device-failover-same-device.md).


## <a name="prerequisites"></a>Wymagania wstępne

- Upewnij się, należy przejrzeć hello zagadnienia dotyczące urządzenia trybu failover. Aby uzyskać więcej informacji, przejdź zbyt[typowe kwestie dotyczące pracy w trybie failover urządzenia](storsimple-8000-device-failover-disaster-recovery.md).

- Muszą mieć urządzenia fizycznego StorSimple 8000 serii wdrożone w centrum danych hello. urządzenie Hello należy uruchomić aktualizacji 3 lub nowszej wersji oprogramowania. Aby uzyskać więcej informacji, przejdź zbyt[wdrażanie lokalnego urządzenia StorSimple](storsimple-8000-deployment-walkthrough-u2.md).


## <a name="steps-toofail-over-tooa-physical-device"></a>Kroki toofail przez urządzenie fizyczne tooa

Wykonaj następujące kroki toorestore hello urządzenia tooa docelowego urządzenia fizycznego.

1. Sprawdź, czy ten kontener woluminów hello żądane toofail za pośrednictwem skojarzone migawki w chmurze. Aby uzyskać więcej informacji, przejdź zbyt[kopii zapasowych toocreate usługi StorSimple za pomocą Menedżera urządzeń](storsimple-8000-manage-backup-policies-u2.md).
2. Przejdź tooyour Menedżera urządzeń StorSimple, a następnie kliknij przycisk **urządzeń**. W hello **urządzeń** bloku, przejdź toohello listy urządzeń połączonych z usługą.
    ![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)
3. Wybierz, a następnie kliknij przycisk urządzenia źródłowego. urządzenia źródłowego Hello ma hello kontenery woluminów, które mają toofail za pośrednictwem. Przejdź za**Ustawienia > kontenery woluminów**.
4. Wybierz kontener woluminów za pośrednictwem urządzenia tooanother chcesz toofail. Kliknij przycisk Lista kontenera woluminów hello hello toodisplay woluminów, w tym kontenerze. Wybierz wolumin, kliknij prawym przyciskiem myszy i kliknij przycisk **Przełącz do trybu Offline** tootake hello woluminu w trybie offline. Powtórz ten proces dla wszystkich woluminów hello w hello kontenera woluminów.
5. Hello Powtórz poprzedni krok dla wszystkich hello kontenery woluminów chcesz toofail za pośrednictwem tooanother urządzenia.
6. Przejdź wstecz toohello **urządzeń** bloku. Na pasku poleceń hello, kliknij **awaryjnie**.
    ![Kliknij opcję niepowodzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)
    
7. W hello **awaryjnie** blok, wykonaj następujące kroki hello:
   
   1. Kliknij przycisk **źródła**. Witaj kontenery woluminów z woluminami skojarzone z migawki w chmurze są wyświetlane. Tylko kontenery hello wyświetlane kwalifikują się do trybu failover. Na liście hello kontenery woluminów wybierz kontenery woluminów hello, którą chcesz toofail za pośrednictwem. **Tylko hello kontenery woluminów z migawkami skojarzonej chmury i woluminy w trybie offline są wyświetlane.**

       ![Wybierz źródło](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. Kliknij przycisk **docelowej**. Dla wybranego w poprzednim kroku hello kontenery woluminów hello wybierz urządzenie docelowe z listy rozwijanej hello dostępnych urządzeń. Tylko urządzenia hello, które mają wystarczającą pojemność tooaccommodate źródła kontenery woluminów są wyświetlane na liście hello.

        ![Wybierz element docelowy](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. Na koniec przejrzeć wszystkie ustawienia trybu failover hello w **Podsumowanie**. Po przejrzeniu hello ustawienia, wybierz hello wyboru wskazujące, że woluminy hello w kontenerach wybranego woluminu w trybie offline. Kliknij przycisk **OK**.

       ![Przejrzyj ustawienia trybu failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. StorSimple tworzy zadanie trybu failover. Kliknij przycisk hello powiadomień toomonitor hello trybu failover zadanie za pośrednictwem hello **zadania** bloku.

    Jeśli kontenera woluminów hello zakończonych niepowodzeniem na woluminach lokalnych, zostanie wyświetlony indywidualnych zadań przywracania dla każdego woluminu lokalnego (a nie dla woluminów warstwowych) w kontenerze hello. Przywracania zadania może potrwać jakiś czas toocomplete. Prawdopodobnie hello zadania trybu failover może zakończyć się wcześniej. Te woluminy mają lokalnych gwarancji, dopiero po zakończeniu zadania przywracania hello.

    ![Monitor, zadanie trybu failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. Po zakończeniu pracy awaryjnej hello Przejdź toohello **urządzeń** bloku.
   
   1. Wybierz urządzenie hello, które zostało użyte jako urządzenie docelowe hello hello procesu pracy awaryjnej.

       ![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. Przejdź toohello **kontenery woluminów** bloku. Wszystkie kontenery woluminów hello, wraz z woluminów hello ze starym urządzeniem hello, powinien być wyświetlany.

       ![Kontenery woluminów docelowego widoku](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a>Następne kroki

* Po wykonaniu trybu failover może być konieczne zbyt[dezaktywację lub usunięcie urządzenia StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Informacje dotyczące sposobu toouse hello Menedżera urządzeń StorSimple usługi znajduje się zbyt[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

