---
title: "aaaSet zapasową bazy danych MySQL na Maszynę wirtualną systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall hello MySQL stosu na maszynie wirtualnej systemu Linux (Ubuntu RedHat rodziny lub systemu operacyjnego) na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a>Jak tooinstall MySQL na platformie Azure
W tym artykule przedstawiono sposób tooinstall i skonfigurować MySQL na maszynie wirtualnej platformy Azure systemem Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a>Zainstaluj MySQL na maszynie wirtualnej
> [!NOTE]
> Musi już mieć maszyny wirtualnej Microsoft Azure z systemem Linux w kolejności toocomplete tego samouczka. Zobacz [samouczek maszyny Wirtualnej systemu Linux Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate i konfigurowanie maszyny Wirtualnej systemu Linux z `mysqlnode` jako nazwę maszyny Wirtualnej hello i `azureuser` jako użytkownika przed kontynuowaniem.
> 
> 

W takim przypadku należy użyć portu 3306 jako hello portu MySQL.  

Połącz toohello maszyny Wirtualnej systemu Linux utworzone przy użyciu programu putty. Jeśli jest to powitania po raz pierwszy używasz maszyny Wirtualnej systemu Linux platformy Azure, zobacz, jak toouse putty łączyć tooa maszyny Wirtualnej systemu Linux [tutaj](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Na przykład w tym artykule używamy repozytorium pakietu tooinstall MySQL5.6. W rzeczywistości MySQL5.6 ma więcej poprawy wydajności niż MySQL5.5.  Więcej informacji [tutaj](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).

### <a name="how-tooinstall-mysql56-on-ubuntu"></a>Jak tooinstall MySQL5.6 na Ubuntu
W tym miejscu użyjemy maszyny Wirtualnej systemu Linux z Ubuntu z platformy Azure.

* Krok 1: Instalacja MySQL serwera 5.6 przełącznika zbyt`root` użytkownika:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Instalowanie serwerów mysql 5.6:
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    Podczas instalacji, zobaczysz poping okno dialogowe się tooask tooset MySQL głównego hasłem poniżej, a należy ustawić hello hasło tutaj.
  
    ![Obraz](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    Hasło wejściowe hello tooconfirm ponownie.

    ![Obraz](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* Krok 2: Serwer MySQL logowania
  
    Po zakończeniu instalacji serwer MySQL, MySQL zostanie uruchomiona automatycznie. Możesz zalogować się serwer MySQL z `root` użytkownika.
    Użyj hello poniżej polecenia toologin i wprowadzania hasła.
  
             #[root@mysqlnode ~]# mysql -uroot -p
* Krok 3: Zarządzanie hello usługi MySQL
  
    () Pobierz stan usługi MySQL
  
             #[root@mysqlnode ~]# service mysql status
  
    (b) uruchomić usługi MySQL
  
             #[root@mysqlnode ~]# service mysql start
  
    (c) zatrzymać usługi MySQL
  
             #[root@mysqlnode ~]# service mysql stop
  
    (d) uruchom ponownie usługi MySQL hello
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a>Jak tooinstall MySQL na Red Hat rodziny jak CentOS, Oracle Linux
W tym miejscu użyjemy maszyny Wirtualnej systemu Linux CentOS lub Oracle Linux.

* Krok 1: Dodaj hello repozytorium MySQL Yum przełącznika zbyt`root` użytkownika:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Pobierz i zainstaluj pakiet zlecenia MySQL hello:
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* Krok 2: Edycja poniżej plik tooenable hello MySQL repozytorium pobieranie hello MySQL5.6 pakietu.
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    Zaktualizuj wartości toobelow tego pliku:
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* Krok 3: Zainstaluj MySQL z repozytorium MySQL zainstalować MySQL:
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    Zostanie zainstalowany pakiet MySQL RPM i wszystkich powiązanych pakietów.
* Krok 4: Zarządzanie hello usługi MySQL
  
    () sprawdź stan usługi hello hello MySQL serwera:
  
           #[root@mysqlnode ~]#service mysqld status
  
    (b) sprawdź, czy działa hello domyślnego portu MySQL serwera:
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    (c) serwer MySQL hello start:

           #[root@mysqlnode ~]#service mysqld start

    d Zatrzymaj serwer MySQL hello:

           #[root@mysqlnode ~]#service mysqld stop

    (e) Ustaw MySQL toostart przy rozruchu systemu hello w górę:

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a>Jak tooinstall MySQL w systemie SUSE Linux
W tym miejscu użyjemy maszyny Wirtualnej systemu Linux z OpenSUSE.

* Krok 1: Pobierz i zainstaluj serwer MySQL
  
    Przełącz zbyt`root` użytkownika za pomocą poniższych poleceń:  
  
           #sudo su -
  
    Pobierz i zainstaluj pakiet MySQL:
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* Krok 2: Zarządzanie hello usługi MySQL
  
    () sprawdź stan hello hello MySQL serwera:
  
           #[root@mysqlnode ~]# rcmysql status
  
    (b) sprawdź, czy hello domyślny numer portu serwera MySQL hello:
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    (c) serwer MySQL hello start:

           #[root@mysqlnode ~]# rcmysql start

    d Zatrzymaj serwer MySQL hello:

           #[root@mysqlnode ~]# rcmysql stop

    (e) Ustaw MySQL toostart przy rozruchu systemu hello w górę:

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a>Następny krok
Znajdź więcej użycia i informacje dotyczące MySQL [tutaj](https://www.mysql.com/).

