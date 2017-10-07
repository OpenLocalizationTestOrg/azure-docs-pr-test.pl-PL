---
title: informacje o wersji 1.2 aktualizacji serii aaaStorSimple 8000 | Dokumentacja firmy Microsoft
description: "Opis nowych funkcji hello, problemy i rozwiązania StorSimple 8000 serii aktualizacji 1.2."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c9aae87-6f77-44b8-b7fa-ebbdc9d8517c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7f564b794573fc3302ab15732e8dd85632ab9243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-12-release-notes-for-your-storsimple-8000-series-device"></a>Zaktualizuj informacje o wersji 1.2 dla danego urządzenia z serii StorSimple 8000

## <a name="overview"></a>Omówienie
Witaj poniższych informacjach o wersji opisano nowe funkcje hello i zidentyfikować problemy krytyczne Otwórz hello StorSimple 8000 serii aktualizacji 1.2. Zawierają one również listę oprogramowania StorSimple hello, sterowników i aktualizacje oprogramowania układowego dysku zawarte w tej wersji. 

Aktualizacja 1.2 może być zastosowane tooany StorSimple urządzenie z systemem zlecenia (GA), Update 0.1, Update 0.2 lub Update 0.3 oprogramowania. Aktualizacja 1.2 nie jest dostępna, jeśli urządzenie działa Update 1 lub Update 1.1. Jeśli urządzenie korzysta z wersji (GA), skontaktuj się z [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) tooassist o zainstalowanie tej aktualizacji.

Witaj następujące wersje oprogramowania rozszerzeń tabeli list hello urządzenia odpowiadającego tooUpdates 1, 1.1 i 1.2.

| Jeśli uruchomiona aktualizacji... | jest to wersja oprogramowania z urządzenia. |
| --- | --- |
| Aktualizacja 1.2 |6.3.9600.17584 |
| Aktualizacja 1.1 |6.3.9600.17521 |
| Update 1.0 |6.3.9600.17491 |

Zapoznaj się z tematem hello informacji zawartych w wersji hello, uwagi przed wdrożeniem hello aktualizacja w rozwiązaniu StorSimple. Aby uzyskać więcej informacji, zobacz temat jak zbyt[zainstalować 1.2 aktualizacji na urządzeniu StorSimple](storsimple-install-update-1.md). 

> [!IMPORTANT]
> * Trwa około 5 – 10 godzin tooinstall tej aktualizacji (w tym aktualizacje systemu Windows hello). 
> * Aktualizacja 1.2 ma oprogramowania LSI sterowników i aktualizacje oprogramowania układowego dysku. tooinstall, wykonaj instrukcje hello [zainstalować 1.2 aktualizacji na urządzeniu StorSimple](storsimple-install-update-1.md).
> * Dostępność nowych wersji nie może wyświetlić aktualizacje od razu, ponieważ jak etapowego wdrażania hello aktualizacji. Skanowanie w poszukiwaniu aktualizacji ponownie za kilka dni one zostanie wkrótce udostępnione.
> 
> 

## <a name="whats-new-in-update-12"></a>Nowości w aktualizacji 1.2
Te funkcje pierwszy zostały wydane z 1 aktualizacji, które zostało wykonane tooa dostępne ograniczony zestaw użytkowników. W wersji 1.2 aktualizacji hello większość użytkowników StorSimple hello zobaczy hello następujące nowe funkcje i ulepszenia:

* **Migracja z urządzeń z serii too8000 serii 5000 7000** — tej wersji wprowadzono nową funkcję migracji, umożliwiający hello StorSimple toomigrate użytkownicy urządzenia serii 5000 7000 ich danych tooa StorSimple 8000 serii fizyczne urządzenia lub Urządzenie wirtualne. Funkcja migracji Hello ma dwa propozycje wartość klucza:                                                                  
  
  * **Ciągłość prowadzenia działalności biznesowej**, włączając migracji istniejących danych na urządzeniach too8000 urządzenia 5000 7000 serii w serii.
  * **Ulepszona funkcja ofert hello 8000 serii urządzeń**, takich jak wydajność scentralizowane zarządzanie wielu urządzeń przy użyciu usługi Menedżer StorSimple, lepiej klasę urządzeń i aktualizacji oprogramowania układowego, urządzenie wirtualne, mobilności danych Funkcje i w przyszłości plan hello.
    
    Zobacz toohello [Przewodnik po migracji](http://www.microsoft.com/download/details.aspx?id=47322) szczegółowe informacje na temat toomigrate urządzenia StorSimple 5000 7000 serii tooan 8000 serii. 
* **Dostępność w portalu Azure dla instytucji rządowych hello** — jest teraz dostępna w portalu Azure dla instytucji rządowych hello StorSimple. Zobacz, jak za[wdrażania urządzenia StorSimple w portalu Azure dla instytucji rządowych hello](storsimple-deployment-walkthrough-gov.md).
* **Obsługę innych dostawców usług w chmurze** — Witaj Amazon S3, Amazon S3 z RRS, HP i OpenStack (beta) są inne obsługiwane dostawcom usług w chmurze.
* **Zaktualizuj toolatest interfejsów API magazynu** — w tej wersji StorSimple zostało zaktualizowane toohello najnowsze usługi Magazyn Azure interfejsów API. Urządzeń z serii StorSimple 8000 z wersjami oprogramowania przed aktualizacją 1 (wersja, 0.1, 0.2 i 0,3) są używane wersje hello starsze niż 17 lipca 2009 API usługi magazynu Azure. Zgodnie z hello zaktualizowane [powiadomienia o usunięciu wersje usług magazynu](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx), przez 1 sierpnia 2016 roku zostaną wycofane te interfejsy API. Konieczne jest zastosować tooAugust wcześniejsze hello StorSimple 8000 serii Update 1 1, 2016. Jeśli tak nie toodo, urządzenia StorSimple przestanie działa prawidłowo.
* **Obsługuje dla strefy nadmiarowego magazynu (ZRS)** — z hello uaktualnienia toohello najnowszą wersję hello interfejsy API usługi Storage, serii StorSimple 8000 hello będzie obsługiwać strefy nadmiarowego magazynu (ZRS) w tooLocally dodanie magazyn geograficznie nadmiarowy (LRS) i geograficznie nadmiarowego Magazyn (GRS). Zobacz toothis [artykuł na temat usługi Azure Storage nadmiarowość opcji](../storage/common/storage-redundancy.md) szczegółowe ZRS.
* **Ulepszone początkowej środowisko wdrożenia i zaktualizuj** — w tej wersji hello instalacji i procesy aktualizacji zostały rozszerzone. Hello instalacji za pomocą Kreatora instalacji hello jest ulepszone tooprovide opinii toohello użytkownika, jeśli ustawienia konfiguracji i zapory sieciowej hello są niepoprawne. Dostarczono dodatkowych diagnostyczne poleceń cmdlet toohelp o Rozwiązywanie problemów z sieci hello urządzenia. Zobacz hello [Rozwiązywanie problemów z artykułu wdrożenia](storsimple-troubleshoot-deployment.md) uzyskać więcej informacji o hello nowych diagnostycznych poleceń cmdlet używanych do rozwiązywania problemów.

## <a name="issues-fixed-in-update-12"></a>Problemy, które usunięto w wersji 1.2 aktualizacji
Witaj w poniższej tabeli przedstawiono podsumowanie problemów, które zostały usunięte w aktualizacjach 1.2, 1.1 i 1.    

| Nie. | Funkcja | Problem | Naprawiono w aktualizacji | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- | --- |
| 1 |Program Windows PowerShell dla StorSimple |Gdy użytkownik uzyskać zdalny dostęp urządzenia StorSimple hello przy użyciu programu Windows PowerShell dla urządzenia StorSimple, a następnie uruchomić Kreatora instalacji hello, tak szybko, jak dane 0 wejściowym IP wystąpił awarii. Ten błąd jest teraz usunięto w wersji Update 1. |Update 1 |Tak |Tak |
| 2 |Resetowanie do ustawień fabrycznych |W niektórych przypadkach po wykonaniu Resetowanie do ustawień fabrycznych urządzenia StorSimple hello zostało zatrzymane i wyświetlony ten komunikat: **toofactory resetowania jest w toku (faza 8)**. To się to zdarzyć, jeśli naciśnięciu klawiszy CTRL + C, gdy polecenie cmdlet hello jest w toku. Ten problem został rozwiązany teraz. |Update 1 |Tak |Nie |
| 3 |Resetowanie do ustawień fabrycznych |Po zresetowaniu fabryki nie powiodło się dwie kontrolera, były dozwolone tooproceed rejestracja urządzeń w usłudze. Spowodowała nieobsługiwany system konfiguracji. W pakiecie Update 1 jest wyświetlany komunikat o błędzie i rejestracji jest zablokowany na urządzeniu, że ma fabryki nie powiodło się resetowanie. |Update 1 |Tak |Nie |
| 4 |Resetowanie do ustawień fabrycznych |W niektórych przypadkach zostały zgłoszone alerty niezgodność dodatnią wartość false. Niezgodność niepoprawne już nie będą generowane alerty na urządzeniach z aktualizacją Update 1. |Update 1 |Tak |Nie |
| 5 |Resetowanie do ustawień fabrycznych |Jeśli resetowania do ustawień fabrycznych zostało przerwane przed toocompletion hello w trybie odzyskiwania urządzeniu wprowadzono i nie pozwala Ci tooaccess środowiska Windows PowerShell dla urządzenia StorSimple. Ten problem został rozwiązany teraz. |Update 1 |Tak |Nie |
| 6 |Odzyskiwanie po awarii |Usterki odzyskiwanie po awarii został rozwiązany, którym odzyskiwania po awarii nie powiedzie się podczas odnajdowania hello kopii zapasowych na urządzeniu docelowym hello. |Update 1 |Tak |Tak |
| 7 |Monitorowanie LED |W niektórych przypadkach monitorowania LED na powitania obu urządzenia nie poinformował prawidłowy stan. niebieski Hello LED został wyłączony. DANE 0 i LED 1 dane zostały miga, nawet gdy te interfejsy nie skonfigurowano. Witaj problem został rozwiązany i monitorowania LED teraz wskazać hello prawidłowy stan. |Update 1 |Tak |Nie |
| 8 |Monitorowanie LED |W niektórych przypadkach po zastosowaniu aktualizacji 1 światła hello niebieski na aktywnym kontrolerze hello wyłączone, umożliwiając tooidentify twardym powitania aktywnym kontrolerze. Ten problem został rozwiązany w tej wersji poprawki. |Aktualizacja 1.2 |Tak |Nie |
| 9 |Interfejsy sieciowe |W poprzednich wersjach urządzenia StorSimple skonfigurowany bez obsługi routingu bramy można umieścić w trybie offline. W tej wersji hello metrykę routingu dla interfejsu dane 0 wprowadzono hello najniższy; w związku z tym nawet jeśli inne interfejsy sieciowe są włączone w chmurze, cały ruch w chmurze hello z hello urządzenia zostaną przesłane za pośrednictwem interfejsu dane 0. |Update 1 |Tak |Tak |
| 10 |Tworzenie kopii zapasowych |Błąd w aktualizacji 1, który spowodował po 24 dni został rozwiązany toofail kopii zapasowych w poprawki hello wersji 1.1 aktualizacji. |Aktualizacja 1.1 |Tak |Tak |
| 11 |Tworzenie kopii zapasowych |Błąd w poprzednich wersjach spowodowało pogorszenie wydajności dla migawki w chmurze zmiany niskiej szybkości przetwarzania. Ten problem został rozwiązany w tej wersji poprawki. |Aktualizacja 1.2 |Tak |Tak |
| 12 |Aktualizacje |Błąd w aktualizacji 1, zgłosił nieudanego uaktualnienia, który spowodował toogo kontrolerów hello w trybie odzyskiwania, został usunięty w tej wersji poprawki. |Aktualizacja 1.2 |Tak |Tak |

## <a name="known-issues-in-update-12"></a>Znane problemy w aktualizacji 1.2
Witaj w poniższej tabeli przedstawiono podsumowanie znanych problemów występujących w tej wersji.

| Nie. | Funkcja | Problem | Komentarz/obejście | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- | --- |
| 1 |Dysku kworum |W rzadkich przypadkach odłączeniu większość hello dysków w obudowie EBOD hello urządzenia 8600 są wynikiem dysku kworum, następnie puli magazynów hello będzie w trybie offline. Pozostanie on w trybie offline nawet wtedy, gdy będzie nawiązywane hello dysków. |Konieczne będzie tooreboot hello urządzenia. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support, dalsze czynności. |Tak |Nie |
| 2 |Identyfikator niepoprawne kontrolera |Po wykonaniu zastąpić kontrolera kontrolera 0 mogą wyglądać jak kontrolera 1. Podczas wymiany kontrolera po załadowaniu hello obraz z węzła równorzędnego hello, identyfikator kontrolera hello można wyświetlane początkowo jako identyfikator hello równorzędnej kontrolera. W rzadkich przypadkach to zachowanie może być widoczny po ponownym uruchomieniu systemu. |Nie jest wymagana żadna akcja użytkownika. Sytuacja ta zostanie rozwiązany samoczynnie po zakończeniu hello zastępczego kontrolera. |Tak |Nie |
| 3 |Konta magazynu |Przy użyciu konta magazynu hello magazynu usługi toodelete hello jest to nieobsługiwany scenariusz. Spowoduje to tooa sytuacji, w której nie można pobrać danych użytkownika. |Tak |Tak | |
| 4 |Urządzenia trybu failover |Wiele przechodzenia kontener woluminów z hello tego samego urządzenia docelowe toodifferent urządzenia źródłowego nie jest obsługiwane. Urządzenie w tryb failover z urządzeń toomultiple jednego urządzenia martwy będzie hello kontenery woluminów na powitania najpierw przejścia w tryb failover urządzeń utraty własności danych. Po przełączeniu te kontenery woluminów są wyświetlane lub zachowywać się inaczej, podczas wyświetlania w hello klasycznego portalu Azure. | |Tak |Nie |
| 5 |Instalacja |Podczas StorSimple karty dla instalacji programu SharePoint należy tooprovide IP urządzenia, aby toofinish instalacji hello pomyślnie. | |Tak |Nie |
| 6 |Serwer proxy sieci Web |Jeśli ma konfigurację serwera proxy sieci web HTTPS jako hello określić protokół, będzie mieć wpływ na komunikacji usługi urządzeń i hello urządzenie przejdzie w trybie offline. Obsługa pakietów również zostanie wygenerowany w procesie hello, wykorzystywanie znaczące ilości zasobów na urządzeniu. |Upewnij się, że hello określony protokół adresu URL serwera proxy sieci web hello ma HTTP. Aby uzyskać więcej informacji, przejdź zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](storsimple-configure-web-proxy.md). |Tak |Nie |
| 7 |Serwer proxy sieci Web |Jeśli możesz skonfigurować i włączyć serwer proxy sieci web na zarejestrowanym urządzeniu, będzie konieczne toorestart hello aktywnym kontrolerze na urządzeniu. | |Tak |Nie |
| 8 |Wysoka chmury opóźnienia i wysokie obciążenie We/Wy |Gdy urządzenie StorSimple napotka kombinacją chmury w bardzo duże opóźnienia (kolejność sekund) i wysokie obciążenie We/Wy, hello urządzenia woluminów przechodzi w stan obniżeniem i hello operacji We/Wy może zakończyć się niepowodzeniem z powodu błędu "urządzenie nie jest gotowe". |Będzie konieczne kontrolery urządzeń hello ponowny rozruch toomanually lub wykonaj toorecover pracy awaryjnej urządzenia z tej sytuacji. |Tak |Nie |
| 9 |Azure PowerShell |Jeśli używasz polecenia cmdlet StorSimple hello **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object - oczekiwania najpierw 1 -** tooselect hello pierwszy obiekt, w którym można utworzyć nowy **VolumeContainer** obiekt hello cmdlet zwraca wszystkie obiekty hello. |Zawijanie hello polecenia cmdlet w nawiasach w następujący sposób: **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object - najpierw 1 - oczekiwania** |Tak |Tak |
| 10 |Migracja |W przypadku wielu kontenery woluminów są przekazywane do migracji, hello EAT dla najnowszej kopii zapasowej jest dokładna tylko dla pierwszego kontenera woluminów hello. Ponadto migracji równoległej rozpocznie się po hello 4 kopie zapasowe w pierwszym kontenera woluminów hello są migrowane. |Firma Microsoft zaleca migrować jeden kontener woluminów naraz. |Tak |Nie |
| 11 |Migracja |Po przywróceniu hello woluminy nie są dodawane toohello kopii zapasowej zasad lub hello dysku wirtualnego grupy. |Konieczne będzie tooadd tych zasad tworzenia kopii zapasowej tooa woluminy w kolejności toocreate tworzenia kopii zapasowych. |Tak |Tak |
| 12 |Migracja |Po zakończeniu migracji hello nie musi dostępu urządzenia z serii 5000/7000 hello hello migracji kontenerów danych. |Firma Microsoft zaleca, aby usunąć hello migracji kontenerów danych po migracji hello jest ukończone i zatwierdzone. |Tak |Nie |
| 13 |Klonowanie i odzyskiwania po awarii |Urządzenia StorSimple z aktualizacją Update 1 nie można sklonować lub wykonać odzyskiwanie po awarii tooa urządzenie z systemem przed aktualizacją oprogramowania 1. |Konieczne będzie tooupdate hello docelowego urządzenia tooUpdate 1 tooallow te operacje |Tak |Tak |
| 14 |Migracja |Kopia zapasowa konfiguracji migracji może zakończyć się niepowodzeniem na urządzeniu z serii 5000 7000 przypadku woluminu grup skojarzonych woluminów. |Usunąć wszystkie grupy pusty woluminu hello z nie skojarzone woluminy, a następnie spróbuj ponownie hello konfigurację z kopii zapasowej. |Tak |Nie |

## <a name="physical-device-updates-in-update-12"></a>Urządzenie fizyczne aktualizacji w 1.2 aktualizacji
Jeśli poprawka aktualizacja 1.2 jest stosowane tooa urządzenie fizyczne (uruchomionego tooUpdate wcześniejszych wersji 1), wersja oprogramowania hello zmieni too6.3.9600.17584.

## <a name="controller-and-firmware-updates-in-update-12"></a>Kontroler aktualizacje w 1.2 aktualizacji
Ta wersja aktualizuje hello sterowników i oprogramowania układowego dysku hello na urządzeniu.

* Aby uzyskać więcej informacji na temat aktualizacji kontrolera SAS hello, zobacz [aktualizacji 1 dla kontrolerów LSI SAS w Microsoft Azure StorSimple urządzenia](https://support.microsoft.com/kb/3043005). 
* Aby uzyskać więcej informacji na temat aktualizacji oprogramowania układowego dysku hello, zobacz [oprogramowania układowego dysku aktualizacji 1 dla programu Microsoft Azure StorSimple urządzenia](https://support.microsoft.com/kb/3063416).

## <a name="virtual-device-updates-in-update-12"></a>Urządzenie wirtualne aktualizacji w 1.2 aktualizacji
Ta aktualizacja nie może być zastosowane toohello urządzenia wirtualnego. Nowe urządzenia wirtualnego należy utworzyć toobe. 

## <a name="next-steps"></a>Następne kroki
* [Zainstaluj aktualizację 1.2 na urządzeniu](storsimple-install-update-1.md).

