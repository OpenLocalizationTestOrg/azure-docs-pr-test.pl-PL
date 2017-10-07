---
title: "Urządzenie wirtualne aaaStorSimple Update 2 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, wdrażania i zarządzania urządzenia wirtualnego StorSimple w sieci wirtualnej Microsoft Azure. (Dotyczy tooStorSimple Update 2)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: f37752a5-cd0c-479b-bef2-ac2c724bcc37
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.openlocfilehash: 8d2a0520f1ed30ebec929c2bdabb4838691b8ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-virtual-device-in-azure"></a>Wdrażanie urządzenia wirtualnego StorSimple oraz zarządzanie nim na platformie Azure
## <a name="overview"></a>Omówienie
Urządzenie wirtualne serii StorSimple 8000 Hello jest zapewnia dodatkową funkcję dołączoną do rozwiązania Microsoft Azure StorSimple. Urządzenie wirtualne StorSimple Hello działa na maszynie wirtualnej w sieci wirtualnej Microsoft Azure i umożliwia tooback się oraz klonowania danych z hostów. Ten przewodnik opisuje sposób toodeploy zarządzania urządzeniem wirtualnym na platformie Azure i jest stosowane tooall hello urządzeń wirtualnych z oprogramowaniem w wersji Update 2 i niżej.

#### <a name="virtual-device-model-comparison"></a>Porównanie modeli urządzenia wirtualnego
Witaj StorSimple, urządzenie wirtualne jest dostępny w dwóch modeli standardowy — 8010 (wcześniej znane jako hello 1100) oraz Premium — 8020 (wprowadzony w wersji Update 2). Porównanie dwóch modeli hello jest przedstawione w poniższej tabeli.

| Model urządzenia | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Maksymalna pojemność** |30 TB |64 TB |
| **Maszyna wirtualna platformy Azure** |Standard_A3 (4 rdzenie, 7 GB pamięci) |Standard_DS3 (4 rdzenie, 14 GB pamięci) |
| **Zgodność wersji** |Wersje przed wprowadzeniem aktualizacji Update 2 lub nowsze |Wersje z aktualizacją Update 2 lub nowsze |
| **Dostępność w danym regionie** |Wszystkie regiony platformy Azure |Wszystkie regiony świadczenia usługi Azure obsługujące usługę Premium Storage i maszyny wirtualne DS3 platformy Azure<br></br> Użyj [tej listy](https://azure.microsoft.com/en-us/regions/services) toosee, jeśli obie *maszyny wirtualnej > serii DS* i *magazynu > dysku magazynu* są dostępne w danym regionie. |
| **Typ magazynu** |Używa usługi Azure Standard Storage dla dysków lokalnych<br></br> Dowiedz się, jak za[Utwórz konto magazynu w warstwie standardowa](../storage/common/storage-create-storage-account.md) |Używa usługi Azure Premium Storage dla dysków lokalnych<sup>2</sup> <br></br>Dowiedz się, jak za[tworzenia konta Premium Storage](../storage/common/storage-premium-storage.md) |
| **Wskazówki dotyczące obciążenia** |Pobieranie plików z kopii zapasowych na poziomie elementu |Tworzenie chmur i scenariusze testowania, krótki czas oczekiwania, bardziej wydajne obciążenia <br></br>Urządzenie pomocnicze do odzyskiwania po awarii |

<sup>1</sup> *wcześniej zwany hello 1100*.

<sup>2</sup> *zarówno hello 8010 i 8020 używać usługi Azure Standard Storage dla hello chmury warstwy. hello różnica istnieje tylko w warstwie lokalnej hello urządzenia hello*.

W tym artykule opisano krok po kroku proces hello wdrażania urządzenia wirtualnego StorSimple na platformie Azure. Zapoznanie się z tym artykułem umożliwi:

* Dowiedz się, jak hello urządzenie wirtualne różni się od urządzenia fizycznego hello.
* Toocreate może być i skonfiguruj hello urządzenia wirtualnego.
* Podłącz urządzenie wirtualne toohello.
* Dowiedz się, jak toowork z urządzeniem wirtualnym hello.

Ten samouczek dotyczy tooall hello urządzeń wirtualnych StorSimple aktualizacją Update 2 i wyższych.

## <a name="how-hello-virtual-device-differs-from-hello-physical-device"></a>Czym urządzenie wirtualne hello różni się od urządzenia fizycznego hello
Urządzenie wirtualne StorSimple Hello jest wyłącznie programowym wersji StorSimple działającą w jednym węźle maszyny wirtualnej w programie Microsoft Azure. Hello urządzenie wirtualne obsługuje scenariuszach odzyskiwania po awarii w których urządzenia fizycznego nie jest dostępna, jest odpowiednie do użycia w poziomie elementu pobierania z kopii zapasowych, lokalnego odzyskiwania po awarii i deweloperów chmury i testowania scenariuszy.

#### <a name="differences-from-hello-physical-device"></a>Różnice z urządzenia fizycznego hello
Witaj poniższej tabeli przedstawiono niektóre podstawowe różnice między hello urządzenia wirtualnego StorSimple oraz urządzenia fizycznego StorSimple hello.

|  | Urządzenie fizyczne | Urządzenie wirtualne |
| --- | --- | --- |
| **Lokalizacja** |Znajduje się w centrum danych hello. |Działa w systemie Azure. |
| **Interfejsy sieciowe** |Ma sześć interfejsów sieciowych: DANE 0 do DANE 5. |Ma tylko jeden interfejs sieciowy: DANE 0. |
| **Rejestracja** |Podczas konfigurowania hello zarejestrowane. |Rejestracja jest osobnym zadaniem. |
| **Klucz szyfrowania danych usługi** |Wygeneruj ponownie na urządzeniu fizycznym hello, a następnie zaktualizuj hello urządzenia wirtualnego z hello nowego klucza. |Nie można ponownie wygenerować z urządzenia wirtualnego hello. |

## <a name="prerequisites-for-hello-virtual-device"></a>Wymagania wstępne dotyczące urządzeń wirtualnych hello
Witaj poniższe sekcje zawierają opis wymagań wstępnych dotyczących urządzenia wirtualnego StorSimple hello konfiguracji. Wcześniejsze toodeploying urządzenie wirtualne, przejrzyj hello [zagadnienia dotyczące zabezpieczeń podczas używania urządzenia wirtualnego](storsimple-security.md#storsimple-virtual-device-security).

#### <a name="azure-requirements"></a>Wymagania systemu Azure
Przed udostępnieniem hello urządzenia wirtualnego należy hello toomake następujące czynności przygotowawcze w środowisku platformy Azure:

* Dla urządzenia wirtualnego hello [Skonfiguruj sieć wirtualną na platformie Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). W przypadku korzystania z usługi Premium Storage należy utworzyć sieć wirtualną w regionie platformy Azure obsługującym tę usługę. regionów usługi Magazyn w warstwie Premium Hello są regionów, które odpowiadają wiersz toohello *dysku magazynu* liście hello [regionów platformy Azure](https://azure.microsoft.com/en-us/regions/services).
* Jest wskazane toouse hello domyślnego serwera DNS zapewnionego w systemie Azure zamiast określania z własnej nazwy serwera DNS. Jeśli nazwa serwera DNS jest nieprawidłowy lub hello serwer DNS nie jest możliwe tooresolve adresy IP poprawnie hello tworzenie urządzenia wirtualnego hello zakończy się niepowodzeniem.
* Sieci typu punkt do lokacji i lokacja do lokacji są opcjonalne. W razie potrzeby można skonfigurować te opcje dla bardziej zaawansowanych scenariuszy.
* Można utworzyć [maszyny wirtualne Azure](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Serwery hosta) w sieci wirtualnej hello używanego hello woluminów udostępnionych przez urządzenie wirtualne hello. Te serwery muszą spełniać następujące wymagania hello:                             

  * Muszą być maszynami wirtualnymi z systemem Windows lub Linux z zainstalowanym oprogramowaniem iSCSI Initiator.
  * Należy uruchomić na powitania tej samej sieci wirtualnej co urządzenie wirtualne hello.
  * Być może tooconnect toohello obiektem docelowym iSCSI urządzenia wirtualnego hello za pośrednictwem hello wewnętrzny adres IP urządzenia wirtualnego hello.
* Upewnij się, że skonfigurowano obsługę dla inicjatora iSCSI i chmury ruchu na powitania sam sieci wirtualnej.

#### <a name="storsimple-requirements"></a>Wymagania dotyczące urządzenia StorSimple
Wprowadź hello następujące usługi Azure StorSimple tooyour aktualizacji przed utworzeniem urządzenia wirtualnego:

* Dodaj [rekordy kontroli dostępu](storsimple-manage-acrs.md) dla hello maszyn wirtualnych, które mają toobe Serwery hosta dla urządzenia wirtualnego.
* Użyj [konta magazynu](storsimple-manage-storage-accounts.md#add-a-storage-account) hello — w tym samym regionie co urządzenie wirtualne hello. Jeśli konta usługi Storage są w różnych regionach, wydajność może zostać obniżona. Możesz korzystać z urządzenia wirtualnego hello konta Standard lub Premium Storage. Więcej informacji na temat toocreate [konta Standard Storage](../storage/common/storage-create-storage-account.md) lub [konta Premium Storage](../storage/common/storage-premium-storage.md)
* Użyj innego konta magazynu do utworzenia urządzenia wirtualnego z hello używane jako dane. Przy użyciu powitalne tego samego konta magazynu może spowodować obniżenie wydajności.

Upewnij się, że masz hello następujących informacji, aby rozpocząć:

* Konto klasycznego portalu Azure z poświadczeniami dostępu.
* Kopia klucza szyfrowania danych usługi powitania od urządzenia fizycznego.

## <a name="create-and-configure-hello-virtual-device"></a>Tworzenie i konfigurowanie urządzenia wirtualnego hello
Przed wykonaniem tych procedur upewnij się, że zostały spełnione hello [wymagania wstępne dotyczące urządzeń wirtualnych hello](#prerequisites-for-the-virtual-device).

Po utworzeniu sieci wirtualnej, skonfigurować usługi Menedżer StorSimple i zarejestrowane urządzenia fizycznego StorSimple w usłudze hello, można użyć hello następujące kroki toocreate i konfigurowanie urządzenia wirtualnego StorSimple.

### <a name="step-1-create-a-virtual-device"></a>Krok 1. Tworzenie urządzenia wirtualnego
Wykonaj hello następującego urządzenia wirtualnego StorSimple hello toocreate czynności.

[!INCLUDE [Create a virtual device](../../includes/storsimple-create-virtual-device-u2.md)]

Jeśli tworzenie urządzenia wirtualnego hello hello nie powiedzie się w tym kroku, nie może mieć toohello połączenie internetowe. Aby uzyskać więcej informacji, przejdź zbyt[Rozwiązywanie problemów z połączeniami Internet](#troubleshoot-internet-connectivity-errors) podczas tworzenia urządzenia wirtualnego.

### <a name="step-2-configure-and-register-hello-virtual-device"></a>Krok 2: Konfigurowanie i rejestrowanie urządzenia wirtualnego hello
Przed rozpoczęciem tej procedury upewnij się, że masz kopię klucza szyfrowania danych usługi hello. Witaj klucza szyfrowania danych usługi został utworzony, gdy skonfigurowano pierwszego urządzenia StorSimple i zostały instrukcją toosave go w bezpiecznym miejscu. Jeśli nie masz kopię klucza szyfrowania danych usługi hello, musi skontaktować się Microsoft Support, aby uzyskać pomoc.

Wykonaj następujące kroki tooconfigure hello i zarejestrować urządzenie wirtualne StorSimple.

[!INCLUDE [Configure and register a virtual device](../../includes/storsimple-configure-register-virtual-device.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Krok 3: Ustawienia konfiguracji dla urządzeń hello modyfikowanie (opcjonalnie)
Witaj poniższej sekcji opisano ustawienia konfiguracji dla urządzeń hello potrzebne do urządzenia wirtualnego StorSimple hello toouse protokołu CHAP, StorSimple Snapshot Manager lub zmienić hasło administratora urządzenia hello.

#### <a name="configure-hello-chap-initiator"></a>Konfigurowanie inicjatora protokołu CHAP hello
Ten parametr zawiera poświadczenia hello, których urządzenie wirtualne (docelowy) oczekuje od inicjatorów hello (serwerów), które próbujesz tooaccess hello woluminów. Witaj inicjatory zapewnią nazwę użytkownika protokołu CHAP i tooidentify hasło protokołu CHAP się tooyour urządzenia podczas tego uwierzytelniania. Aby uzyskać szczegółowy opis kroków, przejdź zbyt[Konfigurowanie protokołu CHAP dla urządzenia](storsimple-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Konfigurowanie obiektu docelowego protokołu CHAP hello
Ten parametr zawiera poświadczenia hello, używane przez urządzenie wirtualne, gdy inicjator z włączonym protokołem CHAP żąda uwierzytelniania wzajemnego lub dwukierunkowego. Urządzenie wirtualne użyje nazwy użytkownika wstecznego protokołu CHAP i wstecznego protokołu CHAP tooidentify hasła sam toohello inicjatora podczas tego procesu uwierzytelniania. Należy pamiętać, że ustawienia obiektu docelowego protokołu CHAP są ustawieniami globalnymi. Gdy są stosowane, wszystkie hello woluminów połączonych toohello magazynu urządzenie wirtualne użyje uwierzytelniania protokołu CHAP. Aby uzyskać szczegółowy opis kroków, przejdź zbyt[Konfigurowanie protokołu CHAP dla urządzenia](storsimple-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Skonfiguruj hasło programu StorSimple Snapshot Manager hello
Oprogramowanie StorSimple Snapshot Manager znajduje się na hoście z systemem Windows i pozwala administratorom tworzenie kopii zapasowych toomanage urządzenia StorSimple w formie hello lokalne i migawki w chmurze.

> [!NOTE]
> Dla urządzenia wirtualnego hello hoście z systemem Windows jest maszyny wirtualnej platformy Azure.
>
>

Podczas konfigurowania urządzenia w hello StorSimple Snapshot Manager, zostanie wyświetlony monit tooprovide hello StorSimple urządzenia IP adresów i haseł tooauthenticate urządzenia magazynującego. Aby uzyskać szczegółowy opis kroków, przejdź zbyt[hasło skonfigurować StorSimple Snapshot Manager](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Hasło administratora urządzenia hello zmiany
Gdy używasz tooaccess interfejsu programu Windows PowerShell hello hello urządzenia wirtualnego, dzięki czemu tooenter wymagane hasło administratora urządzenia. Dla bezpieczeństwa hello danych, są wymagane toochange to hasło przed użyciem urządzenia wirtualnego hello. Aby uzyskać szczegółowy opis kroków, przejdź zbyt[hasło administratora urządzenia Konfiguruj](storsimple-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-virtual-device"></a>Połączyć się zdalnie toohello urządzenia wirtualnego
Urządzenie wirtualne tooyour dostępu zdalnego za pośrednictwem interfejsu programu Windows PowerShell hello nie jest domyślnie włączona. Należy najpierw tooenable zdalne zarządzanie na powitania urządzenia wirtualnego, a następnie go włączać na powitania klienta, które będzie używane tooaccess urządzenia wirtualnego.

Witaj dwuetapowy proces tooconnect zdalnie została szczegółowo opisana poniżej.

### <a name="step-1-configure-remote-management"></a>Krok 1: Konfigurowanie zdalnego zarządzania
Wykonaj następujące kroki tooconfigure zdalnego zarządzania dla urządzenia wirtualnego StorSimple hello.

[!INCLUDE [Configure remote management via HTTP for virtual device](../../includes/storsimple-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-virtual-device"></a>Krok 2: Zdalny dostęp do urządzenia wirtualnego hello
Po włączeniu zdalnego zarządzania na stronie konfiguracji urządzenia StorSimple hello, można użyć programu Windows PowerShell remoting tooconnect toohello urządzenie wirtualne z innej maszyny wirtualnej wewnątrz hello tej samej sieci wirtualnej; na przykład można połączyć z hello hosta maszyny Wirtualnej został skonfigurowany i użyty tooconnect iSCSI. W większości wdrożeń będzie już otwarto tooaccess publiczny punkt końcowy hosta maszyny Wirtualnej, która służy do uzyskiwania dostępu do urządzenia wirtualnego hello.

> [!WARNING]
> **Aby zwiększyć bezpieczeństwo zdecydowanie zaleca się używać protokołu HTTPS podczas nawiązywania połączenia toohello punktów końcowych, a następnie usunąć punkty końcowe powitania po zakończeniu sesji zdalnej programu PowerShell.**
>
>

Należy wykonać procedury hello w [dostępu zdalnego urządzenia StorSimple tooyour](storsimple-remote-connect.md) tooset się komunikację zdalną dla urządzenia wirtualnego.

## <a name="connect-directly-toohello-virtual-device"></a>Bezpośrednie połączenie toohello urządzenia wirtualnego
Można także połączyć bezpośrednio toohello urządzenia wirtualnego. Jeśli chcesz tooconnect bezpośrednio toohello urządzenie wirtualne z innego komputera spoza sieci wirtualnej hello lub poza środowiskiem Microsoft Azure hello należy toocreate dodatkowe punkty końcowe, zgodnie z opisem w hello procedury.

Wykonaj następujące kroki toocreate publiczny punkt końcowy na urządzeniu wirtualnym hello hello.

[!INCLUDE [Create public endpoints on a virtual device](../../includes/storsimple-create-public-endpoints-virtual-device.md)]

Zaleca się połączenia z innej maszyny wirtualnej znajdującej się hello sam wirtualnych sieci, ponieważ takie rozwiązanie zmniejsza hello liczbę publicznych punktów końcowych w sieci wirtualnej. Użycia tej metody, wystarczy podłączyć toohello maszyny wirtualnej za pośrednictwem sesji pulpitu zdalnego, a następnie skonfigurować maszynę wirtualną do użytku, jak w przypadku dowolnego klienta systemu Windows w sieci lokalnej. Nie ma potrzeby numeru portu publicznego hello tooappend, ponieważ hello port będzie już znany.

## <a name="work-with-hello-storsimple-virtual-device"></a>Praca z hello urządzenia wirtualnego StorSimple
Zostanie utworzony i skonfigurowany hello urządzenia wirtualnego StorSimple, jesteś gotowy toostart korzystania z niego. Możesz pracować z kontenerami woluminów, woluminów i zasad tworzenia kopii zapasowych na urządzenie wirtualne tak samo jak na urządzeniu fizycznym StorSimple; Witaj jedyna różnica polega na tym, że należy toomake hello urządzenia wirtualnego należy wybrać z listy urządzeń. Odwołuje się zbyt[toomanage usługi Menedżer StorSimple hello urządzenia wirtualnego użyj](storsimple-manager-service-administration.md) dla procedury krok po kroku z hello zarządzania różnych zadań hello urządzenia wirtualnego.

Witaj poniższych sekcjach omówiono niektóre różnice hello, które można napotkać podczas pracy z urządzeniem wirtualnym hello.

### <a name="maintain-a-storsimple-virtual-device"></a>Obsługa urządzenia wirtualnego StorSimple
Ponieważ jest wyłącznie programowym urządzenia, obsługa urządzenia wirtualnego hello jest minimalny, kiedy porównaniu toomaintenance hello urządzenia fizycznego. Masz hello następujące opcje:

* **Aktualizacje oprogramowania** — można wyświetlić datę hello oprogramowania hello ostatniej aktualizacji, oraz wszystkie komunikaty o stanie aktualizacji. Można użyć hello **skanowanie aktualizacji** przycisk u dołu hello tooperform strony hello ręcznie, jeśli chcesz toocheck nowe aktualizacje. Jeśli są dostępne aktualizacje, kliknij przycisk **Zainstaluj aktualizacje** tooinstall. Ponieważ hello urządzenie wirtualne jest tylko jeden interfejs, oznacza to, że będą niewielkie przerw stosowania aktualizacji. Urządzenie wirtualne Hello będzie zamknięcia i ponownego uruchomienia (w razie potrzeby) tooapply wszelkie aktualizacje, które zostały wydane. Procedury krok po kroku, przejdź zbyt[zaktualizować urządzenie](storsimple-update-device.md#install-regular-updates-via-the-azure-classic-portal).
* **Pakiet obsługi** — można utworzyć i przekazywania toohelp pakiet pomocy technicznej firmy Microsoft Support Rozwiązywanie problemów z urządzeniem wirtualnym. Procedury krok po kroku, przejdź zbyt[tworzenie i zarządzanie nimi pakietu obsługi](storsimple-create-manage-support-package.md).

### <a name="storage-accounts-for-a-virtual-device"></a>Konta magazynu dla urządzeń wirtualnych
Konta magazynu są przeznaczone do użytku przez usługi Menedżer StorSimple hello, hello urządzenie wirtualne oraz urządzenie fizyczne hello. Podczas tworzenia kont magazynu, zalecane jest użycie region hello region jest spójny we wszystkich składników systemu hello upewnij się, identyfikator w hello toohelp przyjazną nazwę. Dla urządzenia wirtualnego jest ważne, że wszystkie hello składniki należeć hello problemy z wydajnością tooprevent tego samego regionu.

Procedury krok po kroku, przejdź zbyt[dodawania konta magazynu](storsimple-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-virtual-device"></a>Dezaktywacja urządzenia wirtualnego StorSimple
Dezaktywacja urządzenia wirtualnego usuwa hello maszyny Wirtualnej i zasoby hello utworzone podczas inicjowania jej obsługi. Po dezaktywacji urządzenia wirtualnego hello, nie można go przywrócić tooits poprzedniego stanu. Przed dezaktywacją urządzenia wirtualnego hello, upewnij się, że toostop lub usunąć klientów i hosty, które od niego zależne.

Dezaktywacja urządzenia wirtualnego wyniki hello następujące akcje:

* Witaj urządzenie wirtualne zostanie usunięte.
* dysk Hello systemu operacyjnego i dyski danych utworzone dla urządzenia wirtualnego hello są usuwane.
* Usługa hostowana Hello i sieć wirtualna utworzone podczas inicjowania obsługi zostaną zachowane. Jeśli nie są używane, należy je usunąć ręcznie.
* Migawki w chmurze utworzone dla urządzenia wirtualnego hello są zachowywane.

Procedury krok po kroku, przejdź zbyt[Dezaktywuj i usuwanie urządzenia StorSimple](storsimple-deactivate-and-delete-device.md).

Jak hello urządzenie wirtualne zostanie wyświetlone jako dezaktywowane na stronie usługi Menedżer StorSimple hello, urządzenie wirtualne hello można usunąć z listy urządzeń na powitania **urządzeń** strony.

### <a name="start-stop-and-restart-a-virtual-device"></a>Uruchamianie, zatrzymywanie i ponowne uruchamianie urządzenia wirtualnego
W odróżnieniu od urządzenia fizycznego StorSimple hello nie jest zasilany włączania toopush przycisk na urządzeniu wirtualnym StorSimple zasilania. Jednak może być zmieniana, gdzie należy toostop i ponownie uruchomić urządzenie wirtualne hello. Na przykład niektóre aktualizacje mogą wymagać się, że ten hello maszyny Wirtualnej można ponownie uruchomić proces aktualizacji hello toofinish. Witaj najprościej można toostart, Zatrzymaj i ponownie uruchom urządzenie wirtualne jest hello toouse konsoli zarządzania maszynami wirtualnymi.

Po wyświetleniu hello konsoli zarządzania stanem urządzenia wirtualnego hello jest **systemem** ponieważ jest uruchamiane domyślnie po jego utworzeniu. Można uruchomić, zatrzymać i ponownie uruchomić maszynę wirtualną w dowolnym momencie.

[!INCLUDE [Stop and restart virtual device](../../includes/storsimple-stop-restart-virtual-device.md)]

### <a name="reset-toofactory-defaults"></a>Resetuj toofactory domyślne
Jeśli zdecydujesz, że chcesz toostart za pośrednictwem z urządzeniem wirtualnym, po prostu dezaktywować i usuń go, a następnie utwórz nową. Podobnie jak zresetowanie urządzenia fizycznego urządzenie wirtualne nie zostaną zainstalowane; jakiekolwiek aktualizacje Dlatego też należy upewnić się, że toocheck aktualizacji przed jego użyciem.

## <a name="fail-over-toohello-virtual-device"></a>Tryb failover toohello urządzenia wirtualnego
Odzyskiwania awaryjnego (DR) jest jednym z hello kluczowych scenariuszy, które hello StorSimple, urządzenie wirtualne zostało zaprojektowane na potrzeby. W tym scenariuszu hello urządzenie fizyczne StorSimple lub całe centrum danych mogą nie być dostępne. Na szczęście można użyć operacji toorestore urządzenie wirtualne w innej lokalizacji. Podczas odzyskiwania po awarii hello kontenery woluminów z urządzenia źródłowego hello zmienić własności i zostały przeniesione toohello urządzenia wirtualnego. Witaj wymagania wstępne dla odzyskiwania po awarii są hello urządzenia wirtualnego zostało utworzone i skonfigurowane, wszystkie woluminy hello w ramach kontenera woluminów hello został przełączony w tryb offline, czy hello kontener woluminów ma skojarzoną migawkę w chmurze.

> [!NOTE]
> * Podczas używania urządzenia wirtualnego jako urządzenia pomocniczego hello do odzyskiwania po awarii, należy pamiętać, że hello 8010 ma 30 TB pamięci standardowej, a 8020 ma 64 TB magazyn w warstwie Premium. Hello wyższa wydajność 8020 urządzenie wirtualne może być bardziej odpowiednie do scenariusza odzyskiwania po awarii.
> * Nie pracy awaryjnej lub klonować z poziomu urządzenia z zaktualizować 2 urządzenia tooa oprogramowaniem 1 przed aktualizacją. Możesz jednak w trybie Failover na urządzenie z systemem Update 2 tooa urządzenia z aktualizacją Update 1 (1.1 lub 1.2)
>
>

Procedury krok po kroku, przejdź zbyt[urządzenia wirtualnego tooa pracy awaryjnej](storsimple-device-failover-disaster-recovery.md#fail-over-to-a-storsimple-virtual-device).

## <a name="shut-down-or-delete-hello-virtual-device"></a>Wyłączanie lub usuwanie hello urządzenia wirtualnego
Jeśli został wcześniej skonfigurowany i użyty wirtualnego StorSimple urządzenia, ale teraz ma toostop Naliczanie opłat za obliczenia na swój, można zamknąć hello urządzenia wirtualnego. Zamykanie hello urządzenia wirtualnego nie powoduje usunięcia jego systemu operacyjnego ani dysków z danymi w magazynie. Powoduje ono zaprzestanie naliczania opłat przypadających na subskrypcję, ale nadal będzie opłaty za magazyn dla hello systemu operacyjnego i dysków z danymi.

Możesz usunąć lub wyłączyć urządzenie wirtualne hello będzie wyświetlany jako **Offline** na stronie urządzenia hello hello usługi Menedżer StorSimple. Można wybrać toodeactivate lub usunąć urządzenie hello, jeśli również toodelete hello kopie zapasowe utworzone przez urządzenie wirtualne hello. Aby uzyskać więcej informacji, zobacz temat [Deactivate and delete a StorSimple device](storsimple-deactivate-and-delete-device.md) (Dezaktywacja i usuwanie urządzenia StorSimple).

[!INCLUDE [Shut down a virtual device](../../includes/storsimple-shutdown-virtual-device.md)]

[!INCLUDE [Delete a virtual device](../../includes/storsimple-delete-virtual-device.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Rozwiązywanie problemów z błędami łączności internetowej
Podczas tworzenia hello urządzenia wirtualnego nie istnieje żadne toohello połączenie internetowe, kroku tworzenia hello zakończy się niepowodzeniem. tootroubleshoot w przypadku niepowodzenia hello ze względu na łączność z Internetem, wykonaj hello następujące kroki w hello klasycznego portalu Azure:

1. Utwórz maszynę wirtualną systemu Windows Server 2012 na platformie Azure. Należy używać tej maszyny wirtualnej hello tego samego konta magazynu, sieci i podsieci, jak używany przez urządzenie wirtualne. Jeśli masz już istniejącą hello hosta serwera systemu Windows Azure przy użyciu tego samego konta magazynu, sieci i podsieci, również umożliwia połączenie z Internetem hello tootroubleshoot.
2. Zdalne Zaloguj się do maszyny wirtualnej hello utworzonej w hello poprzedzających krok.
3. Otwórz okno polecenia wewnątrz maszyny wirtualnej hello (Win + R, a następnie wpisz `cmd`).
4. Uruchom następujące polecenia w wierszu hello hello.

    `nslookup windows.net`
5. Jeśli `nslookup` ulegnie awarii łączności z Internetem uniemożliwia rejestrowanie usługi Menedżer StorSimple toohello hello urządzenia wirtualnego.
6. Wprowadź zmiany hello wymagane tooyour tooensure sieci wirtualnej, która hello urządzenie wirtualne jest możliwe tooaccess Azure witrynach, takich jak "windows.net".

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[toomanage usługi Menedżer StorSimple hello urządzenia wirtualnego użyj](storsimple-manager-service-administration.md).
* Zrozumienie sposobu zbyt[przywracania woluminu StorSimple z zestawu kopii zapasowych](storsimple-restore-from-backup-set.md).
