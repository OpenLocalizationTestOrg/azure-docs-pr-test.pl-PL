---
title: "aaaDeploy urządzenia StorSimple (Update 1) | Dokumentacja firmy Microsoft"
description: "Opisuje hello kroki i najlepsze rozwiązania dotyczące wdrażania usług i urządzeń hello StorSimple Update 1."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ac631d3c-3c53-4c9e-9e4a-5c61c0cd8167
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 339b68f29a73bb77670e76e454cf271c7de4a6e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-1"></a>Wdrażanie lokalnego urządzenia StorSimple z aktualizacją Update 1
> [!div class="op_single_selector"]
> * [Aktualizacja 2](storsimple-deployment-walkthrough-u2.md)
> * [Aktualizacja 1](storsimple-deployment-walkthrough-u1.md)
> * [Wersja ogólnodostępna](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a>Omówienie
Zapraszamy wdrożenia urządzenia Azure StorSimple tooMicrosoft. Te samouczki wdrażania zastosować tooStorSimple 8000 Series Update 1.0. Tej serii samouczków opisano sposób tooconfigure urządzenia StorSimple i zawiera listę kontrolną, wymagania wstępne dotyczące konfiguracji i konfiguracja szczegółowe kroki.

Hello informacje w tych samouczkach założono, że zostały sprawdzone hello środki ostrożności i rozpakowane, wówczas i kablem urządzenia StorSimple. Jeśli nadal potrzebujesz tooperform tych zadań, należy rozpocząć od sprawdzenia hello [środki ostrożności](storsimple-safety.md). W zależności od modelu urządzenia można można następnie je rozpakować, zamontować w stojaku i podłączyć kable, wykonując następujące instrukcje hello:

* [Rozpakowywanie, montowanie w stojaku i podłączanie kabli do urządzenia 8100](storsimple-8100-hardware-installation.md)
* [Rozpakowywanie, montowanie w stojaku i podłączanie kabli do urządzenia 8600](storsimple-8600-hardware-installation.md)

Konieczne będzie administratora uprawnień toocomplete hello procesu instalacji i konfiguracji. Firma Microsoft zaleca przejrzenie listy kontrolnej konfiguracji hello przed rozpoczęciem. Hello wdrażania i konfiguracji może potrwać kilka toocomplete czas.

> [!NOTE]
> Witaj StorSimple informacje na temat wdrażania publikowane w witrynie sieci Web Microsoft Azure hello stosuje tooStorSimple 8000 serii tylko urządzenia. Aby uzyskać pełne informacje dotyczące urządzeń z serii hello 5000 i 7000, przejdź do: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Informacje wdrażania serii 5000 i 7000, zobacz hello [StorSimple systemu Przewodnik Szybki Start](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Kroki wdrażania
Wykonaj te czynności tooconfigure urządzenia StorSimple i podłącz go tooyour usługi Menedżer StorSimple. Ponadto toohello wymagane kroki, są opcjonalne kroki i procedury, których może być konieczne podczas wdrażania hello. instrukcje krok po kroku wdrażania Hello sygnalizującego, kiedy należy wykonać poszczególne kroki opcjonalne.

| Krok | Opis |
| --- | --- |
| **WYMAGANIA WSTĘPNE** |Te należy wykonać w ramach przygotowań do przyszłego wdrożenia hello toobe. |
| Lista kontrolna dotycząca konfiguracji wdrożenia. |Użyj tej listy kontrolnej toogather i rejestrowanie informacji przed tooand podczas wdrażania hello. |
| Wymagania wstępne dotyczące wdrożenia. |Te zweryfikować hello środowisko jest gotowe do wdrożenia. |
|  | |
| **WDROŻENIE KROK PO KROKU** |Te kroki są wymagane toodeploy urządzenia StorSimple w środowisku produkcyjnym. |
| Krok 1. Tworzenie nowej usługi. |Skonfiguruj magazyn i zarządzanie chmurą dla danego urządzenia StorSimple. Jeśli masz istniejącą usługę dla innych urządzeń StorSimple, pomiń ten krok. |
| Krok 2: Pobieranie klucza rejestracji usługi hello. |& Użyj tego klucza tooregister połączenia z usługą zarządzania hello urządzenia StorSimple. |
| Krok 3: Konfigurowanie i rejestrowanie urządzenia hello za pomocą programu Windows PowerShell dla urządzenia StorSimple. |Połącz hello urządzenia tooyour sieci i zarejestrowanie go za pomocą Instalatora hello Azure toocomplete przy użyciu usługi zarządzania hello. |
| Krok 4. Przeprowadzenie minimalnej konfiguracji urządzenia</br>Opcjonalnie: aktualizacja urządzenia StorSimple. |Użyj hello zarządzania usługi toocomplete hello ustawienia urządzenia i Włącz tooprovide magazynu. |
| Krok 5. Tworzenie kontenera woluminów. |Tworzenie kontenera woluminów tooprovision. Kontener woluminów obejmuje konta magazynu, przepustowości i ustawienia szyfrowania wszystkich woluminów hello zawarte w niej. |
| Krok 6. Tworzenie woluminu. |Zainicjuj obsługę woluminów magazynu na powitania urządzeniu StorSimple dla serwerów. |
| Krok 7. Instalowanie, inicjowanie i formatowanie woluminu.</br>Opcjonalnie: konfigurowanie wielościeżkowego wejścia/wyjścia (MPIO) |Połącz podany przez urządzenie hello magazynu iSCSI toohello serwerów. Możesz opcjonalnie skonfigurować wielościeżkowe wejście/wyjście tooensure, że serwery tolerują błędy linków, sieci i interfejsu. |
| Krok 8. Tworzenie kopii zapasowej. |Konfigurowanie sieci tooprotect zasad tworzenia kopii zapasowej danych |
|  | |
| **INNE PROCEDURY** |Procedury toothese toorefer może być konieczne podczas wdrażania rozwiązania. |
| Konfigurowanie nowego konta magazynu dla usługi hello. | |
| Użyj konsoli szeregowej urządzenia toohello PuTTY tooconnect. | |
| Pobierz hello IQN hosta z systemem Windows Server. | |
| Ręczne tworzenie kopii zapasowej. | |

## <a name="deployment-configuration-checklist"></a>Lista kontrolna dotycząca konfiguracji wdrożenia
powitania po Lista kontrolna dotycząca konfiguracji wdrożenia w tym artykule opisano informacje hello toocollect potrzebne przed i konfigurowanie oprogramowania hello na urządzeniu StorSimple. Niektóre z tych informacji wcześniejsze przygotowanie usprawni hello proces wdrażania urządzenia StorSimple hello w danym środowisku. Użyj tej listy kontrolnej uwagi tooalso niezbędnych szczegółów konfiguracji hello podczas wdrażania urządzenia.

| Etap | Parametr | Szczegóły | Wartości |
| --- | --- | --- | --- |
| **Podłączanie kabli do urządzenia** |Dostęp szeregowy |Początkowa konfiguracja urządzenia |Tak/Nie |
|  | | | |
| **Konfigurowanie i rejestrowanie urządzenia** |Ustawienia sieci interfejsu Dane 0 |Adres IP interfejsu Dane 0:</br>Maska podsieci:</br>Brama:</br>Podstawowy serwer DNS:</br>Podstawowy serwer NTP:</br>Adres IP/nazwa FQDN serwera proxy sieci Web (opcjonalnie):</br>Port serwera proxy sieci Web: | |
| &nbsp; |Hasło administratora urządzenia |Hasło musi zawierać od 8 do 15 znaków, w tym małe litery, wielkie litery, cyfry i znaki specjalne. | |
| &nbsp; |Hasło programu StorSimple Snapshot Manager |Hasło musi zawierać od 14 do 15 znaków, w tym małe litery, wielkie litery, cyfry i znaki specjalne. | |
| &nbsp; |Klucz rejestracji usługi |Ten klucz jest generowany na podstawie hello klasycznego portalu Azure. | |
| &nbsp; |Klucz szyfrowania danych usługi |Ten klucz jest tworzony podczas rejestrowania urządzenia hello z usługą zarządzania hello za pośrednictwem hello środowiska Windows PowerShell dla urządzenia StorSimple. Skopiuj ten klucz i zapisz go w bezpiecznym miejscu. | |
|  | | | |
| **Przeprowadzenie minimalnej konfiguracji urządzenia** |Przyjazna nazwa urządzenia |Jest to nazwę opisową hello urządzenia. | |
| &nbsp; |Strefa czasowa |Wszystkie zaplanowane operacje urządzenia będą wykonywane w ramach tej strefy czasowej. | |
| &nbsp; |Pomocniczy serwer DNS |To jest wymagana konfiguracja. | |
| &nbsp; |Interfejs sieciowy: stałe adresy IP kontrolera Dane 0 |Te adresy IP powinny być toohello obsługą routingu internetowego.</br>Stały adres IP kontrolera 0:</br>Stały adres IP kontrolera 1: | |
|  | | | |
| **Dodatkowe ustawienia interfejsu sieciowego** |Interfejs sieciowy: Dane 1</br>Jeśli włączono interfejs iSCSI, nie należy konfigurować hello bramy. |Cel: chmura/iSCSI/nie jest używany</br>Adres IP:</br>Maska podsieci:</br>Brama: | |
| &nbsp; |Interfejs sieciowy: Dane 2</br>Jeśli włączono interfejs iSCSI, nie należy konfigurować hello bramy. |Cel: chmura/iSCSI/nie jest używany</br>Adres IP:</br>Maska podsieci:</br>Brama: | |
| &nbsp; |Interfejs sieciowy: Dane 3</br>Jeśli włączono interfejs iSCSI, nie należy konfigurować hello bramy. |Cel: chmura/iSCSI/nie jest używany</br>Adres IP:</br>Maska podsieci:</br>Brama: | |
| &nbsp; |Interfejs sieciowy: Dane 4</br>Jeśli włączono interfejs iSCSI, nie należy konfigurować hello bramy. |Cel: chmura/iSCSI/nie jest używany</br>Adres IP:</br>Maska podsieci:</br>Brama: | |
| &nbsp; |Interfejs sieciowy: Dane 5</br>Jeśli włączono interfejs iSCSI, nie należy konfigurować hello bramy. |Cel: chmura/iSCSI/nie jest używany</br>Adres IP:</br>Maska podsieci:</br>Brama: | |
|  | | | |
| **Tworzenie kontenera woluminów** |Nazwa kontenera woluminów: |Nazwa kontenera hello | |
| &nbsp; |Konto magazynu Azure: |Magazyn kont dostępu i nazwa klucza tooassociate z tym kontenerem woluminu | |
| &nbsp; |Klucz szyfrowania magazynu w chmurze: |Klucz szyfrowania magazynu w poszczególnych kontenerach | |
|  | | | |
| **Tworzenie woluminu** |Szczegóły poszczególnych woluminów |Nazwa woluminu: | |
| &nbsp; |&nbsp; |Rozmiar: | |
| &nbsp; |&nbsp; |Typ użycia: | |
| &nbsp; |&nbsp; |Nazwa ACR: | |
| &nbsp; |&nbsp; |Domyślne zasady tworzenia kopii zapasowej: | |
|  | | | |
| **Instalowanie, inicjowanie i formatowanie woluminu** |Szczegóły poszczególnych serwerów hosta łączących toohello magazynu |Nazwa serwera Windows Server: | |
| &nbsp; |&nbsp; |Nazwa IQN serwera Windows Server: | |
| &nbsp; |&nbsp; |Nazwa woluminu z systemem Windows Server: | |
| &nbsp; |&nbsp; |Litera dysku/punkt instalacji systemu plików NTFS: | |

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

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> Jeśli nie włączono hello automatyczne tworzenie konta magazynu z usługą, konieczne będzie toocreate co najmniej jedno konto magazynu, po pomyślnym utworzeniu usługi. To konto magazynu będzie używane podczas tworzenia kontenera woluminu.
> 
> * Jeśli nie utworzono automatycznie konta magazynu, należy przejść za[Konfigurowanie nowego konta magazynu dla usługi hello](#configure-a-new-storage-account-for-the-service) szczegółowe informacje.
> * Jeśli włączono automatyczne tworzenie konta magazynu hello Przejdź zbyt[krok 2: Pobierz klucz rejestracji usługi hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Krok 2: Pobieranie klucza rejestracji usługi hello
Po skonfigurowaniu i uruchomieniu usługi Menedżer StorSimple hello należy klucz rejestracji usługi hello tooget. Ten klucz jest używane tooregister i połączenia z usługą hello urządzenia StorSimple.

Wykonaj następujące kroki w hello klasycznego portalu Azure hello.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Krok 3: Konfigurowanie i rejestrowanie urządzenia hello za pomocą programu Windows PowerShell dla urządzenia StorSimple
Użyj programu Windows PowerShell dla StorSimple toocomplete hello początkowej konfiguracji urządzenia StorSimple, zgodnie z objaśnieniem w hello procedury. Konieczne będzie toouse emulacji terminala oprogramowania toocomplete ten krok. Aby uzyskać więcej informacji, zobacz [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-u1](../../includes/storsimple-configure-and-register-device-u1.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Krok 4. Przeprowadzenie minimalnej konfiguracji urządzenia
Hello urządzenia minimalnej konfiguracji urządzenia StorSimple konieczne jest:

* Konfigurowanie hello pomocniczy serwer DNS.
* Włączenie usługi iSCSI na co najmniej jednym interfejsie sieciowym.
* Przypisanie stałych adresów IP kontrolerów hello tooboth.

Wykonaj następujące kroki w hello Azure classic portal toocomplete hello minimalnej konfiguracji urządzenia hello.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Krok 5. Tworzenie kontenera woluminów
Kontener woluminów obejmuje konta magazynu, przepustowości i ustawienia szyfrowania wszystkich woluminów hello zawarte w niej. Toocreate kontener woluminów należy przed zainicjowaniem woluminów na urządzeniu StorSimple.

Wykonaj następujące kroki w hello klasycznego portalu Azure toocreate kontenera woluminów hello.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Krok 6. Tworzenie woluminu
Po utworzeniu kontenera woluminów można udostępnić wolumin magazynu na urządzeniu StorSimple hello serwerów. Wykonaj następujące kroki w hello klasycznego portalu Azure toocreate woluminu hello.

> [!IMPORTANT]
> Menedżer StorSimple może tworzyć tylko woluminy alokowane elastycznie. Nie można tworzyć w pełni lub częściowo inicjowanych woluminów.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Krok 7. Instalowanie, inicjowanie i formatowanie woluminu
Witaj, wykonaj czynności są wykonywane na hoście z systemem Windows Server.

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

Wykonaj następujące kroki w hello klasycznego portalu Azure toocreate zaplanowanego tworzenia kopii zapasowej hello.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

Kopię zapasową można utworzyć ręcznie w dowolnym momencie. Procedur można przejść za[ręczne tworzenie kopii zapasowej](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Konfigurowanie nowego konta magazynu dla usługi hello
Jest to krok opcjonalny tooperform konieczne tylko wtedy, gdy nie włączono hello automatyczne tworzenie konta magazynu z usługą. Konto magazynu Microsoft Azure jest wymagany toocreate kontenera woluminów StorSimple.

Jeśli potrzebujesz konta magazynu Azure w innym regionie toocreate, zobacz [o kontach magazynu Azure](../storage/common/storage-create-storage-account.md) instrukcje krok po kroku.

Wykonaj następujące kroki w hello klasycznego portalu Azure na powitania hello **usługi Menedżer StorSimple** strony.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Użyj konsoli szeregowej urządzenia toohello tooconnect programu PuTTY
tooWindows tooconnect programu PowerShell dla StorSimple, należy toouse oprogramowania emulacji terminala, takiego jak PuTTY. Programu PuTTY można używać, gdy uzyskujesz dostęp do urządzenia hello bezpośrednio za pośrednictwem konsoli szeregowej hello lub przez otwarcie sesji telnet z komputera zdalnego.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Wyszukiwanie aktualizacji i ich stosowanie
Aktualizowanie urządzenia może potrwać kilka godzin. Powitania po tooscan kroki do wykonania i stosowania aktualizacji na urządzeniu.
<!--can take 1-4 hours-->

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

<!-- In step 2, you may be requested toodisable Data 2 and Data 3 prior tooinstalling hello updates. You must disable these network interfaces or hello updates may fail.-->

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Pobierz hello IQN hosta z systemem Windows Server
Wykonaj następujące kroki tooget hello iSCSI hello kwalifikowana nazwa (IQN) hosta z systemem Windows z systemem Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Ręczne tworzenie kopii zapasowej
Wykonaj następujące kroki w hello klasycznego portalu Azure toocreate na żądanie ręczne kopię zapasową pojedynczego woluminu w urządzeniu StorSimple hello.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="configure-mpio"></a>Konfigurowanie wielościeżkowego wejścia/wyjścia (MPIO)
Wielościeżkowe wejście/wyjście (MPIO) jest funkcją opcjonalną i nie jest instalowane domyślnie w systemie Windows Server. Powinno być instalowane jako funkcja za pomocą Menedżera serwera. Instrukcje instalacji wielościeżkowego wejścia/wyjścia, przejdź zbyt[konfigurowanie wielościeżkowego wejścia/wyjścia dla urządzenia StorSimple](storsimple-configure-mpio-windows-server.md).

Instrukcje instalacji wielościeżkowego wejścia/wyjścia dla urządzenia StorSimple podłączonego tooa hosta systemu Linux, przejdź zbyt[konfigurowanie wielościeżkowego wejścia/wyjścia dla hosta z systemem Linux](storsimple-configure-mpio-on-linux.md).

> [!NOTE]
> Wielościeżkowe wejście/wyjście (MPIO) nie jest obsługiwane na urządzeniu wirtualnym StorSimple.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Skonfiguruj [urządzenie wirtualne](storsimple-virtual-device-u2.md).
* Użyj hello [usługi Menedżer StorSimple](storsimple-manager-service-administration.md) toomanage urządzenia StorSimple.

