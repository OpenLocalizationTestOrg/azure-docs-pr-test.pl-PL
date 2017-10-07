---
title: katalog kopii zapasowej Snapshot Manager aaaStorSimple | Dokumentacja firmy Microsoft
description: "Opisuje sposób toouse hello tooview przystawki MMC programu StorSimple Snapshot Manager i zarządzanie nimi hello katalogu kopii zapasowej."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6abdbfd2-22ce-45a5-aa15-38fae4c8f4ec
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 173410095bcec7948d780d7fc258d2e3670bde8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toomanage-hello-backup-catalog"></a>Katalog kopii zapasowej hello toomanage Użyj StorSimple Snapshot Manager

## <a name="overview"></a>Omówienie
podstawową funkcją Hello StorSimple Snapshot Manager jest tooallow kopiuje możesz toocreate spójnych z aplikacją kopii zapasowych woluminów StorSimple w postaci hello migawek. Migawki są następnie wyświetlane w pliku XML o nazwie *katalogu kopii zapasowej*. katalog kopii zapasowej Hello organizuje migawek woluminu grupy, a następnie według migawka lokalna i migawka w chmurze.

W tym samouczku opisano, jak używasz hello **katalog kopii zapasowej** hello toocomplete węzła następujące zadania:

* Przywracanie woluminu
* Klonowanie woluminu lub grupy woluminu
* Usuwanie kopii zapasowej
* Odzyskiwanie pliku
* Przywracanie bazy danych programu Storsimple Snapshot Manager hello

Można przeglądać katalog kopii zapasowej hello rozwijając hello **katalogu kopii zapasowej** węzła w hello **zakres** okienka, a następnie rozszerzanie hello woluminu grupy.

* Kliknięcie nazwy grupy woluminu hello hello **wyniki** w okienku zostaną wyświetlone hello liczbę migawek lokalnych i dostępnych dla grupy woluminu hello migawki w chmurze. 
* Jeśli klikniesz przycisk **migawka lokalna** lub **migawka w chmurze**, hello **wyniki** w okienku zostaną wyświetlone następujące informacje o każdej kopii zapasowej migawki hello (w zależności od Twojego **Widoku** ustawienia):
  
  * **Nazwa** — Witaj czasu hello migawki.
  * **Typ** — czy jest to migawka lokalna i migawka w chmurze.
  * **Właściciel** — Witaj właściciela zawartości. 
  * **Dostępne** — czy hello migawka jest obecnie dostępna. **Wartość true,** wskazuje tej migawki hello jest dostępna i można go przywrócić; **False** wskazuje tej migawki hello nie jest już dostępny. 
  * **Zaimportowane** — czy zaimportowano hello kopii zapasowej. **Wartość true,** wskazuje kopii zapasowej hello została zaimportowana z hello Menedżera urządzeń StorSimple, usługa na urządzeniu hello czasu hello została skonfigurowana w StorSimple Snapshot Manager; **False** wskazuje, że nie został zaimportowany, ale został utworzony przez StorSimple Snapshot Manager. (Można łatwo zidentyfikować grupy woluminu zaimportowany, ponieważ jest dodawany sufiks identyfikujący urządzenie hello, z której zaimportowano hello woluminu grupy.)
    
    ![Katalog kopii zapasowej](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Backup_catalog.png)
* Po rozwinięciu **migawka lokalna** lub **migawka w chmurze**, a następnie kliknij przycisk nazwy poszczególnych migawki hello **wyniki** w okienku zostaną wyświetlone następujące informacje o hello hello Migawka, wybrane:
  
  * **Nazwa** — Witaj określone przez literę dysku woluminu. 
  * **Lokalna nazwa** — Nazwa lokalna hello hello dysku (jeśli jest dostępna). 
  * **Urządzenie** — Witaj nazwa hello urządzenia, na którym hello znajduje się wolumin. 
  * **Dostępne** — czy hello migawka jest obecnie dostępna. **Wartość true,** wskazuje tej migawki hello jest dostępna i można go przywrócić; **False** wskazuje tej migawki hello nie jest już dostępny. 

## <a name="restore-a-volume"></a>Przywracanie woluminu
Użyj hello następujące procedury toorestore woluminu z kopii zapasowej.

#### <a name="prerequisites"></a>Wymagania wstępne
Jeśli nie zostało to jeszcze zrobione, Utwórz wolumin i grupy woluminu, a następnie usuń hello woluminu. Domyślnie StorSimple Snapshot Manager kopię zapasową woluminu przed zezwalające toobe usunięte. W ten sposób można zapobiec utracie danych, jeśli hello wolumin zostanie przypadkowo usunięty lub dane hello muszą toobe odzyskać w dowolnej przyczyny. 

StorSimple Snapshot Manager Wyświetla hello następującą wiadomości, podczas tworzenia kopii zapasowej ostrożności hello.

![Komunikat automatyczne migawki](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Automatic_snap.png) 

> [!IMPORTANT]
> Nie można usunąć woluminu, który jest częścią grupy woluminu. Opcja Usuń Hello jest niedostępna. <br>
> 
> 

#### <a name="toorestore-a-volume"></a>toorestore woluminu
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager. 
2. W hello **zakres** okienku rozwiń hello **katalog kopii zapasowej** węzła, rozwiń grupę woluminu, a następnie kliknij przycisk **migawki lokalne** lub **migawki w chmurze**. Zostanie wyświetlona lista migawek kopii zapasowych w hello **wyniki** okienka.
3. Kopia zapasowa hello Znajdź mają toorestore, kliknij prawym przyciskiem myszy, a następnie kliknij **przywrócić**.
   
    ![Przywracanie kopii zapasowej katalogu](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_BU_catalog.png) 
4. Na stronie potwierdzenia hello, przejrzyj szczegóły hello, wpisz **Potwierdź**, a następnie kliknij przycisk **OK**. StorSimple Snapshot Manager używa hello kopii zapasowej toorestore hello woluminu.
   
    ![Potwierdzenie przywracania](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_volume_msg.png) 
5. Akcja przywracania hello można monitorować podczas jego wykonywania. W hello **zakres** okienku rozwiń hello **zadania** węzeł, a następnie kliknij przycisk **systemem**. Szczegóły zadania Hello są wyświetlane w hello **wyniki** okienka. Po zakończeniu zadania przywracania hello szczegóły zadania hello są przekazanych toohello **ostatnich 24 godzin** listy.

## <a name="clone-a-volume-or-volume-group"></a>Klonowanie woluminu lub grupy woluminu
Użyj hello następujące procedury toocreate duplikat (klonowania) woluminu lub grupy woluminu.

#### <a name="tooclone-a-volume-or-volume-group"></a>tooclone woluminu lub grupy woluminu
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku rozwiń hello **katalog kopii zapasowej** węzła, rozwiń grupę woluminu, a następnie kliknij przycisk **migawki w chmurze**. Zostanie wyświetlona lista kopii zapasowych w hello **wyniki** okienka.
3. Znajdź hello woluminu lub grupy woluminu tooclone, kliknij prawym przyciskiem myszy wolumin hello lub nazwa grupy woluminu i kliknij przycisk **klonowania**. Witaj **migawka w chmurze klonowania** zostanie wyświetlone okno dialogowe.
   
    ![Klonowanie migawka w chmurze](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Zakończenie hello **migawka w chmurze klonowania** okno dialogowe w następujący sposób: 
   
   1. W hello **nazwa** polu tekstowym, wpisz nazwę hello sklonować woluminu. Ta nazwa będzie wyświetlana w hello **woluminów** węzła. 
   2. (Opcjonalnie) zaznacz **dysku**, a następnie wybierz z listy rozwijanej hello literę dysku.
   3. (Opcjonalnie) zaznacz **folderu NTFS**i wpisz ścieżkę folderu, lub kliknij przycisk Przeglądaj i wybierz lokalizację folderu hello. 
   4. Kliknij przycisk **Utwórz**.
5. Po zakończeniu operacji hello proces klonowania, należy zainicjować hello sklonować woluminu. Uruchom Menedżera serwera, a następnie uruchom Zarządzanie dyskami. Aby uzyskać szczegółowe instrukcje, zobacz [instalowania woluminów](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Po zainicjowaniu, hello woluminu, będą wyświetlane w hello **woluminów** węzła w hello **zakres** okienka. Jeśli nie ma woluminu hello na liście, Odśwież listę hello woluminów (powitania kliknij prawym przyciskiem myszy **woluminów** węzeł, a następnie kliknij przycisk **Odśwież**).

## <a name="delete-a-backup"></a>Usuwanie kopii zapasowej
Użyj hello następujące procedury toodelete migawki z hello katalogu kopii zapasowej. 

> [!NOTE]
> Usunięcie migawki spowoduje usunięcie hello kopię zapasową danych skojarzonych z hello migawki. Jednak proces hello wyczyszczenie danych z chmury hello może potrwać pewien czas.<br>


#### <a name="toodelete-a-backup"></a>toodelete kopii zapasowej
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku rozwiń hello **katalog kopii zapasowej** węzła, rozwiń grupę woluminu, a następnie kliknij przycisk **migawki lokalne** lub **migawki w chmurze**. Zostanie wyświetlona lista migawek w hello **wyniki** okienka.
3. Kliknij prawym przyciskiem myszy hello migawki toodelete, a następnie kliknij przycisk **usunąć**.
4. Po wyświetleniu komunikatu potwierdzenia powitania kliknij **OK**.

## <a name="recover-a-file"></a>Odzyskiwanie pliku
Jeśli plik zostanie przypadkowo usunięty z woluminu, można odzyskać pliku hello pobieranie migawki, która wstępnie daty usunięcia hello, przy użyciu toocreate migawki hello klonowania hello woluminu, a następnie kopiowanie pliku hello hello sklonowany toohello oryginalny wolumin.

#### <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem upewnij się, że obecnie wykonać kopii zapasowej grupy woluminu hello. Następnie należy usunąć plik przechowywane na jednym z woluminów hello w tej grupie woluminu. Na koniec użyj hello poniższe kroki toorestore hello usunął plik z kopii zapasowej. 

#### <a name="toorecover-a-deleted-file"></a>toorecover usuniętego pliku
1. Kliknij ikonę StorSimple Snapshot Manager hello na pulpicie. zostanie wyświetlone okno konsoli programu StorSimple Snapshot Manager Hello. 
2. W hello **zakres** okienku rozwiń hello **katalog kopii zapasowej** węzeł i przeglądania tooa migawki, która zawiera plik hello usunięte. Zazwyczaj należy wybierać migawki, która została utworzona tylko przed usunięciem hello.
3. Znajdź hello wolumin ma tooclone, kliknij prawym przyciskiem myszy, a następnie kliknij przycisk **klonowania**. Witaj **migawka w chmurze klonowania** zostanie wyświetlone okno dialogowe.
   
    ![Klonowanie migawka w chmurze](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Zakończenie hello **migawka w chmurze klonowania** okno dialogowe w następujący sposób: 
   
   1. W hello **nazwa** polu tekstowym, wpisz nazwę hello sklonować woluminu. Ta nazwa będzie wyświetlana w hello **woluminów** węzła. 
   2. (Opcjonalnie) Wybierz **dysku**, a następnie wybierz z listy rozwijanej hello literę dysku. 
   3. (Opcjonalnie) Wybierz **folderu NTFS**i wpisz ścieżkę folderu, lub kliknij przycisk **Przeglądaj** i wybierz lokalizację folderu hello. 
   4. Kliknij przycisk **Utwórz**. 
5. Po zakończeniu operacji hello proces klonowania, należy zainicjować hello sklonować woluminu. Uruchom Menedżera serwera, a następnie uruchom Zarządzanie dyskami. Aby uzyskać szczegółowe instrukcje, zobacz [instalowania woluminów](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Po zainicjowaniu, hello woluminu, będą wyświetlane w hello **woluminów** węzła w hello **zakres** okienka. 
   
    Jeśli nie ma woluminu hello na liście, Odśwież listę hello woluminów (powitania kliknij prawym przyciskiem myszy **woluminów** węzeł, a następnie kliknij przycisk **Odśwież**).
6. Otwórz hello NTFS folderu, który zawiera wolumin hello sklonowany, rozwiń węzeł hello **woluminów** węzeł, a następnie otwórz hello sklonować woluminu. Znajdź plik hello mają toorecover i skopiuj go toohello woluminu podstawowego.
7. Po przywróceniu plików hello można usunąć folderu NTFS hello, który zawiera wolumin hello sklonować.

## <a name="restore-hello-storsimple-snapshot-manager-database"></a>Przywracanie bazy danych programu StorSimple Snapshot Manager hello
Należy regularnie wykonywać kopie zapasowe bazy danych programu StorSimple Snapshot Manager hello na komputerze hosta hello. Jeśli komputer-host hello nie powiedzie się z jakiegokolwiek powodu katastrofy lub poważnej awarii, można przywrócić go z kopii zapasowej hello. Tworzenie kopii zapasowej bazy danych hello jest proces ręczny.

#### <a name="tooback-up-and-restore-hello-database"></a>tooback zapasowej i przywracanie bazy danych z hello
1. Zatrzymaj usługi zarządzania StorSimple Microsoft hello:
   
   1. Uruchom Menedżera serwera.
   2. Na pulpicie nawigacyjnym Menedżera serwera hello, na powitania **narzędzia** menu, wybierz opcję **usług**.
   3. Na powitania **usług** okna, wybierz hello **usługi zarządzania StorSimple Microsoft**.
   4. W hello prawym okienku w obszarze **usługi zarządzania StorSimple Microsoft**, kliknij przycisk **Zatrzymaj usługę hello**.
2. Na komputerze-hoście hello Przejdź tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > Folder ProgramData jest folderem ukrytym.
   > 
   > 
3. Znajdź plik XML katalogu hello, kopiowania pliku hello i przechowywanie hello kopiowanie w bezpiecznym miejscu lub w chmurze hello. W przypadku niepowodzenia hello hosta można użyć tego pliku kopii zapasowej toohelp Odzyskaj hello zasad tworzenia kopii zapasowych tworzone StorSimple Snapshot Manager.
   
    ![Plik kopii zapasowej katalogu usługi Azure StorSimple](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_bacatalog.png)
4. Ponowne uruchamianie usługi zarządzania StorSimple Microsoft hello: 
   
   1. Na pulpicie nawigacyjnym Menedżera serwera hello, na powitania **narzędzia** menu, wybierz opcję **usług**.
   2. Na powitania **usług** okna, wybierz hello **usługi zarządzania StorSimple Microsoft**.
   3. W hello prawym okienku w obszarze **usługi zarządzania StorSimple Microsoft**, kliknij przycisk **Uruchom ponownie usługę hello**.
5. Na komputerze-hoście hello Przejdź tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
6. Usuń plik XML katalogu hello i zastąp go hello wersji w kopii zapasowej utworzony. 
7. Kliknij przycisk hello pulpitu StorSimple Snapshot Manager ikona toostart StorSimple Snapshot Manager. 

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [za pomocą programu StorSimple Snapshot Manager tooadminister rozwiązania StorSimple](storsimple-snapshot-manager-admin.md).
* Dowiedz się więcej o [StorSimple Snapshot Manager zadań i przepływów pracy](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows).

