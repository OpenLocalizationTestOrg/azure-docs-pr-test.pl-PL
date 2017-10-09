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
# <a name="how-tooinstall-mysql-on-azure"></a><span data-ttu-id="e1a7f-103">Jak tooinstall MySQL na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e1a7f-103">How tooinstall MySQL on Azure</span></span>
<span data-ttu-id="e1a7f-104">W tym artykule przedstawiono sposób tooinstall i skonfigurować MySQL na maszynie wirtualnej platformy Azure systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-104">In this article, you will learn how tooinstall and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="e1a7f-105">Zainstaluj MySQL na maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e1a7f-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="e1a7f-106">Musi już mieć maszyny wirtualnej Microsoft Azure z systemem Linux w kolejności toocomplete tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-106">You must already have a Microsoft Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="e1a7f-107">Zobacz [samouczek maszyny Wirtualnej systemu Linux Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate i konfigurowanie maszyny Wirtualnej systemu Linux z `mysqlnode` jako nazwę maszyny Wirtualnej hello i `azureuser` jako użytkownika przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate and set up a Linux VM with `mysqlnode` as hello VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="e1a7f-108">W takim przypadku należy użyć portu 3306 jako hello portu MySQL.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-108">In this case, use 3306 port as hello MySQL port.</span></span>  

<span data-ttu-id="e1a7f-109">Połącz toohello maszyny Wirtualnej systemu Linux utworzone przy użyciu programu putty.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-109">Connect toohello Linux VM you created via putty.</span></span> <span data-ttu-id="e1a7f-110">Jeśli jest to powitania po raz pierwszy używasz maszyny Wirtualnej systemu Linux platformy Azure, zobacz, jak toouse putty łączyć tooa maszyny Wirtualnej systemu Linux [tutaj](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1a7f-110">If this is hello first time you use Azure Linux VM, see how toouse putty connect tooa Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e1a7f-111">Na przykład w tym artykule używamy repozytorium pakietu tooinstall MySQL5.6.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-111">We will use repository package tooinstall MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="e1a7f-112">W rzeczywistości MySQL5.6 ma więcej poprawy wydajności niż MySQL5.5.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="e1a7f-113">Więcej informacji [tutaj](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span><span class="sxs-lookup"><span data-stu-id="e1a7f-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-tooinstall-mysql56-on-ubuntu"></a><span data-ttu-id="e1a7f-114">Jak tooinstall MySQL5.6 na Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e1a7f-114">How tooinstall MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="e1a7f-115">W tym miejscu użyjemy maszyny Wirtualnej systemu Linux z Ubuntu z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="e1a7f-116">Krok 1: Instalacja MySQL serwera 5.6 przełącznika zbyt`root` użytkownika:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-116">Step 1: Install MySQL Server 5.6   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="e1a7f-117">Instalowanie serwerów mysql 5.6:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="e1a7f-118">Podczas instalacji, zobaczysz poping okno dialogowe się tooask tooset MySQL głównego hasłem poniżej, a należy ustawić hello hasło tutaj.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-118">During installation, you will see a dialog window poping up tooask you tooset MySQL root password below, and you need set hello password here.</span></span>
  
    ![Obraz](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="e1a7f-120">Hasło wejściowe hello tooconfirm ponownie.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-120">Input hello password again tooconfirm.</span></span>

    ![Obraz](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="e1a7f-122">Krok 2: Serwer MySQL logowania</span><span class="sxs-lookup"><span data-stu-id="e1a7f-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="e1a7f-123">Po zakończeniu instalacji serwer MySQL, MySQL zostanie uruchomiona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="e1a7f-124">Możesz zalogować się serwer MySQL z `root` użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="e1a7f-125">Użyj hello poniżej polecenia toologin i wprowadzania hasła.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-125">Use hello below command toologin and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="e1a7f-126">Krok 3: Zarządzanie hello usługi MySQL</span><span class="sxs-lookup"><span data-stu-id="e1a7f-126">Step 3: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="e1a7f-127">() Pobierz stan usługi MySQL</span><span class="sxs-lookup"><span data-stu-id="e1a7f-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="e1a7f-128">(b) uruchomić usługi MySQL</span><span class="sxs-lookup"><span data-stu-id="e1a7f-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="e1a7f-129">(c) zatrzymać usługi MySQL</span><span class="sxs-lookup"><span data-stu-id="e1a7f-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="e1a7f-130">(d) uruchom ponownie usługi MySQL hello</span><span class="sxs-lookup"><span data-stu-id="e1a7f-130">(d) Restart hello MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="e1a7f-131">Jak tooinstall MySQL na Red Hat rodziny jak CentOS, Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="e1a7f-131">How tooinstall MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="e1a7f-132">W tym miejscu użyjemy maszyny Wirtualnej systemu Linux CentOS lub Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="e1a7f-133">Krok 1: Dodaj hello repozytorium MySQL Yum przełącznika zbyt`root` użytkownika:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-133">Step 1: Add hello MySQL Yum repository   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="e1a7f-134">Pobierz i zainstaluj pakiet zlecenia MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-134">Download and install hello MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="e1a7f-135">Krok 2: Edycja poniżej plik tooenable hello MySQL repozytorium pobieranie hello MySQL5.6 pakietu.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-135">Step 2: Edit below file tooenable hello MySQL repository for downloading hello MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="e1a7f-136">Zaktualizuj wartości toobelow tego pliku:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-136">Update each value of this file toobelow:</span></span>
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="e1a7f-137">Krok 3: Zainstaluj MySQL z repozytorium MySQL zainstalować MySQL:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="e1a7f-138">Zostanie zainstalowany pakiet MySQL RPM i wszystkich powiązanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="e1a7f-139">Krok 4: Zarządzanie hello usługi MySQL</span><span class="sxs-lookup"><span data-stu-id="e1a7f-139">Step 4: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="e1a7f-140">() sprawdź stan usługi hello hello MySQL serwera:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-140">(a) Check hello service status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="e1a7f-141">(b) sprawdź, czy działa hello domyślnego portu MySQL serwera:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-141">(b) Check whether hello default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="e1a7f-142">(c) serwer MySQL hello start:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-142">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="e1a7f-143">d Zatrzymaj serwer MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-143">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="e1a7f-144">(e) Ustaw MySQL toostart przy rozruchu systemu hello w górę:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-144">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a><span data-ttu-id="e1a7f-145">Jak tooinstall MySQL w systemie SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="e1a7f-145">How tooinstall MySQL on SUSE Linux</span></span>
<span data-ttu-id="e1a7f-146">W tym miejscu użyjemy maszyny Wirtualnej systemu Linux z OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="e1a7f-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="e1a7f-147">Krok 1: Pobierz i zainstaluj serwer MySQL</span><span class="sxs-lookup"><span data-stu-id="e1a7f-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="e1a7f-148">Przełącz zbyt`root` użytkownika za pomocą poniższych poleceń:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-148">Switch too`root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="e1a7f-149">Pobierz i zainstaluj pakiet MySQL:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="e1a7f-150">Krok 2: Zarządzanie hello usługi MySQL</span><span class="sxs-lookup"><span data-stu-id="e1a7f-150">Step 2: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="e1a7f-151">() sprawdź stan hello hello MySQL serwera:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-151">(a) Check hello status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="e1a7f-152">(b) sprawdź, czy hello domyślny numer portu serwera MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-152">(b) Check whether hello default port of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="e1a7f-153">(c) serwer MySQL hello start:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-153">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="e1a7f-154">d Zatrzymaj serwer MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-154">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="e1a7f-155">(e) Ustaw MySQL toostart przy rozruchu systemu hello w górę:</span><span class="sxs-lookup"><span data-stu-id="e1a7f-155">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="e1a7f-156">Następny krok</span><span class="sxs-lookup"><span data-stu-id="e1a7f-156">Next Step</span></span>
<span data-ttu-id="e1a7f-157">Znajdź więcej użycia i informacje dotyczące MySQL [tutaj](https://www.mysql.com/).</span><span class="sxs-lookup"><span data-stu-id="e1a7f-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

