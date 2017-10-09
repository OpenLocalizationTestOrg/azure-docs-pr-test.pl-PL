---
title: "aaaStorSimple 8000 zaktualizować 0,2 informacje o wersji | Dokumentacja firmy Microsoft"
description: "Opisuje hello nowe funkcje i poprawki, problemy otwarte i dostępne obejścia hello stycznia 2015 release Microsoft Azure StorSimple (aktualizacja 0,2)."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d9684ae3-b38f-4678-9d70-e5dbc6b03350
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: 1cee795df0b53d9b9276bc33074cf1a7aa188835
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-02-release-notes---january-2015"></a>Informacje o wersji 0,2 StorSimple 8000 z aktualizacją Update - stycznia 2015
## <a name="overview"></a>Omówienie
Witaj poniższych informacjach o wersji zidentyfikować hello krytyczne problemy otwarte dla hello stycznia 2015 r. programu Microsoft Azure StorSimple. Zawierają one również listę hello StorSimple oprogramowania i aktualizacje oprogramowania układowego zawarte w tej wersji. To drugie wydanie hello po wersji StorSimple 8000 serii wersji hello ogólnie dostępna w lipca 2014.

Ta aktualizacja nie powoduje zmiany wersji oprogramowania urządzenia fizycznego hello hello października Update. Wykonywana wersja toobe 6.3.9600.17312. Obraz powitania używana przez obraz urządzenia wirtualnego hello zmienił się w tej wersji. W związku z tym wszystkie nowe urządzenia wirtualnego hello utworzone po 2015-1-20 wyświetli wersji hello jako 6.3.9600.17361.  

Zapoznaj się z tematem hello następujące informacje zawarte w hello informacje o wersji dla hello stycznia 2015 update.

> [!IMPORTANT]
> * Ta aktualizacja nie jest dostępna za pośrednictwem usługi Windows Update i nie można zainstalować podobnie jak inne aktualizacje. Urządzenie nie otrzymają tej aktualizacji, nawet wtedy, gdy w przypadku zastosowania aktualizacji hello przy użyciu hello klasycznego portalu Azure. Ta aktualizacja ma zastosowanie tylko urządzenia toovirtual utworzone po 20 stycznia 2015 r. 
> * Witaj stycznia wersji StorSimple nie zawiera żadnych aktualizacji toohello urządzenia fizycznego StorSimple. Można stosować wszystkie dostępne aktualizacje toohello wirtualnego urządzenia Windows, łącznie z ostatnich zabezpieczeń poprawki, ale nie zobaczą zmiany w wersji dla urządzenia fizycznego StorSimple hello.
> 
> 

## <a name="whats-new-in-hello-january-release"></a>Nowości w wersji stycznia hello
Ta aktualizacja zawiera poprawkę związane z woluminów toohello przechodzi do trybu offline na powitania urządzenia wirtualnego. (Zobacz [rozwiązać problemy w tej wersji](#issues-fixed-in-the-january-release).)  

Aktualizacja Hello nie zawiera nowych funkcji lub funkcji.  

## <a name="issues-fixed-in-hello-january-release"></a>Problemy rozwiązane w wersji stycznia hello
Witaj poniższej tabeli opisano hello problem, który został rozwiązany w ramach tej aktualizacji.

| Nie. | Funkcja | Problem | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- |
| 1 |Woluminy przechodzi do trybu offline |Opóźnienia wysokiej chmury będą się powtarzać kilka minut, woluminy urządzenia wirtualnego StorSimple hello Przejdź w trybie offline na hostach hello. Ta poprawka zwiększa hello próg opóźnienia chmury, a tym samym minimalizując sytuacjach hello, które mogłyby spowodować hello toogo woluminy w tryb offline na hostach. |Nie |Tak |

## <a name="known-issues-in-hello-january-release"></a>Znane problemy w wersji stycznia hello
Witaj w poniższej tabeli przedstawiono podsumowanie znanych problemów występujących w tej wersji.

| Nie. | Funkcja | Problem | Komentarz/obejście | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- | --- |
| 1 |Resetowanie do ustawień fabrycznych |W niektórych przypadkach po wykonaniu Resetowanie do ustawień fabrycznych hello urządzenia StorSimple może zostać zatrzymane i wyświetla ten komunikat: **toofactory resetowania jest w toku (faza 8).** Dzieje się tak, jeśli naciśnij klawisze CTRL + C, gdy polecenie cmdlet hello jest w toku. |Naciskaj klawisze CTRL + C po zainicjowaniu resetowania do ustawień fabrycznych. Jeśli jesteś już w tym stanie, skontaktuj się z Microsoft Support, dalsze czynności. |Tak |Nie |
| 2 |Dysku kworum |W rzadkich przypadkach odłączeniu większość hello dysków w obudowie EBOD hello urządzenia 8600 są wynikiem dysku kworum, następnie puli magazynów hello będzie w trybie offline. Pozostanie on w trybie offline nawet wtedy, gdy będzie nawiązywane hello dysków. |Konieczne będzie tooreboot hello urządzenia. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support, dalsze czynności. |Tak |Nie |
| 3 |Błędy migawkę chmury |W rzadkich przypadkach migawka w chmurze może zakończyć się niepowodzeniem z powodu błędu hello **osiągnięto limit kopii zapasowej maksymalnie**. Dzieje się tak, jeśli przekracza 255 klony online na powitania jednym urządzeniu, z hello tego samego oryginalnego woluminu, który został usunięty. | |Tak |Tak |
| 4 |Identyfikator niepoprawne kontrolera |Po wykonaniu zastąpić kontrolera kontrolera 0 mogą wyglądać jak kontrolera 1. Podczas wymiany kontrolera po załadowaniu hello obraz z węzła równorzędnego hello, identyfikator kontrolera hello można wyświetlane początkowo jako identyfikator hello równorzędnej kontrolera.  W rzadkich przypadkach to zachowanie może być widoczny po ponownym uruchomieniu systemu. |Nie jest wymagana żadna akcja użytkownika. Sytuacja ta zostanie rozwiązany samoczynnie po zakończeniu hello zastępczego kontrolera. |Tak |Nie |
| 5 |Wykresy monitorowania urządzeń |W hello usługi Menedżer StorSimple wykresy monitorowania urządzenia hello nie działają w przypadku podstawowych lub w konfiguracji serwera proxy hello hello urządzenia jest włączone uwierzytelnianie NTLM. |Zmodyfikuj konfigurację serwera proxy sieci web hello hello urządzenia zarejestrowane przy użyciu usługi Menedżer StorSimple, że uwierzytelnianie ustawiono tooNONE. toodo tego hello hello wykonywania programu Windows PowerShell polecenia cmdlet StorSimple Set-HcsWebProxy. |Tak |Tak |
| 6 |Konta magazynu |Przy użyciu konta magazynu hello magazynu usługi toodelete hello jest to nieobsługiwany scenariusz. Spowoduje to tooa sytuacji, w której nie można pobrać danych użytkownika. | |Tak |Tak |
| 7 |Urządzenia trybu failover |Wiele przechodzenia kontener woluminów z hello tego samego urządzenia docelowe toodifferent urządzenia źródłowego nie jest obsługiwane. |Tryb failover z urządzeń toomultiple jednego urządzenia martwy spowoduje, że hello kontenery woluminów na powitania najpierw przejścia w tryb failover urządzeń utraty własności danych. Po przełączeniu te kontenery woluminów są wyświetlane lub zachowywać się inaczej, podczas wyświetlania w hello klasycznego portalu Azure. |Tak |Nie |
| 8 |Instalacja |Podczas StorSimple karty dla instalacji programu SharePoint należy tooprovide IP urządzenia, aby toofinish instalacji hello pomyślnie. | |Tak |Nie |
| 9 |Serwer proxy sieci Web |Jeśli ma konfigurację serwera proxy sieci web HTTPS jako hello określić protokół, będzie mieć wpływ na komunikacji usługi urządzeń i hello urządzenie przejdzie w trybie offline. Obsługa pakietów również zostanie wygenerowany w procesie hello, wykorzystywanie znaczące ilości zasobów na urządzeniu. |Upewnij się, że hello określony protokół adresu URL serwera proxy sieci web hello ma HTTP. Zobacz więcej informacji na temat zbyt[skonfigurować serwer proxy sieci web dla danego urządzenia](storsimple-configure-web-proxy.md). |Tak |Nie |
| 10 |Serwer proxy sieci Web |Jeśli możesz skonfigurować i włączyć serwer proxy sieci web na zarejestrowanym urządzeniu, będzie konieczne toorestart hello aktywnym kontrolerze na urządzeniu. | |Tak |Nie |
| 11 |Wysoka chmury opóźnienia i wysokie obciążenie We/Wy |Gdy urządzenie StorSimple napotka kombinacją chmury w bardzo duże opóźnienia (kolejność sekund) i wysokie obciążenie We/Wy, hello urządzenia woluminów przechodzi w stan obniżeniem i hello operacji We/Wy może zakończyć się niepowodzeniem z powodu błędu "urządzenie nie jest gotowe". |Będzie konieczne kontrolery urządzeń hello ponowny rozruch toomanually lub wykonaj toorecover pracy awaryjnej urządzenia z tej sytuacji. |Tak |Nie |

## <a name="physical-device-updates-in-hello-january-release"></a>Urządzenie fizyczne aktualizacji w wersji stycznia hello
Ta aktualizacja nie zawiera żadnych innych zmian toohello urządzenia StorSimple.

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-hello-january-release"></a>Magistrali Serial attached SCSI (SAS) kontrolera aktualizacje w wersji stycznia hello
Ta wersja nie zawiera żadnych aktualizacji toohello magistrali serial attached SCSI (SAS) kontrolera lub oprogramowanie układowe hello. Aktualizacja sterownika Hello był hello października 2014 roku. 

## <a name="virtual-device-updates-in-hello-january-release"></a>Urządzenie wirtualne aktualizacji w wersji stycznia hello
Ta wersja zawiera zaktualizowaną hello urządzenia wirtualnego. Wszystkie urządzenia wirtualnego hello utworzone po 20 stycznia 2015 wyświetli wersji oprogramowania hello jako 6.3.9600.17361.

