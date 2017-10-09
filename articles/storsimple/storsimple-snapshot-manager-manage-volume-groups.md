---
title: grupy woluminu Snapshot Manager aaaStorSimple | Dokumentacja firmy Microsoft
description: "Opisuje sposób toouse hello toocreate przystawki MMC programu StorSimple Snapshot Manager i zarządzanie grupami woluminu."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a>Użyj toocreate StorSimple Snapshot Manager i Zarządzaj grupami woluminu
## <a name="overview"></a>Omówienie
Można użyć hello **grup woluminu** węzła na powitania **zakres** okienko tooassign woluminów toovolume grup, Wyświetl informacje o grupie woluminu, zaplanować wykonywanie kopii zapasowych i edytować grupy woluminu.

Wolumin grupy są pule tooensure powiązanych woluminów, że kopie zapasowe są spójne z aplikacjami. Aby uzyskać więcej informacji, zobacz [woluminów i woluminów grupy](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) i [integracji z usługą kopiowania woluminów w tle Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).

> [!IMPORTANT]
> * Wszystkie woluminy w grupie woluminu musi pochodzić od dostawcy usług w chmurze pojedynczego.
> * Po skonfigurowaniu grup woluminu niemieszanie udostępnione woluminy klastra (CSV), a nie CSV w hello tej samej grupie woluminu. StorSimple Snapshot Manager nie obsługuje różnych udostępnionych woluminów klastra i z systemem innym niż CSV w hello tego samego migawki.

![Wolumin węzeł grupy](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

**Rysunek 1: Węzeł StorSimple Snapshot Manager woluminu grup** 

W tym samouczku wyjaśniono, jak używasz StorSimple Snapshot Manager do:

* Wyświetlanie informacji o woluminie grup
* Utwórz grupę woluminu
* Tworzenie kopii zapasowej grupy woluminu
* Edytowanie grupy woluminu
* Usuwanie grupy woluminu

Wszystkie te działania są również dostępne na powitania **akcje** okienka.

## <a name="view-volume-groups"></a>Wyświetlanie grup woluminu
Jeśli klikniesz przycisk hello **grup woluminu** węzła, hello **wyniki** w okienku zostaną wyświetlone hello następujących informacji o grupach woluminu, w zależności od opcji kolumny hello wprowadzeniu. (hello kolumn w hello **wyniki** okienku są konfigurowane. Powitania kliknij prawym przyciskiem myszy **woluminów** węzła, wybierz opcję **widoku**, a następnie wybierz **Dodaj/Usuń kolumny**.)

| Kolumny wyników | Opis |
|:--- |:--- |
| Nazwa |Witaj **nazwa** kolumna zawiera nazwę hello hello woluminu grupy. |
| Aplikacja |Witaj **aplikacji** kolumnie jest wyświetlana liczba hello aktualnie zainstalowane składniki zapisywania usługi VSS i systemem hello hosta systemu Windows. |
| Wybrano |Witaj **wybrane** kolumna zawiera numer hello woluminów, które znajdują się w grupie woluminu hello. Wartość zero (0) oznacza, że żadna aplikacja nie jest skojarzony z hello woluminy w grupie woluminu hello. |
| Zaimportowany |Witaj **zaimportowane** kolumna zawiera numer hello importowanych woluminów. Gdy ustawiona zbyt**True**, ta kolumna wskazuje, że grupa woluminu została zaimportowana z hello portalu Azure i programu StorSimple Snapshot Manager nie został utworzony. |

> [!NOTE]
> Grupy woluminu StorSimple Snapshot Manager również są wyświetlane na powitania **zasady tworzenia kopii zapasowej** kartę w hello portalu Azure.
> 
> 

## <a name="create-a-volume-group"></a>Utwórz grupę woluminu
Użyj hello następujące procedury toocreate grupy woluminu.

#### <a name="toocreate-a-volume-group"></a>toocreate grupy woluminu
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku kliknij prawym przyciskiem myszy **grup woluminu**, a następnie kliknij przycisk **Utwórz grupę woluminu**.
   
    ![Utwórz grupę woluminu](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    Witaj **Utwórz grupę woluminu** zostanie wyświetlone okno dialogowe.
   
    ![Tworzenie okna dialogowego grupy woluminu](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. Wprowadź hello następujących informacji:
   
   1. W hello **nazwa** wpisz unikatową nazwę dla nowej grupy woluminu hello.
   2. W hello **aplikacji** polu Wybierz aplikacji skojarzonych z woluminami hello czy dodasz toohello woluminu grupy.
      
       Witaj **aplikacji** okno wyświetla tylko te aplikacje, które korzysta z woluminów StorSimple i mieć składniki zapisywania usługi VSS są włączone dla nich. Składnik zapisywania usługi VSS jest włączone, tylko jeśli hello wszystkie woluminy moduł zapisujący hello jest świadome woluminów StorSimple. Jeśli pole aplikacji hello jest pusta, aplikacje, nie korzysta z woluminów Azure StorSimple, które mają być obsługiwane składniki zapisywania usługi VSS są zainstalowane. (Aktualnie Azure StorSimple obsługuje program Microsoft Exchange i SQL Server). Aby uzyskać więcej informacji na temat zapisywania usługi VSS, zobacz [integracji z usługą kopiowania woluminów w tle Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).
      
       Wybierz aplikację, wszystkie woluminy skojarzone z nim automatycznie zaznaczenie. Z drugiej strony, jeśli wybrano woluminy skojarzone z określoną aplikacją, aplikacji hello jest automatycznie wybierany w hello **aplikacji** pole. 
   3. W hello **woluminów** wybierz grupę toohello tooadd StorSimple woluminów, woluminów. 
      
      * Może zawierać woluminy z jednego lub wielu partycji. (Wiele woluminów partycji może być dynamicznych dysków lub dysków podstawowych z wieloma partycjami.) Wolumin, który zawiera wiele partycji jest traktowany jako pojedyncza jednostka. W związku z tym, jeśli dodasz tylko jeden hello partycje tooa woluminu grupy, hello wszystkie pozostałe partycje są automatycznie dodawanych toothat woluminu grupa na hello sam czas. Po dodaniu wielu grupy woluminu tooa woluminu partycji hello wiele partycji woluminu nadal toobe traktowane jako pojedyncza jednostka.
      * Możesz tworzyć grupy pusty woluminu, przypisując nie toothem żadnych woluminów. 
      * Nie można mieszać udostępnione woluminy klastra (CSV), a nie CSV w hello tej samej grupie woluminu. StorSimple Snapshot Manager nie obsługuje różnych woluminów CSV i woluminów CSV z systemem innym niż w hello tego samego migawki.
4. Kliknij przycisk **OK** toosave hello woluminu grupy.

## <a name="back-up-a-volume-group"></a>Tworzenie kopii zapasowej grupy woluminu
Użyj hello następujące procedury tooback grupy woluminu.

#### <a name="tooback-up-a-volume-group"></a>tooback grupy woluminu
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku rozwiń hello **grup woluminu** węzła, kliknij prawym przyciskiem myszy nazwę grupy woluminu, a następnie kliknij przycisk **wykonać kopii zapasowej**.
   
    ![Natychmiast utworzyć kopię zapasową woluminu grupy](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. W hello **wykonać kopii zapasowej** okno dialogowe, wybierz opcję **migawka lokalna** lub **migawka w chmurze**, a następnie kliknij przycisk **Utwórz**.
   
    ![Zająć kopii zapasowej okna dialogowego](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. tooconfirm, który hello kopii zapasowej jest uruchomiona, rozwiń hello **zadania** węzeł, a następnie kliknij przycisk **systemem**. Kopia zapasowa Hello powinien być wyświetlany.
5. ukończyć powitalnych tooview migawki, rozwiń węzeł hello **katalog kopii zapasowej** węzła, rozwiń nazwę grupy hello woluminu, a następnie kliknij **migawka lokalna** lub **migawka w chmurze**. Hello kopii zapasowej będzie wyświetlane, jeśli zostało zakończone pomyślnie.

## <a name="edit-a-volume-group"></a>Edytowanie grupy woluminu
Użyj hello następujące procedury tooedit grupy woluminu.

#### <a name="tooedit-a-volume-group"></a>tooedit grupy woluminu
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku rozwiń hello **grup woluminu** węzła, kliknij prawym przyciskiem myszy nazwę grupy woluminu, a następnie kliknij przycisk **Edytuj**.
3. Witaj ** Utwórz grupę woluminu ** zostanie wyświetlone okno dialogowe. Możesz zmienić hello **nazwa**, **aplikacji**, i **woluminów** wpisów.
4. Kliknij przycisk **OK** toosave zmiany.

## <a name="delete-a-volume-group"></a>Usuwanie grupy woluminu
Użyj hello następujące procedury toodelete grupy woluminu. 

> [!WARNING]
> Powoduje to również usunięcie wszystkich hello kopii zapasowych skojarzone z grupą woluminu hello.
> 
> 

#### <a name="toodelete-a-volume-group"></a>toodelete grupy woluminu
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku rozwiń hello **grup woluminu** węzła, kliknij prawym przyciskiem myszy nazwę grupy woluminu, a następnie kliknij przycisk **usunąć**.
3. Witaj **Usuń grupę woluminu** zostanie wyświetlone okno dialogowe. Typ **Potwierdź** w hello pola tekstowego, a następnie kliknij przycisk **OK**.
   
    nieodpowiedniej grupy woluminu Hello usunięty z listy hello w hello **wyniki** okienko i wszystkie kopie zapasowe, które są skojarzone z tą grupą woluminu zostaną usunięte z hello katalogu kopii zapasowej.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[użyć tooadminister StorSimple Snapshot Manager rozwiązania StorSimple](storsimple-snapshot-manager-admin.md).
* Dowiedz się, jak za[Użyj toocreate StorSimple Snapshot Manager i zarządzanie zasadami tworzenia kopii zapasowej](storsimple-snapshot-manager-manage-backup-policies.md).

