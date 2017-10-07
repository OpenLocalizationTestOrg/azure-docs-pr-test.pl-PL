---
title: samouczek tworzenia kopii zapasowej Azure StorSimple wirtualnego tablicy aaaMicrosoft | Dokumentacja firmy Microsoft
description: "Opisuje sposób udziały tooback się tablicy wirtualnego StorSimple i woluminów."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a>Tworzyć kopie zapasowe udziały lub woluminy na tablica wirtualnego StorSimple

## <a name="overview"></a>Omówienie

Witaj tablicy wirtualne StorSimple jest hybrydowe chmury magazynu lokalnego urządzenia wirtualnego skonfigurowanego jako serwer plików lub serwera iSCSI. Tablica wirtualnego Hello umożliwia toocreate użytkownika hello zaplanowanych, jak i ręczne tworzenie kopii zapasowych wszystkich hello udziały lub woluminy na urządzeniu hello. Gdy skonfigurowany jako serwer plików, również umożliwia odzyskiwanie na poziomie elementu. W tym samouczku opisano sposób planowania toocreate i ręcznego tworzenia kopii zapasowych i wykonać odzyskiwanie na poziomie elementu toorestore usuniętego pliku w sieci wirtualnej macierzy.

Ten samouczek dotyczy toohello StorSimple wirtualnego tablic tylko. Informacji o serii 8000, zbyt zobaczyć[tworzenia kopii zapasowej urządzenie 8000 series](storsimple-manage-backup-policies-u2.md)

## <a name="back-up-shares-and-volumes"></a>Wykonaj kopię zapasową woluminów i udziałów

Kopie zapasowe zapewnia ochronę w momencie, ułatwia odzyskiwanie i zminimalizować czas przywracania dla woluminów i udziałów. Można utworzyć kopię zapasową udziału lub wolumin w urządzeniu StorSimple na dwa sposoby: **zaplanowane** lub **ręcznego**. Każdej z metod hello jest omówiona w hello następujące sekcje.

## <a name="change-hello-backup-start-time"></a>Zmiana czasu rozpoczęcia tworzenia kopii zapasowej hello

> [!NOTE]
> W tej wersji zaplanowane kopie zapasowe są tworzone przez zasady domyślne, który jest uruchamiany codziennie o określonej godzinie i tworzy kopię zapasową wszystkich hello udziały lub woluminy na urządzeniu hello. Nie jest możliwe toocreate zasady niestandardowe dla zaplanowanych kopii zapasowych w tej chwili.


Tablica wirtualnego StorSimple ma domyślne zasady tworzenia kopii zapasowej, który rozpoczyna się o określonej godzinie dnia (22:30) i tworzy kopię zapasową wszystkich hello udziały lub woluminy na urządzeniu hello raz dziennie. Możesz zmienić czas hello, na które hello kopii zapasowej zostanie uruchomiony, ale częstotliwość hello i hello przechowywania (który określa hello liczbę kopii zapasowych tooretain) nie można zmienić. Podczas te kopie zapasowe całego urządzenia wirtualnego hello jest kopia zapasowa. To może potencjalnie wpłynąć na wydajność hello hello urządzenia i wpływać na powitania obciążeń wdrożonych na urządzeniu hello. Dlatego zaleca się zaplanować te kopie zapasowe dla poza godzinami szczytu.

 toochange hello domyślnego tworzenia kopii zapasowej godzina rozpoczęcia, wykonaj następujące kroki w hello hello [portalu Azure](https://portal.azure.com/).

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a>Witaj toochange godziny rozpoczęcia dla zasad tworzenia kopii zapasowej hello domyślne

1. Przejdź za**urządzeń**. zostanie wyświetlona lista Hello urządzeń zarejestrowanych przy użyciu usługi Menedżer StorSimple urządzenia. 
   
    ![Przejdź toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. Wybierz, a następnie kliknij urządzenie. Witaj **ustawienia** zostanie wyświetlony blok. Przejdź za**Zarządzaj > zasady tworzenia kopii zapasowej**.
   
    ![Wybierz urządzenie](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. W hello **zasady tworzenia kopii zapasowej** bloku hello domyślny czas rozpoczęcia jest 22:30. Można określić hello nową godzinę rozpoczęcia dla harmonogramu dziennego hello w strefie czasowej urządzenia.
   
    ![Przejdź toobackup zasad](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. Kliknij pozycję **Zapisz**.

### <a name="take-a-manual-backup"></a>Wykonaj kopię zapasową ręczne

Ponadto tooscheduled kopie zapasowe, można wykonać ręcznie (na żądanie) kopii zapasowej danych urządzenia w dowolnym momencie.

#### <a name="toocreate-a-manual-backup"></a>toocreate ręcznego tworzenia kopii zapasowej

1. Przejdź za**urządzeń**. Wybierz urządzenie, a następnie kliknij prawym przyciskiem myszy **...**  w prawej hello w hello zaznaczonego wiersza. Wybierz z menu kontekstowego hello **utworzenia kopii zapasowej**.
   
    ![Przejdź tootake kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. W hello **utworzenia kopii zapasowej** bloku, kliknij przycisk **utworzenia kopii zapasowej**. Zostanie utworzona kopia zapasowa, wszystkie udziały hello na powitania serwera plików lub wszystkie woluminy hello na serwerze iSCSI. 
   
    ![Uruchamianie tworzenia kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    Rozpoczęcia tworzenia kopii zapasowej na żądanie i zobacz, czy zadanie tworzenia kopii zapasowej została uruchomiona.
   
    ![Uruchamianie tworzenia kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    Po pomyślnym ukończeniu zadania hello zostanie wyświetlony ponownie. następnie uruchamia proces tworzenia kopii zapasowej Hello.
   
    ![Utworzono zadanie kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. postęp hello tootrack hello kopii zapasowych i Przeglądaj hello szczegóły zadania, kliknij powiadomienie hello. Powoduje to przejście zbyt **szczegóły zadania**.
   
     ![Szczegóły zadania kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. Po wykonaniu kopii zapasowej hello Przejdź zbyt**zarządzania > katalog kopii zapasowej**. Zobaczysz migawkę chmury dla wszystkich udziałów hello (lub woluminów) na urządzeniu.
   
    ![Zakończono tworzenie kopii zapasowej](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a>Wyświetlanie istniejących kopii zapasowych
tooview hello istniejących kopii zapasowych, wykonaj następujące kroki w portalu Azure hello hello.

#### <a name="tooview-existing-backups"></a>tooview istniejące kopie zapasowe

1. Przejdź za**urządzeń** bloku. Wybierz, a następnie kliknij urządzenie. W hello **ustawienia** bloku Przejdź zbyt**zarządzania > katalog kopii zapasowej**.
   
    ![Przejdź do katalogu toobackup](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. Określ powitania po toobe kryteria używane do filtrowania:
   
    - **Zakres czasu** — może być **ostatnich 1 godzina**, **ostatnich 24 godzin**, **ostatnie 7 dni**, **w ciągu ostatnich 30 dni**, **ciągu ostatniego roku**, i **Data niestandardowa**.
    
    - **Urządzenia** — wybierz z listy hello serwerów plików lub serwery iSCSI zarejestrowana przy użyciu usługi Menedżer StorSimple urządzenia.
   
    - **Zainicjowano** — może być automatycznie **zaplanowane** (przy użyciu zasad tworzenia kopii zapasowej) lub **ręcznie** zainicjujesz ().
   
    ![Kopie zapasowe filtru](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. Kliknij przycisk **Zastosuj**. Witaj wyfiltrowanej listy kopii zapasowych jest wyświetlana w hello **katalog kopii zapasowej** bloku. Uwaga tylko 100 elementów kopii zapasowej mogą być wyświetlane w danym momencie.
   
    ![Zaktualizowano katalogu kopii zapasowej](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [administrowanie tablica wirtualnego StorSimple](storsimple-ova-web-ui-admin.md).

