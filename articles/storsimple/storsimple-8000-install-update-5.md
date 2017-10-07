---
title: "aaaInstall aktualizacji 5 na urządzeniu z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
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
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: a832f9953e8e39408efeeed375e3afe8eee8d0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-5-on-your-storsimple-device"></a>Instalowanie aktualizacji 5 na urządzeniu StorSimple

## <a name="overview"></a>Omówienie

W tym samouczku wyjaśniono, jak tooinstall aktualizacji 5 na urządzeniu StorSimple ze starszą wersją oprogramowania za pośrednictwem hello portalu Azure i przy użyciu metody poprawki hello. Metoda poprawki Hello jest używana, gdy brama jest skonfigurowana w interfejsie sieciowym innym niż dane 0 hello urządzenia StorSimple i próbujesz tooupdate z wersji oprogramowania 1 przed aktualizacją.

Aktualizacja 5 obejmuje oprogramowanie urządzenia, Storport i Spaceport, aktualizacje zabezpieczeń systemu operacyjnego i aktualizacje systemu operacyjnego, a aktualizacje oprogramowania układowego dysku.  oprogramowanie urządzenia Hello, Spaceport Storport, zabezpieczeń i inne aktualizacje systemu operacyjnego są Brak aktualizacji. mogą być stosowane Hello Brak lub regularnych aktualizacji, za pośrednictwem portalu Azure hello lub metodą hello poprawki. aktualizacje oprogramowania układowego dysku Hello są aktualizacje zakłócenie i są stosowane, gdy urządzenie hello jest w trybie konserwacji metodą poprawki hello przy użyciu interfejsu programu Windows PowerShell hello hello urządzenia.

> [!IMPORTANT]
> * Zestaw ręczne i automatyczne wstępne sprawdzanie gotowe toohello uprzedniej instalacji toodetermine hello urządzenia kondycji pod względem sprzętu stanu i łączność sieciową. Kontrole wstępne są wykonywane tylko wtedy, gdy należy zastosować aktualizacje hello z hello portalu Azure.
> * Zaleca się zainstalowanie oprogramowania hello i innych regularne aktualizacje za pomocą hello portalu Azure. Interfejsu programu Windows PowerShell toohello hello urządzenia (tooinstall aktualizacje) należy postępować tylko, jeśli hello przed aktualizacją bramy sprawdzenie nie powiedzie się w portalu hello. W zależności od wersji hello aktualizujesz z hello aktualizacji może potrwać 4 godziny (lub nowszego) tooinstall. aktualizacje trybu konserwacji Hello muszą być zainstalowane za pomocą interfejsu programu Windows PowerShell hello hello urządzenia. Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, te spowodować dół czasu dla danego urządzenia.
> * Uruchamianie hello opcjonalne StorSimple Snapshot Manager, upewnij się, uaktualniono Snapshot Manager wersji tooUpdate 5 poprzednich tooupdating hello urządzenia.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-5-via-hello-azure-portal"></a>Instalowanie aktualizacji 5 za pomocą hello portalu Azure
Wykonaj następujące kroki tooupdate hello urządzenia zbyt[aktualizacji 5](storsimple-update5-release-notes.md).

> [!NOTE]
> Microsoft ściąga dodatkowe informacje diagnostyczne z hello urządzenia. W związku z tym gdy działu operacji identyfikuje urządzenia, które występują problemy, firma Microsoft są lepsze informacje wyposażone toocollect z hello urządzenia i diagnozowanie problemów.

[!INCLUDE [storsimple-8000-install-update4-via-portal](../../includes/storsimple-8000-install-update5-via-portal.md)]

Sprawdź, czy urządzenie działa **StorSimple 8000 serii aktualizacji 5 (6.3.9600.17845)**. Witaj **ostatniej aktualizacji daty** powinien być modyfikowany.

* Teraz zobaczysz, że są dostępne aktualizacje trybu konserwacji hello (ten komunikat może nadal toobe są wyświetlane się too24 godzin po zainstalowaniu hello aktualizacji). Aktualizacje trybu konserwacji są destrukcyjne aktualizacje, które powoduje przestój urządzenia i mogą być stosowane tylko za pośrednictwem interfejsu programu Windows PowerShell hello urządzenia.

* Pobierz aktualizacje trybu konserwacji hello przy użyciu hello czynności opisane w [poprawki toodownload](#to-download-hotfixes) toosearch dla i Pobierz KB4011837, który instaluje aktualizacje oprogramowania układowego dysku (hello inne aktualizacje powinny być zainstalowane przez teraz). Wykonaj kroki hello na liście [zainstalowany i sprawdź poprawki trybu konserwacji](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello obsługi trybu aktualizacji.

## <a name="install-update-5-as-a-hotfix"></a>Instalowanie aktualizacji 5 jako poprawki


Hello wersji oprogramowania, które można uaktualnić za pomocą metody poprawki hello są:

* Zaktualizuj 0,1, 0,2, 0,3
* Aktualizacja 1, 1.1 i 1.2
* Aktualizacja 2, 2.1, 2.2
* Aktualizacja 3 w wersji 3.1
* Aktualizacja 4

> [!NOTE] 
> Witaj zalecana metoda tooinstall, jest za pośrednictwem portalu Azure hello aktualizacji 5. Użyj tej procedury, jeśli nie hello bramy wyboru podczas próby aktualizacji hello tooinstall za pośrednictwem hello portalu Azure. Witaj sprawdzenie nie powiedzie się, gdy bramy przypisane interfejs sieciowy 0-DATA tooa urządzeniu jest uruchomiona wersja oprogramowania starszych niż Update 1.

Metoda poprawki Hello polega na powitania następujące trzy kroki:

1. Pobierz hello poprawki z hello wykazu usługi Microsoft Update.
2. Zainstaluj i sprawdź regularne hello poprawki.
3. Zainstaluj i sprawdź poprawkę trybu konserwacji hello.

#### <a name="download-updates-for-your-device"></a>Pobierz aktualizacje dla urządzenia

Należy pobrać i zainstalować następujące hello poprawek w hello określonej kolejności i hello sugerowane folderów:

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji |Zainstaluj w folderze|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4037264 |Aktualizacja oprogramowania<br> Pobierz oba _HcsSfotwareUpdate.exe_ i _CisMSDAgent.exe_ |Regularne <br></br>Bezproblemowa |~ 25 minut. |FirstOrderUpdate|

Aktualizowania z urządzenia z uruchomioną aktualizacji 4, wystarczy tylko aktualizacje zbiorcze tooinstall hello systemu operacyjnego jako drugi aktualizacje kolejności.

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji |Zainstaluj w folderze|
| --- | --- | --- | --- | --- | --- |
| 2A. |KB4025336 |Pakiet aktualizacji zbiorczych systemu operacyjnego <br> Pobierz wersję systemu Windows Server 2012 R2 |Regularne <br></br>Bezproblemowa |- |SecondOrderUpdate|

W przypadku instalowania z urządzenia z uruchomioną aktualizacji 3 lub starszym, należy zainstalować hello ponadto następujące aktualizacje zbiorcze toohello.

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji |Zainstaluj w folderze|
| --- | --- | --- | --- | --- | --- |
| 2B. |KB4011841 <br> KB4011842 |Sterownik LSI i aktualizacje oprogramowania układowego <br> Aktualizacja oprogramowania układowego należy (wersja 3.38) |Regularne <br></br>Bezproblemowa |~ 3 godziny <br> (dotyczy również 2A. + 2B. + 2 C.)|SecondOrderUpdate|
| 2C. |KB3139398 <br> KB3142030 <br> KB3108381 <br> KB3153704 <br> KB3174644 <br> KB3139914   |Pakiet aktualizacji zabezpieczeń systemu operacyjnego <br> Pobierz wersję systemu Windows Server 2012 R2 |Regularne <br></br>Bezproblemowa |- |SecondOrderUpdate|
| 2W. |KB3146621 <br> KB3103616 <br> KB3121261 <br> KB3123538 |Pakiet aktualizacji systemu operacyjnego <br> Pobierz wersję systemu Windows Server 2012 R2 |Regularne <br></br>Bezproblemowa |- |SecondOrderUpdate|


Możesz również przeprowadzić aktualizacje oprogramowania układowego dysku tooinstall na wszystkie aktualizacje hello pokazano hello poprzednich tabel. Możesz sprawdzić, czy należy hello aktualizacje oprogramowania układowego dysku, uruchamiając hello `Get-HcsFirmwareVersion` polecenia cmdlet. Jeśli używasz tych wersji oprogramowania układowego: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N003`, `0107`, a następnie nie trzeba tooinstall te aktualizacje.

| Kolejność | KB | Opis | Typ aktualizacji | Godzina instalacji | Zainstaluj w folderze|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4037263 |Oprogramowanie układowe dysku |Konserwacji <br></br>Problem |~ 30 minut. | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Aktualizowania z aktualizacją Update 4, hello instalacji całkowity czas jest too4 Zamknij godzin.
> * Przed użyciem tej procedury tooapply hello aktualizacji, upewnij się, że zarówno kontrolery urządzeń hello są w trybie online i wszystkie składniki sprzętowe hello są w dobrej kondycji.

Wykonaj następujące kroki toodownload hello i zainstaluj hello poprawki.

[!INCLUDE [storsimple-install-update5-hotfix](../../includes/storsimple-install-update5-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello [wersji aktualizacji 5](storsimple-update5-release-notes.md).

