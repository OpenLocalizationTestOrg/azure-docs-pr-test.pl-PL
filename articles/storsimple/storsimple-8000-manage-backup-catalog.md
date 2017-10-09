---
title: aaaManage katalogu kopii zapasowej StorSimple | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak hello toouse toolist strony katalogu kopii zapasowej usługi Menedżera urządzeń StorSimple, wybierz i Usuń zestawy kopii zapasowych."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a>Użyj toomanage usługi Menedżer StorSimple urządzenia hello katalogu kopii zapasowej
## <a name="overview"></a>Omówienie
Witaj usługi Menedżer StorSimple urządzenia **katalogu kopii zapasowej** bloku Wyświetla wszystkie zestawy kopii zapasowych hello, tworzonych podczas ręczne lub zaplanowane kopie zapasowe są pobierane. Można użyć toolist tej strony hello Tworzenie wszystkich kopii zapasowych dla zasad tworzenia kopii zapasowej lub na wolumin, wybierz lub usunąć kopie zapasowe, lub użyj kopii zapasowej toorestore lub sklonować woluminu.

W tym samouczku opisano toolist, wybierz i Usuń kopię zapasową konfiguracji. toolearn jak toorestore urządzenia z kopii zapasowej, przejdź zbyt[przywrócenie urządzenia z zestawu kopii zapasowych](storsimple-8000-restore-from-backup-set-u2.md). toolearn jak tooclone woluminu, przejdź zbyt[sklonować woluminu StorSimple](storsimple-8000-clone-volume-u2.md).

![Katalog kopii zapasowej](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

Witaj **katalogu kopii zapasowej** bloku zapewnia toonarrow zapytania wybór zestawu kopii zapasowych. Można filtrować hello zestawy kopii zapasowych, które są pobierane, oparte na powitania następujące parametry:

* **Urządzenie** — hello urządzenia, na które hello utworzenia zestawu kopii zapasowych.
* **Zasady tworzenia kopii zapasowej lub woluminie** — Witaj zasad tworzenia kopii zapasowej lub woluminie skojarzonym z tego zestawu kopii zapasowych.
* **Od i do** — Witaj zakres dat i godzin przy tworzeniu zestawu kopii zapasowych hello.

Witaj filtrowane zestawy kopii zapasowych następnie wyszczególniono w oparciu hello następujące atrybuty:

* **Nazwa** — Witaj nazwę zasad tworzenia kopii zapasowej hello lub woluminie skojarzonym z zestawu kopii zapasowych hello.
* **Rozmiar** — Witaj rzeczywisty rozmiar hello zestawu kopii zapasowych.
* **Utworzone na** — hello Data i godzina utworzenia hello kopii zapasowych. 
* **Typ** — zestawy kopii zapasowych można migawki lokalne lub migawki w chmurze. Migawka lokalna jest kopię zapasową wszystkich danych woluminu przechowywane lokalnie na urządzeniu hello toohello tworzenia kopii zapasowych danych woluminu znajdującej się w chmurze hello odwołuje się migawka w chmurze. Migawki lokalne zapewnić szybszy dostęp migawki w chmurze są wybrać, aby zachować odporność danych.
* **Zainicjowane przez** — kopie zapasowe hello może zostać zainicjowane automatycznie według harmonogramu lub ręcznie przez użytkownika. Możesz użyć kopii zapasowych tooschedule zasad tworzenia kopii zapasowej. Alternatywnie można użyć hello **utworzenia kopii zapasowej** tootake opcji ręcznego tworzenia kopii zapasowej.

## <a name="list-backup-sets-for-a-backup-policy"></a>Zestawy kopii zapasowych listy dla zasad tworzenia kopii zapasowej
Wykonaj następujące kroki toolist hello wszystkie kopie zapasowe hello zasad tworzenia kopii zapasowej.

#### <a name="toolist-backup-sets"></a>zestawy kopii zapasowych toolist
1. Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **katalog kopii zapasowej**.

2. Filtrować hello wybory w następujący sposób:
   
   1. Określ zakres czasu hello.
   2. Wybierz odpowiednie urządzenie hello.
   3. Filtruj według **kopii zapasowej zasad** tooview hello odpowiedniego hello kopii zapasowych.
   3. Z listy rozwijanej zasad tworzenia kopii zapasowej hello, wybierz **wszystkie** tooview hello wszystkie kopie zapasowe na powitania wybrane urządzenia.
   4. Kliknij przycisk **Zastosuj** tooexecute tego zapytania.
      
      kopie zapasowe Hello skojarzonych z zasadami tworzenia kopii zapasowej hello wybrane powinna pojawić się na liście hello zestawów kopii zapasowych.

      ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a>Wybierz zestaw kopii zapasowych
Zakończenie hello następujące kroki tooselect kopii zapasowej ustawienie zasad woluminu lub kopii zapasowej.

#### <a name="tooselect-a-backup-set"></a>tooselect zestawu kopii zapasowych
1. Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **katalog kopii zapasowej**.
2. Filtrować hello wybory w następujący sposób:
   
   1. Określ zakres czasu hello. 
   2. Wybierz odpowiednie urządzenie hello. 
   3. Filtruj według zasad woluminu lub kopii zapasowej dla kopii zapasowej hello, że chcesz tooselect.
   4. Kliknij przycisk **Zastosuj** tooexecute tego zapytania.
      
      Hello kopii zapasowych skojarzonych z zasadami hello wybrany wolumin lub kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych.

      ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Wybierz i rozwiń zestawu kopii zapasowych. Możesz teraz przeglądać hello zestawy kopii zapasowych według hello woluminów, które zawiera. Witaj **przywrócić** i **usunąć** opcje są dostępne za pośrednictwem menu kontekstowe hello (kliknij prawym przyciskiem myszy) dla hello zestawu kopii zapasowych. Każda z tych akcji można wykonywać na powitania zestawu kopii zapasowych wybrany.

    ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a>Usuń zestaw kopii zapasowych
Usunięcie kopii zapasowej, jeśli nie chcesz już tooretain hello danych skojarzonych z nim. Wykonaj następujące kroki toodelete zestawu kopii zapasowych hello.

#### <a name="toodelete-a-backup-set"></a>toodelete zestawu kopii zapasowych
 Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **katalog kopii zapasowej**.
2. Filtrować hello wybory w następujący sposób:
   
   1. Określ zakres czasu hello. 
   2. Wybierz odpowiednie urządzenie hello. 
   3. Filtruj według zasad woluminu lub kopii zapasowej dla kopii zapasowej hello, że chcesz tooselect.
   4. Kliknij przycisk **Zastosuj** tooexecute tego zapytania.
      
      Hello kopii zapasowych skojarzonych z zasadami hello wybrany wolumin lub kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych.

      ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. Wybierz i rozwiń zestawu kopii zapasowych. Możesz teraz przeglądać hello zestawy kopii zapasowych według hello woluminów, które zawiera. Witaj **przywrócić** i **usunąć** opcje są dostępne za pośrednictwem menu kontekstowe hello (kliknij prawym przyciskiem myszy) dla hello zestawu kopii zapasowych. Kliknij prawym przyciskiem myszy wybrane hello zestawu kopii zapasowych i wybierz z menu kontekstowego hello **usunąć**.

    ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. Po wyświetleniu monitu o potwierdzenie, przejrzyj informacje wyświetlane hello i kliknij przycisk **usunąć**. Witaj wybranej kopii zapasowej jest trwale usunięte.

    ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. Podczas usuwania hello jest w toku i zostało pomyślnie zakończone, otrzymasz powiadomienie. Po usunięciu hello jest wykonywana, odśwież zapytanie hello na tej stronie. zestaw kopii zapasowych Hello usunięte nie będzie dłużej widoczny na liście hello zestawów kopii zapasowych.

    ![Przejdź do katalogu toobackup](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[Użyj hello toorestore katalogu kopii zapasowej urządzenia z zestawu kopii zapasowych](storsimple-8000-restore-from-backup-set-u2.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

