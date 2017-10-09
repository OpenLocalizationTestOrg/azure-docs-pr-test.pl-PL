---
title: aaaCreate i przekazywanie SUSE Linux wirtualnego dysku twardego na platformie Azure
description: "Dowiedz się toocreate i przekaż Azure wirtualnego dysku twardego (VHD) z systemem operacyjnym SUSE Linux."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: 9185c7e67279357f00db0f43e944e96c58f0dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="b9bb5-103">Przygotowywanie maszyny wirtualnej systemu SLES lub openSUSE dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b9bb5-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="b9bb5-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b9bb5-104">Prerequisites</span></span>
<span data-ttu-id="b9bb5-105">W tym artykule przyjęto założenie, że zainstalowano już SUSE lub openSUSE Linux tooa wirtualnego dysku twardego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system tooa virtual hard disk.</span></span> <span data-ttu-id="b9bb5-106">Wiele narzędzi istnieje toocreate plików VHD, na przykład rozwiązanie wirtualizacji takich jak funkcja Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-106">Multiple tools exist toocreate .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="b9bb5-107">Aby uzyskać instrukcje, zobacz [instalowanie hello roli funkcji Hyper-V i konfigurowanie maszyny wirtualnej](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9bb5-107">For instructions, see [Install hello Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="b9bb5-108">SLES / openSUSE instalacji uwagi</span><span class="sxs-lookup"><span data-stu-id="b9bb5-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="b9bb5-109">Zobacz także [ogólne informacje o instalacji systemu Linux](create-upload-generic.md#general-linux-installation-notes) więcej porad na przygotowanie systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="b9bb5-110">Witaj VHDX format nie jest obsługiwany na platformie Azure, tylko **stały VHD**.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-110">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="b9bb5-111">Możesz przekonwertować format tooVHD dysku hello za pomocą Menedżera funkcji Hyper-V lub hello polecenia cmdlet convert-vhd.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-111">You can convert hello disk tooVHD format using Hyper-V Manager or hello convert-vhd cmdlet.</span></span>
* <span data-ttu-id="b9bb5-112">Podczas instalowania systemu Linux hello zaleca się użycie standardowe partycje, a nie LVM (często hello domyślnie wiele instalacji).</span><span class="sxs-lookup"><span data-stu-id="b9bb5-112">When installing hello Linux system it is recommended that you use standard partitions rather than LVM (often hello default for many installations).</span></span> <span data-ttu-id="b9bb5-113">Pozwoli to uniknąć konfliktów nazw LVM sklonowany maszyn wirtualnych, zwłaszcza w przypadku, gdy na dysku systemu operacyjnego kiedykolwiek wymaga tooanother toobe dołączony maszyny Wirtualnej do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs toobe attached tooanother VM for troubleshooting.</span></span> <span data-ttu-id="b9bb5-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) może być używany dla dysków z danymi, jeśli preferowane.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="b9bb5-115">Nie należy konfigurować partycji wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-115">Do not configure a swap partition on hello OS disk.</span></span> <span data-ttu-id="b9bb5-116">agenta systemu Linux Hello może być skonfigurowany toocreate pliku wymiany na powitania zasobów dysku.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-116">hello Linux agent can be configured toocreate a swap file on hello temporary resource disk.</span></span>  <span data-ttu-id="b9bb5-117">Więcej informacji na ten temat można znaleźć w poniższych krokach hello.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-117">More information about this can be found in hello steps below.</span></span>
* <span data-ttu-id="b9bb5-118">Wszystkie wirtualne dyski twarde hello muszą mieć rozmiary, które są wielokrotności 1 MB.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-118">All of hello VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="b9bb5-119">Użyj SUSE Studio</span><span class="sxs-lookup"><span data-stu-id="b9bb5-119">Use SUSE Studio</span></span>
<span data-ttu-id="b9bb5-120">[SUSE Studio](http://www.susestudio.com) można łatwo tworzyć i zarządzać obrazów SLES i openSUSE platformy Azure i funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="b9bb5-121">Jest to zalecane podejście do dostosowywania własnych obrazów SLES i openSUSE hello.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-121">This is hello recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="b9bb5-122">Jako alternatywne toobuilding własne wirtualnego dysku twardego, SUSE publikuje również obrazów BYOS (Bring Your własnej subskrypcji) dla SLES na [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="b9bb5-122">As an alternative toobuilding your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="b9bb5-123">Przygotowanie SUSE Linux Enterprise Server 11 z dodatkiem SP4</span><span class="sxs-lookup"><span data-stu-id="b9bb5-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="b9bb5-124">W środkowym okienku hello Menedżera funkcji Hyper-V wybierz maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-124">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="b9bb5-125">Kliknij przycisk **Connect** okna hello tooopen hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-125">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="b9bb5-126">Zarejestruj użytkownika tooallow systemu SUSE Linux Enterprise go toodownload aktualizacje i pakiety instalacyjne.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-126">Register your SUSE Linux Enterprise system tooallow it toodownload updates and install packages.</span></span>
4. <span data-ttu-id="b9bb5-127">Zaktualizuj hello system o najnowszych poprawek hello:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-127">Update hello system with hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="b9bb5-128">Zainstaluj hello agenta systemu Linux platformy Azure z repozytorium SLES hello:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-128">Install hello Azure Linux Agent from hello SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="b9bb5-129">Sprawdź, czy agenta waagent ustawiono zbyt "on" w chkconfig, a jeśli nie, ją włączyć automatyczne uruchamianie:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-129">Check if waagent is set too"on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="b9bb5-130">Sprawdź, czy Usługa agenta waagent jest uruchomiona i jeśli nie, uruchom go:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="b9bb5-131">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-131">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="b9bb5-132">toodo tym Otwórz "/ boot/grub/menu.lst" w edytorze tekstów i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-132">toodo this open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="b9bb5-133">Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-133">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="b9bb5-134">Upewnij się, że fstab /boot/grub/menu.lst i/etc/obu dysku hello odwołanie za pomocą jego identyfikatora UUID (przez uuid) zamiast hello identyfikator dysku (według identyfikatora).</span><span class="sxs-lookup"><span data-stu-id="b9bb5-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference hello disk using its UUID (by-uuid) instead of hello disk ID (by-id).</span></span> 
   
    <span data-ttu-id="b9bb5-135">Pobierz identyfikator UUID</span><span class="sxs-lookup"><span data-stu-id="b9bb5-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="b9bb5-136">Jeśli /dev/disk/by-id / jest używany, aktualizacji zarówno /boot/grub/menu.lst i/etc/fstab przy użyciu wartości odpowiednich przez uuid hello</span><span class="sxs-lookup"><span data-stu-id="b9bb5-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with hello proper by-uuid value</span></span>
   
    <span data-ttu-id="b9bb5-137">Przed zmianą</span><span class="sxs-lookup"><span data-stu-id="b9bb5-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="b9bb5-138">Po zmianie</span><span class="sxs-lookup"><span data-stu-id="b9bb5-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="b9bb5-139">Zmodyfikuj udev tooavoid zasady generowania statycznych zasady hello interfejsów Ethernet.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-139">Modify udev rules tooavoid generating static rules for hello Ethernet interface(s).</span></span> <span data-ttu-id="b9bb5-140">Te reguły może spowodować problemy podczas klonowania maszyny wirtualnej w Microsoft Azure lub funkcji Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="b9bb5-141">Zalecane jest plik hello tooedit "/ etc/sysconfig/sieci/dhcp" i zmień hello `DHCLIENT_SET_HOSTNAME` parametr toohello po:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-141">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
    
     <span data-ttu-id="b9bb5-142">DHCLIENT_SET_HOSTNAME = "nie"</span><span class="sxs-lookup"><span data-stu-id="b9bb5-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="b9bb5-143">Komentarz "/ etc/sudoers", lub hello następujące wiersze, jeśli istnieją one usunąć:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-143">In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
    
     <span data-ttu-id="b9bb5-144">Ustawienia domyślne targetpw # poprosić o hello hasło użytkownika docelowego hello tj. główny wszystkich ALL=(ALL) wszystkie # ostrzeżenie!</span><span class="sxs-lookup"><span data-stu-id="b9bb5-144">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="b9bb5-145">Użyj tylko wtedy, wraz z 'Targetpw wartości domyślnych'!</span><span class="sxs-lookup"><span data-stu-id="b9bb5-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="b9bb5-146">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-146">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="b9bb5-147">Zazwyczaj jest to domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-147">This is usually hello default.</span></span>
14. <span data-ttu-id="b9bb5-148">Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-148">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="b9bb5-149">Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-149">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="b9bb5-150">Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-150">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="b9bb5-151">Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok) i zmodyfikuj odpowiednio następujące parametry w /etc/waagent.conf hello:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-151">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="b9bb5-152">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Uwaga: Ustaw ten toowhatever muszą toobe.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
15. <span data-ttu-id="b9bb5-153">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-153">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="b9bb5-154">sudo agenta waagent-force - deprovision</span><span class="sxs-lookup"><span data-stu-id="b9bb5-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="b9bb5-155">Eksportuj HISTSIZE = 0</span><span class="sxs-lookup"><span data-stu-id="b9bb5-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="b9bb5-156">Wyloguj</span><span class="sxs-lookup"><span data-stu-id="b9bb5-156">logout</span></span>
16. <span data-ttu-id="b9bb5-157">Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="b9bb5-158">Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-158">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="b9bb5-159">Przygotowanie openSUSE 13.1 +</span><span class="sxs-lookup"><span data-stu-id="b9bb5-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="b9bb5-160">W środkowym okienku hello Menedżera funkcji Hyper-V wybierz maszynę wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-160">In hello center pane of Hyper-V Manager, select hello virtual machine.</span></span>
2. <span data-ttu-id="b9bb5-161">Kliknij przycisk **Connect** okna hello tooopen hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-161">Click **Connect** tooopen hello window for hello virtual machine.</span></span>
3. <span data-ttu-id="b9bb5-162">Na powitania powłoki, uruchom polecenie hello "`zypper lr`".</span><span class="sxs-lookup"><span data-stu-id="b9bb5-162">On hello shell, run hello command '`zypper lr`'.</span></span> <span data-ttu-id="b9bb5-163">Jeśli to polecenie zwraca dane wyjściowe podobne toohello po, a następnie repozytoria hello są skonfigurowane zgodnie z oczekiwaniami — bez korekt są niezbędne (należy pamiętać, że mogą być różne numery wersji):</span><span class="sxs-lookup"><span data-stu-id="b9bb5-163">If this command returns output similar toohello following, then hello repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="b9bb5-164">Jeśli polecenie hello zwraca "Nie zdefiniowano... repozytoria" Użyj hello następujące polecenia tooadd te repozytoriów:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-164">If hello command returns "No repositories defined..." then use hello following commands tooadd these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="b9bb5-165">Następnie należy sprawdzić repozytoria hello zostały dodane, uruchamiając polecenie hello "`zypper lr`" ponownie.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-165">You can then verify hello repositories have been added by running hello command '`zypper lr`' again.</span></span> <span data-ttu-id="b9bb5-166">W przypadku, gdy jeden hello repozytoriów odpowiednich aktualizacji nie jest włączona, należy je włączyć, wprowadzając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-166">In case one of hello relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="b9bb5-167">Aktualizacja hello jądra toohello najnowszej dostępnej wersji:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-167">Update hello kernel toohello latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="b9bb5-168">Lub tooupdate hello systemowi wszystkich najnowszych poprawek hello:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-168">Or tooupdate hello system with all hello latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="b9bb5-169">Zainstaluj hello agenta systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-169">Install hello Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="b9bb5-170">Zainstaluj zypper sudo WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="b9bb5-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="b9bb5-171">Zmodyfikuj hello jądra rozruchu liniowego chodników konfiguracji tooinclude jądra dodatkowe parametry dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-171">Modify hello kernel boot line in your grub configuration tooinclude additional kernel parameters for Azure.</span></span> <span data-ttu-id="b9bb5-172">toodo, Otwórz "/ boot/grub/menu.lst" w edytorze tekstów i upewnij się, że hello domyślnego jądra obejmuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-172">toodo this, open "/boot/grub/menu.lst" in a text editor and ensure that hello default kernel includes hello following parameters:</span></span>
   
     <span data-ttu-id="b9bb5-173">Konsola = ttyS0 earlyprintk = ttyS0 rootdelay = 300</span><span class="sxs-lookup"><span data-stu-id="b9bb5-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="b9bb5-174">Dzięki konsoli komunikaty są wysyłane toohello pierwszego portu szeregowego, które mogą ułatwić Azure pomocy dotyczącej debugowanie problemów.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-174">This will ensure all console messages are sent toohello first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="b9bb5-175">Ponadto należy usunąć hello poniższych parametrów z hello jądra rozruchu wiersza, jeśli istnieją:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-175">In addition, remove hello following parameters from hello kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="b9bb5-176">Rezerwacja libata.atapi_enabled=0 = 0x1f0, 0x8</span><span class="sxs-lookup"><span data-stu-id="b9bb5-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="b9bb5-177">Zalecane jest plik hello tooedit "/ etc/sysconfig/sieci/dhcp" i zmień hello `DHCLIENT_SET_HOSTNAME` parametr toohello po:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-177">It is recommended tooedit hello file "/etc/sysconfig/network/dhcp" and change hello `DHCLIENT_SET_HOSTNAME` parameter toohello following:</span></span>
   
     <span data-ttu-id="b9bb5-178">DHCLIENT_SET_HOSTNAME = "nie"</span><span class="sxs-lookup"><span data-stu-id="b9bb5-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="b9bb5-179">**Ważne:** w "/ etc/sudoers", komentarz lub usunąć hello następujące wiersze, jeśli istnieją:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-179">**Important:** In "/etc/sudoers", comment out or remove hello following lines if they exist:</span></span>
   
     <span data-ttu-id="b9bb5-180">Ustawienia domyślne targetpw # poprosić o hello hasło użytkownika docelowego hello tj. główny wszystkich ALL=(ALL) wszystkie # ostrzeżenie!</span><span class="sxs-lookup"><span data-stu-id="b9bb5-180">Defaults targetpw   # ask for hello password of hello target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="b9bb5-181">Użyj tylko wtedy, wraz z 'Targetpw wartości domyślnych'!</span><span class="sxs-lookup"><span data-stu-id="b9bb5-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="b9bb5-182">Upewnij się, ten serwer SSH hello jest zainstalowany i skonfigurowany toostart w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-182">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span>  <span data-ttu-id="b9bb5-183">Zazwyczaj jest to domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-183">This is usually hello default.</span></span>
10. <span data-ttu-id="b9bb5-184">Nie należy tworzyć obszar wymiany na powitania dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-184">Do not create swap space on hello OS disk.</span></span>
    
    <span data-ttu-id="b9bb5-185">Witaj agenta systemu Linux platformy Azure mogą automatycznie konfigurować obszar wymiany przy użyciu hello zasób lokalny dysk, który jest dołączony toohello maszyny Wirtualnej po zainicjowaniu obsługi administracyjnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-185">hello Azure Linux Agent can automatically configure swap space using hello local resource disk that is attached toohello VM after provisioning on Azure.</span></span> <span data-ttu-id="b9bb5-186">Ten dysk zasobu lokalnego hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-186">Note that hello local resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span> <span data-ttu-id="b9bb5-187">Po zainstalowaniu hello Azure agenta systemu Linux (zobacz poprzedni krok) i zmodyfikuj odpowiednio następujące parametry w /etc/waagent.conf hello:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-187">After installing hello Azure Linux Agent (see previous step), modify hello following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="b9bb5-188">ResourceDisk.Format=y ResourceDisk.Filesystem=ext4 ResourceDisk.MountPoint=/mnt/resource ResourceDisk.EnableSwap=y ResourceDisk.SwapSizeMB=&#2048;# Uwaga: Ustaw ten toowhatever muszą toobe.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this toowhatever you need it toobe.</span></span>
11. <span data-ttu-id="b9bb5-189">Uruchom hello następującej maszyny wirtualnej hello toodeprovision poleceń i przygotowywania ich do inicjowania obsługi administracyjnej na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-189">Run hello following commands toodeprovision hello virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="b9bb5-190">sudo agenta waagent-force - deprovision</span><span class="sxs-lookup"><span data-stu-id="b9bb5-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="b9bb5-191">Eksportuj HISTSIZE = 0</span><span class="sxs-lookup"><span data-stu-id="b9bb5-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="b9bb5-192">Wyloguj</span><span class="sxs-lookup"><span data-stu-id="b9bb5-192">logout</span></span>
12. <span data-ttu-id="b9bb5-193">Upewnij się, powitalne agenta systemu Linux platformy Azure jest uruchamiany podczas uruchamiania:</span><span class="sxs-lookup"><span data-stu-id="b9bb5-193">Ensure hello Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="b9bb5-194">Kliknij przycisk **akcji -> zamykania w dół** w Menedżerze funkcji Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="b9bb5-195">Dysk VHD systemu Linux jest teraz gotowy toobe przekazać tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-195">Your Linux VHD is now ready toobe uploaded tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9bb5-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b9bb5-196">Next steps</span></span>
<span data-ttu-id="b9bb5-197">Użytkownik jest teraz gotowy toouse SUSE Linux wirtualnego dysku twardego toocreate nowych maszyn wirtualnych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bb5-197">You're now ready toouse your SUSE Linux virtual hard disk toocreate new virtual machines in Azure.</span></span> <span data-ttu-id="b9bb5-198">Jeśli hello jest przesyłana tooAzure pliku VHD powitania po raz pierwszy, zobacz kroki 2 i 3 w [tworzenie i przekazywanie wirtualnego dysku twardego, który zawiera system operacyjny Linux hello](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b9bb5-198">If this is hello first time that you're uploading hello .vhd file tooAzure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains hello Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

