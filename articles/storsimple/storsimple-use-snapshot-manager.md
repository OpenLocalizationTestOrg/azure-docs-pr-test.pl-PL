---
title: "Interfejs użytkownika programu Snapshot Manager aaaStorSimple | Dokumentacja firmy Microsoft"
description: "Zawiera opis interfejsu użytkownika programu StorSimple Snapshot Manager hello i jak toouse on toomanage zadania tworzenia kopii zapasowej i hello kopii zapasowej wykazu."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: c7d91892-2881-41a2-a7a2-908dc3646493
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.custom: 
ms.openlocfilehash: 865520fdaf1b559714b52b428ad136b084d65c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-user-interface-toomanage-backup-jobs-and-backup-catalog"></a>Zadania tworzenia kopii zapasowej toomanage interfejsu użytkownika używana StorSimple Snapshot Manager i katalogu kopii zapasowej

## <a name="overview"></a>Omówienie
Witaj StorSimple Snapshot Manager ma intuicyjnego interfejsu użytkownika może używać tootake i zarządzanie kopiami zapasowymi. W tym samouczku udostępnia interfejs użytkownika toohello wprowadzenie, a następnie wyjaśnia sposób toouse hello składników. Aby uzyskać szczegółowy opis hello StorSimple Snapshot Manager, zobacz [co to jest StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

### <a name="console-description"></a>Opis elementu konsoli
tooview hello użytkowników interface, kliknij ikonę StorSimple Snapshot Manager hello na pulpicie. zostanie wyświetlone okno konsoli Hello, jak pokazano w hello następującej ilustracji.

![Okienka programu StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_gui_panes.png)

okno konsoli Hello ma pięć głównych elementów. Kliknij odpowiednie łącze hello pełny opis każdego elementu.

* [Pasek menu](#menu-bar) 
* [Pasek narzędzi](#tool-bar) 
* [Okienko zakresu](#scope-pane) 
* [W okienku wyników](#results-pane) 
* [W okienku Akcje](#actions-pane) 

Ponadto hello StorSimple Snapshot Manager obsługuje [klawiatury nawigacji i liczbę skrótów](#keyboard-navigation-and-shortcuts).

### <a name="console-accessibility"></a>Ułatwienia dostępu w konsoli
Interfejs użytkownika programu StorSimple Snapshot Manager Hello obsługuje funkcje ułatwień dostępu hello udostępnione przez system operacyjny Windows hello i hello Microsoft Management Console (MMC), a także niektóre skróty klawiaturowe specyficzne dla programu StorSimple Snapshot Manager. 

* Opis funkcji ułatwień dostępu systemu Windows hello, przejdź zbyt[skróty klawiaturowe dla systemu Windows](https://support.microsoft.com/kb/126449). 
* Opis funkcji ułatwień dostępu programu MMC hello Przejdź zbyt[ułatwień dostępu dla programu MMC 3.0](https://technet.microsoft.com/library/cc766075.aspx)
* Opis funkcji ułatwień dostępu programu StorSimple Snapshot Manager hello Przejdź zbyt[klawiatury nawigacji i skróty](#keyboard-navigation-and-shortcuts).

## <a name="menu-bar"></a>Pasek menu
zawiera Hello paska menu u góry okna konsoli hello hello [pliku](#file-menu), [akcji](#action-menu), [widoku](#view-menu), [ulubione](#favorites-menu), [okna ](#window-menu), i [pomocy](#help-menu) menu.

Kliknij dowolny element widoczny na toosee paska menu hello listę dostępnych poleceń tego menu. Witaj poniższy przykład przedstawia hello **widoku** wybranego na pasku menu hello menu.

![Wybrane menu Widok](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png)

### <a name="file-menu"></a>Menu Plik
Witaj **pliku** menu zawiera standardowe polecenia programu Microsoft Management Console (MMC).

#### <a name="menu-access"></a>Dostęp do menu
Witaj tooview **pliku** menu, kliknij przycisk **pliku** hello paska menu. pojawia się po menu Hello.

![Menu Plik StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_FileMenu.png) 

#### <a name="menu-description"></a>Opis elementu menu
Witaj poniższej tabeli opisano elementy, które są wyświetlane na powitania **pliku** menu.

| Element menu | Opis |
|:--- |:--- |
| Nowy |Kliknij przycisk **nowy** toocreate nową konsolę oparte na powitania StorSimple Snapshot Manager. |
| Otwarty |Kliknij przycisk **Otwórz** tooopen istniejącej konsoli. |
| Zapisz |Kliknij przycisk **zapisać** toosave hello bieżącej konsoli. |
| Zapisz jako |Kliknij przycisk **Zapisz jako** toocreate nowy, zmieniono nazwę wystąpienia hello bieżącej konsoli. Użyj hello **Zapisz jako** opcję toocustomize widoku i zapisać go do nowszej pobierania. Na przykład można utworzyć przystawki StorSimple Snapshot Manager tego punktu toospecific serwerów. |
| Dodaj/Usuń przystawkę |Kliknij przycisk **Dodaj/Usuń przystawkę** tooadd lub usuwanie przystawek i tooorganize węzłów w hello **zakres** okienka. Aby uzyskać więcej informacji, przejdź zbyt[Dodaj, Usuń i organizowanie przystawek i rozszerzeń w programie MMC 3.0](https://technet.microsoft.com/library/cc722035.aspx). |
| Opcje |Kliknij przycisk **opcje** toochange hello konsoli ikony, określ tryby dostępu do użytkownika i uprawnienia lub usunąć konsoli pliki tooincrease dostępnego miejsca na dysku. |
| Lista ścieżek pliku |Kliknij przycisk ścieżki w powitalne numerowane listy tooreopen pliku, który ostatnio otwarty. |
| Zakończ |Kliknij przycisk **zakończenia** tooclose hello **pliku** menu. |

### <a name="action-menu"></a>Menu akcji
Użyj hello **akcji** tooselect menu z dostępnych akcji. tooyou dostępne elementy Hello są zależne od wyboru hello w hello **zakres** okienku lub **wyniki** okienka.

#### <a name="menu-access"></a>Dostęp do menu
Witaj tooview **akcji** menu, wykonaj jedną z następujących hello:

* Kliknij prawym przyciskiem myszy element hello **zakres** okienku lub **wyniki** okienka.
* Wybierz element w hello **zakres** okienku lub **wyniki** okienka, a następnie kliknij przycisk **akcji** hello paska menu. 

Na przykład zaznacz górny węzeł hello w hello **zakres** okienka, a następnie kliknij prawym przyciskiem myszy lub kliknij przycisk **akcji** na pasku menu hello hello następujące zostanie wyświetlone menu.

![Menu Akcja StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_Action_menu.png)

Witaj **akcje** okienko (na powitania rogu konsoli hello) zawiera hello tę samą listę akcji jako hello **akcji** menu. Ponadto hello **akcje** okienko zawiera hello **widoku** opcji menu, które pozwalają toocreate niestandardowy widok hello **wyniki** okienka.

![Otwórz w okienku Akcje, z menu Widok](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

#### <a name="menu-description"></a>Opis elementu menu
w poniższej tabeli Hello zawiera alfabetyczną listę akcji StorSimple Snapshot Manager. 

* Witaj **akcji** kolumna zawiera akcje, które mogą wykonywać na węzły i wyniki. 
* Hello **nawigacji** kolumny wyjaśniono, jak odpowiednie hello toodisplay **akcji** menu, w którym można wybrać hello akcji. Niektóre akcje są wyświetlane w wielu **akcji** menu. Te akcje, wybierz jedną **nawigacji** opcję z listy punktowanej hello. 
* Hello **opis** kolumny opisano sposób toouse każdej akcji na powitania **akcji** menu lub w okienku Akcje oraz wyjaśniono, jak działa.

> [!NOTE]
> Witaj **akcje** okienko i **akcji** menu zawierają dodatkowe opcje, takie jak **widoku**, **nowe okno w tym miejscu**,  **Odśwież**, **wyeksportować listę**, i **pomocy**. Te opcje są dostępne jako część hello MMC i nie są określone tooStorSimple Snapshot Manager. Witaj tabela zawiera opisy tych opcji.
> 
> 

| Akcja | Nawigacji | Opis |
|:--- |:--- |:--- |
| Uwierzytelnianie |Kliknij przycisk hello **urządzeń** węzeł i kliknij prawym przyciskiem myszy urządzenie w hello **wyniki** okienka. |Kliknij przycisk **Uwierzytelnij** tooenter hello hasło skonfigurowane dla hello urządzenia. |
| Klonuj |Rozwiń węzeł **katalogu kopii zapasowej**, rozwiń węzeł **migawki w chmurze**, kliknij z kopii zapasowej, a następnie wybierz wolumin hello **wyniki** okienka. |Kliknij przycisk **klonowania** toocreate kopia chmury migawki i zapisz go w lokalizacji, które zostało określone. |
| Konfigurowanie urządzenia |Kliknij prawym przyciskiem myszy hello **urządzeń** węzła. |Kliknij przycisk **Skonfiguruj urządzenie** tooconfigure jednego lub wielu urządzeniach tooconnect toohello hosta systemu Windows. |
| Tworzenie zasad tworzenia kopii zapasowej |Wykonaj jedną z następujących hello:<ul><li>Kliknij prawym przyciskiem myszy **zasady tworzenia kopii zapasowej**.</li><li>Kliknij i rozwiń **grup woluminu**, a następnie kliknij prawym przyciskiem myszy grupę woluminu.</li><li>Kliknij i rozwiń **katalog kopii zapasowej**, a następnie kliknij prawym przyciskiem myszy grupę woluminu.</li></ul> |Kliknij przycisk **Utwórz zasady tworzenia kopii zapasowej** tooconfigure zaplanowanego tworzenia kopii zapasowej dla grupy woluminu. |
| Utwórz grupę woluminu |Wykonaj jedną z następujących hello:<ul><li>Kliknij przycisk hello **woluminów** węzeł, a następnie kliknij prawym przyciskiem myszy wolumin w hello **wyniki** okienka.</li><li>Kliknij prawym przyciskiem myszy hello **grup woluminu** węzła.</li></ul> |Kliknij przycisk **Utwórz grupę woluminu** tooassign woluminów tooa woluminu grupy. |
| Usuwanie |Kliknij węzeł lub wynik (ten element będzie wyświetlany na wiele **akcji** menu i **akcje** okienka.) |Kliknij przycisk **usunąć** toodelete hello węzła lub wynik wybrany. Gdy pojawi się okno dialogowe potwierdzenia hello, potwierdzenia lub anulować usunięcie hello. |
| Szczegóły |Kliknij przycisk hello **urządzeń** węzeł, a następnie kliknij prawym przyciskiem myszy urządzenie w hello **wyniki** okienka. |Kliknij przycisk **szczegóły** toosee hello szczegóły konfiguracji urządzenia. |
| Edytuj |Kliknij przycisk **zasady tworzenia kopii zapasowej**, a następnie kliknij prawym przyciskiem myszy zasadę w hello **wyniki** okienka. |Kliknij przycisk **Edytuj** toochange hello harmonogram tworzenia kopii zapasowych dla grupy woluminu. |
| Wyeksportuj listę |Kliknij dowolny węzeł lub wynik (ten element będzie wyświetlany we wszystkich **akcji** menu i **akcje** okienka.) |Kliknij przycisk **Eksportuj listę** toosave listy w pliku wartości rozdzielanych przecinkami (CSV). Następnie można zaimportować ten plik do arkusza kalkulacyjnego aplikacji do analizy. |
| Pomoc |Kliknij dowolny węzeł lub wynik. (Ten element będzie wyświetlany we wszystkich **akcji** menu i **akcje** okienka.) |Kliknij przycisk **pomocy** tooopen pomocy online w osobnym oknie przeglądarki. |
| Nowe okno w tym miejscu |Kliknij dowolny węzeł lub wynik (ten element będzie wyświetlany we wszystkich **akcji** menu i **akcje** okienka.) |Kliknij przycisk **nowe okno w tym miejscu** tooopen nowe okno programu StorSimple Snapshot Manager. |
| Odśwież |Kliknij dowolny węzeł lub wynik (ten element będzie wyświetlany we wszystkich **akcji** menu i **akcje** okienka.) |Kliknij przycisk **Odśwież** tooupdate hello aktualnie wyświetlany StorSimple Snapshot Manager okna. |
| Odśwież urządzenia |Kliknij przycisk hello **urządzeń** węzeł i kliknij prawym przyciskiem myszy urządzenie w hello **wyniki** okienka. |Kliknij przycisk **Odśwież urządzenia** toosynchronize określonego urządzenia połączone z StorSimple Snapshot Manager. |
| Odśwież urządzenia |Kliknij prawym przyciskiem myszy hello **urządzeń** węzła. |Kliknij przycisk **Odśwież urządzeń** toosynchronize listy urządzeń połączonych z StorSimple Snapshot Manager. |
| Skanuj woluminów |Kliknij prawym przyciskiem myszy hello **woluminów** węzła. |Kliknij przycisk **ponownego skanowania woluminów** tooupdate hello listę woluminów w hello **wyniki** okienka. |
| Przywracanie |Rozwiń węzeł **katalogu kopii zapasowej**, rozwiń grupę woluminu, rozwiń węzeł **migawki lokalne** lub **migawki w chmurze**, a następnie kliknij prawym przyciskiem myszy kopii zapasowej. |Kliknij przycisk **przywrócić** tooreplace hello bieżącej grupy danych woluminu hello danymi z hello wybranej kopii zapasowej. |
| Wykonać kopii zapasowej |Wykonaj jedną z następujących hello:<ul><li>Rozwiń węzeł **grup woluminu**, a następnie kliknij prawym przyciskiem myszy grupę woluminu.</li><li>Rozwiń węzeł **katalog kopii zapasowej**, a następnie kliknij prawym przyciskiem myszy grupę woluminu.</li></ul> |Kliknij przycisk **wykonać kopii zapasowej** toostart zadania tworzenia kopii zapasowej natychmiast. |
| Przełącz wyświetlanie importów |Kliknij prawym przyciskiem myszy górny węzeł hello w hello **zakres** okienka (hello **StorSimple Snapshot Manager** węzła w przykładach hello). |Kliknij przycisk **Przełącz importów wyświetlanie** tooshow lub ukrywanie grup woluminu hello i skojarzonych kopii zapasowych, które zostały zaimportowane z hello pulpit nawigacyjny usługi Menedżer StorSimple urządzenia. |

### <a name="view-menu"></a>Menu Widok
Użyj hello **widoku** toocreate menu niestandardowy widok hello **wyniki** zawartość okienka. Witaj **widoku** zawiera menu **Dodaj/Usuń kolumny** i **Dostosuj** opcje.

#### <a name="menu-access"></a>Dostęp do menu
Dostęp można uzyskać hello **widoku** menu na pasku menu hello lub hello **akcje** okienka.

![Menu Widok programu StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png) 

#### <a name="menu-description"></a>Opis elementu menu
Witaj poniższej tabeli opisano elementy, które są wyświetlane na powitania **widoku** menu.

| Element menu | Opis |
|:--- |:--- |
| Dodawanie/usuwanie kolumn |Kliknij przycisk **Dodaj/Usuń kolumny** tooadd lub usuwanie kolumn w hello **wyniki** okienka. |
| Dostosowywanie |Kliknij przycisk **Dostosuj** tooshow lub Ukryj elementy w oknie konsoli hello StorSimple Snapshot Manager. |

### <a name="favorites-menu"></a>Menu Ulubione
Użyj hello **ulubione** menu tooadd, usuwanie i organizowanie strony widoków i zadań, które są często używane. 

#### <a name="menu-access"></a>Dostęp do menu
Dostęp można uzyskać hello **ulubione** menu na pasku menu hello.

![Menu Ulubione StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_FavoritesMenu.png)

#### <a name="menu-description"></a>Opis elementu menu
Witaj poniższej tabeli opisano elementy, które są wyświetlane na powitania **ulubione** menu.

| Element menu | Opis |
|:--- |:--- |
| Dodaj tooFavorites |Kliknij przycisk **dodać tooFavorites** tooadd hello bieżący widok tooyour listy ulubionych. |
| Skróty do ulubionych |Kliknij przycisk **organizowanie ulubionych** tooorganize hello zawartość folderu Ulubione. |

### <a name="window-menu"></a>Menu okna
Użyj hello **okna** menu tooadd i zmieniać StorSimple Snapshot Manager konsoli systemu windows.

#### <a name="menu-access"></a>Dostęp do menu
Dostęp można uzyskać hello **okna** menu na pasku menu hello.

![Menu okna StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_WindowMenu.png)

Lista numerowana Hello u dołu hello menu hello pokazuje windows hello, które są aktualnie otwarte. Kliknij pozycję wszystkie okna w danym przedziale hello toobring listy na pierwszym planie hello. 

#### <a name="menu-description"></a>Opis elementu menu
Hello poniższej tabeli opisano elementy hello, które pojawiają się na powitania menu okna.

| Element menu | Opis |
|:--- |:--- |
| Nowe okno |Kliknij przycisk **nowe okno** tooopen nowe okno konsoli (w oknie istniejących toohello dodanie). |
| Kaskadowo |Kliknij przycisk **Cascade** toodisplay hello otwartej konsoli windows w kaskadowego stylu. |
| Sąsiadująco w poziomie |Kliknij przycisk **sąsiadująco w poziomie** toodisplay hello otwartej konsoli windows w formacie kafelka (lub siatki). |
| Rozmieść ikony |Jeśli masz wiele konsoli systemu windows Otwórz i rozproszone na pulpicie zminimalizować je, a następnie kliknij przycisk **Rozmieść ikony** tooarrange ich w rzędzie na powitania dolnej części ekranu. |

### <a name="help-menu"></a>Menu Pomoc
Użyj hello **pomocy** tooview menu dostępna Pomoc online dla programu StorSimple Snapshot Manager i hello programu MMC. Można również wyświetlić informacje o hello MMC i StorSimple Snapshot Manager wersje oprogramowania, które są aktualnie zainstalowane w systemie. 

Dostęp można uzyskać hello **pomocy** menu na pasku menu hello. Tematy pomocy StorSimple Snapshot Manager można także przejść z hello **akcje** okienka.

![Menu Pomoc programu StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpMenu.png)

#### <a name="menu-description"></a>Opis elementu menu
Witaj w poniższej tabeli opisano elementy, które są wyświetlane na powitania menu Pomoc.

| Element menu | Opis |
|:--- |:--- |
| Pomoc na temat programu StorSimple Snapshot Manager |Kliknij przycisk **pomocy na StorSimple Snapshot Manager** tooopen StorSimple Snapshot Manager pomocy w osobnym oknie. |
| Tematy pomocy |Kliknij przycisk **tematy Pomocy** tooopen pomocy online programu MMC w osobnym oknie. |
| Witryna TechCenter |Kliknij przycisk **witryny TechCenter** strony głównej Microsoft TechNet Tech Center hello tooopen w osobnym oknie. |
| Informacje programu Microsoft Management Console |Kliknij przycisk **programu Microsoft Management Console** toosee wersję hello programu Microsoft Management Console jest zainstalowana w Twoim systemie. |
| StorSimple Snapshot Manager |Kliknij przycisk **StorSimple Snapshot Manager** toosee, która wersja przystawki hello jest zainstalowana w Twoim systemie. |

## <a name="tool-bar"></a>Pasek narzędzi
pasek narzędzi Hello, znajduje się poniżej paska menu hello zawiera nawigacji i ikony zadań. Każda z ikon to konkretne zadanie tooa skrótów.

### <a name="icon-descriptions"></a>Ikona opisów
Witaj poniższej tabeli opisano hello ikony, które są wyświetlane na pasku narzędzi hello. 

| Ikona | Opis |
|:--- |:--- |
| ![Strzałka w lewo](./media/storsimple-use-snapshot-manager/HCS_SSM_LeftArrow.png) |Kliknij przycisk hello strzałki w lewo ikona tooreturn toohello poprzedniej strony. |
| ![Strzałka w prawo](./media/storsimple-use-snapshot-manager/HCS_SSM_RightArrow.png) |Kliknij przycisk hello strzałki w prawo toogo toohello następnej strony (jeśli strzałkę hello jest szary, hello akcja jest niedostępna). |
| ![Ikona w dół](./media/storsimple-use-snapshot-manager/HCS_SSM_Up.png) |Kliknij przycisk hello się toogo ikony w górę o jeden poziom w drzewie konsoli hello (hello **zakres** okienko). |
| ![Pokaż/Ukryj drzewo konsoli](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowConsoleTree.png) |Kliknij przycisk hello Pokaż/Ukryj konsoli drzewa ikonę tooshow lub ukrywanie hello **zakres** okienka. |
| ![Wyeksportuj listę](./media/storsimple-use-snapshot-manager/HCS_SSM_ExportListIcon.png) |Kliknij przycisk hello eksportu listy ikony tooexport pliku CSV tooa listy, który określisz. |
| ![Ikona pomocy](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpIcon.png) |Kliknij przycisk tooopen ikonę Pomoc hello online tematu Pomocy programu MMC. |
| ![Pokaż/Ukryj okienka Akcje](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowAction.png) |Kliknij przycisk Pokaż/Ukryj hello **akcje** hello tooshow lub Ukryj ikony okienku **akcje** okienka. |

## <a name="scope-pane"></a>Okienko zakresu
Witaj **zakres** okienko to okienko po lewej stronie powitania w hello StorSimple Snapshot Manager interfejsu użytkownika. Zawiera drzewo konsoli (lub węzeł) hello i hello nawigacji podstawowego mechanizmu StorSimple Snapshot Manager. 

### <a name="scope-pane-structure"></a>Zakres okienka struktury
Witaj **zakres** okienko zawiera szereg obiekty aktywne (węzłów) w strukturze drzewa. 

![Okienko zakresu](./media/storsimple-use-snapshot-manager/HCS_SSM_Scope_pane.png) 

* tooexpand lub Zwiń węzeł, kliknij przycisk hello strzałkę ikona dalej toohello nazwa węzła.
* Stan hello tooview lub zawartość węzła, kliknij nazwę węzła hello. Witaj informacje są wyświetlane w hello **wyniki** okienka. 

Witaj **zakres** okienko zawiera hello następujące węzły: 

* [Węzła urządzenia](#devices-node) 
* [Węzeł woluminów](#volumes-node) 
* [Wolumin węzeł grupy](#volume-groups-node) 
* [Węzeł Zasady tworzenia kopii zapasowej](#backup-policies-node) 
* [Węzeł katalogu kopii zapasowej](#backup-catalog-node) 
* [Węzeł zadania](#jobs-node) 

### <a name="scope-pane-tasks"></a>Zakres okienka zadań
Można użyć hello **zakres** toocomplete okienka akcji w określonym węźle. tooselect zadanie, wykonaj jedną z następujących hello:

* Kliknij prawym przyciskiem myszy węzeł hello, a następnie wybierz zadanie hello wyświetlonym menu hello.
* Kliknij węzeł hello, a następnie kliknij przycisk **akcji** hello paska menu. Wybierz zadanie hello wyświetlonym menu hello.
* Kliknij węzeł hello i wybierz opcję hello akcji w hello **akcje** okienka.

Po wybraniu węzła i użyć dowolnego z tych metod toosee listę zadań, są wyświetlane tylko akcje, które mogą być wykonywane w tym węźle.

### <a name="devices-node"></a>Węzła urządzenia
Witaj **urządzeń** reprezentuje węzeł hello urządzenia StorSimple i urządzenia wirtualnego StorSimple, które są połączone tooStorSimple Snapshot Manager. Wybierz tooconnect tego węzła Konfigurowanie urządzenia i importowanie jej skojarzone woluminy, grup woluminów i istniejące kopie zapasowe. Wiele urządzeń może być połączone tooa jednego hosta.

* węzeł hello tooexpand, kliknij ikonę strzałki hello obok zbyt**urządzeń**.
* toosee menu dostępne akcje, kliknij prawym przyciskiem myszy hello **urządzeń** węzła lub kliknij prawym przyciskiem myszy dowolny z węzłów hello, które są widoczne w hello widok rozszerzony.
* Kliknij toosee listę urządzeń skonfigurowanych **urządzeń** w hello **zakres** okienka. zostanie wyświetlona lista Hello urządzeń, wraz z informacjami o wszystkich urządzeniach w hello **wyniki** okienka.

### <a name="volumes-node"></a>Węzeł woluminów
Witaj **woluminów** reprezentuje węzeł hello dyski, które odpowiadają woluminów toohello zainstalowanych przez hosta hello, łącznie z tymi odnalezione za pomocą inicjatora iSCSI i te odnalezione przez urządzenie. Użyj tej listy hello tooview węzła dostępnych woluminów i przypisanie poszczególnych woluminów toovolume grup.

* węzeł hello tooexpand, kliknij ikonę strzałki hello obok zbyt**woluminów**.
* toosee menu dostępne akcje, kliknij prawym przyciskiem myszy hello **woluminów** węzła lub kliknij prawym przyciskiem myszy dowolny z węzłów hello, które są widoczne w hello widok rozszerzony.
* toosee listę woluminów, kliknij przycisk **woluminów** w hello **zakres** okienka. zostanie wyświetlona lista Hello woluminów, wraz z informacjami o każdym woluminie w hello **wyniki** okienka.

### <a name="volume-groups-node"></a>Wolumin węzeł grupy
Grupy woluminu są nazywane również spójności grup. Każda grupa woluminu jest puli woluminów związanych z aplikacją ułatwia tooensure spójności aplikacji podczas operacji tworzenia kopii zapasowej. Użyj hello **grup woluminu** tooconfigure węzła tych grup i tootake interakcyjne kopii zapasowych lub utworzyć harmonogramy tworzenia kopii zapasowej. 

* węzeł hello tooexpand, kliknij ikonę strzałki hello obok zbyt**grup woluminu**.
* toosee menu dostępne akcje, kliknij prawym przyciskiem myszy hello **grup woluminu** węzła lub kliknij prawym przyciskiem myszy dowolny z węzłów hello, które są widoczne w hello widok rozszerzony.
* toosee listy grup wolumin, kliknij przycisk **grup woluminu** w hello **zakres** okienka. Hello lista grup woluminu, wraz z informacjami o każdej grupy woluminu jest wyświetlana w hello **wyniki** okienka.

### <a name="backup-policies-node"></a>Węzeł Zasady tworzenia kopii zapasowej
Zasady tworzenia kopii zapasowej są harmonogramy zadań dla lokalnych i w chmurze migawki. Użyj hello **zasad tworzenia kopii zapasowych** toospecify węzła częstotliwość tworzenia kopii zapasowej i jak długo kopii zapasowej powinny być zachowywane. 

* węzeł hello tooexpand, kliknij ikonę strzałki hello obok zbyt**zasady tworzenia kopii zapasowej**.
* toosee menu dostępne akcje, kliknij prawym przyciskiem myszy hello **zasady tworzenia kopii zapasowej** węzła lub kliknij prawym przyciskiem myszy dowolny z węzłów hello, które są widoczne w hello widok rozszerzony.
* toosee listę zasad tworzenia kopii zapasowej, kliknij przycisk **zasad tworzenia kopii zapasowych** w hello **zakres** okienka. Lista Hello zasad tworzenia kopii zapasowych, wraz z informacjami na temat poszczególnych zasad, zostanie wyświetlona w hello **wyniki** okienka.

> [!NOTE]
> Można zachować maksymalnie 64 kopie zapasowe.


### <a name="backup-catalog-node"></a>Węzeł katalogu kopii zapasowej
Witaj **katalog kopii zapasowej** węzła zawiera listy lokalnie i w innej lokalizacji kopii zapasowych woluminów Azure StorSimple. Ten węzeł jest zorganizowana według grupy woluminu, a kontener grupy Każdy wolumin zawiera osobne struktur migawki lokalne (hello **migawka lokalna**węzła s) i migawki w chmurze (hello **migawki w chmurze** węzła ). Po rozwinięciu kontenera grupy Każdy wolumin zawiera listę wszystkich hello pomyślnie utworzone kopie zapasowe wykonanych interakcyjnego lub skonfigurowanymi zasadami.

* węzeł hello tooexpand, kliknij ikonę strzałki hello obok zbyt**katalog kopii zapasowej**.
* toosee menu dostępne akcje, kliknij prawym przyciskiem myszy hello **katalog kopii zapasowej** węzła lub kliknij prawym przyciskiem myszy dowolny z węzłów hello, które są widoczne w hello widok rozszerzony.
* toosee listę migawki kopii zapasowej, kliknij przycisk **katalogu kopii zapasowej** w hello **zakres** okienka. zostanie wyświetlona lista Hello migawki, wraz z informacjami o każdej migawki w hello **wyniki** okienka.

### <a name="local-snapshots-node"></a>Lokalny węzeł migawki
Witaj **migawki lokalne** węzła listy migawki lokalne dla określonego woluminu grupy. węzeł Hello znajduje się w obszarze hello **katalog kopii zapasowej** węzła w hello **zakres** okienka. Lokalne migawki są kopie danych woluminu, które są przechowywane na urządzeniu Azure StorSimple hello punktu w czasie. Zazwyczaj ten typ kopii zapasowej można tworzyć i szybko przywrócić. Można użyć migawka lokalna, jak w przypadku lokalnej kopii zapasowej.

* węzeł hello tooexpand, kliknij ikonę strzałki hello obok zbyt**migawki lokalne**.
* toosee menu dostępne akcje, kliknij prawym przyciskiem myszy hello **migawki lokalne** węzła lub kliknij prawym przyciskiem myszy dowolny z węzłów hello, które są widoczne w hello widok rozszerzony.
* toosee listę migawki lokalne, kliknij przycisk **migawki lokalne** w hello **zakres** okienka. zostanie wyświetlona lista Hello migawki, wraz z informacjami o każdej migawki w hello **wyniki** okienka.

### <a name="cloud-snapshots-node"></a>Węzeł migawki w chmurze
Witaj **migawki w chmurze** węzła listy migawki w chmurze dla grupy określonego woluminu. węzeł Hello znajduje się w obszarze hello **katalog kopii zapasowej** węzła w hello **zakres** okienka. Migawki w chmurze są kopie danych woluminu, które są przechowywane w chmurze hello punktu w czasie. Migawka w chmurze jest równoważna migawki tooa replikowane w systemie magazynu innych, poza nim. Migawki w chmurze są szczególnie przydatne w scenariuszach odzyskiwania po awarii.

* węzeł hello tooexpand, kliknij ikonę strzałki hello obok zbyt**migawki w chmurze**.
* toosee menu dostępne akcje, kliknij prawym przyciskiem myszy hello **migawki w chmurze** węzła lub kliknij prawym przyciskiem myszy dowolny z węzłów hello, które są widoczne w hello widok rozszerzony.
* toosee listę migawki w chmurze, kliknij przycisk **migawki w chmurze** w hello **zakres** okienka. zostanie wyświetlona lista Hello migawki, wraz z informacjami o każdej migawki w hello **wyniki** okienka.

### <a name="jobs-node"></a>Węzeł zadania
Witaj **zadania** węzła zawiera informacje o zaplanowanym, uruchamianie i ostatnio wykonanych zadań tworzenia kopii zapasowej. 

* węzeł hello tooexpand, kliknij ikonę strzałki hello obok zbyt**zadania**.
* toosee menu dostępne akcje, kliknij prawym przyciskiem myszy hello **zadania** węzła lub kliknij prawym przyciskiem myszy dowolny z węzłów hello, które są widoczne w hello widok rozszerzony.
* toosee listy zadań zaplanowanych, rozwiń węzeł hello **zadania** węzeł, a następnie kliknij przycisk **zaplanowane**. Witaj wcześniej skonfigurowanych zadań i informacje dotyczące każdego zadania zostanie wyświetlona lista w hello **wyniki** okienka. 
* toosee listy ostatnio wykonanych zadań rozwiń hello **zadania** węzeł, a następnie kliknij przycisk **ostatnich 24 godzin**. Zostanie wyświetlona lista zadań, które zostały ukończone w hello ostatnich 24 godzinach w hello **wyniki** okienka. Witaj **wyniki** okienko zawiera także informacje o każdym zadanie zostało ukończone.
* toosee Lista zadań, które są aktualnie uruchomione, rozwiń węzeł hello **zadania** węzeł, a następnie kliknij przycisk **systemem**. zostanie wyświetlona lista Hello aktualnie uruchomionych zadań i informacje dotyczące każdego zadania w hello **wyniki** okienka.

## <a name="results-pane"></a>W okienku wyników
Witaj **wyniki** okienko jest hello środkowym okienku w hello StorSimple Snapshot Manager interfejsu użytkownika. Zawiera on wyświetla i szczegółowe informacje o stanie dla węzła hello wybranym hello **zakres** okienka.

### <a name="example"></a>Przykład
hello toosee poniższy przykład, kliknij przycisk hello **grup woluminu** węzła w hello **zakres** okienka. Witaj **wyniki** okienku zostanie wyświetlona lista grup woluminu o szczegółowe informacje dotyczące każdej grupy.

![W okienku wyników](./media/storsimple-use-snapshot-manager/HCS_SSM_Results_pane.png) 

Można skonfigurować szczegóły hello pokazano hello **wyniki** okienko: kliknij prawym przyciskiem myszy węzeł w hello **zakres** okienku, kliknij przycisk **widoku**, a następnie kliknij przycisk **Dodaj lub usuń Kolumny**.

## <a name="actions-pane"></a>W okienku Akcje
Witaj **akcje** okienko jest hello w prawym okienku w hello StorSimple Snapshot Manager interfejsu użytkownika. Zawiera menu działań, które mogą wykonywać na powitania węzła, widoku lub dane, które należy wybrać w hello **zakres** okienku lub **wyniki** okienka. Hello **akcje** okienko zawiera polecenia takie same jak hello hello **akcji** menu, które są dostępne dla elementów w hello **zakres** okienko i **wyniki**okienka. Opis akcji, zobacz tabelę hello w hello **akcji** części menu.

### <a name="examples"></a>Przykłady
Poniższy przykład, w hello hello toosee **zakres** okienku rozwiń hello **zadania** węzeł i kliknij przycisk **zaplanowane**. Witaj **akcje** w okienku wyświetlana hello Akcje dostępne dla hello **zaplanowane** węzła.

![Przykład zaplanowanych zadań w okienku Akcje](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane.png) 

Więcej opcji toosee, w hello **zakres** okienku rozwiń hello **zadania** węzła, kliknij przycisk **zaplanowane**, a następnie kliknij przycisk zaplanowane zadanie w hello **wyniki**okienka. Witaj **akcje** okienku wyświetlana hello Akcje dostępne dla hello zaplanowanego zadania, jak pokazano w hello poniższy przykład.

![Przykład działania zadania w okienku Akcje](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

## <a name="keyboard-navigation-and-shortcuts"></a>Skróty i nawigacji klawiatury
StorSimple Snapshot Manager umożliwia hello funkcje ułatwień dostępu systemu operacyjnego Windows hello i hello Microsoft Management Console (MMC). Zawiera także niektóre funkcje nawigacji klawiatury i skrótów, które są określone toohello StorSimple Snapshot Manager zgodnie z opisem w hello następujące sekcje.

* [Klawisze nawigacji](#keyboard-navigation-keys) 
* [Menu paska klawiszy skrótów](#menu-bar-shortcut-keys) 
* [Klawisze skrótów okienka zakresu](#scope-pane-shortcut-keys) 

### <a name="keyboard-navigation-keys"></a>Klawisze nawigacji
Witaj poniższej tabeli opisano klucze hello, których można używać interfejsu użytkownika programu StorSimple Snapshot Manager hello toonavigate. 

| Klucz nawigacji | Akcja |
|:--- |:--- |
| Strzałka w dół |Użyj hello toomove klawiszy Strzałka w dół w pionie toohello następnego elementu menu lub okienka. |
| Wprowadź |Naciśnij klawisz hello Enter klucza toocomplete akcję, a następnie kontynuuj toohello następnego kroku. Można na przykład, naciśnij klawisz Enter tooselect **dalej**, **OK**, lub **Utwórz**, a następnie przejdź toohello następnego kroku w kreatorze. |
| ESC |Naciśnij tooclose klucza Esc hello menu lub toocancel i zamknij stronę. |
| F1 |Naciśnij klawisz hello F1 klucza tooview tematu pomocy dla hello aktualnie aktywne okno. |
| F5 |Naciśnij klawisz hello F5 klucza toorefresh węzła. |
| F6 |Naciśnij klawisz F6 hello klucza toomove z hello **zakres** toohello okienko **wyniki** okienka. |
| F10 |Naciśnij pasek menu toohello hello F10 toogo klucza. |
| Strzałka w lewo |Użyj hello toomove klawiszy Strzałka w lewo poziomo z menu paska opcji toohello poprzedniej opcji. W przypadku przenoszenia toohello poprzedniego zostanie wyświetlone menu elementu hello menu paska, akcja hello (lub kontekstu) dla poprzedniego elementu hello. |
| Klawisz strzałki w prawo |Użyj hello toomove klucza strzałki w prawo w poziomie z jednego paska toohello opcji menu obok. W przypadku przenoszenia pojawi się toohello następnego elementu hello menu paska, akcja hello (lub kontekstu) menu hello nowy element. |
| Klawisz TAB |Okienko hello kartę klucza toomove toohello dalej na powitania konsoli lub toohello dalej zaznaczenie lub pola tekstowego na stronie. |
| Klawisz strzałki w górę |Użyj hello się toomove klawiszy strzałek w pionie toohello poprzedniego elementu menu lub okienka. |

### <a name="menu-bar-shortcut-keys"></a>Menu paska klawiszy skrótów
Witaj poniższej tabeli przedstawiono kombinacje klawiszy skrótu hello hello paska menu. Po naciśnięciu klawiszy skrótów hello i otwiera hello menu, można użyć klawiszy skrótów menu (hello podkreślone klawisze menu hello). Aby uzyskać więcej informacji na temat paska menu hello Przejdź zbyt[paska Menu](#menu-bar).

| Skrót | wynik | Klawisz skrótu w menu | wynik |
|:--- |:--- |:--- |:--- |
| ALT + F |Zostanie otwarta hello **pliku** menu. |N |Otwiera nowe wystąpienie konsoli. |
|  |O |Zostanie otwarta hello **narzędzia administracyjne** strony. | |
|  |S |Zapisuje hello StorSimple Snapshot Manager console. | |
|  |A |Zostanie otwarta hello **Zapisz jako** strony. | |
|  |M |Zostanie otwarta hello **Dodaj/Usuń przystawkę** strony. | |
|  |P |Zostanie otwarta hello **opcje** strony. | |
|  |H |Otwiera Pomoc online. | |
| ALT + A |Zostanie otwarta hello **akcji** menu. |I |Włącza opcję wyświetlania importu hello i wyłącza. |
|  |W |Otwiera nową konsolę programu StorSimple Snapshot Manager. | |
|  |F |Konsola programu StorSimple Snapshot Manager hello aktualizacji. | |
|  |L |Zostanie otwarta hello **Eksportuj listę** strony. | |
|  |H |Otwiera Pomoc online. | |
| ALT + V |Zostanie otwarta hello **widoku** menu. |A |Zostanie otwarta hello **Dodaj/Usuń kolumny** strony. |
|  |U |Zostanie otwarta hello **Dostosuj widok** strony. | |
| ALT + O |Zostanie otwarta hello **ulubione** menu. |A |Zostanie otwarta hello **dodać tooFavorites** strony. |
|  |O |Zostanie otwarta hello **organizowanie ulubionych** strony. | |
| ALT + W |Zostanie otwarta hello **okna** menu. |N |Otwiera inne okno StorSimple Snapshot Manager. |
|  |C |Wyświetla wszystkie okna Otwórz konsolę stylów. | |
|  |T |Wyświetla wszystkie otwarte konsoli systemu windows w układzie siatki. | |
|  |I |Rozmieszcza ikony w rzędzie u dołu ekranu hello. | |
| ALT + H |Zostanie otwarta hello **pomocy** menu. |H |Otwiera Pomoc online. |
|  |T |Otwiera stronę sieci web Microsoft TechNet Tech Center hello. | |
|  |A |Zostanie otwarta hello **programu Microsoft Management Console** strony. | |

### <a name="scope-pane-shortcut-keys"></a>Klawisze skrótów okienka zakresu
Witaj w poniższych tabelach skrótów hello kombinacje klawiszy dla każdego węzła w hello **zakres** okienka. 

* [Klawisze skrótów węzła urządzenia](#devices-node-shortcut-keys)
* [Klawisze skrótów węzła woluminów](#volumes-node-shortcut-keys)
* [Klawisze skrótów węzła grupy woluminu](#volume-groups-node-shortcut-keys)
* [Kopia zapasowa klawiszy skrótów węzła zasad](#backup-policies-node-shortcut-keys)
* [Kopia zapasowa klawiszy skrótów węzła katalogu](#backup-catalog-node-shortcut-keys)
* [Klawisze skrótów węzła zadania](#jobs-node-shortcut-keys)

#### <a name="devices-node-shortcut-keys"></a>Klawisze skrótów węzła urządzenia
| Menu skrótów | wynik |
|:--- |:--- |
| C |Zostanie otwarta hello **Skonfiguruj urządzenie** strony. |
| D |Odświeża listę hello urządzeń i szczegóły urządzenia. |
| V |Zostanie otwarta hello **widoku** menu. |
| W |Otwiera nową konsolę programu StorSimple Snapshot Manager koncentruje się na powitania **szczegóły** węzła. |
| F |Konsola programu StorSimple Snapshot Manager hello aktualizacji. |
| L |Zostanie otwarta hello **Eksportuj listę** strony. |
| H |Otwiera Pomoc online. |

#### <a name="volumes-node-shortcut-keys"></a>Klawisze skrótów węzła woluminów
| Menu skrótów | wynik |
|:--- |:--- |
| V |Aktualizacje hello listę woluminów. |
| V (naciśnij dwa razy) |Zostanie otwarta hello **widoku** menu. |
| W |Otwiera nową konsolę programu StorSimple Snapshot Manager koncentruje się na powitania **woluminów** węzła. |
| F |Konsola programu StorSimple Snapshot Manager hello aktualizacji. |
| L |Zostanie otwarta hello **Eksportuj listę** strony. |
| H |Otwiera Pomoc online. |

#### <a name="volume-groups-node-shortcut-keys"></a>Klawisze skrótów węzła grupy woluminu
| Menu skrótów | wynik |
|:--- |:--- |
| G |Zostanie otwarta hello **Utwórz grupę woluminu** strony. |
| V |Zostanie otwarta hello **widoku** menu. |
| W |Otwiera nową konsolę programu StorSimple Snapshot Manager koncentruje się na powitania **grup woluminu** węzła. |
| F |Konsola programu StorSimple Snapshot Manager hello aktualizacji. |
| L |Zostanie otwarta hello **Eksportuj listę** strony. |
| H |Otwiera Pomoc online. |

#### <a name="backup-policies-node-shortcut-keys"></a>Kopia zapasowa klawiszy skrótów węzła zasad
| Menu skrótów | wynik |
|:--- |:--- |
| B |Zostanie otwarta hello **utworzyć zasadę** strony. |
| V |Zostanie otwarta hello **widoku** menu. |
| W |Otwiera nową konsolę programu StorSimple Snapshot Manager koncentruje się na powitania **grup woluminu** węzła. |
| F |Konsola programu StorSimple Snapshot Manager hello aktualizacji. |
| L |Zostanie otwarta hello ** Eksportuj listę ** strony. |
| H |Otwiera Pomoc online. |

#### <a name="backup-catalog-node-shortcut-keys"></a>Kopia zapasowa klawiszy skrótów węzła katalogu
| Menu skrótów | wynik |
|:--- |:--- |
| W |Otwiera nową konsolę programu StorSimple Snapshot Manager koncentruje się na powitania **grup woluminu** węzła. |
| F |Konsola programu StorSimple Snapshot Manager hello aktualizacji. |
| H |Otwiera Pomoc online. |

#### <a name="jobs-node-shortcut-keys"></a>Klawisze skrótów węzła zadania
| Menu skrótów | wynik |
|:--- |:--- |
| V |Zostanie otwarta hello **widoku** menu. |
| W |Otwiera nową konsolę programu StorSimple Snapshot Manager koncentruje się na powitania **zadania** węzła. |
| F |Konsola programu StorSimple Snapshot Manager hello aktualizacji. |
| L |Zostanie otwarta hello **Eksportuj listę** strony. |
| H |Otwiera Pomoc online |

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[użyć tooadminister StorSimple Snapshot Manager rozwiązania StorSimple](storsimple-snapshot-manager-admin.md).
* Dowiedz się, jak za[Użyj tooconnect StorSimple Snapshot Manager i zarządzanie urządzeniami](storsimple-snapshot-manager-manage-devices.md).

