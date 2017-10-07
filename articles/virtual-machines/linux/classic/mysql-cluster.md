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
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a><span data-ttu-id="ff131-103">Zestawów o zrównoważonym obciążeniu tooclusterize MySQL w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="ff131-103">Use load-balanced sets tooclusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ff131-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager](../../../resource-manager-deployment-model.md) i klasycznym.</span><span class="sxs-lookup"><span data-stu-id="ff131-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="ff131-105">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ff131-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="ff131-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ff131-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ff131-107">A [szablonu usługi Resource Manager](https://azure.microsoft.com/documentation/templates/mysql-replication/) jest dostępna, jeśli potrzebujesz toodeploy klaster programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff131-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need toodeploy a MySQL cluster.</span></span>

<span data-ttu-id="ff131-108">W tym artykule Eksploruje i przedstawia hello różne podejścia toodeploy dostępne wysokiej dostępności opartych na systemie Linux usług Microsoft Azure, wysokiej dostępności serwera MySQL jako Elementarz eksploracji.</span><span class="sxs-lookup"><span data-stu-id="ff131-108">This article explores and illustrates hello different approaches available toodeploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="ff131-109">Film pokazujący to rozwiązanie jest dostępne na [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span><span class="sxs-lookup"><span data-stu-id="ff131-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="ff131-110">Firma Microsoft będzie konspektu nieudostępnianych jednostkach, dwa węzły, punktowe MySQL rozwiązanie zapewniające wysoką dostępność na podstawie DRBD, Corosync i rozrusznik.</span><span class="sxs-lookup"><span data-stu-id="ff131-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="ff131-111">Tylko jeden węzeł uruchamia MySQL naraz.</span><span class="sxs-lookup"><span data-stu-id="ff131-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="ff131-112">Odczytywanie i zapisywanie z hello DRBD zasobów jest również ograniczony tooonly jeden węzeł naraz.</span><span class="sxs-lookup"><span data-stu-id="ff131-112">Reading and writing from hello DRBD resource is also limited tooonly one node at a time.</span></span>

<span data-ttu-id="ff131-113">Ponieważ użyjesz równoważeniem obciążenia zestawów w okrężnego tooprovide wykrywania funkcjonalność i punktu końcowego, usuwania i skuteczne odzyskanie hello VIP Microsoft Azure nie istnieje potrzeba rozwiązania adresu VIP, takich jak LV.</span><span class="sxs-lookup"><span data-stu-id="ff131-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure tooprovide round-robin functionality and endpoint detection, removal, and graceful recovery of hello VIP.</span></span> <span data-ttu-id="ff131-114">Witaj adresu VIP jest globalnie podlegającego routingowi adres IPv4 przypisany przez Microsoft Azure, podczas tworzenia usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="ff131-114">hello VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create hello cloud service.</span></span>

<span data-ttu-id="ff131-115">Są dostępne jako Maszynę wirtualną na innych możliwych architektury MySQL, łącznie z klastra NBD, Percona Galera i kilka rozwiązań oprogramowania pośredniczącego, w tym co najmniej jeden [magazynu maszyny Wirtualnej](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="ff131-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="ff131-116">Tak długo, jak te rozwiązania mogą replikować w emisji pojedynczej i multiemisji lub emisji i nie należy polegać na magazyn udostępniony lub wiele interfejsów sieciowych, scenariusze hello powinna być łatwa toodeploy w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ff131-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, hello scenarios should be easy toodeploy on Microsoft Azure.</span></span>

<span data-ttu-id="ff131-117">Tych klastrów architektury można rozszerzyć tooother produktów, takich jak PostgreSQL i OpenLDAP w podobny sposób.</span><span class="sxs-lookup"><span data-stu-id="ff131-117">These clustering architectures can be extended tooother products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="ff131-118">Na przykład procedury Równoważenie obciążenia bez udostępniania żadnego pomyślnie była testowana przy wielu wzorca OpenLDAP i można go oglądać w naszym blogu Channel 9.</span><span class="sxs-lookup"><span data-stu-id="ff131-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="ff131-119">Przygotuj się</span><span class="sxs-lookup"><span data-stu-id="ff131-119">Get ready</span></span>
<span data-ttu-id="ff131-120">Potrzebujesz następujących hello zasobów i możliwości:</span><span class="sxs-lookup"><span data-stu-id="ff131-120">You need hello following resources and abilities:</span></span>

  - <span data-ttu-id="ff131-121">Microsoft Azure konto z prawidłową subskrypcją stanie toocreate co najmniej dwóch maszyn wirtualnych (XS został użyty w tym przykładzie)</span><span class="sxs-lookup"><span data-stu-id="ff131-121">A Microsoft Azure account with a valid subscription, able toocreate at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="ff131-122">Sieci i podsieci</span><span class="sxs-lookup"><span data-stu-id="ff131-122">A network and a subnet</span></span>
  - <span data-ttu-id="ff131-123">Grupa koligacji</span><span class="sxs-lookup"><span data-stu-id="ff131-123">An affinity group</span></span>
  - <span data-ttu-id="ff131-124">Zestaw dostępności</span><span class="sxs-lookup"><span data-stu-id="ff131-124">An availability set</span></span>
  - <span data-ttu-id="ff131-125">Witaj toocreate możliwości wirtualne dyski twarde w tym samym regionie co usługa w chmurze hello hello i dołącz je toohello maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="ff131-125">hello ability toocreate VHDs in hello same region as hello cloud service and attach them toohello Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="ff131-126">Przetestowany środowiska</span><span class="sxs-lookup"><span data-stu-id="ff131-126">Tested environment</span></span>
* <span data-ttu-id="ff131-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="ff131-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="ff131-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="ff131-128">DRBD</span></span>
  * <span data-ttu-id="ff131-129">Serwer MySQL</span><span class="sxs-lookup"><span data-stu-id="ff131-129">MySQL Server</span></span>
  * <span data-ttu-id="ff131-130">Corosync i rozrusznik</span><span class="sxs-lookup"><span data-stu-id="ff131-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="ff131-131">Grupa koligacji</span><span class="sxs-lookup"><span data-stu-id="ff131-131">Affinity group</span></span>
<span data-ttu-id="ff131-132">Utwórz grupę koligacji dla rozwiązania hello logując się toohello klasycznego portalu Azure, wybierając **ustawienia**oraz tworzenia grupy koligacji.</span><span class="sxs-lookup"><span data-stu-id="ff131-132">Create an affinity group for hello solution by signing in toohello Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="ff131-133">Przydzielone zasoby utworzone później zostanie przypisany toothis grupy koligacji.</span><span class="sxs-lookup"><span data-stu-id="ff131-133">Allocated resources created later will be assigned toothis affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="ff131-134">Sieci</span><span class="sxs-lookup"><span data-stu-id="ff131-134">Networks</span></span>
<span data-ttu-id="ff131-135">Utworzono nową sieć, a w sieci hello została utworzona podsieć.</span><span class="sxs-lookup"><span data-stu-id="ff131-135">A new network is created, and a subnet is created inside hello network.</span></span> <span data-ttu-id="ff131-136">W tym przykładzie używane sieci 10.10.10.0/24 z podsieci o prefiksie/24 tylko jeden wewnątrz.</span><span class="sxs-lookup"><span data-stu-id="ff131-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="ff131-137">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="ff131-137">Virtual machines</span></span>
<span data-ttu-id="ff131-138">Witaj pierwsza maszyna wirtualna 13.10 Ubuntu jest tworzona przy użyciu obrazu Endorsed Ubuntu galerii i nosi nazwę `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="ff131-138">hello first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="ff131-139">Nową usługę w chmurze jest tworzony w procesie hello, nazywanym hadb.</span><span class="sxs-lookup"><span data-stu-id="ff131-139">A new cloud service is created in hello process, called hadb.</span></span> <span data-ttu-id="ff131-140">Ta nazwa przedstawiono hello udostępniony, rodzaj równoważenia obciążenia, mające usługi powitania po dodaniu więcej zasobów.</span><span class="sxs-lookup"><span data-stu-id="ff131-140">This name illustrates hello shared, load-balanced nature that hello service will have when more resources are added.</span></span> <span data-ttu-id="ff131-141">Witaj tworzenie `hadb01` ma procesu i jest wypełniane przy użyciu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="ff131-141">hello creation of `hadb01` is uneventful and completed by using hello portal.</span></span> <span data-ttu-id="ff131-142">Punkt końcowy SSH jest tworzony automatycznie, a wybrano hello nowej sieci.</span><span class="sxs-lookup"><span data-stu-id="ff131-142">An endpoint for SSH is automatically created, and hello new network is selected.</span></span> <span data-ttu-id="ff131-143">Teraz możesz utworzyć zbiór dostępności dla hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ff131-143">Now you can create an availability set for hello VMs.</span></span>

<span data-ttu-id="ff131-144">Po hello pierwsza maszyna wirtualna jest tworzony (technicznie, podczas tworzenia usługi w chmurze hello), należy utworzyć hello drugiej maszyny Wirtualnej, `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="ff131-144">After hello first VM is created (technically, when hello cloud service is created), create hello second VM, `hadb02`.</span></span> <span data-ttu-id="ff131-145">Dla hello drugie maszyny Wirtualnej, użyj maszyny Wirtualnej systemu Ubuntu 13.10 z hello galerii przy użyciu portalu hello, ale użyj istniejącej usługi chmury, `hadb.cloudapp.net`, zamiast tworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="ff131-145">For hello second VM, use Ubuntu 13.10 VM from hello Gallery by using hello portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="ff131-146">Witaj sieci i zestawu dostępności powinna być zaznaczona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ff131-146">hello network and availability set should be automatically selected.</span></span> <span data-ttu-id="ff131-147">Punkt końcowy SSH zostanie utworzony, zbyt.</span><span class="sxs-lookup"><span data-stu-id="ff131-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="ff131-148">Po utworzeniu obie maszyny wirtualne, zwróć uwagę na powitania portu SSH dla `hadb01` (TCP 22) i `hadb02` (automatycznie przypisywana przez platformę Azure).</span><span class="sxs-lookup"><span data-stu-id="ff131-148">After both VMs have been created, take note of hello SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="ff131-149">Magazyn dołączony</span><span class="sxs-lookup"><span data-stu-id="ff131-149">Attached storage</span></span>
<span data-ttu-id="ff131-150">Dołącz nowe tooboth dysku maszyn wirtualnych i utworzyć dyski 5 GB w procesie hello.</span><span class="sxs-lookup"><span data-stu-id="ff131-150">Attach a new disk tooboth VMs and create 5-GB disks in hello process.</span></span> <span data-ttu-id="ff131-151">dyski Hello są obsługiwane w hello kontener wirtualnego dysku twardego na użytek dysków główne systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ff131-151">hello disks are hosted in hello VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="ff131-152">Po dyski są tworzone i dołączyć, jest nie konieczności toorestart Linux, ponieważ jądra hello zobaczą hello nowe urządzenie.</span><span class="sxs-lookup"><span data-stu-id="ff131-152">After disks are created and attached, there is no need toorestart Linux because hello kernel will see hello new device.</span></span> <span data-ttu-id="ff131-153">To urządzenie jest zwykle `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="ff131-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="ff131-154">Sprawdź `dmesg` hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ff131-154">Check `dmesg` for hello output.</span></span>

<span data-ttu-id="ff131-155">Na każdej maszynie Wirtualnej, Utwórz partycję za pomocą `cfdisk` (partycji podstawowej, Linux) i zapisu hello nowej partycji tabeli.</span><span class="sxs-lookup"><span data-stu-id="ff131-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write hello new partition table.</span></span> <span data-ttu-id="ff131-156">Nie należy tworzyć system plików na tej partycji.</span><span class="sxs-lookup"><span data-stu-id="ff131-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-hello-cluster"></a><span data-ttu-id="ff131-157">Konfigurowanie klastra hello</span><span class="sxs-lookup"><span data-stu-id="ff131-157">Set up hello cluster</span></span>
<span data-ttu-id="ff131-158">Użyj stanie tooinstall Corosync rozrusznik i DRBD na obu maszynach wirtualnych Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ff131-158">Use APT tooinstall Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="ff131-159">toodo tak z `apt-get`Uruchom hello następujący kod:</span><span class="sxs-lookup"><span data-stu-id="ff131-159">toodo so with `apt-get`, run hello following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="ff131-160">W tej chwili nie należy instalować MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff131-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="ff131-161">Debian i Ubuntu skrypty instalacyjne zainicjować katalog danych MySQL na `/var/lib/mysql`, ale ponieważ hello katalogu zostaną zastąpione przez system plików DRBD, należy tooinstall MySQL później.</span><span class="sxs-lookup"><span data-stu-id="ff131-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because hello directory will be superseded by a DRBD file system, you need tooinstall MySQL later.</span></span>

<span data-ttu-id="ff131-162">Sprawdź (przy użyciu `/sbin/ifconfig`) czy obie maszyny wirtualne korzystają z adresów w podsieci 10.10.10.0/24 hello i że one może wysyłać polecenia ping wzajemnie według nazwy.</span><span class="sxs-lookup"><span data-stu-id="ff131-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in hello 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="ff131-163">Można również użyć `ssh-keygen` i `ssh-copy-id` toomake się, że obie maszyny wirtualne mogą komunikować się za pośrednictwem SSH bez konieczności wprowadzania hasła.</span><span class="sxs-lookup"><span data-stu-id="ff131-163">You can also use `ssh-keygen` and `ssh-copy-id` toomake sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="ff131-164">Konfigurowanie DRBD</span><span class="sxs-lookup"><span data-stu-id="ff131-164">Set up DRBD</span></span>
<span data-ttu-id="ff131-165">Utwórz zasób DRBD używającej bazowy hello `/dev/sdc1` partycji tooproduce `/dev/drbd1` zasobów, które mogą być sformatowane przy użyciu ext3 i używane w węzłach głównych i dodatkowych.</span><span class="sxs-lookup"><span data-stu-id="ff131-165">Create a DRBD resource that uses hello underlying `/dev/sdc1` partition tooproduce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="ff131-166">Otwórz `/etc/drbd.d/r0.res` i kopiowania powitania po definicji zasobu na obu maszynach wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="ff131-166">Open `/etc/drbd.d/r0.res` and copy hello following resource definition on both VMs:</span></span>

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

2. <span data-ttu-id="ff131-167">Inicjowanie hello zasobów za pomocą `drbdadm` na obu maszynach wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="ff131-167">Initialize hello resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="ff131-168">Na hello podstawowej maszyny Wirtualnej (`hadb01`), wymusić własność (podstawowy) hello DRBD zasobów:</span><span class="sxs-lookup"><span data-stu-id="ff131-168">On hello primary VM (`hadb01`), force ownership (primary) of hello DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="ff131-169">Jeśli należy zbadać zawartość hello/proc/drbd (`sudo cat /proc/drbd`) na obu maszynach wirtualnych, powinien zostać wyświetlony `Primary/Secondary` na `hadb01` i `Secondary/Primary` na `hadb02`, zgodnie z rozwiązania hello na tym etapie.</span><span class="sxs-lookup"><span data-stu-id="ff131-169">If you examine hello contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with hello solution at this point.</span></span> <span data-ttu-id="ff131-170">Dysk 5 GB Hello są synchronizowane przez sieć 10.10.10.0/24 hello na toocustomers nie dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="ff131-170">hello 5-GB disk is synchronized over hello 10.10.10.0/24 network at no charge toocustomers.</span></span>

<span data-ttu-id="ff131-171">Po zsynchronizowaniu hello dysku można utworzyć systemu plików hello na `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="ff131-171">After hello disk is synchronized, you can create hello file system on `hadb01`.</span></span> <span data-ttu-id="ff131-172">Do celów testowych, użyliśmy ext2, ale hello następującego kodu utworzy ext3 systemu plików:</span><span class="sxs-lookup"><span data-stu-id="ff131-172">For testing purposes, we used ext2, but hello following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a><span data-ttu-id="ff131-173">Zainstaluj hello DRBD zasobów</span><span class="sxs-lookup"><span data-stu-id="ff131-173">Mount hello DRBD resource</span></span>
<span data-ttu-id="ff131-174">Wszystko jest teraz gotowy toomount hello DRBD zasobów na `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="ff131-174">You're now ready toomount hello DRBD resources on `hadb01`.</span></span> <span data-ttu-id="ff131-175">Użyj debian i pochodne `/var/lib/mysql` jako katalog danych na MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff131-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="ff131-176">Ponieważ nie zainstalowano MySQL, Utwórz katalog hello i zainstalować hello DRBD zasobów.</span><span class="sxs-lookup"><span data-stu-id="ff131-176">Because you haven't installed MySQL, create hello directory and mount hello DRBD resource.</span></span> <span data-ttu-id="ff131-177">tooperform tę opcję, uruchom hello następującego kodu `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="ff131-177">tooperform this option, run hello following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="ff131-178">Konfigurowanie MySQL</span><span class="sxs-lookup"><span data-stu-id="ff131-178">Set up MySQL</span></span>
<span data-ttu-id="ff131-179">Teraz możesz teraz gotowy tooinstall MySQL `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="ff131-179">Now you're ready tooinstall MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="ff131-180">Aby uzyskać `hadb02`, są dostępne dwie opcje.</span><span class="sxs-lookup"><span data-stu-id="ff131-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="ff131-181">Można zainstalować mysql serwer, który będzie utworzyć /var/lib/mysql, wypełnienie nowy katalog danych, a następnie usuń zawartość hello.</span><span class="sxs-lookup"><span data-stu-id="ff131-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove hello contents.</span></span> <span data-ttu-id="ff131-182">tooperform tę opcję, uruchom hello następującego kodu `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="ff131-182">tooperform this option, run hello following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="ff131-183">Druga opcja Hello jest zbyt toofailover`hadb02` , a następnie zainstaluj mysql serwer istnieje.</span><span class="sxs-lookup"><span data-stu-id="ff131-183">hello second option is toofailover too`hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="ff131-184">Skrypty instalacyjne zauważyć hello istniejącej instalacji i nie będzie on touch.</span><span class="sxs-lookup"><span data-stu-id="ff131-184">Installation scripts will notice hello existing installation and won't touch it.</span></span>

<span data-ttu-id="ff131-185">Uruchom hello następujący kod na `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="ff131-185">Run hello following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="ff131-186">Uruchom hello następujący kod na `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="ff131-186">Run hello following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="ff131-187">Jeśli nie planujesz teraz toofailover DRBD, pierwsza opcja hello jest łatwiejsze, ale raczej mniej elegancki.</span><span class="sxs-lookup"><span data-stu-id="ff131-187">If you don't plan toofailover DRBD now, hello first option is easier although arguably less elegant.</span></span> <span data-ttu-id="ff131-188">Po należy wybrać tę opcję, należy rozpocząć pracę nad bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff131-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="ff131-189">Uruchom hello następujący kod na `hadb02` (lub jednego z tych serwerów hello jest aktywna, zgodnie z tooDRBD):</span><span class="sxs-lookup"><span data-stu-id="ff131-189">Run hello following code on `hadb02` (or whichever one of hello servers is active, according tooDRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> <span data-ttu-id="ff131-190">Tej ostatniej instrukcji wyłącza uwierzytelnianie dla użytkownika głównego hello w tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="ff131-190">This last statement effectively disables authentication for hello root user in this table.</span></span> <span data-ttu-id="ff131-191">To powinna zostać zastąpiona przez klasy produkcji PRZYZNAĆ instrukcje i jest dołączany wyłącznie w celach ilustracyjnych.</span><span class="sxs-lookup"><span data-stu-id="ff131-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="ff131-192">Jeśli chcesz toomake zapytania z maszyn wirtualnych poza hello, (co jest hello przeznaczenie tego przewodnika), należy również tooenable sieci dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff131-192">If you want toomake queries from outside hello VMs (which is hello purpose of this guide), you also need tooenable networking for MySQL.</span></span> <span data-ttu-id="ff131-193">Na obu maszynach wirtualnych, należy otworzyć `/etc/mysql/my.cnf` i przejść za`bind-address`.</span><span class="sxs-lookup"><span data-stu-id="ff131-193">On both VMs, open `/etc/mysql/my.cnf` and go too`bind-address`.</span></span> <span data-ttu-id="ff131-194">Zmień adres hello z 127.0.0.1 too0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="ff131-194">Change hello address from 127.0.0.1 too0.0.0.0.</span></span> <span data-ttu-id="ff131-195">Po zapisaniu pliku hello, wystawiać `sudo service mysql restart` na serwerze podstawowym bieżącej.</span><span class="sxs-lookup"><span data-stu-id="ff131-195">After saving hello file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-hello-mysql-load-balanced-set"></a><span data-ttu-id="ff131-196">Utwórz zestaw o zrównoważonym obciążeniu MySQL hello</span><span class="sxs-lookup"><span data-stu-id="ff131-196">Create hello MySQL load-balanced set</span></span>
<span data-ttu-id="ff131-197">Wrócić do poprzedniej strony portalu toohello znajduje się zbyt`hadb01`i wybierz polecenie **punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="ff131-197">Go back toohello portal, go too`hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="ff131-198">toocreate jako punkt końcowy, wybierz MySQL (TCP 3306) z listy rozwijanej hello i wybierz **zestaw o zrównoważonym obciążeniu nowe Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ff131-198">toocreate an endpoint, choose MySQL (TCP 3306) from hello drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="ff131-199">Nazwa hello równoważeniem obciążenia punktu końcowego `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="ff131-199">Name hello load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="ff131-200">Ustaw **czasu** sekund too5 minimalne.</span><span class="sxs-lookup"><span data-stu-id="ff131-200">Set **Time** too5 seconds, minimum.</span></span>

<span data-ttu-id="ff131-201">Po utworzeniu punktu końcowego hello Przejdź zbyt`hadb02`, wybierz **punkty końcowe**i utworzyć punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="ff131-201">After you create hello endpoint, go too`hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="ff131-202">Wybierz `lb-mysql`, a następnie wybierz z listy rozwijanej hello MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff131-202">Choose `lb-mysql`, and then select MySQL from hello drop-down list.</span></span> <span data-ttu-id="ff131-203">Umożliwia także hello wiersza polecenia platformy Azure dla tego kroku.</span><span class="sxs-lookup"><span data-stu-id="ff131-203">You can also use hello Azure CLI for this step.</span></span>

<span data-ttu-id="ff131-204">Masz teraz wszystko, czego należy ręczne operacji hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ff131-204">You now have everything you need for manual operation of hello cluster.</span></span>

### <a name="test-hello-load-balanced-set"></a><span data-ttu-id="ff131-205">Zestaw z równoważeniem obciążenia hello testowania</span><span class="sxs-lookup"><span data-stu-id="ff131-205">Test hello load-balanced set</span></span>
<span data-ttu-id="ff131-206">Za pomocą dowolnego klienta MySQL lub przy użyciu określonych aplikacji, takich jak phpMyAdmin uruchomione jako witryny sieci Web platformy Azure, można wykonać testy z poza maszyny.</span><span class="sxs-lookup"><span data-stu-id="ff131-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="ff131-207">W tym przypadku użyto MySQL przez narzędzie wiersza polecenia w innym polu Linux:</span><span class="sxs-lookup"><span data-stu-id="ff131-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="ff131-208">Ręcznie przechodzenie w tryb failover</span><span class="sxs-lookup"><span data-stu-id="ff131-208">Manually failing over</span></span>
<span data-ttu-id="ff131-209">Tryb failover można symulować zamykanie MySQL, przełączając DRBD w podstawowej i ponownie uruchomić MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff131-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="ff131-210">tooperform to zadanie, uruchom hello następującego kodu na hadb01:</span><span class="sxs-lookup"><span data-stu-id="ff131-210">tooperform this task, run hello following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="ff131-211">Następnie na hadb02:</span><span class="sxs-lookup"><span data-stu-id="ff131-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="ff131-212">Po przejścia w tryb failover ręcznie, można powtarzać zapytania zdalnego i powinien działać prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="ff131-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="ff131-213">Konfigurowanie Corosync</span><span class="sxs-lookup"><span data-stu-id="ff131-213">Set up Corosync</span></span>
<span data-ttu-id="ff131-214">Corosync jest hello wymagane dla toowork rozrusznik podstawowej infrastruktury klastra.</span><span class="sxs-lookup"><span data-stu-id="ff131-214">Corosync is hello underlying cluster infrastructure required for Pacemaker toowork.</span></span> <span data-ttu-id="ff131-215">Pulsu (i innych metod, takich jak Ultramonkey) Corosync jest podziału hello funkcji systemu CRM, rozrusznik pozostaje tooHeartbeat więcej podobnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="ff131-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of hello CRM functionalities, while Pacemaker remains more similar tooHeartbeat in functionality.</span></span>

<span data-ttu-id="ff131-216">Witaj głównym ograniczeniem dla Corosync na platformie Azure jest Corosync preferuje multiemisji za pośrednictwem emisji komunikacji emisji pojedynczej, że sieci Microsoft Azure obsługuje tylko emisji pojedynczej.</span><span class="sxs-lookup"><span data-stu-id="ff131-216">hello main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="ff131-217">Na szczęście Corosync ma pracy tryb emisji pojedynczej.</span><span class="sxs-lookup"><span data-stu-id="ff131-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="ff131-218">ograniczenie tylko rzeczywistego Hello jest, ponieważ wszystkie węzły nie komunikują się ze sobą, należy toodefine hello węzłów w plikach konfiguracji, w tym ich adresy IP.</span><span class="sxs-lookup"><span data-stu-id="ff131-218">hello only real constraint is that because all nodes are not communicating among themselves, you need toodefine hello nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="ff131-219">Możemy użyć hello Corosync przykład plików dla emisji pojedynczej i Zmień powiązanie adresu, węzeł listy i katalogi rejestrowania (używa Ubuntu `/var/log/corosync` podczas przykład Witaj pliki używają `/var/log/cluster`) i Włącz narzędzia kworum.</span><span class="sxs-lookup"><span data-stu-id="ff131-219">We can use hello Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while hello example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="ff131-220">Użyj następujących hello `transport: udpu` dyrektywy i hello ręcznie zdefiniowanych adresów IP dla obu węzłów.</span><span class="sxs-lookup"><span data-stu-id="ff131-220">Use hello following `transport: udpu` directive and hello manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="ff131-221">Uruchom hello następujący kod na `/etc/corosync/corosync.conf` dla obu węzłów:</span><span class="sxs-lookup"><span data-stu-id="ff131-221">Run hello following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

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

<span data-ttu-id="ff131-222">Skopiuj ten plik konfiguracji na obu maszynach wirtualnych i uruchomić Corosync w obu węzłów:</span><span class="sxs-lookup"><span data-stu-id="ff131-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="ff131-223">Wkrótce po uruchomieniu usługi hello hello klastra należy ustanowić pierścienia bieżącego hello i kworum powinien zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="ff131-223">Shortly after starting hello service, hello cluster should be established in hello current ring, and quorum should be constituted.</span></span> <span data-ttu-id="ff131-224">Ta funkcja możemy można sprawdzić, przeglądając dzienniki lub uruchamiając hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="ff131-224">We can check this functionality by reviewing logs or by running hello following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="ff131-225">Zostanie wyświetlony toohello podobne dane wyjściowe po obrazu:</span><span class="sxs-lookup"><span data-stu-id="ff131-225">You will see output similar toohello following image:</span></span>

![corosync quorumtool - l przykładowe dane wyjściowe](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="ff131-227">Konfigurowanie rozrusznik</span><span class="sxs-lookup"><span data-stu-id="ff131-227">Set up Pacemaker</span></span>
<span data-ttu-id="ff131-228">Używa rozrusznik hello toomonitor klastra dla zasobów, zdefiniuj, gdy kolory podstawowe przestaną działać i przełączanie toosecondaries tych zasobów.</span><span class="sxs-lookup"><span data-stu-id="ff131-228">Pacemaker uses hello cluster toomonitor for resources, define when primaries go down, and switch those resources toosecondaries.</span></span> <span data-ttu-id="ff131-229">Można zdefiniować zasoby z zbiór dostępnych skryptów lub skryptów (init jak) najmniej znaczący BAJT, między innymi opcjami.</span><span class="sxs-lookup"><span data-stu-id="ff131-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="ff131-230">Chcemy rozrusznik zasobu DRBD zbyt "własnych" hello, hello punktu instalacji i hello usługi MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff131-230">We want Pacemaker too"own" hello DRBD resource, hello mount point, and hello MySQL service.</span></span> <span data-ttu-id="ff131-231">Jeśli rozrusznik można włączać i wyłączać DRBD, zainstalować i Odinstaluj go i następnie uruchamiać i zatrzymywać MySQL w hello prawo zamówienia, gdy coś zły się dzieje z hello głównej, instalacja została ukończona.</span><span class="sxs-lookup"><span data-stu-id="ff131-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in hello right order when something bad happens with hello primary, setup is complete.</span></span>

<span data-ttu-id="ff131-232">Po zainstalowaniu rozrusznik konfiguracji powinna być prosta, coś, takich jak:</span><span class="sxs-lookup"><span data-stu-id="ff131-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="ff131-233">Sprawdź konfigurację hello uruchamiając `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="ff131-233">Check hello configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="ff131-234">Następnie utwórz plik (takie jak `/tmp/cluster.conf`) z hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="ff131-234">Then create a file (like `/tmp/cluster.conf`) with hello following resources:</span></span>

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

3. <span data-ttu-id="ff131-235">Załadowanie pliku hello do hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ff131-235">Load hello file into hello configuration.</span></span> <span data-ttu-id="ff131-236">Wystarczy toodo to w jednym węźle.</span><span class="sxs-lookup"><span data-stu-id="ff131-236">You only need toodo this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="ff131-237">Upewnij się, że rozrusznik uruchomienie przy rozruchu w obu węzłów:</span><span class="sxs-lookup"><span data-stu-id="ff131-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="ff131-238">Za pomocą `sudo crm_mon –L`, sprawdź, czy ma zostać wzorcem hello hello klastra jednego z węzłów i działa wszystkie zasoby hello.</span><span class="sxs-lookup"><span data-stu-id="ff131-238">By using `sudo crm_mon –L`, verify that one of your nodes has become hello master for hello cluster and is running all hello resources.</span></span> <span data-ttu-id="ff131-239">Możesz użyć instalacji i ps toocheck uruchomionych hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="ff131-239">You can use mount and ps toocheck that hello resources are running.</span></span>

<span data-ttu-id="ff131-240">Zrzut ekranu przedstawia następujące Hello `crm_mon` z jednym węzłem zatrzymane (Zamknij wybierając klawisze Ctrl + C):</span><span class="sxs-lookup"><span data-stu-id="ff131-240">hello following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![węzeł crm_mon zatrzymana](./media/mysql-cluster/image002.png)

<span data-ttu-id="ff131-242">Ten zrzut ekranu przedstawia węzłów, jeden z nich i jeden podrzędny:</span><span class="sxs-lookup"><span data-stu-id="ff131-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operacyjne wzorzec/podrzędny](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="ff131-244">Testowanie</span><span class="sxs-lookup"><span data-stu-id="ff131-244">Testing</span></span>
<span data-ttu-id="ff131-245">Wszystko jest gotowe do symulacji automatycznej pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="ff131-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="ff131-246">Istnieją dwa sposoby toodo to: elastyczne i.</span><span class="sxs-lookup"><span data-stu-id="ff131-246">There are two ways toodo this: soft and hard.</span></span>

<span data-ttu-id="ff131-247">Hello nietrwałego sposób funkcja klastra hello zamknięcia: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="ff131-247">hello soft way uses hello cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="ff131-248">Jeśli możesz użyć tego wzorca hello hello podrzędny ma.</span><span class="sxs-lookup"><span data-stu-id="ff131-248">If you use this on hello master, hello slave takes over.</span></span> <span data-ttu-id="ff131-249">Pamiętaj, aby tooset tego toooff Wstecz.</span><span class="sxs-lookup"><span data-stu-id="ff131-249">Remember tooset this back toooff.</span></span> <span data-ttu-id="ff131-250">Jeśli nie zostanie crm_mon wyświetli jeden węzeł w stan wstrzymania.</span><span class="sxs-lookup"><span data-stu-id="ff131-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="ff131-251">Witaj twardych sposób Trwa zamykanie dół hello podstawowej maszyny Wirtualnej (hadb01) za pośrednictwem portalu hello lub zmieniając hello uruchamiania przełącznika/RL na powitania maszyny Wirtualnej (to znaczy zatrzymania, zamknięcia).</span><span class="sxs-lookup"><span data-stu-id="ff131-251">hello hard way is shutting down hello primary VM (hadb01) via hello portal or by changing hello runlevel on hello VM (that is, halt, shutdown).</span></span> <span data-ttu-id="ff131-252">Pomaga to Corosync i rozrusznik przez sygnalizowania będzie danego wzorca hello w dół.</span><span class="sxs-lookup"><span data-stu-id="ff131-252">This helps Corosync and Pacemaker by signaling that hello master's going down.</span></span> <span data-ttu-id="ff131-253">Można to sprawdzić (przydatne w przypadku okna obsługi), ale możesz też wymusić scenariusz hello zamrażanie hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ff131-253">You can test this (useful for maintenance windows), but you can also force hello scenario by freezing hello VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="ff131-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="ff131-254">STONITH</span></span>
<span data-ttu-id="ff131-255">Powinno być możliwe tooissue wyłączania maszyny Wirtualnej za pomocą hello Azure CLI zamiast STONITH skrypt, który kontroluje urządzenia fizycznego.</span><span class="sxs-lookup"><span data-stu-id="ff131-255">It should be possible tooissue a VM shutdown via hello Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="ff131-256">Można użyć `/usr/lib/stonith/plugins/external/ssh` jako typu podstawowego i Włącz STONITH w konfiguracji klastra hello.</span><span class="sxs-lookup"><span data-stu-id="ff131-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in hello cluster's configuration.</span></span> <span data-ttu-id="ff131-257">Azure CLI powinien być zainstalowany globalnie i ustawienia publikowania hello i powinny być ładowane profilu dla użytkownika hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ff131-257">Azure CLI should be globally installed, and hello publish settings and profile should be loaded for hello cluster's user.</span></span>

<span data-ttu-id="ff131-258">Przykładowy kod dla zasobu hello jest dostępna w [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="ff131-258">Sample code for hello resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="ff131-259">Zmień konfigurację klastra hello przez dodanie powitania po zbyt`sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="ff131-259">Change hello cluster's configuration by adding hello following too`sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="ff131-260">skrypt Hello nie wykonywać testy w górę lub w dół.</span><span class="sxs-lookup"><span data-stu-id="ff131-260">hello script doesn't perform up/down checks.</span></span> <span data-ttu-id="ff131-261">Hello pierwotnego SSH zasobu były 15 kontroli ping, ale czas odzyskiwania dla maszyny Wirtualnej platformy Azure może być więcej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="ff131-261">hello original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="ff131-262">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="ff131-262">Limitations</span></span>
<span data-ttu-id="ff131-263">Zastosuj Hello następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="ff131-263">hello following limitations apply:</span></span>

* <span data-ttu-id="ff131-264">Witaj linbit DRBD zasobów skrypt, który zarządza DRBD jako zasób w używa rozrusznik `drbdadm down` zamknięcia węzła, nawet jeśli węzeł hello właśnie przechodzi w stan wstrzymania.</span><span class="sxs-lookup"><span data-stu-id="ff131-264">hello linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if hello node is just going on standby.</span></span> <span data-ttu-id="ff131-265">To nie jest idealny ponieważ hello podrzędny zostanie nie można synchronizowanie hello DRBD zasobów podczas wzorca hello pobiera zapisów.</span><span class="sxs-lookup"><span data-stu-id="ff131-265">This is not ideal because hello slave will not be synchronizing hello DRBD resource while hello master gets writes.</span></span> <span data-ttu-id="ff131-266">Jeśli wzorzec hello nie powiedzie się graciously, podrzędny hello może zająć ponad starsze stan systemu plików.</span><span class="sxs-lookup"><span data-stu-id="ff131-266">If hello master does not fail graciously, hello slave can take over an older file system state.</span></span> <span data-ttu-id="ff131-267">Istnieją dwa sposoby potencjalnych rozwiązywania to:</span><span class="sxs-lookup"><span data-stu-id="ff131-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="ff131-268">Wymuszanie `drbdadm up r0` we wszystkich węzłach klastra za pośrednictwem lokalnego (nie clusterized) programu alarmowego</span><span class="sxs-lookup"><span data-stu-id="ff131-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="ff131-269">Edytowanie skryptu DRBD linbit hello, upewniając się, że `down` nie jest wywoływana`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="ff131-269">Editing hello linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="ff131-270">Hello modułu równoważenia obciążenia musi toorespond co najmniej pięć sekund, więc aplikacji powinien być typu cluster-aware i być bardziej odporne na limit czasu.</span><span class="sxs-lookup"><span data-stu-id="ff131-270">hello load balancer needs at least five seconds toorespond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="ff131-271">Może również pomóc innych architektur, takich jak kolejki w aplikacji i middlewares zapytania.</span><span class="sxs-lookup"><span data-stu-id="ff131-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="ff131-272">Dostrajanie MySQL jest konieczne tooensure, którą można wykonać zapisu w tempie można zarządzać i pamięci podręczne są wyczyszczone toodisk nawet toominimize możliwa utrata pamięci.</span><span class="sxs-lookup"><span data-stu-id="ff131-272">MySQL tuning is necessary tooensure that writing is done at a manageable pace and caches are flushed toodisk as frequently as possible toominimize memory loss.</span></span>
* <span data-ttu-id="ff131-273">Zapis wydajności jest zależna w maszynie Wirtualnej łączyć hello przełącznika wirtualnego, ponieważ jest używany przez urządzenie hello tooreplicate DRBD mechanizm hello.</span><span class="sxs-lookup"><span data-stu-id="ff131-273">Write performance is dependent in VM interconnect in hello virtual switch because this is hello mechanism used by DRBD tooreplicate hello device.</span></span>
