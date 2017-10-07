---
title: "Szablony przepustowości aaaManage serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toomanage StorSimple przepustowości szablonów, które pozwalają toocontrol przepustowości."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: ebcd1824d7bb9e4c235194c04edbfe8001a3e794
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-bandwidth-templates"></a>Użyj hello Menedżera urządzeń StorSimple usługi toomanage StorSimple przepustowości szablonów

## <a name="overview"></a>Omówienie

Szablony przepustowości umożliwiają wykorzystanie przepustowości sieci tooconfigure przez wiele harmonogramów czasu dnia tootier hello danych z hello chmury toohello urządzenia StorSimple.

Harmonogramy ograniczania przepustowości można:

* Określ harmonogramy niestandardowych przepustowości w zależności od użycia sieci obciążenia hello.
* Scentralizowane zarządzanie i ponowne użycie harmonogramy hello na wielu urządzeniach w sposób łatwy i bezproblemowe.

> [!NOTE]
> Ta funkcja jest dostępna tylko w przypadku urządzenia fizycznego StorSimple (modele 8100 i 8600), a nie urządzenia chmury StorSimple (modele urządzenia 8010 i 8020).


## <a name="hello-bandwidth-templates-blade"></a>Witaj przepustowości szablony bloku

Witaj **szablony przepustowości** bloku wszystkie szablony przepustowości hello usługi w formacie tabelarycznym, a zawiera hello następujących informacji:

* **Nazwa** — nazwa przypisana toohello szablonu przepustowości podczas jej tworzenia.
* **Harmonogram** — Witaj liczba harmonogramów zawarte w szablonie danego przepustowości.
* **Używane przez** — Witaj wiele woluminów za pomocą szablonów przepustowości hello.

Można również znaleźć dodatkowe informacje toohelp Konfigurowanie szablonów przepustowości w:

* [Pytania i odpowiedzi dotyczące przepustowości szablonów](#questions-and-answers-about-bandwidth-templates)
* [Najlepsze rozwiązania dotyczące przepustowości szablonów](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a>Dodaj szablon przepustowości

Wykonaj następujące kroki toocreate nowy szablon przepustowości hello.

#### <a name="tooadd-a-bandwidth-template"></a>tooadd szablonu przepustowości

1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, kliknij przycisk **szablony przepustowości** , a następnie kliknij przycisk **+ Dodaj przepustowości szablonu**.

    ![Kliknij pozycję + Dodaj szablon przepustowości](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. W hello **Dodaj szablon przepustowości** bloku hello następujące kroki:
   
    1. Określ unikatową nazwę dla szablonu przepustowości.
    2. Zdefiniuj harmonogram przepustowości. toocreate harmonogramu:
   
        1. Z listy rozwijanej hello wybierz hello **dni** z hello tygodnia hello harmonogramu jest skonfigurowany dla. Można wybrać kilka dni.        
        
        2. Wprowadź **czas rozpoczęcia** w _gg: mm_ format. Jest to, gdy rozpocznie się hello harmonogramu.

        3. Wprowadź **czas zakończenia** w _gg: mm_ format. Jest to, gdy przestanie hello harmonogramu.
      
           > [!NOTE]
           > Nakładające się harmonogramy nie są dozwolone. Jeśli hello godziny rozpoczęcia i zakończenia spowoduje nakładające się harmonogramu, zobaczysz efekt toothat komunikat błędu.

        4. Określ hello **szybkość przepustowości**. Jest to hello przepustowość w megabitach na sekundę (MB/s) używany przez urządzenia StorSimple w operacji dotyczących chmury hello (przekazywania i pobierania). Wprowadź liczbę z zakresu od 1 do 1000 dla tego pola.

            ![Zdefiniuj harmonogram przepustowości](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            Powtórz hello powyżej kroki toodefine wielu harmonogramów szablonu wszystko będzie gotowe.

        5. Kliknij przycisk **Dodaj** toostart tworzenia szablonu przepustowości. Witaj utworzył szablon jest dodawana toohello listę szablonów przepustowości.
      

## <a name="edit-a-bandwidth-template"></a>Edytuj szablon przepustowości

Wykonaj następujące kroki tooedit szablonu przepustowości hello.

### <a name="tooedit-a-bandwidth-template"></a>tooedit szablonu przepustowości

1. Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **szablony przepustowości**.
2. Hello listy szablonów przepustowości wybierz szablon hello mają toodelete. Kliknij prawym przyciskiem myszy i wybierz z menu kontekstowego hello **usunąć**.
3. Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **OK**. Powinno to usunięcie hello szablonu przepustowości. 
4. Lista Hello przepustowości szablony aktualizacji tooreflect hello usunięcia.

> [!NOTE]
> Nie można zapisać zmiany, w przypadku hello edytowania harmonogramu zachodzi istniejącego harmonogramu w szablonie przepustowości hello, która jest modyfikowana.

## <a name="delete-a-bandwidth-template"></a>Usuń szablon przepustowości

Wykonaj następujące kroki toodelete szablonu przepustowości hello.

#### <a name="toodelete-a-bandwidth-template"></a>toodelete szablonu przepustowości

1. Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **szablony przepustowości**.
2. Hello listy szablonów przepustowości wybierz szablon hello mają toodelete. Kliknij prawym przyciskiem myszy i z menu kontekstowego hello, wybierz opcję Usuń.
3. Po wyświetleniu monitu o potwierdzenie, kliknij przycisk **OK**. Powinno to usunięcie hello szablonu przepustowości.
4. Lista Hello przepustowości szablony aktualizacji tooreflect hello usunięcia.

Jeśli szablon hello jest używany przez wszystkie woluminy, użytkownik nie będzie można toodelete go. Pojawi się komunikat o błędzie wskazujący, że ten szablon hello jest używany. Zostanie wyświetlone okno dialogowe komunikat błędu, udzielanie porad wszystkich hello odwołania toohello szablon powinien zostać usunięty.

Wszystkie hello odwołania toohello szablon, można usunąć po zalogowaniu się do hello **kontenery woluminów** strony i modyfikowanie hello kontenery woluminów, które użyć tego szablonu, aby użyć innego szablonu lub wykorzystanie przepustowości niestandardowych lub nieograniczone ustawienie. Po usunięciu wszystkich odwołań hello, możesz usunąć hello szablonu.

## <a name="use-a-default-bandwidth-template"></a>Użyj domyślnego szablonu przepustowości

Domyślny szablon przepustowości jest dostępne i jest używany przez kontenery woluminów przez kontrolę przepustowości tooenforce domyślne, podczas uzyskiwania dostępu do chmury hello. szablon domyślny Hello służy również jako punkt odniesienia gotowy dla użytkowników, którzy tworzyć własne szablony. Szczegóły Hello tego szablonu domyślnego są:

* **Nazwa** — w nocy nieograniczone, jak i w weekendy
* **Harmonogram** — jeden harmonogram z tooFriday poniedziałek, stosowanym współczynnika przepustowości 1 MB/s miedzy 8 a 17: 00 czasu urządzenia. przepustowość Hello jest ustawiona tooUnlimited pozostałej hello hello tygodnia.

szablon domyślny Hello można edytować. jest śledzony Hello użycia tego szablonu (w tym edytowanej wersji).

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a>Tworzenie szablonu przepustowości całodzienne, która rozpoczyna się od określonego czasu

Postępuj zgodnie z tej procedury toocreate harmonogram, który rozpoczyna się od określonego czasu i uruchamia cały dzień. Przykład Witaj harmonogram hello rozpoczyna się od 9 AM w rano hello i uruchamia do 9 AM hello następnego dnia rano. Jest ważne toonote, który hello rozpoczęcia i zakończenia dla danego planu muszą zarówno być zawarte na powitania sam 24-godzinnym zaplanować i nie może obejmować wiele dni. Jeśli potrzebujesz tooset przepustowości szablonów, które obejmują wiele dni, konieczne będzie toouse wielu harmonogramów (jak pokazano w przykładzie hello).

#### <a name="toocreate-an-all-day-bandwidth-template"></a>toocreate całodzienne szablonu przepustowości

1. Utwórz harmonogram, który rozpoczyna się od 9 AM w rano hello i uruchamia do północy.
2. Dodaj inny harmonogram. Skonfiguruj drugi toorun harmonogram powitania od północy do 9 AM w rano hello.
3. Zapisz szablon przepustowości hello.

Harmonogram złożony Hello będą uruchomione w czasie wybrane i uruchom całodzienne.

## <a name="questions-and-answers-about-bandwidth-templates"></a>Pytania i odpowiedzi dotyczące przepustowości szablonów

**Q**. Co się stanie toobandwidth formantów podczas pracy w zakresie od harmonogramów hello? (Zakończył się zgodnie z harmonogramem i innego nie została jeszcze uruchomiona.)

**A**. W takich przypadkach zostanie zastosowane bez kontroli przepustowości. Oznacza to, że urządzenie hello użyciem przepustowości nieograniczone warstwy toohello danych w chmurze.

**Q**. Czy możesz zmodyfikować szablony przepustowość na urządzeniu w trybie offline?

**A**. Nie będzie toomodify stanie przepustowości szablony na kontenery woluminów Jeśli hello odpowiednie urządzenie jest w trybie offline.

**Q**. Możesz edytować szablon przepustowości skojarzone z kontenera woluminów, gdy hello skojarzone woluminy są w trybie offline?

**A**. Można zmodyfikować szablonu przepustowości skojarzone z kontenera woluminów, których woluminy są w trybie offline. Należy pamiętać, że gdy woluminy są w trybie offline, żadne dane nie będą warstwowy z hello urządzenia toohello chmury.

**Q**. Można usunąć domyślny szablon?

**A**. Mimo że można usunąć szablonu domyślnego, nie jest toodo dobrze tak. Hello użycie szablonu domyślnego, tym edytowanych wersje są śledzone. Hello dane śledzenia są analizowane i za pośrednictwem oczywiście hello czasu jest używane tooimprove hello domyślnego szablonu.

**Q**. Jaki sposób można określić, że szablony przepustowości muszą toobe zmodyfikować?

**A**. Jeden powitalne znaki konieczność toomodify hello przepustowości szablonów jest podczas uruchamiania sieci hello spowolnić lub podlewka wiele razy w ciągu jednego dnia. W takim przypadku monitorowania sieci magazynu i użycia hello analizując hello wykresy wydajności operacji We/Wy i przepustowość sieci.

Z danych o przepływności sieci hello zidentyfikować hello porę dnia, a następnie hello kontenery woluminów, w których hello występuje wąskich gardeł. Jeśli dzieje, gdy dane są warstwowych toohello chmury (uzyskać te informacje z wydajność We/Wy dla wszystkich kontenerów woluminu toocloud urządzenia), musisz wykonać szablonów przepustowości hello toomodify skojarzonych z kontenerów woluminu.

Po zmodyfikowaniu hello szablony są używane, należy toomonitor hello sieci ponownie uzyskać znaczne opóźnienia. Jeśli te nadal istnieje, wymagana będzie toorevisit szablonów przepustowości.

**Q**. Co się stanie, jeśli ma wiele kontenerów wolumin w urządzeniu planuje tego nakładają się na siebie, ale różne limity mają zastosowanie tooeach?

**A**. Załóżmy, że masz urządzenie z 3 kontenery woluminów. Witaj harmonogramy skojarzone z tych kontenerów całkowicie nakładają się. Dla każdego z tych kontenerów limity przepustowości hello używane są 5, 10 lub 15 MB/s odpowiednio. Podczas operacji We/Wy są wykonywane we wszystkich tych kontenerów na powitania, w tym samym czasie, co najmniej hello limity przepustowości hello 3 można stosować: w tym przypadku 5 MB/s one wychodzące udziału żądań We/Wy hello samej kolejki.

## <a name="best-practices-for-bandwidth-templates"></a>Najlepsze rozwiązania dotyczące przepustowości szablonów

Należy stosować następujące najlepsze rozwiązania dla urządzenia StorSimple:

* Konfigurowanie szablonów przepustowości w sieci urządzenia tooenable zmiennej ograniczania przepustowości sieci hello przez urządzenie hello o różnych porach dnia hello. Te szablony przepustowości, gdy jest używany z harmonogramy tworzenia kopii zapasowej można efektywnie wykorzystać dodatkowej przepustowości sieci dla operacji poza godzinami szczytu.
* Oblicz hello rzeczywistej wymaganej dla konkretnego wdrożenia na podstawie rozmiaru hello hello wdrożenia i celu czasu odzyskiwania wymagane hello (RTO) przepustowości.

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

