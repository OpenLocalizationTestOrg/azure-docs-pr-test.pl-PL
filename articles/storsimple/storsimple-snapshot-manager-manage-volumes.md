---
title: "aaaStorSimple Snapshot Manager i woluminów | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse hello tooview przystawki MMC programu StorSimple Snapshot Manager i zarządzanie nimi woluminów i tooconfigure kopii zapasowych."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a>Użyj tooview StorSimple Snapshot Manager i zarządzanie woluminami
## <a name="overview"></a>Omówienie
Hello StorSimple Snapshot Manager można użyć **woluminów** węzła (na powitania **zakres** okienko) tooselect woluminów i wyświetlania informacji o nich. woluminy Hello są widoczne jako dyski, które odpowiadają toohello woluminów zainstalowanych w wyniku hello hosta. Witaj **woluminów** węzeł zawiera woluminy lokalne i typów woluminów, które są obsługiwane przez StorSimple, w tym także woluminów o wykryte za pomocą hello iSCSI i urządzenia. 

Aby uzyskać więcej informacji o obsługiwanych woluminach Przejdź zbyt[obsługi wielu typów woluminu](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).

![Lista woluminu w okienku wyników](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

Witaj **woluminów** węzeł umożliwia również w ponownie przeskanuj lub Usuń woluminy, po StorSimple Snapshot Manager odnajduje je. 

W tym samouczku wyjaśniono, jak można zainstalować, zainicjować i sformatować woluminy i następnie użyć StorSimple Snapshot Manager do:

* Wyświetlanie informacji o woluminach 
* Usuwanie woluminów
* Skanuj woluminów 
* Konfigurowanie podstawowego woluminu i wykonać ich kopię zapasową
* Konfigurowanie dynamicznego woluminu dublowanego i wykonać ich kopię zapasową

> [!NOTE]
> Wszystkie hello **woluminu** węzła akcje są dostępne również w hello **akcje** okienka.
> 
> 

## <a name="mount-volumes"></a>Zainstalować woluminów
Użyj hello następujące procedury toomount, zainicjować i sformatować woluminy StorSimple. Ta procedura wykorzystuje przystawki Zarządzanie dyskami systemu narzędzie do zarządzania dyskami twardymi i hello odpowiednich woluminów lub partycji. Aby uzyskać więcej informacji na temat narzędzia Zarządzanie dyskami Przejdź zbyt[Zarządzanie dyskami](https://technet.microsoft.com/library/cc770943.aspx) w witrynie Microsoft TechNet hello.

#### <a name="toomount-volumes"></a>woluminy toomount
1. Uruchom inicjatora iSCSI firmy Microsoft hello na komputerze hosta.
2. Podaj adresy IP interfejsu hello hello portalu obiektu docelowego lub adres IP odnajdywania, a następnie podłącz urządzenie toohello. Po podłączeniu urządzenia hello woluminy hello będą dostępne tooyour systemu Windows. Aby uzyskać więcej informacji o korzystaniu z inicjatora iSCSI firmy Microsoft hello Przejdź toohello sekcji "Łączenie tooan iSCSI urządzenia docelowego" [Instalowanie i konfigurowanie programu Microsoft iSCSI Initiator][1].
3. Użyj dowolnej z hello następujące opcje toostart Zarządzanie dyskami:
   
   * Wpisz Diskmgmt.msc hello **Uruchom** pole.
   * Uruchom Menedżera serwera, rozwiń hello **magazynu** węzeł, a następnie wybierz **Zarządzanie dyskami**.
   * Uruchom **narzędzia administracyjne**, rozwiń węzeł hello **Zarządzanie komputerem** węzeł, a następnie wybierz **Zarządzanie dyskami**. 
     
     > [!NOTE]
     > Należy użyć toorun uprawnień administratora zarządzania dyskami.
     > 
     > 
4. Wykonaj woluminów hello online:
   
   1. W przystawce Zarządzanie dyskami kliknij prawym przyciskiem myszy każdy wolumin oznaczony **Offline**.
   2. Kliknij przycisk **Uaktywnij ponownie dysk**. Witaj dysku powinna być oznaczona jako **Online** po uaktywnieniu hello dysku.
5. Inicjowanie woluminów hello:
   
   1. Kliknij prawym przyciskiem myszy hello odnalezione woluminów.
   2. W hello menu, wybierz **Inicjowanie dysku**.
   3. W hello **Inicjowanie dysku** okno dialogowe, wybierz opcję hello dyski mają tooinitialize, a następnie kliknij przycisk **OK**.
6. Formatowanie woluminów prostych:
   
   1. Kliknij prawym przyciskiem myszy wolumin, które mają tooformat.
   2. W hello menu, wybierz **nowy wolumin prosty**.
   3. Użyj hello nowy wolumin prosty kreator tooformat hello woluminu:
      
      * Określ rozmiar woluminu hello.
      * Należy podać literę dysku.
      * Wybierz system plików NTFS hello.
      * Określ rozmiar jednostki alokacji 64 KB.
      * Przeprowadź szybkie formatowanie.
7. Formatowanie woluminów wielu partycji. Aby uzyskać instrukcje, przejdź toohello sekcji "Partycje i woluminy" [implementacja Zarządzanie dyskami](https://msdn.microsoft.com/library/dd163556.aspx).

## <a name="view-information-about-your-volumes"></a>Wyświetlanie informacji o woluminach
Użyj hello następujące procedury tooview informacje o lokalnych i woluminy Azure StorSimple.

#### <a name="tooview-volume-information"></a>informacji o woluminie tooview
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager. 
2. W hello **zakres** okienku, kliknij przycisk hello **woluminów** węzła. Lista lokalnych i zainstalowanych woluminów, w tym wszystkie woluminy Azure StorSimple, jest wyświetlana w hello **wyniki** okienka. Witaj kolumn w hello **wyniki** okienku są konfigurowane. (Powitania kliknij prawym przyciskiem myszy **woluminów** węzła, wybierz opcję **widoku**, a następnie wybierz **Dodaj/Usuń kolumny**.)
   
    ![Skonfiguruj hello kolumn](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | Kolumny wyników | Opis |
   |:--- |:--- |
   |  Nazwa |Witaj **nazwa** kolumna zawiera wolumin tooeach odnalezione przypisany literą dysku hello. |
   |  Urządzenie |Witaj **urządzenia** kolumna zawiera adres IP hello hello urządzeń podłączonych toohello hosta komputera. |
   |  Nazwa woluminu urządzenia |Hello **nazwa woluminu urządzenia** kolumna zawiera nazwę hello hello urządzenia woluminu toowhich hello wybrane należy woluminu. Jest to nazwa woluminu hello zdefiniowane w hello portalu Azure dla tego określonego woluminu. |
   |  Dostęp do ścieżki |Witaj **ścieżek dostępu** kolumny Wyświetla hello dostępu do ścieżki toohello woluminu. Jest to hello dysku litera lub punkt instalacji na które hello wolumin jest dostępny na komputerze hosta hello. |

## <a name="delete-a-volume"></a>Usuwanie woluminu
Użyj następującej procedury toodelete woluminu z StorSimple Snapshot Manager hello.

> [!NOTE]
> Nie można usunąć woluminu, jeśli jest częścią żadnej grupy woluminu. (opcja usuwania hello nie jest dostępne dla woluminów, które są elementami członkowskimi grupy woluminu). Należy usunąć hello cały wolumin grupy toodelete hello woluminu.

#### <a name="toodelete-a-volume"></a>toodelete woluminu
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku, kliknij przycisk hello **woluminów** węzła. 
3. W hello **wyniki** okienku, kliknij prawym przyciskiem myszy wolumin hello, które mają toodelete.
4. Polecenie hello menu **usunąć**. 
   
    ![Usuwanie woluminu](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. Witaj **Usuń wolumin** zostanie wyświetlone okno dialogowe. Typ **Potwierdź** w hello pola tekstowego, a następnie kliknij przycisk **OK**.
6. Domyślnie StorSimple Snapshot Manager kopię zapasową woluminu przed jego usunięciem. W ten sposób może chronić należy przed utratą danych usunięcia hello nie była planowana. Wyświetla StorSimple Snapshot Manager **automatyczne migawki** komunikatu o postępie podczas jego kopię zapasową woluminu hello. 
   
    ![Komunikat automatyczne migawki](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a>Skanuj woluminów
Użyj następującej procedury toorescan hello woluminów połączonych tooStorSimple Snapshot Manager hello.

#### <a name="toorescan-hello-volumes"></a>toorescan hello woluminów
1. Kliknij przycisk hello ikony pulpitu toostart StorSimple Snapshot Manager.
2. W hello **zakres** okienku kliknij prawym przyciskiem myszy **woluminów**, a następnie kliknij przycisk **ponownego skanowania woluminów**.
   
    ![Skanuj woluminów](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    Ta procedura synchronizuje hello Lista woluminów z StorSimple Snapshot Manager. Wszelkie zmiany, takie jak nowe woluminy lub usunięte, zostaną uwzględnione w wynikach hello.

## <a name="configure-and-back-up-a-basic-volume"></a>Konfigurowanie i tworzenie kopii zapasowej woluminu podstawowego
Użyj powitania po tooconfigure procedury tworzenia kopii zapasowej woluminu podstawowego, a następnie natychmiast rozpocząć tworzenie kopii zapasowej albo utworzyć zasady dla zaplanowanych kopii zapasowych.

### <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem:

* Upewnij się, że hello urządzenia StorSimple i komputer-host są skonfigurowane prawidłowo. Aby uzyskać więcej informacji, przejdź zbyt[wdrażanie lokalnego urządzenia StorSimple](storsimple-deployment-walkthrough-u2.md).
* Instalowanie i konfigurowanie programu StorSimple Snapshot Manager. Aby uzyskać więcej informacji, przejdź zbyt[wdrażanie StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).

#### <a name="tooconfigure-backup-of-a-basic-volume"></a>Kopia zapasowa tooconfigure woluminu podstawowego
1. Tworzenie woluminu podstawowego na urządzeniu StorSimple hello.
2. Zainstalować, zainicjować i sformatować wolumin hello, zgodnie z opisem w [instalowania woluminów](#mount-volumes). 
3. Kliknij ikonę StorSimple Snapshot Manager hello na pulpicie. zostanie wyświetlone okno programu StorSimple Snapshot Manager Hello. 
4. W hello **zakres** okienku, kliknij prawym przyciskiem myszy hello **woluminów** węzeł, a następnie wybierz **ponownego skanowania woluminów**. Po zakończeniu skanowania hello listę woluminów powinna zostać wyświetlona w hello **wyniki** okienka. 
5. W hello **wyniki** okienku kliknij prawym przyciskiem myszy wolumin hello, a następnie wybierz **Utwórz grupę woluminu**. 
   
    ![Utwórz grupę woluminu](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. W hello **Utwórz grupę woluminu** okno dialogowe, wpisz nazwę grupy woluminu hello, przypisz tooit woluminy, a następnie kliknij **OK**.
7. W hello **zakres** okienku rozwiń hello **grup woluminu** węzła. Nowa grupa woluminu Hello powinna zostać wyświetlona w obszarze hello **grup woluminu** węzła. 
8. Kliknij prawym przyciskiem myszy nazwę grupy hello woluminu.
   
   * toostart interakcyjne (na żądanie) zadanie tworzenia kopii zapasowej, kliknij przycisk **wykonać kopii zapasowej**. 
   * tooschedule automatycznego tworzenia kopii zapasowej, kliknij przycisk **Utwórz zasady tworzenia kopii zapasowej**. Na powitania **ogólne** wybierz z listy hello grupy woluminu. Na powitania **harmonogram** wprowadź szczegóły harmonogramu hello. Gdy skończysz, kliknij przycisk **OK**. 
9. Rozpoczęto tooconfirm, który hello zadanie tworzenia kopii zapasowej, a następnie rozwiń hello **zadania** węzła w hello **zakres** okienku, a następnie kliknij przycisk hello **systemem** węzła. w hello zostanie wyświetlona lista aktualnie uruchomionych zadań Hello **wyniki** okienka. 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a>Konfigurowanie i tworzenie kopii zapasowej woluminu dublowanego dynamiczne
Wykonaj następujące kroki tooconfigure tworzenia kopii zapasowej woluminu dublowanego dynamiczne hello:

* Krok 1: Użyj przystawki Zarządzanie dyskami toocreate dynamicznego woluminu dublowanego. 
* Krok 2: Użyj StorSimple Snapshot Manager tooconfigure kopii zapasowej.

### <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem:

* Upewnij się, że hello urządzenia StorSimple i komputer-host są skonfigurowane prawidłowo. Aby uzyskać więcej informacji, przejdź zbyt[wdrażanie lokalnego urządzenia StorSimple](storsimple-8000-deployment-walkthrough-u2.md).
* Instalowanie i konfigurowanie programu StorSimple Snapshot Manager. Aby uzyskać więcej informacji, przejdź zbyt[wdrażanie StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).
* Skonfiguruj dwa woluminy na powitania urządzenia StorSimple. (W przykładach hello są dostępne woluminy hello **dysk 1** i **Disk 2**.) 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a>Krok 1: Użyj przystawki Zarządzanie dyskami toocreate dynamicznego woluminu dublowanego
Zarządzanie dyskami jest narzędziem system zarządzania dyski i woluminy hello lub partycji, które zawierają. Aby uzyskać więcej informacji na temat narzędzia Zarządzanie dyskami Przejdź zbyt[Zarządzanie dyskami](https://technet.microsoft.com/library/cc770943.aspx) w witrynie Microsoft TechNet hello.

#### <a name="toocreate-a-dynamic-mirrored-volume"></a>toocreate dynamicznego woluminu dublowanego
1. Użyj dowolnej z hello następujące opcje toostart Zarządzanie dyskami: 
   
   * Otwórz hello **Uruchom** wpisz **Diskmgmt.msc**, i naciśnij klawisz Enter.
   * Uruchom Menedżera serwera, rozwiń hello **magazynu** węzeł, a następnie wybierz **Zarządzanie dyskami**. 
   * Uruchom **narzędzia administracyjne**, rozwiń węzeł hello **Zarządzanie komputerem** węzeł, a następnie wybierz **Zarządzanie dyskami**. 
2. Upewnij się, że na urządzeniu StorSimple hello są dostępne dwa woluminy. (W przykładzie hello są dostępne woluminy hello **dysk 1** i **Disk 2**.) 
3. W oknie Zarządzanie dyskami hello w prawej kolumnie hello hello dolnym okienku kliknij prawym przyciskiem myszy **dysk 1** i wybierz **nowy wolumin dublowany**. 
   
    ![Nowy wolumin dublowany](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. Na powitania **nowy wolumin dublowany** strona kreatora, kliknij przycisk **dalej**.
5. Na powitania **Wybierz dyski** wybierz **Disk 2** w hello **wybrane** okienku, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **dalej**. 
6. Na powitania **Przypisz literę dysku lub ścieżka** Zaakceptuj ustawienia domyślne hello, a następnie kliknij pozycję **dalej**. 
7. Na powitania **Format wolumin** strony w hello **rozmiar jednostki alokacji** wybierz opcję **64 KB**. Wybierz hello **Przeprowadź szybkie formatowanie** pole wyboru, a następnie kliknij przycisk **dalej**. 
8. Na powitania **hello wykonywanie nowy wolumin dublowany** , przejrzyj ustawienia, a następnie kliknij przycisk **Zakończ**. 
9. Pojawia się komunikat tooindicate, którego dysk podstawowy hello będą przekonwertowane tooa dysku dynamicznego. Kliknij przycisk **Yes** (Tak).
   
    ![Komunikat konwersji dysku dynamicznego](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. W przystawce Zarządzanie dyskami sprawdź, czy dysk 1 i 2 dysku są widoczne jako dynamiczne woluminy dublowane. (**Dynamiczne** powinny być wyświetlane w kolumnie Stan hello i kolor paska hello pojemności należy zmienić toored i wskazujący woluminu dublowanego.) 
    
    ![Dyski dynamiczne zarządzanie dublowany dysk](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a>Krok 2: Użyj StorSimple Snapshot Manager tooconfigure tworzenia kopii zapasowej
Użyj hello następujące procedury tooconfigure dynamicznego woluminu dublowanego, a następnie albo natychmiast rozpocząć tworzenie kopii zapasowej lub utworzyć zasady dla zaplanowanych kopii zapasowych.

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a>Kopia zapasowa tooconfigure woluminu dublowanego dynamiczne
1. Kliknij ikonę StorSimple Snapshot Manager hello na pulpicie. zostanie wyświetlone okno programu StorSimple Snapshot Manager Hello. 
2. W hello **zakres** okienku, kliknij prawym przyciskiem myszy hello **woluminów** a następnie wybierz węzeł **ponownego skanowania woluminów**. Po zakończeniu skanowania hello listę woluminów powinna zostać wyświetlona w hello **wyniki** okienka. Witaj dynamicznego woluminu dublowanego znajduje się w jednym woluminie. 
3. W hello **wyniki** okienku kliknij prawym przyciskiem myszy hello dynamicznego woluminu dublowanego, a następnie kliknij przycisk **Utwórz grupę woluminu**. 
4. W hello **Utwórz grupę woluminu** okno dialogowe, wpisz nazwę grupy woluminu hello, przypisz hello dynamicznego woluminu dublowanego toothis grupę, a następnie kliknij **OK**. 
5. W hello **zakres** okienku rozwiń hello **grup woluminu** węzła. Nowa grupa woluminu Hello powinna zostać wyświetlona w obszarze hello **grup woluminu** węzła. 
6. Kliknij prawym przyciskiem myszy nazwę grupy hello woluminu. 
   
   * toostart interakcyjne (na żądanie) zadanie tworzenia kopii zapasowej, kliknij przycisk **wykonać kopii zapasowej**. 
   * tooschedule automatycznego tworzenia kopii zapasowej, kliknij przycisk **Utwórz zasady tworzenia kopii zapasowej**. Na powitania **ogólne** strony, grupa woluminu hello wybierz z listy hello. Na powitania **harmonogram** wprowadź szczegóły harmonogramu hello. Gdy skończysz, kliknij przycisk **OK**. 
7. Zadanie tworzenia kopii zapasowej hello można monitorować podczas jego wykonywania. W hello **zakres** okienku rozwiń hello **zadania** węzeł, a następnie kliknij przycisk **systemem**, hello zadania szczegóły są wyświetlane w hello **wyniki** okienka. Po zakończeniu zadania tworzenia kopii zapasowej hello szczegóły hello są przekazanych toohello **ostatnich 24** godziny zadania listy. 

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[użyć tooadminister StorSimple Snapshot Manager rozwiązania StorSimple](storsimple-snapshot-manager-admin.md).
* Dowiedz się, jak za[Użyj toocreate StorSimple Snapshot Manager i Zarządzaj grupami woluminu](storsimple-snapshot-manager-manage-volume-groups.md).

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
