---
title: "aaaConfigure wielościeżkowego We/Wy na hoście z systemem StorSimple Linux | Dokumentacja firmy Microsoft"
description: "Konfigurowanie wielościeżkowego wejścia/wyjścia na hoście z systemem Linux tooa StorSimple połączone systemem CentOS 6.6"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a>Konfigurowanie wielościeżkowego wejścia/wyjścia na hoście StorSimple z systemem CentOS
W tym artykule opisano hello kroki wymagane tooconfigure Wielościeżkowe We/Wy (MPIO) na serwerze hosta Centos 6.6. serwer hosta Hello jest tooyour podłączonego urządzenia Microsoft Azure StorSimple wysokiej dostępności za pośrednictwem inicjatorów iSCSI. Opisuje w szczegółów hello automatycznego odnajdywania urządzeń wielościeżkowego i hello określonych ustawień tylko dla woluminów StorSimple.

Ta procedura jest modeli hello tooall dotyczy urządzeń z serii StorSimple 8000.

> [!NOTE]
> Nie można użyć tej procedury dla urządzenia wirtualnego StorSimple. Aby uzyskać więcej informacji zobacz temat jak tooconfigure obsługiwać serwery dla urządzenia wirtualnego.
> 
> 

## <a name="about-multipathing"></a>O wiele ścieżek
Funkcja wielu ścieżek Hello umożliwia tooconfigure wiele ścieżek wejścia/wyjścia między serwerem hosta a urządzeniem magazynującym. Te ścieżki We/Wy są fizycznych połączeń sieci SAN, które mogą zawierać osobne kable, przełączniki interfejsów sieciowych i kontrolerów. Wiele ścieżek agreguje hello ścieżek wejścia/wyjścia, tooconfigure nowe urządzenie, którego jest skojarzony z wszystkich ścieżek hello agregowane.

Celem Hello wielu ścieżek jest dwukrotne:

* **Wysoka dostępność**: zapewnia alternatywną ścieżkę, jeśli dowolny element ścieżki hello we/wy (takie jak kabel, przełącznika, interfejsu sieciowego lub kontrolera) zakończy się niepowodzeniem.
* **Równoważenie obciążenia**: w zależności od konfiguracji hello urządzenia magazynującego, go poprawić wydajność hello przez wykrycie obciążenia w ścieżkach hello We/Wy i dynamicznie ponowne równoważenie obciążenia tych.

### <a name="about-multipathing-components"></a>O wiele ścieżek składników
Wiele ścieżek w systemie Linux zawiera składniki jądra i przestrzeń użytkownika jak przedstawione w poniższej tabeli.

* **Jądra**: główny składnik hello jest hello *mapowania urządzenia* zmienia trasę We/Wy i obsługuje tryb failover dla ścieżki i grup ścieżki.

* **Przestrzeń użytkownika**: są to *narzędzia wielościeżkowego* który zarządzania multipathed urządzeniami przez poinstruowanie wielościeżkowe moduł mapowania urządzenia hello jakie toodo. narzędzia Hello obejmują:
   
   * **Wielościeżkowe**: zawiera listę i konfiguruje multipathed urządzenia.
   * **Multipathd**: demon wykonujący ścieżki hello wielościeżkowego i monitory.
   * **Nazwa Devmap**: devmaps zapewnia łatwy do rozpoznania tooudev nazwy urządzenia.
   * **Kpartx**: mapuje liniowej devmaps toodevice partycje toomake wielościeżkowe mapy partitionable.
   * **MultiPath.conf**: plik konfiguracji wielościeżkowe demona, tabela wbudowanych konfiguracji hello toooverwrite używane.

### <a name="about-hello-multipathconf-configuration-file"></a>Plik konfiguracji multipath.conf hello — informacje
plik konfiguracji Hello `/etc/multipath.conf` sprawia, że wiele hello funkcji wielu ścieżek do skonfigurowania użytkownika. Witaj `multipath` demon jądra polecenia i hello `multipathd` korzystać z informacji zamieszczonych w tym pliku. Plik Hello konsultacji tylko podczas konfiguracji hello hello wielościeżkowe urządzeń. Upewnij się, że wszystkie zmiany zostały wprowadzone, przed rozpoczęciem powitalne `multipath` polecenia. W przypadku zmodyfikowania pliku hello później, należy toostop a start multipathd ponownie dla efektu tootake zmiany hello.

Witaj multipath.conf zawiera pięć sekcje:

- **Poziomu domyślnych ustawień systemowych** *(wartość domyślna)*: można zastąpić poziomu ustawień domyślnych systemu.
- **Urządzenia na liście zabronionych numerów** *(czarna lista)*: można określić hello listę urządzeń, które nie powinny być kontrolowane na podstawie mapowania urządzenia.
- **Wyeliminować wyjątki** *(blacklist_exceptions)*: można zidentyfikować traktowane jako wielościeżkowe urządzeń, nawet wtedy, gdy na liście zabronionych hello toobe określonych urządzeń.
- **Określone ustawienia kontrolera magazynu** *(urządzeń)*: można określić ustawienia konfiguracji, które mają być zastosowane toodevices, zainstalowanego dostawcy i informacje o produkcie.
- **Określone ustawienia urządzenia** *(multipaths)*: ustawienia konfiguracji tej sekcji strojenia toofine hello można użyć dla poszczególnych jednostek LUN.

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a>Konfigurowanie wielu ścieżek na hoście połączonych tooLinux StorSimple
Host Linux tooa podłączone urządzenia StorSimple można skonfigurować wysoką dostępność i równoważenie obciążenia. Na przykład jeśli hello Linux host ma dwa interfejsy toohello połączonych sieci SAN i hello urządzenie ma dwa interfejsy podłączone toohello SAN hello takie, które te interfejsy są w tej samej podsieci, a następnie będzie 4 ścieżki dostępna. Jednak jeśli każdy interfejs danych w interfejsie hello urządzenia i hosta w innej podsieci IP (i nie wzajemnie obsługują routing), to tylko 2 ścieżki będą dostępne. Można skonfigurować wiele ścieżek tooautomatically odnajdywanie wszystkich ścieżek dostępnych hello, wybrać algorytm równoważenia obciążenia dla tych ścieżek, zastosowania określonych ustawień konfiguracyjnych dla woluminów tylko StorSimple, włączyć i sprawdź wielu ścieżek.

Witaj poniższej procedury opisano tooconfigure wielu ścieżek, gdy urządzenie StorSimple z dwoma interfejsami sieciowymi hosta tooa połączonych z dwoma interfejsami sieciowymi.

## <a name="prerequisites"></a>Wymagania wstępne
Ta sekcja zawiera szczegóły dotyczące wymagań wstępnych dotyczących CentOS serwera oraz urządzenia StorSimple hello konfiguracji.

### <a name="on-centos-host"></a>Na hoście CentOS
1. Upewnij się, że na hoście CentOS ma włączone 2 interfejsów sieciowych. Wpisz:
   
    `ifconfig`
   
    Witaj poniższy przykład przedstawia dane wyjściowe powitania po dwa interfejsy sieciowe (`eth0` i `eth1`) znajdują się na hoście hello.
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. Zainstaluj *iSCSI inicjatora witryny* na serwerze CentOS. Wykonaj następujące kroki tooinstall hello *iSCSI inicjatora witryny*.
   
   1. Zaloguj się jako `root` do hosta CentOS.
   2. Zainstaluj hello *iSCSI inicjatora witryny*. Wpisz:
      
       `yum install iscsi-initiator-utils`
   3. Po hello *iSCSI inicjatora witryny* jest poprawnie zainstalowany, uruchomienie usługi iSCSI hello. Wpisz:
      
       `service iscsid start`
      
       W przypadkach `iscsid` faktycznie nie może uruchomić i hello `--force` opcji mogą być potrzebne.
   4. Włączenie z inicjatora iSCSI w czasie rozruchu, użyj hello tooensure `chkconfig` polecenia tooenable hello usługi.
      
       `chkconfig iscsi on`
   5. tooverify, która została prawidłowo Instalatora, uruchom polecenie hello:
      
       `chkconfig --list | grep iscsi`
      
       Poniżej pokazano przykładowe dane wyjściowe.
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       Z hello powyżej przykładzie widać, że środowisko iSCSI uruchomi w czasie rozruchu wykonywania poziomu 2, 3, 4 i 5.
3. Zainstaluj *urządzenia mapowania wielościeżkowego*. Wpisz:
   
    `yum install device-mapper-multipath`
   
    Witaj, instalacja rozpocznie się. Typ **Y** toocontinue po wyświetleniu monitu o potwierdzenie.

### <a name="on-storsimple-device"></a>Na urządzeniu StorSimple
Urządzenia StorSimple powinny mieć:

* Co najmniej dwa interfejsy włączone dla interfejsu iSCSI. tooverify, że dwa interfejsy są włączone iSCSI na urządzeniu StorSimple, wykonaj następujące kroki w portalu klasycznego Azure dla urządzenia StorSimple hello hello:
  
  1. Zaloguj się do klasycznego portalu powitania dla urządzenia StorSimple.
  2. Wybierz usługę Menedżer StorSimple, kliknij przycisk **urządzeń** i wybierz polecenie hello określonego urządzenia StorSimple. Kliknij przycisk **Konfiguruj** i sprawdź ustawienia interfejsu sieciowego hello. Poniżej przedstawiono zrzut ekranu z dwa interfejsy sieci iSCSI. Tutaj dane 2 i dane 3, zarówno 10 GbE interfejsy są włączone dla interfejsu iSCSI.
     
      ![Konfiguracja MPIO StorsSimple dane 2](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Wielościeżkowe wejście/wyjście StorSimple dane 3 konfiguracji](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      W hello **Konfiguruj** strony
     
     1. Upewnij się, że oba interfejsy sieciowe są włączone iSCSI. Witaj **iSCSI włączone** pola powinna być ustawiona zbyt**tak**.
     2. Sprawdź, czy hello interfejsy sieciowe mają hello samej szybkości, powinny być 1 GbE lub 10 GbE.
     3. Należy pamiętać, adresy hello IPv4 hello włączono interfejs iSCSI interfejsów i Zapisz do późniejszego użytku na hoście hello.
* interfejsy iSCSI Hello na urządzeniu StorSimple powinny być dostępne z hello CentOS serwera.
      tooverify, należy tooprovide hello adresy IP interfejsów sieci iSCSI StorSimple na serwerze hosta. Witaj polecenia używane i hello odpowiednie dane wyjściowe z dane2 (10.126.162.25) i DATA3 (10.126.162.26) są wyświetlane poniżej:
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a>Konfiguracja sprzętu
Zaleca się połączyć z hello dwa iSCSI interfejsy sieci na oddzielnych ścieżek nadmiarowości. na poniższym rysunku Hello przedstawiono hello zalecana konfiguracja sprzętu wysokiej dostępności i równoważenia obciążenia wielu ścieżek dla urządzenia StorSimple i CentOS serwera.

![Konfiguracja sprzętowa wielościeżkowego wejścia/wyjścia dla hosta tooLinux StorSimple](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

Jak pokazano w powyższej ilustracji hello:

* Urządzenia StorSimple znajduje się w konfiguracji aktywny / pasywny z dwóch kontrolerów.
* Dwa przełączniki sieci SAN są kontrolery urządzeń podłączonych tooyour.
* Dwa inicjatorów iSCSI są włączone na urządzeniu StorSimple.
* Dwa interfejsy sieciowe są włączone na hoście CentOS.

Hello powyżej konfiguracji umożliwia uzyskanie 4 osobnych ścieżek między urządzenia i hello hosta, jeśli hello danych hosta i interfejsy są wzajemnie obsługiwać Routing.

> [!IMPORTANT]
> * Zaleca się, że niemieszanie 1 GbE i 10 GbE interfejsów sieciowych do obsługi wielu ścieżek. Korzystając z dwóch interfejsów sieciowych, dotyczą obu interfejsów hello powinna być typu identyczne hello.
> * Na urządzeniu StorSimple DATA0, dane1, DATA4 i DATA5 są 1 GbE interfejsy dane2 i DATA3 są 10 GbE interfejsów. |
> 
> 

## <a name="configuration-steps"></a>Kroki konfiguracji
kroki konfiguracji Hello wielu ścieżek obejmują konfigurowanie hello dostępnych ścieżek automatycznego wykrywania, określając hello równoważenia obciążenia algorytmu toouse, włączanie wielu ścieżek i na koniec Weryfikowanie konfiguracji hello. Każdy z tych kroków omówiono szczegółowo w hello następujące sekcje.

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a>Krok 1: Konfigurowanie wielu ścieżek automatycznego wykrywania
automatycznie odnalezione urządzenia obsługiwane wielościeżkowe Hello i skonfigurowane.

1. Inicjowanie `/etc/multipath.conf` pliku. Wpisz:
   
     `mpathconf --enable`
   
    utworzy Hello powyżej polecenie `sample/etc/multipath.conf` pliku.
2. Uruchom usługę wielu ścieżek. Wpisz:
   
    `service multipathd start`
   
    Zostanie wyświetlony hello następujące dane wyjściowe:
   
    `Starting multipathd daemon:`
3. Włącz automatyczne odnajdowanie multipaths. Wpisz:
   
    `mpathconf --find_multipaths y`
   
    Spowoduje to zmodyfikowanie hello wartości domyślne sekcji z `multipath.conf` w sposób przedstawiony poniżej:
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a>Krok 2: Konfigurowanie wielu ścieżek dla woluminów StorSimple
Domyślnie wszystkie urządzenia są czarny wymienione w pliku multipath.conf hello i będą pomijane. Należy toocreate zabronionych wyjątki tooallow w wielu ścieżek dla woluminów z urządzenia StorSimple.

1. Edytuj hello `/etc/mulitpath.conf` pliku. Wpisz:
   
    `vi /etc/multipath.conf`
2. Zlokalizuj hello blacklist_exceptions sekcji w pliku multipath.conf hello. Urządzenia StorSimple musi toobe wymienione jako wyjątek zabronionych w tej sekcji. Użytkownik może usuń znaczniki komentarza odpowiednich wierszy w tym toomodify pliku go w sposób przedstawiony poniżej (używana tylko hello określonego modelu hello urządzenia, które są używane):
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a>Krok 3: Konfigurowanie wielu ścieżek okrężnego
Ten algorytm równoważenia obciążenia używa wszystkich kontrolera active dostępne toohello multipaths hello w sposób zrównoważony, okrężnego.

1. Edytuj hello `/etc/multipath.conf` pliku. Wpisz:
   
    `vi /etc/multipath.conf`
2. W obszarze hello `defaults` sekcji, ustaw hello `path_grouping_policy` zbyt`multibus`. Witaj `path_grouping_policy` określa hello domyślna ścieżka grupowanie zasady tooapply toounspecified multipaths. Witaj wartości domyślne sekcji będzie wyglądać jak pokazano poniżej.
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> Witaj najbardziej typowe wartości `path_grouping_policy` obejmują:
> 
> * tryb failover = 1 ścieżka według priorytetu grupy
> * multibus = wszystkie prawidłowe ścieżki w grupie o priorytecie 1
> 
> 

### <a name="step-4-enable-multipathing"></a>Krok 4: Włącz wielościeżkowe
1. Uruchom ponownie hello `multipathd` demon. Wpisz:
   
    `service multipathd restart`
2. Witaj dane wyjściowe będą mieć, jak pokazano poniżej:
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a>Krok 5: Sprawdzanie wielu ścieżek
1. Najpierw upewnij się, że iSCSI jest nawiązywane połączenie z urządzenia StorSimple hello w następujący sposób:
   
   a. Odnajdywanie urządzenia StorSimple. Wpisz:
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    wynik Hello, gdy adres IP dla DATA0 jest 10.126.162.25 i jest otwarty port 3260, na urządzeniu StorSimple powitania dla ruchu wychodzącego iSCSI jest w sposób przedstawiony poniżej:
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    Kopiuj hello IQN urządzenia StorSimple `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, z hello poprzedzających danych wyjściowych.

   b. Podłącz urządzenie toohello przy użyciu docelowego IQN. urządzenie StorSimple Hello jest hello obiektu docelowego iSCSI w tym miejscu. Wpisz:

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    Witaj poniższy przykład przedstawia dane wyjściowe z elementem docelowym IQN z `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`. dane wyjściowe Hello wskazuje pomyślnego połączenia toohello dwa interfejsy sieci iSCSI na urządzeniu.

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    Jeśli zostanie wyświetlony interfejs tylko jednego hosta i dwóch ścieżek, następnie należy tooenable obu interfejsów hello na hoście dla interfejsu iSCSI. Możesz wykonać hello [szczegółowe instrukcje w dokumentacji systemu Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).

2. Wolumin jest narażonych toohello CentOS serwera z hello urządzenia StorSimple. Aby uzyskać więcej informacji, zobacz [krok 6: Tworzenie woluminu](storsimple-deployment-walkthrough.md#step-6-create-a-volume) za pośrednictwem hello klasycznego portalu Azure w urządzeniu StorSimple.

3. Sprawdź hello dostępnych ścieżek. Wpisz:

      ```
      multipath –l
      ```

      Poniższy przykład Hello przedstawiono dane hello dwa interfejsy sieci w interfejsie sieciowym pojedynczy host tooa podłączonego urządzenia StorSimple z dwóch ścieżek dostępne.

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a>Rozwiązywanie problemów z wielu ścieżek
Ta sekcja zawiera wskazówki przydatne, jeśli wystąpiły problemy podczas konfigurowania wielu ścieżek.

Q. Nie ma zmiany hello `multipath.conf` pliku wpływają.

A. Jeśli wprowadzono żadnych zmian toohello `multipath.conf` plik, trzeba będzie toorestart hello wielu ścieżek usługi. Wpisz następujące polecenie hello:

    service multipathd restart

Q. Dwa interfejsy sieci na urządzeniu StorSimple hello i dwa interfejsy sieciowe na hoście hello został włączony. Podczas wyświetlania dostępnych ścieżek hello są widoczne tylko dwie ścieżki. Oczekiwana toosee czterech dostępnych ścieżek.

A. Upewnij się, że Witaj dwie ścieżki są na powitania tej samej podsieci i wzajemnie obsługują routing. Jeśli interfejsy sieciowe hello znajdują się na różnych sieci VLAN, a nie obsługuje routingu, wyświetlona zostanie tylko dwie ścieżki. Jednym ze sposobów tooverify jest toomake się upewnić, że może nawiązać połączenie obu interfejsów hosta hello z karty sieciowej na urządzeniu StorSimple hello. Konieczne będzie zbyt[skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) jako weryfikacji jest możliwe tylko za pośrednictwem sesji pomocy technicznej.

Q. Podczas wyświetlania dostępnych ścieżek, nie ma żadnych danych wyjściowych.

A. Zazwyczaj nie ma żadnych ścieżek multipathed sugeruje problem z hello demon wielu ścieżek, i jest to najprawdopodobniej wszelkie problemy w tym miejscu znajduje się w hello `multipath.conf` pliku.

Byłoby warto sprawdzanie, czy rzeczywiście widać niektóre dyski po nawiązaniu połączenia z docelowym toohello jako odpowiedzi z listy wielościeżkowe hello może również oznaczać, że nie ma żadnych dysków.

* Użyj powitania po magistrali SCSI hello toorescan polecenia:
  
    `$ rescan-scsi-bus.sh `(część pakietu sg3_utils)
* Wpisz następujące polecenia hello:
  
    `$ dmesg | grep sd*`
     
     Lub
  
    `$ fdisk –l`
  
    Te będą zwracane szczegóły ostatnio dodane dyski.
* czy jest to dysk StorSimple toodetermine Użyj hello następującego polecenia:
  
    `cat /sys/block/<DISK>/device/model`
  
    Zwraca ciąg, który określa, czy jest to dysk StorSimple.

A mniej prawdopodobne, ale możliwa przyczyna może być również starych iscsid identyfikator PID procesu. Użyj poniższych poleceń toolog poza z sesji iSCSI hello hello:

    iscsiadm -m node --logout -p <Target_IP>

Powtórz to polecenie dla wszystkich interfejsów sieciowych hello połączony na obiektów docelowych iSCSI hello, czyli urządzenia StorSimple. Po wylogowanie ma ze wszystkich sesji iSCSI hello Użyj sesji iSCSI hello tooreestablish IQN hello iSCSI docelowej. Wpisz następujące polecenie hello:

    iscsiadm -m node --login -T <TARGET_IQN>


Q. Nie mam pewności, czy urządzenie jest białej.

A. tooverify, czy urządzenie jest białej, użyj hello następujące polecenie interaktywne rozwiązywania problemów:

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


Aby uzyskać więcej informacji, przejdź zbyt[Użyj Rozwiązywanie problemów z interaktywnego polecenia wielu ścieżek](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).

## <a name="list-of-useful-commands"></a>Lista poleceń przydatne
| Typ | Polecenie | Opis |
| --- | --- | --- |
| **iSCSI** |`service iscsid start` |Uruchomienie usługi iSCSI |
| &nbsp; |`service iscsid stop` |Zatrzymaj usługę iSCSI |
| &nbsp; |`service iscsid restart` |Ponowne uruchomienie usługi iSCSI |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |Odnajdywanie dostępnych elementów docelowych na powitania określony adres |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |Zaloguj się za toohello obiektów docelowych iSCSI |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |Wyloguj się z hello obiektów docelowych iSCSI |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |Nazwa inicjatora iSCSI drukowania |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |Sprawdź stan hello hello sesji iSCSI i wolumin odnalezionych na hoście hello |
| &nbsp; |`iscsi –m session` |Przedstawia wszystkie sesje iSCSI hello między hello hosta i hello urządzenia StorSimple |
|  | | |
| **Wiele ścieżek** |`service multipathd start` |Demon wielościeżkowe Start |
| &nbsp; |`service multipathd stop` |Zatrzymaj demon wielościeżkowych |
| &nbsp; |`service multipathd restart` |Uruchom ponownie demon wielościeżkowych |
| &nbsp; |`chkconfig multipathd on` </br> LUB </br> `mpathconf –with_chkconfig y` |Włącz wielościeżkowe demon toostart w czasie rozruchu |
| &nbsp; |`multipathd –k` |Uruchom konsolę interakcyjne hello do rozwiązywania problemów |
| &nbsp; |`multipath –l` |Lista połączeń wielościeżkowe i urządzeń |
| &nbsp; |`mpathconf --enable` |Utwórz plik przykładowy mulitpath.conf w`/etc/mulitpath.conf` |
|  | | |

## <a name="next-steps"></a>Następne kroki
Jak skonfigurować wielościeżkowego We/Wy na hoście z systemem Linux, może być również konieczne toohello toorefer po CentoS 6.6 dokumentów:

* [Konfigurowanie wielościeżkowego wejścia/wyjścia na CentOS](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [Przewodnik szkolenia systemu Linux](http://linux-training.be/files/books/LinuxAdm.pdf)

