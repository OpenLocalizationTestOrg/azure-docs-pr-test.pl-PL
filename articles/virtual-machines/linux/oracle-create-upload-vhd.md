---
title: aaaCreate i przekazywanie wirtualnego dysku twardego Oracle Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się toocreate i przekaż Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym Oracle Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: be9cf284d7f5e7122a106506a343e53e9f1ac56e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="2cefb-103">Przygotowywanie maszyny wirtualnej systemu Linux w środowisku Oracle dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2cefb-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="2cefb-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2cefb-104">Prerequisites</span></span>
<span data-ttu-id="2cefb-105">W tym artykule przyjęto założenie, zainstalowano wirtualnego dysku twardego Oracle Linux systemu operacyjnego tooa.</span><span class="sxs-lookup"><span data-stu-id="2cefb-105">This article assumes that you have already installed an Oracle Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="2cefb-106">Wiele narzędzi istnieje toocreate plików VHD, na przykład rozwiązanie wirtualizacji takich jak funkcja Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="2cefb-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="2cefb-107">Aby uzyskać instrukcje, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cefb-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="2cefb-108">Oracle Linux instalacji uwagi</span><span class="sxs-lookup"><span data-stu-id="2cefb-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="2cefb-109">Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2cefb-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="2cefb-110">Zgodne jądra Red Hat programu Oracle i ich UEK3 (podzielenie Enterprise jądra) w funkcji Hyper-V i platformy Azure są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="2cefb-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="2cefb-111">Aby uzyskać najlepsze rezultaty należy się tooupdate toohello najnowsze jądra podczas przygotowywania Oracle Linux dysk VHD.</span><span class="sxs-lookup"><span data-stu-id="2cefb-111">For best results, please be sure tooupdate toohello latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="2cefb-112">UEK2 programu Oracle nie jest obsługiwana w funkcji Hyper-V i Azure, ponieważ nie ma hello wymagane sterowniki.</span><span class="sxs-lookup"><span data-stu-id="2cefb-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include hello required drivers.</span></span>
* <span data-ttu-id="2cefb-113">Witaj VHDX format nie jest obsługiwany na platformie Azure, tylko **stały VHD**.</span><span class="sxs-lookup"><span data-stu-id="2cefb-113">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="2cefb-114">Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello polecenia cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="2cefb-114">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="2cefb-115">Podczas instalowania systemu Linux hello zaleca się użycie standardowe partycje, a nie LVM (często hello domyślnie wiele instalacji).</span><span class="sxs-lookup"><span data-stu-id="2cefb-115">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="2cefb-116">Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, zwłaszcza w przypadku, gdy na dysku systemu operacyjnego kiedykolwiek wymaga tooanother toobe dołączony maszyny Wirtualnej do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="2cefb-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="2cefb-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi, jeśli preferowane.</span><span class="sxs-lookup"><span data-stu-id="2cefb-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="2cefb-118">NUMA nie jest obsługiwana dla większych rozmiarów maszyn wirtualnych ze względu na błąd tooa w wersji jądra systemu Linux poniżej 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="2cefb-118">NUMA is not supported for larger VM sizes due tooa bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="2cefb-119">Ten problem, przede wszystkim na środowisko za pomocą hello nadrzędnego Red Hat 2.6.32 jądra.</span><span class="sxs-lookup"><span data-stu-id="2cefb-119">This issue primarily impacts distributions using hello upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="2cefb-120">Ręczna instalacja agenta systemu Linux Azure hello (agenta waagent) automatycznie spowoduje wyłączenie NUMA w konfiguracji CHODNIKÓW hello hello jądra systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="2cefb-120">Manual installation of hello Azure Linux agent (waagent) will automatically disable NUMA in hello GRUB configuration for hello Linux kernel.</span></span> <span data-ttu-id="2cefb-121">Więcej informacji na ten temat można znaleźć w poniższych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="2cefb-121">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="2cefb-122">Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2cefb-122">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="2cefb-123">agenta systemu Linux Hello może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.</span><span class="sxs-lookup"><span data-stu-id="2cefb-123">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="2cefb-124">Więcej informacji na ten temat można znaleźć w poniższych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="2cefb-124">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="2cefb-125">Wszystkie wirtualne dyski twarde hello muszą mieć rozmiary, które są wielokrotności 1 MB.</span><span class="sxs-lookup"><span data-stu-id="2cefb-125">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="2cefb-126">Upewnij się, że hello `Addons` repozytorium jest włączona.</span><span class="sxs-lookup"><span data-stu-id="2cefb-126">Make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="2cefb-127">Edytuj plik hello `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) lub `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux) i zmień wiersz hello `enabled=0` za`enabled=1` w obszarze **[ol6_addons]** lub **[ol7_addons]** w tym plik.</span><span class="sxs-lookup"><span data-stu-id="2cefb-127">Edit hello file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="2cefb-128">Oracle Linux 6.4 +</span><span class="sxs-lookup"><span data-stu-id="2cefb-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="2cefb-129">Należy wykonać kroki konfiguracji określone w systemie operacyjnym hello na powitania toorun maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2cefb-129">You must complete specific configuration steps in hello operating system for hello virtual machine toorun in Azure.</span></span>

1. <span data-ttu-id="2cefb-130">W środkowym okienku hello Menedżera funkcji Hyper-V wybierz maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="2cefb-130">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="2cefb-131">Kliknij przycisk **Connect** okna hello tooopen hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2cefb-131">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="2cefb-132">Odinstaluj NetworkManager, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2cefb-132">Uninstall NetworkManager by running hello following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="2cefb-133">**Uwaga:** Jeśli hello pakiet nie jest już zainstalowany, to polecenie zakończy się niepowodzeniem z komunikatem o błędzie.</span><span class="sxs-lookup"><span data-stu-id="2cefb-133">**Note:** If hello package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="2cefb-134">Taki stan jest oczekiwany.</span><span class="sxs-lookup"><span data-stu-id="2cefb-134">This is expected.</span></span>
4. <span data-ttu-id="2cefb-135">Utwórz plik o nazwie **sieci** w hello `/etc/sysconfig/` katalog, który zawiera hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="2cefb-135">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="2cefb-136">Utwórz plik o nazwie **ifcfg eth0** w hello `/etc/sysconfig/network-scripts/` katalog, który zawiera hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="2cefb-136">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="2cefb-137">Zmodyfikuj udev tooavoid zasady generowania statycznych zasady hello interfejsów Ethernet.</span><span class="sxs-lookup"><span data-stu-id="2cefb-137">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="2cefb-138">Te reguły może spowodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="2cefb-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="2cefb-139">Upewnij się, że Usługa sieciowa hello rozpocznie się podczas rozruchu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2cefb-139">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="2cefb-140">Zainstaluj python pyasn1, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2cefb-140">Install python-pyasn1 by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="2cefb-141">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2cefb-141">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="2cefb-142">toodo tym Otwórz "/ boot/grub/menu.lst" w edytorze tekstów i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="2cefb-142">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="2cefb-143">Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="2cefb-143">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="2cefb-144">Spowoduje to wyłączenie NUMA powodu usterki tooa jądra zgodne Red Hat programu Oracle.</span><span class="sxs-lookup"><span data-stu-id="2cefb-144">This will disable NUMA due tooa bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="2cefb-145">Oprócz powyższych toohello, zalecane jest zbyt*Usuń* hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="2cefb-145">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="2cefb-146">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="2cefb-146">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="2cefb-147">Witaj `crashkernel` opcja może być skonfigurowany w razie potrzeby po lewej, ale należy pamiętać, że ten parametr zmniejszy hello ilość dostępnej pamięci w hello wirtualna najmniej 128 MB, które mogą być problemy na powitania mniejsze rozmiary maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2cefb-147">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="2cefb-148">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="2cefb-148">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="2cefb-149">Zazwyczaj jest to domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="2cefb-149">This is usually hello default.</span></span>
11. <span data-ttu-id="2cefb-150">Zainstaluj hello agenta systemu Linux platformy Azure, uruchamiając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="2cefb-150">Install hello Azure Linux Agent by running hello following command.</span></span> <span data-ttu-id="2cefb-151">Najnowsza wersja Hello jest 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="2cefb-151">hello latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="2cefb-152">Warto zauważyć, że instalowanie pakietu WALinuxAgent hello spowoduje usunięcie hello NetworkManager pakiety NetworkManager gnome jeśli ich nie zostały już usunięte zgodnie z opisem w kroku 2.</span><span class="sxs-lookup"><span data-stu-id="2cefb-152">Note that installing hello WALinuxAgent package will remove hello NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="2cefb-153">Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2cefb-153">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="2cefb-154">Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2cefb-154">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="2cefb-155">Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2cefb-155">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="2cefb-156">Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok) i zmodyfikuj odpowiednio następujące parametry w /etc/waagent.conf hello:</span><span class="sxs-lookup"><span data-stu-id="2cefb-156">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
13. <span data-ttu-id="2cefb-157">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="2cefb-157">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="2cefb-158">Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="2cefb-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="2cefb-159">Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2cefb-159">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="2cefb-160">Oracle Linux 7.0 +</span><span class="sxs-lookup"><span data-stu-id="2cefb-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="2cefb-161">**Zmiany w Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="2cefb-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="2cefb-162">Przygotowywanie maszyny wirtualnej Oracle Linux 7 dla platformy Azure jest bardzo podobne tooOracle Linux 6, jednak istnieje kilka istotnych różnic, warto zauważyć:</span><span class="sxs-lookup"><span data-stu-id="2cefb-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar tooOracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="2cefb-163">Zarówno hello Red Hat zgodne jądra, jak i programu Oracle UEK3 są obsługiwane na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2cefb-163">Both hello Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="2cefb-164">Witaj UEK3 jądra jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="2cefb-164">hello UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="2cefb-165">Witaj NetworkManager już pakiet powoduje konflikt z agenta systemu Linux Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2cefb-165">hello NetworkManager package no longer conflicts with hello Azure Linux agent.</span></span> <span data-ttu-id="2cefb-166">Ten pakiet jest instalowany domyślnie i zaleca się, że nie zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="2cefb-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="2cefb-167">GRUB2 teraz jest używany jako hello inicjującego domyślne, więc hello procedury do edycji parametry jądra został zmieniony (patrz poniżej).</span><span class="sxs-lookup"><span data-stu-id="2cefb-167">GRUB2 is now used as hello default bootloader, so hello procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="2cefb-168">XFS jest teraz hello domyślnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="2cefb-168">XFS is now hello default file system.</span></span> <span data-ttu-id="2cefb-169">nadal można użyć systemu plików ext4 Hello, w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="2cefb-169">hello ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="2cefb-170">**Kroki konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="2cefb-170">**Configuration steps**</span></span>

1. <span data-ttu-id="2cefb-171">W Menedżerze funkcji Hyper-V wybierz hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2cefb-171">In Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="2cefb-172">Kliknij przycisk **Connect** tooopen okna konsoli hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2cefb-172">Click **Connect** tooopen a console window for hello virtual machine.</span></span>
3. <span data-ttu-id="2cefb-173">Utwórz plik o nazwie **sieci** w hello `/etc/sysconfig/` katalog, który zawiera hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="2cefb-173">Create a file named **network** in hello `/etc/sysconfig/` directory that contains hello following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="2cefb-174">Utwórz plik o nazwie **ifcfg eth0** w hello `/etc/sysconfig/network-scripts/` katalog, który zawiera hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="2cefb-174">Create a file named **ifcfg-eth0** in hello `/etc/sysconfig/network-scripts/` directory that contains hello following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="2cefb-175">Zmodyfikuj udev tooavoid zasady generowania statycznych zasady hello interfejsów Ethernet.</span><span class="sxs-lookup"><span data-stu-id="2cefb-175">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="2cefb-176">Te reguły może spowodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="2cefb-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="2cefb-177">Upewnij się, że Usługa sieciowa hello rozpocznie się podczas rozruchu, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2cefb-177">Ensure hello network service will start at boot time by running hello following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="2cefb-178">Zainstaluj pakiet języka python pyasn1 hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2cefb-178">Install hello python-pyasn1 package by running hello following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="2cefb-179">Uruchom następujące polecenie tooclear hello bieżących yum metadanych hello i zainstaluj wszystkie aktualizacje:</span><span class="sxs-lookup"><span data-stu-id="2cefb-179">Run hello following command tooclear hello current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="2cefb-180">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2cefb-180">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="2cefb-181">toodo tym Otwórz "/ etc/domyślne/chodników" w hello edytora i edytowanie tekstu `GRUB_CMDLINE_LINUX` parametrów, na przykład:</span><span class="sxs-lookup"><span data-stu-id="2cefb-181">toodo this open "/etc/default/grub" in a text editor and edit hello `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="2cefb-182">Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="2cefb-182">This will also ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="2cefb-183">On również wyłącza hello nowe OEL 7 konwencje nazewnictwa dla kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="2cefb-183">It also turns off hello new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="2cefb-184">Oprócz powyższych toohello, zalecane jest zbyt*Usuń* hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="2cefb-184">In addition toohello above, it is recommended too*remove* hello following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="2cefb-185">Graficznego i cichy rozruchu nie są przydatne w środowisku chmury, gdy chcemy, aby wszystkie toobe dzienniki hello wysyłane toohello portu szeregowego.</span><span class="sxs-lookup"><span data-stu-id="2cefb-185">Graphical and quiet boot are not useful in a cloud environment where we want all hello logs toobe sent toohello serial port.</span></span>
   
   <span data-ttu-id="2cefb-186">Witaj `crashkernel` opcja może być skonfigurowany w razie potrzeby po lewej, ale należy pamiętać, że ten parametr zmniejszy hello ilość dostępnej pamięci w hello wirtualna najmniej 128 MB, które mogą być problemy na powitania mniejsze rozmiary maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2cefb-186">hello `crashkernel` option may be left configured if desired, but note that this parameter will reduce hello amount of available memory in hello VM by 128MB or more, which may be problematic on hello smaller VM sizes.</span></span>
10. <span data-ttu-id="2cefb-187">Po zakończeniu edycji "/ etc/domyślne/chodników" na powyżej, uruchom hello następujące polecenia toorebuild hello chodników konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="2cefb-187">Once you are done editing "/etc/default/grub" per above, run hello following command toorebuild hello grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="2cefb-188">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="2cefb-188">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="2cefb-189">Zazwyczaj jest to domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="2cefb-189">This is usually hello default.</span></span>
12. <span data-ttu-id="2cefb-190">Zainstaluj agenta systemu Linux Azure hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2cefb-190">Install hello Azure Linux Agent by running hello following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="2cefb-191">Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2cefb-191">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="2cefb-192">Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2cefb-192">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="2cefb-193">Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2cefb-193">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="2cefb-194">Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok hello) i zmodyfikuj odpowiednio następujące parametry w /etc/waagent.conf hello:</span><span class="sxs-lookup"><span data-stu-id="2cefb-194">After installing hello Azure Linux Agent (see hello previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.
14. <span data-ttu-id="2cefb-195">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="2cefb-195">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="2cefb-196">Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="2cefb-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="2cefb-197">Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2cefb-197">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cefb-198">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2cefb-198">Next steps</span></span>
<span data-ttu-id="2cefb-199">Użytkownik jest teraz gotowy toouse Oracle Linux VHD toocreate nowych maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2cefb-199">You're now ready toouse your Oracle Linux .vhd toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="2cefb-200">Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2cefb-200">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

