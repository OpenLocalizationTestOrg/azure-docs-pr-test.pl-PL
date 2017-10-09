---
title: zadania tworzenia kopii zapasowej Snapshot Manager aaaStorSimple | Dokumentacja firmy Microsoft
description: "Opisuje sposób toouse hello tooview przystawki MMC programu StorSimple Snapshot Manager i zarządzanie nimi zaplanowane, uruchomione i zakończonych zadań tworzenia kopii zapasowej."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a>Użyj tooview StorSimple Snapshot Manager i zarządzanie nimi zadania tworzenia kopii zapasowej

## <a name="overview"></a>Omówienie
Hello **zadania** węzła w hello **zakres** w okienku zostaną wyświetlone powitalne **zaplanowane**, **ostatnich 24 godzin**, i **systemem**kopii zapasowej zadania, które inicjowane interakcyjnego lub skonfigurowanymi zasadami. 

W tym samouczku opisano, jak używasz hello **zadania** węzła toodisplay informacji na temat zaplanowane, ostatnie i aktualnie uruchomionych zadań tworzenia kopii zapasowej. (Lista hello zadania i informacji znajduje się na powitania **wyniki** okienko.) Ponadto można kliknij prawym przyciskiem myszy wymienionych zadań i zobacz menu kontekstowego, który zawiera listę dostępnych akcji.

## <a name="view-scheduled-jobs"></a>Wyświetl zaplanowane zadania
Witaj użyj następującej procedury tooview zaplanowanych zadań tworzenia kopii zapasowej.

#### <a name="tooview-scheduled-jobs"></a>tooview zaplanowane zadania
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager. 
2. W hello **zakres** okienku rozwiń hello **zadania** węzeł, a następnie kliknij przycisk **zaplanowane**. Hello następujące informacje są wyświetlane w hello **wyniki** okienka:
   
   * **Nazwa** — Witaj nazwa hello zaplanowaną migawkę
   * **Uruchom** — hello Data i godzina hello następną zaplanowaną migawkę
   * **Ostatnie uruchomienie** — hello Data i godzina ostatniej zaplanowanej migawki hello
     
     > [!NOTE]
     > Jednorazowe tylko migawek, hello **następnego uruchomienia** i **ostatnie uruchomienie** będzie hello takie same.
     
     ![Zaplanowanych zadań kopii zapasowej](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. tooperform dodatkowe akcje w konkretnym zadaniu, kliknij prawym przyciskiem myszy nazwę zadania hello w hello **wyniki** okienka, a następnie zaznacz opcje menu hello.

## <a name="view-recent-jobs"></a>Wyświetl ostatnie zadania
Użyj powitania po tooview procedury tworzenia kopii zapasowej i przywracania zadania, które zostały ukończone w hello ostatnich 24 godzin.

#### <a name="tooview-recent-jobs"></a>tooview ostatnich zadań
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku rozwiń hello **zadania** węzeł, a następnie kliknij przycisk **ostatnich 24 godzin**. Witaj **wyniki** w okienku zostaną wyświetlone zadania tworzenia kopii zapasowej hello w ostatnich 24 godzinach (maksymalnie tooa 64 zadania). Hello następujące informacje są wyświetlane w hello **wyniki** okienko, w zależności od hello **widoku** możesz określić opcje:
   
   * **Nazwa** — Witaj nazwa hello zaplanowaną migawkę.
   * **Rozpoczęto** — hello Data i godzina rozpoczęcia hello migawki.
   * **Zatrzymano** — Data hello i migawki hello zakończono lub zostało przerwane.
   * **Upłynął** — Witaj ilość czasu między hello **uruchomiono** i **zatrzymane** razy.
   * **Stan** — Witaj stan hello niedawno ukończoną zadania. **Powodzenie** wskazuje hello kopii zapasowej został utworzony pomyślnie. **Nie powiodło się** wskazuje hello zadania nie zostało uruchomione pomyślnie.
   * **Informacje o** — Witaj Przyczyna niepowodzenia hello.
   * **Bajty przetwarzane (MB)** — Witaj ilości danych z grupy hello woluminu, który był przetwarzany (w MB). 
     
     ![Zadania, które były uruchamiane w hello w ostatnich 24 godzinach](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. tooperform dodatkowe akcje w konkretnym zadaniu, kliknij prawym przyciskiem myszy nazwę zadania hello w hello **wyniki** okienka, a następnie zaznacz opcje menu hello.
   
    ![Usuwanie zadania](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a>Wyświetl uruchomione zadania
Witaj użyj następującej procedury tooview zadania, które są aktualnie uruchomione.

#### <a name="tooview-currently-running-jobs"></a>tooview aktualnie uruchomionych zadań
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku rozwiń hello **zadania** węzeł, a następnie kliknij przycisk **systemem**. W zależności od hello **widoku** opcje określisz, hello następujących informacji jest wyświetlana w hello **wyniki** okienka:
   
   * **Nazwa** — Witaj nazwa hello zaplanowaną migawkę.
   * **Rozpoczęto** — hello Data i godzina rozpoczęcia hello migawki.
   * **Punkt kontrolny** — Witaj bieżącej akcji hello kopii zapasowej.
   * **Stan** — Witaj procentu ukończenia.
   * **Upłynął** — Witaj ilość czasu, jaki upłynął od chwili rozpoczęcia tworzenia kopii zapasowej hello. 
   * **Średnia przepływność (MB)** — współczynnik łączna liczba bajtów danych przetwarzanych toothat łączny czas poświęcony na przetwarzanie (MB).
   * **Bajty przetwarzane (MB)** — łączna liczba bajtów dane przetworzone (w MB).
   * **Bajty zapisane (MB)** — łączna liczba bajtów danych (w MB). Ona zawiera hello danych, a także hello metadanych i dlatego zazwyczaj większe niż hello przetwarzane bajtów.
     
     ![Obecnie uruchomionych zadań](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. tooperform dodatkowe akcje w konkretnym zadaniu, kliknij prawym przyciskiem myszy nazwę zadania hello w hello **wyniki** okienka, a następnie zaznacz opcje menu hello.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[użyć tooadminister StorSimple Snapshot Manager rozwiązania StorSimple](storsimple-snapshot-manager-admin.md).
* Dowiedz się, jak za[używać katalogu kopii zapasowej hello toomanage StorSimple Snapshot Manager](storsimple-snapshot-manager-manage-backup-catalog.md).

