---
title: aaaClone woluminu z serii StorSimple 8000 | Dokumentacja firmy Microsoft
description: "Zawiera opis hello klonowania różne typy i użycia i wyjaśniono, jak można użyć tooclone zestawu kopii zapasowych poszczególnych woluminów na urządzeniu z serii StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a>Użyj usługi Menedżer StorSimple urządzenia hello w tooclone portalu Azure woluminu

## <a name="overview"></a>Omówienie

W tym samouczku opisano, jak używasz tooclone zestawu kopii zapasowych poszczególnych woluminów za pomocą hello **katalog kopii zapasowej** bloku. Wyjaśniono również hello różnica między *przejściowa* i *stałe* klonów. wskazówki dotyczące Hello w tym samouczku dotyczy urządzenia z serii StorSimple 8000 hello tooall uruchomioną aktualizacją 3 lub nowszym.

Witaj usługi Menedżer StorSimple urządzenia **katalog kopii zapasowej** bloku Wyświetla wszystkie zestawy kopii zapasowych hello, które są tworzone podczas ręczne lub automatyczne kopie zapasowe są pobierane. Następnie możesz wybrać wolumin w tooclone zestawu kopii zapasowych.

 ![Listy zestawu kopii zapasowych](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a>Zagadnienia dotyczące klonowania woluminu

Należy wziąć pod uwagę hello następujących informacji w przypadku klonowania woluminu.

- Klon zachowuje się tak hello sam sposób jak regularne woluminu. Wszelkie operacje dostępnego na woluminie jest dostępna dla hello klonowania.

- Monitorowanie i domyślnego tworzenia kopii zapasowej są automatycznie wyłączane na sklonowanym woluminie. Będzie potrzebny tooconfigure woluminu sklonowany żadnych kopii zapasowych.

- Wolumin przypięty lokalnie jest sklonować jako woluminu warstwowego. Jeśli konieczne hello toobe sklonowany wolumin przypięty lokalnie, możesz przekonwertować wolumin przypięty lokalnie tooa klonowania hello po pomyślnym zakończeniu operacji klonowania hello. Przejdź do informacji na temat konwertowania tooa wolumin warstwowy, który jest lokalnie przypięty woluminu, zbyt[zmienić typ woluminu hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).

- Jeśli spróbujesz tooconvert, który wolumin sklonowany z warstwową toolocally przypięty natychmiast po zakończeniu klonowania (gdy nadal jest przejściowy klonowania), konwersja hello kończy się niepowodzeniem z hello następujący komunikat o błędzie:

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    To jest błąd tylko wtedy, gdy są klonowania na innym urządzeniu tooa. Pomyślnie przekonwertować hello toolocally wolumin przypięty, jeśli najpierw przekonwertuj hello przejściowej klonowania tooa stałe klonowania. Utwórz migawkę chmury tooconvert przejściowej klonowania hello go tooa stałe klonowania.

## <a name="create-a-clone-of-a-volume"></a>Tworzenie własnego klonu woluminu

Można utworzyć klona na hello tego samego urządzenia, innego urządzenia lub nawet urządzenia do chmury przy użyciu lokalnej lub w chmurze migawki.

w poniższej procedurze Hello opisano, jak toocreate klonowania z hello kopii zapasowej wykazu.  Klonowanie tooinitiate alternatywną metodą jest zbyt toogo**woluminów**, wybierz wolumin, a następnie kliknij prawym przyciskiem myszy menu kontekstowe hello tooinvoke i wybierz **klonowania**.

Wykonaj następujące kroki toocreate w klonowania woluminu z katalogu kopii zapasowej hello hello.

#### <a name="tooclone-a-volume"></a>tooclone woluminu

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie kliknij przycisk **katalog kopii zapasowej**.

2. Wybierz kopię zapasową ustawione w następujący sposób:
   
   1. Wybierz odpowiednie urządzenie hello.
   2. Z listy rozwijanej hello wybierz hello zasad woluminu lub kopii zapasowej do utworzenia kopii zapasowej hello czy tooselect.
   3. Określ zakres czasu hello.
   4. Kliknij przycisk **Zastosuj** tooexecute tego zapytania.

    Hello kopii zapasowych skojarzonych z zasadami hello wybrany wolumin lub kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych.
   
    ![Listy zestawu kopii zapasowych](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. Rozwiń hello zestawu kopii zapasowych tooview hello skojarzonych woluminów. Te woluminy muszą być pobierane w trybie offline na hoście hello i urządzenia, zanim będzie można ich przywrócić. Dostęp do woluminów hello na powitania **woluminów** bloku urządzenia i następnie hello wykonaj kroki opisane w temacie [Przełącz do trybu offline wolumin](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake ich w tryb offline.
   
   > [!IMPORTANT]
   > Upewnij się, czy wykonano woluminów hello w tryb offline na hoście hello najpierw, przed podjęciem dalszych na urządzeniu hello hello woluminy w trybie offline. W przypadku niepodjęcia hello woluminy w tryb offline na hoście hello potencjalnie spowodować uszkodzenie toodata.
   
4. Przejdź wstecz toohello **katalog kopii zapasowej** i wybrać wolumin w zestawie kopii zapasowych. Kliknij prawym przyciskiem myszy, a następnie z menu kontekstowego hello, wybierz **klonowania**.

   ![Listy zestawu kopii zapasowych](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. W hello **klonowania** bloku hello następujące kroki:
   
    1. Określ urządzenia docelowego. To jest lokalizacja hello której zostanie utworzona hello klonowania. Można wybrać hello tego samego urządzenia lub określ inne urządzenie.

      > [!NOTE]
      > Upewnij się, że pojemność hello wymagane do klonowania hello jest starsza niż hello o pojemności hello urządzenia docelowego.
       
    2. Określ nazwę unikatową woluminu z klonu. Nazwa Hello musi zawierać od 3 do 127 znaków.
      
        > [!NOTE]
        > Witaj **klonowania woluminu jako** pole będzie **warstwowego** nawet wtedy, gdy są klonowania woluminu przypiętego lokalnie. Nie można zmienić to ustawienie; Jednak jeśli konieczne hello toobe sklonowany wolumin przypięty lokalnie również, można przekonwertować wolumin przypięty lokalnie tooa klonowania powitania po utworzeniu hello klonowania. Przejdź do informacji na temat konwertowania tooa wolumin warstwowy, który jest lokalnie przypięty woluminu, zbyt[zmienić typ woluminu hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).
          
    3. W obszarze **połączone hosty**, określ rekord kontroli dostępu (ACR) dla hello klonowania. Można dodawać nowe ACR lub wybierz z listy istniejących hello. Hello ACR określi, które hosty mogą uzyskiwać dostęp do tego klonu.
      
        ![Listy zestawu kopii zapasowych](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. Kliknij przycisk **klonowania** toocomplete hello operacji.

4. Zadanie klonowania jest inicjowane i użytkownik jest powiadamiany o hello klonowania została pomyślnie utworzona. Kliknij powiadomienie o zadaniu hello lub przejść za**zadania** bloku toomonitor hello klonowania zadania.

    ![Listy zestawu kopii zapasowych](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. Po zakończeniu zadania sklonowany hello Przejdź tooyour urządzenia, a następnie kliknij przycisk **woluminów**. W hello listę woluminów, powinna zostać wyświetlona hello klonowania, która właśnie została utworzona w hello sam kontener woluminu, który ma hello woluminu źródłowego.

    ![Listy zestawu kopii zapasowych](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

Sklonowany, która jest tworzona w ten sposób jest przejściowy klonowania. Aby uzyskać więcej informacji na temat typów w klonowania, zobacz [przejściowej a stałe klony](#transient-vs-permanent-clones).


## <a name="transient-vs-permanent-clones"></a>Przejściowy a klony stałych
Przejściowa klony są tworzone tylko wtedy, gdy w klonowania tooanother urządzenia. Można sklonować określonego woluminu z zestawu kopii zapasowych tooa innego urządzenia zarządzane przez hello Menedżera urządzeń StorSimple. Hello przejściowej klonu ma danych toohello odwołania w hello oryginalnego woluminu i używa tego tooread danych i zapisu lokalnie na urządzeniu docelowym hello.

Po wykonaniu migawkę chmury w klonowania przejściowej klon wynikowy hello jest *stałe* klonowania. W trakcie tego procesu kopii danych hello jest tworzony w chmurze hello hello toocopy czasu, tych danych jest określany przez rozmiar hello hello danych i hello Azure opóźnienia (jest to kopia Azure do platformy Azure). Ten proces może potrwać tooweeks dni. klonowania przejściowej Hello staje się klonowania stałe i nie zawiera odwołania do toohello oryginalnego woluminu danych, który został sklonowany z.

## <a name="scenarios-for-transient-and-permanent-clones"></a>Scenariusze dotyczące klony przejściowych i stałe
Witaj następujące sekcje opisują przykład sytuacji, w których można użyć klony przejściowych i stałe.

### <a name="item-level-recovery-with-a-transient-clone"></a>Odzyskiwanie na poziomie elementu przejściowej klonu
Należy toorecover plik prezentacji programu Microsoft PowerPoint co roku tygodniowych. Administratora IT identyfikuje hello kopii zapasowej z tego czasu, a następnie filtry hello woluminu. Hello administrator, a następnie klonuje wolumin hello, lokalizuje plik hello szukasz i dostarcza mu tooyou. W tym scenariuszu jest używana przejściowej klonowania.

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Testowanie w środowisku produkcyjnym hello stałe klonu
Należy tooverify usterki testowania w środowisku produkcyjnym hello. Tworzenie własnego klonu hello woluminu w środowisku produkcyjnym hello i wykonaj migawkę chmury dla tego klonu toocreate niezależne sklonowany woluminu. W tym scenariuszu stały klonowania jest używany.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[przywracania woluminu StorSimple z zestawu kopii zapasowych](storsimple-8000-restore-from-backup-set-u2.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

