---
title: "aaaInstall 1.2 aktualizacji na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooinstall StorSimple 8000 serii aktualizacji 1.2 na urządzeniu z serii StorSimple 8000."
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
ms.openlocfilehash: 0a7601dc0b1ce60eb854227243ecb02d6fb2c678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a>Zainstaluj aktualizację 1.2 na urządzeniu z serii StorSimple 8000
## <a name="overview"></a>Omówienie
W tym samouczku wyjaśniono, jak tooinstall zaktualizować 1.2 na urządzeniu StorSimple działa tooUpdate wcześniejszych wersji 1 oprogramowania. Samouczek Hello obejmuje również hello dodatkowe kroki wymagane hello aktualizacji, gdy brama jest skonfigurowana w interfejsie sieciowym innym niż dane 0 hello urządzenia StorSimple.

1.2 aktualizacja urządzenia aktualizacji oprogramowania, aktualizacje sterowników LSI i aktualizacje oprogramowania układowego dysku. Witaj LSI sterownik aktualizacji oprogramowania i Brak aktualizacji i mogą być stosowane za pośrednictwem hello klasycznego portalu Azure. aktualizacje oprogramowania układowego dysku Hello są aktualizacje zakłócenie i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell hello hello urządzenia.

W zależności od wersji urządzeniu jest uruchomiona, można określić, czy 1.2 aktualizacji będzie można zastosować. Można sprawdzić wersji oprogramowania hello urządzenia przechodząc toohello **szybkiego dostępu** sekcji urządzenia **pulpitu nawigacyjnego**.

</br>

| Jeśli wersja oprogramowania... | Co się stanie w portalu hello? |
| --- | --- |
| Wydanie — ogólna dostępność |Jeśli używasz wydanej wersji (GA), nie należy stosować tej aktualizacji. Sprawdź [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate urządzenia. |
| Update 0.1 |Portal ma zastosowanie aktualizacja 1.2. |
| Update 0.2 |Portal ma zastosowanie aktualizacja 1.2. |
| Update 0.3 |Portal ma zastosowanie aktualizacja 1.2. |
| Update 1 |Ta aktualizacja nie będzie dostępne. |
| Aktualizacja 1.1 |Ta aktualizacja nie będzie dostępne. |

</br>

> [!IMPORTANT]
> * Nie widzisz 1.2 aktualizacji natychmiast, ponieważ jak etapowego wdrażania hello aktualizacji. Skanowanie w poszukiwaniu aktualizacji ponownie za kilka dni jako tej aktualizacji zostanie wkrótce udostępnione.
> * Ta aktualizacja obejmuje zestaw kondycji urządzenia hello toodetermine ręczne i automatyczne wstępne sprawdzanie pod względem sprzętu stanu i łączność sieciową. Kontrole wstępne są wykonywane tylko wtedy, gdy należy zastosować aktualizacje hello z hello klasycznego portalu Azure.
> * Zaleca się instalowanie oprogramowania hello i aktualizacje sterowników za pomocą hello klasycznego portalu Azure. Interfejsu programu Windows PowerShell toohello hello urządzenia (tooinstall aktualizacje) należy postępować tylko, jeśli hello przed aktualizacją bramy sprawdzenie nie powiedzie się w portalu hello. Witaj aktualizacji może potrwać tooinstall 5 – 10 godzin (w tym aktualizacje systemu Windows hello). aktualizacje trybu konserwacji Hello muszą być zainstalowane za pomocą interfejsu programu Windows PowerShell hello hello urządzenia. Aktualizacje trybu konserwacji są aktualizacje destrukcyjne, te spowoduje dół czasu dla danego urządzenia.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-hello-azure-classic-portal"></a>Zainstaluj aktualizację 1.2 za pośrednictwem hello klasycznego portalu Azure
Wykonaj następujące kroki tooupdate hello urządzenia zbyt[1.2 aktualizacji](storsimple-update1-release-notes.md). Użyj tej procedury, tylko wtedy, gdy brama skonfigurowany w interfejsie sieciowym 0 danych na urządzeniu.

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Sprawdź, czy urządzenie działa **1.2 aktualizacji serii StorSimple 8000 (6.3.9600.17584)**. Witaj **ostatniej aktualizacji daty** również powinien być modyfikowany. Widoczny będzie również, że są dostępne aktualizacje tryb konserwacji (ten komunikat może nadal toobe są wyświetlane się too24 godzin po zainstalowaniu hello aktualizacji).
   
   Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, które powoduje przestój urządzenia i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell hello urządzenia.
   
   ![Strona konserwacji](./media/storsimple-install-update-1/InstallUpdate12_10M.png "strony konserwacji")
2. Pobierz aktualizacje trybu konserwacji hello przy użyciu hello czynności opisane w [poprawki toodownload](#to-download-hotfixes) toosearch dla i Pobierz KB3063416, który instaluje aktualizacje oprogramowania układowego dysku (hello inne aktualizacje powinny być zainstalowane przez teraz).
3. Wykonaj kroki hello na liście [zainstalować i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello obsługi trybu aktualizacji.
4. W klasycznym portalu Azure hello kolejno toohello **konserwacji** i u dołu hello hello strony, kliknij przycisk **Wyszukaj aktualizacje** toocheck wszystkie aktualizacje systemu Windows, a następnie kliknij przycisk **Zainstaluj aktualizacje** . Zakończeniu po wszystkich z hello aktualizacje zostały pomyślnie zainstalowane.

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a>Zainstaluj aktualizację 1.2 na urządzeniu, który ma skonfigurowane dla interfejsu sieciowego 0-DATA bramę
Tej procedury należy użyć tylko w przypadku awarii hello bramy wyboru podczas próby aktualizacji hello tooinstall za pośrednictwem hello klasycznego portalu Azure. Witaj sprawdzenie nie powiedzie się, masz przypisane interfejs sieciowy 0-DATA tooa bramy i urządzeniu jest uruchomiona tooUpdate wcześniejszych wersji 1 oprogramowania. Jeśli urządzenie nie ma bramy w interfejsie sieciowym 0-DATA, należy zaktualizować urządzenia bezpośrednio z hello klasycznego portalu Azure. Zobacz [instalacji aktualizacji 1.2 za pośrednictwem klasycznego portalu Azure hello](#install-update-1.2-via-the-azure-classic-portal).

Hello wersje oprogramowania, które można uaktualnić za pomocą tej metody to Update 0.1, Update 0.2 i Update 0.3.

> [!IMPORTANT]
> * Jeśli urządzenie korzysta z wersji Release (GA), skontaktuj się z [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist z hello aktualizacji.
> * Ta procedura toobe musi wykonać tylko raz tooapply, 1.2 aktualizacji. Możesz użyć hello Azure classic portal tooapply kolejnych aktualizacji.
> 
> 

Jeśli urządzenie korzysta z oprogramowania 1 przed aktualizacją i ma bramę, ustaw dla interfejsu sieciowego, inne niż dane 0, można zastosować aktualizacji 1.2 hello następujące dwa sposoby:

* **Opcja 1**: Pobierz aktualizację hello i zastosować je za pomocą hello `Start-HcsHotfix` polecenia cmdlet z interfejsu programu Windows PowerShell hello hello urządzenia. Jest to zalecana metoda hello. **Nie należy używać tej metody tooapply 1.2 aktualizacji, jeśli urządzenie korzysta z aktualizacji w wersji 1.0 lub 1.1 aktualizacji.**
* **Opcja 2**: Usuń konfigurację bramy hello i hello instalacji aktualizacji bezpośrednio z hello klasycznego portalu Azure.

Szczegółowe instrukcje dla każdego z nich są przedstawione w hello następujące sekcje.

## <a name="option-1-use-windows-powershell-for-storsimple-tooapply-update-12-as-a-hotfix"></a>Opcja 1: Użyj środowiska Windows PowerShell dla StorSimple tooapply 1.2 aktualizacji jako poprawki
Tej procedury należy używać tylko wtedy, gdy używasz wersji Update 0.1, 0.2, 0.3 i jeśli Twoje wyboru bramy nie powiodło się podczas próby aktualizacji tooinstall z hello klasycznego portalu Azure. Jeśli używasz wersji (GA) oprogramowania, skontaktuj się z [Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate urządzenia.

tooinstall 1.2 aktualizacji jako poprawki, należy pobrać i zainstalować hello następujące poprawki:

| Kolejność | KB | Opis | Typ aktualizacji |
| --- | --- | --- | --- |
| 1 |KB3063418 |Aktualizacja oprogramowania |Regularne |
| 2 |KB3043005 |Aktualizacja kontrolera LSI SAS |Regularne |
| 3 |KB3063416 |Oprogramowanie układowe dysku |Konserwacji |

Przed użyciem tej procedury tooapply hello aktualizacji, upewnij się, że:

* Zarówno kontrolery urządzeń są w trybie online.

Wykonaj następujące kroki tooapply 1.2 aktualizacji hello. **Witaj aktualizacji może potrwać około 2 godziny toocomplete (około 30 minut do oprogramowania, 30 minut dla sterownika, 45 minut dla oprogramowania układowego dysku).**

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-hello-azure-classic-portal-tooapply-update-12-after-removing-hello-gateway-configuration"></a>Opcja 2: Użycie hello klasycznego portalu Azure tooapply 1.2 aktualizacji po usunięciu konfiguracji bramy hello
Ta procedura dotyczy tylko urządzeń tooStorSimple uruchomione tooUpdate wcześniejszych wersji 1 oprogramowania i mieć bramę ustawić w interfejsie sieciowym innym niż dane 0. Konieczne będzie tooclear hello ustawienie wcześniejsze tooapplying hello jest aktualizacja bramy.

Witaj aktualizacji może potrwać kilka godzin toocomplete. Jeśli hosty w różnych podsieciach, usunięcia konfiguracji bramy hello na powitania interfejsów iSCSI może spowodować Przestój. Zaleca się konfigurowanie dane 0 przestoje hello tooreduce ruchu iSCSI.

Wykonaj następujące kroki toodisable hello sieciowej z bramą hello hello, a następnie Zastosuj aktualizację hello.

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [wersji 1.2 aktualizacji](storsimple-update1-release-notes.md).

