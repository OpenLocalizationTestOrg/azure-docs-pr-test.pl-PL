---
title: aaaRestore woluminu StorSimple z kopii zapasowej | Dokumentacja firmy Microsoft
description: "W tym artykule wyjaśniono, jak toouse hello toorestore strony katalogu kopii zapasowej usługi Menedżer StorSimple woluminu StorSimple z zestawu kopii zapasowych."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6f289c39-96c7-4d57-b68a-4bc2e99aef9d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/22/2017
ms.author: alkohli
ms.openlocfilehash: c2e38765e750749f5764b5cbf2167d3cd5edfe5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set-update-2"></a>Przywracania woluminu StorSimple z zestawu kopii zapasowych (Update 2)
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Omówienie
Witaj **katalogu kopii zapasowej** na stronie są wyświetlane wszystkie zestawy kopii zapasowych hello, które są tworzone podczas ręczne lub automatyczne kopie zapasowe są pobierane. Użyj tej strony toolist i zarządzanie kopiami zapasowymi, Przywróć z zestawu kopii zapasowych lub klonowania woluminu.

 ![Strona katalogu kopii zapasowej](./media/storsimple-restore-from-backup-set-u2/restore.png)

Ten samouczek wyjaśnia sposób toouse hello **katalogu kopii zapasowej** strony toorestore urządzenia z zestawu kopii zapasowych.

Można przywrócić woluminu z dysku lokalnego lub kopia zapasowa w chmurze. W obu przypadkach operacji przywracania hello łączy hello woluminu w trybie online, podczas gdy danych jest pobierany w tle hello. 

## <a name="before-you-restore"></a>Przed przywróceniem
Przed rozpoczęciem operacji przywracania należy zwrócić uwagę hello następujące ostrzeżenia:

* **Przełącz do trybu offline wolumin hello** — zająć hello woluminu w trybie offline na hoście zarówno hello i hello urządzenia przed rozpoczęciem powitalne operacji przywracania. Mimo że operacji przywracania hello automatycznie przywrócić hello online na urządzeniu hello, należy przełączyć na hoście hello ręcznie hello urządzeniem w trybie online. Na hoście hello można przełączyć hello woluminu w trybie online, gdy wolumin hello jest w trybie online na urządzeniu hello. (Nie trzeba toowait dopiero po zakończeniu operacji przywracania hello.) Procedur można przejść za[Przełącz do trybu offline wolumin](storsimple-manage-volumes-u2.md#take-a-volume-offline).
* **Typ woluminu po przywróceniu** — usunięte woluminy są przywracane na podstawie typu hello w migawce hello. Woluminy, które zostały przypięty lokalnie zostaną przywrócone jako woluminów przypiętych lokalnie i woluminów, które zostały do warstwy zostaną przywrócone jako woluminy warstwowe.
  
    Istniejące woluminy hello bieżącego użycia typu woluminu hello zastępuje hello typu, który jest przechowywany w migawce hello. Na przykład można odzyskać wolumin z migawki, która została podjęta, jeśli typ woluminu hello został warstwowy i że typ woluminu jest teraz lokalnie przypięty (ukończenia operacji konwersji tooa), następnie przywróceniu hello woluminu jako woluminu przypiętego lokalnie. Podobnie jeśli istniejącego woluminu przypiętego lokalnie jest rozwinięty, a następnie przywrócić z starsze migawką gdy wolumin hello był mniejszy, hello przywróconej wolumin zachowuje bieżący rozmiar po rozwinięciu hello.
  
    Nie można przekonwertować woluminu z woluminu przypiętego lokalnie tooa wolumin warstwowy lub _odwrotnie_ podczas woluminu hello jest przywracana. Poczekaj, aż zakończeniu operacji przywracania hello, a następnie można przekonwertować typu tooanother woluminu hello. Informacje o konwersji woluminu, przejdź za[zmienić typ woluminu hello](storsimple-manage-volumes-u2.md#change-the-volume-type). 
* **Witaj rozmiar woluminu jest widoczny w woluminie hello przywrócić** — to jest ważną kwestią w przypadku przywracania woluminu przypiętego lokalnie, która została usunięta (ponieważ woluminów przypiętych lokalnie są w pełni zaaprowizowanym). Upewnij się, że masz wystarczającą ilość miejsca, przed podjęciem próby toorestore woluminu przypiętego lokalnie, który został wcześniej usunięty. 
* **Nie można rozszerzyć woluminu, gdy jest przywracana** — poczekaj na zakończenie operacji przywracania hello przed podjęciem próby tooexpand hello woluminu. Informacje o rozszerzaniu woluminu, przejdź zbyt[zmodyfikować woluminu](storsimple-manage-volumes-u2.md#modify-a-volume).
* **Podczas przywracania woluminu lokalnego można wykonywać kopii zapasowej** — dla procedury Przejdź zbyt[przy użyciu zasad tworzenia kopii zapasowej toomanage usługi Menedżer StorSimple hello](storsimple-manage-backup-policies.md).
* **Możesz anulować operacji przywracania** — Jeśli anulujesz hello zadania przywracania, następnie hello wolumin zostanie wycofana toohello stan sprzed zainicjował hello przywracania. Procedur można przejść za[anulować zadanie](storsimple-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Jak przywrócić pracę
Dla urządzeń z systemem aktualizacji 4 lub nowszym systemem heatmap przywracania jest zaimplementowana. Jako dane tooaccess żądań hosta hello uzyskać dostęp do urządzenia hello, te żądania są śledzone, i heatmap jest tworzone. Wysoka częstość powoduje fragmentów danych z wyższej cieplna natomiast mniejszej szybkości żądania tłumaczy toochunks z niższym interakcji. Należy uruchomić hello dane co najmniej dwa razy toobe oznaczona jako _gorących_. Plik jest modyfikowany jest również oznaczona jako _gorących_. Po rozpoczęciu przywracania hello aktywnego dodawaniem danych występuje oparte na powitania heatmap. Dla wersji starszej niż 4 aktualizacji danych hello została pobrana podczas przywracania oparte na dostęp tylko. 

Na podstawie Heatmap śledzenia jest włączona tylko woluminami warstwowymi i przypięty lokalnie woluminy nie są obsługiwane. Przywracanie na podstawie Heatmap również nie jest obsługiwana w przypadku klonowania urządzenie tooanother woluminu. Jeśli istnieje przywracania w miejscu i firma Microsoft nie rehydrate (jak dane są już dostępne w lokalnie), a następnie na urządzeniu hello istnieje migawka lokalna dla toobe woluminu hello przywrócona. Domyślnie podczas przywracania, hello Preparaty nawadniające zadań są inicjowane z wyprzedzeniem rehydrate dane oparte na powitania heatmap. W pakiecie Update 4 poleceń cmdlet programu Windows PowerShell może być używane tooquery uruchomionych zadań Preparaty nawadniające, anulowanie zadania Preparaty nawadniające i Pobierz stan hello hello Preparaty nawadniające zadania.

* `Get-HcsRehydrationJob`— To polecenie cmdlet pobiera stan hello hello Preparaty nawadniające zadania. Zadanie pojedynczego Preparaty nawadniające zostanie wywołany dla jednego woluminu.
* `Set-HcsRehydrationJob`— To polecenie cmdlet pozwala toopause, zatrzymać, wznowić zadanie Preparaty nawadniające hello, gdy Preparaty nawadniające hello jest w toku. 

Aby uzyskać więcej informacji na poleceń cmdlet Preparaty nawadniające Przejdź zbyt[Dokumentacja poleceń cmdlet programu Windows PowerShell dla StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

Z automatycznego rehdyration zwykle wyższa wydajność odczytu przejściowej oczekuje. rzeczywiste magniutde Hello ulepszeń zależy od różnych czynników, takich jak wzorzec dostępu, przenoszenia danych i typ danych. toocancel zadania Preparaty nawadniające, możesz użyć polecenia cmdlet programu PowerShell hello. Jeśli chcesz toopermanently Wyłącz Preparaty nawadniające zadania dla wszystkich przyszłych operacji przywracania hello, skontaktuj się z Microsoft Support.

## <a name="how-toouse-hello-backup-catalog"></a>Jak toouse hello katalogu kopii zapasowej
Witaj **katalogu kopii zapasowej** strona zawiera zapytanie, które pomaga toonarrow wybór zestawu kopii zapasowych. Można filtrować hello zestawy kopii zapasowych pobieranych oparte na powitania następujące parametry:

* **Urządzenie** — hello urządzenia, na które hello utworzenia zestawu kopii zapasowych.
* **Wykonaj kopię zapasową zasad** lub **woluminu** — Witaj zasad tworzenia kopii zapasowej lub woluminie skojarzonym z tego zestawu kopii zapasowych.
* **Z** i **do** — Witaj zakres dat i godzin przy tworzeniu zestawu kopii zapasowych hello.

Witaj filtrowane zestawy kopii zapasowych następnie wyszczególniono w oparciu hello następujące atrybuty:

* **Nazwa** — Witaj nazwę zasad tworzenia kopii zapasowej hello lub woluminie skojarzonym z zestawu kopii zapasowych hello.
* **Rozmiar** — Witaj rzeczywisty rozmiar hello zestawu kopii zapasowych.
* **Utworzony na** — hello Data i godzina utworzenia hello kopii zapasowych. 
* **Typ** — zestawy kopii zapasowych można migawki lokalne lub migawki w chmurze. Migawka lokalna jest kopię zapasową wszystkich danych woluminu przechowywane lokalnie na powitania urządzenia. Migawka w chmurze odwołuje się toohello tworzenia kopii zapasowych danych woluminu znajdującej się w chmurze hello. Migawki lokalne zapewnić szybszy dostęp migawki w chmurze są wybrać, aby zachować odporność danych.
* **Zainicjowane przez** — kopie zapasowe hello może zostać zainicjowane automatycznie zgodnie z harmonogramem tooa lub ręcznie przez użytkownika. (Możesz użyć kopii zapasowych tooschedule zasad tworzenia kopii zapasowej. Alternatywnie można użyć hello **utworzenia kopii zapasowej** tootake opcji interakcyjne kopii zapasowej.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Jak toorestore woluminu StorSimple z kopii zapasowej
Można użyć hello **katalogu kopii zapasowej** strony toorestore woluminu StorSimple z określonej kopii zapasowej. Należy jednak pamiętać, przywracanie wolumin zostanie przywrócona hello woluminu toohello stan, jaki był po wykonaniu kopii zapasowej hello. Dane, które zostały dodane po hello operacji tworzenia kopii zapasowej zostaną utracone.

> [!WARNING]
> Przywracanie z kopii zapasowej zastępuje istniejące woluminy hello z kopii zapasowej hello. Może to spowodować utratę hello żadnych danych, które zostało zapisane po wykonaniu kopii zapasowej hello.
> 
> 

### <a name="toorestore-your-volume"></a>toorestore woluminu
1. Na stronie usługi Menedżer StorSimple powitania kliknij hello **katalog kopii zapasowej** kartę.
   
    ![Katalog kopii zapasowej](./media/storsimple-restore-from-backup-set-u2/restore.png)
2. Wybierz kopię zapasową ustawione w następujący sposób:
   
   1. Wybierz odpowiednie urządzenie hello.
   2. Z listy rozwijanej hello wybierz hello zasad woluminu lub kopii zapasowej do utworzenia kopii zapasowej hello czy tooselect.
   3. Określ zakres czasu hello.
   4. Kliknij ikonę znacznika wyboru hello ![ikona znacznika wyboru](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png) tooexecute tego zapytania.
      
      Hello kopii zapasowych skojarzonych z zasadami hello wybrany wolumin lub kopii zapasowej powinny być wyświetlane na liście hello zestawów kopii zapasowych.
3. Rozwiń hello zestawu kopii zapasowych tooview hello skojarzonych woluminów. Te woluminy muszą być pobierane w trybie offline na hoście hello i urządzenia, zanim będzie można ich przywrócić. Dostęp do woluminów hello na powitania **kontenery woluminów** strony, a następnie wykonaj kroki hello [woluminu Przełącz do trybu offline](storsimple-manage-volumes-u2.md#take-a-volume-offline) tootake ich w tryb offline.
   
   > [!IMPORTANT]
   > Upewnij się, czy wykonano woluminów hello w tryb offline na hoście hello najpierw, przed podjęciem dalszych na urządzeniu hello hello woluminy w trybie offline. W przypadku niepodjęcia hello woluminy w tryb offline na hoście hello potencjalnie spowodować uszkodzenie toodata.
   > 
   > 
4. Przejdź wstecz toohello **katalogu kopii zapasowej** i wybierz zestaw kopii zapasowych.
5. Kliknij przycisk **przywrócić** u dołu hello hello strony.
6. Zostanie wyświetlony monit o potwierdzenie. Przejrzyj hello przywracanie informacji o, a następnie zaznacz pole wyboru potwierdzenia hello.
   
    ![Strona potwierdzenia](./media/storsimple-restore-from-backup-set-u2/ConfirmRestore.png)
7. Kliknij ikonę znacznika wyboru hello ![Ikona znacznika wyboru](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png). Rozpoczyna zadanie przywracania. Możesz wyświetlić zadania hello uzyskując dostęp do hello **zadania** strony. 
8. Po zakończeniu przywracania hello można sprawdzić zawartość hello woluminów zastępuje woluminy z kopii zapasowej hello.

![Zobacz film](./media/storsimple-restore-from-backup-set-u2/Video_icon.png) **Zobacz film**

toowatch film wideo przedstawiający sposób Użyj klonowania hello i przywracania funkcji w plikach toorecover usunięte StorSimple, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="if-hello-restore-fails"></a>Jeśli hello przywracania kończy się niepowodzeniem
W przypadku odebrania alertu hello restore operacja kończy się niepowodzeniem dla dowolnej przyczyny. W takim przypadku tooverify listy kopii zapasowych hello odświeżania, który hello kopii zapasowej jest nadal ważny. Jeśli kopia zapasowa hello jest poprawna i że jest przywracana z chmury hello, następnie problemy z łącznością przyczyną może być hello problem. 

toocomplete hello operację przywracania, wykonaj hello woluminu w trybie offline na hoście hello i ponów próbę wykonania operacji przywracania hello. Wszelkie zmiany danych woluminu toohello wykonanych podczas procesu przywracania hello zostaną utracone.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[woluminów StorSimple zarządzanie](storsimple-manage-volumes-u2.md).
* Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

