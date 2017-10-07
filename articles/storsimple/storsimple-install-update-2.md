---
title: "aaaInstall Update 2 na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooinstall StorSimple 8000 serii Update 2 na urządzeniu z serii StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: 33a0bea4358c944644563192f686af332d2ad7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>Instalowanie aktualizacji 2 na urządzeniu StorSimple
## <a name="overview"></a>Omówienie
W tym samouczku wyjaśniono, jak tooinstall Update 2 na urządzeniu StorSimple uruchomiona starsza wersja oprogramowania za pośrednictwem hello klasycznego portalu Azure. Samouczek Hello obejmuje również kroki hello wymagana hello aktualizacji, gdy brama jest skonfigurowana w interfejsie sieciowym innym niż dane 0 hello urządzenia StorSimple i próbujesz tooupdate z wersji oprogramowania 1 przed aktualizacją.

Aktualizacja 2 obejmuje urządzenia aktualizacji oprogramowania, aktualizacje sterowników LSI i aktualizacje oprogramowania układowego dysku. LSI aktualizacji i oprogramowania urządzenia Hello Brak aktualizacji i mogą być stosowane za pośrednictwem hello klasycznego portalu Azure. aktualizacje oprogramowania układowego dysku Hello są aktualizacje zakłócenie i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell hello hello urządzenia.

> [!IMPORTANT]
> * Nie widzisz Update 2 natychmiast, ponieważ jak etapowego wdrażania hello aktualizacji. Skanowanie w poszukiwaniu aktualizacji ponownie za kilka dni jako tej aktualizacji zostanie wkrótce udostępnione.
> * Zestaw ręczne i automatyczne wstępne sprawdzanie gotowe toohello uprzedniej instalacji toodetermine hello urządzenia kondycji pod względem sprzętu stanu i łączność sieciową. Kontrole wstępne są wykonywane tylko wtedy, gdy należy zastosować aktualizacje hello z hello klasycznego portalu Azure.
> * Zaleca się instalowanie oprogramowania hello i aktualizacje sterowników za pomocą hello klasycznego portalu Azure. Interfejsu programu Windows PowerShell toohello hello urządzenia (tooinstall aktualizacje) należy postępować tylko, jeśli hello przed aktualizacją bramy sprawdzenie nie powiedzie się w portalu hello. Witaj aktualizacji może potrwać tooinstall 4-7 godzin (w tym aktualizacje systemu Windows hello). aktualizacje trybu konserwacji Hello muszą być zainstalowane za pomocą interfejsu programu Windows PowerShell hello hello urządzenia. Aktualizacje trybu konserwacji są aktualizacje destrukcyjne, te spowoduje dół czasu dla danego urządzenia.
> * Uruchamianie hello opcjonalne StorSimple Snapshot Manager, upewnij się, uaktualniono Snapshot Manager wersji tooUpdate 2 wcześniejsze tooupdating hello urządzenia.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-hello-azure-classic-portal"></a>Instalowanie aktualizacji 2 za pośrednictwem hello klasycznego portalu Azure
Wykonaj następujące kroki tooupdate hello urządzenia zbyt[Update 2](storsimple-update2-release-notes.md).

> [!NOTE]
> Aktualizacja 2 umożliwia toopull Microsoft dodatkowe informacje diagnostyczne z hello urządzenia. W związku z tym gdy działu operacji identyfikuje urządzenia, które występują problemy, firma Microsoft są lepsze informacje wyposażone toocollect z hello urządzenia i diagnozowanie problemów. Akceptowanie Update 2, umożliwia nam tooprovide ta obsługa aktywne.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Sprawdź, czy urządzenie działa **StorSimple 8000 serii Update 2 (6.3.9600.17673)**. Witaj **ostatniej aktualizacji daty** również powinien być modyfikowany. Widoczny będzie również, że są dostępne aktualizacje tryb konserwacji (ten komunikat może nadal toobe są wyświetlane się too24 godzin po zainstalowaniu hello aktualizacji).
   
   Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, które powoduje przestój urządzenia i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell hello urządzenia. W niektórych przypadkach po uruchomieniu aktualizacji 1.2, oprogramowania układowego dysku mogą być już aktualne, w tym przypadku nie trzeba tooinstall aktualizuje dowolny tryb konserwacji.
2. Pobierz aktualizacje trybu konserwacji hello przy użyciu hello czynności opisane w [poprawki toodownload](#to-download-hotfixes) toosearch dla i Pobierz KB3121899, który instaluje aktualizacje oprogramowania układowego dysku (hello inne aktualizacje powinny być zainstalowane przez teraz).
3. Wykonaj kroki hello na liście [zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello obsługi trybu aktualizacji.

## <a name="install-update-2-as-a-hotfix"></a>Instalowanie aktualizacji 2 jako poprawki
Użyj tej procedury, jeśli nie hello bramy wyboru podczas próby aktualizacji hello tooinstall za pośrednictwem hello klasycznego portalu Azure. Witaj sprawdzenie nie powiedzie się, masz przypisane interfejs sieciowy 0-DATA tooa bramy i urządzeniu jest uruchomiona tooUpdate wcześniejszych wersji 1 oprogramowania.

Hello wersji oprogramowania, które można uaktualnić za pomocą metody poprawki hello są Update 0.1, Update 0.2 i Update 0.3, aktualizacja 1, aktualizacja 1.1 i 1.2 aktualizacji. Metoda poprawki Hello polega na powitania następujące trzy kroki:

* Pobierz hello poprawki z hello wykazu usługi Microsoft Update.
* Zainstaluj i sprawdź regularne hello poprawki.
* Zainstaluj i sprawdź poprawkę trybu konserwacji hello.

tooinstall Update 2 jako poprawki, należy pobrać i zainstalować hello następujące poprawki:

| Kolejność | KB | Opis | Typ aktualizacji |
| --- | --- | --- | --- |
| 1 |KB3121901 |Aktualizacja oprogramowania |Regularne |
| 2 |KB3121900 |Sterownik LSI |Regularne |
| 3 |KB3080728 |Poprawka Storport </br> Windows Server 2012 R2 |Regularne |
| 4 |KB3090322 |Poprawka spaceport </br> Windows Server 2012 R2 |Regularne |
| 5 |KB3121899 |Oprogramowanie układowe dysku |Konserwacji |

> [!IMPORTANT]
> * Jeśli urządzenie korzysta z wersji Release (GA), skontaktuj się z [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist z hello aktualizacji.
> * Ta procedura toobe musi wykonać tylko raz tooapply Update 2. Możesz użyć hello Azure classic portal tooapply kolejnych aktualizacji.
> * Każda instalacja poprawek może zająć toocomplete około 20 minut. Godzina instalacji całkowita jest too2 Zamknij godzin.
> * Przed użyciem tej procedury tooapply hello aktualizacji, upewnij się, że zarówno kontrolery urządzeń są w trybie online i wszystkie składniki sprzętowe hello są w dobrej kondycji.
> 
> 

Jako poprawki, należy wykonać następujące kroki tooapply hello tej aktualizacji.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [wersji Update 2](storsimple-update2-release-notes.md).

