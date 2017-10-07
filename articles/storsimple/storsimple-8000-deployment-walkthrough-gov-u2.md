---
title: "urządzenia z serii aaaDeploy StorSimple 8000 w portalu dla instytucji rządowych | Dokumentacja firmy Microsoft"
description: "Opisuje hello kroki i najlepsze rozwiązania w zakresie wdrażania hello urządzenia serii StorSimple 8000 z aktualizacją Update 3 i później i hello usługi w hello portal Azure dla instytucji rządowych."
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
ms.workload: NA
ms.date: 06/22/2017
ms.author: alkohli
ms.openlocfilehash: ea643cd59dcdf17482268d14c1348a3b5fb098b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal"></a>Wdrażanie lokalnego urządzenia StorSimple w portalu dla instytucji rządowych hello

## <a name="overview"></a>Omówienie
Zapraszamy wdrożenia urządzenia Azure StorSimple tooMicrosoft. Te samouczki wdrażania zastosować toohello z serii StorSimple 8000 uruchamiania 3 aktualizacji oprogramowania lub później hello w portalu Azure dla instytucji rządowych. Tej serii samouczków uwzględniono listę kontrolną, listę wymagania wstępne dotyczące konfiguracji oraz szczegółowe opisy kroków konfiguracji dla urządzenia StorSimple.

Hello informacje w tych samouczkach założono, że zostały sprawdzone hello środki ostrożności i rozpakowane, wówczas i kablem urządzenia StorSimple. Jeśli nadal potrzebujesz tooperform tych zadań, należy rozpocząć od sprawdzenia hello [środki ostrożności](storsimple-safety.md). Wykonaj instrukcje dotyczące urządzenia hello toounpack, instalacji w stojaku i Podłączanie kabli do urządzenia.

* [Rozpakowywanie, montowanie w stojaku i podłączanie kabli do urządzenia 8100](storsimple-8100-hardware-installation.md)
* [Rozpakowywanie, montowanie w stojaku i podłączanie kabli do urządzenia 8600](storsimple-8600-hardware-installation.md)

Konieczne będzie administratora uprawnień toocomplete hello procesu instalacji i konfiguracji. Firma Microsoft zaleca przejrzenie listy kontrolnej konfiguracji hello przed rozpoczęciem. Hello wdrażania i konfiguracji może potrwać kilka toocomplete czas.

> [!NOTE]
> Witaj StorSimple informacje na temat wdrażania publikowane w witrynie sieci Web Microsoft Azure hello stosuje tooStorSimple 8000 serii tylko urządzenia. Aby uzyskać pełne informacje dotyczące urządzeń z serii hello 7000, przejdź do: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Informacje dotyczące wdrażania urządzeń z serii 7000, zobacz hello [StorSimple systemu Przewodnik Szybki Start](http://onlinehelp.storsimple.com/111_Appliance/).


## <a name="deployment-steps"></a>Kroki wdrażania
Wykonaj te czynności tooconfigure urządzenia StorSimple i usługa Menedżera urządzeń StorSimple tooyour connect. Ponadto toohello wymagane kroki, są opcjonalne kroki i procedury, że może być konieczne toocomplete podczas wdrażania hello. instrukcje krok po kroku wdrażania Hello sygnalizującego, kiedy należy wykonać poszczególne kroki opcjonalne.

| Krok | Opis |
| --- | --- |
| **WYMAGANIA WSTĘPNE** |Te należy wykonać w ramach przygotowań do przyszłego wdrożenia hello toobe. |
| [Lista kontrolna dotycząca konfiguracji wdrożenia](#deployment-configuration-checklist) |Użyj tej listy kontrolnej toogather i rejestrowanie informacji przed tooand podczas wdrażania hello. |
| [Wymagania wstępne dotyczące wdrożenia](#deployment-prerequisites) |Te zweryfikować tego hello środowisko jest gotowe do wdrożenia. |
|  | |
| **WDROŻENIE KROK PO KROKU** |Te kroki są wymagane toodeploy urządzenia StorSimple w środowisku produkcyjnym. |
| [Krok 1. Tworzenie nowej usługi](#step-1-create-a-new-service) |Skonfiguruj magazyn i zarządzanie chmurą dla danego urządzenia StorSimple. *Jeśli masz istniejącą usługę dla innych urządzeń StorSimple, pomiń ten krok*. |
| [Krok 2: Pobieranie klucza rejestracji usługi hello](#step-2-get-the-service-registration-key) |Użyj tego klucza tooregister i połączyć z usługą zarządzania hello urządzenia StorSimple. |
| [Krok 3: Konfigurowanie i rejestrowanie urządzenia hello za pomocą programu Windows PowerShell dla urządzenia StorSimple](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |Połącz hello urządzenia tooyour sieci i zarejestrowanie go za pomocą Instalatora hello Azure toocomplete przy użyciu usługi zarządzania hello. |
| [Krok 4: Przeprowadzenie hello minimalnej konfiguracji urządzenia](#step-4-complete-minimum-device-setup) </br>Opcjonalnie: aktualizacja urządzenia StorSimple. |Użyj hello zarządzania usługi toocomplete hello ustawienia urządzenia i Włącz tooprovide magazynu. |
| [Krok 5. Tworzenie kontenera woluminów](#step-5-create-a-volume-container) |Tworzenie kontenera woluminów tooprovision. Kontener woluminów obejmuje konta magazynu, przepustowości i ustawienia szyfrowania wszystkich woluminów hello zawarte w niej. |
| [Krok 6. Tworzenie woluminu](#step-6-create-a-volume) |Zainicjuj obsługę woluminów magazynu na powitania urządzeniu StorSimple dla serwerów. |
| [Krok 7. Instalowanie, inicjowanie i formatowanie woluminu](#step-7-mount-initialize-and-format-a-volume) </br>Opcjonalnie: konfigurowanie wielościeżkowego wejścia/wyjścia (MPIO) |Połącz podany przez urządzenie hello magazynu iSCSI toohello serwerów. Opcjonalnie skonfigurować wielościeżkowe wejście/wyjście tooensure, że serwery tolerują błędy linków, sieci i interfejsu. |
| [Krok 8. Tworzenie kopii zapasowej](#step-8-take-a-backup) |Konfigurowanie sieci tooprotect zasad tworzenia kopii zapasowej danych |
|  | |
| **INNE PROCEDURY** |Procedury toothese toorefer może być konieczne podczas wdrażania rozwiązania. |
| [Konfigurowanie nowego konta magazynu dla usługi hello](#configure-a-new-storage-account-for-the-service) | |
| [Użyj konsoli szeregowej urządzenia toohello tooconnect programu PuTTY](#use-putty-to-connect-to-the-device-serial-console) | |
| [Wyszukiwanie i stosowanie aktualizacji](#scan-for-and-apply-updates) | |
| [Pobierz hello IQN hosta z systemem Windows Server](#get-the-iqn-of-a-windows-server-host) | |
| [Ręczne tworzenie kopii zapasowej](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a>Lista kontrolna dotycząca konfiguracji wdrożenia
Przed przystąpieniem do wdrażania urządzenia StorSimple, konieczne będzie toocollect informacji tooconfigure hello oprogramowania na urządzeniu. Niektóre z tych informacji wcześniejsze przygotowanie usprawni hello proces wdrażania urządzenia StorSimple hello w danym środowisku. Pobranie i użycie szczegóły konfiguracji ta lista kontrolna toonote hello, podczas wdrażania urządzenia.

[Pobieranie listy kontrolnej dotyczącej konfiguracji wdrożenia urządzenia StorSimple](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a>Wymagania wstępne dotyczące wdrożenia
Hello następujące sekcje opisano wymagania wstępne dotyczące hello konfiguracji dla usługi Menedżer urządzeń StorSimple oraz urządzenia StorSimple.

### <a name="for-hello-storsimple-device-manager-service"></a>Dla hello usługi Menedżer StorSimple urządzenia
Przed rozpoczęciem upewnij się, że:

* Masz konto Microsoft z poświadczeniami dostępu.
* Masz konto magazynu platformy Microsoft Azure z poświadczeniami dostępu.
* Subskrypcja platformy Microsoft Azure jest włączona dla hello usługi Menedżer StorSimple urządzenia. Subskrypcję należy zakupić w ramach hello [umowy Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).
* Masz dostęp do oprogramowania do emulacji tooterminal takiego jak PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Dla urządzenia hello w centrum danych hello
Przed skonfigurowaniem urządzenia hello, upewnij się, że:

* Urządzenie zostało całkowicie rozpakowane, zamontowane w stojaku i podłączono wszystkie kable umożliwiające dostęp do zasilania, sieci oraz dostęp szeregowy, zgodnie z opisem w części:
  
  * [Rozpakowywanie, montowanie w stojaku i podłączanie kabli do urządzenia 8100](storsimple-8100-hardware-installation.md)
  * [Rozpakowywanie, montowanie w stojaku i podłączanie kabli do urządzenia 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Witaj sieci w centrum danych hello
Przed rozpoczęciem upewnij się, że:

* Witaj portów w zaporze centrum danych są otwarte tooallow dla ruchu iSCSI i chmury zgodnie z opisem w [wymagania dotyczące sieci dla urządzenia StorSimple](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>Wdrożenie krok po kroku
Użyj hello następujące instrukcje krok po kroku toodeploy urządzenia StorSimple w centrum danych hello.

## <a name="step-1-create-a-new-service"></a>Krok 1. Tworzenie nowej usługi
Usługa Menedżer urządzeń StorSimple umożliwia zarządzanie wieloma urządzeniami StorSimple. Wykonaj następujące kroki toocreate nowe wystąpienie klasy hello usługi Menedżer StorSimple urządzenia hello.

[!INCLUDE [storsimple-8000-create-new-service-gov](../../includes/storsimple-8000-create-new-service-gov.md)]

> [!IMPORTANT]
> Jeśli nie włączono hello automatyczne tworzenie konta magazynu z usługą, konieczne będzie toocreate co najmniej jedno konto magazynu, po pomyślnym utworzeniu usługi. To konto magazynu będzie używane podczas tworzenia kontenera woluminu.
> 
> * Jeśli nie utworzono automatycznie konta magazynu, należy przejść za[Konfigurowanie nowego konta magazynu dla usługi hello](#configure-a-new-storage-account-for-the-service) szczegółowe informacje.
> * Jeśli włączono automatyczne tworzenie konta magazynu hello Przejdź zbyt[krok 2: Pobierz klucz rejestracji usługi hello](#step-2-get-the-service-registration-key).


## <a name="step-2-get-hello-service-registration-key"></a>Krok 2: Pobieranie klucza rejestracji usługi hello
Po skonfigurowaniu i uruchomieniu hello usługi Menedżer StorSimple urządzenia należy klucz rejestracji usługi hello tooget. Ten klucz jest używany tooregister i połączyć z usługą toohello urządzenia StorSimple.

Wykonaj następujące kroki w portalu dla instytucji rządowych hello hello.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Krok 3: Konfigurowanie i rejestrowanie urządzenia hello za pomocą programu Windows PowerShell dla urządzenia StorSimple
Użyj programu Windows PowerShell dla StorSimple toocomplete hello początkowej konfiguracji urządzenia StorSimple, zgodnie z objaśnieniem w hello procedury. Konieczne będzie toouse emulacji terminala oprogramowania toocomplete ten krok. Aby uzyskać więcej informacji, zobacz [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-8000-configure-and-register-device-gov](../../includes/storsimple-8000-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Krok 4. Przeprowadzenie minimalnej konfiguracji urządzenia
Hello urządzenia minimalnej konfiguracji urządzenia StorSimple konieczne jest:

* Podaj przyjazną nazwę dla urządzenia.
* Ustaw strefę czasową hello urządzenia.
* Przypisanie stałych adresów IP kontrolerów hello tooboth.

Wykonaj następujące kroki w hello Azure dla instytucji rządowych portalu toocomplete hello minimalnej konfiguracji urządzenia hello.

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a>Krok 5. Tworzenie kontenera woluminów
Kontener woluminów obejmuje konta magazynu, przepustowości i ustawienia szyfrowania wszystkich woluminów hello zawarte w niej. Toocreate kontener woluminów należy przed zainicjowaniem woluminów na urządzeniu StorSimple.

Wykonaj następujące kroki w portalu toocreate dla instytucji rządowych hello kontener woluminów hello.

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Krok 6. Tworzenie woluminu
Po utworzeniu kontenera woluminów można udostępnić wolumin magazynu na urządzeniu StorSimple hello serwerów. Wykonaj następujące kroki w portalu toocreate dla instytucji rządowych hello woluminu hello.

> [!IMPORTANT]
> Menedżer urządzeń StorSimple można tworzyć tylko woluminy alokowane elastycznie.  Nie można jednak tworzyć woluminów inicjowanych częściowo.

[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Krok 7. Instalowanie, inicjowanie i formatowanie woluminu
Na hoście z systemem Windows Server, należy wykonać następujące kroki.

> [!IMPORTANT]
> * Witaj wysokiej dostępności rozwiązania StorSimple zaleca się konfigurowanie wielościeżkowego wejścia/wyjścia na iSCSI wcześniejsze tooconfiguring serwerów (opcjonalnie) z hosta. Konfiguracja wielościeżkowego wejścia/wyjścia na serwerach hostów zapewni, że hello serwery będą tolerować, łącza, sieci lub interfejsu.
> * Instrukcje iSCSI i wielościeżkowego wejścia/wyjścia instalacji i konfiguracji na hoście systemu Windows Server, przejdź zbyt[konfigurowanie wielościeżkowego wejścia/wyjścia dla urządzenia StorSimple](storsimple-configure-mpio-windows-server.md). Te będą również zawierają hello kroki toomount, inicjowanie i formatowanie woluminów StorSimple.
> * Instrukcje iSCSI i wielościeżkowego wejścia/wyjścia instalacji i konfiguracji na hoście z systemem Linux, przejdź zbyt[konfigurowanie wielościeżkowego wejścia/wyjścia dla hosta z systemem StorSimple Linux](storsimple-configure-mpio-on-linux.md)

Jeśli zdecydować tooconfigure wielościeżkowego wejścia/wyjścia, wykonać następujące kroki toomount hello, zainicjować i sformatować woluminy StorSimple na hoście systemu Windows Server.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Krok 8. Tworzenie kopii zapasowej
Kopie zapasowe oferują ochronę woluminów w określonym momencie i udoskonalają możliwości odzyskiwania przy równoczesnym zminimalizowaniu czasów przywracania. W urządzeniu StorSimple można wykonywać dwa typy kopii zapasowych: migawki lokalne i migawki w chmurze. Kopie obu typów można tworzyć jako **zaplanowane** lub **ręczne**.

Wykonaj następujące kroki w portalu toocreate dla instytucji rządowych hello zaplanowanego tworzenia kopii zapasowej hello.

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

Kopię zapasową można utworzyć ręcznie w dowolnym momencie. Procedur można przejść za[ręczne tworzenie kopii zapasowej](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Konfigurowanie nowego konta magazynu dla usługi hello
Jest to krok opcjonalny tooperform konieczne tylko wtedy, gdy nie włączono hello automatyczne tworzenie konta magazynu z usługą. Konto magazynu Microsoft Azure jest wymagany toocreate kontenera woluminów StorSimple.

Jeśli potrzebujesz konta magazynu Azure w innym regionie toocreate, zobacz [o kontach magazynu Azure](../storage/common/storage-create-storage-account.md) instrukcje krok po kroku.

Wykonaj następujące kroki w portalu dla instytucji rządowych hello na powitania hello **usługi Menedżer StorSimple urządzenia** strony.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Użyj konsoli szeregowej urządzenia toohello tooconnect programu PuTTY
tooWindows tooconnect programu PowerShell dla StorSimple, należy toouse oprogramowania emulacji terminala, takiego jak PuTTY. Programu PuTTY można używać, gdy uzyskujesz dostęp do urządzenia hello bezpośrednio za pośrednictwem konsoli szeregowej hello lub przez otwarcie sesji telnet z komputera zdalnego.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Wyszukiwanie aktualizacji i ich stosowanie
Aktualizowanie urządzenia może potrwać kilka godzin. Aby uzyskać szczegółowy opis kroków jak tooinstall hello najnowszej aktualizacji, przejdź zbyt[zainstalować aktualizacji 4](storsimple-8000-install-update-4.md).

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Pobierz hello IQN hosta z systemem Windows Server
Wykonaj następujące kroki tooget hello iSCSI hello kwalifikowana nazwa (IQN) hosta z systemem Windows z systemem Windows Server® 2012.

[!INCLUDE [Get IQN of your Windows Server host](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Ręczne tworzenie kopii zapasowej
Wykonaj następujące kroki w portalu toocreate dla instytucji rządowych hello na żądanie ręcznie kopię zapasową pojedynczego woluminu w urządzeniu StorSimple hello.

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Następne kroki
* Skonfiguruj [urządzenie wirtualne](storsimple-8000-cloud-appliance-u2.md).
* Użyj hello [usługi Menedżer StorSimple urządzenia](storsimple-8000-manager-service-administration.md) toomanage urządzenia StorSimple.

