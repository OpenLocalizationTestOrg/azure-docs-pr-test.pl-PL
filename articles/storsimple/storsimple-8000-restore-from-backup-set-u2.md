---
title: aaaRestore woluminu z kopii zapasowej w serii StorSimple 8000 | Dokumentacja firmy Microsoft
description: "W tym artykule wyjaśniono, jak toouse hello toorestore katalogu kopii zapasowej usługi Menedżer StorSimple urządzenia woluminu StorSimple z zestawu kopii zapasowych."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 0fe2e4c23a23c75ce4058a8531356c94c973c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Przywracania woluminu StorSimple z zestawu kopii zapasowych

## <a name="overview"></a>Omówienie

W tym samouczku opisano operacji przywracania hello wykonać na urządzeniu serii StorSimple 8000 przy użyciu istniejącego zestawu kopii zapasowych. Użyj hello **katalog kopii zapasowej** bloku toorestore woluminu z dysku lokalnego lub kopia zapasowa w chmurze. Witaj **katalog kopii zapasowej** bloku Wyświetla wszystkie zestawy kopii zapasowych hello, które są tworzone podczas ręczne lub automatyczne kopie zapasowe są pobierane. Hello operacji przywracania z zestawu kopii zapasowych łączy hello woluminu w trybie online, podczas gdy danych jest pobierany w tle hello.

Alternatywna metoda toostart przywracania jest zbyt toogo**urządzenia > [urządzenia] > woluminów**. W hello **woluminów** bloku, wybierz wolumin, menu kontekstowe hello tooinvoke kliknij prawym przyciskiem myszy, a następnie wybierz **przywrócić**.

## <a name="before-you-restore"></a>Przed przywróceniem

Przed rozpoczęciem przywracania, przejrzyj hello następujące ostrzeżenia:

* **Wolumin hello należy wykonać w trybie offline** — zająć hello woluminu w trybie offline na hoście zarówno hello i hello urządzenia przed rozpoczęciem powitalne operacji przywracania. Mimo że operacji przywracania hello automatycznie przywrócić hello online na urządzeniu hello, należy przełączyć na hoście hello ręcznie hello urządzeniem w trybie online. Na hoście hello można przełączyć hello woluminu w trybie online, jak wolumin hello jest w trybie online na urządzeniu hello. (Nie trzeba toowait dopiero po zakończeniu operacji przywracania hello.) Procedur można przejść za[Przełącz do trybu offline wolumin](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).

* **Typ woluminu po przywróceniu** — usunięte woluminy są przywracane na podstawie typu hello w migawce hello; to, że woluminy, które zostały przypięty lokalnie zostaną przywrócone jako woluminów przypiętych lokalnie i woluminów, które zostały do warstwy zostaną przywrócone jako woluminy warstwowe.

    Istniejące woluminy hello bieżącego użycia typu woluminu hello zastępuje hello typu, który jest przechowywany w migawce hello. Na przykład woluminu w przypadku przywracania z migawki, która została podjęta, jeśli typ woluminu hello został do warstwy, że typ woluminu jest teraz lokalnie przypięty (ukończenia operacji konwersji tooa wykonano) następnie hello wolumin zostanie przywrócony jako woluminu przypiętego lokalnie. Podobnie jeśli rozwinięty istniejącego woluminu przypiętego lokalnie, a następnie przywrócone z starsze migawką gdy wolumin hello był mniejszy, hello woluminu przywrócone zostaną zachowane hello bieżący rozmiar po rozwinięciu.

    Nie można przekonwertować na woluminie z woluminu przypiętego lokalnie tooa woluminu warstwowego lub z tooa woluminu przypiętego lokalnie warstwowej woluminu, podczas gdy wolumin hello jest przywracana. Poczekaj, aż zakończeniu operacji przywracania hello, a następnie można przekonwertować typu tooanother woluminu hello. Informacje o konwersji woluminu, przejdź za[zmienić typ woluminu hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type). 

* **Witaj rozmiar woluminu jest widoczny w woluminie hello przywrócić** — to jest ważną kwestią w przypadku przywracania woluminu przypiętego lokalnie, która została usunięta (ponieważ woluminów przypiętych lokalnie są w pełni zaaprowizowanym). Upewnij się, że masz wystarczającą ilość miejsca, przed podjęciem próby toorestore woluminu przypiętego lokalnie, który został wcześniej usunięty.

* **Nie można rozszerzyć woluminu, gdy jest przywracana** — poczekaj na zakończenie operacji przywracania hello przed podjęciem próby tooexpand hello woluminu. Informacje o rozszerzaniu woluminu, przejdź zbyt[zmodyfikować woluminu](storsimple-8000-manage-volumes-u2.md#modify-a-volume).

* **Podczas przywracania woluminu lokalnego można wykonywać kopii zapasowej** — dla procedury Przejdź zbyt[przy użyciu zasad tworzenia kopii zapasowej toomanage usługi Menedżer StorSimple urządzenia hello](storsimple-8000-manage-backup-policies-u2.md).

* **Możesz anulować operacji przywracania** — Jeśli anulujesz hello zadania przywracania, a następnie wolumin hello zostanie wycofana toohello stan sprzed zainicjował operację przywracania hello. Procedur można przejść za[anulować zadanie](storsimple-8000-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Jak przywrócić pracę

Dla urządzeń z systemem aktualizacji 4 lub nowszym systemem heatmap przywracania jest zaimplementowana. Jako dane tooaccess żądań hosta hello uzyskać dostęp do urządzenia hello, te żądania są śledzone, i heatmap jest tworzone. Wysoka częstość powoduje fragmentów danych z wyższej cieplna natomiast mniejszej szybkości żądania tłumaczy toochunks z niższym interakcji. Należy uruchomić hello dane co najmniej dwa razy toobe oznaczona jako _gorących_. Plik jest modyfikowany jest również oznaczona jako _gorących_. Po rozpoczęciu przywracania hello aktywnego dodawaniem danych występuje oparte na powitania heatmap. W wersjach wcześniejszych niż aktualizacja 4, danych hello jest pobierana podczas przywracania oparte na dostęp tylko.

Hello następujące ostrzeżenia stosowane na podstawie tooheatmap przywracania:

* Heatmap śledzenie jest włączone tylko dla woluminów warstwowych i woluminów przypiętych lokalnie nie są obsługiwane.

* Przywracanie na podstawie Heatmap nie jest obsługiwana w przypadku klonowania urządzenie tooanother woluminu. 

* Jeśli istnieje przywracania w miejscu i firma Microsoft nie rehydrate (jak dane są już dostępne w lokalnie), a następnie na urządzeniu hello istnieje migawka lokalna dla toobe woluminu hello przywrócona. 

* Domyślnie podczas przywracania, hello Preparaty nawadniające zadań są inicjowane z wyprzedzeniem rehydrate dane oparte na powitania heatmap. 

W pakiecie Update 4 poleceń cmdlet programu Windows PowerShell może być używane tooquery uruchomionych zadań Preparaty nawadniające, anulowanie zadania Preparaty nawadniające i Pobierz stan hello hello Preparaty nawadniające zadania.

* `Get-HcsRehydrationJob`— To polecenie cmdlet pobiera stan hello hello Preparaty nawadniające zadania. Zadanie pojedynczego Preparaty nawadniające zostanie wywołany dla jednego woluminu.

* `Set-HcsRehydrationJob`— To polecenie cmdlet pozwala toopause, zatrzymać, wznowić zadanie Preparaty nawadniające hello, gdy Preparaty nawadniające hello jest w toku.

Aby uzyskać więcej informacji na poleceń cmdlet Preparaty nawadniające Przejdź zbyt[Dokumentacja poleceń cmdlet programu Windows PowerShell dla StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

Z automatycznego rehdyration zwykle wyższa wydajność odczytu przejściowej oczekuje. rzeczywiste magniutde Hello ulepszeń zależy od różnych czynników, takich jak wzorzec dostępu, przenoszenia danych i typ danych. 

toocancel zadania Preparaty nawadniające, możesz użyć polecenia cmdlet programu PowerShell hello. Jeśli chcesz toopermanently Wyłącz Preparaty nawadniające zadania hello wszystkich przyszłych operacji przywracania, [skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md).

## <a name="how-toouse-hello-backup-catalog"></a>Jak toouse hello katalogu kopii zapasowej

Witaj **katalogu kopii zapasowej** blok zawiera zapytanie, które pomaga toonarrow wybór zestawu kopii zapasowych. Można filtrować hello zestawy kopii zapasowych pobieranych oparte na powitania następujące parametry:

* **Zakres czasu** — Witaj zakres dat i godzin przy tworzeniu zestawu kopii zapasowych hello.
* **Urządzenie** — hello urządzenia, na które hello utworzenia zestawu kopii zapasowych.
* **Wykonaj kopię zapasową zasad** lub **woluminu** — Witaj zasad tworzenia kopii zapasowej lub woluminie skojarzonym z tego zestawu kopii zapasowych.

Witaj filtrowane zestawy kopii zapasowych następnie wyszczególniono w oparciu hello następujące atrybuty:

* **Nazwa** — Witaj nazwę zasad tworzenia kopii zapasowej hello lub woluminie skojarzonym z zestawu kopii zapasowych hello.
* **Typ** — zestawy kopii zapasowych można migawki lokalne lub migawki w chmurze. Migawka lokalna jest kopię zapasową wszystkich danych woluminu przechowywane lokalnie na urządzeniu hello toohello tworzenia kopii zapasowych danych woluminu znajdującej się w chmurze hello odwołuje się migawka w chmurze. Migawki lokalne zapewnić szybszy dostęp migawki w chmurze są wybrać, aby zachować odporność danych.
* **Rozmiar** — Witaj rzeczywisty rozmiar hello zestawu kopii zapasowych.
* **Utworzony na** — hello Data i godzina utworzenia hello kopii zapasowych. 
* **Woluminy** — Witaj wiele woluminów skojarzone z zestawu kopii zapasowych hello.
* **Zainicjowano** — kopie zapasowe hello może zostać zainicjowane automatycznie zgodnie z harmonogramem tooa lub ręcznie przez użytkownika. (Możesz użyć kopii zapasowych tooschedule zasad tworzenia kopii zapasowej. Alternatywnie można użyć hello **utworzenia kopii zapasowej** tootake opcji interakcyjnego lub na żądanie kopii zapasowej.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Jak toorestore woluminu StorSimple z kopii zapasowej

Można użyć hello **katalogu kopii zapasowej** toorestore bloku woluminu StorSimple z określonej kopii zapasowej. Należy jednak pamiętać, przywracanie wolumin zostanie przywrócony stan hello toohello woluminu, jakim był po wykonaniu kopii zapasowej hello. Dane, które zostały dodane po hello operacji tworzenia kopii zapasowej zostaną utracone.

> [!WARNING]
> Przywracanie z kopii zapasowej spowoduje zastąpienie istniejących woluminów hello z kopii zapasowej hello. Może to spowodować utratę hello żadnych danych, które zostało zapisane po wykonaniu kopii zapasowej hello.


### <a name="toorestore-your-volume"></a>toorestore woluminu
1. Przejdź tooyour usługi Menedżer urządzeń StorSimple, a następnie kliknij przycisk **katalog kopii zapasowej**.

2. Wybierz kopię zapasową ustawione w następujący sposób:
   
   1. Określ zakres czasu hello.
   2. Wybierz odpowiednie urządzenie hello.
   3. Z listy rozwijanej hello wybierz hello zasad woluminu lub kopii zapasowej do utworzenia kopii zapasowej hello czy tooselect.
   4. Kliknij przycisk **Zastosuj** tooexecute tego zapytania.

    Hello kopii zapasowych skojarzonych z zasadami hello wybrany wolumin lub kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych.
   
    ![Listy zestawu kopii zapasowych](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. Rozwiń hello zestawu kopii zapasowych tooview hello skojarzonych woluminów. Te woluminy muszą być pobierane w trybie offline na hoście hello i urządzenia, zanim będzie można ich przywrócić. Dostęp do woluminów hello na powitania **woluminów** bloku urządzenia i następnie hello wykonaj kroki opisane w temacie [Przełącz do trybu offline wolumin](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake ich w tryb offline.
   
   > [!IMPORTANT]
   > Upewnij się, czy wykonano woluminów hello w tryb offline na hoście hello najpierw, przed podjęciem dalszych na urządzeniu hello hello woluminy w trybie offline. W przypadku niepodjęcia hello woluminy w tryb offline na hoście hello potencjalnie spowodować uszkodzenie toodata.
   
4. Przejdź wstecz toohello **katalogu kopii zapasowej** i wybierz zestaw kopii zapasowych. Kliknij prawym przyciskiem myszy, a następnie z menu kontekstowego hello, wybierz **przywrócić**.

    ![Listy zestawu kopii zapasowych](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. Pojawi się monit o potwierdzenie. Przejrzyj hello przywracanie informacji o, a następnie zaznacz pole wyboru potwierdzenia hello.
   
    ![Strona potwierdzenia](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  Kliknij przycisk **przywrócić**. Powoduje to zainicjowanie zadania przywracania, które można wyświetlić, uzyskując dostęp do hello **zadania** strony.

    ![Strona potwierdzenia](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. Po zakończeniu przywracania hello Sprawdź zawartość hello woluminów zastępuje woluminy z kopii zapasowej hello.


## <a name="if-hello-restore-fails"></a>Jeśli hello przywracania kończy się niepowodzeniem

Otrzymasz alert hello przywracania operacja kończy się niepowodzeniem dla dowolnej przyczyny. W takim przypadku tooverify listy kopii zapasowych hello odświeżania, który hello kopii zapasowej jest nadal ważny. Jeśli kopia zapasowa hello jest poprawna i że jest przywracana z chmury hello, następnie problemy z łącznością przyczyną może być hello problem.

toocomplete hello operację przywracania, wykonaj hello woluminu w trybie offline na hoście hello i ponów próbę wykonania operacji przywracania hello. Uwaga w procesie przywracania danych woluminu toohello zmiany wykonane podczas hello zostaną utracone.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[woluminów StorSimple zarządzanie](storsimple-8000-manage-volumes-u2.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).

