---
title: "urządzenie aaaInstall Microsoft Azure StorSimple 8100 | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toounpack, montowanie i Podłączanie kabli do urządzenia StorSimple 8100, aby wdrożyć i skonfigurować oprogramowanie hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6098a01e-c031-488a-a8d7-0b607ce665e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 76b94e57318b6c25dc3333ae73edc9e4752b7d1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8100-device"></a>Rozpakowywanie, w stojaku, a Podłączanie kabli do urządzenia StorSimple 8100
## <a name="overview"></a>Omówienie
Do urządzenia 8100 Microsoft Azure StorSimple jest obudowa pojedynczego urządzenia montowane w stojaku. W tym samouczku wyjaśniono, jak toounpack, zamontować w stojaku i podłączyć kable hello StorSimple 8100 urządzeń sprzętowych przed Konfigurowanie i wdrażanie urządzenia StorSimple hello.

## <a name="unpack-your-storsimple-8100-device"></a>Rozpakuj do urządzenia StorSimple 8100
Witaj poniższych krokach przedstawiono Wyczyść, szczegółowe instrukcje dotyczące toounpack urządzenia magazynującego StorSimple 8100. To urządzenie jest dostarczany w jednym polu.

### <a name="prepare-toounpack-your-device"></a>Przygotowanie toounpack urządzenia
Przed Rozpakuj urządzenia, przejrzyj hello następujących informacji.

![Ikona ostrzeżenia](./media/storsimple-safety/IC740879.png)![ikona ciężki](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png) **ostrzeżenie!**

1. Upewnij się, że jest dwóch osób toomanage dostępne hello wagę hello obudowy, jeśli są obsługuje go ręcznie. Obudowa pełni skonfigurowany można porównać się too32 kg (70 kg).
2. Umieść pole hello na powierzchni płaskiej, poziomu.

Następnie wykonaj następujące kroki toounpack hello urządzenia.

#### <a name="toounpack-your-device"></a>toounpack urządzenia
1. Sprawdź, czy pole hello i piana pakietów hello crushes, części, szkody limitu górnego lub widocznego uszkodzenia. Jeśli pole hello lub pakowania poważnie jest uszkodzony, nie otwieraj okno hello. Sprawdź [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) toohelp należy ocenić, czy urządzenie hello jest w dobrym stanie.
2. Rozpakuj hello pole. następujące obraz powitania przedstawiono hello rozpakowane urządzenia StorSimple.
   
     ![Rozpakuj urządzenia magazynu](./media/storsimple-8100-hardware-installation/HCSUnpackyour2Udevice.png)
   
    **Wczytaj widoku urządzenia pamięci masowej**
   
   | Etykieta | Opis |
   | --- | --- |
   |   1 |Pole pakowania |
   |   2 |Pianki dołu |
   |   3 |Urządzenie |
   |   4 |Górny pianki |
   |   5 |Pole akcesoriów |
3. Po rozpakowywania pole hello, upewnij się, że masz:
   
   * 1 urządzenie jednej obudowie
   * 2 przewodów zasilania
   * 1 skrzyżowanego kabla Ethernet
   * 2 kable konsoli szeregowej
   * Konwerter USB seryjny 1 dostęp szeregowy
   * 1 śrubokręt T10 odporne
   * 4 QSFP-do-kart SFP + do użytku z interfejsami sieciowymi Ethernet 10
   * 1 w stojaku kit (2 po stronie szyny z instalowanie sprzętu)
   * Pobieranie rozpoczęte dokumentacji
     
     Jeśli nie masz żadnego z elementów hello wymienionych powyżej, [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md).

Witaj, następnym krokiem jest toorack instalacji urządzenia.

## <a name="rack-mount-your-storsimple-8100-device"></a>W stojaku do urządzenia StorSimple 8100
Wykonaj hello dalej kroki tooinstall urządzenia magazynującego StorSimple 8100 w stojaku standardowe 19 cala z przodu i tylnej wpisów. urządzenie Hello StorSimple 8100 ma jednej obudowie podstawowego.

Instalacja Hello składa się z wielu kroków, z których każdy jest omówione w hello zgodnie z procedurami.

> [!IMPORTANT]
> Urządzenia StorSimple musi być montowane w stojaku do prawidłowego działania.
> 
> 

### <a name="prepare-hello-site"></a>Przygotowanie hello lokacji
Witaj urządzenie musi być zainstalowane w standardowe stojak cala 19, który ma przodu oraz tylnej wpisów. Użyj powitania po tooprepare procedury instalacji stojaku.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>tooprepare hello lokacji stojak instalacji
1. Upewnij się, że urządzenie hello bezpiecznie opiera się na prosty, stabilny i poziomu pracy powierzchni (lub podobny).
2. Sprawdź, czy hello lokacji, której zamierzasz tooset zapasowej ma standardowe zasilacza z niezależne źródło lub stojak jednostki dystrybucji zasilania (PDU) z awaryjny dostarczania (UPS).
3. Upewnij się, że gniazdo jeden 2U jest dostępna w stojaku hello, w którym planujesz toomount hello urządzenia.

![Ikona ostrzeżenia](./media/storsimple-safety/IC740879.png)![ikona ciężki](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png) **ostrzeżenie!**

Upewnij się, że jest dwóch osób toomanage dostępne hello wagi, jeśli Instalator urządzenia hello są Obsługa ręcznie. Obudowa pełni skonfigurowany można porównać się too32 kg (70 kg).

### <a name="rack-prerequisites"></a>Wymagania wstępne w stojaku
Obudowa 8100 Hello jest przeznaczony do instalacji w stojaku standard CAL 19 cabinet z:

* Minimalna głębokość 27.84 cali w stojaku po toopost.
* Maksymalna waga 32 kg hello urządzenia
* Maksymalnego wykorzystania wstecz Pascal 5 (miernika wody 0,5 mm).

### <a name="rack-mounting-rail-kit"></a>Stojakach kolei kit
Instalowanie szyny zestaw jest przeznaczony dla hello stojak 19 cala w pliku cabinet. szyny Hello zostały przetestowane toohandle hello maksymalną obudowa wagi. Te szyny będzie również umożliwiać instalacji wielu obudowach bez utraty miejsca w stojaku hello.

#### <a name="tooinstall-hello-device-on-hello-rails"></a>urządzenie hello tooinstall na powitania szyny
1. Wykonaj ten krok tylko wtedy, gdy wewnętrzny szyny nie są zainstalowane na urządzeniu. Zazwyczaj szyny wewnętrzny hello są instalowane na powitania fabryki. Jeśli szyny nie są zainstalowane, następnie zainstalować hello slajdów kolei po lewej i prawej kolei toohello strony hello obudowa obudowy. Dołącz ich przy użyciu sześciu śruby metryki na każdej stronie. toohelp orientacji, kolei hello slajdów są oznaczone **LH — przodu** i **RH — przodu**, a końcem ma zakończenia hello, który jest dołączony tyłu hello hello załącznika.<br/>
   
    ![Podstawa montażowa tooenclosure slajdów kolei dołączenia](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)

    **Strony toohello obudowa hello slajdów dołączenia kolei wewnętrzny**
   
    Etykieta | Opis
    ----- | -----------
    1     | M 3 x 4 śruby head przycisku
    2     | Podstawa montażowa slajdów

2. Dołącz zewnętrzne kolei po lewej stronie powitania i zewnętrzne po prawej stronie zestawy toohello stojak cabinet pionowy elementów członkowskich. zaznaczono nawiasy Hello **LH**, **RH**, i **ta strona w górę** tooguide za pośrednictwem hello poprawisz orientacji.
3. Znajdź numery PIN kolei hello na powitania przodu i do tyłu hello kolei zestawu. Rozszerzanie hello kolei toofit między hello stojak wpisów i Wstaw hello numerów PIN do przodu hello i luk element pionowy w stojaku tylnej post. Pamiętaj, że zestaw kolei hello jest poziom.
4. Użyj dwóch członków hello podane metryki śruby toosecure hello kolei zestawu toohello stojak pionowy. Użyj jednej śrubie na wierzch hello i jeden tyłu hello.
5. Powtórz te kroki dla hello innych kolei zestawu.<br/>
   
     ![Dołączenia toorack slajdów kolei cabinet](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Dołączanie stojak toohello zestawy kolei zewnętrzne**
   
   | Etykieta | Opis |
   | --- | --- |
   |   1 |Ładunku gwintowanym |
   |   2 |Gwintowanym post stojak front przerw kwadratowe |
   |   3 |Numery PIN front lokalizacji kolei po lewej stronie |
   |   4 |Ładunku gwintowanym |
   |   5 |Numery PIN tylnej lokalizacji kolei po lewej stronie |

### <a name="mounting-hello-device-in-hello-rack"></a>Instalowanie urządzenia hello w stojaku hello
Za pomocą hello stojaku, które właśnie zostały zainstalowane, wykonaj następujące kroki toomount hello urządzenia w stojaku hello hello.

#### <a name="toomount-hello-device"></a>toomount hello urządzenia
1. Z Asystentem Podnieś obudowa hello i wyrównanie go z hello stojaku.
2. Starannie Włóż hello urządzenia do szyny hello, a następnie Wypchnij urządzenia hello całkowicie w stojaku hello cabinet.<br/>
   
    ![Wstawianie w stojaku hello urządzenia](./media/storsimple-8100-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Instalowanie urządzenia hello w stojaku hello**
3. Usuń hello lewej i prawej front kołnierza włączony klawisz caps ściąganie caps hello wolne. caps kołnierza powitania po prostu przyciąganie na powitania kołnierze.
4. Zabezpiecz obudowa hello w stojaku hello instalując co podane gwintowanym Phillips head za pośrednictwem każdej kołnierza, lewy i prawy.
5. Zainstaluj caps kołnierza hello naciskając je w miejscu i przyciąganie ich w miejscu.<br/>
   
     ![Instalowanie kołnierza CAP](./media/storsimple-8100-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Instalowanie hello kołnierza CAP**
   
   | Etykieta | Opis |
   | --- | --- |
   |   1 |Obudowa gwintowanym zaczepienia |

Witaj, następnym krokiem jest toocable Twojego urządzenia pod kątem zasilania, sieci i dostęp szeregowy.

## <a name="cable-your-storsimple-8100-device"></a>Podłączanie kabli do urządzenia StorSimple 8100
Witaj poniższe procedury wyjaśniają, jak toocable do zasilania, sieci i połączenia szeregowego urządzenia StorSimple 8100.

### <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem powitalne okablowania urządzenia, będą potrzebne:

* Urządzenie magazynujące, całkowicie rozpakowane i stojaku.
* 2 kable zasilania, które są dołączone do urządzenia
* Dostęp too2 jednostki dystrybucji zasilania (zalecane).
* Kable sieciowe
* Podany kable szeregowe
* Szeregowego USB konwertera z odpowiedni sterownik hello zainstalowane na komputerze (w razie potrzeby)
* Podany 4 QSFP-do-kart SFP + do użytku z interfejsami sieciowymi Ethernet 10
* [Sprzętu obsługiwanego przez hello 10 GbE interfejsy na urządzeniu StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="power-cabling"></a>Okablowanie zasilania
Urządzenie zawiera nadmiarowe zasilania i chłodzenia modułów (PCMs). Zarówno PCMs muszą być zainstalowane i połączone toodifferent power źródeł tooensure wysokiej dostępności.

Wykonaj następujące kroki toocable hello urządzenia zasilania.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

### <a name="network-cabling"></a>Okablowanie sieci
Urządzenie jest Konfiguracja aktywnego gotowości: w dowolnym momencie, jeden moduł kontrolera jest aktywna i przetwarzanie wszystkich operacji dysku i sieci podczas hello inny moduł kontrolera przechodzi w stan wstrzymania. W przypadku niepowodzenia kontrolera kontrolera rezerwy hello jest aktywowany bezpośrednio i kontynuuje wszystkie operacje hello dysku i sieci.

toosupport tej pracy awaryjnej nadmiarowych kontrolera, należy toocable urządzenia sieciowe zgodnie z opisem w hello następujące kroki.

#### <a name="toocable-for-network-connection"></a>toocable dla połączenia sieciowego
1. Urządzenie ma sześć interfejsów sieciowych na każdym kontrolerze: cztery 1 GB/s i dwa 10 GB/s Ethernet portów. Zidentyfikuj hello danych różne porty na płyty montażowej hello urządzenia.
   
    ![Płyty montażowej urządzenia 8100](./media/storsimple-8100-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Powrót z urządzenia hello przedstawiający porty danych**
   
   | Etykieta | Opis |
   | --- | --- |
   |   0,1,4,5 |Interfejsy sieciowe Ethernet 1 |
   |   2,3 |Interfejsy sieciowe Ethernet 10 |
   |   6 |Porty szeregowe |
2. Zobacz powitania po diagram okablowanie sieci. (Konfiguracja minimalna sieci hello znajduje się pełny liniami niebieski. Dodatkowe czynności konfiguracyjne wymagane wysokiej dostępności i wydajności znajduje się za pomocą linii kropkowanej).

    ![Podłączanie kabli do urządzenia 2U sieci](./media/storsimple-8100-hardware-installation/HCSCableYour2UDeviceforNetwork.png)

    **Okablowania urządzenia sieciowego**

   |Etykieta | Opis |
   |----- | ----------- |
   | A    | Sieć LAN z dostępem do Internetu |
   | B    | Kontrolera 0 |
   | C    | PCM 0 |
   | D    | Kontrolera 1 |
   | E    | PCM 1 |
   | F, G | Hosts |
   | 0-5  | Interfejsy sieciowe |



W przypadku okablowania hello urządzenia, wymaga minimalnej konfiguracji hello:

* Co najmniej dwa interfejsy sieciowe podłączone na każdym kontrolerze, aby uzyskać dostęp z chmury i jeden dla interfejsu iSCSI. Witaj dane 0 portu jest automatycznie włączona i skonfigurowana za pośrednictwem konsoli szeregowej hello hello urządzenia. Oprócz dane 0 innego portu danych musi toobe skonfigurowana za pośrednictwem hello klasycznego portalu Azure. W takim przypadku połączyć dane 0 portu toohello głównej LAN (sieci z dostępem do Internetu). Witaj innych danych, które porty mogą być połączone segment sieci LAN (VLAN) tooSAN/iSCSI hello sieci, w zależności od roli hello przeznaczone.
* Identyczne interfejsów w każdej toohello kontrolera połączony sam sieciowa tooensure dostępność, jeśli do pracy awaryjnej kontrolera. Na przykład jeśli wybierzesz tooconnect dane 0, a dane 3 dla jednego z kontrolerów hello należy hello tooconnect odpowiednie dane 0 i dane 3 na hello inny kontroler.

Należy pamiętać o wysokiej dostępności i wydajność:

* Jeśli to możliwe, należy skonfigurować parę interfejsu sieciowego, aby uzyskać dostęp do chmury (1 GbE) i inną parę dla interfejsu iSCSI (10 GbE zalecana) na każdym kontrolerze.
* Jeśli to możliwe, należy połączyć interfejsów sieciowych z każdego kontrolera tootwo różnych przełączników tooensure dostępności awariami przełącznika. Witaj rysunku przedstawiono Witaj dwie 10 GbE interfejsy sieciowe dane 2 i dane 3 z każdego kontrolera połączone tootwo różnych przełączników.

Aby uzyskać więcej informacji, zobacz toohello **interfejsy sieciowe** w obszarze hello [wymagania dotyczące wysokiej dostępności dla urządzenia StorSimple](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Jeśli używasz nadawczo-odbiorczych SFP + z interfejsów sieciowych 10 GbE, użyj hello podane QSFP-SFP + kart. Aby uzyskać więcej informacji, przejdź zbyt[obsługiwanym sprzęcie interfejsów sieciowych GbE hello 10 na urządzeniu StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Okablowanie portu szeregowego
Wykonaj następujące kroki toocable hello portu szeregowego.

#### <a name="toocable-for-serial-connection"></a>toocable dla połączenia szeregowego
1. Urządzenie ma portu szeregowego na każdym kontrolerze, który jest identyfikowany przez ikona klucza. Zobacz ilustracji toohello w hello [okablowanie sieci](#network-cabling) sekcji toolocate hello portów szeregowych płyty montażowej hello urządzenia.
2. Zidentyfikuj kontroler active hello na płyty montażowej Twoje urządzenie. Migający LED niebieski wskazuje, że ten kontroler hello jest aktywny.
3. Przy użyciu hello podane kable szeregowe (w razie potrzeby hello szeregowego USB konwerter dla komputera przenośnego), a Uzyskuj dostęp do konsoli lub komputerze z (urządzenie toohello emulacji terminala) toohello portu szeregowego hello active kontrolera.
4. Zainstaluj sterowniki USB seryjny hello (dostarczane z urządzeniem hello) na komputerze.
5. Skonfiguruj połączenie szeregowe hello w następujący sposób: 115 200 transmisji, 8 bitów danych 1 bit zatrzymania, bez parzystości i sterowanie przepływem ustawić tooNone.
6. Zweryfikować hello połączenia, naciskając klawisz Enter na powitania konsoli. Menu konsoli szeregowej powinny być wyświetlane.

> [!NOTE]
> **Zarządzania lights-Out**: gdy urządzenie hello jest zainstalowane w zdalnym centrum danych lub w pokoju komputera o ograniczonym dostępie, upewnij się, że hello połączenia szeregowego tooboth kontrolery są zawsze połączone tooa konsoli szeregowej przełącznika lub podobnego sprzętu. Dzięki temu poza pasmem zdalnego sterowania i pomocy technicznej operacje przypadku zakłócenia w sieci lub nieoczekiwanych awarii.
> 
> 

Urządzenie jest teraz kablem zasilania, dostępu do sieci i połączenie szeregowe. Witaj, następnym krokiem jest tooconfigure hello oprogramowania i wdrażania urządzenia.

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak za[wdrażania i konfigurowania lokalnego urządzenia StorSimple](storsimple-deployment-walkthrough-u2.md).

