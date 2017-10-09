---
title: "aaaDeploy urządzenia StorSimple w portalu dla instytucji rządowych | Dokumentacja firmy Microsoft"
description: "Opisuje hello kroki i najlepsze rozwiązania dotyczące wdrażania urządzeń hello StorSimple Update 2 i usług w portalu Azure dla instytucji rządowych hello."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 5277538c-797e-4e8e-b613-31b5c10cf5a9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/16/2016
ms.author: v-sharos
ms.openlocfilehash: 68104988595341a49a87d78c4a9b1d2675759c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal-update-2"></a>Wdrażanie lokalnego urządzenia StorSimple w hello Portal dla instytucji rządowych (Update 2)
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a>Omówienie
Zapraszamy wdrożenia urządzenia Azure StorSimple tooMicrosoft. Te samouczki wdrażania zastosować toohello z serii StorSimple 8000 uruchamiania 2 aktualizacji oprogramowania w portalu Azure dla instytucji rządowych hello. Tej serii samouczków uwzględniono listę kontrolną, listę wymagania wstępne dotyczące konfiguracji oraz szczegółowe opisy kroków konfiguracji dla urządzenia StorSimple.

Hello informacje w tych samouczkach założono, że zostały sprawdzone hello środki ostrożności i rozpakowane, wówczas i kablem urządzenia StorSimple. Jeśli nadal potrzebujesz tooperform tych zadań, należy rozpocząć od sprawdzenia hello [środki ostrożności](storsimple-safety.md). Wykonaj instrukcje dotyczące urządzenia hello toounpack, instalacji w stojaku i Podłączanie kabli do urządzenia.

* [Rozpakowywanie, montowanie w stojaku i podłączanie kabli do urządzenia 8100](storsimple-8100-hardware-installation.md)
* [Rozpakowywanie, montowanie w stojaku i podłączanie kabli do urządzenia 8600](storsimple-8600-hardware-installation.md)

Konieczne będzie administratora uprawnień toocomplete hello procesu instalacji i konfiguracji. Firma Microsoft zaleca przejrzenie listy kontrolnej konfiguracji hello przed rozpoczęciem. Hello wdrażania i konfiguracji może potrwać kilka toocomplete czas.

> [!NOTE]
> Witaj StorSimple informacje na temat wdrażania publikowane w witrynie sieci Web Microsoft Azure hello stosuje tooStorSimple 8000 serii tylko urządzenia. Aby uzyskać pełne informacje dotyczące urządzeń z serii hello 7000, przejdź do: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Informacje dotyczące wdrażania urządzeń z serii 7000, zobacz hello [StorSimple systemu Przewodnik Szybki Start](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Kroki wdrażania
Wykonaj te czynności tooconfigure urządzenia StorSimple i podłącz go tooyour usługi Menedżer StorSimple. Ponadto toohello wymagane kroki, są opcjonalne kroki i procedury, że może być konieczne toocomplete podczas wdrażania hello. instrukcje krok po kroku wdrażania Hello sygnalizującego, kiedy należy wykonać poszczególne kroki opcjonalne.

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
| [Konfigurowanie wielościeżkowego wejścia/wyjścia](#configure-mpio) | |

## <a name="deployment-configuration-checklist"></a>Lista kontrolna dotycząca konfiguracji wdrożenia
Przed przystąpieniem do wdrażania urządzenia StorSimple, konieczne będzie toocollect informacji tooconfigure hello oprogramowania na urządzeniu. Niektóre z tych informacji wcześniejsze przygotowanie usprawni hello proces wdrażania urządzenia StorSimple hello w danym środowisku. Pobranie i użycie szczegóły konfiguracji ta lista kontrolna toonote hello, podczas wdrażania urządzenia.  

[Pobieranie listy kontrolnej dotyczącej konfiguracji wdrożenia urządzenia StorSimple](http://www.microsoft.com/download/details.aspx?id=49159)  

## <a name="deployment-prerequisites"></a>Wymagania wstępne dotyczące wdrożenia
Hello następujące sekcje opisano wymagania wstępne dotyczące hello konfiguracji dla usługi Menedżer StorSimple oraz urządzenia StorSimple.

### <a name="for-hello-storsimple-manager-service"></a>Dla hello usługi Menedżer StorSimple
Przed rozpoczęciem upewnij się, że:

* Masz konto Microsoft z poświadczeniami dostępu.
* Masz konto magazynu platformy Microsoft Azure z poświadczeniami dostępu.
* Subskrypcja platformy Microsoft Azure jest włączona dla hello usługi Menedżer StorSimple. Subskrypcję należy zakupić w ramach hello [umowy Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).
* Masz dostęp do oprogramowania do emulacji tooterminal takiego jak PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Dla urządzenia hello w centrum danych hello
Przed skonfigurowaniem urządzenia hello, upewnij się, że:

* Urządzenie zostało całkowicie rozpakowane, zamontowane w stojaku i podłączono wszystkie kable umożliwiające dostęp do zasilania, sieci oraz dostęp szeregowy, zgodnie z opisem w części:
  
  * [Rozpakowywanie, montowanie w stojaku i podłączanie kabli do urządzenia 8100](storsimple-8100-hardware-installation.md)
  * [Rozpakowywanie, montowanie w stojaku i podłączanie kabli do urządzenia 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Witaj sieci w centrum danych hello
Przed rozpoczęciem upewnij się, że:

* Witaj portów w zaporze centrum danych są otwarte tooallow dla ruchu iSCSI i chmury zgodnie z opisem w [wymagania dotyczące sieci dla urządzenia StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>Wdrożenie krok po kroku
Użyj hello następujące instrukcje krok po kroku toodeploy urządzenia StorSimple w centrum danych hello.

## <a name="step-1-create-a-new-service"></a>Krok 1. Tworzenie nowej usługi
Usługa Menedżer StorSimple umożliwia zarządzanie wieloma urządzeniami StorSimple. Wykonaj następujące kroki toocreate nowe wystąpienie usługi Menedżer StorSimple hello hello.

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> Jeśli nie włączono hello automatyczne tworzenie konta magazynu z usługą, konieczne będzie toocreate co najmniej jedno konto magazynu, po pomyślnym utworzeniu usługi. To konto magazynu będzie używane podczas tworzenia kontenera woluminu.
> 
> * Jeśli nie utworzono automatycznie konta magazynu, należy przejść za[Konfigurowanie nowego konta magazynu dla usługi hello](#configure-a-new-storage-account-for-the-service) szczegółowe informacje.
> * Jeśli włączono automatyczne tworzenie konta magazynu hello Przejdź zbyt[krok 2: Pobierz klucz rejestracji usługi hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Krok 2: Pobieranie klucza rejestracji usługi hello
Po skonfigurowaniu i uruchomieniu usługi Menedżer StorSimple hello należy klucz rejestracji usługi hello tooget. Ten klucz jest używany tooregister i połączyć z usługą toohello urządzenia StorSimple.

Wykonaj następujące kroki w hello Portal dla instytucji rządowych hello.

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Krok 3: Konfigurowanie i rejestrowanie urządzenia hello za pomocą programu Windows PowerShell dla urządzenia StorSimple
Użyj programu Windows PowerShell dla StorSimple toocomplete hello początkowej konfiguracji urządzenia StorSimple, zgodnie z objaśnieniem w hello procedury. Konieczne będzie toouse emulacji terminala oprogramowania toocomplete ten krok. Aby uzyskać więcej informacji, zobacz [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Krok 4. Przeprowadzenie minimalnej konfiguracji urządzenia
Hello urządzenia minimalnej konfiguracji urządzenia StorSimple konieczne jest:

* Konfigurowanie hello pomocniczy serwer DNS.
* Włączenie usługi iSCSI na co najmniej jednym interfejsie sieciowym.
* Przypisanie stałych adresów IP kontrolerów hello tooboth.

Wykonaj następujące kroki w hello Portal dla instytucji rządowych toocomplete hello minimalnej konfiguracji urządzenia hello.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Krok 5. Tworzenie kontenera woluminów
Kontener woluminów obejmuje konta magazynu, przepustowości i ustawienia szyfrowania wszystkich woluminów hello zawarte w niej. Toocreate kontener woluminów należy przed zainicjowaniem woluminów na urządzeniu StorSimple.

Wykonaj następujące kroki w toocreate Portal dla instytucji rządowych hello kontener woluminów hello.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Krok 6. Tworzenie woluminu
Po utworzeniu kontenera woluminów można udostępnić wolumin magazynu na urządzeniu StorSimple hello serwerów. Wykonaj następujące kroki w toocreate Portal dla instytucji rządowych hello woluminu hello.

> [!IMPORTANT]
> Azure StorSimple można tworzyć tylko woluminy alokowane elastycznie.  Nie można utworzyć w pełni lub częściowo inicjowanych woluminów w systemie Azure StorSimple.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Krok 7. Instalowanie, inicjowanie i formatowanie woluminu
Na hoście z systemem Windows Server, należy wykonać następujące kroki.

> [!IMPORTANT]
> * Witaj wysokiej dostępności rozwiązania StorSimple zaleca się konfigurowanie wielościeżkowego wejścia/wyjścia na iSCSI wcześniejsze tooconfiguring serwerów (opcjonalnie) z hosta. Konfiguracja wielościeżkowego wejścia/wyjścia na serwerach hostów zapewni, że hello serwery będą tolerować, łącza, sieci lub interfejsu.
> * Instrukcje iSCSI i wielościeżkowego wejścia/wyjścia instalacji i konfiguracji na hoście systemu Windows Server, przejdź zbyt[konfigurowanie wielościeżkowego wejścia/wyjścia dla urządzenia StorSimple](storsimple-configure-mpio-windows-server.md). Te będą również zawierają hello kroki toomount, inicjowanie i formatowanie woluminów StorSimple.
> * Instrukcje iSCSI i wielościeżkowego wejścia/wyjścia instalacji i konfiguracji na hoście z systemem Linux, przejdź zbyt[konfigurowanie wielościeżkowego wejścia/wyjścia dla hosta z systemem StorSimple Linux](storsimple-configure-mpio-on-linux.md)
> 
> 

Jeśli zdecydować tooconfigure wielościeżkowego wejścia/wyjścia, wykonać następujące kroki toomount hello, zainicjować i sformatować woluminy StorSimple na hoście systemu Windows Server.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Krok 8. Tworzenie kopii zapasowej
Kopie zapasowe oferują ochronę woluminów w określonym momencie i udoskonalają możliwości odzyskiwania przy równoczesnym zminimalizowaniu czasów przywracania. W urządzeniu StorSimple można wykonywać dwa typy kopii zapasowych: migawki lokalne i migawki w chmurze. Kopie obu typów można tworzyć jako **zaplanowane** lub **ręczne**.

Wykonaj następujące kroki w toocreate Portal dla instytucji rządowych hello zaplanowanego tworzenia kopii zapasowej hello.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

Kopię zapasową można utworzyć ręcznie w dowolnym momencie. Procedur można przejść za[ręczne tworzenie kopii zapasowej](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Konfigurowanie nowego konta magazynu dla usługi hello
Jest to krok opcjonalny tooperform konieczne tylko wtedy, gdy nie włączono hello automatyczne tworzenie konta magazynu z usługą. Konto magazynu Microsoft Azure jest wymagany toocreate kontenera woluminów StorSimple.

Jeśli potrzebujesz konta magazynu Azure w innym regionie toocreate, zobacz [o kontach magazynu Azure](../storage/common/storage-create-storage-account.md) instrukcje krok po kroku.

Wykonaj następujące kroki w hello Portal dla instytucji rządowych na powitania hello **usługi Menedżer StorSimple** strony.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Użyj konsoli szeregowej urządzenia toohello tooconnect programu PuTTY
tooWindows tooconnect programu PowerShell dla StorSimple, należy toouse oprogramowania emulacji terminala, takiego jak PuTTY. Programu PuTTY można używać, gdy uzyskujesz dostęp do urządzenia hello bezpośrednio za pośrednictwem konsoli szeregowej hello lub przez otwarcie sesji telnet z komputera zdalnego.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Wyszukiwanie aktualizacji i ich stosowanie
Aktualizowanie urządzenia może potrwać kilka godzin. Powitania po tooscan kroki do wykonania i stosowania aktualizacji na urządzeniu.

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a>tooupdate urządzenia
1. Na urządzeniu hello **Szybki Start** kliknij przycisk **urządzeń**. Wybierz urządzenie fizyczne hello, kliknij przycisk **konserwacji** , a następnie kliknij przycisk **Wyszukaj aktualizacje**.  
2. Utworzono tooscan zadania dostępne aktualizacje. Jeśli aktualizacje są dostępne, hello **Wyszukaj aktualizacje** zmiany zbyt**Zainstaluj aktualizacje**. Kliknij pozycję **Zainstaluj aktualizacje**.
3. Zostanie utworzone zadanie aktualizacji. Monitorowanie stanu hello aktualizacji przechodząc zbyt**zadania**.
   
   > [!NOTE]
   > Po uruchomieniu zadania aktualizacji hello natychmiast wyświetla stan hello 50 procentach. Stan Hello zmienia too100 procent dopiero po zakończeniu zadania aktualizacji hello. Brak stanu nie jest w czasie rzeczywistym hello procesu aktualizacji.
   > 
   > 
4. Po pomyślnym zaktualizowaniu urządzenia hello, Włącz interfejsy sieciowe dane 2 i dane 3, jeśli zostały one wyłączone.

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Pobierz hello IQN hosta z systemem Windows Server
Wykonaj następujące kroki tooget hello iSCSI hello kwalifikowana nazwa (IQN) hosta z systemem Windows z systemem Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Ręczne tworzenie kopii zapasowej
Wykonaj następujące kroki w hello Portal dla instytucji rządowych toocreate na żądanie ręczne kopię zapasową pojedynczego woluminu w urządzeniu StorSimple hello.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a>Konfigurowanie wielościeżkowego wejścia/wyjścia (MPIO)
Wielościeżkowe wejście/wyjście (MPIO) jest funkcją opcjonalną i nie jest instalowane domyślnie w systemie Windows Server. Powinno być instalowane jako funkcja za pomocą Menedżera serwera. Instrukcje instalacji wielościeżkowego wejścia/wyjścia, przejdź zbyt[konfigurowanie wielościeżkowego wejścia/wyjścia dla urządzenia StorSimple](storsimple-configure-mpio-windows-server.md).

Instrukcje instalacji wielościeżkowego wejścia/wyjścia dla urządzenia StorSimple podłączonego tooa hosta systemu Linux, przejdź zbyt[konfigurowanie wielościeżkowego wejścia/wyjścia dla hosta z systemem Linux](storsimple-configure-mpio-on-linux.md).

> [!NOTE]
> Wielościeżkowe wejście/wyjście nie jest obsługiwana na urządzeniu wirtualnym StorSimple na platformie Azure.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Skonfiguruj [urządzenie wirtualne](storsimple-virtual-device-u2.md).
* Użyj hello [usługi Menedżer StorSimple](storsimple-manager-service-administration.md) toomanage urządzenia StorSimple.

