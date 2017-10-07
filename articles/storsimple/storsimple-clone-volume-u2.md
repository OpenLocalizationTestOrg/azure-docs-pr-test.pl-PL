---
title: aaaClone woluminu serii StorSimple 8000 | Dokumentacja firmy Microsoft
description: "Zawiera opis hello klonowania różnych typów i kiedy toouse oraz wyjaśniono, jak używasz tooclone zestawu kopii zapasowych poszczególnych woluminów."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: f457625d2e3aa173f7ccf26984e1902a64e33b5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume-update-2"></a>Użyj tooclone usługi Menedżer StorSimple hello woluminu (Update 2)
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Omówienie
Witaj usługi Menedżer StorSimple **katalogu kopii zapasowej** na stronie są wyświetlane wszystkie zestawy kopii zapasowych hello, które są tworzone podczas ręczne lub automatyczne kopie zapasowe są pobierane. Można użyć toolist tej strony hello Tworzenie wszystkich kopii zapasowych dla zasad tworzenia kopii zapasowej lub na wolumin, wybierz lub usunąć kopie zapasowe, lub użyj kopii zapasowej toorestore lub sklonować woluminu.

![Strona katalogu kopii zapasowej](./media/storsimple-clone-volume-u2/backupCatalog.png)  

W tym samouczku opisano, jak używasz tooclone zestawu kopii zapasowych poszczególnych woluminów. Wyjaśniono również hello różnica między *przejściowa* i *stałe* klonów.

> [!NOTE]
> Jako wolumin warstwowy zostaną sklonowane woluminu przypiętego lokalnie. Jeśli konieczne hello toobe sklonowany wolumin przypięty lokalnie, możesz przekonwertować wolumin przypięty lokalnie tooa klonowania hello po pomyślnym zakończeniu operacji klonowania hello. Przejdź do informacji na temat konwertowania tooa wolumin warstwowy, który jest lokalnie przypięty woluminu, zbyt[zmienić typ woluminu hello](storsimple-manage-volumes-u2.md#change-the-volume-type).
> 
> Jeśli spróbujesz tooconvert, który wolumin sklonowany z warstwową toolocally przypięty natychmiast po zakończeniu klonowania (gdy nadal jest przejściowy klonowania), Niepowodzenie konwersji hello hello następujący komunikat o błędzie:
> 
> `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.` 
> 
> To jest błąd tylko wtedy, gdy są klonowania na innym urządzeniu tooa. Pomyślnie przekonwertować hello toolocally wolumin przypięty, jeśli najpierw przekonwertuj hello przejściowej klonowania tooa stałe klonowania. tooconvert hello przejściowej klonowania tooa stałe klonowania, Utwórz migawkę chmury go.
> 
> 

## <a name="create-a-clone-of-a-volume"></a>Tworzenie własnego klonu woluminu
Można utworzyć klona na hello tego samego urządzenia, innego urządzenia lub nawet maszynę wirtualną za pomocą lokalnie lub w chmurze migawki.

#### <a name="tooclone-a-volume"></a>tooclone woluminu
1. Na stronie usługi Menedżer StorSimple powitania kliknij hello **katalog kopii zapasowej** i wybierz zestaw kopii zapasowych.
2. Rozwiń hello zestawu kopii zapasowych tooview hello skojarzonych woluminów. Kliknij i wybierz wolumin z zestawu kopii zapasowych hello.
   
     ![Klonowanie woluminu](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. Kliknij przycisk **klonowania** toobegin w klonowania hello wybrany wolumin.
4. W Kreatorze woluminu w klonowania hello w obszarze **Określ nazwę i lokalizację**:
   
   1. Określ urządzenia docelowego. To jest lokalizacja hello której zostanie utworzona hello klonowania. Można wybrać hello tego samego urządzenia lub określ inne urządzenie. Jeśli wybierzesz woluminu skojarzony z innym dostawcom usług w chmurze hello (nie Azure), listy rozwijanej liście dla urządzenia docelowego hello zostaną wyświetlone tylko fizyczne urządzenia. Nie można sklonować woluminu skojarzony z innym dostawcom usług w chmurze na urządzeniu wirtualnym.
      
      > [!NOTE]
      > Upewnij się, że pojemność hello wymagane do klonowania hello jest starsza niż hello o pojemności hello urządzenia docelowego.
      > 
      > 
   2. Określ nazwę unikatową woluminu z klonu. Nazwa Hello musi zawierać od 3 do 127 znaków. 
      
      > [!NOTE]
      > Witaj **klonowania woluminu jako** pole będzie **warstwowego** nawet wtedy, gdy są klonowania woluminu przypiętego lokalnie. Nie można zmienić to ustawienie; Jednak jeśli konieczne hello toobe sklonowany wolumin przypięty lokalnie również, można przekonwertować wolumin przypięty lokalnie tooa klonowania powitania po utworzeniu hello klonowania. Przejdź do informacji na temat konwertowania tooa wolumin warstwowy, który jest lokalnie przypięty woluminu, zbyt[zmienić typ woluminu hello](storsimple-manage-volumes-u2.md#change-the-volume-type).
      > 
      > 
      
        ![Kreator klonowania 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. Kliknij ikonę strzałki hello ![ikona strzałki](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) tooproceed toohello następnej strony.
5. W obszarze **określić hosty, na których można korzystać z tego woluminu**:
   
   1. Określ rekord kontroli dostępu (ACR) dla hello klonowania. Można dodawać nowe ACR lub wybierz z listy istniejących hello.
      
        ![Kreator klonowania 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. Kliknij ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)Operacja hello toocomplete.
6. Zadanie klonowania zostanie rozpoczęte i użytkownik zostanie powiadomiony, gdy hello klonowania została pomyślnie utworzona. Kliknij przycisk **zadania** zadania w klonowania hello toomonitor na powitania **zadania** strony. Zostanie wyświetlony hello następującą wiadomości, po zakończeniu zadania sklonowany hello:
   
    ![Komunikat w klonowania](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. Po hello ukończenia zadania w klonowania:
   
   1. Przejdź toohello **urządzeń** strony i wybierz hello **kontenery woluminów** kartę. 
   2. Wybierz kontener woluminów hello skojarzony z hello woluminu źródłowego, który można sklonować. Na liście hello woluminów powinna zostać wyświetlona hello klonowania, który został właśnie utworzony.

> [!NOTE]
> Monitorowanie i domyślnego tworzenia kopii zapasowej są automatycznie wyłączane na sklonowanym woluminie.
> 
> 

Sklonowany, która jest tworzona w ten sposób jest przejściowy klonowania. Aby uzyskać więcej informacji na temat typów w klonowania, zobacz [przejściowej a stałe klony](#transient-vs-permanent-clones).

Tego klonu jest teraz regularne woluminu, a żadnej operacji dostępnego na woluminie będą dostępne dla hello klonowania. Konieczne będzie tooconfigure ten wolumin do wszelkich kopii zapasowych.

## <a name="transient-vs-permanent-clones"></a>Przejściowy a klony stałych
Przejściowa klony są tworzone tylko wtedy, gdy są klonowania tooa innego urządzenia. Można sklonować określonego woluminu z zestawu kopii zapasowych tooa innego urządzenia zarządzane przez hello Menedżer StorSimple. klonowania przejściowej Hello będzie zawiera dane toohello odwołania do oryginalnego woluminu hello będzie używać tego tooread danych i zapisywać lokalnie na urządzeniu docelowym hello. 

Po wykonaniu migawkę chmury w klonowania przejściowej hello klonowania wynikowy będzie *stałe* klonowania. W trakcie tego procesu kopii danych hello jest tworzony w chmurze hello hello toocopy czasu, tych danych jest określany przez rozmiar hello hello danych i hello Azure opóźnienia (jest to kopia Azure do platformy Azure). Ten proces może potrwać tooweeks dni. sklonowany przejściowej Hello staje się stałe klonowania w ten sposób i nie zawiera odwołania do toohello oryginalnego woluminu danych, który został sklonowany z. 

## <a name="scenarios-for-transient-and-permanent-clones"></a>Scenariusze dotyczące klony przejściowych i stałe
Witaj następujące sekcje opisują przykład sytuacji, w których można użyć klony przejściowych i stałe.

### <a name="item-level-recovery-with-a-transient-clone"></a>Odzyskiwanie na poziomie elementu przejściowej klonu
Należy toorecover plik prezentacji programu Microsoft PowerPoint co roku tygodniowych. IT administrator identyfikuje hello kopii zapasowej z tego przedziału czasu i następnie filtry hello woluminu. Hello administrator, a następnie klonuje wolumin hello, lokalizuje plik hello szukasz i dostarcza mu tooyou. W tym scenariuszu jest używana przejściowej klonowania. 

![Zobacz film](./media/storsimple-clone-volume-u2/Video_icon.png) **Zobacz film**

toowatch film wideo przedstawiający sposób Użyj klonowania hello i przywracania funkcji w plikach toorecover usunięte StorSimple, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Testowanie w środowisku produkcyjnym hello stałe klonu
Należy tooverify usterki testowania w środowisku produkcyjnym hello. Tworzenie własnego klonu hello woluminu w środowisku produkcyjnym hello i wykonaj migawkę chmury dla tego klonu toocreate niezależne sklonowany woluminu. W tym scenariuszu stały klonowania jest używany.  

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[przywracania woluminu StorSimple z zestawu kopii zapasowych](storsimple-restore-from-backup-set-u2.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

