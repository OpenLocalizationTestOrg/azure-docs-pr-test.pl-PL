---
title: "aaaInstall aktualizacji 3 na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooinstall StorSimple 8000 serii aktualizacji 3 na urządzeniu z serii StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c6c4634d-4f3a-4bc4-b307-a22bf18664e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a156b8919639f1c7afb0fdef3d882d40d48f1c48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-3-on-your-storsimple-8000-series-device"></a>Zainstaluj na urządzeniu z serii StorSimple 8000 z aktualizacją Update 3

## <a name="overview"></a>Omówienie

W tym samouczku wyjaśniono, jak tooinstall aktualizacji 3 na urządzeniu StorSimple ze starszą wersją oprogramowania za pośrednictwem hello klasycznego portalu Azure i przy użyciu metody poprawki hello. Metoda poprawki Hello jest używana, gdy brama jest skonfigurowana w interfejsie sieciowym innym niż dane 0 hello urządzenia StorSimple i próbujesz tooupdate z wersji oprogramowania 1 przed aktualizacją.

Aktualizacja 3 obejmuje oprogramowanie urządzenia, LSI sterowników i oprogramowania układowego, Storport i aktualizuje Spaceport. Jeśli aktualizacja Update 2 lub starszej wersji, utworzy również być wymagane tooapply iSCSI, usługi WMI i w niektórych przypadkach dysku aktualizacje oprogramowania układowego. Witaj oprogramowania urządzenia, WMI iSCSI, LSI sterownika, Spaceport i Storport poprawki Brak aktualizacji i mogą być stosowane za pośrednictwem hello klasycznego portalu Azure. aktualizacje oprogramowania układowego dysku Hello są aktualizacje zakłócenie i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell hello hello urządzenia. 

> [!IMPORTANT]
> * Zestaw ręczne i automatyczne wstępne sprawdzanie gotowe toohello uprzedniej instalacji toodetermine hello urządzenia kondycji pod względem sprzętu stanu i łączność sieciową. Kontrole wstępne są wykonywane tylko wtedy, gdy należy zastosować aktualizacje hello z hello klasycznego portalu Azure.
> * Zaleca się instalowanie oprogramowania hello i aktualizacje sterowników za pomocą hello klasycznego portalu Azure. Interfejsu programu Windows PowerShell toohello hello urządzenia (tooinstall aktualizacje) należy postępować tylko, jeśli hello przed aktualizacją bramy sprawdzenie nie powiedzie się w portalu hello. W zależności od wersji hello, aktualizowanej z hello aktualizacji może potrwać tooinstall 2.5 1,5 godziny. aktualizacje trybu konserwacji Hello muszą być zainstalowane za pomocą interfejsu programu Windows PowerShell hello hello urządzenia. Aktualizacje trybu konserwacji są aktualizacje destrukcyjne, te spowoduje dół czasu dla danego urządzenia.
> * Uruchamianie hello opcjonalne StorSimple Snapshot Manager, upewnij się, uaktualniono Snapshot Manager wersji tooUpdate 2 wcześniejsze tooupdating hello urządzenia.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-3-via-hello-azure-classic-portal"></a>Instalowanie aktualizacji 3 za pomocą hello klasycznego portalu Azure
Wykonaj następujące kroki tooupdate hello urządzenia zbyt[Update 3](storsimple-update3-release-notes.md).

> [!NOTE]
> Stosowania Update 2 lub nowszym (w tym Update 2.1), Microsoft będzie możliwe toopull dodatkowe informacje diagnostyczne z hello urządzenia. W związku z tym gdy działu operacji identyfikuje urządzenia, które występują problemy, firma Microsoft są lepsze informacje wyposażone toocollect z hello urządzenia i diagnozowanie problemów. Akceptując Update 2 lub nowszej, musisz zezwolić nam tooprovide ta obsługa aktywne.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Sprawdź, czy urządzenie działa **StorSimple 8000 serii Update 3 (6.3.9600.17759)**. Witaj **ostatniej aktualizacji daty** również powinien być modyfikowany. 
   - Aktualizowania z poprzednich tooUpdate w wersji 2, pojawi się także o dostępnych aktualizacjach trybu konserwacji hello (ten komunikat może nadal toobe są wyświetlane się too24 godzin po zainstalowaniu hello aktualizacji).
     Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, które powoduje przestój urządzenia i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell hello urządzenia. W niektórych przypadkach po uruchomieniu aktualizacji 1.2, oprogramowania układowego dysku mogą być już aktualne, w tym przypadku nie trzeba tooinstall aktualizuje dowolny tryb konserwacji.
   - W przypadku aktualizacji z Update 2 lub nowszej, urządzenie powinno być teraz aktualne. Można pominąć hello następnego kroku.

Pobierz aktualizacje trybu konserwacji hello przy użyciu hello czynności opisane w [poprawki toodownload](#to-download-hotfixes) toosearch dla i Pobierz KB3121899, który instaluje aktualizacje oprogramowania układowego dysku (hello inne aktualizacje powinny być zainstalowane przez teraz). Wykonaj kroki hello na liście [zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello obsługi trybu aktualizacji. 

## <a name="install-update-3-as-a-hotfix"></a>Instalowanie aktualizacji 3 jako poprawki
Użyj tej procedury, jeśli nie hello bramy wyboru podczas próby aktualizacji hello tooinstall za pośrednictwem hello klasycznego portalu Azure. Witaj sprawdzenie nie powiedzie się, masz przypisane interfejs sieciowy 0-DATA tooa bramy i urządzeniu jest uruchomiona tooUpdate wcześniejszych wersji 1 oprogramowania.

Hello wersji oprogramowania, które można uaktualnić za pomocą metody poprawki hello są:

* Zaktualizuj 0,1, 0,2, 0,3
* Aktualizacja 1, 1.1 i 1.2
* Aktualizacja 2, 2.1, 2.2 

> [!IMPORTANT]
> * Jeśli urządzenie korzysta z wersji Release (GA), skontaktuj się z [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist z hello aktualizacji.
> 
> 

Metoda poprawki Hello polega na powitania następujące trzy kroki:

1. Pobierz hello poprawki z hello wykazu usługi Microsoft Update.
2. Zainstaluj i sprawdź regularne hello poprawki.
3. Zainstaluj i sprawdź poprawkę trybu konserwacji hello (tylko wtedy, gdy aktualizacje oprogramowania 2 przed aktualizacją).

#### <a name="download-updates-for-your-device"></a>Pobierz aktualizacje dla urządzenia
**Jeśli urządzenie działa Update 2.1 lub 2.2**, musisz pobrać i zainstalować następujące poprawek w określonej kolejności hello hello:

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji |
| --- | --- | --- | --- | --- |
| 1. |KB3186843 |Aktualizacja oprogramowania &#42; |Regularne <br></br>Bezproblemowa |~ 45 minut. |
| 2. |KB3186859 |LSI sterowników i oprogramowania układowego |Regularne <br></br>Bezproblemowa |~ 20 minut. |
| 3. |KB3121261 |Poprawka Storport i Spaceport </br> Windows Server 2012 R2 |Regularne <br></br>Bezproblemowa |~ 20 minut. |

&#42;  *Należy pamiętać, że hello aktualizacji oprogramowania składa się z dwóch plików binarnych: Aktualizacja urządzenia poprzedzone znakiem `all-hcsmdssoftwareupdate` hello konfiguracji (ci) i agent usług Mds poprzedzone znakiem `all-cismdsagentupdatebundle`. aktualizacji oprogramowania hello urządzenia musi zostać zainstalowany przed hello konfiguracji (ci) i usług Mds Agent. Należy również uruchomić ponownie hello na aktywnym kontrolerze za pośrednictwem hello `Restart-HcsController` polecenia cmdlet po zastosowaniu hello konfiguracji (ci) i aktualizacja agenta usług Mds (i przed zastosowaniem hello pozostałych aktualizacji).* 

**Jeśli urządzenie działa Update 0.1, 0.2, 0.3, 1.0, 1.1, 1.2 lub 2.0**, należy pobrać i zainstalować hello następujące poprawki w przypadku dodawania toohello oprogramowania LSI sterowników i oprogramowania układowego aktualizuje (hello podanymi w powyższej tabeli), w określonej kolejności hello:

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji |
| --- | --- | --- | --- | --- |
| 4. |KB3146621 |Pakiet iSCSI |Regularne <br></br>Bezproblemowa |~ 20 minut. |
| 5. |KB3103616 |Pakiet usługi WMI |Regularne <br></br>Bezproblemowa |~ 12 minut. |

<br></br>

**Jeśli urządzenie korzysta z wersji 0,2, 0,3, 1.0, 1.1 i 1.2**, może być również konieczne tooinstall aktualizacje oprogramowania układowego dysku na wszystkich aktualizacji hello pokazano hello poprzednich tabel. Możesz sprawdzić, czy należy hello aktualizacje oprogramowania układowego dysku, uruchamiając hello `Get-HcsFirmwareVersion` polecenia cmdlet. Jeśli używasz tych wersji oprogramowania układowego: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, a następnie nie trzeba tooinstall te aktualizacje.

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji |
| --- | --- | --- | --- | --- |
| 6. |KB3121899 |Oprogramowanie układowe dysku |Konserwacji <br></br>Problem |~ 30 minut. |

<br></br>

> [!IMPORTANT]
> * Ta procedura toobe musi wykonać tylko raz tooapply Update 3. Możesz użyć hello Azure classic portal tooapply kolejnych aktualizacji.
> * Aktualizowania z 2.2 aktualizacji, godzinę instalacji całkowita hello jest Zamknij too1.1 godzin.
> * Przed użyciem tej procedury tooapply hello aktualizacji, upewnij się, że zarówno kontrolery urządzeń hello są w trybie online i wszystkie składniki sprzętowe hello są w dobrej kondycji.
> 
> 

Wykonaj następujące kroki toodownload hello i zainstaluj hello poprawki.

[!INCLUDE [storsimple-install-update3-hotfix](../../includes/storsimple-install-update3-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [wersji Update 3](storsimple-update3-release-notes.md).

