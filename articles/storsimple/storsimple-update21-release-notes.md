---
title: informacje o wersji 2.2 aktualizacji serii aaaStorSimple 8000 | Dokumentacja firmy Microsoft
description: "Opis nowych funkcji hello, problemy i rozwiązania StorSimple 8000 serii aktualizacji w wersji 2.2."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5cf03ea8-2a0f-4552-b6dc-7ea517783d7b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/18/2016
ms.author: alkohli
ms.openlocfilehash: a2902126f4011fa9ade64f63a8abdec095874fb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-22-release-notes"></a>Informacje o wersji StorSimple 8000 serii aktualizacji w wersji 2.2
## <a name="overview"></a>Omówienie
Witaj poniższych informacjach o wersji opisano nowe funkcje hello i zidentyfikować hello krytyczne problemy otwarte dla StorSimple 8000 serii aktualizacji w wersji 2.2. Zawierają one również listę aktualizacji oprogramowania StorSimple hello zawarte w tej wersji. 

Aktualizacja 2.2 może być zastosowane tooany StorSimple urządzenie z systemem zlecenia (GA) lub Update 0.1 za pośrednictwem Update 2.1. Wersja urządzenia Hello skojarzone z 2.2 aktualizacji jest 6.3.9600.17708.

Zapoznaj się z tematem hello informacji zawartych w wersji hello, uwagi przed wdrożeniem hello aktualizacja w rozwiązaniu StorSimple.

> [!IMPORTANT]
> * Aktualizacja 2.2 ma tylko aktualizacje oprogramowania. Trwa około 1,5 – 2 godz. tooinstall tej aktualizacji. 
> * Jeśli używasz Update 2.1, zaleca się zastosowanie aktualizacji 2.2 tak szybko, jak to możliwe.
> * Dostępność nowych wersji nie może wyświetlić aktualizacje od razu, ponieważ jak etapowego wdrażania hello aktualizacji. Poczekaj kilka dni, a następnie skanowanie w poszukiwaniu aktualizacji ponownie jako te staną się dostępne wkrótce.
> 
> 

## <a name="whats-new-in-update-22"></a>Nowości w aktualizacji w wersji 2.2
Witaj następujące klucza wprowadzono ulepszenia w wersji 2.2 aktualizacji.

* **Automatyczne odzyskiwanie optymalizacje** — kiedy dane są usuwane na woluminy alokowane elastycznie hello nieużywane magazynu bloki muszą toobe odzyskana. Tej wersji ma ulepszone hello miejsca odzyskiwanie proces z chmury hello powodujące hello nieużywane miejsce która staje się dostępna szybciej w porównaniu toohello poprzednie wersje.
* **Migawki usprawnień wydajności** – 2.2 aktualizacji zawiera ulepszone hello czasu tooprocess migawka w chmurze w pewnych sytuacjach, gdy są używane duże woluminy i ma minimalnej toono tworzeniem danych. Scenariusz, w którym będzie korzystać z to rozszerzenie jest hello archiwum woluminów.
* **Ograniczenie funkcjonalności pakietu obsługi zbierania** — były udoskonalenia w sposób hello pakietu obsługi hello jest zebrane i przekazane w tej wersji. 
* **Ulepszenia niezawodności zaktualizować** — to wydanie zawiera poprawki, które powodują powstanie większą niezawodność aktualizacji.

## <a name="issues-fixed-in-update-22"></a>Problemy rozwiązane w wersji 2.2 aktualizacji
następujące tabele Hello zawiera podsumowanie problemów, które zostały usunięte w wersji 2.2 aktualizacji i 2.1.    

| Nie | Funkcja | Problem | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- |
| 1 |Wydajność hosta |W hello starszej wersji, problemy z wydajnością po stronie hosta zaobserwowano podczas tworzenia woluminu przypiętego lokalnie hello podczas konwersji hello tooa wolumin warstwowy, który jest lokalnie przypięty woluminu. W tej wersji, powodując poprawy wydajności hosta hello podczas procedur tworzenia i konwersji woluminu hello rozwiązaniu tych problemów. |Tak |Nie |
| 2 |Woluminów przypiętych lokalnie |W rzadkich przypadkach hello systemu może ulec awarii podczas tworzenia woluminu przypiętego lokalnie. Ten problem został rozwiązany w tej wersji. |Tak |Nie |
| 3 |Obsługa poziomów |Podczas hello metadanych dla warstwy hello StorSimple chmury urządzenia (urządzenia 8010 i 8020) zbyt hello chmury były sporadyczne awarie. Tego problemu w tej wersji. |Nie |Tak |
| 4 |Tworzenie migawki |Wystąpiły problemy tworzenie powiązanych toohello przyrostowe migawek w scenariuszach z dużych woluminów i minimalnego toono zmian danych. Te problemy zostały rozwiązane w tej wersji. |Tak |Tak |
| 5 |Openstack uwierzytelniania |Używając Openstack jako dostawcy usług w chmurze hello hello użytkownika może działać Authentication toohello powiązanych usterek rzadkim gdzie analizatora składni JSON hello spowodowała awarię. Ten problem został rozwiązany w tej wersji. |Tak |Nie |
| 6 |Kopiuj po stronie hosta |We wcześniejszych wersjach oprogramowania rzadkim błędów związanych z toohello odciążonego transferu danych chronometrażu moment kopiowanie hello danych z jednego woluminu tooanother woluminu. To spowoduje awarię kontrolera, a hello system potencjalnie można przejść do trybu odzyskiwania. Ten problem został rozwiązany w tej wersji. |Tak |Nie |
| 7 |Instrumentacja zarządzania Windows (WMI) |W poprzednich wersjach hello oprogramowania, zostały kilka wystąpień awarii serwera proxy sieci web, z wyjątkiem hello "<ManagementException> błąd ładowania dostawcy". Ten błąd był przeciek pamięci WMI tooa oparte na atrybutach i jest stałe. |Tak |Nie |
| 8 |Aktualizacja |Niektórych sporadycznie hello poprzednie wersje oprogramowania, w hello użytkownik otrzymał "CisPowershellHcsscripterror" podczas próby tooscan lub instalacji aktualizacji. Tego problemu w tej wersji. |Tak |Tak |
| 9 |Pakiet pomocy technicznej |W tej wersji są dostępne ulepszenia sposób toohello pakietu obsługi hello jest zebrane i przekazane. |Tak |Tak |

## <a name="known-issues-in-update-22"></a>Znane problemy w wersji 2.2 aktualizacji
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

## <a name="controller-and-firmware-updates-in-update-22"></a>Kontroler aktualizacje w wersji 2.2 aktualizacji
Ta wersja zawiera aktualizacji oprogramowania. Jednak aktualizowania z poprzednich tooUpdate w wersji 2, konieczne będzie tooinstall sterownika Storport, Spaceport i (w niektórych przypadkach) na dysku aktualizacje oprogramowania układowego na urządzeniu.

Aby uzyskać więcej informacji na temat sposobu tooinstall hello sterownika Storport, Spaceport i aktualizacje oprogramowania układowego dysku, zobacz [zainstalować aktualizację 2.2](storsimple-install-update-21.md) na urządzeniu StorSimple.

## <a name="virtual-device-updates-in-update-22"></a>Urządzenie wirtualne aktualizacji w wersji 2.2 aktualizacji
Ta aktualizacja nie może być zastosowane toohello urządzenia wirtualnego. Nowe urządzenia wirtualnego należy utworzyć toobe. 

## <a name="next-step"></a>Następny krok
Dowiedz się, jak za[zainstalować aktualizację 2.2](storsimple-install-update-21.md) na urządzeniu StorSimple.

