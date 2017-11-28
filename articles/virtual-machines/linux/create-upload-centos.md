---
title: Tworzenie i przekazywanie dysku VHD na podstawie CentOS Linux na platformie Azure
description: "Dowiedz się utworzyć i przekazać Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym na podstawie CentOS Linux."
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
ms.openlocfilehash: 010f4b05b35fa1f31c14f34a5fae9298fcd831e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="1786a-103">Przygotowywanie maszyny wirtualnej systemu CentOS dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1786a-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="1786a-104">Przygotowanie maszyny wirtualnej CentOS 6.x dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1786a-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="1786a-105">Przygotowanie maszyny wirtualnej CentOS 7.0 + Azure</span><span class="sxs-lookup"><span data-stu-id="1786a-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="1786a-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1786a-106">Prerequisites</span></span>
<span data-ttu-id="1786a-107">W tym artykule przyjęto założenie, zainstalowano CentOS (lub podobny pochodnej) systemu operacyjnego Linux do wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="1786a-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="1786a-108">Istnieje wiele narzędzi do tworzenia plików VHD, na przykład rozwiązanie wirtualizacji takich jak funkcja Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1786a-108">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="1786a-109">Aby uzyskać instrukcje, zobacz [Instalowanie roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="1786a-109">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="1786a-110">**Informacje o instalacji centOS**</span><span class="sxs-lookup"><span data-stu-id="1786a-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="1786a-111">Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="1786a-112">VHDX format jest nieobsługiwane w systemie Azure, tylko **stały VHD**.</span><span class="sxs-lookup"><span data-stu-id="1786a-112">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="1786a-113">Dysk można przekonwertować na format wirtualnego dysku twardego za pomocą Menedżera funkcji Hyper-V lub polecenia cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="1786a-113">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span> <span data-ttu-id="1786a-114">Jeśli używasz VirtualBox oznacza to, wybierając **stały rozmiar** zamiast domyślnego dynamicznie przydzielane podczas tworzenia dysku.</span><span class="sxs-lookup"><span data-stu-id="1786a-114">If you are using VirtualBox this means selecting **Fixed size** as opposed to the default dynamically allocated when creating the disk.</span></span>
* <span data-ttu-id="1786a-115">Podczas instalowania systemu Linux jest *zalecane* używasz standardowe partycje, a nie LVM (często domyślnie dla wielu instalacji).</span><span class="sxs-lookup"><span data-stu-id="1786a-115">When installing the Linux system it is *recommended* that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="1786a-116">Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, szczególnie, gdy dysk systemu operacyjnego kiedykolwiek musi być dołączona do innego identyczne maszyny Wirtualnej do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="1786a-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another identical VM for troubleshooting.</span></span> <span data-ttu-id="1786a-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="1786a-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="1786a-118">Wymagana jest obsługa jądra służący do instalowania systemów plików funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1786a-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="1786a-119">Przy pierwszym uruchomieniu komputera na platformie Azure konfiguracji inicjowania obsługi administracyjnej jest przekazywany do maszyny Wirtualnej systemu Linux za pomocą nośnika sformatowany UDF, dołączonego do gościa.</span><span class="sxs-lookup"><span data-stu-id="1786a-119">At first boot on Azure the provisioning configuration is passed to the Linux VM via UDF-formatted media that is attached to the guest.</span></span> <span data-ttu-id="1786a-120">Agent systemu Linux platformy Azure musi mieć możliwość zainstalowania systemu plików funkcji zdefiniowanej przez użytkownika do odczytu konfiguracji i udostępnić Maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1786a-120">The Azure Linux agent must be able to mount the UDF file system to read its configuration and provision the VM.</span></span>
* <span data-ttu-id="1786a-121">Wersje jądra systemu Linux poniżej 2.6.37 nie obsługują NUMA w funkcji Hyper-V o dużym rozmiarze maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1786a-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="1786a-122">Ten problem wpływa głównie na starszą dystrybucji przy użyciu nadrzędnego Red Hat 2.6.32 jądra i ustalono w RHEL 6.6 (jądra-2.6.32 504).</span><span class="sxs-lookup"><span data-stu-id="1786a-122">This issue primarily impacts older distributions using the upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="1786a-123">Komputerów z systemami niestandardowych jądra starsze niż 2.6.37 lub systemem RHEL jądra starsze niż 2.6.32-504 należy ustawić parametr rozruchowego `numa=off` na wiersza polecenia w grub.conf jądra.</span><span class="sxs-lookup"><span data-stu-id="1786a-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set the boot parameter `numa=off` on the kernel command-line in grub.conf.</span></span> <span data-ttu-id="1786a-124">Aby uzyskać więcej informacji, zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="1786a-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="1786a-125">Nie należy konfigurować wymiany partycji na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="1786a-125">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="1786a-126">Aby utworzyć plik wymiany na dysku zasobów można skonfigurować agenta systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="1786a-126">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="1786a-127">Więcej informacji na ten temat można znaleźć w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="1786a-127">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="1786a-128">Wszystkie wirtualne dyski twarde muszą mieć rozmiary, które są wielokrotności 1 MB.</span><span class="sxs-lookup"><span data-stu-id="1786a-128">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="1786a-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="1786a-129">CentOS 6.x</span></span>

1. <span data-ttu-id="1786a-130">W Menedżerze funkcji Hyper-V wybierz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="1786a-130">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="1786a-131">Kliknij przycisk **Connect** aby otworzyć okno konsoli dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1786a-131">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="1786a-132">W CentOS 6 NetworkManager może zakłócać agenta systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-132">In CentOS 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="1786a-133">Odinstalowania tego pakietu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1786a-133">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="1786a-134">Utwórz lub Edytuj plik `/etc/sysconfig/network` i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="1786a-134">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="1786a-135">Utwórz lub Edytuj plik `/etc/sysconfig/network-scripts/ifcfg-eth0` i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="1786a-135">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="1786a-136">Modyfikuj reguły udev, aby uniknąć generowania statyczne reguły dla interfejsów Ethernet.</span><span class="sxs-lookup"><span data-stu-id="1786a-136">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="1786a-137">Te reguły może spowodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="1786a-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="1786a-138">Upewnij się, że usługa sieci zostanie uruchomiona podczas rozruchu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1786a-138">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="1786a-139">Jeśli chcesz użyć wstecznych OpenLogic, które znajdują się w centrach danych platformy Azure, a następnie zastąp `/etc/yum.repos.d/CentOS-Base.repo` pliku z następujących repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="1786a-139">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="1786a-140">Spowoduje to również dodanie **[openlogic]** repozytorium, która obejmuje dodatkowe pakiety, takie jak agenta systemu Linux platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="1786a-140">This will also add the **[openlogic]** repository that includes additional packages such as the Azure Linux agent:</span></span>

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
    <span data-ttu-id="1786a-141">Pozostała część tego przewodnika zakłada, używane są co najmniej `[openlogic]` repozytorium, która będzie używana do zainstalowania agenta systemu Linux Azure poniżej.</span><span class="sxs-lookup"><span data-stu-id="1786a-141">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>


9. <span data-ttu-id="1786a-142">Dodaj następujący wiersz do /etc/yum.conf:</span><span class="sxs-lookup"><span data-stu-id="1786a-142">Add the following line to /etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="1786a-143">Uruchom następujące polecenie, aby wyczyścić bieżących metadanych yum i zaktualizuj system z najnowszych pakietów:</span><span class="sxs-lookup"><span data-stu-id="1786a-143">Run the following command to clear the current yum metadata and update the system with the latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="1786a-144">Jeśli tworzysz obrazu dla starszej wersji CentOS, zalecane jest wszystkich pakietów aktualizacji do najnowszej wersji:</span><span class="sxs-lookup"><span data-stu-id="1786a-144">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="1786a-145">Po uruchomieniu tego polecenia może być wymagane ponowne uruchomienie komputera.</span><span class="sxs-lookup"><span data-stu-id="1786a-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="1786a-146">(Opcjonalnie) Zainstaluj sterowniki dla usługi integracji systemu Linux (LIS).</span><span class="sxs-lookup"><span data-stu-id="1786a-146">(Optional) Install the drivers for the Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="1786a-147">Kroku **wymagane** dla CentOS 6.3 i wcześniejszych oraz opcjonalny w przypadku nowszych wersjach.</span><span class="sxs-lookup"><span data-stu-id="1786a-147">The step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="1786a-148">Alternatywnie, można wykonać instrukcje dotyczące ręcznej instalacji [stronę pobierania LIS](https://go.microsoft.com/fwlink/?linkid=403033) do zainstalowania obr. / min na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1786a-148">Alternatively, you can follow the manual installation instructions on the [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) to install the RPM onto your VM.</span></span>
 
12. <span data-ttu-id="1786a-149">Zainstaluj agenta systemu Linux platformy Azure i zależności:</span><span class="sxs-lookup"><span data-stu-id="1786a-149">Install the Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="1786a-150">Pakiet WALinuxAgent spowoduje usunięcie NetworkManager i pakiety NetworkManager gnome jeśli ich nie zostały już usunięte zgodnie z opisem w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="1786a-150">The WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="1786a-151">Zmodyfikuj wiersza rozruchu jądra w konfiguracji chodników uwzględnienie jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-151">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="1786a-152">Aby to zrobić, otwórz `/boot/grub/menu.lst` w edytorze tekstów i upewnij się, że jądra domyślna zawiera następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="1786a-152">To do this, open `/boot/grub/menu.lst` in a text editor and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="1786a-153">Dzięki konsoli komunikaty są wysyłane do pierwszego portu szeregowego może pomóc Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="1786a-153">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="1786a-154">Oprócz powyższego, zaleca się *Usuń* następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="1786a-154">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="1786a-155">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie dzienniki, które mają być wysyłane do portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="1786a-155">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="1786a-156">`crashkernel` Opcja może być skonfigurowany w razie potrzeby po lewej, ale należy pamiętać, że ten parametr zmniejsza ilość dostępnej pamięci w maszynie Wirtualnej najmniej 128 MB, które mogą być problemy na mniejsze rozmiary maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1786a-156">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="1786a-157">CentOS 6.5 lub starszej należy również ustawić parametr jądra `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="1786a-157">CentOS 6.5 and earlier must also set the kernel parameter `numa=off`.</span></span> <span data-ttu-id="1786a-158">Zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="1786a-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="1786a-159">Upewnij się, że serwer SSH jest zainstalowany i skonfigurowany do uruchamiania w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="1786a-159">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="1786a-160">Zazwyczaj jest to wartość domyślna.</span><span class="sxs-lookup"><span data-stu-id="1786a-160">This is usually the default.</span></span>

15. <span data-ttu-id="1786a-161">Nie należy tworzyć zamiany miejsca na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="1786a-161">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="1786a-162">Agent systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu dysku zasób lokalny, który jest dołączony do maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-162">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="1786a-163">Należy zauważyć, że dysk lokalny zasób *tymczasowego* na dysku i może opróżnić, gdy maszyna wirtualna jest anulowana.</span><span class="sxs-lookup"><span data-stu-id="1786a-163">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="1786a-164">Po zainstalowaniu agenta systemu Linux platformy Azure (zobacz poprzedni krok) i zmodyfikuj następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="1786a-164">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="1786a-165">Uruchom następujące polecenia, aby anulowanie zastrzeżenia maszyny wirtualnej i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="1786a-165">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="1786a-166">Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1786a-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="1786a-167">Dysk VHD systemu Linux jest teraz gotowy do przekazania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-167">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="1786a-168">CentOS 7.0 +</span><span class="sxs-lookup"><span data-stu-id="1786a-168">CentOS 7.0+</span></span>
<span data-ttu-id="1786a-169">**Zmiany w CentOS 7 (lub podobny pochodne)**</span><span class="sxs-lookup"><span data-stu-id="1786a-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="1786a-170">Przygotowywanie maszyny wirtualnej CentOS 7 dla platformy Azure jest bardzo podobny do CentOS 6, jednak istnieje kilka istotnych różnic, warto zauważyć:</span><span class="sxs-lookup"><span data-stu-id="1786a-170">Preparing a CentOS 7 virtual machine for Azure is very similar to CentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="1786a-171">Pakiet NetworkManager nie powodował konfliktu z agentem systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-171">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="1786a-172">Ten pakiet jest instalowany domyślnie i zaleca się, że nie zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="1786a-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="1786a-173">GRUB2 teraz jest używana jako inicjującego domyślne, więc procedury do edycji parametry jądra został zmieniony (patrz poniżej).</span><span class="sxs-lookup"><span data-stu-id="1786a-173">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="1786a-174">XFS jest teraz domyślny system plików.</span><span class="sxs-lookup"><span data-stu-id="1786a-174">XFS is now the default file system.</span></span> <span data-ttu-id="1786a-175">Nadal można ext4 systemu plików, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="1786a-175">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="1786a-176">**Kroki konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="1786a-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="1786a-177">W Menedżerze funkcji Hyper-V wybierz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="1786a-177">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="1786a-178">Kliknij przycisk **Connect** aby otworzyć okno konsoli dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1786a-178">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="1786a-179">Utwórz lub Edytuj plik `/etc/sysconfig/network` i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="1786a-179">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="1786a-180">Utwórz lub Edytuj plik `/etc/sysconfig/network-scripts/ifcfg-eth0` i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="1786a-180">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="1786a-181">Modyfikuj reguły udev, aby uniknąć generowania statyczne reguły dla interfejsów Ethernet.</span><span class="sxs-lookup"><span data-stu-id="1786a-181">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="1786a-182">Te reguły może spowodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="1786a-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="1786a-183">Jeśli chcesz użyć wstecznych OpenLogic, które znajdują się w centrach danych platformy Azure, a następnie zastąp `/etc/yum.repos.d/CentOS-Base.repo` pliku z następujących repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="1786a-183">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="1786a-184">Spowoduje to również dodanie **[openlogic]** repozytorium, zawierającą pakietów dla agenta systemu Linux platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="1786a-184">This will also add the **[openlogic]** repository that includes packages for the Azure Linux agent:</span></span>
   
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
    <span data-ttu-id="1786a-185">Pozostała część tego przewodnika zakłada, używane są co najmniej `[openlogic]` repozytorium, która będzie używana do zainstalowania agenta systemu Linux Azure poniżej.</span><span class="sxs-lookup"><span data-stu-id="1786a-185">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>

7. <span data-ttu-id="1786a-186">Uruchom następujące polecenie, aby wyczyścić bieżący metadanych yum i zainstaluj wszystkie aktualizacje:</span><span class="sxs-lookup"><span data-stu-id="1786a-186">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="1786a-187">Jeśli tworzysz obrazu dla starszej wersji CentOS, zalecane jest wszystkich pakietów aktualizacji do najnowszej wersji:</span><span class="sxs-lookup"><span data-stu-id="1786a-187">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="1786a-188">Ponowne uruchomienie, może być wymagane po uruchomieniu tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="1786a-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="1786a-189">Zmodyfikuj wiersza rozruchu jądra w konfiguracji chodników uwzględnienie jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-189">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="1786a-190">Aby to zrobić, otwórz `/etc/default/grub` w edytorze tekstów i edytowanie `GRUB_CMDLINE_LINUX` parametrów, na przykład:</span><span class="sxs-lookup"><span data-stu-id="1786a-190">To do this, open `/etc/default/grub` in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="1786a-191">Dzięki konsoli komunikaty są wysyłane do pierwszego portu szeregowego może pomóc Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="1786a-191">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="1786a-192">On również wyłącza nowe CentOS 7 konwencje nazewnictwa dla kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="1786a-192">It also turns off the new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="1786a-193">Oprócz powyższego, zaleca się *Usuń* następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="1786a-193">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="1786a-194">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie dzienniki, które mają być wysyłane do portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="1786a-194">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="1786a-195">`crashkernel` Opcja może być skonfigurowany w razie potrzeby po lewej, ale należy pamiętać, że ten parametr zmniejsza ilość dostępnej pamięci w maszynie Wirtualnej najmniej 128 MB, które mogą być problemy na mniejsze rozmiary maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1786a-195">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

9. <span data-ttu-id="1786a-196">Po zakończeniu edycji `/etc/default/grub` na powyżej, uruchom następujące polecenie, aby odbudować chodników konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="1786a-196">Once you are done editing `/etc/default/grub` per above, run the following command to rebuild the grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="1786a-197">Jeśli tworzenie obrazu z **VMWare, VirtualBox lub KVM:** funkcji Hyper-V upewnij się, że sterowniki są uwzględnione w initramfs:</span><span class="sxs-lookup"><span data-stu-id="1786a-197">If building the image from **VMWare, VirtualBox or KVM:** Ensure the Hyper-V drivers are included in the initramfs:</span></span>
   
   <span data-ttu-id="1786a-198">Edytuj `/etc/dracut.conf`, Dodaj zawartość:</span><span class="sxs-lookup"><span data-stu-id="1786a-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="1786a-199">Odbuduj initramfs:</span><span class="sxs-lookup"><span data-stu-id="1786a-199">Rebuild the initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="1786a-200">Zainstaluj agenta systemu Linux platformy Azure i zależności:</span><span class="sxs-lookup"><span data-stu-id="1786a-200">Install the Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="1786a-201">Nie należy tworzyć zamiany miejsca na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="1786a-201">Do not create swap space on the OS disk.</span></span>
   
   <span data-ttu-id="1786a-202">Agent systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu dysku zasób lokalny, który jest dołączony do maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-202">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="1786a-203">Należy zauważyć, że dysk lokalny zasób *tymczasowego* na dysku i może opróżnić, gdy maszyna wirtualna jest anulowana.</span><span class="sxs-lookup"><span data-stu-id="1786a-203">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="1786a-204">Po zainstalowaniu agenta systemu Linux platformy Azure (zobacz poprzedni krok) i zmodyfikuj następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="1786a-204">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="1786a-205">Uruchom następujące polecenia, aby anulowanie zastrzeżenia maszyny wirtualnej i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="1786a-205">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="1786a-206">Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1786a-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="1786a-207">Dysk VHD systemu Linux jest teraz gotowy do przekazania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-207">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1786a-208">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1786a-208">Next steps</span></span>
<span data-ttu-id="1786a-209">Teraz możesz używać wirtualnego dysku twardego systemu CentOS Linux do tworzenia nowych maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1786a-209">You're now ready to use your CentOS Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="1786a-210">Jeśli jest to czy jest przekazywanie pliku VHD na platformę Azure po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1786a-210">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

