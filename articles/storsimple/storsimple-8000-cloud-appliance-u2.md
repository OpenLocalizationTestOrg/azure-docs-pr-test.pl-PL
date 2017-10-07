---
title: "aaaStorSimple chmury urządzenia Update 3 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, wdrażania i zarządzania urządzenia chmury StorSimple, w sieci wirtualnej Microsoft Azure. (Dotyczy tooStorSimple aktualizacji 3 lub nowszym)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: ba60a629f1f4b8f0d4566eeb45bae8696f50d0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-cloud-appliance-in-azure-update-3-and-later"></a>Wdrażanie urządzenia StorSimple w chmurze oraz zarządzanie nim na platformie Azure (aktualizacja Update 3 i nowsze)

## <a name="overview"></a>Omówienie

Witaj StorSimple 8000 serii chmury urządzenia jest zapewnia dodatkową funkcję dołączoną do rozwiązania Microsoft Azure StorSimple. Witaj urządzenia chmury StorSimple działa na maszynie wirtualnej w sieci wirtualnej Microsoft Azure i umożliwia tooback się oraz klonowania danych z hostów.

W tym artykule opisano toodeploy krok po kroku proces hello i zarządzaj nimi urządzenia chmury StorSimple na platformie Azure. Zapoznanie się z tym artykułem umożliwi:

* Dowiedz się, jak urządzenia chmury hello różni się od urządzenia fizycznego hello.
* Toocreate może być i skonfiguruj hello urządzenia chmury.
* Podłącz urządzenia chmury toohello.
* Dowiedz się, jak toowork z hello chmury urządzenia.

Ten samouczek dotyczy hello tooall urządzenia chmury StorSimple z aktualizacją Update 3 i nowszych.

#### <a name="cloud-appliance-model-comparison"></a>Porównanie modeli urządzeń w chmurze

Hello urządzenia chmury StorSimple jest dostępny w dwóch modeli standardowy — 8010 (wcześniej znane jako hello 1100) oraz Premium — 8020 (wprowadzony w wersji Update 2). Hello w poniższej tabeli przedstawiono porównanie hello dwa modele.

| Model urządzenia | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Maksymalna pojemność** |30 TB |64 TB |
| **Maszyna wirtualna platformy Azure** |Standard_A3 (4 rdzenie, 7 GB pamięci)| Standard_DS3 (4 rdzenie, 14 GB pamięci)|
| **Dostępność w danym regionie** |Wszystkie regiony platformy Azure |Regiony świadczenia usługi Azure obsługujące usługę Premium Storage i maszyny wirtualne DS3 platformy Azure<br></br>Użyj [tej listy](https://azure.microsoft.com/regions/services/) toosee, jeśli obie **maszyny wirtualnej > serii DS** i **magazynu > dysku magazynu** są dostępne w danym regionie. |
| **Typ magazynu** |Używa usługi Azure Standard Storage dla dysków lokalnych<br></br> Dowiedz się, jak za[Utwórz konto magazynu w warstwie standardowa](../storage/common/storage-create-storage-account.md) |Używa usługi Azure Premium Storage dla dysków lokalnych<sup>2</sup> <br></br>Dowiedz się, jak za[tworzenia konta Premium Storage](../storage/common/storage-premium-storage.md) |
| **Wskazówki dotyczące obciążenia** |Pobieranie plików z kopii zapasowych na poziomie elementu |Scenariusze tworzenia i testowania w chmurze <br></br>Obciążenia o małych opóźnieniach i większej wydajności<br></br>Urządzenie pomocnicze do odzyskiwania po awarii |

<sup>1</sup> *wcześniej zwany hello 1100*.

<sup>2</sup> *zarówno hello 8010 i 8020 używać usługi Azure Standard Storage dla hello chmury warstwy. hello różnica istnieje tylko w warstwie lokalnej hello urządzenia hello*.

## <a name="how-hello-cloud-appliance-differs-from-hello-physical-device"></a>Jak urządzenia chmury hello różni się od urządzenia fizycznego hello

Witaj urządzenia chmury StorSimple jest wyłącznie programowym wersji StorSimple działającą w jednym węźle maszyny wirtualnej w programie Microsoft Azure. urządzenia chmury Hello obsługuje scenariusze odzyskiwania po awarii, w których urządzenie fizyczne nie jest dostępna. urządzenia chmury Hello jest odpowiednie do użycia w poziomie elementu pobierania z kopii zapasowych, lokalnego odzyskiwania po awarii i scenariusze tworzenia i testowania chmury.

#### <a name="differences-from-hello-physical-device"></a>Różnice z urządzenia fizycznego hello

Witaj poniższej tabeli przedstawiono niektóre podstawowe różnice między hello urządzenia chmury StorSimple i hello urządzenia fizycznego StorSimple.

|  | Urządzenie fizyczne | Urządzenie w chmurze |
| --- | --- | --- |
| **Lokalizacja** |Znajduje się w centrum danych hello. |Działa w systemie Azure. |
| **Interfejsy sieciowe** |Ma sześć interfejsów sieciowych: DANE 0 do DANE 5. |Ma tylko jeden interfejs sieciowy: DANE 0. |
| **Rejestracja** |Podczas kroku konfiguracji początkowej hello zarejestrowane. |Rejestracja jest osobnym zadaniem. |
| **Klucz szyfrowania danych usługi** |Wygeneruj ponownie na urządzeniu fizycznym hello, a następnie zaktualizuj urządzenia chmury hello z hello nowego klucza. |Nie można ponownie wygenerować z urządzenia do chmury hello. |
| **Obsługiwane typy woluminów** |Obsługiwane są zarówno woluminy przypięte lokalnie, jak i woluminy warstwowe. |Obsługiwane są tylko woluminy warstwowe. |

## <a name="prerequisites-for-hello-cloud-appliance"></a>Wymagania wstępne dotyczące hello urządzenia chmury

Hello następujące sekcje opisano wymagania wstępne dotyczące hello konfiguracji dla urządzenia StorSimple w chmurze. Przed wdrożeniem urządzenia chmury, przejrzyj hello uwagi dotyczące zabezpieczeń przy użyciu urządzenia chmury.

[!INCLUDE [StorSimple Cloud Appliance security](../../includes/storsimple-8000-cloud-appliance-security.md)]

#### <a name="azure-requirements"></a>Wymagania systemu Azure

Przed udostępnieniem urządzenia chmury hello należy hello toomake następujące czynności przygotowawcze w środowisku platformy Azure:

* Upewnij się, że masz urządzenie fizyczne StorSimple z serii 8000 (model 8100 lub 8600) wdrożone i działające w centrum danych. Zarejestruj to urządzenie z hello tej samej usługi Menedżer StorSimple urządzenia, które będą toocreate a StorSimple urządzenia chmury dla.
* Dla urządzenia chmury hello [Skonfiguruj sieć wirtualną na platformie Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). W przypadku korzystania z usługi Premium Storage należy utworzyć sieć wirtualną w regionie platformy Azure obsługującym tę usługę. regiony usługi Premium Storage Hello są regionów, które odpowiadają toohello wiersza dla magazynu danych na dysku w hello [listę regionów platformy Azure](https://azure.microsoft.com/regions/services/).
* Zaleca się, że używasz hello domyślnego serwera DNS zapewnionego w systemie Azure zamiast określania z własnej nazwy serwera DNS. Jeśli nazwa serwera DNS jest nieprawidłowy lub hello serwer DNS nie jest możliwe tooresolve adresy IP poprawnie hello tworzenia urządzenia chmury hello kończy się niepowodzeniem.
* Sieci typu punkt do lokacji i lokacja do lokacji są opcjonalne. W razie potrzeby można skonfigurować te opcje dla bardziej zaawansowanych scenariuszy.
* Można utworzyć [maszyny wirtualne Azure](../virtual-machines/virtual-machines-windows-quick-create-portal.md) (Serwery hosta) w sieci wirtualnej hello używanego hello woluminów udostępnionych przez hello urządzenia chmury. Te serwery muszą spełniać następujące wymagania hello:

  * Muszą być maszynami wirtualnymi z systemem Windows lub Linux z zainstalowanym oprogramowaniem iSCSI Initiator.
  * Należy uruchomić na powitania tej samej sieci wirtualnej jako urządzenia chmury hello.
  * Być może tooconnect toohello obiektem docelowym iSCSI urządzenia chmury hello za pośrednictwem hello wewnętrzny adres IP urządzenia chmury hello.
  * Upewnij się, że skonfigurowano obsługę dla inicjatora iSCSI i chmury ruchu na powitania sam sieci wirtualnej.

#### <a name="storsimple-requirements"></a>Wymagania dotyczące urządzenia StorSimple

Wprowadź hello następujące usługi Menedżer StorSimple urządzenia tooyour aktualizacje, przed utworzeniem urządzenia chmury:

* Dodaj [rekordy kontroli dostępu](storsimple-8000-manage-acrs.md) hello w maszynach wirtualnych znajdujących się na serwery hosta hello toobe będzie dla urządzenia chmury.
* Użyj [konta magazynu](storsimple-8000-manage-storage-accounts.md#add-a-storage-account) w hello tego samego regionu hello urządzenia chmury. Jeśli konta usługi Storage są w różnych regionach, wydajność może zostać obniżona. Możesz korzystać z urządzenia do chmury hello konta Standard lub Premium Storage. Więcej informacji na temat toocreate [konta Standard Storage](../storage/common/storage-create-storage-account.md) lub [konta Premium Storage](../storage/common/storage-premium-storage.md)
* Użyj innego konta magazynu do utworzenia urządzenia chmury z hello używane jako dane. Przy użyciu powitalne tego samego konta magazynu może spowodować obniżenie wydajności.

Upewnij się, że masz hello następujących informacji, aby rozpocząć:

* Konto witryny Azure Portal z poświadczeniami dostępu.
* Kopię klucza szyfrowania danych usługi powitania od urządzenia fizycznego zarejestrowano toohello usługę Menedżer urządzeń StorSimple.

## <a name="create-and-configure-hello-cloud-appliance"></a>Tworzenie i konfigurowanie urządzenia chmury hello

Przed wykonaniem tych procedur upewnij się, że zostały spełnione hello [wymagania wstępne dotyczące urządzenia chmury hello](#prerequisites-for-the-cloud-appliance).

Wykonaj następujące kroki toocreate urządzenia chmury StorSimple hello.

### <a name="step-1-create-a-cloud-appliance"></a>Krok 1. Tworzenie urządzenia w chmurze

Wykonaj następujące kroki toocreate hello urządzenia chmury StorSimple hello.

[!INCLUDE [Create a cloud appliance](../../includes/storsimple-8000-create-cloud-appliance-u2.md)]

Jeśli tworzenie hello urządzenia chmury hello nie powiedzie się w tym kroku, nie może mieć toohello połączenie internetowe. Aby uzyskać więcej informacji, przejdź zbyt[Rozwiązywanie problemów z połączeniami Internet](#troubleshoot-internet-connectivity-errors) podczas tworzenia urządzenia chmury.

### <a name="step-2-configure-and-register-hello-cloud-appliance"></a>Krok 2: Konfigurowanie i rejestrowanie urządzenia chmury hello

Przed rozpoczęciem tej procedury upewnij się, że masz kopię klucza szyfrowania danych usługi hello. klucz szyfrowania danych usługi Hello jest tworzony podczas rejestrowania pierwszego urządzenia fizycznego StorSimple z hello usługi Menedżer StorSimple urządzenia. Zostały instrukcją toosave go w bezpiecznym miejscu. Jeśli nie masz kopię klucza szyfrowania danych usługi hello, musi skontaktować się Microsoft Support, aby uzyskać pomoc.

Wykonaj następujące kroki tooconfigure hello i rejestrowanie urządzenia StorSimple w chmurze.

[!INCLUDE [Configure and register a cloud appliance](../../includes/storsimple-8000-configure-register-cloud-appliance.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Krok 3: Ustawienia konfiguracji dla urządzeń hello modyfikowanie (opcjonalnie)

Witaj poniższej sekcji opisano ustawienia konfiguracji dla urządzeń hello potrzebnych dla hello urządzenia chmury StorSimple, jeśli chcesz toouse protokołu CHAP, StorSimple Snapshot Manager lub zmień hasło administratora urządzenia hello.

#### <a name="configure-hello-chap-initiator"></a>Konfigurowanie inicjatora protokołu CHAP hello

Ten parametr zawiera poświadczenia hello, które urządzenia chmury (docelowy) oczekuje od inicjatorów hello (serwerów), które próbujesz tooaccess hello woluminów. Inicjatory Hello Podaj nazwę użytkownika protokołu CHAP i tooidentify hasło protokołu CHAP się tooyour urządzenia podczas tego uwierzytelniania. Aby uzyskać szczegółowy opis kroków, przejdź zbyt[Konfigurowanie protokołu CHAP dla urządzenia](storsimple-8000-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Konfigurowanie obiektu docelowego protokołu CHAP hello

Ten parametr zawiera poświadczenia hello, używane przez urządzenia chmury, gdy inicjator z włączonym protokołem CHAP żąda uwierzytelniania wzajemnego lub dwukierunkowego. Urządzenia chmury używa nazwy użytkownika wstecznego protokołu CHAP i wstecznego protokołu CHAP tooidentify hasła sam toohello inicjatora podczas tego procesu uwierzytelniania.

> [!NOTE]
> Ustawienia obiektu docelowego protokołu CHAP są ustawieniami globalnymi. Te ustawienia są stosowane, wszystkie woluminy hello podłączony uwierzytelniania protokołu CHAP użycia urządzenia toohello w chmurze.

Aby uzyskać szczegółowy opis kroków, przejdź zbyt[Konfigurowanie protokołu CHAP dla urządzenia](storsimple-8000-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Skonfiguruj hasło programu StorSimple Snapshot Manager hello

Oprogramowanie StorSimple Snapshot Manager znajduje się na hoście z systemem Windows i pozwala administratorom tworzenie kopii zapasowych toomanage urządzenia StorSimple w formie hello lokalne i migawki w chmurze.

> [!NOTE]
> Dla urządzenia chmury hello host systemu Windows jest maszyny wirtualnej platformy Azure.

Podczas konfigurowania urządzenia w hello StorSimple Snapshot Manager, zostanie wyświetlony monit tooprovide hello StorSimple urządzenia IP adresów i haseł tooauthenticate urządzenia magazynującego. Aby uzyskać szczegółowy opis kroków, przejdź zbyt[hasło skonfigurować StorSimple Snapshot Manager](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Hasło administratora urządzenia hello zmiany

Gdy używasz tooaccess interfejsu programu Windows PowerShell hello hello urządzenia chmury, są wymagane tooenter hasło administratora urządzenia. Przed użyciem urządzenia chmury hello hello zabezpieczeń danych, należy zmienić to hasło. Aby uzyskać szczegółowy opis kroków, przejdź zbyt[hasło administratora urządzenia Konfiguruj](../storsimple/storsimple-8000-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-cloud-appliance"></a>Połączyć się zdalnie toohello urządzenia chmury

Urządzenia chmury tooyour dostępu zdalnego za pośrednictwem interfejsu programu Windows PowerShell hello nie jest domyślnie włączona. Należy włączyć zdalne zarządzanie na urządzenia chmury hello najpierw, a następnie na powitania klienta używane urządzenia chmury hello tooaccess.

Hello dwuetapowej procedury w tym artykule opisano sposób tooconnect zdalnie tooyour chmury urządzenia.

### <a name="step-1-configure-remote-management"></a>Krok 1: Konfigurowanie zdalnego zarządzania

Wykonaj następujące kroki tooconfigure zdalnego zarządzania dla urządzenia StorSimple w chmurze hello.

[!INCLUDE [Configure remote management via HTTP for cloud appliance](../../includes/storsimple-8000-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-cloud-appliance"></a>Krok 2: Zdalny dostęp do urządzenia chmury hello

Po włączeniu zdalnego zarządzania na urządzeniu chmury hello, użyj programu Windows PowerShell remoting tooconnect toohello urządzenia z innej maszyny wirtualnej wewnątrz hello tej samej sieci wirtualnej. Na przykład można połączyć z hello hosta maszyny Wirtualnej został skonfigurowany i użyty tooconnect iSCSI. W większości wdrożeń otworzy hosta maszyny Wirtualnej, który służy do uzyskiwania dostępu do urządzenia chmury hello tooaccess publiczny punkt końcowy.

> [!WARNING]
> **Aby zwiększyć bezpieczeństwo zdecydowanie zaleca się używać protokołu HTTPS podczas nawiązywania połączenia toohello punktów końcowych, a następnie usunąć punkty końcowe powitania po zakończeniu sesji zdalnej programu PowerShell.**

Należy wykonać procedury hello w [dostępu zdalnego urządzenia StorSimple tooyour](storsimple-8000-remote-connect.md) tooset się komunikację zdalną dla urządzenia chmury.

## <a name="connect-directly-toohello-cloud-appliance"></a>Bezpośrednie połączenie toohello urządzenia chmury

Można także połączyć bezpośrednio toohello urządzenia chmury. tooconnect bezpośrednio toohello w chmurze, urządzenia z innego komputera spoza hello sieci wirtualnej lub hello poza środowiskiem Microsoft Azure, należy utworzyć dodatkowe punkty końcowe.

Wykonaj następujące kroki toocreate publiczny punkt końcowy na urządzeniu chmury hello hello.

[!INCLUDE [Create public endpoints on a cloud appliance](../../includes/storsimple-8000-create-public-endpoints-cloud-appliance.md)]

Zaleca się połączenia z innej maszyny wirtualnej znajdującej się hello sam wirtualnych sieci, ponieważ takie rozwiązanie zmniejsza hello liczbę publicznych punktów końcowych w sieci wirtualnej. W takim przypadku połączenie toohello maszyny wirtualnej za pośrednictwem sesji pulpitu zdalnego, a następnie skonfiguruj maszyny wirtualnej do użytku, jak w przypadku dowolnego klienta systemu Windows w sieci lokalnej. Nie ma potrzeby numeru portu publicznego hello tooappend, ponieważ hello port jest już znany.

## <a name="work-with-hello-storsimple-cloud-appliance"></a>Praca z hello urządzenia chmury StorSimple

Teraz zostanie utworzony i skonfigurowany hello urządzenia chmury StorSimple, wszystko jest gotowe toostart korzystania z niego. W urządzeniu w chmurze można pracować z kontenerami woluminów, woluminami i zasadami tworzenia kopii zapasowych tak samo jak w przypadku urządzenia fizycznego StorSimple. Witaj jedyna różnica polega na tym, że należy toomake urządzenia chmury hello należy wybrać z listy urządzeń. Odwołuje się zbyt[Użyj toomanage usługi Menedżer StorSimple urządzenia hello urządzenia chmury](storsimple-8000-manager-service-administration.md) dla procedury krok po kroku z hello zarządzania różnych zadań hello urządzenia chmury.

Witaj poniższych sekcjach omówiono niektóre różnice hello, które wystąpią podczas pracy z urządzenia do chmury hello.

### <a name="maintain-a-storsimple-cloud-appliance"></a>Konserwacja urządzenia StorSimple w chmurze

Ponieważ jest to urządzenie tylko do oprogramowania, obsługa urządzenia chmury hello jest minimalny, kiedy porównaniu toomaintenance hello urządzenia fizycznego.

Urządzenia w chmurze nie można aktualizować. Użyj hello najnowszą wersję oprogramowania toocreate nowego urządzenia chmury.


### <a name="storage-accounts-for-a-cloud-appliance"></a>Konta magazynu dla urządzenia w chmurze

Konta magazynu są przeznaczone do użytku przez hello usługi Menedżer urządzeń StorSimple, urządzenia chmury hello oraz hello urządzenia fizycznego. Podczas tworzenia kont magazynu, zaleca się użyć identyfikatora regionu w przyjaznej nazwie hello. Dzięki temu, upewnij się, że hello region jest spójny we wszystkich składników systemu hello. Urządzenia chmury, ważne jest, że wszystkie składniki hello znajdują się w hello problemy z wydajnością tooprevent tego samego regionu.

Procedury krok po kroku, przejdź zbyt[dodawania konta magazynu](storsimple-8000-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-cloud-appliance"></a>Dezaktywacja urządzenia StorSimple w chmurze

Po dezaktywacji urządzenia chmury hello akcja usuwa hello maszyny Wirtualnej i zasoby hello utworzone podczas inicjowania jej obsługi. Po dezaktywacji urządzenia chmury hello, nie można go przywrócić tooits poprzedniego stanu. Przed dezaktywacją urządzenia chmury hello, upewnij się, że toostop lub usunąć klientów i hosty, które od niego zależne.

Dezaktywacja urządzenia chmury wyniki hello następujące akcje:

* urządzenia chmury Hello jest usuwany.
* dysk Hello systemu operacyjnego i dyski danych utworzone dla urządzenia chmury hello są usuwane.
* Usługa hostowana Hello i sieć wirtualna utworzone podczas inicjowania obsługi zostaną zachowane. Jeśli nie są używane, należy je usunąć ręcznie.
* Migawki w chmurze utworzone dla urządzenia chmury hello są zachowywane.

Procedury krok po kroku, przejdź zbyt[Dezaktywuj i usuwanie urządzenia StorSimple](storsimple-8000-deactivate-and-delete-device.md).

Jak urządzenia chmury hello zostanie wyświetlone jako dezaktywowane na bloku usługi Menedżer StorSimple urządzenia hello, można usunąć urządzenia chmury hello z listy urządzeń na powitania **urządzeń** bloku.

### <a name="start-stop-and-restart-a-cloud-appliance"></a>Uruchamianie, zatrzymywanie i ponowne uruchamianie urządzenia w chmurze
W odróżnieniu od urządzenia fizycznego StorSimple hello nie jest zasilany zasilania poza przycisk toopush na urządzeniu z StorSimple w chmurze. Jednak może być zmieniana, gdzie należy toostop i ponowne uruchomienie urządzenia chmury hello.

Witaj najprościej można toostart, Zatrzymaj i ponownie uruchom urządzenia chmury odbywa się za pośrednictwem hello bloku usługi maszyn wirtualnych. Przejdź hello maszyny wirtualnej usługi. Z listy hello maszyn wirtualnych zidentyfikować hello wirtualna odpowiedniego urządzenia chmury tooyour (nazwę), a następnie kliknij przycisk hello nazwę maszyny Wirtualnej. Po wyświetleniu z bloku maszyny wirtualnej jest stan urządzenia cloud hello **systemem** ponieważ jest uruchamiane domyślnie po jego utworzeniu. Można uruchomić, zatrzymać i ponownie uruchomić maszynę wirtualną w dowolnym momencie.

[!INCLUDE [Stop and restart cloud appliance](../../includes/storsimple-8000-stop-restart-cloud-appliance.md)]

### <a name="reset-toofactory-defaults"></a>Resetuj toofactory domyślne
Jeśli zdecydujesz się mają toostart za pośrednictwem z urządzenia do chmury, Dezaktywuj i usuń go, a następnie utwórz nowy.

## <a name="fail-over-toohello-cloud-appliance"></a>Tryb failover toohello urządzenia chmury
Odzyskiwania awaryjnego (DR) jest jednym z hello kluczowych scenariuszy, które hello urządzenia chmury StorSimple zostało zaprojektowane na potrzeby. W tym scenariuszu hello urządzenie fizyczne StorSimple lub całe centrum danych mogą nie być dostępne. Na szczęście można użyć operacji toorestore urządzenia w innej lokalizacji. Podczas odzyskiwania po awarii hello kontenery woluminów z urządzenia źródłowego hello zmienić własności i zostały przeniesione toohello urządzenia chmury.

wymagania wstępne Hello do odzyskiwania po awarii są:

* urządzenia chmury Hello zostało utworzone i skonfigurowane.
* Wszystkie woluminy hello w ramach kontenera woluminów hello są w trybie offline.
* kontener woluminów Hello, który przejścia w tryb failover, ma skojarzoną migawkę w chmurze.

> [!NOTE]
> * Korzystając z urządzenia chmury jako hello urządzenie pomocnicze do odzyskiwania po awarii, należy pamiętać, że hello 8010 ma 30 TB pamięci standardowej, a 8020 ma 64 TB magazyn w warstwie Premium. urządzenia chmury 8020 wyższa wydajność Hello może być bardziej odpowiednie do scenariusza odzyskiwania po awarii.

Procedury krok po kroku, przejdź zbyt[awaryjnie urządzenia chmury tooa](storsimple-8000-device-failover-cloud-appliance.md).

## <a name="delete-hello-cloud-appliance"></a>Usuwanie urządzenia chmury hello
Jeśli wcześniej skonfigurowane i używane urządzenia chmury StorSimple, ale teraz ma toostop Naliczanie opłat za obliczenia na swój, musisz zatrzymać hello urządzenia chmury. Trwa zatrzymywanie urządzenia chmury hello cofa alokację hello maszyny Wirtualnej. Po wykonaniu tej akcji opłaty związane z subskrypcją nie będą naliczane. jednak będą nadal Hello opłaty za magazyn dla hello systemu operacyjnego i dysków z danymi.

toostop, który hello wszystkich opłat, należy usunąć urządzenia chmury hello. toodelete hello kopii zapasowych utworzonych przez urządzenia chmury hello można dezaktywować lub usunąć hello urządzenia. Aby uzyskać więcej informacji, zobacz temat [Deactivate and delete a StorSimple device](storsimple-8000-deactivate-and-delete-device.md) (Dezaktywacja i usuwanie urządzenia StorSimple).

[!INCLUDE [Delete a cloud appliance](../../includes/storsimple-8000-delete-cloud-appliance.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Rozwiązywanie problemów z błędami łączności internetowej
Podczas tworzenia hello urządzenia chmury, jeśli nie istnieje żadne toohello połączenie internetowe, hello tworzenia krok zakończy się niepowodzeniem. tootroubleshoot awarie połączenia z Internetu, wykonaj następujące kroki w portalu Azure hello hello:

1. [Utwórz maszynę wirtualną systemu Windows Server 2012 na platformie Azure](/articles/virtual-machines/windows/quick-create-portal.md). Należy używać tej maszyny wirtualnej hello tego samego konta magazynu, sieci wirtualnej i podsieci, jak używany przez urządzenia z chmury. Jeśli istnieje hello hosta serwera systemu Windows Azure przy użyciu tego samego konta magazynu, sieci i podsieci, również umożliwia połączenie z Internetem hello tootroubleshoot.
2. Zdalne Zaloguj się do maszyny wirtualnej hello utworzonej w hello poprzedzających krok.
3. Otwórz okno polecenia wewnątrz maszyny wirtualnej hello (Win + R, a następnie wpisz `cmd`).
4. Uruchom następujące polecenia w wierszu hello hello.

    `nslookup windows.net`
5. Jeśli `nslookup` ulegnie awarii łączności z Internetem uniemożliwia urządzenia chmury hello rejestrowaniu toohello usługi Menedżer urządzeń StorSimple.
6. Zmiany hello wymagane jest tooyour tooensure sieci wirtualnej, która hello urządzenia chmury stanie tooaccess witryn Azure takich jak _windows.net_.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[Użyj toomanage usługi Menedżer StorSimple urządzenia hello urządzenia chmury](storsimple-8000-manager-service-administration.md).
* Zrozumienie sposobu zbyt[przywracania woluminu StorSimple z zestawu kopii zapasowych](storsimple-8000-restore-from-backup-set-u2.md).
