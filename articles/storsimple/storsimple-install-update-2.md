---
title: "Instalowanie aktualizacji 2 na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak zainstalować StorSimple 8000 serii Update 2 na urządzeniu z serii StorSimple 8000."
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
ms.openlocfilehash: e788439608b7122f2bca6b99b832baa5258e472d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>Instalowanie aktualizacji 2 na urządzeniu StorSimple
## <a name="overview"></a>Omówienie
W tym samouczku przedstawiono sposób instalacji aktualizacji 2 na urządzeniu StorSimple uruchomiona starsza wersja oprogramowania za pośrednictwem klasycznego portalu Azure. Samouczek obejmuje również kroków wymaganych do aktualizacji, gdy brama jest skonfigurowany w interfejsie sieciowym innym niż dane 0 urządzenia StorSimple i są próby aktualizacji z wersji oprogramowania 1 przed aktualizacją.

Aktualizacja 2 obejmuje urządzenia aktualizacji oprogramowania, aktualizacje sterowników LSI i aktualizacje oprogramowania układowego dysku. LSI aktualizacji oprogramowania urządzenia i Brak aktualizacji i mogą być stosowane za pośrednictwem klasycznego portalu Azure. Aktualizacje oprogramowania układowego dysku destrukcyjne aktualizacji i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell urządzenia.

> [!IMPORTANT]
> * Nie widzisz Update 2 natychmiast, ponieważ jak etapowego wdrażania aktualizacji. Skanowanie w poszukiwaniu aktualizacji ponownie za kilka dni jako tej aktualizacji zostanie wkrótce udostępnione.
> * Zestaw ręczne i automatyczne wstępne sprawdzanie gotowe czasu zainstalowania w celu określenia kondycji urządzenia pod względem sprzętu stanu i łączność sieciową. Kontrole wstępne są wykonywane tylko wtedy, gdy należy zastosować aktualizacje z klasycznego portalu Azure.
> * Zaleca się zainstalowanie aktualizacji oprogramowania i sterowników za pośrednictwem klasycznego portalu Azure. Tylko powinien możesz przejść do interfejsu programu Windows PowerShell, urządzenia (w celu instalowania aktualizacji), jeśli sprawdzenie przed aktualizacją bramy nie powiedzie się w portalu. Zastosowanie aktualizacji może potrwać 4-7 godzin instalacji (w tym aktualizacje systemu Windows). Aktualizacje trybu konserwacji musi być zainstalowany za pośrednictwem interfejsu programu Windows PowerShell urządzenia. Aktualizacje trybu konserwacji są aktualizacje destrukcyjne, te spowoduje dół czasu dla danego urządzenia.
> * Uruchomiona opcjonalne StorSimple Snapshot Manager, upewnij się, że uaktualniono wersji Snapshot Manager do wersji Update 2 przed zaktualizowaniem urządzenia.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-the-azure-classic-portal"></a>Instalowanie aktualizacji 2 za pośrednictwem klasycznego portalu Azure
Wykonaj poniższe kroki, aby zaktualizować urządzenie do [Update 2](storsimple-update2-release-notes.md).

> [!NOTE]
> Aktualizacja 2 umożliwia firmie Microsoft ściągnięcia dodatkowych informacji diagnostycznych z urządzenia. W związku z tym gdy działu operacji identyfikuje urządzenia, które występują problemy, firma Microsoft mają większe możliwości zbierania informacji z urządzenia i diagnozowanie problemów. Akceptowanie Update 2, umożliwia firmie Microsoft w celu obsługi aktywne.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Sprawdź, czy urządzenie działa **StorSimple 8000 serii Update 2 (6.3.9600.17673)**. **Ostatniej aktualizacji daty** również powinien być modyfikowany. Widoczny będzie również, że są dostępne aktualizacje tryb konserwacji (ten komunikat może nadal wyświetlane przez 24 godziny, po zainstalowaniu aktualizacji).
   
   Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, które powoduje przestój urządzenia i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell urządzenia. W niektórych przypadkach po uruchomieniu 1.2 aktualizacji oprogramowania układowego dysku mogą być już aktualne, w którym to przypadku nie trzeba instalować żadnych aktualizacji w trybie konserwacji.
2. Pobierz aktualizacje tryb konserwacji przy użyciu kroków opisanych w [do pobrania poprawek](#to-download-hotfixes) do wyszukania i pobrania KB3121899, które instaluje aktualizacje oprogramowania układowego dysku (inne aktualizacje powinny być zainstalowane przez teraz).
3. Wykonaj czynności opisane w [zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes) trybu konserwacji do zainstalowania aktualizacji.

## <a name="install-update-2-as-a-hotfix"></a>Instalowanie aktualizacji 2 jako poprawki
Użyj tej procedury, jeśli nie wyboru bramy, podczas próby zainstalowania aktualizacji za pośrednictwem klasycznego portalu Azure. Sprawdzenie nie powiedzie się, masz przypisane do karty sieciowej 0-DATA bramy i urządzenia z wersją oprogramowania przed Update 1.

Wersje oprogramowania, które można uaktualnić za pomocą metody poprawki są Update 0.1, Update 0.2 i Update 0.3, aktualizacja 1, aktualizacja 1.1 i 1.2 aktualizacji. Metoda poprawki obejmuje następujące trzy kroki:

* Pobierz poprawki z wykazu usługi Microsoft Update.
* Zainstaluj i sprawdź regularne poprawki.
* Zainstaluj i sprawdź poprawkę trybu konserwacji.

Aby zainstalować aktualizacji 2 jako poprawki, należy pobrać i zainstalować następujące poprawki:

| Kolejność | KB | Opis | Typ aktualizacji |
| --- | --- | --- | --- |
| 1 |KB3121901 |Aktualizacja oprogramowania |Regularne |
| 2 |KB3121900 |Sterownik LSI |Regularne |
| 3 |KB3080728 |Poprawka Storport </br> Windows Server 2012 R2 |Regularne |
| 4 |KB3090322 |Poprawka spaceport </br> Windows Server 2012 R2 |Regularne |
| 5 |KB3121899 |Oprogramowanie układowe dysku |Konserwacji |

> [!IMPORTANT]
> * Jeśli urządzenie korzysta z wersji Release (GA), skontaktuj się z [Microsoft Support](storsimple-contact-microsoft-support.md) pomocne podczas aktualizacji.
> * Ta procedura musi zostać wykonana tylko raz do zastosowania aktualizacji 2. Klasyczny portal Azure umożliwia stosowanie kolejnych aktualizacji.
> * Każdej instalacji poprawki może trwać około 20 minut, aby zakończyć. Godzina instalacji całkowita jest bliski 2 godziny.
> * Przed użyciem tej procedury, aby zastosować aktualizację, upewnij się, że zarówno kontrolery urządzeń są w trybie online i wszystkie składniki sprzętowe są w dobrej kondycji.
> 
> 

Wykonaj poniższe kroki, aby zastosować tę aktualizację jako poprawki.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [wersji Update 2](storsimple-update2-release-notes.md).

