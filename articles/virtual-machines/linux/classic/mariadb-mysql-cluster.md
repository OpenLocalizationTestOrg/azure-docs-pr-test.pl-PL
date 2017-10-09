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
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="95a7c-103">Klaster MariaDB (MySQL): samouczek platformy Azure</span><span class="sxs-lookup"><span data-stu-id="95a7c-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="95a7c-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager](../../../resource-manager-deployment-model.md) i klasycznym.</span><span class="sxs-lookup"><span data-stu-id="95a7c-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="95a7c-105">W tym artykule omówiono hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="95a7c-105">This article covers hello classic deployment model.</span></span> <span data-ttu-id="95a7c-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="95a7c-106">Microsoft recommends that most new deployments use hello Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="95a7c-107">MariaDB Enterprise klastra jest teraz dostępna w hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="95a7c-107">MariaDB Enterprise cluster is now available in hello Azure Marketplace.</span></span> <span data-ttu-id="95a7c-108">nową ofertę Hello automatycznie wdraża klaster MariaDB Galera na usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="95a7c-108">hello new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="95a7c-109">Należy używać hello nową ofertę z [portalu Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="95a7c-109">You should use hello new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="95a7c-110">W tym artykule opisano sposób toocreate wzorzec wielu [Galera](http://galeracluster.com/products/) klaster [MariaDBs](https://mariadb.org/en/about/) (zastępuje niezawodne, skalowalne i niezawodne dzięki wsuwanej konstrukcji MySQL) toowork w środowisku wysokiej dostępności na platformie Azure maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="95a7c-110">This article shows you how toocreate a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) toowork in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="95a7c-111">Omówienie architektury</span><span class="sxs-lookup"><span data-stu-id="95a7c-111">Architecture overview</span></span>
<span data-ttu-id="95a7c-112">W tym artykule opisano, jak hello toocomplete następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="95a7c-112">This article describes how toocomplete hello following steps:</span></span>

- <span data-ttu-id="95a7c-113">Tworzenie klastra z trzema węzłami.</span><span class="sxs-lookup"><span data-stu-id="95a7c-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="95a7c-114">Oddzielne hello dysków z danymi z hello dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="95a7c-114">Separate hello data disks from hello OS disk.</span></span>
- <span data-ttu-id="95a7c-115">Tworzenie dysków danych hello w macierzy RAID-0/rozkładane ustawienie tooincrease IOPS.</span><span class="sxs-lookup"><span data-stu-id="95a7c-115">Create hello data disks in RAID-0/striped setting tooincrease IOPS.</span></span>
- <span data-ttu-id="95a7c-116">Moduł równoważenia obciążenia Azure toobalance hello obciążenia na użytek hello trzy węzły.</span><span class="sxs-lookup"><span data-stu-id="95a7c-116">Use Azure Load Balancer toobalance hello load for hello three nodes.</span></span>
- <span data-ttu-id="95a7c-117">toominimize powtarzających się działać, utworzyć obraz maszyny Wirtualnej, który zawiera MariaDB + Galera i użyć go toocreate hello innych maszyn wirtualnych klastra.</span><span class="sxs-lookup"><span data-stu-id="95a7c-117">toominimize repetitive work, create a VM image that contains MariaDB + Galera and use it toocreate hello other cluster VMs.</span></span>

![Architektura systemu](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="95a7c-119">W tym temacie używa hello [interfejsu wiersza polecenia Azure](../../../cli-install-nodejs.md) narzędzia, dlatego upewnij się, że toodownload je i podłącz je zgodnie z instrukcjami toohello tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="95a7c-119">This topic uses hello [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure toodownload them and connect them tooyour Azure subscription according toohello instructions.</span></span> <span data-ttu-id="95a7c-120">Jeśli potrzebujesz polecenia toohello odwołanie dostępne w hello Azure CLI, zobacz hello [Dokumentacja poleceń interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="95a7c-120">If you need a reference toohello commands available in hello Azure CLI, see hello [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="95a7c-121">Należy również zbyt[Tworzenie klucza SSH do uwierzytelniania] i zanotuj lokalizację pliku PEM hello.</span><span class="sxs-lookup"><span data-stu-id="95a7c-121">You will also need too[create an SSH key for authentication] and make note of hello .pem file location.</span></span>
>
>

## <a name="create-hello-template"></a><span data-ttu-id="95a7c-122">Tworzenie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="95a7c-122">Create hello template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="95a7c-123">Infrastruktura</span><span class="sxs-lookup"><span data-stu-id="95a7c-123">Infrastructure</span></span>
1. <span data-ttu-id="95a7c-124">Utwórz zasoby hello toohold grupy koligacji razem.</span><span class="sxs-lookup"><span data-stu-id="95a7c-124">Create an affinity group toohold hello resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="95a7c-125">Tworzenie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95a7c-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="95a7c-126">Tworzenie wszystkich naszych dysków toohost konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="95a7c-126">Create a storage account toohost all our disks.</span></span> <span data-ttu-id="95a7c-127">Więcej niż 40 intensywnie używane dyski nie należy umieścić na powitania tego samego tooavoid konta magazynu, aktywując limitu konta magazynu IOPS hello 20 000.</span><span class="sxs-lookup"><span data-stu-id="95a7c-127">You shouldn't place more than 40 heavily used disks on hello same storage account tooavoid hitting hello 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="95a7c-128">Możesz w tym przypadku znacznie poniżej ten limit, więc będą przechowywane wszystkie elementy na powitania tego samego konta dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="95a7c-128">In this case, you're well below that limit, so you'll store everything on hello same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="95a7c-129">Znajdź nazwę obrazu maszyny wirtualnej CentOS 7 hello hello.</span><span class="sxs-lookup"><span data-stu-id="95a7c-129">Find hello name of hello CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="95a7c-130">Witaj dane wyjściowe będą wyglądać mniej więcej tak `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="95a7c-130">hello output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="95a7c-131">Użyj tej nazwy w powitania po kroku.</span><span class="sxs-lookup"><span data-stu-id="95a7c-131">Use that name in hello following step.</span></span>
5. <span data-ttu-id="95a7c-132">Utwórz szablon maszyny Wirtualnej hello i Zastąp /path/to/key.pem ścieżka hello przechowywania klucza SSH PEM hello wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="95a7c-132">Create hello VM template and replace /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="95a7c-133">Dołącz cztery 500 GB danych toohello dysków maszyny Wirtualnej do użytku w konfiguracji RAID hello.</span><span class="sxs-lookup"><span data-stu-id="95a7c-133">Attach four 500-GB data disks toohello VM for use in hello RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="95a7c-134">Użyj SSH toosign toohello szablonu maszyny Wirtualnej, który został utworzony na mariadbhatemplate.cloudapp.net:22 i Połącz przy użyciu klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="95a7c-134">Use SSH toosign in toohello template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="95a7c-135">Oprogramowanie</span><span class="sxs-lookup"><span data-stu-id="95a7c-135">Software</span></span>
1. <span data-ttu-id="95a7c-136">Pobierz hello głównego.</span><span class="sxs-lookup"><span data-stu-id="95a7c-136">Get hello root.</span></span>

        sudo su

2. <span data-ttu-id="95a7c-137">Zainstaluj obsługę RAID:</span><span class="sxs-lookup"><span data-stu-id="95a7c-137">Install RAID support:</span></span>

    <span data-ttu-id="95a7c-138">a.</span><span class="sxs-lookup"><span data-stu-id="95a7c-138">a.</span></span> <span data-ttu-id="95a7c-139">Zainstaluj mdadm.</span><span class="sxs-lookup"><span data-stu-id="95a7c-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="95a7c-140">b.</span><span class="sxs-lookup"><span data-stu-id="95a7c-140">b.</span></span> <span data-ttu-id="95a7c-141">Utwórz konfigurację RAID0/stripe hello EXT4 systemie plików.</span><span class="sxs-lookup"><span data-stu-id="95a7c-141">Create hello RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="95a7c-142">c.</span><span class="sxs-lookup"><span data-stu-id="95a7c-142">c.</span></span> <span data-ttu-id="95a7c-143">Utworzyć katalogu punktu instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="95a7c-143">Create hello mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="95a7c-144">d.</span><span class="sxs-lookup"><span data-stu-id="95a7c-144">d.</span></span> <span data-ttu-id="95a7c-145">Pobrać hello urządzenie RAID hello nowo utworzony identyfikator UUID.</span><span class="sxs-lookup"><span data-stu-id="95a7c-145">Retrieve hello UUID of hello newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="95a7c-146">e.</span><span class="sxs-lookup"><span data-stu-id="95a7c-146">e.</span></span> <span data-ttu-id="95a7c-147">Edytuj /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="95a7c-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="95a7c-148">f.</span><span class="sxs-lookup"><span data-stu-id="95a7c-148">f.</span></span> <span data-ttu-id="95a7c-149">Dodaj automatycznie tooenable urządzenia hello instalowanie na ponowne uruchomienie komputera, zamieniając wartość hello hello UUID uzyskane z poprzednich hello **blkid** polecenia.</span><span class="sxs-lookup"><span data-stu-id="95a7c-149">Add hello device tooenable auto mounting on reboot, replacing hello UUID with hello value obtained from hello previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="95a7c-150">g.</span><span class="sxs-lookup"><span data-stu-id="95a7c-150">g.</span></span> <span data-ttu-id="95a7c-151">Zainstaluj hello nowej partycji.</span><span class="sxs-lookup"><span data-stu-id="95a7c-151">Mount hello new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="95a7c-152">Zainstaluj MariaDB.</span><span class="sxs-lookup"><span data-stu-id="95a7c-152">Install MariaDB.</span></span>

    <span data-ttu-id="95a7c-153">a.</span><span class="sxs-lookup"><span data-stu-id="95a7c-153">a.</span></span> <span data-ttu-id="95a7c-154">Utwórz plik MariaDB.repo hello.</span><span class="sxs-lookup"><span data-stu-id="95a7c-154">Create hello MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="95a7c-155">b.</span><span class="sxs-lookup"><span data-stu-id="95a7c-155">b.</span></span> <span data-ttu-id="95a7c-156">Wypełnienie pliku repozytorium hello hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="95a7c-156">Fill hello repo file with hello following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="95a7c-157">c.</span><span class="sxs-lookup"><span data-stu-id="95a7c-157">c.</span></span> <span data-ttu-id="95a7c-158">konflikty tooavoid, Usuń istniejące przyrostek i mariadb biblioteki.</span><span class="sxs-lookup"><span data-stu-id="95a7c-158">tooavoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="95a7c-159">d.</span><span class="sxs-lookup"><span data-stu-id="95a7c-159">d.</span></span> <span data-ttu-id="95a7c-160">Zainstaluj MariaDB z Galera.</span><span class="sxs-lookup"><span data-stu-id="95a7c-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="95a7c-161">Przenieś hello MySQL danych katalogu toohello RAID bloku urządzenia.</span><span class="sxs-lookup"><span data-stu-id="95a7c-161">Move hello MySQL data directory toohello RAID block device.</span></span>

    <span data-ttu-id="95a7c-162">a.</span><span class="sxs-lookup"><span data-stu-id="95a7c-162">a.</span></span> <span data-ttu-id="95a7c-163">Skopiuj bieżący katalog MySQL hello do nowej lokalizacji i Usuń katalog starego hello.</span><span class="sxs-lookup"><span data-stu-id="95a7c-163">Copy hello current MySQL directory into its new location and remove hello old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="95a7c-164">b.</span><span class="sxs-lookup"><span data-stu-id="95a7c-164">b.</span></span> <span data-ttu-id="95a7c-165">Ustawianie uprawnień dla nowego katalogu hello odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="95a7c-165">Set permissions for hello new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="95a7c-166">c.</span><span class="sxs-lookup"><span data-stu-id="95a7c-166">c.</span></span> <span data-ttu-id="95a7c-167">Tworzenie łącza symbolicznego, wskazujące hello starego katalogu toohello nową lokalizację na powitania partycji RAID.</span><span class="sxs-lookup"><span data-stu-id="95a7c-167">Create a symlink that points hello old directory toohello new location on hello RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="95a7c-168">Ponieważ [SELinux zakłóca działanie klastra hello](http://galeracluster.com/documentation-webpages/configuration.html#selinux), jest konieczne toodisable na powitania bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="95a7c-168">Because [SELinux interferes with hello cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary toodisable it for hello current session.</span></span> <span data-ttu-id="95a7c-169">Edytuj `/etc/selinux/config` toodisable dla kolejnych ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="95a7c-169">Edit `/etc/selinux/config` toodisable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. <span data-ttu-id="95a7c-170">Sprawdź poprawność uruchamia MySQL.</span><span class="sxs-lookup"><span data-stu-id="95a7c-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="95a7c-171">a.</span><span class="sxs-lookup"><span data-stu-id="95a7c-171">a.</span></span> <span data-ttu-id="95a7c-172">Uruchom MySQL.</span><span class="sxs-lookup"><span data-stu-id="95a7c-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="95a7c-173">b.</span><span class="sxs-lookup"><span data-stu-id="95a7c-173">b.</span></span> <span data-ttu-id="95a7c-174">Secure hello MySQL instalacji, ustaw hasła głównego hello usunąć użytkowników anonimowych toodisable głównego zdalnego logowania i Usuń hello testowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="95a7c-174">Secure hello MySQL installation, set hello root password, remove anonymous users toodisable remote root login, and remove hello test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="95a7c-175">c.</span><span class="sxs-lookup"><span data-stu-id="95a7c-175">c.</span></span> <span data-ttu-id="95a7c-176">Utwórz użytkownika na powitania bazy danych, dla operacji klastra i opcjonalnie dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="95a7c-176">Create a user on hello database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="95a7c-177">d.</span><span class="sxs-lookup"><span data-stu-id="95a7c-177">d.</span></span> <span data-ttu-id="95a7c-178">Zatrzymaj MySQL.</span><span class="sxs-lookup"><span data-stu-id="95a7c-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="95a7c-179">Utwórz symbol zastępczy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="95a7c-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="95a7c-180">a.</span><span class="sxs-lookup"><span data-stu-id="95a7c-180">a.</span></span> <span data-ttu-id="95a7c-181">Edytuj hello MySQL konfiguracji toocreate symbol zastępczy hello ustawienia klastra.</span><span class="sxs-lookup"><span data-stu-id="95a7c-181">Edit hello MySQL configuration toocreate a placeholder for hello cluster settings.</span></span> <span data-ttu-id="95a7c-182">Nie zastępuj hello  **`<Variables>`**  lub Usuń komentarz teraz.</span><span class="sxs-lookup"><span data-stu-id="95a7c-182">Do not replace hello **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="95a7c-183">Które nastąpi po utworzeniu maszyny Wirtualnej za pomocą tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="95a7c-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="95a7c-184">b.</span><span class="sxs-lookup"><span data-stu-id="95a7c-184">b.</span></span> <span data-ttu-id="95a7c-185">Edytuj hello  **[galera]**  sekcji i wyczyszczenie go.</span><span class="sxs-lookup"><span data-stu-id="95a7c-185">Edit hello **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="95a7c-186">c.</span><span class="sxs-lookup"><span data-stu-id="95a7c-186">c.</span></span> <span data-ttu-id="95a7c-187">Edytuj hello **[mariadb]** sekcji.</span><span class="sxs-lookup"><span data-stu-id="95a7c-187">Edit hello **[mariadb]** section.</span></span>

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
8. <span data-ttu-id="95a7c-188">Otwórz wymagane porty w zaporze hello przy użyciu FirewallD na CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="95a7c-188">Open required ports on hello firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="95a7c-189">MySQL:`firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="95a7c-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="95a7c-190">GALERA:`firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="95a7c-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="95a7c-191">GALERA IST:`firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="95a7c-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="95a7c-192">RSYNC:`firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="95a7c-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="95a7c-193">Załaduj ponownie hello zapory:`firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="95a7c-193">Reload hello firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="95a7c-194">Optymalizacja wydajności hello systemu.</span><span class="sxs-lookup"><span data-stu-id="95a7c-194">Optimize hello system for performance.</span></span> <span data-ttu-id="95a7c-195">Aby uzyskać więcej informacji, zobacz [strategii dostrajania wydajności](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="95a7c-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="95a7c-196">a.</span><span class="sxs-lookup"><span data-stu-id="95a7c-196">a.</span></span> <span data-ttu-id="95a7c-197">Edytuj plik konfiguracji MySQL hello ponownie.</span><span class="sxs-lookup"><span data-stu-id="95a7c-197">Edit hello MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="95a7c-198">b.</span><span class="sxs-lookup"><span data-stu-id="95a7c-198">b.</span></span> <span data-ttu-id="95a7c-199">Edytuj hello **[mariadb]** sekcji i Dołącz powitania po zawartości:</span><span class="sxs-lookup"><span data-stu-id="95a7c-199">Edit hello **[mariadb]** section and append hello following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="95a7c-200">Firma Microsoft zaleca tego innodb\_buforu\_pool_size wynosi 70 procent pamięci maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="95a7c-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="95a7c-201">W tym przykładzie ustawieniu co 2.45 GB dla średnich hello maszyny Wirtualnej platformy Azure w wersji 3.5 GB pamięci RAM.</span><span class="sxs-lookup"><span data-stu-id="95a7c-201">In this example, it has been set at 2.45 GB for hello medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="95a7c-202">Zatrzymaj MySQL, wyłącz usługi MySQL działania uruchamiania tooavoid zakłócania hello klastra podczas dodawania węzła i anulowanie zastrzeżenia hello maszyny.</span><span class="sxs-lookup"><span data-stu-id="95a7c-202">Stop MySQL, disable MySQL service from running on startup tooavoid disrupting hello cluster when adding a node, and deprovision hello machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="95a7c-203">Przechwyć hello maszyny Wirtualnej za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="95a7c-203">Capture hello VM through hello portal.</span></span> <span data-ttu-id="95a7c-204">(Aktualnie [wystawiać &#1268; w narzędziach wiersza polecenia platformy Azure hello](https://github.com/Azure/azure-xplat-cli/issues/1268) opisuje obrazy przechwycone przez narzędzia wiersza polecenia platformy Azure hello nie należy przechwytywać hello dołączonych dysków z danymi faktów hello.)</span><span class="sxs-lookup"><span data-stu-id="95a7c-204">(Currently, [issue #1268 in hello Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes hello fact that images captured by hello Azure CLI tools do not capture hello attached data disks.)</span></span>

    <span data-ttu-id="95a7c-205">a.</span><span class="sxs-lookup"><span data-stu-id="95a7c-205">a.</span></span> <span data-ttu-id="95a7c-206">Zamknij maszynę hello za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="95a7c-206">Shut down hello machine through hello portal.</span></span>

    <span data-ttu-id="95a7c-207">b.</span><span class="sxs-lookup"><span data-stu-id="95a7c-207">b.</span></span> <span data-ttu-id="95a7c-208">Kliknij przycisk **przechwytywania** i określ nazwę obrazu hello jako **mariadb galera obrazu**.</span><span class="sxs-lookup"><span data-stu-id="95a7c-208">Click **Capture** and specify hello image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="95a7c-209">Podaj opis i sprawdź "Uruchomiono agenta waagent."</span><span class="sxs-lookup"><span data-stu-id="95a7c-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Przechwytywanie maszyny wirtualnej hello](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a><span data-ttu-id="95a7c-211">Tworzenie klastra hello</span><span class="sxs-lookup"><span data-stu-id="95a7c-211">Create hello cluster</span></span>
<span data-ttu-id="95a7c-212">Utworzyć trzy maszyny wirtualne za pomocą szablonu hello utworzone, a następnie skonfigurować i uruchomić hello klastra.</span><span class="sxs-lookup"><span data-stu-id="95a7c-212">Create three VMs with hello template you created, and then configure and start hello cluster.</span></span>

1. <span data-ttu-id="95a7c-213">Utwórz hello pierwsza maszyna wirtualna 7 CentOS z hello w mariadb obrazu galera obrazu utworzonego, zapewniając hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="95a7c-213">Create hello first CentOS 7 VM from hello mariadb-galera-image image you created, providing hello following information:</span></span>

 - <span data-ttu-id="95a7c-214">Nazwa sieci wirtualnej: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="95a7c-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="95a7c-215">Podsieci: mariadb</span><span class="sxs-lookup"><span data-stu-id="95a7c-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="95a7c-216">Rozmiar maszyny: średni</span><span class="sxs-lookup"><span data-stu-id="95a7c-216">Machine size: medium</span></span>
 - <span data-ttu-id="95a7c-217">Nazwa usługi w chmurze: mariadbha (lub nazwa ma toobe dostępne za pośrednictwem mariadbha.cloudapp.net)</span><span class="sxs-lookup"><span data-stu-id="95a7c-217">Cloud service name: mariadbha (or whatever name you want toobe accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="95a7c-218">Nazwa maszyny: mariadb1</span><span class="sxs-lookup"><span data-stu-id="95a7c-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="95a7c-219">Nazwa użytkownika: azureuser</span><span class="sxs-lookup"><span data-stu-id="95a7c-219">Username: azureuser</span></span>
 - <span data-ttu-id="95a7c-220">Dostęp SSH: włączone</span><span class="sxs-lookup"><span data-stu-id="95a7c-220">SSH access: enabled</span></span>
 - <span data-ttu-id="95a7c-221">Przekazywanie pliku PEM certyfikatu SSH hello i zastępowanie /path/to/key.pem ze ścieżką hello przechowywania hello wygenerowany klucz SSH PEM.</span><span class="sxs-lookup"><span data-stu-id="95a7c-221">Passing hello SSH certificate .pem file and replacing /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="95a7c-222">Witaj następujące polecenia są podzielić na wiele wierszy z myślą o przejrzystości, ale należy wprowadzić jako jeden wiersz.</span><span class="sxs-lookup"><span data-stu-id="95a7c-222">hello following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
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
2. <span data-ttu-id="95a7c-223">Utwórz dwie maszyny wirtualne więcej łącząc je usługi w chmurze mariadbha toohello.</span><span class="sxs-lookup"><span data-stu-id="95a7c-223">Create two more virtual machines by connecting them toohello mariadbha cloud service.</span></span> <span data-ttu-id="95a7c-224">Zmień nazwę maszyny Wirtualnej hello i hello portu tooa unikatowy portu SSH nie powoduje konflikt z innych maszyn wirtualnych w hello tej samej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="95a7c-224">Change hello VM name and hello SSH port tooa unique port not conflicting with other VMs in hello same cloud service.</span></span>

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
  <span data-ttu-id="95a7c-225">Dla MariaDB3:</span><span class="sxs-lookup"><span data-stu-id="95a7c-225">For MariaDB3:</span></span>

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
3. <span data-ttu-id="95a7c-226">Tooget hello wewnętrzny adres IP każdego hello trzech maszyn wirtualnych będą potrzebne do następnego kroku hello:</span><span class="sxs-lookup"><span data-stu-id="95a7c-226">You will need tooget hello internal IP address of each of hello three VMs for hello next step:</span></span>

    ![Pobieranie adresu IP](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="95a7c-228">Użyj SSH toosign w toohello trzech maszyn wirtualnych i edycję pliku konfiguracyjnego hello na każdym z nich.</span><span class="sxs-lookup"><span data-stu-id="95a7c-228">Use SSH toosign in toohello three VMs and edit hello configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="95a7c-229">Usuń znaczniki komentarza  **`wsrep_cluster_name`**  i  **`wsrep_cluster_address`**  przez usunięcie hello  **#**  na początku hello hello wiersza.</span><span class="sxs-lookup"><span data-stu-id="95a7c-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing hello **#** at hello beginning of hello line.</span></span>
    <span data-ttu-id="95a7c-230">Ponadto Zastąp  **`<ServerIP>`**  w  **`wsrep_node_address`**  i  **`<NodeName>`**  w  **`wsrep_node_name`**  z hello Maszyny Wirtualnej IP adres i nazwę odpowiednio i Usuń komentarz także te wiersze.</span><span class="sxs-lookup"><span data-stu-id="95a7c-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with hello VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="95a7c-231">Uruchom klaster hello na MariaDB1 i pozwól mu uruchamiane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="95a7c-231">Start hello cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="95a7c-232">Uruchom MySQL na MariaDB2 i MariaDB3 i pozwól mu uruchamiane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="95a7c-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a><span data-ttu-id="95a7c-233">Klaster hello równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="95a7c-233">Load balance hello cluster</span></span>
<span data-ttu-id="95a7c-234">Po utworzeniu hello klastrowane maszyny wirtualne zostały dodane do zestawu dostępności o nazwie tooensure clusteravset, że zostały wprowadzone w różnych domenach awarii i aktualizacji i że Azure nigdy nie wykonuje konserwacji na wszystkich komputerach jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="95a7c-234">When you created hello clustered VMs, you added them into an availability set called clusteravset tooensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="95a7c-235">Ta konfiguracja spełnia wymagania hello toobe obsługiwane przez hello Umowa dotycząca poziomu usług platformy Azure (SLA).</span><span class="sxs-lookup"><span data-stu-id="95a7c-235">This configuration meets hello requirements toobe supported by hello Azure service level agreement (SLA).</span></span>

<span data-ttu-id="95a7c-236">Teraz przy użyciu usługi równoważenia obciążenia Azure toobalance żądania między hello trzy węzły.</span><span class="sxs-lookup"><span data-stu-id="95a7c-236">Now use Azure Load Balancer toobalance requests between hello three nodes.</span></span>

<span data-ttu-id="95a7c-237">Uruchom następujące polecenia na komputerze przy użyciu interfejsu wiersza polecenia Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="95a7c-237">Run hello following commands on your machine by using hello Azure CLI.</span></span>

<span data-ttu-id="95a7c-238">Struktura parametrów polecenia Hello jest:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="95a7c-238">hello command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="95a7c-239">Witaj CLI ustawia hello obciążenia modułu równoważenia sondowania interwał too15 sekund, które mogą być nieco zbyt długa.</span><span class="sxs-lookup"><span data-stu-id="95a7c-239">hello CLI sets hello load balancer probe interval too15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="95a7c-240">Zmienić w portalu hello w obszarze **punkty końcowe** dla dowolnego hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="95a7c-240">Change it in hello portal under **Endpoints** for any of hello VMs.</span></span>

![Edytuj punktu końcowego](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="95a7c-242">Wybierz **hello ponownej konfiguracji ustawić Load-Balanced**.</span><span class="sxs-lookup"><span data-stu-id="95a7c-242">Select **Reconfigure hello Load-Balanced Set**.</span></span>

![Skonfiguruj ponownie hello — zestaw o zrównoważonym obciążeniu](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="95a7c-244">Zmień **interwał sondowania** too5 sekund i Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="95a7c-244">Change **Probe Interval** too5 seconds and save your changes.</span></span>

![Interwał sondowania zmian](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a><span data-ttu-id="95a7c-246">Sprawdzanie poprawności klastra hello</span><span class="sxs-lookup"><span data-stu-id="95a7c-246">Validate hello cluster</span></span>
<span data-ttu-id="95a7c-247">Witaj twardych praca jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="95a7c-247">hello hard work is done.</span></span> <span data-ttu-id="95a7c-248">Witaj klastra powinna być teraz dostępne w `mariadbha.cloudapp.net:3306`, które trafienia hello modułu równoważenia obciążenia i trasy żądania między hello trzech maszyn wirtualnych bez problemów i wydajne.</span><span class="sxs-lookup"><span data-stu-id="95a7c-248">hello cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits hello load balancer and route requests between hello three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="95a7c-249">Użyj Twoje ulubione tooconnect klienta MySQL lub połączyć się z jednego z hello tooverify maszyn wirtualnych, które działa ten klaster.</span><span class="sxs-lookup"><span data-stu-id="95a7c-249">Use your favorite MySQL client tooconnect, or connect from one of hello VMs tooverify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="95a7c-250">Następnie utwórz bazę danych i wypełnić ją niektórych danych.</span><span class="sxs-lookup"><span data-stu-id="95a7c-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="95a7c-251">Hello bazy danych, który utworzono zwraca hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="95a7c-251">hello database you created returns hello following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="95a7c-252">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="95a7c-252">Next steps</span></span>
<span data-ttu-id="95a7c-253">W tym artykule tworzone MariaDB trzy + Galera klastra wysokiej dostępności na platformie Azure wirtualnych maszyn uruchomionych CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="95a7c-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="95a7c-254">maszyny wirtualne Hello jest równoważone z modułem równoważenia obciążenia w Azure.</span><span class="sxs-lookup"><span data-stu-id="95a7c-254">hello VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="95a7c-255">Może być toolook w [inny sposób toocluster bazy danych MySQL na systemie Linux](mysql-cluster.md) i sposoby zbyt[optymalizacji i testowania wydajności MySQL na maszynach wirtualnych systemu Linux Azure](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="95a7c-255">You might want toolook at [another way toocluster MySQL on Linux](mysql-cluster.md) and ways too[optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

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
