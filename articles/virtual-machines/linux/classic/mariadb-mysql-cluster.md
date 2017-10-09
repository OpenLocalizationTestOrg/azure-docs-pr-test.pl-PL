---
title: aaaRun MariaDB (MySQL) klastra na platformie Azure | Dokumentacja firmy Microsoft
description: "Utwórz MariaDB + Galera MySQL klastra na maszynach wirtualnych Azure"
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a>Klaster MariaDB (MySQL): samouczek platformy Azure
> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager](../../../resource-manager-deployment-model.md) i klasycznym. W tym artykule omówiono hello klasycznego modelu wdrażania. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu usługi Azure Resource Manager.

> [!NOTE]
> MariaDB Enterprise klastra jest teraz dostępna w hello Azure Marketplace. nową ofertę Hello automatycznie wdraża klaster MariaDB Galera na usługi Azure Resource Manager. Należy używać hello nową ofertę z [portalu Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).
>
>

W tym artykule opisano sposób toocreate wzorzec wielu [Galera](http://galeracluster.com/products/) klaster [MariaDBs](https://mariadb.org/en/about/) (zastępuje niezawodne, skalowalne i niezawodne dzięki wsuwanej konstrukcji MySQL) toowork w środowisku wysokiej dostępności na platformie Azure maszyny wirtualne.

## <a name="architecture-overview"></a>Omówienie architektury
W tym artykule opisano, jak hello toocomplete następujące kroki:

- Tworzenie klastra z trzema węzłami.
- Oddzielne hello dysków z danymi z hello dysku systemu operacyjnego.
- Tworzenie dysków danych hello w macierzy RAID-0/rozkładane ustawienie tooincrease IOPS.
- Moduł równoważenia obciążenia Azure toobalance hello obciążenia na użytek hello trzy węzły.
- toominimize powtarzających się działać, utworzyć obraz maszyny Wirtualnej, który zawiera MariaDB + Galera i użyć go toocreate hello innych maszyn wirtualnych klastra.

![Architektura systemu](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> W tym temacie używa hello [interfejsu wiersza polecenia Azure](../../../cli-install-nodejs.md) narzędzia, dlatego upewnij się, że toodownload je i podłącz je zgodnie z instrukcjami toohello tooyour subskrypcji platformy Azure. Jeśli potrzebujesz polecenia toohello odwołanie dostępne w hello Azure CLI, zobacz hello [Dokumentacja poleceń interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Należy również zbyt[Tworzenie klucza SSH do uwierzytelniania] i zanotuj lokalizację pliku PEM hello.
>
>

## <a name="create-hello-template"></a>Tworzenie szablonu hello
### <a name="infrastructure"></a>Infrastruktura
1. Utwórz zasoby hello toohold grupy koligacji razem.

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. Tworzenie sieci wirtualnej.

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. Tworzenie wszystkich naszych dysków toohost konta magazynu. Więcej niż 40 intensywnie używane dyski nie należy umieścić na powitania tego samego tooavoid konta magazynu, aktywując limitu konta magazynu IOPS hello 20 000. Możesz w tym przypadku znacznie poniżej ten limit, więc będą przechowywane wszystkie elementy na powitania tego samego konta dla uproszczenia.

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. Znajdź nazwę obrazu maszyny wirtualnej CentOS 7 hello hello.

        azure vm image list | findstr CentOS
   Witaj dane wyjściowe będą wyglądać mniej więcej tak `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.

   Użyj tej nazwy w powitania po kroku.
5. Utwórz szablon maszyny Wirtualnej hello i Zastąp /path/to/key.pem ścieżka hello przechowywania klucza SSH PEM hello wygenerowany.

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. Dołącz cztery 500 GB danych toohello dysków maszyny Wirtualnej do użytku w konfiguracji RAID hello.

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. Użyj SSH toosign toohello szablonu maszyny Wirtualnej, który został utworzony na mariadbhatemplate.cloudapp.net:22 i Połącz przy użyciu klucza prywatnego.

### <a name="software"></a>Oprogramowanie
1. Pobierz hello głównego.

        sudo su

2. Zainstaluj obsługę RAID:

    a. Zainstaluj mdadm.

              yum install mdadm

    b. Utwórz konfigurację RAID0/stripe hello EXT4 systemie plików.

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    c. Utworzyć katalogu punktu instalacji hello.

              mkdir /mnt/data
    d. Pobrać hello urządzenie RAID hello nowo utworzony identyfikator UUID.

              blkid | grep /dev/md0
    e. Edytuj /etc/fstab.

              vi /etc/fstab
    f. Dodaj automatycznie tooenable urządzenia hello instalowanie na ponowne uruchomienie komputera, zamieniając wartość hello hello UUID uzyskane z poprzednich hello **blkid** polecenia.

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    g. Zainstaluj hello nowej partycji.

              mount /mnt/data

3. Zainstaluj MariaDB.

    a. Utwórz plik MariaDB.repo hello.

                vi /etc/yum.repos.d/MariaDB.repo

    b. Wypełnienie pliku repozytorium hello hello następującej zawartości:

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    c. konflikty tooavoid, Usuń istniejące przyrostek i mariadb biblioteki.

           yum remove postfix mariadb-libs-*
    d. Zainstaluj MariaDB z Galera.

           yum install MariaDB-Galera-server MariaDB-client galera

4. Przenieś hello MySQL danych katalogu toohello RAID bloku urządzenia.

    a. Skopiuj bieżący katalog MySQL hello do nowej lokalizacji i Usuń katalog starego hello.

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    b. Ustawianie uprawnień dla nowego katalogu hello odpowiednio.

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    c. Tworzenie łącza symbolicznego, wskazujące hello starego katalogu toohello nową lokalizację na powitania partycji RAID.

           ln -s /mnt/data/mysql /var/lib/mysql

5. Ponieważ [SELinux zakłóca działanie klastra hello](http://galeracluster.com/documentation-webpages/configuration.html#selinux), jest konieczne toodisable na powitania bieżącej sesji. Edytuj `/etc/selinux/config` toodisable dla kolejnych ponownego uruchomienia.

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. Sprawdź poprawność uruchamia MySQL.

   a. Uruchom MySQL.

           service mysql start
   b. Secure hello MySQL instalacji, ustaw hasła głównego hello usunąć użytkowników anonimowych toodisable głównego zdalnego logowania i Usuń hello testowej bazy danych.

           mysql_secure_installation
   c. Utwórz użytkownika na powitania bazy danych, dla operacji klastra i opcjonalnie dla aplikacji.

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   d. Zatrzymaj MySQL.

            service mysql stop
7. Utwórz symbol zastępczy konfiguracji.

   a. Edytuj hello MySQL konfiguracji toocreate symbol zastępczy hello ustawienia klastra. Nie zastępuj hello  **`<Variables>`**  lub Usuń komentarz teraz. Które nastąpi po utworzeniu maszyny Wirtualnej za pomocą tego szablonu.

            vi /etc/my.cnf.d/server.cnf
   b. Edytuj hello  **[galera]**  sekcji i wyczyszczenie go.

   c. Edytuj hello **[mariadb]** sekcji.

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. Otwórz wymagane porty w zaporze hello przy użyciu FirewallD na CentOS 7.

   * MySQL:`firewall-cmd --zone=public --add-port=3306/tcp --permanent`
   * GALERA:`firewall-cmd --zone=public --add-port=4567/tcp --permanent`
   * GALERA IST:`firewall-cmd --zone=public --add-port=4568/tcp --permanent`
   * RSYNC:`firewall-cmd --zone=public --add-port=4444/tcp --permanent`
   * Załaduj ponownie hello zapory:`firewall-cmd --reload`

9. Optymalizacja wydajności hello systemu. Aby uzyskać więcej informacji, zobacz [strategii dostrajania wydajności](optimize-mysql.md).

   a. Edytuj plik konfiguracji MySQL hello ponownie.

            vi /etc/my.cnf.d/server.cnf
   b. Edytuj hello **[mariadb]** sekcji i Dołącz powitania po zawartości:

   > [!NOTE]
   > Firma Microsoft zaleca tego innodb\_buforu\_pool_size wynosi 70 procent pamięci maszyny Wirtualnej. W tym przykładzie ustawieniu co 2.45 GB dla średnich hello maszyny Wirtualnej platformy Azure w wersji 3.5 GB pamięci RAM.
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. Zatrzymaj MySQL, wyłącz usługi MySQL działania uruchamiania tooavoid zakłócania hello klastra podczas dodawania węzła i anulowanie zastrzeżenia hello maszyny.

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. Przechwyć hello maszyny Wirtualnej za pośrednictwem portalu hello. (Aktualnie [wystawiać &#1268; w narzędziach wiersza polecenia platformy Azure hello](https://github.com/Azure/azure-xplat-cli/issues/1268) opisuje obrazy przechwycone przez narzędzia wiersza polecenia platformy Azure hello nie należy przechwytywać hello dołączonych dysków z danymi faktów hello.)

    a. Zamknij maszynę hello za pośrednictwem portalu hello.

    b. Kliknij przycisk **przechwytywania** i określ nazwę obrazu hello jako **mariadb galera obrazu**. Podaj opis i sprawdź "Uruchomiono agenta waagent."
      
      ![Przechwytywanie maszyny wirtualnej hello](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a>Tworzenie klastra hello
Utworzyć trzy maszyny wirtualne za pomocą szablonu hello utworzone, a następnie skonfigurować i uruchomić hello klastra.

1. Utwórz hello pierwsza maszyna wirtualna 7 CentOS z hello w mariadb obrazu galera obrazu utworzonego, zapewniając hello następujących informacji:

 - Nazwa sieci wirtualnej: mariadbvnet
 - Podsieci: mariadb
 - Rozmiar maszyny: średni
 - Nazwa usługi w chmurze: mariadbha (lub nazwa ma toobe dostępne za pośrednictwem mariadbha.cloudapp.net)
 - Nazwa maszyny: mariadb1
 - Nazwa użytkownika: azureuser
 - Dostęp SSH: włączone
 - Przekazywanie pliku PEM certyfikatu SSH hello i zastępowanie /path/to/key.pem ze ścieżką hello przechowywania hello wygenerowany klucz SSH PEM.

   > [!NOTE]
   > Witaj następujące polecenia są podzielić na wiele wierszy z myślą o przejrzystości, ale należy wprowadzić jako jeden wiersz.
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. Utwórz dwie maszyny wirtualne więcej łącząc je usługi w chmurze mariadbha toohello. Zmień nazwę maszyny Wirtualnej hello i hello portu tooa unikatowy portu SSH nie powoduje konflikt z innych maszyn wirtualnych w hello tej samej usługi w chmurze.

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  Dla MariaDB3:

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. Tooget hello wewnętrzny adres IP każdego hello trzech maszyn wirtualnych będą potrzebne do następnego kroku hello:

    ![Pobieranie adresu IP](./media/mariadb-mysql-cluster/IP.png)
4. Użyj SSH toosign w toohello trzech maszyn wirtualnych i edycję pliku konfiguracyjnego hello na każdym z nich.

        sudo vi /etc/my.cnf.d/server.cnf

    Usuń znaczniki komentarza  **`wsrep_cluster_name`**  i  **`wsrep_cluster_address`**  przez usunięcie hello  **#**  na początku hello hello wiersza.
    Ponadto Zastąp  **`<ServerIP>`**  w  **`wsrep_node_address`**  i  **`<NodeName>`**  w  **`wsrep_node_name`**  z hello Maszyny Wirtualnej IP adres i nazwę odpowiednio i Usuń komentarz także te wiersze.
5. Uruchom klaster hello na MariaDB1 i pozwól mu uruchamiane automatycznie.

        sudo service mysql bootstrap
        chkconfig mysql on
6. Uruchom MySQL na MariaDB2 i MariaDB3 i pozwól mu uruchamiane automatycznie.

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a>Klaster hello równoważenia obciążenia
Po utworzeniu hello klastrowane maszyny wirtualne zostały dodane do zestawu dostępności o nazwie tooensure clusteravset, że zostały wprowadzone w różnych domenach awarii i aktualizacji i że Azure nigdy nie wykonuje konserwacji na wszystkich komputerach jednocześnie. Ta konfiguracja spełnia wymagania hello toobe obsługiwane przez hello Umowa dotycząca poziomu usług platformy Azure (SLA).

Teraz przy użyciu usługi równoważenia obciążenia Azure toobalance żądania między hello trzy węzły.

Uruchom następujące polecenia na komputerze przy użyciu interfejsu wiersza polecenia Azure hello hello.

Struktura parametrów polecenia Hello jest:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

Witaj CLI ustawia hello obciążenia modułu równoważenia sondowania interwał too15 sekund, które mogą być nieco zbyt długa. Zmienić w portalu hello w obszarze **punkty końcowe** dla dowolnego hello maszyn wirtualnych.

![Edytuj punktu końcowego](./media/mariadb-mysql-cluster/Endpoint.PNG)

Wybierz **hello ponownej konfiguracji ustawić Load-Balanced**.

![Skonfiguruj ponownie hello — zestaw o zrównoważonym obciążeniu](./media/mariadb-mysql-cluster/Endpoint2.PNG)

Zmień **interwał sondowania** too5 sekund i Zapisz zmiany.

![Interwał sondowania zmian](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a>Sprawdzanie poprawności klastra hello
Witaj twardych praca jest wykonywana. Witaj klastra powinna być teraz dostępne w `mariadbha.cloudapp.net:3306`, które trafienia hello modułu równoważenia obciążenia i trasy żądania między hello trzech maszyn wirtualnych bez problemów i wydajne.

Użyj Twoje ulubione tooconnect klienta MySQL lub połączyć się z jednego z hello tooverify maszyn wirtualnych, które działa ten klaster.

     mysql -u cluster -h mariadbha.cloudapp.net -p

Następnie utwórz bazę danych i wypełnić ją niektórych danych.

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

Hello bazy danych, który utworzono zwraca hello w poniższej tabeli:

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
W tym artykule tworzone MariaDB trzy + Galera klastra wysokiej dostępności na platformie Azure wirtualnych maszyn uruchomionych CentOS 7. maszyny wirtualne Hello jest równoważone z modułem równoważenia obciążenia w Azure.

Może być toolook w [inny sposób toocluster bazy danych MySQL na systemie Linux](mysql-cluster.md) i sposoby zbyt[optymalizacji i testowania wydajności MySQL na maszynach wirtualnych systemu Linux Azure](optimize-mysql.md).

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[Tworzenie klucza SSH do uwierzytelniania]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
