---
title: "Tworzenie i przekazywanie Red Hat Enterprise Linux wirtualnego dysku twardego do użycia na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się utworzyć i przekazać Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym Red Hat Linux."
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
ms.openlocfilehash: b753c76b8c3d789c681d7fbff6aa07590b860be5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="eab64-103">Przygotowywanie maszyny wirtualnej systemu Red Hat dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eab64-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="eab64-104">W tym artykule dowiesz się, jak przygotować maszyny wirtualnej Red Hat Enterprise Linux (RHEL) do użycia na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-104">In this article, you will learn how to prepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="eab64-105">Wersje RHEL, które zostały omówione w tym artykule są 6.7 + i 7.1 +.</span><span class="sxs-lookup"><span data-stu-id="eab64-105">The versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="eab64-106">Funkcje hypervisor w celu przygotowania, które zostały omówione w tym artykule są maszyny wirtualnej funkcji Hyper-V, na podstawie jądra (KVM) i VMware.</span><span class="sxs-lookup"><span data-stu-id="eab64-106">The hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="eab64-107">Aby uzyskać więcej informacji o wymaganiach dotyczących kwalifikuje się do uczestnictwa w programie dostęp do chmury Red Hat, zobacz [Red Hat dostęp do chmury witryny sieci Web](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) i [systemem RHEL na platformie Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="eab64-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/ecosystem/ccsp/microsoft-azure).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="eab64-108">Przygotowywanie maszyny wirtualnej z systemem Red Hat z Menedżera funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="eab64-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="eab64-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eab64-109">Prerequisites</span></span>
<span data-ttu-id="eab64-110">W tej sekcji założono, że zostały już uzyskane z pliku ISO z witryny sieci Web Red Hat i zainstalowane obrazu RHEL do wirtualnego dysku twardego (VHD).</span><span class="sxs-lookup"><span data-stu-id="eab64-110">This section assumes that you have already obtained an ISO file from the Red Hat website and installed the RHEL image to a virtual hard disk (VHD).</span></span> <span data-ttu-id="eab64-111">Aby uzyskać więcej informacji o sposobie użycia Menedżera funkcji Hyper-V do zainstalowania obrazu systemu operacyjnego, zobacz [Instalowanie roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="eab64-111">For more details about how to use Hyper-V Manager to install an operating system image, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="eab64-112">**RHEL uwagi instalacji**</span><span class="sxs-lookup"><span data-stu-id="eab64-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="eab64-113">Azure nie obsługuje formatu VHDX.</span><span class="sxs-lookup"><span data-stu-id="eab64-113">Azure does not support the VHDX format.</span></span> <span data-ttu-id="eab64-114">Azure obsługuje tylko stałe wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="eab64-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="eab64-115">Menedżer funkcji Hyper-V umożliwia Konwertuj dysk na format wirtualnego dysku twardego, lub można użyć polecenia cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="eab64-115">You can use Hyper-V Manager to convert the disk to VHD format, or you can use the convert-vhd cmdlet.</span></span> <span data-ttu-id="eab64-116">Jeśli używasz VirtualBox, wybierz **stały rozmiar** zamiast domyślnego dynamicznie przydzielane opcji podczas tworzenia dysku.</span><span class="sxs-lookup"><span data-stu-id="eab64-116">If you use VirtualBox, select **Fixed size** as opposed to the default dynamically allocated option when you create the disk.</span></span>
* <span data-ttu-id="eab64-117">Azure obsługuje tylko maszyny wirtualne generacji 1.</span><span class="sxs-lookup"><span data-stu-id="eab64-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="eab64-118">Maszyny wirtualne generacji 1 można przekonwertować z VHDX do formatu pliku wirtualnego dysku twardego i dynamicznie powiększające się na dysku o stałym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="eab64-118">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed-size disk.</span></span> <span data-ttu-id="eab64-119">Nie można zmienić generację maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="eab64-120">Aby uzyskać więcej informacji, zobacz [należy tworzyć maszyny wirtualne generacji 1 lub 2 w funkcji Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="eab64-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="eab64-121">Maksymalny rozmiar, jaki jest dozwolony dla wirtualnego dysku twardego jest 1,023 GB.</span><span class="sxs-lookup"><span data-stu-id="eab64-121">The maximum size that's allowed for the VHD is 1,023 GB.</span></span>
* <span data-ttu-id="eab64-122">Po zainstalowaniu systemu operacyjnego Linux, zaleca się użycie standardowe partycje, a nie logiczne woluminu Manager (LVM), często jest to wartość domyślna dla wielu urządzeń.</span><span class="sxs-lookup"><span data-stu-id="eab64-122">When you install the Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often the default for many installations.</span></span> <span data-ttu-id="eab64-123">Takie rozwiązanie pozwoli uniknąć LVM nazwa powoduje konflikt z sklonowane maszyny wirtualne, szczególnie jeśli kiedykolwiek zajdzie potrzeba Podłącz dysk systemu operacyjnego do innej maszyny wirtualnej identyczne do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="eab64-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need to attach an operating system disk to another identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="eab64-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="eab64-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="eab64-125">Wymagana jest obsługa jądra służący do instalowania systemów plików uniwersalny Format dysku (UDF).</span><span class="sxs-lookup"><span data-stu-id="eab64-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="eab64-126">Przy pierwszym uruchomieniu komputera na platformie Azure sformatowany UDF nośnika dołączonego do Gość przekazuje inicjowania obsługi konfiguracji maszyny wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="eab64-126">At first boot on Azure, the UDF-formatted media that is attached to the guest passes the provisioning configuration to the Linux virtual machine.</span></span> <span data-ttu-id="eab64-127">Agent systemu Linux platformy Azure musi mieć możliwość zainstalowania systemu plików funkcji zdefiniowanej przez użytkownika do odczytu konfiguracji i udostępnić maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-127">The Azure Linux Agent must be able to mount the UDF file system to read its configuration and provision the virtual machine.</span></span>
* <span data-ttu-id="eab64-128">Wersje starsze niż 2.6.37 jądra systemu Linux nie obsługują dostępu niejednolitego pamięci (NUMA) w ramach funkcji Hyper-V o dużym rozmiarze maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-128">Versions of the Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="eab64-129">Ten problem wpływa głównie na starszą dystrybucje, korzystających z nadrzędnego jądra Red Hat 2.6.32 zostało ustalone w 6.6 RHEL (jądra-2.6.32 504).</span><span class="sxs-lookup"><span data-stu-id="eab64-129">This issue primarily impacts older distributions that use the upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="eab64-130">Systemy systemem jądra niestandardowych, które są starsze niż 2.6.37 lub należy ustawić na podstawie RHEL jądra, które są starsze niż 2.6.32-504 `numa=off` rozruch parametru w wierszu polecenia jądra w grub.conf.</span><span class="sxs-lookup"><span data-stu-id="eab64-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set the `numa=off` boot parameter on the kernel command line in grub.conf.</span></span> <span data-ttu-id="eab64-131">Aby uzyskać więcej informacji, zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="eab64-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="eab64-132">Nie należy konfigurować wymiany partycji na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="eab64-132">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="eab64-133">Aby utworzyć plik wymiany na dysku zasobów można skonfigurować agenta systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="eab64-133">The Linux Agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="eab64-134">Więcej informacji na ten temat można znaleźć w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="eab64-134">More information about this can be found in the following steps.</span></span>
* <span data-ttu-id="eab64-135">Wszystkie wirtualne dyski twarde muszą mieć rozmiary, które są wielokrotności 1 MB.</span><span class="sxs-lookup"><span data-stu-id="eab64-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="eab64-136">Przygotowanie RHEL 6 maszyny wirtualnej z Menedżera funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="eab64-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="eab64-137">W Menedżerze funkcji Hyper-V wybierz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="eab64-137">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="eab64-138">Kliknij przycisk **Connect** aby otworzyć okno konsoli dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-138">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="eab64-139">6 RHEL NetworkManager może zakłócać agenta systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-139">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="eab64-140">Odinstalowania tego pakietu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-140">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="eab64-141">Utwórz lub Edytuj `/etc/sysconfig/network` pliku i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-141">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="eab64-142">Utwórz lub Edytuj `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-142">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="eab64-143">Przenieś lub usuń reguły udev, aby uniknąć generowania statyczne reguły dla interfejsu Ethernet.</span><span class="sxs-lookup"><span data-stu-id="eab64-143">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="eab64-144">Te reguły powodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="eab64-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="eab64-145">Upewnij się, że Usługa sieciowa będzie uruchamiane podczas rozruchu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-145">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="eab64-146">Zarejestruj subskrypcję Red Hat, aby umożliwić instalację pakietów z repozytorium RHEL, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-146">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="eab64-147">Pakiet WALinuxAgent `WALinuxAgent-<version>`, ma zostać przypisany do repozytorium dodatki Red Hat.</span><span class="sxs-lookup"><span data-stu-id="eab64-147">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="eab64-148">Włącz repozytorium dodatki, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-148">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="eab64-149">Zmodyfikuj wiersza rozruchu jądra w konfiguracji chodników uwzględnienie jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-149">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="eab64-150">Aby wykonać tę zmianę, otwórz `/boot/grub/menu.lst` w edytorze tekstu i upewnij się, że jądra domyślna zawiera następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="eab64-150">To do this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="eab64-151">To zapewni również, że wszystkie komunikaty konsoli są wysyłane do pierwszego portu szeregowego może pomóc Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="eab64-151">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="eab64-152">Ponadto zaleca się, że należy usunąć następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="eab64-152">In addition, we recommended that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="eab64-153">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie dzienniki, które mają być wysyłane do portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="eab64-153">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="eab64-154">Możesz pozostawić `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="eab64-154">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="eab64-155">Należy pamiętać, że ten parametr zmniejsza ilość dostępnej pamięci w maszyny wirtualnej za pomocą 128 MB lub większej.</span><span class="sxs-lookup"><span data-stu-id="eab64-155">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more.</span></span> <span data-ttu-id="eab64-156">Ta konfiguracja może być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="eab64-157">RHEL 6.5 lub starszej należy również ustawić `numa=off` parametru jądra.</span><span class="sxs-lookup"><span data-stu-id="eab64-157">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="eab64-158">Zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="eab64-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="eab64-159">Upewnij się, że serwer bezpiecznej powłoki (SSH) jest zainstalowany i skonfigurowany do uruchamiania w czasie rozruchu, zazwyczaj jest to wartość domyślna.</span><span class="sxs-lookup"><span data-stu-id="eab64-159">Ensure that the secure shell (SSH) server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="eab64-160">Zmień /etc/ssh/sshd_config ma zawierać następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="eab64-160">Modify /etc/ssh/sshd_config to include the following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="eab64-161">Zainstaluj agenta systemu Linux platformy Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-161">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

    <span data-ttu-id="eab64-162">Instalowanie pakietu WALinuxAgent usuwa NetworkManager i pakiety NetworkManager gnome Jeśli nie zostały już usunięte w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="eab64-162">Installing the WALinuxAgent package removes the NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="eab64-163">Nie należy tworzyć zamiany miejsca na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="eab64-163">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="eab64-164">Agent systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu dysku zasób lokalny, który jest dołączony do maszyny wirtualnej po udostępnieniu maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-164">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="eab64-165">Należy pamiętać, że dysk zasobu lokalnego jest tymczasowe i czy mogą być opróżniany podczas maszyny wirtualnej jest anulowana.</span><span class="sxs-lookup"><span data-stu-id="eab64-165">Note that the local resource disk is a temporary disk and that it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="eab64-166">Po zainstalowaniu agenta systemu Linux platformy Azure w poprzednim kroku, zmodyfikuj odpowiednio w /etc/waagent.conf następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="eab64-166">After you install the Azure Linux Agent in the previous step, modify the following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

14. <span data-ttu-id="eab64-167">Wyrejestruj subskrypcji (w razie potrzeby), uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-167">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="eab64-168">Uruchom następujące polecenia, aby anulowanie zastrzeżenia maszyny wirtualnej i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="eab64-168">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="eab64-169">Kliknij przycisk **akcji** > **zamknąć** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="eab64-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="eab64-170">Dysk VHD systemu Linux jest teraz gotowy do przekazania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-170">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="eab64-171">Przygotowanie RHEL 7 maszyny wirtualnej z Menedżera funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="eab64-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="eab64-172">W Menedżerze funkcji Hyper-V wybierz maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="eab64-172">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="eab64-173">Kliknij przycisk **Connect** aby otworzyć okno konsoli dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-173">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="eab64-174">Utwórz lub Edytuj `/etc/sysconfig/network` pliku i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-174">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="eab64-175">Utwórz lub Edytuj `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-175">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="eab64-176">Upewnij się, że Usługa sieciowa będzie uruchamiane podczas rozruchu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-176">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="eab64-177">Zarejestruj subskrypcję Red Hat, aby umożliwić instalację pakietów z repozytorium RHEL, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-177">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="eab64-178">Zmodyfikuj wiersza rozruchu jądra w konfiguracji chodników uwzględnienie jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-178">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="eab64-179">Aby wykonać tę zmianę, otwórz `/etc/default/grub` w edytorze tekstów i edycja `GRUB_CMDLINE_LINUX` parametru.</span><span class="sxs-lookup"><span data-stu-id="eab64-179">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="eab64-180">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eab64-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="eab64-181">To zapewni również, że wszystkie komunikaty konsoli są wysyłane do pierwszego portu szeregowego może pomóc Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="eab64-181">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="eab64-182">Ta konfiguracja również wyłącza nowych systemów RHEL 7 konwencji nazewnictwa, dla kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="eab64-182">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="eab64-183">Ponadto zaleca się, że należy usunąć następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="eab64-183">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="eab64-184">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie dzienniki, które mają być wysyłane do portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="eab64-184">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="eab64-185">Możesz pozostawić `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="eab64-185">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="eab64-186">Należy pamiętać, że ten parametr zmniejsza ilość dostępnej pamięci w maszynie wirtualnej najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-186">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="eab64-187">Po zakończeniu edycji `/etc/default/grub`, uruchom następujące polecenie, aby odbudować chodników konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="eab64-187">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="eab64-188">Sprawdź, czy serwer SSH jest zainstalowany i skonfigurowany do uruchamiania w czasie rozruchu, która zwykle jest ustawiona domyślnie.</span><span class="sxs-lookup"><span data-stu-id="eab64-188">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="eab64-189">Modyfikowanie `/etc/ssh/sshd_config` ma zawierać następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="eab64-189">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="eab64-190">Pakiet WALinuxAgent `WALinuxAgent-<version>`, ma zostać przypisany do repozytorium dodatki Red Hat.</span><span class="sxs-lookup"><span data-stu-id="eab64-190">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="eab64-191">Włącz repozytorium dodatki, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-191">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="eab64-192">Zainstaluj agenta systemu Linux platformy Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-192">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="eab64-193">Nie należy tworzyć zamiany miejsca na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="eab64-193">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="eab64-194">Agent systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu dysku zasób lokalny, który jest dołączony do maszyny wirtualnej po udostępnieniu maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-194">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="eab64-195">Zauważ, że dysk lokalny zasób jest tymczasowego, i może opróżnić, gdy maszyna wirtualna jest anulowana.</span><span class="sxs-lookup"><span data-stu-id="eab64-195">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="eab64-196">Po zainstalowaniu agenta systemu Linux platformy Azure w poprzednim kroku, należy zmodyfikować następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="eab64-196">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="eab64-197">Jeśli chcesz wyrejestrować subskrypcji, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-197">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="eab64-198">Uruchom następujące polecenia, aby anulowanie zastrzeżenia maszyny wirtualnej i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="eab64-198">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="eab64-199">Kliknij przycisk **akcji** > **zamknąć** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="eab64-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="eab64-200">Dysk VHD systemu Linux jest teraz gotowy do przekazania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-200">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="eab64-201">Przygotowywanie maszyny wirtualnej z systemem Red Hat z KVM</span><span class="sxs-lookup"><span data-stu-id="eab64-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="eab64-202">Przygotowanie maszyny wirtualnej RHEL 6 z KVM</span><span class="sxs-lookup"><span data-stu-id="eab64-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="eab64-203">Pobierz obraz KVM RHEL 6 z Red Hat witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="eab64-203">Download the KVM image of RHEL 6 from the Red Hat website.</span></span>

2. <span data-ttu-id="eab64-204">Ustaw hasło główne.</span><span class="sxs-lookup"><span data-stu-id="eab64-204">Set a root password.</span></span>

    <span data-ttu-id="eab64-205">Generowanie zaszyfrowane hasło, a następnie skopiuj dane wyjściowe polecenia:</span><span class="sxs-lookup"><span data-stu-id="eab64-205">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="eab64-206">Ustaw hasło główne z guestfish:</span><span class="sxs-lookup"><span data-stu-id="eab64-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="eab64-207">Zmiany w tym polu drugiego użytkownika root z "!"</span><span class="sxs-lookup"><span data-stu-id="eab64-207">Change the second field of the root user from "!!"</span></span> <span data-ttu-id="eab64-208">zaszyfrowane hasło.</span><span class="sxs-lookup"><span data-stu-id="eab64-208">to the encrypted password.</span></span>

3. <span data-ttu-id="eab64-209">Utwórz maszynę wirtualną w KVM z obrazu qcow2.</span><span class="sxs-lookup"><span data-stu-id="eab64-209">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="eab64-210">Ustaw typ dysku **qcow2**i ustaw model urządzenia interfejsu sieci wirtualnej **virtio**.</span><span class="sxs-lookup"><span data-stu-id="eab64-210">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="eab64-211">Następnie uruchom maszynę wirtualną, a następnie zaloguj się jako katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="eab64-211">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="eab64-212">Utwórz lub Edytuj `/etc/sysconfig/network` pliku i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-212">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="eab64-213">Utwórz lub Edytuj `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-213">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="eab64-214">Przenieś lub usuń reguły udev, aby uniknąć generowania statyczne reguły dla interfejsu Ethernet.</span><span class="sxs-lookup"><span data-stu-id="eab64-214">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="eab64-215">Te reguły powodować problemy podczas klonowania maszyny wirtualnej Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="eab64-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="eab64-216">Upewnij się, że Usługa sieciowa będzie uruchamiane podczas rozruchu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-216">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="eab64-217">Zarejestruj subskrypcję Red Hat, aby umożliwić instalację pakietów z repozytorium RHEL, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-217">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="eab64-218">Zmodyfikuj wiersza rozruchu jądra w konfiguracji chodników uwzględnienie jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-218">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="eab64-219">Aby wykonać tę konfigurację, otwórz `/boot/grub/menu.lst` w edytorze tekstu i upewnij się, że jądra domyślna zawiera następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="eab64-219">To do this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="eab64-220">To zapewni również, że wszystkie komunikaty konsoli są wysyłane do pierwszego portu szeregowego może pomóc Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="eab64-220">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="eab64-221">Ponadto zaleca się, że należy usunąć następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="eab64-221">In addition, we recommend that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="eab64-222">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie dzienniki, które mają być wysyłane do portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="eab64-222">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="eab64-223">Możesz pozostawić `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="eab64-223">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="eab64-224">Należy pamiętać, że ten parametr zmniejsza ilość dostępnej pamięci w maszynie wirtualnej najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-224">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="eab64-225">RHEL 6.5 lub starszej należy również ustawić `numa=off` parametru jądra.</span><span class="sxs-lookup"><span data-stu-id="eab64-225">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="eab64-226">Zobacz Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="eab64-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="eab64-227">Dodawanie modułów funkcji Hyper-V do initramfs:</span><span class="sxs-lookup"><span data-stu-id="eab64-227">Add Hyper-V modules to initramfs:</span></span>  

    <span data-ttu-id="eab64-228">Edytuj `/etc/dracut.conf`i dodaj następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="eab64-228">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="eab64-229">Odbuduj initramfs:</span><span class="sxs-lookup"><span data-stu-id="eab64-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="eab64-230">Odinstaluj init chmury:</span><span class="sxs-lookup"><span data-stu-id="eab64-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="eab64-231">Upewnij się, że serwer SSH jest zainstalowany i skonfigurowany do uruchamiania w czasie rozruchu:</span><span class="sxs-lookup"><span data-stu-id="eab64-231">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="eab64-232">Zmień /etc/ssh/sshd_config, aby uwzględnić następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="eab64-232">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="eab64-233">Pakiet WALinuxAgent `WALinuxAgent-<version>`, ma zostać przypisany do repozytorium dodatki Red Hat.</span><span class="sxs-lookup"><span data-stu-id="eab64-233">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="eab64-234">Włącz repozytorium dodatki, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-234">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="eab64-235">Zainstaluj agenta systemu Linux platformy Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-235">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="eab64-236">Agent systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu dysku zasób lokalny, który jest dołączony do maszyny wirtualnej po udostępnieniu maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-236">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="eab64-237">Zauważ, że dysk lokalny zasób jest tymczasowego, i może opróżnić, gdy maszyna wirtualna jest anulowana.</span><span class="sxs-lookup"><span data-stu-id="eab64-237">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="eab64-238">Po zainstalowaniu agenta systemu Linux platformy Azure w poprzednim kroku, należy zmodyfikować następujące parametry w **/etc/waagent.conf** odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="eab64-238">After you install the Azure Linux Agent in the previous step, modify the following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="eab64-239">Wyrejestruj subskrypcji (w razie potrzeby), uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-239">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="eab64-240">Uruchom następujące polecenia, aby anulowanie zastrzeżenia maszyny wirtualnej i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="eab64-240">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="eab64-241">Zamknij maszynę wirtualną w KVM.</span><span class="sxs-lookup"><span data-stu-id="eab64-241">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="eab64-242">Konwertuj obraz qcow2 na format wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="eab64-242">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="eab64-243">Najpierw Konwertuj obraz na raw format:</span><span class="sxs-lookup"><span data-stu-id="eab64-243">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="eab64-244">Upewnij się, że rozmiar obrazu raw jest zgodne z 1 MB.</span><span class="sxs-lookup"><span data-stu-id="eab64-244">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="eab64-245">W przeciwnym razie zaokrąglij w górę rozmiar, aby były wyrównane z 1 MB:</span><span class="sxs-lookup"><span data-stu-id="eab64-245">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="eab64-246">Konwertuj raw dysku na dysk VHD o stałym rozmiarze:</span><span class="sxs-lookup"><span data-stu-id="eab64-246">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="eab64-247">Przygotowanie maszyny wirtualnej RHEL 7 z KVM</span><span class="sxs-lookup"><span data-stu-id="eab64-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="eab64-248">Pobierz obraz KVM RHEL 7 z Red Hat witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="eab64-248">Download the KVM image of RHEL 7 from the Red Hat website.</span></span> <span data-ttu-id="eab64-249">Ta procedura wykorzystuje RHEL 7, co w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="eab64-249">This procedure uses RHEL 7 as the example.</span></span>

2. <span data-ttu-id="eab64-250">Ustaw hasło główne.</span><span class="sxs-lookup"><span data-stu-id="eab64-250">Set a root password.</span></span>

    <span data-ttu-id="eab64-251">Generowanie zaszyfrowane hasło, a następnie skopiuj dane wyjściowe polecenia:</span><span class="sxs-lookup"><span data-stu-id="eab64-251">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="eab64-252">Ustaw hasło główne z guestfish:</span><span class="sxs-lookup"><span data-stu-id="eab64-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="eab64-253">Zmień drugie pole użytkownika głównego z "!"</span><span class="sxs-lookup"><span data-stu-id="eab64-253">Change the second field of root user from "!!"</span></span> <span data-ttu-id="eab64-254">zaszyfrowane hasło.</span><span class="sxs-lookup"><span data-stu-id="eab64-254">to the encrypted password.</span></span>

3. <span data-ttu-id="eab64-255">Utwórz maszynę wirtualną w KVM z obrazu qcow2.</span><span class="sxs-lookup"><span data-stu-id="eab64-255">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="eab64-256">Ustaw typ dysku **qcow2**i ustaw model urządzenia interfejsu sieci wirtualnej **virtio**.</span><span class="sxs-lookup"><span data-stu-id="eab64-256">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="eab64-257">Następnie uruchom maszynę wirtualną, a następnie zaloguj się jako katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="eab64-257">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="eab64-258">Utwórz lub Edytuj `/etc/sysconfig/network` pliku i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-258">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="eab64-259">Utwórz lub Edytuj `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-259">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="eab64-260">Upewnij się, że Usługa sieciowa będzie uruchamiane podczas rozruchu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-260">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="eab64-261">Zarejestruj subskrypcję Red Hat umożliwia przeprowadzenie instalacji pakietów z repozytorium RHEL, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-261">Register your Red Hat subscription to enable installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="eab64-262">Zmodyfikuj wiersza rozruchu jądra w konfiguracji chodników uwzględnienie jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-262">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="eab64-263">Aby wykonać tę konfigurację, otwórz `/etc/default/grub` w edytorze tekstów i edycja `GRUB_CMDLINE_LINUX` parametru.</span><span class="sxs-lookup"><span data-stu-id="eab64-263">To do this configuration, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="eab64-264">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eab64-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="eab64-265">To polecenie sprawia, że wszystkie komunikaty konsoli są wysyłane do pierwszego portu szeregowego może pomóc Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="eab64-265">This command also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="eab64-266">Polecenie również wyłącza nowych systemów RHEL 7 konwencji nazewnictwa, dla kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="eab64-266">The command also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="eab64-267">Ponadto zaleca się, że należy usunąć następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="eab64-267">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="eab64-268">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie dzienniki, które mają być wysyłane do portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="eab64-268">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="eab64-269">Możesz pozostawić `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="eab64-269">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="eab64-270">Należy pamiętać, że ten parametr zmniejsza ilość dostępnej pamięci w maszynie wirtualnej najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-270">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="eab64-271">Po zakończeniu edycji `/etc/default/grub`, uruchom następujące polecenie, aby odbudować chodników konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="eab64-271">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="eab64-272">Dodawanie modułów funkcji Hyper-V do initramfs.</span><span class="sxs-lookup"><span data-stu-id="eab64-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="eab64-273">Edytuj `/etc/dracut.conf` i Dodaj zawartość:</span><span class="sxs-lookup"><span data-stu-id="eab64-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="eab64-274">Odbuduj initramfs:</span><span class="sxs-lookup"><span data-stu-id="eab64-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="eab64-275">Odinstaluj init chmury:</span><span class="sxs-lookup"><span data-stu-id="eab64-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="eab64-276">Upewnij się, że serwer SSH jest zainstalowany i skonfigurowany do uruchamiania w czasie rozruchu:</span><span class="sxs-lookup"><span data-stu-id="eab64-276">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="eab64-277">Zmień /etc/ssh/sshd_config, aby uwzględnić następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="eab64-277">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="eab64-278">Pakiet WALinuxAgent `WALinuxAgent-<version>`, ma zostać przypisany do repozytorium dodatki Red Hat.</span><span class="sxs-lookup"><span data-stu-id="eab64-278">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="eab64-279">Włącz repozytorium dodatki, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-279">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="eab64-280">Zainstaluj agenta systemu Linux platformy Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-280">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="eab64-281">Włącz usługę agenta waagent:</span><span class="sxs-lookup"><span data-stu-id="eab64-281">Enable the waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="eab64-282">Nie należy tworzyć zamiany miejsca na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="eab64-282">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="eab64-283">Agent systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu dysku zasób lokalny, który jest dołączony do maszyny wirtualnej po udostępnieniu maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-283">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="eab64-284">Zauważ, że dysk lokalny zasób jest tymczasowego, i może opróżnić, gdy maszyna wirtualna jest anulowana.</span><span class="sxs-lookup"><span data-stu-id="eab64-284">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="eab64-285">Po zainstalowaniu agenta systemu Linux platformy Azure w poprzednim kroku, należy zmodyfikować następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="eab64-285">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="eab64-286">Wyrejestruj subskrypcji (w razie potrzeby), uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-286">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="eab64-287">Uruchom następujące polecenia, aby anulowanie zastrzeżenia maszyny wirtualnej i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="eab64-287">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="eab64-288">Zamknij maszynę wirtualną w KVM.</span><span class="sxs-lookup"><span data-stu-id="eab64-288">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="eab64-289">Konwertuj obraz qcow2 na format wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="eab64-289">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="eab64-290">Najpierw Konwertuj obraz na raw format:</span><span class="sxs-lookup"><span data-stu-id="eab64-290">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="eab64-291">Upewnij się, że rozmiar obrazu raw jest zgodne z 1 MB.</span><span class="sxs-lookup"><span data-stu-id="eab64-291">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="eab64-292">W przeciwnym razie zaokrąglij w górę rozmiar, aby były wyrównane z 1 MB:</span><span class="sxs-lookup"><span data-stu-id="eab64-292">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="eab64-293">Konwertuj raw dysku na dysk VHD o stałym rozmiarze:</span><span class="sxs-lookup"><span data-stu-id="eab64-293">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="eab64-294">Przygotowywanie maszyny wirtualnej z systemem Red Hat z programu VMware</span><span class="sxs-lookup"><span data-stu-id="eab64-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="eab64-295">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eab64-295">Prerequisites</span></span>
<span data-ttu-id="eab64-296">W tej sekcji założono, zainstalowano RHEL maszyny wirtualnej w środowisku programu VMware.</span><span class="sxs-lookup"><span data-stu-id="eab64-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="eab64-297">Aby uzyskać więcej informacji o sposobie instalowania systemu operacyjnego w środowisku programu VMware, zobacz [Przewodnik instalacji systemu operacyjnego gościa VMware](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="eab64-297">For details about how to install an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="eab64-298">Po zainstalowaniu systemu operacyjnego Linux, zaleca się użycie standardowe partycje, a nie LVM, często jest to wartość domyślna dla wielu urządzeń.</span><span class="sxs-lookup"><span data-stu-id="eab64-298">When you install the Linux operating system, we recommend that you use standard partitions rather than LVM, which is often the default for many installations.</span></span> <span data-ttu-id="eab64-299">Pozwoli to uniknąć konfliktów nazw LVM ze sklonowanej maszyny wirtualnej, zwłaszcza w przypadku, gdy dysk systemu operacyjnego kiedykolwiek musi zostać dołączony do innej maszyny wirtualnej w celu rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="eab64-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs to be attached to another virtual machine for troubleshooting.</span></span> <span data-ttu-id="eab64-300">LVM RAID można lub na dyskach danych, jeśli preferowane.</span><span class="sxs-lookup"><span data-stu-id="eab64-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="eab64-301">Nie należy konfigurować wymiany partycji na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="eab64-301">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="eab64-302">Można skonfigurować agenta systemu Linux, aby utworzyć plik wymiany na dysku zasobów.</span><span class="sxs-lookup"><span data-stu-id="eab64-302">You can configure the Linux agent to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="eab64-303">Więcej informacji na ten temat można znaleźć w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="eab64-303">You can find more information about this in the steps that follow.</span></span>
* <span data-ttu-id="eab64-304">Po utworzeniu wirtualnego dysku twardego, wybierz **magazynu wirtualnego dysku w postaci jednego pliku**.</span><span class="sxs-lookup"><span data-stu-id="eab64-304">When you create the virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="eab64-305">Przygotowanie RHEL 6 maszyny wirtualnej z programu VMware</span><span class="sxs-lookup"><span data-stu-id="eab64-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="eab64-306">6 RHEL NetworkManager może zakłócać agenta systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-306">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="eab64-307">Odinstalowania tego pakietu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-307">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="eab64-308">Utwórz plik o nazwie **sieci** w katalogu/etc/sysconfig/zawierający następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-308">Create a file named **network** in the /etc/sysconfig/ directory that contains the following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="eab64-309">Utwórz lub Edytuj `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-309">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="eab64-310">Przenieś lub usuń reguły udev, aby uniknąć generowania statyczne reguły dla interfejsu Ethernet.</span><span class="sxs-lookup"><span data-stu-id="eab64-310">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="eab64-311">Te reguły powodować problemy podczas klonowania maszyny wirtualnej Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="eab64-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="eab64-312">Upewnij się, że Usługa sieciowa będzie uruchamiane podczas rozruchu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-312">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="eab64-313">Zarejestruj subskrypcję Red Hat, aby umożliwić instalację pakietów z repozytorium RHEL, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-313">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="eab64-314">Pakiet WALinuxAgent `WALinuxAgent-<version>`, ma zostać przypisany do repozytorium dodatki Red Hat.</span><span class="sxs-lookup"><span data-stu-id="eab64-314">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="eab64-315">Włącz repozytorium dodatki, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-315">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="eab64-316">Zmodyfikuj wiersza rozruchu jądra w konfiguracji chodników uwzględnienie jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-316">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="eab64-317">Aby to zrobić, otwórz `/etc/default/grub` w edytorze tekstów i edycja `GRUB_CMDLINE_LINUX` parametru.</span><span class="sxs-lookup"><span data-stu-id="eab64-317">To do this, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="eab64-318">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eab64-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0"
   
   <span data-ttu-id="eab64-319">To zapewni również, że wszystkie komunikaty konsoli są wysyłane do pierwszego portu szeregowego może pomóc Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="eab64-319">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="eab64-320">Ponadto zaleca się, że należy usunąć następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="eab64-320">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="eab64-321">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie dzienniki, które mają być wysyłane do portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="eab64-321">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="eab64-322">Możesz pozostawić `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="eab64-322">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="eab64-323">Należy pamiętać, że ten parametr zmniejsza ilość dostępnej pamięci w maszynie wirtualnej najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-323">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="eab64-324">Dodawanie modułów funkcji Hyper-V do initramfs:</span><span class="sxs-lookup"><span data-stu-id="eab64-324">Add Hyper-V modules to initramfs:</span></span>

    <span data-ttu-id="eab64-325">Edytuj `/etc/dracut.conf`i dodaj następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="eab64-325">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="eab64-326">Odbuduj initramfs:</span><span class="sxs-lookup"><span data-stu-id="eab64-326">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="eab64-327">Sprawdź, czy serwer SSH jest zainstalowany i skonfigurowany do uruchamiania w czasie rozruchu, która zwykle jest ustawiona domyślnie.</span><span class="sxs-lookup"><span data-stu-id="eab64-327">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="eab64-328">Modyfikowanie `/etc/ssh/sshd_config` ma zawierać następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="eab64-328">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

    <span data-ttu-id="eab64-329">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="eab64-329">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="eab64-330">Zainstaluj agenta systemu Linux platformy Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-330">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="eab64-331">Nie należy tworzyć zamiany miejsca na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="eab64-331">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="eab64-332">Agent systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu dysku zasób lokalny, który jest dołączony do maszyny wirtualnej po udostępnieniu maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-332">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="eab64-333">Zauważ, że dysk lokalny zasób jest tymczasowego, i może opróżnić, gdy maszyna wirtualna jest anulowana.</span><span class="sxs-lookup"><span data-stu-id="eab64-333">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="eab64-334">Po zainstalowaniu agenta systemu Linux platformy Azure w poprzednim kroku, należy zmodyfikować następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="eab64-334">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="eab64-335">Wyrejestruj subskrypcji (w razie potrzeby), uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-335">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="eab64-336">Uruchom następujące polecenia, aby anulowanie zastrzeżenia maszyny wirtualnej i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="eab64-336">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="eab64-337">Zamknij maszynę wirtualną i konwertowania pliku VMDK do pliku VHD.</span><span class="sxs-lookup"><span data-stu-id="eab64-337">Shut down the virtual machine, and convert the VMDK file to a .vhd file.</span></span>

    <span data-ttu-id="eab64-338">Najpierw Konwertuj obraz na raw format:</span><span class="sxs-lookup"><span data-stu-id="eab64-338">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="eab64-339">Upewnij się, że rozmiar obrazu raw jest zgodne z 1 MB.</span><span class="sxs-lookup"><span data-stu-id="eab64-339">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="eab64-340">W przeciwnym razie zaokrąglij w górę rozmiar, aby były wyrównane z 1 MB:</span><span class="sxs-lookup"><span data-stu-id="eab64-340">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="eab64-341">Konwertuj raw dysku na dysk VHD o stałym rozmiarze:</span><span class="sxs-lookup"><span data-stu-id="eab64-341">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="eab64-342">Przygotowanie RHEL 7 maszyny wirtualnej z programu VMware</span><span class="sxs-lookup"><span data-stu-id="eab64-342">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="eab64-343">Utwórz lub Edytuj `/etc/sysconfig/network` pliku i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-343">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="eab64-344">Utwórz lub Edytuj `/etc/sysconfig/network-scripts/ifcfg-eth0` pliku i Dodaj następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="eab64-344">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="eab64-345">Upewnij się, że Usługa sieciowa będzie uruchamiane podczas rozruchu, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-345">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="eab64-346">Zarejestruj subskrypcję Red Hat, aby umożliwić instalację pakietów z repozytorium RHEL, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-346">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="eab64-347">Zmodyfikuj wiersza rozruchu jądra w konfiguracji chodników uwzględnienie jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-347">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="eab64-348">Aby wykonać tę zmianę, otwórz `/etc/default/grub` w edytorze tekstów i edycja `GRUB_CMDLINE_LINUX` parametru.</span><span class="sxs-lookup"><span data-stu-id="eab64-348">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="eab64-349">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eab64-349">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="eab64-350">Taka konfiguracja powoduje, że wszystkie komunikaty konsoli są wysyłane do pierwszego portu szeregowego może pomóc Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="eab64-350">This configuration also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="eab64-351">On również wyłącza nowych systemów RHEL 7 konwencje nazewnictwa dla kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="eab64-351">It also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="eab64-352">Ponadto zaleca się, że należy usunąć następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="eab64-352">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="eab64-353">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie dzienniki, które mają być wysyłane do portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="eab64-353">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="eab64-354">Możesz pozostawić `crashkernel` opcji skonfigurowanych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="eab64-354">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="eab64-355">Należy pamiętać, że ten parametr zmniejsza ilość dostępnej pamięci w maszynie wirtualnej najmniej 128 MB, mogą być problemy na mniejsze rozmiary maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-355">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="eab64-356">Po zakończeniu edycji `/etc/default/grub`, uruchom następujące polecenie, aby odbudować chodników konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="eab64-356">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="eab64-357">Dodawanie modułów funkcji Hyper-V do initramfs.</span><span class="sxs-lookup"><span data-stu-id="eab64-357">Add Hyper-V modules to initramfs.</span></span>

    <span data-ttu-id="eab64-358">Edytuj `/etc/dracut.conf`, Dodaj zawartość:</span><span class="sxs-lookup"><span data-stu-id="eab64-358">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="eab64-359">Odbuduj initramfs:</span><span class="sxs-lookup"><span data-stu-id="eab64-359">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="eab64-360">Upewnij się, że serwer SSH jest zainstalowany i skonfigurowany do uruchamiania w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="eab64-360">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="eab64-361">To ustawienie jest zazwyczaj domyślnie.</span><span class="sxs-lookup"><span data-stu-id="eab64-361">This setting is usually the default.</span></span> <span data-ttu-id="eab64-362">Modyfikowanie `/etc/ssh/sshd_config` ma zawierać następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="eab64-362">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="eab64-363">Pakiet WALinuxAgent `WALinuxAgent-<version>`, ma zostać przypisany do repozytorium dodatki Red Hat.</span><span class="sxs-lookup"><span data-stu-id="eab64-363">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="eab64-364">Włącz repozytorium dodatki, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-364">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="eab64-365">Zainstaluj agenta systemu Linux platformy Azure, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-365">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="eab64-366">Nie należy tworzyć zamiany miejsca na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="eab64-366">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="eab64-367">Agent systemu Linux platformy Azure może automatycznie skonfigurować obszar wymiany przy użyciu dysku zasób lokalny, który jest dołączony do maszyny wirtualnej po udostępnieniu maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-367">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="eab64-368">Zauważ, że dysk lokalny zasób jest tymczasowego, i może opróżnić, gdy maszyna wirtualna jest anulowana.</span><span class="sxs-lookup"><span data-stu-id="eab64-368">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="eab64-369">Po zainstalowaniu agenta systemu Linux platformy Azure w poprzednim kroku, należy zmodyfikować następujące parametry w `/etc/waagent.conf` odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="eab64-369">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

12. <span data-ttu-id="eab64-370">Jeśli chcesz wyrejestrować subskrypcji, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="eab64-370">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="eab64-371">Uruchom następujące polecenia, aby anulowanie zastrzeżenia maszyny wirtualnej i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="eab64-371">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="eab64-372">Zamknij maszynę wirtualną i konwertowania pliku VMDK do formatu wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="eab64-372">Shut down the virtual machine, and convert the VMDK file to the VHD format.</span></span>

    <span data-ttu-id="eab64-373">Najpierw Konwertuj obraz na raw format:</span><span class="sxs-lookup"><span data-stu-id="eab64-373">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="eab64-374">Upewnij się, że rozmiar obrazu raw jest zgodne z 1 MB.</span><span class="sxs-lookup"><span data-stu-id="eab64-374">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="eab64-375">W przeciwnym razie zaokrąglij w górę rozmiar, aby były wyrównane z 1 MB:</span><span class="sxs-lookup"><span data-stu-id="eab64-375">Otherwise, round up the size to align with 1 MB:</span></span>

        # MB=$((1024*1024))
        # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \
          gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

        # rounded_size=$((($size/$MB + 1)*$MB))
        # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="eab64-376">Konwertuj raw dysku na dysk VHD o stałym rozmiarze:</span><span class="sxs-lookup"><span data-stu-id="eab64-376">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="eab64-377">Przygotowywanie maszyny wirtualnej z systemem Red Hat z obrazu ISO za pomocą pliku kickstart automatycznie</span><span class="sxs-lookup"><span data-stu-id="eab64-377">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="eab64-378">Przygotowanie RHEL 7 maszyny wirtualnej z pliku kickstart</span><span class="sxs-lookup"><span data-stu-id="eab64-378">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="eab64-379">Utwórz plik kickstart, który zawiera następującą zawartość, a następnie zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="eab64-379">Create a kickstart file that includes the following content, and save the file.</span></span> <span data-ttu-id="eab64-380">Aby uzyskać szczegółowe informacje o instalacji kickstart, zobacz [Przewodnik instalacji Kickstart](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="eab64-380">For details about kickstart installation, see the [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run the Setup Agent on first boot
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

        # Clear the MBR
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

        # Power down the machine after install
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

        # Disable the root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set the cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build the grub cfg
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

2. <span data-ttu-id="eab64-381">Umieść plik kickstart, gdy system instalacji do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="eab64-381">Place the kickstart file where the installation system can access it.</span></span>

3. <span data-ttu-id="eab64-382">W Menedżerze funkcji Hyper-V Utwórz nową maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="eab64-382">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="eab64-383">Na **Podłączanie wirtualnego dysku twardego** wybierz pozycję **Dołącz wirtualny dysk twardy później**i ukończenie Kreatora nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-383">On the **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete the New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="eab64-384">Otwórz ustawienia maszyny wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="eab64-384">Open the virtual machine settings:</span></span>

    <span data-ttu-id="eab64-385">a.</span><span class="sxs-lookup"><span data-stu-id="eab64-385">a.</span></span>  <span data-ttu-id="eab64-386">Dołącz nowy wirtualny dysk twardy do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eab64-386">Attach a new virtual hard disk to the virtual machine.</span></span> <span data-ttu-id="eab64-387">Upewnij się wybrać **formatu wirtualnego dysku twardego** i **o stałym rozmiarze**.</span><span class="sxs-lookup"><span data-stu-id="eab64-387">Make sure to select **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="eab64-388">b.</span><span class="sxs-lookup"><span data-stu-id="eab64-388">b.</span></span>  <span data-ttu-id="eab64-389">Dołącz instalacji ISO na dysk DVD.</span><span class="sxs-lookup"><span data-stu-id="eab64-389">Attach the installation ISO to the DVD drive.</span></span>

    <span data-ttu-id="eab64-390">c.</span><span class="sxs-lookup"><span data-stu-id="eab64-390">c.</span></span>  <span data-ttu-id="eab64-391">Ustaw systemu BIOS z dysku CD.</span><span class="sxs-lookup"><span data-stu-id="eab64-391">Set the BIOS to boot from CD.</span></span>

5. <span data-ttu-id="eab64-392">Uruchamia maszynę wirtualną.</span><span class="sxs-lookup"><span data-stu-id="eab64-392">Start the virtual machine.</span></span> <span data-ttu-id="eab64-393">Gdy pojawi się w podręczniku instalacji, naciśnij klawisz **kartę** do konfigurowania opcji rozruchu.</span><span class="sxs-lookup"><span data-stu-id="eab64-393">When the installation guide appears, press **Tab** to configure the boot options.</span></span>

6. <span data-ttu-id="eab64-394">Wprowadź `inst.ks=<the location of the kickstart file>` na końcu opcje rozruchu, a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="eab64-394">Enter `inst.ks=<the location of the kickstart file>` at the end of the boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="eab64-395">Poczekaj na zakończenie instalacji.</span><span class="sxs-lookup"><span data-stu-id="eab64-395">Wait for the installation to finish.</span></span> <span data-ttu-id="eab64-396">Po zakończeniu, maszyna wirtualna zostanie zamknięta automatycznie.</span><span class="sxs-lookup"><span data-stu-id="eab64-396">When it's finished, the virtual machine will be shut down automatically.</span></span> <span data-ttu-id="eab64-397">Dysk VHD systemu Linux jest teraz gotowy do przekazania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-397">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="eab64-398">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="eab64-398">Known issues</span></span>
### <a name="the-hyper-v-driver-could-not-be-included-in-the-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="eab64-399">Sterownik funkcji Hyper-V nie może znajdować się w początkowej dysku RAM, korzystając z funkcji hypervisor z systemem innym niż do funkcji Hyper-V</span><span class="sxs-lookup"><span data-stu-id="eab64-399">The Hyper-V driver could not be included in the initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="eab64-400">W niektórych przypadkach instalatorów systemu Linux może nie zawierać sterowników dla funkcji Hyper-V w początkowej dysku RAM (initrd lub initramfs), chyba że Linux wykryje, że jest on uruchomiony w środowisku funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="eab64-400">In some cases, Linux installers might not include the drivers for Hyper-V in the initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="eab64-401">Podczas korzystania z różnych wirtualizacji systemu (czyli Virtualbox, Xen itp.), aby przygotować obraz systemu Linux, może być konieczne odbudowanie initrd w celu zapewnienia, że co najmniej modułów jądra hv_vmbus i hv_storvsc są dostępne w początkowej dysku RAM.</span><span class="sxs-lookup"><span data-stu-id="eab64-401">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) to prepare your Linux image, you might need to rebuild initrd to ensure that at least the hv_vmbus and hv_storvsc kernel modules are available on the initial RAM disk.</span></span> <span data-ttu-id="eab64-402">To znany problem z co najmniej w systemach, które są oparte na nadrzędnego dystrybucji Red Hat.</span><span class="sxs-lookup"><span data-stu-id="eab64-402">This is a known issue at least on systems that are based on the upstream Red Hat distribution.</span></span>

<span data-ttu-id="eab64-403">Aby rozwiązać ten problem, Dodaj modułów funkcji Hyper-V do initramfs i odbuduj go:</span><span class="sxs-lookup"><span data-stu-id="eab64-403">To resolve this issue, add Hyper-V modules to initramfs and rebuild it:</span></span>

<span data-ttu-id="eab64-404">Edytuj `/etc/dracut.conf`i dodaj następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="eab64-404">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="eab64-405">Odbuduj initramfs:</span><span class="sxs-lookup"><span data-stu-id="eab64-405">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="eab64-406">Aby uzyskać więcej informacji, zapoznaj się z informacjami [odbudowywania initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="eab64-406">For more details, see the information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eab64-407">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eab64-407">Next steps</span></span>
<span data-ttu-id="eab64-408">Teraz możesz używać wirtualnego dysku twardego Red Hat Enterprise Linux do tworzenia nowych maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eab64-408">You're now ready to use your Red Hat Enterprise Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="eab64-409">Jeśli jest to czy jest przekazywanie pliku VHD na platformę Azure po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eab64-409">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="eab64-410">Aby uzyskać więcej informacji o funkcjach hypervisor, które są certyfikowane do uruchamiania Red Hat Enterprise Linux, zobacz [Red Hat witryny sieci Web](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="eab64-410">For more details about the hypervisors that are certified to run Red Hat Enterprise Linux, see [the Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
