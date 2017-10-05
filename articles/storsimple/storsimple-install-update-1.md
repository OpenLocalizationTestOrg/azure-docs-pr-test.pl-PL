---
title: "Zainstaluj aktualizację 1.2 na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak zainstalować StorSimple 8000 serii aktualizacji 1.2 na urządzeniu z serii StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 80ff35cc47dfc38089f4c392ef4c90baf9ccc03e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a>Zainstaluj aktualizację 1.2 na urządzeniu z serii StorSimple 8000
## <a name="overview"></a>Omówienie
W tym samouczku przedstawiono sposób instalacji 1.2 aktualizacji na urządzeniu StorSimple, w którym jest uruchomiona wersja oprogramowania przed Update 1. Samouczek obejmuje również dodatkowych kroków wymaganych do aktualizacji, gdy brama jest skonfigurowana w interfejsie sieciowym innym niż dane 0 urządzenia StorSimple.

1.2 aktualizacja urządzenia aktualizacji oprogramowania, aktualizacje sterowników LSI i aktualizacje oprogramowania układowego dysku. Oprogramowanie i aktualizacje sterowników LSI Brak aktualizacji i mogą być stosowane za pośrednictwem klasycznego portalu Azure. Aktualizacje oprogramowania układowego dysku destrukcyjne aktualizacji i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell urządzenia.

W zależności od wersji urządzeniu jest uruchomiona, można określić, czy 1.2 aktualizacji będzie można zastosować. Można sprawdzić wersji oprogramowania na urządzeniu, przechodząc do **szybkiego dostępu** sekcji urządzenia **pulpitu nawigacyjnego**.

</br>

| Jeśli wersja oprogramowania... | Co się stanie w portalu? |
| --- | --- |
| Wydanie — ogólna dostępność |Jeśli używasz wydanej wersji (GA), nie należy stosować tej aktualizacji. Sprawdź [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) Aby zaktualizować urządzenie. |
| Update 0.1 |Portal ma zastosowanie aktualizacja 1.2. |
| Update 0.2 |Portal ma zastosowanie aktualizacja 1.2. |
| Update 0.3 |Portal ma zastosowanie aktualizacja 1.2. |
| Update 1 |Ta aktualizacja nie będzie dostępne. |
| Aktualizacja 1.1 |Ta aktualizacja nie będzie dostępne. |

</br>

> [!IMPORTANT]
> * Nie widzisz 1.2 aktualizacji natychmiast, ponieważ jak etapowego wdrażania aktualizacji. Skanowanie w poszukiwaniu aktualizacji ponownie za kilka dni jako tej aktualizacji zostanie wkrótce udostępnione.
> * Ta aktualizacja obejmuje zestaw wstępne Sprawdzanie ręczne i automatyczne ustalenie kondycji urządzenia pod względem sprzętu stanu i łączność sieciową. Kontrole wstępne są wykonywane tylko wtedy, gdy należy zastosować aktualizacje z klasycznego portalu Azure.
> * Zaleca się zainstalowanie aktualizacji oprogramowania i sterowników za pośrednictwem klasycznego portalu Azure. Tylko powinien możesz przejść do interfejsu programu Windows PowerShell, urządzenia (w celu instalowania aktualizacji), jeśli sprawdzenie przed aktualizacją bramy nie powiedzie się w portalu. Aktualizacji może zająć 5 – 10 godzin instalacji (w tym aktualizacje systemu Windows). Aktualizacje trybu konserwacji musi być zainstalowany za pośrednictwem interfejsu programu Windows PowerShell urządzenia. Aktualizacje trybu konserwacji są aktualizacje destrukcyjne, te spowoduje dół czasu dla danego urządzenia.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-the-azure-classic-portal"></a>Zainstaluj aktualizację 1.2 za pośrednictwem klasycznego portalu Azure
Wykonaj poniższe kroki, aby zaktualizować urządzenie do [zaktualizować 1.2](storsimple-update1-release-notes.md). Użyj tej procedury, tylko wtedy, gdy brama skonfigurowany w interfejsie sieciowym 0 danych na urządzeniu.

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Sprawdź, czy urządzenie działa **1.2 aktualizacji serii StorSimple 8000 (6.3.9600.17584)**. **Ostatniej aktualizacji daty** również powinien być modyfikowany. Widoczny będzie również, że są dostępne aktualizacje tryb konserwacji (ten komunikat może nadal wyświetlane przez 24 godziny, po zainstalowaniu aktualizacji).
   
   Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, które powoduje przestój urządzenia i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell urządzenia.
   
   ![Strona konserwacji](./media/storsimple-install-update-1/InstallUpdate12_10M.png "strony konserwacji")
2. Pobierz aktualizacje tryb konserwacji przy użyciu kroków opisanych w [do pobrania poprawek](#to-download-hotfixes) do wyszukania i pobrania KB3063416, które instaluje aktualizacje oprogramowania układowego dysku (inne aktualizacje powinny być zainstalowane przez teraz).
3. Wykonaj czynności opisane w [zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes) trybu konserwacji do zainstalowania aktualizacji.
4. W klasycznym portalu Azure, przejdź do **konserwacji** i u dołu strony, kliknij przycisk **Wyszukaj aktualizacje** Sprawdź, czy wszystkie aktualizacje systemu Windows, a następnie kliknij przycisk **Zainstaluj aktualizacje**. Zakończeniu po pomyślnie zainstalowano wszystkie aktualizacje.

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a>Zainstaluj aktualizację 1.2 na urządzeniu, który ma skonfigurowane dla interfejsu sieciowego 0-DATA bramę
Tej procedury należy używać tylko wtedy, gdy nie zostanie wyboru bramy, podczas próby zainstalowania aktualizacji za pośrednictwem klasycznego portalu Azure. Sprawdzenie nie powiedzie się, masz przypisane do karty sieciowej 0-DATA bramy i urządzenia z wersją oprogramowania przed Update 1. Jeśli urządzenie nie ma bramy w interfejsie sieciowym 0-DATA, należy zaktualizować urządzenia bezpośrednio z klasycznego portalu Azure. Zobacz [instalacji aktualizacji 1.2 za pośrednictwem klasycznego portalu Azure](#install-update-1.2-via-the-azure-classic-portal).

Wersje oprogramowania, które można uaktualnić za pomocą tej metody to Update 0.1, Update 0.2 i Update 0.3.

> [!IMPORTANT]
> * Jeśli urządzenie korzysta z wersji Release (GA), skontaktuj się z [Microsoft Support](storsimple-contact-microsoft-support.md) pomocne podczas aktualizacji.
> * Ta procedura musi zostać wykonana tylko raz do zastosowania aktualizacji 1.2. Klasyczny portal Azure umożliwia stosowanie kolejnych aktualizacji.
> 
> 

Jeśli urządzenie korzysta z oprogramowania 1 przed aktualizacją i ma bramę, ustaw dla interfejsu sieciowego, inne niż dane 0, 1.2 aktualizację można zastosować dwa sposoby:

* **Opcja 1**: Pobierz aktualizację i zastosować je za pomocą `Start-HcsHotfix` polecenia cmdlet w interfejsie programu Windows PowerShell urządzenia. Jest to zalecana metoda. **Nie należy używać tej metody do zastosowania aktualizacji 1.2, jeśli urządzenie korzysta z aktualizacji w wersji 1.0 lub 1.1 aktualizacji.**
* **Opcja 2**: Usuń konfigurację bramy i zainstalować aktualizację bezpośrednio z klasycznego portalu Azure.

W poniższych sekcjach znajdują się szczegółowe instrukcje dla każdego z nich.

## <a name="option-1-use-windows-powershell-for-storsimple-to-apply-update-12-as-a-hotfix"></a>Opcja 1: Użyj środowiska Windows PowerShell dla urządzenia StorSimple w celu zastosowania aktualizacji 1.2 jako poprawki
Tej procedury należy używać tylko wtedy, gdy używasz wersji Update 0.1, 0.2, 0.3 i jeśli Twoje wyboru bramy nie powiodło się podczas próby zainstalowania aktualizacji z klasycznego portalu Azure. Jeśli używasz wersji (GA) oprogramowania, skontaktuj się z [Microsoft Support](storsimple-contact-microsoft-support.md) Aby zaktualizować urządzenie.

Aby zainstalować aktualizację 1.2 jako poprawki, należy pobrać i zainstalować następujące poprawki:

| Kolejność | KB | Opis | Typ aktualizacji |
| --- | --- | --- | --- |
| 1 |KB3063418 |Aktualizacja oprogramowania |Regularne |
| 2 |KB3043005 |Aktualizacja kontrolera LSI SAS |Regularne |
| 3 |KB3063416 |Oprogramowanie układowe dysku |Konserwacji |

Przed użyciem tej procedury, aby zastosować aktualizację, upewnij się, że:

* Zarówno kontrolery urządzeń są w trybie online.

Wykonaj poniższe kroki, aby zastosować aktualizację 1.2. **Aktualizacji może potrwać około 2 godziny do ukończenia (około 30 minut do oprogramowania, 30 minut dla sterownika, 45 minut dla oprogramowania układowego dysku).**

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-the-azure-classic-portal-to-apply-update-12-after-removing-the-gateway-configuration"></a>Opcja 2: Użyj klasycznego portalu Azure do zastosowania aktualizacji 1.2 po usunięciu konfiguracji bramy
Ta procedura ma zastosowanie tylko do urządzenia StorSimple wersji oprogramowania przed Update 1 i brama ustawić w interfejsie sieciowym innym niż dane 0. Należy wyczyścić bramy przed zastosowaniem aktualizacji.

Aktualizacja może potrwać kilka godzin. Jeśli hosty w różnych podsieciach, usuwając konfigurację bramy w interfejsach iSCSI może spowodować Przestój. Zaleca się skonfigurowanie danych 0 dla ruchu iSCSI, aby zmniejszyć przestoje.

Wykonaj poniższe kroki, aby wyłączyć interfejsu sieciowego z bramą, a następnie Zastosuj aktualizację.

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [wersji 1.2 aktualizacji](storsimple-update1-release-notes.md).

