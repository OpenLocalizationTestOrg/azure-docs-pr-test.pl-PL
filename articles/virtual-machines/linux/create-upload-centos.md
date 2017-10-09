---
title: aaaCreate i przekazywanie dysku VHD na podstawie CentOS Linux na platformie Azure
description: "Dowiedz się toocreate i przekaż Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym na podstawie CentOS Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 78f36be1d36e3d44cb836c912d143f2c9a72aab5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="092dd-103">Przygotowywanie maszyny wirtualnej systemu CentOS dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="092dd-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="092dd-104">Przygotowanie maszyny wirtualnej CentOS 6.x dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="092dd-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="092dd-105">Przygotowanie maszyny wirtualnej CentOS 7.0 + Azure</span><span class="sxs-lookup"><span data-stu-id="092dd-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="092dd-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="092dd-106">Prerequisites</span></span>
<span data-ttu-id="092dd-107">W tym artykule przyjęto założenie, zainstalowano CentOS (lub podobny pochodnej) Linux tooa wirtualnego dysku twardego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="092dd-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="092dd-108">Wiele narzędzi istnieje toocreate plików VHD, na przykład rozwiązanie wirtualizacji takich jak funkcja Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="092dd-108">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="092dd-109">Aby uzyskać instrukcje, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="092dd-109">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="092dd-110">**Informacje o instalacji centOS**</span><span class="sxs-lookup"><span data-stu-id="092dd-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="092dd-111">Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="092dd-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="092dd-112">Witaj VHDX format nie jest obsługiwany na platformie Azure, tylko **stały VHD**.</span><span class="sxs-lookup"><span data-stu-id="092dd-112">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="092dd-113">Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello polecenia cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="092dd-113">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span> <span data-ttu-id="092dd-114">Jeśli używasz VirtualBox oznacza to, wybierając **stały rozmiar** jako przeciwieństwie domyślne toohello dynamicznie przydzielane podczas tworzenia dysku hello.</span><span class="sxs-lookup"><span data-stu-id="092dd-114">If you are using VirtualBox this means selecting **Fixed size** as opposed toohello default dynamically allocated when creating hello disk.</span></span>
* <span data-ttu-id="092dd-115">Podczas instalowania systemu Linux hello jest *zalecane* używasz standardowe partycje, a nie LVM (często hello domyślnie wiele instalacji).</span><span class="sxs-lookup"><span data-stu-id="092dd-115">When installing hello Linux system it is *recommended* that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="092dd-116">Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, szczególnie w przypadku, gdy dysk systemu operacyjnego musi kiedykolwiek tooanother toobe dołączony identycznych maszyn wirtualnych do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="092dd-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother identical VM for troubleshooting.</span></span> <span data-ttu-id="092dd-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="092dd-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="092dd-118">Wymagana jest obsługa jądra służący do instalowania systemów plików funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="092dd-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="092dd-119">Przy pierwszym uruchomieniu komputera na Azure hello konfiguracji inicjowania obsługi administracyjnej jest przekazywany toohello maszyny Wirtualnej systemu Linux za pomocą nośnika sformatowany funkcji zdefiniowanej przez użytkownika, która jest dołączona toohello gościa.</span><span class="sxs-lookup"><span data-stu-id="092dd-119">At first boot on Azure hello provisioning configuration is passed toohello Linux VM via UDF-formatted media that is attached toohello guest.</span></span> <span data-ttu-id="092dd-120">agenta systemu Linux Azure Hello musi być możliwe toomount hello UDF pliku system tooread swojej konfiguracji i udostępnić hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="092dd-120">hello Azure Linux agent must be able toomount hello UDF file system tooread its configuration and provision hello VM.</span></span>
* <span data-ttu-id="092dd-121">Wersje jądra systemu Linux poniżej 2.6.37 nie obsługują NUMA w funkcji Hyper-V o dużym rozmiarze maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="092dd-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="092dd-122">Ten problem wpływa głównie na starszą dystrybucji przy użyciu powitania od Red Hat 2.6.32 jądra i ustalono w RHEL 6.6 (jądra-2.6.32 504).</span><span class="sxs-lookup"><span data-stu-id="092dd-122">This issue primarily impacts older distributions using hello upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="092dd-123">Parametr rozruchu hello komputerów z systemami niestandardowych jądra starsze niż 2.6.37 lub systemem RHEL jądra starsze niż 2.6.32-504 należy ustawić `numa=off` na powitania jądra wiersza polecenia w grub.conf.</span><span class="sxs-lookup"><span data-stu-id="092dd-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set hello boot parameter `numa=off` on hello kernel command-line in grub.conf.</span></span> <span data-ttu-id="092dd-124">Aby uzyskać więcej informacji, zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="092dd-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="092dd-125">Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="092dd-125">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="092dd-126">agenta systemu Linux Hello może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.</span><span class="sxs-lookup"><span data-stu-id="092dd-126">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="092dd-127">Więcej informacji na ten temat można znaleźć w poniższych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="092dd-127">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="092dd-128">Wszystkie wirtualne dyski twarde hello muszą mieć rozmiary, które są wielokrotności 1 MB.</span><span class="sxs-lookup"><span data-stu-id="092dd-128">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="092dd-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="092dd-129">CentOS 6.x</span></span>

1. <span data-ttu-id="092dd-130">W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="092dd-130">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="092dd-131">Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="092dd-131">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="092dd-132">W CentOS 6 NetworkManager może zakłócać hello agenta systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="092dd-132">In CentOS 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="092dd-133">Odinstalowania tego pakietu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="092dd-133">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="092dd-134">Utwórz lub Edytuj plik hello `/etc/sysconfig/network` i Dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="092dd-134">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="092dd-135">Utwórz lub Edytuj plik hello `/etc/sysconfig/network-scripts/ifcfg-eth0` i Dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="092dd-135">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="092dd-136">Zmodyfikuj udev tooavoid zasady generowania statycznych zasady hello interfejsów Ethernet.</span><span class="sxs-lookup"><span data-stu-id="092dd-136">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="092dd-137">Te reguły może spowodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="092dd-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="092dd-138">Upewnij się, że Usługa sieciowa hello rozpocznie się podczas rozruchu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="092dd-138">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="092dd-139">Jeśli chcesz toouse hello OpenLogic duplikatów, które znajdują się w obrębie hello centrach danych platformy Azure, Zastąp hello `/etc/yum.repos.d/CentOS-Base.repo` pliku z powitania po repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="092dd-139">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="092dd-140">Spowoduje to również dodanie hello **[openlogic]** repozytorium, zawierający dodatkowe pakiety, takie jak agenta systemu Linux Azure hello:</span><span class="sxs-lookup"><span data-stu-id="092dd-140">This will also add hello **[openlogic]** repository that includes additional packages such as hello Azure Linux agent:</span></span>

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    <span data-ttu-id="092dd-141">Witaj dalszej części tego przewodnika zakłada, używane są co najmniej hello `[openlogic]` repozytorium, która będzie agenta systemu Linux Azure hello tooinstall używane poniżej.</span><span class="sxs-lookup"><span data-stu-id="092dd-141">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>


9. <span data-ttu-id="092dd-142">Dodaj powitania po too/etc/yum.conf wiersza:</span><span class="sxs-lookup"><span data-stu-id="092dd-142">Add hello following line too/etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="092dd-143">Uruchom następujące polecenie tooclear hello bieżącego yum metadanych i aktualizacji hello systemu z najnowszych pakietów hello hello:</span><span class="sxs-lookup"><span data-stu-id="092dd-143">Run hello following command tooclear hello current yum metadata and update hello system with hello latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="092dd-144">Jeśli tworzysz obrazu dla starszej wersji CentOS, zalecane jest tooupdate, który hello wszystkie pakiety toohello najnowsza wersja:</span><span class="sxs-lookup"><span data-stu-id="092dd-144">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="092dd-145">Po uruchomieniu tego polecenia może być wymagane ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="092dd-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="092dd-146">(Opcjonalnie) Zainstaluj sterowniki hello hello usługi integracji systemu Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="092dd-146">(Optional) Install hello drivers for hello Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="092dd-147">krok Hello jest **wymagane** dla CentOS 6.3 i wcześniejszych oraz opcjonalny w przypadku nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="092dd-147">hello step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="092dd-148">Alternatywnie możesz wykonać instrukcje dotyczące ręcznej instalacji hello na powitania [stronę pobierania LIS](https://go.microsoft.com/fwlink/?linkid=403033) hello tooinstall obr. / min na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="092dd-148">Alternatively, you can follow hello manual installation instructions on hello [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) tooinstall hello RPM onto your VM.</span></span>
 
12. <span data-ttu-id="092dd-149">Zainstaluj hello Azure agenta systemu Linux oraz zależności:</span><span class="sxs-lookup"><span data-stu-id="092dd-149">Install hello Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="092dd-150">Pakiet WALinuxAgent Hello spowoduje usunięcie hello NetworkManager i NetworkManager gnome pakietów, jeśli ich nie zostały już usunięte zgodnie z opisem w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="092dd-150">hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="092dd-151">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="092dd-151">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="092dd-152">toodo, otwórz `/boot/grub/menu.lst` w edytorze tekstów i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="092dd-152">toodo this, open `/boot/grub/menu.lst` in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="092dd-153">Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="092dd-153">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="092dd-154">Oprócz powyższych toohello, zalecane jest zbyt*Usuń* hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="092dd-154">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="092dd-155">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="092dd-155">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="092dd-156">Witaj `crashkernel` opcja może być skonfigurowany w razie potrzeby po lewej, ale należy pamiętać, że ten parametr zmniejszy hello ilość dostępnej pamięci w hello wirtualna najmniej 128 MB, które mogą być problemy na powitania mniejsze rozmiary maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="092dd-156">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="092dd-157">CentOS 6.5 lub starszej należy również ustawić parametr jądra hello `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="092dd-157">CentOS 6.5 and earlier must also set hello kernel parameter `numa=off`.</span></span> <span data-ttu-id="092dd-158">Zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="092dd-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="092dd-159">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="092dd-159">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="092dd-160">Zazwyczaj jest to domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="092dd-160">This is usually hello default.</span></span>

15. <span data-ttu-id="092dd-161">Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="092dd-161">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="092dd-162">Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="092dd-162">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="092dd-163">Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="092dd-163">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="092dd-164">Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok), zmodyfikuj hello następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="092dd-164">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="092dd-165">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="092dd-165">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="092dd-166">Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="092dd-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="092dd-167">Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.</span><span class="sxs-lookup"><span data-stu-id="092dd-167">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="092dd-168">CentOS 7.0 +</span><span class="sxs-lookup"><span data-stu-id="092dd-168">CentOS 7.0+</span></span>
<span data-ttu-id="092dd-169">**Zmiany w CentOS 7 (lub podobny pochodne)**</span><span class="sxs-lookup"><span data-stu-id="092dd-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="092dd-170">Przygotowywanie maszyny wirtualnej CentOS 7 dla platformy Azure jest bardzo podobne tooCentOS 6, jednak istnieje kilka istotnych różnic, warto zauważyć:</span><span class="sxs-lookup"><span data-stu-id="092dd-170">Preparing a CentOS 7 virtual machine for Azure is very similar tooCentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="092dd-171">Witaj NetworkManager już pakiet powoduje konflikt z agenta systemu Linux Azure hello.</span><span class="sxs-lookup"><span data-stu-id="092dd-171">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="092dd-172">Ten pakiet jest instalowany domyślnie i zaleca się, że nie zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="092dd-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="092dd-173">GRUB2 teraz jest używany jako hello inicjującego domyślne, więc hello procedury do edycji parametry jądra został zmieniony (patrz poniżej).</span><span class="sxs-lookup"><span data-stu-id="092dd-173">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="092dd-174">XFS jest teraz hello domyślnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="092dd-174">XFS is now hello default file system.</span></span> <span data-ttu-id="092dd-175">nadal można użyć systemu plików ext4 Hello, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="092dd-175">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="092dd-176">**Kroki konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="092dd-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="092dd-177">W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="092dd-177">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="092dd-178">Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="092dd-178">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="092dd-179">Utwórz lub Edytuj plik hello `/etc/sysconfig/network` i Dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="092dd-179">Create or edit hello file `/etc/sysconfig/network` and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="092dd-180">Utwórz lub Edytuj plik hello `/etc/sysconfig/network-scripts/ifcfg-eth0` i Dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="092dd-180">Create or edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="092dd-181">Zmodyfikuj udev tooavoid zasady generowania statycznych zasady hello interfejsów Ethernet.</span><span class="sxs-lookup"><span data-stu-id="092dd-181">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="092dd-182">Te reguły może spowodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="092dd-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="092dd-183">Jeśli chcesz toouse hello OpenLogic duplikatów, które znajdują się w obrębie hello centrach danych platformy Azure, Zastąp hello `/etc/yum.repos.d/CentOS-Base.repo` pliku z powitania po repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="092dd-183">If you would like toouse hello OpenLogic mirrors that are hosted within hello Azure datacenters, then replace hello `/etc/yum.repos.d/CentOS-Base.repo` file with hello following repositories.</span></span>  <span data-ttu-id="092dd-184">Spowoduje to również dodanie hello **[openlogic]** repozytorium, zawierającą pakietów hello Azure Linux agenta:</span><span class="sxs-lookup"><span data-stu-id="092dd-184">This will also add hello **[openlogic]** repository that includes packages for hello Azure Linux agent:</span></span>
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    <span data-ttu-id="092dd-185">Witaj dalszej części tego przewodnika zakłada, używane są co najmniej hello `[openlogic]` repozytorium, która będzie agenta systemu Linux Azure hello tooinstall używane poniżej.</span><span class="sxs-lookup"><span data-stu-id="092dd-185">hello rest of this guide will assume you are using at least hello `[openlogic]` repo, which will be used tooinstall hello Azure Linux agent below.</span></span>

7. <span data-ttu-id="092dd-186">Uruchom następujące polecenie tooclear hello bieżących yum metadanych hello i zainstaluj wszystkie aktualizacje:</span><span class="sxs-lookup"><span data-stu-id="092dd-186">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="092dd-187">Jeśli tworzysz obrazu dla starszej wersji CentOS, zalecane jest tooupdate, który hello wszystkie pakiety toohello najnowsza wersja:</span><span class="sxs-lookup"><span data-stu-id="092dd-187">Unless you are creating an image for an older version of CentOS, it is recommended tooupdate all hello packages toohello latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="092dd-188">Ponowne uruchomienie, może być wymagane po uruchomieniu tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="092dd-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="092dd-189">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="092dd-189">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="092dd-190">toodo, otwórz `/etc/default/grub` w hello edytora i edytowanie tekstu `GRUB_CMDLINE_LINUX` parametrów, na przykład:</span><span class="sxs-lookup"><span data-stu-id="092dd-190">toodo this, open `/etc/default/grub` in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="092dd-191">Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="092dd-191">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="092dd-192">On również wyłącza hello nowe CentOS 7 konwencje nazewnictwa dla kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="092dd-192">It also turns off hello new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="092dd-193">Oprócz powyższych toohello, zalecane jest zbyt*Usuń* hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="092dd-193">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="092dd-194">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="092dd-194">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="092dd-195">Witaj `crashkernel` opcja może być skonfigurowany w razie potrzeby po lewej, ale należy pamiętać, że ten parametr zmniejszy hello ilość dostępnej pamięci w hello wirtualna najmniej 128 MB, które mogą być problemy na powitania mniejsze rozmiary maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="092dd-195">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>

9. <span data-ttu-id="092dd-196">Po zakończeniu edycji `/etc/default/grub` na powyżej, uruchom hello następujące polecenia toorebuild hello chodników konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="092dd-196">Once you are done editing `/etc/default/grub` per above, run hello following command toorebuild hello grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="092dd-197">Obraz powitania od kompilowania **VMWare, VirtualBox lub KVM:** sterowniki hello funkcji Hyper-V upewnij się, że znajdują się w hello initramfs:</span><span class="sxs-lookup"><span data-stu-id="092dd-197">If building hello image from **VMWare, VirtualBox or KVM:** Ensure hello Hyper-V drivers are included in hello initramfs:</span></span>
   
   <span data-ttu-id="092dd-198">Edytuj `/etc/dracut.conf`, Dodaj zawartość:</span><span class="sxs-lookup"><span data-stu-id="092dd-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="092dd-199">Odbuduj hello initramfs:</span><span class="sxs-lookup"><span data-stu-id="092dd-199">Rebuild hello initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="092dd-200">Zainstaluj hello Azure agenta systemu Linux oraz zależności:</span><span class="sxs-lookup"><span data-stu-id="092dd-200">Install hello Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="092dd-201">Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="092dd-201">Do not create swap space on hello OS disk.</span></span>
   
   <span data-ttu-id="092dd-202">Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="092dd-202">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="092dd-203">Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="092dd-203">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="092dd-204">Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok), zmodyfikuj hello następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="092dd-204">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="092dd-205">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="092dd-205">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="092dd-206">Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="092dd-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="092dd-207">Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.</span><span class="sxs-lookup"><span data-stu-id="092dd-207">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="092dd-208">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="092dd-208">Next steps</span></span>
<span data-ttu-id="092dd-209">Użytkownik jest teraz gotowy toouse Twojego systemu CentOS Linux wirtualnego dysku twardego toocreate nowych maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="092dd-209">You're now ready toouse your CentOS Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="092dd-210">Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="092dd-210">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

