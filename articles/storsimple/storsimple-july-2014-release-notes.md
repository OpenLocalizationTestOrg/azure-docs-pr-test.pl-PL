---
title: informacje o wersji aaaStorSimple 8000 wersji wersji | Dokumentacja firmy Microsoft
description: "Opisuje hello nowe funkcje, problemy otwarte i dostępne obejścia hello lipca 2014 Microsoft Azure StorSimple wersji."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 12f1796e-37c3-42b4-b997-a84fc1950c20
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 74863a3e2811dc7be5e6f482a5be4bbc37e3cd71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-release-version-release-notes---july-2014"></a>Informacje o wersji Wersja Release serii StorSimple 8000 — lipiec 2014
## <a name="overview"></a>Omówienie
informacje o wersji Hello wykonaj zidentyfikować hello krytyczne problemy otwarte dla hello z serii StorSimple 8000 wersji ogólnodostępnej (GA) lipca 2014 Microsoft Azure StorSimple. Ta wersja odpowiada wersji toosoftware 6.3.9600.17215.  

Jeżeli nie określono inaczej, te informacje o wersji zastosować modele tooall hello urządzenia StorSimple. Hello informacje o wersji są stale aktualizowane; wykrywane krytyczne problemy wymagające obejścia zostaną dodane. Przed wdrożeniem rozwiązania Microsoft Azure StorSimple, należy wziąć pod uwagę hello następujących informacji.  

## <a name="known-issues-in-this-release"></a>Znane problemy w tej wersji
Witaj w poniższej tabeli przedstawiono podsumowanie znanych problemów występujących w tej wersji.  

| Nie. | Funkcja | Problem | Komentarz/obejście | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- | --- |
| 1 |Resetowanie do ustawień fabrycznych |W niektórych przypadkach po wykonaniu Resetowanie do ustawień fabrycznych hello urządzenia StorSimple może zostać zatrzymane i wyświetla ten komunikat: **toofactory resetowania jest w toku (faza 8)**. Dzieje się tak, jeśli naciśnij klawisze CTRL + C, gdy polecenie cmdlet hello jest w toku. |Naciskaj klawisze CTRL + C po zainicjowaniu resetowania do ustawień fabrycznych. Jeśli jesteś już w tym stanie, skontaktuj się z Microsoft Support, dalsze czynności. |Tak |Nie |
| 2 |Dysku kworum |W rzadkich przypadkach odłączeniu większość hello dysków w obudowie EBOD hello urządzenia 8600 są wynikiem dysku kworum, następnie puli magazynów hello będzie w trybie offline. Pozostanie on w trybie offline nawet wtedy, gdy będzie nawiązywane hello dysków. |Konieczne będzie tooreboot hello urządzenia. Jeśli hello problem będzie się powtarzać, skontaktuj się z Microsoft Support, dalsze czynności. |Tak |Nie |
| 3 |Błędy migawkę chmury |W rzadkich przypadkach migawka w chmurze może zakończyć się niepowodzeniem z powodu błędu hello **osiągnięto limit kopii zapasowej maksymalnie**. Dzieje się tak, jeśli przekracza 255 klony online na powitania jednym urządzeniu, z hello tego samego oryginalnego woluminu, który został usunięty. | |Tak |Tak |
| 4 |Identyfikator niepoprawne kontrolera |Po wykonaniu zastąpić kontrolera kontrolera 0 mogą wyglądać jak kontrolera 1. Podczas wymiany kontrolera po załadowaniu hello obraz z węzła równorzędnego hello, identyfikator kontrolera hello można wyświetlane początkowo jako identyfikator hello równorzędnej kontrolera. W rzadkich przypadkach to zachowanie może być widoczny po ponownym uruchomieniu systemu. |Nie jest wymagana żadna akcja użytkownika. Sytuacja ta zostanie rozwiązany samoczynnie po zakończeniu hello zastępczego kontrolera. |Tak |Nie |
| 5 |Wykresy monitorowania urządzeń |W hello usługi Menedżer StorSimple wykresy monitorowania urządzenia hello nie działają w przypadku podstawowych lub w konfiguracji serwera proxy hello hello urządzenia jest włączone uwierzytelnianie NTLM. |Zmodyfikuj konfigurację serwera proxy sieci web hello hello urządzenia zarejestrowane przy użyciu usługi Menedżer StorSimple, że uwierzytelnianie ustawiono tooNONE. toodo tego hello hello wykonywania programu Windows PowerShell polecenia cmdlet StorSimple Set-HcsWebProxy. |Tak |Tak |
| 6 |Konta magazynu |Przy użyciu konta magazynu hello magazynu usługi toodelete hello jest to nieobsługiwany scenariusz. Spowoduje to tooa sytuacji, w której nie można pobrać danych użytkownika. | |Tak |Tak |
| 7 |Powrót po awarii |Powrót po awarii w ciągu 24 godzin odzyskiwania awaryjnego (DR) nie jest obsługiwana. | |Tak |Nie |
| 8 |Urządzenia trybu failover |Wiele przechodzenia kontener woluminów z hello tego samego urządzenia docelowe toodifferent urządzenia źródłowego nie jest obsługiwane. Tryb failover z urządzeń toomultiple jednego urządzenia martwy spowoduje, że hello kontenery woluminów na powitania najpierw przejścia w tryb failover urządzeń utraty własności danych. Po przełączeniu te kontenery woluminów są wyświetlane lub zachowywać się inaczej, podczas wyświetlania w hello klasycznego portalu Azure. | |Tak |Nie |
| 9 |Instalacja |Podczas StorSimple karty dla instalacji programu SharePoint należy tooprovide IP urządzenia dla toofinish instalacji hello pomyślnie. | |Tak |Nie |
| 10 |Interfejsy sieciowe |Interfejsy sieciowe dane 2 i dane 3 zostały zamienione hello oprogramowania. |Skontaktuj się z Microsoft Support, jeśli potrzebujesz tooconfigure tych interfejsów. |Tak |Nie |

