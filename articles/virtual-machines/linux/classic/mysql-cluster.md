---
title: "aaaClusterize MySQL z równoważeniem obciążenia zestawami | Dokumentacja firmy Microsoft"
description: "Konfigurowanie równoważenia obciążenia, wysoka dostępność, klaster programu Linux MySQL utworzone z hello klasycznego modelu wdrażania na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a>Zestawów o zrównoważonym obciążeniu tooclusterize MySQL w systemie Linux
> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager](../../../resource-manager-deployment-model.md) i klasycznym. W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. A [szablonu usługi Resource Manager](https://azure.microsoft.com/documentation/templates/mysql-replication/) jest dostępna, jeśli potrzebujesz toodeploy klaster programu MySQL.

W tym artykule Eksploruje i przedstawia hello różne podejścia toodeploy dostępne wysokiej dostępności opartych na systemie Linux usług Microsoft Azure, wysokiej dostępności serwera MySQL jako Elementarz eksploracji. Film pokazujący to rozwiązanie jest dostępne na [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).

Firma Microsoft będzie konspektu nieudostępnianych jednostkach, dwa węzły, punktowe MySQL rozwiązanie zapewniające wysoką dostępność na podstawie DRBD, Corosync i rozrusznik. Tylko jeden węzeł uruchamia MySQL naraz. Odczytywanie i zapisywanie z hello DRBD zasobów jest również ograniczony tooonly jeden węzeł naraz.

Ponieważ użyjesz równoważeniem obciążenia zestawów w okrężnego tooprovide wykrywania funkcjonalność i punktu końcowego, usuwania i skuteczne odzyskanie hello VIP Microsoft Azure nie istnieje potrzeba rozwiązania adresu VIP, takich jak LV. Witaj adresu VIP jest globalnie podlegającego routingowi adres IPv4 przypisany przez Microsoft Azure, podczas tworzenia usługi w chmurze hello.

Są dostępne jako Maszynę wirtualną na innych możliwych architektury MySQL, łącznie z klastra NBD, Percona Galera i kilka rozwiązań oprogramowania pośredniczącego, w tym co najmniej jeden [magazynu maszyny Wirtualnej](http://vmdepot.msopentech.com). Tak długo, jak te rozwiązania mogą replikować w emisji pojedynczej i multiemisji lub emisji i nie należy polegać na magazyn udostępniony lub wiele interfejsów sieciowych, scenariusze hello powinna być łatwa toodeploy w systemie Microsoft Azure.

Tych klastrów architektury można rozszerzyć tooother produktów, takich jak PostgreSQL i OpenLDAP w podobny sposób. Na przykład procedury Równoważenie obciążenia bez udostępniania żadnego pomyślnie była testowana przy wielu wzorca OpenLDAP i można go oglądać w naszym blogu Channel 9.

## <a name="get-ready"></a>Przygotuj się
Potrzebujesz następujących hello zasobów i możliwości:

  - Microsoft Azure konto z prawidłową subskrypcją stanie toocreate co najmniej dwóch maszyn wirtualnych (XS został użyty w tym przykładzie)
  - Sieci i podsieci
  - Grupa koligacji
  - Zestaw dostępności
  - Witaj toocreate możliwości wirtualne dyski twarde w tym samym regionie co usługa w chmurze hello hello i dołącz je toohello maszyn wirtualnych systemu Linux

### <a name="tested-environment"></a>Przetestowany środowiska
* Ubuntu 13.10
  * DRBD
  * Serwer MySQL
  * Corosync i rozrusznik

### <a name="affinity-group"></a>Grupa koligacji
Utwórz grupę koligacji dla rozwiązania hello logując się toohello klasycznego portalu Azure, wybierając **ustawienia**oraz tworzenia grupy koligacji. Przydzielone zasoby utworzone później zostanie przypisany toothis grupy koligacji.

### <a name="networks"></a>Sieci
Utworzono nową sieć, a w sieci hello została utworzona podsieć. W tym przykładzie używane sieci 10.10.10.0/24 z podsieci o prefiksie/24 tylko jeden wewnątrz.

### <a name="virtual-machines"></a>Maszyny wirtualne
Witaj pierwsza maszyna wirtualna 13.10 Ubuntu jest tworzona przy użyciu obrazu Endorsed Ubuntu galerii i nosi nazwę `hadb01`. Nową usługę w chmurze jest tworzony w procesie hello, nazywanym hadb. Ta nazwa przedstawiono hello udostępniony, rodzaj równoważenia obciążenia, mające usługi powitania po dodaniu więcej zasobów. Witaj tworzenie `hadb01` ma procesu i jest wypełniane przy użyciu portalu hello. Punkt końcowy SSH jest tworzony automatycznie, a wybrano hello nowej sieci. Teraz możesz utworzyć zbiór dostępności dla hello maszyn wirtualnych.

Po hello pierwsza maszyna wirtualna jest tworzony (technicznie, podczas tworzenia usługi w chmurze hello), należy utworzyć hello drugiej maszyny Wirtualnej, `hadb02`. Dla hello drugie maszyny Wirtualnej, użyj maszyny Wirtualnej systemu Ubuntu 13.10 z hello galerii przy użyciu portalu hello, ale użyj istniejącej usługi chmury, `hadb.cloudapp.net`, zamiast tworzyć nowy. Witaj sieci i zestawu dostępności powinna być zaznaczona automatycznie. Punkt końcowy SSH zostanie utworzony, zbyt.

Po utworzeniu obie maszyny wirtualne, zwróć uwagę na powitania portu SSH dla `hadb01` (TCP 22) i `hadb02` (automatycznie przypisywana przez platformę Azure).

### <a name="attached-storage"></a>Magazyn dołączony
Dołącz nowe tooboth dysku maszyn wirtualnych i utworzyć dyski 5 GB w procesie hello. dyski Hello są obsługiwane w hello kontener wirtualnego dysku twardego na użytek dysków główne systemu operacyjnego. Po dyski są tworzone i dołączyć, jest nie konieczności toorestart Linux, ponieważ jądra hello zobaczą hello nowe urządzenie. To urządzenie jest zwykle `/dev/sdc`. Sprawdź `dmesg` hello danych wyjściowych.

Na każdej maszynie Wirtualnej, Utwórz partycję za pomocą `cfdisk` (partycji podstawowej, Linux) i zapisu hello nowej partycji tabeli. Nie należy tworzyć system plików na tej partycji.

## <a name="set-up-hello-cluster"></a>Konfigurowanie klastra hello
Użyj stanie tooinstall Corosync rozrusznik i DRBD na obu maszynach wirtualnych Ubuntu. toodo tak z `apt-get`Uruchom hello następujący kod:

    sudo apt-get install corosync pacemaker drbd8-utils.

W tej chwili nie należy instalować MySQL. Debian i Ubuntu skrypty instalacyjne zainicjować katalog danych MySQL na `/var/lib/mysql`, ale ponieważ hello katalogu zostaną zastąpione przez system plików DRBD, należy tooinstall MySQL później.

Sprawdź (przy użyciu `/sbin/ifconfig`) czy obie maszyny wirtualne korzystają z adresów w podsieci 10.10.10.0/24 hello i że one może wysyłać polecenia ping wzajemnie według nazwy. Można również użyć `ssh-keygen` i `ssh-copy-id` toomake się, że obie maszyny wirtualne mogą komunikować się za pośrednictwem SSH bez konieczności wprowadzania hasła.

### <a name="set-up-drbd"></a>Konfigurowanie DRBD
Utwórz zasób DRBD używającej bazowy hello `/dev/sdc1` partycji tooproduce `/dev/drbd1` zasobów, które mogą być sformatowane przy użyciu ext3 i używane w węzłach głównych i dodatkowych.

1. Otwórz `/etc/drbd.d/r0.res` i kopiowania powitania po definicji zasobu na obu maszynach wirtualnych:

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. Inicjowanie hello zasobów za pomocą `drbdadm` na obu maszynach wirtualnych:

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. Na hello podstawowej maszyny Wirtualnej (`hadb01`), wymusić własność (podstawowy) hello DRBD zasobów:

        sudo drbdadm primary --force r0

Jeśli należy zbadać zawartość hello/proc/drbd (`sudo cat /proc/drbd`) na obu maszynach wirtualnych, powinien zostać wyświetlony `Primary/Secondary` na `hadb01` i `Secondary/Primary` na `hadb02`, zgodnie z rozwiązania hello na tym etapie. Dysk 5 GB Hello są synchronizowane przez sieć 10.10.10.0/24 hello na toocustomers nie dodatkowych opłat.

Po zsynchronizowaniu hello dysku można utworzyć systemu plików hello na `hadb01`. Do celów testowych, użyliśmy ext2, ale hello następującego kodu utworzy ext3 systemu plików:

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a>Zainstaluj hello DRBD zasobów
Wszystko jest teraz gotowy toomount hello DRBD zasobów na `hadb01`. Użyj debian i pochodne `/var/lib/mysql` jako katalog danych na MySQL. Ponieważ nie zainstalowano MySQL, Utwórz katalog hello i zainstalować hello DRBD zasobów. tooperform tę opcję, uruchom hello następującego kodu `hadb01`:

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a>Konfigurowanie MySQL
Teraz możesz teraz gotowy tooinstall MySQL `hadb01`:

    sudo apt-get install mysql-server

Aby uzyskać `hadb02`, są dostępne dwie opcje. Można zainstalować mysql serwer, który będzie utworzyć /var/lib/mysql, wypełnienie nowy katalog danych, a następnie usuń zawartość hello. tooperform tę opcję, uruchom hello następującego kodu `hadb02`:

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

Druga opcja Hello jest zbyt toofailover`hadb02` , a następnie zainstaluj mysql serwer istnieje. Skrypty instalacyjne zauważyć hello istniejącej instalacji i nie będzie on touch.

Uruchom hello następujący kod na `hadb01`:

    sudo drbdadm secondary –force r0

Uruchom hello następujący kod na `hadb02`:

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

Jeśli nie planujesz teraz toofailover DRBD, pierwsza opcja hello jest łatwiejsze, ale raczej mniej elegancki. Po należy wybrać tę opcję, należy rozpocząć pracę nad bazy danych MySQL. Uruchom hello następujący kod na `hadb02` (lub jednego z tych serwerów hello jest aktywna, zgodnie z tooDRBD):

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> Tej ostatniej instrukcji wyłącza uwierzytelnianie dla użytkownika głównego hello w tej tabeli. To powinna zostać zastąpiona przez klasy produkcji PRZYZNAĆ instrukcje i jest dołączany wyłącznie w celach ilustracyjnych.

Jeśli chcesz toomake zapytania z maszyn wirtualnych poza hello, (co jest hello przeznaczenie tego przewodnika), należy również tooenable sieci dla programu MySQL. Na obu maszynach wirtualnych, należy otworzyć `/etc/mysql/my.cnf` i przejść za`bind-address`. Zmień adres hello z 127.0.0.1 too0.0.0.0. Po zapisaniu pliku hello, wystawiać `sudo service mysql restart` na serwerze podstawowym bieżącej.

### <a name="create-hello-mysql-load-balanced-set"></a>Utwórz zestaw o zrównoważonym obciążeniu MySQL hello
Wrócić do poprzedniej strony portalu toohello znajduje się zbyt`hadb01`i wybierz polecenie **punkty końcowe**. toocreate jako punkt końcowy, wybierz MySQL (TCP 3306) z listy rozwijanej hello i wybierz **zestaw o zrównoważonym obciążeniu nowe Utwórz**. Nazwa hello równoważeniem obciążenia punktu końcowego `lb-mysql`. Ustaw **czasu** sekund too5 minimalne.

Po utworzeniu punktu końcowego hello Przejdź zbyt`hadb02`, wybierz **punkty końcowe**i utworzyć punktu końcowego. Wybierz `lb-mysql`, a następnie wybierz z listy rozwijanej hello MySQL. Umożliwia także hello wiersza polecenia platformy Azure dla tego kroku.

Masz teraz wszystko, czego należy ręczne operacji hello klastra.

### <a name="test-hello-load-balanced-set"></a>Zestaw z równoważeniem obciążenia hello testowania
Za pomocą dowolnego klienta MySQL lub przy użyciu określonych aplikacji, takich jak phpMyAdmin uruchomione jako witryny sieci Web platformy Azure, można wykonać testy z poza maszyny. W tym przypadku użyto MySQL przez narzędzie wiersza polecenia w innym polu Linux:

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a>Ręcznie przechodzenie w tryb failover
Tryb failover można symulować zamykanie MySQL, przełączając DRBD w podstawowej i ponownie uruchomić MySQL.

tooperform to zadanie, uruchom hello następującego kodu na hadb01:

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

Następnie na hadb02:

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

Po przejścia w tryb failover ręcznie, można powtarzać zapytania zdalnego i powinien działać prawidłowo.

## <a name="set-up-corosync"></a>Konfigurowanie Corosync
Corosync jest hello wymagane dla toowork rozrusznik podstawowej infrastruktury klastra. Pulsu (i innych metod, takich jak Ultramonkey) Corosync jest podziału hello funkcji systemu CRM, rozrusznik pozostaje tooHeartbeat więcej podobnych funkcji.

Witaj głównym ograniczeniem dla Corosync na platformie Azure jest Corosync preferuje multiemisji za pośrednictwem emisji komunikacji emisji pojedynczej, że sieci Microsoft Azure obsługuje tylko emisji pojedynczej.

Na szczęście Corosync ma pracy tryb emisji pojedynczej. ograniczenie tylko rzeczywistego Hello jest, ponieważ wszystkie węzły nie komunikują się ze sobą, należy toodefine hello węzłów w plikach konfiguracji, w tym ich adresy IP. Możemy użyć hello Corosync przykład plików dla emisji pojedynczej i Zmień powiązanie adresu, węzeł listy i katalogi rejestrowania (używa Ubuntu `/var/log/corosync` podczas przykład Witaj pliki używają `/var/log/cluster`) i Włącz narzędzia kworum.

> [!NOTE]
> Użyj następujących hello `transport: udpu` dyrektywy i hello ręcznie zdefiniowanych adresów IP dla obu węzłów.

Uruchom hello następujący kod na `/etc/corosync/corosync.conf` dla obu węzłów:

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

Skopiuj ten plik konfiguracji na obu maszynach wirtualnych i uruchomić Corosync w obu węzłów:

    sudo service start corosync

Wkrótce po uruchomieniu usługi hello hello klastra należy ustanowić pierścienia bieżącego hello i kworum powinien zostać utworzony. Ta funkcja możemy można sprawdzić, przeglądając dzienniki lub uruchamiając hello następującego kodu:

    sudo corosync-quorumtool –l

Zostanie wyświetlony toohello podobne dane wyjściowe po obrazu:

![corosync quorumtool - l przykładowe dane wyjściowe](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a>Konfigurowanie rozrusznik
Używa rozrusznik hello toomonitor klastra dla zasobów, zdefiniuj, gdy kolory podstawowe przestaną działać i przełączanie toosecondaries tych zasobów. Można zdefiniować zasoby z zbiór dostępnych skryptów lub skryptów (init jak) najmniej znaczący BAJT, między innymi opcjami.

Chcemy rozrusznik zasobu DRBD zbyt "własnych" hello, hello punktu instalacji i hello usługi MySQL. Jeśli rozrusznik można włączać i wyłączać DRBD, zainstalować i Odinstaluj go i następnie uruchamiać i zatrzymywać MySQL w hello prawo zamówienia, gdy coś zły się dzieje z hello głównej, instalacja została ukończona.

Po zainstalowaniu rozrusznik konfiguracji powinna być prosta, coś, takich jak:

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. Sprawdź konfigurację hello uruchamiając `sudo crm configure show`.
2. Następnie utwórz plik (takie jak `/tmp/cluster.conf`) z hello następujące zasoby:

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. Załadowanie pliku hello do hello konfiguracji. Wystarczy toodo to w jednym węźle.

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. Upewnij się, że rozrusznik uruchomienie przy rozruchu w obu węzłów:

        sudo update-rc.d pacemaker defaults

5. Za pomocą `sudo crm_mon –L`, sprawdź, czy ma zostać wzorcem hello hello klastra jednego z węzłów i działa wszystkie zasoby hello. Możesz użyć instalacji i ps toocheck uruchomionych hello zasobów.

Zrzut ekranu przedstawia następujące Hello `crm_mon` z jednym węzłem zatrzymane (Zamknij wybierając klawisze Ctrl + C):

![węzeł crm_mon zatrzymana](./media/mysql-cluster/image002.png)

Ten zrzut ekranu przedstawia węzłów, jeden z nich i jeden podrzędny:

![crm_mon operacyjne wzorzec/podrzędny](./media/mysql-cluster/image003.png)

## <a name="testing"></a>Testowanie
Wszystko jest gotowe do symulacji automatycznej pracy awaryjnej. Istnieją dwa sposoby toodo to: elastyczne i.

Hello nietrwałego sposób funkcja klastra hello zamknięcia: ``crm_standby -U `uname -n` -v on``. Jeśli możesz użyć tego wzorca hello hello podrzędny ma. Pamiętaj, aby tooset tego toooff Wstecz. Jeśli nie zostanie crm_mon wyświetli jeden węzeł w stan wstrzymania.

Witaj twardych sposób Trwa zamykanie dół hello podstawowej maszyny Wirtualnej (hadb01) za pośrednictwem portalu hello lub zmieniając hello uruchamiania przełącznika/RL na powitania maszyny Wirtualnej (to znaczy zatrzymania, zamknięcia). Pomaga to Corosync i rozrusznik przez sygnalizowania będzie danego wzorca hello w dół. Można to sprawdzić (przydatne w przypadku okna obsługi), ale możesz też wymusić scenariusz hello zamrażanie hello maszyny Wirtualnej.

## <a name="stonith"></a>STONITH
Powinno być możliwe tooissue wyłączania maszyny Wirtualnej za pomocą hello Azure CLI zamiast STONITH skrypt, który kontroluje urządzenia fizycznego. Można użyć `/usr/lib/stonith/plugins/external/ssh` jako typu podstawowego i Włącz STONITH w konfiguracji klastra hello. Azure CLI powinien być zainstalowany globalnie i ustawienia publikowania hello i powinny być ładowane profilu dla użytkownika hello klastra.

Przykładowy kod dla zasobu hello jest dostępna w [GitHub](https://github.com/bureado/aztonith). Zmień konfigurację klastra hello przez dodanie powitania po zbyt`sudo crm configure`:

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> skrypt Hello nie wykonywać testy w górę lub w dół. Hello pierwotnego SSH zasobu były 15 kontroli ping, ale czas odzyskiwania dla maszyny Wirtualnej platformy Azure może być więcej zmiennej.

## <a name="limitations"></a>Ograniczenia
Zastosuj Hello następujące ograniczenia:

* Witaj linbit DRBD zasobów skrypt, który zarządza DRBD jako zasób w używa rozrusznik `drbdadm down` zamknięcia węzła, nawet jeśli węzeł hello właśnie przechodzi w stan wstrzymania. To nie jest idealny ponieważ hello podrzędny zostanie nie można synchronizowanie hello DRBD zasobów podczas wzorca hello pobiera zapisów. Jeśli wzorzec hello nie powiedzie się graciously, podrzędny hello może zająć ponad starsze stan systemu plików. Istnieją dwa sposoby potencjalnych rozwiązywania to:
  * Wymuszanie `drbdadm up r0` we wszystkich węzłach klastra za pośrednictwem lokalnego (nie clusterized) programu alarmowego
  * Edytowanie skryptu DRBD linbit hello, upewniając się, że `down` nie jest wywoływana`/usr/lib/ocf/resource.d/linbit/drbd`
* Hello modułu równoważenia obciążenia musi toorespond co najmniej pięć sekund, więc aplikacji powinien być typu cluster-aware i być bardziej odporne na limit czasu. Może również pomóc innych architektur, takich jak kolejki w aplikacji i middlewares zapytania.
* Dostrajanie MySQL jest konieczne tooensure, którą można wykonać zapisu w tempie można zarządzać i pamięci podręczne są wyczyszczone toodisk nawet toominimize możliwa utrata pamięci.
* Zapis wydajności jest zależna w maszynie Wirtualnej łączyć hello przełącznika wirtualnego, ponieważ jest używany przez urządzenie hello tooreplicate DRBD mechanizm hello.
