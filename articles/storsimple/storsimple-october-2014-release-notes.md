---
title: "aaaStorSimple 8000 zaktualizować 0,1 informacje o wersji | Dokumentacja firmy Microsoft"
description: "Opisuje hello nowe funkcje i poprawki, problemy otwarte i dostępne obejścia hello października 2014 r. wersji Microsoft Azure StorSimple (aktualizacja 0,1)."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: fd35e3c3-4770-460c-999d-f72ab7053a20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 684e31cb0b356ec59a9d6c245e5d2bc062cc4f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-01-release-notes--october-2014"></a>StorSimple 8000 z aktualizacją Update 0.1 wersji — październik 2014 r.
## <a name="overview"></a>Omówienie
Hello następujące informacje o wersji zidentyfikować krytyczne problemy otwarte hello aktualizacji serii StorSimple 8000 0,1 wydane w ramach października 2014 r. Zawierają one również listę hello StorSimple oprogramowania i aktualizacje oprogramowania układowego zawarte w tej wersji. Po utworzeniu wersji StorSimple 8000 serii wersji hello został ogólnie dostępna w lipca 2014 r. i odpowiada wersji toosoftware 6.3.9600.17312 jest hello pierwszej wersji.  

Firma Microsoft zaleca skanowanie pod kątem oraz zastosować dostępne aktualizacje od razu po zainstalowaniu urządzenia hello. Można również włączyć funkcję aktualizacji automatycznych toodownload i zainstalować aktualizacje o wysokim priorytecie od firmy Microsoft, natychmiast po ich udostępnieniu. Aby uzyskać więcej informacji, zobacz temat jak zbyt[aktualizacja urządzenia StorSimple](storsimple-update-device.md).  

Przejrzyj hello informacje zawarte w informacjach o wersji hello przed wdrożeniem aktualizacji hello w rozwiązaniu StorSimple.  

> [!IMPORTANT]
> * Użyj hello usługi Menedżer StorSimple i nie programu Windows PowerShell dla StorSimple tooinstall powitalne października aktualizacji.  
> * aktualizacje Hello zwykle zajmują około 3 toocomplete godzin.  
> * Witaj października wersji StorSimple nie zawiera żadnych aktualizacji toohello urządzenia wirtualnego StorSimple. Można nadal stosować wszystkich dostępnych aktualizacji systemu Windows, w tym najnowsze poprawki zabezpieczeń, ale nie zobaczą zmiany w wersji dla urządzenia wirtualnego hello.  
> 
> 

Upewnij się, że hello następujące wymagania wstępne są niespełnienia tooupdating wcześniejsze urządzenia StorSimple.  

* Upewnij się, że zarówno kontrolery urządzeń są uruchomione przed rozpoczęciem skanowania aktualizacji. Jeśli nie działa albo kontrolera, hello skanowanie zakończy się niepowodzeniem. tooverify kontrolerów hello będące w dobrej kondycji, przejdź zbyt**stan sprzętu** w obszarze hello **konserwacji** strony. Jeśli istnieją składniki który **wymaga uwagi**, skontaktuj się z Microsoft Support przed kontynuowaniem.  
* Sprawdź, czy stałe adresy IP dla obu kontrolera 0 i kontrolera 1 są rutowalne i można połączyć toohello Internet, ponieważ są one używane do obsługi hello aktualizacje toohello urządzenia. Można użyć hello [polecenia cmdlet Test-Connection](https://technet.microsoft.com/library/hh849808.aspx) tooping znanego adresu poza hello sieci, takich jak outlook.com, tooverify, który hello kontroler ma toohello łączność poza siecią.  
* Upewnij się, że hello wymagane porty wyjściowe są dostępne na urządzeniu StorSimple dla komunikacji wychodzącej. Aby uzyskać więcej informacji, zobacz hello [wymagania dotyczące sieci dla urządzenia StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).  
* Jeśli wersja oprogramowania urządzenia hello jest starsza niż 6.3.9600.17312 (aktualizacja z października 2014 r.), należy wyłączyć hello porty dane 2 i dane 3, jeśli włączone, przed rozpoczęciem powitalne aktualizacji. Pozostawienie hello dane 2 i dane 3 porty włączona po zastosowaniu aktualizacji hello, może to spowodować toogo kontrolera Twoje urządzenie w trybie odzyskiwania. Należy pamiętać, po wyłączeniu hello interfejsów sieciowych, wszystkie woluminy hello skojarzone zostanie przełączone do trybu offline i hello we/wy zostanie zakłócone na czas trwania hello hello aktualizacji.  

## <a name="whats-new-in-hello-october-release"></a>Nowości w wersji października hello
Ta aktualizacja obejmuje hello następujące ulepszenia:

* Można teraz używać toomanage interfejsu użytkownika usługi Menedżer StorSimple hello kontrolerów urządzeń. dostępne są akcje zarządzania Hello ponownie, zamknij lub włączyć na kontrolerze. Aby uzyskać więcej informacji, przejdź zbyt[kontrolery urządzeń StorSimple zarządzanie](storsimple-manage-device-controller.md).  
* Można zaplanować zgodnie z kombinacji tooday tydzień i dzień czasowej alokacji przepustowości sieci WAN. Dzięki temu toomake lepsze wykorzystanie przepustowości sieci WAN poza godzinami szczytu. Przepustowość różne szablony są dozwolone dla kontenerów inny wolumin. Aby uzyskać więcej informacji, przejdź zbyt[zarządzania szablonami przepustowości StorSimple](storsimple-manage-bandwidth-templates.md).  
* Można skonfigurować powiadomienia e-mail tooproactively powiadomienia hello administratorom i innym istniejących lub planowanych prawdopodobnie problemy. Aby uzyskać więcej informacji, przejdź zbyt[Konfigurowanie ustawień alertów](storsimple-manage-alerts.md#configure-alert-settings).  

## <a name="issues-fixed-in-hello-october-release"></a>Problemy rozwiązane w wersji października hello
Witaj Poniższa tabela zawiera podsumowanie problemów, które zostały usunięte w ramach tej aktualizacji.  

| Nie. | Funkcja | Problem | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- |
| 1 |Interfejsy sieciowe |W hello poprzedniej wersji, hello interfejsy sieciowe dane 2 i dane 3 zostały zamienione hello oprogramowania. Ten problem został naprawiony w ramach tej aktualizacji. Wyczyść ustawienia hello i wyłączyć te interfejsy sieciowe, przed zainstalowaniem aktualizacji hello. Po zainstalowaniu aktualizacji hello, konieczne będzie tooreconfigure tych interfejsów. |Tak |Nie |
| 2 |Pakiet pomocy technicznej |W poprzedniej wersji hello, po przeprowadzeniu hello środowiska Windows PowerShell **HcsSupportPackage eksportu** polecenia cmdlet tooretrieve hello kontrolera zarządzania płytą główną (BMC) dzienniki operacji hello nie powiodło się z hello następujące ostrzeżenie: "tekst hello Operacja powiodła się na tym kontrolerze, ale nie na kontrolerze równorzędnej hello powodu toohello następujące błędy. Sprawdź, czy hello elementu równorzędnego jest w dobrej kondycji i czy bieżący węzeł hello można połączyć elementu równorzędnego toohello." Ten problem teraz zostanie usunięty. |Tak |Nie |
| 3 |Urządzenia trybu failover |W poprzedniej wersji hello było ryzyko niespójność danych Jeśli **odnajdywanie kopii zapasowej** zadanie nie powiodło się podczas pracy w trybie failover urządzenia. Ten problem teraz zostanie usunięty. |Tak |Nie |
| 4 |Urządzenia trybu failover |W hello poprzedniej wersji, przejściu w tryb failover urządzeń, kopie zapasowe były widoczne, ale kontenera woluminów skojarzone hello nie jest obecny na urządzeniu docelowym hello. Ten problem teraz zostanie usunięty. |Tak |Nie |
| 5 |Urządzenia trybu failover |W poprzedniej wersji hello wystąpił błąd w hello wyliczenie kopii zapasowych w chmurze podczas operacji przywracania rejestru hello, który może potencjalnie pozwolić na toodata niespójności, jeśli wystąpiły chmury problemy z połączeniem. |Tak |Nie |
| 6 |Aktualizacja oprogramowania układowego |W poprzedniej wersji hello hello zadanie aktualizacji oprogramowania układowego urządzenia nie powiodła się i wyświetlony błąd, co podane hello poleceń cmdlet nie jest rozpoznawanym, czy w związku z tym nie można zaktualizować tego hello. Kontroler Hello następnie przeszedł do trybu odzyskiwania. Ten problem teraz zostanie usunięty. |Tak |Nie |
| 7 |Instalacja |Teraz Naprawiono błędy spowodowane hello urządzenia nie są obrazami poprawnie podczas instalacji. |Tak |Nie |
| 8 |Resetowanie do ustawień fabrycznych |Teraz można opcjonalnie pomijania sprawdzania oprogramowania układowego hello na resetowanie do ustawień fabrycznych. Jest to zmiana z hello poprzedniej wersji. |Tak |Nie |
| 9 |Resetowanie do ustawień fabrycznych |W poprzedniej wersji hello podczas uruchamiania polecenia cmdlet resetowania fabryki kontroli wersji oprogramowania układowego wprowadzono tylko dla niektórych składników sprzętowych. Po ponownym hello w procesie hello, która może spowodować toofail resetowania hello wprowadzono dodatkowe oprogramowanie układowe kontroli. Ta poprawka zapewnia, że wszystkie testy oprogramowania układowego hello są wykonany, gdy uruchomiono polecenie cmdlet resetowania fabryki hello i przed hello systemu pierwszy ponowny rozruch. |Tak |Nie |
| 10 |Obracanie klucza konta magazynu |Witaj **Invoke HcsmServiceDataEncryptionKeyChange** polecenia cmdlet używane klucze konta magazynu hello toorotate teraz monity hello klucza szyfrowania danych usługi hello tooenter użytkownika. Jest to zmiana z poprzedniej wersji hello, w których hello klucza szyfrowania danych usługi został przekazany jako parametr wbudowanego. |Tak |Nie |
| 11 |Powrót po awarii w ciągu 24 godzin |Podczas odzyskiwania po awarii oczyszczania hello na powitania urządzenia źródłowego nie nastąpiły toofail bezpośrednio, powodując powrotu po awarii. Ten problem został naprawiony w tej wersji. |Tak |Nie |

## <a name="known-issues-in-hello-october-release"></a>Znane problemy w wersji października hello
Witaj w poniższej tabeli przedstawiono podsumowanie znanych problemów występujących w tej wersji.

| Nie. | Funkcja | Problem | Komentarz/obejście | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- | --- |
| 1 |Resetowanie do ustawień fabrycznych |W niektórych przypadkach po wykonaniu Resetowanie do ustawień fabrycznych hello urządzenia StorSimple może zostać zatrzymane i wyświetla ten komunikat: **toofactory resetowania jest w toku (faza 8)**. Dzieje się tak, jeśli naciśnij klawisze CTRL + C, gdy polecenie cmdlet hello jest w toku. |Naciskaj klawisze CTRL + C po zainicjowaniu resetowania do ustawień fabrycznych. Jeśli jesteś już w tym stanie, skontaktuj się z Microsoft Support, dalsze czynności. |Tak |Nie |
| 2 |Resetowanie do ustawień fabrycznych |Czy urządzenia StorSimple, która jest aktualizowana w wersji tooOctober 2014 GA nie Resetowanie do ustawień fabrycznych. |Ta operacja działa tylko, jeśli zainstalowano poprawkę. Skontaktuj się z Microsoft Support tooget tej poprawki wymagane. |Tak |Nie |
| 3 |Dysku kworum |W rzadkich przypadkach odłączeniu większość hello dysków w obudowie EBOD hello urządzenia 8600 są wynikiem dysku kworum, następnie puli magazynów hello będzie w trybie offline. Pozostanie on w trybie offline nawet wtedy, gdy będzie nawiązywane hello dysków. |Konieczne będzie tooreboot hello urządzenia. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support, dalsze czynności. |Tak |Nie |
| 4 |Błędy migawkę chmury |W rzadkich przypadkach migawka w chmurze może zakończyć się niepowodzeniem z powodu błędu hello **osiągnięto limit kopii zapasowej maksymalnie**. Dzieje się tak, jeśli przekracza 255 klony online na powitania jednym urządzeniu, z hello tego samego oryginalnego woluminu, który został usunięty. | |Tak |Tak |
| 5 |Identyfikator niepoprawne kontrolera |Po wykonaniu zastąpić kontrolera kontrolera 0 mogą wyglądać jak kontrolera 1. Podczas wymiany kontrolera po załadowaniu hello obraz z węzła równorzędnego hello, identyfikator kontrolera hello można wyświetlane początkowo jako identyfikator hello równorzędnej kontrolera. W rzadkich przypadkach to zachowanie może być widoczny po ponownym uruchomieniu systemu. |Nie jest wymagana żadna akcja użytkownika. Sytuacja ta zostanie rozwiązany samoczynnie po zakończeniu hello zastępczego kontrolera. |Tak |Nie |
| 6 |Wykresy monitorowania urządzeń |W hello usługi Menedżer StorSimple wykresy monitorowania urządzenia hello nie działają w przypadku podstawowych lub w konfiguracji serwera proxy hello hello urządzenia jest włączone uwierzytelnianie NTLM. |Zmodyfikuj konfigurację serwera proxy sieci web hello hello urządzenia zarejestrowane przy użyciu usługi Menedżer StorSimple, że uwierzytelnianie ustawiono tooNONE. toodo tego hello hello wykonywania programu Windows PowerShell polecenia cmdlet StorSimple Set-HcsWebProxy. |Tak |Tak |
| 7 |Konta magazynu |Przy użyciu konta magazynu hello magazynu usługi toodelete hello jest to nieobsługiwany scenariusz. Spowoduje to tooa sytuacji, w której nie można pobrać danych użytkownika. | |Tak |Tak |
| 8 |Urządzenia trybu failover |Wiele przechodzenia kontener woluminów z hello tego samego urządzenia docelowe toodifferent urządzenia źródłowego nie jest obsługiwane. |Tryb failover z urządzeń toomultiple jednego urządzenia martwy spowoduje, że hello kontenery woluminów na powitania najpierw przejścia w tryb failover urządzeń utraty własności danych. Po przełączeniu te kontenery woluminów są wyświetlane lub zachowywać się inaczej, podczas wyświetlania w hello klasycznego portalu Azure. |Tak |Nie |
| 9 |Instalacja |Podczas StorSimple karty dla instalacji programu SharePoint należy tooprovide IP urządzenia, aby toofinish instalacji hello pomyślnie. | |Tak |Nie |
| 10 |Serwer proxy sieci Web |Jeśli ma konfigurację serwera proxy sieci web HTTPS jako hello określić protokół, będzie mieć wpływ na komunikacji usługi urządzeń i hello urządzenie przejdzie w trybie offline. Obsługa pakietów również zostanie wygenerowany w procesie hello, wykorzystywanie znaczące ilości zasobów na urządzeniu. |Upewnij się, że hello określony protokół adresu URL serwera proxy sieci web hello ma HTTP. Więcej informacji na temat zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](storsimple-configure-web-proxy.md). |Tak |Nie |
| 11 |Serwer proxy sieci Web |Jeśli możesz skonfigurować i włączyć serwer proxy sieci web na zarejestrowanym urządzeniu, będzie konieczne toorestart hello aktywnym kontrolerze na urządzeniu. | |Tak |Nie |
| 12 |Wysoka chmury opóźnienia i wysokie obciążenie We/Wy |Gdy urządzenie StorSimple napotka kombinacją chmury w bardzo duże opóźnienia (kolejność sekund) i wysokie obciążenie We/Wy, hello urządzenia woluminów przechodzi w stan obniżeniem i hello operacji We/Wy może zakończyć się niepowodzeniem z powodu błędu "urządzenie nie jest gotowe". |Będzie konieczne kontrolery urządzeń hello ponowny rozruch toomanually lub wykonaj toorecover pracy awaryjnej urządzenia z tej sytuacji. |Tak |Nie |

## <a name="physical-device-updates-in-hello-october-release"></a>Urządzenie fizyczne aktualizacji w wersji października hello
Te aktualizacje zostały zastosowane tooa urządzenia fizycznego, wersji oprogramowania hello zmienia too6.3.9600.17312. Jeżeli nie określono inaczej, te informacje o wersji zastosować modele tooall hello urządzenia StorSimple. Aby uzyskać więcej informacji na temat tych aktualizacji, zobacz [aktualizacji oprogramowania urządzenia fizycznego października 2014 r. dla systemu Microsoft Azure StorSimple urządzenia](http://support.microsoft.com/kb/2986997).  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-october-release"></a>Magistrali Serial attached SCSI (SAS) kontrolera aktualizacje w wersji października hello
Ta wersja aktualizuje hello sterowników i oprogramowania układowego hello na powitania kontrolera SAS z urządzenia fizycznego. Aby uzyskać więcej informacji na temat aktualizacji kontrolera SAS hello, zobacz [aktualizacji października 2014 r. dla kontrolerów LSI SAS w Microsoft Azure StorSimple urządzenia](http://support.microsoft.com/kb/2987020).   

Aktualizacja zbiorcza oprogramowania układowego niezawodnością problemy z składników sprzętowych urządzeń hello ma również zastosowanie tej wersji. Aby uzyskać więcej informacji na temat aktualizacji oprogramowania układowego hello, zobacz [aktualizacji oprogramowania układowego października 2014 r. dla systemu Microsoft Azure StorSimple urządzenia](http://support.microsoft.com/kb/2987015).  

## <a name="virtual-device-updates-in-hello-october-release"></a>Urządzenie wirtualne aktualizacji w wersji października hello
Ta wersja nie zawiera żadnych aktualizacji dla urządzenia wirtualnego hello. Zastosowanie tej aktualizacji nie spowoduje zmiany wersji oprogramowania hello urządzenia wirtualnego.

