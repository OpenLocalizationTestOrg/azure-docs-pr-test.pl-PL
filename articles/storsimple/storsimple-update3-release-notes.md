---
title: informacje o wersji aaaStorSimple 8000 serii Update 3 | Dokumentacja firmy Microsoft
description: "Opis nowych funkcji hello, problemy i rozwiązania StorSimple 8000 serii Update 3."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 2158aa7a-4ac3-42ba-8796-610d1adb984d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5bfcba61f7f210531437f650eafaad4dbd8c7c45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-3-release-notes-for-your-storsimple-8000-series-device"></a>Aktualizacja 3 informacje o wersji dla danego urządzenia z serii StorSimple 8000

## <a name="overview"></a>Omówienie
Witaj poniższych informacjach o wersji opisano nowe funkcje hello i zidentyfikować hello krytyczne problemy otwarte dla StorSimple 8000 serii Update 3. Zawierają one również listę aktualizacji oprogramowania StorSimple hello zawarte w tej wersji. 

Aktualizacja 3 może być zastosowane tooany StorSimple urządzenie z systemem zlecenia (GA) lub Update 0.1 za pomocą aktualizacji w wersji 2.2. Wersja urządzenia Hello skojarzony z aktualizacją Update 3 jest 6.3.9600.17759.

Zapoznaj się z tematem hello informacji zawartych w wersji hello, uwagi przed wdrożeniem hello aktualizacja w rozwiązaniu StorSimple.

> [!IMPORTANT]
> * Aktualizacja 3 ma oprogramowanie urządzenia, LSI sterowników i oprogramowania układowego i Storport i Spaceport aktualizacji. Trwa około 1,5 – 2 godz. tooinstall tej aktualizacji. 
> * Dostępność nowych wersji nie może wyświetlić aktualizacje od razu, ponieważ jak etapowego wdrażania hello aktualizacji. Poczekaj kilka dni, a następnie skanowanie w poszukiwaniu aktualizacji ponownie jako te staną się dostępne wkrótce.
> 
> 

## <a name="whats-new-in-update-3"></a>Nowości w wersji Update 3
Witaj następujące ulepszenia klucza i poprawki zostały wprowadzone w wersji Update 3.

* **Automatyczne zmiany odzyskiwanie miejsca** — uruchamianie Update 3 algorytmów odzyskiwanie miejsca hello jest uruchamiane na kontrolerze rezerwy hello hello systemu, co powoduje szybsze wykonywanie. Aby uzyskać więcej informacji na powitania porty, które są wymagane toowork z odzyskiwanie miejsca można znaleźć toohello [StorSimple wymagań sieciowych](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* **Ulepszenia wydajności** — Update 3 ulepszono chmury toohello wydajność odczytu i zapisu.
* **Ulepszenia związane z migracją** — w tej wersji kilka poprawek i ulepszenia zostały przygotowane dla funkcji migracji powitania od urządzeń z serii 5000/7000 urządzeń too8000 serii. Aby uzyskać więcej informacji na jak toouse hello funkcji migracji, przejdź zbyt[migracji z serii 5000/7000 urządzeń too8000 serii urządzenia](https://gallery.technet.microsoft.com/Azure-StorSimple-50007000-c1a0460b). 
* **Monitorowanie pokrewne poprawki** — w tej wersji błędy związane z toomonitoring wykresy, pulpit nawigacyjny usługi i urządzenia pulpitu nawigacyjnego zostały usunięte.

## <a name="issues-fixed-in-update-3"></a>Problemy rozwiązane w ramach aktualizacji Update 3
następujące tabele Hello zawiera podsumowanie problemów, które zostały usunięte w wersji Update 3.    

| Nie | Funkcja | Problem | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- |
| 1 |Migracja danych po stronie hosta |W hello wcześniejszych wersji hello urządzenia chmury StorSimple zostało przechodzi do trybu offline podczas migracji danych po stronie hosta. Tego problemu w tej wersji. |Nie |Tak |
| 2 |Woluminów przypiętych lokalnie |W poprzedniej wersji hello wystąpiły problemy dotyczące powiązanych tooI/O błędów, niepowodzenia konwersji woluminu i błędów ścieżki danych dla woluminów przypiętych lokalnie. Te problemy zostały spowodowane głównego i stałym w tej wersji. |Tak |Nie |
| 3 |Monitorowanie |Było wiele jednostek pokrewnych tooreporting problemów i monitorowania, a także wykresy pulpitu nawigacyjnego urządzenia, którym nieprawdziwych informacji został wyświetlony dla lokalnie przypięty woluminów. Te problemy zostały rozwiązane w tej wersji. |Tak |Nie |
| 4 |Duże zapisy we/wy |W przypadku używania StorSimple dla obciążeń obejmujących duże zapisy, hello użytkownika może działać na usterkę rzadkim gdzie hello zestaw roboczy został trwa warstwy do chmury hello. Ten problem został rozwiązany w tej wersji. |Tak |Tak |
| 5 |Tworzenie kopii zapasowych |W niektórych rzadkich przypadkach hello poprzednie wersje oprogramowania po użytkownik przejął kopii zapasowej zdalnego klonowania, czy wystąpiły błędy chmury i operacji hello spowoduje błąd. W tej wersji hello problemu i hello operacja zakończy się pomyślnie. |Tak |Tak |
| 6 |Zasady tworzenia kopii zapasowych |W niektórych rzadkich przypadkach w hello wcześniej wersje oprogramowania, wystąpił błąd powiązane toohello usunięcie zasad tworzenia kopii zapasowej. Tego problemu w tej wersji. |Tak |Tak |

## <a name="known-issues-in-update-3"></a>Znane problemy w wersji Update 3
Witaj w poniższej tabeli przedstawiono podsumowanie znanych problemów występujących w tej wersji.

| Nie. | Funkcja | Problem | Komentarz / obejście problemu | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- | --- |
| 1 |Dysku kworum |W rzadkich przypadkach jeśli większość hello dysków w obudowie EBOD hello urządzenia 8600 rozłączenia spowodować, że nie ma dysku kworum, następnie hello puli magazynu przejdzie w trybie offline. Pozostanie on w trybie offline nawet wtedy, gdy będzie nawiązywane hello dysków. |Konieczne będzie tooreboot hello urządzenia. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support, dalsze czynności. |Tak |Nie |
| 2 |Identyfikator niepoprawne kontrolera |Po wykonaniu zastąpić kontrolera kontrolera 0 mogą wyglądać jak kontrolera 1. Podczas wymiany kontrolera po załadowaniu hello obraz z węzła równorzędnego hello, identyfikator kontrolera hello można wyświetlane początkowo jako identyfikator hello równorzędnej kontrolera. W rzadkich przypadkach to zachowanie może być widoczny po ponownym uruchomieniu systemu. |Nie jest wymagana żadna akcja użytkownika. Sytuacja ta zostanie rozwiązany samoczynnie po zakończeniu hello zastępczego kontrolera. |Tak |Nie |
| 3 |Konta magazynu |Przy użyciu konta magazynu hello magazynu usługi toodelete hello jest to nieobsługiwany scenariusz. Spowoduje to tooa sytuacji, w której nie można pobrać danych użytkownika. | |Tak |Tak |
| 4 |Urządzenia trybu failover |Wiele przechodzenia kontener woluminów z hello tego samego urządzenia docelowe toodifferent urządzenia źródłowego nie jest obsługiwane. Tryb failover z urządzeń toomultiple jednego urządzenia martwy spowoduje, że hello kontenery woluminów na powitania najpierw przejścia w tryb failover urządzeń utraty własności danych. Po przełączeniu te kontenery woluminów są wyświetlane lub zachowywać się inaczej, podczas wyświetlania w hello klasycznego portalu Azure. | |Tak |Nie |
| 5 |Instalacja |Podczas StorSimple karty dla instalacji programu SharePoint należy tooprovide IP urządzenia, aby toofinish instalacji hello pomyślnie. | |Tak |Nie |
| 6 |Serwer proxy sieci Web |Jeśli ma konfigurację serwera proxy sieci web HTTPS jako hello określić protokół, będzie mieć wpływ na komunikacji usługi urządzeń i hello urządzenie przejdzie w trybie offline. Obsługa pakietów również zostanie wygenerowany w procesie hello, wykorzystywanie znaczące ilości zasobów na urządzeniu. |Upewnij się, że hello określony protokół adresu URL serwera proxy sieci web hello ma HTTP. Aby uzyskać więcej informacji, przejdź zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](storsimple-configure-web-proxy.md). |Tak |Nie |
| 7 |Serwer proxy sieci Web |Jeśli możesz skonfigurować i włączyć serwer proxy sieci web na zarejestrowanym urządzeniu, będzie konieczne toorestart hello aktywnym kontrolerze na urządzeniu. | |Tak |Nie |
| 8 |Wysoka chmury opóźnienia i wysokie obciążenie We/Wy |Gdy urządzenie StorSimple napotka kombinacją chmury w bardzo duże opóźnienia (kolejność sekund) i wysokie obciążenie We/Wy, hello urządzenia woluminów przechodzi w stan obniżeniem i hello operacji We/Wy może zakończyć się niepowodzeniem z powodu błędu "urządzenie nie jest gotowe". |Będzie konieczne kontrolery urządzeń hello ponowny rozruch toomanually lub wykonaj toorecover pracy awaryjnej urządzenia z tej sytuacji. |Tak |Nie |
| 9 |Azure PowerShell |Jeśli używasz polecenia cmdlet StorSimple hello **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object - oczekiwania najpierw 1 -** tooselect hello pierwszy obiekt, w którym można utworzyć nowy **VolumeContainer** obiekt hello cmdlet zwraca wszystkie obiekty hello. |Zawijanie hello polecenia cmdlet w nawiasach w następujący sposób: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - najpierw 1 - oczekiwania** |Tak |Tak |
| 10 |Migracja |W przypadku wielu kontenery woluminów są przekazywane do migracji, hello EAT dla najnowszej kopii zapasowej jest dokładna tylko dla pierwszego kontenera woluminów hello. Ponadto migracji równoległej rozpocznie się po hello 4 kopie zapasowe w pierwszym kontenera woluminów hello są migrowane. |Firma Microsoft zaleca migrować jeden kontener woluminów naraz. |Tak |Nie |
| 11 |Migracja |Po przywróceniu hello woluminy nie są dodawane toohello kopii zapasowej zasad lub hello dysku wirtualnego grupy. |Konieczne będzie tooadd tych zasad tworzenia kopii zapasowej tooa woluminy w kolejności toocreate tworzenia kopii zapasowych. |Tak |Tak |
| 12 |Migracja |Po zakończeniu migracji hello nie musi dostępu urządzenia z serii 5000/7000 hello hello migracji kontenerów danych. |Firma Microsoft zaleca, aby usunąć hello migracji kontenerów danych po migracji hello jest ukończone i zatwierdzone. |Tak |Nie |
| 13 |Klonowanie i odzyskiwania po awarii |Urządzenia StorSimple z aktualizacją Update 1 nie można sklonować lub wykonać urządzenia tooa odzyskiwania po awarii 1 oprogramowaniem przed aktualizacją. |Konieczne będzie tooupdate hello docelowego urządzenia tooUpdate 1 tooallow te operacje |Tak |Tak |
| 14 |Migracja |Kopia zapasowa konfiguracji migracji może zakończyć się niepowodzeniem na urządzeniu z serii 5000 7000 przypadku woluminu grup skojarzonych woluminów. |Usunąć wszystkie grupy pusty woluminu hello z nie skojarzone woluminy, a następnie spróbuj ponownie hello konfigurację z kopii zapasowej. |Tak |Nie |
| 15 |Polecenia cmdlet programu PowerShell systemu Azure i woluminów przypiętych lokalnie |Nie można utworzyć woluminu przypiętego lokalnie za pomocą poleceń cmdlet programu Azure PowerShell. (Będzie warstwowa każdym woluminie tworzonych za pomocą programu Azure PowerShell.) |Należy zawsze używać woluminów tooconfigure przypięty lokalnie usługi Menedżer StorSimple hello. |Tak |Nie |
| 16 |Miejsce dostępne dla woluminów przypiętych lokalnie |Jeśli usuniesz woluminu przypiętego lokalnie hello miejsca dla nowych woluminów mogły nie zostać zaktualizowane od razu. aktualizacje usługi Menedżer StorSimple Hello hello lokalne miejsce dostępne mniej więcej co godzinę. |Poczekaj, aż godziny przed podjęciem próby toocreate hello nowego woluminu. |Tak |Nie |
| 17 |Woluminów przypiętych lokalnie |Zadanie przywracania przedstawia kopii zapasowej migawki tymczasowego hello w hello katalogu kopii zapasowej, ale tylko na czas trwania hello hello zadanie przywracania. Ponadto udostępnia ona grupy dysków wirtualnych z prefiksem **tmpCollection** na powitania **zasady tworzenia kopii zapasowej** strony, ale tylko na czas trwania hello hello zadanie przywracania. |Ten problem może wystąpić, jeśli zadanie przywracania ma przypięty tylko lokalnie woluminów lub mieszane lokalnie woluminów przypiętych i warstwowego. Jeśli zadanie przywracania hello zawiera tylko woluminów warstwowych, ten problem nie zostanie przeprowadzona. Interwencja użytkownika nie jest wymagane. |Tak |Nie |
| 18 |Woluminów przypiętych lokalnie |Jeśli anulowanie zadania przywracania, a do kontrolera pracy awaryjnej natychmiast później, zostaną wyświetlone zadanie przywracania hello **** zamiast **anulowane**. Jeśli zadanie przywracania kończy się niepowodzeniem, a do kontrolera pracy awaryjnej natychmiast później, zostaną wyświetlone zadanie przywracania hello **anulowane** zamiast ****. |Ten problem może wystąpić, jeśli zadanie przywracania ma przypięty tylko lokalnie woluminów lub mieszane lokalnie woluminów przypiętych i warstwowego. Jeśli zadanie przywracania hello zawiera tylko woluminów warstwowych, ten problem nie zostanie przeprowadzona. Interwencja użytkownika nie jest wymagane. |Tak |Nie |
| 19 |Woluminów przypiętych lokalnie |Anulowanie zadania przywracania, lub jeśli przywracania kończy się niepowodzeniem, a następnie do kontrolera pracy awaryjnej, zadanie przywracania dodatkowe pojawi się na powitania **zadania** strony. |Ten problem może wystąpić, jeśli zadanie przywracania ma przypięty tylko lokalnie woluminów lub mieszane lokalnie woluminów przypiętych i warstwowego. Jeśli zadanie przywracania hello zawiera tylko woluminów warstwowych, ten problem nie zostanie przeprowadzona. Interwencja użytkownika nie jest wymagane. |Tak |Nie |
| 20 |Woluminów przypiętych lokalnie |Jeśli spróbujesz tooconvert wolumin warstwowy (utworzone i sklonowany z 1.2 aktualizacji lub starszym) wolumin przypięty lokalnie tooa urządzeniu zaczyna brakować miejsca lub brak awarii chmury, a następnie hello clone(s) może być uszkodzony. |Ten problem występuje tylko w przypadku woluminów, które zostały utworzone i sklonowany z przed aktualizacją 2.1 oprogramowania. Powinno to być rzadkim scenariusza. | | |
| 21 |Konwersja woluminu |Nie aktualizuj hello ACRs dołączonych tooa woluminu w trakcie konwersji woluminu (warstwowych toolocally przypięty lub na odwrót). Aktualizowanie hello ACRs może spowodować uszkodzenie danych. |W razie potrzeby zaktualizować konwersji woluminu wcześniejsze toohello ACRs hello i nie należy wprowadzać żadnych późniejszych ACR aktualizacji podczas konwersji hello jest w toku. | | |
| 22 |Aktualizacje |Podczas stosowania aktualizacji 3, hello **konserwacji** strony w hello Azure klasycznego portalu będą następujące hello wyświetlania komunikatu pokrewne tooUpdate 2 — "serii StorSimple 8000 z aktualizacją Update 2 obejmuje możliwość hello zbieranie tooproactively firmy Microsoft Rejestrowanie informacji z własnego urządzenia, gdy zostanie wykryte, potencjalne problemy". To jest błąd, ponieważ wskazuje, że urządzenie hello są zaktualizowane tooUpdate 2. Urządzenie powitania po tooUpdate succeesfully aktualizacji 3 ten komunikat zniknie. |Ten problem zostanie rozwiązany w przyszłej wersji. |Tak |Nie |

## <a name="controller-and-firmware-updates-in-update-3"></a>Kontroler aktualizacje w wersji Update 3
Ta wersja zawiera LSI sterowników i oprogramowania układowego. Aby uzyskać więcej informacji na temat sposobu tooinstall hello LSI sterowników i aktualizacje oprogramowania układowego, zobacz [zainstalować aktualizacji 3](storsimple-install-update-3.md) na urządzeniu StorSimple.

## <a name="virtual-device-updates-in-update-3"></a>Urządzenie wirtualne aktualizacji w wersji Update 3
Ta aktualizacja nie może być zastosowane toohello urządzenia chmury StorSimple (znanej także jako hello urządzenia wirtualnego). Nowe urządzenia wirtualnego należy utworzyć toobe. 

## <a name="next-step"></a>Następny krok
Dowiedz się, jak za[zainstalować aktualizacji 3](storsimple-install-update-3.md) na urządzeniu StorSimple.

