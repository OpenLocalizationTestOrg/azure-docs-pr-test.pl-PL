---
title: "aaaCreate i przekazać Red Hat Enterprise Linux wirtualnego dysku twardego do użycia na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się toocreate i przekaż Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym Red Hat Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/28/2017
ms.author: szark
ms.openlocfilehash: bdd1bbfbee55b5cc61d69a09b06b6bd2c3de362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="da37b-103">Przygotowywanie maszyny wirtualnej systemu Red Hat dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="da37b-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="da37b-104">W tym artykule przedstawiono sposób tooprepare maszynę wirtualną Red Hat Enterprise Linux (RHEL) do użycia na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-104">In this article, you will learn how tooprepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="da37b-105">Hello wersje RHEL, które zostały omówione w tym artykule są 6.7 + i 7.1 +.</span><span class="sxs-lookup"><span data-stu-id="da37b-105">hello versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="da37b-106">Witaj funkcji hypervisor w celu przygotowania, które zostały omówione w tym artykule są maszyny wirtualnej funkcji Hyper-V, na podstawie jądra (KVM) i VMware.</span><span class="sxs-lookup"><span data-stu-id="da37b-106">hello hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="da37b-107">Aby uzyskać więcej informacji o wymaganiach dotyczących kwalifikuje się do uczestnictwa w programie dostęp do chmury Red Hat, zobacz [Red Hat dostęp do chmury witryny sieci Web](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) i [systemem RHEL na platformie Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="da37b-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="da37b-108">Przygotowywanie maszyny wirtualnej z systemem Red Hat z Menedżera funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="da37b-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="da37b-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="da37b-109">Prerequisites</span></span>
<span data-ttu-id="da37b-110">W tej sekcji założono już uzyskane plik ISO z witryny sieci Web hello Red Hat i zainstalowanych hello RHEL obrazu tooa wirtualnego dysku twardego (VHD).</span><span class="sxs-lookup"><span data-stu-id="da37b-110">This section assumes that you have already obtained an ISO file from hello Red Hat website and installed hello RHEL image tooa virtual hard disk (VHD).</span></span> <span data-ttu-id="da37b-111">Aby uzyskać więcej informacji o tym, jak toouse Menedżera funkcji Hyper-V tooinstall obrazu systemu operacyjnego, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="da37b-111">For more details about how toouse Hyper-V Manager tooinstall an operating system image, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="da37b-112">**RHEL uwagi instalacji**</span><span class="sxs-lookup"><span data-stu-id="da37b-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="da37b-113">Azure nie obsługuje formatu VHDX hello.</span><span class="sxs-lookup"><span data-stu-id="da37b-113">Azure does not support hello VHDX format.</span></span> <span data-ttu-id="da37b-114">Azure obsługuje tylko stałe wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="da37b-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="da37b-115">Można użyć formatu tooVHD dysku hello tooconvert Menedżera funkcji Hyper-V, lub można użyć polecenia cmdlet convert-vhd hello.</span><span class="sxs-lookup"><span data-stu-id="da37b-115">You can use Hyper-V Manager tooconvert hello disk tooVHD format, or you can use hello convert-vhd cmdlet.</span></span> <span data-ttu-id="da37b-116">Jeśli używasz VirtualBox, wybierz **stały rozmiar** nazwą domyślną toohello dynamicznie przydzielane opcji podczas tworzenia dysku hello.</span><span class="sxs-lookup"><span data-stu-id="da37b-116">If you use VirtualBox, select **Fixed size** as opposed toohello default dynamically allocated option when you create hello disk.</span></span>
* <span data-ttu-id="da37b-117">Azure obsługuje tylko maszyny wirtualne generacji 1.</span><span class="sxs-lookup"><span data-stu-id="da37b-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="da37b-118">Maszyny wirtualne generacji 1 można przekonwertować z formatu pliku wirtualnego dysku twardego toohello VHDX i dynamicznie powiększający się dysk o stałym rozmiarze tooa.</span><span class="sxs-lookup"><span data-stu-id="da37b-118">You can convert a generation 1 virtual machine from VHDX toohello VHD file format and from dynamically expanding tooa fixed-size disk.</span></span> <span data-ttu-id="da37b-119">Nie można zmienić generację maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="da37b-120">Aby uzyskać więcej informacji, zobacz [należy tworzyć maszyny wirtualne generacji 1 lub 2 w funkcji Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="da37b-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="da37b-121">Witaj maksymalny rozmiar, jaki jest dozwolony dla hello wirtualnego dysku twardego jest 1,023 GB.</span><span class="sxs-lookup"><span data-stu-id="da37b-121">hello maximum size that's allowed for hello VHD is 1,023 GB.</span></span>
* <span data-ttu-id="da37b-122">Po zainstalowaniu systemu operacyjnego Linux hello firma Microsoft zaleca użycie standardowe partycje, a nie logiczne woluminu Manager (LVM), często jest domyślna powitania dla wielu urządzeń.</span><span class="sxs-lookup"><span data-stu-id="da37b-122">When you install hello Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often hello default for many installations.</span></span> <span data-ttu-id="da37b-123">Takie rozwiązanie pozwoli uniknąć LVM nazwa powoduje konflikt z sklonowane maszyny wirtualne, szczególnie jeśli kiedykolwiek zajdzie tooattach system operacyjny dysku tooanother identycznej maszyny wirtualnej do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="da37b-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need tooattach an operating system disk tooanother identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="da37b-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="da37b-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="da37b-125">Wymagana jest obsługa jądra służący do instalowania systemów plików uniwersalny Format dysku (UDF).</span><span class="sxs-lookup"><span data-stu-id="da37b-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="da37b-126">Przy pierwszym uruchomieniu komputera, na platformy Azure, nośnik hello sformatowany funkcji zdefiniowanej przez użytkownika, który jest dołączony toohello gościa przekazuje hello inicjowania obsługi administracyjnej toohello konfiguracji maszyny wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="da37b-126">At first boot on Azure, hello UDF-formatted media that is attached toohello guest passes hello provisioning configuration toohello Linux virtual machine.</span></span> <span data-ttu-id="da37b-127">Hello agenta systemu Linux platformy Azure musi być możliwe toomount hello UDF pliku system tooread swojej konfiguracji i aprowizowanie maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="da37b-127">hello Azure Linux Agent must be able toomount hello UDF file system tooread its configuration and provision hello virtual machine.</span></span>
* <span data-ttu-id="da37b-128">Wersje starsze niż 2.6.37 hello jądra systemu Linux nie obsługują dostępu niejednolitego pamięci (NUMA) w ramach funkcji Hyper-V o dużym rozmiarze maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-128">Versions of hello Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="da37b-129">Ten problem wpływa głównie na starszą dystrybucje Użyj powitania od jądra Red Hat 2.6.32 zostało ustalone w 6.6 RHEL (jądra-2.6.32 504).</span><span class="sxs-lookup"><span data-stu-id="da37b-129">This issue primarily impacts older distributions that use hello upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="da37b-130">Systemy, systemem jądra niestandardowych, które są starsze niż 2.6.37 lub systemem RHEL jądra, które są starsze niż 2.6.32-504 należy ustawić hello `numa=off` rozruch parametru w wierszu polecenia jądra hello grub.conf.</span><span class="sxs-lookup"><span data-stu-id="da37b-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set hello `numa=off` boot parameter on hello kernel command line in grub.conf.</span></span> <span data-ttu-id="da37b-131">Aby uzyskać więcej informacji, zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="da37b-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="da37b-132">Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="da37b-132">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="da37b-133">Witaj agenta systemu Linux może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.</span><span class="sxs-lookup"><span data-stu-id="da37b-133">hello Linux Agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="da37b-134">Więcej informacji na ten temat można znaleźć w hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="da37b-134">More information about this can be found in hello following steps.</span></span>
* <span data-ttu-id="da37b-135">Wszystkie wirtualne dyski twarde muszą mieć rozmiary, które są wielokrotności 1 MB.</span><span class="sxs-lookup"><span data-stu-id="da37b-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="da37b-136">Przygotowanie RHEL 6 maszyny wirtualnej z Menedżera funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="da37b-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="da37b-137">W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-137">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="da37b-138">Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-138">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="da37b-139">6 RHEL NetworkManager może zakłócać hello agenta systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-139">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="da37b-140">Odinstalowania tego pakietu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-140">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="da37b-141">Utwórz lub Edytuj hello `/etc/sysconfig/network` pliku, a następnie dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-141">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="da37b-142">Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-142">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="da37b-143">Przenieś (albo usuń) tooavoid reguły udev hello generowania statycznych zasady hello interfejs typu Ethernet.</span><span class="sxs-lookup"><span data-stu-id="da37b-143">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="da37b-144">Te reguły powodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="da37b-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="da37b-145">Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-145">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="da37b-146">Zarejestruj Red Hat subskrypcji tooenable hello instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-146">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="da37b-147">Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="da37b-147">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="da37b-148">Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-148">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="da37b-149">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-149">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="da37b-150">toodo modyfikacji, otwórz `/boot/grub/menu.lst` w edytorze tekstu i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="da37b-150">toodo this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="da37b-151">To będzie również upewnij się, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="da37b-151">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="da37b-152">Ponadto zaleca się usunięcie hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="da37b-152">In addition, we recommended that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="da37b-153">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="da37b-153">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>  <span data-ttu-id="da37b-154">Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="da37b-154">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="da37b-155">Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB.</span><span class="sxs-lookup"><span data-stu-id="da37b-155">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more.</span></span> <span data-ttu-id="da37b-156">Ta konfiguracja może być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="da37b-157">RHEL 6.5 lub starszej należy również ustawić hello `numa=off` parametru jądra.</span><span class="sxs-lookup"><span data-stu-id="da37b-157">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="da37b-158">Zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="da37b-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="da37b-159">Upewnij się, powitania serwera bezpiecznej powłoki (SSH) jest zainstalowany i skonfigurowany toostart w czasie rozruchu, która zwykle jest domyślnie hello.</span><span class="sxs-lookup"><span data-stu-id="da37b-159">Ensure that hello secure shell (SSH) server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="da37b-160">Modyfikowanie hello tooinclude /etc/ssh/sshd_config po wierszu:</span><span class="sxs-lookup"><span data-stu-id="da37b-160">Modify /etc/ssh/sshd_config tooinclude hello following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="da37b-161">Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-161">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="da37b-162">Instalowanie pakietu WALinuxAgent hello usuwa hello NetworkManager i NetworkManager gnome pakietów, jeśli ich nie zostały już usunięte w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="da37b-162">Installing hello WALinuxAgent package removes hello NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="da37b-163">Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="da37b-163">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="da37b-164">Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-164">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="da37b-165">Należy pamiętać, tym hello lokalnych zasobów dysk jest dyskiem tymczasowego i czy mogą być opróżniany podczas hello maszyny wirtualnej jest anulowana.</span><span class="sxs-lookup"><span data-stu-id="da37b-165">Note that hello local resource disk is a temporary disk and that it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="da37b-166">Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować odpowiednio następujące parametry w /etc/waagent.conf hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-166">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

14. <span data-ttu-id="da37b-167">Wyrejestruj hello subskrypcji (w razie potrzeby), uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-167">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="da37b-168">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="da37b-168">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="da37b-169">Kliknij przycisk **akcji** > **zamknąć** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="da37b-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="da37b-170">Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.</span><span class="sxs-lookup"><span data-stu-id="da37b-170">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="da37b-171">Przygotowanie RHEL 7 maszyny wirtualnej z Menedżera funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="da37b-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="da37b-172">W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-172">In Hyper-V Manager, select hello virtual machine.</span></span>

2. <span data-ttu-id="da37b-173">Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-173">Click **Connect** tooopen a console window for hello virtual machine.</span></span>

3. <span data-ttu-id="da37b-174">Utwórz lub Edytuj hello `/etc/sysconfig/network` pliku, a następnie dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-174">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="da37b-175">Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-175">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="da37b-176">Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-176">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="da37b-177">Zarejestruj Red Hat subskrypcji tooenable hello instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-177">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="da37b-178">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-178">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="da37b-179">toodo modyfikacji, otwórz `/etc/default/grub` w edytorze tekstów i Edycja hello `GRUB_CMDLINE_LINUX` parametru.</span><span class="sxs-lookup"><span data-stu-id="da37b-179">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="da37b-180">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="da37b-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="da37b-181">To będzie również upewnij się, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="da37b-181">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="da37b-182">Ta konfiguracja również wyłącza hello nowych systemów RHEL 7 konwencji nazewnictwa, dla kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="da37b-182">This configuration also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="da37b-183">Ponadto zaleca się usunięcie hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="da37b-183">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="da37b-184">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="da37b-184">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="da37b-185">Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="da37b-185">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="da37b-186">Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-186">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="da37b-187">Po zakończeniu edycji `/etc/default/grub`Uruchom hello następujące polecenia toorebuild hello chodników konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="da37b-187">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="da37b-188">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu, która zwykle jest domyślnie hello.</span><span class="sxs-lookup"><span data-stu-id="da37b-188">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="da37b-189">Modyfikowanie `/etc/ssh/sshd_config` hello tooinclude po wierszu:</span><span class="sxs-lookup"><span data-stu-id="da37b-189">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="da37b-190">Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="da37b-190">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="da37b-191">Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-191">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="da37b-192">Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-192">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="da37b-193">Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="da37b-193">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="da37b-194">Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-194">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="da37b-195">Należy pamiętać, że hello zasób lokalny dysk jest tymczasowe i może opróżnić, gdy maszyna wirtualna hello jest anulowaną aprowizacją.</span><span class="sxs-lookup"><span data-stu-id="da37b-195">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="da37b-196">Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować hello następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="da37b-196">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="da37b-197">Jeśli chcesz toounregister hello subskrypcji, uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="da37b-197">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="da37b-198">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="da37b-198">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="da37b-199">Kliknij przycisk **akcji** > **zamknąć** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="da37b-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="da37b-200">Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.</span><span class="sxs-lookup"><span data-stu-id="da37b-200">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="da37b-201">Przygotowywanie maszyny wirtualnej z systemem Red Hat z KVM</span><span class="sxs-lookup"><span data-stu-id="da37b-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="da37b-202">Przygotowanie maszyny wirtualnej RHEL 6 z KVM</span><span class="sxs-lookup"><span data-stu-id="da37b-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="da37b-203">Pobierz obraz KVM hello 6 RHEL z hello Red Hat witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="da37b-203">Download hello KVM image of RHEL 6 from hello Red Hat website.</span></span>

2. <span data-ttu-id="da37b-204">Ustaw hasło główne.</span><span class="sxs-lookup"><span data-stu-id="da37b-204">Set a root password.</span></span>

    <span data-ttu-id="da37b-205">Generowanie zaszyfrowane hasło, a następnie skopiuj dane wyjściowe polecenia hello hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-205">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="da37b-206">Ustaw hasło główne z guestfish:</span><span class="sxs-lookup"><span data-stu-id="da37b-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="da37b-207">Zmień hello drugie pole hello głównego użytkownika z "!"</span><span class="sxs-lookup"><span data-stu-id="da37b-207">Change hello second field of hello root user from "!!"</span></span> <span data-ttu-id="da37b-208">toohello zaszyfrowane hasło.</span><span class="sxs-lookup"><span data-stu-id="da37b-208">toohello encrypted password.</span></span>

3. <span data-ttu-id="da37b-209">Utwórz maszynę wirtualną w KVM hello qcow2 obrazu.</span><span class="sxs-lookup"><span data-stu-id="da37b-209">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="da37b-210">Ustaw typ dysku hello zbyt**qcow2**i ustaw model urządzenia interfejsu sieci wirtualnej hello zbyt**virtio**.</span><span class="sxs-lookup"><span data-stu-id="da37b-210">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="da37b-211">Następnie uruchom maszynę wirtualną hello i zaloguj się jako katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="da37b-211">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="da37b-212">Utwórz lub Edytuj hello `/etc/sysconfig/network` pliku, a następnie dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-212">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="da37b-213">Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-213">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="da37b-214">Przenieś (albo usuń) tooavoid reguły udev hello generowania statycznych zasady hello interfejs typu Ethernet.</span><span class="sxs-lookup"><span data-stu-id="da37b-214">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="da37b-215">Te reguły powodować problemy podczas klonowania maszyny wirtualnej Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="da37b-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="da37b-216">Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-216">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="da37b-217">Zarejestruj Red Hat subskrypcji tooenable hello instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-217">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="da37b-218">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-218">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="da37b-219">toodo tej konfiguracji, otwórz `/boot/grub/menu.lst` w edytorze tekstu i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="da37b-219">toodo this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that hello default kernel includes hello following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="da37b-220">To będzie również upewnij się, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="da37b-220">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="da37b-221">Ponadto zaleca się usunięcie hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="da37b-221">In addition, we recommend that you remove hello following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="da37b-222">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="da37b-222">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="da37b-223">Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="da37b-223">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="da37b-224">Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-224">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="da37b-225">RHEL 6.5 lub starszej należy również ustawić hello `numa=off` parametru jądra.</span><span class="sxs-lookup"><span data-stu-id="da37b-225">RHEL 6.5 and earlier must also set hello `numa=off` kernel parameter.</span></span> <span data-ttu-id="da37b-226">Zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="da37b-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="da37b-227">Dodawanie funkcji Hyper-V tooinitramfs modułów:</span><span class="sxs-lookup"><span data-stu-id="da37b-227">Add Hyper-V modules tooinitramfs:</span></span>  

    <span data-ttu-id="da37b-228">Edytuj `/etc/dracut.conf`i Dodaj hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="da37b-228">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="da37b-229">Odbuduj initramfs:</span><span class="sxs-lookup"><span data-stu-id="da37b-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="da37b-230">Odinstaluj init chmury:</span><span class="sxs-lookup"><span data-stu-id="da37b-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="da37b-231">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu:</span><span class="sxs-lookup"><span data-stu-id="da37b-231">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="da37b-232">Modyfikowanie hello tooinclude /etc/ssh/sshd_config następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="da37b-232">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="da37b-233">Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="da37b-233">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="da37b-234">Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-234">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="da37b-235">Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-235">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="da37b-236">Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-236">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="da37b-237">Należy pamiętać, że hello zasób lokalny dysk jest tymczasowe i może opróżnić, gdy maszyna wirtualna hello jest anulowaną aprowizacją.</span><span class="sxs-lookup"><span data-stu-id="da37b-237">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="da37b-238">Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować hello następujące parametry w **/etc/waagent.conf** odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="da37b-238">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="da37b-239">Wyrejestruj hello subskrypcji (w razie potrzeby), uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-239">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="da37b-240">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="da37b-240">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="da37b-241">Zamknij maszynę wirtualną hello w KVM.</span><span class="sxs-lookup"><span data-stu-id="da37b-241">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="da37b-242">Konwertowanie formatu wirtualnego dysku twardego toohello hello qcow2 obrazu.</span><span class="sxs-lookup"><span data-stu-id="da37b-242">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="da37b-243">Najpierw przekonwertować format tooraw obrazu hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-243">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="da37b-244">Upewnij się, że rozmiar hello nieprzetworzone hello jest zgodne z 1 MB.</span><span class="sxs-lookup"><span data-stu-id="da37b-244">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="da37b-245">W przeciwnym razie zaokrąglij w górę tooalign rozmiar hello z 1 MB:</span><span class="sxs-lookup"><span data-stu-id="da37b-245">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="da37b-246">Konwertuj hello tooa raw dysku stałym rozmiarze wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="da37b-246">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="da37b-247">Przygotowanie maszyny wirtualnej RHEL 7 z KVM</span><span class="sxs-lookup"><span data-stu-id="da37b-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="da37b-248">Pobierz obraz KVM hello RHEL 7 z hello Red Hat witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="da37b-248">Download hello KVM image of RHEL 7 from hello Red Hat website.</span></span> <span data-ttu-id="da37b-249">Ta procedura wykorzystuje RHEL 7 jako przykład Witaj.</span><span class="sxs-lookup"><span data-stu-id="da37b-249">This procedure uses RHEL 7 as hello example.</span></span>

2. <span data-ttu-id="da37b-250">Ustaw hasło główne.</span><span class="sxs-lookup"><span data-stu-id="da37b-250">Set a root password.</span></span>

    <span data-ttu-id="da37b-251">Generowanie zaszyfrowane hasło, a następnie skopiuj dane wyjściowe polecenia hello hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-251">Generate an encrypted password, and copy hello output of hello command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="da37b-252">Ustaw hasło główne z guestfish:</span><span class="sxs-lookup"><span data-stu-id="da37b-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="da37b-253">Zmień hello drugie pole użytkownika głównego z "!"</span><span class="sxs-lookup"><span data-stu-id="da37b-253">Change hello second field of root user from "!!"</span></span> <span data-ttu-id="da37b-254">toohello zaszyfrowane hasło.</span><span class="sxs-lookup"><span data-stu-id="da37b-254">toohello encrypted password.</span></span>

3. <span data-ttu-id="da37b-255">Utwórz maszynę wirtualną w KVM hello qcow2 obrazu.</span><span class="sxs-lookup"><span data-stu-id="da37b-255">Create a virtual machine in KVM from hello qcow2 image.</span></span> <span data-ttu-id="da37b-256">Ustaw typ dysku hello zbyt**qcow2**i ustaw model urządzenia interfejsu sieci wirtualnej hello zbyt**virtio**.</span><span class="sxs-lookup"><span data-stu-id="da37b-256">Set hello disk type too**qcow2**, and set hello virtual network interface device model too**virtio**.</span></span> <span data-ttu-id="da37b-257">Następnie uruchom maszynę wirtualną hello i zaloguj się jako katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="da37b-257">Then, start hello virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="da37b-258">Utwórz lub Edytuj hello `/etc/sysconfig/network` pliku, a następnie dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-258">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="da37b-259">Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-259">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="da37b-260">Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-260">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="da37b-261">Zarejestruj Red Hat subskrypcji tooenable instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-261">Register your Red Hat subscription tooenable installation of packages from hello RHEL repository by running hello following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="da37b-262">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-262">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="da37b-263">toodo tej konfiguracji, otwórz `/etc/default/grub` w edytorze tekstów i Edycja hello `GRUB_CMDLINE_LINUX` parametru.</span><span class="sxs-lookup"><span data-stu-id="da37b-263">toodo this configuration, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="da37b-264">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="da37b-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="da37b-265">To polecenie sprawia, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="da37b-265">This command also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="da37b-266">polecenie Hello również wyłącza hello nowych systemów RHEL 7 konwencji nazewnictwa, dla kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="da37b-266">hello command also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="da37b-267">Ponadto zaleca się usunięcie hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="da37b-267">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="da37b-268">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="da37b-268">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="da37b-269">Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="da37b-269">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="da37b-270">Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-270">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="da37b-271">Po zakończeniu edycji `/etc/default/grub`Uruchom hello następujące polecenia toorebuild hello chodników konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="da37b-271">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="da37b-272">Dodawanie modułów funkcji Hyper-V do initramfs.</span><span class="sxs-lookup"><span data-stu-id="da37b-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="da37b-273">Edytuj `/etc/dracut.conf` i Dodaj zawartość:</span><span class="sxs-lookup"><span data-stu-id="da37b-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="da37b-274">Odbuduj initramfs:</span><span class="sxs-lookup"><span data-stu-id="da37b-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="da37b-275">Odinstaluj init chmury:</span><span class="sxs-lookup"><span data-stu-id="da37b-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="da37b-276">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu:</span><span class="sxs-lookup"><span data-stu-id="da37b-276">Ensure that hello SSH server is installed and configured toostart at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="da37b-277">Modyfikowanie hello tooinclude /etc/ssh/sshd_config następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="da37b-277">Modify /etc/ssh/sshd_config tooinclude hello following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="da37b-278">Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="da37b-278">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="da37b-279">Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-279">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="da37b-280">Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-280">Install hello Azure Linux Agent by running hello following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="da37b-281">Włącz usługę agenta waagent hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-281">Enable hello waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="da37b-282">Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="da37b-282">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="da37b-283">Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-283">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="da37b-284">Należy pamiętać, że hello zasób lokalny dysk jest tymczasowe i może opróżnić, gdy maszyna wirtualna hello jest anulowaną aprowizacją.</span><span class="sxs-lookup"><span data-stu-id="da37b-284">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="da37b-285">Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować hello następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="da37b-285">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

16. <span data-ttu-id="da37b-286">Wyrejestruj hello subskrypcji (w razie potrzeby), uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-286">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="da37b-287">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="da37b-287">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="da37b-288">Zamknij maszynę wirtualną hello w KVM.</span><span class="sxs-lookup"><span data-stu-id="da37b-288">Shut down hello virtual machine in KVM.</span></span>

19. <span data-ttu-id="da37b-289">Konwertowanie formatu wirtualnego dysku twardego toohello hello qcow2 obrazu.</span><span class="sxs-lookup"><span data-stu-id="da37b-289">Convert hello qcow2 image toohello VHD format.</span></span>

    <span data-ttu-id="da37b-290">Najpierw przekonwertować format tooraw obrazu hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-290">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="da37b-291">Upewnij się, że rozmiar hello nieprzetworzone hello jest zgodne z 1 MB.</span><span class="sxs-lookup"><span data-stu-id="da37b-291">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="da37b-292">W przeciwnym razie zaokrąglij w górę tooalign rozmiar hello z 1 MB:</span><span class="sxs-lookup"><span data-stu-id="da37b-292">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="da37b-293">Konwertuj hello tooa raw dysku stałym rozmiarze wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="da37b-293">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="da37b-294">Przygotowywanie maszyny wirtualnej z systemem Red Hat z programu VMware</span><span class="sxs-lookup"><span data-stu-id="da37b-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="da37b-295">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="da37b-295">Prerequisites</span></span>
<span data-ttu-id="da37b-296">W tej sekcji założono, zainstalowano RHEL maszyny wirtualnej w środowisku programu VMware.</span><span class="sxs-lookup"><span data-stu-id="da37b-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="da37b-297">Aby uzyskać więcej informacji o tooinstall systemu operacyjnego w programie VMware, zobacz temat [Przewodnik instalacji systemu operacyjnego gościa VMware](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="da37b-297">For details about how tooinstall an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="da37b-298">Po zainstalowaniu systemu operacyjnego Linux hello firma Microsoft zaleca użycie standardowe partycje, a nie LVM, często jest domyślna powitania dla wielu urządzeń.</span><span class="sxs-lookup"><span data-stu-id="da37b-298">When you install hello Linux operating system, we recommend that you use standard partitions rather than LVM, which is often hello default for many installations.</span></span> <span data-ttu-id="da37b-299">Pozwoli to uniknąć konfliktów nazw LVM ze sklonowanej maszyny wirtualnej, szczególnie w przypadku, jeśli kiedykolwiek dysku systemu operacyjnego musi maszyny wirtualnej tooanother toobe dołączony do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="da37b-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs toobe attached tooanother virtual machine for troubleshooting.</span></span> <span data-ttu-id="da37b-300">LVM RAID można lub na dyskach danych, jeśli preferowane.</span><span class="sxs-lookup"><span data-stu-id="da37b-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="da37b-301">Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="da37b-301">Do not configure a swap partition on hello operating system disk.</span></span> <span data-ttu-id="da37b-302">Można skonfigurować hello Linux agent toocreate pliku wymiany na powitania zasobów dysku.</span><span class="sxs-lookup"><span data-stu-id="da37b-302">You can configure hello Linux agent toocreate a swap file on hello temporary resource disk.</span></span> <span data-ttu-id="da37b-303">Więcej informacji na ten temat można znaleźć w hello kroki, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="da37b-303">You can find more information about this in hello steps that follow.</span></span>
* <span data-ttu-id="da37b-304">Podczas tworzenia wirtualnego dysku twardego hello wybrać **magazynu wirtualnego dysku w postaci jednego pliku**.</span><span class="sxs-lookup"><span data-stu-id="da37b-304">When you create hello virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="da37b-305">Przygotowanie RHEL 6 maszyny wirtualnej z programu VMware</span><span class="sxs-lookup"><span data-stu-id="da37b-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="da37b-306">6 RHEL NetworkManager może zakłócać hello agenta systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-306">In RHEL 6, NetworkManager can interfere with hello Azure Linux agent.</span></span> <span data-ttu-id="da37b-307">Odinstalowania tego pakietu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-307">Uninstall this package by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="da37b-308">Utwórz plik o nazwie **sieci** w hello/etc/sysconfig/katalogu, który zawiera hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-308">Create a file named **network** in hello /etc/sysconfig/ directory that contains hello following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="da37b-309">Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-309">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="da37b-310">Przenieś (albo usuń) tooavoid reguły udev hello generowania statycznych zasady hello interfejs typu Ethernet.</span><span class="sxs-lookup"><span data-stu-id="da37b-310">Move (or remove) hello udev rules tooavoid generating static rules for hello Ethernet interface.</span></span> <span data-ttu-id="da37b-311">Te reguły powodować problemy podczas klonowania maszyny wirtualnej Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="da37b-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="da37b-312">Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-312">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="da37b-313">Zarejestruj Red Hat subskrypcji tooenable hello instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-313">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="da37b-314">Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="da37b-314">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="da37b-315">Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-315">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="da37b-316">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-316">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="da37b-317">toodo, otwórz `/etc/default/grub` w edytorze tekstów i Edycja hello `GRUB_CMDLINE_LINUX` parametru.</span><span class="sxs-lookup"><span data-stu-id="da37b-317">toodo this, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="da37b-318">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="da37b-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="da37b-319">To będzie również upewnij się, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="da37b-319">This will also ensure that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="da37b-320">Ponadto zaleca się usunięcie hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="da37b-320">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="da37b-321">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="da37b-321">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="da37b-322">Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="da37b-322">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="da37b-323">Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-323">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="da37b-324">Dodawanie funkcji Hyper-V tooinitramfs modułów:</span><span class="sxs-lookup"><span data-stu-id="da37b-324">Add Hyper-V modules tooinitramfs:</span></span>

    <span data-ttu-id="da37b-325">Edytuj `/etc/dracut.conf`i Dodaj hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="da37b-325">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="da37b-326">Odbuduj initramfs:</span><span class="sxs-lookup"><span data-stu-id="da37b-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="da37b-327">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu, która zwykle jest domyślnie hello.</span><span class="sxs-lookup"><span data-stu-id="da37b-327">Ensure that hello SSH server is installed and configured toostart at boot time, which is usually hello default.</span></span> <span data-ttu-id="da37b-328">Modyfikowanie `/etc/ssh/sshd_config` hello tooinclude po wierszu:</span><span class="sxs-lookup"><span data-stu-id="da37b-328">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

    <span data-ttu-id="da37b-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="da37b-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="da37b-330">Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-330">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="da37b-331">Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="da37b-331">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="da37b-332">Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-332">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="da37b-333">Należy pamiętać, że hello zasób lokalny dysk jest tymczasowe i może opróżnić, gdy maszyna wirtualna hello jest anulowaną aprowizacją.</span><span class="sxs-lookup"><span data-stu-id="da37b-333">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="da37b-334">Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować hello następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="da37b-334">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

13. <span data-ttu-id="da37b-335">Wyrejestruj hello subskrypcji (w razie potrzeby), uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-335">Unregister hello subscription (if necessary) by running hello following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="da37b-336">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="da37b-336">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="da37b-337">Zamknij maszynę wirtualną hello i konwersji pliku VHD tooa pliku VMDK hello.</span><span class="sxs-lookup"><span data-stu-id="da37b-337">Shut down hello virtual machine, and convert hello VMDK file tooa .vhd file.</span></span>

    <span data-ttu-id="da37b-338">Najpierw przekonwertować format tooraw obrazu hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-338">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="da37b-339">Upewnij się, że rozmiar hello nieprzetworzone hello jest zgodne z 1 MB.</span><span class="sxs-lookup"><span data-stu-id="da37b-339">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="da37b-340">W przeciwnym razie zaokrąglij w górę tooalign rozmiar hello z 1 MB:</span><span class="sxs-lookup"><span data-stu-id="da37b-340">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="da37b-341">Konwertuj hello tooa raw dysku stałym rozmiarze wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="da37b-341">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="da37b-342">Przygotowanie RHEL 7 maszyny wirtualnej z programu VMware</span><span class="sxs-lookup"><span data-stu-id="da37b-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="da37b-343">Utwórz lub Edytuj hello `/etc/sysconfig/network` pliku, a następnie dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-343">Create or edit hello `/etc/sysconfig/network` file, and add hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="da37b-344">Utwórz lub Edytuj hello `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku, a następnie dodaj hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="da37b-344">Create or edit hello `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="da37b-345">Upewnij się, że Usługa sieciowa hello zostanie uruchomione w czasie rozruchu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-345">Ensure that hello network service will start at boot time by running hello following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="da37b-346">Zarejestruj Red Hat subskrypcji tooenable hello instalacji pakietów z repozytorium RHEL hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-346">Register your Red Hat subscription tooenable hello installation of packages from hello RHEL repository by running hello following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="da37b-347">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-347">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="da37b-348">toodo modyfikacji, otwórz `/etc/default/grub` w edytorze tekstów i Edycja hello `GRUB_CMDLINE_LINUX` parametru.</span><span class="sxs-lookup"><span data-stu-id="da37b-348">toodo this modification, open `/etc/default/grub` in a text editor, and edit hello `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="da37b-349">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="da37b-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="da37b-350">Taka konfiguracja powoduje, że wszystkie komunikaty konsoli są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="da37b-350">This configuration also ensures that all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="da37b-351">On również wyłącza hello nowych systemów RHEL 7 konwencje nazewnictwa dla kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="da37b-351">It also turns off hello new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="da37b-352">Ponadto zaleca się usunięcie hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="da37b-352">In addition, we recommend that you remove hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="da37b-353">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="da37b-353">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span> <span data-ttu-id="da37b-354">Możesz pozostawić hello `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="da37b-354">You can leave hello `crashkernel` option configured if desired.</span></span> <span data-ttu-id="da37b-355">Należy pamiętać, że ten parametr zmniejsza hello ilość dostępnej pamięci w maszynie wirtualnej hello najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-355">Note that this parameter reduces hello amount of available memory in hello virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="da37b-356">Po zakończeniu edycji `/etc/default/grub`Uruchom hello następujące polecenia toorebuild hello chodników konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="da37b-356">After you are done editing `/etc/default/grub`, run hello following command toorebuild hello grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="da37b-357">Dodaj tooinitramfs modułów funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="da37b-357">Add Hyper-V modules tooinitramfs.</span></span>

    <span data-ttu-id="da37b-358">Edytuj `/etc/dracut.conf`, Dodaj zawartość:</span><span class="sxs-lookup"><span data-stu-id="da37b-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="da37b-359">Odbuduj initramfs:</span><span class="sxs-lookup"><span data-stu-id="da37b-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="da37b-360">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="da37b-360">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="da37b-361">To ustawienie jest zazwyczaj hello domyślnym.</span><span class="sxs-lookup"><span data-stu-id="da37b-361">This setting is usually hello default.</span></span> <span data-ttu-id="da37b-362">Modyfikowanie `/etc/ssh/sshd_config` hello tooinclude po wierszu:</span><span class="sxs-lookup"><span data-stu-id="da37b-362">Modify `/etc/ssh/sshd_config` tooinclude hello following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="da37b-363">Pakiet WALinuxAgent Hello, `WALinuxAgent-<version>`, został naciśnięty toohello Red Hat dodatki repozytorium.</span><span class="sxs-lookup"><span data-stu-id="da37b-363">hello WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed toohello Red Hat extras repository.</span></span> <span data-ttu-id="da37b-364">Włącz hello dodatki repozytorium, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-364">Enable hello extras repository by running hello following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="da37b-365">Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-365">Install hello Azure Linux Agent by running hello following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="da37b-366">Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="da37b-366">Do not create swap space on hello operating system disk.</span></span>

    <span data-ttu-id="da37b-367">Hello agenta systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu hello dysku zasób lokalny, który jest dołączony toohello maszyny wirtualnej po udostępnieniu hello maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-367">hello Azure Linux Agent can automatically configure swap space by using hello local resource disk that is attached toohello virtual machine after hello virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="da37b-368">Należy pamiętać, że hello zasób lokalny dysk jest tymczasowe i może opróżnić, gdy maszyna wirtualna hello jest anulowaną aprowizacją.</span><span class="sxs-lookup"><span data-stu-id="da37b-368">Note that hello local resource disk is a temporary disk, and it might be emptied when hello virtual machine is deprovisioned.</span></span> <span data-ttu-id="da37b-369">Po zainstalowaniu agenta systemu Linux Azure hello w poprzednim kroku hello zmodyfikować hello następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="da37b-369">After you install hello Azure Linux Agent in hello previous step, modify hello following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.

12. <span data-ttu-id="da37b-370">Jeśli chcesz toounregister hello subskrypcji, uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="da37b-370">If you want toounregister hello subscription, run hello following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="da37b-371">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="da37b-371">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="da37b-372">Zamknij maszynę wirtualną hello i przekonwertować formatu wirtualnego dysku twardego toohello pliku VMDK hello.</span><span class="sxs-lookup"><span data-stu-id="da37b-372">Shut down hello virtual machine, and convert hello VMDK file toohello VHD format.</span></span>

    <span data-ttu-id="da37b-373">Najpierw przekonwertować format tooraw obrazu hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-373">First convert hello image tooraw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="da37b-374">Upewnij się, że rozmiar hello nieprzetworzone hello jest zgodne z 1 MB.</span><span class="sxs-lookup"><span data-stu-id="da37b-374">Make sure that hello size of hello raw image is aligned with 1 MB.</span></span> <span data-ttu-id="da37b-375">W przeciwnym razie zaokrąglij w górę tooalign rozmiar hello z 1 MB:</span><span class="sxs-lookup"><span data-stu-id="da37b-375">Otherwise, round up hello size tooalign with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="da37b-376">Konwertuj hello tooa raw dysku stałym rozmiarze wirtualnego dysku twardego:</span><span class="sxs-lookup"><span data-stu-id="da37b-376">Convert hello raw disk tooa fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="da37b-377">Przygotowywanie maszyny wirtualnej z systemem Red Hat z obrazu ISO za pomocą pliku kickstart automatycznie</span><span class="sxs-lookup"><span data-stu-id="da37b-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="da37b-378">Przygotowanie RHEL 7 maszyny wirtualnej z pliku kickstart</span><span class="sxs-lookup"><span data-stu-id="da37b-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="da37b-379">Utwórz plik kickstart zawierający powitania po zawartości i Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="da37b-379">Create a kickstart file that includes hello following content, and save hello file.</span></span> <span data-ttu-id="da37b-380">Aby uzyskać szczegółowe informacje o instalacji kickstart, zobacz hello [Przewodnik instalacji Kickstart](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="da37b-380">For details about kickstart installation, see hello [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run hello Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear hello MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down hello machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable hello root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set hello cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build hello grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. <span data-ttu-id="da37b-381">Umieść plik kickstart hello gdzie hello instalacji systemu do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="da37b-381">Place hello kickstart file where hello installation system can access it.</span></span>

3. <span data-ttu-id="da37b-382">W Menedżerze funkcji Hyper-V Utwórz nową maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="da37b-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="da37b-383">Na powitania **Podłączanie wirtualnego dysku twardego** wybierz pozycję **Dołącz wirtualny dysk twardy później**oraz pełną hello Kreatora nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da37b-383">On hello **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete hello New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="da37b-384">Otwórz ustawienia maszyny wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="da37b-384">Open hello virtual machine settings:</span></span>

    <span data-ttu-id="da37b-385">a.</span><span class="sxs-lookup"><span data-stu-id="da37b-385">a.</span></span>  <span data-ttu-id="da37b-386">Dołączanie nowej maszyny wirtualnej toohello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="da37b-386">Attach a new virtual hard disk toohello virtual machine.</span></span> <span data-ttu-id="da37b-387">Upewnij się, że tooselect **formatu wirtualnego dysku twardego** i **o stałym rozmiarze**.</span><span class="sxs-lookup"><span data-stu-id="da37b-387">Make sure tooselect **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="da37b-388">b.</span><span class="sxs-lookup"><span data-stu-id="da37b-388">b.</span></span>  <span data-ttu-id="da37b-389">Dołącz instalacji hello stacji dysków DVD toohello ISO.</span><span class="sxs-lookup"><span data-stu-id="da37b-389">Attach hello installation ISO toohello DVD drive.</span></span>

    <span data-ttu-id="da37b-390">c.</span><span class="sxs-lookup"><span data-stu-id="da37b-390">c.</span></span>  <span data-ttu-id="da37b-391">Ustaw hello tooboot systemu BIOS z dysku CD.</span><span class="sxs-lookup"><span data-stu-id="da37b-391">Set hello BIOS tooboot from CD.</span></span>

5. <span data-ttu-id="da37b-392">Uruchom maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="da37b-392">Start hello virtual machine.</span></span> <span data-ttu-id="da37b-393">Po wyświetleniu Przewodnik instalacji hello naciśnij **kartę** opcje rozruchu hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="da37b-393">When hello installation guide appears, press **Tab** tooconfigure hello boot options.</span></span>

6. <span data-ttu-id="da37b-394">Wprowadź `inst.ks=<hello location of hello kickstart file>` na końcu hello hello opcje rozruchu, a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="da37b-394">Enter `inst.ks=<hello location of hello kickstart file>` at hello end of hello boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="da37b-395">Poczekaj na powitania toofinish instalacji.</span><span class="sxs-lookup"><span data-stu-id="da37b-395">Wait for hello installation toofinish.</span></span> <span data-ttu-id="da37b-396">Po zakończeniu hello maszyna wirtualna zostanie zamknięta automatycznie.</span><span class="sxs-lookup"><span data-stu-id="da37b-396">When it's finished, hello virtual machine will be shut down automatically.</span></span> <span data-ttu-id="da37b-397">Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.</span><span class="sxs-lookup"><span data-stu-id="da37b-397">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="da37b-398">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="da37b-398">Known issues</span></span>
### <a name="hello-hyper-v-driver-could-not-be-included-in-hello-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="da37b-399">Hello sterownik funkcji Hyper-V nie może znajdować się w hello początkowej dysku RAM, korzystając z funkcji hypervisor z systemem innym niż do funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="da37b-399">hello Hyper-V driver could not be included in hello initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="da37b-400">W niektórych przypadkach instalatorów systemu Linux może nie zawierać sterowników hello funkcji Hyper-v hello początkowej dysku RAM (initrd lub initramfs), chyba że Linux wykryje, że jest on uruchomiony w środowisku funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="da37b-400">In some cases, Linux installers might not include hello drivers for Hyper-V in hello initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="da37b-401">Podczas korzystania z tooprepare systemu (czyli Virtualbox, Xen itp.) wirtualizacji innego obrazu systemu Linux, może być konieczne tooensure initrd toorebuild, że co najmniej hello hv_vmbus i hv_storvsc jądra moduły są dostępne na powitania początkowej dysku RAM.</span><span class="sxs-lookup"><span data-stu-id="da37b-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) tooprepare your Linux image, you might need toorebuild initrd tooensure that at least hello hv_vmbus and hv_storvsc kernel modules are available on hello initial RAM disk.</span></span> <span data-ttu-id="da37b-402">To znany problem z co najmniej w systemach, które są oparte na powitania nadrzędnego Red Hat dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="da37b-402">This is a known issue at least on systems that are based on hello upstream Red Hat distribution.</span></span>

<span data-ttu-id="da37b-403">tooresolve ten problem, Dodaj tooinitramfs modułów funkcji Hyper-V i odbuduj go:</span><span class="sxs-lookup"><span data-stu-id="da37b-403">tooresolve this issue, add Hyper-V modules tooinitramfs and rebuild it:</span></span>

<span data-ttu-id="da37b-404">Edytuj `/etc/dracut.conf`i Dodaj hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="da37b-404">Edit `/etc/dracut.conf`, and add hello following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="da37b-405">Odbuduj initramfs:</span><span class="sxs-lookup"><span data-stu-id="da37b-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="da37b-406">Aby uzyskać więcej informacji, zobacz hello informacji [odbudowywania initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="da37b-406">For more details, see hello information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="da37b-407">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da37b-407">Next steps</span></span>
<span data-ttu-id="da37b-408">Użytkownik jest teraz gotowy toouse Red Hat Enterprise Linux wirtualnego dysku twardego toocreate nowych maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="da37b-408">You're now ready toouse your Red Hat Enterprise Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="da37b-409">Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da37b-409">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="da37b-410">Aby uzyskać więcej informacji na temat funkcji hypervisor hello, które są certyfikowane toorun Red Hat Enterprise Linux, zobacz [hello Red Hat witryny sieci Web](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="da37b-410">For more details about hello hypervisors that are certified toorun Red Hat Enterprise Linux, see [hello Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
