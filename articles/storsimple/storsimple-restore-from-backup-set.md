---
title: aaaRestore woluminu StorSimple z kopii zapasowej | Dokumentacja firmy Microsoft
description: "W tym artykule wyjaśniono, jak toouse hello toorestore strony katalogu kopii zapasowej usługi Menedżer StorSimple woluminu StorSimple z zestawu kopii zapasowych."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Przywracania woluminu StorSimple z zestawu kopii zapasowych
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Omówienie
Witaj **katalogu kopii zapasowej** na stronie są wyświetlane wszystkie zestawy kopii zapasowych hello, które są tworzone podczas ręczne lub automatyczne kopie zapasowe są pobierane. Można użyć toolist tej strony hello Tworzenie wszystkich kopii zapasowych dla zasad tworzenia kopii zapasowej lub na wolumin, wybierz lub usunąć kopie zapasowe, lub użyj kopii zapasowej toorestore lub sklonować woluminu.

 ![Strona katalogu kopii zapasowej](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

Ten samouczek wyjaśnia sposób toouse hello **katalogu kopii zapasowej** strony toorestore woluminu na urządzeniu z zestawu kopii zapasowych.

## <a name="how-toouse-hello-backup-catalog"></a>Jak toouse hello katalogu kopii zapasowej
Witaj **katalogu kopii zapasowej** strona zawiera zapytanie, które pomaga toonarrow wybór zestawu kopii zapasowych. Można filtrować hello zestawy kopii zapasowych pobieranych oparte na powitania następujące parametry:

* **Urządzenie** — hello urządzenia, na które hello utworzenia zestawu kopii zapasowych.
* **Wykonaj kopię zapasową zasad** lub **woluminu** — Witaj zasad tworzenia kopii zapasowej lub woluminie skojarzonym z tego zestawu kopii zapasowych.
* **Z** i **do** — Witaj zakres dat i godzin przy tworzeniu zestawu kopii zapasowych hello.

Witaj filtrowane zestawy kopii zapasowych następnie wyszczególniono w oparciu hello następujące atrybuty:

* **Nazwa** — Witaj nazwę zasad tworzenia kopii zapasowej hello lub woluminie skojarzonym z zestawu kopii zapasowych hello.
* **Rozmiar** — Witaj rzeczywisty rozmiar hello zestawu kopii zapasowych.
* **Utworzony na** — hello Data i godzina utworzenia hello kopii zapasowych. 
* **Typ** — zestawy kopii zapasowych można migawki lokalne lub migawki w chmurze. Migawka lokalna jest kopię zapasową wszystkich danych woluminu przechowywane lokalnie na urządzeniu hello toohello tworzenia kopii zapasowych danych woluminu znajdującej się w chmurze hello odwołuje się migawka w chmurze. Migawki lokalne zapewnić szybszy dostęp migawki w chmurze są wybrać, aby zachować odporność danych.
* **Zainicjowane przez** — kopie zapasowe hello może zostać zainicjowane automatycznie zgodnie z harmonogramem tooa lub ręcznie przez użytkownika. (Możesz użyć kopii zapasowych tooschedule zasad tworzenia kopii zapasowej. Alternatywnie można użyć hello **utworzenia kopii zapasowej** tootake opcji interakcyjne kopii zapasowej.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Jak toorestore woluminu StorSimple z kopii zapasowej
Można użyć hello **katalogu kopii zapasowej** strony toorestore woluminu StorSimple z określonej kopii zapasowej. 

> [!WARNING]
> Przywracanie z kopii zapasowej spowoduje zastąpienie istniejących woluminów hello z kopii zapasowej hello. Może to spowodować utratę hello żadnych danych, które zostało zapisane po wykonaniu kopii zapasowej hello.
> 
> 

Przed rozpoczęciem przywracania na woluminie upewnij się, że wolumin hello jest w trybie offline. Najpierw należy tootake hello woluminu w trybie offline na hoście hello, a następnie hello urządzenia. Wykonaj kroki hello w [Przełącz do trybu offline wolumin](storsimple-manage-volumes.md#take-a-volume-offline). Wykonaj hello poniższych kroków toorestore woluminu z zestawu kopii zapasowych.

### <a name="toorestore-from-a-backup-set"></a>toorestore z zestawu kopii zapasowych
1. Na stronie usługi Menedżer StorSimple powitania kliknij hello **katalog kopii zapasowej** kartę.
   
    ![Katalog kopii zapasowej](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. Wybierz kopię zapasową ustawione w następujący sposób:
   
   1. Wybierz odpowiednie urządzenie hello.
   2. Z listy rozwijanej hello wybierz hello zasad woluminu lub kopii zapasowej do utworzenia kopii zapasowej hello czy tooselect.
   3. Określ zakres czasu hello.
   4. Kliknij ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) tooexecute tego zapytania.
      
      Hello kopii zapasowych skojarzonych z zasadami hello wybrany wolumin lub kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych.
3. Rozwiń hello zestawu kopii zapasowych tooview hello skojarzonych woluminów. Te woluminy muszą być pobierane w trybie offline na hoście hello i urządzenia, zanim będzie można ich przywrócić. Wykonaj kroki hello w [Przełącz do trybu offline wolumin](storsimple-manage-volumes.md#take-a-volume-offline).
   
   > [!IMPORTANT]
   > Upewnij się, czy wykonano woluminów hello w tryb offline na hoście hello najpierw, przed podjęciem dalszych na urządzeniu hello hello woluminy w trybie offline. W przypadku niepodjęcia hello woluminy w tryb offline na hoście hello potencjalnie spowodować uszkodzenie toodata.
   > 
   > 
4. Wybierz zestaw kopii zapasowych. Kliknij przycisk **przywrócić** u dołu hello hello strony.
5. Pojawi się monit o potwierdzenie. 
   
    ![Strona potwierdzenia](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. Przejrzyj informacje o przywracania hello i kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png). Spowoduje to zainicjowanie zadania przywracania, które można wyświetlić, uzyskując dostęp do hello **zadania** strony. 
7. Po zakończeniu przywracania hello można sprawdzić zawartość hello woluminów zastępuje woluminy z kopii zapasowej hello.

![Zobacz film](./media/storsimple-restore-from-backup-set/Video_icon.png) **Zobacz film**

toowatch film wideo przedstawiający sposób Użyj klonowania hello i przywracania funkcji w plikach toorecover usunięte StorSimple, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[woluminów StorSimple zarządzanie](storsimple-manage-volumes.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

