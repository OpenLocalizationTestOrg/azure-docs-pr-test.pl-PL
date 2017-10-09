---
title: informacje o wersji aaaStorSimple 8000 serii Update 2 | Dokumentacja firmy Microsoft
description: "Opisuje nowe funkcje hello, problemy i rozwiązania StorSimple 8000 serii Update 2."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: e2c8bffd-7fc5-4b77-b632-a4f59edacc3a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 36c75aad900c7b1286a924732967b8ee519a3d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-2-release-notes"></a>Informacje o wersji StorSimple 8000 serii Update 2
## <a name="overview"></a>Omówienie
Witaj poniższych informacjach o wersji opisano nowe funkcje hello i zidentyfikować problemy krytyczne Otwórz hello StorSimple 8000 serii Update 2. Zawierają one również listę hello oprogramowanie StorSimple, sterowników i aktualizacje oprogramowania układowego dysku zawarte w tej wersji. 

Aktualizacja 2 może być zastosowane tooany StorSimple urządzenie z systemem zlecenia (GA) lub Update 0.1 za pośrednictwem aktualizacji 1.2. Wersja urządzenia Hello skojarzone z Update 2 jest 6.3.9600.17673.

Zapoznaj się z tematem hello informacji zawartych w wersji hello, uwagi przed wdrożeniem hello aktualizacja w rozwiązaniu StorSimple.

> [!IMPORTANT]
> * Trwa około 4-7 godzin tooinstall tej aktualizacji (w tym aktualizacje systemu Windows hello). 
> * Aktualizacja 2 ma oprogramowania, LSI sterowników i aktualizacje oprogramowania układowego dysków SSD.
> * Dostępność nowych wersji nie może wyświetlić aktualizacje od razu, ponieważ jak etapowego wdrażania hello aktualizacji. Poczekaj kilka dni, a następnie skanowanie w poszukiwaniu aktualizacji ponownie jako te staną się dostępne wkrótce.
> 
> 

## <a name="whats-new-in-update-2"></a>Nowości w wersji Update 2
Aktualizacja 2 wprowadzono następujące nowe funkcje hello.

* **Przypięty lokalnie woluminach** — w poprzednich wersjach z serii StorSimple 8000 hello bloki danych zostały chmury toohello warstwowego na podstawie użycia. Nie było żadnych tooguarantee sposób, że bloki czy pozostanie na lokalnym. W wersji Update 2 podczas tworzenia woluminu, można wyznaczyć woluminu jako przypiętych lokalnie i podstawowe dane z tego woluminu nie będzie toohello warstwowych chmury. Nadal będzie migawek woluminów przypiętych lokalnie kopiowany toohello chmury dla kopii zapasowej, dzięki czemu hello chmury mogą służyć do celów odzyskiwania danych mobilności i odzyskiwaniem po awarii. Ponadto można zmienić hello typ woluminu (to znaczy przekonwertować woluminy przypięte toolocally woluminy warstwowe i tootiered woluminy przypięte lokalnie Konwertuj). 
* **Ulepszenia urządzenia wirtualnego StorSimple** — wcześniej hello z serii StorSimple 8000 umieszczona hello urządzenia wirtualnego jako rozwiązanie lub programowanie i testowanie odzyskiwania po awarii. Można było tylko jeden model (model 1100) urządzenia wirtualnego. Aktualizacja 2 wprowadza dwa modele urządzenia wirtualnego: 
  
  * 8010 (dawniej — poprawkami hello 1100) — bez zmian; ma pojemności 30 TB i korzysta z usługi Azure standard storage.
  * — 8020 ma 64 TB pojemności i korzysta z magazynu Azure Premium zwiększonej wydajności.
    
    Brak jednego wirtualnego dysku twardego dla obu modeli urządzenia wirtualnego (8010/8020). Przy pierwszym uruchomieniu urządzenia wirtualnego hello, wykryje hello platformy parametrów i dotyczy wersji modelu poprawne hello.
* **Ulepszenia sieci** — Update 2 zawiera następujące ulepszenia sieci hello:
  
  * Wiele kart sieciowych można włączyć dla chmury hello tak, aby tryb failover może wystąpić, jeśli karta sieciowa nie powiedzie się.
  * Ulepszenia routingu, o stałej metryki dla chmury włączone bloków.
  * Spróbuj wykonać ponownie online zasobów nie powiodło się przed trybu failover.
  * Nowe alerty błędów usługi.
* **Aktualizowanie ulepszenia** — w aktualizacji 1.2 i wcześniej, serii StorSimple 8000 hello został zaktualizowany przez dwa kanały: Aktualizacja klastra, iSCSI i itd i Microsoft Update do pliki binarne i oprogramowanie układowe systemu Windows.
    Aktualizacja 2 wykorzystuje usługę Microsoft Update dla wszystkich pakietów aktualizacji. Powinno to spowodować czasu tooless poprawki lub podczas pracy w trybie Failover. 
* **Aktualizacje oprogramowania układowego** — Witaj następujące oprogramowanie układowe dostępnych aktualizacji:
  
  * LSI: lsi_sas2.sys wersja produktu 2.00.72.10
  * Tylko SSD (Brak aktualizacji HDD): XMGG, XGEG KZ50, F6C2 i VR08
* **Obsługa aktywnego** — Update 2 umożliwia toopull Microsoft dodatkowe informacje diagnostyczne z hello urządzenia. Nasz zespół operacji identyfikuje urządzenia, które występują problemy, firma Microsoft są lepsze informacje wyposażone toocollect z hello urządzenia i diagnozowanie problemów. **Akceptowanie Update 2, umożliwia nam tooprovide ta obsługa aktywnego**.    

## <a name="issues-fixed-in-update-2"></a>Problemy, które usunięto w wersji Update 2
następujące tabele Hello zawiera podsumowanie problemów, które zostały usunięte w wersji 2 aktualizacji.    

| Nie. | Funkcja | Problem | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- |
| 1 |Interfejsy sieciowe |Po uaktualnieniu tooUpdate 1 hello usługi Menedżer StorSimple zgłosił, że porty dane2 i Data3 hello nie powiodło się na jeden kontroler. Ten problem został rozwiązany. |Tak |Nie |
| 2 |Aktualizacje |Po uaktualnieniu tooUpdate 1 alerty alarmu podczas hello klasycznego portalu Azure na wielu urządzeniach. Ten problem został rozwiązany. |Tak |Nie |
| 3 |Openstack uwierzytelniania |Korzystając z Openstack jako dostawcy usługi w chmurze, można komunikat o błędzie czy ciągu uwierzytelniania chmury jest za długa. Problem został rozwiązany. |Tak |Nie |

## <a name="known-issues-in-update-2"></a>Znane problemy w wersji Update 2
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
| 20 |Woluminów przypiętych lokalnie |Jeśli spróbujesz tooconvert wolumin warstwowy (utworzone i sklonowany z 1.2 aktualizacji lub starszym) wolumin przypięty lokalnie tooa urządzeniu zaczyna brakować miejsca lub brak awarii chmury, a następnie hello clone(s) może być uszkodzony. |Ten problem występuje tylko w przypadku woluminów, które zostały utworzone i sklonowany z przed aktualizacją 2 oprogramowania. Powinno to być rzadkim scenariusza. | | |
| 21 |Konwersja woluminu |Nie aktualizuj hello ACRs dołączonych tooa woluminu w trakcie konwersji woluminu (warstwowych toolocally przypięty lub na odwrót). Aktualizowanie hello ACRs może spowodować uszkodzenie danych. |W razie potrzeby zaktualizować konwersji woluminu wcześniejsze toohello ACRs hello i nie należy wprowadzać żadnych późniejszych ACR aktualizacji podczas konwersji hello jest w toku. | | |

## <a name="controller-and-firmware-updates-in-update-2"></a>Kontroler aktualizacje w wersji Update 2
Ta wersja aktualizuje hello sterowników i oprogramowania układowego dysku hello na urządzeniu.

* Aby uzyskać więcej informacji na temat oprogramowania układowego LSI hello aktualizacji, zobacz artykuł bazy wiedzy Microsoft Knowledge base 3121900. 
* Aby uzyskać więcej informacji na temat oprogramowania układowego dysku hello aktualizacji, zobacz artykuł bazy wiedzy Microsoft Knowledge base 3121899.

## <a name="virtual-device-updates-in-update-2"></a>Urządzenie wirtualne aktualizacji w wersji Update 2
Ta aktualizacja nie może być zastosowane toohello urządzenia wirtualnego. Nowe urządzenia wirtualnego należy utworzyć toobe. 

## <a name="next-step"></a>Następny krok
Dowiedz się, jak za[zainstalować aktualizacji 2](storsimple-install-update-2.md) na urządzeniu StorSimple.

