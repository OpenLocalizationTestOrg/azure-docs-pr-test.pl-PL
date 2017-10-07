---
title: aaaManage katalogu kopii zapasowej StorSimple | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak toouse hello Menedżer StorSimple usługi tworzenia kopii zapasowej wykazu strony toolist, wybierz i Usuń zestawy kopii zapasowych dla woluminu."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a>Użyj toomanage usługi Menedżer StorSimple hello katalogu kopii zapasowej
## <a name="overview"></a>Omówienie
Witaj usługi Menedżer StorSimple **katalogu kopii zapasowej** na stronie są wyświetlane wszystkie zestawy kopii zapasowych hello, tworzonych podczas ręczne lub zaplanowane kopie zapasowe są pobierane. Można użyć toolist tej strony hello Tworzenie wszystkich kopii zapasowych dla zasad tworzenia kopii zapasowej lub na wolumin, wybierz lub usunąć kopie zapasowe, lub użyj kopii zapasowej toorestore lub sklonować woluminu.

W tym samouczku opisano toolist, wybierz i Usuń kopię zapasową konfiguracji. toolearn jak toorestore urządzenia z kopii zapasowej, przejdź zbyt[przywrócenie urządzenia z zestawu kopii zapasowych](storsimple-restore-from-backup-set.md). toolearn jak tooclone woluminu, przejdź zbyt[sklonować woluminu StorSimple](storsimple-clone-volume.md).

![Katalog kopii zapasowej](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

Witaj **katalogu kopii zapasowej** strona zawiera toonarrow zapytania wybór zestawu kopii zapasowych. Można filtrować hello zestawy kopii zapasowych, które są pobierane, oparte na powitania następujące parametry:

* **Urządzenie** — hello urządzenia, na które hello utworzenia zestawu kopii zapasowych.
* **Wykonaj kopię zapasową zasad lub woluminu** — Witaj zasad tworzenia kopii zapasowej lub woluminie skojarzonym z tego zestawu kopii zapasowych.
* **Od i do** — Witaj zakres dat i godzin przy tworzeniu zestawu kopii zapasowych hello.

Witaj filtrowane zestawy kopii zapasowych następnie wyszczególniono w oparciu hello następujące atrybuty:

* **Nazwa** — Witaj nazwę zasad tworzenia kopii zapasowej hello lub woluminie skojarzonym z zestawu kopii zapasowych hello.
* **Rozmiar** — Witaj rzeczywisty rozmiar hello zestawu kopii zapasowych.
* **Utworzone na** — hello Data i godzina utworzenia hello kopii zapasowych. 
* **Typ** — zestawy kopii zapasowych można migawki lokalne lub migawki w chmurze. Migawka lokalna jest kopię zapasową wszystkich danych woluminu przechowywane lokalnie na urządzeniu hello toohello tworzenia kopii zapasowych danych woluminu znajdującej się w chmurze hello odwołuje się migawka w chmurze. Migawki lokalne zapewnić szybszy dostęp migawki w chmurze są wybrać, aby zachować odporność danych.
* **Zainicjowane przez** — kopie zapasowe hello może zostać zainicjowane automatycznie według harmonogramu lub ręcznie przez użytkownika. Możesz użyć kopii zapasowych tooschedule zasad tworzenia kopii zapasowej. Alternatywnie można użyć hello **utworzenia kopii zapasowej** tootake opcji ręcznego tworzenia kopii zapasowej.

## <a name="list-backup-sets-for-a-volume"></a>Zestawy kopii zapasowych listy woluminu
Wykonaj następujące kroki toolist hello wszystkie kopie zapasowe hello woluminu.

#### <a name="toolist-backup-sets"></a>zestawy kopii zapasowych toolist
1. Na stronie usługi Menedżer StorSimple powitania kliknij hello **katalog kopii zapasowej** kartę.
2. Filtrować hello wybory w następujący sposób:
   
   1. Wybierz odpowiednie urządzenie hello.
   2. Z listy rozwijanej hello wybierz tooview woluminu kopii zapasowych hello odpowiedniego hello.
   3. Określ zakres czasu hello.
   4. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute tego zapytania.
      
      kopie zapasowe Hello skojarzone z woluminu hello wybrane powinna pojawić się na liście hello zestawów kopii zapasowych.

## <a name="select-a-backup-set"></a>Wybierz zestaw kopii zapasowych
Zakończenie hello następujące kroki tooselect kopii zapasowej ustawienie zasad woluminu lub kopii zapasowej.

#### <a name="tooselect-a-backup-set"></a>tooselect zestawu kopii zapasowych
1. Na stronie usługi Menedżer StorSimple powitania kliknij hello **katalog kopii zapasowej** kartę.
2. Filtrować hello wybory w następujący sposób:
   
   1. Wybierz odpowiednie urządzenie hello.
   2. Z listy rozwijanej hello wybierz hello zasad woluminu lub kopii zapasowej do utworzenia kopii zapasowej hello czy tooselect.
   3. Określ zakres czasu hello.
   4. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute tego zapytania.
      
      Hello kopii zapasowych skojarzonych z zasadami hello wybrany wolumin lub kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych.
3. Wybierz i rozwiń zestawu kopii zapasowych. Witaj **przywrócić** i **usunąć** opcje są wyświetlane u dołu hello hello strony. Każda z tych akcji można wykonywać na powitania zestawu kopii zapasowych wybrany.

## <a name="delete-a-backup-set"></a>Usuń zestaw kopii zapasowych
Usunięcie kopii zapasowej, jeśli nie chcesz już tooretain hello danych skojarzonych z nim. Wykonaj następujące kroki toodelete zestawu kopii zapasowych hello.

#### <a name="toodelete-a-backup-set"></a>toodelete zestawu kopii zapasowych
1. Na stronie usługi Menedżer StorSimple powitania kliknij hello **kartę katalog kopii zapasowej**.
2. Filtrować hello wybory w następujący sposób:
   
   1. Wybierz odpowiednie urządzenie hello.
   2. Z listy rozwijanej hello wybierz hello zasad woluminu lub kopii zapasowej do utworzenia kopii zapasowej hello czy tooselect.
   3. Określ zakres czasu hello.
   4. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute tego zapytania.
      
      Hello kopii zapasowych skojarzonych z zasadami hello wybrany wolumin lub kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych.
3. Wybierz i rozwiń zestawu kopii zapasowych. Witaj **przywrócić** i **usunąć** opcje są wyświetlane u dołu hello hello strony. Kliknij polecenie **Usuń**.
4. Podczas usuwania hello jest w toku i zostało pomyślnie zakończone, otrzymasz powiadomienie. Po usunięciu hello jest wykonywana, odśwież zapytanie hello na tej stronie. zestaw kopii zapasowych Hello usunięte nie będzie dłużej widoczny na liście hello zestawów kopii zapasowych.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[Użyj hello toorestore katalogu kopii zapasowej urządzenia z zestawu kopii zapasowych](storsimple-restore-from-backup-set.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

