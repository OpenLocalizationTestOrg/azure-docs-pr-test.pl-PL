---
title: "tryb failover aaaStorSimple, odzyskiwania po awarii dla urządzeń z serii 8000 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toofail za pośrednictwem sieci toohello urządzenia StorSimple tego samego urządzenia."
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a>Tryb failover urządzenia toosame urządzenia fizycznego StorSimple

## <a name="overview"></a>Omówienie

W tym samouczku opisano toofail wymagane kroki hello za pośrednictwem tooitself urządzenie fizyczne serii StorSimple 8000, w przypadku awarii. StorSimple używa hello urządzenia trybu failover funkcji toomigrate danych z urządzenia fizycznego źródła w hello urządzenie fizyczne tooanother centrum danych. wskazówki Hello w tym samouczku dotyczy urządzeń fizycznych serii tooStorSimple 8000 wersjami oprogramowania aktualizacji 3 lub nowszym.

toolearn więcej informacji na temat trybu failover urządzeń i jak jest używane toorecover po awarii, przejdź zbyt[trybu Failover i odzyskiwania po awarii dla urządzeń z serii StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail za pośrednictwem urządzenia fizycznego tooanother urządzenie fizyczne, przejdź zbyt[awaryjnie toohello takie same urządzenia fizycznego StorSimple](storsimple-8000-device-failover-physical-device.md). toofail za pośrednictwem tooa urządzenia fizycznego StorSimple urządzenia chmury StorSimple, przejdź zbyt[awaryjnie tooa urządzenia chmury StorSimple](storsimple-8000-device-failover-cloud-appliance.md).


## <a name="prerequisites"></a>Wymagania wstępne

- Upewnij się, należy przejrzeć hello zagadnienia dotyczące urządzenia trybu failover. Aby uzyskać więcej informacji, przejdź zbyt[typowe kwestie dotyczące pracy w trybie failover urządzenia](storsimple-8000-device-failover-disaster-recovery.md).


## <a name="steps-toofail-over-toohello-same-device"></a>Kroki toofail za pośrednictwem toohello tym samym urządzeniu

Wykonaj następujące kroki, jeśli wymagana jest toofail toohello hello tego samego urządzenia.

1. Twórz migawki chmurze wszystkie woluminy hello w urządzeniu. Aby uzyskać więcej informacji, przejdź zbyt[kopii zapasowych toocreate usługi StorSimple za pomocą Menedżera urządzeń](storsimple-8000-manage-backup-policies-u2.md).
2. Zresetowanie urządzenia toofactory domyślnych. Wykonaj hello szczegółowe instrukcje w [jak tooreset toofactory urządzenia StorSimple domyślne ustawienia](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Przejdź toohello usługi Menedżer urządzeń StorSimple, a następnie wybierz **urządzeń**. W hello **urządzeń** bloku hello starym urządzeniem powinny być widoczne jako **Offline**.

    ![Urządzenia źródłowego w trybie offline](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. Skonfiguruj urządzenie i zarejestruj go ponownie przy użyciu usługi Menedżer StorSimple urządzenia. Witaj nowo zarejestrowane urządzenia powinny być widoczne jako **gotowe tooset się**. Nazwa urządzenia Hello nowe urządzenie hello jest hello tak samo jak w starym urządzeniem hello ale dołączony liczb tooindicate urządzenia hello została domyślne toofactory resetowania i ponownie zarejestrowane.

    ![Nowo zarejestrowane urządzenia tooset gotowy górę](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. Dla hello nowe urządzenie wykonaj konfigurację urządzenia hello. Aby uzyskać więcej informacji, przejdź zbyt[krok 4: przeprowadzenie minimalnej konfiguracji urządzenia](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup). Na powitania **urządzeń** bloku hello stan urządzenia hello zmienia się zbyt**Online**.

   > [!IMPORTANT]
   > **Najpierw ukończyć powitalnych minimalnej konfiguracji lub programu DR może zakończyć się niepowodzeniem.**

    ![Nowo zarejestrowanym urządzeniem w trybie online](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. Wybierz urządzenie starego hello (stan w trybie offline), a następnie na pasku poleceń hello, kliknij **awaryjnie**. W hello **awaryjnie** bloku, wybierz urządzenie starego jako źródło hello i określ urządzenie docelowe hello hello nowo zarejestrowane urządzenia.

    ![Podsumowanie trybu failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    Aby uzyskać szczegółowe instrukcje, zobacz zbyt[awaryjnie urządzenie fizyczne tooanother](#fail-over-to-another-physical-device).

7. Tworzone jest zadanie przywracania urządzenia można monitorować z hello **zadania** bloku.

8. Po pomyślnym ukończeniu zadania hello dostępu hello nowe urządzenie i przejdź toohello **kontenery woluminów** bloku. Sprawdź, czy wszystkie kontenery woluminów hello ze starym urządzeniem hello zostały zmigrowane toohello nowe urządzenie.

   ![Kontenery woluminów migracji](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. Po zakończeniu pracy awaryjnej hello można zdezaktywować i usunąć hello starego urządzenie z portalu hello. Wybierz hello starego urządzenia (w trybie offline), kliknij prawym przyciskiem myszy, a następnie wybierz **Dezaktywuj**. Po dezaktywacji urządzenia hello hello stan urządzenia hello jest aktualizowany.

     ![Urządzenia źródłowego dezaktywowany](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. Wybierz hello dezaktywować urządzenie, kliknij prawym przyciskiem myszy, a następnie wybierz **usunąć**. Spowoduje to usunięcie urządzenia hello hello liście urządzeń.

    ![Urządzenia źródłowego usunięte](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a>Następne kroki

* Po wykonaniu trybu failover może być konieczne zbyt[dezaktywację lub usunięcie urządzenia StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Informacje dotyczące sposobu toouse hello Menedżera urządzeń StorSimple usługi znajduje się zbyt[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

