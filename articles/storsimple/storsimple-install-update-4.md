---
title: "aaaInstall 4 aktualizacji na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooinstall StorSimple 8000 serii aktualizacji 4 na urządzeniu z serii StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/30/2017
ms.author: alkohli
ms.openlocfilehash: 62c0ae94afdbb1027d3075962afa04d49fd1f60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-4-on-your-storsimple-device"></a>Instalowanie aktualizacji 4 na urządzeniu StorSimple

## <a name="overview"></a>Omówienie

W tym samouczku wyjaśniono, jak tooinstall 4 aktualizacji na urządzeniu StorSimple ze starszą wersją oprogramowania za pośrednictwem hello klasycznego portalu Azure i przy użyciu metody poprawki hello. Metoda poprawki Hello jest używana, gdy brama jest skonfigurowana w interfejsie sieciowym innym niż dane 0 hello urządzenia StorSimple i próbujesz tooupdate z wersji oprogramowania 1 przed aktualizacją.

Aktualizacja 4 zawiera oprogramowania urządzenia, oprogramowania układowego należy LSI sterowników i oprogramowania układowego Storport i Spaceport, systemu operacyjnego aktualizacje zabezpieczeń i inne aktualizacje systemu operacyjnego hosta.  oprogramowanie urządzenia Hello, oprogramowania układowego należy Spaceport, Storport i inne aktualizacje systemu operacyjnego są Brak aktualizacji. za pomocą hello klasycznego portalu Azure lub za pomocą metody poprawki hello można zastosować Hello Brak lub regularne aktualizacje. aktualizacje oprogramowania układowego dysku Hello są aktualizacje zakłócenie i mogą być stosowane tylko przy użyciu metody poprawki hello przy użyciu interfejsu programu Windows PowerShell hello hello urządzenia. 

> [!IMPORTANT]
> * Zestaw ręczne i automatyczne wstępne sprawdzanie gotowe toohello uprzedniej instalacji toodetermine hello urządzenia kondycji pod względem sprzętu stanu i łączność sieciową. Kontrole wstępne są wykonywane tylko wtedy, gdy należy zastosować aktualizacje hello z hello klasycznego portalu Azure.
> * Zaleca się zainstalowanie oprogramowania hello i innych regularne aktualizacje za pomocą hello klasycznego portalu Azure. Interfejsu programu Windows PowerShell toohello hello urządzenia (tooinstall aktualizacje) należy postępować tylko, jeśli hello przed aktualizacją bramy sprawdzenie nie powiedzie się w portalu hello. W zależności od wersji hello aktualizujesz z hello aktualizacji może potrwać 4 godziny (lub nowszego) tooinstall. należy także zainstalować aktualizacje trybu konserwacji Hello za pośrednictwem interfejsu programu Windows PowerShell hello hello urządzenia. Aktualizacje trybu konserwacji są aktualizacje destrukcyjne, te spowoduje dół czasu dla danego urządzenia.
> * Uruchamianie hello opcjonalne StorSimple Snapshot Manager, upewnij się, uaktualniono Snapshot Manager wersji tooUpdate 4 wcześniejsze tooupdating hello urządzenia.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-4-via-hello-azure-classic-portal"></a>Instalowanie aktualizacji 4 za pośrednictwem hello klasycznego portalu Azure
Wykonaj następujące kroki tooupdate hello urządzenia zbyt[Update 4](storsimple-update4-release-notes.md).

> [!NOTE]
> Stosowania Update 2 lub nowszym (w tym Update 2.1), Microsoft będzie możliwe toopull dodatkowe informacje diagnostyczne z hello urządzenia. W związku z tym gdy działu operacji identyfikuje urządzenia, które występują problemy, firma Microsoft są lepsze informacje wyposażone toocollect z hello urządzenia i diagnozowanie problemów. Akceptując Update 2 lub nowszej, musisz zezwolić nam tooprovide ta obsługa aktywne. 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Sprawdź, czy urządzenie działa **StorSimple 8000 serii aktualizacji w wersji 4 (6.3.9600.17820)**. Witaj **ostatniej aktualizacji daty** również powinien być modyfikowany. 

* Teraz zobaczysz, że są dostępne aktualizacje trybu konserwacji hello (ten komunikat może nadal toobe są wyświetlane się too24 godzin po zainstalowaniu hello aktualizacji). Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, które powoduje przestój urządzenia i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell hello urządzenia.
 
* Pobierz aktualizacje trybu konserwacji hello przy użyciu hello czynności opisane w [poprawki toodownload](#to-download-hotfixes) toosearch dla i Pobierz KB4011837, który instaluje aktualizacje oprogramowania układowego dysku (hello inne aktualizacje powinny być zainstalowane przez teraz). Wykonaj kroki hello na liście [zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello obsługi trybu aktualizacji. 

## <a name="install-update-4-as-a-hotfix"></a>Instalowanie aktualizacji 4 jako poprawki
Witaj zalecana metoda tooinstall, aktualizacja 4 jest za pośrednictwem hello klasycznego portalu Azure.

Użyj tej procedury, jeśli nie hello bramy wyboru podczas próby aktualizacji hello tooinstall za pośrednictwem hello klasycznego portalu Azure. Witaj sprawdzenie nie powiedzie się, masz przypisane interfejs sieciowy 0-DATA tooa bramy i urządzeniu jest uruchomiona tooUpdate wcześniejszych wersji 1 oprogramowania.

Hello wersji oprogramowania, które można uaktualnić za pomocą metody poprawki hello są:

* Zaktualizuj 0,1, 0,2, 0,3
* Aktualizacja 1, 1.1 i 1.2
* Aktualizacja 2, 2.1, 2.2
* Aktualizacja 3 w wersji 3.1 


Metoda poprawki Hello polega na powitania następujące trzy kroki:

1. Pobierz hello poprawki z hello wykazu usługi Microsoft Update.
2. Zainstaluj i sprawdź regularne hello poprawki.
3. Zainstaluj i sprawdź poprawkę trybu konserwacji hello.

#### <a name="download-updates-for-your-device"></a>Pobierz aktualizacje dla urządzenia

Należy pobrać i zainstalować następujące hello poprawek w hello określonej kolejności i hello sugerowane folderów:

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji |Zainstaluj w folderze|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4011839 <br> (2 plików) |Aktualizacja oprogramowania urządzenia <br> Aktualizacja konfiguracji (ci) / MDS agenta |Regularne <br></br>Bezproblemowa |~ 25 minut. |FirstOrderUpdate <br> _Zainstaluj aktualizację oprogramowania urządzenia przed aktualizacją agenta konfiguracji (ci) / MDS_|
| 2A. |KB4011841 <br> KB4011842 |Sterownik LSI i aktualizacje oprogramowania układowego <br> Aktualizacja oprogramowania układowego należy (wersja 3.38) |Regularne <br></br>Bezproblemowa |~ 3 godziny <br> (dotyczy również 2A. + 2B. + 2 C.)|SecondOrderUpdate|
| 2B. |KB3139398, KB3108381 <br> KB3205400, KB3142030 <br> KB3197873, KB3192392  <br> KB3153704, KB3174644 <br> KB3139914  |Pakiet aktualizacji zabezpieczeń systemu operacyjnego |Regularne <br></br>Bezproblemowa |- |SecondOrderUpdate|
| 2C. |KB3210083, KB3103616 <br> KB3146621, KB3121261 <br> KB3123538 |Pakiet aktualizacji systemu operacyjnego |Regularne <br></br>Bezproblemowa |- |SecondOrderUpdate|

Możesz również przeprowadzić aktualizacje oprogramowania układowego dysku tooinstall na wszystkie aktualizacje hello pokazano hello poprzednich tabel. Możesz sprawdzić, czy należy hello aktualizacje oprogramowania układowego dysku, uruchamiając hello `Get-HcsFirmwareVersion` polecenia cmdlet. Jeśli używasz tych wersji oprogramowania układowego: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N002`, `0106`, a następnie nie trzeba tooinstall te aktualizacje.

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji | Zainstaluj w folderze|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4011837 |Oprogramowanie układowe dysku |Konserwacji <br></br>Problem |~ 30 minut. | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Ta procedura toobe potrzeb tylko raz wykonać tooapply Update 4. Możesz użyć hello Azure classic portal tooapply kolejnych aktualizacji.
> * Jeśli aktualizacja Update 3 lub 3.1, hello instalacji całkowity czas jest too4 Zamknij godzin.
> * Przed użyciem tej procedury tooapply hello aktualizacji, upewnij się, że zarówno kontrolery urządzeń hello są w trybie online i wszystkie składniki sprzętowe hello są w dobrej kondycji.

Wykonaj następujące kroki toodownload hello i zainstaluj hello poprawki.

[!INCLUDE [storsimple-install-update4-hotfix](../../includes/storsimple-install-update4-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [wersji aktualizacji 4](storsimple-update4-release-notes.md).

