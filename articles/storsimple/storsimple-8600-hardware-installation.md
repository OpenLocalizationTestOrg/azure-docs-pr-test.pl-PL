---
title: "urządzenie aaaInstall Microsoft Azure StorSimple 8600 | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toounpack, montowanie i Podłączanie kabli do urządzenia StorSimple 8600, aby wdrożyć i skonfigurować oprogramowanie hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3d82ba5f-3e34-40dc-9c33-50f952bc6be8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/24/2016
ms.author: alkohli
ms.openlocfilehash: 0fc0ddf076725fededdde33a260b950b72edc8db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8600-device"></a>Rozpakowywanie, w stojaku, a Podłączanie kabli do urządzenia StorSimple 8600
## <a name="overview"></a>Omówienie
Do urządzenia 8600 Microsoft Azure StorSimple urządzenia podwójną obudowa i składa się z podstawowym i obudowy EBOD. W tym samouczku wyjaśniono, jak toounpack, zamontować w stojaku i podłączyć kable hello StorSimple 8600 urządzeń sprzętowych przed skonfigurowaniem hello StorSimple oprogramowania.

## <a name="unpack-your-storsimple-8600-device"></a>Rozpakuj do urządzenia StorSimple 8600
Witaj poniższych krokach przedstawiono Wyczyść, szczegółowe informacje na temat toounpack urządzenia magazynującego StorSimple 8600. To urządzenie jest dostarczany w dwóch pól, dla podstawowego obudowa hello i drugi dla hello EBOD obudowy. Te dwa pola następnie są umieszczane w jednym polu.

### <a name="prepare-toounpack-your-device"></a>Przygotowanie toounpack urządzenia
Przed Rozpakuj urządzenia, przejrzyj hello następujących informacji.

![Ikona ostrzeżenia](./media/storsimple-safety/IC740879.png)![ikona ciężki](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **ostrzeżenie!**

1. Upewnij się, że jest dwóch osób toomanage dostępne hello wagi hello urządzenia, jeśli są obsługuje go ręcznie. Obudowa pełni skonfigurowany można porównać się too32 kg (70 kg).
2. Umieść pole hello na powierzchni płaskiej, poziomu.

Następnie wykonaj następujące kroki toounpack hello urządzenia.

#### <a name="toounpack-your-device"></a>toounpack urządzenia
1. Sprawdź, czy pole hello i piana pakietów hello crushes, części, szkody limitu górnego lub widocznego uszkodzenia. Jeśli pole hello lub pakowania poważnie jest uszkodzony, nie otwieraj okno hello. Sprawdź [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) toohelp należy ocenić, czy urządzenie hello jest w dobrym stanie.
2. Otwórz hello zewnętrznego pola, a następnie wyjmij hello dwa pola odpowiadające tooprimary i obudowy EBOD. Można teraz Rozpakuj hello podstawowego i obudowy EBOD. powitania po rysunku przedstawiono hello rozpakowane jednego z obudów hello.
   
    ![Rozpakuj urządzenia magazynu](./media/storsimple-8600-hardware-installation/HCSUnpackyour4Udevice.png)
   
    **Wczytaj widoku urządzenia pamięci masowej**
   
   | Etykieta | Opis |
   | --- | --- |
   |   1 |Pole pakowania |
   |   2 |Kabli SAS (w pasku Akcesoria i kable) |
   |   3 |Pianki dołu |
   |   4 |Urządzenie |
   |   5 |Górny pianki |
   |   6 |Pole akcesoriów |
3. Po rozpakowywania hello dwa pola, upewnij się, że masz:
   
   * Obudowa głównej 1 (obudowa głównej hello i obudowy EBOD znajdują się w dwóch oddzielnych pól)
   * Obudowa EBOD 1
   * kable 4, 2, w każdym polu
   * 2 kabli SAS (tooconnect hello głównej obudowy tooEBOD obudowy)
   * 1 skrzyżowanego kabla Ethernet
   * 2 kable konsoli szeregowej
   * Konwerter USB seryjny 1 dostęp szeregowy
   * 4 QSFP-do-kart SFP + do użytku z interfejsami sieciowymi Ethernet 10
   * 2 stojak zestawów (4 szyny po stronie z instalowania sprzętu, 2 hello obudowa podstawowego i obudowy EBOD), 1 w każdym polu
   * Pobieranie rozpoczęte dokumentacji
     
     Jeśli nie masz żadnego z elementów hello wymienionych powyżej, [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md).  

Witaj, następnym krokiem jest toorack instalacji urządzenia.

## <a name="rack-mount-your-storsimple-8600-device"></a>W stojaku do urządzenia StorSimple 8600
Wykonaj hello dalej tooinstall kroki do urządzenia StorSimple 8600 magazynu w stojaku standardowe 19 cala z przodu i tylnej wpisów. To urządzenie jest dostarczany z dwóch obudów: głównej obudowy i obudowy EBOD. Oba te muszą toobe montowane w stojaku.

Instalacja Hello składa się z wielu kroków, z których każdy jest omówione w hello zgodnie z procedurami.

> [!IMPORTANT]
> Urządzenia StorSimple musi być montowane w stojaku do prawidłowego działania.
> 
> 

### <a name="site-preparation"></a>Przygotowanie lokacji
obudowy Hello musi być zainstalowany w standardowe stojak cala 19, który ma przodu oraz tylnej wpisów. Użyj powitania po tooprepare procedury instalacji stojaku.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>tooprepare hello lokacji stojak instalacji
1. Upewnij się, że hello podstawowego i obudowy EBOD są nieaktywnych bezpiecznie na powierzchni płaskiej stabilny i poziomu pracy (lub podobny).
2. Sprawdź tej lokacji hello, gdzie mają tooset zapasowej ma standardowe AC zasilania z niezależne źródło lub stojak jednostki dystrybucji zasilania (PDU) z zasilacz awaryjny (UPS).
3. Upewnij się, że gniazdo (2 X 2U) jeden 4U jest dostępna w stojaku hello, w którym planujesz toomount hello obudów.

![Ikona ostrzeżenia](./media/storsimple-safety/IC740879.png)![ikona ciężki](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **ostrzeżenie!**

 Upewnij się, że jest dwóch osób toomanage dostępne hello wagi, jeśli Instalator urządzenia hello są Obsługa ręcznie. Obudowa pełni skonfigurowany można porównać się too32 kg (70 kg).

### <a name="rack-prerequisites"></a>Wymagania wstępne w stojaku
obudowy Hello są przeznaczone do instalacji w stojaku standard CAL 19 cabinet z:

* Minimalna głębokość 27.84 cali w stojaku post toopost
* Maksymalna waga 32 kg hello urządzenia
* Maksymalnym wstecz nacisku Pascal 5 (mm 0,5 limitu górnego miernika)

### <a name="rack-mounting-rail-kit"></a>Stojakach kolei kit
Zestaw instalowanie szyny będzie przeznaczony dla hello stojak 19 cala w pliku cabinet. szyny Hello zostały przetestowane toohandle hello maksymalną obudowa wagi. Te szyny będzie również umożliwiać instalacji wielu obudowach bez utraty miejsca w stojaku hello. Najpierw zainstaluj hello EBOD obudowy.

#### <a name="tooinstall-hello-ebod-enclosure-on-hello-rails"></a>Witaj tooinstall obudowa EBOD na powitania szyny
1. Wykonaj ten krok tylko wtedy, gdy wewnętrzny szyny nie są zainstalowane na urządzeniu. Zazwyczaj szyny wewnętrzny hello są instalowane na powitania fabryki. Jeśli szyny nie są zainstalowane, następnie zainstalować hello slajdów kolei po lewej i prawej kolei toohello strony hello obudowa obudowy. Dołącz ich przy użyciu sześciu śruby metryki na każdej stronie. toohelp orientacji, kolei hello slajdów są oznaczone **LH — przodu** i **RH — przodu**, a końcem ma zakończenia hello, który jest dołączony tyłu hello hello załącznika.
   
    ![Podstawa montażowa tooenclosure slajdów kolei dołączenia](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)
   
    **Dołączenia kolei slajdów strony toohello obudowa hello**
   
   | Etykieta | Opis |
   | --- | --- |
   |  1 |M 3 x 4 śruby head przycisku |
   |  2 |Podstawa montażowa slajdów |
2. Dołącz hello kolei lewej i po prawej stronie zestawy toohello stojak cabinet pionowy elementów członkowskich. zaznaczono nawiasy Hello **LH**, **RH**, i **ta strona w górę** tooguide przez poprawnej orientacji.
3. Znajdź numery PIN kolei hello na powitania przodu i do tyłu hello kolei zestawu. Rozszerzanie hello kolei toofit między hello stojak wpisów i włóż hello numerów PIN do hello post front i stojak tyłu element pionowy luk. Pamiętaj, że zestaw kolei hello jest poziom.
4. Zabezpiecz hello stojak toohello zestawu kolei podane pionowej elementy członkowskie przy użyciu dwóch hello śruby metryki. Użyj jednej śrubie na wierzch hello i jeden tyłu hello.
5. Powtórz te kroki dla hello innych kolei zestawu.
   
     ![Dołączenia toorack slajdów kolei cabinet](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Dołączanie kolei zestawy toohello stojak**
   
   | Etykieta | Opis |
   | --- | --- |
   |   1 |Ładunku gwintowanym |
   |   2 |Gwintowanym post stojak front przerw kwadratowe |
   |   3 |Numery PIN lokalizacji front kolei w lewo |
   |   4 |Ładunku gwintowanym |
   |   5 |Po lewej stronie kolei tylnej lokalizacji PIN |

### <a name="mounting-hello-ebod-enclosure-in-hello-rack"></a>Instalowanie obudowa EBOD hello w stojaku hello
Za pomocą hello stojaku, które właśnie zostały zainstalowane, wykonaj następujące kroki toomount hello EBOD obudowa w stojaku hello hello.

#### <a name="toomount-hello-ebod-enclosure"></a>Witaj toomount obudowa EBOD
1. Z Asystentem Podnieś obudowa hello i wyrównanie go z hello stojaku.
2. Starannie Włóż hello obudowy do szyny hello, a następnie Wypchnij go całkowicie w stojaku hello cabinet.
   
    ![Wstawianie w stojaku hello urządzenia](./media/storsimple-8600-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Instalowanie obudowa hello w stojaku hello**
3. Usuń hello lewej i prawej front kołnierza włączony klawisz caps ściąganie caps hello wolne. caps kołnierza powitania po prostu przyciąganie na powitania kołnierze.
4. Zabezpiecz obudowa hello w stojaku hello instalując co podane gwintowanym Phillips head za pośrednictwem każdej kołnierza, lewy i prawy.
5. Zainstaluj caps kołnierza hello naciskając je w miejscu i przyciąganie ich w miejscu.
   
     ![Instalowanie kołnierza CAP](./media/storsimple-8600-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Instalowanie hello kołnierza CAP**
   
   | Etykieta | Opis |
   | --- | --- |
   |   1 |Obudowa gwintowanym zaczepienia |

### <a name="mounting-hello-primary-enclosure-in-hello-rack"></a>Instalowanie hello obudowa podstawowego w stojaku hello
Po zakończeniu instalowania hello EBOD obudowy, konieczne będzie obudowa głównej hello toomount następujące hello te same czynności.

> [!NOTE]
> * Jest możliwe toohave kilka pustych miejsc w hello stojak między hello obudowy podstawowego i obudowy EBOD hello.
> * Użyj hello podane 2m SAS kabel tooconnect hello głównej obudowa toohello EBOD obudowy.
> * Nie ma żadnych ograniczeń na powitania względne położenie hello head jednostki toohello EBOD jednostek. W związku z tym hello obudowa podstawowego można umieścić w hello top miejsca i obudowy EBOD hello poniżej — albo na odwrót.
> 
> 

Witaj, następnym krokiem jest toocable Twojego urządzenia pod kątem zasilania, sieci i dostęp szeregowy.

## <a name="cable-your-storsimple-8600-device"></a>Podłączanie kabli do urządzenia StorSimple 8600
Witaj poniższe procedury wyjaśniają, jak toocable do zasilania, sieci i połączenia szeregowego urządzenia StorSimple 8600.

### <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem toocable urządzenia będą potrzebne:

* Obudowa podstawowym, a obudowa EBOD hello, całkowicie rozpakowane.
* 4 kable zasilania (2 hello podstawowego i hello obudowa EBOD), które dołączone do urządzenia
* 2 kabli SAS dostarczony wraz z hello urządzenia tooconnect hello EBOD obudowa toohello głównej obudowy
* Dostęp too2 jednostki dystrybucji zasilania (PDU) (zalecane)
* Kable sieciowe
* Podany kable szeregowe
* Konwerter seryjny USB z odpowiedni sterownik hello zainstalowane na komputerze (w razie potrzeby)
* Podany 4 QSFP-do-kart SFP + do użytku z interfejsami sieciowymi Ethernet 10
* [Sprzętu obsługiwanego przez hello 10 GbE interfejsy na urządzeniu StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="sas-and-power-cabling"></a>Sygnatury dostępu Współdzielonego i okablowanie zasilania
Urządzenie ma głównej obudowy oraz obudowy EBOD. Wymaga to toobe jednostki hello kablem razem łączności Serial Attached SCSI (SAS) i zasilania.

Podczas konfigurowania tego urządzenia do powitania po raz pierwszy, należy wykonać czynności hello SAS najpierw okablowania i następnie pełne hello kroki okablowania zasilania.

[!INCLUDE [storsimple-cable-8600-for-SAS](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

### <a name="network-cabling"></a>Okablowanie sieci
Urządzenie znajduje się w konfiguracji aktywnego gotowości: w dowolnym momencie, jeden moduł kontrolera jest aktywna i przetwarzanie wszystkich operacji dysku i sieci podczas hello inny moduł kontrolera przechodzi w stan wstrzymania. W przypadku niepowodzenia kontrolera kontrolera rezerwy hello natychmiast aktywuje i kontynuuje wszystkie operacje hello dysku i sieci.

toosupport tej pracy awaryjnej nadmiarowych kontrolera, należy toocable urządzenie sieci, jak pokazano w hello następujące kroki.

#### <a name="toocable-for-network-connection"></a>toocable dla połączenia sieciowego
1. Urządzenie ma sześć interfejsów sieciowych na każdym kontrolerze: cztery 1 GB/s i 10 dwa porty Ethernet GB/s. Zobacz toohello po ilustracji tooidentify hello danych portów płyty montażowej hello urządzenia.
   
     ![Płyty montażowej urządzenia 8600](./media/storsimple-8600-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Powrót z urządzenia przedstawiający hello porty danych**
   
   | Etykieta | Opis |
   | --- | --- |
   |   0,1,4,5 |Interfejsy sieciowe Ethernet 1 |
   |   2,3 |Interfejsy sieciowe Ethernet 10 |
   |   6 |Porty szeregowe |
2. Zobacz powitania po diagram okablowanie sieci. (Konfiguracja minimalna sieci hello znajduje się pełny liniami niebieski. Wysokiej dostępności i wydajności konieczności dodatkowej konfiguracji znajduje się za pomocą linii przerywana.)

![Podłączanie kabli do urządzenia 4U sieci](./media/storsimple-8600-hardware-installation/HCSCableYour4UDeviceforNetwork.png)

**Okablowania urządzenia sieciowego**

| Etykieta | Opis |
| --- | --- |
| A |Sieć LAN z dostępem do Internetu |
| B |Kontrolera 0 |
| C |PCM 0 |
| D |Kontrolera 1 |
| E |PCM 1 |
| F |EBOD kontrolera 0 |
| G |EBOD kontrolera 1 |
| H, I |Hosty (na przykład serwery plików) |
| 0-5 |Interfejsy sieciowe |
| 6 |Obudowa podstawowego |
| 7 |Obudowa EBOD |

W przypadku okablowania hello urządzenia, wymaga minimalnej konfiguracji hello:

* Co najmniej dwa interfejsy sieciowe podłączone na każdym kontrolerze, aby uzyskać dostęp z chmury i jeden dla interfejsu iSCSI. Witaj dane 0 portu jest automatycznie włączona i skonfigurowana za pośrednictwem konsoli szeregowej hello hello urządzenia. Oprócz dane 0 innego portu danych musi toobe skonfigurowana za pośrednictwem hello klasycznego portalu Azure. W takim przypadku połączyć dane 0 portu toohello głównej LAN (sieci z dostępem do Internetu). Witaj innych danych, które porty mogą być połączone segment sieci LAN (VLAN) tooSAN/iSCSI hello sieci, w zależności od roli hello przeznaczone.
* Identyczne interfejsów w każdej toohello kontrolera połączony sam sieciowa tooensure dostępność, jeśli do pracy awaryjnej kontrolera. Na przykład jeśli wybierzesz tooconnect dane 0, a dane 3 dla jednego z kontrolerów hello należy hello tooconnect odpowiednie dane 0 i dane 3 na hello inny kontroler.

Należy pamiętać o wysokiej dostępności i wydajność:

* Jeśli to możliwe, należy skonfigurować parę interfejsu sieciowego, aby uzyskać dostęp do chmury (1 GbE) i inną parę dla interfejsu iSCSI (10 GbE zalecana) na każdym kontrolerze.
* Jeśli to możliwe, należy połączyć interfejsów sieciowych z każdego kontrolera tootwo różnych przełączników tooensure dostępności awariami przełącznika. Witaj rysunku przedstawiono Witaj dwie 10 GbE interfejsy sieciowe dane 2 i dane 3 z każdego kontrolera połączone tootwo różnych przełączników. Aby uzyskać więcej informacji, zobacz toohello **interfejsy sieciowe** w obszarze hello [wymagania dotyczące wysokiej dostępności dla urządzenia StorSimple](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Jeśli używasz nadawczo-odbiorczych SFP + z interfejsów sieciowych 10 GbE, użyj hello udostępnione QSFP-SFP + kart. Aby uzyskać więcej informacji, przejdź zbyt[obsługiwanym sprzęcie interfejsów sieciowych GbE hello 10 na urządzeniu StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Okablowanie portu szeregowego
Wykonaj następujące kroki toocable hello portu szeregowego.

#### <a name="toocable-for-serial-connection"></a>toocable dla połączenia szeregowego
1. Urządzenie ma portu szeregowego na każdym kontrolerze, który jest identyfikowany przez ikona klucza. porty szeregowe hello toolocate, można znaleźć toohello ilustracji przedstawiono hello danych porty na powitania obu urządzenia.
2. Zidentyfikuj kontroler active hello na płyty montażowej Twoje urządzenie. Migający LED niebieski wskazuje, że ten kontroler hello jest aktywny.
3. Przy użyciu kabel szeregowy hello podane (w razie potrzeby hello szeregowego USB konwerter dla komputera przenośnego), a Uzyskuj dostęp do konsoli lub komputerze z (urządzenie toohello emulacji terminala) toohello portu szeregowego hello active kontrolera.
4. Zainstaluj sterowniki USB seryjny hello (dostarczane z urządzeniem hello) na komputerze.
5. Skonfiguruj połączenie szeregowe hello w następujący sposób:
   
   * 115 200 transmisji
   * 8 bitów danych
   * 1 bit zatrzymania
   * Brak parzystości
   * Sterowanie przepływem ustawić także**None**
6. Zweryfikować hello połączenia, naciskając klawisz Enter na powitania konsoli. Menu konsoli szeregowej powinny być wyświetlane.

> [!NOTE]
> **Zarządzanie lights-Out:** podczas urządzenie hello jest zainstalowane w zdalnym centrum danych lub w pokoju komputera o ograniczonym dostępie, upewnij się, że hello połączenia szeregowego tooboth kontrolery są zawsze połączone tooa konsoli szeregowej przełącznika lub podobnego sprzętu. Dzięki temu poza pasmem zdalnego sterowania i pomocy technicznej operacji w przypadku przerw w działaniu sieci lub nieoczekiwanych awarii.
> 
> 

Ukończono okablowania do zasilania, dostęp do sieci, urządzenia i serial connection.hello następnym krokiem jest tooconfigure hello oprogramowania na urządzeniu.

## <a name="next-steps"></a>Następne kroki
Teraz można przystąpić zbyt[wdrażania i konfigurowania lokalnego urządzenia StorSimple](storsimple-deployment-walkthrough-u2.md).

