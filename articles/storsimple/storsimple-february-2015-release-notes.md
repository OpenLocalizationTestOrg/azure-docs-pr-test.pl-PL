---
title: "aaaStorSimple 8000 zaktualizować 0,3 informacje o wersji | Dokumentacja firmy Microsoft"
description: "Opisuje hello nowe funkcje i poprawki, problemy otwarte i dostępne obejścia hello luty 2015 release Microsoft Azure StorSimple (aktualizacja 0,3)."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: b01bfd04-f9f8-45f4-ade8-95ac2b979e6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 53638f9d286b2085c6b45f9e3fae75c34fc73e7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-03-release-notes---february-2015"></a>Informacje o wersji 0,3 StorSimple 8000 z aktualizacją Update — luty 2015
## <a name="overview"></a>Omówienie
Hello następujące informacje o wersji zidentyfikować problemy krytyczne Otwórz hello aktualizacji serii StorSimple 8000 0,3 wydane w ramach luty 2015. Zawierają one również listę hello StorSimple oprogramowania i aktualizacje oprogramowania układowego zawarte w tej wersji. Trzecie wydanie hello jest po wersji StorSimple 8000 serii wersji hello ogólnie dostępna w lipca 2014.

Ta aktualizacja nie powoduje zmiany wersji oprogramowania urządzenia hello hello stycznia Update. Wykonywana wersja toobe 6.3.9600.17312. Można potwierdzić, sprawdzając powitania po zainstalowaniu tej aktualizacji hello **ostatniej aktualizacji** daty. W przypadku daty hello 2/10/2015 lub nowszego, następnie hello aktualizacja została zainstalowana pomyślnie.  

Firma Microsoft zaleca skanowanie pod kątem oraz zastosować dostępne aktualizacje od razu po zainstalowaniu urządzenia StorSimple. Można również włączyć funkcję aktualizacji automatycznych toodownload i zainstalować aktualizacje o wysokim priorytecie od firmy Microsoft, natychmiast po ich udostępnieniu. Aby uzyskać więcej informacji, zobacz [aktualizacja urządzenia StorSimple](storsimple-update-device.md).  

Zapoznaj się z tematem hello informacji zawartych w wersji hello, uwagi przed wdrożeniem hello aktualizacja w rozwiązaniu StorSimple.  

> [!IMPORTANT]
> * Użyj usługi Menedżer StorSimple hello i nie środowiska Windows PowerShell dla StorSimple tooinstall hello lutego aktualizacji.   
> * Trwa około godzinę tooinstall tej aktualizacji. Jednak jeśli instalujesz aktualizacje zbiorcze hello może potrwać około 3 toocomplete godzin.  
> * Witaj lutego wersji StorSimple nie zawiera żadnych aktualizacji toohello urządzenia wirtualnego StorSimple. Można stosować wszystkie dostępne aktualizacje toohello wirtualnego urządzenia Windows, łącznie z ostatnich zabezpieczeń poprawki, ale nie zobaczą zmiany w wersji dla urządzenia wirtualnego hello.  
> 
> 

Upewnij się, że hello następujące wymagania wstępne są niespełnienia tooupdating wcześniejsze urządzenia StorSimple.  

* Upewnij się, że zarówno kontrolery urządzeń są uruchomione przed rozpoczęciem skanowania aktualizacji. Jeśli nie działa albo kontrolera, hello skanowanie zakończy się niepowodzeniem. tooverify kontrolerów hello będące w dobrej kondycji, przejdź zbyt**stan sprzętu** w obszarze hello **konserwacji** strony. Jeśli istnieją składniki który **wymaga uwagi**, skontaktuj się z Microsoft Support przed kontynuowaniem.
* Upewnij się, że stałe adresy IP dla kontrolera 0 i kontrolera 1 są rutowalne i mogą łączyć się toohello Internet, ponieważ są one używane do obsługi hello aktualizacje toohello urządzenia. Można użyć hello [polecenia cmdlet Test-Connection](https://technet.microsoft.com/library/hh849808.aspx) tooping znanego adresu poza hello sieci, takich jak outlook.com, tooverify, który hello kontroler ma toohello łączność poza siecią.
* Upewnij się, że porty 80 i 443 są dostępne na urządzeniu StorSimple dla komunikacji wychodzącej. Aby uzyskać więcej informacji, zobacz hello [wymagania dotyczące sieci dla urządzenia StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
* Jeśli wersja oprogramowania urządzenia hello jest starsza niż 6.3.9600.17312 (aktualizacja z października 2014 r.), należy wyłączyć hello porty dane 2 i dane 3, jeśli włączone, przed rozpoczęciem powitalne aktualizacji. Pozostawienie hello dane 2 i dane 3 porty włączone po zainstalowaniu aktualizacji hello może spowodować toogo kontrolera Twoje urządzenie w trybie odzyskiwania. Należy pamiętać, po wyłączeniu hello interfejsów sieciowych, wszystkie woluminy hello skojarzone zostanie przełączone do trybu offline i hello operacji We/Wy zostanie zakłócone na czas trwania hello hello aktualizacji.  

## <a name="whats-new-in-hello-february-release"></a>Nowości w wersji lutego hello
Ta aktualizacja zawiera poprawkę dotyczącą problemu resetowania fabryki hello, który wystąpił na urządzeniach, które ma został uaktualniony z toohello wersji hello GA wersji z października 2014 r. Aby uzyskać więcej informacji, zobacz [rozwiązać problemy w tej wersji](#issues-fixed-in-the-february-release).   

Ta aktualizacja nie zawiera nowych funkcji lub funkcji.  

## <a name="issues-fixed-in-hello-february-release"></a>Problemy rozwiązane w wersji lutego hello
Witaj poniższej tabeli opisano hello problem, który został rozwiązany w ramach tej aktualizacji.  

| Nie. | Funkcja | Problem | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- |
| 1 |Resetowanie do ustawień fabrycznych |Możesz spróbować tooperform resetowania urządzenia, która pierwotnie była GA hello wersji (wersja 6.3.9600.17215) do ustawień fabrycznych zainstalowany, ale został zaktualizowany toohello października wersji (wersja 6.3.9600.17312). Fabryka Hello zresetować kończy się niepowodzeniem i hello urządzenie stanie się niestabilny. |Tak |Nie |

## <a name="known-issues-in-hello-february-release"></a>Znane problemy w wersji lutego hello
Witaj w poniższej tabeli przedstawiono podsumowanie znanych problemów występujących w tej wersji.

| Nie. | Funkcja | Problem | Komentarz/obejście | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- | --- |
| 1 |Resetowanie do ustawień fabrycznych |W niektórych przypadkach po wykonaniu Resetowanie do ustawień fabrycznych hello urządzenia StorSimple może zostać zatrzymane i wyświetla ten komunikat: **toofactory resetowania jest w toku (faza 8)**. Dzieje się tak, jeśli naciśnij klawisze CTRL + C, gdy polecenie cmdlet hello jest w toku. |Naciskaj klawisze CTRL + C po zainicjowaniu resetowania do ustawień fabrycznych. Jeśli jesteś już w tym stanie, skontaktuj się z Microsoft Support, dalsze czynności. |Tak |Nie |
| 2 |Dysku kworum |W rzadkich przypadkach odłączeniu większość hello dysków w obudowie EBOD hello z 8600device są wynikiem dysku kworum, następnie puli magazynów hello będzie w trybie offline. Pozostanie on w trybie offline nawet wtedy, gdy będzie nawiązywane hello dysków. |Konieczne będzie tooreboot hello urządzenia. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support, dalsze czynności. |Tak |Nie |
| 3 |Błędy migawkę chmury |W rzadkich przypadkach migawka w chmurze może zakończyć się niepowodzeniem z powodu błędu hello **osiągnięto limit kopii zapasowej maksymalnie**. Dzieje się tak, jeśli przekracza 255 klony online na powitania jednym urządzeniu, z hello tego samego oryginalnego woluminu, który został usunięty. | |Tak |Tak |
| 4 |Identyfikator niepoprawne kontrolera |Po wykonaniu zastąpić kontrolera kontrolera 0 mogą wyglądać jak kontrolera 1. Podczas wymiany kontrolera po załadowaniu hello obraz z węzła równorzędnego hello, identyfikator kontrolera hello można wyświetlane początkowo jako identyfikator hello równorzędnej kontrolera. W rzadkich przypadkach to zachowanie może być widoczny po ponownym uruchomieniu systemu. |Nie jest wymagana żadna akcja użytkownika. Sytuacja ta zostanie rozwiązany samoczynnie po zakończeniu hello zastępczego kontrolera. |Tak |Nie |
| 5 |Wykresy monitorowania urządzeń |W hello usługi Menedżer StorSimple wykresy monitorowania urządzenia hello nie działają w przypadku podstawowych lub w konfiguracji serwera proxy hello hello urządzenia jest włączone uwierzytelnianie NTLM. |Zmodyfikuj konfigurację serwera proxy sieci web hello hello urządzenia zarejestrowane przy użyciu usługi Menedżer StorSimple, że uwierzytelnianie ustawiono tooNONE. toodo tego hello hello wykonywania programu Windows PowerShell polecenia cmdlet StorSimple Set-HcsWebProxy. |Tak |Tak |
| 6 |Konta magazynu |Przy użyciu konta magazynu hello magazynu usługi toodelete hello jest to nieobsługiwany scenariusz. Spowoduje to tooa sytuacji, w której nie można pobrać danych użytkownika. | |Tak |Tak |
| 7 |Urządzenia trybu failover |Wiele przechodzenia kontener woluminów z hello tego samego urządzenia docelowe toodifferent urządzenia źródłowego nie jest obsługiwane.    Tryb failover z urządzeń toomultiple jednego urządzenia martwy spowoduje, że hello kontenery woluminów na powitania najpierw przejścia w tryb failover urządzeń utraty własności danych. Po przełączeniu te kontenery woluminów są wyświetlane lub zachowywać się inaczej, podczas wyświetlania w hello klasycznego portalu Azure. | |Tak |Nie |
| 8 |Instalacja |Podczas StorSimple karty dla instalacji programu SharePoint należy tooprovide IP urządzenia, aby toofinish instalacji hello pomyślnie. | |Tak |Nie |
| 9 |Serwer proxy sieci Web |Jeśli ma konfigurację serwera proxy sieci web HTTPS jako hello określić protokół, będzie mieć wpływ na komunikacji usługi urządzeń i hello urządzenie przejdzie w trybie offline. Obsługa pakietów również zostanie wygenerowany w procesie hello, wykorzystywanie znaczące ilości zasobów na urządzeniu. |Upewnij się, że hello określony protokół adresu URL serwera proxy sieci web hello ma HTTP. Więcej informacji na temat zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](storsimple-configure-web-proxy.md). |Tak |Nie |
| 10 |Serwer proxy sieci Web |Jeśli możesz skonfigurować i włączyć serwer proxy sieci web na zarejestrowanym urządzeniu, będzie konieczne toorestart hello aktywnym kontrolerze na urządzeniu. | |Tak |Nie |
| 11 |Wysoka chmury opóźnienia i wysokie obciążenie We/Wy |Gdy urządzenie StorSimple napotka kombinacją chmury w bardzo duże opóźnienia (kolejność sekund) i wysokie obciążenie We/Wy, hello urządzenia woluminów przechodzi w stan obniżeniem i hello operacji We/Wy może zakończyć się niepowodzeniem z powodu błędu "urządzenie nie jest gotowe". |Będzie konieczne kontrolery urządzeń hello ponowny rozruch toomanually lub wykonaj toorecover pracy awaryjnej urządzenia z tej sytuacji. |Tak |Nie |

## <a name="physical-device-updates-in-hello-february-release"></a>Urządzenie fizyczne aktualizacji w wersji lutego hello
Tej aktualizacji poprawki hello fabryki zresetować problem, który wystąpił na urządzeniach, które ma został uaktualniony z toohello wersji hello GA wersji z października 2014 r. Nie zawiera żadnych innych aktualizacji toohello urządzenia StorSimple.  

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-february-release"></a>Magistrali Serial attached SCSI (SAS) kontrolera aktualizacje w wersji lutego hello
Ta wersja nie zawiera żadnych aktualizacji toohello magistrali serial attached SCSI (SAS) kontrolera lub oprogramowanie układowe hello. Aktualizacja sterownika Hello był hello października 2014 roku.  

## <a name="virtual-device-updates-in-hello-february-release"></a>Urządzenie wirtualne aktualizacji w wersji lutego hello
Ta wersja nie zawiera żadnych aktualizacji dla urządzenia wirtualnego hello. Zastosowanie tej aktualizacji nie spowoduje zmiany wersji oprogramowania hello urządzenia wirtualnego.

