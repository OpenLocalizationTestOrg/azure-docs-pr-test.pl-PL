---
title: "aaaInstall 2.2 aktualizacji na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooinstall StorSimple 8000 serii aktualizacji w wersji 2.2 na urządzeniu z serii StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 047c7a4b-73d0-45ea-8d51-c54d71871392
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2016
ms.author: alkohli
ms.openlocfilehash: cedb83ce42bc6bb81a4e43345da3f25b71036d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-22-on-your-storsimple-device"></a>Zainstaluj aktualizację 2.2 na urządzeniu StorSimple
## <a name="overview"></a>Omówienie
W tym samouczku wyjaśniono, jak tooinstall 2.2 aktualizacji na urządzeniu StorSimple ze starszą wersją oprogramowania za pośrednictwem hello klasycznego portalu Azure i przy użyciu metody poprawki hello. Metoda poprawki Hello jest używana, gdy brama jest skonfigurowana w interfejsie sieciowym innym niż dane 0 hello urządzenia StorSimple i próbujesz tooupdate z wersji oprogramowania 1 przed aktualizacją.

2.2 aktualizacja urządzenia, usługi WMI, aktualizacji oprogramowania i iSCSI. Jeśli aktualizacja z wersji 2.1, tylko aktualizacji oprogramowania urządzenia hello należy toobe zastosowane. Jeśli aktualizacja z wersji 2 przed aktualizacją, będzie również sterowników wymaganych tooapply LSI, Spaceport Storport i aktualizacje oprogramowania układowego dysku. Witaj oprogramowania urządzenia, WMI iSCSI, LSI sterownika, Spaceport i Storport poprawki Brak aktualizacji i mogą być stosowane za pośrednictwem hello klasycznego portalu Azure. aktualizacje oprogramowania układowego dysku Hello są aktualizacje zakłócenie i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell hello hello urządzenia. 

> [!IMPORTANT]
> * Zestaw ręczne i automatyczne wstępne sprawdzanie gotowe toohello uprzedniej instalacji toodetermine hello urządzenia kondycji pod względem sprzętu stanu i łączność sieciową. Kontrole wstępne są wykonywane tylko wtedy, gdy należy zastosować aktualizacje hello z hello klasycznego portalu Azure.
> * Zaleca się instalowanie oprogramowania hello i aktualizacje sterowników za pomocą hello klasycznego portalu Azure. Interfejsu programu Windows PowerShell toohello hello urządzenia (tooinstall aktualizacje) należy postępować tylko, jeśli hello przed aktualizacją bramy sprawdzenie nie powiedzie się w portalu hello. W zależności od wersji hello, aktualizowanej z hello aktualizacji może potrwać tooinstall 2.5 1,5 godziny. aktualizacje trybu konserwacji Hello muszą być zainstalowane za pomocą interfejsu programu Windows PowerShell hello hello urządzenia. Aktualizacje trybu konserwacji są aktualizacje destrukcyjne, te spowoduje dół czasu dla danego urządzenia.
> * Uruchamianie hello opcjonalne StorSimple Snapshot Manager, upewnij się, uaktualniono Snapshot Manager wersji tooUpdate 2.2 wcześniejsze tooupdating hello urządzenia.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-22-via-hello-azure-classic-portal"></a>Zainstaluj aktualizację 2.2 za pośrednictwem hello klasycznego portalu Azure
Wykonaj następujące kroki tooupdate hello urządzenia zbyt[2.2 aktualizacji](storsimple-update21-release-notes.md).

> [!NOTE]
> Stosowania Update 2 lub nowszym (w tym Update 2.1), Microsoft będzie możliwe toopull dodatkowe informacje diagnostyczne z hello urządzenia. W związku z tym gdy działu operacji identyfikuje urządzenia, które występują problemy, firma Microsoft są lepsze informacje wyposażone toocollect z hello urządzenia i diagnozowanie problemów. Akceptując Update 2 lub nowszej, musisz zezwolić nam tooprovide ta obsługa aktywne.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Sprawdź, czy urządzenie działa **StorSimple 8000 serii aktualizacji 2.2 (6.3.9600.17708)**. Witaj **ostatniej aktualizacji daty** również powinien być modyfikowany. 
   
   Aktualizowania z poprzednich tooUpdate w wersji 2, pojawi się także o dostępnych aktualizacjach trybu konserwacji hello (ten komunikat może nadal toobe są wyświetlane się too24 godzin po zainstalowaniu hello aktualizacji).
   
   Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, które powoduje przestój urządzenia i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell hello urządzenia. W niektórych przypadkach po uruchomieniu aktualizacji 1.2, oprogramowania układowego dysku mogą być już aktualne, w tym przypadku nie trzeba tooinstall aktualizuje dowolny tryb konserwacji.
   
   Jeśli są aktualizowane z Update 2, urządzenie powinno być teraz aktualne. Można pominąć hello pozostałe kroki.
2. Pobierz aktualizacje trybu konserwacji hello przy użyciu hello czynności opisane w [poprawki toodownload](#to-download-hotfixes) toosearch dla i Pobierz KB3121899, który instaluje aktualizacje oprogramowania układowego dysku (hello inne aktualizacje powinny być zainstalowane przez teraz).
3. Wykonaj kroki hello na liście [zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello obsługi trybu aktualizacji. 

## <a name="install-update-22-as-a-hotfix"></a>Instalowanie aktualizacji 2.2 jako poprawki
Użyj tej procedury, jeśli nie hello bramy wyboru podczas próby aktualizacji hello tooinstall za pośrednictwem hello klasycznego portalu Azure. Witaj sprawdzenie nie powiedzie się, masz przypisane interfejs sieciowy 0-DATA tooa bramy i urządzeniu jest uruchomiona tooUpdate wcześniejszych wersji 1 oprogramowania.

Hello wersji oprogramowania, które można uaktualnić za pomocą metody poprawki hello są:

* Zaktualizuj 0,1, 0,2, 0,3
* Aktualizacja 1, 1.1 i 1.2
* Aktualizacja 2, 2.1 

> [!IMPORTANT]
> * Jeśli urządzenie korzysta z wersji Release (GA), skontaktuj się z [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist z hello aktualizacji.
> 
> 

Metoda poprawki Hello polega na powitania następujące trzy kroki:

* Pobierz hello poprawki z hello wykazu usługi Microsoft Update.
* Zainstaluj i sprawdź regularne hello poprawki.
* Zainstaluj i sprawdź poprawkę trybu konserwacji hello (tylko wtedy, gdy aktualizacje oprogramowania 2 przed aktualizacją).

#### <a name="download-updates-for-a-device-running-update-21-software"></a>Pobierz aktualizacje na urządzeniu z systemem 2.1 aktualizacji oprogramowania
**Jeśli urządzenie korzysta z aktualizacji 2.1**, należy pobrać tylko hello urządzenia oprogramowania aktualizacji KB3179904. Zainstaluj tylko hello pliku binarnego poprzedzone znakiem "all-hcsmdssoftwareudpate". Nie należy instalować hello konfiguracji (ci) i aktualizacja agenta MDS hello poprzedzone znakiem `all-cismdsagentupdatebundle`. Błąd toodo tak spowoduje błąd. Jest to Brak aktualizacji, We/Wy nie zostanie zakłócone i hello urządzenia nie będą miały żadnych przestojów.

#### <a name="download-updates-for-a-device-running-update-2-software"></a>Pobierz aktualizacje dla urządzenia z oprogramowaniem Update 2
**Jeśli urządzenie korzysta z Update 2**, musisz pobrać i zainstalować następujące poprawek w określonej kolejności hello hello:

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji |
| --- | --- | --- | --- | --- |
| 1. |KB3179904 |Aktualizacja oprogramowania &#42; |Regularne <br></br>Bezproblemowa |~ 45 minut. |
| 2. |KB3146621 |Pakiet iSCSI |Regularne <br></br>Bezproblemowa |~ 20 minut. |
| 3. |KB3103616 |Pakiet usługi WMI |Regularne <br></br>Bezproblemowa |~ 12 minut. |

 &#42;  *Należy zwrócić uwagę, aktualizacji oprogramowania składa się z dwóch plików binarnych: Aktualizacja urządzenia poprzedzone znakiem `all-hcsmdssoftwareupdate` hello konfiguracji (ci) i agent usług Mds poprzedzone znakiem `all-cismdsagentupdatebundle`. aktualizacji oprogramowania hello urządzenia musi zostać zainstalowany przed hello konfiguracji (ci) i usług Mds agenta. Należy również uruchomić ponownie hello na aktywnym kontrolerze za pośrednictwem hello `Restart-HcsController` polecenia cmdlet po zastosowaniu hello konfiguracji (ci) i aktualizacja agenta usług MDS (i przed zastosowaniem hello pozostałych aktualizacji).* 

#### <a name="download-updates-for-a-device-running-pre-update-2-software"></a>Pobierz aktualizacje na urządzeniu z systemem przed aktualizacją oprogramowania 2
**Jeśli urządzenie korzysta z wersji 0,2, 0,3 1.0 i 1.1**, należy pobrać i instalacji hello LSI sterowników i oprogramowania układowego aktualizacji dodatkowo toohello, iSCSI, aktualizacji oprogramowania i usługi WMI. Ta aktualizacja jest już zainstalowany, jeśli używasz zaktualizować 1.2 lub 2. 

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji |
| --- | --- | --- | --- | --- |
| 4. |KB3121900 |LSI sterowników i oprogramowania układowego |Regularne <br></br>Bezproblemowa |~ 20 minut. |

<br></br>
**Jeśli urządzenie korzysta z wersji 0,2, 0,3, 1.0, 1.1 i 1.2**, musisz pobrać i zainstalować hello Spaceport i popraw Storport hello. Te są już zainstalowane, jeśli używasz Update 2.

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji |
| --- | --- | --- | --- | --- |
| 5. |KB3090322 |Poprawka spaceport </br> Windows Server 2012 R2 |Regularne <br></br>Bezproblemowa |~ 20 minut. |
| 6. |KB3080728 |Poprawka Storport </br> Windows Server 2012 R2 |Regularne <br></br>Bezproblemowa |~ 20 minut. |

<br></br>
Możesz również przeprowadzić aktualizacje oprogramowania układowego tooinstall dysku. Możesz sprawdzić, czy należy hello aktualizacje oprogramowania układowego dysku, uruchamiając hello `Get-HcsFirmwareVersion` polecenia cmdlet. Jeśli używasz tych wersji oprogramowania układowego: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, a następnie nie trzeba tooinstall te aktualizacje.

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji |
| --- | --- | --- | --- | --- |
| 7. |KB3121899 |Oprogramowanie układowe dysku |Konserwacji <br></br>Problem |~ 30 minut. |

<br></br>

> [!IMPORTANT]
> * Ta procedura toobe musi wykonać tylko raz tooapply 2.2 aktualizacji. Możesz użyć hello Azure classic portal tooapply kolejnych aktualizacji.
> * Jeśli aktualizacja Update 2, hello instalacji całkowity czas jest godziny too1.5 Zamknij.
> * Przed użyciem tej procedury tooapply hello aktualizacji, upewnij się, że zarówno kontrolery urządzeń hello są w trybie online i wszystkie składniki sprzętowe hello są w dobrej kondycji.
> 
> 

Wykonaj następujące kroki toodownload hello i zainstaluj hello poprawki.

[!INCLUDE [storsimple-install-update21-hotfix](../../includes/storsimple-install-update21-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [wersji Update 2.1](storsimple-update21-release-notes.md).

