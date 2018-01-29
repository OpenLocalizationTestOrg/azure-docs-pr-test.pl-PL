---
title: Informacje o wersji StorSimple 8000 serii Update 2 | Dokumentacja firmy Microsoft
description: "Opisuje nowe funkcje, problemy i rozwiązania StorSimple 8000 serii Update 2."
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
ms.date: 11/03/2017
ms.author: v-sharos
ms.openlocfilehash: 285c5abf574544737f3d30981a6c5b8f9548922a
ms.sourcegitcommit: 0930aabc3ede63240f60c2c61baa88ac6576c508
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/07/2017
---
# <a name="storsimple-8000-series-update-2-release-notes"></a>Informacje o wersji StorSimple 8000 serii Update 2
> [!NOTE]
> Klasyczny portal dla urządzenia StorSimple jest przestarzały. Menedżerowie urządzenia StorSimple zostanie automatycznie przełączona do nowego portalu Azure, zgodnie z harmonogramem wycofywanie. Otrzymasz wiadomość e-mail i powiadomienie portalu dla tego przeniesienia. Ten dokument również zostaną wkrótce wycofane. Wszelkie pytania dotyczące przeniesienie, zobacz [— często zadawane pytania: przejść do portalu Azure](storsimple-8000-move-azure-portal-faq.md).

## <a name="overview"></a>Omówienie
Poniższe informacje o wersji opisano nowe funkcje i zidentyfikować problemy krytyczne Otwórz StorSimple 8000 serii Update 2. Zawierają one również listę oprogramowania StorSimple, sterowników i aktualizacje oprogramowania układowego dysku zawarte w tej wersji. 

Aktualizacja 2 może odnosić się do każdego urządzenia StorSimple z wersji (GA) lub Update 0.1 za pośrednictwem aktualizacji 1.2. Wersja urządzenia skojarzone z Update 2 jest 6.3.9600.17673.

Przejrzyj informacje zawarte w informacjach o wersji przed wdrożeniem aktualizacji w rozwiązaniu StorSimple.

> [!IMPORTANT]
> * Trwa około 4-7 godzin, aby zainstalować tę aktualizację (w tym aktualizacje systemu Windows). 
> * Aktualizacja 2 ma oprogramowania, LSI sterowników i aktualizacje oprogramowania układowego dysków SSD.
> * Dostępność nowych wersji nie może wyświetlić aktualizacje od razu, ponieważ jak etapowego wdrażania aktualizacji. Poczekaj kilka dni, a następnie skanowanie w poszukiwaniu aktualizacji ponownie jako te staną się dostępne wkrótce.
> 
> 

## <a name="whats-new-in-update-2"></a>Nowości w wersji Update 2
Aktualizacja 2 wprowadzono następujące nowe funkcje.

* **Przypięty lokalnie woluminach** — w poprzednich wersjach z serii StorSimple 8000 bloki danych zostały warstwy do chmury na podstawie użycia. Nie można było ma gwarancji, że bloki czy pozostanie na lokalnym. W wersji Update 2 podczas tworzenia woluminu, można wyznaczyć woluminu jako przypiętych lokalnie i podstawowe dane z tego woluminu do nie będzie można warstwy do chmury. Migawki woluminów przypiętych lokalnie nadal zostaną skopiowane do chmury na potrzeby tworzenia kopii zapasowej, dzięki czemu chmury mogą służyć do celów odzyskiwania danych mobilności i odzyskiwaniem po awarii. Ponadto można zmienić typu woluminu (to, że Konwertuj do warstwy woluminów woluminów przypiętych lokalnie i woluminów przekonwertować przypięty lokalnie do warstwy). 
* **Ulepszenia urządzenia wirtualnego StorSimple** — wcześniej serii StorSimple 8000 umieszczona urządzenia wirtualnego jako rozwiązanie lub programowanie i testowanie odzyskiwania po awarii. Można było tylko jeden model (model 1100) urządzenia wirtualnego. Aktualizacja 2 wprowadza dwa modele urządzenia wirtualnego: 
  
  * 8010 (wcześniej nazywanych 1100) — bez zmian; ma pojemności 30 TB i korzysta z usługi Azure standard storage.
  * — 8020 ma 64 TB pojemności i korzysta z magazynu Azure Premium zwiększonej wydajności.
    
    Brak jednego wirtualnego dysku twardego dla obu modeli urządzenia wirtualnego (8010/8020). Przy pierwszym uruchomieniu urządzenia wirtualnego, wykryje parametry platformy i dotyczy wersji modelu poprawne.
* **Ulepszenia sieci** — Update 2 zawiera następujące ulepszenia sieci:
  
  * Wiele kart sieciowych można włączyć dla chmury, dzięki czemu trybu failover może wystąpić, jeśli karta sieciowa nie powiedzie się.
  * Ulepszenia routingu, o stałej metryki dla chmury włączone bloków.
  * Spróbuj wykonać ponownie online zasobów nie powiodło się przed trybu failover.
  * Nowe alerty błędów usługi.
* **Aktualizowanie ulepszenia** — w aktualizacji 1.2 i wcześniej, serii StorSimple 8000 został zaktualizowany przez dwa kanały: Aktualizacja klastra, iSCSI i itd i Microsoft Update do pliki binarne i oprogramowanie układowe systemu Windows.
    Aktualizacja 2 wykorzystuje usługę Microsoft Update dla wszystkich pakietów aktualizacji. Powinno to spowodować mniej czasu poprawki lub podczas pracy w trybie Failover. 
* **Aktualizacje oprogramowania układowego** — następujące oprogramowanie układowe dostępnych aktualizacji:
  
  * LSI: lsi_sas2.sys wersja produktu 2.00.72.10
  * Tylko SSD (Brak aktualizacji HDD): XMGG, XGEG KZ50, F6C2 i VR08
* **Obsługa aktywnego** — Update 2 umożliwia firmie Microsoft ściągnięcia dodatkowych informacji diagnostycznych z urządzenia. Gdy działu operacji identyfikuje urządzenia, które występują problemy, firma Microsoft mają większe możliwości zbierania informacji z urządzenia i diagnozowanie problemów. **Akceptowanie Update 2, umożliwia firmie Microsoft w celu obsługi aktywnego**.    

## <a name="issues-fixed-in-update-2"></a>Problemy, które usunięto w wersji Update 2
Poniższe tabele zawiera podsumowanie problemów, które zostały usunięte w wersji 2 aktualizacji.    

| Nie. | Funkcja | Problem | Dotyczy urządzenia fizycznego | Dotyczy urządzenia wirtualnego |
| --- | --- | --- | --- | --- |
| 1 |Interfejsy sieciowe |Po uaktualnieniu do aktualizacji 1 usługi Menedżer StorSimple zgłosił, że porty dane2 i Data3 nie powiodło się na jeden kontroler. Ten problem został rozwiązany. |Tak |Nie |
| 2 |Aktualizacje |Po uaktualnieniu do aktualizacji 1 alerty alarmu wystąpił w klasycznym portalu Azure na wielu urządzeniach. Ten problem został rozwiązany. |Tak |Nie |
| 3 |Openstack uwierzytelniania |Korzystając z Openstack jako dostawcy usługi w chmurze, można komunikat o błędzie czy ciągu uwierzytelniania chmury jest za długa. Problem został rozwiązany. |Tak |Nie |

## <a name="known-issues-in-update-2"></a>Znane problemy w wersji Update 2
Poniższa tabela zawiera podsumowanie znanych problemów występujących w tej wersji.

| Nie. | Funkcja | Problem | Komentarz / obejście problemu | Dotyczy urządzenia fizycznego | Dotyczy urządzenia wirtualnego |
| --- | --- | --- | --- | --- | --- |
| 1 |Dysku kworum |W rzadkich przypadkach jeśli większość dysków w obudowie EBOD urządzenia 8600 rozłączenia spowodować, że nie ma dysku kworum, następnie puli magazynu przejdzie w trybie offline. Pozostanie on w trybie offline nawet wtedy, gdy dyski są podłączeni ponownie. |Należy ponowne uruchomienie urządzenia. Jeśli problem będzie się powtarzać, skontaktuj się z Microsoft Support, dalsze czynności. |Tak |Nie |
| 2 |Identyfikator niepoprawne kontrolera |Po wykonaniu zastąpić kontrolera kontrolera 0 mogą wyglądać jak kontrolera 1. Podczas wymiany kontrolera podczas ładowania obrazu z węzła równorzędnego identyfikator kontrolera można wyświetlane początkowo jako identyfikator kontrolera elementu równorzędnego. W rzadkich przypadkach to zachowanie może być widoczny po ponownym uruchomieniu systemu. |Nie jest wymagana żadna akcja użytkownika. Sytuacja ta zostanie rozwiązany samoczynnie po zakończeniu zastąpienia kontrolera. |Tak |Nie |
| 3 |Konta magazynu |Korzystanie z usługi Magazyn można usunąć konta magazynu jest to nieobsługiwany scenariusz. Spowoduje to doprowadzić do sytuacji, w której nie można pobrać danych użytkownika. | |Tak |Tak |
| 4 |Urządzenia trybu failover |Wiele przechodzenia kontener woluminów z tego samego urządzenia źródłowego na urządzeniach inny element docelowy nie jest obsługiwane. Tryb failover z jednym urządzeniu martwy na wielu urządzeniach spowoduje, że kontenery woluminów na pierwszym przejścia w tryb failover urządzeń utraty własności danych. Po przełączeniu te kontenery woluminów są wyświetlane lub zachowywać się inaczej, podczas wyświetlania w klasycznym portalu Azure. | |Tak |Nie |
| 5 |Instalacja |Podczas StorSimple karty dla instalacji programu SharePoint musisz podać IP urządzenia, aby instalacja zakończyło się pomyślnie. | |Tak |Nie |
| 6 |Serwer proxy sieci Web |Jeśli konfiguracji serwera proxy sieci web ma określony protokół HTTPS, będzie mieć wpływ na komunikacji usługi urządzeń i urządzenie przejdzie w tryb offline. Obsługa pakietów również zostanie wygenerowany w procesie wykorzystywanie znaczące ilości zasobów na urządzeniu. |Upewnij się, że adres URL serwera proxy sieci web ma HTTP jako protokół określony. Aby uzyskać więcej informacji, zobacz temat [Konfigurowanie serwera proxy sieci Web dla urządzenia](storsimple-configure-web-proxy.md). |Tak |Nie |
| 7 |Serwer proxy sieci Web |Jeśli możesz skonfigurować i włączyć serwer proxy sieci web na zarejestrowanym urządzeniu, będzie konieczne ponowne uruchomienie kontrolera active na urządzeniu. | |Tak |Nie |
| 8 |Wysoka chmury opóźnienia i wysokie obciążenie We/Wy |Gdy urządzenie StorSimple napotka kombinacją chmury w bardzo duże opóźnienia (kolejność sekund) i wysokie obciążenie We/Wy, woluminy urządzenia przechodzi w stan obniżeniem i operacji We/Wy może zakończyć się niepowodzeniem z powodu błędu "urządzenie nie jest gotowe". |Konieczne będzie ręczne ponownego uruchamiania kontrolerów urządzeń lub urządzeń w tryb failover do odzyskania z tej sytuacji. |Tak |Nie |
| 9 |Azure PowerShell |Jeśli używasz polecenia cmdlet StorSimple **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object - oczekiwania najpierw 1 -** aby zaznaczyć pierwszy obiekt, w którym można utworzyć nowy **VolumeContainer** obiektu, polecenie cmdlet zwraca wszystkie obiekty. |Opakuj polecenie cmdlet w nawiasach w następujący sposób: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - najpierw 1 - oczekiwania** |Tak |Tak |
| 10 |Migracja |W przypadku wielu kontenery woluminów są przekazywane do migracji, EAT dla najnowszej kopii zapasowej jest dokładna tylko dla pierwszego kontenera woluminów. Ponadto migracji równoległej rozpocznie się po pierwszych 4 kopie zapasowe w pierwszym kontenera woluminów są migrowane. |Firma Microsoft zaleca migrować jeden kontener woluminów naraz. |Tak |Nie |
| 11 |Migracja |Po przywróceniu woluminy nie są dodawane do zasad tworzenia kopii zapasowej lub grupie dysków wirtualnych. |Należy dodać te woluminy do zasad tworzenia kopii zapasowej, aby tworzenie kopii zapasowych. |Tak |Tak |
| 12 |Migracja |Po zakończeniu migracji urządzenia z serii 5000/7000 Brak dostępu do kontenerów migrowanych danych. |Zaleca się usunąć kontenery migrowanych danych, po migracji ukończone i zatwierdzone. |Tak |Nie |
| 13 |Klonowanie i odzyskiwania po awarii |Urządzenia StorSimple z aktualizacją Update 1 nie można sklonować lub wykonać odzyskiwanie po awarii na urządzeniu z systemem przed aktualizacją oprogramowania 1. |Należy zaktualizować urządzenie do aktualizacji 1, aby umożliwić te operacje |Tak |Tak |
| 14 |Migracja |Kopia zapasowa konfiguracji migracji może zakończyć się niepowodzeniem na urządzeniu z serii 5000 7000 przypadku woluminu grup skojarzonych woluminów. |Usunąć wszystkie grupy pusty woluminu z nie skojarzone woluminy, a następnie spróbuj ponownie konfigurację kopii zapasowej. |Tak |Nie |
| 15 |Polecenia cmdlet programu PowerShell systemu Azure i woluminów przypiętych lokalnie |Nie można utworzyć woluminu przypiętego lokalnie za pomocą poleceń cmdlet programu Azure PowerShell. (Będzie warstwowa każdym woluminie tworzonych za pomocą programu Azure PowerShell.) |Aby skonfigurować woluminów przypiętych lokalnie zawsze używać usługi Menedżer StorSimple. |Tak |Nie |
| 16 |Miejsce dostępne dla woluminów przypiętych lokalnie |Jeśli usuniesz woluminu przypiętego lokalnie, miejsce dostępne dla nowych woluminów mogły nie zostać zaktualizowane od razu. Aktualizacje usługi Menedżer StorSimple lokalne miejsce dostępne mniej więcej co godzinę. |Poczekaj, aż godziny przed podjęciem próby utworzenia nowego woluminu. |Tak |Nie |
| 17 |Woluminów przypiętych lokalnie |Zadanie przywracania przedstawia tymczasowego migawki kopii zapasowej w katalogu kopii zapasowej, ale tylko na czas trwania zadania przywracania. Ponadto udostępnia ona grupy dysków wirtualnych z prefiksem **tmpCollection** na **zasady tworzenia kopii zapasowej** strony, ale tylko na czas trwania zadania przywracania. |Ten problem może wystąpić, jeśli zadanie przywracania ma przypięty tylko lokalnie woluminów lub mieszane lokalnie woluminów przypiętych i warstwowego. Jeśli zadanie przywracania zawiera tylko woluminów warstwowych, ten problem nie zostanie przeprowadzona. Interwencja użytkownika nie jest wymagane. |Tak |Nie |
| 18 |Woluminów przypiętych lokalnie |Jeśli anulowanie zadania przywracania, a do kontrolera pracy awaryjnej natychmiast po wyświetli zadanie **przywracania** zamiast **anulowane**. Jeśli zadanie przywracania kończy się niepowodzeniem, a do kontrolera pracy awaryjnej natychmiast po wyświetli zadanie **przywracania** **anulowane** zamiast. |Ten problem może wystąpić, jeśli zadanie przywracania ma przypięty tylko lokalnie woluminów lub mieszane lokalnie woluminów przypiętych i warstwowego. Jeśli zadanie przywracania zawiera tylko woluminów warstwowych, ten problem nie zostanie przeprowadzona. Interwencja użytkownika nie jest wymagane. |Tak |Nie |
| 19 |Woluminów przypiętych lokalnie |Anulowanie zadania przywracania, lub jeśli przywracania kończy się niepowodzeniem, a następnie do kontrolera pracy awaryjnej, zadanie przywracania dodatkowe pojawi się na **zadania** strony. |Ten problem może wystąpić, jeśli zadanie przywracania ma przypięty tylko lokalnie woluminów lub mieszane lokalnie woluminów przypiętych i warstwowego. Jeśli zadanie przywracania zawiera tylko woluminów warstwowych, ten problem nie zostanie przeprowadzona. Interwencja użytkownika nie jest wymagane. |Tak |Nie |
| 20 |Woluminów przypiętych lokalnie |Jeśli użytkownik próbuje przekonwertować wolumin warstwowy (utworzone i sklonowany z 1.2 aktualizacji lub starszym) do woluminu przypiętego lokalnie i urządzeniu zaczyna brakować miejsca lub awarii chmury, clone(s) może być uszkodzony. |Ten problem występuje tylko w przypadku woluminów, które zostały utworzone i sklonowany z przed aktualizacją 2 oprogramowania. Powinno to być rzadkim scenariusza. | | |
| 21 |Konwersja woluminu |Nie aktualizuj ACRs dołączone do woluminu w trakcie konwersji woluminu (warstwowa do przypięty lokalnie lub na odwrót). Aktualizowanie ACRs może spowodować uszkodzenie danych. |W razie potrzeby zaktualizuj ACRs przed konwersji woluminu, a nie wprowadzaj żadnych późniejszych ACR aktualizacje w trakcie konwersji. | | |

## <a name="controller-and-firmware-updates-in-update-2"></a>Kontroler aktualizacje w wersji Update 2
Ta wersja aktualizacje sterowników i oprogramowania układowego dysku na urządzeniu.

* Aby uzyskać więcej informacji na temat oprogramowania układowego LSI aktualizacji, zobacz artykuł bazy wiedzy Microsoft Knowledge base 3121900. 
* Aby uzyskać więcej informacji na temat oprogramowania układowego dysku aktualizacji, zobacz artykuł bazy wiedzy Microsoft Knowledge base 3121899.

## <a name="virtual-device-updates-in-update-2"></a>Urządzenie wirtualne aktualizacji w wersji Update 2
Ta aktualizacja nie można zastosować do urządzenia wirtualnego. Nowe urządzenia wirtualnego będzie muszą zostać utworzone. 

## <a name="next-step"></a>Następny krok
Dowiedz się, jak [zainstalować aktualizacji 2](storsimple-install-update-2.md) na urządzeniu StorSimple.

